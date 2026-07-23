---
layout: default
title: Context Engineering 
permalink: /context-engineering/
---

# Context Engineering
At a high level, Context is everything an LLM ingests at inference time; and Context Engineering is what that exact input looks like.

**NB. Context Engineering =/= Prompt Engineering; see below:**
<img src="/assets/pengi_vs_cengi.png" alt="Prompt Engineering vs Context Engineering" style="max-width:100%; height:auto;">
For further info ,see my [earlier article]({% post_url 2026-06-01-prompt_engineering %}) where I go deep on system prompts and provide practical examples.

More precisely, context engineering is how one designs, structures, and optimizes context input at the point of ingestion such that model understanding and reasoning are maximized, model outputs are consistently relevant and high quality, and model behavior is predictable and aligned with stated goals/use cases.

While closely related, input context and the context window (or context length) are two different concepts. The [context window](https://www.ibm.com/think/topics/context-window) is the technical limit to the model’s working memory - how many tokens it can process at once. In practice, performance noticeably degrades as this window fills up; we call this [context rot](https://www.trychroma.com/research/context-rot). 

Input context is all the tokens that the model reads up to the point of generation, per turn; that is, everything that is sent in a single request - the system prompt, conversation history, user input, any retrieved documents or tool call outputs, and other injected content. This, too, has its own peculiarities, such as the ‘lost in the middle’ phenomenon, where models tend to pay more attention to the beginning and end of input context, while information in the middle gets ‘lost’.

## The Context Stack

LLMs are powerful next-token predictors that excel at knowledge work, but they cannot read minds - they only ‘see’ and ingest tokens in their context window. Every user prompt and supporting scaffolding must thus pass through this single channel. 

It’s therefore best to think of context as a stacked, layered structure - a deliberately sequenced stack of information that the model ingests. The order, clarity, and structure of this information dramatically influences how well the model performs. 

While attention is theoretically global, decoder-only LLMs (GenAI, i.e. practically every LLM we use today) are causal - each token can attend only to itself and preceding tokens. The entire input context is therefore ‘read’ as a single left-to-right sequence. In the case of the context stack below, this is top-to-bottom. The earliest tokens, the system prompt, are the furthest from the ‘generation point’ - when the model stops reading tokens and begins generating them to output a response; while the user prompt, coming immediately before the ‘generation point’, exerts large influence on model output.

This, coupled with the ‘lost in the middle’ effect, produces a strong PRIMARY + RECENCY bias. Information placed at the very beginning of the input context (typically the system prompt) and at the very end (the user prompt) receive a disproportionately high share of attention. Consequently, both the absolute order of the context ‘stack’ and the relative distance of important information from either end of the input context are important factors to consider when engineering context.

<img src="/assets/context_stack.png" alt="The Context Stack" style="max-width:100%; height:auto;">

The context stack above is best thought of a general theoretical representation of input context design, rather than canon engineering blueprints for input context architecture. 
The system prompt defines identity, goals, and hard constraints such as safety guardrails. Naturally, all this information must be attended to reliably, i.e. the model must give it a lot of attention, so the system prompt comes first in order to exploit primacy bias. 
Tools and function definitions follow close behind, giving the model a suite of available actions through MCP servers, skills, API calls, bespoke functions, etc.
Retrieved/external content (web search results, RAG documents) and key info/summaries come next. 
Full conversation history is often truncated and summarized, i.e. compressed into smaller high-quality representations through context compression.
Current user input comes last to exploit recency bias, often accompanied by scaffolding such as delimiters, tags, format instructions, or few-shot examples to further shape output.

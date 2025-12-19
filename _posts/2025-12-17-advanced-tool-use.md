---
layout: post
title: Advanced Tool Use - Empowering LLMs to build and use their own tools
---

In this post I will demonstrate how to significantly enhance the abilities of any LLM model, as long as it is competent enough to write workng Python code and make tool calls:
[![add_tool_demo]({{ site.baseurl }}/images/add_tool_demo.jpeg)]({{ site.baseurl }}/advanced-tool-use)

***Draft/Edits in Progress - this will be removed once the post is complete***

## TL;DR
Intead of specifying a gerneral or custom toolset, start with only **add_tool**, giving the model the ability (and inclination), to write and use new tools.

## Demo Video
(Coming soon!)

## Introduction
Tool calling is what gives a Large Language Model (LLM), abilities beyond generating output text for you to read.

## Tested
I have enjoyed very positive results testing this new method with a number of different models over the last week, including:
 - [Qwen3-Coder-30B-A3B-Instruct](https://huggingface.co/Qwen/Qwen3-Coder-30B-A3B-Instruct) (bf16)
 - [Qwen3-Next-80B-A3B-Instruct](https://huggingface.co/Qwen/Qwen3-Next-80B-A3B-Instruct) (8-bit)
 - [Qwen3-Next-80B-A3B-Thinking](https://huggingface.co/Qwen/Qwen3-Next-80B-A3B-Thinking) (8-bit)
 - [Qwen3-235B-A22B-Thinking-2507](https://huggingface.co/Qwen/Qwen3-235B-A22B-Thinking-2507) (mix-3-6-bit)
 - [GLM-4.6V](https://huggingface.co/zai-org/GLM-4.6V) (8-bit)
 - [INTELLECT-3](https://huggingface.co/PrimeIntellect/INTELLECT-3) (8-bit)
 - [Devstral-Small-2-24B-Instruct-2512](https://huggingface.co/mistralai/Devstral-Small-2-24B-Instruct-2512) (bf16)
 - [Devstral-2-123B-Instruct-2512](https://huggingface.co/mistralai/Devstral-2-123B-Instruct-2512) (6-bit)

## Disclaimer
The above models and specific quantizations are not in any way an indication of what is required for advanced tool use. I tested Qwen3-Coder-30B-A3B-Instruct at 4-bit quantization (16GB) which was able to successfully add and use multiple new tools, including programatic tool calling, although it was not able to add tools with moderate complexity (like an SSL cert checker) which all of the above handle without issue.

## Related
[Introducing advanced tool use on the Claude Developer Platform](https://www.anthropic.com/engineering/advanced-tool-use)
[Agent Skills](https://agentskills.io/home)
[Tool Use Example](https://github.com/ml-explore/mlx-lm/blob/main/mlx_lm/examples/tool_use.py)
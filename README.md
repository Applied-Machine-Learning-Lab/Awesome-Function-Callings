# Awesome-Function-Callings

This repository is consistent with our survey paper. 

[![Awesome](https://awesome.re/badge.svg)](https://github.com/sindresorhus/awesome)
[![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

## Table of Contents

- [Sample Construction & Fine-tuning](#sample-construction--fine-tuning)
- [Deployment & Inference](#deployment--inference)
- [Evaluation](#evaluation)
- [Industry Products](#industry-products)
- [References](#references)

## Sample Construction & Fine-tuning

### Function Collection

- **Manual Construction**: Human-crafted functions [[1]](#1)
- **LLM Generation**: Automated function creation using LLMs [[2]](#2)
- **Web Mining**: Web-based function extraction [[3]](#3)

### Sample Construction

- **Text Representation**: Toolformer [[4]](#4), ToolGen [[5]](#5)
- **Token Representation**: Toolformer [[4]](#4), ToolGen [[5]](#5)
- **Multi-turn Interaction**: GraphQL-RestBench [[6]](#6), Hammer [[7]](#7)

### Fine-tuning Strategies

- **SFT** (Supervised Fine-tuning): ToolGen [[5]](#5), RAIT [[8]](#8)
- **PEFT** (Parameter-Efficient FT): GPT4Tools [[9]](#9), CITI [[10]](#10)
- **RL & RLHF**: WebGPT [[11]](#11), TaskMatrix.AI [[12]](#12)

## Deployment & Inference

### Task Planning

- **Foundational Mechanisms**: ReAct [[13]](#13), TACO [[14]](#14)
- **GUI-based**: AppAgent [[15]](#15), OS-ATLAS [[16]](#16)
- **System Optimizations**: Orca [[17]](#17), MemGPT [[18]](#18)

### Prompt Construction

- **Few-shot Integration**: NexusRaven [[19]](#19)
- **Context Management**: Chain-of-Thought [[20]](#20)
- **Query-based Retrieval**: Ask-when-Needed [[21]](#21)

### Function Generation

- **Grammar Control**: Grammar-Aligned [[22]](#22)
- **Multi-agent**: Ibsen [[23]](#23)
- **Experience Transfer**: Qian et al. [[24]](#24)

## Evaluation

### Overall Performance

- **Pass Rate**: ToolLLM [[25]](#25)
- **Quality Metrics**: BLEU [[26]](#26), ROUGE-L [[27]](#27)

### Benchmarks

- **Comprehensive**: ToolLLM [[25]](#25), BigCodeBench [[28]](#28)
- **Specialized**: Mobile-Bench [[29]](#29), RadABench [[30]](#30)

## Industry Products

| Product             | Description                           | Link                                                      |
| ------------------- | ------------------------------------- | --------------------------------------------------------- |
| Semantic Kernel     | Microsoft's LLM integration framework | [GitHub](https://github.com/microsoft/semantic-kernel)    |
| LangChain           | Building context-aware applications   | [GitHub](https://github.com/langchain-ai/langchain)       |
| AutoGPT             | Autonomous AI agent framework         | [GitHub](https://github.com/Significant-Gravitas/AutoGPT) |
| vLLM                | High-throughput LLM serving           | [GitHub](https://github.com/vllm-project/vllm)            |
| GLM-130B            | 130B bilingual LLM                    | [OpenReview](https://openreview.net/forum?id=-Aw0rrrPUF)  |
| Wolfram Mathematica | Symbolic computation integration      | [Official](https://www.wolfram.com/mathematica/)          |

## References

<a id="1">[1]</a> Yao et al. React: Synergizing Reasoning and Acting (2022)  
<a id="2">[2]</a> Schick et al. Toolformer (2023)  
<a id="3">[3]</a> Qin et al. WebCPM (2023)  

**[⬆ Back to Top](#awesome-function-callings)**

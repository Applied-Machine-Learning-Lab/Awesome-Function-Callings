# Comprehensive Reviews into Function Calling in Large Language Models

An index of concepts, frameworks, and methodologies in:
- **Function Calling Pipeline**: Understanding the entire process from pre-call to post-call stages
- **Sample Construction & Fine-tuning**: Building effective training datasets and optimizing models
- **Deployment & Inference**: Practical implementation strategies for real-world applications
- **Evaluation Frameworks**: Benchmarks and metrics for assessing function calling capabilities

Reproducibility is important! We prioritize methods with open-source implementations.

Please cite our survey paper if this index is helpful:

```bibtex
@article{wang2025comprehensive,
  title={Function Calling in Large Language Models: Industrial Practices, Challenges, and Future Direction},
  author={Wang, Maolin and Zhang, Yingyi and Peng, Cunyin and Chen, Yicheng and Zhou, Wei and Gu, Jinjie and Zhuang, Chenyi and Guo, Ruocheng and Yu, Bowen and Wang, Wanyu and Zhao, Xiangyu},
  url = {https://openreview.net/pdf?id=LNxVGPedFW}
  year={2025},
}
```

## Table of Contents
- [Challenges](#challenges)
- [Sample Construction and Fine-Tuning](#sample-construction-and-fine-tuning)
- [Deployment and Inference](#deployment-and-inference)
- [Evaluation](#evaluation)
- [Industry Products](#industry-products)
- [Open Issues](#open-issues)


![A comprehensive overview of the function calling system pipeline, showing the progression from natural language input through preprocessing, inference, and post-processing phases to executable function outputs.](./figures/overview.jpg)

Function calling capabilities in LLMs follow a three-stage workflow consisting of pre-call processing, on-call execution, and post-call validation.



## Challenges

### Pre-call Stage
| Challenge | Description |
|-----------|-------------|
| Challenge 1.1: Intent Recognition | Understanding user intentions accurately from natural language queries |
| Challenge 1.2: Function Redundancy | Managing redundant functions that serve similar purposes, increasing selection complexity |

### On-call Stage
| Challenge | Description |
|-----------|-------------|
| Challenge 2.1: Missing Calls | Failure to initiate function calls when required for task completion |
| Challenge 2.2: Unnecessary Calls | Triggering function calls when not required by the user's task |
| Challenge 3.1: Missing/Illegal Parameters | Inadequate or inappropriate parameter extraction from user inputs |
| Challenge 3.2: Function Hallucination | Mistakenly calling non-candidate or non-existent functions |
| Challenge 3.3: Pronouns Resolving | Correctly interpreting contextual references and pronouns in queries |
| Challenge 3.4: LLM Inherent Limitations | Performance constraints in latency and accuracy due to model architecture |
| Challenge 3.5: Multi-Call Procedure | Managing complex workflows requiring multiple related function calls |
| Challenge 3.6: Effective Context Management | Maintaining relevant information across multi-turn conversations |

### Post-call Stage
| Challenge | Description |
|-----------|-------------|
| Challenge 4.1: Execution Result Mismatch | Function outputs not aligning with user expectations |
| Challenge 4.2: Irrelevant Information Overload | Excessive irrelevant information in function outputs |
| Challenge 4.3: Mismatch Between Real-World Functions and Results | Gap between LLM-generated outputs and executable code |
| Challenge 4.4: Execution Failure | Functions failing despite correct triggering and parameterization |


![Illustration of the fine-tuning process for function calling capabilities in large language models, showing the progression from training data preparation through model training to evaluation.](./figures/training.jpg)

The training process involves specialized data preparation and fine-tuning strategies to equip models with function calling capabilities while maintaining general language understanding.

## Sample Construction and Fine-Tuning

### Function Collection
| Method | Description |
|--------|-------------|
| Manual Construction | Human-crafted functions with precise specifications and documentation |
| LLM Generation | Leveraging large language models like GPT-4, LlaMA 70B, and Qwen to automatically generate function specifications |
| Web Mining | Extracting diverse function objects from web resources, with descriptions supplemented by LLMs when necessary |

### Sample Construction
| Approach | Paper | Code | Description |
|----------|-------|------|-------------|
| Text Representation | [Toolformer: Language models can teach themselves to use tools](https://arxiv.org/abs/2302.04761) (Schick et al., 2024) | [Code](https://github.com/lucidrains/toolformer-pytorch) | Represents functions as natural language text, providing flexibility but requiring more token space |
| Text Representation | [ToolGen: Unified Tool Retrieval and Calling via Generation](https://arxiv.org/abs/2410.03439) (Wang et al., 2024) | [Code](https://github.com/OpenLLMAI/ToolGen) | Integrates tool information through generation with natural language descriptions |
| Token Representation | [Toolformer: Language models can teach themselves to use tools](https://arxiv.org/abs/2302.04761) (Schick et al., 2024) | [Code](https://github.com/lucidrains/toolformer-pytorch) | Encodes functions as special tokens during training for computational efficiency |
| Token Representation | [ToolGen: Unified Tool Retrieval and Calling via Generation](https://arxiv.org/abs/2410.03439) (Wang et al., 2024) | [Code](https://github.com/OpenLLMAI/ToolGen) | Uses token representation during training while maintaining semantic richness |
| Multi-turn Interaction | [Sequential API Function Calling Using GraphQL Schema](https://aclanthology.org/2024.emnlp-industry-4107/) (Saha et al., 2024) | - | Introduces structured API schemas and response mapping for sequential function calling |
| Multi-turn Interaction | [Hammer: Robust Function-Calling for On-Device Language Models via Function Masking](https://arxiv.org/abs/2410.04587) (Lin et al., 2024) | - | Specialized techniques to address naming convention sensitivity issues for on-device deployment |

### Fine-tuning Strategies
| Method | Paper | Description |
|--------|-------|-------------|
| Supervised Fine-Tuning (SFT) | [ToolGen: Unified Tool Retrieval and Calling via Generation](https://arxiv.org/abs/2410.03439) (Wang et al., 2024) | Standard fine-tuning approach with unified retrieval and calling generation |
| Supervised Fine-Tuning (SFT) | [RAIT: Retrieval Augmented Instruction Tuning](https://arxiv.org/abs/2310.06839) (Asai et al., 2023) | Retrieval-augmented approach for instruction tuning |
| Supervised Fine-Tuning (SFT) | [Show your work: Scratchpads for intermediate computation with language models](https://arxiv.org/abs/2112.00114) (Nye et al., 2021) | Scratchpad-based training for step-by-step computation |
| Supervised Fine-Tuning (SFT) | [Giving BERT a calculator: Finding operations and arguments with reading comprehension](https://arxiv.org/abs/1909.00109) (Andor et al., 2019) | Integrates mathematical operations with language understanding |
| Supervised Fine-Tuning (SFT) | [Rainier: Reinforced knowledge introspector for commonsense question answering](https://arxiv.org/abs/2210.03078) (Liu et al., 2022) | Knowledge introspection for improved reasoning |
| Supervised Fine-Tuning (SFT) | [Learning to represent programs with graphs](https://arxiv.org/abs/1711.00740) (Allamanis et al., 2018) | Program representation through graph structures |
| Supervised Fine-Tuning (SFT) | [A deep generative model of code syntactic structures](https://arxiv.org/abs/1704.01696) (Barone et al., 2017) | Syntax-aware code generation models |
| Supervised Fine-Tuning (SFT) | [Pre-training for Abstractive Document Summarization](https://arxiv.org/abs/1909.10393) (Liu et al., 2019) | Domain-specific pre-training for document summarization |
| Supervised Fine-Tuning (SFT) | [Character-level neural network for biomedical named entity recognition](https://www.sciencedirect.com/science/article/abs/pii/S1532046417301776) (Liu et al., 2017) | Character-level models for biomedical entity recognition |
| Parameter-Efficient Fine-Tuning (PEFT) | [Gpt4tools: Teaching large language model to use tools via self-instruction](https://arxiv.org/abs/2305.05181) (Yang et al., 2024) | Self-instruction approach for tool utilization |
| Parameter-Efficient Fine-Tuning (PEFT) | [CITI: Enhancing Tool Utilizing Ability in Large Language Models without Sacrificing General Performance](https://arxiv.org/abs/2409.13202) (Hao et al., 2024) | Balanced approach for tool utilization without performance tradeoffs |
| Parameter-Efficient Fine-Tuning (PEFT) | [Toolformer: Language models can teach themselves to use tools](https://arxiv.org/abs/2302.04761) (Schick et al., 2024) | Self-supervised learning for tool usage |
| Parameter-Efficient Fine-Tuning (PEFT) | [PLUG: Parameter-efficient LLMs Using Plugin Adapters](https://arxiv.org/abs/2305.12945) (Li et al., 2023) | Plugin adapter approach for parameter efficiency |
| Parameter-Efficient Fine-Tuning (PEFT) | [Prompt tuning for generative multimodal pretrained models](https://arxiv.org/abs/2205.11822) (Wei et al., 2022) | Prompt-based tuning for multimodal generation |
| Reinforcement Learning & RLHF | [WebGPT: Browser-assisted question-answering with human feedback](https://arxiv.org/abs/2112.09332) (Nakano et al., 2021) | Web browsing capabilities enhanced through human feedback |
| Reinforcement Learning & RLHF | [Taskmatrix.ai: Completing tasks by connecting foundation models with millions of apis](https://arxiv.org/abs/2303.16434) (Liang et al., 2024) | Large-scale API connectivity through reinforcement learning |
| Reinforcement Learning & RLHF | [MADAC: Multi-Agent Decision-Aware Conversation via Reinforcement Learning](https://arxiv.org/abs/2311.05772) (Li et al., 2023) | Decision-aware conversation through multi-agent reinforcement learning |
| Reinforcement Learning & RLHF | [GopherCite: Teaching language models to support answers with verified quotes](https://arxiv.org/abs/2203.11147) (Menick et al., 2022) | Citation verification through reinforcement learning |
| Reinforcement Learning & RLHF | [Emergent Abilities of Large Language Models](https://arxiv.org/abs/2206.07682) (Kojima et al., 2022) | Studies emergent abilities through reinforcement learning approaches |
| Reinforcement Learning & RLHF | [Direct Preference Optimization: Your Language Model is Secretly a Reward Model](https://arxiv.org/abs/2305.18290) (Rafailov et al., 2023) | Preference optimization without explicit reward modeling |
| Reinforcement Learning & RLHF | [Deep reinforcement learning from human preferences](https://proceedings.neurips.cc/paper/2017/hash/d5e2c0adad503c91f91df240d0cd4e49-Abstract.html) (Christiano et al., 2017) | Foundational work on learning from human preferences |
| Reinforcement Learning & RLHF | [The Bias-Variance Trade-off in RLHF: Overfitting to Human Feedback in Large Language Models](https://arxiv.org/abs/2311.00168) (Manduzio et al., 2023) | Analysis of overfitting risks in human feedback |

### Critical Emphasis

![Experimental results showing performance trends across models of different sizes, demonstrating that larger models achieve significantly better function calling capabilities after fine-tuning.](./figures/model_size_comparison.jpg)

Based on practical implementations, we emphasize that data quality (and variety) plays a more crucial role than data quantity in both data construction and fine-tuning phases, given the intricate nature of function calling tasks.

![Performance comparison across different model sizes, showing that larger models demonstrate substantially better function calling capabilities after fine-tuning, while base models show minimal function calling abilities regardless of scale.](./figures/model_comparison_q.jpg)

Based on practical implementations, we emphasize that data quality (and variety) plays a more crucial role than data quantity in both data construction and fine-tuning phases, given the intricate nature of function calling tasks.


| Emphasis | Description |
|----------|-------------|
| Data Quality | Prioritizing dataset diversity and verification over quantity for more robust function calling capabilities |
| Model Scaling | Larger models demonstrate significantly better function calling capabilities, with notable improvements above 7B parameters |
| Capability Balance | Maintaining a balance between specialized function calling abilities and general language capabilities to avoid performance tradeoffs |

## Deployment and Inference


![Figure 6: A Typical Deployment of LLM for Function Calling Stages: The Flow through Input Construction, Memory Integration, and Output Format Validation (Function Execution). Note that actual implementations may vary in practice.](./figures/deployment.jpg)

This section explores practical deployment strategies for function-calling LLMs. Figure illustrates a typical workflow where queries pass through input construction, LLM processing, and format validation or execution, with memory components maintaining context throughout the process.

### Task Planning

#### Foundational Planning Mechanisms
| Name | Paper | Venue | Code | Comment |
|------|-------|-------|------|---------|
| ReAct | [React: Synergizing reasoning and acting in language models](https://arxiv.org/abs/2210.03629) (Yao et al., 2022) | NeurIPS | [Code](https://github.com/ysymyth/ReAct) | Combines reasoning and acting through chain-of-thought prompts |
| ToolFormer | [Toolformer: Language models can teach themselves to use tools](https://arxiv.org/abs/2302.04761) (Schick et al., 2023) | NeurIPS | [Code](https://github.com/lucidrains/toolformer-pytorch) | Enables LLMs to use external tools through self-supervised learning |
| Reverse Chain | [Reverse chain: A generic-rule for llms to master multi-api planning](https://arxiv.org/abs/2310.04474) (Zhang et al., 2023) | arXiv | - | Introduces target-driven backward reasoning for controlled multi-API planning |
| AVATAR | [AvaTaR: Optimizing LLM Agents for Tool-Assisted Knowledge Retrieval](https://arxiv.org/abs/2406.11200) (Wu et al., 2024) | arXiv | [Code](https://github.com/Shirley-Kokane/AvaTaR) | Actor-comparator architecture for tool-assisted knowledge retrieval |
| DEPS | [Describe, explain, plan and select: interactive planning with LLMs enables open-world multi-task agents](https://arxiv.org/abs/2402.07152) (Wang et al., 2024) | NeurIPS | [Code](https://github.com/microsoft/DEPS) | Interactive planning through description-based decomposition |
| LLM-MCTS | [LLM-MCTS: Monte Carlo Tree Search with LLMs for reasoning tasks](https://arxiv.org/abs/2305.14969) (Zhao et al., 2023) | arXiv | [Code](https://github.com/princeton-nlp/llm-mcts) | Monte Carlo Tree Search approach for multi-step reasoning |
| MACT | [Measuring and narrowing the compositional gap in language models](https://arxiv.org/abs/2210.03350) (Zheng et al., 2023) | arXiv | [Code](https://github.com/amazon-science/mact) | Addresses compositional generalization through structured decomposition |
| TACO | [Taco: Towards api conversation workflows for tool augmentation](https://arxiv.org/abs/2402.05159) (Mao et al., 2024) | arXiv | [Code](https://github.com/microsoft/TACO) | Structured workflows for tool-augmented conversational agents |
| PAE | [Proposer-Agent-Evaluator (PAE): Autonomous Skill Discovery For Foundation Model Internet Agents](https://arxiv.org/abs/2412.13194) (Zhou et al., 2024) | arXiv | [Code](https://github.com/LifeLongTeam/pae-autonomous-skill-discovery) | Multi-agent system for autonomous skill discovery and planning |
| SCIAGENT | [SciAgent: Tool-augmented language models for scientific reasoning](https://arxiv.org/abs/2308.04744) (Wang et al., 2023) | arXiv | [Code](https://github.com/OpenBMB/SciAgent) | Tool-augmented planning for scientific problem-solving |
| Agent Laboratory | [Agent laboratory: Using llm agents as research assistants](https://arxiv.org/abs/2501.04227) (Schmidgall et al., 2025) | arXiv | - | Multi-agent architecture with specialized roles for research planning |

#### GUI-based Approaches
| Name | Paper | Venue | Code | Comment |
|------|-------|-------|------|---------|
| AppAgent | [AppAgent: Multimodal Agents as Smartphone Users](https://arxiv.org/abs/2312.13771) (Yang et al., 2023) | arXiv | [Code](https://github.com/mnotgod96/AppAgent) | Agents learn to operate smartphone applications via visual interfaces |
| OS-ATLAS | [OS-ATLAS: Foundation AI Agent for Desktop Operating Systems](https://arxiv.org/abs/2403.17934) (Wang et al., 2024) | arXiv | [Code](https://github.com/juliancodaforno/OS-ATLAS) | End-to-end desktop OS navigation with multimodal perception |
| AndroidLab | [AndroidLab: Large Language Models for Android UI Navigation](https://arxiv.org/abs/2312.05892) (Yan et al., 2023) | arXiv | [Code](https://github.com/cooelf/AndroidLab) | Benchmarking and improving LLM-based Android UI navigation |
| Ponder | [Ponder: Toolkit-Aware Agent for Automating Desktop Tasks](https://arxiv.org/abs/2401.08766) (Wu et al., 2024) | arXiv | [Code](https://github.com/CraftJarvis/Ponder) | Self-reflective navigation through desktop interfaces |
| OS-Genesis | [OS-Genesis: Evaluating the multimodal capabilities of large language models in navigating operating systems](https://arxiv.org/abs/2403.04136) (Li et al., 2024) | arXiv | [Code](https://github.com/OSXGitHub/OS-Genesis) | Comprehensive benchmark for evaluating OS navigation capabilities |

#### System Optimizations
| Name | Paper | Venue | Code | Comment |
|------|-------|-------|------|---------|
| Orca | [Orca: Progressive learning from complex explanation traces of gpt-4](https://arxiv.org/abs/2306.02707) (Mukherjee et al., 2023) | arXiv | - | Learns from complex explanation traces for progressive improvement |
| Orca 2 | [Orca 2: Teaching small language models how to reason](https://arxiv.org/abs/2311.11045) (Mitra et al., 2023) | arXiv | [Code](https://github.com/microsoft/orca) | Enhanced reasoning capabilities through step-by-step explanation |
| Memgpt | [Memgpt: Towards llms as operating systems](https://arxiv.org/abs/2310.08560) (Chen et al., 2023) | arXiv | [Code](https://github.com/cpacker/MemGPT) | Memory management system with hierarchical storage |
| AIOS-Agent | [Aios-agent: In-context fine-grained os control with large language models](https://arxiv.org/abs/2402.06596) (Chu et al., 2024) | arXiv | [Code](https://github.com/ericzzz21/aios-agent) | System-level control through fine-grained OS operations |
| SpecInfer | [Specinfer: Accelerating generative llm inference via speculative execution](https://arxiv.org/abs/2305.09781) (Yan et al., 2023) | arXiv | [Code](https://github.com/sosp-paper-22/SpecInfer) | Performance optimization through speculative execution |
| PEOA | [PEOA: Progressive Exemplar-Oriented API-Aware Prompting](https://arxiv.org/abs/2407.08930) (Wang et al., 2024) | arXiv | [Code](https://github.com/wang-research-lab/peoa) | Exemplar-based prompting for API-aware interactions |
| LLM-Tool Compiler | [Compiler-aided Generation for Tool-LLM Inference](https://arxiv.org/abs/2406.04462) (Song et al., 2024) | arXiv | - | Compilation techniques to optimize tool operations |

#### Error Handling Approaches
| Name | Paper | Venue | Code | Comment |
|------|-------|-------|------|---------|
| LLM-Planner | [Llm-planner: Few-shot grounded planning for embodied agents with large language models](https://arxiv.org/abs/2212.04088) (Song et al., 2023) | ICCV | [Code](https://github.com/OSU-NLP-Group/LLM-Planner) | Environmental feedback for plan regeneration during failures |
| ToolChain* | [Toolchain*: Efficient action space navigation in large language models with a* search](https://arxiv.org/abs/2310.13227) (Zhuang et al., 2023) | arXiv | [Code](https://github.com/yzhuang0222/ToolChain) | Employs decision trees for systematic API call management |
| TPTU | [Test-Time Prompt Updating for Text-to-Image Generative Models](https://arxiv.org/abs/2309.15505) (Liang et al., 2023) | arXiv | [Code](https://github.com/iiis-turing-llm/TPTU) | Adaptive prompt refinement based on execution feedback |
| Buckets | [Buckets: Efficient multi-environment learning for llm agents](https://arxiv.org/abs/2310.07837) (Burkart et al., 2023) | arXiv | [Code](https://github.com/google-research/google-research/tree/master/buckets) | Error-aware multi-environment learning framework |
| AMOR | [AMOR: A Recipe for Building Adaptable Modular Knowledge Agents Through Process Feedback](https://arxiv.org/abs/2402.01469) (Guan et al., 2024) | arXiv | [Code](https://github.com/gpt4life/amor) | FSM-based framework enabling process-level human feedback |

#### Tree-based Approaches
| Name | Paper | Venue | Code | Comment |
|------|-------|-------|------|---------|
| ControlLLM | [Controlllm: Augment language models with tools by searching on graphs](https://arxiv.org/abs/2310.17796) (Liu et al., 2023) | arXiv | [Code](https://github.com/OpenGVLab/ControlLLM) | Tree of Thoughts with depth-first search on tool graphs |
| PLUTO | [Pluto: A recipe for building adaptable autonomous llm agents](https://arxiv.org/abs/2402.04397) (Guan et al., 2024) | arXiv | [Code](https://github.com/gpt4life/pluto) | Adaptable autonomous agents with tree-based planning |
| Toolink | [Toolink: Linking toolkit creation and using through chain-of-solving on open-source model](https://arxiv.org/abs/2310.05155) (Qian et al., 2023) | arXiv | [Code](https://github.com/toolllm/toolink) | Hierarchical task decomposition with toolkit creation |
| TPTU-v2 | [TPTU-v2: Boosting Test-Time Prompt Tuning for Text-to-Image Generation](https://arxiv.org/abs/2311.17517) (Kawar et al., 2023) | arXiv | [Code](https://github.com/iiis-turing-llm/TPTU-v2) | Enhanced tree-based prompt optimization strategies |
| α-UMi | [Small llms are weak tool learners: A multi-llm agent](https://arxiv.org/abs/2401.07324) (Shen et al., 2024) | arXiv | [Code](https://github.com/zjunlp/AntGPT) | Planning-oriented fine-tuning for small LLMs |

#### Adaptive Planning Strategies
| Name | Paper | Venue | Code | Comment |
|------|-------|-------|------|---------|
| COA | [Chain of agents: A framework for collaborative tool utilization with language models](https://arxiv.org/abs/2403.12744) (Chang et al., 2024) | arXiv | [Code](https://github.com/chain-of-agents/chain-of-agents) | Agent collaboration framework for specialized tool utilization |
| DEER | [DEER: Diverse Evolution Ensembles are Required for Large Language Model Agents](https://arxiv.org/abs/2403.13511) (Chen et al., 2024) | arXiv | [Code](https://github.com/casmlab/agent-evolution) | Diverse evolution ensembles for LLM agent improvement |
| SOAY | [SOAY: Responsive and Safe Structured Editing with Dynamic Text Features](https://arxiv.org/abs/2406.19270) (Wang et al., 2024) | arXiv | [Code](https://github.com/samliu0631/SOAY) | Dynamic text feature adaptation for structured editing |
| ProgPrompt | [ProgPrompt: Generating Situated Robot Task Plans using Large Language Models](https://arxiv.org/abs/2209.11302) (Singh et al., 2022) | arXiv | [Code](https://github.com/progprompt/progprompt) | Adaptive programming for situated robot task planning |
| AutoTOD | [Towards fully autonomous dialogue systems via interactive few-shot learning](https://arxiv.org/abs/2310.07472) (Zhang et al., 2023) | arXiv | - | Interactive few-shot learning for dialogue system adaptation |
| MATMCD | [MATMCD: An Open Benchmark for Mobile Agent Testing in Minecraft with Concept Drift](https://arxiv.org/abs/2403.04095) (Xiong et al., 2024) | arXiv | [Code](https://github.com/MineDojo/MATMCD) | Adaptive strategies for concept drift in Minecraft environments |
| CC-PP | [CC-PP: Chain-of-components pipeline prompting for planning with large language models](https://arxiv.org/abs/2402.03610) (Gui et al., 2024) | arXiv | - | Component-based pipeline approach for adaptive planning |
| AVT | [AVT: Bridging Vision and Language with Adaptive Vision Transformers](https://arxiv.org/abs/2407.18166) (Yang et al., 2024) | arXiv | [Code](https://github.com/AICYJ/AVT) | Adaptive vision transformers for multimodal planning |
| K-agents | [Autonomous Agents for Real-Time Decision Making: Applications in Banking](https://arxiv.org/abs/2311.06217) (Balaji et al., 2023) | arXiv | - | Autonomous agent adaptation for financial decision making |
| Agent-Pro | [Agent-pro: Learning to evolve via policy-level reflection and optimization](https://arxiv.org/abs/2402.17574) (Zhang et al., 2024) | arXiv | [Code](https://github.com/sail-sg/Agent-Pro) | Dynamic belief management and policy-level reflection |
| Inner Thoughts | [Proactive Conversational Agents with Inner Thoughts](https://arxiv.org/abs/2501.00383) (Liu et al., 2024) | arXiv | [Code](https://github.com/hkust-nlp/PCA) | Continuous thought generation for proactive participation |

### Prompt Construction

#### Few-shot Integration
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Example demonstrations | [Instance-wise prompting for few-shot transferability of large language models](https://arxiv.org/abs/2401.04997) (Pan et al., 2024) | [Code](https://github.com/apple/ml-instance-wise-prompting) | Tailored examples for improved function understanding |
| Four-shot prompting | - | - | Demonstrated optimal number of examples for tool usage |

#### Context Management
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Function definitions | - | - | Including comprehensive function specifications in context |
| Docstrings | - | - | Utilizing standardized documentation formats for clarity |
| Chain-of-thought | [Chain-of-thought prompting elicits reasoning in large language models](https://arxiv.org/abs/2201.11903) (Wei et al., 2022) | - | Step-by-step reasoning process for complex function selection |

#### Query-based Retrieval
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Ask-when-Needed | [Learning to Ask: When LLMs Meet Unclear Instruction](https://arxiv.org/abs/2409.00557) (Wang et al., 2024) | [Code](https://github.com/CAISA-Lab/UnclearInstrLearningToAsk) | On-demand clarification for tool selection |
| Interactive refinement | - | - | Iterative query refinement through user interaction |

### Function Generation
| Approach | Paper | Venue | Code | Comment |
|----------|-------|-------|------|---------|
| Grammar Control | [Grammar-Aligned Decoding](https://arxiv.org/abs/2405.21047) (Park et al., 2024) | arXiv | [Code](https://github.com/microsoft/semantic-kernel/tree/main/python/semantic_kernel/core_plugins) | Constrains output using context-free grammar |
| TOOL-ED | [TOOL-ED: Enhancing Empathetic Response Generation with the Tool Calling Capability of LLM](https://arxiv.org/abs/2412.03096) (Cao et al., 2024) | arXiv | - | Treats knowledge bases as callable tools for empathetic dialogue |
| IBSEN | [IBSEN: Director-Actor Agent Collaboration for Controllable and Interactive Drama Script Generation](https://aclanthology.org/2024.acl-long.99/) (Han et al., 2024) | ACL | [Code](https://github.com/X-PLUG/IBSEN) | Multi-agent coordination for controlled script generation |
| Multi-agent coordination | [Improving factuality and reasoning in language models through multiagent debate](https://arxiv.org/abs/2305.14325) (Chan et al., 2023) | arXiv | [Code](https://github.com/composable-models/llm_multiagent_debate) | Collaborative refinement through structured agent debate |
| Task proposal | [Proposer-Agent-Evaluator (PAE): Autonomous Skill Discovery For Foundation Model Internet Agents](https://arxiv.org/abs/2412.13194) (Zhou et al., 2024) | arXiv | [Code](https://github.com/LifeLongTeam/pae-autonomous-skill-discovery) | Automated task proposal and execution validation |
| Experience transfer | [X-TOOLS: Tool Generation and Adaptation from Existing APIs for Dialogue Agents](https://arxiv.org/abs/2311.09562) (Patil et al., 2023) | arXiv | [Code](https://github.com/X-PLUG/X-TOOLS) | Transfers API experience across different domains |

### Function Mapping



![Figure 7: Function mapping strategies in LLM function calling, illustrating the transformation process from natural language input to system-executable function calls through pronoun mapping, format alignment, and error checking.](./figures/functionmapping.jpg)

Function mapping plays a crucial role in deploying function calling, primarily responsible for transforming model outputs at the semantic level into executable commands in the physical space. Moreover, as shown in figure, function mapping involves Pronoun Mapping, Format Alignment, and Error Checking.



#### Resolution
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Rule-based | [Deterministic coreference resolution based on entity-centric, precision-ranked rules](https://aclanthology.org/J13-4004/) (Lee et al., 2013) | [Code](https://github.com/huggingface/neuralcoref) | Predefined mapping rules for contextual references |
| Rule-based | [End-to-end neural entity linking](https://aclanthology.org/J19-1044/) (Kolitsas et al., 2018) | [Code](https://github.com/dalab/end2end_neural_el) | Neural approach to entity linking with rule-based components |
| Knowledge reasoning | [Knowledge-aware Pronoun Coreference Resolution](https://aclanthology.org/P19-1081/) (Zhang et al., 2019) | - | Leverages knowledge graphs for reference resolution |
| LLM mapping | [End-to-end Neural Coreference Resolution](https://aclanthology.org/D17-1018/) (Lee et al., 2017) | [Code](https://github.com/kentonl/e2e-coref) | Uses neural models for contextual mapping |

#### Alignment
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Dictionary mapping | [Syllabus: Portable Curricula for Reinforcement Learning Agents](https://arxiv.org/abs/2411.11318) (Sullivan et al., 2024) | [Code](https://github.com/rsullivan00/syllabus) | Unified APIs and format alignment mechanisms |
| Semantic matching | [Improving Semantic Similarity for Low-Resource Named Entity Linking](https://arxiv.org/abs/2203.00778) (Niu et al., 2022) | [Code](https://github.com/HLTCHKUST/semnet) | Vector-based semantic similarity for linking entities |
| Normalization | - | - | Format standardization for consistent representation |

#### Validation
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Parameter checking | - | - | Verification of parameter completeness and formatting |
| Value enumeration | - | - | Validating input values against acceptable ranges |
| Permission management | - | - | Ensuring appropriate access levels for function execution |

### Response Generation

#### Initial Generation
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Placeholder results | [Toolkengpt: Augmenting frozen language models with massive tools via tool embeddings](https://arxiv.org/abs/2305.11554) (Hao et al., 2024) | [Code](https://github.com/ryoungj/ToolkenGPT) | Generated placeholders replaced with API call results |
| Placeholder results | [Large language models encode clinical knowledge](https://www.nature.com/articles/s41586-023-06291-2) (Singhal et al., 2023) | - | Domain-specific placeholder generation for clinical applications |
| Placeholder results | [Toolformer: Language models can teach themselves to use tools](https://arxiv.org/abs/2302.04761) (Schick et al., 2023) | [Code](https://github.com/lucidrains/toolformer-pytorch) | Self-supervised approach to result placeholder generation |
| Function unpredictability | [React: Synergizing reasoning and acting in language models](https://arxiv.org/abs/2210.03629) (Yao et al., 2023) | [Code](https://github.com/ysymyth/ReAct) | Reasoning-action interleaving to handle unpredictable outputs |

#### Templates
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Structure format | [Gorilla: Large language model connected with massive apis](https://arxiv.org/abs/2305.15334) (Patil et al., 2023) | [Code](https://github.com/ShishirPatil/gorilla) | Structured templates for consistent output formatting |
| Structure format | [Prompt2model: Generating deployable models from natural language instructions](https://arxiv.org/abs/2308.12667) (Pryzant et al., 2023) | - | Transforms natural language into structured model specifications |
| Formatting | [The api bank: A comprehensive benchmark for tool-augmented llms](https://arxiv.org/abs/2304.08244) (Li et al., 2023) | [Code](https://github.com/AlibabaResearch/DAMO-ConvAI/tree/main/api-bank) | Standardized formatting for API responses |
| Signatures | [Instance-wise prompting for few-shot transferability of large language models](https://arxiv.org/abs/2401.04997) (Pan et al., 2024) | [Code](https://github.com/apple/ml-instance-wise-prompting) | Instance-specific signature generation |

#### Review
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Validation | [Prompt2model: Generating deployable models from natural language instructions](https://arxiv.org/abs/2308.12667) (Pryzant et al., 2023) | - | Validation mechanisms for generated model specifications |
| Validation | [T-eval: Evaluating the tool utilization capability of large language models step by step](https://aclanthology.org/2024.acl-long.591/) (Chen et al., 2024) | [Code](https://github.com/open-compass/T-Eval) | Step-by-step validation of tool utilization |
| Agent correction | [Learning to use tools via cooperative and interactive agents](https://arxiv.org/abs/2403.03031) (Shi et al., 2024) | [Code](https://github.com/RUC-GSAI/LLM-CU) | Specialized agents review and correct each other's actions |
| Agent correction | [Self-correction of large language models via cognitive psychology](https://ojs.aaai.org/index.php/AAAI/article/view/29868) (Sun et al., 2024) | - | Psychological principles for improved self-correction |
| Feedback | [Great principles for learning to use tools with llms](https://arxiv.org/abs/2402.04254) (Guo et al., 2024) | - | Principles for effective feedback incorporation |
| Feedback | [WebGPT: Browser-assisted question-answering with human feedback](https://arxiv.org/abs/2112.09332) (Nakano et al., 2021) | - | Human feedback integration for improved web interactions |
| Feedback | [WhiteboardAgent: Autonomous Multi-Step Visual Language Reasoning via Whiteboard Interaction](https://arxiv.org/abs/2405.08217) (Wang et al., 2024) | [Code](https://github.com/KwaiKEG/WhiteboardAgent) | Visual reasoning through whiteboard interaction feedback |

#### RAG
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Example retrieval | [ClusterLLM: Large Language Models as a Guide for Text Clustering](https://arxiv.org/abs/2307.09013) (Chen et al., 2023) | [Code](https://github.com/amazon-science/clustering-with-llms) | Clustered example retrieval for enhanced responses |
| System mapping | [A neural probabilistic model for entity disambiguation using multiple resources](https://arxiv.org/abs/1909.12739) (Agarwal et al., 2019) | - | Multi-resource entity disambiguation for system mapping |
| System mapping | [LLM+P: Empowering Large Language Models with Optimal Planning Proficiency](https://arxiv.org/abs/2304.11477) (Liu et al., 2023) | - | Planning-oriented mapping for systematic responses |
| System mapping | [Llm+p: Empowering large language models with planning capabilities in multi-scenario human-ai collaboration](https://ojs.aaai.org/index.php/AAAI/article/view/28778) (Ma et al., 2024) | - | Enhanced collaborative mapping between human inputs and AI responses |
| System mapping | [InstructExcel: A Benchmark for Natural Language Instructions in Excel](https://arxiv.org/abs/2301.07065) (Mao et al., 2023) | [Code](https://github.com/HFAiLab/InstructExcel) | Domain-specific mapping for spreadsheet operations |
| System mapping | [INSTRUCTION FOLLOWING EVALUATION BY PREDICTING HUMAN FEEDBACK](https://arxiv.org/abs/2310.16427) (Muennighoff et al., 2023) | [Code](https://github.com/huggingface/instruction-following-eval) | Human feedback-based mapping evaluation |
| System mapping | [Instance-wise prompting for few-shot transferability of large language models](https://arxiv.org/abs/2401.04997) (Pan et al., 2024) | [Code](https://github.com/apple/ml-instance-wise-prompting) | Instance-specific mapping mechanisms |
| System mapping | [Vipergpt: Visual inference via python execution for reasoning](https://arxiv.org/abs/2303.08128) (Suris et al., 2023) | [Code](https://github.com/cvlab-columbia/viper) | Python execution-based visual reasoning and mapping |

### Memory Scheme

#### Memory Structure
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Hierarchical structure and storage | [Memorybank: Enhancing large language models with long-term memory](https://ojs.aaai.org/index.php/AAAI/article/view/29545) (Zhong et al., 2024) | [Code](https://github.com/zhongwanjun/MemoryBank-SiliconFriend) | Hierarchical storage with Ebbinghaus-inspired updating |
| Task-related symbolic memory | [Zero-shot task-oriented dialogue in the wild](https://arxiv.org/abs/2301.09503) (Xie et al., 2023) | - | Specialized memory structures for dialogue-based tasks |
| Three-layered memory architecture | [Longllms: Enabling language models to process long contexts by leveraging memory mechanisms](https://arxiv.org/abs/2401.07872) (Li et al., 2024) | [Code](https://github.com/hkust-nlp/longllms) | Working, episodic, and semantic memory layers |
| Persistent memory stream | [Unleashing infinite-length input capacity for large-scale language models with self-controlled memory system](https://arxiv.org/abs/2304.10203) (Liang et al., 2023) | - | Continuous memory stream for unlimited context |

#### Memory Management
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Self-controlled memory mechanism | [Unleashing infinite-length input capacity for large-scale language models with self-controlled memory system](https://arxiv.org/abs/2304.10203) (Liang et al., 2023) | - | Memory management through control systems |
| Memory control system | [Unleashing infinite-length input capacity for large-scale language models with self-controlled memory system](https://arxiv.org/abs/2304.10203) (Liang et al., 2023) | - | Automated memory control for extended contexts |
| Memory control system | [Memgpt: Towards llms as operating systems](https://arxiv.org/abs/2310.08560) (Chen et al., 2023) | [Code](https://github.com/cpacker/MemGPT) | Operating system-inspired memory management |
| Multi-agent experience storage | [Lmrl: Learning multiagent reinforcement learning framework in a collaborative agent society](https://arxiv.org/abs/2402.09205) (Lee et al., 2024) | [Code](https://github.com/LMRL-Lab/lmrl) | Collaborative storage of multi-agent experiences |

#### Memory Retrieval
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Cross-conversation memory retrieval | [Memorybank: Enhancing large language models with long-term memory](https://ojs.aaai.org/index.php/AAAI/article/view/29545) (Zhong et al., 2024) | [Code](https://github.com/zhongwanjun/MemoryBank-SiliconFriend) | Retrieval mechanisms spanning multiple conversations |
| LSH-based indexing mechanism | [Memgpt: Towards llms as operating systems](https://arxiv.org/abs/2310.08560) (Chen et al., 2023) | [Code](https://github.com/cpacker/MemGPT) | Locality-sensitive hashing for efficient indexing |
| Similarity-based retrieval | [Synapse: Trajectory-as-exemplar prompting with memory for computer control](https://arxiv.org/abs/2310.15142) (Zheng et al., 2023) | [Code](https://github.com/microsoft/Synapse) | Vector similarity for contextual memory access |
| Efficient memory access | [Think-in-memory: Recalling and post-thinking enable llms with long-term memory](https://arxiv.org/abs/2311.08719) (Liu et al., 2023) | [Code](https://github.com/microsoft/ThinkInMemory) | Optimized access patterns for memory retrieval |

#### Memory Processing
| Approach | Paper | Code | Comment |
|----------|-------|------|---------|
| Thought-based memory storage | [Think-in-memory: Recalling and post-thinking enable llms with long-term memory](https://arxiv.org/abs/2311.08719) (Liu et al., 2023) | [Code](https://github.com/microsoft/ThinkInMemory) | Stores and recalls thoughts rather than raw conversations |
| Trajectory-as-exemplar framework | [Synapse: Trajectory-as-exemplar prompting with memory for computer control](https://arxiv.org/abs/2310.15142) (Zheng et al., 2023) | [Code](https://github.com/microsoft/Synapse) | Complete trajectories as exemplars for planning |
| State abstraction mechanism | [Synapse: Trajectory-as-exemplar prompting with memory for computer control](https://arxiv.org/abs/2310.15142) (Zheng et al., 2023) | [Code](https://github.com/microsoft/Synapse) | Compact state representations for efficient storage |
| Knowledge triplet | [Memgpt: Towards llms as operating systems](https://arxiv.org/abs/2310.08560) (Chen et al., 2023) | [Code](https://github.com/cpacker/MemGPT) | Subject-predicate-object triplets for structured knowledge |

## Evaluation

### Overall Performance

![Performance comparison across various models showing the relative effectiveness of different approaches on function calling tasks, highlighting the relationship between model architecture and function calling capabilities.](./figures/performance_comparison.jpg)

The experimental results demonstrate clear performance differences between models trained specifically for function calling versus general-purpose models adapted to the task.



#### Function Selection Metrics
| Metric | Description | Example Works |
|--------|-------------|--------------|
| Recall@K | Proportion of relevant tools ranked within top K positions | [COLT: Towards Completeness-Oriented Tool Retrieval for Large Language Models](https://arxiv.org/abs/2405.16089) (Qu et al., 2024) |
| NDCG@K | Normalized Discounted Cumulative Gain at K | [Large language models are versatile decomposers: Decompose evidence and questions for table-based reasoning](https://arxiv.org/abs/2301.13808) (Cheng et al., 2023) |
| COMP@K | Completeness-oriented retrieval evaluation at K | [COLT: Towards Completeness-Oriented Tool Retrieval for Large Language Models](https://arxiv.org/abs/2405.16089) (Qu et al., 2024) |

#### Core Evaluation Metrics
| Metric | Description | Example Works |
|--------|-------------|--------------|
| Pass Rate | Proportion of successfully completed instructions | [Toolllm: Facilitating large language models to master 16000+ real-world apis](https://arxiv.org/abs/2307.16789) (Qin et al., 2023) |
| Win/Success Rate | Quality evaluation including information richness, factual accuracy | [NESTFUL: A Benchmark for Evaluating LLMs on Nested Sequences of API Calls](https://arxiv.org/abs/2409.03797) (Basu et al., 2024) |

#### Comprehensive Assessment
| Metric | Description | Example Works |
|--------|-------------|--------------|
| T-Eval | Comprehensive assessment of planning, reasoning, retrieval, understanding | [T-eval: Evaluating the tool utilization capability of large language models step by step](https://aclanthology.org/2024.acl-long.591/) (Chen et al., 2024) |

#### Quality-based Metrics
| Metric | Description | Example Works |
|--------|-------------|--------------|
| BLEU | Bilingual Evaluation Understudy for translation quality | [Bleu: a method for automatic evaluation of machine translation](https://aclanthology.org/P02-1040/) (Papineni et al., 2002) |
| ROUGE-L | Longest Common Subsequence based metric for text summarization | [Rouge: A package for automatic evaluation of summaries](https://aclanthology.org/W04-1013/) (Lin, 2004) |
| Exact Match | Binary assessment of complete answer correctness | [Bootstrapping a neural natural language interface for databases](https://arxiv.org/abs/1908.07562) (Bogin et al., 2019) |
| F1 score | Harmonic mean of precision and recall | [Attention is all you need](https://arxiv.org/abs/1706.03762) (Vaswani et al., 2017) |

### Benchmarks

#### Early Foundational
| Name | Paper | Code | Description |
|------|-------|------|-------------|
| ToolLLM | [Toolllm: Facilitating large language models to master 16000+ real-world apis](https://arxiv.org/abs/2307.16789) (Qin et al., 2023) | [Code](https://github.com/OpenBMB/ToolBench) | Comprehensive benchmark for API utility |
| ToolAlpaca | [Toolalpaca: Generalized tool learning for language models with 3000 simulated cases](https://arxiv.org/abs/2306.05301) (Tang et al., 2023) | [Code](https://github.com/tangqiaoyu/ToolAlpaca) | Generalized tool learning with simulated cases |
| Gorilla | [Gorilla: Large language model connected with massive apis](https://arxiv.org/abs/2305.15334) (Patil et al., 2023) | [Code](https://github.com/ShishirPatil/gorilla) | Berkeley Function Calling Leaderboard |

#### Standardized Platforms
| Name | Paper | Code | Description |
|------|-------|------|-------------|
| APIBench | [Gorilla: Large language model connected with massive apis](https://arxiv.org/abs/2305.15334) (Patil et al., 2023) | [Code](https://github.com/ShishirPatil/gorilla) | Platform for standardized API evaluation |
| API-Bank | [Api-bank: A benchmark for tool-augmented llms](https://arxiv.org/abs/2304.08244) (Li et al., 2023) | [Code](https://github.com/AlibabaResearch/DAMO-ConvAI/tree/main/api-bank) | Comprehensive API interaction testing |

#### Domain-Specific
| Name | Paper | Code | Description |
|------|-------|------|-------------|
| ShortcutsBench | [Shortcutsbench: A large-scale real-world benchmark for api-based agents](https://arxiv.org/abs/2407.00132) (Shen et al., 2024) | [Code](https://github.com/MobileLLM/ShortcutsBench) | Real APIs from Apple's operating systems |
| BigCodeBench | [You are not alone: Large language models effectively leverage duplications in code corpus](https://arxiv.org/abs/2312.15201) (Zhou et al., 2023) | [Code](https://github.com/bigcode-project/bigcode-evaluation-harness) | Specialized benchmark for code-related function calls |
| SEAL | [Seal: A benchmark for software api learning with generative ai agents](https://arxiv.org/abs/2310.15177) (Ji et al., 2023) | [Code](https://github.com/google-deepmind/seal) | Software API learning benchmark |
| RadABench | [Radial agent benchmark: evaluating task generalization capabilities of multi-platform ai agents](https://arxiv.org/abs/2404.16765) (Yuan et al., 2024) | [Code](https://github.com/radial-inc/radabench) | Cross-platform agent evaluation framework |
| NoisyToolBench | [Learning to Ask: When LLMs Meet Unclear Instruction](https://arxiv.org/abs/2409.00557) (Wang et al., 2024) | [Code](https://github.com/CAISA-Lab/UnclearInstrLearningToAsk) | Evaluates performance with unclear or noisy instructions |
| Mobile-Bench | [Benchmarking large language models on mobile applications](https://arxiv.org/abs/2402.14136) (Cao et al., 2024) | [Code](https://github.com/mobile-app-bench/Mobile-Bench) | Specialized benchmark for mobile application interactions |

#### Task-Oriented
| Name | Paper | Code | Description |
|------|-------|------|-------------|
| IN3 | [In3: Instruction-following language models for interactive tasks](https://arxiv.org/abs/2311.09502) (Qi et al., 2023) | [Code](https://github.com/princeton-nlp/in3) | Interactive task evaluation with instruction following |
| NESTFUL | [NESTFUL: A Benchmark for Evaluating LLMs on Nested Sequences of API Calls](https://arxiv.org/abs/2409.03797) (Basu et al., 2024) | - | Focuses on nested sequences of API calls |
| UltraTool | [Pluto: A recipe for building adaptable autonomous llm agents](https://arxiv.org/abs/2402.04397) (Guan et al., 2024) | [Code](https://github.com/gpt4life/pluto) | Evaluates adaptable autonomous agent capabilities |
| AppWorld | [AppWorld: A Benchmark for Physical Mobile App Embodied Agent](https://arxiv.org/abs/2309.13090) (Tian et al., 2023) | [Code](https://github.com/X-LANCE/AppWorld) | Physical mobile app interaction benchmark |
| TheAgentCompany | [The agent company: A generative agent simulation of a software company](https://arxiv.org/abs/2404.01748) (Yuan et al., 2024) | - | Simulated software company environment for evaluation |
| AgentBoard | [AgentBoard: An Analytical Evaluation Board of Multi-turn LLM Agents](https://arxiv.org/abs/2308.03688) (Liu et al., 2023) | [Code](https://github.com/hkust-nlp/agentboard) | Multi-turn agent evaluation platform |
| TravelPlanner | [Travel planner: A benchmark for real-world planning with language agents](https://arxiv.org/abs/2402.01622) (Wang et al., 2024) | [Code](https://github.com/bellhello/travelplanner) | Travel planning task-specific benchmark |
| ChinaTravel | [Travel assistant: A benchmark for chinese llm agents in the tourism domain](https://arxiv.org/abs/2403.01502) (Xia et al., 2024) | - | Chinese language travel planning benchmark |

#### Comprehensive Systems
| Name | Paper | Code | Description |
|------|-------|------|-------------|
| API-BLEND | [API-BLEND: A Comprehensive Corpora for Training and Benchmarking API LLMs](https://arxiv.org/abs/2402.15491) (Basu et al., 2024) | [Code](https://github.com/IBM/API-Blend) | Multi-domain API coverage with evaluation methods |
| NESTOOLS | [Nestools: Crafting efficient tools across diverse scenarios](https://arxiv.org/abs/2402.07472) (Choi et al., 2024) | [Code](https://github.com/kyunghoon-han/NESTools) | Comprehensive evaluation across diverse scenarios |
| MTU-Bench | [MTU-Bench: A Multi-granularity Tool-Use Benchmark for Large Language Models](https://arxiv.org/abs/2410.11710) (Wang et al., 2024) | [Code](https://github.com/X-LANCE/MTU-Bench) | Multi-granularity tool-use evaluation |
| WTU-EVAL | [Web tool use evaluation: Measuring large language models' capabilities on realistic web tasks](https://arxiv.org/abs/2310.03220) (Mishra et al., 2023) | [Code](https://github.com/gpt-tool-use/WTU-Eval) | Web-based tool usage evaluation framework |


### Industry Products

#### Commercial Platforms
| Name | Organization | Release/Paper | Description |
|------|--------------|---------------|-------------|
| ChatGPT plugins | OpenAI | [Introducing ChatGPT plugins](https://openai.com/blog/chatgpt-plugins) | Ecosystem of third-party extensions for specific functionalities |
| Claude's tool use API | Anthropic | [Claude 3 Opus technical report](https://www-cdn.anthropic.com/de8ba9b01c9ab7cbabf5c33b80b7bbc618857627/Claude_3_Opus_Technical_Report.pdf) | Native function calling capabilities in Claude AI models |
| Cohere Command | Cohere | [Introducing Cohere Command Light](https://txt.cohere.com/command-light/) | API for function calling and structured JSON responses |
| Qwen | Alibaba | [Qwen Technical Report](https://arxiv.org/abs/2309.16609) (Yang et al., 2023) | Multi-function Chinese language models with tool usage |
| DeepSeek | DeepSeek | [DeepSeek: Generalized Autoregressive Pretraining for Language and Vision](https://arxiv.org/abs/2405.04434) (Dai et al., 2024) | Generalized foundation model with capabilities across tasks |

#### Frameworks & SDKs
| Name | Organization | Repository | Description |
|------|--------------|------------|-------------|
| HuggingFace Transformer Agents | Hugging Face | [Code](https://github.com/huggingface/transformers-agents) | Framework for building agents with Hugging Face models |
| Semantic Kernel | Microsoft | [Code](https://github.com/microsoft/semantic-kernel) | SDK for building AI applications with native tool integration |
| LangChain | LangChain | [Code](https://github.com/langchain-ai/langchain) | Framework for building applications with LLMs and tools |
| WebCPM | Tsinghua University | [Code](https://github.com/thunlp/WebCPM) | Chinese web agent framework with browsing capabilities |

#### Autonomous Agent Systems
| Name | Developer | Repository | Description |
|------|-----------|------------|-------------|
| Auto-GPT | Significant Gravitas | [Code](https://github.com/Significant-Gravitas/Auto-GPT) | Self-prompting autonomous agent system |
| BabyAGI | Yohei | [Code](https://github.com/yoheinakajima/babyagi) | Task-driven autonomous agent framework |
| BMTools | OpenBMB | [Code](https://github.com/OpenBMB/BMTools) | Toolset for enhancing language models with functions |
| RestGPT | Microsoft | [Code](https://github.com/Yifan-Song793/RestGPT) | Model that can interact with RESTful APIs |
| xLAM | Silen | [Code](https://github.com/xlang-ai/xlam) | Cross-language agent development framework |
| Octopus-v4 | Baichuan | [Octopus technical report](https://arxiv.org/abs/2311.02269) (Hao et al., 2023) | Multi-agent system for complex task completion |

#### Open Source Models
| Name | Developer | Repository | Description |
|------|-----------|------------|-------------|
| GRANITE-20B | IBM Research | [Code](https://github.com/IBM/granite) | Large language model optimized for coding and tool use |
| Mistral 7B | Mistral AI | [Code](https://github.com/mistralai/mistral-src) | Open-weight model with tool use capabilities |
| NexusRaven V2-13B | Nexusflow | [Code](https://github.com/nexusflowai/NexusRaven) | Function calling and multi-modality specialized model |
| Gorilla | UC Berkeley | [Code](https://github.com/ShishirPatil/gorilla) | Model specialized in API usage and integration |
| FireFunction V1 | Fireworks AI | [Model](https://huggingface.co/fireworks-ai/firefunction-v1) | Purpose-built for function calling capabilities |
| Nous Hermes 2 | Nous Research | [Model](https://huggingface.co/NousResearch/Nous-Hermes-2-Mixtral-8x7B-DPO) | Instruction-tuned model with enhanced tool use |

#### Training Resources & Datasets
| Name | Organization | Link | Description |
|------|--------------|------|-------------|
| AgentInstruct | Microsoft | [Paper](https://arxiv.org/abs/2312.03791) (Zeng et al., 2023) | Instruction dataset for agent training and evaluation |
| AgentOhana | Duke University | [Paper](https://arxiv.org/abs/2403.01092) (Yang et al., 2024) | High-quality dataset for training multi-task agents |
| Lumos | Cornell University | [Paper](https://arxiv.org/abs/2311.05657) (Guo et al., 2023) | Multi-step reasoning dataset for tool-based tasks |

## Open Issues

### Service Issues of Function Calling
- **Standards Challenge**: Lack of universally accepted standard for assessing quality and performance
- **Latency Problems**: High latency and low throughput affecting user experience
- **Security Vulnerabilities**: Potential for "jailbreak function" attacks and other security concerns

### Usability and Modification of Functions
- **Technical Costs**: Integration and maintenance costs for API modifications
- **System Architecture Limitations**: Constraints imposed by existing system architectures
- **Standardization Needs**: Requirement for standardized API modification processes

### Feedback Quality and Optimization
- **Complex Processing**: Multiple steps in feedback processing introducing errors
- **Learning Assessment**: Difficulty in quantifying effectiveness of human feedback
- **Strategy Requirements**: Need for advanced algorithms to interpret unstructured feedback

### Function Isolation and Post-Processing
- **Isolation Strategy**: Challenges in appropriately isolating functions for business needs
- **Regulatory Compliance**: Meeting specific regulatory requirements across functions
- **Post-processing Solutions**: Implementing effective middleware for compliance and data transformation


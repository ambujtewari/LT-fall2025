# STATS 700, Fall 2025

Since the release of OpenAI's o1 and DeepSeek's R1 models, interest in the reasoning capabilities of LLMs has increased. This half-semester (7-week) course will cover some of the main ingredients that go into enhancing an LLM's reasoning capability. We will also discuss some recent theory papers that try to understand this fascinating emerging area from a mathematical perspective.

Prior exposure to LLMs and learning theory will help but is not required. But a high level of mathematical maturity will be needed to fully benefit from this course. The topics list below is tentative and subject to change.

# Logistics
Time & Days: TuTh 2:30PM - 4:00PM  
Location: 2060 [SKB](https://maps.studentlife.umich.edu/building/school-of-kinesiology-building)  
Half semester course dates: Aug 25, 2025-Oct 10, 2025

# Topics

## Background (~ 2 weeks)

J&M = [Speech and Language Processing](https://web.stanford.edu/~jurafsky/slp3/) (3rd ed. draft)
by [Dan Jurafsky](http://web.stanford.edu/people/jurafsky/) and [James H. Martin](https://home.cs.colorado.edu/~martin/)

### LLMs
- Transformers, J&M Chapter 9 [annotated chapter](https://www.dropbox.com/scl/fi/n3b9qk371jxdiafmlgzey/9.pdf?rlkey=wmo5j2z20adsjg6cqm6r3ymok&st=s9d9pyov&dl=0)
- Large Language Models, J&M Chapter 10 [annotated chapter](https://www.dropbox.com/scl/fi/i2y21c1ihrdjqsh8s9t0e/10.pdf?rlkey=w21kuuhg5j1om4s7j0uvk3k6q&st=hl9zr433&dl=0)
- Model Alignment, Prompting, and In-Context Learning, J&M Chapter 12 [annotated chapter](https://www.dropbox.com/scl/fi/v2jtyiczxs0vt5mleu6vs/12.pdf?rlkey=p10o9jpvq6sws5j7fmuubm0ey&st=mexbje0m&dl=0)
- Since Section 12.7 (Model Alignment with Human Preferences) is missing in Chapter 12 above, we will refer to parts of the [RLHF book](https://rlhfbook.com/) being written by [Nathan Lambert](https://natolambert.com/), currently a post-training lead at the Allen Institute for AI.

### Reasoning LLMs
- [DeepSeek R1 Technical Report](https://arxiv.org/abs/2501.12948)
- [Sebastien Raschka's blog post](https://magazine.sebastianraschka.com/p/understanding-reasoning-llms)
- [(How) Do reasoning models reason?](https://nyaspubs.onlinelibrary.wiley.com/doi/pdf/10.1111/nyas.15339)
- [Reasoning Language Models: A Blueprint](https://ar5iv.labs.arxiv.org/html/2501.11223)
- [From System 1 to System 2: A Survey of Reasoning Large Language Models](https://ar5iv.labs.arxiv.org/html/2502.17419)

## Theory Papers (~ 5 weeks)

- [A Theory of Emergent In-Context Learning as Implicit Structure Induction](https://arxiv.org/pdf/2303.07971)
  - Two main results: (1) ICL abilities can arise if next-token pretraining is done on distributions with compositional structure. (2) Prompting an LLM to produce intermediate tokens can improve performance.
- [Chain of Thought Empowers Transformers to Solve Inherently Serial Problems](https://openreview.net/pdf?id=3EWTEy9MTM), ICLR 2024
  - With T steps of CoT, constant-depth transformers with constant-bit precision and logarithmic embedding size can solve any problem solvable by Boolean circuits of size T.
- [Scaling Test-Time Compute Without Verification or RL is Suboptimal](https://openreview.net/pdf?id=beeNgQEfe2), ICML 2025
  - Proves that verifier-based methods using RL/search dominate verifier-free methods based on distillation or cloning search traces, given fixed compute/data budgets.
- [Optimizing Test-Time Compute via Meta Reinforcement Finetuning](https://openreview.net/pdf?id=TqODUDsU4u), ICML 2025
  - Formalizes optimizing test-time compute as a meta-RL problem, offering guidance on how to optimally allocate inference-time computation.
- [On the Power of Context-Enhanced Learning in LLMs](https://openreview.net/pdf?id=Gn6L4QRKf7), ICML 2025
  - Proposes CEL, a variant of supervised fine-tuning where extra context is provided but gradients are not taken through it. In a simplified setting, shows CEL can be exponentially more sample-efficient than vanilla SFT for multi-step reasoning tasks.
- [Understanding Chain-of-Thought in LLMs through Information Theory](https://openreview.net/pdf?id=IjOWms0hrf), ICML 2025
  - Provides an information-theoretic framework that quantifies the “information gain” at each reasoning step.
- [A Theory of Learning with Autoregressive Chain of Thought](https://proceedings.mlr.press/v291/joshi25a.html), COLT 2025
  - Proposes a learning-theoretic framework where prompt-to-answer mapping is modeled as repeated application of a time-invariant “single-step” function. Considers both observed and latent CoT settings, showing sample complexity can be independent of CoT length, with attention arising naturally in the framework.
- [When More is Less: Understanding Chain-of-Thought Length in LLMs](https://arxiv.org/pdf/2502.07266)
  - Studies optimal CoT lengths, showing that longer is not always better: performance peaks at a sweet spot, then declines due to error accumulation.
- [Rethinking Fine-Tuning when Scaling Test-Time Compute: Limiting Confidence Improves Mathematical Reasoning](https://ar5iv.labs.arxiv.org/html/2502.07154)
  - Shows that Pass@N is misaligned with cross-entropy training. Proposes confidence-limiting objectives that improve performance on math and reasoning tasks.
- [On Learning Verifiers for Chain-of-Thought Reasoning](https://ar5iv.labs.arxiv.org/html/2505.22650)
  - Analyzes the PAC-learnability of verifiers for CoT reasoning. Derives sample-complexity upper bounds and impossibility results.
- [Is Chain-of-Thought Reasoning of LLMs a Mirage? A Data Distribution Lens](https://arxiv.org/pdf/2508.01191)
  - Argues that CoT gains are distribution-dependent and may vanish out-of-distribution, suggesting that CoT reasoning is brittle and not robustly general.

## Interesting Observations Waiting for Theoretical Analysis

- [Chain-of-Thought Reasoning Without Prompting](https://proceedings.neurips.cc/paper_files/paper/2024/file/7a8e7fd295aa04eac4b470ae27f8785c-Paper-Conference.pdf), NeurIPS 2024
- [Stop Anthropomorphizing Intermediate Tokens as Reasoning/Thinking Traces!](https://arxiv.org/pdf/2504.09762)
  - Poaition paper warning researchers against interpreting CoT tokens in human terms. One conclusion to draw from this position paper is that more work in needed in understanding how and when CoT traces help LLMs reason and plan. E.g.,
    - They might provide an extra "scratchpad" for the LLM to compute the final answer
    - They might enable exploration of reasoning paths of more depth and breadth
    - Training using CoT traces might help LLMs learn reusable skills and benefit from process supervision
    - Training using CoT traces might help LLM's training objective with test time metrics
    - How can we tell is CoT traces are helping? Or not helping?
    - If CoT traces could be trusted, they might provide ways to audit/critique/check/verify LLM solutions to reasoning problems
- [Reinforcement Learning for Reasoning in Large Language Models with One Training Example](https://arxiv.org/pdf/2504.20571)
- [Spurious Rewards: Rethinking Training Signals in RLVR](https://arxiv.org/pdf/2506.10947)


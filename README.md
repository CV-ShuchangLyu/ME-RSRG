<div align="center">
<h3> Think and Answer ME: Benchmarking and Exploring Multi-Entity Reasoning Grounding in Remote Sensing </h3>

  <p align="center">
    <a href='https://www.baidu.com'>
      <img src='https://img.shields.io/badge/Paper-PDF-green?style=flat&logo=arXiv&logoColor=green' alt='arXiv PDF'> </a>
    <a href='https://www.baidu.com'  style='padding-left: 0.5rem;'>
      <img src='https://img.shields.io/badge/Project-Page-blue?style=flat&logo=Google%20chrome&logoColor=blue' alt='Project Page'> </a>
    <a href='https://www.baidu.com' style='padding-left: 0.5rem;'>
      <img src='https://img.shields.io/badge/Hugging%20Face-Dataset-orange?logo=huggingface' alt='Dataset'>
  </p>
</div>


[Shuchang Lyu](https://scholar.google.com.hk/citations?user=SwGcxzMAAAAJ&hl=zh-TW), [Haiquan Wen](https://scholar.google.com/citations?user=hQadNAUAAAAJ), [Guangliang Cheng](https://scholar.google.com/citations?user=FToOC-wAAAAJ&hl=en), Meng Li, [Zheng Zhou](https://scholar.google.com/citations?user=L5o4LTcAAAAJ&hl=en&oi=sra), [You Zhou](https://scholar.google.com.hk/citations?user=dfEZDv4AAAAJ&hl=en), [Dingding Yao](https://scholar.google.com/citations?user=UrqQkEsAAAAJ&hl=zh-CN), [Zhenwei Shi](https://scholar.google.com.hk/citations?user=kNhFWQIAAAAJ&hl=en&oi=ao)


Welcome to our work **EAR**, for multi-entity reasoning grounding in remote sensing.

In this work, we propose:

> ✅ **One Dataset:** **ME-RSRG:** A new benchmark dataset for Multi-Entity Reasoning Grounding in Remote Sensing!
>
> ✅ **One Framework: EAR:** An Entity-Aware Reasoning framework based on visual-linguistic foundation models.
>
> ✅ **Two-Stage Optimization:** Combining supervised fine-tuning with entity-aware reward-driven GRPO.
>


## Abstract
Recent advances in reasoning language models and reinforcement learning with verifiable rewards have significantly enhanced multi-step reasoning capabilities. This progress motivates the extension of reasoning paradigms to remote sensing visual grounding task. However, existing remote sensing grounding methods remain largely confined to perception-level matching and single-entity formulations, limiting the role of explicit reasoning and inter-entity modeling. To address this challenge, we introduce a new benchmark dataset for Multi-Entity Reasoning Grounding in Remote Sensing (ME-RSRG). Based on ME-RSRG, we reformulate remote sensing grounding as a multi-entity reasoning task and propose an Entity-Aware Reasoning (EAR) framework built upon visual-linguistic foundation models. EAR generates structured reasoning traces and subject-object grounding outputs. It adopts supervised fine-tuning for cold-start initialization and is further optimized via entity-aware reward-driven Group Relative Policy Optimization (GRPO). Extensive experiments on ME-RSRG demonstrate the challenges of multi-entity reasoning and verify the effectiveness of our proposed EAR framework. Our dataset, code, and models will be available soon.

## Overview

<div align="left">
  <img src="Figs/Fig1.png" width="100%">
    <figcaption>
  <strong>(a) Matching-based visual grounding.</strong> Conventional approach focuses on aligning a single referring expression with one target subject.
  <strong>(b) Multi-entity reasoning grounding.</strong> Our proposed approach explicitly extracts multiple entities and produces structured reasoning-aware outputs for more interpretable understanding of complex remote sensing scenes.
</figcaption>
</div>

## Proposed Dataset: ME-RSRG

<div align="left">
  <img src="Figs/Fig2.png" width="100%">
    <figcaption>
  <strong>(a) Dataset production.</strong> The construction pipeline of ME-RSRG follows a 5-step process: dataset collection, instance selection, manual annotation, expert assessment, and CoT generation.
  <strong>(b) Dataset statics.</strong> ME-RSRG contains 7,162 images and 12,091 image-text instances, split into 10,305 training instances and 1,786 test instances.
  <strong>(c) Data case.</strong> Representative examples showing large-scale spatial layouts, multi-entity ambiguity, and structured reasoning requirements.
</figcaption>
</div>

### Dataset Production
ME-RSRG is constructed through a rigorous 5-step pipeline:
1. **Dataset Collection:** Collected from three benchmark RS visual grounding datasets: RSVG-HR, DIOR-RSVG, and OPT-RSVG.
2. **Instance Selection:** Used Gemini-2.5-Pro to filter expressions containing explicit subject-object structures and multiple entities.
3. **Manual Annotation:** Inherited original bounding box annotations and language descriptions, then identified and labeled corresponding object entities.
4. **Expert Assessment:** Domain experts conducted strict quality review of annotations.
5. **CoT Generation:** Generated reasoning traces for ~20% of the training set using Gemini-2.5-Pro.

### Dataset Analysis
- **Size:** 7,162 images and 12,091 image-text instances
- **Split:** 10,305 training instances (6,028 images) and 1,786 test instances (1,134 images)
- **CoT Annotations:** 2,149 training instances with explicit <think>...</think> reasoning tags
- **Challenges:** Large-scale spatial layouts, multi-entity ambiguity, and structured reasoning requirements

## Proposed Method: EAR Framework

<div align="left">
  <img src="Figs/Fig3.png" width="100%">
    <figcaption>
  <strong>Overview of EAR framework.</strong> We adopt a two-stage optimization strategy. SFT is first applied as a cold-start initialization. With SFT-parameters loaded to policy model, entity-aware reward-driven GRPO is then employed to further refine the model.
</figcaption>
</div>

### Entity-Aware Reward Model
The core component of EAR is an Entity-Aware Reward model consisting of three components:
1. **Two-level format reward:** Ensures structured reasoning and answer outputs.
2. **Entity-aware grounding accuracy reward:** Evaluates subject and object localization separately.
3. **Relational consistency reward:** Assesses the coherence of predicted inter-entity relations.

### Optimization Strategy
EAR adopts a two-stage optimization approach:
1. **Stage I: Supervised Fine-Tuning (SFT):** Initializes the policy model with structured reasoning capability using CoT-annotated samples.
2. **Stage II: Entity-Aware Reward-Driven GRPO:** Refines the model through entity-aware rewards that explicitly evaluate grounding correctness for different entity roles.

## Experimental Results

### Performance on ME-RSRG Dataset

| Methods (policy models) | Baseline |  |  | SFT |  |  | EAR |  |  |
|-------------------------|----------|---|---|-----|---|---|-----|---|---|
|                         | sub.     | obj.| mean| sub.| obj.| mean| sub.| obj.| mean|
|-------------------------|----------|---|---|-----|---|---|-----|---|---|
| **Qwen-VL series**      |          |    |    |     |    |    |     |    |    |
| Qwen2-VL-2B             | 1.40     | 1.15| 1.27| 23.18| 23.08| 23.13| 27.55| 22.93| 25.16|
| Qwen2.5-VL-3B           | 7.45     | 10.81| 9.18| 27.04| 30.43| 28.79| 38.63| 42.08| 40.41|
| Qwen2.5-VL-7B           | 11.31    | 9.44| 10.35| 31.75| 34.84| 33.34| **44.40**| **48.90**| **46.72**|
| Qwen3-VL-4B             | 20.95    | 13.80| 17.25| **36.39**| **35.89**| **36.13**| 38.52| 36.83| 37.65|

### Key Findings
- **EAR Framework Effectiveness:** With optimization under the EAR framework, the Qwen2.5-VL series achieves over 10% improvement in mAcc@0.5 value.
- **Consistent Gains:** All evaluated visual-linguistic foundation models show consistent gains when optimized with the EAR framework.
- **Best Performance:** Qwen2.5-VL-7B in the EAR framework achieves the best performance with mAcc@0.5 of 46.72%.

## Contributions
1. **ME-RSRG Dataset:** A new and challenging benchmark dataset for multi-entity reasoning grounding in remote sensing, explicitly modeling multiple entities and their semantic roles.
2. **EAR Framework:** An Entity-Aware Reasoning framework based on visual-linguistic foundation models, integrating supervised fine-tuning and entity-aware reward-driven GRPO.
3. **Comprehensive Benchmarking:** Extensive experiments verifying the effectiveness of EAR in structured relational grounding, with consistent performance gains across different foundation models.


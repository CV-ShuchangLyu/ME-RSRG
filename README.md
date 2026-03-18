<div align="center">
<h3> Think and Answer ME: Benchmarking and Exploring Multi-Entity Reasoning Grounding in Remote Sensing </h3>

  <p align="center">
    <a href='https://arxiv.org/abs/2603.12788'>
      <img src='https://img.shields.io/badge/Paper-PDF-green?style=flat&logo=arXiv&logoColor=green' alt='arXiv PDF'> </a>
    <a href='https://github.com/CV-ShuchangLyu/ME-RSRG'  style='padding-left: 0.5rem;'>
      <img src='https://img.shields.io/badge/Project-Page-blue?style=flat&logo=Google%20chrome&logoColor=blue' alt='Project Page'> </a>
    <a href='https://github.com/CV-ShuchangLyu/ME-RSRG' style='padding-left: 0.5rem;'>
      <img src='https://img.shields.io/badge/Hugging%20Face-Dataset-orange?logo=huggingface' alt='Dataset'>
  </p>
</div>


[Shuchang Lyu](https://scholar.google.com.hk/citations?user=SwGcxzMAAAAJ&hl=zh-TW), [Haiquan Wen](https://scholar.google.com/citations?user=hQadNAUAAAAJ), [Guangliang Cheng](https://scholar.google.com/citations?user=FToOC-wAAAAJ&hl=en), [Meng Li](https://scholar.google.com/citations?hl=zh-CN&user=wlI9uTYAAAAJ), [Zheng Zhou](https://scholar.google.com/citations?user=L5o4LTcAAAAJ&hl=en&oi=sra), [You Zhou](https://scholar.google.com.hk/citations?user=dfEZDv4AAAAJ&hl=en), [Dingding Yao](https://scholar.google.com/citations?user=UrqQkEsAAAAJ&hl=zh-CN), [Zhenwei Shi](https://scholar.google.com.hk/citations?user=kNhFWQIAAAAJ&hl=en&oi=ao)


Welcome to our work **EAR**, for multi-entity reasoning grounding in remote sensing.

In this work, we propose:

> ✅ **One Dataset:** **ME-RSRG:** A new benchmark dataset for Multi-Entity Reasoning Grounding in Remote Sensing!
>
> ✅ **One Framework: EAR:** An Entity-Aware Reasoning framework based on visual-linguistic foundation models.
>
> ✅ **Two-Stage Optimization:** Combining supervised fine-tuning with entity-aware reward-driven GRPO.
>

## Proposed Dataset: ME-RSRG

<div align="left">
  <img src="Figs/Fig1.png" width="100%">
    <figcaption>
  <strong>(a) Dataset production.</strong> The construction pipeline of ME-RSRG follows a 5-step process: dataset collection, instance selection, manual annotation, expert assessment, and CoT generation.
  <strong>(b) Dataset statics.</strong> ME-RSRG contains 7,162 images and 12,091 image-text instances, split into 10,305 training instances and 1,786 test instances.
  <strong>(c) Data case.</strong> Representative examples showing large-scale spatial layouts, multi-entity ambiguity, and structured reasoning requirements.
</figcaption>
</div>

## Proposed Method: EAR Framework
<div align="left">
  <img src="Figs/Fig2.png" width="100%">
    <figcaption>
  <strong>Overview of EAR framework.</strong> We adopt a two-stage optimization strategy. SFT is first applied as a cold-start initialization. With SFT-parameters loaded to policy model, entity-aware reward-driven GRPO is then employed to further refine the model.
</figcaption>
</div>

## News 🔥🔥
[2026-03-17] The original version of our proposed ME-RSRG is released!! [google drive](https://drive.google.com/file/d/1GRrDBYmYr0IuLXENR5ZmXmvswjcY0SEI/view?usp=drive_link)

[2026-03-16] The arxiv version of our paper is released!! [ArXiv paper] (https://arxiv.org/abs/2603.12788)

[TBD] We plan to release the hf/modelscope version ME-RSRG Dataset soon.

## Datasets: ME-RSRG
The original dataset contains the original images and annotations (.xml).

* For each folder (rsvg_hr, dior_rsvg, opt-rsvg), we provide list (.txt) in ''Annotations'' folder
* In experiments, the ''train'' and ''val'' sets are merged for training while the ''test'' set is used for testing.
* The ''train_with_think'' set provides the instances with ''\<think\>\</think\>'' tags. This set is used in SFT stage.
* The instances of ''train_with_think'' is a sub-set of ''train'' set, which means the instances in ''train_with_think''(removing \<think\> tags) are also used in GRPO stage 

## Please Cite
```
@misc{lyu2026thinkanswermebenchmarking,
      title={Think and Answer ME: Benchmarking and Exploring Multi-Entity Reasoning Grounding in Remote Sensing}, 
      author={Shuchang Lyu and Haiquan Wen and Guangliang Cheng and Meng Li and Zheng Zhou and You Zhou and Dingding Yao and Zhenwei Shi},
      year={2026},
      eprint={2603.12788},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2603.12788}, 
}
```

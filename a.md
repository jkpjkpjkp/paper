# 引言

Former research highlights the inaccuracies in visual-grounding (vision-perception) in large multimodal models (LMMs) [BLINK, Eyes-wide-shut, Cambrian]. While LMMs are the SOTA way of visual question answering (VQA), due to this visual perception bottleneck, even today's SOTA LMMs cannot accurately count past a dozen objects. 

Our first motivation is to emulate a human VQA process, where human may continually focus on related areas, taking longer gaze at related areas for more accurate perception, we hypothesize that a inference-time LMM workflow can have a similar effect and lead to better visual perceptive performance. 

Another line of work sparkling in [FunSearch] and propspered recently into [ADAS, AFlow] seeks to optimize llm workflows automatically, offering a second motivation to our work. 

Our work first tries to improve LMM's visual perception using a hand-crafted agentic system, and secondly use LMM to automatically optimize LMM workflows that answer vqa questions. Experiments on the challenging Zerobench-subtasks dataset showed improved results. 



# 文献综述

## Vision-Language Models
Vision-only models (SAM, Depth-anything; image-to-3d, 3d-pointcloud methods; computational photography), vision-focused models such as detection (GroundingDINO, OwlV2, FlorenceV2) and language-focused models (LMMs). To bridge this vision-language (say-what-you-see) gap, works such as semantic segmentation (Seg-Zero 2503.06520) and counting (CountGD) succeeds on specific vision-centric tasks. 
Early efforts of fusing these models include Set-of-Mask prompting, eliciting abilities in SAM to help VLM. 


## Improving LMM's visual perception
[V*: Guided Visual Search] use reference objects (choose reference based on common-sense, e.g. cups are usually near a table) to guide a detection model to zoom in to find object of interest. 

[Eyes-wide-shut] 
[some paper stating the hallucination comes from focusing on text token]

## ADAS

Recently, a stream of work (ADAS, AFlow) seeks to optimize llm workflows automatically. This leads us to presume a similar llm-driven tree search optimization can lead to a synergetic VQA workflow combining strengths of the aforementioned 3 families of v-l models. 

## Tree search and effective workflow in pure-text setting


# 手工设计的方法

## 启发
通过使用没有视觉的LLM，forcing it to split visual perception into multiple smaller steps, to bypass the limitation of visual hallucination. 

## 算法
我们使用没有视觉的LLM（deepseek v3），通过调用工具回答vqa问题。工具池包括VLM（glm-4v-plus）、Grounding(Grounding_Dino和Owl_v2)、SAM2(Segment Anything)、Depth Anything v2。仅依靠较弱的VLM和Grounding，LLM可以在MuirBench的Counting子任务超过领先的VLM，包括GPT-4o。

具体地，

## 实验

### Dataset:
MuirBench focuses on robust multi-image understanding capabilities of multimodal LLMs. Its `Counting` subtask requires semantic counting beyond the capabilities of grounding models (e.g. How many pandas is standing on wood logs?) 

### Baseline:
GPT-4o: 49.15%
GLM-4v-plus (the vlm we use in our pipeline): TODO: 10 tasks 0%, need to look into


# 自动生成的方法

## Method

in each round, we run the 3 strongest graph, run each 5 tasks from select_task (see below) (3x5 runs), then pick the strongest overall graph to optimize. this is different from Aflow (see related works)(TODO: Ablation needed)

in accordance to Aflow, we keep a record of what modifications have already been explored for the current graph, so as to avoid duplicated efforts treading down the same path of optimization. 

## Design Details

### less experimenting
since image tasks are more token-expensive than text tasks, we test the graphs restrainedly. specifically, only 5 runs of the graph are conducted at each optimization step, gaining a randomized view of the graph's performance. 

### select high-variance tasks
randomly pick high-variance tasks (task whose score average among graphs is close to 0.5). this is self-stabilizing to prioritize indicative tasks, as when the graphs become stronger, harder tasks become closer to have a 50% chance of being solved. 



## 实验

### Implementation details:
We use different model for workflow execution and optimization. 

## 消融


# 结论
我们确定了AFlow用于VQA也可以生成优于baseline的方法。gs






# Appendix

## Synergizing Grounding_Dino (G_Dino) and Owl_v2

the 2 strongest open weights open vocabulary grounding models have an interestingly distinctive design on when to merge the modalities. 

G_Dino merges vision and language very early, enabling vision encoder to focus on objects of interest, leading to superior bounding box IoU. Owl_v2 does this much later in pipeline, leading to reduced halucination. 

By applying a de-hallucination filter (use G_Dino bboxes, but keep only labels that are also detectable by Owl_v2). 

We also applied a heuristic bbox deduplication process. 
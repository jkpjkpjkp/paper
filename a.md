# 引言
A series of work including Eyes-Wide-Shut highlights large motimodal model(lmm)s' limited accuracy in visual perception. While they are the SOTA way of visual question answering (VQA), their design and training process limits their visual perception to within a ~200 token per image span, which cannot capture fine details or all relationships in complex images. A demonstration of which is that today's SOTA LMMs still cannot count accurately even a dozen objects. 

To emulate a human VQA process, where human may continually focus on related areas, taking longer gaze at related areas for more accurate perception, we hypothesize that a inference-time LMM workflow can have a similar effect and lead to better visual perceptive performance. 

This work uses LMM to automatically optimize LMM workflows that answer vqa questions. Experiments on the challenging Zerobench-subtasks dataset showed improved results. 



# 文献综述

## Vision-Language Models
Vision-only models (SAM, Depth-anything; image-to-3d, 3d-pointcloud methods; computational photography), vision-focused models such as detection (GroundingDINO, OwlV2, FlorenceV2) and language-focused models (LMMs). To bridge this vision-language (say-what-you-see) gap, works such as semantic segmentation (Seg-Zero 2503.06520) and counting (CountGD) succeeds on specific vision-centric tasks. 
Early efforts of fusing these models include Set-of-Mask prompting, eliciting abilities in SAM to help VLM. 


## Halucination in LVLM

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


# 自动生成的方法

## 对Aflow的改动（方法）

## 实验

## 消融


# 结论
我们确定了AFlow用于VQA也可以生成优于baseline的方法。gs
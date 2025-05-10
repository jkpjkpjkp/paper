Among vision-language related foundation models there are 3 genre, namely vision-only models (SAM, Depth-anything; image-to-3d, 3d-pointcloud methods; computational photography), vision-focused models such as detection (GroundingDINO, OwlV2, FlorenceV2) and language-focused models (LMMs). To bridge this vision-language (say-what-you-see) gap, works such as semantic segmentation (Seg-Zero 2503.06520) and counting (CountGD) succeeds on specific vision-centric tasks. 


Early efforts of fusing these models include Set-of-Mask prompting, 

Many efforts focus on agentic image generation (ImageRAG 2502.09411v1); not so many on agentic visual perception. 

Recently, a stream of work (ADAS, AFlow) seeks to optimize llm workflows automatically. This leads us to presume a similar llm-driven tree search optimization can lead to a synergetic VQA workflow combining strengths of the aforementioned 3 families of v-l models. 
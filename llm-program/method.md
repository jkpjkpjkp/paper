我们使用没有视觉的LLM（deepseek v3），通过调用工具回答vqa问题。工具池包括VLM（glm-4v-plus）、Grounding(Grounding_Dino和Owl_v2)、SAM2(Segment Anything)、Depth Anything v2。仅依靠较弱的VLM和Grounding，LLM可以在MuirBench的Counting子任务超过领先的VLM，包括GPT-4o。

具体地，
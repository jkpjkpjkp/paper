## Combining strengths of G_Dino and Owl_v2

the 2 strongest open weights open vocabulary grounding models have an interestingly distinctive design on when to merge the modalities. 

G_Dino merges vision and language very early, enabling vision encoder to focus on objects of interest, leading to superior bounding box IoU. Owl_v2 does this much later in pipeline, leading to reduced halucination. 

By applying a de-hallucination filter (use G_Dino bboxes, but keep only labels that are also detectable by Owl_v2). 

We also applied a heuristic bbox deduplication process. 


## Failed attempts

crop-spawn. 
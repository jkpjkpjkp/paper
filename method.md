
since image tasks are more token-expensive than text tasks, we test the graphs restrainedly. specifically, only 5 runs of the graph are conducted at each optimization step, gaining a randomized view of the graph's performance. 



### select_task()
randomly pick high-variance tasks (task whose score average among graphs is close to 0.5). this is self-stabilizing to prioritize indicative tasks, as when the graphs become stronger, harder tasks become closer to have a 50% chance of being solved. 

for fair comparison, we pick the 3 strongest graph, run each on 5 tasks (3x5 runs), then pick the strongest overall graph. 


in accordance with Aflow, we keep a record of what modifications have already been explored for the current graph, so as to avoid duplicated efforts treading down the same path of optimization. 
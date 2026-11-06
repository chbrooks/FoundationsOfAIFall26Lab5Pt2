### Lab 5, part 2: Bayesian Networks and HMMs

#### Due Nov 17, 11:59pm

In this lab, you'll work with pre-built models of Bayesian Networks and Hidden Markov Models
to understand their behavior and how to use them for inference. 

You should add a PDF containing all of your answers in this repo and commit and push it.

Part 2a: Bayesian Networks. 

To begin, load the Wildfire Ignition Network into your browser. 

**Getting started**

Question 1. Without any observations, what variable is most likely to be true? What variable is the least likely to be true?

Question 2: Look at the Fire Ignited CPT. Which cause is more likely to start a fire - Lightning, or Line Spark? 
What happens when both occur at once?

**Reasoning from Causes to Effects. (predictive reasoning)**

Question 3: Set Storm season to true. Which nodes move, and which show “no change”?

Question 4: Clear the evidence and set Aging grid to true instead. Which nodes move this time? 
Which nodes moved in both cases, and why?

**Reasoning from Effects to Causes (Diagnostic Reasoning)**

Question 5: Set Smoke spotted to true. Which node moves the most? 
Do both root causes (Storm season and Aging grid) move?

**Explaining Away** 

Question 6:  Set Fire ignited to true and note P(Line spark). Then set Lightning strike to true. 
What happens to Line spark, and why?

Question 7: Now cycle Lightning strike to false. What happens to Line spark now?

Question 8: Above, Aging grid also changed, even though it’s two steps from Lightning strike. Why?

**D-separation**

An advantage of graphical representations is that the graph alone tells you whether new evidence can move a variable.
Use these rules on each path between the two nodes:

- Chain (A → B → C) or fork (A ← B → C): the path is blocked if B is observed.
- Collider (A → B ← C): the path is blocked unless B, or something downstream of B, is observed.
- X and Y are d-separated given the evidence if every path between them is blocked. Then observing X cannot change Y.

Question 9: For each row, write your prediction and the path that decides it before touching the page. 
Then set the first evidence, click the second node to true, and read whether the watched node moved.

| # | First set (true) | Then observe (true) | Watch | Predict: does it move? | Deciding path | Page result |
| --- | --- | --- | --- | --- | --- | --- |
| C1 | nothing | Storm season | Aging grid | | | |
| C2 | Smoke spotted | Storm season | Aging grid | | | |
| C3 | Smoke spotted, Line spark | Storm season | Aging grid | | | |
| C4 | Fire ignited | Lightning strike | Smoke spotted | | | |
| C5 | nothing | Smoke spotted | Large wildfire | | | |
| C6 | Fire ignited | Smoke spotted | Large wildfire | | | |
| C7 | nothing | Overgrown brush | Smoke spotted | | | |
| C8 | Aging grid | Overgrown brush | Smoke spotted | | | |
| C9 | Large wildfire | Overgrown brush | Lightning strike | | | |
| C10 | Fire ignited | Overgrown brush | Lightning strike | | | |
| C11 | Fire ignited | Storm season | Large wildfire | | | |
| C12 | Line spark | Aging grid | Smoke spotted | | | |


**Same structure, different story**

Now look at the Crop Failure network. It has the same graph structure as the wildfire network, 
but with different variables and different numbers. Each node maps one to one.

Question 10: Repeat questions 3-8 with the Crop Failure Network. 
What results are the same between the two networks, and what are different?


### Part 2b: Hidden Markov Models. 

For this portion of the lab, we'll work with the Overnight Fire HMM model. Load that into a web browser to begin.

**Getting oriented**

Question 1: Before looking at any probabilities, read the two rows of sensor readings. When do you think the fire started? 

Question 2: The page shows three answers for the fire: forward, smoothed and Viterbi. In your own words, what information does each one use?

Question 3: Find the first hour where forward P(burning) goes above 0.5. Is that before, after or the same as your guess?

**Forward vs Smoothing**

Question 4. At hour 2 there’s a single hotspot. Compare forward and smoothed P(burning) there. 
Which would a dispatcher have seen at hour 2? Why does smoothing discount that hotspot?

Question 5. At hour 9 there’s no hotspot, even though hotspots appear before and after it. 
What happens to forward P(burning) at hour 9? What happens to smoothed? Explain the difference.

Question 6. Look at hour 7. Smoothed P(burning) is noticeably higher than forward. 
Which later readings cause that?

**Viterbi**

Question 7. According to Viterbi, in which hour did the fire start, and in which hour did the fuel turn dry?

**Hidden Variables**

Question 8. Click hour 8 to open the joint state panel. Which of the four combined states is most likely under forward? Under smoothing? Which one does Viterbi pick?

Question 9. Pick the Humidity stays normal preset. Compare forward P(burning) at hours 8 to 10 with the original readings. Why does humidity matter?

Question 10. Remove the hotspots at hours 10, 11 and 12. Does smoothing still believe there was a fire at hours 8 and 9?

**Change the model**

Question 11. Lower “Hotspot | not burning” (the false alarm rate) to 0.01, then raise it to 0.2. What happens to the hour 2 spike in each case?

Question 12. Set “Burning keeps burning” to 0.5, so fires often go out. How does the hour 9 missed detection look now under smoothing?

Question 13. A dispatcher deciding whether to send a crew, an investigator writing a report, and a court asking for one clear timeline each need 
a different answer. Which algorithm fits each, and why?


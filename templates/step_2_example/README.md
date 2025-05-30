### Control Flow Analysis Results:
- withdraw() execution path: requires phase==1 condition
- invest() state transitions: 
  * Path 1: invested < goal → phase = 0
  * Path 2: invested >= goal → phase = 1
- refund() state effects: invested -= invests[msg.sender]

### Function Combination Enumeration:
1. [invest] → Analysis: single call sets phase=0, cannot reach withdraw bug
2. [invest, invest] → Analysis: 
   * First invest: invested = donations, phase = 0
   * Second invest: if (invested + donations >= goal) → phase = 1 -- CHECKED
3. [invest, refund] → Analysis:
   * invest: invested += donations
   * refund: invested -= invests[msg.sender] (resets effect) -- CHECKED
4. [invest, refund, invest] → Analysis: offsetting nullifies first invest
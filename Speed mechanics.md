
# Speed mechanics
**This document explains the speed mechanics of the game in depth. Speed is a new stat to the series introduced in this game, supposedly affecting accuracy and evasion, but no one ever knew how by how much. It just felt like moves were missing all the time for no reason compared to the earlier games in the series.**

## Mechanics explanation

First, the game looks at the ratio of the speed between the attacker and the defender for 5 thresholds: 2.0, 1.5, 0.5, 0.3 and 0.0. The game picks the first one that your ratio is higher than.

Then, it chooses a corresponding accuracy stage multiplier to add to the current accuracy stage (min 0, default 15, max 30). These are, respectively: +5, +2, +0, -2, -5.

Assuming neutral accuracy stage of 15 as the starting point, these result in the following accuracy modifiers: 109%, 100%, 95%, 86%, 67%. This gets multiplied with the accuracy of the move itself and then the evasion stages of the enemy to obtain the final result. Notice how you have a 95% modifier by default.

But that's not all! My watchpoint for reading the speed stat was firing off twice whenever a move hit. That's suspicious. I tried to figure out what that code was doing, assuming it was related to evasion stages, but it really didn't seem to affect them. Instead, I noticed that my attack stat and move power were present in those calculations. Changed the multiplier and sure enough, I dealt 999 damage. So speed affects damage too, who knew. Though it's very minor as it only acts as a multiplier for your move power, like the space globe in Explorers of Sky.

The damage calculation for speed uses a similar mechanism, where the thresholds are 2.0, 1.6, 1.3, 0.5 and 0.0 with _move power_ multipliers of 1.4, 1.2, 1.1, 1.0 and 0.8, respectively.

## Full accuracy and evasion stage tables

| Stage | Accuracy hit rate modifier | Evasion hit rate modifier |
|--|--|--|
|-15  | 0.40 |N/A|
|-14  | 0.44 |N/A|
|-13  | 0.45 |N/A|
|-12  | 0.47 |N/A|
|-11  | 0.49 |N/A|
|-10  |  0.51|2.0|
|-9  | 0.53 |1.90
|-8  | 0.55 |1.85
|-7  | 0.59 |1.80
|-6  | 0.62 |1.75
|-5  | 0.67 |1.70
|-4  | 0.73 |1.65
|-3  | 0.80 |1.60
|-2  | 0.86 |1.50
|-1  | 0.91 |1.35
|0  | 0.95 |1.00
|+1 | 0.98 |0.80
|+2 | 1.00 |0.70
|+3 | 1.03 |0.60
|+4 | 1.06 |0.50
|+5 | 1.09 |0.40
|+6 | 1.12 |0.35
|+7 | 1.15 |0.30
|+8 | 1.20 |0.25
|+9 | 1.25 |0.20
|+10 | 1.30 |0.15
|+11 | 1.35 |N/A|
|+12 | 1.4 |N/A|
|+13 | 1.5 |N/A|
|+14 | 1.8 |N/A|
|+15 | 2.0 |N/A|


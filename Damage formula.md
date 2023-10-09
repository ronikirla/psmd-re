
# Speed mechanics
**This document explains the damage formula of the game in depth. For the most part the damage formula of this game seems to be a pretty typical additive PMD damage formula. However, it has some weird quirks.**

## Formula breakdown

`max(1,floor(((attack_power - defense / 4) * type_modifier * level_modifier * rng + 0.4) * attack_stage_modifier * defense_stage_modifier)) * post_modifiers`

Where:

`attack_power = (attack + move_power * speed_modifier) * some_modifier`

`speed_modifier` is explained in [my speed mechanics breakdown](Speed%20mechanics.md)\
`some_modifier` was always 1 in my testing but had for example a conditional for 0.85 for physical attacks specifically, could be burn etc.?

`type_modifier = stab * type_1 * type_2 * 0.925^4` normally\
`                1` in an NVE alliance

`stab = 1.2` if applicable, `1` otherwise\
ineffective: `0`\
not very effective: `0.81`\
regular effective: `0.925`\
super effective: `1.1`

This part makes very little sense, but it also explains why NVE alliances are super powerful. For some reason the regular effective multiplier is below 1 and not only that but the game basically checks for these multipliers six times, despite there only being two types. I have no idea why, I didn't find any case where those multipliers would be anything other than regular effective, hence the 0.925^4. This causes the type multiplier to always be significantly below 1, so NVE alliances just straight up setting the value to 1 cause the insane damage boost. Also it renders stab irrelevant.

`level_modifier = 1.0 + floor((user_level - target_level) / 10) * 0.1`

Level is pretty important, as it adds a mulitplier bonus, which is rare in PMD where most things are additive. And it matters defensively too! Actually way more than defense. Defense is pretty useless in this game as it gets divided by 4.

`rng = random range from 0.875 to 1.125`

`attack_stage_modifier` and `defense_stage_modfifer`:

See table below. These were pretty much already known empirically but here they are. Notable is the difference in the first stages in defense and diminishing returns after. Attack is similar, but to a lesser extent.

`post_modifiers` are applied after rounding in another function. I didn't look very deep into these, but it looks like it has at least a 1.4x modifier for crits and it also has the multipliers for moves like Electro Ball and Gyro Ball.

## Extra findings

- Power boost X/Y are applied as a +1 attack stage boost for each emera. Having both X+Y gives +2 accuracy stages, meaning in the typical case with evenly matched speed it brings your base accuracy to 100% from 95%.
- Guard boost similarly gives +1 defense stage per emera.

## Full attack and defense stage tables

| Stage | Attack damage modifier | Defense damage modifier |
|--|--|--|
|-10 |  0.37|2.35|
|-9  |  0.39|2.30|
|-8  |  0.41|2.20|
|-7  |  0.43|2.10|
|-6  |  0.45|2.00|
|-5  |  0.50|1.90|
|-4  |  0.55|1.80|
|-3  |  0.60|1.70|
|-2  |  0.67|1.60|
|-1  |  0.75|1.50|
| 0  |  1.00|1.00|
|+1  |  1.35|0.55|
|+2  |  1.50|0.45|
|+3  |  1.60|0.40|
|+4  |  1.70|0.35|
|+5  |  1.90|0.30|
|+6  |  2.00|0.25|
|+7  |  2.10|0.20|
|+8  |  2.20|0.15|
|+9  |  2.30|0.13|
|+10 |  2.35|0.10|


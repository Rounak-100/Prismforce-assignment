# Abhimanyu in the Chakravyuha Problem
## Problem Statement
Abhimanyu is trapped in a Chakravyuha, a complex battle formation with 11 concentric circles, each guarded by an enemy. Abhimanyu starts in the innermost circle with an initial power `p` and must cross all the circles to reach the Pandavas' army.

### Given:
- Each circle is guarded by an enemy with power levels `k1, k2, ..., k11`.
- Abhimanyu has a boon to skip fighting an enemy `a` times.
- Abhimanyu can recharge himself with full power `b` times.
- Battling an enemy results in a loss of power equal to the enemy's power level.
- If Abhimanyu's power drops below the enemy's power level when entering a circle, he loses the battle.
- Enemies in the 3rd and 7th circles can regenerate once with half their initial power and attack Abhimanyu from behind if he is battling in the next circle.

### Goal:
Determine if Abhimanyu can cross all 11 circles and reach the Pandavas' army.

## Solution Approach
To solve this problem, we use a dynamic programming (DP) approach combined with recursion. The DP approach helps in optimizing the solution by storing intermediate results to avoid redundant calculations.

### Dynamic Programming Approach:
#### DP Table:
We maintain a 5-dimensional DP table `dp[circleIndex][remainingPower][a][b][isPrevSkipped]` where:

- `circleIndex`: Current circle index (0 to 10).
- `remainingPower`: Abhimanyu's remaining power after previous battles.
- `a`: Number of skips remaining.
- `b`: Number of recharges remaining.
- `isPrevSkipped`: Boolean flag indicating if the previous circle was skipped.

#### Recursive Function:
- **Base Case:** If `circleIndex == levelCount` (all circles crossed), return true.
- **Memoization Check:** Before computing, check if the current state is already computed in the DP table. If yes, return the stored result.
- **Power Calculation:** Calculate the power needed to defeat the current enemy, including any additional power required if the previous circle's enemy regenerates and attacks from behind (for circles 3 and 7).
- **Three Possible Actions:**
    - **Defeat the enemy:** If Abhimanyu's power is sufficient, move to the next circle after reducing power.
    - **Skip the circle:** If skips are available, skip the current circle and move to the next one.
    - **Recharge and fight:** If recharges are available, recharge to full power and fight the enemy.
- **Store Result:** Save the result in the DP table and return the final decision.

## Time Complexity
#### Time Complexity: $$O(n * p * a * b * 2)$$

- `n` is the number of circles (11)
- `p` is the initial power
- `a` is the number of skips
- `b` is the number of recharges.

This ensures that each state is only computed once.

## Space Complexity
### Space Complexity: $$O(n * p * a * b * 2)$$ 
due to the size of the DP table.

## Example Execution
### Test Case 1
```
p: 50
a: 2
b: 1
k: 46 5 4 10 9 8 6 1 40 30 20

Expected Output: YES
```

#### Explanation: 
- **Circle 1 (Enemy Power = 46) :** Abhimanyu can skip this circle (1 skip used, 1 remaining).

- **Circle 2-8 :** Abhimanyu defeats this enemy, reducing his power to 2.

- **Circle 9 (Enemy Power = 40) :** bhimanyu can skip this circle (1 skip used, 0 remaining).
Abhimanyu recharges (1 recharge used, 0 remaining), restoring his power to 50, and defeats the enemy.

- **Circle 10 (Enemy Power = 30) :** Abhimanyu recharges (1 recharge used, 0 remaining), restoring his power to 50, and defeats the enemy.

- **Circle 11 (Enemy Power = 20) :** With enough remaining power, Abhimanyu defeats the final enemy.

Therefore, Abhimanyu successfully crosses all circles, resulting in the output `YES`.

### Test Case 2
```
p: 150
a: 2
b: 2
k: 110 100 90 80 70 60 50 40 30 20 10

Expected Output: NO
```
#### Explanation: 
Even with available skips and recharges, Abhimanyu’s power is insufficient to defeat all enemies.

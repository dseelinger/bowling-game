# bowling-game

## Steps

1. Create a "project" named BowlingGame
2. Create a unit test file named BowlingGameTest
3. Create the test "Gutter Game" and verify you get an error (create object or call function)
4. Implement enough of BowlingGame to make it pass.
5. In the test roll 10 gutterballs and confirm it's 0. Fails
6. Create Score method/function.
6. Make it pass (simplest way possible)
7. Create 2nd test AllOnes. Score should be 20
8. Track rolls, return score. Passes.
9. Roll loop is duplicated. Refactor to remove duplication.
10. Create third test, OneSpare (comment to distinguish spare), all others are 3s. Total should be 17.
11. Test fails.
12. Discuss potential solutions. Flag to remember previous would make a bad design worse. Why? 

Using a flag to remember the previous roll could suggest a design problem because it often leads to the following issues:
- Encapsulation Violation: Flags can introduce additional state management within a class or method, potentially leaking implementation details that should be hidden from other parts of the program. This violates the principle of encapsulation, making the code harder to maintain and reason about.
- Increased Complexity: Managing flags can complicate the logic and create opportunities for bugs, especially as the codebase grows. This makes the code less straightforward and harder to test, going against the principles of simplicity in TDD.
- Single Responsibility Principle (SRP): A flag might indicate that a class or method is doing too much—trying to handle both game state and scoring. It’s better to design the system so each component has a single, well-defined responsibility.
- Potential for Errors: Relying on a flag can lead to situations where it’s improperly set or cleared, introducing subtle and hard-to-diagnose bugs.
The temptation to use a flag can be a red flag for a design that doesn't naturally express the behavior or rules of bowling through its structure. Instead, a cleaner approach might be to use an array to store rolls and then process them sequentially without needing additional state tracking. This aligns with TDD's emphasis on iterative refinement and maintaining simplicity in code design.

14. But our design is already bad. How?
    - "Roll" calculates the score, but doesn't imply that.
    - "Score" does NOT calculate the score, but the name implies that it does.
15. We have a failing test. In order to refactor before that test passes, we need to comment it out.
16. Refactor "Roll" so that it records the rolls.
17. Refactor "Score" so that it calculates the score.
18. Remove temporary variables
19. Uncomment-out the third test (still fails)
20. Scoring by adding roll[i] + roll[i+1] won't work because i might not reference the first ball of the frame. So the design is still wrong. Need to walk through the array two balls (one frame) at a time.
21. Implement the above. (re-commenting out test 3)
22. re-Uncomment-out test 3 (fails)
23. Make it work!
24. Still have 3 issues:
    - Still an ugly comment in the test
    - Ugly comment in the conditional
    - i is a bad name for a variable (is it really?)
25. Rename i
26. Method Extract "Spare"
27. Extract Method in test "RollSpare"
28. Test 4 - Roll Strike.
29. Implement Roll Strike. Passes, but it's ugly:
    - Ugly Comment in TestOneStrike
    - Another ugly comment in conditional
    - All the expressions are starting to look ugly.
30. Extract Several methods in prod code to get rid of ugly expressions:
    - SumOfBallsInFrame
    - SpareBonus
    - StrikeBonus
31. Add "IsStrike" to get rid of ugly comment in production
32. Add "RollStrike" in test to get rid of ugly comment in test.
33. Create 5th test - which is a perfect game. It just works
34. Note that it doesn't match anything like you thought it would be as a Object Oriented Programmer
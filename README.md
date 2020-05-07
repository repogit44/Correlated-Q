# Correlated-Q

Replication of results found in Figure 3(parts a-d) in *Correlated Q-Learning* by Amy Greenwald and Keith Hall Greenwald, Hall, and Serrano 2003. 

Course Instructor has all the rights on course materials, homeworks, exams and projects. Please note that unauthorized use of any previous semester course materials, such as tests, quizzes, homework, projects, videos, and any other coursework, is prohibited in this course.


## 1 Soccer Game

The game is played on a 2x4 grid. The two players, A and B, can occupy distinct cells of the grid and can choose one of the 5 actions at each step: N, S, E, W, and stick. The players’ actions are executed in random order. When the player with ball moves into the player without the ball, the former loses the ball to the latter while if the player without the ball runs into the player with the ball, he cannot steal the ball. The sum of scores is always zero. If the player with the ball moves into the goal area then he scores +100 if it’s his own goal and -100 if it’s the other player’s goal. In either case, the game ends.

In the implementation, the cells are numbered from 0 - 7 with top left as 0 and bottom right as 7. The 5 actions N, S, E, W and stick hence are encoded as -4, 4, +1, -1 and 0. If the action causes the player to move out of the grid, then the system would enforce the player to stick. As the two players can not occupy the same cell, there are in total 112 states. The game ends after 50 steps anyway if no one wins.

## 2 Algorithms

* Q-learning: the game is treated as single-player game - the learner is ignorant of the actions taken by his opponent;
* Friend-Q: the learner naively assumes that the opponent will help him to maximize the reward and achieve a coordinated equilibrium;
* Foe-Q: opposite to the Friend-Q, in Foe-Q the opponent tries to minimax the learner's rewards and reaches the adversial equilibrium;
* Correlated-Q(CE-Q): *u*CE-Q is applied where the objective function is to maximize the sum of the players' rewards and linear programming is used to find the correlated equilibrium.

Error Calculation: For Friend-Q, Foe-Q and CE-Q, the error is calculated as the difference in Q values corresponding to state s, with player A taking action S and player B sticking at time t and time t−1, if this combination is not encountered at time t, then error will be 0. For Q-learning, the error values reflect the player A’s Q-values corresponding to state s and action S.

## 3 Implementation

Off-policy Correlated-Q, Foe-Q, Friend-Q (γ = 0.9) and on-policy Q-learning (γ = 0.9). Q-learning is on-policy and ε-greedy, with ε = 0.01 while other algorithms are off- policy(equivalently on-policy and ε = 1). Due to the computation capacity, except Q-learning which was trained for 10^e5 as in the paper, all the rest learners are trained with 5^e4 iterations. To compensate for that, the hyperparameters are selected more carefully.

Overall, all four algorithms implemented matched the pattern in author's paper, except Q-learning all the rest algorithms converges. For Friend-Q result, although the error increase at the very beginning probably because of the randomness, the pattern is consistent with the original result, converging rapidly after several thousand iterations. 




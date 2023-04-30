Download Link: https://assignmentchef.com/product/solved-fit2004-assignment-2-dynamic-programming
<br>
<ol>

 <li>Think of test cases that you can use to check if your algorithm works.

  <ul>

   <li>Use the edge cases you found during the previous phase to inspire your test cases.</li>

   <li>It is also a good idea to generate large random test cases.</li>

   <li>Sharing test cases is allowed, as it is not helping solve the assignment.</li>

  </ul></li>

 <li>Code up your algorithm, (remember decomposition and comments) and test it on the tests you have thought of.</li>

 <li>Try to break your code. Think of what kinds of inputs you could be presented with which your code might not be able to handle.

  <ul>

   <li>Large inputs</li>

   <li>Small inputs</li>

   <li>Inputs with strange properties</li>

   <li>What if everything is the same?</li>

   <li>What if everything is different?</li>

   <li>..</li>

  </ul></li>

</ol>

<h1>Documentation</h1>

For this assignment (and all assignments in this unit) you are required to document and comment your code appropriately. This documentation/commenting must consist of (but is not limited to)

<ul>

 <li>For each function, high level description of that function. This should be a one or two sentence explanation of what this function does. One good way of presenting this information is by specifying what the input to the function is, and what output the function produces (if appropriate)</li>

 <li>For each function, the Big-O complexity of that function, in terms of the input. Make sure you specify what the variables involved in your complexity refer to. Remember that the complexity of a function includes the complexity of any function calls it makes.</li>

 <li>Within functions, comments where appropriate. Generally speaking, you would comment complicated lines of code (which you should try to minimise) or a large block of code which performs a clear and distinct task (often blocks like this are good candidates to be their own functions!).</li>

</ul>

<h1>1           Game Master</h1>

You and your friends are playing a table-top role playing game, and you are the game master. You want to design an encounter, and you have a certain difficulty target that you want to reach. You also have a list of monsters, and you want to select a group of monsters whose difficulty ratings sum up to the target difficulty.

You are interested in finding out how many different possible encounters there are which satisfy this requirement. To solve this problem, you will write a function count_encounters(target_difficulty, monster_list).

<h2>1.1          Input</h2>

target_difficulty is a non-negative integer.

monster_list is a list of tuples. Each tuple represents a type of monster. The first value in each tuple is a string, which is the name of the type of monster. The second value is a positive integer, representing the difficulty of that particular type of monster.

<h2>1.2          Output</h2>

count_encounters returns an integer, which is the number of different sets of monsters whose difficulties sum to target_difficulty. A type of monster may be used more than once in an encounter.

<h2>1.3          Example</h2>

target_difficulty = 15 monster_list = [(“bear”, 5), (“imp”, 2), (“kobold”, 3), (“dragon”, 10)] print(count_encounters(target_difficulty, monster_list)) &gt;&gt;&gt; 9

In the above example, the possible encounters are:

1 dragon, 1 bear

1 dragon, 1 kobold, 1 imp

3 bear

2 bear, 1 kobold, 1 imp

1 bear, 2 kobold, 2 imp

1 bear, 5 imp

5 kobold

3 kobold, 3 imp

1 kobold, 6 imp

Your answer does not need to compute these possible sets of monsters, this list is provided to help you understand the example answer of 9

<h2>1.4          Complexity</h2>

count_encounters should run in <em>O</em>(<em>DM</em>) where

<ul>

 <li><em>D </em>is the value of target_difficulty</li>

 <li><em>M </em>is the length of monster_list</li>

</ul>

<h1>2           Greenhouse</h1>

You are a gardener in charge of a greenhouse. You are growing a variety of exotic plants as decoration for a party. You want to maximise the chance that all the plants are grown by the day of the party. In order to cause plants to grow more quickly, you can put sun lamps above the plants to give them more nutrients.

You have calculated the probability that each plant will be ready on time, based on the number of lamps you assign to it. You cannot move the lamps around once you assign them to a plant. You want to maximise the chance that all the plants are fully grown by the day of the party. To solve this problem, write a function best_lamp_allocation(num_p, num_l, probs)

<h2>2.1          Input</h2>

num_p and num_l are positive integers representing the number of plants and lamps respectively.

probs is a list of lists, where probs[i][j] represents the probability that plant i will be ready in time if it is allocated j lamps. Values in probs are floats between 0 and 1 inclusive.

Plants do not always grow faster with more light, so it is possible for the probabilities to decrease as well as increase, as the number of lamps increases. In other words, the lists within probs may not be sorted ascending.

<h2>2.2          Output</h2>

best_lamp_allocation returns an float, which is the highest probability of all plants being ready by the party that can be obtained by allocating lamps to plants optimally.

<h2>2.3          Example</h2>

probs = [[0.5, 0.5, 1],[0.25,0.1,0.75]] best_lamp_allocation(2,2,probs)

&gt;&gt;&gt; 0.375

probs = [[0.5, 0.75, 0.25],[0.75,0.25,0.8]] print(best_lamp_allocation(2,2,probs))

&gt;&gt;&gt; 0.5625

<h2>2.4          Explanation of example</h2>

In the first example, we have 2 lamps to use. If we assign 0 lamps to plant 0, it has a 0.5 probability of being ready. We would need to assign the full 2 lamps to it to improve its chance (to 1). We have 2 lamps left, so the best thing to do is assign both to plant 1, for a probability of 0.75. This gives an overall probability of 0.75*0.5=0.375.

We again have 2 lamps and 2 plants, but with different probabilities. This time, the most efficient thing is to not use all the lamps! Giving 1 lamp to plant 0 and 0 lamps to plant 1 give a probability of 0.5625. It would be ideal to give 1 lamp to plant 0 and 2 lamps to plant 1, but we do not have 3 lamps so this is impossible.

<h2>2.5          Approach</h2>

A good place to start would be answering one or both of the following questions:

<ul>

 <li>Come up with an idea for what your memo array looks like. What are its dimensions? What values will be stored in each cell (i.e. what are the overlapping subproblems)</li>

 <li>Come up with a recursive solution to this problem. If we have solved all previous (what does previous mean here?) subproblems, how can we use that information to solve the current subproblem?</li>

</ul>

To help with the above, here are some things to think about:

<ul>

 <li>Which memo cells can we fill in trivially (i.e. with no reference to smaller subproblems)?</li>

 <li>If we are considering how many lamps to give to plant <em>i</em>, and we decide to give it <em>x </em>lamps, what is the maximum number of lamps we can give to plants 0<em>,</em>1<em>,…i </em>−1? When is the answer num_l−<em>x</em>? When is it not num_l−<em>x</em>?</li>

 <li>Having answered the question above, what does this tell us about the subproblems that we should be solving?</li>

 <li>What options do we have to try while solving each subproblem?</li>

 <li>In What order should we traverse the cells of the memo array?</li>

</ul>

<h2>2.6          Complexity</h2>

best_lamp_allocation should run in <em>O</em>(<em>PL</em><sup>2</sup>) time and <em>O</em>(<em>PL</em>) space, where <em>P </em>is num_p, and

<em>L </em>is num_l
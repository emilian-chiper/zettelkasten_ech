### Meta
2024-10-31 22:52
**Tags:** [[math]] [[precalculus]]
**Status:** #completed 

### 1. Understand the Problem
Read the problem and ensure you understand it. Questions:
- What’s the unknown?
- What are the given quantities?
- What are the given conditions?
- Draw a diagram.
- Introduce suitable notation.

### 2. Think of a Plan
“How can I relate the given to the unknown?” If you don’t see a connection immediately:
- Try to recognize something familiar,
- Try to recognize patterns,
- Use analogy,
- Introduce something extra
- Take cases,
- Work backward,
- Establish subgoals,
- Indirect reasoning (proof by contradiction)
- Mathematical induction

### 3. Carry Out the Plan
Check each stage of the plan and write the details that prove that each state is correct.

### 4. Look Back
Check for errors. Familiarize yourself with the solution.

### PROBLEM
A driver sets out on a journey. For the first half of the distance, she drives at the leisurely pace of 30 mi/h; during the second half she drives 60 mi/h. What is her average speed on this trip?

#### 1. Thinking about the problem
Temptation:
$$
\frac{30+60}{2}=45mi/h
$$
Incorrect.

**Try a special case.**
Suppose that the total distance traveled is $120mi$. Since the first $60mi$ is traveled at $30mi/h$, it takes $2h$. The second $60mi$ is traveled at $60mi/h$, so it takes one hour. Thus, the total time is $2 + 1 = 3$ hours and the average speed is:
$$
\frac{120}{3}=40mi/h
$$
So our guess of $45mi/h$ was wrong.

##### SOLUTION
**Understand the problem.**
We must look more carefully at the meaning of average speed:
$$
average\;speed = \frac{distance\;traveled}{time\;elapsed}
$$
**Introduce notation.**
Let $d$ be the distance traveled on each half of the trip.
Let $t_1$ and $t_2$ be the times taken for the first and second halves of the trip.

**State what is given.**
For the first half of the trip we have
$$
30 = \frac{d}{t_1}
$$
and for the second half we have
$$
60 = \frac{d}{t_2}
$$

**Identify the unknown.**
Now we identify the quantity that we are asked to find:
$$
average\;speed\;for\;entire\;trip = \frac{total\;distance}{total\;time} = \frac{2d}{t_1+t_2}
$$

**Connect the given with the unknown.**
To calculate this quantity, we need to know $t_1$ and $t_2$, so we solve the above equations for these times:
$$
t_1=\frac{d}{30} \qquad t_2=\frac{d}{60}
$$
Now we have the ingredients needed to calculate the desired quantity:
$$
average\;speed=\frac{2d}{t_1+t_2}=\frac{2d}{\frac{d}{30}+\frac{d}{60}}
$$
$$
=\frac{60(2d)}{60(\frac{d}{30}+\frac{d}{60})}
$$
$$
=\frac{120d}{2d+d}=\frac{120d}{3d}=40
$$
So the average speed for the entire trip is $40mi/h$.
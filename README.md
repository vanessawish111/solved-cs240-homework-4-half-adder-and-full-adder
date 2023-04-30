Download Link: https://assignmentchef.com/product/solved-cs240-homework-4-half-adder-and-full-adder
<br>
The assignment is to use bitwise operations to add two numbers.

Half Adder and Full Adder

In digital circuits, the half adder adds two input bits, P and Q, and produces two output bits, sum S and carry C. See the left part of Figure 1. The truth table of the half adder is as follows.

<table width="117">

 <tbody>

  <tr>

   <td width="55">input</td>

   <td width="62">output</td>

  </tr>

  <tr>

   <td width="55">P     Q</td>

   <td width="62">C        S</td>

  </tr>

  <tr>

   <td width="55">0      0</td>

   <td width="62">0        0</td>

  </tr>

  <tr>

   <td width="55">0      1</td>

   <td width="62">0        1</td>

  </tr>

  <tr>

   <td width="55">1      0</td>

   <td width="62">0        1</td>

  </tr>

  <tr>

   <td width="55">1      1</td>

   <td width="62">1        0</td>

  </tr>

 </tbody>

</table>

Ideally, we should write one function that computes both S and C, but we have not discussed how to return multiple values from a function. Therefore, we write two functions that compute S and C separately, as follows. enum bits {ZERO, ONE};

enum bits halfAdderSum(enum bits P, enum bits Q) {

P       Q                                                   P       Q

(P AND Q)   C

S

(P XOR Q)

Figure 1: Left: the half adder. Right: the full adder

return P ^ Q;

}

enum bits halfAdderCarry(enum bits P, enum bits Q)

{

return P &amp; Q;

}

The half adder adds only two bits. It becomes inadequate when we want to add more than two bits. Let us consider adding two 8-bit integers, <em>P</em><sub>7</sub><em>P</em><sub>6</sub><em>P</em><sub>5</sub><em>P</em><sub>4</sub><em>P</em><sub>3</sub><em>P</em><sub>2</sub><em>P</em><sub>1</sub><em>P</em><sub>0 </sub>and <em>Q</em><sub>7</sub><em>Q</em><sub>6</sub><em>Q</em><sub>5</sub><em>Q</em><sub>4</sub><em>Q</em><sub>3</sub><em>Q</em><sub>2</sub><em>Q</em><sub>1</sub><em>Q</em><sub>0</sub>. After we add <em>P</em><sub>0 </sub>and <em>Q</em><sub>0</sub>, the carry bit may be 1. We must incorporate it when adding <em>P</em><sub>1 </sub>and <em>Q</em><sub>1</sub>. Thus we need the full adder that takes three inputs: P, Q, and the carry-in Cin. The output bits are sum S and carry-out Cout. See the right part of Figure 1. The truth table of the full adder is as follows.

<table width="169">

 <tbody>

  <tr>

   <td colspan="3" width="95">input</td>

   <td colspan="2" width="74">output</td>

  </tr>

  <tr>

   <td width="35">P</td>

   <td width="28">Q</td>

   <td width="32">Cin</td>

   <td width="58">Cout</td>

   <td width="17">S</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="28">0</td>

   <td width="32">0</td>

   <td width="58">0</td>

   <td width="17">0</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="28">0</td>

   <td width="32">1</td>

   <td width="58">0</td>

   <td width="17">1</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="28">1</td>

   <td width="32">0</td>

   <td width="58">0</td>

   <td width="17">1</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="28">1</td>

   <td width="32">1</td>

   <td width="58">1</td>

   <td width="17">0</td>

  </tr>

  <tr>

   <td width="35">1</td>

   <td width="28">0</td>

   <td width="32">0</td>

   <td width="58">0</td>

   <td width="17">1</td>

  </tr>

  <tr>

   <td width="35">1</td>

   <td width="28">0</td>

   <td width="32">1</td>

   <td width="58">1</td>

   <td width="17">0</td>

  </tr>

  <tr>

   <td width="35">1</td>

   <td width="28">1</td>

   <td width="32">0</td>

   <td width="58">1</td>

   <td width="17">0</td>

  </tr>

  <tr>

   <td width="35">1</td>

   <td width="28">1</td>

   <td width="32">1</td>

   <td width="58">1</td>

   <td width="17">1</td>

  </tr>

 </tbody>

</table>

Your task in this part of the homework is to implement the two functions for the full adder in the file adder.c. enum bits {ZERO, ONE};

enum bits fullAdderSum(enum bits P, enum bits Q, enum bits Cin)

{

}

enum bits fullAdderCarry(enum bits P, enum bits Q, enum bits Cin)

{

}

You should start by working out the Boolean expressions for S and Cout, and try to use as few Boolean operators as possible. The essence of C programming is brevity and efficiency.

<h2>2          Adding Two Numbers</h2>

Now you are ready to add two 32-bit integers bit by bit. Using a cascade of full adders, you can add a pair of bits and the carry bit from the previous position, save the sum bit, and send the carry bit to the next position. The first Cin should be set to zero. If we assume the sum of the two numbers does not overflow the 32-bit storage, we can safely discard the last Cout.

Your task in this part of the homework is to implement myAdd() in the file myAdd.c. The algorithm works as follows.

<h3>                                                                                            P1     Q1                 P0     Q0</h3>

Figure 2: Using a cascade of full adders to add two numbers.

<ol>

 <li>Initialize Cin to zero</li>

 <li>For <em>i </em>= 0<em>,</em>1<em>,…,</em>31

  <ul>

   <li>Extract the <em>i</em>-th bits from P and Q</li>

   <li>Use fullAdderSum() and fullAdderCarry() to calculate the sum bit S and the carry bit Cout</li>

   <li>Write the sum bit to the <em>i</em>-bit of mySum</li>

   <li>Move Cout to Cin for the next iteration</li>

  </ul></li>

</ol>

There are many ways to extract a bit or write a bit in a 32-bit storage. See the lecture notes 7 and 8 for different methods that operate on bits.

<h2>3        The Driver</h2>

The driver is in the file main.c. You should not change anything in the main program, but you should write some comments at the top of the file.

Make sure your C code follows the style guidelines. In the Report.txt file, you should write pseudo code and discuss what you found difficult about this assignment, how you planned your approach to it, and what you learned completing it.
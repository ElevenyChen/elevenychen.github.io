---
layout: post
title:  "Machine Learning: Forum Post Sorting"
date:   2022-11-21 13:50:39
categories: algorithms
---
<small>Because of code confidentiality, this page only demonstrates the framework</small>
<br>
<h1>Machine Learning: Forum Post Sorting</h1>
Piazza is a learning management system which allows students to ask questions in a forum-type format. Instructors can set up "tags" for the class content, such as "Assignment 1," "Project 2," "Midterm Exam," "Class Logistic," etc. Each post shoud be properly categorized by the student who posts it, or it should be automatically categorized by the ai("Potatobot").
<br>
![piazza1](/static/projects/ml-classification/piazza1.png)
<br>
<br>
<h3>Piazza Dataset</h3>
<p>Forum theme: EECS 280 (the second largest course at University of Michigan)</p>
<p>Labels:</p>
<p>By topic: "Project 1," "Project 2," "Project 3," "Project 4," "Project 5," "Midterm," "Final"</p>
<p>By author: "Instructor," "Student"</p>
<p>Train: W14-W16, EECS280 Piazza Post, with proper labels</p>
<p>Validation: SP16, EECS280 Piazza Post</p>
<p>Test: W17, EECS280 Piazza Post</p>
<br>
<br>
<h3>Model Construction</h3>
<p>Set: texts are considered unordered and non-repetitive</p>
<p>Conditional Probability: we write P(A) to denote the probability (between 0 and 1) that some event A will occur. We write P(A|B) to denote the probability that event A will occur given that we already know event B has occurred.</p>
<br>
<br>
<h3>Prediction Model</h3>
![piazza3](/static/projects/ml-classification/ml1.png)
![piazza4](/static/projects/ml-classification/ml2.png)
<br>
<br>
<h3>Result Demonstruation</h3>
<pre><code>
INPUT AND OUTPUT
INPUT AND OUTPUT
INPUT AND OUTPUT
INPUT AND OUTPUT
INPUT AND OUTPUT
INPUT AND OUTPUT
</code></pre>





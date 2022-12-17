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
<p>By <strong>topic</strong>: "Project 1," "Project 2," "Project 3," "Project 4," "Project 5," "Midterm," "Final"</p>
<p>By <strong>author</strong>: "Instructor," "Student"</p>
<p><strong>Train</strong>: W14-W16, EECS280 Piazza Post, with proper labels</p>
<p><strong>Validation</strong>: SP16, EECS280 Piazza Post</p>
<p><strong>Test</strong>: W17, EECS280 Piazza Post</p>
<p>(Post content was downloaded by crawlers)</p>
<p>(Index categorization is based on binary search tree, the searching is based on map)</p>
<br>
<h3>Model Construction</h3>
<p><strong>Set</strong>: texts are considered unordered and non-repetitive</p>
<p><strong>Conditional Probability</strong>: we write P(A) to denote the probability (between 0 and 1) that some event A will occur. We write P(A|B) to denote the probability that event A will occur given that we already know event B has occurred.</p>
<br>
<br>
<h3>Prediction Model</h3>
![piazza3](/static/projects/ml-classification/ml1.png)
![piazza4](/static/projects/ml-classification/ml2.png)
<br>
<h3>Result Demonstruation</h3>
Small size sample run:
<pre><code>trained on 8 examples

test data:
  correct = euchre, predicted = euchre, log-probability score = -13.7
  content = my code segfaults when bob is the dealer

  correct = euchre, predicted = calculator, log-probability score = -12.5
  content = no rational explanation for this bug

  correct = calculator, predicted = calculator, log-probability score = -13.6
  content = countif function in stack class not working

performance: 2 / 3 posts predicted correctly
</code></pre>
<br>
Midium size sample run:
<pre><code>trained on 2552 examples
test data:
  correct = exam, predicted = exam, log-probability score = -162
  content = final exam scores have been released and regrade requests are open please take a look at the solutions before submitting a regrade request solutions have been posted on the google drive you have until sunday at 100 pm to submit a regrade request requests submitted after this time will not be processed exam statistics can be found in the grade statistics thread in 7
  ......
  
performance: 245 / 332 posts predicted correctly
</code></pre>
<br>
  
Large size sample run:
<pre><code>trained on 11365 examples

test data:
  correct = instructor, predicted = instructor, log-probability score = -112
  content = we want to express our appreciation for those of you who completed the projects with honesty and integrity this semester 9 cases involving 15 current and 10 past students from our course are being referred to the honor council pin
  ......
  
performance: 2602 / 2988 posts predicted correctly
</code></pre>





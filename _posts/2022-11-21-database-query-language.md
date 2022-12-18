---
layout: post
title:  "Database Query Language (SimpleQL)"
date:   2022-11-21 15:50:39
categories: database
---
<small>Because of code confidentiality, this page only demonstrates the framework</small>
<br>
<h1>Database Query Language: SimpleQL</h1>
A relational database is the most common means of data storage and retrieval in the modern age. A relational database model stores data into one or more tables, where each table has columns and rows. The columns represent a value that can be attributed to an entry (such as <code>color</code>, <code>name</code>, or <code>ID</code>) and the rows represent individual entries or records (such as <code>Name</code>, <code>my_cat</code>, or <code>ABC_1695</code>). For instance, the table pictured below has each row corresponding to a car (a data type), and the columns group a car’s vendors, model, etc. such that this information can be easily retrieved.
<br>
[!SQL1](/static/projects/SQL/)
<br>
<p>However, a database can do much more than simply store information. You must be able to retrieve specific information in an efficient manner. For relational databases, the structured query language (SQL) is a defined method of retrieving information programmatically. It looks like real English, where a valid command for the above table could be:</p>
<pre><code>SELECT Model from Cars marketplace where Price < 30000
</code></pre>
<br>
<p>which would return a list of models:</p>
<pre><code>[Corvette, Corvette, Malibu, Malibu, Malibu]
</code></pre>
<br>
<h3>Database Commands</h3>
<h4><strong>CREATE</stong></h4>
<p>Add a new table to the database:</p>
<h5>CREATE Syntax</h5>
<pre><code> CREATE <tablename> <N> <coltype1> <coltype2> ... <coltypeN> <colname1> <colname2> ... <colnameN>
</code></pre>
<p>Creates a new table with N columns (where N > 0). Each column contains data of type <code><coltype></code> and is accessed with the name <code><coltype></code>. Table names and column names should be guaranteed to be space-free. No two columns in the same table can have the same name (you do not need to check). Valid data types for coltype are <code>{double, int, bool, string}</code>. This table is initially empty.</p>
<h5>CREATE Output</h5>
<p>Print the following on a single line followed by a newline:</p>
<pre><code>New table <tablename> with column(s) <colname1> <colname2> ... <colnameN> created
</code></pre>




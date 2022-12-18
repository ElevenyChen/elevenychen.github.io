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
![SQL1](/static/projects/SQL/SQL.png)
<p>However, a database can do much more than simply store information. You must be able to retrieve specific information in an efficient manner. For relational databases, the structured query language (SQL) is a defined method of retrieving information programmatically. It looks like real English, where a valid command for the above table could be:</p>
<pre><code>SELECT Model from Cars marketplace where Price < 30000
</code></pre>
<p>which would return a list of models:</p>
<pre><code>[Corvette, Corvette, Malibu, Malibu, Malibu]
</code></pre>
<br>
<h2>Darabase Commands</h2>
<p>These commands affect the structure of the database and the running of the command shell. They include the creation and removal of tables, but do not deal with any actual data (items of type <code>string</code>, <code>double</code>, <code>int</code> or <code>bool</code>).
</p>
<h3>CREATE</h3>
<p>Add a new table to the database:</p>
<h4>CREATE Syntax</h4>
{% highlight ruby %}
CREATE <tablename> <N> <coltype1> <coltype2> ... <coltypeN> <colname1> <colname2> ... <colnameN>
{% endhighlight %}
<p>Creates a new table with N columns (where N > 0). Each column contains data of type <code>[coltype]</code> and is accessed with the name <code>[coltype]</code>. Table names and column names should be guaranteed to be space-free. No two columns in the same table can have the same name (you do not need to check). Valid data types for coltype are <code>{double, int, bool, string}</code>. This table is initially empty.</p>
<h4>CREATE Output</h4>
<p>Print the following on a single line followed by a newline:</p>
{% highlight ruby %}
New table <tablename> with column(s) <colname1> <colname2> ... <colnameN> created
{% endhighlight %}

<br>
<h3>QUIT</h3>
<p>Exit the program and delete all data in the database.</p>
<h4>QUIT Syntax</h4>
<pre><code>QUIT
</code></pre>
<p>Cleans up all internal data (i.e. no memory leaks) and exits the program. Note that the program must exit with a <code>return 0</code> from <code>main()</code>.</p>
<h4>QUIT Output</h4>
<p>Print a goodbye message, followed by a newline.</p>
<pre><code>Thanks for being Simple!
</code></pre>

<br>
<h3>REMOVE</h3>
<p>Remove existing table from the database, deleting all data in the table and its definition.</p>
<h4>REMOVE Syntax</h4>
{% highlight ruby %}
REMOVE <tablename>
{% endhighlight %}
<p>Removes the table specified by <code>[tablename]</code> and all associated data from the database, including any created index.</p>
<h4>REMOVE Output</h4>
<p>Print a confirmation of table deletion, followed by a newline, as follows:</p>
{% highlight ruby %}
Table <tablename> deleted
{% endhighlight %}
<br>



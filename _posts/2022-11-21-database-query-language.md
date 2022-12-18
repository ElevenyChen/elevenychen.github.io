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
<p>Cleans up all internal data (i.e. no memory leaks) and exits the program. The program exits with a <code>return 0</code> from <code>main()</code>.</p>
<h4>QUIT Output</h4>
<p>Print a goodbye message, followed by a newline.</p>
<pre><code>Thanks for being simple!
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
<h2>Table Commands</h2>
<p>These commands work on one or more tables and are responsible for interacting with actual data, including insertion, deletion, printing, and indexing.</p>
<h3>INSERT</h3>
<p>Insert new rows at the end (append) of the specified table.</p>
<h4>INSERT Syntax</h4>
{% highlight ruby %}
INSERT INTO <tablename> <N> ROWS 
<value11> <value12> ... <value1M> 
<value21> <value22> ... <value2M> 
... 
<valueN1> <valueN2> ... <valueNM>
{% endhighlight %}
<p>Inserts <code>N</code> new rows into the table specified by tablename. The first line of the command specifies the tablename and the number of rows, <code>N > 0</code>, to be inserted. The next <code>N</code> lines specify the values to be inserted into the table. Each line contains <code>M</code> values, where <code>M</code> is guaranteed to be equal to the number of columns in the table. The first value, <code>[value11]</code>, should be inserted into the first column of the table in the first inserted row, the second value, <code>[value12]</code>, into the second column of the table in the first inserted row, and so on. Additionally, the types of the values are guaranteed to be the same as the types of the columns they are inserted into. For example, if the second column of the table contains integers, <code>[value12]</code> is guaranteed to be an <code>int</code>. Further, <code>string</code> items are guaranteed to be a single string of whitespace delimited characters (i.e. <code>foo bar</code> is invalid, but <code>foo_bar</code> is acceptable).</p>
<h4>INSERT Output</h4>
<p>Print the message shown below, followed by a newline, where <code>N</code> is the number of rows inserted, <code>[startN]</code> is the index of the first row added in the table, and <code>[endN]</code> is the index of the last row added to the table, 0 based. So, if there were <code>K</code> rows in the table prior to insertion, <code>[startN] = K</code>, and <code>[endN] = K + N - 1</code>.</p>
{% highlight ruby %}
Added <N> rows to <tablename> from position <startN> to <endN>
{% endhighlight %}

<br>
<h3>PRINT</h3>
<p>Print values from selected columns, in the given order, from specified rows.</p>
<h4>PRINT Syntax</h4>
{% highlight ruby %}
PRINT FROM <tablename> <N> <print_colname1> <print_colname2> ... <print_colnameN> {WHERE <colname> <OP> <value> | ALL}
{% endhighlight %}
<p>Directs the program to print the columns specified by <code>[print_colname1]</code>, <code>[print_colname2]</code>, … <code>[print_colnameN]</code> from some/all rows in <code>[tablename]</code>. If there is no condition, the command is of the form <code>PRINT ... ALL</code>, and the matching columns from all rows of the table are printed strictly in insertion order. If there is a condition, the command is of the form <code>PRINT ... WHERE [colname] [OP] <value></code>, and only rows whose values in the selected <code>[colname]</code> pass the condition are printed. The rules for the conditional portion are the same as for the DELETE command. The number and order of the column names given in the command do not have to match the number or order of columns in the specified table.</p>
<p>If no index exists or there is a <code>hash</code> index on the conditional column, the results should be printed in order of insertion into the table.</p>
<p>If a bst index exists on the conditional column, the results should be printed in the order in the BST (least item to greatest item for <code>std::map</code> constructed with the default <code>std::less</code> operator), with ties broken by order of insertion into the table.</p>
<h4>PRINT Output</h4>
<p>Print the requested data followed by a summary. Printing the data is accomplished by printing a single line with the names of the selected columns, followed by a single line from each specified row, where the values of each of the selected columns are separated by a single space. Every line should be followed by a newline.</p>
{% highlight ruby %}
<print_colname2> ... <print_colnameN>
<value2row1> ... <valueNrow1>
...
<value2rowM> ... <valueNrowM>
{% endhighlight %}
<p>To print the summary, on a single line, print the number of rows <code>M</code> printed, and the <code>[tablename]</code> from which the rows were printed, followed by a newline.</p>
{% highlight ruby %}
Printed <M> matching rows from <tablename>
{% endhighlight %}

<br>
<h3>DELETE</h3>
<p>Delete selected rows from the specified table.</p>
<h4>DELETE Syntax</h4>
{% highlight ruby %}
DELETE FROM <tablename> WHERE <colname> <OP> <value>
{% endhighlight %}
<p>Deletes all rows from the table specified by <code>[tablename]</code> where the value of the entry in <code>[colname]</code> satisfies the operation <code>[OP]</code> with the given value <code>[value]</code>. You can assume that <code>[value]</code> will always be of the same type as <code>[colname]</code>. For example, to delete all rows from table1 where the entries in column name equal John, the command would be:</p>
{% highlight ruby %}
DELETE FROM table1 WHERE name = John
{% endhighlight %}
<p>Or, to delete all rows from <code>tableSmall</code> where the entries in column size are greater than <code>15</code>, the command would be:</p>
{% highlight ruby %}
DELETE FROM tableSmall WHERE size > 15
{% endhighlight %}
<p><code>[OP]</code> can be from the set <code>{<, >, =}</code>.</p>
<h4>DELETE Output</h4>
<p>Print a summary of the number of rows deleted from the table as shown below, followed by a newline:</p>
{% highlight ruby %}
Deleted <N> rows from <tablename>
{% endhighlight %}

<br>
<h3>JOIN</h3>
<p>Join two tables where values in selected columns match, and print results.</p>
<h4>JOIN Syntax</h4>
{% highlight ruby %}
JOIN <tablename1> AND <tablename2> WHERE <colname1> = <colname2> AND PRINT <N> <print_colname1> <1|2> <print_colname2> <1|2> ... <print_colnameN> <1|2>
{% endhighlight %}
<p>Directs the program to print the data in <code>N</code> columns, selected by <code>[print_colname1]</code>, <code>[print_colname2]</code>, … <code>[print_colnameN]</code>. The <code>[print_colname]</code>s will be the names of columns in either the first table <code>[tablename1]</code> or the second table <code>[tablename2]</code>, as chosen by the <code>1/2</code> argument directly following each </code>[print_colname]</code>.</p>
<h4>JOIN Output</h4>
<p>Print the requested data followed by a summary. Printing the data is accomplished by printing a single line with the names of the selected columns, followed by a single line from each joined row, where the values of each of the selected columns are separated by a single space. Every line should be followed by a newline.<p>
{% highlight ruby %}
<print_colname1> <print_colname2> ... <print_colnameN>
<value1rowA> <value2rowA> ... <valueNrowA>
...
<value1rowM> <value2rowM> ... <valueNrowM>
{% endhighlight %}
<p>To print the summary, on a single line, print the number of rows <code>N</code> printed, and both <code>[tablename1]</code> and <code>[tablename2]</code> which were joined, followed by a newline.<p>
{% highlight ruby %}
Printed <N> rows from joining <tablename1> to <tablename2>
{% endhighlight %}

<br>
<h3>GENERATE</h3>
<p>Create a search index on the selected column in the specified table.</p>
<h4>GENERATE Syntax</h4>
{% highlight ruby %}
GENERATE FOR <tablename> <indextype> INDEX ON <colname>
{% endhighlight %}
<p>Directs the program to create an index of the type <code>[indextype]</code> on the column <code>[colname]</code> in the table <code>[tablename]</code>, where <code>[indextype]</code> is limited to the set <code>{hash, bst}</code>, denoting a hash table index and a binary search tree index respectively. Given the <code>[indextype]</code> hash on column <code>[colname]</code>, the program should create a hash table that allows a row in the table to be found rapidly given a particular value in the column <code>[colnam]</code>. Given the <code>[indextype]</code> bst on column <code>[colname]</code>, the program should create a binary search tree that allows rows in the table to be found rapidly given a particular value in the column <code>[colname]</code>. Only one user-generated Index may exist per table, at any one time. If a valid index is requested on a table that already has one, discard the old index before building the new one.</p>
<p>When <code>bst</code> is the specified index type, a <code>std::map</code> should be applied; when <code>hash</code> is the specified index type, a <code>std::unordered_map</code> should be utilized. It is acceptable for both types to exist at the same time, but only one should be in use or contain data at any given time.</p>
<br>

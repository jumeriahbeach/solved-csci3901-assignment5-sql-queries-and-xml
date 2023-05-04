Download Link: https://assignmentchef.com/product/solved-csci3901-assignment5-sql-queries-and-xml
<br>
Access SQL through Java, practice developing SQL queries, and gain some exposure to XML.

Background

You work for the Northwind food distribution company. Management periodically wants a summary of the company’s operation <strong>over a period of time</strong>.

Problem

Your job is to extract the summary information from the database, given a particular time period. You will store the summary information in a file that follows an XML format. Someone else will then use XML tools (notably XSLT) to convert your information into something that management will review.

There is <strong>no specific class structure </strong>for this problem. You are tasked with writing a command-line program with no constraints on the structure except for

<ul>

 <li>the program inputs, summarized below,</li>

 <li>the program outputs, summarized below, and</li>

 <li><strong>your code must compile</strong></li>

</ul>

<h2>Input</h2>

Your program will obtain the following information from the keyboard in the following order:

<ul>

 <li>The starting date for the period to summarize</li>

 <li>The ending date for the period to summarize</li>

 <li>The name of the file for the output</li>

</ul>

All dates will be in a YYYY-MM-DD format. For instance, valid text input for the date will be 2002-02-17.

<h2>Output</h2>

Your program will <strong>write all of its output to the specified file</strong>.

You will extract and report data in 3 categories:

<ol>

 <li>Customer information

  <ul>

   <li>Report the <strong>customer name</strong>, <strong>address</strong>, <strong>number of orders in this period</strong>, and <strong>total dollar value of their orders in this period</strong>.</li>

  </ul></li>

 <li>Product information

  <ul>

   <li>Report, <strong>for each product category</strong>, the <strong>category name </strong>and <strong>for each product in the category</strong>, report the <strong>name</strong>, <strong>supplier</strong>, <strong>units sold</strong>, and <strong>total dollar value of product sold in this period</strong>.</li>

  </ul></li>

 <li>Supplier information

  <ul>

   <li>Report, <strong>for each supplier with products sold in this period</strong>, the <strong>supplier name</strong>, <strong>address</strong>, <strong>number of products sold</strong>, and the <strong>total dollar value of business that we sold from this supplier’s products in this period</strong>.</li>

  </ul></li>

</ol>

In all of the reporting, do not report any customers, products, or suppliers who have not had any interaction over the reporting period.

Your output file will be in an XML format. XML uses a set of tags to surround data to let you know what the data is. Some tags can be nested in other tags. HTML follows an XML-style format.

We will use a simple version of XML. The first line of your XML file should provide information on the version of XML to use. The following line will be sufficient:

&lt;?xml version=”1.0″ encoding=”UTF-8″ ?&gt;

Following this first line, we get a set of nested tags to store the data. The starting tag has the format &lt;…&gt; and the matching ending tag has the format &lt;/…&gt; (differing by the ending slash) where … is the tag name. The outermost tag is period summary

Here is a description of the XML schema we will use in Document Type Definition (DTD) format (see <a href="https://en.wikipedia.org/wiki/Document_type_definition#XML_DTD_schema_example">https://en.wikipedia.org/wiki/Document</a> <a href="https://en.wikipedia.org/wiki/Document_type_definition#XML_DTD_schema_example">type</a> <a href="https://en.wikipedia.org/wiki/Document_type_definition#XML_DTD_schema_example">definition#XML</a> <a href="https://en.wikipedia.org/wiki/Document_type_definition#XML_DTD_schema_example">DTD</a> <a href="https://en.wikipedia.org/wiki/Document_type_definition#XML_DTD_schema_example">schema</a> <a href="https://en.wikipedia.org/wiki/Document_type_definition#XML_DTD_schema_example">example)</a>.

&lt;!ELEMENT period_summary (period, customer_list, product_list, supplier_list)&gt;

&lt;!ELEMENT period (start_date, end_date)&gt;

&lt;!ELEMENT customer_list (customer*)&gt;

&lt;!ELEMENT customer (customer_name, address, num_orders, order_value)&gt;

&lt;!ELEMENT address (street_address, city, region, postal_code, country)&gt;

&lt;!ELEMENT product_list (category*)&gt;

&lt;!ELEMENT category (category_name, product*)&gt;

&lt;!ELEMENT product (product_name, supplier_name, units_sold, sale_value)&gt;

&lt;!ELEMENT supplier_list (supplier)&gt;

&lt;!ELEMENT supplier (supplier_name, address, num_products, product_value)&gt;

&lt;!ELEMENT start_date (#PCDATA)&gt;

&lt;!ELEMENT end_date (#PCDATA)&gt;

&lt;!ELEMENT customer_name (#PCDATA)&gt;

&lt;!ELEMENT num_orders (#PCDATA)&gt;

&lt;!ELEMENT order_value (#PCDATA)&gt;

&lt;!ELEMENT street_address (#PCDATA)&gt; &lt;!ELEMENT city (#PCDATA)&gt;

&lt;!ELEMENT region (#PCDATA)&gt;

&lt;!ELEMENT postal_code (#PCDATA)&gt;

&lt;!ELEMENT country (#PCDATA)&gt;

&lt;!ELEMENT category_name (#PCDATA)&gt; &lt;!ELEMENT product_name (#PCDATA)&gt;

&lt;!ELEMENT supplier_name (#PCDATA)&gt;

&lt;!ELEMENT units_sold (#PCDATA)&gt;

&lt;!ELEMENT sale_value (#PCDATA)&gt;

&lt;!ELEMENT address (#PCDATA)&gt;

&lt;!ELEMENT num_products (#PCDATA)&gt;

&lt;!ELEMENT product_value (#PCDATA)&gt;

This means that a tag period summary must contain nested tags for each of

<ul>

 <li>period,</li>

 <li>customer list,</li>

 <li>product list, and</li>

 <li>supplier list.</li>

</ul>

In the tag period, the nested tag start date is defined further below as #PCDATA — this simply means that the start date tag will <strong>not </strong>contain any nested data and will instead just be a string, such as &lt;start date&gt; 1996-01-30 &lt;/start date&gt; The tag customer list will contain <strong>zero or more </strong>nested customer tags, as indicated by the * after the customer tag in the !ELEMENT clause.

While spacing doesn’t matter in an XML file, you should always use line breaks and tabs to make the XML file readable by a person.

<strong>Sample output</strong>

&lt;?xml version=”1.0″ encoding=”UTF-8″ ?&gt; &lt;period_summary&gt;

&lt;period&gt;

&lt;start_date&gt; 1996-01-30 &lt;/start_date&gt;

&lt;end_date&gt; 1996-02-02 &lt;/end_date&gt;

&lt;/period&gt;

&lt;customer_list&gt;

&lt;customer&gt;

&lt;customer_name&gt; foo &lt;/customer_name&gt; &lt;address&gt;

&lt;street_address&gt; 123 Hemming Way &lt;/street_address&gt;

&lt;city&gt; Brandon &lt;/city&gt;

&lt;region&gt; Manitoba &lt;/region&gt;

&lt;postal_code&gt; P3J 4V2 &lt;/postal_code&gt;

&lt;country&gt; Canada &lt;/country&gt;

&lt;/address&gt;

&lt;num_orders&gt; 30 &lt;/num_orders&gt;

&lt;order_value&gt; 11425 &lt;/order_value&gt;

&lt;/customer&gt;

&lt;/customer_list&gt;

&lt;product_list&gt;

&lt;category&gt;

&lt;category_name&gt; games &lt;/category_name&gt; &lt;product&gt;

&lt;product_name&gt; game1 &lt;/product_name &gt;

&lt;supplier_name&gt; a_supplier &lt;/supplier_name&gt;

&lt;units_sold&gt; 100 &lt;/units_sold&gt;

&lt;sale_value&gt; 500 &lt;/sale_value&gt;

&lt;/product&gt;

&lt;/category&gt;

&lt;/product_list&gt;

&lt;supplier_list&gt;

&lt;supplier&gt;

&lt;supplier_name&gt; a_supplier &lt;/supplier_name&gt; &lt;address&gt;

&lt;street_address&gt; 456 Falcoln Ridge &lt;/street_address&gt;

&lt;city&gt; Saskatoon &lt;/city&gt;

&lt;region&gt; Saskatchewan &lt;/region&gt;

&lt;postal_code&gt; Q3C 1T8 &lt;/postal_code&gt;

&lt;country&gt; Canada &lt;/country&gt;

&lt;/address&gt;

&lt;num_products&gt; 5 &lt;/num_products&gt;

&lt;product_value&gt; 1250 &lt;/product_value&gt;

&lt;/supplier&gt;

&lt;/supplier_list&gt;

&lt;/period_summary&gt;

<h2>Constraints</h2>

<ul>

 <li>You may use any data structure from the Java Collection Framework.</li>

 <li>Write your solution in Java. <strong>The solution code must be your own</strong>.</li>

 <li>Use the mysql JDBC connection for Java.</li>

 <li>If in doubt for testing, I will be running your program on cs.dal.ca. Correct operation of your program shouldn’t rely on any packages that aren’t available on that system.</li>

</ul>

<h2>Notes</h2>

<ul>

 <li>Use SQL vs Java for processing data as you deem best.</li>

 <li>Be sure to document your approach and any resources that you use.</li>

 <li>Look at where the bulk of the marks are in the marking scheme to help focus your efforts.</li>

 <li>You can run your queries against the csci3901 database on cs.dal.ca. I will also make the sql file for the database available to you so that you can create your own copy of the database.</li>

</ul>

.. contents::

============
Disclaimer
============
**redturtle.sqlcontens** is a **dangerous** package. 

Read carefully the documentation before using it. 
Even if this package is developed to execute "SELECT" queries, it accepts any 
kind of query without validation. In the current development state you can **even DROP** stuff from your DB, 
and this is **dangerous** and **evilish**.

**SECURITY HINT**: it is better, when possible to access the external DB with a
read only account. This can **save the world**! 

**Do not query large amount of data or blobs**, 
redturtle.sqlcontents is not designed for that task!

Be aware that long queries or network problems can **lock your instance threads**!

============
Introduction
============

This package is developed to satisfy the demand to execute and present simple SQL 
queries on Plone using SQLAlchemy.

It introduces two archetypes to your Plone site:

- `SQLFolder`_
- `SQLQuery`_

With this contents you can display the data returned by the queries into Plone pages.

===========
Description
===========

SQLFolder
=========

The SQLFolder object is globally addable and can contain SQLQuery objects.
The SQLFolder has a **connection_url** field where you can specify how to connect 
to an external DB through SQLAlchemy.
Please take a look to `the SQLAlchemy documentation
<http://docs.sqlalchemy.org/en/rel_0_7/core/engines.html>`_).

.. image:: http://blog.redturtle.it/pypi-images/redturtle.sqlcontents/sqlfolder_edit.png/image_preview

SQLQuery
========

Inside a SQLFolder you can create SQLQueries, document like objects that 
contain a field **query**.
Inside this field you can specify any kind of query to your database, **without
constraints**, even if it supposed to be a SELECT.

.. image:: http://blog.redturtle.it/pypi-images/redturtle.sqlcontents/sqlquery_edit.png/image_preview

The default view for the SQLQuery objects takes the results from your query and
presents them in a paginated table.
The header of the tables is composed, by default, by the column names, but you 
can define a replacement mapping filling properly the field **column_names**.

.. image:: http://blog.redturtle.it/pypi-images/redturtle.sqlcontents/sqlquery_view.png/image_preview

============
Installation
============
 
Add redturtle.sqlcontents to the egg section of your instance::
  
  [instance]
  eggs=
      ...
      redturtle.sqlcontents
      ...

In order to make the connection to your database server of choice effective 
you may  need to install (using systm tools or buildout) the proper libraries, 
e.g:

- MySQL-python
- cx_Oracle
- psycopg2
- python-sqlite

In older Plone (previous to version 3.3.2) you need to do the same with the 
zcml section.

=====
Notes
=====
**redturtle.sqlcontents** has been tested with Plone 3.3.4 and Plone 4.2. 
I assume the compatibility with the intermediate releases.

**redturtle.sqlcontents** depends on:

- `SQLAlchemy <http://www.sqlalchemy.org/>`_
- `Products.DataGridField <http://plone.org/products/datagridfield>`_

Those packages are automatically included by **redturtle.sqlcontents** inside
your buildout, so you do not have to take care about them.

In **Plone 3** installations you may want to pin the Products.DataGridField to 
a version lower than 1.7 (1.6.2 is the proper one at the time of writing).

Credits
=======

Developed with the support of `ARPA Veneto`__; ARPA Veneto supports the
`PloneGov initiative`__.

__ http://www.arpa.veneto.it/
__ http://www.plonegov.it/

Authors
=======

This product was developed by RedTurtle Technology team.

.. image:: http://www.redturtle.it/redturtle_banner.png
   :alt: RedTurtle Technology Site
   :target: http://www.redturtle.it/

TODO?
=====
- Validate the queries through registrable adapters;
- Present the data through adapters to handle blob, dates and so on;
- Add more connection parameters to the SQLFolder object;
- Optimize DB connections;
- Add some cache here and there;
- More aggressive caching;
- Caching;

More about the database
==================

Description
----------
The portal's database can be approached with RESTful ajax calls, which are handles by the mongo-by-params module. Storing records can only be done with local POST messages, querying can be done cross-domain as well, using JSONP


Querying through REST
-------------
The module supports basic querying on mongodb using URL parameters. Before reading these specs a basic insight on how `querying on mongodb <http://www.mongodb.org/display/DOCS/Advanced+Queries>`_ works is helpful.

To view the examples a good `json plugin <http://www.google.com/search?q=json+plugin&ie=utf-8&oe=utf-8&aq=t&rls=org.mozilla:en-US:official&client=firefox-a#hl=en&client=firefox-a&hs=Xlh&rls=org.mozilla:en-US%3Aofficial&sclient=psy-ab&q=json+plugin+browser&oq=json+plugin+browser&aq=f&aqi=g-K1&aql=&gs_l=serp.3..0i30.9844.12260.0.12477.8.4.0.4.4.0.162.349.3j1.4.0...0.0.gFgY1MOFTDU&pbx=1&bav=on.2,or.r_gc.r_pw.r_qf.,cf.osb&fp=c1e99b5acbebabce&biw=1920&bih=1017>`_ for your browser is helpful as well.

The mapping::

		http://domain.x:port/db/collection_name[?limit=n&offset=n&fields[]=x&fields[]=y&callback=func&field=value]

The above example shows the way the module interprets the path and (optional) parameters semantically. As you can see, some fields are reserved keywords. Because parameters are mapped directly to fields in the database, it would not work to store data in the database using any these reserved keywords:

- *limit* - the amount of records to be retrieved (default = limitless)

- *offset* - offset of the first record in the resultset (default = 0)

- *fields* - array of fields to be retrieved from each record (default = all fields are retrieved)

- *callback* - the JSONP callback function.

Setting the limit or offset keyword to a non integer value will lead to the parameter being ignored. 

The fields parameter is actually an array parameter and so can be passed multiple times::

		?fields[]=fieldname1&fields[]=fieldname2

Examples
-------

The examples below are actually paginated to protect your browser from crashing when clicking on it:

- Viewing the entire collection: `/db/named_entities <http://hack4europe.kbresearch.nl/db/named_entities?limit=10>`_

- Changing the limit and offset: `/db/named_entities?limit=10&offset=10  <http://hack4europe.kbresearch.nl/db/named_entities?limit=10&offset=10>`_

- Defining a JSONP callback:  `/db/named_entities?callback=myns.myfunc  <http://hack4europe.kbresearch.nl/db/named_entities?limit=10&callback=myns.myfunc>`_

- Requesting specific fields: `/db/named_entities?fields[]=recordId&fields[]=type  <http://hack4europe.kbresearch.nl/db/named_entities?limit=10&fields[]=recordId&fields[]=type>`_

- Querying on a specific field: `/db/named_entities?type=HealthCondition <http://hack4europe.kbresearch.nl/db/named_entities?limit=10&type=HealthCondition>`_



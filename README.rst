The Portal Thingy Hack4Europe Hackathon entry
=============================================

Live Demo
---------
`Portal Thingy <http://hack4europe.kbresearch.nl>`_.

Description
-----------
This portal enables users to search the Europeana collections and to enrich it metadata using a local mongodb and remote API's.


Adding the API keys
-------------------
In order for the portal to actually do anything with the remote API's two API keys need to be entered in the file `client/index.html <https://github.com/renevanderark/hack4europe/blob/master/client/index.html>`_. The Europeana API key goes on `line 23 <https://github.com/renevanderark/hack4europe/blob/master/client/index.html#L23>`_. And the Alchemy API key (which is restricted to non-profit research activity) goes on `line 28 <https://github.com/renevanderark/hack4europe/blob/master/client/index.html#L23>`_.


Running out of the box
----------------------
On a Ubuntu/Debian distribution with Aptitude the ./go.sh shell script should run out of the box, installing all prerequisites and starting the portal on a local host. Installing the prerequisites can take a long time, seeing as the entire google V8 engine and node.js need to be built from source. Probably it's best to run it as a sudo user. Even better is to have a good look at the script and only install the prerequisites that you do not have installed yet.

- Starting the portal::

    $ sudo ./go.sh

- If everything went well, the portal can be vistied locally at your `local host on port 8000 <http://localhost:8000/>`_.

More on the Project
-------------------
The portal uses a mongodb installment to store user's contributions. New records can be added through RESTful local-domain ajax calls, querying on the database can be done cross-domain as well, using JSONP. `More about the database <https://github.com/renevanderark/hack4europe/tree/master/srv>`_. For instructions on how to let client code talk to the db go `here <https://github.com/renevanderark/hack4europe/tree/master/client>`_

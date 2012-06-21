Client
======

The portal's activities.

Adding the API keys
-------------------
In order for the portal to actually do anything with the remote API's two API keys need to be entered in the file `index.html <https://github.com/renevanderark/hack4europe/blob/master/client/index.html>`_. The Europeana API key goes on `line 23 <https://github.com/renevanderark/hack4europe/blob/master/client/index.html#L23>`_. And the Alchemy API key (which is restricted to non-profit research activity) goes on `line 28 <https://github.com/renevanderark/hack4europe/blob/master/client/index.html#L23>`_.

Storing a record to the database
---------------

Easiest is to use the 'upsert' action - I only use that. I wrote handlers for other types of updates, but upserting is fun and easy: if the record defined by your query exists it gets updated, otherwise it gets created.

Example from the project::

	var data = {
		recordId: "[your record id; is not necessary but makes sense if you want to link to some other data]",
		lemma: "Your_Wiki_lemma",
		type: entity.type,
		text: entity.text
	};
	$.ajax({
		type: "POST",
		url: "db/named_entities",
		data: {upsert: data, set: data}, /** the actual instructions, ('upsert' defines the record to find, 'set' is the actual update) **/
		success: function(data) {
			saveButton.attr("disabled", "true");
			saveButton.html("Enrichment saved");
		}
	});

Another example from the project::

	var latLon = {lat: 12.34, lon: 56.7};
	$.ajax({
		type: "POST",
		url: "db/geolocations",
		data: {
			upsert: {recordId: recordId, geo: latLon },
			set: {recordId: recordId, geo: latLon }
		}
	});

Querying the db using ajax 
----
...is done asynchronously, because stuff gets streamed, so you need the entire block of data to make sure everything is in before another you do another query call that messes up the first call... Believe me, it happens::

	$.ajax("db/geolocations", {
		async: false,
		data: {recordId: recordId},
		success: function(data) {
			if(data[0] != null) {
				$.each(data, function(i, record) {
					if(record == null) { return; }
					console.log(record);
				});
			}
		}
	});


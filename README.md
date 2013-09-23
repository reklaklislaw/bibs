bibs
====


Deprecated
----------
<h3> bibs is replaced by <a href='https://github.com/reklaklislaw/rest_easy'>'rest_easy'</a>
</h3>



Bibliographic Search
------------


License: GPLv3

An experimental python module with the goal of a shared syntax for querying RESTful Bibliographic APIs.

(in development)

Requires python 2.7 or greater.

Example
-----

	from bibs.bibs import Bibs

	b = Bibs()
	results = b.search("api_key->xxxx:sourceResource->title->Tom Sawyer", 'dplav2', 'items')

where **api_key->xxxx:sourceResource->title->Tom Sawyer** is the *query*, **dplav2** is the bibliographic *source*, and **items** is the *api*. 


Query
-----

Queries are composed of one or more key/value pairs. Keys and their values are to be separated by an **->**, while each pair is separated by an **:**. Key/values may also be nested. For instance, to search Open Library's "query" api for all editions that contain a Title of Contents with an entry for page 19:

	b.search("types->edition:table_of_contents->pagenum->19", 'openlibrary', 'query') 

Multiple values may be indicated by an **|** separating the values, like:

	 b.search('types->edition:subjects->war|peace', 'openlibrary', 'query')

Or,

	 b.search('oclc->424023|isbn->0030110408', 'hathitrust', 'multi_volumes_full')


Optional arguments are to be preceded by an **@**, like:

	 b.search('types->edition:title->Macbeth @publish_date->null:limit->5', 'openlibrary', 'query')

where **publish_date->null** will request data from the **publish_date** field for all editions found whose title is 'Macbeth', and **limit->5** will limit the results to five.  

If you need to include one of the special characters ( **:** **->** **@** **|** ) in your query, escape it by preceding it with **\**


One can pass the argument **return_format** to search() to convert your results to a format not supported by the API. Accepted values are **json**, **xml**, or **object**. **object** will either return an object of class 'QueryObject' or a list of such, depending on the nature of the data being converted. (Also note that python does not allow special characters in variable names, and so when necessary they will be changed to a double underscore, for example '@xmlns:xli' will become '__xmlns__xli'. One can also specify types for the object to inherit from by assigning a tuple of types to the argument **inherit_from**.

**pretty_print** is another optional argument which when set to **True** will pretty print your search results, in addition to returning them.


<h3>Prototypes</h3>
TODO -> documentation


<h3>Fields</h3>
TODO -> documentation


<h3>Options</h3>
TODO -> documentation


Source
-----

Each source is mapped in YAML, providing the information necessary to parse queries and the documentation on how to form queries. 


Currently supported Sources:

- dplav2           (<a href='http://dp.la'>Digital Public Library of America</a>)
- bhlv2            (<a href='http://biodiversityheritagelibrary.org'>Biodiversity Heritage Library</a>)
- hathitrust       (<a href='http://hathitrust.org'>Hathi Trust</a>)
- openlibrary      (<a href='http://openlibrary.org'>Open Library</a>)
- europeanav2      (<a href='http://europeana.eu'>Europeana</a>)
- googlebooks      (<a href='http://books.google.com'>Google Books</a>)
- locsruv1.1       (<a href='http://loc.gov/standards/sru'>Library of Congress SRU</a>)
- librarythingv1.1 (<a href='http://www.librarything.com'>Library Thing</a>)
- dlesev1.1        (<a href='http://www.dlese.org'>Digital Library for Earth System Education</a>)


Help
-----

A help function is provided for getting information about the supported sources and APIs.

       	b.help()

...will print the currently supported sources.

     	b.help('librarythingv1.1')

...will print the supported APIs and information concerning source librarythingv1.1.

     	b.help('librarythingv1.1', 'rest')

...will print information concerning librarythingv1.1's API 'rest', including grammer and a high-level view of the accepted parameters, and options. 

One can get specific information about the API's parameters by providing a third 'drill-down' style argument using the same syntax for forming queries:
    
	b.help('librarythingv1.1', 'rest', 'params')

...will print the complete list of parameters for 'rest', while

     	b.help('librarythingv1.1', 'rest', 'params->ck->getwork')

...will print the specs for the 'ck' prototype's 'getwork' parameter.


Installation
-----

- Download and unpack the zip.
- python 2.7 -> "pip install bibs/ -r bibs/requirements.txt" or run "python bibs/setup.py install" and install the dependencies yourself.
- python 3.x  -> "pip-3.x install bibs/ -r bibs/requirements.txt" or run "python bibs/setup.py install" and install the dependencies yourself.

Dependencies
- lxml
- PyYAML
- xmltodict
- dicttoxml

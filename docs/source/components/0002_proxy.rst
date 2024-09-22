=====
Proxy
=====

Any repository object that is a subclass of :code:`ore:Aggregation` can be ordered by being represented by a :code:`ore:Proxy`.
This includes :code:`pcdm:Collection`, :code:`pcdm:Object`, and any subclass of :code:`pcdm:Object` including
:code:`pcdmworks:FileSet` or :code:`pcdmworks:Range`. A :code:`pcdm:File` is not an instance of a :code:`ore:Aggregation`
so it cannot be ordered unless it is a part of :code:`pcdmworks:FileSet`.

Any member of a work that does not have an ordering proxy node is assumed to be unordered according to the PCDM ordering
extension.  To keep things simple for us, we assume multi-canvased works will have a proxy node for any canvas.  Anything
without a proxy node might be accessible but not as an ordered canvas. Similarly, all our collections are unordered and
do not have proxy nodes related to a specific work.

-------------
Minimum Model
-------------

A simple fileset may have many more properties, but should look something like this:

.. code-block:: turtle

    @prefix ex: <http://example.org/> .
    @prefix iana: <http://www.iana.org/assignments/relation/> .
    @prefix ore: <http://www.openarchives.org/ore/1.0/datamodel#> .
    @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

    ex:ProxyForPageTwo a ore:Proxy ;
        ore:proxyIn ex:BookWork ;
        ore:proxyFor ex:BookPageTwoFileset ;
        iana:prev ex:ProxyForPageOne ;
        iana:next ex:ProxyForPageThree .

--------------------
Rules and Guidelines
--------------------

A Proxy **MUST**:

* be an instance of :code:`ore:Proxy` via the :code:`rdf:type` property.
* have :code:`1` :code:`ore:proxyFor` that links to the resource being ordered.
* have :code:`1` :code:`ore:proxyIn` that links ot the aggregation the resource is being ordered in.

A Proxy **MUST NOT**:

* be included in multiple aggregations. When this is needed, an additional proxy must be minted.

A Proxy **SHOULD**:

* have a :code:`iana:prev` property if not the the first item in an ordered list that links to the resource before the current resource.
* have a :code:`iana:next` property if not the the last item in an ordered list that links to the resource after the current resource

--------
Examples
--------

A Proxy for a Page of a Book
============================

A book-like object with ordered pages should have a proxy for each fileset including the Image, HOCR, and OCR.

In this example, 1 fileset with files is shown, along with a corresponding Proxy and two other proxies with their filesets
omitted.

.. code-block:: turtle

    @prefix ex: <http://example.org/> .
    @prefix iana: <http://www.iana.org/assignments/relation/> .
    @prefix ore: <http://www.openarchives.org/ore/1.0/datamodel#> .
    @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix pcdm: <http://pcdm.org/models#> .
    @prefix pcdmworks: <http://pcdm.org/works#> .
    @prefix pcdmuse: <http://pcdm.org/use#> .
    @prefix pcdmff: <http://pcdm.org/file-format-types#> .
    @prefix fedora: <http://fedora.info/definitions/v4/repository#> .

    ex:ProxyForPageOne a ore:Proxy ;
        ore:proxyIn ex:BookWork ;
        ore:proxyFor ex:BookPageOneFileset ;
        iana:next ex:ProxyForPageTwo .

    ex:ProxyForPageTwo a ore:Proxy ;
        ore:proxyIn ex:BookWork ;
        ore:proxyFor ex:BookPageTwoFileset ;
        iana:prev ex:ProxyForPageOne ;
        iana:next ex:ProxyForPageThree .

    ex:ProxyForPageThree a ore:Proxy ;
        ore:proxyIn ex:BookWork ;
        ore:proxyFor ex:BookPageThreeFileset ;
        iana:prev ex:ProxyForPageTwo .

    ex:BookPageOneFileset a pcdmworks:Fileset ;
        rdfs:label "Example Book: Page 1" ;
        pcdm:memberOf ex:BookWork ;
        pcdm:hasFile ex:Image, ex:HOCR, ex:OCR .

    ex:Image a pcdmuse:ServiceFile, pcdmff:Image ;
        pcdm:fileOf ex:BookPageOneFileset ;
        fedora:hasBinary <https://path/to/image_0001.jp2> .

    ex:HOCR a pcdmff:HTML ;
        pcdm:fileOf ex:BookPageOneFileset ;
        fedora:hasBinary <https://path/to/image_0001.html> .

    ex:OCR a pcdmuse:ExtractedText ;
        pcdm:fileOf ex:BookPageOneFileset ;
        fedora:hasBinary <https://path/to/image_0001.txt> .


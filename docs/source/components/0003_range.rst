=====
Range
=====

Some works such as books, compound objects, or complex audio visual works may have a hierarchy that describes the
various sections and subsections of an item.  By creating a :code:`Range` to represent each section and subsection,
a viewer can leverage this data and provide users a way to navigate across a work using each these resources.

The `PCDM Works Extension <https://pcdm.org/2021/04/09/works>`_ defines multiple two classes for modelling this type of
data: :code:`pcdmworks:TopRange` and :code:`pcdmworks:Range`. These classes were informed by the
`IIIF Presentation API <https://iiif.io/api/presentation/3.0/#54-range>`_. Prior to version 3 of the API specification,
the top most Range required a :code:`viewingHint="top"` property, and the :code:`pcdmworks:TopRange` class provided
a way to distinguish between the two.  As of version 3.0 of the API, this requirement is no longer needed and thus we do
not need both classes.

-------------
Minimum Model
-------------

A simple :code:`Range` may have many more properties, but should look something like this:

.. code-block:: turtle

    @prefix ex: <http://example.org/> .
    @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix pcdm: <http://pcdm.org/models#> .
    @prefix pcdmworks: <http://pcdm.org/works#> .

    ex:Range a pcdmworks:Range ;
        rdfs:label "An Example Top Level Range" ;
        pcdm:memberOf ex:Work ;
        pcdm:hasMember ex:FileSet .

--------------------
Rules and Guidelines
--------------------

A Range **MUST**:

* be an instance of :code:`pcdmworks:Range` via the :code:`rdf:type` property.
* be related to a parent Work via :code:`pcdm:memberOf` or :code:`pcdm:hasMember`.
* be related to a :code:`pcdmworks:FileSet` or other :code:`pcdm:Object` instance via :code:`pcdm:hasMember`.
* have a label in a property like :code:`rdfs:label` unless its not intended for viewing. This requirement comes from IIIF presentation's requirement for client viewers making use of these concepts.
* use :code:`iana` properties and :code:`ore:Proxy` classes for ordering of the ranges.

A Range **MAY**:

* have other descriptive metadata properties.

-------------------
Real World Examples
-------------------

A Book with Minimal Hierarchy
=============================

This object builds off the example in the proxy section, but eliminates some nodes including the :code:`pcdm:File` resources,
the parent book, and a couple of referenced chapters to make the relevant parts of this example easier to understand.

For full examples of a completed object, see the work-types or recipes section.

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

    # This is a Proxy for Page 1 that will be Canvas 1 in a IIIF Manifest and is the Front Cover
    ex:ProxyForPageOne a ore:Proxy ;
        ore:proxyIn ex:BookWork ;
        ore:proxyFor ex:BookPageOneFileset ;
        iana:next ex:ProxyForPageTwo .

    # This is a Proxy for Page 6 that will be Canvas 6 in a IIIF Manifest and is the start of Chapter 1
    ex:ProxyForPageSix a ore:Proxy ;
        ore:proxyIn ex:BookWork ;
        ore:proxyFor ex:BookPageSixFileset ;
        iana:prev ex:ProxyForPageFive ;
        iana:next ex:ProxyForPageSeven .

    # This is a Proxy for Page 33 that will be Canvas 33 in a IIIF Manifest and is the back cover
    ex:ProxyForPageThirtyThree a ore:Proxy ;
        ore:proxyIn ex:BookWork ;
        ore:proxyFor ex:BookPageThirtyThreeFileset ;
        iana:prev ex:ProxyForPageThirtyTwo .

    # This is a Fileset that includes the files used by Canvas 1 in the presentation manifest.
    ex:BookPageOneFileset a pcdmworks:Fileset ;
        rdfs:label "Page One" ;
        pcdm:memberOf ex:BookWork ;
        pcdm:hasFile ex:Image, ex:HOCR, ex:OCR .

    # This is a Range that represents the Front Cover of a Book and points to the page 1 fileset
    ex:FrontCover a pcdmworks:Range ;
        rdfs:label "Front Cover" ;
        pcdm:memberOf ex:BookWork ;
        pcdm:hasMember ex:BookPageOneFileset .

    # This is a Proxy for the front cover range in a IIIF Manfiest
    ex:ProxyForFrontCover a ore:Proxy ;
        ore:proxyIn ex:BookWork ;
        ore:proxyFor ex:FrontCover ;
        iana:next ex:ChapterOne .

    # This is a Range that represents Chapter 1 of a Book and points to the page 6 fileset
    ex:ChapterOne a pcdmworks:Range ;
        rdfs:label "Chapter One" ;
        pcdm:memberOf ex:BookWork ;
        pcdm:hasMember ex:BookPageSixFileset .

    # This is a Proxy for the chapter one range in a IIIF Manfiest
    ex:ProxyForChapterOne a ore:Proxy ;
        ore:proxyIn ex:BookWork ;
        ore:proxyFor ex:ChapterOne ;
        iana:next ex:ChapterTwo .

    # This is a Range that represents Chapter 33 of a Book and points to the page 33 fileset
    ex:BackCover a pcdmworks:Range ;
        rdfs:label "Back Cover" ;
        pcdm:memberOf ex:BookWork ;
        pcdm:hasMember ex:BookPageThirtyThreeFileset .

    # This is a Proxy for the back cover in a IIIF Manfiest
    ex:ProxyForBackCover a ore:Proxy ;
        ore:proxyIn ex:BookWork ;
        ore:proxyFor ex:BackCover ;
        iana:prev ex:ChapterThree .

A Book with Complex Hierarchy
=============================

We need a more complex example as the above likely won't work for places like National Library of Wales.

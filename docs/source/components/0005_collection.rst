==========
Collection
==========

PCDM defines its own class for collections: :code:`pcdm:Collection`. A Collection is a group of resources that have
descriptive metadata, access metadata, and may link to works and/or collections. By default, member works and
collections are an unordered set, but can be ordered using the ORE Proxy class.

-------------
Minimum Model
-------------

A simple :code:`Collection` instance may have many more properties, but should look something like this:

.. code-block:: turtle

    @prefix ex: <http://example.org/> .
    @prefix pcdm: <http://pcdm.org/models#> .
    @prefix dc: <http://purl.org/dc/elements/1.1/> .

    ex:Collection a pcdm:Collection ;
        dc:title "My Image Collection" ;
        pcdm:hasMember ex:ImageOne, ex:ImageTwo, ex:ImageThree, ex:ImageFour .

--------------------
Rules and Guidelines
--------------------

A Collection **MUST**:

* be an instance of :code:`pcdm:Collection` via the :code:`rdf:type` property.
* be related to parent Collections or child works via :code:`pcdm:memberOf` or :code:`pcdm:hasMember` properties.
* have mandatory descriptive elements as stated by `Metadata Guidelines for Digital Resources at Texas A&M University Libraries <https://drive.google.com/file/d/1uN8FHSM8WrziIImwJ1ji6H3GxwGh4Cwe/view?usp=sharing>`_

A Collection **MAY**:

* have other descriptive metadata properties.
* have many objects or filesets.
* have proxies if the works in the collection require order.

A Collection **MUST NOT**:

* contain child files directly.

-------------------
Real World Examples
-------------------

An Unordered Collection with many Works
=======================================

Here is a very basic collection:

.. code-block:: turtle

    @prefix ex: <http://example.org/> .
    @prefix pcdm: <http://pcdm.org/models#> .
    @prefix dc: <http://purl.org/dc/elements/1.1/> .

    ex:Collection a pcdm:Collection ;
        dc:title "Image Collection" ;
        pcdm:hasMember ex:ImageOne, ex:ImageTwo, ex:ImageThree, ex:ImageFour .

    ex:ImageOne a pcdmworks:Work ;
        dc:title "A Map" ;
        dc:rights <http://rightsstatements.org/vocab/InC-EDU/1.0/> ;
        dc:format "reformatted digital" ;
        dc:type "StillImage", "Text" ;
        dc:publisher "Texas A & M University. Libraries" ;
        pcdm:memberOf ex:Collection ;
        pcdm:hasMember ex:MapFront, ex:MapBack ;
        pcdm:hasFile ex:GISDataSet .

    ex:ImageTwo a pcdmworks:Work ;
        dc:title "A Picture of a Cat" ;
        dc:rights <http://rightsstatements.org/vocab/InC-EDU/1.0/> ;
        dc:format "reformatted digital" ;
        dc:type "StillImage", "Text" ;
        dc:publisher "Texas A & M University. Libraries" ;
        pcdm:memberOf ex:Collection ;
        pcdm:hasMember ex:TheActualImage ;


A Collection with Many Works and an Attached FileSet
====================================================

An Ordered Collection
=====================

A Collection with No Works But Many Collections
===============================================



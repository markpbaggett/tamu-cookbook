=======
FileSet
=======

Often, a work may have a group of interconnected files that must be organized together in order to be understood.
For this specific use case, the PCDM Works ontology defines the :code:`pcdmworks:FileSet`, a subclass of a :code:`pcdm:Object`.

-------------
Minimum Model
-------------

.. code-block:: turtle

    @prefix ex: <http://example.org/> .
    @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix pcdm: <http://pcdm.org/models#> .
    @prefix pcdmworks: <http://pcdm.org/works#> .


    ex:FileSet a pcdmworks:FileSet ;
        pcdm:memberOf ex:Work ;
        pcdm:hasFile ex:FileOne, ex:FileTwo, ex:FileThree .

--------------------
Rules and Guidelines
--------------------

A FileSet **MUST**:

* be an instance of :code:`pcdmworks:FileSet` via the :code:`rdf:type` property.
* have 1 :code:`pcdm:hasFile` property with :code:`1-n` :code:`pcdm:File` resources.

A FileSet **SHOULD**:

A FileSet **MAY**:

* have a :code:`rdfs:label` to make the resource more semantically understandable.
* have other descriptive metadata properties.

-------------------
Real World Examples
-------------------

The Service files of a page of a book
=====================================

A Book work may have many pages.  Each page may be represented by an image of the page, with OCR and HOCR or ALTO XML
that coordiante to specific pixels on the page image.  A :code:`FileSet` should be used in this instance:

.. code-block:: turtle

    @prefix ex: <http://example.org/> .
    @prefix fedora: <http://fedora.info/definitions/v4/repository#> .
    @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix pcdm: <http://pcdm.org/models#> .
    @prefix pcdmworks: <http://pcdm.org/works#> .
    @prefix pcdmuse: <http://pcdm.org/use#> .
    @prefix pcdmff: <http://pcdm.org/file-format-types#> .

    ex:PageOneOfABook a pcdmworks:Fileset ;
        rdfs:label "Example Book: Page 1" ;
        pcdm:memberOf ex:Book ;
        pcdm:hasFile ex:Image, ex:HOCR, ex:OCR .

    ex:Image a pcdmuse:ServiceFile, pcdmff:Image ;
        pcdm:fileOf ex:PageOneOfABook ;
        fedora:hasBinary <https://path/to/image_0001.jp2> .

    ex:HOCR a pcdmff:HTML ;
        pcdm:fileOf ex:PageOneOfABook ;
        fedora:hasBinary <https://path/to/image_0001.html> .

    ex:OCR a pcdmuse:ExtractedText ;
        pcdm:fileOf ex:PageOneOfABook ;
        fedora:hasBinary <https://path/to/image_0001.txt> .
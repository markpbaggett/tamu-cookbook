=======================================
Simplest Image - No Filesets or Proxies
=======================================

--------
Use Case
--------

A librarian wants to put an Image work online in an exhibit so that it can be shared and potentially annotated. The work
consists of one file, :code:`image.jpg`, and descriptive metadata about the file.

--------------------
Implementation Notes
--------------------

In order to store the item in Fedora, the parent resource will be an instance of :code:`pcdmworks:Work`. This object
will include the descriptive metadata.

Our components allow for flexibility in how we approach the rest of the implementation. The relationship between the
image file and the :code:`pcdmworks:Work` can be expressed either through a :code:`pcdm:hasFile` with an attached
:code:`pcdm:File` or a :code:`pcdm:hasMember` with a :code:`pcdmworks:FileSet`. The latter is more complex, but may provide
greater consistency across all works in a repository. Many Fedora applications including Hyrax and and Hyku choose to
follow this more complex option in favor of consistency. For this exercise though, we will use the former option.

Fedora Implementation
=====================

These are the nodes for

.. code-block:: turtle

    @prefix ex: <http://example.org/> .
    @prefix fedora: <http://fedora.info/definitions/v4/repository#> .
    @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix pcdm: <http://pcdm.org/models#> .
    @prefix pcdmworks: <http://pcdm.org/works#> .
    @prefix pcdmuse: <http://pcdm.org/use#> .
    @prefix pcdmff: <http://pcdm.org/file-format-types#> .
    @prefix dc: <http://purl.org/dc/elements/1.1/> .
    @prefix nepomuk: <http://www.semanticdesktop.org/ontologies/2007/03/22/nfo#> .
    @prefix exif: <http://www.w3.org/2003/12/exif/ns#> .
    @prefix ebucore: <http://www.ebu.ch/metadata/ontologies/ebucore/ebucore#> .
    @prefix premis: <http://www.loc.gov/premis/rdf/v1#> .

    # This is the Work.
    ex:Work a pcdmworks:Work ;
        dc:title "Simplest Image" ;
        dc:rights <http://rightsstatements.org/vocab/NoC-CR/1.0/> ;
        dc:format "born digital" ;
        dc:type "StillImage", "Text" ;
        dc:publisher "Texas A & M University. Libraries" ;
        pcdm:memberOf ex:Collection ;
        pcdm:hasFile ex:SimplestImageFile .

    # This is the Image Canvas.
    ex:SimplestImageFile a pcdmuse:IntermediateFile, pcdmff:Image ;
        pcdm:fileOf ex:Work ;
        fedora:hasBinary <https://markpbaggett.github.io/tamu-cookbook/fixtures/images/simplest-image.png> ;
        ebucore:width "600"^^<http://www.w3.org/2001/XMLSchema#string> ;
        ebucore:fileSize "12288"^^<http://www.w3.org/2001/XMLSchema#string> ;
        premis:hasSize "12288"^^<http://www.w3.org/2001/XMLSchema#long> ;
        exif:orientation "normal*"^^<http://www.w3.org/2001/XMLSchema#string> ;
        exif:colorSpace "RGB"^^<http://www.w3.org/2001/XMLSchema#string> ;
        ebucore:hasMimeType "image/png"^^<http://www.w3.org/2001/XMLSchema#string> ;
        ebucore:height "400"^^<http://www.w3.org/2001/XMLSchema#string> ;
        nepomuk:hashValue "da39a3ee5e6b4b0d3255bfef95601890afd80709"^^<http://www.w3.org/2001/XMLSchema#string> ;
        ebucore:filename "simplest-image.png"^^<http://www.w3.org/2001/XMLSchema#string> .

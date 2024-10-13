=============================
File:  Subtypes and Use Cases
=============================

For decades, libraries, archives, and museums have attempted to create a semantic registry for file formats to help
institutions preserve and understand digital content. The first and most successful attempt at this historically has been
`PRONOM <https://www.nationalarchives.gov.uk/PRONOM/>`_. In early 2011, PRONOM released its
`Linked Data Version <http://labs.nationalarchives.gov.uk/wordpress/index.php/2011/01/linked-data-and-pronom/>`_, but it
was shuttered several years later. Between 2005 and 2015, other efforts were made in this area in the Global Digital Format
Registry and Unified Digital Format Registry. Unfortunately, both efforts collapsed and the work of both is no longer
available online.

When PCDM started, there was an effort to try and bring UDFR ideas into PCDM via the `File Formats Extension <https://pcdm.org/2015/10/14/file-format-types>`_.
While some context is now lost due to decision making in PCDM, leveraging classes defined here here affords us a straight
forward solution for making interoperability with other formats such as IIIF Presentation easier.

In addition to the File Formats Extension, `PCDM Use Extension <https://pcdm.org/2021/04/09/use>`_ defines classes that
are not directly derived from the projects above but instead are common use cases in repositories.

This section defines some subclasses of :code:`pcdm:File` that may be used in place of or addition to :code:`pcdm:File`.

----------
Philosophy
----------

There are multiple ways to model files. For our purposes, we do not care about capturing every subclass that applies to
a single file. Instead, we want to prescribe and select subclasses that apply to our use cases in as few conepts as possible.
For this reason, we will attempt to apply only one subclass per File unless additional classes are needed to successully
capture semantic meaning.

--------
Canvases
--------

A Canvas, as defined by `IIIF presentation <https://iiif.io/api/presentation/3.0/#53-canvas>`_, acts as a central point
for assembling the different content resources that make up the display of a work. In IIIF, files with a
:code:`motivation="painting"` are added to the canvas and displayed directly to users in a viewer, while other Files may
be served by the viewer indirectly. In our repository, we need a way to differentiate between these types of files. This
section describes the different file types that may be painted on a :code:`canvas`.

Image
=====

.. important::

    Images may be stored as a file of a work but not intended for display.  For our purposes, these are not Images.

Any images that are painted on a :code:`Canvas` should be an instance of :code:`pcdmff:Image`. Images of pages of books
may need to be a part of a :code:`pcdmworks:FileSet` in order to be understood with OCR. Regardless an image that is painted
on a canvas should look something like this and may have more or fewer triples depending on decisions made elsewhere in
this document:

.. code-block:: turtle

    @prefix ex: <http://example.org/> .
    @prefix fedora: <http://fedora.info/definitions/v4/repository#> .
    @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix pcdm: <http://pcdm.org/models#> .
    @prefix pcdmuse: <http://pcdm.org/use#> .
    @prefix nepomuk: <http://www.semanticdesktop.org/ontologies/2007/03/22/nfo#> .
    @prefix exif: <http://www.w3.org/2003/12/exif/ns#> .
    @prefix ebucore: <http://www.ebu.ch/metadata/ontologies/ebucore/ebucore#> .
    @prefix premis: <http://www.loc.gov/premis/rdf/v1#> .

    ex:Image a pcdmff:Image;
        pcdm:fileOf ex:ImageWork ;
        fedora:hasBinary <https://path/to/preservation%20file.tif> .
        ebucore:width "2106"^^<http://www.w3.org/2001/XMLSchema#string> ;
        ebucore:fileSize "17765536"^^<http://www.w3.org/2001/XMLSchema#string> ;
        premis:hasSize "17765536"^^<http://www.w3.org/2001/XMLSchema#long> ;
        exif:orientation "normal*"^^<http://www.w3.org/2001/XMLSchema#string> ;
        exif:colorSpace "RGB"^^<http://www.w3.org/2001/XMLSchema#string> ;
        ebucore:hasMimeType "image/tiff"^^<http://www.w3.org/2001/XMLSchema#string> ;
        ebucore:height "2808"^^<http://www.w3.org/2001/XMLSchema#string> ;
        nepomuk:hashValue "99d14ee8c28517e10c637e0e0a675b94"^^<http://www.w3.org/2001/XMLSchema#string> ;
        ebucore:filename "preservation file.tif"^^<http://www.w3.org/2001/XMLSchema#string> ;
        exif:software "Adobe Photoshop CS2 Windows"^^<http://www.w3.org/2001/XMLSchema#string> .


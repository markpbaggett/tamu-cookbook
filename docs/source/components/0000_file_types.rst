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
a file. Instead, we want to prescribe and select subclasses that apply to our use cases.  For this reason, we will often
only use 1 subclass in this document unless the use case is complex enough that it requires two.

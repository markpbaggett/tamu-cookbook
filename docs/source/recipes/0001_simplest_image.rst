==============
Simplest Image
==============

--------
Use Case
--------

A librarian wants to put an Image work online in an exhibit. The work consists of one file, :code:`image.jpg`, and
descriptive metadata.

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


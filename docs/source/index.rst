.. TAMU Work Types and Presentation Recipes documentation master file, created by
   sphinx-quickstart on Fri Sep 13 16:05:20 2024.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

DRAFT: TAMU Work Type Components and Presentation Recipes
=========================================================

This portal contains philosophy, work and file types, and presentation recipes for future models.

At this point, this is mostly a thought exercise to help think about complex content modelling in a repository and
ramifications for consuming and interoperable systems.

The document is split into several sections.  The *Introduction* attempts to provide background about RDF, best practices,
our current repository, and things that must be decided before anything here can be used. The *Components* section
attempts to define all the individual resources that might be found in a Fedora repository, their shapes, and how they
might relate to other resources. The *Work Types* section does not yet exist and will hopefully be dropped completely
in lieu of just flexible component parts that can be easily distinguished, reused, and identified by librarians and other
people responsible for populating the repository. In the hopes that work types can be dropped completely, a *Recipes*
section will be added here that explains how a known use case should be modelled using the components described and how
they are ultimately transformed to IIIF Presentation 3 and other API specifications outside of the repository using
external tooling.

.. toctree::
   :maxdepth: 1
   :caption: Introduction
   :glob:

   contents/*

.. toctree::
   :maxdepth: 1
   :caption: Components
   :glob:

   components/*

.. toctree::
   :maxdepth: 1
   :caption: Worktypes
   :glob:

   work-types/*

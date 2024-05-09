``Profiling::ProfilingSection``
===============================

.. role:: cppkokkos(code)
   :language: cppkokkos

Defined in header ``<Kokkos_Profiling_ProfileSection.hpp>``

Usage
-----

.. code-block:: cpp

   Kokkos::Profiling::ProfilingSection section("label");
   section.start();
   // <code>
   section.stop();
    


The class ``ProfilingSection`` is a section ID wrapper that provides a
convenient `RAII-style <https://en.cppreference.com/w/cpp/language/raii>`_
mechanism to manage a user-defined profiling section.

When a ``ProfilingSection`` object is created, a profiling section is created
with the user-provided stringand the objects holds on to the section ID.

When control leaves the scope in which the ``ProfilingSection`` object was
created, the ``ProfilingSection`` is destructed, and the underlying section is
properly destroyed.

The ``ProfilingSection`` class is non-copyable.


.. cppkokkos:Function:: ProfilingSection(std::string const& sectionName);

   Constructs a section with user-provided label.
   Calls ``Profiling::createProfileSection(sectionName, &sectionID);``

.. cppkokkos:Function:: ~ProfilingSection();

   Deletes the section.
   Calls ``Profiling.destroyProfileSection(sectionID);``

.. cppkokkos:Function:: void start();

   Starts the section.
   Calls ``Profiling::startSection(sectionID);``

.. cppkokkos:Function:: void stop();

   Ends the section.
   Calls ``Profiling::stopSection(sectionID);``


**See also**

`ScopedRegion <scoped_region.html>`_: implements a scope-based region ownership wrapper

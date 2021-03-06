target_precompile_headers
-------------------------

Add a list of header files to precompile.

.. code-block:: cmake

  target_precompile_headers(<target>
    <INTERFACE|PUBLIC|PRIVATE> [header1...]
    [<INTERFACE|PUBLIC|PRIVATE> [header2...] ...])

Adds header files to :prop_tgt:`PRECOMPILE_HEADERS` or
:prop_tgt:`INTERFACE_PRECOMPILE_HEADERS` target properties.

Precompiling header files can speed up compilation by creating a partially
processed version of some header files, and then using that version during
compilations rather than repeatedly parsing the original headers.

The named ``<target>`` must have been created by a command such as
:command:`add_executable` or :command:`add_library` and must not be an
:ref:`ALIAS target <Alias Targets>`.

The ``INTERFACE``, ``PUBLIC`` and ``PRIVATE`` keywords are required to
specify the scope of the following arguments.  ``PRIVATE`` and ``PUBLIC``
items will populate the :prop_tgt:`PRECOMPILE_HEADERS` property of
``<target>``.  ``PUBLIC`` and ``INTERFACE`` items will populate the
:prop_tgt:`INTERFACE_PRECOMPILE_HEADERS` property of ``<target>``.
(:ref:`IMPORTED targets <Imported Targets>` only support ``INTERFACE`` items.)
Repeated calls for the same ``<target>`` append items in the order called.

Arguments to ``target_precompile_headers`` may use "generator expressions"
with the syntax ``$<...>``.
See the :manual:`cmake-generator-expressions(7)` manual for available
expressions.  See the :manual:`cmake-compile-features(7)` manual for
information on compile features and a list of supported compilers.

.. code-block:: cmake

  target_precompile_headers(<target>
    PUBLIC
      "project_header.h"
    PRIVATE
      <unordered_map>
  )

Header files will be double quoted if they are not specified with double
quotes or angle brackets.

See Also
^^^^^^^^

For disabling precompile headers for specific targets there is the
property :prop_tgt:`DISABLE_PRECOMPILE_HEADERS`.

For skipping certain source files there is the source file property
:prop_sf:`SKIP_PRECOMPILE_HEADERS`.

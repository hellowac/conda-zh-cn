:py:mod:`enums`
===============

.. py:module:: conda.models.enums

.. autoapi-nested-parse::

   Collection of enums used throughout conda.



Classes
-------

.. autoapisummary::

   conda.models.enums.Arch
   conda.models.enums.Platform
   conda.models.enums.FileMode
   conda.models.enums.LinkType
   conda.models.enums.PathType
   conda.models.enums.PackageType
   conda.models.enums.NoarchType




.. py:class:: Arch(*args, **kwds)


   Bases: :py:obj:`enum.Enum`

   Create a collection of name/value pairs.

   Example enumeration:

   >>> class Color(Enum):
   ...     RED = 1
   ...     BLUE = 2
   ...     GREEN = 3

   Access them by:

   - attribute access:

     >>> Color.RED
     <Color.RED: 1>

   - value lookup:

     >>> Color(1)
     <Color.RED: 1>

   - name lookup:

     >>> Color['RED']
     <Color.RED: 1>

   Enumerations can be iterated over, and know how many members they have:

   >>> len(Color)
   3

   >>> list(Color)
   [<Color.RED: 1>, <Color.BLUE: 2>, <Color.GREEN: 3>]

   Methods can be added to enumerations, and members can have their own
   attributes -- see the documentation for details.

   .. py:attribute:: x86
      :value: 'x86'

      

   .. py:attribute:: x86_64
      :value: 'x86_64'

      

   .. py:attribute:: arm64
      :value: 'arm64'

      

   .. py:attribute:: armv6l
      :value: 'armv6l'

      

   .. py:attribute:: armv7l
      :value: 'armv7l'

      

   .. py:attribute:: aarch64
      :value: 'aarch64'

      

   .. py:attribute:: ppc64
      :value: 'ppc64'

      

   .. py:attribute:: ppc64le
      :value: 'ppc64le'

      

   .. py:attribute:: riscv64
      :value: 'riscv64'

      

   .. py:attribute:: s390x
      :value: 's390x'

      

   .. py:attribute:: wasm32
      :value: 'wasm32'

      

   .. py:attribute:: z
      :value: 'z'

      

   .. py:method:: from_sys()
      :classmethod:


   .. py:method:: __json__()



.. py:class:: Platform(*args, **kwds)


   Bases: :py:obj:`enum.Enum`

   Create a collection of name/value pairs.

   Example enumeration:

   >>> class Color(Enum):
   ...     RED = 1
   ...     BLUE = 2
   ...     GREEN = 3

   Access them by:

   - attribute access:

     >>> Color.RED
     <Color.RED: 1>

   - value lookup:

     >>> Color(1)
     <Color.RED: 1>

   - name lookup:

     >>> Color['RED']
     <Color.RED: 1>

   Enumerations can be iterated over, and know how many members they have:

   >>> len(Color)
   3

   >>> list(Color)
   [<Color.RED: 1>, <Color.BLUE: 2>, <Color.GREEN: 3>]

   Methods can be added to enumerations, and members can have their own
   attributes -- see the documentation for details.

   .. py:attribute:: freebsd
      :value: 'freebsd'

      

   .. py:attribute:: linux
      :value: 'linux'

      

   .. py:attribute:: win
      :value: 'win32'

      

   .. py:attribute:: openbsd
      :value: 'openbsd5'

      

   .. py:attribute:: osx
      :value: 'darwin'

      

   .. py:attribute:: zos
      :value: 'zos'

      

   .. py:attribute:: emscripten
      :value: 'emscripten'

      

   .. py:attribute:: wasi
      :value: 'wasi'

      

   .. py:method:: from_sys()
      :classmethod:


   .. py:method:: __json__()



.. py:class:: FileMode(*args, **kwds)


   Bases: :py:obj:`enum.Enum`

   Create a collection of name/value pairs.

   Example enumeration:

   >>> class Color(Enum):
   ...     RED = 1
   ...     BLUE = 2
   ...     GREEN = 3

   Access them by:

   - attribute access:

     >>> Color.RED
     <Color.RED: 1>

   - value lookup:

     >>> Color(1)
     <Color.RED: 1>

   - name lookup:

     >>> Color['RED']
     <Color.RED: 1>

   Enumerations can be iterated over, and know how many members they have:

   >>> len(Color)
   3

   >>> list(Color)
   [<Color.RED: 1>, <Color.BLUE: 2>, <Color.GREEN: 3>]

   Methods can be added to enumerations, and members can have their own
   attributes -- see the documentation for details.

   .. py:attribute:: text
      :value: 'text'

      

   .. py:attribute:: binary
      :value: 'binary'

      

   .. py:method:: __str__()

      Return str(self).



.. py:class:: LinkType(*args, **kwds)


   Bases: :py:obj:`enum.Enum`

   Create a collection of name/value pairs.

   Example enumeration:

   >>> class Color(Enum):
   ...     RED = 1
   ...     BLUE = 2
   ...     GREEN = 3

   Access them by:

   - attribute access:

     >>> Color.RED
     <Color.RED: 1>

   - value lookup:

     >>> Color(1)
     <Color.RED: 1>

   - name lookup:

     >>> Color['RED']
     <Color.RED: 1>

   Enumerations can be iterated over, and know how many members they have:

   >>> len(Color)
   3

   >>> list(Color)
   [<Color.RED: 1>, <Color.BLUE: 2>, <Color.GREEN: 3>]

   Methods can be added to enumerations, and members can have their own
   attributes -- see the documentation for details.

   .. py:attribute:: hardlink
      :value: 1

      

   .. py:attribute:: softlink
      :value: 2

      

   .. py:attribute:: copy
      :value: 3

      

   .. py:attribute:: directory
      :value: 4

      

   .. py:method:: __int__()


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: __json__()



.. py:class:: PathType(*args, **kwds)


   Bases: :py:obj:`enum.Enum`

   Refers to if the file in question is hard linked or soft linked. Originally designed to be used
   in paths.json

   .. py:attribute:: hardlink
      :value: 'hardlink'

      

   .. py:attribute:: softlink
      :value: 'softlink'

      

   .. py:attribute:: directory
      :value: 'directory'

      

   .. py:attribute:: linked_package_record
      :value: 'linked_package_record'

      

   .. py:attribute:: pyc_file
      :value: 'pyc_file'

      

   .. py:attribute:: unix_python_entry_point
      :value: 'unix_python_entry_point'

      

   .. py:attribute:: windows_python_entry_point_script
      :value: 'windows_python_entry_point_script'

      

   .. py:attribute:: windows_python_entry_point_exe
      :value: 'windows_python_entry_point_exe'

      

   .. py:method:: basic_types()


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: __json__()



.. py:class:: PackageType(*args, **kwds)


   Bases: :py:obj:`enum.Enum`

   Create a collection of name/value pairs.

   Example enumeration:

   >>> class Color(Enum):
   ...     RED = 1
   ...     BLUE = 2
   ...     GREEN = 3

   Access them by:

   - attribute access:

     >>> Color.RED
     <Color.RED: 1>

   - value lookup:

     >>> Color(1)
     <Color.RED: 1>

   - name lookup:

     >>> Color['RED']
     <Color.RED: 1>

   Enumerations can be iterated over, and know how many members they have:

   >>> len(Color)
   3

   >>> list(Color)
   [<Color.RED: 1>, <Color.BLUE: 2>, <Color.GREEN: 3>]

   Methods can be added to enumerations, and members can have their own
   attributes -- see the documentation for details.

   .. py:attribute:: NOARCH_GENERIC
      :value: 'noarch_generic'

      

   .. py:attribute:: NOARCH_PYTHON
      :value: 'noarch_python'

      

   .. py:attribute:: VIRTUAL_PRIVATE_ENV
      :value: 'virtual_private_env'

      

   .. py:attribute:: VIRTUAL_PYTHON_WHEEL
      :value: 'virtual_python_wheel'

      

   .. py:attribute:: VIRTUAL_PYTHON_EGG_MANAGEABLE
      :value: 'virtual_python_egg_manageable'

      

   .. py:attribute:: VIRTUAL_PYTHON_EGG_UNMANAGEABLE
      :value: 'virtual_python_egg_unmanageable'

      

   .. py:attribute:: VIRTUAL_PYTHON_EGG_LINK
      :value: 'virtual_python_egg_link'

      

   .. py:attribute:: VIRTUAL_SYSTEM
      :value: 'virtual_system'

      

   .. py:method:: conda_package_types()
      :staticmethod:


   .. py:method:: unmanageable_package_types()
      :staticmethod:



.. py:class:: NoarchType(*args, **kwds)


   Bases: :py:obj:`enum.Enum`

   Create a collection of name/value pairs.

   Example enumeration:

   >>> class Color(Enum):
   ...     RED = 1
   ...     BLUE = 2
   ...     GREEN = 3

   Access them by:

   - attribute access:

     >>> Color.RED
     <Color.RED: 1>

   - value lookup:

     >>> Color(1)
     <Color.RED: 1>

   - name lookup:

     >>> Color['RED']
     <Color.RED: 1>

   Enumerations can be iterated over, and know how many members they have:

   >>> len(Color)
   3

   >>> list(Color)
   [<Color.RED: 1>, <Color.BLUE: 2>, <Color.GREEN: 3>]

   Methods can be added to enumerations, and members can have their own
   attributes -- see the documentation for details.

   .. py:attribute:: generic
      :value: 'generic'

      

   .. py:attribute:: python
      :value: 'python'

      

   .. py:method:: coerce(val)
      :staticmethod:




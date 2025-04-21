:py:mod:`windows`
=================

.. py:module:: conda.common._os.windows


Classes
-------

.. autoapisummary::

   conda.common._os.windows.SW
   conda.common._os.windows.ERROR



Functions
---------

.. autoapisummary::

   conda.common._os.windows.get_free_space_on_windows
   conda.common._os.windows.is_admin_on_windows
   conda.common._os.windows._wait_and_close_handle
   conda.common._os.windows.run_as_admin



Attributes
----------

.. autoapisummary::

   conda.common._os.windows.PHANDLE


.. py:data:: PHANDLE

   

.. py:class:: SW


   Bases: :py:obj:`enum.IntEnum`

   Enum where members are also (and must be) ints

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:attribute:: HIDE
      :value: 0

      

   .. py:attribute:: MAXIMIZE
      :value: 3

      

   .. py:attribute:: MINIMIZE
      :value: 6

      

   .. py:attribute:: RESTORE
      :value: 9

      

   .. py:attribute:: SHOW
      :value: 5

      

   .. py:attribute:: SHOWDEFAULT
      :value: 10

      

   .. py:attribute:: SHOWMAXIMIZED
      :value: 3

      

   .. py:attribute:: SHOWMINIMIZED
      :value: 2

      

   .. py:attribute:: SHOWMINNOACTIVE
      :value: 7

      

   .. py:attribute:: SHOWNA
      :value: 8

      

   .. py:attribute:: SHOWNOACTIVATE
      :value: 4

      

   .. py:attribute:: SHOWNORMAL
      :value: 1

      


.. py:class:: ERROR


   Bases: :py:obj:`enum.IntEnum`

   Enum where members are also (and must be) ints

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:attribute:: ZERO
      :value: 0

      

   .. py:attribute:: FILE_NOT_FOUND
      :value: 2

      

   .. py:attribute:: PATH_NOT_FOUND
      :value: 3

      

   .. py:attribute:: BAD_FORMAT
      :value: 11

      

   .. py:attribute:: ACCESS_DENIED
      :value: 5

      

   .. py:attribute:: ASSOC_INCOMPLETE
      :value: 27

      

   .. py:attribute:: DDE_BUSY
      :value: 30

      

   .. py:attribute:: DDE_FAIL
      :value: 29

      

   .. py:attribute:: DDE_TIMEOUT
      :value: 28

      

   .. py:attribute:: DLL_NOT_FOUND
      :value: 32

      

   .. py:attribute:: NO_ASSOC
      :value: 31

      

   .. py:attribute:: OOM
      :value: 8

      

   .. py:attribute:: SHARE
      :value: 26

      


.. py:function:: get_free_space_on_windows(dir_name)


.. py:function:: is_admin_on_windows()


.. py:function:: _wait_and_close_handle(process_handle)

   Waits until spawned process finishes and closes the handle for it.


.. py:function:: run_as_admin(args, wait=True)

   Run command line argument list (`args`) with elevated privileges.

   If `wait` is True, the process will block until completion.

   .. rubric:: 备注

   - no stdin / stdout / stderr pipe support
   - does not automatically quote arguments (i.e. for paths that may contain spaces)

   See:
   - http://stackoverflow.com/a/19719292/1170370 on 20160407 MCS.
   - msdn.microsoft.com/en-us/library/windows/desktop/bb762153(v=vs.85).aspx
   - https://github.com/ContinuumIO/menuinst/blob/master/menuinst/windows/win_elevate.py
   - https://github.com/saltstack/salt-windows-install/blob/master/deps/salt/python/App/Lib/site-packages/win32/Demos/pipes/runproc.py  # NOQA
   - https://github.com/twonds/twisted/blob/master/twisted/internet/_dumbwin32proc.py
   - https://stackoverflow.com/a/19982092/2127762
   - https://www.codeproject.com/Articles/19165/Vista-UAC-The-Definitive-Guide
   - https://github.com/JustAMan/pyWinClobber/blob/master/win32elevate.py



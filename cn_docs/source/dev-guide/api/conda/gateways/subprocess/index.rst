:py:mod:`subprocess`
====================

.. py:module:: conda.gateways.subprocess

.. autoapi-nested-parse::

   Helpler functions for subprocess.




Functions
---------

.. autoapisummary::

   conda.gateways.subprocess._format_output
   conda.gateways.subprocess.any_subprocess
   conda.gateways.subprocess.subprocess_call
   conda.gateways.subprocess._subprocess_clean_env
   conda.gateways.subprocess.subprocess_call_with_clean_env



Attributes
----------

.. autoapisummary::

   conda.gateways.subprocess.Response


.. py:data:: Response

   

.. py:function:: _format_output(command_str, cwd, rc, stdout, stderr)


.. py:function:: any_subprocess(args, prefix, env=None, cwd=None)


.. py:function:: subprocess_call(command: str | os.PathLike | pathlib.Path | collections.abc.Sequence[str | os.PathLike | pathlib.Path], env: dict[str, str] | None = None, path: str | os.PathLike | pathlib.Path | None = None, stdin: str | None = None, raise_on_error: bool = True, capture_output: bool = True)

   This utility function should be preferred for all conda subprocessing.
   It handles multiple tricky details.


.. py:function:: _subprocess_clean_env(env, clean_python=True, clean_conda=True)


.. py:function:: subprocess_call_with_clean_env(command, path=None, stdin=None, raise_on_error=True, clean_python=True, clean_conda=True)



:py:mod:`pip`
=============

.. py:module:: conda.env.installers.pip

.. autoapi-nested-parse::

   Pip-flavored installer.




Functions
---------

.. autoapisummary::

   conda.env.installers.pip._pip_install_via_requirements
   conda.env.installers.pip.install



.. py:function:: _pip_install_via_requirements(prefix, specs, args, *_, **kwargs)

   Installs the pip dependencies in specs using a temporary pip requirements file.

   :param prefix: The path to the python and pip executables.
   :type prefix: string
   :param specs: Each element should be a valid pip dependency.
                 See: https://pip.pypa.io/en/stable/user_guide/#requirements-files
                      https://pip.pypa.io/en/stable/reference/pip_install/#requirements-file-format
   :type specs: iterable of strings


.. py:function:: install(*args, **kwargs)



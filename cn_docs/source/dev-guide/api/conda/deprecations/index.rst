:py:mod:`deprecations`
======================

.. py:module:: conda.deprecations

.. autoapi-nested-parse::

   Tools to aid in deprecating code.



Classes
-------

.. autoapisummary::

   conda.deprecations.DeprecationHandler




Attributes
----------

.. autoapisummary::

   conda.deprecations.T
   conda.deprecations.deprecated


.. py:data:: T

   

.. py:exception:: DeprecatedError


   Bases: :py:obj:`RuntimeError`

   Unspecified run-time error.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:class:: DeprecationHandler(version: str)


   
   Factory to create a deprecation handle for the specified version.

   :param version: The version to compare against when checking deprecation statuses.

   .. py:attribute:: _version
      :type: str | None

      

   .. py:attribute:: _version_tuple
      :type: tuple[int, Ellipsis] | None

      

   .. py:attribute:: _version_object
      :type: packaging.version.Version | None

      

   .. py:method:: _get_version_tuple(version: str) -> tuple[int, Ellipsis] | None
      :staticmethod:

      Return version as non-empty tuple of ints if possible, else None.

      :param version: Version string to parse.


   .. py:method:: _version_less_than(version: str) -> bool

      Test whether own version is less than the given version.

      :param version: Version string to compare against.


   .. py:method:: __call__(deprecate_in: str, remove_in: str, *, addendum: str | None = None, stack: int = 0, deprecation_type: type[Warning] = DeprecationWarning) -> Callable[[Callable[P, T]], Callable[P, T]]

      Deprecation decorator for functions, methods, & classes.

      :param deprecate_in: Version in which code will be marked as deprecated.
      :param remove_in: Version in which code is expected to be removed.
      :param addendum: Optional additional messaging. Useful to indicate what to do instead.
      :param stack: Optional stacklevel increment.


   .. py:method:: argument(deprecate_in: str, remove_in: str, argument: str, *, rename: str | None = None, addendum: str | None = None, stack: int = 0, deprecation_type: type[Warning] = DeprecationWarning) -> Callable[[Callable[P, T]], Callable[P, T]]

      Deprecation decorator for keyword arguments.

      :param deprecate_in: Version in which code will be marked as deprecated.
      :param remove_in: Version in which code is expected to be removed.
      :param argument: The argument to deprecate.
      :param rename: Optional new argument name.
      :param addendum: Optional additional messaging. Useful to indicate what to do instead.
      :param stack: Optional stacklevel increment.


   .. py:method:: action(deprecate_in: str, remove_in: str, action: ActionType, *, addendum: str | None = None, stack: int = 0, deprecation_type: type[Warning] = FutureWarning) -> ActionType

      Wraps any argparse.Action to issue a deprecation warning.


   .. py:method:: module(deprecate_in: str, remove_in: str, *, addendum: str | None = None, stack: int = 0) -> None

      Deprecation function for modules.

      :param deprecate_in: Version in which code will be marked as deprecated.
      :param remove_in: Version in which code is expected to be removed.
      :param addendum: Optional additional messaging. Useful to indicate what to do instead.
      :param stack: Optional stacklevel increment.


   .. py:method:: constant(deprecate_in: str, remove_in: str, constant: str, value: Any, *, addendum: str | None = None, stack: int = 0, deprecation_type: type[Warning] = DeprecationWarning) -> None

      Deprecation function for module constant/global.

      :param deprecate_in: Version in which code will be marked as deprecated.
      :param remove_in: Version in which code is expected to be removed.
      :param constant:
      :param value:
      :param addendum: Optional additional messaging. Useful to indicate what to do instead.
      :param stack: Optional stacklevel increment.


   .. py:method:: topic(deprecate_in: str, remove_in: str, *, topic: str, addendum: str | None = None, stack: int = 0, deprecation_type: type[Warning] = DeprecationWarning) -> None

      Deprecation function for a topic.

      :param deprecate_in: Version in which code will be marked as deprecated.
      :param remove_in: Version in which code is expected to be removed.
      :param topic: The topic being deprecated.
      :param addendum: Optional additional messaging. Useful to indicate what to do instead.
      :param stack: Optional stacklevel increment.


   .. py:method:: _get_module(stack: int) -> tuple[types.ModuleType, str]

      Detect the module from which we are being called.

      :param stack: The stacklevel increment.
      :return: The module and module name.


   .. py:method:: _generate_message(deprecate_in: str, remove_in: str, prefix: str, addendum: str | None, *, deprecation_type: type[Warning]) -> tuple[type[Warning] | None, str]

      Generate the standardized deprecation message and determine whether the
      deprecation is pending, active, or past.

      :param deprecate_in: Version in which code will be marked as deprecated.
      :param remove_in: Version in which code is expected to be removed.
      :param prefix: The message prefix, usually the function name.
      :param addendum: Additional messaging. Useful to indicate what to do instead.
      :param deprecation_type: The warning type to use for active deprecations.
      :return: The warning category (if applicable) and the message.



.. py:data:: deprecated

   


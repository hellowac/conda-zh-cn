:py:mod:`exceptions`
====================

.. py:module:: conda.exceptions

.. autoapi-nested-parse::

   Conda exceptions.




Functions
---------

.. autoapisummary::

   conda.exceptions.maybe_raise
   conda.exceptions.print_conda_exception
   conda.exceptions._format_exc



.. py:exception:: ResolvePackageNotFound(bad_deps)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: LockError(message)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: ArgumentError(message, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:attribute:: return_code
      :value: 2

      


.. py:exception:: Help(message, caused_by=None, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: ActivateHelp


   Bases: :py:obj:`Help`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: DeactivateHelp


   Bases: :py:obj:`Help`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: GenericHelp(command)


   Bases: :py:obj:`Help`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaSignalInterrupt(signum)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: TooManyArgumentsError(expected, received, offending_arguments, optional_message='', *args)


   Bases: :py:obj:`ArgumentError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: ClobberError(message, path_conflict, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:method:: __repr__()

      Return repr(self).



.. py:exception:: BasicClobberError(source_path, target_path, context)


   Bases: :py:obj:`ClobberError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: KnownPackageClobberError(target_path, colliding_dist_being_linked, colliding_linked_dist, context)


   Bases: :py:obj:`ClobberError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: UnknownPackageClobberError(target_path, colliding_dist_being_linked, context)


   Bases: :py:obj:`ClobberError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: SharedLinkPathClobberError(target_path, incompatible_package_dists, context)


   Bases: :py:obj:`ClobberError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CommandNotFoundError(command)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: PathNotFoundError(path)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`OSError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: DirectoryNotFoundError(path)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: EnvironmentLocationNotFound(location)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: EnvironmentNameNotFound(environment_name)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: NoBaseEnvironmentError


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: DirectoryNotACondaEnvironmentError(target_directory)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaEnvironmentError(message, *args)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`OSError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: DryRunExit


   Bases: :py:obj:`conda.CondaExitZero`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaSystemExit(*args)


   Bases: :py:obj:`conda.CondaExitZero`, :py:obj:`SystemExit`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: PaddingError(dist, placeholder, placeholder_length)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: LinkError(message)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaOSError(message, **kwargs)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`OSError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: ProxyError


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaIOError(message, *args)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`OSError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaFileIOError(filepath, message, *args)


   Bases: :py:obj:`CondaIOError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaKeyError(key, message, *args)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`KeyError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: ChannelError(message, caused_by=None, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: ChannelNotAllowed(channel)


   Bases: :py:obj:`ChannelError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:attribute:: warning
      :value: 'Channel not included in allowlist'

      


.. py:exception:: ChannelDenied(channel)


   Bases: :py:obj:`ChannelNotAllowed`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:attribute:: warning
      :value: 'Channel included in denylist'

      


.. py:exception:: UnavailableInvalidChannel(channel, status_code, response: requests.models.Response | None = None)


   Bases: :py:obj:`ChannelError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:attribute:: status_code
      :type: str | int

      


.. py:exception:: OperationNotAllowed(message)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaImportError(message)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`ImportError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: ParseError(message)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CouldntParseError(reason)


   Bases: :py:obj:`ParseError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: ChecksumMismatchError(url, target_full_path, checksum_type, expected_checksum, actual_checksum, partial_download=False)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: PackageNotInstalledError(prefix, package_name)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaHTTPError(message, url, status_code, reason, elapsed_time, response=None, caused_by=None)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaSSLError(message, caused_by=None, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: AuthenticationError(message, caused_by=None, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: PackagesNotFoundError(packages, channel_urls=())


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: UnsatisfiableError(bad_deps, chains=True, strict=False)


   Bases: :py:obj:`conda.CondaError`

   An exception to report unsatisfiable dependencies.

   :param bad_deps: a list of tuples of objects (likely MatchSpecs).
   :param chains: (optional) if True, the tuples are interpreted as chains
                  of dependencies, from top level to bottom. If False, the tuples
                  are interpreted as simple lists of conflicting specs.

   :returns: Raises an exception with a formatted message detailing the
             unsatisfiable specifications.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:method:: _format_chain_str(bad_deps)



.. py:exception:: RemoveError(message)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: DisallowedPackageError(package_ref, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: SpecsConfigurationConflictError(requested_specs, pinned_specs, prefix)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaIndexError(message)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`IndexError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaValueError(message, *args, **kwargs)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`ValueError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CyclicalDependencyError(packages_with_cycles, **kwargs)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`ValueError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CorruptedEnvironmentError(environment_location, corrupted_file, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaHistoryError(message)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaUpgradeError(message)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaVerificationError(message)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: SafetyError(message)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaMemoryError(caused_by, **kwargs)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`MemoryError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: NotWritableError(path, errno, **kwargs)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`OSError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: NoWritableEnvsDirError(envs_dirs, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: NoWritablePkgsDirError(pkgs_dirs, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: EnvironmentNotWritableError(environment_location, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaDependencyError(message)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: BinaryPrefixReplacementError(path, placeholder, new_prefix, original_data_length, new_data_length)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: InvalidSpec(message: str, **kwargs)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`ValueError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: InvalidVersionSpec(invalid_spec: str, details: str)


   Bases: :py:obj:`InvalidSpec`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: InvalidMatchSpec(invalid_spec: str, details: str)


   Bases: :py:obj:`InvalidSpec`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: EncodingError(caused_by, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: NoSpaceLeftError(caused_by, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaEnvException(message, *args, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: EnvironmentFileNotFound(filename, *args, **kwargs)


   Bases: :py:obj:`CondaEnvException`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: EnvironmentFileExtensionNotValid(filename, *args, **kwargs)


   Bases: :py:obj:`CondaEnvException`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: EnvironmentFileEmpty(filename, *args, **kwargs)


   Bases: :py:obj:`CondaEnvException`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: EnvironmentFileNotDownloaded(username, packagename, *args, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: SpecNotFound(msg, *args, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: PluginError(message, caused_by=None, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:function:: maybe_raise(error, context)


.. py:function:: print_conda_exception(exc_val, exc_tb=None)


.. py:function:: _format_exc(exc_val=None, exc_tb=None)


.. py:exception:: InvalidInstaller(name)


   Bases: :py:obj:`Exception`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.



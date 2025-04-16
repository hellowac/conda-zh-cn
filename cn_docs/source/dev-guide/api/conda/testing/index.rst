:py:mod:`testing`
=================

.. py:module:: conda.testing


.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   cases/index.rst
   fixtures/index.rst
   gateways/index.rst
   helpers/index.rst
   integration/index.rst
   notices/index.rst
   solver_helpers/index.rst


Classes
-------

.. autoapisummary::

   conda.testing.CondaCLIFixture
   conda.testing.PathFactoryFixture
   conda.testing.TmpChannelFixture
   conda.testing.TmpEnvFixture



Functions
---------

.. autoapisummary::

   conda.testing.conda_cli
   conda.testing.context_aware_monkeypatch
   conda.testing.path_factory
   conda.testing.tmp_channel
   conda.testing.tmp_env
   conda.testing.tmp_envs_dir
   conda.testing.tmp_pkgs_dir
   conda.testing.conda_move_to_front_of_PATH



Attributes
----------

.. autoapisummary::

   conda.testing.deprecated


.. py:data:: deprecated

   

.. py:class:: CondaCLIFixture


   .. py:attribute:: capsys
      :type: pytest.CaptureFixture | None

      

   .. py:method:: __call__(*argv: str | os.PathLike[str] | pathlib.Path, raises: type[Exception] | tuple[type[Exception], Ellipsis]) -> tuple[str, str, pytest.ExceptionInfo]
                  __call__(*argv: str | os.PathLike[str] | pathlib.Path) -> tuple[str, str, int]

      Test conda CLI. Mimic what is done in `conda.cli.main.main`.

      `conda ...` == `conda_cli(...)`

      :param argv: Arguments to parse.
      :param raises: Expected exception to intercept. If provided, the raised exception
          will be returned instead of exit code (see pytest.raises and pytest.ExceptionInfo).
      :return: Command results (stdout, stderr, exit code or pytest.ExceptionInfo).


   .. py:method:: _cast_args(argv: tuple[str | os.PathLike[str] | pathlib.Path, Ellipsis]) -> collections.abc.Iterable[str]
      :staticmethod:

      Cast args to string and inspect for `conda run`.

      `conda run` is a unique case that requires `--dev` to use the src shell scripts
      and not the shell scripts provided by the installer.



.. py:class:: PathFactoryFixture


   .. py:attribute:: tmp_path
      :type: pathlib.Path

      

   .. py:method:: __call__(name: str | None = None, prefix: str | None = None, suffix: str | None = None) -> pathlib.Path

      Unique, non-existent path factory.

      Extends pytest's `tmp_path` fixture with a new unique, non-existent path for usage in cases
      where we need a temporary path that doesn't exist yet.

      :param name: Path name to append to `tmp_path`
      :param prefix: Prefix to prepend to unique name generated
      :param suffix: Suffix to append to unique name generated
      :return: A new unique path



.. py:class:: TmpChannelFixture


   .. py:attribute:: path_factory
      :type: PathFactoryFixture

      

   .. py:attribute:: conda_cli
      :type: CondaCLIFixture

      

   .. py:method:: __call__(*packages: str) -> collections.abc.Iterator[tuple[pathlib.Path, str]]



.. py:class:: TmpEnvFixture


   .. py:attribute:: path_factory
      :type: PathFactoryFixture | pytest.TempPathFactory

      

   .. py:attribute:: conda_cli
      :type: CondaCLIFixture

      

   .. py:method:: get_path() -> pathlib.Path


   .. py:method:: __call__(*packages: str, prefix: str | os.PathLike | None = None) -> collections.abc.Iterator[pathlib.Path]

      Generate a conda environment with the provided packages.

      :param packages: The packages to install into environment
      :param prefix: The prefix at which to install the conda environment
      :return: The conda environment's prefix



.. py:function:: conda_cli(capsys: pytest.CaptureFixture) -> collections.abc.Iterator[CondaCLIFixture]

   A function scoped fixture returning CondaCLIFixture instance.

   Use this for any commands that are local to the current test (e.g., creating a
   conda environment only used in the test).


.. py:function:: context_aware_monkeypatch(monkeypatch: pytest.MonkeyPatch) -> pytest.MonkeyPatch

   A monkeypatch fixture that resets context after each test.


.. py:function:: path_factory(tmp_path: pathlib.Path) -> collections.abc.Iterator[PathFactoryFixture]

   A function scoped fixture returning PathFactoryFixture instance.

   Use this to generate any number of temporary paths for the test that are unique and
   do not exist yet.


.. py:function:: tmp_channel(path_factory: PathFactoryFixture, conda_cli: CondaCLIFixture) -> collections.abc.Iterator[TmpChannelFixture]

   A function scoped fixture returning TmpChannelFixture instance.


.. py:function:: tmp_env(path_factory: PathFactoryFixture, conda_cli: CondaCLIFixture) -> collections.abc.Iterator[TmpEnvFixture]

   A function scoped fixture returning TmpEnvFixture instance.

   Use this when creating a conda environment that is local to the current test.


.. py:function:: tmp_envs_dir(path_factory: PathFactoryFixture, mocker: pytest_mock.MockerFixture) -> collections.abc.Iterator[pathlib.Path]

   A function scoped fixture returning a temporary environment directory.


.. py:function:: tmp_pkgs_dir(path_factory: PathFactoryFixture, mocker: pytest_mock.MockerFixture) -> collections.abc.Iterator[pathlib.Path]

   A function scoped fixture returning a temporary package cache directory.


.. py:function:: conda_move_to_front_of_PATH()



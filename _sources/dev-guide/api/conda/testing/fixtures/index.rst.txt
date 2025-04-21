:py:mod:`fixtures`
==================

.. py:module:: conda.testing.fixtures

.. autoapi-nested-parse::

   Collection of pytest fixtures used in conda tests.



Classes
-------

.. autoapisummary::

   conda.testing.fixtures.CondaCLIFixture
   conda.testing.fixtures.PathFactoryFixture
   conda.testing.fixtures.TmpEnvFixture
   conda.testing.fixtures.TmpChannelFixture



Functions
---------

.. autoapisummary::

   conda.testing.fixtures.suppress_resource_warning
   conda.testing.fixtures.tmpdir
   conda.testing.fixtures.clear_subdir_cache
   conda.testing.fixtures.disable_channel_notices
   conda.testing.fixtures.reset_conda_context
   conda.testing.fixtures.temp_package_cache
   conda.testing.fixtures.parametrized_solver_fixture
   conda.testing.fixtures.solver_classic
   conda.testing.fixtures.solver_libmamba
   conda.testing.fixtures._solver_helper
   conda.testing.fixtures.session_capsys
   conda.testing.fixtures.conda_cli
   conda.testing.fixtures.session_conda_cli
   conda.testing.fixtures.path_factory
   conda.testing.fixtures.tmp_env
   conda.testing.fixtures.session_tmp_env
   conda.testing.fixtures.tmp_channel
   conda.testing.fixtures.context_aware_monkeypatch
   conda.testing.fixtures.tmp_pkgs_dir
   conda.testing.fixtures.tmp_envs_dir
   conda.testing.fixtures.PYTHONPATH



Attributes
----------

.. autoapisummary::

   conda.testing.fixtures.Solver


.. py:function:: suppress_resource_warning()

   Suppress `Unclosed Socket Warning`

   It seems urllib3 keeps a socket open to avoid costly recreation costs.

   xref: https://github.com/kennethreitz/requests/issues/1882


.. py:function:: tmpdir(tmpdir, request)


.. py:function:: clear_subdir_cache()


.. py:function:: disable_channel_notices()

   Fixture that will set "context.number_channel_notices" to 0 and then set
   it back to its original value.

   This is also a good example of how to override values in the context object.


.. py:function:: reset_conda_context()

   Resets the context object after each test function is run.


.. py:function:: temp_package_cache(tmp_path_factory)

   Used to isolate package or index cache from other tests.


.. py:function:: parametrized_solver_fixture(request: pytest.FixtureRequest, monkeypatch: pytest.MonkeyPatch) -> collections.abc.Iterable[Literal[libmamba, classic]]

   A parameterized fixture that sets the solver backend to (1) libmamba
   and (2) classic for each test. It's using autouse=True, so only import it in
   modules that actually need it.

   Note that skips and xfails need to be done _inside_ the test body.
   Decorators can't be used because they are evaluated before the
   fixture has done its work!

   So, instead of:

       @pytest.mark.skipif(context.solver == "libmamba", reason="...")
       def test_foo():
           ...

   Do:

       def test_foo():
           if context.solver == "libmamba":
               pytest.skip("...")
           ...


.. py:function:: solver_classic(request: pytest.FixtureRequest, monkeypatch: pytest.MonkeyPatch) -> collections.abc.Iterable[Literal[classic]]


.. py:function:: solver_libmamba(request: pytest.FixtureRequest, monkeypatch: pytest.MonkeyPatch) -> collections.abc.Iterable[Literal[libmamba]]


.. py:data:: Solver

   

.. py:function:: _solver_helper(request: pytest.FixtureRequest, monkeypatch: pytest.MonkeyPatch, solver: Solver) -> collections.abc.Iterable[Solver]


.. py:function:: session_capsys(request) -> collections.abc.Iterator[_pytest.capture.MultiCapture]


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



.. py:function:: conda_cli(capsys: pytest.CaptureFixture) -> collections.abc.Iterator[CondaCLIFixture]

   A function scoped fixture returning CondaCLIFixture instance.

   Use this for any commands that are local to the current test (e.g., creating a
   conda environment only used in the test).


.. py:function:: session_conda_cli() -> collections.abc.Iterator[CondaCLIFixture]

   A session scoped fixture returning CondaCLIFixture instance.

   Use this for any commands that are global to the test session (e.g., creating a
   conda environment shared across tests, `conda info`, etc.).


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



.. py:function:: path_factory(tmp_path: pathlib.Path) -> collections.abc.Iterator[PathFactoryFixture]

   A function scoped fixture returning PathFactoryFixture instance.

   Use this to generate any number of temporary paths for the test that are unique and
   do not exist yet.


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



.. py:function:: tmp_env(path_factory: PathFactoryFixture, conda_cli: CondaCLIFixture) -> collections.abc.Iterator[TmpEnvFixture]

   A function scoped fixture returning TmpEnvFixture instance.

   Use this when creating a conda environment that is local to the current test.


.. py:function:: session_tmp_env(tmp_path_factory: pytest.TempPathFactory, session_conda_cli: CondaCLIFixture) -> collections.abc.Iterator[TmpEnvFixture]

   A session scoped fixture returning TmpEnvFixture instance.

   Use this when creating a conda environment that is shared across tests.


.. py:class:: TmpChannelFixture


   .. py:attribute:: path_factory
      :type: PathFactoryFixture

      

   .. py:attribute:: conda_cli
      :type: CondaCLIFixture

      

   .. py:method:: __call__(*packages: str) -> collections.abc.Iterator[tuple[pathlib.Path, str]]



.. py:function:: tmp_channel(path_factory: PathFactoryFixture, conda_cli: CondaCLIFixture) -> collections.abc.Iterator[TmpChannelFixture]

   A function scoped fixture returning TmpChannelFixture instance.


.. py:function:: context_aware_monkeypatch(monkeypatch: pytest.MonkeyPatch) -> pytest.MonkeyPatch

   A monkeypatch fixture that resets context after each test.


.. py:function:: tmp_pkgs_dir(path_factory: PathFactoryFixture, mocker: pytest_mock.MockerFixture) -> collections.abc.Iterator[pathlib.Path]

   A function scoped fixture returning a temporary package cache directory.


.. py:function:: tmp_envs_dir(path_factory: PathFactoryFixture, mocker: pytest_mock.MockerFixture) -> collections.abc.Iterator[pathlib.Path]

   A function scoped fixture returning a temporary environment directory.


.. py:function:: PYTHONPATH()

   We need to set this so Python loads the dev version of 'conda', usually taken
   from `conda/` in the root of the cloned repo. This root is usually the working
   directory when we run `pytest`.
   Otherwise, it will import the one installed in the base environment, which might
   have not been overwritten with `pip install -e . --no-deps`. This doesn't happen
   in other tests because they run with the equivalent of `python -m conda`. However,
   some tests directly run `conda (shell function) which calls `conda` (Python entry
   point). When a script is called this way, it bypasses the automatic "working directory
   is first on sys.path" behavior you find in `python -m` style calls. See
   https://docs.python.org/3/library/sys_path_init.html for details.



:py:mod:`decorators`
====================

.. py:module:: conda.auxlib.decorators


Classes
-------

.. autoapisummary::

   conda.auxlib.decorators.classproperty



Functions
---------

.. autoapisummary::

   conda.auxlib.decorators.memoizemethod
   conda.auxlib.decorators.clear_memoized_methods
   conda.auxlib.decorators.memoizedproperty



.. py:function:: memoizemethod(method)

   Decorator to cause a method to cache it's results in self for each
   combination of inputs and return the cached result on subsequent calls.
   Does not support named arguments or arg values that are not hashable.

   >>> class Foo (object):
   ...   @memoizemethod
   ...   def foo(self, x, y=0):
   ...     print('running method with', x, y)
   ...     return x + y + 3
   ...
   >>> foo1 = Foo()
   >>> foo2 = Foo()
   >>> foo1.foo(10)
   running method with 10 0
   13
   >>> foo1.foo(10)
   13
   >>> foo2.foo(11, y=7)
   running method with 11 7
   21
   >>> foo2.foo(11)
   running method with 11 0
   14
   >>> foo2.foo(11, y=7)
   21
   >>> class Foo (object):
   ...   def __init__(self, lower):
   ...     self.lower = lower
   ...   @memoizemethod
   ...   def range_tuple(self, upper):
   ...     print('running function')
   ...     return tuple(i for i in range(self.lower, upper))
   ...   @memoizemethod
   ...   def range_iter(self, upper):
   ...     print('running function')
   ...     return (i for i in range(self.lower, upper))
   ...
   >>> foo = Foo(3)
   >>> foo.range_tuple(6)
   running function
   (3, 4, 5)
   >>> foo.range_tuple(7)
   running function
   (3, 4, 5, 6)
   >>> foo.range_tuple(6)
   (3, 4, 5)
   >>> foo.range_iter(6)
   Traceback (most recent call last):
   TypeError: Can't memoize a generator or non-hashable object!


.. py:function:: clear_memoized_methods(obj, *method_names)

   Clear the memoized method or @memoizedproperty results for the given
   method names from the given object.

   >>> v = [0]
   >>> def inc():
   ...     v[0] += 1
   ...     return v[0]
   ...
   >>> class Foo(object):
   ...    @memoizemethod
   ...    def foo(self):
   ...        return inc()
   ...    @memoizedproperty
   ...    def g(self):
   ...       return inc()
   ...
   >>> f = Foo()
   >>> f.foo(), f.foo()
   (1, 1)
   >>> clear_memoized_methods(f, 'foo')
   >>> (f.foo(), f.foo(), f.g, f.g)
   (2, 2, 3, 3)
   >>> (f.foo(), f.foo(), f.g, f.g)
   (2, 2, 3, 3)
   >>> clear_memoized_methods(f, 'g', 'no_problem_if_undefined')
   >>> f.g, f.foo(), f.g
   (4, 2, 4)
   >>> f.foo()
   2


.. py:function:: memoizedproperty(func)

   Decorator to cause a method to cache it's results in self for each
   combination of inputs and return the cached result on subsequent calls.
   Does not support named arguments or arg values that are not hashable.

   >>> class Foo (object):
   ...   _x = 1
   ...   @memoizedproperty
   ...   def foo(self):
   ...     self._x += 1
   ...     print('updating and returning {0}'.format(self._x))
   ...     return self._x
   ...
   >>> foo1 = Foo()
   >>> foo2 = Foo()
   >>> foo1.foo
   updating and returning 2
   2
   >>> foo1.foo
   2
   >>> foo2.foo
   updating and returning 2
   2
   >>> foo1.foo
   2


.. py:class:: classproperty(getter=None, setter=None)


   .. py:method:: __get__(obj, type_=None)


   .. py:method:: __set__(obj, value)


   .. py:method:: setter(setter)




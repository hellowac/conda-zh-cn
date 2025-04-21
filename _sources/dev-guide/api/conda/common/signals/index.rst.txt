:py:mod:`signals`
=================

.. py:module:: conda.common.signals

.. autoapi-nested-parse::

   Intercept signals and handle them gracefully.




Functions
---------

.. autoapisummary::

   conda.common.signals.get_signal_name
   conda.common.signals.signal_handler



Attributes
----------

.. autoapisummary::

   conda.common.signals.INTERRUPT_SIGNALS


.. py:data:: INTERRUPT_SIGNALS
   :value: ('SIGABRT', 'SIGINT', 'SIGTERM', 'SIGQUIT', 'SIGBREAK')

   

.. py:function:: get_signal_name(signum)

   .. rubric:: 示例

   >>> from signal import SIGINT
   >>> get_signal_name(SIGINT)
   'SIGINT'


.. py:function:: signal_handler(handler)



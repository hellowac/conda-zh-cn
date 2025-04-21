:py:mod:`constants`
===================

.. py:module:: conda.trust.constants

.. autoapi-nested-parse::

   Context trust constants.

   You could argue that the signatures being here is not necessary; indeed, we
   are not necessarily going to be able to check them *properly* (based on some
   prior expectations) as the user, since this is the beginning of trust
   bootstrapping, the first/backup version of the root of trust metadata.
   Still, the signatures here are useful for diagnostic purposes, and, more
   important, to allow self-consistency checks: that helps us avoid breaking the
   chain of trust if someone accidentally lists the wrong keys down the line. (:
   The discrepancy can be detected when loading the root data, and we can
   decline to cache incorrect trust metadata that would make further root
   updates impossible.



.. py:data:: INITIAL_TRUST_ROOT

   

.. py:data:: KEY_MGR_FILE
   :value: 'key_mgr.json'

   


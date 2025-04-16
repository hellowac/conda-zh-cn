:py:mod:`ftp`
=============

.. py:module:: conda.gateways.connection.adapters.ftp

.. autoapi-nested-parse::

   Defines FTP transport adapter for CondaSession (requests.Session).

   Taken from requests-ftp (https://github.com/Lukasa/requests-ftp/blob/master/requests_ftp/ftp.py).

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.



Classes
-------

.. autoapisummary::

   conda.gateways.connection.adapters.ftp.FTPAdapter



Functions
---------

.. autoapisummary::

   conda.gateways.connection.adapters.ftp._new_makepasv
   conda.gateways.connection.adapters.ftp.data_callback_factory
   conda.gateways.connection.adapters.ftp.build_text_response
   conda.gateways.connection.adapters.ftp.build_binary_response
   conda.gateways.connection.adapters.ftp.build_response
   conda.gateways.connection.adapters.ftp.get_status_code_from_code_response



Attributes
----------

.. autoapisummary::

   conda.gateways.connection.adapters.ftp._old_makepasv


.. py:data:: _old_makepasv

   

.. py:function:: _new_makepasv(self)


.. py:class:: FTPAdapter


   Bases: :py:obj:`conda.gateways.connection.BaseAdapter`

   A Requests Transport Adapter that handles FTP urls.

   .. py:method:: send(request, **kwargs)

      Sends a PreparedRequest object over FTP. Returns a response object.


   .. py:method:: close()

      Dispose of any internal state.


   .. py:method:: list(path, request)

      Executes the FTP LIST command on the given path.


   .. py:method:: retr(path, request)

      Executes the FTP RETR command on the given path.


   .. py:method:: nlst(path, request)

      Executes the FTP NLST command on the given path.


   .. py:method:: get_username_password_from_header(request)

      Given a PreparedRequest object, reverse the process of adding HTTP
      Basic auth to obtain the username and password. Allows the FTP adapter
      to piggyback on the basic auth notation without changing the control
      flow.


   .. py:method:: get_host_and_path_from_url(request)

      Given a PreparedRequest object, split the URL in such a manner as to
      determine the host and the path. This is a separate method to wrap some
      of urlparse's craziness.



.. py:function:: data_callback_factory(variable)

   Returns a callback suitable for use by the FTP library. This callback
   will repeatedly save data into the variable provided to this function. This
   variable should be a file-like structure.


.. py:function:: build_text_response(request, data, code)

   Build a response for textual data.


.. py:function:: build_binary_response(request, data, code)

   Build a response for data whose encoding is unknown.


.. py:function:: build_response(request, data, code, encoding)

   Builds a response object from the data returned by ftplib, using the
   specified encoding.


.. py:function:: get_status_code_from_code_response(code)

   Handle complicated code response, even multi-lines.

   We get the status code in two ways:
   - extracting the code from the last valid line in the response
   - getting it from the 3 first digits in the code
   After a comparison between the two values,
   we can safely set the code or raise a warning.
   .. rubric:: 示例

   - get_status_code_from_code_response('200 Welcome') == 200
   - multi_line_code = '226-File successfully transferred\n226 0.000 seconds'
     get_status_code_from_code_response(multi_line_code) == 226
   - multi_line_with_code_conflicts = '200-File successfully transferred\n226 0.000 seconds'
     get_status_code_from_code_response(multi_line_with_code_conflicts) == 226

   For more detail see RFC 959, page 36, on multi-line responses:
       https://www.ietf.org/rfc/rfc959.txt
       "Thus the format for multi-line replies is that the first line
        will begin with the exact required reply code, followed
        immediately by a Hyphen, "-" (also known as Minus), followed by
        text.  The last line will begin with the same code, followed
        immediately by Space <SP>, optionally some text, and the Telnet
        end-of-line code."



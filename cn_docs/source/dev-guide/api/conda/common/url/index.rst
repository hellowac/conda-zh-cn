:py:mod:`url`
=============

.. py:module:: conda.common.url

.. autoapi-nested-parse::

   Common URL utilities.



Classes
-------

.. autoapisummary::

   conda.common.url.Url



Functions
---------

.. autoapisummary::

   conda.common.url.hex_octal_to_int
   conda.common.url.percent_decode
   conda.common.url.path_to_url
   conda.common.url.urlparse
   conda.common.url.url_to_s3_info
   conda.common.url.is_url
   conda.common.url.is_ipv4_address
   conda.common.url.is_ipv6_address
   conda.common.url.is_ip_address
   conda.common.url.join
   conda.common.url.has_scheme
   conda.common.url.strip_scheme
   conda.common.url.mask_anaconda_token
   conda.common.url.split_anaconda_token
   conda.common.url.split_platform
   conda.common.url._split_platform_re
   conda.common.url.has_platform
   conda.common.url.split_scheme_auth_token
   conda.common.url.split_conda_url_easy_parts
   conda.common.url.get_proxy_username_and_pass
   conda.common.url.add_username_and_password
   conda.common.url.maybe_add_auth
   conda.common.url.maybe_unquote
   conda.common.url.remove_auth



Attributes
----------

.. autoapisummary::

   conda.common.url.file_scheme
   conda.common.url.url_attrs
   conda.common.url.join_url


.. py:function:: hex_octal_to_int(ho)


.. py:function:: percent_decode(path)


.. py:data:: file_scheme
   :value: 'file://'

   def url_to_path(url):
   assert url.startswith(file_scheme), "{} is not a file-scheme URL".format(url)
   decoded = percent_decode(url[len(file_scheme):])
   if decoded.startswith('/') and decoded[2] == ':':
       # A Windows path.
       decoded.replace('/', '\')
   return decoded

.. py:function:: path_to_url(path)


.. py:data:: url_attrs
   :value: ('scheme', 'path', 'query', 'fragment', 'username', 'password', 'hostname', 'port')

   

.. py:class:: Url


   Bases: :py:obj:`namedtuple`\ (\ :py:obj:`'Url'`\ , :py:obj:`url_attrs`\ )

   Object used to represent a Url. The string representation of this object is a url string.

   This object was inspired by the urllib3 implementation as it gives you a way to construct
   URLs from various parts. The motivation behind this object was making something that is
   interoperable with built the `urllib.parse.urlparse` function and has more features than
   the built-in `ParseResult` object.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:property:: auth


   .. py:property:: netloc


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: as_dict() -> dict

      Provide a public interface for namedtuple's _asdict


   .. py:method:: replace(**kwargs) -> Url

      Provide a public interface for namedtuple's _replace


   .. py:method:: from_parse_result(parse_result: urllib.parse.ParseResult) -> Url
      :classmethod:



.. py:function:: urlparse(url: str) -> Url


.. py:function:: url_to_s3_info(url)

   Convert an s3 url to a tuple of bucket and key.

   .. rubric:: Examples

   >>> url_to_s3_info("s3://bucket-name.bucket/here/is/the/key")
   ('bucket-name.bucket', '/here/is/the/key')


.. py:function:: is_url(url)

   .. rubric:: Examples

   >>> is_url(None)
   False
   >>> is_url("s3://some/bucket")
   True


.. py:function:: is_ipv4_address(string_ip)

   .. rubric:: Examples

   >>> [is_ipv4_address(ip) for ip in ('8.8.8.8', '192.168.10.10', '255.255.255.255')]
   [True, True, True]
   >>> [is_ipv4_address(ip) for ip in ('8.8.8', '192.168.10.10.20', '256.255.255.255', '::1')]
   [False, False, False, False]


.. py:function:: is_ipv6_address(string_ip)

   .. rubric:: Examples

   >> [is_ipv6_address(ip) for ip in ('::1', '2001:db8:85a3::370:7334', '1234:'*7+'1234')]
   [True, True, True]
   >> [is_ipv6_address(ip) for ip in ('192.168.10.10', '1234:'*8+'1234')]
   [False, False]


.. py:function:: is_ip_address(string_ip)

   .. rubric:: Examples

   >> is_ip_address('192.168.10.10')
   True
   >> is_ip_address('::1')
   True
   >> is_ip_address('www.google.com')
   False


.. py:function:: join(*args)


.. py:data:: join_url

   

.. py:function:: has_scheme(value)


.. py:function:: strip_scheme(url)

   .. rubric:: Examples

   >>> strip_scheme("https://www.conda.io")
   'www.conda.io'
   >>> strip_scheme("s3://some.bucket/plus/a/path.ext")
   'some.bucket/plus/a/path.ext'


.. py:function:: mask_anaconda_token(url)


.. py:function:: split_anaconda_token(url)

   .. rubric:: Examples

   >>> split_anaconda_token("https://1.2.3.4/t/tk-123-456/path")
   (u'https://1.2.3.4/path', u'tk-123-456')
   >>> split_anaconda_token("https://1.2.3.4/t//path")
   (u'https://1.2.3.4/path', u'')
   >>> split_anaconda_token("https://some.domain/api/t/tk-123-456/path")
   (u'https://some.domain/api/path', u'tk-123-456')
   >>> split_anaconda_token("https://1.2.3.4/conda/t/tk-123-456/path")
   (u'https://1.2.3.4/conda/path', u'tk-123-456')
   >>> split_anaconda_token("https://1.2.3.4/path")
   (u'https://1.2.3.4/path', None)
   >>> split_anaconda_token("https://10.2.3.4:8080/conda/t/tk-123-45")
   (u'https://10.2.3.4:8080/conda', u'tk-123-45')


.. py:function:: split_platform(known_subdirs, url)

   .. rubric:: Examples

   >>> from conda.base.constants import KNOWN_SUBDIRS
   >>> split_platform(KNOWN_SUBDIRS, "https://1.2.3.4/t/tk-123/linux-ppc64le/path")
   (u'https://1.2.3.4/t/tk-123/path', u'linux-ppc64le')


.. py:function:: _split_platform_re(known_subdirs)


.. py:function:: has_platform(url, known_subdirs)


.. py:function:: split_scheme_auth_token(url)

   .. rubric:: Examples

   >>> split_scheme_auth_token("https://u:p@conda.io/t/x1029384756/more/path")
   ('conda.io/more/path', 'https', 'u:p', 'x1029384756')
   >>> split_scheme_auth_token(None)
   (None, None, None, None)


.. py:function:: split_conda_url_easy_parts(known_subdirs, url)


.. py:function:: get_proxy_username_and_pass(scheme)


.. py:function:: add_username_and_password(url: str, username: str, password: str) -> str

   Inserts `username` and `password` into provided `url`

   >>> add_username_and_password('https://anaconda.org', 'TestUser', 'Password')
   'https://TestUser:Password@anaconda.org'


.. py:function:: maybe_add_auth(url: str, auth: str, force=False) -> str

   Add auth if the url doesn't currently have it.

   By default, does not replace auth if it already exists.  Setting ``force`` to ``True``
   overrides this behavior.

   .. rubric:: Examples

   >>> maybe_add_auth("https://www.conda.io", "user:passwd")
   'https://user:passwd@www.conda.io'
   >>> maybe_add_auth("https://www.conda.io", "")
   'https://www.conda.io'


.. py:function:: maybe_unquote(url)


.. py:function:: remove_auth(url: str) -> str

   Remove embedded authentication from URL.

   .. code-block:: pycon

      >>> remove_auth("https://user:password@anaconda.com")
      'https://anaconda.com'



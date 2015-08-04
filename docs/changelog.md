# Changelog

## 0.5.0
- Automatic pagination now requires explicity ``pages()`` call
- Support for ``len()``
- Atributes of wrapped ``data`` can now be accessed via executor

##0.4.1
- changed parameters for Adapter's ``get_request_kwargs``. Also, subclasses are expected to call ``super``.
- added mixins to allow adapters to easily choose witch data format they will be dealing with.
- ``ServerError`` and ``ClientError`` are now raised on 4xx and 5xx response status. This behaviour can be customized for each service by overwriting adapter's ``process_response`` method.
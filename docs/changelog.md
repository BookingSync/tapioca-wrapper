# Changelog

## 0.6.0
- Giving access to request_method in ``get_request_kwargs``
- Verifying response content before trying to convert it to json on ``JSONAdapterMixin``
- Support for ``in`` operator
- pep8 improvments

## 0.5.3
- Adding ``max_pages`` and ``max_items`` to ``pages`` method

## 0.5.1
- Verifying if there's data before json dumping it on ``JSONAdapterMixin``

## 0.5.0
- Automatic pagination now requires explicity ``pages()`` call
- Support for ``len()``
- Atributes of wrapped data can now be accessed via executor
- It's now possible to iterate over wrapped lists

##0.4.1
- changed parameters for Adapter's ``get_request_kwargs``. Also, subclasses are expected to call ``super``.
- added mixins to allow adapters to easily choose witch data format they will be dealing with.
- ``ServerError`` and ``ClientError`` are now raised on 4xx and 5xx response status. This behaviour can be customized for each service by overwriting adapter's ``process_response`` method.
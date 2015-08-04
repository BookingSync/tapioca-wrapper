# Wrapping an API with Tapioca

This is all the code you need to build the Facebook Graph API wrapper you just played with:

**This is a tapioca 0.3.x code, some interfaces changed on new verisions.**
``` python
# source here: https://github.com/vintasoftware/tapioca-facebook/blob/master/tapioca_facebook/tapioca_facebook.py

from tapioca import (
    TapiocaAdapter, generate_wrapper_from_adapter, JSONAdapterMixin)
from requests_oauthlib import OAuth2

from resource_mapping import RESOURCE_MAPPING


class FacebookClientAdapter(JSONAdapterMixin, TapiocaAdapter):
    api_root = 'https://graph.facebook.com/'
    resource_mapping = RESOURCE_MAPPING

    def get_request_kwargs(self, api_params, *args, **kwargs):
        params = super(FacebookClientAdapter, self).get_request_kwargs(
            api_params, *args, **kwargs)

        params['auth'] = OAuth2(
            api_params.get('client_id'), token={
            'access_token': api_params.get('access_token'),
            'token_type': 'Bearer'})

        return params

    def get_iterator_list(self, response_data):
        return response_data['data']

    def get_iterator_next_request_kwargs(self,
            iterator_request_kwargs, response_data, response):
        paging = response_data.get('paging')
        if not paging:
            return
        url = paging.get('next')

        if url:
            return {'url': url}


Facebook = generate_wrapper_from_adapter(FacebookClientAdapter)
```
Everything else is what we call ```resource_mapping``` and its merely documentation. You can take a look  [here](https://github.com/vintasoftware/tapioca-facebook/blob/master/tapioca_facebook/resource_mapping.py).

**don't forget to add your new flavour to the [list](flavours.md)**

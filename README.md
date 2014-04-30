Jade field mixins
=================

A collection of Jade mixins for defining form fields. The style and structure follow [Bootstrap](https://github.com/twbs/bootstrap) form definition. Initially crafted for recreating dashboards using [KeystoneJS](https://github.com/JedWatson/keystone)


#### field

The base input field that we extend to build everything.

Accepted arguments:
* type
* name
* value
* placeholder

```jade
+field({ type: 'email', name: 'email', value: '', placeholder: 'email@example.com' })
```
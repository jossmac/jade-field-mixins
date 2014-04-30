Jade field mixins
=================

A collection of Jade mixins for defining form fields. The style and structure follow [Bootstrap's](https://github.com/twbs/bootstrap) form definition. Initially crafted for recreating dashboards using [KeystoneJS](https://github.com/JedWatson/keystone)

##### Table of Contents  
- [Standalone fields](#standalone)
- [Labelled fields](#labelled)
- [Attributes](#attributes)


<a name="standalone"/>
## Standalone fields


#### field

The base input field that we extend to build everything.

Accepted arguments:
* type
* name
* value
* placeholder

```Jade
+field({ type: 'email', name: 'email', value: '', placeholder: 'email@example.com' })
```

Returns

```HTML
<input type="email" name="email" placeholder="email@example.com">
```


#### textarea

A simple text area.

Accepted arguments:
* name
* value
* placeholder

```Jade
+textarea({ name: 'message', value: 'Hi there', placeholder: 'Message' })
```

Returns

```HTML
<textarea name="message" placeholder="Message">Hi there</textarea>
```


#### button

Buttons replace `<input type="submit">` because they're more flexible

Accepted arguments:
* type (optional, defaults to "button")
* label
* [attributes](#attributes): class (optional, defaults to "btn-default")

```Jade
+button({ label: 'Save changes', type: 'submit'}).btn-primary
```

Returns

```HTML
<button type="submit" class="btn btn-primary">Save changes</button>
```




<a name="labelled"/>
## Labelled fields

This is where Jade mixins really start to shine.
Note: Labelled fields expect a parent '.form-horizontal' to display a label left of the field

#### labelled field

Accepted arguments:
* label
* field args (type, name, value, placeholder)

```Jade
+labelled-field({ label: 'Admin Name', name: 'name', type: 'text', value: 'Karla Rowling' })
```

Returns

```HTML
<div class="form-group">
  <label class="col-sm-3">Admin Name</label>
  <div class="col-sm-9">
    <input type="text" class="form-control" value="Karla Rowling" name="name">
  </div>
</div>
```




<a name="attributes"/>
## Attributes

Note that all mixins accept appended attributes so you can your add own classes and IDs, which can . For instance:

```Jade
+mixin({args})#special-field
+mixin({args}).big-field
```
They can also be chained:

```Jade
+mixin({args})#special-field.big-field.light-text
```
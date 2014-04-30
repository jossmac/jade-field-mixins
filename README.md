Jade Field Mixins
=================

A collection of [Jade mixins](http://jade-lang.com/reference/#mixins) for defining form fields. The style and structure follow [Bootstrap's](https://github.com/twbs/bootstrap) form implementation. Initially crafted for recreating dashboards using [KeystoneJS](https://github.com/JedWatson/keystone).

To get a better idea of how you might use them checkout the [real world example](http://www.jossmackison.me/codepen/field-mixins).

##### Table of Contents  
- [Attributes](#attributes)
- [Standalone fields](#standalone)
- [Labelled fields](#labelled)




<a name="attributes"/>
## Attributes

All mixins accept appended attributes so you can your add own classes and IDs. For instance:

```Jade
+mixin({args})#special-field
+mixin({args}).big-field
```
They can also be chained:

```Jade
+mixin({args})#special-field.big-field.light-text
```





<a name="standalone"/>
## Standalone fields


### Field

The base input field that we extend to build everything. Accepted arguments:
* type
* name
* value
* placeholder

```Jade
+field({ type: "email", name: "email", value: "", placeholder: "email@example.com" })
```

Which yields:

```HTML
<input type="email" class="form-control" name="email" placeholder="email@example.com">
```


### Textarea

A simple textarea. Accepted arguments:
* name
* value
* placeholder

```Jade
+textarea({ name: "message", value: "Hi there", placeholder: "Message" })
```

Which yields:

```HTML
<textarea name="message" class="form-control" placeholder="Message">Hi there</textarea>
```


### Checkbox

A simple checkbox. Accepted arguments:
* name
* value (optional: defaults to "true")
* checked (Boolean)
* disabled (Boolean)

```Jade
+checkbox({ label: "Accepted Terms and Conditions", name: "acceptedTermsAndConditions" })
```

Which yields:

```HTML
<div class="checkbox">
  <label>
    <input type="checkbox" value="true" id="acceptedTermsAndConditions" name="acceptedTermsAndConditions">
    Accepted Terms and Conditions
  </label>
</div>
```


### Address field

###### Note: the location field also stores "name", "number", "country", and "geo" whilst this mixin ignores them.

A tidy layout for the [KeystoneJS location field](http://keystonejs.com/docs/database/#fieldtypes-location). Accepted arguments:
* name
* value (Object)

```Jade
+address-field({ name: "location", value: { street1: "Shop 36, 468 Oxford St", suburb: "Bondi", state: "NSW", postcode: "2098" } }).input-lg
```

Which yields:

```HTML
<div class="form-control-wrapper">
  <input name="location.street1" value="Shop 36, 468 Oxford St" placeholder="Street 1" class="form-control" type="text">
</div>
<div class="form-control-wrapper">
  <input name="location.street2" placeholder="Street 2" class="form-control" type="text">
</div>
<div class="form-control-wrapper">
  <input name="location.suburb" value="Bondi" placeholder="Suburb" class="form-control" type="text">
</div>
<div class="form-control-wrapper form-control-row">
  <div class="col-xs-6">
    <input name="location.state" value="NSW" placeholder="State" class="form-control" type="text">
  </div>
  <div class="col-xs-6">
    <input name="location.postcode" value="2098" placeholder="Postcode" class="form-control" type="text">
  </div>
</div>
```


### Upload

Browsers provide nice, native UI for file fields; let them handle it. Accepted arguments:
* type

```Jade
+upload({ name: "image" })
```

Which yields:

```HTML
<div class="field-upload">
  <input type="file" name="image">
</div>
```


### Button

Buttons replace `<input type="submit">` because they're more flexible. Accepted arguments:
* type (optional: defaults to "button")
* label
* [attributes](#attributes): class (optional, defaults to "btn-default")

```Jade
+button({ label: "Save changes", type: "submit'}).btn-primary
```

Which yields:

```HTML
<button type="submit" class="btn btn-primary">Save changes</button>
```




<a name="labelled"/>
## Labelled fields

Labelled fields include their dependent mixins so you don't have to. "labelled-field" includes "field" etc.

###### Note: Labelled fields expect a parent '.form-horizontal' to display a label left of the field

### Labelled field

Accepted arguments:
* label
* field args (type, name, value, placeholder)

```Jade
+labelled-field({ label: "Admin Name", name: "name", type: "text", value: "TJ Holowaychuk" })
```

Which yields:

```HTML
<div class="form-group">
  <label class="col-sm-3">Admin Name</label>
  <div class="col-sm-9">
    <input type="text" class="form-control" value="TJ Holowaychuk" name="name">
  </div>
</div>
```


### Labelled Textarea

Accepted arguments:
* label
* name
* value
* placeholder

```Jade
+labelled-textarea({ label: "Summary", name: "summary", value: "Programmer, author & artist. Creator of the Luna programming language, Express, Koa, Stylus, Component, Mocha, Jade, rework, node-canvas and others. Pastafarian", placeholder: "Tell us about yourself" })
```

Which yields:

```HTML
<div class="form-group">
  <label class="col-sm-3">Summary</label>
  <div class="col-sm-9">
    <textarea class="form-control" placeholder="Tell us about yourself" name="summary">Programmer, author &amp; artist. Creator of the Luna programming language, Express, Koa, Stylus, Component, Mocha, Jade, rework, node-canvas and others. Pastafarian</textarea>
  </div>
</div>
```


### Labelled Checkbox

Accepted arguments:
* name
* value (optional: defaults to "true")
* checked (Boolean)
* disabled (Boolean)

```Jade
+checkbox({ label: "Accepted Terms and Conditions", name: "acceptedTermsAndConditions", checked: true, disabled: true })
```

Which yields:

```HTML
<div class="checkbox">
  <label>
    <input type="checkbox" disabled="" checked="" value="true" id="acceptedTermsAndConditions" name="acceptedTermsAndConditions">
    Accepted Terms and Conditions
  </label>
</div>
```


### Labelled Address field

###### Note: the location field also stores "name", "number", "country", and "geo".

A tidy layout for the [KeystoneJS location field](http://keystonejs.com/docs/database/#fieldtypes-location). Accepted arguments:
* name
* value (Object)

```Jade
+address-field({ label: "Address", name: "location", value: { street1: "Shop 36, 468 Oxford St", suburb: "Bondi", state: "NSW", postcode: "2098" } }).input-lg
```

Which yields:

```HTML
<div class="form-group">
  <label class="col-sm-3">Address</label>
  <div class="col-sm-9">
    <div class="form-control-wrapper">
      <input type="text" class="form-control" placeholder="Street 1" value="Shop 36, 468 Oxford St" name="address.street1">
    </div>
    <div class="form-control-wrapper">
      <input type="text" class="form-control" placeholder="Street 2" name="address.street2">
    </div>
    <div class="form-control-wrapper">
      <input type="text" class="form-control" placeholder="Suburb" value="Bondi" name="address.suburb">
    </div>
    <div class="form-control-wrapper form-control-row">
      <div class="col-xs-6">
        <input type="text" class="form-control" placeholder="State" value="NSW" name="address.state">
      </div>
      <div class="col-xs-6">
        <input type="text" class="form-control" placeholder="Postcode" value="2098" name="address.postcode">
      </div>
    </div>
  </div>
</div>
```


### Labelled Upload

Browsers provide nice, native UI for file fields; let them handle it. Accepted arguments:
* type

```Jade
+labelled-upload({ label: "Image", name: "image" })
```

Which yields:

```HTML
<div class="form-group">
  <label class="col-sm-3">Image</label>
  <div class="col-sm-9">
    <div class="field-upload">
      <input type="file" name="image">
    </div>
  </div>
</div>
```


### Labelled Button

Offset the button so it's inline with the other fields. Accepted arguments:
* type (optional: defaults to "button")
* label
* [attributes](#attributes): class (optional, defaults to "btn-default")

```Jade
+labelled-button({ label: "Click me" })
```

Which yields:

```HTML
<div class="form-group">
  <div class="col-sm-9 col-sm-offset-3">
    <button class="btn btn-default" type="button">Click me</button>
  </div>
</div>
```










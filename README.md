Field Mixins
============

A collection of [Jade mixins](http://jade-lang.com/reference/#mixins) for defining form fields. Whilst anyone is welcome to use these mixins they were initially crafted for recreating a front-end admin UI for [KeystoneJS](https://github.com/JedWatson/keystone) applications. The style and structure follows [Bootstrap's](https://github.com/twbs/bootstrap) form implementation, but could easily be repurposed.

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
* type (String) (String)
* name (String) (String)
* value (String) (String)
* placeholder (String) (String)

```Jade
+field({ type: 'email', name: 'email', value: 'email@example.com', placeholder: 'Email Address' })
```

Which yields:

```HTML
<input type="email" class="form-control" name="email" value="email@example.com" placeholder="Email Address">
```


### Textarea

A simple textarea. Accepted arguments:
* name (String)
* value (String)
* placeholder (String)

```Jade
+textarea({ name: 'message', value: 'Hi there', placeholder: 'Message' })
```

Which yields:

```HTML
<textarea name="message" class="form-control" placeholder="Message">Hi there</textarea>
```


### Checkbox

A simple checkbox. Accepted arguments:
* name (String)
* value (String) : defaults to "true"
* checked (Boolean)
* disabled (Boolean)

```Jade
+checkbox({ label: 'Accepted Terms and Conditions', name: 'acceptedTermsAndConditions' })
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

A tidy layout for the [KeystoneJS location field](http://keystonejs.com/docs/database/#fieldtypes-location). Accepted arguments:
* name (String)
* value (Object) { street1, street2, suburb, state, postcode }

###### Note: the location field also stores "name', "number', "country', and "geo" whilst this mixin ignores them.

```Jade
+address-field({ name: 'location', value: { street1: 'Shop 36, 468 Oxford St', suburb: 'Bondi', state: 'NSW', postcode: '2098' } }).input-lg
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
* name (String)

```Jade
+upload({ name: 'image' })
```

Which yields:

```HTML
<div class="field-upload">
  <input type="file" name="image">
</div>
```


### Icon Field

Display an icon left of the field to indicate context to the user eg; "ion-social-twitter" from the amazing [Ionicons icon set](http://ionicons.com)

This was built for icon fonts though should work fine with sprited images.

Accepted arguments:
* icon (String)
* field args (type, name, value, placeholder)

```Jade
+icon-field({ type: 'text', name: 'twitter', icon: 'ion-social-twitter' })
```

Which yields:

```HTML
<div class="icon-field">
  <span class="ion-social-twitter icon"></span>
  <input type="text" class="form-control" name="twitter">
</div>
```


### Character Field

Display a character left of the field to indicate context to the user eg; "$" for a money field

Accepted arguments:
* character (String)
* field args (type, name, value, placeholder)

```Jade
+icon-field({ type: 'text', name: 'twitter', icon: 'ion-social-twitter' })
```

Which yields:

```HTML
<div class="icon-field">
  <span class="ion-social-twitter icon"></span>
  <input type="text" class="form-control" name="twitter">
</div>
```


### Button

Buttons rather than `<input type="submit">` because they're more flexible. Accepted arguments:
* type (String) : defaults to "button"
* label (String)

###### Note: the button class defaults to "btn-default". See [attributes](#attributes)

```Jade
+button({ buttonlabel: 'Save changes', type: 'submit'}).btn-primary
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
* label (String)
* field args (type, name, value, placeholder)

```Jade
+labelled-field({ label: 'Admin Name', name: 'name', type: 'text', value: 'TJ Holowaychuk' })
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
* label (String)
* field args (name, value, placeholder)

```Jade
+labelled-textarea({ label: 'Summary', name: 'summary', value: 'Programmer, author & artist. Creator of the Luna programming language, Express, Koa, Stylus, Component, Mocha, Jade, rework, node-canvas and others. Pastafarian', placeholder: 'Tell us about yourself' })
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
* label (String)
* name (String)
* value (String) : defaults to "true"
* checked (Boolean)
* disabled (Boolean)

```Jade
+checkbox({ label: 'Accepted Terms and Conditions', name: 'acceptedTermsAndConditions', checked: true, disabled: true })
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

A tidy layout for the [KeystoneJS location field](http://keystonejs.com/docs/database/#fieldtypes-location). Accepted arguments:
* label (String)
* name (String)
* value (Object) { street1, street2, suburb, state, postcode }

###### Note: the location field also stores "name', "number', "country', and "geo".

```Jade
+address-field({ label: 'Address', name: 'location', value: { street1: 'Shop 36, 468 Oxford St', suburb: 'Bondi', state: 'NSW', postcode: '2098' } }).input-lg
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
* label (String)
* name (String)

```Jade
+labelled-upload({ label: 'Image', name: 'image' })
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

Offset the button so its inline with the rest of the fields. Leaving the label column empty. Accepted arguments:
* type (String) : defaults to "button"
* label (String)

###### Note: the button class defaults to "btn-default". See [attributes](#attributes)

```Jade
+labelled-button({ buttonlabel: 'Click me' })
```

Which yields:

```HTML
<div class="form-group">
  <div class="col-sm-9 col-sm-offset-3">
    <button class="btn btn-default" type="button">Click me</button>
  </div>
</div>
```










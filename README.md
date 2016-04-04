__Mongoose 4+__ plugin to perform population into schema's virtual property.

[![NPM](https://nodei.co/npm/mongoose-populate-extended.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/mongoose-populate-extended/)

### Description
Mongoose ODM population does not provide an ability to populate documents into custom defined virtual property. This plugin enchances population functionality to provide such.

Plugin defines a new schema's property definition option __`asVirtual`__ that contains a key reference to the virtual property that will be populated. After population is performed the original reference is left intact.

### Usage
Learn by example

```javascript
var mongoose = require("mongoose");

// define schema
var schema = new Schema({
	propId: {
		type: mongoose.Schema.Types.ObjectId,
		ref: "Reference",
		asVirtual: "prop"	// populate into `prop` virtual property
	}
})

// register plugin
var populateExtended = require("mongoose-populate-extended")(mongoose);
schema.plugin(populateExtended);

// define schema's model
var Model = mongoose.model("Model", schema);
```

### Perform population
On `Model` model:
```javascript
Model.populate(models, "propId", function (err, _models) {
	// _models are equal to models and are populated with propId reference
	_models.forEach(function (model) {
		// model.propId is left intact
		// model.prop contains populated document
	});
})
```
On an instance of `Model`:
```javascript
model.populate("propId", function (err, _model) {
	// _model is equal to model and is populated with propId reference
	// _model.propId is left intact
	// _model.prop contains populated document
})
```
On a `Query`:
```javascript
Model.find().populate("propId").exec(function (err, models) { ... });
Model.findOne().populate("propId").exec(function (err, model) { ... });
```

### Changelog

#### v0.0.1

* Initial release

### License

MIT
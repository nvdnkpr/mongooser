#Mongooser
===============

Mongoose REPL

## install

```
npm install mongooser -g
```

## usage

```
mongooser [options]

  Options:

    -h, --help           output usage information
    -V, --version        output the version number
    -c --config <path>   configuration path
```

Your configuration should be a module. The module should be formatted as follows:

```js
exports.connect = 'mongodb://localhost:port/dbname'
exports.Users = 'path/to/a/schema'
exports.Views = 'path/to/a/model'
exports.Checkins = [ schema, options ]
```

### connection string _(required)_

```
// key must be named "connect"
exports.connect = 'mongodb://localhost/name_of_db'
```

### Schemas/Models

There are three approaches to expose your models to the REPL:

```
exports.NameOfYourModel = 'path/to/your/schema'

// or

exports.NameOfYourModel = 'path/to/your/model'

// or

exports.NameOfYourModel = [ new Schema(..), schemaOptions ]
```

The array approach allows us to quickly set up configuration by including the `Schema` and its options directly in the configuration file.

See the [test configuration]() for another example.

## repl

When `mongooser` starts it exposes your `Models` globally:

![](http://dl.dropbox.com/u/11198966/mongooser-startup.png)

You can query in traditional `Mongoose` fashion:

```
mongooser> Book.where('title').equals('How to make paper airplanes').exec(print)
mongooser> ...
mongooser> null { title: 'A Tale of Two Cities', _id: 4fbb25a950badf0000000001 }
```

A few observations:

  - `print`: is a global function available which prints query results to the repl nicely.
  - `p`: is an alias of `print`
  - executing a query dumps the query object to the repl first (represented above with ...)
  - the `print` helper displays returned arguments in order

## globals

 - `connection`: your db connection object
 - `models`: array of each loaded Model name
 - `schemas`: your schemas included in configuration
 - `mongoose`: the `mongoose` module
 - Models: each model created from your configuration

## tests

Run the tests with `make test`.

[LICENSE](https://github.com/aheckmann/mongooser/blob/master/LICENSE)

js-runtime-builtins
===================

Maintaining lists of built-in symbols of various JS runtimes.

Rational
---------

Various project (e.g. `Jshint <https://github.com/jshint/jshint>`_, `Eslint
<https://github.com/nzakas/eslint>`_) need lists of global symbols built in into
any particular JS runtime, in order to detect if a global symbol found in code
is a known built-in. Those lists are usually burried inside the projects and are
therefore hard to reuse and hard to maintain by a larger community. This repo
tries to amend this.

Approach
--------

Symbols are organized in class hierarchies, to take advantage of hierarchy
lookup for common symbols. The root class is **ecma** to signify the core
language, and then classes like **node** and **browser** inheriting from it, the
latter being inherited by **safari** and so forth.

The downside is that you have to instantiate the class you want to lookup in
(with **new**), which is a tang more difficult than map lookups. The upside is
you get inheritance.

Use
---

As it is intended as a Node module, this is how you would use it:

::

   var builtins = require('js-builtins');
   var node_builtins = new builtins.node();

   if ('process' in node_builtins && 'Math' in node_builtins)
      console.log('node contains both generic and special symbols');


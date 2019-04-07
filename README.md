DictUtils.jl
============

Utility functions for manipulating Dicts in Julia.  This library contains a
hodgepodge of functions which are useful when working with Dicts.  Some of
these functions will be more generally useful as well.


General Functions
-----------------

  coalesce(args...) Returns the first non-null argument
                    (or null if no such argument exists).
  parsePrimitive(type, string) Parses the string into a primitive value of
                               the given type.


Serialization/Deserialization Functions
---------------------------------------

  showCompact(dict[, config]) Returns a string representation of the dict in
                              a 'compact' format.  By default this compact
                              format uses commas as separators between entries
                              and colons as separators between keys and values.
                              The keys and values are serialzied according to
                              the output of 'string'.  config can be passed
                              in to alter the separators.
  parseCompact(dict, keytype, valuetype[, config]) Undoes the serialization
                                                   done by showCompact.


Combining Dicts
---------------

  combine!(func, map1, map2) Alter the first map1 so that it contains the
                             result of combining map1 and map2 keywise.  For
                             each key, the corresponding values in map1 and
                             map2 will be passed into the supplied function.
                             If the key does not exist in the map then null
                             is massed into the function instead.  The result
                             of this function call will be the value
                             associated with the key in the output map.
  addDicts!(map1, map2, weight) A special case of combine!().  This combines
                                the two maps by adding values when keys
                                overlap and otherwise taking either existing
                                value.  The values in the second map are
                                scaled by weight.


Modifying Dicts
---------------

  mapValues(function, dict) Alter the dict by applying a function to each
                            value.  The keys remain unchanged.
  normalizeDict!(dict) A special case of mapValues! where the mapping ensures
                       that the sum of the values in each map sums to one.


Subsetting Dicts
----------------

  sortedHead!([function, ]dict, numToKeep) Modify dict by only keeping the
                                           entries which are among the first
                                           numToKeep when sorted by function.
                                           If the function is omitted, then
                                           they are storted by '<'.
  sortedTail!(dict, numToKeep) Same as sortedHead!() but in reverse order.

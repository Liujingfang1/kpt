## apis merge3



### Synopsis


Description:

  merge3 identifies changes between an original source + updated source and merges the result
  into a destination, overriding the destination fields where they have changed between
  original and updated.

  ### Merge Rules

  Fields are recursively merged using the following rules:

  - scalars
    - if present in either dest or updated and 'null', clear the value
    - if unchanged between original and updated, keep dest value
    - if changed between original and updated (added, deleted, changed), take the updated value

  - non-associative lists -- lists without a merge key
    - if present in either dest or updated and 'null', clear the value
    - if unchanged between original and updated, keep dest value
    - if changed between original and updated (added, deleted, changed), take the updated value

  - map keys and fields -- paired by the map-key / field-name
    - if present in either dest or updated and 'null', clear the value
    - if present only in the dest, it keeps its value
    - if not-present in the dest, add the delta between original-updated as a field
    - otherwise recursively merge the value between original, updated, dest

  - associative list elements -- paired by the associative key
    - if present only in the dest, it keeps its value
    - if not-present in the dest, add the delta between original-updated as a field
    - otherwise recursively merge the value between original, updated, dest

  ### Associative Keys

  Associative keys are used to identify "same" elements within 2 different lists, and merge them.
  The following fields are recognized as associative keys:

[`mountPath`, `devicePath`, `ip`, `type`, `topologyKey`, `name`, `containerPort`]

  Any lists where all of the elements contain associative keys will be merged as associative lists.


```
apis merge3 [flags]
```

### Options

```
  -h, --help   help for merge3
```

### SEE ALSO

* [apis](apis.md)	 - Contains api information for kpt

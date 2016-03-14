# YAML-HDL

## Specifications

### Top-Level Keys

#### meta

Data about the module is specified here.

Required:

1. `name`: names the module
2. `mid`: module id that is randomly generated, uniquely identifying this module

Optional:

1. `create_date`: creation date, format: [YYYY-MM-DD]
2. `author`: author

#### req

Non-primitive modules which are referenced from this module. Optional.

Required:

1. `mid`: module id that should be imported

Optional:

1. `name`: name that is used in `modules` later. If left blank, default name specified in the module's `meta` can be used.
2. `location`: where the module is found. [default=0]
2.1: `0`: in the same file - in this case the mid of the sub-module doesn't really matter as long as it can be found
2.2: `1`: in the same directory (not applicable for web-based used)
2.3: `2`: in the online repository - mid is used to find

#### in

All inputs must be specified here.

Required:

1. `name`: names an input 

Optional:

1. `width`: number of bits [default=1]

#### out

All outputs must be specified here.

Required:

1. `name`: names an output 

Optional:

1. `width`: number of bits [default=1]

#### debug

The debug top-level key is optional. The nodes specified here are used for debug purposes.

Required:

1. `name`: names a debug wire

Optional:

1. `width`: number of bits [default=1]

#### modules

These are the structural logic components connecting input to output. Technically optional since output could be directly connected to input.

1. `name`: module that is used
2. `in`: associative array of inputs
3. `out`: associative array of outputs

### Single Module Per File

One way to keep track of modules is to separate each module into their own file. Downside to this is that many of the files will hold meaningless modules. 

### Multiple Modules Per File

Simply nest the entire module as shown in the `two_bit_adder_single_file` example. Only the first module can be referenced by any supermodules. 

### Primitive modules

Primitives are special. They don't have to be imported. Primitives are also the only modules that currently support variable 1-indexed arguments. 

For example, the `and` module works like this:

```
- name: and
	in:
	  	- 1: a
	  	- 2: b
	  	- 3: c
	out:
	  	- 1: out
```

#### Existing Primitives

1. `and`
2. `or`
3. `not`
4. `xor`
5. `nand`
6. `nor`
7. `xnor`

## Examples

Examples can be found in the `examples` folder

## Future Development

This is version 0. Improvements are coming. A few planned ones are listed here. 

* Tri-states
* FF/latches
* Creation of variable argument indexed modules

## License

GNU General Public License v3.0
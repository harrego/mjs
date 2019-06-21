# mjs

Cleaner JavaScript that gives YOU more control

## Features

- No garbage collection allowing the user to integrate a tightly controlled version that WORKS for THEIR NEEDS
- Verbose and easy to read code that explains exactly what the code is doing

## Low / High Level 

For speed, MJS  has a variety of components that go from lower level than ASM (e.g. if statements) to higher level than ASM (e.g. functions). This graph puts MJS on a scale when compared to other languages:

![Low to high level languages graph](https://raw.githubusercontent.com/harrego/mjs/master/images/high-low-langs-graph.png)

## Syntax

### Function

A simple function that takes the arguments `greeting` and `name` to produce a string with the two joined together with a space looks like this. E.g. "hello" and "mjs" would produce `hello mjs`

```
__ADDTOSTACK(_SYS_MJS_POSITION_IN_MEMORY___sys_mem)._native_mjs_callback_(__ADDTOSTACK(
"greeting name"._native_mjs_extension_args_()._unsafe_throwable_native_mjs_converter_fa
ctory(**&TOP_STACK_NATIVE_MJS_ARGUMENT__FIRST_AND_SECOND)))._native_mjs_extension_args_
("greeting name")._native_mjs_extension_arg_types_("SYS_DEPENDANT_NON_NATIVE_MJS_STRING
_CHAR_MACRO_TYPE")._unsafe_throwable_native_mjs_converter_factory_(*&SYS_DEPENDANT_NON_
NATIVE_MJS_NULL___OF_POINTER)
``` 

#### Explained

MJS is verbose so while at a glance it looks complicated, upon furthur inspection it makes more sense that other languages.

1. `__ADDTOSTACK()` means it will simply add it to memory so it can be called in future. `_SYS_MJS_POSITION_IN_MEMORY___sys_mem` inside of it addresses where in memory to add it, in this case just the system memory. If you read the variable as a sentence it makes sense.
2. The `._native_mjs_callback_()` at the end of `__ADDTOSTACK()` is simply what is run when the function is called. Think of it as what is inside `{ .. }` in JavaScript.
  - The name `_native_mjs_callback_()` is much more readable than `{ }` which is why it was chosen.
3. Inside of the callback we see `__ADDTOSTACK()` again. In this case it means "print to the console" as a `SYS_DEPENDANT_NON_NATIVE_MJS_STRING_CHAR_MACRO_TYPE` type (a string, we'll come back to it later) is inside rather a location in memory.
  - `SYS_DEPENDANT_NON_NATIVE_MJS_STRING_CHAR_MACRO_TYPE` is a great example of the easy to read names in MJS. A "string" (from other languages) can mean many things, a `SYS_DEPENDANT_NON_NATIVE_MJS_STRING_CHAR_MACRO_TYPE` is clear what it is.
4. At the end of the `SYS_DEPENDANT_NON_NATIVE_MJS_STRING_CHAR_MACRO_TYPE`, `._native_mjs_extension_args_()` is chained on the end. This simply means that the content inside of the `SYS_DEPENDANT_NON_NATIVE_MJS_STRING_CHAR_MACRO_TYPE` refers to the arguments of the function (this are defined later in the code). If we look back at the content it says `"greeting name"`, these are both arguments (again, these are defined later).
5. Next we see `._unsafe_throwable_native_mjs_converter_factory(**&TOP_STACK_NATIVE_MJS_ARGUMENT__FIRST_AND_SECOND)))` chained at the end. Looking at a name explains what is happening here. It is an `unsafe`, error `throwing`, `native MJS`, `converter factory`. A converter factory simply takes one types and turns it to another. In this case we are taking a `SYS_DEPENDANT_NON_NATIVE_MJS_STRING_CHAR_MACRO_TYPE` and casting it to a `**&TOP_STACK_NATIVE_MJS_ARGUMENT__FIRST_AND_SECOND` (an argument). This will take our `SYS_DEPENDANT_NON_NATIVE_MJS_STRING_CHAR_MACRO_TYPE` and convert it to the `FIRST_AND_SECOND` arguments of the function, in this case `greeting` and `name`.
  - You may also notice the `**&` at the start of the `TOP_STACK_NATIVE_MJS_ARGUMENT__FIRST_AND_SECOND` type, this means that it is a double pointer that points to another location in memory. This type is always a double pointer pointing to another location in memory. Make sure you never forget it!
6. As you may notice the last chained functions contained `)))` at the end, this means we have finished within `_native_mjs_callback_`. Now we must add the arguments needed to call the function. This is a simple function chained at the end, `._native_mjs_extension_args_("greeting name")`. It is simply creating two arguments `greeting` and `name`. Arguments are separated by a space in a `SYS_DEPENDANT_NON_NATIVE_MJS_STRING_CHAR_MACRO_TYPE`.
7. Next we see `._native_mjs_extension_arg_types_("SYS_DEPENDANT_NON_NATIVE_MJS_STRING_CHAR_MACRO_TYPE")` chained at the end. This is simply defining the types the arguments must be, this is a "dummy function" which means it does nothing and is for documentation purposes only. MJS is a strict-type language but only for single pointer of pointer of location of `SYS_DEPENDANT_NON_NATIVE_MJS_NULL___OF_POINTER`. This means every variable/argument must be of that type and converted when needed.
8. The last statement does exactly what we discussed, it makes the callback a `*&SYS_DEPENDANT_NON_NATIVE_MJS_NULL___OF_POINTER`. It looks like this chained on the end: `._unsafe_throwable_native_mjs_converter_factory_(*&SYS_DEPENDANT_NON_NATIVE_MJS_NULL___OF_POINTER)`. You may recognise `_unsafe_throwable_native_mjs_converter_factory_` from earlier.
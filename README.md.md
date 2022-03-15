# Interesting Language Features

## Match case
- Matching of all types at least by ==
- Matching by type hierarchy
- Matching by tree structure somehow

## Tuples
- Multiple variable return
- `x, y = y, x` swap

## Strong typesystem

- Compile time info includes
	- Data layout (size, alignment, ...)
	- Typecategory (pointer, value, class, enum, function, ...)
	- Typename (class name, enum name, function name, ...)
	- Lifetime (scope)
	- Constraints (custom checkers)
	- ...
	- If it's class, it contains information about all the underlying types
	- ...
	- Compile time analysis info (branch analysis results, read-only access, ...)
	- Constness
	- What annotations a certain function has
	- What functions a certain annotation has
	- What parameter names a function has
- Compile time reflection of the type

## Others
- if/else/... that return values
- for each in collection
- error handling
- named parameters
- modules
- chained comparison operators `(0 <= i && i < length) == (0 <= i < length)`
- shortcircuit condition execution `false && never_called()`
- implicit conversions (namely to boolean)
- beware of the lacking type checking in dynamic languages (namely JS) => there would be nice to have ALL these nicely: `isArray()`, `isPlainObject()`, `isObject()`, `isEmptyArray()`, `isNull()`, `isUndefined()`, `isNaN()`, `isEmptyObject()` (Not via unintuitive hacks that rely on some arbitrary truth about a type)
- flow control does not create a new scope, functions and classes do tho (if that is the case it would be nice to allow creation of arbitrary scopes) or maybe have a keyboard that exports a variable out of the current scope
- `for` has special optional blocks (`before first`, `after first`, `after last`, `after break`)
- custom control flow functions
- python list comprehension `some_list = [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]`
- variable names binded via pointer(which means, can be unbound and reassigned somewhere else)
- when interop with C, allow for parametrized import/export of functions and structs to reduce boilerplate
- get index when using `foreach`
- shadow keyword (shadowing names can lead to unexpected results, but it can be a wanted feature eg. in constructors, so let's just make it error by default, valid by explicit keyword)
- importing modules can not only change names one by one but by a function as well (to change casing for example or add prefix for the whole group of imported names, this conversion have to be checked for collisions, unless shadow keyword is specified)
- `operator[]` can have multiple arguments
- range literal 4:5 (to be used anywhere suited but `opertator[]` comes to mind first)
- ranges can than be unified, intersected, etc
- range will act as a generator of indexes
- `operator[]` overloaded for index generator will accept ranges as well tanks to isa relation between index generator and index range
- some kind of implicit conversion between indexes and iterators would be nice (note that this would make a chain of implicit conversions from index range to iterator generator which would be useful, this is perhaps a architectural problem, or maybe not)
- weak and strong typedef
	- `weak typedef range<index_type, value_type::iterator> as my_range`
	- this would allow for creation of `my_range` variable that could be passed into function that accepts original type without conversion
	- `strong typedef`, on the other hand, would create a new type identical to the original, but without any implicit or expicit conversion defined a function that accepts the original would not accept the new type (the opposite is true as well unless a keyword perhaps)
	- use case
		- aliasing long types to shorter more readable and more context aware names
		- creating a typesystem of meassuring units all based on int with some simple oneline conversion functions like `typedef int as second`, `typedef int as minute`, `implicit min_to_sec(x: minute) -> second {return x * 60}`
		- if parameters of functions are individually well described as `int`s but the function needs more of these parameters, user of such function may be confused and prone to error, but if the user have to state the type of each separately it is much more readable (this usecase may be replaced by named parameters tho)
			- `foo(velocity(15), dir_x(6), dir_y(7), dir_z(-1))`
			- functions could specify if a set of typedefs of the same base type can be used interchangebly ??? BIG QUESTIONMARK
- custom literals (like seconds, minutes, ...)
	- maybe just allowing prefix / suffix of some already known literals like numbers, strings,... But that wouldn't make nice literals of dates for example (maybe only if it was a string but that isn't that nice is it, it would be okish if the literal construction would take place at compile time and asserts would be available at lint time)
- Runtime/Sugartime&Compiletime/Linttime
- Static/... analysis defined in the language to run at Linttime
- unpacking arguments `a = [1, 2, 3]; foo(*a) == foo(1, 2, 3);`
- function binding `foo(int a, int b) {...} let bar = foo(5, _);`
- ability to write an app that is able to execute things based on compiletime reflection, like writing a test runner that is able to inject data/objects/fixtures into test functions' parameters based on the parameters' names (keep in mind that a test case might want to fetch multiple pieces of the same data returned by the same fixture)
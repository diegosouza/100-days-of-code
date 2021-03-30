# 100 Days Of Code - Log

### Day 1: 2021-03-13

- I played with `mix` and `iex` to remember basic stuff
- I inspected [IEx.Helpers](https://hexdocs.pm/iex/IEx.Helpers.html) and I found/remembered interesting stuff such as:
  - `h/1` to see module/function documentation
  - `ls/0` and `ls/1` to list current directory or another one
  - `i/1` to inspect data types, related modules and implemented protocols
  - `c/1` to compile a standalone source file
  - `exports/1` to see all functions and macros exported by a module
- `IEx.pry()` brings me to the context where I insert `require IEx; IEx.pry()`
- `mix test --cover` is builtin and a nice code coverage tool, but [excoveralls](https://hexdocs.pm/excoveralls) seems even better and it has an awesome [html report](https://hexdocs.pm/excoveralls/readme.html#mix-coveralls-html-show-coverage-as-html-report)

Interesting projects I may use to study or to try a small contribution:

- https://github.com/warmwaffles/exqlite
- https://github.com/whitepaperclip/live_phone
- https://github.com/patrykwozinski/youtex
- https://github.com/gmartsenkov/dry_validation
- https://github.com/zwelden/taskerville
- https://github.com/devstopfix/plug-ratelimit
- https://github.com/Simrayz/foresight

### Day 2: 2021-03-14

- [Issue opened](https://github.com/parroty/excoveralls/issues/253) for excoveralls
- [Played with typespecs in a project](https://github.com/diegosouza/joi/commit/33a49d55d1eb15e9fb07da7543fd9fce6ca59409). Unfortunately, I could not express a typespec for the current structure (list containing atom + several tuples) without a deep refactoring. Sample: `[:string, min_length: 6]`
- I called `mix dialyzer` maybe for the first time :thinking:

### Day 3: 2021-03-15

Today I learned or remembered:

- How to measure execution time with Erlang: `:timer.tc/1`
- Prepending is faster than appending for lists:
  - `to_prepend ++ list` or `[to_prepend | list]` :heavy_check_mark: **(faster)**
  - `list ++ to_append` :x: **(slower)**
- Lambdas can have multiple clauses and guards:

```elixir
division = fn
  x, y when y == 0 -> raise "division by zero"
  x, y -> x / y
end
```

- `Kernel.binding/1` returns bounded variables in a context (very useful inside `iex`)
- Structs are Maps with `__struct__: StructName` inside
- Polymorphism:
  - Structs for varying data
  - Protocols for varying behaviour
- Started the [Refactor a Markdown parser exercise on exercism](https://exercism.io/tracks/elixir/exercises/markdown)

Interesting projects I found:
- [typed_struct](https://github.com/ejpcmac/typed_struct) to define typed structs without boilerplate
- [exconstructor](https://hex.pm/packages/exconstructor) to create structs from JSON

### Day 4: 2021-03-16

- A function with multiple clauses and default values [must have a function head, declaring the defaults](https://elixir-lang.org/getting-started/modules-and-functions.html#default-arguments)
- Solved an [exercism refactoring challenge](https://exercism.io/my/solutions/29a254e2ed5b4ca282d23e78a7811f1f):
  - [Initial code](https://github.com/diegosouza/exercism/blob/05cfc5b96c1389126cc23c00312a5291604aba56/elixir/markdown/lib/markdown.ex)
  - [Slightly refactored code](https://github.com/diegosouza/exercism/blob/b1c0806610353350a2b083bdebcdd8217d2bd2a2/elixir/markdown/lib/markdown.ex). Harder than I expected. Later I'll read other people's solution to learn from my weaknesses
- Started the [Robot Simulator challenge on exercism](https://github.com/diegosouza/exercism/commit/5921be5d1fab0f70937e4b3907fdd09c8753eac5)
- Started using [watchexec](https://github.com/watchexec/watchexec) to rerun tests after file changes

### Day 5: 2021-03-17

- Created guards using `defguard`
- Learned I should avoid putting tuples inside structs, maps and nested structures (they're not good to traverse/access/update)
- [Finished the Robot Simulator challenge](https://github.com/diegosouza/exercism/blob/af6581a05c71fd770516afeb81707f7386ca96b4/elixir/robot-simulator/lib/robot_simulator.ex) from exercism

### Day 6: 2021-03-18

- Studied [a good example](https://github.com/diegosouza/exercism/commit/13db2bbbed3f4b788a2d847b10ed854fd122a786) how pattern matching with strings + recursion can be powerful
- Played with the String module + regex
- Started the List Ops challenge from exercism

### Day 7: 2021-03-19

- Learned I need to call `mix text` inside `iex` explicitly to debug using `require IEx; IEx.pry()`: `iex -S mix test`
- [Finished the List Ops challenge](https://github.com/diegosouza/exercism/blob/90dddd65139048de887cae841aeee8adaeeb0566/elixir/list-ops/lib/list_ops.ex) from exercism. It was a big challenge to me
- `cons` operator (`|`) used several times, like never before

### Day 8: 2021-03-20

- Played a little with the [youtex](https://github.com/patrykwozinski/youtex) codebase
- Sent [a tiny PR](https://github.com/patrykwozinski/youtex/pull/3) for the `youtex` project. Probably others will arrive
- Realized I have to study macros seriously. They're essential to create DSLs

### Day 9: 2021-03-21

After watching [The Upside Down Dimension of Elixir - An Intro to Metaprogramming](https://www.youtube.com/watch?v=EFAgc7YqDP8) my comprehension about macros is really better:

- Macros are in general AST -> AST, usually with a 3 elements tuple like this: `{atom() | tuple(), keyword_metadata(), [param1, param2]}` (there are some exceptions)
- `quote(opts, block)` transforms the block content into AST. Something like:

```elixir
quote do
  sum(1, 2, 3)
end

# {:sum, [], [1,2,3]}
```

- `unquote(expression)` transforms AST to normal values/expressions. Depending on the data, `Macro.escape(value)` is also needed
- Contexts:
  - Macro contexxt: before the quote block
  - Caller's context: inside the quote block
- `use(module, opts \\ [])` is a macro to call the `module.__using__()` to the caller's context

More contributions to [patrykwozinski/youtex](https://github.com/patrykwozinski/youtex). One issue + 2 PRs:

- [https://github.com/patrykwozinski/youtex/issues/5](https://github.com/patrykwozinski/youtex/issues/5)
- [https://github.com/patrykwozinski/youtex/pull/6](https://github.com/patrykwozinski/youtex/pull/6)
- [https://github.com/patrykwozinski/youtex/pull/4](https://github.com/patrykwozinski/youtex/pull/4)

### Day 10: 2021-03-22

2 PRs:

- [https://github.com/patrykwozinski/youtex/pull/7](https://github.com/patrykwozinski/youtex/pull/7)
- Second one to be submitted tomorrow

Also I learned multiple when guard clauses have `or` effect

### Day 11: 2021-03-23

Played with the [youtex](https://github.com/patrykwozinski/youtex) codebase and I sent [one PR](https://github.com/patrykwozinski/youtex/pull/9)

Feeling a lot more confident to do some refactoring (already started)

### Day 12: 2021-03-24

My first [refactoring PR with substantial changes](https://github.com/patrykwozinski/youtex/pull/10) for an Elixir project, including some tests (where no one existed before)

### Day 13: 2021-03-25

Today I learned:

- Every `binary` is a `bitstring`, but not all bitstrings are binaries (data type)
- `<<1,2,3::4>>` every element has 1 byte (8 bits) except the third element (it has 4 bits), so the value is a bitstring but not a binary (not a multiple of 8)
- Strings in Elixir are binaries
- ``<<head:utf8, tail::binary> = my_string` is for bitstrings what [head | tail]` is for lists
- `?a` gives me the code point for the char `a`. Pattern matching the char: `0x0061 = 97 = ?a`

Great example for binary string with pattern matching:

```elixir
<<cpf_first_chunk::binary-size(3), cpf_second_chunk::binary-size(3), cpf_third_chunk::binary-size(3), cpf_digits::binary-size(2)>>` = "12345678910"
"#{cpf_first_chunk}.#{cpf_second_chunk}.#{cpf_third_chunk}-#{cpf_digits}"
```

### Day 14: 2021-03-26

Interesting projects I found:

- https://github.com/still-ex/still

I tried to use [bakeware](https://github.com/bake-bake-bake/bakeware) to generate a binary like a standalone file webserver (through cowboy). I realized I need to review GenServers and Supervisors.

Recap:

- GenServer (I forgot the "client" and "server" side differences)
- The goal of a GenServer is to abstract the receive loop for developers
- `handle_info/2` is often used with `Kernel.send` and `Process.send_after` to do some periodic task
- The `:sys` module from Erlang provides some great debugging + statistical info/tracing
- Application is a behaviour. It has it's own environment (that can be defined in `application/0`) and several methods to handle the lifecycle
- Agent is a Genserver to keep state (simpler)
- Task is a for short-lived async computation
- Supervisor strategies:
  - `:one_to_one` if one children dies, it's the only restarted
  - `:one_for_all` if one children dies, all supervised children are restarted
  - `:rest_for_one` restarts the dead one and the others after/below it
  - `:simple_one_for_one` is deprecated in favor of `DynamicSupervisor`
  - the `restart` option passed to the child takes precedence over one of the stategies above:
    - `:permanent` always restart
    - `:transient` restarts when crashed
    - `:temporary` never restarts

### Day 15: 2021-03-27

Golden resource of the day: [https://kobrakai.de/kolumne/child-specs-in-elixir/](https://kobrakai.de/kolumne/child-specs-in-elixir/)

Supervisor child spec map (`:restart`, `:shutdown`, `:type` and `:modules` are optional with defaults):

```elixir
%{
  id: Stack,
  start: {Stack, :start_link, [[:hello]]}
}
```

The several ways of doing it may be confusing for beginners:

```elixir
children = [
  # Module only
  MyApp.Supervisor,
  # Tuple
  {Registry, keys: :unique, name: Registry.ViaTest},
  # One-off way to build a child spec map 
  :poolboy.child_spec(name, pool_args, worker_args),
  # Inline child spec map
  %{id: Stack, start: {Stack, :start_link, [[:hello]]}}
]
```

**MyApp.Supervisor** is a shortcut for **{MyApp.Supervisor, []}** and therefore **MyApp.Supervisor.child_spec([])**.

The old way was something like this:

```elixir
children = [
  worker(MyWorker, [arg1, arg2, arg3]),
  supervisor(MySupervisor, [arg1])
]
```

When we call `use GenServer` or `use Supervisor`, both inject to us a `child_spec/1`.

**Cowboy and Plug**

- `cowboy` is an erlang package, `plug_cowboy` is an Elixir package with `cowboy` and `plug` as dependencies
- A Plug should have the methods `init(options)` and `call(conn, opts)`
- `use Plug.Router` with `plug :match` and `plug :dispatch` + routes creates a valid Plug 
- `plug Plug.Logger` before `:match`and `:dispatch` enables logging

### Day 16: 2021-03-28

Played with some main Plug modules and concepts.

Together with [bakeware](https://github.com/bake-bake-bake/bakeware/), I already can start a local and extremely basic file server, parsing parameters with [OptionParser](https://hexdocs.pm/elixir/OptionParser.html).

### Day 17: 2021-03-29

Registry:

- Interesting to avoid reaching the BEAM's limit for atoms
- Often used with `DynamicSupervisor`
- It uses ETS tables
- To use with `:via` tuple

The binary generated with `bakeware` didn't work as expected. I stopped with a basic file share using cowboy and few options.

I played with `GenStage` using the basic documentation (1 producer + 1 producer consumer + 1 consumer).

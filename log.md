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

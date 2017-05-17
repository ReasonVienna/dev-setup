# ReasonVienna Development Setup

In this repository you will find all the instructions and tools you
need to be able to contribute to our Reason projects at
ReasonVienna. This guide will also give you some insights in the
ReasonML ecosystem and explain the responsibilites of all required
tools.

## Reason Ecosystem & Installation

When people think about Reason, they think about the revamped syntax
addon for OCaml.  Actually, Reason is more than that. It is a complete
toolchain for building Reason & OCaml applications with an opinionated
workflow.

**OCaml specific tools:**


**The toolchain contains following things:**

| Name          | Description   | From which opam package? |
| ------------- | ------------- | --------------- |
| `refmt`       | This is the reformatter for pretty-printing reason-code | reason |
| `ocamlmerlin`      | This is the (OCaml-specific) tool which gives you autocompletion & compiler errors in your editor | merlin |
| `ocamlmerlin-reason` | This is a bridge to make `merlin` understand the reason syntax             | reason |
| `rebuild`     | This is a compiled wrapper of `ocamlbuild` with saner defaults and reason syntax addon| reason |

### Installation

OCaml is installed via `opam`, the OCaml pendant to `nvm` & `npm`.
It manages your OCaml compiler versions which are called a `switch`.
Each `switch` has its own set of installed opam packages.

``` bash
# Install opam (OSX homebrew)
brew install opam

# This will initialize your opam environment
opam init

# **Note**: add the line below to your ~/.bashrc or ~/.zshrc too; it's needed at every shell startup
eval $(opam config env)
```

After the initialization, `opam` will store your complete OCaml
environment (packages, compilers, configuration) in `~/.opam`.

This weird `eval $(opam config env)` statement is used to inject the
current `opam` configuration in your `$PATH` variable.  This is super
important for the editor integration. Otherwise your editor
plugin will not find the tools needed to provide you with
autocompletion etc.

Now it is time to install the correct OCaml compiler for Reason:

``` bash
opam update
opam switch 4.02.3

# You will probably have to eval your config again
eval $(opam config env)
```

Since we now have the correct compiler installed, we can now install all required `opam` packages:

``` bash
opam install reason
opam install merlin
```

Let's check if everything is working:

``` bash
which ocamlmerlin refmt ocamlmerlin-reason

echo 'print_string "hello!"' > hello.re

# rebuild is another binary exposed by the Reason package
rebuild hello.native # Automatically generates hello.native from hello.re

./hello.native # Should display "hello!"
```

## Editor Integration

Since there are many editors out there, we try to align to one
specific editor, which turned out to be VSCode.  If you are attending
to our mob programming sessions, it is highly recommended to set
everything up, in case someone else needs to work on the same machine.

Of course, feel free to use whatever editor you want. You can check
out the
official
[Editor Integration Section](https://facebook.github.io/reason/tools.html#editor-integration) for
your target editor.



## VSCode

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

**The toolchain contains following things:**

| Name          | Description   | From which opam package? |
| ------------- | ------------- | --------------- |
| `ocamlmerlin`      | This is the (OCaml-specific) tool which gives you autocompletion & compiler errors in your editor | merlin |
| `ocamlmerlin-reason` | This is a bridge to make `merlin` understand the reason syntax             | reason |
| `rtop`        | Interactive Reason interpreter for your terminal | reason |
| `refmt`       | This is the reformatter for pretty-printing reason-code | reason |
| `rebuild`     | This is a compiled wrapper of `ocamlbuild` with saner defaults and reason syntax addon| reason |

Reason is heavily built on existing OCaml infrastructure, so you will
probably encounter many OCaml related terms. Don't get discouraged by
this, but we promise that you will get used to it very quickly, as
soon as you build your first Reason application.

### OCaml / Reason Tools Installation

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
plugin will not be able to find the tools needed to provide you with
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
opam install reason.1.13.7
opam install merlin.2.5.4
```

Let's check if everything is set up correctly:

``` bash
which ocamlmerlin refmt ocamlmerlin-reason

echo 'print_string "hello!"' > hello.re

# rebuild is another binary exposed by the Reason package
rebuild hello.native # Automatically generates hello.native from hello.re

./hello.native # Should display "hello!"
```

### BuckleScript

You probably noticed that we didn't install anything JavaScript related yet, right?
Maybe you also know that there are two specific workflows described on the offical Reason website:

* [jsWorkflow](https://facebook.github.io/reason/jsWorkflow.html)
* [nativeWorkflow](https://facebook.github.io/reason/nativeWorkflow.html#native-workflow)

For now, we installed all the tools we need for our editor integration & for building native OCaml applications.
To build JavaScript, you need to use the BuckleScript platform, which is installed via `npm`.

Here are the official install instructions of a newly created `npm` based project:

``` bash
# new folder setup, add package.json, install BuckleScript
mkdir -p test/src && cd test
echo 'print_endline "hello!";' > src/test.re
npm init -y
npm install --save-dev bs-platform

# basic BuckleScript build config, start it in watch mode
echo '{"name": "test", "sources": "src"}' > bsconfig.json
./node_modules/.bin/bsb -w
```

BuckleScript is installed as `bs-platform`. The interesting part about
this package is, that it also ships with a complete OCaml environment
and has all the tools it need to build OCaml code and to transform the
result to JavaScript.

You will probably ask why we installed `opam` in the beginning then?
That's because (as for right now) it is the easiest way to install all the
required tools for our editor integration.

There is also a `npm` based ([reason-cli](https://github.com/reasonml/reason-cli)) approach, but as in our experience the
installation process was very fragile and problematic on various
machines.



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

To efficiently write Reason code in VSCode, we need the ReasonML
plugin, which can be
found [here](https://github.com/freebroccolo/vscode-reasonml).

You can install it directly in VSCode by searching for `reasonml` in the plugin repository
If all the previous installation steps have be done correctly, you should now be able to open
a ReasonML project and get all the `merlin` features as auto-completion and type inference.

We also recommend to enable following setting in your ReasonML settings:

```
"reason.formatOnSave": true,
```

This will automatically transform your code with `refmt`, whenever you save a Reason file.

## Contributing

That's it! Hopefully this will get you started for some ReasonML
at ReasonVienna :-) If you have ideas to make this guide more helpful,
just let us know or send a PR with your proposed changes!


Make sure to check our [ReasonVienna Meetup Page](https://www.meetup.com/Reason-Vienna/) for upcoming events or
follow us on twitter: [@reasonvienna](https://twitter.com/reasonvienna)


Happy Coding!



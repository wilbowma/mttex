# MTTeX
Welcome to the Meta-Theory LaTeX package.

This package provides numerous macros and combinators for formatting
meta-theory---particularly multi-language compiler-correctness
meta-theory. I use "combinator" to mean a macro that takes macros as
inputs and defines new macros, or a macro that can be partially applied
to produce a new macro. This README provides sections describing various
aspects of the package.

## Why MTTeX
Partly because it's a La*TeX* package for type-setting *m*eta-*t*heory, and
partly because it's pronounced "Empty TeX". This package started because
the prevailing method for writing papers in my lab was to copy and paste
a file called "defs.tex" and modify it for the new project. I felt the
patterns found in this file could be abstracted, ideally to the point
that "defs.tex" was practically empty.

## Table of Contents

* [Installation](#installation)
* [Required Packages](#required-packages)
* [Options](#options)
* [How to Read](#how-to-read)
* [Automagic Title-case](#automagic-title-case)
* [TODO and Comments](#todo-and-comments)
* [Label References](#label-references)
* [Font Shorthand](#font-shorthand)
* [Theorem Environment](#thm-environments)
* [Math Environments](#math-environments)
* [Standard Source/Target Macros](#standard-source-target-macros)
* [Meta-Language Macros](#meta-language-macros)
* [Language Symbol Macros](#language-symbol-macros)
* [Language Combinators](#language-combinators)
* [Meta-Theory Combinators](#meta-theory-combinators)
* [Spacing](#spacing)

## Installation
I recommend installing this package via git submodules until I figure
out how to do LaTeX packages. From a git repository that could use this
project, do
```bash
git submodule add git@github.com:wilbowma/mttex
ln -s mttex/*.sty .
```

Then add `\usepackage{mttex}` to your main TeX file.

## Required Packages
This package includes several packages not available on CTAN, and
requires several that are on CTAN.

The following packages included in this package.
* `mathpartir`
* `unlist`

The following packages are required and available on CTAN. Many of these
are included in standard LaTeX installations.
* `todonotes`
* `letltxmacro`
* `hyperref`
* `ifthen`
* `latexsym`
* `amsmath`
* `amssymb`
* `stmaryrd`
* `amsbsy`
* `upgreek`
* `url`
* `mathrsfs`
* `amsthm`
* `titlecaps`

The following packages are required due to ACM recommendation and
available on CTAN. These are included in standard LaTeX installations.
* `microtype`
* `inputenc`
* `fontenc`

## Options
This package defines the following options:

* `omit` -- This option causes the `\omitthis` macro to discard its
  argument, enabling passages to exist in the source that are not
  rendered in the output.
* `todo` -- Normally, the `\todo` macro is omitted when the `omit`
  option is specified. This option prevents only `\todo` macros from
  being omitted.
* `nosigplan` -- This option disables ACM/SIGPLAN specific features, such as `natbib`
  citation style.
* `techrpt` -- This option enables features formatting a technical appendix, such as
  `\usepackage{fullpage}`
* `paper` -- This option disables features for formatting a technical appendix. This
  option is on by default.
* `balance` -- This option balances the column on the last page.
* `draft` -- This option passes `draft` to `hyperref`.

## How to Read
Each documented macro starts with the name of the macro and an interface
declaring the number of arguments, possibly followed by the default
value for #1. The interface is followed by an explanation of the macro's
purpose and its arguments.
```latex
\macroname[<args>][default-value]
Has this purpose.
  #1 : A description of the first argument.
  #2 : And of the second argument.
```

Macros may be undocumented but given with their interface or their
definitions if they merely provide shorthand or match a standard
interface.

## Automagic Title-case
This package redefines the following standard macros. These macros match
the interface of their standard counter-parts, with some caveats listed before, but automatically
output the titles in title-case.
```latex
\title[2][]
\section[2][]
\subsection[2][]
\subsubsection[2][]
```

The original macro are still accessible, though they are @ protected. To
access these, you need to surround their uses with `\makeatletter` and
`\makeatother`.
```latex
\@title[2][]
\@section[2][]
\@subsection[2][]
\@subsubsection[2][]
```

You can control which words should be left lower-case the macro
`\Addlcwords`. By default, the following words are added:
```latex
\Addlcwords{for a is but and with of in as the etc on to if}
```

Caveats:
Including math and certain macros inside the title or section name will cause the `titlecaps` package to choke.
To workaround this, use the following pattern:

```
\makeatlatter
\@section{\titlecaps{Title bla bla} $\math$ \titlecaps{More math}}
\makeatother
```

## TODO and Comments
This package provides the following macros for adding TODO comments.
```latex
\omitthis[1]
Does not render its argument if the omit option is specified.
  #1 : A comment to potentially omit.
```

```latex
\todo[2][]
Add a margin comment, and registers the comment into a todo list.
  #1 : Formatting options for the todo macro. See the todonotes package
    for more information.
  #2 : The todo comment
```

```latex
\listoftodos
Formats a list containing all comments added by calls to \todo.
```

```latex
\todoleft[2][]
Like \todo, but adds the comment to the left margin.
```

```latex
\margincomment[2][]
Like \todo, but colors the comment in green and does not add it to the todolist
```

```latex
\inlinecomment[2][]
Like \margincomment, but places the comment inline rather than in the margin.
```

## Label References
This package provides the following macros for referring to sections,
figures, lemmas, and theorems.
```latex
\secref[1]
Formats a reference to a section.
  #1 : The label for the section to reference.
```

```latex
\figref[1]
Formats a reference to a figure.
  #1 : The label for the figure to reference.
```

```latex
\lemref[1]
Formats a reference to a lemma.
  #1 : The label for the lemma to reference.
```

```latex
\thmref[1]
Formats a reference to a theorem.
  #1 : The label for the theorem to reference.
```

## Font Shorthand
This package provides the following shorthand for fonts:
```latex
% Text fonts
\newcommand{\tbf}[1]{\textbf{#1}}
\newcommand{\trm}[1]{\textrm{#1}}
\newcommand{\tnl}[1]{\small{\trm{#1}}}

% Math fonts
\newcommand{\mbb}[1]{\mathbb{#1}}
\newcommand{\mbf}[1]{\mathbf{#1}}
\renewcommand{\mit}[1]{\mathit{#1}}
\newcommand{\mrm}[1]{\mathrm{#1}}
\newcommand{\mtt}[1]{\mathtt{#1}}
\newcommand{\mcal}[1]{\mathcal{#1}}
\newcommand{\mfrak}[1]{\mathfrak{#1}}
\newcommand{\msf}[1]{\mathsf{#1}}
\newcommand{\mscr}[1]{\mathscr{#1}}
\renewcommand{\b}{\boldsymbol}
```

## Theorem Environments
This package provides environments for theorems, lemmas, conjectures, corollaries, and definitions
These are all generated and styled using amsthm:
```latex
\newtheoremstyle{athm}{\topsep}{\topsep}%
     {\athmbody}      % Body font
     {}               % Indent amount (empty = no indent, \parindent = para indent)
     {\athmhead}      % Thm head font
     {\athmheadpunct} % Punctuation after thm head
     {\athmheadspace} % Space after thm head
     {\thmname{#1}\thmnumber{ #2}\thmnote{~\,(#3)}} % Thm head spec

\newtheorem{theorem}{Theorem}[section]
\newtheorem{lemma}[theorem]{Lemma}
\newtheorem{conjecture}[theorem]{Conjecture}
\newtheorem{corollary}[theorem]{Corollary}
\newtheorem{definition}[theorem]{Definition}
```

If you want to redefine the default style, you can renew the following commands:
```latex
\newcommand{\athmbody}[1]{#1}
\newcommand{\athmhead}{\bfseries}
\newcommand{\athmheadpunct}{}
\newcommand{\athmheadspace}{\newline}
 ```

## Math Environments
This package provides the following extra math environments:

### Math Paragraph and Math Display
```latex
\newenvironment{sdisplaymath}
Like the displaymath environment, but makes everything \small.
```

```latex
\newenvironment{fdisplaymath}
Like the displaymath environment, but makes everything \footnotesize.
```

```latex
\newenvironment{smathpar}
Like mathpar, but makes everything \small.
```

```latex
\newenvironment{fmathpar}
Like mathpar, but makes everything \footnotesize.
```

### Align Environments
```latex
\newenvironment{alignS}
Like align, but ignores space after the end of the environment
```

```latex
\newenvironment{salignS}
Like alignS, but but makes everything \small
```

```latex
\newenvironment{falignS}
Like alignS, but but makes everything \footnotesize
```

### Stack Environments
The stack environments format each line by stacking them atop each
other, similar to the array environment with one column.

```latex
\newenvironment{stackCC}
A stack environment that center aligns the column vertically and
horizontially.
```

```latex
\newenvironment{stackCL}
A stack environment that center aligns the column vertically and left
aligns the column horizontially.
```

```latex
\newenvironment{stackTL}
A stack environment that top aligns the column vertically and left
aligns the column horizontially.
```

```latex
\newenvironment{stackTR}
A stack environment that top aligns the column vertically and right
aligns the column horizontially.
```

```latex
\newenvironment{stackBC}
A stack environment that bottom aligns the column vertically and center
aligns the column horizontially.
```

```latex
\newenvironment{stackBL}
A stack environment that bottom aligns the column vertically and left
aligns the column horizontially.
```

### Cases and Subcases
This package redefines the `cases` environment, and provides cases and
subcases. This helps format nested proofs.
```latex
\renewenvironment{cases}
\newcommand{\case}[1][]
\newcommand{\scase}[1][]
\newcommand{\sscase}[1][]
```

## Standard Source/Target Macros
This package provides a few standard formatting macros for source/target
languages. They assume the source should be in a blue, sans-serif font,
while the target should be in a bold, red, serif font.
```latex
\newcommand{\scolor}[1]{\textcolor{blue}{#1}}
\newcommand{\tcolor}[1]{\textcolor{red}{#1}}

\newcommand{\sfonttext}[1]{\textsf{\scolor{#1}}}
\newcommand{\tfonttext}[1]{\textsf{\tcolor{#1}}}

\newcommand{\sfont}[1]{\mathsf{\scolor{#1}}}
\newcommand{\tfont}[1]{\mathbf{\tcolor{#1}}}

\newcommand{\sfontsym}[1]{\sfont{#1}}
\newcommand{\tfontsym}[1]{\b{\tfont{#1}}}

\newcommand{\scal}[1]{\sfontsym{\mathcal{#1}}}
\newcommand{\tcal}[1]{\tfontsym{\mathcal{#1}}}

\newcommand{\sprime}{\scolor{\prime}}
\newcommand{\tprime}{\tcolor{\prime}}
```

## Meta-Language Macros
```latex
\newcommand{\metafont}[1]{\mathrm{#1}}
\newcommand{\dom}[1]{\metafont{dom}(#1)}
\newcommand{\cod}[1]{\metafont{cod}(#1)}
\newcommand{\rng}[1]{\metafont{rng}(#1)}
\newcommand{\FV}{\metafont{fv}}
\newcommand{\FTV}{\metafont{ftv}}
\newcommand{\subst}[3]{{#1}[{#2}/{#3}]}
\newcommand{\defeq}{\stackrel{\metafont{def}}{=}}
\newcommand{\finmap}{\stackrel{\metafont{fin}}{\rightarrow}}
\renewcommand{\iff}{\metafont{iff}}
\newcommand{\lsem}{\left\llbracket}
\newcommand{\rsem}{\right\rrbracket}
\newcommand{\sembrace}[1]{\lsem{#1}\rsem}
\newcommand{\powset}[1]{\mathscr{P}(#1)}
\newcommand{\irred}[1]{\metafont{irred}(#1)}
\renewcommand{\max}[2]{\metafont{max}(#1,#2)}
\newcommand{\free}[2]{\metafont{free}(#1,#2)}
\newcommand{\running}[2]{\metafont{running}({#1},{#2})}
\newcommand{\pair}[2]{( #1, #2 )}
\newcommand{\triple}[3]{( #1, #2, #3 )}

\newcommand{\satisfy}{\vDash}

\newcommand{\plus}{+}
\newcommand{\etal}{\textit{et al.}}
\newcommand{\ie}{\emph{i.e.}}
\newcommand{\eg}{\emph{e.g.}}
\newcommand{\etc}{\emph{etc.}}
\newcommand{\bump}{\hspace{3.5pt}}
\newcommand{\fresh}[1]{(\mit{fresh}\:#1)}
\newcommand{\where}[1]{\mrm{where}\:#1}

\newcommand{\lang}[1]{\mrm{\trm{#1}}}
```

## Language Symbol Macros
```latex
\newcommand{\emptyenv}{\cdot}
\newcommand{\emptyctx}{[\cdot]}
\newcommand{\hole}{\emptyctx}
\newcommand{\hw}[1]{\lbrack{#1}\rbrack}
\newcommand{\ectx}{E}
\newcommand{\ctx}{C}

\newcommand{\hooklongrightarrow}{\lhook\joinrel\longrightarrow}
\newcommand{\redexstep}{\hookrightarrow}
\newcommand{\redexstepinv}{\hookleftarrow}

\newcommand{\step}{\longmapsto}
\newcommand{\stepin}[1]{\step^{#1}}
\newcommand{\stepstar}{\stepin{*}}

\newcommand{\red}{\Downarrow}
\newcommand{\diverg}[1]{#1 \Uparrow}

\newcommand{\termin}[1]{#1\red}
\newcommand{\terminw}[2]{\termin{#1} #2}

\newcommand{\transarrow}{\leadsto}
\newcommand{\backtransarrow}{\twoheadrightarrow}

\newcommand{\funarrow}{\rightarrow}
\newcommand{\ctxarrow}{\Rightarrow}

\newcommand{\bnfalt}{{\bf \,\,\mid\,\,}}
\newcommand{\bnfdef}{{\bf ::=}}
```

## Language Combinators
This package provides various combinators for generating macros that
format multi-language meta-theory.

### Language Combinator TOC
* [Generating a Language](#generating-a-language)
* [Meta-Variables](#meta-variables)
* [List-of-Meta-Variables Combinators](#list-of-meta-variables-combinators)
* [Formatting Types and Expressions](#formatting-types-and-expressions)
* [List-of-Types Combinator](#list-of-types-combinator)
* [List-of-Expressions Combinator](#list-of-expressions-combinator)
* [Detailed Type Combinator Documentation](#detailed-type-combinator-documentation)
* [Detailed Expression Combinator Documentation](#detailed-expression-combinator-documentation)

### Generating a Language
This package provides a single combinator for generating all the macros
for type-setting meta-variables, types, and expressions. While this is
probably the macro you want to use, you will need to understand the
macros it composes to understand the macros it generates. They are
explained below.
```latex
\newlanguage[8]
Generates macros for formatting meta-variables, types, and expressions
of a language.

#1 : A formatting macro for super-scripts, sub-scripts, and primes in
  this language, such as \tcolor
#2 : A formatting macro for math text in this language, such as \tfont
#3 : A formatting macro for symbols in this language, such as
  \tfontsym
#4 : A language prefix for the macros, such as t
#5 : A list of meta-variables for which to generate macros via
  \newmetavars, such as {x, e, v}
#6 : A list of meta-variables for which to generate macros via
  \newmetavarsS, such as {ty/\tau,alpha\alpha}
#7 : A list of types for which to generate macros via \newtypes, such
  as {fun, forall, exist, pair, bool, unit}
#8 : A list of expressions for which to generate macros via
  \newexprs, such as {fun, app, if, true, false, unit}

Usage:
  \newlanguage{\scolor}{\sfont}{\sfontsym}{s}
  {x,e,v}
  {alpha/\alpha,ty/\sigma}
  {fun,bool}
  {fun,app,if,true,false}
```

### Meta-Variables
Writing all the macros to properly format language meta-variables is
obnoxious. So this package provides combinators for meta-variables.
```latex
\newmetavar[3]
Implements the * LaTeX idiom after currying. It expands in to either
\newmetavarStar{#1}{#2}{#3} or \newmetavarNoStar{#1}{#2}{#3} depending
on whether the character following its 3rd argument is a * or not.
  #1 : A formatting macro for the meta-var, such a \tfont
  #2 : A formatting macro for the subscripts, superscripts, and primes,
    such as \tcolor
  #3 : A string prefix for the name of the macro, such as t

Usage:
  \newcommand{\newtmetavar}{\newmetavar{\tfont}{\tcolor}{t}}
  \newtmetavar{x}
  \newtmetavar*{ty}{\tau}
```

```latex
\newmetavarStar[5]
Generates some standard macros for formatting a meta-variable.
  #1 : A formatting macro for the meta-var, such a \tfont
  #2 : A formatting macro for the subscripts, superscripts, and primes,
    such as \tcolor
  #3 : A string prefix for the name of the macro, such as t
  #4 : A string name of the macro, such as ty
  #5 : A string to format and display this meta-variable as, such as
    \tau

Usage:
  \newmetavarStar{\tfont}{\tcolor}{t}{ty}{\tau}

This usage generates the following definitions:

  \newcommand{\ttymetavar}[3]{
     \metavar{\tfont{\tau}}{\tcolor{#1}}{\tcolor{#2}}{\tcolor{\prime}}{#3}
   }

  \newcommand{\tty}{ \ttymetavar{}{}{} }
  \newcommand{\ttyin}[1]{ \ttymetavar{#1}{}{0} }
  \newcommand{\ttyto}[1]{ \ttymetavar{}{#1}{0} }
  \newcommand{\ttypr}[1][1]{ \ttymetavar{}{}{#1} }
  \newcommand{\ttyone}{ \ttymetavar{1}{}{} }
  \newcommand{\ttyonepr}[1][1]{ \ttymetavar{1}{}{#1}}
  \newcommand{\ttytwo}{ \ttymetavar{2}{}{} }
  \newcommand{\ttytwopr}{ \ttymetavar{2}{}{1} }
  \newcommand{\ttythree}{ \ttymetavar{3}{}{} }
  \newcommand{\ttythreepr}{ \ttymetavar{3}{}{1} }
  \newcommand{\ttyi}{ \ttymetavar{i}{}{} }
  \newcommand{\ttyipr}[1][1]{ \ttymetavar{i}{}{#1} }
  \newcommand{\ttyn}{ \ttymetavar{n}{}{} }
  \newcommand{\ttynpr}[1][1]{ \ttymetavar{n}{}{#1} }

  \ttymetavar takes an unformatted sub-script, super-script, and
  a natural number n indicating the number of primes. It then formats
  the sub-script, the super-script, and n primes and attaches them to
  the formatted meta-variable.
```

```latex
\newmetavarNoStar[4]
Like \netmetavarStar, but assumes the name of the macro is also the
display symbol.
  #1 : A formatting macro for the meta-var, such a \tfont
  #2 : A formatting macro for the subscripts, superscripts, and primes,
    such as \tcolor
  #3 : A string prefix for the name of the macro, such as t
  #4 : A string name of the macro and symbol to format and display, such
    as x

Usage:
  \newmetavarNoStar{\tfont}{\tcolor}{t}{x}

This usage is equivalent to
  \newmetavarStar{\tfont}{\tcolor}{t}{x}{x}
```

```latex
\metavar[5]
Formats a language meta-var.
  #1 : a pre-formatted symbol representing the meta-variable
  #2 : a pre-formatted subscript
  #3 : a pre-formatted superscript
  #4 : a pre-formatted prime symbol
  #5 : a natural number, representing the number of primes

Usage:
  \newcommand{\txmetavar}[3]{
    \metavar{\tfont{x}}{\tcolor{#1}}{\tcolor{#2}}{\tprime}{#3}
  }
  \newcommand{\tx}{\txmetavar{}{}{}}
  \newcommand{\txone}{\txmetavar{1}{}{}}
  \newcommand{\txonepr}{\txmetavar{1}{}{1}}
```

```latex
\metavarto[2]
Formats a language meta-var with only a superscript.
  #1 : a pre-formatted symbol representing the meta-var
  #2 : a pre-formatted superscript

Usage:
  \newcommand{\txF}{\metavarto{\tx}{f}}
```

```latex
\metavarin[2]
Formats a language meta-var with only a subscript.
  #1 : a pre-formatted symbol representing the meta-var
  #2 : a pre-formatted subscript

Usage:
  \newcommand{\txone}{\metavarin{\tx}{\tcolor{1}}}
```

```latex
\metavarpr[3]
Formats a language meta-var with only primes, takes 3 parameters:
  #1 : a pre-formatted symbol representing the meta-var
  #2 : a pre-formatted prime symbol
  #3 : a natural number representing the number of primes

Usage:
  \newcommand{\txpr}{\metavarpr{\tx}{\prime}{1}}
  \newcommand{\txdubpr}{\metavarpr{\tx}{\prime}{2}}
```

### List-of-Meta-Variables Combinators
Generating meta-variables one at a time is annoying, so this package
provides combinators for lists of meta-variables.

```latex
\newmetavars[4]
Defines new metavar macros for a list of names, assuming each metavar
will be displayed via the symbol it is named.  Essentially, it calls
\newmetavar for each name in its 4th parameter.
  #1 : A formatting macro for the meta-var, such a \tfont
  #2 : A formatting macro for the subscripts, superscripts, and primes,
    such as \tcolor
  #3 : A string prefix for the name of the macro, such as t
  #4 : A list of names.

Usage:
  \newmetavars{\tfont}{\tcolor}{t}{x,e,v}
  \newcommand{\newsmetavars}{\newmetavars{\sfont}{\scolor}{s}}
  \newsmetavars{x,e,v}
```

```latex
\newmetavarsS[4]
Defines new metavar macros for a list of name/symbol pairs. Essentially,
it calls \newmetavar* for each name/symbol pair in its 4th parameter.
  #1 : A formatting macro for the meta-var, such a \tfont
  #2 : A formatting macro for the subscripts, superscripts, and primes,
    such as \tcolor
  #3 : A string prefix for the name of the macro, such as t
  #4 : A list of name/symbol pairs, separated literally by a /.

Usage:
  \newmetavarsS{\tfont}{\tcolor}{t}{x/x,e/e,v/v,alpha/\b{\alpha}}
  \newcommand{\newsmetavarsS}{\newmetavarsS{\sfontsym}{\scolor}{s}}
  \newsmetavarsS{\alpha/\alpha, ty/\sigma}
```

### Formatting Types and Expressions
This package provides combinators for formatting lambda calculus types
and expressions.

Each combinator starts with a tag and ends with a suffix followed.
The suffix for type combinators is `ty` and the suffix for expression
combinators is `e`. For instance, the function type combinator is
`\funty` and the function expression combinator is `\fune`.

Each combinator takes a formatting macro for symbols, such as
`\tfontsym`, as its first argument, and a formatting macro for text,
such as `\tfont`, as its second argument. The rest of the arguments
are the sub-types or sub-expressions required for the type or
expression. While the arguments are fairly standard and in an intuitive
order, they are documented in detail below.

The package provides the following the following types and expressions.
The tag which starts each element of the list indicates the prefix of of
the combinator.

* fun: function types and function expressions
* app: application expressions
* polyfun: polymorphic function types and polymorphic functions
* papp: polymorphic application expressions
* forall: universal types and abstraction expressions
* inst: instantiation expressions
* exist: existential types
* pi: pi types (dependent function types)
* sigma: sigma types (dependent pair types)
* pack: pack expressions
* unpack: unpack expressions
* mu: isorecursive types
* fold: fold expression
* unfold: unfold expressions
* fix: fix-point expressions
* unit: the unit type, and the unit expression
* void: the void type
* bool: boolean types
* set: the type Set
* prop: the type Prop
* type: the type of types, Type
* true: true expressions
* false: false expressions
* if: if expressions
* pair: pair types and pair expressions
* prj: projection from a pair
* sum: sum types and sum expressions (injections)
* case: case expressions
* dcase: dependent case expressions.
* let: let expressions
* alet: let expressions with type annotations on the bound expression

### List-of-Types Combinator
Generating type macros one at a time is annoying, so this package
provides combinators for lists of types. The macros are generated
attaching a prefix and suffix to the tag, followed by ty.  For instance,
the macro generate for `fun` when using the prefix `s` and suffix `ty`
is `\sfunty`.
```latex
\newtypes[5]
Generates type formatting macros given a list of tags.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : A formatting macro for text, such as \tfont
  #3 : A prefix for the name of each macro, such as t
  #4 : A suffix for the name of each macro, such as ty
  #5 : A list of type tags, such as {fun,bool,void,unit}
```

### List-of-Expressions Combinator
Generating expression macros one at a time is annoying, so this package
provides combinators for lists of expressions. The macros are generated
attaching a prefix and suffice to the tag. For instance, the macro
generate for `fun` when using the prefix `s` and suffix `e` is `\sfune`.
```latex
\newexprs[5]
Generates type formatting macros given a list of tags.
  #1 : A formatting macro for symbols, such as \sfontsym
  #2 : A formatting macro for text, such as \sfont
  #3 : A prefix for the name of each macro, such as s
  #4 : A suffix for the name of each macro, such as e
  #5 : A list of type tags, such as {fun,bool,void,unit}
```

#### Detailed Type Combinator Documentation
```latex
\funty[4]
Formats a function type.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : A formatting macro for text, such as \tfont
  #3 : The pre-formatted argument to the function
  #4 : The pre-formatted result of the function
```

```latex
\polyfunty[5]
Formats a polymorphic function type.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : A formatting macro for text, such as \tfont
  #3 : The pre-formatted type-variable to bind
  #4 : The pre-formatted argument to the function
  #5 : The pre-formatted result of the function
```

```latex
\forallty[4]
Formats a polymorphic type.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : A formatting macro for text, such as \tfont
  #3 : The pre-formatted type-variable to bind
  #4 : The pre-formatted result in which the type-variable is bound
```

```latex
\existty[4]
Formats an existential type.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : A formatting macro for text, such as \tfont
  #3 : The pre-formatted type-variable to bind
  #4 : The pre-formatted result in which the type-variable is bound
```

```latex
\muty[4]
Formats a recursive type.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : A formatting macro for text, such as \tfont
  #3 : The pre-formatted type-variable to bind
  #4 : The pre-formatted result in which the type-variable is bound
```

```latex
\unitty[2]
Formats a unit type.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : A formatting macro for text, such as \tfont
```

```latex
\pity[4]
Formats a dependent function type.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : The pre-formatted variable to bind
  #3 : The pre-formatted argument type
  #4 : The pre-formatted result type
```

```latex
\sigmaty[5]
Formats a dependent pair type.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : The pre-formatted variable the function binds.
  #4 : The pre-formatted type of the variable.
  #5 : The pre-formatted body of the function.
```

```latex
\voidty[2]
Formats a void type.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : A formatting macro for text, such as \tfont
```

```latex
\boolty[2]
Formats a bool type.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : A formatting macro for text, such as \tfont
```

```latex
\typety[3][i]
Formats a type of types, or universe (Type)

  #1 : A formatting macros for symbols, such as \tfontsym
  #2 : A formatting macros for text, such as \tfont.
  #3 : A pre-formatted universe level, which defaults to i.
```

```latex
\propty[2]
Formats the type Prop, as in CIC's impredicative universe Prop.

  #1 : A formatting macros for symbols, such as \tfontsym
  #2 : A formatting macros for text, such as \tfont.
```

```latex
\setty[2]
Formats the type Set, as in CIC's predicative universe Set.

  #1 : A formatting macros for symbols, such as \tfontsym
  #2 : A formatting macros for text, such as \tfont.
```

```latex
\pairty[4]
Formats a pair type.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : A formatting macro for text, such as \tfont
  #3 : The pre-formatted type for the first component of the pair
  #4 : The pre-formatted type for the second component of the pair
```

```latex
\sumty[4]
Formats a sum type.
  #1 : A formatting macro for symbols, such as \tfontsym
  #2 : A formatting macro for text, such as \tfont
  #3 : The pre-formatted type for the first component of the sum
  #4 : The pre-formatted type for the second component of the sum
```

#### Detailed Expression Combinator Documentation
```latex
\fune[5]
Formats a function expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : The pre-formatted variable the function binds.
  #4 : The pre-formatted type of the variable.
  #5 : The pre-formatted body of the function.
```

```latex
\polyfune[6]
Formats a polymorphic function expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : The pre-formatted type variable the function binds.
  #4 : The pre-formatted variable the function binds.
  #5 : The pre-formatted type of the variable.
  #6 : The pre-formatted body of the function.
```

```latex
\abstre[4]
Formats an polymorphic abstraction expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : The pre-formatted type variable the abstraction binds.
  #4 : The pre-formatted the body of the abstract.
```

```latex
\inste[4]
Formats an instantiation expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : The pre-formatted polymorphic abstraction to instantiate.
  #4 : The pre-formatted type with which to instantiate the abstraction.
```

```latex
\appe[4]
Formats an application expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : The pre-formatted function.
  #4 : The pre-formatted argument.
```

```latex
\pappe[5]
Formats a polymorphic function application expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : A pre-formatted polymorphic function expression.
  #4 : A pre-formatted type with which to instantiate.
  #5 : A pre-formatted argument to the function.
```

```latex
\ife[5]
Formats an if expression
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : A pre-formatted discriminant expression.
  #4 : A pre-formatted consequent expression.
  #5 : A pre-formatted alternate expression.
```

```latex
\packe[5]
Formats a pack expression
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : A pre-formatted type witness.
  #4 : A pre-formatted value witness.
  #5 : A pre-formatted existential type abstracting the witness type.
```

```latex
\unpacke[6]
Formats an unpack expression
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : A pre-formatted type variable.
  #4 : A pre-formatted expression variable.
  #5 : A pre-formatted existential witness expression.
  #6 : A pre-formatted expression in which to bind the existential.
```

```latex
\lete[5]
Formats a let expression
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : A pre-formatted expression variable.
  #4 : A pre-formatted expression to bind.
  #5 : A pre-formatted body expression for the let.
```

```latex
\alete[6]
Formats a let expression with an annotation on the bound expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : A pre-formatted expression variable.
  #4 : A pre-formatted expression to bind.
  #5 : A pre-formatted annotation for bound expression.
  #6 : A pre-formatted body expression for the let.
```

```latex
\folde[4]
Formats a fold expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : A pre-formatted mu type.
  #4 : A pre-formatted expression of isorecursive type.
```

```latex
\unfolde[3]
Formats an unfold expression
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : A pre-formatted expression of isorecursive type.
```

```latex
\fixe[5]
Formats a recursive function expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : The pre-formatted variable the function binds.
  #4 : The pre-formatted type of the variable.
  #5 : The pre-formatted body of the function.
```

```latex
\unite[2]
Formats a unit expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
```

```latex
\truee[2]
Formats a true expression
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
```

```latex
\falsee[2]
Formats a false expression
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
```

```latex
\paire[4]
Formats a pair expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : A pre-formatted expression for the first component of the pair.
  #4 : A pre-formatted expression for the second component of the pair.
```

```latex
\prje[4]
Formats a projection expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : An unformatted natural number, either 1 or 2, indicating which
    component of the pair to project.
  #4 : A pre-formatted pair expression to project.
```

```latex
\sume[4]
Formats a sum expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : An unformatted natural number, either 1 or 2, indicating into which
    side of the sum to inject the expression. 1 indicates left, 2
  #4 : A pre-formatted expression to inject into a sum.
```

```latex
\casee[7]
Formats a case expression.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : A pre-formatted discriminant expression.
  #4 : A pre-formatted variable to bind in the left branch.
  #5 : A pre-formatted expression for the left branch.
  #6 : A pre-formatted variable to bind in the right branch.
  #7 : A pre-formatted expression for the right branch.
```

```latex
\dcasee[5] formats a dependent case analysis expression, like that of CIC's.
  #1 : A formatting macro for symbols, such as \tfontsym.
  #2 : A formatting macro for text, such as \tfont.
  #3 : A pre-formatted discriminant expression.
  #4 : A pre-formatted motive
  #5 : A pre-formatted list of branch expressions.
```

## Meta-Theory Combinators
This package provides combinators for formatting meta-theory, including
well-formedness and typing judgments, contextual equivalence, context
typing, and logical relations.

### Meta-Theory Combinator TOC
* [Judgments](#judgments)
* [Context Typing](#context-typing)
* [Contextual Equivalence](#contextual-equivalence)
* [Logical Relations](#logical-relations)

### Judgments
```latex
\wf[2]
Formats a well-formedness judgment.
  #1 : Pre-formatted assumptions, such as \tfont{\Delta}
  #2 : The pre-formatted proposition, such as \tfont{\alpha}

Usage:
  \wf{\Delta}{\alpha}

Renders like:
  Δ ⊢ α
```

```latex
\judg[3]
Formats a well-typedness judgment.
  #1 : The assumptions, such as \tfont{\Delta};\tfont{\Gamma}
  #2 : The term, such as \tfont{e}
  #3 : The type, such as \tfont{\tau}

Usage:
  \judg{\Delta;\Gamma}{e}{\tau}

Renders like:
  Δ;Γ ⊢ e : τ
```

### Context Typing
```latex
\ctxarrowty[3]
Formats a context typing arrow
  #1 : A formatting macro for symbols, such as \stfontsym
  #2 : The type of the hole
  #3 : The type of the result
```

```latex
\ctxty[5]
Formats a context type, with different typing contexts for the hole and
result
  #1 : A formatting macro for symbols, such as \stfontsym
  #2 : The typing contexts for the hole
  #3 : The type of the hole
  #4 : The typing contexts for the result
  #5 : The type of the result
```

```latex
\ctxtyjudg[6]
Formats a context typing judgment.
  #1 : A formatting macro for symbols, such as \stfontsym
  #2 : A pre-formatted context
  #3 : The typing contexts for the hole
  #4 : The type of the hole
  #5 : The typing contexts for the result
  #6 : The type of the result
```

### Contextual Equivalence
```latex
\ciueqvjudg[4]
Formats a c.i.u. equivalence judgment.
  #1 : Pre-formatted typing contexts, such as
    \tfont{\Delta};\tfont{\Gamma}
  #2 : A pre-formatted expression
  #3 : A pre-formatted c.i.u. equivalent expression
  #4 : A pre-formatted type for the expressions
```

```latex
\ctxeqvjudg[4]
Formats a contextual equivalence judgment.
  #1 : Pre-formatted typing contexts, such as
    \tfont{\Delta};\tfont{\Gamma}
  #2 : A pre-formatted expression
  #3 : A pre-formatted contextually equivalent expression
  #4 : A pre-formatted type for the expressions
```

### Logical Relations
```latex
\lr[3]
Formats a logical relation set.
  #1 : A formatting macro, such as \tfont
  #2 : A letter for the relation, such a V or E
  #3 : A pre-formatted index for the relation

Usage:
  \newcommand{\srelV}{\lr{\sfont}{V}}
  \newcommand{\trelV}{\lr{\tfont}{V}}
```

```latex
\lrV[2]
\lrE[2]
\lrG[2]
\lrD[2]
\lrK[2]
\lrO[2]
Format logical relation sets.
  #1 : A formatting macro, such as \tfont
  #2 : A pre-formatted index for relation

Usage:
  \newcommand{\srelV}{\lrV{\sfont}}
  \newcommand{\trelV}{\lrV{\tfont}}
```

```latex
\mapext[3]
Extends a key/value map
  #1 : A pre-formatted symbol for the map, such as \tfont{\gamma}
  #2 : A pre-formatted key for the new mapping, such as \tfont{\tx}
  #3 : A pre-formatted symbol for the value of the new mapping such as
    \tfont{\tau}

Usage:
  \newcommand{\btrlrgamma}{\btrfont{\gamma}}
  \newcommand{\btrlrgammaext}{\mapext{\btrlrgamma}}
```

```latex
\binmapext[4]
Extends a map whose value is a pair.
  #1 : A pre-formatted symbol for the map, such as \tfont{\rho}
  #2 : A pre-formatted key for the new mapping, such as \tfont{\alpha}
  #3 : A pre-formatted symbol for the first element of the value such as
    \tfont{\tau}
  #4 : A pre-formatted symbol for the second element of the value

Usage:
  \newcommand{\slrgamma}{\sfont{\gamma}}
  \newcommand{\slrgammaext}{\binmapext{\slrgamma}}
```

```latex
\trimapext[5]
Like \binmapext, but extends a map whose value is a triple.
  #1 : A pre-formatted symbol for the map, such as \tfont{\rho}
  #2 : A pre-formatted key for the new mapping, such as \tfont{\alpha}
  #3 : A pre-formatted symbol for the first element of the value such as
    \tfont{\tau}
  #4 : A pre-formatted symbol for the second element of the value
  #5 : A pre-formatted symbol for the third element of the value

Usage:
  \newcommand{\tlrrho}{\tfont{\rho}}
  \newcommand{\tlrrhoext}{\trimapext{\tlrrho}}
```

```latex
\mapat[2]
Applies a map to a key key.
  #1 : A pre-formatted symbol for the map, as as \tfont{\rho}
  #2 : A pre-formatted symbol for the key
```

```latex
\maponeat[2]
Projects the first element of the value of a map at some key.
  #1 : A pre-formatted symbol for the map, as as \tfont{\rho}
  #2 : A pre-formatted symbol for the key
```

```latex
\maptwoat[2]
Like \maponeat but projects the second element.
```

```latex
\maprelat[2]
Like \maponeat but projects the third element, which is assumed to be a
relation.
```

## Spacing

To define meta-language combinators with consistent spacing, you are
encouraged to liberally use the predefined LaTeX macros `\mathopen`,
`\mathclose`, `\mathbin`, `\mathpunct` that determine character
spacing. For example, our language combinator `\forallty` for
polymorphic quantification ∀α.σ can be defined as follows:

```latex
% Formats a polymorphic type.
%   #1 : A formatting macro for symbols, such as \tfontsym
%   #2 : A formatting macro for text, such as \tfont
%   #3 : The pre-formatted type-variable to bind
%   #4 : The pre-formatted result in which the type-variable is bound
\newcommand{\forallty}[4]{\mathopen{#1{\uplambda}} #3 \mathpunct{#1{.}} #4}
```

In addition, this package defines the macros `\maththinbin` and
`\maththickbin` to use smaller and larger spacing than plain
`\mathbin` around their arguments. `\maththinbin` is used around the
colon of `\fune` (λ(x:σ).e), and `\maththickbin` is used around the
vertical bar separating the two branches of a `\casee` statement (case
e of x₁.e₁ | x₂.e₂).

When defining language expression combinators, it is also common to
use keywords instead of mathematical symbols: `let`, `in`, `if`,
`then`, `else`, `pack`, `unfold`, etc. This package defines macros
similar to the math spacing classes above: `\kwopen`, `\kwopen`,
`\kwbin` and `\kwrel`. Finally, `\kwinfix` can be used for keywords
used as infix operators (`pack`, `unfold`, etc.). See for example the
following definitions:

```latex
% \packe: pack (σ,e) as ∃α.σ
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted type witness.
% #4 : A pre-formatted value witness.
% #5 : A pre-formatted existential type abstracting the witness type.
\newcommand{\packe}[5]{%
  \kwopen{#2{pack}}%
  \paire{#1}{#2}{#3}{#4}%
  \kwbin{#2{as}}%
  #5%
}

% \lete: let x = e in e'
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted expression variable.
% #4 : A pre-formatted expression to bind.
% #5 : A pre-formatted body expression for the let.
\newcommand{\lete}[5]{%
  \kwopen{#2{let}}%
  #3%
  \mathbin{#1{=}}%
  #4%
  \kwbin{#2{in}}%
  #5%
}

% \unfolde: unfold e
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted expression of isorecursive type.
\newcommand{\unfolde}[3]{\kwinfix{#2{unfold}} #3}
```

# SeCCTex
Welcome to the Secure and Correct Compilers Tex package.

This package includes several packages not available on CTAN, and
requires several that are on CTAN. See `secctex.sty` for a complete
list of packages.

This package provides numerous macros for formatting multi-language
meta-theory. This README provides sections describing various aspects of
the package. The first few sections are dedicated to features that are not
specific to multi-language meta-theory.

FYI, I use combinator to mean a macro that takes macros as inputs and defines
new macros, or a macro that can be partially applied to produce a new
macro.

## Table of Contents

* Options
* Automagic Title-case
* TODO and comments
* Reference
* Font shorthand
* Math environments
* Language combinators
* Meta-theory combinators

## Options
This package defines the following options:

* `omit` -- This option causes the `\omitthis` macro to discard its
  argument, enabling passages to exist in the source that are not
  rendered in the output.
* `todo` -- Normally, the `\todo` macro is omitted when the `omit`
  option is specified. This option prevents only `\todo` macros from
  being omitted.
* `nosigplan` disables ACM/SIGPLAN specific features, such as `natbib`
  citation style.
* `techrpt` enables options for formatting a technical appendix, such as
  `\usepackage{fullpage}`
* `paper` disables options for formatting a technical appendix. This
  option is on by default.
* `balance` balances the column on the last page.


## Automagic Title-case
This package redefines the following standard macros. These macros match
the interface of their standard counter-parts, but automatically output
the titles in title-case.
```latex
\title[2][]
\section[2][]
\subsection[2][]
\subsubsection[2][]
```

The original macro are still accessible, though they are @ protected.
```latex
\makeatletter

\@title[2][]
\@section[2][]
\@subsection[2][]
\@subsubsection[2][]

\makeatother
```

You can control which words should be left lower-case the macro
`\Addlcwords`. By default, the following words are added:
```latex
\Addlcwords{for a is but and with of in as the etc on to if}
```

## TODO and comments
This package provides the following macros for adding TODO comments.
```latex
% \todo adds a margin comment, and registers the comment into a todo list.
%
% #1 : Formatting options for the todo macro. See the todonotes package
%   for more information.
% #2 : The todo comment
\todo[2][]

% \todoleft is like \todo, but adds the comment to the left margin.
\todoleft[2][]

% \margincomment is like \todo, but colors the comment in green and does
% not add it to the todolist
\margincomment[2][]

% \inlinecomment is like \margincomment, but places the comment inline
% rather than in the margin.
\inlinecomment[2][]
```

## Reference
This package provides the following macros for referring to sections,
figures, lemmas, and theorems.
```latex
% \secref formats a reference to a section.
%
% #1 : The label for the section to reference.
\secref[1]

% \figref formats a reference to a figure.
%
% #1 : The label for the figure to reference.
\figref[1]

% \lemref formats a reference to a lemma.
%
% #1 : The label for the lemma to reference.
\lemref[1]

% \thmref formats a reference to a theorem.
%
% #1 : The label for the theorem to reference.
\thmref[1]
```

## Font shorthand
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

## Math environments
This package provides the following extra math environments:

### Math paragraph and math display
```latex
% sdisplaymath is like the displaymath environment, but makes
% everything \small
\newenvironment{sdisplaymath}

% fdisplaymath is like the displaymath environment, but makes
% everything \footnotesize
\newenvironment{fdisplaymath}

% smathpar is like mathpar, but makes everything \small
\newenvironment{smathpar}

% fmathpar is like mathpar, but makes everything \footnotesize
\newenvironment{fmathpar}
```

### Align environments
```latex
% alignS is like align, but ignores space after the end of the
% environment
\newenvironment{alignS}

% salignS is like alignS, but but makes everything \small
\newenvironment{salignS}

% falignS is like alignS, but but makes everything \footnotesize
\newenvironment{falignS}
```

### Stack environments
The stack environments format each line by stacking them atop each
other, similar to the array environment with one column.

```latex
% stackCC is a stack environment that center aligns the column
% vertically and horizontially.
\newenvironment{stackCC}

% stackCL is a stack environment that center aligns the column
% vertically and left aligns the column horizontially.
\newenvironment{stackCL}

% stackTL is a stack environment that top aligns the column
% vertically and left aligns the column horizontially.
\newenvironment{stackTL}

% stackTR is a stack environment that top aligns the column
% vertically and right aligns the column horizontially.
\newenvironment{stackTR}

% stackBC is a stack environment that bottom aligns the column
% vertically and center aligns the column horizontially.
\newenvironment{stackBC}

% stackBL is a stack environment that bottom aligns the column
% vertically and left aligns the column horizontially.
\newenvironment{stackBL}
```

### Cases and subcases
This package redefines the `cases` environment, and provides cases and
subcases. This helps format nested proofs.
```latex
\renewenvironment{cases}
\newcommand{\case}[1][]
\newcommand{\scase}[1][]
\newcommand{\sscase}[1][]
```

## Standard source/target macros
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

## Language, meta-theory, and meta-language macros
Best you just look at the `%% Meta Language` section of defs.tex

## Language combinators
This package provides various combinators for generating macros that
format multi-language meta-theory.

### Generating a language
```latex
% \newlanguage generates macros for formatting meta-variables, types,
% and expressions of a language.
%
% #1 : A formatting macro for super-scripts, sub-scripts, and primes in
%   this language, such as \tcolor
% #2 : A formatting macro for math text in this language, such as \tfont
% #3 : A formatting macro for symbols in this language, such as
%   \tfontsym
% #4 : A language prefix for the macros, such as t
% #5 : A list of meta-variables for which to generate macros via
%   \newlmetavars, such as {x, e, v}
% #6 : A list of meta-variables for which to generate macros via
%   \newlmetavarsS, such as {ty/\tau,alpha\alpha}
% #7 : A list of types for which to generate macros via \newltypes, such
%   as {fun, forall, exist, pair, bool, unit}
% #8 : A list of expressions for which to generate macros via
%   \newlexprs, such as {fun, app, if, true, false, unit}
%
% Usage:
%   \newlanguage{\scolor}{\sfont}{\sfontsym}{s}
%   {x,e,v}
%   {alpha/\alpha,ty/\sigma}
%   {fun,bool}
%   {fun,app,if,true,false}
\renewcommand{\newlanguage}[8]
```

### Meta-variables
Writing all the macros to properly format language meta-variables is
obnoxious. So this package provides combinators for meta-variables.
```latex
% \newlmetavar implement the * LaTeX idiom after currying. It expands in
% to either \newlmetavarStar or \newlmetavarNoStar depending on whether the
% character following its 3rd argument is a * or not.
%
% Usage:
%   \newcommand{\newtmetavar}{\newlmetavar{\tfont}{\tcolor}{t}}
%   \newtmetavar{x}
%   \newtmetavar*{ty}{\tau}
\newcommand{\newlmetavar}[4]

% \newlmetavarStar generates some standard macros for formatting a meta-var,
% and takes 5 paraemters:
%
% #1 : A formatting macro for the meta-var, such a \tfont
% #2 : A formatting macro for the subscripts, superscripts, and primes,
%   such as \tcolor
% #3 : A string prefix for the name of the macro, such as t
% #4 : A string name of the macro, such as ty
% #5 : A string to format and display this meta-variable as, such as
%   \tau
%
% Usage:
%   \newlmetavarStar{\tfont}{\tcolor}{t}{ty}{\tau}
%
% This usage generates the following definitions:
%  \newcommand{\ttymetavar}[3]{
%    \lmetvar{\tfont{\tau}}{\tcolor{#1}}{\tcolor{#2}}{\tcolor{\prime}}{#3}
%  }
%  \newcommand{\tty}{ \ttymetavar{}{}{} }
%  \newcommand{\ttyin}[1]{ \ttymetavar{#1}{}{0} }
%  \newcommand{\ttyto}[1]{ \ttymetavar{}{#1}{0} }
%  \newcommand{\ttypr}[1][1]{ \ttymetavar{}{}{#1} }
%  \newcommand{\ttyone}{ \ttymetavar{1}{}{} }
%  \newcommand{\ttyonepr}[1][1]{ \ttymetavar{1}{}{#1}}
%  \newcommand{\ttytwo}{ \ttymetavar{2}{}{} }
%  \newcommand{\ttytwopr}{ \ttymetavar{2}{}{1} }
%  \newcommand{\ttyi}{ \ttymetavar{i}{}{} }
%  \newcommand{\ttyipr}[1][1]{ \ttymetavar{i}{}{#1} }
%  \newcommand{\ttyn}{ \ttymetavar{n}{}{} }
%  \newcommand{\ttynpr}[1][1]{ \ttymetavar{n}{}{#1} }
\newcommand{\newlmetavarStar}[5]

% \newlmetavarNoStar is like \netlmetavarStar, but assumes the name of
% the macro is also the display symbol.
% It takes 4 paraemters:
%
% #1 : A formatting macro for the meta-var, such a \tfont
% #2 : A formatting macro for the subscripts, superscripts, and primes,
%   such as \tcolor
% #3 : A string prefix for the name of the macro, such as t
% #4 : A string name of the macro and symbol to format and display, such
% as x
%
% Usage:
%   \newlmetavarNoStar{\tfont}{\tcolor}{t}{x}
%
% This usage is equivalent to
%   \newlmetavarStar{\tfont}{\tcolor}{t}{x}{x}
\newcommand{\newlmetavarNoStar}[4]

% \lmetavar formats a language meta-var.
%
% #1 : a pre-formatted symbol representing the meta-variable
% #2 : a pre-formatted subscript
% #3 : a pre-formatted superscript
% #4 : a pre-formatted prime symbol
% #5 : a natural number, representing the number of primes
%
% Usage:
%   \newcommand{\txmetavar}[3]{
%     \lmetavar{\tfont{x}}{\tcolor{#1}}{\tcolor{#2}}{\tprime}{#3}
%   }
%   \newcommand{\tx}{\txmetavar{}{}{}}
%   \newcommand{\txone}{\txmetavar{1}{}{}}
%   \newcommand{\txonepr}{\txmetavar{1}{}{1}}
\newcommand{\lmetavar}[5]

% \lmetavarto formats a language meta-var with only a superscript.
%
% #1 : a pre-formatted symbol representing the meta-var
% #2 : a pre-formatted superscript
%
% Usage:
%   \newcommand{\txF}{\lmetavarto{\tx}{f}}
\newcommand{\lmetavarto}[2]

% \lmetavarin formats a language meta-var with only a subscript.
%
% #1 : a pre-formatted symbol representing the meta-var
% #2 : a pre-formatted subscript
%
% Usage:
%   \newcommand{\txone}{\lmetavarto{\tx}{\tcolor{1}}}
\newcommand{\lmetavarin}[2]

% \lmetavarpr formats a language meta-var with only primes, takes 3
% parameters:
%
% #1 : a pre-formatted symbol representing the meta-var
% #2 : a pre-formatted prime symbol
% #3 : a natural number representing the number of primes
%
% Usage:
%   \newcommand{\txpr}{\lmetavarto{\tx}{\prime}{1}}
%   \newcommand{\txdubpr}{\lmetavarto{\tx}{\prime}{2}}
\newcommand{\lmetavarpr}[3]
```

### Lists of meta-variables
Generating meta-variables one at a time is annoying, so this package
provides combinators for lists of meta-variables.

```latex
% \newlmetavar defines new metavar macros for a list of names, assuming
% each metavar will be displayed via the symbol it is named.
% Essentially, it calls \newlmetavar for each name in its 4th parameter.
%
% #1 : A formatting macro for the meta-var, such a \tfont
% #2 : A formatting macro for the subscripts, superscripts, and primes,
%   such as \tcolor
% #3 : A string prefix for the name of the macro, such as t
% #4 : A list of names.
%
% Usage:
%   \newlmetavars{\tfont}{\tcolor}{t}{x,e,v}
%   \newcommand{\newsmetavars}{\newlmetavars{\sfont}{\scolor}{s}}
%   \newsmetavars{x,e,v}
\newcommand{\newlmetavars}[4]

% \newlmetavarS defines new metavar macros for a list of name/symbol
% pairs. Essentially, it calls \newlmetavar* for each name/symbol pair
% in its 4th parameter.
%
% #1 : A formatting macro for the meta-var, such a \tfont
% #2 : A formatting macro for the subscripts, superscripts, and primes,
%   such as \tcolor
% #3 : A string prefix for the name of the macro, such as t
% #4 : A list of name/symbol pairs, separated literally by a /.
%
% Usage:
%   \newlmetavarsS{\tfont}{\tcolor}{t}{x/x,e/e,v/v,alpha/\b{\alpha}}
%   \newcommand{\newsmetavarsS}{\newlmetavarsS{\sfontsym}{\scolor}{s}}
%   \newsmetavarsS{\alpha/\alpha, ty/\sigma}
\newcommand{\newlmetavarsS}[4]
```

### Formatting types and expressions
This package provides combinators for formatting lambda calculus types
and expressions.

Each combinator starts with a tag and ends with a suffix followed by an `S`.
The suffix for type combinators is `ty` and the suffix for expression
combinators is `e`. For instance, the function type combinator is
`\funtyS` and the function expression combinator is `\funeS`.

Each combinator takes a formatting macro for symbols, such as
`\tfontsym`, as its first argument, and a formatting macro for text,
such as `\tfont`, as its second argument. The rest of the arguments
are the sub-types or sub-expressions required for the type or
expression.

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
* pack: pack expressions
* unpack: unpack expressions
* mu: isorecursive types
* fold: fold expression
* unfold: unfold expressions
* unit: the unit type, and the unit expression
* void: the void type
* bool: boolean types
* true: true expressions
* false: false expressions
* if: if expressions
* pair: pair types and pair expressions
* sum: sum types and sum expressions (injections)
* case: case expressions
* let: let expressions

## Meta-theory combinator
This package provides combinators for formatting meta-theory, including
well-formedness and typing judgments, contextual equivalence, context
typing, and logical relations.

### Judgments
```latex
% \wf formats a well-formedness judgment.
%
% #1 : Pre-formatted assumptions, such as \tfont{\Delta}
% #2 : The pre-formatted proposition, such as \tfont{\alpha}
%
% Usage:
%  \wf{\Delta}{\alpha}
%
% Renders like:
% Δ ⊢ α
\newcommand{\wf}[2]

% \judg formats a well-typedness judgment.
%
% #1 : The assumptions, such as \tfont{\Delta};\tfont{\Gamma}
% #2 : The term, such as \tfont{e}
% #3 : The type, such as \tfont{\tau}
%
% Usage:
%  \judg{\Delta;\Gamma}{e}{\tau}
%
% Renders like:
% Δ;Γ ⊢ e : τ
\newcommand{\judg}[3]
```

### Context Typing
```latex
% \ctxtarrowty formats a context typing arrow
%
% #1 : A formatting macro for symbols, such as \stfontsym
% #2 : The type of the hole
% #3 : The type of the result
\newcommand{\ctxtarrowty}[3]

% \ctxtty formats a context type, with different typing contexts for the
% hole and result
%
% #1 : A formatting macro for symbols, such as \stfontsym
% #2 : The typing contexts for the hole
% #3 : The type of the hole
% #4 : The typing contexts for the result
% #5 : The type of the result
\newcommand{\ctxtty}[5]

% \ctxttyjudg formats a context typing judgment.
%
% #1 : A formatting macro for symbols, such as \stfontsym
% #2 : A pre-formatted context
% #3 : The typing contexts for the hole
% #4 : The type of the hole
% #5 : The typing contexts for the result
% #6 : The type of the result
\newcommand{\ctxttyjudg}[6]
```

### Contextual Equivalence
```latex
% \ciueqvjudg formats a c.i.u. equivalence judgment.
%
% #1 : Pre-formatted typing contexts, such as
%   \tfont{\Delta};\tfont{\Gamma}
% #2 : A pre-formatted expression
% #3 : A pre-formatted c.i.u. equivalent expression
% #4 : A pre-formatted type for the expressions
\newcommand{\ciueqvjudg}[4]

% \ctxeqvjudg formats a contextual equivalence judgment.
%
% #1 : Pre-formatted typing contexts, such as
%   \tfont{\Delta};\tfont{\Gamma}
% #2 : A pre-formatted expression
% #3 : A pre-formatted contextually equivalent expression
% #4 : A pre-formatted type for the expressions
\newcommand{\ctxeqvjudg}[4]
```

### Logical Relations
```latex
% \lr formats a logical relation set.
%
% #1 : A formatting macro, such as \tfont
% #2 : A letter for the relation, such a V or E
% #3 : A pre-formatted index for the relation
%
% Usage:
%  \newcommand{\srelV}[1]{\lr{\sfont}{V}{#1}}
%  \newcommand{\trelV}[2]{\lr{\tfont}{V}{#1}{#2}}
\newcommand{\lr}[3]

% \lrV,\lrE,\lrG,\lrD,\lrK,\lrO format logical relation sets.
%
% #1 : A formatting macro, such as \tfont
% #2 : A pre-formatted index for relation
%
% Usage:
%  \newcommand{\srelV}[1]{\lrV{\sfont}{#1}}
%  \newcommand{\trelV}[2]{\lrV{\tfont}{#1}{#2}}
\newcommand{\lrV}[2]
\newcommand{\lrE}[2]
\newcommand{\lrG}[2]
\newcommand{\lrD}[2]
\newcommand{\lrK}[2]
\newcommand{\lrO}[2]

% \binmapext extends a map whose value is a pair.
%
% #1 : A pre-formatted symbol for the map, such as \tfont{\rho}
% #2 : A pre-formatted key for the new mapping, such as \tfont{\alpha}
% #3 : A pre-formatted symbol for the first element of the value such as
%   \tfont{\tau}
% #4 : A pre-formatted symbol for the second element of the value
%
% Usage:
%  \newcommand{\slrgamma}{\sfont{\gamma}}
%  \newcommand{\slrgammaext}{\binmapext{\slrgamma}}
\newcommand{\binmapext}[4]

% \trimapext is like \binmapext, but extends a map whose value is a triple.
%
% #1 : A pre-formatted symbol for the map, such as \tfont{\rho}
% #2 : A pre-formatted key for the new mapping, such as \tfont{\alpha}
% #3 : A pre-formatted symbol for the first element of the value such as
%   \tfont{\tau}
% #4 : A pre-formatted symbol for the second element of the value
% #5 : A pre-formatted symbol for the third element of the value
%
% Usage:
%  \newcommand{\tlrrho}{\tfont{\rho}}
%  \newcommand{\tlrrhoext}{\trimapext{\tlrrho}}
\newcommand{\trimapext}[5]

% \maponeat projects the first element of the value of a map at some
% key.
%
% #1 : A pre-formatted symbol for the map, as as \tfont{\rho}
% #2 : A pre-formatted symbol for the key
\newcommand{\maponeat}[2]

% \maptwoat is like \maponeat but projects the second element.
% The interface is the same
\newcommand{\maptwoat}[2]

% \maprelat is like \maponeat but projects the third element, which is
% assumed to be a relation.
\newcommand{\maprelat}[2]
```

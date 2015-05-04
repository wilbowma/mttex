# SeCCTex
Welcome to the Secure and Correct Compilers Tex package.

This package includes several packages not available on CTAN, and
requires several that are on CTAN. See `secctex.sty` for a complete
list of packages.

This package provides numerous macros for formatting multi-language
meta-theory. This README provides sections describing various aspects of
the package.

In this README, I use "combinator" to mean a macro that takes macros as
inputs and defines new macros, or a macro that can be partially applied
to produce a new macro.

## Table of Contents

* [Options](#options)
* [How to Read](#how-to-read)
* [Automagic Title-case](#automagic-title-case)
* [TODO and Comments](#todo-and-comments)
* [Label References](#label-references)
* [Font Shorthand](#font-shorthand)
* [Math Environments](#math-environments)
* [Standard Source/Target Macros](#standard-source-target-macros)
* [Meta-Language Macros](#meta-language-macros)
* [Language Symbol Macros](#language-symbol-macros)
* [Language Combinators](#language-combinators)
* [Meta-Theory Combinators](#meta-theory-combinators)

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

## How to Read
Until I get around to make the documentation more readable, use this
guide to translate.

Each documented macro is preceded by documentation that explains the
purpose of the macro and each of its arguments. The arguments are
numbered in the same way they are used in LaTeX. Below the documentation
the macro is show with its interface, i.e., the number of arguments, and
the default value of the optional argument (if any).

Macros may be undocumented but given with their interface or their
definitions if they merely provide shorthand or match a standard
interface.

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

## TODO and Comments
This package provides the following macros for adding TODO comments.
```latex
% \omitthis does not render its argument if the omit option is
% specified.
%
% #1 : A comment to potentially omit.
\omitthis[1]

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

## Label References
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

## Math Environments
This package provides the following extra math environments:

### Math Paragraph and Math Display
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

### Align Environments
```latex
% alignS is like align, but ignores space after the end of the
% environment
\newenvironment{alignS}

% salignS is like alignS, but but makes everything \small
\newenvironment{salignS}

% falignS is like alignS, but but makes everything \footnotesize
\newenvironment{falignS}
```

### Stack Environments
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
\newcommand{\bump}{\hspace{3.5pt}}
\newcommand{\fresh}[1]{(\mit{fresh}\:#1)}
\newcommand{\where}[1]{\mrm{where}\:#1}

\newcommand{\lang}[1]{\mrm{\trm{#1}}}
```

## Language Symbol Macros
```latex
\newcommand{\empctx}{\cdot}
\newcommand{\hole}{[\cdot]}
\newcommand{\hw}[1]{\lbrack{#1}\rbrack}
\newcommand{\ectxt}{E}
\newcommand{\ctxt}{C}

\newcommand{\hooklongrightarrow}{\lhook\joinrel\longrightarrow}
\newcommand{\redexstep}{\hookrightarrow}

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

### Generating a Language
This package provides a single combinator for generating all the macros
for type-setting meta-variables, types, and expressions. While this is
probably the macro you want to use, you will need to understand the
macros it composes to understand the macros it generates. They are
explained below.
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
%   \newmetavars, such as {x, e, v}
% #6 : A list of meta-variables for which to generate macros via
%   \newmetavarsS, such as {ty/\tau,alpha\alpha}
% #7 : A list of types for which to generate macros via \newtypes, such
%   as {fun, forall, exist, pair, bool, unit}
% #8 : A list of expressions for which to generate macros via
%   \newexprs, such as {fun, app, if, true, false, unit}
%
% Usage:
%   \newlanguage{\scolor}{\sfont}{\sfontsym}{s}
%   {x,e,v}
%   {alpha/\alpha,ty/\sigma}
%   {fun,bool}
%   {fun,app,if,true,false}
\newlanguage[8]
```

### Meta-Variables
Writing all the macros to properly format language meta-variables is
obnoxious. So this package provides combinators for meta-variables.
```latex
% \newmetavar implement the * LaTeX idiom after currying. It expands in
% to either \newmetavarStar or \newmetavarNoStar depending on whether the
% character following its 3rd argument is a * or not.
%
% Usage:
%   \newcommand{\newtmetavar}{\newmetavar{\tfont}{\tcolor}{t}}
%   \newtmetavar{x}
%   \newtmetavar*{ty}{\tau}
\newmetavar[4]

% \newmetavarStar generates some standard macros for formatting a meta-var,
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
%   \newmetavarStar{\tfont}{\tcolor}{t}{ty}{\tau}
%
% This usage generates the following definitions:
%
%   \newcommand{\ttymetavar}[3]{
%      \metavar{\tfont{\tau}}{\tcolor{#1}}{\tcolor{#2}}{\tcolor{\prime}}{#3}
%    }
%
%   \newcommand{\tty}{ \ttymetavar{}{}{} }
%   \newcommand{\ttyin}[1]{ \ttymetavar{#1}{}{0} }
%   \newcommand{\ttyto}[1]{ \ttymetavar{}{#1}{0} }
%   \newcommand{\ttypr}[1][1]{ \ttymetavar{}{}{#1} }
%   \newcommand{\ttyone}{ \ttymetavar{1}{}{} }
%   \newcommand{\ttyonepr}[1][1]{ \ttymetavar{1}{}{#1}}
%   \newcommand{\ttytwo}{ \ttymetavar{2}{}{} }
%   \newcommand{\ttytwopr}{ \ttymetavar{2}{}{1} }
%   \newcommand{\ttyi}{ \ttymetavar{i}{}{} }
%   \newcommand{\ttyipr}[1][1]{ \ttymetavar{i}{}{#1} }
%   \newcommand{\ttyn}{ \ttymetavar{n}{}{} }
%   \newcommand{\ttynpr}[1][1]{ \ttymetavar{n}{}{#1} }
%
%   \ttymetavar takes an unformatted sub-script, super-script, and
%   a natural number n indicating the number of primes. It then formats
%   the sub-script, the super-script, and n primes and attaches them to
%   the formatted meta-variable.
%
\newmetavarStar[5]

% \newmetavarNoStar is like \netmetavarStar, but assumes the name of
% the macro is also the display symbol.
% It takes 4 paraemters:
%
% #1 : A formatting macro for the meta-var, such a \tfont
% #2 : A formatting macro for the subscripts, superscripts, and primes,
%   such as \tcolor
% #3 : A string prefix for the name of the macro, such as t
% #4 : A string name of the macro and symbol to format and display, such
%   as x
%
% Usage:
%   \newmetavarNoStar{\tfont}{\tcolor}{t}{x}
%
% This usage is equivalent to
%   \newmetavarStar{\tfont}{\tcolor}{t}{x}{x}
\newmetavarNoStar[4]

% \metavar formats a language meta-var.
%
% #1 : a pre-formatted symbol representing the meta-variable
% #2 : a pre-formatted subscript
% #3 : a pre-formatted superscript
% #4 : a pre-formatted prime symbol
% #5 : a natural number, representing the number of primes
%
% Usage:
%   \newcommand{\txmetavar}[3]{
%     \metavar{\tfont{x}}{\tcolor{#1}}{\tcolor{#2}}{\tprime}{#3}
%   }
%   \newcommand{\tx}{\txmetavar{}{}{}}
%   \newcommand{\txone}{\txmetavar{1}{}{}}
%   \newcommand{\txonepr}{\txmetavar{1}{}{1}}
\metavar[5]

% \metavarto formats a language meta-var with only a superscript.
%
% #1 : a pre-formatted symbol representing the meta-var
% #2 : a pre-formatted superscript
%
% Usage:
%   \newcommand{\txF}{\metavarto{\tx}{f}}
\metavarto[2]

% \metavarin formats a language meta-var with only a subscript.
%
% #1 : a pre-formatted symbol representing the meta-var
% #2 : a pre-formatted subscript
%
% Usage:
%   \newcommand{\txone}{\metavarto{\tx}{\tcolor{1}}}
\metavarin[2]

% \metavarpr formats a language meta-var with only primes, takes 3
% parameters:
%
% #1 : a pre-formatted symbol representing the meta-var
% #2 : a pre-formatted prime symbol
% #3 : a natural number representing the number of primes
%
% Usage:
%   \newcommand{\txpr}{\metavarto{\tx}{\prime}{1}}
%   \newcommand{\txdubpr}{\metavarto{\tx}{\prime}{2}}
\metavarpr[3]
```

### List of Meta-Variables Combinators
Generating meta-variables one at a time is annoying, so this package
provides combinators for lists of meta-variables.

```latex
% \newmetavar defines new metavar macros for a list of names, assuming
% each metavar will be displayed via the symbol it is named.
% Essentially, it calls \newmetavar for each name in its 4th parameter.
%
% #1 : A formatting macro for the meta-var, such a \tfont
% #2 : A formatting macro for the subscripts, superscripts, and primes,
%   such as \tcolor
% #3 : A string prefix for the name of the macro, such as t
% #4 : A list of names.
%
% Usage:
%   \newmetavars{\tfont}{\tcolor}{t}{x,e,v}
%   \newcommand{\newsmetavars}{\newmetavars{\sfont}{\scolor}{s}}
%   \newsmetavars{x,e,v}
\newmetavars[4]

% \newmetavarS defines new metavar macros for a list of name/symbol
% pairs. Essentially, it calls \newmetavar* for each name/symbol pair
% in its 4th parameter.
%
% #1 : A formatting macro for the meta-var, such a \tfont
% #2 : A formatting macro for the subscripts, superscripts, and primes,
%   such as \tcolor
% #3 : A string prefix for the name of the macro, such as t
% #4 : A list of name/symbol pairs, separated literally by a /.
%
% Usage:
%   \newmetavarsS{\tfont}{\tcolor}{t}{x/x,e/e,v/v,alpha/\b{\alpha}}
%   \newcommand{\newsmetavarsS}{\newmetavarsS{\sfontsym}{\scolor}{s}}
%   \newsmetavarsS{\alpha/\alpha, ty/\sigma}
\newmetavarsS[4]
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
* prj: projection from a pair
* sum: sum types and sum expressions (injections)
* case: case expressions
* let: let expressions

### List of Types Combinator
Generating type macros one at a time is annoying, so this package
provides combinators for lists of types. The macros are generated
attaching a prefix and suffix to the tag, followed by ty.  For instance,
the macro generate for `fun` when using the prefix `s` and suffix `ty`
is `\sfunty`.
```latex
% \newtypes generates type formatting macros given a list of tags.
%
% #1 : A formatting macro for symbols, such as \tfontsym
% #2 : A formatting macro for text, such as \tfont
% #3 : A prefix for the name of each macro, such as t
% #4 : A suffix for the name of each macro, such as ty
% #5 : A list of type tags, such as {fun,bool,void,unit}
\newtypes[5]
```

### Lists of Expressions Combinator
Generating expression macros one at a time is annoying, so this package
provides combinators for lists of expressions. The macros are generated
attaching a prefix and suffice to the tag. For instance, the macro
generate for `fun` when using the prefix `s` and suffix `e` is `\sfune`.
```latex
% \newexprs generates type formatting macros given a list of tags.
%
% #1 : A formatting macro for symbols, such as \sfontsym
% #2 : A formatting macro for text, such as \sfont
% #3 : A prefix for the name of each macro, such as s
% #4 : A suffix for the name of each macro, such as e
% #5 : A list of type tags, such as {fun,bool,void,unit}
\newexprs[5]
```

#### Detailed Type Combinator Documentation
```latex
% \funty formats a function type.
%
% #1 : A formatting macro for symbols, such as \tfontsym
% #2 : A formatting macro for text, such as \tfont
% #3 : The pre-formatted argument to the function
% #4 : The pre-formatted result of the function
\funty[4]

% \polyfunty formats a polymorphic function type.
%
% #1 : A formatting macro for symbols, such as \tfontsym
% #2 : A formatting macro for text, such as \tfont
% #3 : The pre-formatted type-variable to bind
% #4 : The pre-formatted argument to the function
% #5 : The pre-formatted result of the function
\polyfunty[5]

% \forallty formats a polymorphic type.
%
% #1 : A formatting macro for symbols, such as \tfontsym
% #2 : A formatting macro for text, such as \tfont
% #3 : The pre-formatted type-variable to bind
% #4 : The pre-formatted result in which the type-variable is bound
\forallty[4]

% \existty formats an existential type.
%
% #1 : A formatting macro for symbols, such as \tfontsym
% #2 : A formatting macro for text, such as \tfont
% #3 : The pre-formatted type-variable to bind
% #4 : The pre-formatted result in which the type-variable is bound
\existty[4]

% \muty formats a recursive type.
%
% #1 : A formatting macro for symbols, such as \tfontsym
% #2 : A formatting macro for text, such as \tfont
% #3 : The pre-formatted type-variable to bind
% #4 : The pre-formatted result in which the type-variable is bound
\muty[4]

% \unitty formats a unit type.
%
% #1 : A formatting macro for symbols, such as \tfontsym
% #2 : A formatting macro for text, such as \tfont
\unitty[2]

% \voidty formats a void type.
%
% #1 : A formatting macro for symbols, such as \tfontsym
% #2 : A formatting macro for text, such as \tfont
\voidty[2]

% \boolty formats a bool type.
%
% #1 : A formatting macro for symbols, such as \tfontsym
% #2 : A formatting macro for text, such as \tfont
\boolty[2]

% \pairty formats a pair type.
%
% #1 : A formatting macro for symbols, such as \tfontsym
% #2 : A formatting macro for text, such as \tfont
% #3 : The pre-formatted type for the first component of the pair
% #4 : The pre-formatted type for the second component of the pair
\pairty[4]

% \sumty formats a sum type.
%
% #1 : A formatting macro for symbols, such as \tfontsym
% #2 : A formatting macro for text, such as \tfont
% #3 : The pre-formatted type for the first component of the sum
% #4 : The pre-formatted type for the second component of the sum
\sumty[4]
```

#### Detailed Type Combinator Documentation
```latex
% \fune formats a function expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : The pre-formatted variable the function binds.
% #4 : The pre-formatted type of the variable.
% #5 : The pre-formatted body of the function.
\fune[5]

% \polyfune formats a polymorphic function expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : The pre-formatted type variable the function binds.
% #4 : The pre-formatted variable the function binds.
% #5 : The pre-formatted type of the variable.
% #6 : The pre-formatted body of the function.
\polyfune[6]

% \abstre formats an polymorphic abstraction expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : The pre-formatted type variable the abstraction binds.
% #4 : The pre-formatted the body of the abstract.
\abstre[4]

% \inste formats an instantiation expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : The pre-formatted polymorphic abstraction to instantiate.
% #4 : The pre-formatted type with which to instantiate the abstraction.
\inste[4]

% \appe formats an application expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : The pre-formatted function.
% #4 : The pre-formatted argument.
\appe[4]

% \pappe formats a polymorphic function application expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted polymorphic function expression.
% #4 : A pre-formatted type with which to instantiate.
% #5 : A pre-formatted argument to the function.
\pappe[5]

% \ife formats an if expression 
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted discriminant expression.
% #4 : A pre-formatted consequent expression.
% #5 : A pre-formatted alternate expression.
\ife[5]

% \packe formats a pack expression
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted type witness.
% #4 : A pre-formatted value witness.
% #5 : A pre-formatted existential type abstracting the witness type.
\packe[5]

% \unpacke formats an unpack expression
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted type variable.
% #4 : A pre-formatted expression variable.
% #5 : A pre-formatted existential witness expression.
% #6 : A pre-formatted expression in which to bind the existential.
\unpacke[6]

% \lete formats a let expression
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted expression variable.
% #4 : A pre-formatted expression to bind.
% #5 : A pre-formatted body expression for the let.
\lete[5]

% \folde formats a fold expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted mu type.
% #4 : A pre-formatted expression of isorecursive type.
\folde[4]

% \unfolde formats an unfold expression
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted expression of isorecursive type.
\unfolde[3]

% \unite formats a unit expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
\unite[2]

% \truee formats a true expression
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
\truee[2]

% \falsee formats a false expression
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
\falsee[2]

% \paire formats a pair expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted expression for the first component of the pair.
% #4 : A pre-formatted expression for the second component of the pair.
\paire[4]

% \prje formats a projection expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : An unformatted natural number, either 1 or 2, indicating which
%   component of the pair to project.
% #4 : A pre-formatted pair expression to project.
\prje[4]

% \sume formats a sum expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : An unformatted natural number, either 1 or 2, indicating into which
%   side of the sum to inject the expression. 1 indicates left, 2
% #4 : A pre-formatted expression to inject into a sum.
\sume[4]

% \casee formats a case expression.
%
% #1 : A formatting macro for symbols, such as \tfontsym.
% #2 : A formatting macro for text, such as \tfont.
% #3 : A pre-formatted discriminant expression.
% #4 : A pre-formatted variable to bind in the left branch.
% #5 : A pre-formatted expression for the left branch.
% #6 : A pre-formatted variable to bind in the right branch.
% #7 : A pre-formatted expression for the right branch.
\casee[7]
```

## Meta-Theory Combinators
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
\wf[2]

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
\judg[3]
```

### Context Typing
```latex
% \ctxtarrowty formats a context typing arrow
%
% #1 : A formatting macro for symbols, such as \stfontsym
% #2 : The type of the hole
% #3 : The type of the result
\ctxtarrowty[3]

% \ctxtty formats a context type, with different typing contexts for the
% hole and result
%
% #1 : A formatting macro for symbols, such as \stfontsym
% #2 : The typing contexts for the hole
% #3 : The type of the hole
% #4 : The typing contexts for the result
% #5 : The type of the result
\ctxtty[5]

% \ctxttyjudg formats a context typing judgment.
%
% #1 : A formatting macro for symbols, such as \stfontsym
% #2 : A pre-formatted context
% #3 : The typing contexts for the hole
% #4 : The type of the hole
% #5 : The typing contexts for the result
% #6 : The type of the result
\ctxttyjudg[6]
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
\ciueqvjudg[4]

% \ctxeqvjudg formats a contextual equivalence judgment.
%
% #1 : Pre-formatted typing contexts, such as
%   \tfont{\Delta};\tfont{\Gamma}
% #2 : A pre-formatted expression
% #3 : A pre-formatted contextually equivalent expression
% #4 : A pre-formatted type for the expressions
\ctxeqvjudg[4]
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
%  \newcommand{\srelV}{\lr{\sfont}{V}}
%  \newcommand{\trelV}{\lr{\tfont}{V}}
\lr[3]

% \lrV,\lrE,\lrG,\lrD,\lrK,\lrO format logical relation sets.
%
% #1 : A formatting macro, such as \tfont
% #2 : A pre-formatted index for relation
%
% Usage:
%  \newcommand{\srelV}{\lrV{\sfont}}
%  \newcommand{\trelV}{\lrV{\tfont}}
\lrV[2]
\lrE[2]
\lrG[2]
\lrD[2]
\lrK[2]
\lrO[2]

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
\binmapext[4]

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
\trimapext[5]

% \maponeat projects the first element of the value of a map at some
% key.
%
% #1 : A pre-formatted symbol for the map, as as \tfont{\rho}
% #2 : A pre-formatted symbol for the key
\maponeat[2]

% \maptwoat is like \maponeat but projects the second element.
% The interface is the same
\maptwoat[2]

% \maprelat is like \maponeat but projects the third element, which is
% assumed to be a relation.
\maprelat[2]
```

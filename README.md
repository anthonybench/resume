# <img alt="LaTeX logo" src="https://i.imgur.com/FojJMiQ.png" width="180" style="padding-right:10px" /> <img alt="LaTeX logo" src="https://i.imgur.com/nxrayFX.png" width="40" style="padding-bottom:15px" /> <img alt="LaTeX logo" src="https://i.imgur.com/vNEW7vO.png" width="100" />
*My personally written guide for typesetting LaTeX documents in Overleaf.*

You can view my resume [here](https://sleepyblog.org/about) 😊

<br />

## **Table of Contents**

*Getting Started*
> - [LaTeX Document Anatomy](#latex-document-anatomy)
> - [Overleaf](#overleaf)
> - [Basic Syntax](#basic-syntax)

*Preamble*
> - [Document Class](#document-class)
> - [Importing Packages](#importing-packages)
> - [Typefaces](#typefaces)
> - [Title](#title)
> - [User Defined Commands](#user-defined-commands)

*Body*
> - [Title Set](#title-set)
> - [Formatting](#formatting)
> - [Sections](#sections)
> - [Equations](#equations)
> - [Images](#images)
> - [Code Snippets](#code-snippets)

*Further Development*
> - [Classes and Packages](#classes-and-packages)
> - [Tikz](#tikz)

[References](#references)

<br />

## **Getting Started**
<hr>

## LaTeX Document Anatomy
*LaTeX* is a set of macros for the typesetting language *TeX*. A *TeX* document is ultimately made of two parts, the `preamble` and the `body`. The *preamble* is where the document layout and user definitions are declared, followed by the *body* defined between `\begin{document}` and `\end{document}`, providing the document's content. The first part of this doc explains the *preamble* fundamentals, while the second explains the *body* fundamentals.

## Overleaf
*LaTeX* is interpreted into document file format, commonly pdf, by a *LaTeX Engine*. While there are several engines you can set up for local development, there is no obvious benefit to doing so as long as you have internet access. [*OverLeaf*](https://www.overleaf.com/) is an online *LaTeX* editor that can organize and develop a large number of projects for free, lets you switch between engines, and gives you access to a massive community template library all with cloud convenience.

## Basic Syntax
*LaTeX* has somewhat confusing nomenclature when it comes to commands, so forgive yourself if this paragraph is confusing to read at first. There are 2 categories of "commands" that are effectively macros, special words prepended by a `\` character that '*do something*'. The first is called a **command** (which confuses most), which can be thought of as function, accepting *input* and possibly *options* in a single declaration. The second is called an **environment**, which sets some typesetting condition either after the declaration, or between `\begin{something}` and `\end{something}` declarations. We will look at the first below, and explore the latter shortly after. **Please note**; this doc refers to both "command types" as commands. This distinction is only explained here to aid in further reading, which is unavoidable for even moderate *LaTeX* development.

**Commands** generally take the following form:
```latex
\exampleCommand[option1, option2, ...]{Input Text}
```
With some command input, **units** may be required after the number. The common units are `in`, `cm`, `mm` such as the following example:
```latex
\usepackage[margin=1.25in]{geometry}
```

To **Import packages**, use the `\usepackage` command in the preamble:
```latex
\usepackage{examplePackage}
```

**Single line comments** are prepended by `%`:
```latex
% this is a comment
```
**Multi-line comments** are not supported natively, however there is a popular package **verbatim**:
```latex
\usepackage{verbatim}
\begin{comment}
these are
all
comments
\end{comment}
```

**Escaping special characters** works as follows:
| Result | Input |
| --- | --- |
| `#` | `\#` |
| `$` | `\$` |
| `%` | `\%` |
| `&` | `\&` |
| `\` | `\textbackslash{}` |
| `^` | `\textasciicircum{}` |
| `_` | `\_` |
| `{` | `\{` |
| `}` | `\}` |
| `~` | `\textasciitilde{}` |

<br />

## **Preamble**
<hr>

## Document Class
Below are the essentials. [Here's a terrific guide](https://texblog.org/2013/02/13/latex-documentclass-options-illustrated/#multiplecol) for the `\documentclass` command.\
All documents begin with `\documentclass[options]{type}`.\

Common **types**:
> `article` - most default document type, for short reports and program documentation.\
> `minimal` - sets only page size and base font.\
> `report` - for long reports and more significant thesis-esque documents.\
> `slides` - aptly named, base font is large sans-serif.\
> `beamer` - for presentations.\
> `letter` - aptly named, big margins.\
> `book` - aptly named, sets separate title page.

Common **options**:\
Enclosed in `{ }` will be a set of common values for the given option.
> *Font size* - { 10pt, 11pt, 12pt }\
> *Paper* - { a4paper, letterpaper, legalpaper, executivepaper }\
> *Orientation* - { landscape, portrait }\
> *Page printing* - { oneside, twoside }\
> *Title behavior* - { notitlepage, titlepage }\
> *Columns* - { onecolumn, twocolumn }\
> *Formula layout* - { fleqn, leqno }

A note on 'formula layout', `fleqn` means "*flush left equations*", and `leqno` means "*left equation numbers*".

An **example** of a document class I use for school reports:
```latex
\documentclass[12pt,letterpaper,twoside,titlepage,fleqn]{article}
```

## Importing Packages
After your document class is configured, it is customary to import your packages with the `\usepackage` command. Here are **some common packages I use**:
```latex
\usepackage[utf8]{inputenc} % unicode support
\usepackage{verbatim} % multi-line comments
\usepackage[margin=0.75in]{geometry} % margin setting
\usepackage[T1]{fontenc} % access native typefaces
\usepackage{fontspec} % access imported typefaces || pdfLaTeX Only!
\usepackage[rm,light]{roboto} % set main typeface
\usepackage{amsmath} % equation setting
\usepackage{amssymb} % math symbols
\usepackage{ragged2e} % text alignment
\usepackage[normalem]{ulem} % text styling
\usepackage{indentfirst} % force subsection first paragraph indent
\usepackage{hyperref} % nice hyperlinks, formatted by the following
\hypersetup{
    colorlinks=true,
    linkcolor=blue,
    urlcolor=magenta,
}
\usepackage{xcolor} % for defining colors, one example below
\definecolor{codepurple}{rgb}{0.58,0,0.82}
\usepackage{listings} % formatting code snippets, configured with the following
\lstdefinestyle{mystyle}{
    backgroundcolor=\color{{rgb}{0.95,0.95,0.92}},   
    commentstyle=\color{{rgb}{0,0.6,0}},
    keywordstyle=\color{magenta},
    numberstyle=\tiny\color{{rgb}{0.5,0.5,0.5}},
    stringstyle=\color{{rgb}{0.58,0,0.82}},
    basicstyle=\ttfamily\footnotesize,
    breakatwhitespace=false,         
    breaklines=true,                 
    captionpos=b,                    
    keepspaces=true,                 
    numbers=left,                    
    numbersep=5pt,                  
    showspaces=false,                
    showstringspaces=false,
    showtabs=false,                  
    tabsize=2
}
```

## Typefaces
There are many typefaces supported by *LaTeX* in *Overleaf*, and the complete catalogue is listed in the references at the bottom of this doc (*and [here](https://tug.org/FontCatalogue/) for convenience*). To set a typeface from the native catalogue, include the following packages:
```latex
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}

\usepackage[rm,light]{roboto} % this one sets the new main typeface.
```
The package that sets the main typeface can be chosen to your liking.\
To **import fonts**, you must change the compiler from your **menu** in the editor view of a given project in *Overleaf* to **XeLaTeX**. By default, it will be **pdfLaTeX**. From there, you can add the font file to your project's file tree, and set it like the following:
```latex
\usepackage[utf8]{inputenc}
\usepackage{fontspec}
\setmainfont[Ligatures=TeX]{OleoScript-Regular.ttf}
```

## Title
Next, you can use a few commands to set the document's **title**:
```latex
\title{Example Document}
\author{Sleepy Boy \thanks{The Computer Action Team}}
\date{December 18th, 2020}
```
This will get set later at the top of the *body*. The `\thanks{}` command nested in the `\author{}` command will add the input text as a foot note to the first page. If you do not write your own `\date{}` declaration, a default one will be set for you with the format `<month_name> <day_number>, <year>`.

## User Defined Commands
You may define your own commands with the `\newcommand` command. This feature is too dense of a topic to explain here, if this doc is to stay succinct. Thus, an example of a simple common use case is given here, and references for further reading are provided at the bottom:
```latex
\newcommand{\plusbinomial}[3][2]{(#2 + #3)^#1} % definition in preamble
\[ \plusbinomial[4]{y}{y} \] % setting declarations in body
\[ \plusbinomial{x}{y} \] % this declaration will rely on a default value
```
In this example, the definition works as follows:
- The first parameter `[3]` is the number of inputs for the command.
- The next parameter `[2]` is the default value for the first input. You can keep providing default values this way. When you do, that input becomes optional when setting declarations in the body.
- For the expression wrapped in `{ }`, `#1` is the first argument provided, and so on.

<br />

## **Body**
<hr>

## Title Set
The body should begin with the following line, setting the title you configured in the preamble:
```latex
\maketitle
```
Again, note that this will set a footnote if the title configuration in the preamble contained a `\thanks{}` declaration.

## Formatting
**Statements containing symbols** should be wrapped with the `$`. Overleaf will do this for you if it thinks you forgot to, then flags a warning:
```latex
$\theta$
```
To **declare a new line**, append the line with `\\`:
```latex
Hello World\\
```
To **declare a size of vertical whitespace**:
```latex
\vspace{10mm}
```
For setting justification for a block of text, use `center`, `flushleft` and `flushright` in the following command:
```latex
\begin{center}
I'm centered!
\end{center}
```
There is also a popular package **ragged2e** that manages alignment in a lighter syntax:
```latex
\usepackage{ragged2e}
\begin{document}
\centering
I'm centered!
\FlushRight
I'm right-justified!
\FlushLeft
I'm back to default justification!
\end{document}
```
For typical **type-face styling**:
```latex
\textit{Italic}
\textbf{Bold}
\underline{Underline}
\sout{Strike-through} % \usepackage[normalem]{ulem} 
```
To set environments with a **shifted font size**:
```latex
\Huge Huge
\huge huge
\LARGE LARGE
\Large Large
\large large
\normalsize normalsize
\small small
\footnotesize footnotesize
\scriptsize sciprtsize
\tiny tiny
```
For **hyperlinks**, you can make use of the **hyperref** package and configure your link colors with the `\hypersetup{<config>}` command, demonstrated in the [packages](#importing-packages) section of this doc. You may then declare a hyperlink in the body with the `url{<address>}` command. Example:
```latex
\url{[LinkedIn](https://www.linkedin.com/in/anthonybench/)}
```
## Sections
To make a **new section**:
```latex
\section{Numbered Section Title}
\section*{Section Title} % the * character removes numbering
```
and to make a **new subsection**:
```latex
\subsection{Numbered Subsection Title}
\subsection*{Subsection Title} % the * character removes numbering
```
**Paragraphs** are bodies of text seperated by blank lines, and the first paragraphs of sections/subsections are not indented by default. To **enforce the first paragraph to indent**, include `\usepackage{indentfirst}` in the preamble. To **force no indent** at a paragraphs onset, prepend the paragraph with the `\noindent` command.

## Equations
There are two ways to enclose text to declare an equation; `\[ \]` for **display mode** and `\( \)` for **inline mode**.\
**Superscripts** get prepended by `^`, while **superscripts** pet prepended by `_`.\
**Fractions** are formatted with the `\frac{}{}` command.\\
An example of a *display mode* equation:
```latex
\[ m_1gh = \frac{m_1v^2}{2} \]
```

## Images
The `\usepackage` command from the **graphicx** package inserts images into the document where ever declared:
```latex
\usepackage{graphicx}
\begin{document}
\includegraphics[scale=<n>]{<path>}
\end{document}
```
where `<n>` is a floating point number that represents percent scale of the source image. It is recommended to take use of *Overleaf*'s file system for each project, thus image hosting is not necessary. The `<path>` is the relative path from the document's file. An **example** is given below:
```latex
\includegraphics[scale=1.5]{img/app.yaml.png}
```
You can caption an image with the `\caption{<caption text>}` command within the *figure* environment, demonstrated here:
```latex
\begin{figure}
    \includegraphics[width=\textwidth]{sleepyboy.png}
    \caption{The sleepiest boy}
\end{figure}
```

## Code Snippets
With the **listings** package, you can wrap a block of text intended to be a code snippet with `\begin{lstlisting}` and `\end{lstlisting}`. Something uncommon about this utility is that options `[ ]` come *after* the command input. For example, one option is to specify the language so that the package knows to style keywords, and would be declared as follows:
```latex
\begin{lstlisting}[language=Python]
from math import factorial as F
def weightedCombinationSum(n, weight):
    res = 0
    for i in range(n+1):
        res += (F(n) // (F(i) * F(n - i))) * (weight**i)
    return res
\end{lstlisting}
```
But let's not pretend that colorless code snippets are cool. They aren't.

This package offers *a lot* of configuration options, but first we need another package to write maintainable code when we manage colors, **xcolor**. With this package, we can define in the preamble with the `\definecolor{<color_name>}{rgb}{<x>,<y>,<z>}` command. The `<color_name>` input is the handle for the custom color, `<x>,<y>,<z>` are the floating point rgb values defining the color. An example:
```latex
\definecolor{codepurple}{rgb}{0.58,0,0.82}
```

You don't per-say *need* the above package, but it makes for much more maintanable code and is suggested by the *TeX* community at large. After your colors are defined, we can configure a code snippet style with the `\lstdefinestyle{<style_name>}{<config_settings>}` command. The first input `<style_name>` is for the name you are associating the following style options with. The second input `<config_settings>` is where you write your configurations. This should be done in the preamble. An example is given here with all of the configuration options:
```latex
\lstdefinestyle{mystyle}{
    backgroundcolor=\color{backcolour},   
    commentstyle=\color{codegreen},
    keywordstyle=\color{magenta},
    numberstyle=\tiny\color{codegray},
    stringstyle=\color{codepurple},
    basicstyle=\ttfamily\footnotesize,
    breakatwhitespace=false,         
    breaklines=true,                 
    captionpos=b,                    
    keepspaces=true,                 
    numbers=left,                    
    numbersep=5pt,                  
    showspaces=false,                
    showstringspaces=false,
    showtabs=false,                  
    tabsize=2
}
```
Finally, you can set a style configuration by declaring its name in the body with the `\lstset{style=<style_name>}` command. Here's an example of all of this in motion:
```latex
% preamble %
\usepackage{xcolor} % define colors
\definecolor{codegreen}{rgb}{0,0.6,0}
\definecolor{codegray}{rgb}{0.5,0.5,0.5}
\definecolor{codepurple}{rgb}{0.58,0,0.82}
\definecolor{backcolour}{rgb}{0.95,0.95,0.92}

\usepackage{listings} % configure code snippet style
\lstdefinestyle{mystyle}{
    backgroundcolor=\color{backcolour},   
    commentstyle=\color{codegreen},
    keywordstyle=\color{magenta},
    numberstyle=\tiny\color{codegray},
    stringstyle=\color{codepurple},
    basicstyle=\ttfamily\footnotesize,
    breakatwhitespace=false,         
    breaklines=true,                 
    captionpos=b,                    
    keepspaces=true,                 
    numbers=left,                    
    numbersep=5pt,                  
    showspaces=false,                
    showstringspaces=false,
    showtabs=false,                  
    tabsize=2
}

% body %
\begin{document}

\lstset{style=myStyle} % declare style
\begin{lstlisting}[language=Python] % set code snippet
from math import factorial as F
def weightedCombinationSum(n, weight):
    res = 0
    for i in range(n+1):
        res += (F(n) // (F(i) * F(n - i))) * (weight**i)
    return res
\end{lstlisting}

\end{document}
```

<br />

## **Further Development**
<hr>

## Classes and Packages
For modularity, elements you define can be separated into files for repeated use. Such a file is refered to as either a *class* with the `.cls` extension or a *package* with the `.sty` extension. The rule of thumb is to make your code a *class* if it's specific to a document type, like if it's meant for just school reports for example. Else if it's intended to add functionality to any arbitrary document type, then it should be a *package*.

## TikZ
One package that likely deserves it's own document is **TikZ**, which provides a litany of powerful graphical tools for setting shape, images and other graphical flair. This package is quite complex, but time spent learning it can be rewarding. Should you accept the challenge, include this import in the preamble:
```latex
\usepackage{tikz}
```

<br />

## **References**
<hr>

- [**Overleaf documentation Home**](https://www.overleaf.com/learn)
- [**TeX Stack Exchange Home**](https://tex.stackexchange.com/)
- [**LaTeX WikiBooks Home**](https://en.wikibooks.org/wiki/LaTeX)
- [**Document Class breakdown**](https://texblog.org/2013/02/13/latex-documentclass-options-illustrated/#multiplecol)
- [**Best YouTube tutorial**](https://www.youtube.com/watch?v=fCzF5gDy60g) (*imo*)
- [**Other YouTube tutorial**](https://www.youtube.com/watch?v=VhmkLrOjLsw) (*he pronounces LaTeX wrong, but I'll forgive him*)
- [**Native LaTeX Font Catalog**](https://tug.org/FontCatalogue/)

<br />

[Back to Table of Contents](#table-of-contents)
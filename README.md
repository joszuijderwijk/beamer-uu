# UU Beamer Theme

A LaTeX Beamer theme for Utrecht University, built on the official brand guidelines (colours, typography, logo placement).

## Quick Start

```latex
\documentclass[aspectratio=169]{beamer}
\usetheme{UU}

\title{Your Title}
\author{Your Name}
\institute{Department \\ Utrecht University}
\date{\today}

\begin{document}
\begin{frame}[plain]
  \titlepage
\end{frame}

\section{Topic}

\begin{frame}{Slide Title}
  Content...
\end{frame}

\standoutframe{A bold statement.}
\thankframe{Thank You!}{email@uu.nl}
\end{document}
```

## Options

Pass as `\usetheme[option1,option2]{UU}`:

| Option | Effect |
|--------|--------|
| `nl` | Use Dutch logo (Universiteit Utrecht) |
| `showlogo` | Show small B/W logo on every content slide |
| `nosectionpage` | Suppress automatic section divider slides |

Logos are selected automatically from the `logos/` folder based on the `nl` option.

## Special Frames

```latex
\standoutframe{Key takeaway text.}    % yellow emphasis slide
\sectionframe{Section Title}          % manual section divider (same style as automatic)
\thankframe{Thank You!}{contact info} % yellow closing slide with logo
```

`\sectionframe` is useful with the `nosectionpage` option, or to insert a
divider mid-section without starting a new `\section`.

## Conference / Multi-Author Title Page

Activate multi-author layout with `\multiauthor`, then reset with `\singleauthor`:

```latex
\author[Alice et al.]{Alice\inst{1} \and Bob\inst{1} \and Eve\inst{2}}
\addinstitute{1}{Dept.\ of ICS, Utrecht University}
\addinstitute{2}{Faculty of EEMCS, Delft University of Technology}
\multiauthor
\venue{NeurIPS 2026, Utrecht}  % optional venue line

\begin{frame}[plain]
  \titlepage
\end{frame}

\clearinstitutes   % reset before switching back
\singleauthor
```

`\addinstitute{n}{Name}` accumulates entries in order — no manual `\scriptsize`
formatting needed. `\clearinstitutes` resets the list and counter.
For full manual control, `\confinstitute{...}` still accepts raw tabular content.

`\venue{...}` replaces the date on the title page with a venue + date combination.

## Code Listings

The `listings` package is pre-configured with UU colours. Use `[fragile]` on
the frame and write code verbatim — no escaping:

```latex
\begin{frame}[fragile]{My Code}
  \begin{lstlisting}[language=Python]
def greet(name):
    return f"Hello, {name}!"
  \end{lstlisting}
\end{frame}
```

Keywords are rendered in dark blue bold, strings in green, comments in gray
italic, with a light gray background. Override individual settings with a local
`\lstset` after `\usetheme`.

## Typography

| Role | Font | Fallback |
|------|------|----------|
| Titles & headings | Merriweather (serif) | Palatino |
| Body text | Open Sans (sans) | Default sans |

```bash
sudo apt install texlive-fonts-extra   # Merriweather + Open Sans
```

## Brand Colours

All available as LaTeX colour names for use in TikZ, text, etc.
Yellow is the primary colour. Red is used sparingly as accent.
Secondary colours are for data visualisation and infographics only.

For more information we refer to [the official guidelines](https://www.uu.nl/en/organisation/corporate-identity/brand-policy/colour).

## Design

- **Title slide** — Asymmetric yellow bar + gradient with radiating lines from the Sol logo
- **Content slides** — Clean white, serif frame titles, yellow rule accent
- **Section dividers** — Full-bleed UU yellow (automatic and `\sectionframe`)
- **Standout** — Yellow with centred black text between accent rules
- **Thank-you** — Yellow with centred B/W logo below text

## Installation

Copy the `.sty` files and `logos/` folder next to your `.tex` file, or install globally into your local texmf tree:

```bash
cp beamer*.sty ~/texmf/tex/latex/beamer-uu/
cp -r logos ~/texmf/tex/latex/beamer-uu/
```

## Compilation

The theme uses `biblatex` with `biber`. Two or three passes are needed:

```bash
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

Or use `latexmk`:

```bash
latexmk -pdf main.tex
```

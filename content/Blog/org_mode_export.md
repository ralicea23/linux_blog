
---
title: "Emacs Exports to PDF"
date: "2024-01-10"
description: "org-mode configs"
tags:
- doom-emacs
- org-mode
ShowReadingTime: "True"
---

![linux](/img/doom_emacs.png)

# Doom Emacs

After hearing about `Emacs` for some time, I began using it last year. Initially, I hesitated due to its steep learning curve and the time investment it required. However, the challenge has been quite rewarding. `Emacs` has revolutionized my daily computer interactions. Although I used to rely heavily on the mouse, `Emacs` has shifted my workflow to be more keyboard-centric, enhancing my overall experience.

The standout feature for me is `Org-mode`, which has significantly improved my productivity. It makes other text editors, like Microsoft Word, seem less capable by comparison. I wonder why I wasn&rsquo;t aware of `Org-mode` sooner.

Currently, I use `Emacs` for a variety of tasks including writing documents, managing blogs, creating Hugo websites, composing and checking emails, navigating the terminal, and editing LaTeX documents. I&rsquo;m looking forward to learning more about its features, such as the agenda, Org-roam, and others.

In this blog post, I aim to discuss exporting to PDF with Org-mode. After extensive research and watching numerous tutorials, I&rsquo;ve established a modest configuration. I&rsquo;m still refining a few tweaks to better suit my workflow, drawing inspiration from various sources online. I welcome advice from experts to help streamline and enhance my configuration.

# Org-mode
```
`Org-mode` preamble I use to export PDF.

    #+OPTIONS: toc:nil title:nil
    #+SETUPFILE: /run/media/rob/RobLinux/My_Documents/emacs/org/setupfiles/org_article_file.org
    #+LATEX_HEADER:\usepackage{fancyheadings}
    #+LATEX_HEADER: \usepackage{minted}
    #+LaTeX_HEADER: \usemintedstyle{manni}
    #+LATEX_HEADER:\usepackage{pdfpages}

    #+BEGIN_EXPORT latex
    \includepdf[pages=1,fitpaper]{linux_files.pdf}

    \pagenumbering{\fancyhf{}}
    \pagestyle{headings}
    \pagenumbering{arabic}

    \fancyhead[R]{\thepage}

    \fancyfoot[C]{New Linux User}
    \pagestyle{fancy}
    \renewcommand{\footrulewidth}{1px}

    \definecolor{dkgreen}{rgb}{0,0.6,0}
    \definecolor{gray}{rgb}{0.5,0.5,0.5}
    \definecolor{mauve}{rgb}{0.58,0,0.82}
    #+END_EXPORT

    @@latex:\clearpage@@
    #+BEGIN_EXPORT latex
    \clearpage \tableofcontents \setcounter{tocdepth}{5} \clearpage
    #+END_EXPORT
```
The `SETUPFILE` configuration i&rsquo;m using is from `Jake B` [YouTube channel](https://www.youtube.com/@JakeBox0). I am actively learning from this configuration and making the necessary adjustments to tailor it to my
preferences.
```
    #+title: Org Article File

    #+LaTeX_CLASS: org-plain-latex
    #+LaTeX_CLASS_OPTIONS: [letterpaper, 12pt]
    #+LATEX_HEADER: \usepackage{lmodern} % Ensures we have the right font
    #+LATEX_HEADER: \usepackage[T1]{fontenc}
    #+LATEX_HEADER: \usepackage[AUTO]{inputenc}
    #+LATEX_HEADER: \usepackage{graphicx}
    #+LATEX_HEADER: \usepackage{amsmath, amsthm, amssymb}
    #+LATEX_HEADER: \usepackage[table, xcdraw]{xcolor}

    % Colorizing links in a nicer way.
    #+LATEX_HEADER: \definecolor{bblue}{HTML}{0645AD}
    #+LATEX_HEADER: \usepackage[colorlinks]{hyperref}
    #+LATEX_HEADER: \hypersetup{colorlinks, linkcolor=blue, urlcolor=bblue}

    % Moving up the title.
    % #+LATEX_HEADER: \usepackage{titling}
    % #+LATEX_HEADER: \setlength{\droptitle}{-6em}

    #+LATEX_HEADER: \setlength{\parindent}{0pt}
    #+LATEX_HEADER: \setlength{\parskip}{1em}
    #+LATEX_HEADER: \usepackage[stretch=10]{microtype}
    #+LATEX_HEADER: \usepackage{hyphenat}
    #+LATEX_HEADER: \usepackage{ragged2e}
    #+LATEX_HEADER: \usepackage{subfig} % Subfigures (not needed in Org I think)
    #+LATEX_HEADER: \usepackage{hyperref} % Links
    #+LATEX_HEADER: \usepackage{listings} % Code highlighting
    % Disables flush alignment on the right side. Personal preference.
    # #+LATEX_HEADER: \RaggedRight

    % Page geometry
    #+LATEX_HEADER: \usepackage[top=1in, bottom=1in, left=.5in, right=.5in]{geometry}
    % #+LATEX_HEADER: \setcounter{tocdepth}{5}
    % #+LATEX_HEADER: \setcounter{secnumdepth}{5}

    % Line spacing
    #+LATEX_HEADER: \renewcommand{\baselinestretch}{1.15}

    % Page numbering - this disables it
    # #+LATEX_HEADER: \pagenumbering{gobble}

    % Spacing, titling, text setting.
    % #+LATEX_HEADER: \usepackage[explicit]{titlesec}

    % Title customization
    % #+LATEX_HEADER: \pretitle{\begin{center}\fontsize{20pt}{20pt}\selectfont}
    % #+LATEX_HEADER: \posttitle{\par\end{center}}
    % #+LATEX_HEADER: \preauthor{\begin{center}\vspace{-6bp}\fontsize{14pt}{14pt}\selectfont}
    % #+LATEX_HEADER: \postauthor{\par\end{center}\vspace{-25bp}}

    % #+LATEX_HEADER: \predate{\begin{center}\fontsize{12pt}{12pt}\selectfont}
    % #+LATEX_HEADER: \postdate{\par\end{center}\vspace{0em}}


    % Section/subsection headings:

    %Section
    % #+LATEX_HEADER: \titlespacing\section{0pt}{5pt}{5pt} % left margin, space before section header, space after section header

    %Subsection
    % #+LATEX_HEADER: \titlespacing\subsection{0pt}{5pt}{-2pt} % left margin, space before subsection header, space after subsection header

    %Subsubsection
    % #+LATEX_HEADER: \titlespacing\subsubsection{0pt}{5pt}{-2pt} % left margin, space before subsection header, space after subsection header

    % List spacing
    #+LATEX_HEADER: \usepackage{enumitem}
    #+LATEX_HEADER: \setlist{itemsep=-2pt} % or \setlist{noitemsep} to leave space around whole list


    # %Section
    % #+LATEX_HEADER: \titleformat{\section} {\Large}{\thesection}{1em}{\textbf{#1}} % Section header formatting
    % #+LATEX_HEADER: \titlespacing\section{0pt}{5pt}{-5pt} % left margin, space before section header, space after section header

    # %Subsection
    % #+LATEX_HEADER: \titleformat{\subsection} {\large}{\thesubsection}{1em}{\textbf{#1}}
    \titlespacing\subsection{0pt}{5pt}{-5pt} % left margin, space before subsection header, space after subsection header

    # %Subsubsection
    % # #+LATEX_HEADER: \titleformat{\subsubsection} {\large}{\the subsubsection}{1em}{#1}
    \titlespacing\subsubsection{0pt}{5pt}{-5pt} % left margin, space before subsection header, space after subsection header

    % Code Blocks Listings
    #+LATEX_HEADER: \usepackage{color}
    #+LATEX_HEADER: \usepackage{listings}
    #+LATEX_HEADER: \usepackage{minted}
```
Example produced [PDF](https://github.com/ralicea23/org-mode-to-pdf/blob/main/my_linux_files.pdf).

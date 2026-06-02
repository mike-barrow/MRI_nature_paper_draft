================================================================================
WBPET Dataset Descriptor -- LaTeX build instructions
================================================================================

Target venue : Nature Scientific Data (Data Descriptor article type)
Template      : Springer Nature article class (sn-jnl.cls), Nature reference
                style (sn-nature). The original, unmodified template lives in
                ./sn-article-template/ for reference.

--------------------------------------------------------------------------------
FILES
--------------------------------------------------------------------------------
  main.tex            Manuscript skeleton; \input{}s the section files below.
  abstract.tex        Working abstract.
  methods.tex         Methods (cohort, acquisition, curation, annotation, ethics).
  datarecords.tex     Data Records (layout, metadata/index, labels, reports).
  validation.tex      Technical Validation.
  usagenotes.tex      Usage Notes.
  codeavailability.tex Code availability.
  references.bib      Bibliography database (currently a placeholder entry).

  Section bodies are conceptual STUBS with bracketed placeholders and % notes.
  Open design decisions are flagged inline (search for "OPEN DECISION").
  Before submission, inline all \input{} files into main.tex (SN wants one .tex).
  sn-jnl.cls          Springer Nature document class (copied from template).
  sn-nature.bst       Nature Portfolio BibTeX style (copied from template).
  sn-article-template/ Pristine upstream template + user manual (sn-article.pdf,
                       user-manual.pdf) for reference.

NOTE ON SUBMISSION: Springer Nature requires the manuscript as a SINGLE .tex
file. This working draft splits the abstract into abstract.tex via \input{} for
convenience. Before submission, inline abstract.tex into main.tex and paste the
generated .bbl in place of the \bibliography command.

--------------------------------------------------------------------------------
HOW TO BUILD
--------------------------------------------------------------------------------
From this directory:

    pdflatex main.tex
    bibtex   main
    pdflatex main.tex
    pdflatex main.tex

Produces main.pdf.

--------------------------------------------------------------------------------
REQUIRED LaTeX PACKAGES
--------------------------------------------------------------------------------
The sn-jnl.cls document class and main.tex depend on packages that are NOT in a
minimal/base TeX Live install. A full TeX Live install ("scheme-full") satisfies
all of them. If you maintain a minimal install, the following packages are
required (and were found missing on at least one machine):

  Package        Provides (.sty)          Needed by
  -------------  -----------------------  -----------------------------------
  sttools        cuted.sty, vruler.sty    sn-jnl.cls (multi-column / line nos.)
  threeparttable threeparttable.sty       sn-jnl.cls (table notes)
  wrapfig        wrapfig.sty              sn-jnl.cls
  breakurl       breakurl.sty             sn-jnl.cls
  appendix       appendix.sty             main.tex (\usepackage[title]{appendix})
  apacite        apacite.sty, apacite.bst sn-jnl.cls (only for the sn-apa style;
                                          loaded by the class regardless)

Also assumed present (usually in texlive-latex-recommended, but listed for
completeness): graphicx, multirow, amsmath, amssymb, amsfonts, amsthm,
mathrsfs, xcolor, textcomp, manyfoot, booktabs, algorithm, algorithmicx,
algpseudocode, listings, geometry, natbib.

INSTALLING THE MISSING PACKAGES
-------------------------------
* Debian / Ubuntu (system TeX Live via apt) -- requires sudo:

      sudo apt-get install texlive-latex-extra texlive-bibtex-extra texlive-science

  texlive-latex-extra provides sttools (cuted, vruler), threeparttable, wrapfig,
  breakurl, appendix; texlive-bibtex-extra provides apacite.

* TeX Live via tlmgr (non-Debian, or a self-managed TeX Live tree):

      tlmgr install sttools threeparttable wrapfig breakurl appendix apacite

  NOTE: On Debian/Ubuntu the apt-managed TeX Live cannot be extended with tlmgr
  unless its release matches the remote repository; prefer the apt route there,
  or install a self-managed current TeX Live from https://tug.org/texlive/.

* Simplest option on any platform: install the full TeX Live scheme
  ("scheme-full"), which includes everything above.

--------------------------------------------------------------------------------
BUILD ARTIFACTS (do not commit)
--------------------------------------------------------------------------------
  main.aux  main.bbl  main.blg  main.log  main.out  main.pdf
================================================================================

# WBPETDataset — Project Context

## Task

This workspace is for authoring a **dataset paper** targeting Nature's
**Scientific Data** venue (https://www.nature.com/sdata/).

### Subject of the paper
A **whole-body pediatric MRI dataset**.

### Dataset characteristics
- **Modality / format:** MRI scans in **NIfTI** format.
- **Scope:** several hundred example scans.
- **Age range:** 0–26 years (pediatric through young adult).
- **Content:** a mix of scans with **various pathologies** and **clear
  (normal) scans**.

### Target venue notes
- Nature *Scientific Data* publishes **Data Descriptor** articles — peer-reviewed,
  structured descriptions of scientifically valuable datasets. The emphasis is on
  the data (provenance, acquisition, format, validation, reuse potential) rather
  than on a hypothesis-driven analysis.

## Workspace layout
- `ExamplePaper/` — reference Scientific Data paper (`s41597-026-07379-w_reference.pdf`)
  to model structure/style against.
- `WritingSamples/` — prior writing samples for voice/style reference.
- `Latex/` — LaTeX sources for the manuscript (see Manuscript status below).
- `Images/` — figures for the manuscript (currently empty).

## Manuscript status (as of 2026-06-02)
- Built in `Latex/` using the Springer Nature class (`sn-jnl.cls`, `sn-nature`
  Nature Portfolio reference style). Upstream template kept pristine in
  `Latex/sn-article-template/`. Required class/bst copied into `Latex/`.
- `Latex/main.tex` is the master file; it `\input{}`s the section files below in
  the Scientific Data Data-Descriptor order, plus back matter (Author
  contributions, Competing interests, Data availability). Title is a working
  title; author/affiliation block is placeholder.
- Section files — currently **conceptual stubs with reusable boilerplate**
  paraphrased/genericized from the reference paper (each has a header comment
  flagging "modeled on reference — REWRITE before submission"; specifics marked
  `[TBD: ...]`; open choices marked `OPEN DECISION`):
  - `abstract.tex` — working abstract (user-edited).
  - `background.tex` — Background & Summary (AI → whole-body taxonomy → adult/CT
    gap → pediatric-MRI motivation).
  - `methods.tex` — Ethics, Participants, Clinical MRI protocols, Data
    processing, Annotation. Ethics/access wording in the reference is Danish/EU
    GDPR + PublicnEUro and does NOT apply — retarget to Stanford IRB/HIPAA.
    BET skull-stripping is brain-specific, likely N/A for whole-body.
  - `datarecords.tex` — layout, NIfTI + sidecar JSON, indexing-variable table,
    SQLite relational index, label records (keyed by reader/anatomy), reports.
  - `validation.tex` — expert Likert quality scoring, inter-reader agreement,
    integrity checks, report de-id audit, baseline.
  - `usagenotes.tex` — access conditions, querying the index, query/preview
    client, multimodal report use, splits/limitations.
  - `codeavailability.tex` — conversion/scrubbing/index-builder/client/validation
    code.
  - `references.bib` — placeholder bib entry only (no real citations yet).
- Figures are compiling `\fbox` placeholders (`fig:cohort`, `fig:workflow`), not
  real images — swap in our own. Placeholder tables: `tab:acq`, `tab:qc`,
  `tab:vars`.
- SUBMISSION NOTE: SN wants a single `.tex`. Before submission, inline all
  `\input{}` files into `main.tex` and paste the `.bbl` in place of
  `\bibliography`.
- Build: `pdflatex main` → `bibtex main` → `pdflatex main` ×2 (run from
  `Latex/`). Required packages + install notes in `Latex/README.txt`.
- VERIFIED building (2026-06-02): produces `main.pdf` (~8 pp), no errors, all
  refs resolve. bibtex "no \citation" / natbib "empty thebibliography" warnings
  are expected until real refs are cited.
- TeX environment note: required packages came from `texlive-latex-extra` +
  `texlive-bibtex-extra`. The `texlive-full` install wedged on ConTeXt's format
  build (Ubuntu bug #2058409 / Debian #913697: luatex socket disabled vs
  context, postinst blocks on TeX's `?` prompt). Fix is to feed the prompt:
  `yes q | sudo dpkg --configure -a` (or `sudo dpkg --configure -a </dev/null`).

## Open TODOs / follow-ups
- **Additional sequences:** check whether 3D Slicer can filter/select by
  sequence (e.g., DWI). Decision on supporting additional sequences depends on
  this. _Owner: undecided — needs assigning._
- **De-identification approach:** uncertain what the best method is. Candidate
  idea: use existing classes/tools to build an automatic de-facer. Needs a
  decision before release. _Owner: undecided._ (Ties into the report-scrubbing
  and de-identification stubs in `Latex/methods.tex` / `validation.tex`.)
  - **Ask AIMI for help with de-identification** and check whether there is an
    associated cost. _Felix TODO._
- **Data hosting / DOI:** the dataset itself likely must be published *outside*
  Nature (Scientific Data publishes the descriptor; the data live in an approved
  external repository with its own DOI). Uncertain whether AIMI (Stanford
  internal) can provide the required DOI.
  - **Leading candidate: PhysioNet** (https://physionet.org/about/publish/).
    Its descriptor structure (Background, Methods, Content Description, Usage
    Notes) parallels Scientific Data, and it provides a preflight validation
    tool (`pip install physionet` → `physionet validate PATH`).
  - **Sidebar / precursor:** we believe we ought to publish *something else
    first* before the main dataset descriptor. _TBD what that precursor is._
- **Schema overlap with Croissant:** PhysioNet recommends **Croissant** metadata
  (MLCommons standard; user wrote "crousiont"), generated via the Croissant
  Baker tool (`pip install croissant-baker` → `croissant-baker --input PATH`).
  TODO: determine how much our proposed indexing schema (see Table in
  `Latex/datarecords.tex`) overlaps with Croissant — if it largely covers our
  needs, adopt Croissant rather than maintaining a parallel custom schema.
  _Owner: undecided._

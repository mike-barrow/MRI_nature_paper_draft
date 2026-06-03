# WBPETDataset — Project Context

## Task

This workspace is for authoring a **dataset paper** targeting Nature's
**Scientific Data** venue (https://www.nature.com/sdata/).

### Subject of the paper
A **pediatric whole-body PET/MRI dataset**.

### Dataset characteristics
- **Modality / format:** whole-body **PET/MRI**, released as **DICOM** (TCIA),
  segmentations as **DICOM-SEG**. (NIfTI conversions pending a question to Michael.)
- **Scope:** [TBD] examinations (target ~[TBD]).
- **Age range:** [TBD] years (pediatric through young adult).
- **Content:** anatomy-segmented scans, tumor-lesion-segmented scans, and
  disease-free follow-up scans.

### Target venue notes
- Nature *Scientific Data* publishes **Data Descriptor** articles, peer-reviewed
  structured descriptions of scientifically valuable datasets. The emphasis is on
  the data (provenance, acquisition, format, validation, reuse potential) rather
  than on a hypothesis-driven analysis.

## Workspace layout
- **Template:** the manuscript follows the **AutoPET data descriptor** (Gatidis
  et al. 2022, *Sci Data* 9:601, `s41597-022-01718-3`) as the primary
  structural and stylistic model. AutoPET is whole-body PET oncology with lesion
  segmentation, on TCIA under CC BY 4.0, co-authored by our TCIA contact Sergios
  Gatidis. The earlier brain-MRI taxonomy paper (`s41597-026-07379-w`) is the
  retired template; borrow from it only the acquisition-parameter-table device
  and its explicit access-description discipline.
- `WritingSamples/` — prior writing samples for voice/style reference.
- `Latex/` — LaTeX sources for the manuscript (see Manuscript status below).
- `Images/` — figures for the manuscript (currently empty).

## Manuscript status (as of 2026-06-03)

- Built in `Latex/` using the Springer Nature class (`sn-jnl.cls`, `sn-nature`
  Nature Portfolio reference style). Upstream template kept pristine in
  `Latex/sn-article-template/`. Required class and bst copied into `Latex/`.
- `Latex/main.tex` is the master file; it `\input{}`s the section files below in
  the Scientific Data Data-Descriptor order, plus back matter (Author
  contributions, Competing interests, Funding, Data availability). Title is set;
  the author/affiliation block is a placeholder pending the author list.
- Section files (each `\input` into `main.tex` in Data-Descriptor order):
  - `abstract.tex` — abstract (hand-written by Michael, pending a revision pass).
  - `background.tex` — Background & Summary (pediatric whole-body PET/MRI motivation, with citations).
  - `methods.tex` — Ethics, Participants, Image acquisition (PET + MRI), Data processing, Annotation.
  - `datarecords.tex` — TCIA DICOM hierarchy, per-examination metadata CSV, label records.
  - `validation.tex` — expert image-quality screen, inter-reader agreement, data integrity, baseline.
  - `usagenotes.tex` — access conditions, reading the data, cohort selection, suggested splits and limitations.
  - `codeavailability.tex` — code availability statement.
  - `references.bib` — cited references.
- Figures are compiling `\fbox` placeholders (`fig:cohort`, `fig:workflow`), to be
  replaced with real images. Placeholder tables: `tab:acq`, `tab:qc`, `tab:vars`.
- SUBMISSION NOTE: SN wants a single `.tex`. Before submission, inline all
  `\input{}` files into `main.tex` and paste the `.bbl` in place of
  `\bibliography`.
- Build: `pdflatex main` then `bibtex main` then `pdflatex main` x2 (run from
  `Latex/`). Required packages and install notes in `Latex/README.txt`.
- Builds clean: `main.pdf` (9 pp), no errors, all references resolve.

## To-do and decisions

### Decisions (current)

- **Template:** follows the AutoPET data descriptor (Gatidis et al. 2022, *Sci Data* 9:601).
- **Authorship:** all authors contributed equally, no designated first author. Implemented in `main.tex` via `\equalcont`. Set and order to be confirmed with the co-authors.
- **Acknowledgements:** none (optional section omitted).
- **Data format:** DICOM only, with segmentations as DICOM-SEG. Whether to also ship NIfTI conversions is an open question for Michael.
- **Released components:** imaging (DICOM), anatomical segmentations, tumor-lesion segmentations, disease-free follow-up examinations, and indexing metadata. No radiology reports, and no staging or metabolic-response labels in the public release.
- **Host:** TCIA, open under CC BY 4.0. The descriptor names a single host of record.
- **De-identification:** to a HIPAA standard, most likely through the TCIA submission pipeline, with whole-body defacing of the MR and PET and a per-subject date shift. Verified by the host after deposit.
- **Spelling:** American English throughout the body (matches the title). The abstract is the one exception, pending revision.
- **PET acquisition:** tracer is FDG in all examinations. The Methods acquisition section covers both PET and MRI.
- **Data Records:** TCIA DICOM hierarchy plus a per-examination metadata CSV plus label records (no BIDS, no SQLite index, no Croissant, no separate query client).
- **Technical Validation:** an expert image-quality screen flags non-diagnostic scans. Whether to publish a trained segmentation baseline, inter-reader agreement, or both is still open.
- **Bibliography:** `references.bib` holds the cited references, and the Springer Nature style `sn-nature.bst` is included in `Latex/` so the bibliography builds.
- **Figures and tables:** `fig:cohort` (cohort overview) and `fig:workflow` are placeholders pending real images; `tab:acq`, `tab:qc`, `tab:vars` pending values.

All quantitative cohort numbers are intentionally left `[TBD]` for now, to be filled in one pass once the counts are reconciled.

### To-do, by person

**Felix**
- Corresponding author and institutional email (`main.tex`).
- Funding statement: NCI R01 CA269231 plus the travel grant (`main.tex`).
- Cohort numbers: total N, patient count, ages, the three subset counts (anatomy / lesion / follow-up), and the overlap (`background.tex`, `methods.tex`, `datarecords.tex`).
- Segmentation release format: NIfTI or DICOM-SEG (`methods.tex`, `datarecords.tex`).
- Annotation protocol: confirm whether a written protocol exists (`methods.tex`).
- Annotator experience levels: confirm (`methods.tex`).
- Technical Validation: decide whether to publish the trained model, the inter-reader agreement, or both (`validation.tex`).
- Usage Notes access conditions: de-id status, access model, license, timelines, commercial-use terms (`usagenotes.tex`).
- Code Availability: confirm which code, if any, is released and where (`codeavailability.tex`).
- TCIA submission: obtain the accession number, DOI, and final access conditions once the collection is set up (`main.tex`, `datarecords.tex`, `usagenotes.tex`).
- De-identification and defacing pipeline.
- AIMI and hosting: confirm with Scientific Data whether AIMI can serve as the host (inquiry drafted).
- Decide whether a precursor publication is needed before the descriptor.

**Michael**
- Confirm the author set and order under the all-equal model (`main.tex`).
- CRediT author contributions per author (`main.tex`).
- Acquisition (`methods.tex`): PET/MR scanner make and model, field strength, FDG injected activity and uptake time, the core MRI sequence set, and the per-protocol parameters (TR/TE/flip/voxel/orientation) for `tab:acq`.
- DICOM StudyDate range (acquisition start and end) and the per-subject sex split (`methods.tex`).
- Whether NIfTI conversions can ship alongside the DICOM / DICOM-SEG release.

**Heike**
- Darlene Okpokpo: stays on the author list or not, given the Stanford-affiliation-only rule on the R01 (`main.tex`).
- Exact per-author affiliation strings (`main.tex`).
- Approving IRB and protocol number for the released cohort (`methods.tex`).
- Legal basis and consent model, for example an IRB-approved waiver of informed consent (`methods.tex`).
- Name the board-certified radiologist for the image-quality review (`validation.tex`).

### Questions for Michael
1. For the descriptor, do we keep the AIMI poster author set (Horvath, Barrow, Singh, Lokesha, Okpokpo, Gatidis, Daldrup-Link), and are you good with an all-authors-contributed-equally model (no designated first author)?
2. Can you give CRediT-style contributions per author?
3. Can we additionally provide NIfTI conversions alongside the DICOM / DICOM-SEG release, or is DICOM-only simpler on your side?
4. Acquisition details: PET/MR scanner make and model, field strength, FDG injected activity and uptake time, the core MRI sequence set, and the per-protocol parameters (TR/TE/flip/voxel/orientation) for Table 1?
5. The DICOM StudyDate range (acquisition start and end) and the per-subject sex split?

### Questions for Heike
1. Does Darlene Okpokpo stay on the author list given the Stanford-affiliation-only rule on the R01 (she is no longer at Stanford)?
2. Can you confirm the exact affiliation strings for each co-author?
3. What is the approving IRB and protocol number for the released pediatric PET/MRI cohort (retrospective)?
4. What is the consent model? Was an IRB waiver of informed consent granted for sharing the de-identified data, or were patients consented?

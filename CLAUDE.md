# Pediatric whole-body PET/MRI dataset descriptors — project context

## Task

This repository holds **two** Nature *Scientific Data* Data Descriptor manuscripts built from
one single-center pediatric whole-body PET/MRI lymphoma cohort. The earlier unified descriptor
was split into two papers, divided by labeled task rather than by raw modality:

- **PediMRI** (`Latex/pedimri/`, working label) — pediatric whole-body **MRI** with
  multi-structure normal-anatomy segmentations. Modeled on the Multi-Modal Pelvic MRI
  organ-segmentation descriptor (Scientific Data 2025, `s41597-025-05623-3`).
- **PediPET** (`Latex/pedipet/`, working label) — pediatric **FDG-PET/MRI** with tumor-lesion
  segmentations and disease-free follow-up references, the pediatric counterpart to AutoPET.
  Modeled on the AutoPET descriptor (Gatidis et al. 2022, Scientific Data 9:601).

Both descriptors draw on overlapping patients and the same co-acquired imaging. Each states the
cohort overlap and cross-references the other, and each is framed as a distinct labeled-task
release so the two remain separately publishable. The companion of each cannot be a numbered
data citation until its Digital Object Identifier is minted.

The superseded unified draft is kept at `Latex/original/` for reference.

## Scope (target)

Approximately 300 whole-body PET/MRI examinations: about 80 carry normal-anatomy segmentations
(PediMRI) and about 120 carry tumor-lesion segmentations (PediPET), plus disease-free follow-up
references (PediPET). Final counts are `[TBD]` until the release cohort is locked.

## Manuscript status

Both manuscripts are drafted through every mandated Scientific Data section (Background &
Summary, Methods including an Ethics statement, Data Records, Technical Validation, Usage Notes,
Data Availability, Code Availability, Author Contributions, Competing Interests, Funding), in the
required order with Code Availability immediately before the references. Both compile cleanly
(`sn-jnl` class, `sn-nature` reference style). Every unverified specific is marked `[TBD]`. Each
title is within 110 characters with no colon, parentheses, brand name, or advertising word, and
each abstract is under 170 words with no findings claims.

The descriptors describe the dataset as it will exist at publication: de-identification, the
HIPAA Expert Determination, face and pelvic defacing, repository deposit with a DOI, and the
technical-validation analyses are written as accomplished. Only genuinely-unknown specifics
(tool names and versions, the repository, accession, DOI, license, scanner and acquisition
parameters, counts, and metric values) remain `[TBD]`.

## Open items, by owner

**Michael — acquisition, cohort numbers, baselines**
- PET/MR scanner make and model, field strength.
- MRI sequence set and the representative acquisition parameters (TR, TE, flip angle, voxel
  size, orientation) for the acquisition table.
- FDG injected activity, uptake time, reconstruction, attenuation-correction method.
- DICOM StudyDate range; per-subject sex; cohort counts (whole N, the anatomy / lesion /
  disease-free subset counts, and the overlap between subsets).
- The reproducible segmentation baselines: the anatomy-segmentation model (Dice, HD95) and the
  lesion-segmentation baseline (Dice, false-positive and false-negative volumes), with the
  training and evaluation scripts and the corrected data export, so the Technical Validation
  numbers are reproducible.
- Whether derived NIfTI ships alongside the DICOM and DICOM-SEG release.

**Heike — authorship, ethics, host**
- Author set, order, first-author designation, and the per-author affiliation strings.
- The consent and waiver model and the approval date for protocol 44706.
- The Expert Determination certifying party.
- The repository and the open-versus-controlled-access decision, which drives the license.

**Felix**
- Pelvic defacing tool and pipeline.
- Per-case protocol-provenance map.
- Limb-bone label provenance and its redistribution license.
- The inter-reader and qualitative-rating studies.
- Repository deposit, accession, and DOI; the companion-descriptor DOI cross-references; the
  article-processing charge.

## Per-paper notes

- Both papers cite the adult TotalSegmentator MRI tool (`Wasserthal_2025`) as the adult-trained
  reference for the difficulty of pediatric anatomy.
- PediPET cites the EANM paediatric dosage card (`Lassmann_2007`) for weight-based FDG dosing,
  and AutoPET (`Gatidis_2022` and its repository deposit) as the template and the comparator.
- Figures are compiling placeholders pending real images.

## Build

From each paper's subdirectory: `pdflatex main`, then `bibtex main`, then `pdflatex main`
twice. Delete the build artifacts afterward, keeping only the source. Before submission, inline
the section files and the references into a single `.tex` (Scientific Data requires the
references embedded directly, with no separate `.bib` or `.bbl`).

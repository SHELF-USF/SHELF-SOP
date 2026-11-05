# SHELF SOP 4: Data Management

This SOP covers SHELF data from collection through archiving: submission,
QA/QC, the database, version control, and archiving. Terms such as transect,
TransectID, and contig are defined in the SOP 1 glossary.

---

## 4.1 Data, study components, and personnel

### 4.1.1 SHELF data products

SHELF uses DNA barcoding to identify fish eggs collected on the West Florida
Shelf (WFS) with a Continuous Underway Fish Egg Sampler (CUFES). The goal is
to describe where and when fish spawn. Program background is given in SOP 1.

**Primary data products** (archived and submitted to GRIIDC):

1. **Transect records**: metadata for every CUFES transect (location, date, time,
   depth, vessel). All other data link to these records. They are
   recorded in the field under SOP 2.
2. **Environmental data**: continuous flowthrough sensor data (temperature,
   salinity, chlorophyll, etc.) and echosounder data recorded underway on
   each cruise. *[Database import pending]*
3. **Egg counts**: the total and picked egg counts for each transect, including
   transects where eggs were collected but not barcoded. These are recorded
   during egg picking under SOP 3.
4. **Barcoded egg sequences**: individual egg identifications with species,
   percent match, collection location, and related metadata. These are
   produced under SOP 3.

**Source documents** (kept internally to support QA/QC, but not archived as
primary data products):

- **Field datasheets**: scanned paper records of transect-level observations,
  stored as PDFs in `01_Data/04_source_data/01_cruises/`

### 4.1.2 Study components by SHELF phase

#### SHELF Phase I (2017–2018)

| StudyComponent | Description |
|----------------|-------------|
| `depm` | Daily Egg Production Method analyses |
| `acoustics` | Acoustics targeted study |
| `stable_isotopes` | Stable isotope targeted study |
| `benthic_mapping` | Benthic habitat mapping targeted study |

*Note: Phase I data are partly archived in `01_Data/04_source_data/08_legacy/`.
Full import into the SHELF database is pending.*

#### SHELF Phase II (2019–2022)

| StudyComponent | Description |
|----------------|-------------|
| `fall_shelf_time_series` | Annual fall SEAMAP and FIO shelf cruises; the founding long-term time series (Phase II used archived SEAMAP samples from 2013, 2014, and 2019) |
| `metabarcoding` | Targeted study testing metabarcoding methods |

*Note: Phase II metabarcoding data have not yet been imported into the database.*

#### SHELF Phase III (February 1, 2023 – July 31, 2027)

| StudyComponent | Description |
|----------------|-------------|
| `fall_shelf_time_series` | Annual fall SEAMAP and FIO shelf cruises; the founding long-term time series |
| `seasons_shelf_time_series` | FIO shelf cruises in all four seasons (TS1) |
| `seasons_reef_time_series` | FIO reef cruises in all four seasons (TS2) |
| `winter_mocness` | 2012 MOCNESS depth-stratified tows, testing the assumption that eggs concentrate near the surface (TS3) |
| `barcoding_success` | Study of barcoding success rates with multiple primers (TS4) |

### 4.1.3 Personnel and responsibilities

| Role | Person(s) | Responsibility |
|------|-----------|---------------|
| PI | Stallings | Program oversight, database management, funder reporting, analyses |
| Co-PI | Breitbart | Direction of DNA barcoding, oversight of sequence data |
| PI lab manager | AliciaGrace Marley | Field operations, DNA barcoding, data coordination |
| Co-PI lab manager | Makenzie Kerr | Barcoding lab operations, submission of sequence data |
| Graduate student | Jessica Sklar | Field operations, DNA barcoding, data submission, analyses |
| Graduate student | Alexis Mitchem | Data submission, analyses, targeted studies |
| Undergraduate assistants | Varies by semester (see `tbl_Personnel`) | Egg picking, egg counting, bench work |
| SEAMAP (NOAA) | Glenn Zapfe et al. | Annual fall CUFES cruises, archived egg samples |

---

## 4.2 Shared folder structure

All SHELF data are stored in a shared OneDrive folder, which team members
open through their USF OneDrive account. All file paths in this SOP are
given relative to the shared root, `1. SHELF_SHARED/`. The full OneDrive path
above that level differs from user to user. How to get access, and the
rules for using the folder, are in SOP 1, Section 1.8.2.

```
1. SHELF_SHARED/
├── 00_MD_SHELF/            ← notes, meeting notes
├── 01_Data/                ← all data (Section 4.2.1)
├── 02_Analyses & Figures/  ← R projects, figures
├── 03_Reports & Proposals/ ← reports, proposals
├── 04_Literature/          ← references, publications
├── 05_Manuscripts/         ← manuscript drafts
├── 06_Presentations/       ← presentations
├── 07_Photos/              ← cruise, outreach photos
├── 08_Logos/               ← logos, branding
└── 09_SOP/                 ← SOP releases (Word)
```

### 4.2.1 Data folder structure (01_Data)

The live database file and the folders that support it sit directly in
`01_Data/`. All source data are organized under `04_source_data/`.

```
01_Data/
├── SHELF_DB_WORK.accdb     ← live database
├── 01_archive/             ← dated database snapshots
│   └── SHELF_DB_YYYYMMDD.accdb
├── 02_tables/              ← living tables, staging
│   ├── tbl_Personnel.xlsx  ← personnel roster
│   └── staging/            ← files awaiting import
│       ├── sequence_csv_instructions.md
│       ├── example_sequences_import.csv
│       ├── example_failed_import.csv
│       └── example_eggcounts_import.csv
├── 03_scripts/             ← R scripts (SHELF-DB repo)
└── 04_source_data/         ← source data (read-only)
    ├── 01_cruises/         ← scanned datasheets
    ├── 02_cufes/           ← CUFES transect files
    ├── 03_site_selection/  ← GRTS site selection
    ├── 04_environmental/   ← flowthrough, echosounder
    ├── 05_egg_counts/      ← egg count sheets
    ├── 06_sequences/       ← barcoding lab files
    ├── 07_taxa/            ← FishBase pulls, taxa data
    └── 08_legacy/          ← files awaiting import
```

`08_legacy/` holds Phase I data, the metabarcoding master spreadsheet,
larvae occurrences, cruise statistics, and other files awaiting import or
classification.

#### Key principles
- The database and its supporting folders sit directly in `01_Data/`, not in
  a subfolder.
- `04_source_data/` is an archive. Files there are read, never edited.
- `02_tables/staging/` is the only folder that receives new files for
  import.
- After a successful import, move the source files from `staging/` to the
  matching `04_source_data/` subfolder.
- Site selection code is kept in `03_site_selection/` as a source data
  reference. Working analytical versions live in `02_Analyses & Figures/`.

### 4.2.2 Naming conventions

**Cruise folders**: `YYYY-MM (CruiseCode)`, e.g., `2024-11 (HO2507)`

**Cruise codes**: `[VesselCode][FY][NN]`. FIO assigns these, and SHELF
uses them unchanged. `[FY]` is the two-digit Florida fiscal year (July 1 –
June 30), and `[NN]` is the cruise number within that fiscal year. For
example, `WB2410` is the 10th Weatherbird II cruise of FY2024 (July 2023 –
June 2024). The cruise code does **not** give the calendar month of the
cruise; use the cruise date or the `[YYYYMM]` part of file names for that.
SEAMAP cruises use NOAA's cruise identifiers (e.g., `GU2403`, Gordon Gunter).

#### TransectID format
- FIO cruises: `[CruiseCode]_[Station].[N]`, e.g., `WB2410_B111.1`.
  The extension numbers transects in chronological order from the station.
  `.1` is the transect that begins exactly on station, `.2` is the next, and so
  on. Extensions are not zero-padded (`.1`, `.2` … `.10`). The captain and
  the on-duty science crew coordinate by radio, and no new transect is
  started if the vessel will reach the next station in less than 35 minutes. SOP 2
  describes the procedure at sea.
- SEAMAP cruises: the CUFES number only, e.g., `11620`
- MOCNESS: `OR298_[Station].[DepthBin]`, e.g., `OR298_58.2`
- When one sample fills more than one vial, SOP 2 adds a vial suffix (e.g.,
  `B119.2.1`, `B119.2.2`). Vial suffixes are **not** part of the TransectID.
  All vials from one transect share a single TransectID.

**Source and submission file naming**: every file submitted to `staging/`
or stored in `04_source_data/` follows this convention:

`[datatype]_[CruiseCode]_[YYYYMM]`

- `[datatype]` gives the data type and, where relevant, the collection
  context, e.g., `sequences_reef`, `sequences_shelf`, `failed_reef`,
  `eggcounts`, `environmental`, `datasheets`
- `[CruiseCode]` is the cruise identifier, e.g., `WB2410`, `GU2403`, `HO2507`
- `[YYYYMM]` is the year and month of collection

Examples:
- `sequences_reef_WB2410_202406.csv`
- `failed_reef_WB2410_202406.csv`
- `sequences_shelf_HO2507_202411.csv`
- `eggcounts_GU2403_202409.csv`
- `environmental_WB2601_202509.csv`
- `datasheets_WB2505_202412.pdf`

---

## 4.3 Database

### 4.3.1 Tables

SHELF uses a Microsoft Access relational database as its main data store.
Its core tables are listed below. Other tables are being developed and will
be documented in later versions of this SOP.

| Table | Contents |
|-------|----------|
| `tbl_Cruises` | One row per cruise: CruiseID, CruiseCode, vessel, phase |
| `tbl_Vessels` | Vessel names and IDs |
| `tbl_Transects` | One row per CUFES transect: location, date, time, depth |
| `tbl_Sequences` | One row per barcoded egg identification |
| `tbl_FailedSequences` | Eggs that did not produce an accepted identification |
| `tbl_EggCounts` | Total and picked egg counts per transect |
| `tbl_Taxa` | Species-level biological attributes from FishBase |
| `tbl_Personnel`, `tbl_PersonnelRoles`, `tbl_PersonnelPhases` | SHELF team members, their roles, and the phases they worked in |
| `tbl_ProposedSeq` | Proposed egg counts per study component (budget tracking) |
| Other tables | Environmental data, reef survey data, and others are planned for future import |

#### New taxa entries

- When an entry names more than one species, list them in alphabetical
  order (e.g., `Decapterus punctatus/tabl`, not `Decapterus tabl/punctatus`).
- Leave `Genus`, `Species`, and `Family` blank for any species pair,
  multi-species, or genus-level entry (e.g., `Decapterus punctatus/tabl`),
  even if the species share a genus.
- Set `Resolved = TRUE` only when `ScientificName` is a single, fully
  resolved species.
- FishBase trait data (via `rfishbase`) are pulled only for entries with
  `Resolved = TRUE`. Unresolved entries keep their trait fields blank.

### 4.3.2 Database file versioning

The database file uses a `WORK`/dated-archive convention: underscores only,
no version numbers. The date alone tells archive copies apart, because
archiving happens at most once a day. The folder layout is shown in
Section 4.2.1.

#### Conventions
- `SHELF_DB_WORK.accdb` is the only database file that is ever edited.
- Before any major data import, save a dated copy in `01_archive/` named
  `SHELF_DB_YYYYMMDD.accdb`.
- Never rename, edit, or delete an archive copy.
- Never rename `SHELF_DB_WORK.accdb`. All R scripts refer to this filename.
- R scripts read input files from `02_tables/staging/`. They never write to
  `04_source_data/`.
- R scripts that refer to the database or staging files must build file
  paths with `Sys.getenv("USERPROFILE")` rather than a hard-coded user path.
  This lets the same script run for any team member with access to the
  shared OneDrive folder.

### 4.3.3 Local development copy

Analysis code may be developed against a static local copy of the database
before it is moved into the shared folder. This keeps work in progress away
from the live, constantly synced production database. It also avoids
OneDrive conflict copies, which happen when a binary Access file is open in
more than one place at the same time.

1. Keep the local copy in a single-user folder outside the shared team
   structure, named `SHELF_DB_CLONE.accdb` so it cannot be mistaken for the
   production file. Refresh it by hand. Never sync it live with
   `SHELF_DB_WORK.accdb`.
2. Develop and test scripts against the local copy.
3. Once the scripts work, copy only the code files (`.Rproj`, `.qmd`, `.R`)
   into the matching shared analysis folder.
4. In the copied scripts, change the database path to point to
   `SHELF_DB_WORK.accdb`.
5. Never copy a database file from a local copy into the shared folder.

### 4.3.4 GitHub repository

All R scripts that import, modify, or query the database are kept under
version control in a private GitHub repository, `SHELF-DB`, in the SHELF
organization (`SHELF-USF`), shown below. How
to get a GitHub account and access is described in SOP 1, Section 1.8.3.

```
SHELF-DB/
├── README.md   ← setup, connection, conventions
├── import/     ← import scripts
├── qaqc/       ← QA/QC validation scripts
├── queries/    ← key Access queries, as SQL
└── utils/      ← shared helper functions
```

`README.md` covers setup, the database connection, and script conventions.
`import/` holds the scripts for sequences, transects, egg counts, and
personnel.

#### Commit conventions
- Commit scripts both before and after running them against the database.
- Commit message format: `[table] brief description`, e.g.,
  `[tbl_Sequences] import WB2601 fall shelf sequences`
- Never commit database files (`.accdb`) to GitHub. They are binary files;
  use `01_archive/` instead.

---

## 4.4 Data submission by SHELF team members

### 4.4.1 General principles

All data produced by the SHELF team (sequences, egg counts, environmental
data, datasheets) must be:

1. Uploaded to `01_Data/02_tables/staging/` in the shared OneDrive folder
2. Named and formatted as described in this SOP (Section 4.2.2)
3. Submitted within 10 days of collection or processing being completed,
   unless a different timeline has been agreed with the PI

After uploading, the submitter must notify both the **PI and the PI's lab
manager**, by email or Teams message, giving the filename. This allows QA/QC
and database import to happen promptly.

**Data files sent by email are not accepted.** They will be returned with a
request to upload them to the shared folder.

### 4.4.2 Sequence data (barcoding lab)

Successful identifications and failed barcoding records for a cruise must be
submitted together as a pair:

1. `sequences_[context]_[CruiseCode]_[YYYYMM].csv`: successful identifications
2. `failed_[context]_[CruiseCode]_[YYYYMM].csv`: failed barcoding attempts

These resources in the staging folder explain how to prepare the files:
- `sequence_csv_instructions.md`: requirements for each column and common
  mistakes
- `example_sequences_import.csv`: template to copy and fill in

SOP 3, Section 3.9, produces a bench spreadsheet in this column layout.

#### Successful sequence CSV format

| Column | Required | Format | Notes |
|--------|----------|--------|-------|
| TransectID | Yes | Text | Must exactly match a TransectID in `tbl_Transects` |
| EggNumber | Yes | Integer or `contigNN` | Plain integer for a single egg (a read that did not assemble into a contig). `contig01`, `contig02`, etc. for contigs: consensus sequences assembled from the overlapping reads of two or more eggs in the same transect. A transect can have several contigs. See the SOP 1 glossary |
| ScientificName | Yes | `Genus species` | Must exactly match `tbl_Taxa`. For unresolved IDs, list the candidate species alphabetically, separated by `/` (e.g., `Decapterus punctatus/tabl`) |
| NumberEggs | Yes | Positive integer | 1 for single eggs. For contigs, the number of reads (eggs) assembled into the contig (≥2) |
| PercentID | Yes | 97–100 | BOLD probability of placement or GenBank BLAST percent identity. No % symbol. IDs below 97% go in the failed file (`LowPercentID`) |
| DNAdb | Yes | `BOLD` or `GenBank` | Exact capitalization. Use `GenBank` for IDs made with NCBI BLAST |
| Station | Yes | Text | Station label from the bench sheet |
| Notes | No | Free text | Leave blank if there is nothing to note |
| Sequence | Yes | DNA string | Must not be empty. Valid nucleotide codes only (A, C, G, T, U, N, or IUPAC ambiguity codes), no spaces |
| CollectionType | Yes | Controlled value | See Section 4.5.1 |
| StudyComponent | Yes | Controlled value | See Section 4.5.2 |
| Phase | Yes | Integer | See Section 4.5.4. Phase III = 3 |

**Failed sequence CSV format** (see `example_failed_import.csv`). One row
per egg that did not produce an accepted identification:

| Column | Required | Format | Notes |
|--------|----------|--------|-------|
| TransectID | Yes | Text | Must match `tbl_Transects` |
| EggNumber | Yes | Integer | Egg number from the bench sheet / plate map |
| FailReason | Yes | Controlled value | See Section 4.5.3. Use `Unknown` if the cause is not known |
| NumberEggs | Yes | Positive integer | Normally 1 |
| DNAdb | No | `BOLD` or `GenBank` | Only if a search was run (`NoMatch`, `LowPercentID`, `InvertebrateMatch`) |
| ScientificName | No | `Genus species` | Best match, for near-miss IDs (`LowPercentID`) and `InvertebrateMatch` |
| PercentID | No | 0–100 | Percent of the best match, if a search was run |
| Sequence | No | DNA string | If a sequence was obtained. Same character rules as above |
| CollectionType | Yes | Controlled value | See Section 4.5.1 |
| StudyComponent | Yes | Controlled value | See Section 4.5.2 |
| Phase | Yes | Integer | See Section 4.5.4 |
| Notes | No | Free text | |

### 4.4.3 Egg count data (egg picking)

Egg counts are recorded during egg picking (SOP 3, Section 3.3). Submit
them as a CSV, using `example_eggcounts_import.csv` in the staging folder as
the template.

| Column | Required | Format | Notes |
|--------|----------|--------|-------|
| TransectID | Yes | Text | Must match `tbl_Transects` |
| EggsPicked | Yes | Non-negative integer | Eggs picked from the sample (≤96) |
| EggsTotal | Yes | Non-negative integer | Total eggs in the sample (all vials) |
| Time_min | No | Positive number | Picking time in minutes, if recorded |
| DatePicked | No | YYYY-MM-DD | Date the eggs were picked in the lab |
| Obs | Yes | Text | Observer initials |
| Notes | No | Free text | |

### 4.4.4 Adding new personnel

The official SHELF personnel roster is `01_Data/02_tables/tbl_Personnel.xlsx`.
Add new people there, not directly in the database. To add a person:

1. Open `tbl_Personnel.xlsx` and add a row with the person's information.
2. Fill in the required fields: `LastName`, `FirstName`, `InstitutionID`,
   `IsActive`, `Roles`.
3. For `Roles`, use the `RoleID` value from `tbl_PersonnelRoles`, not the
   role name.
4. Save the file in the shared OneDrive folder.
5. Tell the PI or lab manager that a new person has been added.
6. The PI runs `update_personnel.R` to sync the roster to the database.

The script is safe to re-run at any time. It never duplicates or overwrites
existing records. It inserts only rows that are not already in the database
(matched on LastName + FirstName).

---

## 4.5 Controlled vocabularies

These are the approved values for fields that require standard entries. Any
value outside these lists fails QA/QC validation, and the data will not be
imported until it is corrected. This section also serves as a secondary
source of metadata for the SHELF database.

### 4.5.1 CollectionType

| Value | Description |
|-------|-------------|
| `SEAMAP_fall` | Annual NOAA SEAMAP fall cruise (August–September) |
| `SEAMAP_winter` | SEAMAP winter cruise (MOCNESS 2012) |
| `FIO_shelf_summer` | FIO shelf cruise, summer |
| `FIO_shelf_winter` | FIO shelf cruise, winter |
| `FIO_shelf_spring` | FIO shelf cruise, spring |
| `FIO_shelf_fall` | FIO shelf cruise, fall |
| `FIO_reef_summer` | FIO reef cruise, summer |
| `FIO_reef_winter` | FIO reef cruise, winter |
| `FIO_reef_spring` | FIO reef cruise, spring |
| `FIO_reef_fall` | FIO reef cruise, fall |

### 4.5.2 StudyComponent

| Value | Phase | Description |
|-------|-------|-------------|
| `depm` | I | Daily Egg Production Method analyses |
| `acoustics` | I | Acoustics targeted study |
| `stable_isotopes` | I | Stable isotope targeted study |
| `benthic_mapping` | I | Benthic habitat mapping targeted study |
| `fall_shelf_time_series` | II, III | Founding fall time series (SEAMAP + FIO_shelf_fall) |
| `metabarcoding` | II | Test of metabarcoding methods |
| `seasons_shelf_time_series` | III | Seasonal shelf sampling (TS1) |
| `seasons_reef_time_series` | III | Seasonal reef sampling (TS2) |
| `winter_mocness` | III | 2012 MOCNESS depth study (TS3) |
| `barcoding_success` | III | Barcoding success study with multiple primers (TS4) |

### 4.5.3 FailReason

| Value | Description |
|-------|-------------|
| `NotEnoughBP` | Sequence too short; not enough base pairs (BOLD requires ≥80 bp) |
| `NoMatch` | No species-level match in BOLD or GenBank |
| `LowPercentID` | Best match is below the 97% acceptance threshold (SOP 3, Section 3.9) |
| `PCRFail` | PCR amplification failed (no band on the gel) |
| `InvertebrateMatch` | Sequence matched an invertebrate (e.g., squid) |
| `Unknown` | The egg failed, but the cause is not known |

### 4.5.4 Phase

Phases are written as Roman numerals in text and stored as integers in the
database.

| Value | Name | Period of performance |
|-------|------|-----------------------|
| `1` | SHELF Phase I | 2017–2018 |
| `2` | SHELF Phase II | 2019–2022 |
| `3` | SHELF Phase III | February 1, 2023 – July 31, 2027 |
| `4` | SHELF Phase IV | TBD |
| `5` | SHELF Phase V | TBD |

### 4.5.5 DNAdb

| Value | Description |
|-------|-------------|
| `BOLD` | Barcode of Life Data System |
| `GenBank` | NCBI GenBank nucleotide database (searched with BLAST) |

---

## 4.6 QA/QC procedures

### 4.6.1 Automated QA/QC (R scripts)

All data submitted for import are run through an automated QA/QC validation
script before any records are added. The scripts:

- check that all required fields are filled in
- check that foreign keys (e.g., TransectID, ScientificName) match existing
  database records
- check that controlled-vocabulary fields contain only approved values
- flag duplicate records
- report every problem in a single pass. **Nothing is imported if any row
  fails.**

The QA/QC scripts are kept in the `qaqc/` folder of the SHELF-DB GitHub
repository.

### 4.6.2 Manual QA/QC (expert review of identifications)

The PI also reviews sequence data by hand. This review is a data-management
step: it happens after the barcoding lab submits its files. SOP 3 points to
this section.

- Each species identification is checked for plausibility against FishBase,
  the World Register of Marine Species (WoRMS), and the peer-reviewed
  literature, with attention to known distributions in the Gulf of Mexico
  and western Atlantic.
- Identifications flagged as possible misidentifications (e.g., Indo-Pacific
  species) are reviewed and removed if confirmed wrong.

### 4.6.3 Data backup

- The live database (`SHELF_DB_WORK.accdb`) is stored on OneDrive, which
  provides continuous cloud backup.
- A dated archive copy is saved in `01_archive/` before every major import.
- R scripts that modify the database are committed to GitHub before and
  after each run.

---

## 4.7 Data archiving and publication

### 4.7.1 GRIIDC submission

At the end of each SHELF phase, all data and metadata are submitted to
GRIIDC (Gulf of Mexico Research Initiative Information and Data Cooperative,
https://data.gulfresearchinitiative.org/) for long-term archiving. Under the
Phase III award terms, data are due within 90 days of the end of the period
of performance. Phase III ends July 31, 2027, so data are due by
**October 29, 2027**.

The submission includes:
- database tables exported as CSV files
- dataset metadata, entered through GRIIDC's dataset submission form
- the SHELF SOPs (SOPs 1–4)
- all R scripts from the SHELF-DB GitHub repository

### 4.7.2 Metadata

SHELF metadata come from three sources:
- **GRIIDC dataset submission**: project purpose, sampling design,
  geographic and temporal extent, and personnel are entered in GRIIDC's
  submission form, which produces the dataset's formal metadata record.
- **`tbl_Metadata`** in the SHELF database: field names, descriptions,
  units, and expected ranges. It is exported with the database tables.
- **The SHELF SOPs**: sampling methods (SOPs 2–3), naming conventions
  (Section 4.2.2), and controlled vocabularies (Section 4.5).

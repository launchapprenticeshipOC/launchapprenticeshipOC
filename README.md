# Apprenticeship Mapping Tools

Single-file, browser-based tools for mapping community college programs and courses to apprenticeship standards, built for regional apprenticeship work with the LAUNCH Apprenticeship Network in Orange County, California.

Every tool is one self-contained `.html` file. There is nothing to install and no build step. Open a file in a browser and it runs.

## What is in this repo

| Tool | What it answers | Main data |
|---|---|---|
| [`CHW_Pathway_Mapping.html`](CHW_Pathway_Mapping.html) | Which Orange County college programs line up with the Community Health Worker standard and related allied health and behavioral health standards? | COCI program export, LAUNCH Standards sheet |
| [`LAUNCH_Apprenticeship_Standards.html`](LAUNCH_Apprenticeship_Standards.html) | What is in the LAUNCH standards, and which colleges are LEAs on them? | LAUNCH Standards sheet |
| [`Saddleback_Course_Flow.html`](Saddleback_Course_Flow.html) | How do Saddleback's automotive courses flow from occupation to skill group to course to module, and how many hours is that? | Saddleback course mapping sheet, module hours, CID form, catalog |
| [`Saddleback_Course_Mapper.html`](Saddleback_Course_Mapper.html) | What happens to program hours and competency coverage if we swap courses or change which occupation counts a course? | Same as the course flow, plus per-competency edits |

## Using the tools

1. Download the `.html` file, or clone the repo.
2. Open the file in a current browser (Chrome, Edge, Firefox, or Safari).
3. To share a live link, turn on GitHub Pages for the repo and link to the file.

Notes:

- Headings and body text use Barlow, loaded from Google Fonts. Offline, the page falls back to Arial Narrow and system fonts.
- Pages follow the viewer's light or dark setting.
- Edits you make in the Course Mapper and the hours builder are saved in your browser's local storage. They stay on your machine and are not sent anywhere.

## The tools

### CHW and Allied Health Pathway Map

Maps college programs to LAUNCH standards by occupation, college, and program, with award type and units.

- **Overview:** a grid of occupations by colleges, with program counts and dots for the program types present.
- **By occupation:** each standard's DAS number, O\*NET and RAPIDS codes, status, and LEA colleges, with its programs listed by college.
- **By college:** everything one college offers, grouped by LAUNCH occupation.
- **Template mode:** load a Smartsheet CSV export for a different pathway. Set the title and the focus occupation in the panel at the bottom of the page.

The sample data covers 13 occupations, 10 Orange County colleges, and 76 programs. Programs that only loosely match an occupation are labeled as a nearest match or a feeder.

### LAUNCH Apprenticeship Standards

A browsable view of the LAUNCH standards sheet.

- **Overview:** one tile per program, grouped by sector, with DAS number and a status bar.
- **By program:** each occupation with its O\*NET and RAPIDS codes, status, progress, and LEA colleges.
- **By LEA college:** every occupation a college is an LEA for.
- **Search and filter:** search by occupation, code, DAS number, or college, and filter by status.

The sample data has 24 programs and 72 occupations. The sector groups are for navigation only and are not in the sheet.

### Saddleback Course Flow
Traces every automotive competency from occupation to skill group to course to module.

- **Live view:** skill groups on the left and an animated Sankey on the right. Every change redraws the chart.
- **Course flow:** a Sankey chart. Select any node to trace its path and list its competencies.
- **Course path:** courses grouped by module, with hours.
- **Hours builder:** switch courses on or off against a target, with prerequisite warnings and a count of competencies left without a course. Presets cover the module pivot as given, the CID form as submitted, and combinations that reach a target.
- **All competencies:** a filterable list of every competency.

Courses flagged as added are the ones in the module pivot that are not on the CID form.

How it counts:

- **Skill groups stay with their occupation.** They cannot be moved.
- **Courses are assigned to one occupation** in the course ledger, and a course's hours count once, under that occupation. Unassigned courses are not counted. Hours by occupation therefore always add up to the program total.
- **Hours are units times 18**, which reproduces the figures in the module pivot.
- **Replace in every group** controls how far a course swap reaches. Off, it changes only the group you clicked. On, it changes every group that uses the course. Per-competency edits on the Competencies tab always act on the competencies you picked.
- **Replacing or mapping a course** assigns it to the group's occupation if it was unassigned. **Removing** a course from its last group unassigns it.

Exports:

- **Sheet CSV** keeps the sheet's five columns, with the revised course for each competency.
- **Course list CSV** has the CID form's fields: course code, title, occupation, and total course hours.

## Data and file formats

The sample data in each tool is a snapshot of Smartsheet sheets and documents from fall 2026. To refresh it, export the sheet from Smartsheet with File, Export, Export sheet to CSV, then load the CSV using the file input in the tool's notes section.

**CHW and Allied Health Pathway Map** expects these columns:

`College`, `Pathway`, `Control Number`, `Program`, `Award`, `Units`, `LAUNCH Standard`, `O*NET Code`, `RAPIDS Code`, `Occupation`

Optional columns:

`Relationship` (Nearest match, Feeder, or Pending COCI), `Standard Status`, `Standard LEAs`, `Occupation Note`

Rows with a blank `Occupation` are left out of the visual. Fill `Standard Status`, `Standard LEAs`, and `Occupation Note` once per occupation, on its first row.

**Saddleback Course Flow and Course Mapper** expect these columns:

`Occupation`, `Occupational Skills`, `Competency #`, `Competency`, `Course`

Put cross-listed courses in one cell, such as `AUTO 105/107`. Both A and B courses are separate courses, for example `AUTO 104A` and `AUTO 104B`. A cell of `N/A - On-the-Job Training` marks a competency taught on the job.

## Adding a pathway

1. Add a row per program, or per competency, to the matching Smartsheet and fill the columns above.
2. Export the sheet as CSV.
3. Open the tool and load the CSV.
4. Set the title and the focus occupation where the tool offers it.

To start from the existing sheets, use Save as Template in Smartsheet so the columns and dropdowns carry over.

## Design conventions

All tools follow the LAUNCH design board:

- **Palette:** LAUNCH Sky `#29AAE1`, LAUNCH Blue `#247EB2`, LAUNCH Deep Blue `#1F4171`, CCC Navy `#032F6E`, and LAUNCH Orange `#FAAB1A`. Orange and sky are used as fills, not as text on white.
- **Type:** Barlow Condensed Bold for headlines and Barlow for body text.
- **Gradient:** the wordmark gradient is used only as a thin band.
- **Logos:** the tools do not reproduce the LAUNCH wordmark or the California Community Colleges logo. Add the official logo file on white where you need it.

## Adding a new tool

- Keep it to one HTML file with no dependencies, so it opens by double-clicking.
- Reuse the palette, fonts, and light and dark theme variables above.
- Read and write CSV in the sheet's column layout so work moves cleanly between the tool and Smartsheet.
- Keep keyboard access working. Nodes and controls should be reachable with Tab and activated with Enter or Space.
- Add a short section to this README with the tool's purpose, views, and data columns.

## Known limits

- The sample data is a point-in-time snapshot and does not update on its own.
- AUTO 208 appears in the module pivot and the sheet but not in the Saddleback catalog page used for course units. Its 3 units come from the pivot.
- LEA names and sector groupings in the standards tool come from the sheet as read, and sector groups are an organizing aid.

## Before you publish the repo

The sample data embedded in these files comes from Smartsheet sheets and internal documents. Before making the repo public, confirm that sharing the standards, course mappings, and program lists is permitted, or keep the repo private. Do not commit Smartsheet links, contact details, or exports with names and emails.

## License

Add a license here before sharing the repo.

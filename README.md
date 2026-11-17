# LAUNCH Apprenticeship OC: Mapping Tools

Browser-based tools for mapping community college programs and courses to apprenticeship standards. They support regional apprenticeship work with the LAUNCH Apprenticeship Network in Orange County, California.

Each tool is one self-contained `index.html` file in its own folder. There is nothing to install and no build step.

## The tools

Live pages are published with GitHub Pages at `https://launchapprenticeshipoc.github.io/launchapprenticeshipOC/`.

| Tool | Live page | What it does |
|---|---|---|
| Saddleback Course Mapper | [`Saddleback/AutomotiveAIXR/`](https://launchapprenticeshipoc.github.io/launchapprenticeshipOC/Saddleback/AutomotiveAIXR/index.html) | Maps Saddleback's automotive courses to occupations and competencies, and shows how program hours change when you swap courses or change which occupation counts a course. |
| CHW and Allied Health Pathways | [`CHWPathways/`](https://launchapprenticeshipoc.github.io/launchapprenticeshipOC/CHWPathways/index.html) | Matches Orange County college programs to the Community Health Worker standard and related allied health and behavioral health standards. |
| DAS Approved Standards | [`DASapprovedStandards/`](https://launchapprenticeshipoc.github.io/launchapprenticeshipOC/DASapprovedStandards/index.html) | Browses the LAUNCH apprenticeship standards by program, occupation, and LEA college. |
| Production Technician Pathway Planner | [`ProductionTech/Saddleback_Starfish/`](https://launchapprenticeshipoc.github.io/launchapprenticeshipOC/ProductionTech/Saddleback_Starfish/index.html) | Plans course pathways for the Production Technician apprenticeship at Saddleback, checked against the standards' competencies. |

## Repo layout

```
launchapprenticeshipOC/
├── Saddleback/
│   └── AutomotiveAIXR/
│       └── index.html            Saddleback Course Mapper
├── CHWPathways/
│   └── index.html                CHW and allied health pathway map
├── DASapprovedStandards/
│   └── index.html                LAUNCH apprenticeship standards
└── ProductionTech/
    └── Saddleback_Starfish/
        └── index.html            Production Technician pathway planner
```

## Using the tools

- **Online:** open any live page above.
- **Locally:** clone the repo and open a tool's `index.html` in a current browser (Chrome, Edge, Firefox, or Safari).
- **Fonts and theme:** headings and body text use Barlow, loaded from Google Fonts. Offline, pages fall back to Arial Narrow and system fonts. Pages follow the viewer's light or dark setting.
- **Saved edits:** edits in the Course Mapper are saved in your browser's local storage. They stay on your machine and are not sent anywhere.

## Saddleback Course Mapper

Skill groups stay with their occupation. The tool lets you decide which courses teach which competencies, and which occupation counts each course's hours.

Tabs:

- **Live view:** skill groups on the left and an animated Sankey chart on the right. Every change redraws the chart.
- **Course mapper:** the same editing with a full panel of totals and a course ledger.
- **Sankey flow:** the chart at full size, with a competency list for the selected node. The last column shows which occupation counts each course.
- **Competencies:** set the course for each competency on its own, or tick several and apply a course to all of them.

How it counts:

- **Skill groups cannot be moved** between occupations.
- **A course counts once,** under the occupation you assign it to in the course ledger. Unassigned courses are not counted, so hours by occupation always add up to the program total.
- **Hours are units times 18.** AUTO 104A and 104B are separate 5-unit, 90-hour courses.
- **Replace in every group** controls how far a course swap reaches. Off, it changes only the group you clicked. On, it changes every group that uses the course. Edits on the Competencies tab always act on the competencies you picked.
- **Replacing or mapping a course** assigns it to the group's occupation if it was unassigned. **Removing** a course from its last group unassigns it.

Exports:

- **Sheet CSV** keeps the sheet's five columns, with the revised course for each competency.
- **Course list CSV** has the fields of the Curriculum Identification Form: course code, title, occupation, and total course hours.

## CHW and Allied Health Pathways

Maps college programs to LAUNCH standards by occupation, college, and program, with award type and units.

- **Overview:** a grid of occupations by colleges, with program counts and dots for the program types present.
- **By occupation:** each standard's DAS number, O\*NET and RAPIDS codes, status, and LEA colleges, with its programs listed by college.
- **By college:** everything one college offers, grouped by LAUNCH occupation.
- **Template mode:** load a Smartsheet CSV export for a different pathway, then set the title and the focus occupation.

Programs that only loosely match an occupation are labeled as a nearest match or a feeder.

## DAS Approved Standards

A browsable view of the LAUNCH apprenticeship standards.

- **Overview:** one tile per program, grouped by sector, with its DAS file number and a status bar.
- **By program:** each occupation with its O\*NET and RAPIDS codes, status, progress, and LEA colleges.
- **By LEA college:** every occupation a college is an LEA for.
- **Search and filter:** search by occupation, code, DAS number, or college, and filter by status.

Sector groups are an organizing aid and are not in the source sheet.

## Production Technician Pathway Planner

An interactive planner for the Production Technician apprenticeship at Saddleback, built on the program standards (DAS file 99764, LAUNCH Industrial Technology & Manufacturing).

- Shows alternate course pathways for an incumbent-worker plan across Advanced Manufacturing, Graphic Communication, and Electronic Technology.
- A pathway is valid as long as it meets the standards' competency checklist. The standards' sample related instruction courses are a guide only.

## Data and file formats

Sample data in each tool is a snapshot of Smartsheet sheets and program documents from fall 2026. To refresh it, export the sheet from Smartsheet with File, Export, Export sheet to CSV, then load the CSV using the file input in the tool's notes section.

**CHW and Allied Health Pathways** expects these columns:

`College`, `Pathway`, `Control Number`, `Program`, `Award`, `Units`, `LAUNCH Standard`, `O*NET Code`, `RAPIDS Code`, `Occupation`

Optional columns: `Relationship` (Nearest match, Feeder, or Pending COCI), `Standard Status`, `Standard LEAs`, `Occupation Note`.

Rows with a blank `Occupation` are left out of the visual. Fill `Standard Status`, `Standard LEAs`, and `Occupation Note` once per occupation, on its first row.

**Saddleback Course Mapper** expects these columns:

`Occupation`, `Occupational Skills`, `Competency #`, `Competency`, `Course`

Put cross-listed courses in one cell, such as `AUTO 105/107`. A and B courses are separate courses, such as `AUTO 104A` and `AUTO 104B`. A cell of `N/A - On-the-Job Training` marks a competency taught on the job.

## Adding a pathway or a tool

- **New pathway in an existing tool:** add rows to the matching Smartsheet, export it as CSV, and load it in the tool. Use Save as Template in Smartsheet to carry the columns and dropdowns over.
- **New tool:** create a folder and put the tool in one `index.html` with no dependencies, so it opens by double-clicking and works on GitHub Pages.
- Reuse the palette, fonts, and light and dark theme variables below.
- Read and write CSV in the sheet's column layout so work moves cleanly between the tool and Smartsheet.
- Keep keyboard access working: controls reachable with Tab and activated with Enter or Space.
- Add a section to this README with the tool's purpose, views, and data columns.

## Design conventions

All tools follow the LAUNCH design board:

- **Palette:** LAUNCH Sky `#29AAE1`, LAUNCH Blue `#247EB2`, LAUNCH Deep Blue `#1F4171`, CCC Navy `#032F6E`, and LAUNCH Orange `#FAAB1A`. Orange and sky are used as fills, not as text on white.
- **Type:** Barlow Condensed Bold for headlines and Barlow for body text.
- **Gradient:** the wordmark gradient is used only as a thin band.
- **Logos:** the tools do not reproduce the LAUNCH wordmark or the California Community Colleges logo. Add the official logo file on white where you need it.

## Known limits

- Sample data is a point-in-time snapshot and does not update on its own.
- AUTO 208 appears in the module pivot and the sheet but not on the Saddleback catalog page used for course units. Its 3 units come from the pivot.
- LEA names and sector groupings come from the sheets as read.

## Published data

Everything embedded in these pages is visible to anyone with the link. Keep Smartsheet links, contact details, and names of individual employees or apprentices out of the files.

## License

Add a license here before sharing the repo widely.

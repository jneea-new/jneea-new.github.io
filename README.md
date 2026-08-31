# New JNEEA web site using Hugo on GitHub 

After an earlier, aborted attempt (in 2024) to transition our existing Drupal website to a GitHub based solution using the Jekyll framework,
we start a new attempt based on Hugo.

Roadmap:

[X] Step 1: Front Matter Schema & Data Conventions (Finalized)
[ ] Step 2: Individual Paper Template (`layouts/_default/single.html`)
[ ] Step 3: Volume Index Template (`layouts/_default/list.html`)
[ ] Step 4: Base Layout & CSS Integration (`layouts/_default/baseof.html`)
[ ] Step 5: GitHub Repository & Actions Workflow Setup

## Step 1 : JNEEA Content Guidelines & Front Matter Schema

Contents of the journal are organized in volumes YYYY which have "issues" or "numbers" n = 1, 2, 3...

For each issue there is a file `YYYY-N.md` placed under `content/volumes/<YEAR>/`,
e.g., `content/volumes/2026/2026-1.md`.

They have all metadata (cf. below) in the YAML header, and the abstract of the paper as body.

### Metadata Schema (YAML Front Matter) -- Keys & Conventions

Keys *should* be in lowercase, but can and often will be capitalized (e.g. Author:, Received:, ...).
We can/will still query them as .Params.authors, .Params.received, ...

```yaml
MS-Number: String "JNEEA-YYMMDDn" or number YYMMDDn, where 20YY-MM-DD is the submission (= received) date,
  and n = 1, 2, 3... disambiguates multiple submissions received the same day.
Title: String. Full paper title. Normal capitalization: Capitals only for the first word and names. 
      Can use minimal HTML or Unicode if necessary for math.
Author(s): Can be a string or list of strings or mappings. If a string has " and " inside, 
  split there to get a list of authors [possibly in format "Doe, John and Ellen, Sue"], 
  which then can have one or multiple common **address(es)/affiliation(s)**.
  These may be given following a ":" as value of this mapping (string or number or list), 
  or on a subsequent "Address" line. Numbers refer to items of "Address", cf. below.
Address (alias: Affiliation(s)): String or mapping or list of strings or mappings, 
  for one or more affiliations. If more than one, they are displayed as a numbered or unnumbered list,
  depending on whether numbers were used in the "Author(s)" section to refer to Affiliations.
Email: String or list of strings: If a single one, it is that of the corresponding author;
  if multiples, probably one per author. Only used internally, not shown on the web site (but maybe in the PDF). 
Received: Date (YYYY-MM-DD) or String.
Revised: Date (YYYY-MM-DD), List of Dates/Strings, or String.
Accepted: Date (YYYY-MM-DD) or custom descriptive String (e.g., "conditionally `<DATE>`, final version `<DATE>`").
Published: Date (YYYY-MM-DD) or String.
Volume: Integer 20YY with YY = 00..99
Number: Integer N = 1, 2, 3...
Pages: String, e.g., "1-18" (can be entered without quotes: 1-18)
PDF (alias: File, Filename): String. Path relative to static directory (e.g., "papers/2026/2026-1.pdf").
MSC: List of Strings, e.g.: 12A34 56X87
Keywords: String or list of strings, e.g.: Evolution equation, quantum computer.
  Will usually by printed as is, but if it is a single string that has a ";",
  this is the list element separator; if it hasn't a ";" but a ",", then this is the separator.
  To enter a single key phrase containing a ",", it must be given as list, i.e.,
  in [...] or on a subsequent line starting with "- ".
```

At the URL `/<YEAR>/`, a list of all issues/"numbers" will be available, of the form
  1. A. U. Thor, N. Otherone: Title, vol. YYYY, n° N, (YYYY), pp. x--y: View Abstract - [Download PDF [xxx KB]]
  2. ...

### Examples
```yaml
MS-Number: JNEEA-2608201
Title: Our nice paper
Authors: { Jane Doe and John Smith: 1, Gaston Lagaffe: [1,2] }
Address:
  1: Department of Mathematics, University A, Country
  2: Institute of Advanced Trouble, U.S.A.
Email: jdoe@univ-a.edu
Received: August 20, 2026
Revised: September 1, 2026
Accepted: conditionally August 30, 2026, final version Sept. 2, 2026
Published: 2026-09-15
Volume: 2026
Number: 9
Pages: 111-118
PDF: JNEEA-vol.2026-no.1.pdf
MSC: 12A34 56X87
Keywords: Evolution equation, quantum computer.
```

MSC Numbers in Quotes: Quotes are not mandatory for standard MSC codes containing letters (e.g., 35K55). 
However, YAML automatically interprets purely numerical inputs (like 42005) as integers. 
Using plain strings without quotes works fine as long as our script formats them consistently.

## Step 2: Individual Paper Template (`layouts/_default/single.html`)
see there.

## Step 3: Volume Index Template (`layouts/_default/list.html`)

## Step 4: Base Layout & CSS Integration (`layouts/_default/baseof.html`)

## Step 5: GitHub Repository & Actions Workflow Setup

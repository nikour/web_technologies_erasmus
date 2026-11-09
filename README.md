# Fingerprint pool

Shared dataset for **Web Technologies, Homework 1 (fingerprinting)**.

Fingerprinting is about *populations*: one machine is one data point, and uniqueness, entropy and anonymity sets only make sense over many users. Together you build a small dataset of fonts and canvas renders from many different browsers, and later analyse it (Task 4 of the homework).

**Data deadline: 17 November.** This is only the deadline for putting your data files here, so that everybody can start working with the pooled data. It is **not** the homework deadline.

## What to collect

Two single-file tools, in [`tools/`](tools/). Everybody runs exactly the same test, so results from different machines can be compared.

| Tool | What it does | What you get |
|---|---|---|
| [`fonts_capture.html`](tools/fonts_capture.html) | Checks a fixed list of 353 candidate fonts and finds out which ones your browser can use. | a **JSON** file with the list of installed font families |
| [`canvas_capture.html`](tools/canvas_capture.html) | Draws one fixed picture (text, emoji, gradient, curves, ...) on a canvas. | a **PNG** image of what your browser rendered |

The tools deliberately **do not compute hashes**. The font list and the image are the data; hashing and comparing them is part of your analysis.

### How to run a tool

1. Open the HTML file in a browser: double-click it, or serve the folder (`python -m http.server 8000`) and open `http://localhost:8000/tools/fonts_capture.html`.
2. Fill in your **nickname** (not your real name), **browser and version** and **operating system**. Browser and OS are pre-filled from your browser; check them. Leave **setting** at `default`.
3. The font tool runs by itself. The canvas tool draws immediately.
4. Click **Save**. Your browser downloads the file. If it asks whether to allow downloads, allow.

Do this in **every browser you have installed** (Chrome, Edge, Firefox, Safari, Opera, Vivaldi, Brave, Tor Browser, Mullvad Browser, ...). One file of each kind per browser. Run each browser with its normal, default settings.

If a protection hides something (a blank canvas, almost no fonts), **that is a valid result**: save it anyway.

## Where the files go

```
web_technologies_erasmus/
├── README.md
├── tools/                 the two capture tools (do not edit)
├── data/
│   ├── fonts/             fonts__<nick>__<browser>__<os>__<setting>.json
│   └── canvas/            canvas__<nick>__<browser>__<os>__<setting>.png
└── analysis/              your scripts and notebooks (after the deadline)
```

Example file names:

```
data/fonts/fonts__fox42__firefox-159__windows11__default.json
data/canvas/canvas__fox42__firefox-159__windows11__default.png
```

The tools build the file names for you. **Do not rename the files.**

## How to contribute

You will be added as a collaborator. Then:

```bash
git clone https://github.com/nikour/web_technologies_erasmus.git
cd web_technologies_erasmus
# copy your downloaded files into data/fonts/ and data/canvas/
git add data
git commit -m "Add fonts and canvas data from <nickname>"
git pull --rebase
git push
```

Because every file name contains your nickname, you will not clash with other people's files.

## Rules

- **Nickname only.** No real names, e-mail addresses or other personal data in files or commit messages.
- Run the tools only on **your own devices**, or on someone else's **with their permission**. Share only what you are comfortable sharing: a font list and a canvas image *are* fingerprints.
- **One file set per browser.** Add your own files only: do not edit, rename or delete other people's.
- Files must be in the repository by **17 November**. After that the dataset is **frozen**: everybody analyses the same data.
- The data describes your classmates' devices. Use it for this course only; do not publish it or share it outside the group.

## What is inside the files

**Fonts JSON** (`data/fonts/*.json`)

| Field | Meaning |
|---|---|
| `nick`, `browser`, `os`, `setting`, `notes` | what you entered |
| `installed` | the font families your browser could use (this is the data) |
| `testedByGroup` | the full candidate list, in groups (`windows`, `office`, `macos`, `linux_open`, `design_tex`, `international`), so you can build subsets |
| `testedCount`, `foundCount` | how many fonts were tested and found |
| `stableBetweenRuns`, `passesNeeded` | whether repeated measurements agreed |
| `listVersion`, `userAgent`, `date`, `detectionMs` | context |

**Canvas PNG** (`data/canvas/*.png`): the rendered 460 x 140 image. Nickname, browser, OS and setting are in the file name.

## Analysis (after the deadline)

Put your scripts in `analysis/` (for example one subfolder per person). The homework brief lists the questions to answer: how many distinct font lists, anonymity sets, entropy, how many fonts you need, pixel differences between canvas images, and whether you can link two browsers of the same person.

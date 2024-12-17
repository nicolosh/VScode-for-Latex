# VScode for Latex
How to install `Latex` for `VScode` on any Operative System (O.S) with no need of installing `perl` or `latexmk`:  

***

- *Install VScode*  
  https://code.visualstudio.com/

- *Install LaTeX Workshop*  
  Install LaTeX Workshop extension inside VScode by clicking **`Ctrl + Shift + X`** and typing **`LaTeX Workshop`** inside the market place extensions search bar or directly go [here](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) and click onto the green button **`Install`**  

- *Install MikTex depending on the O.S you have installed on your machine*  
  https://miktex.org/download 
 
***

## Compiling
Press **`Ctrl + Shift + P`** then click *`LaTeX Workshop: Build with Recipe`* and finally click further on **`pdflatex -> bibtex -> pdflatex * 2`**.

In order to compile correctly using `VScode` do as follows
1. Open *`settings.json`* by pressing **`Ctrl + Shift + P`** and then clicking on *`Preferences: Open User Settings (JSON)`*.  

2. Then write down the following code inside the *`settings.json`* file:  
```json
"latex-workshop.latex.tools": [  
    {
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
        ],
        "command": "pdflatex",
        "name": "pdflatex"
    },
    {
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
        ],
        "command": "xelatex",
        "name": "xelatex"
    },
    {
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "-pdf",
            "-outdir=%OUTDIR%",
            "%DOC%"
        ],
        "command": "latexmk",
        "name": "latexmk"
    },
    {
        "args": [
            "%DOCFILE%"
        ],
        "command": "bibtex",
        "name": "bibtex"
    },
    {
        "args": [
            "%DOCFILE%"
        ],
        "command": "biber",
        "name": "biber"
    }
],
"latex-workshop.latex.recipes": [
    {
        "name": "latexmk",
        "tools": [
            "latexmk"
        ]
    },
    {
        "name": "latexmk -> bibtex -> latexmk*2",
        "tools": [
            "latexmk",
            "bibtex",
            "latexmk",
            "latexmk"
        ]
    },
    {
        "name": "latexmk -> biber -> latexmk*2",
        "tools": [
            "latexmk",
            "biber",
            "latexmk",
            "latexmk"
        ]
    },
    {
        "name": "pdflatex",
        "tools": [
            "pdflatex"
        ]
    },
    {
        "name": "pdflatex -> bibtex -> pdflatex*2",
        "tools": [
            "pdflatex",
            "bibtex",
            "pdflatex",
            "pdflatex"
        ]
    },
    {
        "name": "pdflatex -> biber -> pdflatex*2",
        "tools": [
            "pdflatex",
            "biber",
            "pdflatex",
            "pdflatex"
        ]
    },
    {
        "name": "xelatex",
        "tools": [
            "xelatex"
        ]
    },
    {
        "name": "xelatex -> bibtex -> xelatex*2",
        "tools": [
            "xelatex",
            "bibtex",
            "xelatex",
            "xelatex"
        ]
    },
    {
        "name": "xelatex -> biber -> xelatex*2",
        "tools": [
            "xelatex",
            "biber",
            "xelatex",
            "xelatex"
        ]
    },
    {
        "name": "bibtex",
        "tools": [
            "bibtex"
        ]
    },
    {
        "name": "biber",
        "tools": [
            "biber"
        ]
    },
],
// Fix citation warnings in editor when using biber (wavy lines).
"latex-workshop.intellisense.citation.backend": "biblatex",
// Set bibliography indentation to four spaces (default: two).
"latex-workshop.bibtex-format.tab": "4 spaces",
// Avoid building PDF every time a file is modified or saved.
"latex-workshop.latex.autoBuild.run": "never",
// Sync PDF with cursor position after compiling.
"latex-workshop.synctex.afterBuild.enabled": true,
// Automatically choose last used recipe on next build.
"latex-workshop.latex.recipe.default": "lastUsed",
```

3. Open *`keybindings.json`* by pressing **`Ctrl + Shift + P`** and then clicking on *`Preferences: Open Keyboard Shortcuts (JSON)`*.  

*Write the following code inside the `keybindings.json` file*:  
```json
// Place your key bindings in this file to override the defaults
[
    // click on ctrl+s to rebuild the project for getting the pdf version of your latex document
    {
        "key": "ctrl+s",
        "command": "latex-workshop.build",
        "when": "!config.latex-workshop.bind.altKeymap.enabled && !virtualWorkspace && editorLangId =~ /^latex$|^latex-expl3$|^rsweave$|^jlweave$|^pweave$/"
    },
    // click on the pdf to visualize and refresh the page clicking alt+enter
    { 
        "key": "alt+enter",
        "command": "latex-workshop.refresh-viewer"
    },
    {
        "key": "ctrl+l c",
        "command": "latex-workshop.citation"
    },
    {
        "key": "ctrl+l escape",
        "command": "latex-workshop.kill"
    },
    {
        "key": "ctrl+l x",
        "command": "workbench.view.extension.latex-workshop-activitybar",
        "when": "!config.latex-workshop.bind.altKeymap.enabled"
    },
]
```
___

### Compiling issue
If the following error shows up in the log *`Please (re)run Biber on the file: output and rerun LaTeX afterwards.`*, then you need to run `biber documentname` command in the terminal without the tex extension. 
Finally, you need to rerun *`LaTeX`* by pressing the combination of keys as chosen inside the *`keybindings.json`* (i.e.*`ctrl+s`*) on the *`documentname.tex`* file or performing the following ordered list of operations such
- Click on **`Ctrl + Shift + P`**
- Select *`LaTeX Workshop: Build with recipe`*
- Select **`pdflatex -> bibtex -> pdflatex * 2`**

___    


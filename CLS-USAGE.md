# Hebrew Academic Template CLS – Usage Guide
## Complete Instructions for Writing Mixed Hebrew-English Documents

**Document Class:** `hebrew-academic-template.cls`
**LaTeX Engine:** LuaLaTeX (required)
**Distribution:** MiKTeX or TeX Live
**Author:** Dr. Yoram Segal

---

## Table of Contents

1. [System Requirements](#system-requirements)
2. [Quick Start](#quick-start)
3. [Document Structure](#document-structure)
4. [Language Mixing](#language-mixing)
5. [Text Direction Rules](#text-direction-rules)
6. [CLS Functions Reference](#cls-functions-reference)
7. [Tables with RTL Support](#tables-with-rtl-support)
8. [Python Code Blocks](#python-code-blocks)
9. [Special Characters](#special-characters)
10. [Mathematical Expressions](#mathematical-expressions)
11. [Bibliography](#bibliography)
12. [Troubleshooting](#troubleshooting)

---

## System Requirements

### Required Software
- **LaTeX Engine:** LuaLaTeX (not pdflatex or xelatex)
- **Distribution:** MiKTeX (Windows) or TeX Live (Linux/Mac)
- **Document Class:** `hebrew-academic-template.cls` (must be in project directory)

### Font Requirements
The CLS uses smart font fallback:
- **Windows/MiKTeX:** Times New Roman (English), David CLM (Hebrew), Courier New (code)
- **Linux/TeX Live:** Latin Modern Roman (English), DejaVu Sans (Hebrew), DejaVu Sans Mono (code)

---

## Quick Start

### Minimal Document Template

```latex
% !TEX program = lualatex
% !TEX encoding = UTF-8

\documentclass{hebrew-academic-template}

% Bibliography
\addbibresource{global.bib}

% Document metadata
\hebrewtitle{כותרת המסמך בעברית}
\englishtitle{English Document Title}
\hebrewauthor{ד"ר יורם סגל}
\date{\texthebrew{ספטמבר} \textenglish{2025}}

\begin{document}

\maketitle

\tableofcontents

\newpage

\hebrewsection{פרק ראשון}

טקסט עברי עם מונח אנגלי \en{Machine Learning} בתוכו.

\hebrewsubsection{תת-פרק}

עוד טקסט עברי...

\printenglishbibliography

\end{document}
```

### Compilation Commands

```bash
# Full compilation with bibliography
lualatex document.tex
biber document
lualatex document.tex
lualatex document.tex

# Quick compilation (no bibliography changes)
lualatex document.tex
```

---

## Document Structure

### Title Page

```latex
\hebrewtitle{כותרת עברית}
\englishtitle{English Title}
\hebrewauthor{ד"ר יורם סגל}
\date{\texthebrew{אוקטובר} \textenglish{2025}}

\begin{document}
\maketitle
```

### Sections and Subsections

```latex
% Hebrew section (RTL)
\hebrewsection{מבוא: רקע היסטורי}

% Hebrew subsection (RTL)
\hebrewsubsection{מושגי יסוד}

% English section (LTR) - rare, use only if entire section is English
\englishsection{Background: Historical Context}
```

**Important:** Section numbers are always LTR (left-to-right), even in Hebrew sections.

---

## Language Mixing

### Inline English in Hebrew Text

```latex
% Short English terms
בפרק זה נלמד על \en{Machine Learning} ו\en{-Deep Learning}.

% English with Hebrew explanation
האלגוריתם \en{Gradient Descent} משתמש בנגזרת.

% Multiple English words
שיטת \en{K-Nearest Neighbors (KNN)} היא אלגוריתם פשוט.
```

### Inline Hebrew in English Sections (rare)

```latex
\startenglish
This section discusses the concept of \heb{מתאם} (correlation).
\stopenglish
```

### Numbers in Hebrew Text

```latex
% Always use \num{} for numbers in Hebrew text
הדגימה כוללת \num{1000} נקודות.
הדיוק הוא \num{0.95} או \percent{95}.

% Years
בשנת \hebyear{1801}, גאוס פיתח את שיטת הריבועים הפחותים.
```

---

## Text Direction Rules

### Golden Rules

1. **Hebrew text:** Always RTL (right-to-left)
2. **English text:** Always LTR (left-to-right)
3. **Numbers:** Always LTR, even in Hebrew text (use `\num{}`)
4. **Math formulas:** Always LTR (automatic in `$ $` or `\begin{equation}`)
5. **Code blocks:** Always LTR (automatic in `pythonbox` environments)
6. **Page numbers:** Always LTR (automatic)
7. **Section numbers:** Always LTR (automatic)

### Text Direction Functions

| Function | Purpose | Example |
|----------|---------|---------|
| `\en{text}` | English in Hebrew context | `למידה באמצעות \en{Supervised Learning}` |
| `\heb{text}` | Hebrew in English context (rare) | `The \heb{מתאם} coefficient` |
| `\LTR{text}` | Force LTR direction | `\LTR{ABC-123}` |
| `\RTL{text}` | Force RTL direction | `\RTL{טקסט עברי}` |

---

## CLS Functions Reference

### Language and Text Direction

```latex
\en{English text}              % English in Hebrew context
\heb{Hebrew text}              % Hebrew in English context (rare)
\ilm{Inline LTR text}          % Inline math/English terms
\LTR{Force LTR}                % Force left-to-right
\RTL{Force RTL}                % Force right-to-left
\textenglish{English}          % Polyglossia English
\texthebrew{Hebrew}            % Polyglossia Hebrew
```

### Numbers and Formatting

```latex
\num{123}                      % Numbers (always LTR)
\num{0.95}                     % Decimal numbers
\percent{80}                   % Percentages (80%)
\hebyear{2025}                 % Years in Hebrew text
```

### Special Characters (Important!)

```latex
% ❌ NEVER use these directly in Hebrew text:
R²                             % NOT SUPPORTED in David CLM font
→                              % NOT SUPPORTED
©                              % NOT SUPPORTED

% ✅ ALWAYS use CLS commands instead:
\Rsquared{}                    % R² (math mode)
\Rtwo{}                        % R² (text mode alternative)
\rarrow{}                      % Logical arrow in Hebrew RTL (←)
\textenglish{©}                % Copyright symbol
$\neq$                         % Not equal (≠)
```

### Sections

```latex
\hebrewsection{Hebrew Title}   % Hebrew section with LTR number
\hebrewsubsection{Hebrew}      % Hebrew subsection
\englishsection{English}       % English section (rare)
```

### Lists

```latex
% Hebrew itemize
\begin{itemize}
\item פריט ראשון
\item פריט שני עם \en{English term}
\end{itemize}

% Hebrew enumerate (numbers are automatic LTR)
\begin{enumerate}
\item פריט ראשון
\item פריט שני
\end{enumerate}
```

### Figures and Images

```latex
\hebrewfigure[htbp]{
  \includegraphics[width=0.8\textwidth]{image.png}
}{כיתוב התמונה בעברית}
```

---

## Tables with RTL Support

### Basic Hebrew Table

```latex
\begin{hebrewtable}[H]
\caption{כותרת הטבלה}
\centering
\begin{rtltabular}{|r|r|r|}
\hline
\textbf{\hebcell{עמודה 1}} & \textbf{\hebcell{עמודה 2}} & \textbf{\hebcell{עמודה 3}} \\
\hline
\num{1} & \num{0.85} & \hebcell{ערך גבוה} \\
\hline
\num{2} & \num{0.72} & \hebcell{ערך בינוני} \\
\hline
\end{rtltabular}
\end{hebrewtable}
```

### Table Functions

| Function | Purpose | Example |
|----------|---------|---------|
| `\hebcell{text}` | Hebrew RTL cell | `\hebcell{טקסט עברי}` |
| `\mixedcell{text}` | Mixed Hebrew-English cell | `\mixedcell{Hebrew \en{English}}` |
| `\num{}` in cells | LTR numbers | `\num{123}` |

### Mixed Content Table Example

```latex
\begin{hebrewtable}[H]
\caption{השוואת אלגוריתמים}
\centering
\begin{rtltabular}{|r|c|c|c|}
\hline
\textbf{\hebcell{אלגוריתם}} & \textbf{\hebcell{דיוק}} & \textbf{\hebcell{זמן}} & \textbf{\hebcell{מורכבות}} \\
\hline
\hebcell{\en{K-NN}} & \num{0.92} & \num{10} \hebcell{שניות} & $O(n)$ \\
\hline
\hebcell{\en{SVM}} & \num{0.95} & \num{30} \hebcell{שניות} & $O(n^2)$ \\
\hline
\end{rtltabular}
\end{hebrewtable}
```

---

## Python Code Blocks

### Floating Code Block (`pythonbox`)

Use for short code blocks that fit on one page:

```latex
\begin{pythonbox}[תיאור הקוד בעברית]
import numpy as np
from sklearn.decomposition import PCA

# Reduce dimensionality
pca = PCA(n_components=2)
X_reduced = pca.fit_transform(X)
\end{pythonbox}
```

### Non-Floating Code Block (`pythonbox*`)

Use for long code blocks that may span multiple pages:

```latex
\begin{pythonbox*}[אלגוריתם \en{Gradient Descent}]
def gradient_descent(X, y, alpha=0.01, max_iters=1000):
    n, d = X.shape
    w = np.zeros(d)

    for iteration in range(max_iters):
        y_pred = X @ w
        gradient = (2/n) * X.T @ (X @ w - y)
        w = w - alpha * gradient

    return w
\end{pythonbox*}
```

### Python Code Block Rules

✅ **Always:**
- Title in **Hebrew RTL** using `[Hebrew title]` parameter
- Code body in **English LTR** (automatic)
- Comments in **English only** (never Hebrew!)
- Titles display in **bold black text** on **light gray background**

❌ **Never:**
- Hebrew comments inside code: `# יצירת מטריצה` ← WRONG
- Hebrew variable names: `מטריצה = np.array([])` ← WRONG
- Mixed RTL/LTR inside code body

### Title Visibility Fix (Recent Update)

The CLS now uses `coltitle=black` to ensure Hebrew RTL titles are visible on gray background.

**Before fix:** White text on light gray = invisible
**After fix:** Black bold text on light gray = visible ✓

### Overflow Prevention

If `pythonbox*` code still overflows into footer:

**Solution:** Simplify code to show ONLY core functions:
- ❌ Remove: Non-core imports (`matplotlib`, `sklearn` examples)
- ❌ Remove: `print` statements, docstrings, example data
- ❌ Remove: Visualization code (UNLESS visualization IS the main topic)
- ✅ Keep: ONLY the core algorithm/function being demonstrated

**Alternative:** Convert to Python pseudocode instead of executable code.

---

## Special Characters

### The Problem

The David CLM Hebrew font does NOT support many Unicode special characters:
- `R²` (superscript 2)
- `→` (rightward arrow)
- `©` (copyright)
- `≠` (not equal)

**Direct use in Hebrew text will cause missing characters or compilation errors.**

### The Solution

Use CLS-provided commands that work around font limitations:

#### R² (R-squared)

```latex
% ❌ WRONG in Hebrew text:
מקדם הקביעה R² הוא מדד לטיב ההתאמה

% ✅ CORRECT:
מקדם הקביעה \Rsquared{} הוא מדד לטיב ההתאמה

% Alternative (text mode):
מקדם הקביעה \Rtwo{} הוא מדד לטיב ההתאמה
```

**Implementation:**
- `\Rsquared{}` uses math mode: `\ensuremath{R^2}`
- `\Rtwo{}` uses superscript: `R\textsuperscript{2}`

#### Arrows in Hebrew RTL

```latex
% ❌ WRONG:
אם $x > 5$ → המודל יחזה \num{1}

% ✅ CORRECT:
אם $x > 5$ \rarrow{} המודל יחזה \num{1}
```

**Explanation:** In Hebrew RTL context, logical "implies" (→) should visually point **left** (←) to maintain reading direction. The `\rarrow{}` command uses `$\leftarrow$` automatically.

#### Copyright Symbol

```latex
% ❌ WRONG:
כל הזכויות שמורות ©

% ✅ CORRECT:
כל הזכויות שמורות \textenglish{©}
```

#### Not Equal Symbol

```latex
% ❌ WRONG:
$x ≠ y$

% ✅ CORRECT:
$x \neq y$
```

### Complete Special Characters Reference

| Character | ❌ Direct | ✅ CLS Command | Notes |
|-----------|----------|----------------|-------|
| R² | `R²` | `\Rsquared{}` | Math mode |
| R² | `R²` | `\Rtwo{}` | Text mode |
| → | `→` | `\rarrow{}` | Points left (←) in Hebrew RTL |
| © | `©` | `\textenglish{©}` | Uses English font |
| ≠ | `≠` | `$\neq$` | Math mode |
| ± | `±` | `$\pm$` | Math mode |
| × | `×` | `$\times$` | Math mode |
| ÷ | `÷` | `$\div$` | Math mode |

---

## Mathematical Expressions

### Inline Math

```latex
% Math is always LTR (automatic)
השונות מוגדרת כ\en{-}$\sigma^2 = E[(X - \mu)^2]$

% Hebrew explanation with math
מקדם הקורלציה $r$ נמצא בטווח $-1 \leq r \leq 1$
```

### Display Math

```latex
% Numbered equation
\begin{equation}
R^2 = 1 - \frac{SS_{\text{res}}}{SS_{\text{tot}}}
\end{equation}

% Unnumbered equation
\[
\mathbf{w} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}
\]
```

### Hebrew Text in Math

```latex
% Use \text{} for English labels
$SS_{\text{res}}$ = sum of squared residuals

% Use \hebmath{} for Hebrew labels (rare)
$x_{\hebmath{ממוצע}}$

% Use \hebsub{} for Hebrew subscripts
$x_{\hebsub{עברי}}$
```

### Math Alignment

```latex
\begin{align}
y &= mx + b \\
\hat{y} &= w_0 + w_1 x \\
\text{MSE} &= \frac{1}{n}\sum_{i=1}^n (y_i - \hat{y}_i)^2
\end{align}
```

---

## Bibliography

### Setup in Main Document

```latex
\documentclass{hebrew-academic-template}

% Add bibliography file
\addbibresource{global.bib}

\begin{document}

% ... document content ...

% Print English bibliography (IEEE style)
\printenglishbibliography

\end{document}
```

### Bibliography File Format (global.bib)

```bibtex
@article{bellman1957,
  author = {Bellman, Richard E.},
  title = {Dynamic Programming},
  year = {1957},
  journal = {Princeton University Press},
  keywords = {english}
}

@book{strang2019,
  author = {Strang, Gilbert},
  title = {Linear Algebra and Learning from Data},
  year = {2019},
  publisher = {Wellesley-Cambridge Press},
  keywords = {english}
}

@article{pearson1896,
  author = {Pearson, Karl},
  title = {Mathematical Contributions to the Theory of Evolution},
  year = {1896},
  journal = {Philosophical Transactions of the Royal Society A},
  volume = {187},
  pages = {253--318},
  keywords = {english}
}
```

**Important:** Add `keywords = {english}` to all English references.

### Citing References

```latex
% In Hebrew text
גאוס פיתח את שיטת הריבועים הפחותים \cite{gauss1809}.

% Multiple citations
שיטות אלו תוארו במחקרים רבים \cite{pearson1896, fisher1925, bellman1957}.
```

### Bibliography Commands

| Command | Purpose |
|---------|---------|
| `\printenglishbibliography` | English references (LTR, left-aligned) |
| `\printhebrewbibliography` | Hebrew references (RTL, right-aligned) |
| `\cite{key}` | Cite a reference |

---

## Troubleshooting

### Compilation Errors

**Error:** `Font "David CLM" not found`
**Solution:** Use TeX Live (Linux) with DejaVu Sans fallback, or install David CLM on Windows

**Error:** `File hebrew-academic-template.cls not found`
**Solution:** Ensure CLS file is in the same directory as your .tex file

**Error:** `Undefined control sequence \hebrewsection`
**Solution:** Make sure you're using `\documentclass{hebrew-academic-template}`

### Text Direction Issues

**Problem:** English text appears backwards
**Solution:** Wrap in `\en{English text}` command

**Problem:** Numbers appear backwards in Hebrew text
**Solution:** Use `\num{123}` instead of direct `123`

**Problem:** Math formulas appear RTL
**Solution:** Math is automatically LTR; check if you're using `$ $` or `\[ \]` correctly

### Code Block Issues

**Problem:** Python code appears RTL
**Solution:** Use `pythonbox` or `pythonbox*` environments (automatic LTR)

**Problem:** Hebrew title invisible on gray background
**Solution:** Update CLS to latest version with `coltitle=black` fix

**Problem:** Code block overflows into footer
**Solution:**
1. Use `pythonbox*` (non-floating) instead of `pythonbox`
2. Simplify code: remove prints, docstrings, examples
3. Keep ONLY core algorithm

### Special Character Issues

**Problem:** `R²` appears as missing character
**Solution:** Use `\Rsquared{}` instead

**Problem:** `→` arrow missing or wrong direction
**Solution:** Use `\rarrow{}` (automatically adjusts for RTL)

**Problem:** `©` copyright missing
**Solution:** Use `\textenglish{©}`

### Table Issues

**Problem:** Hebrew text in table appears LTR
**Solution:** Use `\hebcell{Hebrew text}` for each Hebrew cell

**Problem:** Numbers in table appear RTL
**Solution:** Use `\num{123}` in all cells with numbers

**Problem:** Mixed content doesn't align properly
**Solution:** Use `\mixedcell{Hebrew \en{English}}` for complex cells

### Bibliography Issues

**Problem:** Bibliography doesn't appear
**Solution:** Run full compilation sequence:
```bash
lualatex document.tex
biber document
lualatex document.tex
lualatex document.tex
```

**Problem:** Citation numbers appear RTL
**Solution:** CLS automatically handles this with `\ltrnumber{}` wrapper

**Problem:** Hebrew and English references mixed
**Solution:** Add `keywords = {english}` or `keywords = {hebrew}` to each entry in .bib file

---

## Best Practices

### ✅ Do

- Always use `\en{}` for English terms in Hebrew text
- Always use `\num{}` for numbers in Hebrew text
- Use `\Rsquared{}` instead of `R²`
- Keep Python code comments in English
- Simplify code blocks to avoid overflow
- Use `pythonbox*` for long code (non-floating)
- Add `keywords = {english}` to all bib entries
- Test compilation after major changes

### ❌ Don't

- Mix RTL/LTR manually without CLS commands
- Use direct Unicode special characters (R², →, ©)
- Write Hebrew comments in Python code
- Use `pdflatex` or `xelatex` (must use LuaLaTeX)
- Create overly long code blocks without simplification
- Forget to run `biber` when bibliography changes
- Use direct numbers like `123` in Hebrew text (use `\num{123}`)

---

## Quick Reference Card

### Most Common Commands

```latex
% Language
\en{English}                   % English in Hebrew
\num{123}                      % Numbers

% Sections
\hebrewsection{Title}          % Hebrew section
\hebrewsubsection{Subtitle}    % Hebrew subsection

% Special characters
\Rsquared{}                    % R²
\rarrow{}                      % → (becomes ← in RTL)
\textenglish{©}                % ©

% Code
\begin{pythonbox}[Title]       % Short code
\begin{pythonbox*}[Title]      % Long code (non-floating)

% Tables
\begin{hebrewtable}[H]         % Hebrew table
\hebcell{Hebrew}               % RTL cell

% Math
$formula$                      % Inline math (auto LTR)
\begin{equation}               % Display math

% Bibliography
\cite{key}                     % Citation
\printenglishbibliography      % Print bibliography
```

---

## Support and Documentation

### Additional Resources

- **Example Files:** See `chapters/l9-ch*.tex` for real-world examples
- **Recent Changes:** See `CLS-CHANGES-README.md` for latest updates
- **Main README:** See `README.md` for book overview
- **MiKTeX Docs:** https://miktex.org/docs
- **LuaLaTeX Docs:** https://www.luatex.org/

### Getting Help

1. Check this guide for CLS-specific issues
2. Review example chapter files for usage patterns
3. Consult MiKTeX/LuaLaTeX documentation for LaTeX issues
4. Test with minimal document to isolate problems

---

**© 2025 Dr. Yoram Segal. All rights reserved.**

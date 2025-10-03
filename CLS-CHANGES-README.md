# Hebrew Academic Template CLS - Recent Changes

## Python Code Block Title Color Fix

### Issue
Python code blocks (`pythonbox` and `pythonbox*`) had Hebrew RTL titles appearing in white text on light gray background, making them invisible.

### Solution (CLS-based)
Added `coltitle=black` parameter to both `pythonbox` and `pythonbox*` environment definitions in `hebrew-academic-template.cls`.

**Changed in CLS (lines 486, 522):**
```latex
% Regular pythonbox (floating)
\newtcblisting{pythonbox}[1][]{
  ...
  fonttitle=\bfseries,
  coltitle=black,        % <-- ADDED: Black title text
  title=#1,
  ...
}

% Non-floating pythonbox* (for long code)
\newtcblisting{pythonbox*}[1][]{
  ...
  fonttitle=\bfseries,
  coltitle=black,        % <-- ADDED: Black title text
  title=#1,
  ...
}
```

### Usage
No changes needed in `.tex` files. The title parameter works the same:

```latex
\begin{pythonbox*}[Hebrew title text here]
# Python code
\end{pythonbox*}
```

Now the Hebrew title appears in **bold black text** on gray background (visible).

---

## Python Code Overflow Prevention

### Documentation Added to CLS
Added comprehensive overflow prevention guidance as comments in CLS (lines 502-508):

```latex
% IMPORTANT: If pythonbox* code still overflows into footer:
% SOLUTION - Simplify code to show ONLY core functions:
%   - Remove: imports of non-core libraries (matplotlib, sklearn examples)
%   - Remove: print statements, docstrings, example data generation
%   - Remove: visualization code (UNLESS it IS the main topic)
%   - Keep: ONLY the core algorithm/function being demonstrated
% Alternative: Convert to Python pseudocode instead of executable code
```

### When to Use pythonbox vs pythonbox*
- **`pythonbox`**: Short code blocks that fit on one page (floating)
- **`pythonbox*`**: Long code blocks that need to split across pages (non-floating)

If `pythonbox*` still overflows, simplify the code as per CLS documentation above.

---

## Summary of CLS Functions

### For Python Code
| Function | Purpose | Title Color |
|----------|---------|-------------|
| `\begin{pythonbox}[title]` | Short, floating code blocks | Bold black |
| `\begin{pythonbox*}[title]` | Long, non-floating code blocks | Bold black |

Both support Hebrew RTL titles with proper visibility on gray background.

---

## Files Modified
- `hebrew-academic-template.cls` (lines 486, 522): Added `coltitle=black`
- `hebrew-academic-template.cls` (lines 502-508): Added overflow prevention docs

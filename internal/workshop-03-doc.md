### Python Primer — Topic Coverage Map

---

#### 1. Getting Started

**Original**
- Installing Python via Anaconda
- Terminal interpreter, script files, Jupyter Notebooks
- Windows-specific notes

**Add**
- Conda environment setup (replacing Anaconda)
- VSCode as the recommended editor

---

#### 2. Mathematical Operators and Variables

**Original**
- `+`, `-`, `*`, `/`, `**`, `%`
- Order of operations
- Integer vs float types
- Type casting
- Variable assignment

**Toy example**
- GC content calculated from individual base counts — motivates order of operations naturally: `(g + c) / (g + c + a + t)`

**Real example**
- Calculate GC content across a set of real gene sequences from a provided FASTA file; show that GC content varies across genes and is not uniform

---

#### 3. Boolean Values and Operations

**Original**
- `True`, `False`
- Comparison operators `<`, `>`, `<=`, `>=`, `==`, `!=`
- `and`, `or`, `not`

**Add**
- `None` — what it is, when it appears, how to check for it (`if x is None`)

**Toy example**
- Is a read high quality? `mean_quality >= 30` returns `True` or `False`

**Real example**
- Flag reads from a real quality score distribution as passing or failing a threshold; show what proportion of reads pass

---

#### 4. String Variables and Operations

**Original**
- Single and double quotes
- Concatenation with `+`
- Indexing and slicing
- `.upper()`, `.lower()`
- `.count()`
- `len()`
- `.format()`
- Type conversion to/from strings

**Add**
- f-strings — introduce here, replace `.format()` throughout for consistency; include numeric formatting (`{value:.2f}`, `{value:>10}`) since students will use these immediately when printing tabular results
- `.strip()` — remove whitespace and newlines
- `.split()` — split on a delimiter into a list
- `.startswith()` — check string prefix
- Comments as documentation — brief explicit note on when and how to use them

**Toy example**
- A short hardcoded DNA string: indexing to get a specific base, `.upper()` to normalize, `len()` to get sequence length, `.count()` to count a base

**Real example**
- Parse a real FASTA header line: use `.startswith()` to identify header lines, `.strip()` to clean whitespace, `.split()` to extract the gene name from a header like `>BRCA1 chromosome 17`

---

#### 5. Container Variables

**Original**
- Lists: indexing, slicing, `.append()`, `in`, `len()`, `range()`, concatenation
- Sets: `.add()`, `.remove()`, `.union()`, `.difference()`, `.intersection()`
- Dictionaries: key-value pairs, adding entries, `.keys()`, `.values()`

**Add**
- List comprehensions — full treatment: basic form, filter form, and nested form, each shown side by side with the equivalent for loop so students can read either
- Brief note that sets are also useful for fast membership testing, not just set operations
- **Choosing a data structure** — explicit short section framed as a decision guide:
  - Need order? → list
  - Need fast lookup by a key? → dict
  - Need to check membership quickly or enforce uniqueness? → set
  - Show a biological example for each choice to make it concrete

**Toy examples**
- List: a list of short hardcoded gene names; practice indexing, slicing, `.append()`, and `in`
- Set: two small hardcoded gene sets — find shared and unique genes using `.intersection()` and `.difference()`
- Dict: a small hardcoded codon table — look up what amino acid a codon encodes

**Real examples**
- List: a list of quality scores from a real FASTQ record; filter to passing scores using a list comprehension
- Set: two real DE gene lists from different conditions; find genes DE in both, DE only in one, and not DE in either — interpret the result biologically
- Dict: build a gene-to-GC-content dictionary from a real FASTA file; look up GC content by gene name

---

#### 6. Control Flow

**Original**
- `if`, `elif`, `else`

**Add**
- Nothing — biological examples replace toy ones

**Toy example**
- Classify a read as high / acceptable / low quality based on mean quality score using `if`, `elif`, `else`

**Real example**
- Classify variants from a real VCF-like TSV by allele frequency into homozygous reference, heterozygous, and homozygous alternate; count how many variants fall into each category

---

#### 7. Loops

**Original**
- `for` loops over lists and with `range()`
- Nested `for` loops
- `while` loops
- ~~Nested `while` loops~~ — removed, rarely appears in bioinformatics code and adds cognitive load without payoff

**Add**
- `enumerate()` — cleaner alternative to `range(len(list))` for indexed iteration
- `zip()` — iterating over two lists simultaneously, e.g. pairing gene names with expression values
- Brief flag that compact loop forms exist and will appear in LLM output — point forward to list comprehensions where they're covered fully

**Toy example**
- Iterate over a list of short hardcoded sequences and print the GC content of each — ties back to the GC content calculation from section 2 and shows function composition

**Real example**
- Iterate over all sequences in a real FASTA file, compute GC content for each, and collect results into a list; use `enumerate()` to track position and `zip()` to pair gene names with GC values for printing

---

#### 8. Functions

**Original**
- `def`, `return`
- Docstrings
- Optional parameters with defaults
- Scope

**Add**
- `assert` — introduced here as a habit, used throughout
- Returning multiple values via tuples — brief note, framed as "you'll see this in LLM output"
- Explicit note on the spec → docstring → assert → implement pattern, framed informally

**Toy examples**
- `is_valid_sequence(sequence)` — returns `True` if the string contains only A, T, G, C; used as the worked example with full spec → assert → implement walkthrough
- `gc_content(sequence)` — returns GC proportion as a float; first scaffolded function students implement themselves

**Real examples**
- `count_bases(sequence)` — returns a dictionary of base counts; used inside `gc_content()` to show function composition
- `reverse_complement(sequence)` — returns the reverse complement; applied to a set of real primer sequences to verify they are correctly designed

---

#### 9. File Input and Output

**Original**
- `open()` in read and write mode
- `readline()` and manual file handling
- `with` / `as` pattern

**Add**
- `.strip()` in context of file parsing (ties back to strings section)
- `.split()` in context of reading TSV files
- `.startswith()` in context of FASTA parsing

**Toy example**
- Read a small hardcoded FASTA-like string written directly in the notebook as a multiline string; parse it into a dictionary of gene name → sequence without needing an external file

**Real example**
- Read a real FASTA file of gene sequences; parse into a dictionary; write a TSV of gene name and GC content to a new file; verify the output by reading it back and checking a known entry

---

#### 10. Error Messages and Debugging

**Original**
- One `TypeError` shown in the sets section, no explanation

**Add**
- New short section: how to read a traceback — find the relevant line, read the error type, common errors students will encounter (`TypeError`, `IndexError`, `KeyError`, `ZeroDivisionError`)
- Basic `try/except` — not to master but to recognize and understand when the LLM generates it; show the pattern once with a biological example
- Brief note on using `assert` to catch errors before they happen
- Framing: LLM-generated code will sometimes fail — knowing how to read the error is how you fix it

**Toy example**
- Deliberately trigger each common error type using simple code and read the traceback: index past the end of a sequence string (`IndexError`), look up a codon not in the table (`KeyError`), call `len()` on an integer (`TypeError`)

**Real example**
- Introduce a deliberate bug into the FASTA parser from section 9 — e.g. forgetting to call `.strip()` — and show how the traceback identifies the problem; fix it and verify with an assert

---

#### 11. Importing Modules

**Original**
- `import`
- `from X import Y`
- `as` for renaming
- `math`, `os` examples

**Add**
- Forward pointer to `numpy`, `pandas`, `matplotlib` as the core scientific stack
- Drop `biopython` — too much overhead at this level
- Brief note that LLMs will import libraries you haven't seen — that's normal, look them up

**Toy example**
- `import math` and use `math.log2()` to log-transform a hardcoded expression value — motivates why importing domain-relevant functions is more useful than reimplementing them

**Real example**
- Import `matplotlib.pyplot` and plot the GC content values computed across the real FASTA file from section 9 as a histogram; interpret the distribution

---

#### 12. Conclusion

**Original**
- Brief summary, pointer to VanderPlas

**Add**
- Informal note naming the `assert` habit explicitly
- Connection to LLM use: assertions are how you verify what the LLM gave you
- Keep VanderPlas pointer
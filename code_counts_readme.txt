# README - code_counts.csv

This CSV contains metadata and code metrics for each question file in the **HPC_Complete** dataset, with additional details extracted from the original parent question files located in **JSON_individualQs**.  

The CSV merges information from both the HPC-processed files and their corresponding parent question files, enabling correlation studies between code complexity, question text complexity, and other attributes.

---

## Column Descriptions

### File Metadata
- **hpc_folder**  
  The folder in which the HPC JSON file resides (e.g., `JSON_individualQs_HPC_done`).

- **hpc_filename**  
  The full filename of the HPC JSON file, including identifiers.

- **parent_folder**  
  The folder in which the original parent JSON question file resides (from `JSON_individualQs`).

- **parent_filename**  
  The full filename of the parent JSON file.

- **HPC_extraction_type**  
  Indicates how the HPC file was extracted:  
  • `"LLM"` — extracted automatically (LLM).  
  • `"Manual"` — extracted manually.  
  • `""` — not classified.

- **set_number**  
  Numeric set number parsed from the filename (e.g., from `set_1` → 1).

- **method**  
  Question method (e.g., `"multiple-choice"`, `"drag-and-drop"`).

- **subject**  
  Topic of the question (e.g., `"If-Statements"`, `"Loops"`).

- **model**  
  LLM model used to generate the question (e.g., `"gpt-4o"`).

- **question_number**  
  Numeric question identifier parsed from filename (e.g., `q1` → 1).

---

### HPC File Metrics (code snippets only)


- **hpc_snippets**  
  Number of code snippets/Strings (i.e., witing " ") in the 'HPC' field of the JSON file.

- **hpc_newlines**  
  Count of newlines across snippets (ignores leading/trailing blank lines). So total lines are hpc_snippets + hpc_newlines

- **hpc_chars**  
  Total number of characters (including whitespace) across snippets.

- **hpc_chars_nonws**  
  Total characters excluding whitespace.

- **hpc_pykeywords**  
  Count of Python reserved keywords, functions, constan, exceptions, comun libraries from Python. Total unique names: 189

- **hpc_pykeywords_cf**  
  Count of control-flow–related keywords (subset: `if, elif, else, for, while, try, except, finally, with, match, case, and, or`).

- **hpc_max_nesting_depth**  
  Maximum indentation depth in any snippet (approximate nesting).

- **hpc_tokens**  
  Count of identifier tokens (variable, function, class names, etc) across snippets.

- **hpc_avg_tokens_per_code_line**  
  Average number of tokens per code line.

- **hpc_operators**  
  Count of operator symbols (`+`, `-`, `*`, `==`, etc.) across code snippets.

- **hpc_operators_per_token_ratio**  
  Ratio of operators to tokens.

- **hpc_avg_line_length**  
  Average line length for code-only lines.

- **hpc_max_line_length**  
  Maximum line length among code-only lines.
									

---

### Parent File Metrics (original question text)


- **parent_chars**  
  Total number of characters in the entire parent question file (including whitespace)

- **parent_snippets**  
  Number of code snippets/Strings (i.e., witing " ")  in the parent question file.

- **parent_newlines**  
  Count of newlines across snippets. So total lines are parent_snippets + parent_newlines

- **parent_chars_from_snippets**  
  Total number of characters from the snippets (this remove the characters from the JSON strucutre) 
  
- **parent_chars_nonws**  
  Total number of characters from the snippets (this remove the characters from the JSON strucutre), without the whitespaces

- **parent_pykeywords**  
  Count of Python reserved keywords, functions, constan, exceptions, comun libraries from Python. Total unique names: 189

- **parent_pykeywords_cf**  
  Count of control-flow–related keywords (subset: `if, elif, else, for, while, try, except, finally, with, match, case, and, or`).

- **parent_max_nesting_depth**  
  Maximum indentation depth in any snippet (approximate nesting).

- **parent_tokens**  
  Count of identifier tokens (variable, function, class names, etc) across snippets.

- **parent_avg_tokens_per_code_line**
The average number of tokens (words, symbols, or lexical units) per line of code in the parent code block

- **parent_operators**
measures the number of operator symbols (\*\*|//|==|!=|<=|>=|:=|<<|>>|[-+*/%<>=&|^~]) found within the parent code block.

- **parent_operators_per_token_ratio**
The ratio between the number of operators in a parent code block and the total number of tokens [(parent_operators / max(1, parent_tokens))]

- **parent_avg_line_length	**
The average number of characters per line in the parent code block (or text block), typically excluding empty lines.

- **parent_max_line_length	**
The maximum number of characters in a single line within the parent code block or text block.

- **parent_answerchoices_count**
measures the number of answer choices associated with the parent question or prompt.

- **parent_avg_answerchoice_length**  
  Average character length of all provided answer choices.  
  • Captures `"options"`, `"choices"`, or `"answers"` keys.  
  • Supports both list and dictionary formats.  
  • If average length = 0 for multiple-choice questions, a note is added in the `note` column to flag manual review.


- **in_question**
Number of code snippets found in the question

- **elsewhere**
Number of code snippets found elsewere besides the question


- **in_question_chars**	
Total number of charaters of code snippets found in the question


- **elsewhere_chars**
Total number of charaters of code snippets found elsewere besides the question


- **question_embedding**
Vector representation of the full question text generated using a sentence-embedding model.

- **answers_embedding**
Vector representation of all answer or code snippet text associated with the question.

- **mc_choices_sim_matrix**
JSON-encoded cosine similarity matrix showing pairwise similarity between all answer choices.

- **mc_choices_sim_mean**
Average cosine similarity across all distinct pairs of answer choices.

- **mc_choices_sim_max**
Highest cosine similarity value found between any two answer choices.

- **mc_choices_sim_pair**
Indices of the two most similar answer choices within the similarity matrix.

- **mc_choices_n**
Total number of answer choices analyzed for the question.
---

### Other Columns
- **note**  
  Special notes or warnings:  
  • `"PARSE_WARN"` — filename parsing issue.  
  • `"SKIPPED"` — JSON could not be loaded.  
  • `"MISSING_QUESTION_FILE"` — no parent file found.  
  • `"MCQ_NO_ANSWERS"` — multiple-choice question with no captured answers (manual check needed).  
  • Blank if no issues.
  
  
  
  

---

✅ This file enables analysis of both **code complexity (HPC metrics)** and **question text complexity (parent metrics)**.  

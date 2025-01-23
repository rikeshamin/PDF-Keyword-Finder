# PDF Keyword Finder

## Overview

I developed this tool to streamline the process of conducting mass keyword searches in literature during my PhD. It allows for efficient identification of keywords across multiple PDF files in a single directory, saving time and effort. The tool generates a CSV file summarizing the matched keywords and their corresponding file names, enabling easy analysis and organization.

## Features
- Extracts text from PDF files using the `pdfplumber` library.
- Preprocesses text to remove line breaks, hyphens, and extra spaces.
- Searches for user-specified keywords within the extracted text.
- Saves the results (matching filenames and keywords) to a CSV file.

---

## Installation
### Prerequisites
Ensure you have the following installed on your system:
- Python 3.7 or higher
- pip (Python package installer)

### Required Libraries
Install the necessary Python libraries using pip:
```bash
pip install pdfplumber pandas
```

---

## Usage
### Command-Line Arguments
The script requires the following command-line arguments:
1. **pdf_directory**: Path to the directory containing the PDF files.
2. **keywords**: Comma-separated list of keywords to search for.
3. **csv_path**: Path to save the output CSV file.

### Example
To search for keywords "Python" and "Data" in PDF files located in `/path/to/pdfs` and save the results to `/path/to/output.csv`, run:
```bash
python pdf_keyword_finder.py "/path/to/pdfs" "Python,Data" "/path/to/output.csv"
```
---

## Additional Ideas (when time permits)
- Integrate the OpenAI API to enhance usability and provide more accurate keyword matching by leveraging advanced natural language processing capabilities.
- Improve the tool's compatibility with scanned PDFs by incorporating Optical Character Recognition (OCR) functionality to handle files without extractable text.

---

## License
This project is licensed under the MIT License. See the LICENSE file for details.

---

## Contribution
Feel free to star, fork the repository, create issues, or submit pull requests to improve this tool. Suggestions and feedback are VERY welcome!


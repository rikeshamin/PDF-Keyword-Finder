import os
import pdfplumber
import pandas as pd
import argparse

class PDFKeywordFinder:
    def __init__(self, pdf_directory, keywords, csv_path):
        self.pdf_directory = os.path.abspath(pdf_directory)
        self.keywords = [keyword.strip() for keyword in keywords.split(',')]
        self.csv_path = os.path.abspath(csv_path)

    def extract_text_from_pdf(self, pdf_path):
        """Extract text from a PDF file using pdfplumber."""
        text = ""
        try:
            with pdfplumber.open(pdf_path) as pdf:
                for page in pdf.pages:
                    text += page.extract_text()
        except Exception as e:
            print(f"Error reading {pdf_path}: {e}")
        return text

    def preprocess_text(self, text):
        """Preprocess text by removing line breaks, hyphens, and extra spaces."""
        text = text.replace('\n', ' ').replace('- ', '').strip()
        return text

    def find_keywords_in_pdfs(self):
        """Find PDFs containing any of the keywords and return a list of tuples with their filenames and keywords."""
        matching_files = []

        for root, _, files in os.walk(self.pdf_directory):
            for file in files:
                if file.lower().endswith('.pdf'):
                    pdf_path = os.path.join(root, file)
                    text = self.extract_text_from_pdf(pdf_path)

                    # Preprocess the text
                    processed_text = self.preprocess_text(text)

                    matching_keywords = [keyword for keyword in self.keywords if keyword.lower() in processed_text.lower()]
                    if matching_keywords:
                        matching_files.append((file, ", ".join(matching_keywords)))

        return matching_files

    def save_to_csv(self, file_list):
        """Save the list of filenames and keywords to a CSV file."""
        os.makedirs(os.path.dirname(self.csv_path), exist_ok=True)

        df = pd.DataFrame(file_list, columns=["File Name", "Matching Keywords"])
        df['Searched Keywords'] = ", ".join(self.keywords)
        df.to_csv(self.csv_path, index=False)

    def execute(self):
        matching_files = self.find_keywords_in_pdfs()
        self.save_to_csv(matching_files)
        print(f"Files containing the keywords have been saved to {self.csv_path}")


def main():
    parser = argparse.ArgumentParser(description="Search for keywords in PDF files and save matching filenames to a CSV file.")
    parser.add_argument("pdf_directory", help="Directory containing PDF files")
    parser.add_argument("keywords", help="Comma-separated list of keywords to search for")
    parser.add_argument("csv_path", help="Path to save the output CSV file")

    args = parser.parse_args()

    finder = PDFKeywordFinder(args.pdf_directory, args.keywords, args.csv_path)
    finder.execute()


if __name__ == "__main__":
    main()

# Converting-Word-Document-to-CSV

## OVERVIEW
This repository contains python scripts and documentation for converting a word document to a CSV file. 
This word document contains a list of award categoories. The goal is to convert the file to a csv, assign each categories to a unique ID and also have all the categories share the same programe ID.This script can be used for other files 

## LIBRARIES NEEDED
- python-docx
- import csv
- import uuid
- from docx import Document

  ## Steps
- Ensure that the word document and the script are in the same directory
- using any python IDE of your choice,import the libraries needed and use the scripts below.

  ## Python codes

  ```Python
  pip install python-docx
   import csv
   import uuid
   from docx import Document

``` #Reading in the word document
    def read_docx(file_path):
    doc = Document(file_path)
    categories = [para.text for para in doc.paragraphs if para.text.strip() != '']
    return categories

    #Writing the data to a CSV file.
    def write_csv(data, csv_file, program_id):
    
     rows = [{"name": category, "id": str(uuid.uuid4()), "program_id": program_id} for category in data]
      with open(csv_file, mode='w', newline='') as file:
        writer = csv.DictWriter(file, fieldnames=["name", "id", "program_id"])
        writer.writeheader()
        writer.writerows(rows)

         #Converting the docx file to a CSV file.
      def convert_docx_to_csv(docx_file, csv_file, program_id):
   
      data = read_docx(docx_file)
      write_csv(data, csv_file, program_id)

      #File paths
      docx_file = 'OFFICIAL UMBGTA CATEGORIES.docx' #replace with your file name
      csv_file = '/Users/Admin/Desktop/UMBGTA_CATEGORIES.csv' #repalce 'Admin' with your directory name

      #Common program_id
       program_id = "21cd94e6-8aca-4d97-b8aa-38651edcee52"

#Convert DOCX to CSV
convert_docx_to_csv(docx_file, csv_file, program_id)

print(f"CSV file '{csv_file}' created successfully.")
```



## Explanation
### read_docx(file_path):
- Reads the DOCX file and extracts the text content into a list of categories.

### write_csv(data, csv_file, program_id):
 - Writes the extracted categories into a CSV file.
- Each category is assigned a unique UUID.
- All categories share the same program_id.

### convert_docx_to_csv(docx_file, csv_file, program_id):
-Combines the reading and writing processes into a single function for ease of use.
    

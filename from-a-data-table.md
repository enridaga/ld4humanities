
# Recipe: produce RDF from a Google form

 - A Google Form Spreadsheet
 - Prepare column names (first row)
 - Identify the Subject column (S)
 - Generate a tuple for each column value (S, c, v) - G SQL
 - Clean: remove tuples with empty values
 - Format tuples into valid N3 triples
 - Download as TSV
 

You can create a new Google Spreadsheet and follow what I do or just watch :)
 
[LINK](https://docs.google.com/spreadsheets/d/1j_LHZIOhkbD61r7fSxuf4017tgbOoL_Z6tLT0oDQz_0)

Test the result: http://www.easyrdf.org/converter

## Ingestion Service Pipeline
# Overview

The following section describes the end-to-end workflow of the Ingestion Service, detailing how legal documents move from raw input sources to fully normalized, validated, and structured outputs ready for downstream processing.

## Pipeline Workflow
# Input Sources

- PDF

- DOCX

# Processing Steps

1. Fetch document
Retrieve the file from the configured source (upload, crawler, or external provider).

2. Store raw file in Amazon S3
Save the unmodified input to the raw bucket for traceability and reproducibility.

3. Perform OCR (if needed)
Apply OCR when the document is scanned or lacks extractable text.

4. Parse text using predefined rules
Apply parsing logic defined in specs/ to detect structure, headings, sections, articles, tables, subthemes, etc.

5. Normalize content to XML
Build a structured XML file following the defined data contract.

6. Validate XML against XSD
Ensure schema compliance using the XML Schema Definition (spec/xml-schema.xsd).

7. Convert to canonical JSON
Transform the validated XML into the normalized JSON structure used across the system.

8. Push normalized output to storage
Store the final JSON in the designated normalized layer (S3 or DynamoDB — decision pending).

# Storage Layers

- S3 Raw Store – original input files

- S3 Normalized Store – validated XML and canonical JSON

- DynamoDB (pending discussion) – potential structured store for search and referencing

# Outputs

- Example normalized output:
- example-law.json

# Error Handling

Any failed file must be moved to:
s3://bucket/errors/<id>
Along with an associated log file describing the failure reason.

## Pseudocode Example:

# Extract content from PDF and convert to XML
python src/extract_pdf.py \
    --input example.pdf \
    --output xml/example.xml

# Normalize and validate XML, then output canonical JSON
python src/normalize_xml.py \
    --input xml/example.xml \
    --schema spec/xml-schema.xsd \
    --output normalized/example.json
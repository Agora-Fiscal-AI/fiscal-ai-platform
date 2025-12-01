# XML Standard V1

- Root tag '<lawDocument>'
- Required tags: '<id>', '<title>', '<year>', '<section>','<articles>',subthemes['<roman>'(in case of use),'<incise>'(in case of use)].
- Each '<section>', must contain '<sectionName>' and '<article>'
- Each '<article>' must contain <artcleNumber> and '<text>', if it has subthemes['<roman>'(in case of use),'<incise>'(in case of use)] if '<article>' has tables there must be the csv arn:path in S3, it must be showed as '<table name= "arn:path">' (!Nothing showed in XML)
- Ecoding: UTF-8
- Strip: page headers/footers, line numbers.

# Large Explanation

# Root Element

- The XML document must start with the root element:
<lawDocument>

- Required Child Elements

- The following elements are mandatory within the document structure:

<id> – Unique identifier of the legal document

<title> – Official title of the law or normative document

<year> – Publication or enactment year

<section> – Parent container for one or more sections

<articles> – Container for the collection of articles

- Subtheme elements (optional, only if applicable):

<roman> – Roman numeral subdivisions

<incise> – Incise or alphabetical subdivisions

- Section Structure

Each <section> element must include the following:

<sectionName> – The name or heading of the section

One or more <article> elements

Article Structure

Each <article> element must contain:

<articleNumber> – Identifier or index of the article

<text> – Complete textual content of the article

Optional elements (only if applicable):
Subtheme elements:

<roman>

<incise>

Tables:

If an article includes table data, the table itself must not appear in the XML.
Instead, the XML must reference the corresponding CSV file stored in S3 using an ARN path.
This reference must follow the format:

<table name="arn:aws:s3:::bucket/path/to/table.csv" />


(Note: No table data should be embedded inside the XML.)

Encoding

All XML documents must use UTF-8 encoding.

Normalization / Cleaning Rules

During ingestion, the following elements must be removed:

Page headers

Page footers

Line numbers
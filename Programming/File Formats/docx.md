# .DOCX File Format
- is well-known format for Microsoft Word documents. Introduced from 2007 with the release of Microsoft Office 2007, the structure of this new Document format was changed from plain binary to a combination of XML and binary files. Docx files can be opened with Word 2007 and lateral versions but not with the earlier version of MS Word which support DOC file extensions

## File Structure:
- The .docx file in itself is a collection of different xml files that are compressed and then renamed to the extension (.docx).

- document.xml is the primary housing of the word document structure and conforms to the WordprocessingML part of the schemas in **wml.xsd**

## Formatting
- Office Open XML documents follow the ECMA-376 schema.
- This defines their vocabularies, document representation, and packaging.

- It also specifies the requirements for consumers and produces of Office Open XML.

- ECMA-376 contains 4 parts but only part 2 has been adopted in the last edition of the Standard.


## The Standard
- The four parts of the Standard are the following:
  - 1. "Fundamentals and Markup Language Reference"
  - 2. "Open Packaging Conventions"
  - 3. "Markup Compatibility and Extensibility"
  - 4. "Transitional Migration Features"

- **Open XML** in itself is a standard. And it was designed from the start to be capable of faithfully representing the pre-existing corpus of word-processing document, presentations, and spreadsheets that are encoded in binary formats defined by Microsoft.

## Open XML
- defines the format for word-processing, presentation, and spreadsheet documents. 
- Each document is specified through a primary markup language:
  - **WordprocessingML**
  - **PresentiationML**
  - **SpreadsheetML**

### Internationalization
- supports alot of languages
- Inherently supports Unicode because it is XML. In addition, OpenXML ha a rich set of internationalization features that have been refined over the course of many years.

- **Text Orientation**: supports left-to-right (LTR), right-to-left (RTL) and also bidirectional (BIDI). In **WordProcessingML** text direction can be controlled on both the paragraph level and the level of a run within a paragraph. 


## Word Processing ML
- is composed of a collection of stories. Each story is one fo the following:

    - The main document
    - the glossary document
    - A subdocument
    - a header
    - a footer
    - a comment
    - a frame, a text box
    - a footnote
    - or an endnote

- The only Required Story is the main document. It is the target of the package relationship whose type is: http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument

- A typical path would be:
  - **document**
  - **body**
  - **p** (paragraph)
  - **r** (run) is a contiguous piece of text with identical properties, contains no additional markup. 
  - **t** (text range). Contains an arbitrary amount of text with no formatting, line breaks, tables, graphics, or other non-text material.


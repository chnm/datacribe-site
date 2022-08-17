---
title: Importing DataScribe data to Omeka S
type: page
summary: "How to use a DataScribe export to update the items in your Omeka S installation."
---

For this process, you will need:

- a DataScribe project and dataset;
- the [CSV Import module](https://omeka.org/s/docs/user-manual/modules/csvimport/#column-options) for Omeka S;
- an understanding of Omeka S [items](https://omeka.org/s/docs/user-manual/content/items/) and [resource templates](https://omeka.org/s/docs/user-manual/content/resource-template/).

**{discussion of pre work goes here}** In this example, transcribers are supposed to use the semicolon to separate the names of streets on each census sheet. This should allow us to use the "multivalue separator" option in the CSV import. However, there is of course the chance that a transcriber will forget and use a comma. For that reason you might want to use a more distinct separator or do manual separation before importing (see below).

**Note** This mapping process described here will only work when importing the exported data into the *same* Omeka S installation where the DataScribe transcription has taken place.

The screenshots in this example are all of 1950 Census data using the Census Sheet Data form[(download json file)](/tutorials/censusSheetDataForm.json), importing into items using the Census Items resource template [(download json file)](/tutorials/censusDocumentTemplate.json). If you want to run a test using these resources, download the linked jsons and a selection of pages from the [1950 Census website](https://1950census.archives.gov). Create a dataset with the form and transcribe at least three sheets (items).

## Add exported data to existing items

The example in this tutorial has a one to one correlation between the record and the item; each item only generates one record.

### Prepartion

Be mindful of possible post-processing work when creating the guidelines and form. 

In this example, transcribers are supposed to use the semicolon to separate the names of streets on each census sheet. This should allow us to use the "multi-value separator" option in the CSV import. However, there is of course the chance that a transcriber will forget and use a comma. For that reason you might want to use a more distinct separator or do manual separation before importing (see below). 

Also make sure you have a template for incoming information, or at least you know what properties you want to use. This example we've created an extended census documents template with additional properties for all of the fields in the DataScribe form. Note that there is also a property in the template for the DataScribe item number.

### Get and review CSV

In the dataset you're using, go to the "More actions" dropdown in the upper right corner of the browser window.

First choose the "Validate export" option. Exports must be validated before they are run.

If the validation goes smoothly, re-open the "More actions" dropdown and select "Export dataset." Once the export is complete, you can scroll down to the end of the right-hand drawer. Use right-click or a similar option on the "download dataset" link to save the csv file to your computer.

Open the csv file to ensure that it is complete and that all of the rows have the proper formatting. 

If you want to split the data in some of the rows into separate columns, you can do so here. Some csv reading software (Google Sheets, Excel) will split text into columns at specific punctuation marks. This is an alternative to using the multi-value separator option in the csv import.

### Import

Start a new import with the CSV Importer and use your dataset export csv file. Set the import type to "Items."

It is very helpful to add a comment saying what you are importing. Comments display in the Post Imports tab but filenames do not. An example would be "updating items with transcribed data from Dataset name, Project name."

#### Map csv columns

When mapping columns to Omeka S data, it may be be useful to have written which column heading maps to which property in Omeka S for reference when setting these options. If you have created a template for the data, having the template open in another window or having a screenshot as reference is also a good choice.

If you decided to use the multi-value option, you will need to indicate that in the mapping options for that column. Click the wrench icon and ensure that the "use multivalue separator" box is checked.

If you have the Numeric Data Types module installed, you can import any date or datetime data fields in timestamp format.

#### Basic import settings

Basic settings: make sure you select template if using. Also be sure to have your multi-value separator set to the right thing.

Once you are in options, go to the advanced settings. You want to choose "Append data to the resource: Add new data to the resource, based on an identifier for an existing resource. (Cannot be undone.)" For the identifier column, chose the Omeka Item # column. The identifier property is "internal ID" (meaning the Omeka S item ID).

#### Advanced import settings

In the advanced settings tab, use the Import type dropdown to choose: "Append data to the resource: Add new data to the resource, based on an identifier for an existing resource. (Cannot be undone.)"

For the identifier column, chose the Omeka Item # column. This column is automatically created by DataScribe in the export. For the identifier property, choose "internal ID" (meaning the Omeka S item ID).

### Verify the import

Once the import is complete, open at least one of the Omeka S items you know were part of the item set which populated the dataset. Check to make sure that the information has been properly mapped and imported. 

Remember that if the import had errors you will have to *manually* remove the bad data. Imports which append data cannot be undone.

## Variations

In addition to updating Omeka S items with information, one row in the exported csv per Omeka S item, there are other possible approaches. These are suggestions about how you might modify the above tutorial to run these sorts of import updates.

### Add multiple records to one item

**Text goes here.**

### Add records as new items

If you wanted to create new items from your DataScribe export, you could modify the tutorial by taking the following steps:

- In the Advanced tab, keep the option set to "Add new items"
- Use the column `Omeka S Item #` to create a link between the new item from the record to the existing item for the image transcribed:

  - Map the `Omeka S Item #` column to a property like `Is Part Of` so that it will appear in the new item's metadata.
  - Use the options for the mapping to set the data type to "Import as Omeka S resource ID".
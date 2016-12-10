---
title: CSV Storage
sidebar: mydoc_sidebar
permalink: multi-model-storage-csv.html
folder: mydoc
---

## CSV Storage

The BlobCity DB supports insert of data in CSV format. This can be individual records or a complete CSV file that is imported in bulk. However because of the lack of ability of CSV to have strongly consistent column bindings, any CSV data inserted into the DB is converted to an equivalent JSON object and then stored. The conversion to JSON, ensures strong column bindings even when columns in the table are renamed or the number of columns in the collection are changed over time.

The functioning of the CSV storage is exactly same as that of the JSON storage explained in earlier sections. The way CSV data is inserted into the DB however differs, and is explained in this section.
{% include links.html %}

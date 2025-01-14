# DataHarmonizer

A standardized browser-based spreadsheet editor and validator that can be run offline and locally, which works of of [LinkML](https://linkml.io/) data specifications. This is an experimental version of DataHarmonizer being used to develop a **food recipe model** as part of the FoodOn project.

This project, created by the Centre for Infectious Disease Genomics and One Health (CIDGOH), at Simon Fraser University, is now an open-source collaboration with contributions from the National Microbiome Data Collaborative (NMDC), the LinkML development team, and others.  Watch Rhiannon Cameron and Damion Dooley describe this application on [YouTube](https://www.youtube.com/watch?v=rdN2_Vhwb8E&t=38s&ab_channel=CANARIEInc.) at the Canadian Research Software Conference (CRSC2021).

|Chrome|Firefox|Edge|
|---|---|---|
|49+|34+|12+|

![alt text](./images/editCopyPasteDelete.gif)

## Installation

This repository currently contains two kinds of release. 
1) A stand-alone browser-based version of DataHarmonizer that includes templates for modelling **recipes**. Release notes indicate which versions of these templates are included.

```
To get the stand-alone version, download the zipped source code from the latest release at:
https://github.com/Public-Health-Bioinformatics/DataHarmonizer/releases

Extract the zipped file.

To run the application, navigate to the extracted folder and open `web/dist/index.html`.

Alternately, to run the application in development mode so that it is responsive to changes in linkml schemas and templates that you are editing, see the **Development** section below. 

# Stand-Alone DataHarmonizer Functionality

## Select Template

The default template loaded is the "food recipe" template. To change the spreadsheet template, select the white text box to the right of **Template**, it always contains the name of template currently active, or navigated to **File** followed by **Change Template**. An in-app window will appear that allows you to select from the available templates in the drop-down menu. After selecting the desired template, click **Open** to activate the template.

![change template](./images/changeTemplate.gif)

See more on the Wiki [DataHarmonizer templates](https://github.com/cidgoh/DataHarmonizer/wiki/DataHarmonizer-Templates) page.

## Usage

You can edit the cells manually, or upload `xlsx`, `xls`, `tsv` and `csv` files via **File** > **Open**. You can also save the spreadsheet's contents to your local hard-drive in the aforementioned formats, or **File** > **Export** your data as an `.xls` document formatted for submission a specified portal, database, or repository.

![saving and exporting files](./images/exportingFiles.gif)

Click the **Validate** button to validate your spreadsheet's values against a
standardized vocabulary. You can then browse through the errors using the **Next Error** button. Missing value are indicated in _dark red_, while incorrect values are _light red_.

![validating cells and checking next error](./images/validatingCells.gif)

Double click any column headers for information on the template's vocabulary.

![double click headers for more info](./images/doubleClickHeaders.gif)

You can quickly navigate to a column by selecting **Settings** > **Jump to...**. An in-app window will appear, select the desired column header from the drop-down list or begin typing it's name to narrow down the list options. Selecting the column header from the drop down list will immediately relocate you to that column on the spreadsheet.

![jump to column](./images/jumpToColumn.gif)

You can also automatically fill a column with a specified value, but only in rows with corresponding values in the first `sample ID` column. To use this feature select **Settings** > **Fill column...**. Select the desired column header from the drop-down list or begin typing it's name to narrow down the list options, then specify the value to fill with and click **Ok** to apply.

![fill column, in rows with corresponding sample IDs, with specified value](./images/fillColumn.gif)

For _more information_ on available application features, select the **Help** button followed by **Getting Started** from within the DataHarmonizer application.

## Example Data

The stand-alone version of DataHarmonizer when built is placed in the /web/dist/ folder, with the following structure.  Templates with example data testing functionalities can be found within the following folder structure leading to the "exampleInput/" folder, when available:

```
. TOP LEVEL DIRECTORY
├── images
├── libraries
├── script
└── template
│   ├── templateOfInterest
│   │   └── exampleInput
│   └── ...
```

Note that the source of the built "template/" folder above is actually in /web/templates/, where example input data should be placed before performing the build process.  You will see a recipe folder there with under development schemas for recipe-related ontology-driven data structures.

- [`recipe`](https://github.com/FoodOntology/DataHarmonizer/tree/master/web/templates/recipe/) templates.

Having made changes to either of:

  web/templates/recipe/schema_core.yaml
  web/templates/recipe/schema_slots.tsv
  web/templates/recipe/schema_enums.tsv

Rerun:

  python ../../../script/tabular_to_schema.py
  python ../../../script/linkml.py -i schema.yaml
  
To regenerate the schema.json file which drives DataHarmonizer template options.


## Version Control

Versioning of templates, features, and functionality is modeled on semantic versioning (i.e. versions are expressed as “DataHarmonizer X.Y.Z”).
Changes to vocabulary in template pick lists are updated by incremental increases to the third position in the version (i.e. “Z” position).
Changes to fields and features are updated by incremental increases to the second position in the version (i.e. “Y” position).
Changes to basic infrastructure or major changes to functionality are updated by incremental increases to the first position in the version (i.e. “X” position).

Descriptions of updates are provided in [release notes](https://github.com/cidgoh/DataHarmonizer/releases) for every new version.

Discussions contributing to updates may be tracked on the DataHarmonizer GitHub issue tracker.

# Development

Code in this repository is split mainly between two folders: `lib` and `web`. The `lib` folder contains the core interface components which are published to NPM and can be used by any client to build a user interface. The `web` folder contains an implementation of one such interface, using the components defined in `lib`. The interface implemented in the `web` folder is packaged and [made available to users as releases of this repository](#Installation).

## Prerequisites

For development, you must have [Node.js](https://nodejs.org) and [Yarn](https://yarnpkg.com/getting-started/install) installed. If you have Node.js version 16.10 or later (highly recommended) and you have not used Yarn before, you can enable it by running:

```shell
corepack enable
```

## Installing

To install the dependencies of this package for development simply run:

```shell
yarn
```

## Running Locally

Developing either the library components in `lib` or the interface in `web` can be done using the same command:

```shell
yarn dev
```

This will start a [webpack development server](https://webpack.js.org/configuration/dev-server/) running locally on `localhost:8080`. Changes to either `lib` or `web` should be loaded automatically in your browser. This serves as interface for testing and debugging the core library components (in the lib directory) and that interface itself (the web directory).

## Publishing and Releasing

To bundle the canonical interface run:

```shell
yarn build:web
```
You can open web/dist/index.html in your browser to test the distributable bundle and verify it runs in "offline".

To bundle the library components into lib/dist for downstream clients to use via API instead of the canonical interface, run:

```shell
yarn build:lib
```

`TODO: describe how to prepare a release containing just the web/dist/ folder and templates; and describe how to use the API.`

## Roadmap

This project is now in production, with new features being added occasionally.  The [Projects](https://github.com/cidgoh/DataHarmonizer/projects/1) tab indicates anticipated functionality.

# Support

If you have any ideas for improving the application, or have encountered any problems running the application, [please open an issue for discussion][1].

[1]: https://github.com/Public-Health-Bioinformatics/DataHarmonizer/issues

## Additional Information

For more information about the DataHarmonizer, it's templates, and how to use them, check out the [DataHarmonizer Wiki](https://github.com/Public-Health-Bioinformatics/DataHarmonizer/wiki).

## Acknowledgement

- [Handsontable](https://handsontable.com/) was used to build the grid.  DataHarmonizer is configured to reference the "non-commercial-and-evaluation" handsontable license "for purposes not intended toward monetary compensation such as, but not limited to, teaching, academic research, evaluation, testing and experimentation"; if this application is used for commercial purposes, this should be revised as per https://handsontable.com/docs/license-key/
- [SheetJS](https://sheetjs.com/) was used to open and save local files. The community edition was used under the [Apache 2.0](https://github.com/SheetJS/sheetjs/blob/master/LICENSE) license.

## License

DataHarmonizer javascript, python and other code not mentioned in the Acknowledgement above is covered by the [MIT](LICENSE) license.


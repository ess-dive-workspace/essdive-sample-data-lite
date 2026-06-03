# ESS-DIVE Sample Data - Lite Reporting Format Instructions

## SCOPE
- The Sample Data - Lite Reporting Format is intended for laboratory-generated sample data. This can include a set of individual samples or a time series of measurements on a single sample.
- This reporting format (RF) provides guidance on file structure and contents for data and metadata. It includes a term guide, templates, examples, and several controlled vocabularies.
- To be compliant with this RF, you must also adhere to the requirements in the [CSV](https://github.com/ess-dive-workspace/essdive-csv-structure) and [File Level Metadata](https://github.com/ess-dive-workspace/essdive-file-level-metadata) Reporting Formats.
- A more detailed version of this reporting format ([Sample Data - Full](https://github.com/ess-dive-workspace/essdive-sample-data-full/tree/release-v1.0.0)) is also available for laboratory-generated sample data.
    - The Full version supports more detailed metadata and provides flexibility to describe more approaches. For example, sample tracking, named locations, non-point locations, and complex / detailed methods are supported.
    - The Lite version supports less detailed metadata and only common approaches. For example, point locations in only WGS84 datum and high-level methods are supported; sample tracking is not supported.

## CHECKLIST FOR SUBMISSION
- [Data files](#data-files) (as many as needed)
- [Methods file](#methods-file) (one)
- [Data dictionary](#data-dictionary-files) (as many as needed)
- [File level metadata](#file-level-metadata-file) (one)

## DATA FILES
- **Purpose:** provides measurement data for each sample.
- **Format:** comma-separated value (.csv)
- Use the template and term guide to structure data files.
    - Required fields include:
        - `material`
        - `datetime_collected`
        - `{measurement_column_name}`
    - Conditionally required fields include:
        - `latitude` and `longitude`
            - Condition: Required to have either `latitude` and `longitude` or `location_description`
        - `location_description`
            - Condition: Required to have either `latitude` and `longitude` or `location_description`
        - `time_elapsed`
            - Condition: Required for time series measurements on a single sample
   - Optional fields include:
       - `sample_name`
       - `vertical_position`
       - `vertical_position_reference`
       - `treatment_id`
       - `datetime_measured`
       - `{measurement_column_name}_flag`
       - `notes`
- Include as many measurement columns/rows as desired. Each `{measurement_column_name}` must be defined in the data dictionary using the RF-specified fields.
- If multiple flags are provided in a single cell, they should be separated by a semicolon and space.
- Flags and treatments should be defined in the Methods File.
- If data files contain time series measurements on a single sample, one sample is allowed per file and `time_elapsed` cannot have repeated values.

## METHODS FILE
- **Purpose:** describe methods used in data generation and define flags and treatments.
- **Format:** Text file (.txt)
- Name the file “`sample_method.txt`” or with the suffix  “`_sample_method.txt`”.

## FILES GOVERNED BY OTHER REPORTING FORMATS
### DATA DICTIONARY FILES
- **Purpose:** lists and describes `column_or_row_name` to provide metadata for each column/row header.
- **Format:** comma-separated value (.csv)
- **Governed by:** File Level Metadata (FLMD) Reporting Format available at https://github.com/ess-dive-workspace/essdive-file-level-metadata, with required modifications detailed in this Sample Data - Lite Reporting Format.
- Use the Sample Data - Lite Reporting Format template to structure data dictionary (dd) files. The template includes original FLMD Reporting Format terms and extensions that build upon it. Use the Sample Data - Lite Reporting Format term guide for descriptions and requirements; original FLMD terms that are not extended have links to the FLMD term guide. Extensions are marked with an asterisk below.
    - Required fields include:
        - `column_or_row_name`
        - `unit`*
        - `definition`*
        - `measured_variable`*
    - Optional fields include:
        - `column_or_row_long_name`
        - `data_type`
        - `missing_value_code`*
        - `unit_basis`*
        - `statistic_measurement`*
        - `statistic_spatial`*
        - `statistic_temporal`*
        - `representation_temporal`*
        - `notes`*
- The data dictionary template includes definitions for the data file's required and optional terms. These definitions must be used as-is in the definition column when you create the data dictionaries for your data package.
- Column/row headers defined in the dd cannot be repeated in the same dd. If column/row headers have different metadata across data files, the data files must use separate dd files.
- If your dataset contains other data dictionaries, the data dictionaries associated with these Sample Data - Lite Reporting Format files must be separate.

### FILE LEVEL METADATA FILE
- **Purpose:** lists and describes file_name to provide metadata for each file.
- **Format:** comma-separated value (.csv)
- **Governed by:** FLMD Reporting Format available at https://github.com/ess-dive-workspace/essdive-file-level-metadata, with required modifications detailed in this Sample Data - Lite Reporting Format.
- Use the Sample Data - Lite Reporting Format template to structure FLMD files. The template includes original FLMD Reporting Format terms and extensions that build upon it. Use the Sample Data - Lite Reporting Format term guide for descriptions and requirements; original FLMD terms that are not extended have links to the FLMD term guide. Extensions are marked with an asterisk below.
     - Required fields include:
          - `file_name`
          - `file_description`
          - `standard`*
          - `data_dictionary_file_name`*
     - Optional fields include:
          - `file_version`
          - `data_orientation` = horizontal
          - `header_rows` = 1
          - `column_or_or_name_position` = 1
          - `notes`
- The data, methods and attributes, and data dictionary files listed in the FLMD should have “ESS-DIVE Sample Data - Lite Reporting Format v1” listed in the `standard` column.
- If you include the optional fields `data_orientation`, `header_rows`, or `column_or_row_name_position`, report the values above for the files following this RF.

## ADDITIONAL CONSIDERATIONS
- You are encouraged to include raw data files, instrument specification PDFs from manufacturers, code used for data collection or data processing, and/or links to relevant content (i.e., GitHub, Zenodo). The RF does not provide specific guidance on formats of these additional files.

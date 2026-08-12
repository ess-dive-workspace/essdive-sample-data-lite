# Instructions

## SCOPE
- The Sample Data - Lite Reporting Format is intended for data-generated in a laboratory from physical samples. This can include a set of individual samples or a time series of measurements on a single sample.
- This reporting format (RF) provides guidance on file structure and contents for data and metadata. It includes a term guide, templates, examples, and several controlled vocabularies.
- To be compliant with this RF, you must also adhere to the requirements in the [CSV](https://github.com/ess-dive-workspace/essdive-csv-structure) and [File Level Metadata](https://github.com/ess-dive-workspace/essdive-file-level-metadata) Reporting Formats, as detailed below.
- A more detailed version of this reporting format ([Sample Data - Full](https://github.com/ess-dive-workspace/essdive-sample-data-full/tree/release-v1.0.0)) is also available for laboratory-generated sample data.
    - The Full version supports more detailed metadata and provides flexibility to describe more approaches. For example, sample tracking, named locations, non-point locations, and complex / detailed methods are supported.
    - This Lite version supports less detailed metadata and only common approaches. For example, point locations in only WGS84 datum and high-level methods are supported; sample tracking is not supported.

## CHECKLIST FOR SUBMISSION
- [Data file(s)](#data-files) (as many as needed)
- [Methods file](#methods-file) (one)
- [Data dictionary file(s)](#data-dictionary-files) (as many as needed)
- [File level metadata file](#file-level-metadata-file) (one)

## DATA FILES
- **Purpose:** provides measurement data for the sample(s).
- **Format:** comma-separated value (.csv)
- Use the template and term guide to structure data files.
    - Required terms include:
        - `material_collected`
        - `datetime_collected`
        - `{measurement_column_name}`
    - Conditionally required terms include:
        - `latitude` and `longitude`
            - Condition: Required to have either `latitude` and `longitude` or `location_description`
        - `location_description`
            - Condition: Required to have either `latitude` and `longitude` or `location_description`
        - `time_elapsed`
            - Condition: Required for time series measurements on a single sample
   - Optional terms include:
       - `sample_name`
       - `vertical_position`
       - `vertical_position_reference`
       - `treatment_id`
       - `datetime_measured`
       - `common_flag`
       - `{measurement_column_name}_flag`
       - `notes`
- Include as many measurement columns as desired. Each `{measurement_column_name}` must be defined in the data dictionary using the RF-specified terms.
- If multiple flags are provided in a single cell, they should be separated by a semicolon and space.
- Flags and treatments should be defined in the Methods File.
- If data files contain time series measurements on a single sample, each file can only contain a time series for one sample. The column required for a time series (`time_elapsed`) cannot have repeated values.

## METHODS FILE
- **Purpose:** describe methods used in data generation and define flags and treatments.
- **Format:** Text file (.txt)
- Name the file “`sample_method.txt`” or with the suffix  “`_sample_method.txt`”.

## FILES GOVERNED BY OTHER REPORTING FORMATS
### DATA DICTIONARY FILES
- **Purpose:** lists and describes `column_or_row_name` to provide metadata for each column header.
- **Format:** comma-separated value (.csv)
- **Governed by:** [File Level Metadata (FLMD) Reporting Format](https://github.com/ess-dive-workspace/essdive-file-level-metadata) with required modifications detailed in this Sample Data - Lite Reporting Format (see details below).
- Use the Sample Data - Lite Reporting Format template to structure data dictionary (DD) files. Name the file “`dd.csv`” or with the suffix “`_dd.csv`”. The term guide has term descriptions and requirements. _Extension (new) or modified terms that build on the dd structure governed by the FLMD Reporting Format are marked with a plus below._
    - Required terms include:
        - `column_or_row_name`
        - `unit`+
        - `definition`+
        - `measured_variable`+
    - Optional terms include:
        - `material_measured`+
        - `column_or_row_long_name`
        - `data_type`+
        - `missing_value_code`+
        - `unit_basis`+
        - `representation_temporal`+
        - `statistic_measurement`+
        - `statistic_measurement_number`+
        - `statistic_spatial`+
        - `statistic_spatial_number`+
        - `statistic_temporal`+
        - `statistic_temporal_number`+
        - `statistic_detail`+
        - `notes`+
- The data dictionary template includes definitions for the data file's required and optional terms. These definitions must be used as-is in the `definition` column when you create the data dictionaries for your data package.
- Column names (`column_or_row_name`) defined in the DD cannot be repeated in the same DD.
    - If column headers have different metadata across data files (e.g., a different unit or description) but the column names do not change, the data files must use separate DD files i.e., there must be a specific DD file per data file.
- If your dataset contains other data dictionaries, the data dictionaries associated with these Sample Data - Lite Reporting Format files must be separate.

### FILE LEVEL METADATA FILE
- **Purpose:** lists and describes `file_name` to provide metadata for each file.
- **Format:** comma-separated value (.csv)
- **Governed by:** [File Level Metadata (FLMD) Reporting Format](https://github.com/ess-dive-workspace/essdive-file-level-metadata) with required modifications detailed in this Sample Data - Lite Reporting Format (see details below).
- Use the Sample Data - Lite Reporting Format template to structure FLMD files. Name the file “`flmd.csv`” or with the suffix “`_flmd.csv`”. The term guide has term descriptions and requirements. _Extension (new) or modified terms that build on the FLMD structure governed by the FLMD Reporting Format are marked with a plus below._ 
     - Required terms include:
          - `file_name`
          - `file_description`
          - `standard`+
          - `data_dictionary_file_name`+
     - Optional terms include:
          - `file_version`
          - `data_orientation`
          - `header_rows`
          - `column_or_or_name_position`
          - `notes`
- The data and methods and attributes files listed in the FLMD should have “ESS-DIVE Sample Data - Lite Reporting Format v1” listed in the `standard` column.
- If you include the optional terms `data_orientation`, `header_rows`, or `column_or_row_name_position`, the reported values should be “horizontal”, “1”, and “1”, respectively, for the files following this RF.

## ADDITIONAL CONSIDERATIONS
- You are encouraged to include raw data files, instrument specification PDFs from manufacturers, code used for data collection or data processing, and/or links to relevant content (i.e., GitHub, Zenodo). The RF does not provide specific guidance on formats of these additional files.

# Term Guide

The Sample Data - Lite Reporting Format terms are defined below, including whether that term is required, conditionally required, or optional, a brief definition, formatting requirements, an example, and additional guidance.

A single asterisk (*) below marks terms that are required. Two asterisks (**) mark fields that are conditionally required.

### Terms of the reporting format:
[**Sample Data File**](#sample-data-file)
- [material](#material)*
- [datetime_collected](#datetime_collected)*
- [{measurement_column_name}](#measurement_column_name)*
- [latitude](#latitude)**
- [longitude](#longitude)**
- [location_description](#location_description)**
- [time_elapsed](#time_elapsed)**
- [sample_name](#sample_name)
- [vertical_position](#vertical_position)
- [vertical_position_reference](#vertical_position_reference)
- [treatment_id](#treatment_id)
- [datetime_measured](#datetime_measured)
- [{measurement_column_name}_flag](#measurement_column_name_flag)
- [notes](#notes)
 
[**File Level Metadata File**](#file-level-metadata-file)
- [file_name](#file_name)*
- [file_description](#file_description)*
- [standard](#standard)*
- [data_dictionary_file_name](#data_dictionary_file_name)*
- [file_version](#file_version)
- [data_orientation](#data_orientation)
- [header_rows](#header_rows)
- [column_or_row_name_position](#column_or_row_name_position)
- [notes](#notes-1)

[**Data Dictionary File**](#data-dictionary-file)
- [column_or_row_name](#column_or_row_name)*
- [unit](#unit)*
- [definition](#definition)*
- [measured_variable](#measured_variable)*
- [column_or_row_long_name](#column_or_row_long_name)
- [data_type](#data_type)
- [missing_value_code](#missing_value_code)
- [unit_basis](#unit_basis)
- [statistic_measurement](#statistic_measurement)
- [statistic_spatial](#statistic_spatial)
- [statistic_temporal](#statistic_temporal)
- [representation_temporal](#representation_temporal)
- [notes](#notes-2)

---
## Sample Data File
### material
|term|`material`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-lite/blob/release-v1.0.0/controlled_vocabulary.md#material)|
|unit|N/A|
|definition|Material / medium being measured.|
|example|Liquid>aqueous|
|additional guidance|Material / medium of the sample.|

### datetime_collected
|term|`datetime_collected`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|datetime, ISO 8601:2019|
|unit|N/A|
|definition|Date and time of sample collection, to known specificity. |
|example|2026-03-11T13:00-06:00 |
|additional guidance|Dates must be reported in the ISO 8601:2019 standard (YYYY-MM-DD) and completed to known precision (e.g. YYYY-MM, YYYY). Times must be reported with a date in either Coordinated Universal Time (UTC) (YYYY-MM-DDThh:mm:ssZ) or Local Standard Time with the UTC offset (YYYY-MM-DDThh:mm±hh:mm). It is strongly recommended not to change UTC offset in the middle of a time series (i.e., do not switch from Standard Time to Daylight Savings Time). Complete times to known precision (e.g. YYYY-MM-DDThh). Use of "T" and either “Z” or “±” characters are required. <br><br> YYYY = 4-digit year, MM = 2-digit month, DD = 2-digit day of month, hh = 2-digit hour ranging from 00-23, mm = 2-digit minute, ss = 2-digit second.|

### {measurement_column_name}
|term|`{measurement_column_name}`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|text; only UTF-8 characters are permitted|
|unit|N/A|
|definition|User-defined measurement column name. Strongly recommend to use only letters, numbers, underscores, and hyphens.|
|example|temp_soil_2|
|additional guidance|`{measurement_column_name}` is considered arbitrary. They are not parsed for information on type of variable, unit, statistic, or temporal representation. Each `{measurement_column_name}` must be defined in the data dictionary file using the required fields that include `measured_variable` and `unit`. Optional fields, such as `statistic_*`, `representation_temporal`, and `unit_basis`, should be used to fully describe the measurement characteristics. |

### latitude
|term|`latitude`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|Required conditionally: either `latitude` and `longitude` or `location_description` must be used|
|format|numeric; range (-90, 90)|
|unit|degree|
|definition|Latitude of the location, in decimal degree and in decimal degree and in a coordinate reference system with WGS84 datum. Provide latitude in +/- notation, rather than North/South notation.|
|example|46.27487|
|additional guidance|The numeric precision should reflect actual spatial precision of the measurement; this typically means having 3-5 significant digits if latitude is based on GPS. <br><br> The location will be considered a point at the reported latitude and longitude.|

### longitude
|term|`longitute`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|Required conditionally: either `latitude` and `longitude` or `location_description` must be used|
|format|numeric; range (-180, 180)|
|unit|degree|
|definition|Longitude of the location, in decimal degree and in a coordinate reference system with WGS84 datum. Provide longitude in +/- notation, rather than East/West notation.|
|example|-119.26988|
|additional guidance|The numeric precision should reflect actual spatial precision of the measurement; this typically means having 3-5 significant digits if longitude is based on GPS. <br><br> The location will be considered a point at the reported latitude and longitude.|

### location_description
|term|`location_description`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|Required conditionally: either `latitude` and `longitude` or `location_description` must be used|
|format|Free text|
|unit|N/A|
|definition|Text description of a location. Details could include physical environment, sampling infrastructure, ecosystem type, and habitat.|
|example|Sediment along eastern shoreline of the Columbia River, Richland, WA, USA|
|additional guidance|`latitude` and `longitude` is strongly recommended rather than using only the `location_description` field.|

### time_elapsed
|term|`time_elapsed`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|Required conditionally for time series measurements on a single sample|
|format|numeric|
|unit|second|
|definition|Cumulative time elapsed, to known specificity, between the first measurement and the current measurement, on a single sample.|
|example|30|
|additional guidance|Used to indicate the passage of time when taking multiple measurements through time on a single sample.|

### sample_name
|term|`sample_name`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Collector's project-specific sample name, which must be unique for each sample within the dataset that you are submitting.|
|example|CM_023|
|additional guidance|Sample names must be unique within the dataset and ideally are unique across a project.|

### vertical_position
|term|`vertical_position`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|numeric|
|unit|meter|
|definition|Height / altitude (positive numbers) or depth (negative numbers) in reference to the ground surface, unless a different reference is specified in the `vertical_reference_position` field. One vertical position is allowed for each location.|
|example|-0.25|
|additional guidance|N/A|

### vertical_position_reference
|term|`vertical_position_reference`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-lite/blob/release-v1.0.0/controlled_vocabulary.md#vertical_position_reference)|
|unit|N/A|
|definition|Reference for the vertical_position. If vertical_position is not provided in reference to the ground surface, a vertical_position_reference must be specified.|
|example|water_bed|
|additional guidance|If your vertical position reference is not in the controlled vocabulary, choose `other` and provide the vertical position reference in the notes field.|

### treatment_id
|term|`treatment_id`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|text; only UTF-8 characters are permitted |
|unit|N/A|
|definition|User-defined identifier that indicates what treatment was used for manipulation experiments, if applicable. Strongly recommended that only letters, numbers, hyphens, and underscores are used.|
|example|treatment_wet_01|
|additional guidance|Treatment IDs should be defined within the methods and attributes file. <br><br> It is recommended that if there is no treatment but the column is present, the `treatment_id` should be “N/A”. It is recommended that if there is a control treatment, the `treatment_id` should be “control”.|

### datetime_measured
|term|`datetime_measured`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|datetime, ISO 8601:2019|
|unit|N/A|
|definition|Date and time of measurement, to known specificity.|
|example|2026-03-12T13:50-06:00|
|additional guidance|Dates must be reported in the ISO 8601:2019 standard (YYYY-MM-DD) and completed to known precision (e.g. YYYY-MM, YYYY). Times must be reported with a date in either Coordinated Universal Time (UTC) (YYYY-MM-DDThh:mm:ssZ) or Local Standard Time with the UTC offset (YYYY-MM-DDThh:mm±hh:mm). It is strongly recommended not to change UTC offset in the middle of a time series (i.e., do not switch from Standard Time to Daylight Savings Time). Complete times to known precision (e.g. YYYY-MM-DDThh). Use of "T" and either “Z” or “±” characters are required. <br><br> YYYY = 4-digit year, MM = 2-digit month, DD = 2-digit day of month, hh = 2-digit hour ranging from 00-23, mm = 2-digit minute, ss = 2-digit second.|

### {measurement_column_name}_flag
|term|`{measurement_column_name}_flag`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|text; only UTF-8 characters are permitted|
|unit|N/A|
|definition|User-defined identifier that indicates a flag for the individual measurement in the corresponding measurement_column_name. Strongly recommend to use only letters, numbers, underscores, and hyphens.|
|example|temp_soil_2_flag|
|additional guidance|Column header for associated `{measurement_column_name}` will be appended with “_flag” for a flag column. If abbreviated/coded flags are used, we strongly recommend that these are defined within the required methods file.|

### notes
|term|`notes`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Free text notes field.|
|example|Storm event occurred during sampling.|
|additional guidance|N/A|

---

## File Level Metadata File
### file_name
|term|`file_name`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|N/A|
|definition|Provide the name of the associated file. File names should be unique and be as descriptive as possible about the file contents. Use only letters (e.g. CamelCase), numbers, and underscores. Do not include spaces. Hyphens allowed but not preferred. Use "\*" wildcard when the FLMD applies to multiple files. For example - the same FLMD applies to all soil core files in this data package - "soil_cores_*.csv"|
|example|measurements.csv|
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/flmd_quick_guide.md#file-name).|

### file_description
|term|`file_description`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement| required|
|format|N/A|
|definition|A brief description (minimum of 10 characters) of the file and what distinguishes this file from other files in the data package. Include information about the type of data (images, observations, experimental, etc.) |
|example|Geochemistry data measurements, including anions and cations, for 2025-06-08 to 2026-01-02.|
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/flmd_quick_guide.md#file-description).|

### standard
|term|`standard`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/RF_FLMD_Standard_Terms.csv)|
|definition|Identify if an ESS-DIVE Reporting Format or any other data or metadata standard was applied to the data file. Standard names for the ESS-DIVE reporting formats are available in the [Standard FLMD Term List](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/RF_FLMD_Standard_Terms.csv).| 
|example|ESS-DIVE Sample Data - Lite Reporting Format v1|
|additional guidance|For any files following the Sample Data - Lite reporting format, including data, methods and attributes, and data dictionary, provide "ESS-DIVE Sample Data - Lite Reporting Format v1" in the `standard` field.|

### data_dictionary_file_name
|term|`standard`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|text; contains “_dd.csv"|
|definition|The file name of the data dictionary that corresponds to the provided “file_name” entry. The file name must end with “_dd.csv”.| 
|example|measurements_dd.csv|
|additional guidance|N/A|

### file_version
|term|`file_version`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|definition|This is the version of the data file being described in the FLMD. The data file version is assigned by the data provider and not by the system. This would change if the data file is updated after the data package is published. Changes should be explained in the Notes field.| 
|example|version 1|
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/flmd_quick_guide.md#file-version).|

### data_orientation
|term|`data_orientation`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|horizontal or vertical|
|definition|Describe how the data are organized within the data matrix. Choose between "horizontal" (i.e., data are organized in rows with column headers) or "vertical" (i.e., data are organized in columns with row headers).| 
|example|horizontal|
|additional guidance|For files following the Sample Data - Lite reporting format, the `data_orientation` value should be "horizontal".| 

### header_rows
|term|`header_rows`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|numeric|
|unit|N/A|
|definition|Provide the total number of header rows before the start of the first data row, including the column header or row name. Do not include commented-out (i.e., column/rows that begin with a hash (#)) in the header_rows count. This field is marked as optional, but is required if any data files have more than one header row.|
|example|1|
|additional guidance|For files following the Sample Data - Lite reporting format, the `header_rows` value should be 1.|

### column_or_row_name_position
|term|`column_or_row_name_position`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|numeric|
|unit|N/A|
|definition|Provide the row or column number that contains the header names. This field is not required if there are no rows or columns before the row/column names. If not included, it will be assumed that header names are in row 1 (horizontal orientation) or column 1 (vertical orientation). Do not include commented-out (i.e., column/rows that begin with a hash (#)) in the column_or_row_name_position count. |
|example|1|
|additional guidance|For files following the Sample Data - Lite reporting format, the `column_or_row_name_position` value should be 1.|

### notes
|term|`notes`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|definition|Information provided would be data file specific. Details may include details on data file versioning, reporting format, software requirements, data quality, etc.| 
|example||
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/flmd_quick_guide.md#notes).| 

---

## Data Dictionary File
### column_or_row_name
|term|`column_or_row_name`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|free text|
|unit|N/A|
|definition|Column or row name from the data file. Provide entries for each column or row name from the data matrix in the data file.|
|example|temp_soil_2|
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/CSV_dd/csv_dd_quick_guide.md#column-or-row-name).|

### unit
|term|`unit`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-lite/blob/release-v1.0.0/controlled_vocabulary.md#unit)|
|unit|N/A|
|definition|Unit of measurement.|
|example|degree Celsius|
|additional guidance|Insert "N/A" when units aren't applicable.|

### definition
|term|`definition`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|free text|
|unit|N/A|
|definition|A description of the column/row header.|
|example|Soil temperature replicate 2 at location loc_25d|
|additional guidance|Definitions for reporting format terms must be used as is from the provided data dictionary template. For user-defined `{measurement_column_name}`, the measurement characteristics must be defined in the required fields that include `measured_variable` and `unit`. Optional fields, such as `statistic_*`, `representation_temporal`, and `unit_basis`, should be used to fully describe the measurement characteristics. The measurement characteristics can be repeated in the definition; however downstream resources will primarily utilize the other specific data dictionary fields.|

### measured_variable
|term|`measured_variable`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-lite/blob/release-v1.0.0/controlled_vocabulary.md#measured_variable)|
|unit|N/A|
|definition|The variable or property being measured. This field is only used for `{measurement_column_name}` column headers / rows.|
|example|temperature|
|additional guidance|N/A|

### column_or_row_long_name
|term|`column_or_row_long_name`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|recommended|
|format|free text|
|unit|N/A|
|definition|Longer human-readable column or row name. Sometimes this may be identical to Definition or even Column_or_Row_Name.|
|example|temperature_soil_2|
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/CSV_dd/csv_dd_quick_guide.md#column-or-row-long-name)|

### data_type
|term|`data_type`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-lite/blob/release-v1.0.0/controlled_vocabulary.md#data_type)|
|unit|N/A|
|definition|Data type for each column|
|example|text|
|additional guidance|N/A|

### missing_value_code
|term|`missing_value_code`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|The missing value code used for missing measurements. Only one code allowed.|
|example|-9999|
|additional guidance|Based on the CSV Reporting Format guidelines, for columns containing numeric data, ESS-DIVE recommends using "-9999" as the missing value code. For columns containing character data, ESS-DIVE recommends using "N/A" as the missing value code. If you would like to use a different missing value code, specify the used missing value code within this field. If a missing value code is not applicable for a column, leave this entry blank or use a generic missing value code.|

### unit_basis
|term|`unit_basis`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Basis for how the measurement values are quantified (e.g., “as nitrate” vs. “as nitrogen”; “per kg dry sediment”). Provide if relevant.|
|example|as carbon|
|additional guidance|This information is important for the correct interpretation of the measurement value.|

### statistic_measurement
|term|`statistic_measurement`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-lite/blob/release-v1.0.0/controlled_vocabulary.md#statistic)|
|unit|N/A|
|definition|Statistic description, if applicable. This term is only used for {measurement_column_name} headers / rows if the measured value represents repeated observations of the same scientifically-equivalent spatial location and/or temporal period (e.g., replicates), or for general uncertainty in the measurement itself.|
|example|mean|
|additional guidance|A measurement statistic typically describes variation or uncertainty in the measurement. This can be obtained / reported by an instrument or calculated via replicates. Replicates include multiple measures on the same physical sample and/or samples collected at different locations and times that are not indistinguishable for the scientific purpose. Use the spatial and / or temporal statistical descriptions, if the variability is due to multiple scientifically important locations or time periods.|

### statistic_spatial
|term|`statistic_spatial`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-lite/blob/release-v1.0.0/controlled_vocabulary.md#statistic)|
|unit|N/A|
|definition|Statistical description, if applicable. This term is only used for {measurement_column_name} headers / rows if the measured value represents a combination of individual observations from separate locations to represent a larger location.|
|example|mean|
|additional guidance|The spatial statistic should be used to describe measurement values that are a combination of separate spatial locations.|

### statistic_temporal
|term|`statistic_temporal`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-lite/blob/release-v1.0.0/controlled_vocabulary.md#statistic)|
|unit|N/A|
|definition|Statistic description, if applicable. This term is only used for {measurement_column_name} headers / rows if the measured value represents a combination of individual observations at different times to represent a larger time period. In most cases, a corresponding representation_temporal should be specified.|
|example|mean|
|additional guidance|The temporal statistic should be used when the measurement value is a combination of individual measurements made at separate times.|

### representation_temporal
|term|`representation_temporal`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-lite/blob/release-v1.0.0/controlled_vocabulary.md#representation_temporal)|
|unit|N/A|
|definition|Temporal representativeness of the measurement, if applicable. This field is only used for data dictionary rows where the column_or_row_name entry is a measured variable. In many cases, a corresponding statistic_temporal should be specified. The temporal representation will be considered instantaneous if no value is provided and datetime_measured is reported (instead of datetime_measured_start and datetime_measured_end).|
|example|month|
|additional guidance|The temporal representation should be used when the measurement value is not an instantaneous observation and/or represents a non-instantaneous time period. <br><br> If `datetime_measured_start` and `datetime_measured_end` are reported and a temporal representation is applicable, the temporal representation should match the temporal difference.|

### notes
|term|`notes`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Free text notes field|
|example||
|additional guidance|N/A|

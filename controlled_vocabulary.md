# Controlled Vocabulary for Sample Data Lite Reporting Format
Below we list the controlled vocabularies for applicable terms that can be found in ESS-DIVE's Sample Data Lite reporting format templates.

Controlled vocabularies are available for the following terms:
- Sample Data Lite File
     - [material](#material)
     - [vertical_position_reference](#vertical_position_reference)
- Data Dictionary File
     - [unit](#unit)
     - [representation_temporal](#representation_temporal)
     - [statistic](#statistic)
     - [measured_variable](#measured_variable)
     - [data_type](#data_type)

---
## Sample Data Lite File
### material
|Controlled Vocabulary|
|:-----------------------------------------------------------------|
|Gas|
|Ice|
|Liquid>aqueous|
|Liquid>organic|
|Mineral|
|NotApplicable|
|Organic Material|
|Other|
|Particulate|
|Plant Structure|
|Rock|
|Sediment|
|Soil|
|Synthetic|
|Tephra|

### vertical_position_reference
|Controlled Vocabulary|Definition|
|:----------------------------------------------------|:----------------------------------------------------|
| ground_surface | local ground surface |
| well_casing_top | top of a well casing |
| water_bed | bed or bottom of a water body (e.g., lake, river, stream) |
| water_surface | surface of a water body (e.g., lake, river, stream) |
| mean_sea_level | mean sea level |
| unknown | The vertical position reference is unknown. |
| other | The vertical position reference is known, but not in the predefined list. Provide the known vertical position reference in the notes field. |

---
## Data Dictionary File
### unit
The controlled vocabulary for the unit is based on the [Unified Code of Unified Measurements (UCUM)](https://ucum.org/ucum).
|Controlled Vocabulary|UCUM Code|
|:----------------------------------------------------|:----------------------------------------------------|
|degree Celsius|Cel|
|microsiemens per centimeter|uS/cm|
|milligrams per liter|mg/L|
|percent saturation|%{saturation}|
|pH|[pH]|
|moles per kilogram|mol/kg|
|moles per liter|mol/L|
|percent|%|
|per mille|/10*2|
|count|{count}|
|milliliter|mL|
|liter|L|
|millimeter|mm|
|centimeter|cm|
|meter|m|
|kilometer|km|
|milligram|mg|
|gram|g|
|kilogram|kg|
|feet (international)|[ft_i]|

### representation_temporal
|Controlled Vocabulary|
|:-----------------------------------------------------------------|
|year|
|month|
|day|
|2-hour|
|hour|
|30-minute|
|15-minute|
|5-minute|
|minute|
|second|
|hertz|
|other|

### statistic
|Controlled Vocabulary|Definition|
|:-------------------------------------------------------------------------------|:----------------------------------------------------|
| mean | ISO 3534: 2006-1 sample mean (average, arithmetic mean) sum of random variables in a random sample divided by the number of terms in the sum |
| minimum | Minimum value |
| median | ISO 3534: 2006-1 sample median [(*n*+1)/2]th order statistic, if the sample size (see ISO 3534-2:2006, 1.2.26) *n* is odd; sum of the (*n*/2)th and [(*n*/2) + 1]th order statistics divided by 2, if the sample size *n* is even |
| maximum | Maximum value |
| total | Sum or cumulative amount measured during the sampling period |
| standard deviation | ISO 3534:2006-1 standard deviation: positive square root of the variance; or sample standard deviation: non-negative square root of the sample variance |
| standard error | ISO 3534:2006-1 standard error: standard deviation of an estimator. An estimator of the standard error is the sample standard deviation divided by the square root of the number of samples. |
| measurement uncertainty | JCGM 200:2012, 3rd edition https://jcg m.bipm.org/vim/en/2.26.html measurement uncertainty: non-negative parameter characterizing the dispersion of the quantity values being attributed to a measured (`measured_variable`), based on the information used |
| R2 | Coefficient of determination |
| RMSE | Root mean square error |
| p-value | ISO 3534:2006-1 p-value: probability of observing the observed test statistic value or any other value at least as unfavourable to the null hypothesis |
| CV | ISO 3534:2006-1 sample coefficient of variation: sample standard deviation divided by the sample mean |
| covariance | ISO 3534:2006-1 sample covariance: sum of products of deviations of pairs of random variables in a random sample from their sample means divided by the number of terms in the sum minus one |

### measured_variable
Use the Consortium of Universities for the Advancement of Hydrologic Science (CUAHSI) [Variable Name controlled vocabulary](https://his.cuahsi.org/mastercvreg/edit_cv11.aspx?tbl=VariableNameCV&id=1157579162) for the `measured_variable` field. CHUASHI's controlled vocabulary is based upon [ODM2's variable name controlled vocabulary](http://vocabulary.odm2.org/variablename/). 

### data_type
|Controlled Vocabulary|
|:-----------------------------------------------------------------|
|text|
|numeric|
|date|
|datetime|

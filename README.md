# common-operational-datasets-schemas
[draft] JSON Schemas for datasets know to be used as as Common Operational Datasets. Draft from https://github.com/fititnt/yet-another-ontology-for-humanitarian-emergency-assistance


## Quickstart

### How to prepare the data for validation

#### Data in a format directly convertible to Geojson

To validate your data, please convert to Geojson.

The Geojson output validates? Then assume your data matches.

#### Data already Geojson

> @TODO explain

#### Tabular data not directly convertible to Geojson

For sake of convention, also inspired by [JSON API](https://jsonapi.org/),
the JSON Schemas will also validate against list of objects inside a object under an `data` key.

**Example input (CSV)**
```csv
id,value
1,ACME
2,XPTO
```

**Example output (JSON data)**
```json
{
  "data": [
    {
      "id": 1,
      "value": "ACME"
    },
    {
      "id": 2,
      "value": "XPTO"
    }
  ]
}
```

##### Example

Using csvjson (installable with `pip install csvkit`, see https://github.com/wireservice/csvkit)
and `jq` (see https://stedolan.github.io/jq/):

```bash
csvjson example-input.csv | jq '{data: .}' > example-output.json
```

### How to validate

Check <https://json-schema.org/implementations.html#validators> full list.
The only strong requeriment is a tool compatible with JSON Schema 2022-08-31 or newer.

One example of online tool is <https://json-schema.hyperjump.io/>.

One example of command line tool installable with `pip install jsonschema'[format]'` is <https://github.com/python-jsonschema/jsonschema>.


<!--
# https://www.npmjs.com/package/@jbroutier/csv-validator
yarn install -g @jbroutier/csv-validator


csv-validator example/raw/2022_cod-ab-sample_moz_adm3.hxl.csv schema/cod-ab~tabular.schema.json
csv-validator example/raw/test.temp.csv schema/test.temp.json

# pip install csvkit
csvjson example/raw/2022_cod-ab-sample_moz_adm3.csv | jq '{data: .}' > example/raw/2022_cod-ab-sample_moz_adm3.csv.temp.json

# https://github.com/python-jsonschema/jsonschema
pip install jsonschema[format]

jsonschema --instance example/raw/2022_cod-ab-sample_moz_adm3.csv.temp.json schema/cod-ab.schema.json
-->
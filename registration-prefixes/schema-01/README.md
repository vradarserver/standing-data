# Registration Prefixes Schema 1

## Files

There is one file: `reg-prefixes.csv`

## Content

The file is a comma-separated value file. Strings are optionally
delimited with double-quotes. Commas within quoted strings are
ignored. Double quotes within quoted strings are escaped with
a second double quote.

The first row contains column headings.

## Columns

There is one row per combination of:

* Prefix (some countries have more than one)
* Country
* Decoding regular expression

To be clear, you can have more than one row per country.

Some countries will also share the same prefix.

| Ordinal | Heading               | Type   | Meaning |
| ---     | ---                   | ---    | --- |
| 0       | `Prefix`              | string | The registration prefix allocated to this country. |
| 1       | `CountryISO2`         | string | The ISO2 identifier of the country that owns the prefix. |
| 2       | `HasHyphen`           | int    | 1 if the prefix is usually followed by a dash, 0 if it is not. |
| 3       | `DecodeFullRegex`     | string | Regular expression to decode a full registration (including dash) starting with this row's `Prefix`. Always contains a single group called *code*. |
| 4       | `DecodeNoHyphenRegex` | string | Regular expression to decode a full registration (excluding dash) starting with this row's `Prefix`. Always contains a single group called *code*. |
| 5       | `FormatTemplate`      | string | Template which, when "`{code}`" is replaced with an aircraft's registration code, will produce a full registration using this row's `Prefix`. |

### Future-proofing
The schema allows for new columns to be added in the future, with the
following caveats:

* The ordinal, heading, type and meaning of existing columns will not change
  in future versions of the file.
* New columns will always be added after existing columns.


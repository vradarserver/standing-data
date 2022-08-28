# Countries Schema 1

## Files

There is one file: `countries.csv`

## Content

The file is a comma-separated value file. Strings are optionally
delimited with double-quotes. Commas within quoted strings are
ignored. Double quotes within quotes strings are escaped with
a second double quote.

The first row contains column headings.

## Columns

There is one row for each country.

| Ordinal | Heading   Type    | Meaning |
| ---     | ---       ---     | --- |
| 0       | `ISO`    | string | The ISO2 identifier of the country. |
| 1       | `Name`   | string | The name of this country. |

### Future-proofing
The schema allows for new columns to be added in the future, with the
following caveats:

* The ordinal, heading, type and meaning of existing columns will not change
  in future versions of the file.
* New columns will always be added after existing columns.

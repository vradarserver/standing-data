# Airlines Schema 1

## Files

There is one file: `airlines.csv`

## Content

The file is a comma-separated value file. Strings are optionally
delimited with double-quotes. Commas within quoted strings are
ignored. Double quotes within quotes strings are escaped with
a second double quote.

The first row contains column headings.

## Columns

There is one row for each airline.

| Ordinal | Heading                    | Type   | Meaning |
| ---     | ---                        | ---    | --- |
| 0       | `Code`                     | string | The code that the rest of the schema-01 data uses to refer to the airline. Either the ICAO or IATA code. |
| 1       | `Name`                     | string | The name of the airline. |
| 2       | `ICAO`                     | string | The 3 character alphabetical unique code assigned to the airline by ICAO. |
| 3       | `IATA`                     | string | The 2 character alphanumeric code assigned to the airline by IATA. Not unique. |
| 4       | `PositioningFlightPattern` | string | A regular expression pattern that identifies the airline's positioning flights. |
| 5       | `CharterFlightPattern`     | string | A regular expression pattern that identifies the airline's charter flights. |

,,,,,

### Future-proofing
The schema allows for new columns to be added in the future, with the
following caveats:

* The ordinal, heading, type and meaning of existing columns will not change
  in future versions of the file.
* New columns will always be added after existing columns.

# Airports Schema 1

## Files and Folders

The folders are based on the airport's code, which is either its
`ICAO` code or, if that is not known, then it's its `IATA` code.

The folder is the first letter of the airport's code.

The airport details are stored within a CSV file whose name is formed from
the first two digits of the code.

E.G. the details for an airport whose code is EGLL would be found in:

```
E
+- EG.csv
```

The reason for this is to try to avoid very large CSV files.

## Content

The file is a comma-separated value file. Strings are optionally
delimited with double-quotes. Commas within quoted strings are
ignored. Double quotes within quoted strings are escaped with
a second double quote.

The first row contains column headings.

## Columns

There is one row for each airport.

| Ordinal | Heading        | Type   | Meaning |
| ---     | ---            | ---    | --- |
| 0       | `Code`         | string | The code that the rest of the schema-01 data uses to refer to the airport. Either the ICAO or IATA code. |
| 1       | `Name`         | string | The name of the airport. |
| 2       | `ICAO`         | string | The 4 character alphanumeric unique code assigned to the airport by ICAO. |
| 3       | `IATA`         | string | The 3 character alphabetical unique code assigned to the airport by IATA. |
| 4       | `Location`     | string | The city or town nearest to the airport. |
| 5       | `CountryISO2`  | string | The ISO-2 code of the country that the airport is in (or one of them if the airport straddles a border). |
| 6       | `Latitude`     | number | The latitude of the airport. |
| 7       | `Longitude`    | number | The longitude of the airport. |
| 8       | `AltitudeFeet` | number | The altitude of the airport in feet. |

### Future-proofing
The schema allows for new columns to be added in the future, with the
following caveats:

* The ordinal, heading, type and meaning of existing columns will not change
  in future versions of the file.
* New columns will always be added after existing columns.

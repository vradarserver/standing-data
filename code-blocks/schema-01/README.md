# Code Blocks Schema 1

## Files

There is one file: `code-blocks.csv`

## Content

The file is a comma-separated value file. Strings are optionally
delimited with double-quotes. Commas within quoted strings are
ignored. Double quotes within quoted strings are escaped with
a second double quote.

The first row contains column headings.

## Columns

There is one row for each code block.

Code blocks are not independent ranges, there are overlaps. For a given ICAO you should
look for the smallest range that contains the Mode-S code that you are searching for.

| Ordinal | Heading              | Type   | Meaning |
| ---     | ---                  | ---    | --- |
| 0       | `Start`              | hex    | The ICAO code at the start of the block. |
| 1       | `Finish`             | hex    | The ICAO code at the end of the block. |
| 2       | `Count`              | number | The number of codes in the block. |
| 3       | `Bitmask`            | hex    | The bitmask to use when searching for a block. Always the same as `Start`. |
| 4       | `SignificantBitmask` | hex    | The bitmask to use when searching for a block. Always ((NOT `Finish`) OR `Bitmask`) AND 0xFFFFFF. |
| 5       | `IsMilitary`         | number | 1 if the block is for use by military, 0 otherwise. |
| 6       | `CountryISO2`        | string | The ISO2 code of the country that owns the code block. |

,,,,,

### Future-proofing
The schema allows for new columns to be added in the future, with the
following caveats:

* The ordinal, heading, type and meaning of existing columns will not change
  in future versions of the file.
* New columns will always be added after existing columns.

## Bitmask and SignificantBitmask

There is code out there that uses these fields to find the appropriate code block for
an aircraft's ICAO identifier. The method used is:

* Iterate through each code block in descending order of `SignificantBitmask`.
* AND the aircraft Mode-S identifier with the `SignificantBitmask`.
* If the result equals the `Bitmask` then the code block matches.
* Stop searching as soon as you find a match.

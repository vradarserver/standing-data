# Aircraft Schema 1

## Content

As of the time of writing most of the aircraft lookup data stored on the
database originally came from `PlaneBase`. None of the `PlaneBase` data
is reproduced here.

The last update from `PlaneBase` was in April 2021. Between April 2021 and
June 2022 the lookup data was not updated.

In June 2022 the SDM site began accepting user submissions and corrections
of aircraft lookup data.

The data represented here is **just** the aircraft lookup data submitted by
VRS users since June 2022. This is quite a small subset of the lookup data.


## Files and Folders

The folders are arranged in two levels and are based on the aircraft's
Mode-S ICAO identifier when converted to upper-case base-16 and padded with
leading zeros to 6 digits.

For example, if an aircraft's Mode-S identifier is 1234 then after
conversion to 6 digit hex its ICAO would be 0004D2.

The top level folder is the 1st digit of the ICAO.

The second level folder is the 1st and 2nd digits of the ICAO.

The aircraft's details are stored within a CSV file whose name is formed
from the first three digits of the ICAO.

E.G. the details for an aircraft whose ICAO is 407AF3 would be found in:

```
4
+- 40
   +- 407.csv
```

The reason for this is to try to avoid very large CSV files.

## Content

The file is a comma-separated value file. Strings are optionally
delimited with double-quotes. Commas within quoted strings are
ignored. Double quotes within quotes strings are escaped with
a second double quote.

The first row contains column headings.

## Columns

There is one row for each aircraft.

| Ordinal | Heading                | Type   | Meaning |
| ---     | ---                    | ---    | --- |
| 0       | `ICAO`                 | string | The six hex digit Mode-S ICAO code (upper-case) assigned to the aircraft. |
| 1       | `Registration`         | string | The aircraft's registration. |
| 2       | `ModelICAO`            | string | Either the aircraft's ICAO8643 model type code or a fake model type code. |
| 3       | `Manufacturer`         | string | The manufacturer of the aircraft. |
| 4       | `Model`                | string | The aircraft model. |
| 5       | `ManufacturerAndModel` | string | The manufacturer and model. Sometimes it uses a truncated form of the manufacturer's name. |
| 6       | `IsPrivateOperator`    | number | 1 if the operator is a private individual, 0 if it is a business. |
| 7       | `Operator`             | string | The name of the operator if it is a business or `Private` if it is a private individual. |
| 8       | `AirlineCode`          | string | The `Code` of the airline that operates the aircraft. |
| 9       | `SerialNumber`         | string | The aircraft's serial number as assigned during manufacture. |
| 10      | `YearBuilt`            | number | The year of manufacture. |

### Future-proofing
The schema allows for new columns to be added in the future, with the
following caveats:

* The ordinal, heading, type and meaning of existing columns will not change
  in future versions of the file.
* New columns will always be added after existing columns.

## Fake Model Types
Fake model type codes always begin with a hyphen. Genuine ICAO 8643 codes do not begin with a hyphen. The fake codes
are:

| Code | Meaning |
| ---  | --- |
| -GND | Ground vehicle. |
| -TWR | Tower or other fixed installation. |

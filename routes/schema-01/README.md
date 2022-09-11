# Route Schema 1

## Callsigns

The SDM database stores routes against callsigns. Callsigns are formed from
the airline's 3 character alphabetical code followed by a number of up to
four digits. The number can have either one or two characters at the end.

Private aircraft, and aircraft with no filed flight plan, use their registration
as a callsign. Virtual Radar Server does not try to resolve routes for these.

The callsign transmitted by ADS-B is typically entered into the aircraft's
systems by a pilot, which can lead to inconsistencies.

Both Virtual Radar Server and the SDM site normalise a callsign before using
it in lookups of routes.

### Normalisation

The callsign is split into a code portion and a number portion. This is done
using a regular expression like this:

```
^(?<code>[A-Z]{2,3}|[A-Z][0-9]|[0-9][A-Z])(?<number>\d[A-Z0-9]*)
```

That will allow for either an ICAO or IATA code and a number of any length.

If the pilot had entered their airline's IATA code then this is swapped out
for the ICAO. If an airline has both an ICAO and an IATA code then the repository
will only show callsigns against the airline's ICAO.

The leading zeros are then stripped from the number. However, if this leads
to a number that is either empty, or just letters, then a single zero is added
back to the start of the number.

Finally the number is checked for validity. After trimming it cannot be longer
than four characters. Either the last or the last two characters can be alphabetical.
If "n" is a digit and "A" is a letter then all possible valid combinations for the
number are:

```
n
nn
nA
nnn
nnA
nAA
nnnn
nnnA
nnAA
```

#### Examples

Here are some callsigns before and after normalisation (where the airline with
the ICAO code EZY also has the IATA code U2):

| Before  | After |
| ---     | --- |
| EZY1200 | EZY1200 |
| EZY0001 | EZY1 |
| EZY0000 | EZY0 |
| EZY00AB | EZY0AB |
| U21234  | EZY1234 |

## Files and Folders

The routes are split into folders that are named after the first character of the
callsign's code.

The routes are then stored in files named after the callsign's code. There are
two naming conventions for routes depending on whether there are more than 10,000
routes recorded for the code.

### Up to 10,000 routes

All of the routes are stored in a single file named `<code>-all.csv`, where `<code>`
is the callsign code in upper-case.

The -all suffix is used to avoid clashing with reserved filenames in Windows and DOS.

### More than 10,000 routes

The routes are split across up-to ten files named `<code>-<digit>.csv`, where
`<code>` is the callsign code and `<digit>` is the first digit of the callsign's
number.

The reason for this is to try to avoid very large CSV files.

## Content

The file is a comma-separated value file. Strings are optionally
delimited with double-quotes. Commas within quoted strings are
ignored. Double quotes within quotes strings are escaped with
a second double quote.

The first row contains column headings.

## Columns

There is one row for each callsign.

| Ordinal | Heading        | Type   | Meaning |
| ---     | ---            | ---    | --- |
| 0       | `Callsign`     | string | The normalised callsign. |
| 1       | `Code`         | string | The code portion of the callsign. |
| 2       | `Number`       | string | The number portion of the callsign. |
| 3       | `AirlineCode`  | string | The code that should be used to lookup the owning airline. |
| 4       | `AirportCodes` | string | A hyphen-separated list of airport codes for each airport in the route, in the order that they are flown. |

The airline and airport codes are guaranteed to be `Code` fields in the schema-01 airline and airport CSV files.

### Future-proofing
The schema allows for new columns to be added in the future, with the
following caveats:

* The ordinal, heading, type and meaning of existing columns will not change
  in future versions of the file.
* New columns will always be added after existing columns.

# Standing Data

This repository will eventually hold CSV files (ideally with full git
history, where appropriate) of the aviation data currently stored by the
SDM site and used by Virtual Radar Server.

However, I have to write the utilities to build the history and the files
first :) So it might take a little while for the full set to get here.

## Pull Requests

In principle this repository could be used as a way of making large-scale
changes to the SDM data without having to submit each record through the site.

I'm in two minds about this. I can see that it would make it easier to
submit changes but the nice thing about the batched one-by-one approach is
that someone can review and fix-up all of the data before it gets added to
the database. Mass edits of text files could be harder to review.

Also I would have to write something to copy the changes from the text files
to the SDM database.

For the time being pull requests will be declined for this repository.

## Aircraft Lookup Data

As of the time of writing most of the aircraft lookup data stored on the
database originally came from `PlaneBase`. None of the `PlaneBase` data
will be reproduced here.

The last update from `PlaneBase` was in April 2021. Between April 2021 and
June 2022 the lookup data was not updated.

In June 2022 the SDM site began accepting user submissions and corrections
of aircraft lookup data.

It is my intention to add the aircraft lookup data submitted by VRS users
since June 2022 to this repository. This will obviously be quite a small
set when compared to the `PlaneBase` set, but c'est la vie.

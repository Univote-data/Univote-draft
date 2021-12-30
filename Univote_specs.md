# Univote specifications (draft)
Version 0.1

Files using the Univote format are json files respecting a set of specifications, described here.  
This is a temporary draft, not the actual official specifications.

Phrases in bold are definitions which are supposed to be the most consistent in the structure between Univote files.

"Divisible object" refers to any object containing "divs", a list of Division objects specifying results of setsets of the divisible object.

# Objects in Univote
The highest object in a file must contain two objects: Definitions, and Data

## Definitions object
This object contains various informations about the election, either more useful to the program such as the electoral system used, the aliases for some properties (whether "none of the above" votes are counted as "valid votes" for example); or more useful to human readers such as the date, or some textual context.

## Data object
This is the main object containing all the data. It contains `"elections"`, a list of Election objects.

## Election object
**The election object defines one election**. It contains `"votings"`, a list of Voting objects, and can contain `"nationalResults"`, a Result object containing a summary of national results with either only the number of seats of with a normalized votes count between the Voting objects (which is widely agreed upon)

## Voting object
**The voting object defines a subset of the election where the electoral rules are mostly identical**. It is a divisible object.

> For example, a file describing general elections in the UK would contain 1 with all the constituencies, legislative elections in Israel would contain 1 for the national results, federal elections in Germany would contain 2 (1 for the FPTP part by constituency and 1 for the PR part by state), and legislative elections in Taiwan would contain 3 (1 for the FPTP constituencies, 1 for the aboriginal seats, and 1 for the national PR). Elections in the US may have one voting object per state since the structure of the vote and electoral law can heavily differ between the states.

## Division object
The Division object is a subset of a Voting or another Division object. **It describes a given division or subdivision and can give either a tally or a sub-result**. It can contain a Results object.

> For example, in Spain Division objects may be used for autonomous communities (for tallying), provinces (special case, section object, see below), and municipalities (for detailing sub-results).

### Section object
Section objects are Division objects with a `"section": true` attribute. It is the most fundamental object in the document. **A Section object describes the largest independent unit of voting, for which moving votes between sub-components cannot affect the results**. ~~It must have a magnitude of at least 1 (meaning it must be legally able to independently elect at least one person in the case of an election)~~ (<- debated)

> For example, sections may define: Constituencies in British general elections, national results in Israeli legislative elections, constituencies and states respectively for the FPTP and PR components of German federal elections; and constituencies, aboriginal constituencies, and nationwide results respectively for the FPTP, Aboriginal, and PR components of Taiwanese legislative elections.

## Results object
The Result object stores a single set of results from a vote, and all the data associated to this set of results. The format of the voting object is highly dependant on the voting system defined in the Definitions object, can widely vary dependending on the level of information inputted, and should be able to accomodate edge cases such as cardinal (ranking) or ordinal (scoring) systems.

The Results object is defined [here](Univote_specs_res.md).

Note: if multiple rounds are held, they are grouped by Section. The way multiple rounds and re-runs are grouped remains to be determined.
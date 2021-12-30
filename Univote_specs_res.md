# Univote specifications - Results & Candidacies (draft)

## Results object

The Results object contains a number of values and attributes to give informations about the results (such as the number of valid votes), and `"candidacies"`, a list of Candidacy objects.

Currently-defined attributes and values are:
- `"population"` (num): the population of the division
- `"registeredVoters"` (num): the number of registered voters
- `"participatingVoters"` (num): the number of voters turning out to vote
- `"abstentions"` (num): the number of non-participating registered voters
- `"invalidVotes"` (num): the number of invalid votes (not counted in the results percentages)
  - A number of specific reasons should be included, they remain to be determined.
- `"validVotes"` (num): the number of valid votes (counted in the results percentages)

## Candidacy object
All candidacy objects have the `"type"` attribute, set either to `"list"` or `"person"`, defining whether it is a group of people or a single person. There is also the `"choice"` value for referendums or ballot measures.

Some attributes can be present for any type of candidacy (but they do not have to be used in all cases).

- `"name"` (str): Contains either the name of the list, person, or option. Capitalization should follow the ballot paper, official announcements, or common usage.
- `"firstName"` (str, person only): Contains the first name of the person. Capitalization should follow the ballot paper, official announcements, or common usage.
- `"lastName"` (str, person only): Contains the last name of the person. Capitalization should follow the ballot paper, official announcements, or common usage.
- `"party"` (str or list[str], person or list only): Contains the partisan affiliation of the person or list (will have to be defined more clearly)
- `"support"` (list[str]): Contains the list of parties supporting the list, candidacy, or choice.
- `"components"` (list[Candidacy], person or list only): Contains the list of sub-components (for example members of lists, or sub-apparented lists)
- `"elected"` (bool, person or choice): Indicates whether the person has been elected
- `"qualified"` (bool): Indicates whether the person or list is qualified for the next round
- `"baseRank"` (num): Indicates the base rank on a list, or the order of apparition on the ballot (may have to be splitted)
- `"rerank"` (num): Indicates the rank after the vote has occured, not necessarily by number of votes (such as in the Netherlands where candidates passing the threshold are re-ranked higher, then the base rank is followed)
- `"votes"`: (num): Indicates the number of votes received by the person or candidacy
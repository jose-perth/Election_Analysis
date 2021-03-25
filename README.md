# Election_Analysis

## Overview of Project

This project is the third weekly challenge of the Data Science Bootcamp.  It allows us to put into practice and showcase the skills learned in Module 3 of the bootcamp.

### Purpose

The Colorado Board of Elections has requested information to be computed from their input file. This information will be included as part of an election audit.

The information requested includes:

- Total number of votes cast
- County information:
    - The voter turnout for each county
    - The percentage of votes from each county out of the total count
    - The county with the highest turnout
- Complete list of candidates who received votes
- Total number of votes each candidate received
- Percentage of votes each candidate won
- The winner of the election based on popular vote

## Results

Analysis of the input file was carried out using Python 3.9.2.  The output file is [election_results](/analysis/election_results.txt).

input file :arrow_right: [Python Script](PyPoll_Challenge.py)    :arrow_right: [election_results](/analysis/election_results.txt)

The input file is a CSV file with a hearder row and the following information for the ballots:

- ballot ID
- county
- candidate

Note: the input file **election_results.csv** is too large to be displayed in GitHub, but it can be downloaded from the folder [resources/](resources/).

### Election Audit Results

Below is a snapshot of the election audit results requested by the Colorado Board of Elections.

[![election results](/resources/election_results_snapshot.png "Election Results")](/resources/election_results_snapshot.png)

We can further discuss the information requested by the Colorado Board of Elections.

- Total votes: there were 369,711 ballots in the input file.
- County votes: votes were tallied by county and a percentage of votes for each county with respect to the total number of votes presented to 1 decimal place.

| County    | Percentage Votes  | Votes |
|:---       |:---:              |---:   |
| Jefferson  | 10.5% | 38,855 |
| Denver | 82.8% | 306,055 |
| Arapahoe | 6.7% | 24,801|

  The code used to calculate and display the percentage value is:

```python
# 6c: Calculate the percentage of votes for the county.
        vote_percentage = float(votes) / float(total_votes) * 100
        county_results = (
            f"{county_name}: {vote_percentage:.1f}% ({votes:,})\n")
```

  Note the ` :.1f ` used to display the value to 1 decimal place.

- Denver has the largest number of votes with 306,055, or 82.8% of the total number.
- Candidate votes: votes were tallied by candidate and a percentage of the total calculated for each candidate, to 1 decimal place.

| Candidate    | Percentage Votes  | Votes |
|:---       |:---:              |---:   |
| Charles Casper Stockham | 23.0% | 85,213 |
| Diana DeGette | 73.8% | 272,892 |
| Raymon Anthony Doane | 3.1% | 11,606 |

- The analysis determined that the candidate ***Diana DeGette*** obtained the most votes with 272,892 votes, which corresponds to 73.8% of the total vote count.

A text file with these results is available at [`analysis/election_results.txt`](analysis/election_results.txt).

## Election Audit Summary

The script created is able to provide the information requested by the Colorado Board of Elections.  

However, it can be enhanced to cover other needs that may arise in the future.  Including:

1. Ability to read and tabulate from multiple input files with a similar format. Python's `os` library provides methods such as `os.scandir()` and `os.walk()` that can be used to process multiple files in one run. For example the code below can be used as a first loop:

```python
    directory = os.path.join('input_files')
    for filename in os.scandir(directory):
```

2. Ability to identify and report duplicate Ballot ID's. Although this will increase the processing time due to the searchs involved, this step could be critical when dealing with input files from multiple sources as further action may be required for those ballots. As a first step on the analysis, each ballot ID must be checked against a master ballot list and added to it if it doesn't exists. Similar to existing code:

```python
    if ballot_id not in ballot_master:
        # Add the ballot ID to the ballot list.
        ballot_master.append(ballot_id)
```

3. Provide candidate totals by County to help audit County level elections. Initial pseudocoding points to nested dictionaries to store the `candidate_votes` dictionary in a `county_votes` dictionary.
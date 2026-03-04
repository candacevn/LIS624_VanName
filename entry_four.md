# Entry four
This entry will contain notes related the PQF and yaz commands as used for command-line library searches.

## man page for yaz
If you want to check out the man page for yaz, enter ``` man yaz-client ``` . There are lists of commands stored there that are useful for searching!

## Loading ``` yaz-client ``` and connecting to the OPAC
* Enter the command ``` yaz-client ```
* ``` Z> ``` should begin all lines while ``` yaz-client ``` is launched
* Connect to the UK OPAC via ``` open saalck-uky.alma.exlibrisgroup.com:1921/01SAA_UKY ```

## Prefix Query Format (PQF) for queries!
* Boolean operators ``` @add ``` , ``` @or ``` , ``` @not ``` etc. go directly after ``` find ```
* Examples of field search formats: ``` @attr 1=4 "title field term" ``` , ```@attr 1=21 "subject heading term" ``` , ``` @attr 1=1 "name, personal term" ```

## Basic commands for yaz
* ``` find ``` begins all search requests!
* ``` show #  ``` where the # is the number of the record you would like to see
* ``` quit ``` to exit out of yaz

### Using the man: Sort command
* ``` sort ``` sorts result sets!
* Command format is ``` sort #=#,#=# < ```
* ``` #=# ``` indicates specifc field (multi-field sorts use commans and NO spaces).
* ``` < ``` and ``` > ``` are flags used to specify sort ascending and descending, respectively.

## Downloading resultss in yaz
* To download only the records examined with ``` show ```, use the option ``` -m ```
* Format is ``` yaz-client -m recordname.marc ```
* Conduct a search using ``` yaz-client ```, making sure to ``` show ``` results.

* To download all records for a specific query, use the command ``` set_marcdump ```
* Format is ``` set_marcdump  recordname.new ```
* Conduct a search, making sure to use ``` show 1 +# ``` where 3 is the total


## Converting bib record file types
* Use ``` head recordname.marc ``` to view the first lines of the file.
* Check the file type using ``` file recordname.marc ```

### JSON
* Basic convertion can be done using ```yaz-marcdump```
* Format conversion command: ``` yaz-marcdump -o json recordname.marc > recordname.json ```
* For better readabiliy use the ``` JQ ``` command
* Readable format command: ``` jq . recordname.json > recordname-formatted.json ```
* Simple file scan command: ``` less recordname-formatted.json ```
* Advanced file searches utilize MARC and JQ formats

### XML
* Format conversion command resembles json conversion: ``` yaz-marcdump -o marcxml recordname.marc > recordname.xml ```
* Query XML files using ```xmlstarlet ``` , similarly to jq querying

# Some Takeaways
This entry was super long, so here is a quick summary for future-me and others interested in this repository:
* yaz-client is a Z39.50 protocol information retrieval client
* Z39.50 protocol is an important coomunications standard for information searching and retrieval.

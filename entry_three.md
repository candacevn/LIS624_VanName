# Entry Three
These notes will focus on grep, uploading files, and reading .bib files!

## Regular expressions "regex":
* ``` ^ ``` regex indicates the beginning of the line. Format ``` ^term1 ```.
* ``` $ ``` indicates end of the line. Format ``` term$ ```.

## Command line options: 
* Count matches- ``` -c ``` retrieves the frequency of total lines containing the search term 
* Case matching- ``` -i ``` performs searches while ignoring case-sensitivity 
* Invert matching- ``` -v ``` searches for lines that do not contain the search term 
* Alternate matching- ``` | ``` Called an infix operator. performs the Boolean operator OR function. Format ``` (term1|term2) ```. 
* Whole word matching- ``` -w ``` searches for the term as the whole word, not as part of a word as is the default. 
* Context matches- ``` -bnum ``` or ``` -anum ``` where num is a value you substitute. The value will indicate the number of lines surrounding (before or after) the matching line to retrieve in addition. 
* Halt matching- ``` -mnum ``` where the value is the number of retrieved lines to stop at. 
* Return line numbers for each hit- ``` -n ``` 
* Character class matching- ``` [num1-num2]{num3} ``` or ``` [let1-let2]{num1} ``` character classes and repetition; character classes ``` {let1-let2} ``` indicate whether the search is for letters or numbers, and the range to look within. Repetition ``` {num} ``` indicates how many of the characters in the specified range to look for. Other function ``` char1.{num}char2 ``` allows the user to search for a term beginning and ending with specified characters and with a specified number of characters between. 

## Uploading files: 
Using the browser, there is a button at the top that allows you to upload a file! If for some reason that doesn’t work, try running the following: gcloud compute scp file_name "server_name":~/ --zone "zone_name" --project "project_name" 

## .bib file structure: 
* View the full file using less file.bib 
* Entry types- begin with an ``` @ ```. To search for entry types, use ``` grep ^@ file.bib ```. 
* Cite key follows the entry type, and begins with the author’s last name 
* Tags and fields are followed by ``` = ```.

## Takeaways
* I learned how to use regular expressions and command line options to format searches in bib records.
* I felt like this process was easier the more I looked into and noted the different regx and command line options.
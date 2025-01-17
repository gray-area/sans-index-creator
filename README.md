# sans-index-creator

Forked from GeOrg3

https://github.com/Ge0rg3/sans-index-creator

## Requirements

The following steps require a Linux system in order to perform the actions. Additionally, the following packages will need to be installed. 

qpdf

``sudo apt-get install qpdf``

pdftotext

``sudo apt-get install poppler-utils``

## How to use

1) Download course pdf's from https://www.sans.org/account/download-materials. Download each book individually, not the combined version.

2) Create a password file, paste your SANS password in it and save it.

    ```
    nano password.tx
    Paste or enter your SANS password.
    ctrl+x
    y
    Enter
    ```
  
3) Remove pdf password through qpdf:

    ```qpdf --password-file=password.txt -decrypt "SANS_Book_1.pdf" "SANS_Book_1_unlocked.pdf"```
  
4) Convert new pdf to txt:

    ```pdftotext SANS_Book_1_unlocked.pdf SANS_Book_1_unlocked.txt```
  
5) Create index based off txt file (this can take ~5 minutes because each word is searched for in the full English dictionary):

    ```python3 sans_indexer.py -i SANS_Book_1_unlocked.txt -o SANS_Book_1_Index.txt -n "John Smith"```

Please note that the -n field is used to split the txt into pages, as we use the License name as the page delimiter (it is the only string persistant across pages). You will need to enter YOUR first and last name where "John Smith" is noted in the comand above. 

**NOTE**: Repeat steps 3-5 for each book, changing the "1" in the file name to the corresponding book.

Combine the indexes created by `sans_indexer.py` into one index with the following command:

    python3 index_combiner.py SANS_Book_1_Index.txt SANS_Book_2_Index.txt SANS_Book_3_Index.txt > combined_index.txt. 

This will create an index which displays both book number and page number of each keyword.

## How Does it Work?

For something to be counted as a "word" (and therefore added to the index), it has to meet certain criteria:

```
* At least 3 chars once certain characters/phrases are stripped from it
* Not in the English dictionary
* Does not start with number
* Is not a link
```

## Output example
Here is a snippet of the output for a course pdf:
```
shell-item: 2(38)
shellbag-hives: 2(59)
shellbag: 3(110, 260)
shellbags: 1(113, 286) | 3(244, 286)
shelllinkheader: 2(9)
shellnoroam: 2(55) | 3(287)
shift+delete: 2(225)
shimcache: 1(47, 208) | 2(239) | 3(5)
shimcacheparser.py: 1(210)
shimcacheparser: 1(210)
showkeys: 1(136)
sic-c: 1(275)
sid: 2(224, 225, 263, 264, 269) | 3(286)
siem: 1(257) | 2(180)
sign-out: 3(229)
signed-off: 3(229)
signedin_time: 3(205, 206, 287)
signedinuser.json: 3(186)
signons.sqlite: 3(128)
simple-to-create-and-modify: 1(46)
sin: 2(19)
single-use: 3(194)
single-user: 1(11)
sister: 1(89)
site-by-site: 3(189)
site-specific: 3(181)
site/remove: 3(248)
site_engagement: 3(205, 287)
sitecollectionadminadded: 1(243)
sites/: 3(197)
six: 1(17, 19, 36) | 2(180, 263) | 3(174, 187)
siz: 2(151)
sizeofimage: 1(213)
skydrive: 1(10, 11, 231)
skype: 1(10, 36, 37, 75, 86, 89, 117, 223, 230) | 2(28, 69, 130, 201, 275, 330) | 3(110, 260, 287)
sleuthkit: 1(136)
```

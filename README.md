# ECE459 Lab 2 Output Comparison Tool
A comparison tool for Lab 2 of the University of Waterloo's Winter 2023 offering of [ECE459](https://github.com/jzarnett/ece459/).

This tool identifies incorrectly-formatted outputs and finds differences between outputs.

## Usage
`python3 compare.py <FILE_1> <FILE_2> [TOLERANCE]`
- `FILE_1`: the path to the first file to compare
- `FILE_2`: the path to the second file to compare
- `TOLERANCE`: optional non-negative tolerance for comparing counts between outputs. Ignores differences in values `v1` and `v2` where `|v2 - v1| <= TOLERANCE`. Default value is 0.

## Examples
### Comparison of Equal Files
`python3 compare.py demo/sample2.txt demo/sample2.txt 1`
```
Files match within specified tolerance
```

### Comparison of Unequal Files 
`python3 compare.py demo/sample1.txt demo/sample2.txt 2`
```
Detected inconsistency in file 'demo/sample1.txt':
        Mismatch between declared double dictionary length (20) and actual dictionary length (21)

Detected mismatches while comparing files:
        Found mismatches in header:
                Mismatch in declared double_dict_len: 20 vs. 21
                Mismatch in declared triple_dict_len: 26 vs. 27
                Mismatch in declared all_tokens_len: 19 vs. 14

        Found mismatches exceeding tolerance for double_dict with keys:
                'Found^block': 9 vs. 4

        sample token sets are not equal
                Set 1 contains additional token(s) {'rdd_42_21'}
                Set 2 contains additional token(s) {'split:'}

        dynamic token sets are not equal
                Set 2 contains additional token(s) {'rdd_42_20'}
```
### Incorrectly-Formatted File
`python3 compare.py demo/sample1.txt demo/badformat.txt`
```
Encountered error while parsing file 'demo/badformat.txt'
Format error: mismatched regex at line 1
        Expected line with format 'double dictionary list len (\d+), triple (\d+), all tokens (\d+)'
        Received 'quadruples'
```

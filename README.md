# Esoteric Errors: issues without enough Google results

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fjacksenk%2Fesoteric-errors&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=Views&edge_flat=false)](https://hits.seeyoufarm.com)

A record of esoteric and hard to Google issues and solutions to help future searchers, or more likely myself

## GENERIC_INTERNAL_ERROR: length of field blocks differ: field 0: 320, block 18: 0

Date: 2022-01-17

Related: Athena (Presto), DynamoDB, Glue, Parquet

Issue: When Athena attempts to scan a parquet file it throws an error similar to `GENERIC_INTERNAL_ERROR: length of field blocks differ: field 0: 320, block 18: 0`

Context: Using AWS Glue to import records from DynamoDB and convert them to Parquet; the Parquet files were valid and could be openned and examined using tools such as `parquet-tools` but Athena refused to read them

Cause: The Parquet file had a column which was a struct, the struct had a duplicated field with different casing, i.e. myField1 vs myfield1

Solution: Ensure no duplicated (irrespective of case) fields exist within nested objects (merge myField1 and myfield1 into one, or drop one)

## SYNTAX_ERROR: line 1:8: SELECT * not allowed from relation that has no columns

Date: 2022-01-19

Related: Athena, Lake Formation

Issue: Table does have columns but scanning returns an error claiming no columns exist

Cause: Lack of permissions

Solution: Ensure you've granted sufficient permissions in Lake Formation to describe and select the table

#backend development report

## SparkSQL issues
- Lack of support for `create temporary table tbl as ...` forces ad hoc management of temporaries
- dots not supported in names even with quoting.
- case insensitive
- lack of support of ant-joins, set ops



## dplyr issues
- difficult to add a new win fucntion
- mistakenly incomplete src_translate_env difficult to track down; maybe better defaults?
- had to rewrite INSERT INTO for only small diff from other dbs
- had to rewrite join lack of USING clause
- had to rewrite semi-join because of small syntax difference
- lots of rewriting in joins, reasons starting to fade from memory
- monkey patch for outer, unique_name (no longer needed) and n_distinct (nice to have)
- rewrite _mutate for seq eval
_ rewrite _filter to support new col in expression (aka HAVING)
- boilerplate for missing capabilities like commit and rollback
- monkey patch for over because of syntax differences
- more, a code search for dplyr will reveal all of them


*rewrite*  means that I had to duplicate a chunk of code which may represent a maintenance burden in the long run and may drift from the dplyr original. Unfortunately it was not clear and in most cases it seemed impossible to extend the original behavior using NextMethod. The custom code is not a lot but is stuck somwhere in the middle of the parten class method. So unfortunately there is code duplication between dplyr and dplyr-spark. All the duplications are marked for proper credit and as maintenance markers. In case of bugs, check  if the tbl_sql or DBIconnection method by the same  name has changed.

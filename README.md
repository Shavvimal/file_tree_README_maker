# Readme tree with link generator
## Renaming Files
Ensure all file names dont include spaces. Use this command to rename all files in the cwd by removing all the spaces and replacing with underscores:

```for f in *.*; do mv "$f" "${f// /_}"; done```
## Recursively rename files
Replace all spaces in current working directory recursively with an underscore

```while read line ; do mv "$line" "${line// /_}" ; done < <(find ./ -iname "* *")```

Remove all spaces in current working directory recursively

```while read line ; do mv "$line" "${line// /}" ; done < <(find ./ -iname "* *")```

## Generate README.md
use:

```find DIR -type f \( -name '*.[ch]' -o -name '*.cpp' \) | sort -t '/' -k 1 -k 2 | awk -v base=BASE -f path/to/script >> README.md ```

where

```DIR``` is ```.``` or dirname, for a compact result avoid '/'s. 
The sort step is optional. ```BASE``` is a path prefix, e.g. 'https://github.com/ApolloDataTeam/TBM-analysis/blob/main/'

example:

```find . -type f \( -name '*.ipynb' -o -name '*.pkl' -o -name '*.csv' -o -name '*.sql' -o -name '*.py' -o -name '*.png' \) | sort -t '/' -k 1 -k 2 | awk -v base=https://github.com/ApolloDataTeam/TBM-analysis/blob/main/ -f ./scr.bash >> README.md ```
## Generate list without hierachy
use:
```find . -name "*" | sed "s|^\./\(.*\)|* \[\1\]($url/$repo/$branch/\1)|"```
## Example for this Repo
Run: 

```find . -type f \( -name '*.bash' -o -name '*.md' \) | sort -t '/' -k 1 -k 2 | awk -v base=https://github.com/Shavvimal/file_tree_README_maker/blob/main/ -f ./scr.bash >> README.md ```

to get: 

 * [README.md](https://github.com/Shavvimal/file_tree_README_maker/blob/main/README.md)
 * [scr.bash](https://github.com/Shavvimal/file_tree_README_maker/blob/main/scr.bash)

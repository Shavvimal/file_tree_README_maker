# Readme tree with link generator
## Renaming Files
Ensure all file names dont include spaces. Use this command to rename all files in the cwd by removing all the spaces and replacing with underscores:

```for f in *.*; do mv "$f" "${f// /_}"; done```
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
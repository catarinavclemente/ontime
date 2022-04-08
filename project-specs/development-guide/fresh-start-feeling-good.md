# Fresh start - Feeling Good

After \
This command below will remove all of the items from the Git index (not from the working directory or local repository), and then will update the Git index, while respecting Git ignores. _PS. Index = Cache_

git rm -r --cached . && git add . && git commit -am "EJPREV: Remove ignored files."

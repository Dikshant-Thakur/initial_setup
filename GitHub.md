# How to use GitHub

## Check with remote (Github) repository.
1. First fetch the data, fetching ka mtlb clone nahi. Download hoti hai information agr humein check krna ho difference. 
``` bash
git fetch origin main
```
2. After fetching, fir hum compare kr skte hai *main* branch.
``` bash
git diff main origin/main
``` 
or
``` bash
git status
``` 

### How to make new branch and merge it. 
These are following steps: <br>
1. Switch to the main branch, pull the latest changes and create the new branch.
``` bash
git checkout main

# Latest changes pull karein
git pull origin main

# Nayi branch banayein aur uspar switch karein
# example - git checkout -b feature/pure-pursuit
git checkout -b feature/your-feature-nam
```
2. Stage the files and commit the message. 
``` bash
# Files check karein
git status

# Files add karein
git add .

# Professional commit message (Conventional Commits)
git commit -m "feat: implement navigation constraints for move_base"
```

3. Push the branch.
``` bash
git push -u origin feature/your-feature-name
```

4. On Github usually yellow banner dikhata hai, *Compare & pull request* uspr click kro. <br>
5. Pull Request (PR) Open karein. 
6. PR description mein batayein ki aapne kya change kiya hai.
7. Tag the other contributor or reviewer. 
8. Once all the review part has been done. GitHub UI par "Merge pull request" button click karein.
9. Merge ho jane ke baad, local repo ko wapas clean karein:
``` bash

# Main par wapas jayein
git checkout main

# Nayi changes fetch karein
git pull origin main

# Purani feature branch ko delete kar dein
git branch -d feature/your-feature-name

```
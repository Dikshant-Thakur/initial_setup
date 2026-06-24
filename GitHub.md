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

### How to check local repo name linked to global repo

``` bash
git remote -v
```

## Error and its solution

### 1. ! [rejected] main -> main (fetch first)
GitHub(aka remote) par kuch naye commits hain jo tumhare local repo mein nahi hain.<br>
Pehle same the - A. <br>
Fir remote mein changes karein - A → B → C → D <br>
 aur local mein changes kiya - A → E <br>
 To ye clash ho rha hai. Iska safe trika hai A → B → C → D → E krna uske liye <br>
 ``` bash 
 git pull origin main --rebase
 ```
Agar conflict aata hai to Git ruk jayega aur batayega kaunsi file mein issue hai. In the log window you can see the conflict file ab usko dekhne k liye. 
``` bash
git status
```

fir tmhe pta lg jaaega ki kaunci filoes mein fir vscode mein jaakr solve krna. <br>
esa dikhega - 
``` bash
<<<<<<< HEAD
remote wala code
=======
tumhara local code
>>>>>> 61a8e49
```
To matlab:

<<<<<<< HEAD se ======= tak = GitHub (remote) version <br>
======= se >>>>>>> tak = tumhara local version <br>

Current Change - Ye woh version hai jo abhi branch mein maujood hai. To Current Change = GitHub/remote version <br>
Incoming Change - Ye woh version hai jo Git apply karne ki koshish kar raha hai. To Incoming Change = tumhara local commit. <br>
Jab changes ho jaaye fir rebase continue kario
``` bash
git rebase --continue
```
and then to check ki sab sahi hai 
``` bash
git status
```
message sgould *nothing to commit, working tree clean* and then push onto the remote repository.

 ### 2. Submodules/Nested git problem


 ``` bash
#Step zero - check submodules, Current folder ke andar jitni .git directories hain, mujhe dikhao
find . -name ".git" -type d

#aur difference command- Kya parent repository ne officially kisi folder ko submodule declare kiya hai?
git submodule status

 # First remove the tracking from the orignal Gut index ki ye submodule hai
 git rm --cached <folder_name>

 # Then delete .git folder of that submodule
 rm -rf <folder_nameZ/.git

# then again add that submodue as a normal folder
git add <folder_name>

#commmit
git commit -m"commit_message"
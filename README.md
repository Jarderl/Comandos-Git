1. Create a new repository from scratch

  echo "# Git-Comandos" >> README.md   # create a README file
- git init                             # initialize a new Git repo
- git add README.md                    # stage the README
- git commit -m "first commit"         # commit it
- git branch -M main                   # rename default branch to 'main'
- git remote add origin https://github.com/
- git push -u origin main              # push to GitHub

---

2. Push an existing local repository


- git remote add origin https://github.com/------
- git branch -M main                   # ensure branch is named 'main'
- git push -u origin main              # push everything to GitHub

# Exercises

Work in Git Bash (Windows) or the Terminal (macOS). Run `pwd` whenever you are not sure where you are.
Start every level from the folder `shell-practice` (the one you cloned).

## Level 1 — Where am I? Paths

1. Run `pwd`. Write down the path: this is the absolute path of `shell-practice` on your computer.
2. Go into `playground/stations` and list its content with `ls`, then with `ls -a`.
   Which name appears only with `-a`? Why?
3. Read that hidden file with `cat`. What is the secret word?
4. Go into `playground/stations/europe`. From there, go to `playground/logs` with **one** `cd`
   and a **relative** path.
5. You are in `playground/logs`. Without moving, print the content of `playground/reports/2024/q1.txt`
   (one command, relative path).
6. Type `cd ~`, then `pwd`. Where are you? Then `cd -`: where are you now?
7. From anywhere, go back to `playground/notes` with one `cd` and an **absolute** path
   (use what you wrote in exercise 1, or start with `~`).

## Level 2 — Look inside files

8. How many lines does `playground/stations/europe/paris.csv` have? How many measurements
   (the first line holds the column names)?
9. Print the first 3 lines of `playground/stations/asia/tokyo.csv`.
10. Print the last line of `playground/logs/station.log`.
11. Open `playground/logs/station.log` with `less`, go to the next page, then leave.
    Which key leaves?

## Level 3 — Create, copy, move, delete (in `playground/tmp` only)

12. Go into `playground/tmp`. Create the folders `a/b/c` with **one** command.
13. Copy `playground/stations/europe/paris.csv` into `tmp`, under the name `paris_copy.csv`.
14. Rename `paris_copy.csv` into `paris_backup.csv`.
15. Delete the folder `a` and everything inside it. Check with `ls`.
16. Run `git status` from `shell-practice`. Why are your files in `tmp` not listed?
    (Hint: read `.gitignore` with `cat`.)

## Level 4 — Redirections and pipes (in `playground/tmp`)

17. Predict the content of `list.txt`, then check with `cat`:
    ```bash
    echo "one" > list.txt
    echo "two" > list.txt
    echo "three" >> list.txt
    ```
18. Save the list of the European station files into `tmp/europe.txt` with one command.
19. How many lines of `playground/logs/station.log` contain `ERROR`? One command, with a pipe.
20. How many of these `ERROR` lines are about `tokyo`? One command, with two pipes.
21. How many lines contain `WARN`? And `INFO`?

## Level 5 — Search

22. Which report mentions a heatwave? Search all the files of `playground/reports` with one command.
23. List all the `.csv` files under `playground/stations`. How many are there? (Count them with a pipe.)
24. Which file of `playground/notes` mentions Madrid?

## Level 6 — Read the history of this repository

25. How many commits does this repository have? Who wrote them?
26. One commit fixed a wrong temperature in Berlin. Who made it, and which value was replaced
    by which one? (`git log`, then `git show` with the identifier of that commit.)
27. Which files did the commit "Add the Asian stations" add?

## Level 7 — Git in your own folder

Leave `shell-practice` first: `cd ..`. Everything below happens in a new folder `git_gym`.

28. Create `git_gym`, go into it, turn it into a repository. Create a file `plan.txt` with one line
    `Monday: run`, stage it, commit it. Check with `git log --oneline`.
29. Add a second line `Tuesday: swim`, look at the change with `git diff`, commit.
30. Create a branch `feature/wednesday`, go to it, add `Wednesday: bike`, commit.
    Go back to `main` and merge the branch. Fast-forward or three-way merge? Why?
31. Provoke a conflict: on a new branch `feature/monday`, change line 1 into `Monday: walk`, commit.
    Back on `main`, change line 1 into `Monday: rest`, commit. Merge `feature/monday`.
    Read the markers, resolve (keep the version you want), finish the merge. Look at `git lg`
    (or `git log --oneline --graph --all`).
32. Replace the content of `plan.txt` by `oops` and save; undo it with one Git command.
33. Add a line `Thursday: gym` and commit it. You regret it: cancel this commit without erasing history.
    How many commits does `git log --oneline` show before and after?

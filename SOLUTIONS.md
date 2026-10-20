# Solutions

Try each exercise before reading its solution. Your paths and commit identifiers may differ.

## Level 1 — Where am I? Paths

1. `pwd` prints something like `/c/Users/alice/Documents/courses/git/shell-practice`
   (macOS: `/Users/alice/...`). It starts with `/`: an absolute path.
2. `cd playground/stations`, `ls` → `asia  europe`; `ls -a` → `.  ..  .calibration  asia  europe`.
   `.calibration` starts with a dot: names starting with a dot are hidden, only `-a` (all) shows them.
3. `cat .calibration` → the secret word is `KANGAROO`.
4. `cd ../../logs`: `..` goes up to `stations`, the second `..` up to `playground`, then into `logs`.
5. `cat ../reports/2024/q1.txt` (up to `playground`, then down into `reports/2024`).
6. `cd ~` goes to your home folder (`pwd` → `/c/Users/alice` or `/Users/alice`); `cd -` goes back
   to the previous folder, `playground/logs`.
7. `cd ~/Documents/courses/git/shell-practice/playground/notes` (adapt to the path of exercise 1).
   It works from any folder because it starts with `~`.

## Level 2 — Look inside files

8. `wc -l playground/stations/europe/paris.csv` → `11`: 1 line of column names + 10 measurements.
9. `head -n 3 playground/stations/asia/tokyo.csv`:
   ```
   date,temp_c,rain_mm
   2024-01-01,5.1,0.0
   2024-01-02,6.7,0.0
   ```
10. `tail -n 1 playground/logs/station.log` → `2024-03-01 18:00:00 INFO paris: reading ok`.
11. `less playground/logs/station.log`, Space for the next page, `q` to leave.

## Level 3 — Create, copy, move, delete

12. `cd playground/tmp`, then `mkdir -p a/b/c` (`-p` creates the whole chain).
13. `cp ../stations/europe/paris.csv paris_copy.csv`
14. `mv paris_copy.csv paris_backup.csv` (`mv` moves, and renames).
15. `rm -r a` (`-r`: the folder and everything inside). `ls` → `paris_backup.csv`.
16. `.gitignore` contains `playground/tmp/*` (ignore everything in `tmp`) and `!playground/tmp/.gitkeep`
    (except `.gitkeep`, which keeps the empty folder in Git). Ignored files never appear in `git status`.

## Level 4 — Redirections and pipes

17. `two` then `three`: `>` replaces the content (so `one` is erased), `>>` adds at the end.
18. `ls ../stations/europe > europe.txt` (from `tmp`); `cat europe.txt` → `berlin.csv`, `london.csv`, `paris.csv`.
19. `grep ERROR ../logs/station.log | wc -l` → `7`.
20. `grep ERROR ../logs/station.log | grep tokyo | wc -l` → `3`.
21. `grep WARN ../logs/station.log | wc -l` → `5`; `grep INFO ../logs/station.log | wc -l` → `48`
    (7 + 5 + 48 = 60 lines: check with `wc -l`).

## Level 5 — Search

22. `grep -r heatwave playground/reports` → `playground/reports/2024/q2.txt` (Delhi, May 2024).
23. `find playground/stations -name "*.csv"` lists 5 files;
    `find playground/stations -name "*.csv" | wc -l` → `5`.
24. `grep -r Madrid playground/notes` → `playground/notes/todo.md`.

## Level 6 — Read the history of this repository

25. `git log --oneline` → 5 commits. `git log` shows the authors: Course Staff, Alice Martin, Bob Nguyen.
26. `git log` shows that Bob Nguyen wrote "Fix a wrong temperature in Berlin".
    `git show <its identifier>` shows in `berlin.csv`:
    ```
    -2024-01-04,99.0,0.0
    +2024-01-04,2.9,0.0
    ```
    The wrong value 99.0 was replaced by 2.9 (the station log reported "value out of range (99.0)").
27. `git show --stat <identifier of "Add the Asian stations">` (or `git log --stat`):
    `playground/stations/asia/delhi.csv` and `playground/stations/asia/tokyo.csv`.

## Level 7 — Git in your own folder

28. ```bash
    cd ..
    mkdir git_gym
    cd git_gym
    git init
    echo "Monday: run" > plan.txt      # or create the file in VS Code
    git add plan.txt
    git commit -m "Add Monday"
    git log --oneline                  # 1 commit
    ```
29. ```bash
    echo "Tuesday: swim" >> plan.txt   # >> adds at the end
    git diff                           # +Tuesday: swim
    git add plan.txt
    git commit -m "Add Tuesday"
    ```
30. ```bash
    git switch -c feature/wednesday
    echo "Wednesday: bike" >> plan.txt
    git add plan.txt
    git commit -m "Add Wednesday"
    git switch main
    git merge feature/wednesday        # Fast-forward
    ```
    A fast-forward: `main` did not move since the branch was created, so Git only moves the label.
31. ```bash
    git switch -c feature/monday
    # line 1 -> "Monday: walk", save
    git add plan.txt
    git commit -m "Walk on Monday"
    git switch main
    # line 1 -> "Monday: rest", save
    git add plan.txt
    git commit -m "Rest on Monday"
    git merge feature/monday           # CONFLICT (content): Merge conflict in plan.txt
    ```
    The file contains:
    ```
    <<<<<<< HEAD
    Monday: rest
    =======
    Monday: walk
    >>>>>>> feature/monday
    Tuesday: swim
    Wednesday: bike
    ```
    Keep one line (or write a mix), delete the three marker lines, save, then
    `git add plan.txt` and `git commit` (the message `Merge branch 'feature/monday'` is ready).
    `git log --oneline --graph --all` shows the two lines joining in the merge commit.
32. `git restore plan.txt`: the file goes back to the version of the last commit.
33. ```bash
    echo "Thursday: gym" >> plan.txt
    git add plan.txt
    git commit -m "Add Thursday"       # 7 commits
    git revert HEAD                    # a new commit that removes the line: 8 commits
    ```
    `git revert` does not erase the commit "Add Thursday": it adds a commit that does the opposite.

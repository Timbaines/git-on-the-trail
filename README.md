# Git On The Trail Workshop

Git Basics Crash Course: Learn the fundamentals of Git through the lens of planning and executing a hike on the Highline Trail in Glacier National Park. Just as a successful hike requires preparation, checkpoints, and safe navigation with your group, Git helps us track work, explore safely, and collaborate smoothly.

## Prerequisites
- Have Git installed and verify it works. [Git official website](https://git-scm.com/)
    - Check your version: `git --version`
- Configure identity:
    - `git config --global user.name "Your Name"`
    - `git config --global user.email "your.email@example.com"`
- Optional defaults:
    - `git config --global init.defaultBranch main`
- Have a GitHub account if you plan to push to a remote repository.

## Section 1: Base Camp Setup
*Preparing for our hike*

### 1) Setting Up Your Git Identity

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 2) Establish Your Base Camp
Before beginning any hike, you need to establish a base camp where you'll organize your gear and plan your route.

```bash
mkdir 2025-09-git-on-the-trail
cd 2025-09-git-on-the-trail
git init
```

### — What just happened?
- We created a folder called 'highline-adventure' that's considered our base camp. We entered it and initialized a Git repository with `git init` to start tracking our hiking progress.
- `git init` created a hidden `.git` folder that records your trail history. You typically won’t interact with it directly.

### 3) Gear Checklist Preparation
Every hike starts with a gear list. Let's create a gear checklist for your hike in the 'highline-adventure' folder.

```bash
echo "Weather: Clear, 63°F, light breeze, Time Started: 8:00am, Condition: Well-maintained trail paths" > trail-conditions.txt
echo "Water bottles, hiking boots, Map, Compass, Bear spray, Camera" > gear-checklist.txt
```

### — What just happened?
- We instructed to write a "string" to the files and the ">" greater than symbol is a redirection operator that sends the output of the `echo` command to the two new files.

### 4) Review Your Gear Checklist Before Committing To Hiking
Before we add items to our backpack, we want to see what's available to pack and what will be packed.

- Option A: add specific gear
```bash
git status
git add trail-conditions.txt
```

- Option B: add all your gear

```bash
git add .
git status
```

- Before we close up our backpack, compare what is being brought versus what we planned using `git diff --staged`.

```bash
git diff --staged
```

### 5) Close Up Your Backpack And Begin Hiking
When you're ready to begin your hike, make a trail checkpoint with a detailed message using `git commit -m "message"`.

```bash
git commit -m "First Commit: Establish base camp; pack initial gear; ready to hike."
```

### 6) Connecting To The Park Headquarters (Remote Repository)
Just as hikers register with park headquarters and share their planned route, connect your local repository to a remote on GitHub so others can follow your progress.

1. On GitHub, create a new repository called 'highline-adventure.'
2. Do not initialize it with a README.md file.
3. Copy the commands under “…or push an existing repository from the command line” and paste them in your terminal.

```bash
git remote add origin https://github.com/your-username/highline-adventure.git
git branch -M main
git push -u origin main
```

### — What just happened?
- `git remote add origin` connects your base camp to park HQ (GitHub).
- `git branch -M main` ensures your default branch is named "main."
- `git push -u origin main` uploads your first checkpoint and sets upstream tracking so future `git push`/`git pull` don’t need extra arguments.

### Pro-Tip: Global Ignore Configuration To Avoid Obstacles
- macOS-created .DS_Store files can show up as untracked changes and get committed by mistake.

#### macOS (ignore Finder files globally)

```bash
touch ~/.gitignore_global
echo ".DS_Store" >> ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global
```
This prevents those files from appearing as untracked across all repos.

## Section 2: Navigating The Trail And Reviewing Progress History
*Tracking your progress and navigating obstacles*

### 7) Reviewing Your Trail Log
Like reading prior trail entries, you can look back at your progress using `git log`.

```bash
git log
```

For a quick scan:

```bash
git log --oneline
```

### 8) Making Trail Updates
As we make progress on our hike, let’s update the trail log and gear list.

```bash
echo "Update: Reached Haystack Pass — Weather: Clear, 58°F, Windy; Arrival: 10:26am; Conditions: Clear skies" >> trail-conditions.txt
echo "Added: First aid kit, extra socks" >> gear-checklist.txt
```

### 9) See What's Changed Since Last Camp
Compare current trail conditions to the last checkpoint using `git diff`.

```bash
git diff
```

### 10) Sharing Trail Updates With Other Hikers
Before making major decisions, check if other hikers have posted updates from HQ. Remember: `git pull` is equivalent to `git fetch` and a merge by default.

```bash
git pull
```

### — Best practices for syncing trail updates
- Pull the latest updates before starting work and before you push.
- Use descriptive, focused commit messages in your trail log.
- Push trail updates regularly so the group stays synchronized.

### 11) Abandon A Wrong Turn
If you made local, uncommitted edits to a file that you want to discard, backtrack to the last saved version with `git restore <file>` (affects your working copy, not history).

```bash
git restore trail-conditions.txt
git status
```

### — What just happened?
- You discarded your uncommitted changes in `trail-conditions.txt`, returning it to the last staged/committed state.
- Note: If the change was already committed, use `git revert <commit>` to undo safely by making a new commit (or advanced: `git reset`).

### 12) Removing An Item Added to our Backpack by Mistake
If you staged an item you don’t want to include in the next checkpoint, unstage it while keeping your edits with `git restore --staged <file>`.

```bash
git add gear-checklist.txt
git restore --staged gear-checklist.txt
```

### 13) Reaching Your Next Checkpoint
After making good progress, stage and commit with a concise message.

```bash
git add .
git commit -m "Second Commit: Removed Haystack Pass trail notes; add items to backpack."
```

### 14) Syncing With Trail HQ
Sync your latest progress to park HQ so others can benefit. If you set the upstream in step 6, a plain push works; otherwise, use `-u` the first time on a new branch.

```bash
git push
```

### — Checking Trail Updates Before Syncing
Before or after you push, it’s good practice to check if others updated the trail log:

For Example, let's copy the README.md file provided and head over to GitHub. Click on the "Add README" button and paste the contents
into the text box. Then, click "Commit changes."

```bash
git pull
```

Note: In more advanced scenarios, multiple hikers might update the same files, which can lead to merge conflicts that require resolution. In this workshop, we will focus on staying in sync while keeping history simple. For further learning, research the commands `git fetch`, `git pull --ff-only`, and `git rebase`.

## Section 3: Exploring Alternative Trails
*Branching paths and route management*

### 15) Scout Available Trails
Before exploring alternative routes, list the trails you have locally.

```bash
git branch
```

### 16) Taking An Established Side Trail
Switch to an existing branch (trail) or create one to explore a known path.

```bash
git branch scenic-route  # Mark this trail junction
git switch scenic-route  # Take the scenic route
```

### 17) Making A New Trail and Branching Off
When you discover uncharted territory, create and switch to a new branch immediately.

```bash
git switch -c wildlife-photography-detour
```

### 18) Documenting Your Detour
Record what you found on the detour and checkpoint it.

```bash
echo "Spotted a group of mountain goats. Crown of the Continent views were excellent. Took Photos." > photo-opportunities.txt
git add .
git commit -m "Third Commit: Log wildlife photo opportunities and scenic viewpoints."
```

### 19) Switching Between Known Trails
Move between established trails to continue exploration.

```bash
git switch main
git switch scenic-route
git switch wildlife-photography-detour
```

### 20) Sharing Your New Trail Discovery
When you’re ready to share a new trail with HQ and other hikers, push it. Use `-u` the first time so future pushes are simpler.

```bash
git push -u origin wildlife-photography-detour
# Since this is the first push to a new local branch, we are adding the "-u origin <branch>" argument.
```

### 21) Merging Trail Log Reports
Combine your discoveries with the main trail log.

```bash
git switch main
git merge wildlife-photography-detour
git push origin main
```

## 🎉 Congratulations!
You’ve reached the end of the Git On The Trail Workshop! Whether this was a refresher or you learned something new, I hope I’ve helped you feel more equipped to prepare, navigate, and collaborate with confidence.

### Trail Summary: Essential Commands You've learned in this workshop

- `git config` — Set up your hiker identity
- `git init` — Establish your base camp (initialize repository)
- `git status` — Check the status of your gear
- `git add <file>` — Pack specific items
- `git add .` — Pack everything at once (use with intention)
- `git diff --staged` — Compare what’s packed against your plan
- `git commit -m "message"` — Create a checkpoint with a descriptive message
- `git remote add origin <url>` — Connect base camp to trail HQ
- `git branch -M main` — Ensure your main trail is named "main"
- `git push -u origin main` — First upload to HQ and set tracking
- `git pull` - Pull trail updates from Park Headquarters
- `git pull --ff-only` — Get latest trail updates safely (fast-forward only)
- `git log` — Review detailed trail history
- `git log --oneline` — Quick summary of the trail history
- `git diff` — Compare your working copy to the last checkpoint
- `git restore <file>` — Discard local, uncommitted changes to a file
- `git restore --staged <file>` — Unstage while keeping edits
- `git branch` — Scout available trails
- `git branch <branch-name>` — Mark a new trail junction
- `git switch` — Switch between known trails
- `git switch -c <branch-name>` — Create a new trail and take it
- `git push -u origin <branch-name>` — First push of a new trail to HQ
- `git merge <branch-name>` — Merge trail discoveries

### Key Takeaways
- 🏔️ Git is like hiking: it's about preparation, tracking progress, and working with others safely
- 🎒 Commits are checkpoints: make them frequent and with clear descriptions of your progress
- 🗺️ Branches are alternative routes: use them to explore without affecting your main trail
- 👥 Collaboration requires communication: clear commit messages and regular syncing prevent team conflicts
- 🔄 Version control is powerful: you can always backtrack, explore alternatives, and combine discoveries

### Hiking Beyond The Basics: Group Collaboration Commands

Once you are comfortable with the basics, explore more advanced Git commands to coordinate complex expeditions:

#### Advanced Group Coordination:

- `git clone <url>` — Join an existing trail log
- `git fetch` — Check trail updates without changing your files
- `git rebase` — Replay your discoveries atop the latest trail log (advanced)
- `git stash` — Temporarily store gear while switching trails

#### Conflict Resolution:
- `git merge --abort` — Cancel a problematic merge
- `git reset --hard HEAD` — Return to last known safe position (destructive)
- `git revert <commit>` — Undo a commit safely by creating a new commit
- `git cherry-pick <commit>` — Apply specific discoveries from the trails

#### Repository Inspection:
- `git remote -v` — View all connected trail headquarters
- `git branch -r` — See all remote trails
- `git show <commit>` — Examine specific trail log entries in detail

## Resources

- [Git official website](https://git-scm.com/)
- [Pro Git Book Download](https://git-scm.com/book/en/v2)

**If you ever decide to visit Montana and hike in Glacier National Park, here’s a great organization with knowledgeable guides who share the park’s history throughout the hiking tour.:**
- [Glacier Institute](https://glacierinstitute.org/)


## Ideas To Branch Off This Workshop

### Beginner Projects
- Personal Coding Journal: Track your learning progress with daily commits
- Recipe Collection: Version control your favorite recipes with branches for variations
- Project Documentation: Maintain a README for your projects with a proper Git workflow

### Intermediate Challenges
- Collaborative Website: Work with friends to build a simple website using branches
- Open Source Contribution: Find a beginner-friendly project and contribute
- Backup Strategy: Use Git as part of your file backup and versioning system

### Advanced Expeditions
- Git Workflow Mastery: Learn GitFlow, GitHub Flow, or other branching strategies
- Automation Integration: Combine Git with CI/CD pipelines
- Large Team Coordination: Explore advanced conflict resolution and repository management

# sml_2026
Public course repository for the class Stochastic Modeling and Financial Mathematics, Constructor University Bremen, Fall 2026

See the [course website](https://math.constructor.university/petrat/teaching/2026_fall_stochastic_modeling/) for more information.

Helpful links:
* For an introduction to Scientific Python, you can refer to this [Introduction](https://mids.ku.de/oliver/teaching/scipy-intro/scipy-intro.pdf), written by Marcel Oliver ([html link](https://mids.ku.de/oliver/teaching/scipy-intro/scipy-intro/index.html)). (It is a bit old, but still very good.)
* [Understanding git conceptually](http://www.sbf5.com/~cduan/technical/git/), an excellent general introduction to git by Charles Duan.
* For an introduction to using and properly setting up git (written for an older version of this class), see [Introduction to git for academics](https://bitbucket.org/marcel_oliver/git_for_academics/)

---

Below, you find detailed instructions for using git and github for this course:
- [Installing and Configuring Git](#installing-and-configuring-git)
- [Setup Git for the Course](#setup-git-for-the-course)
- [Normal Workflow](#normal-workflow)
- [Quick Reference](#quick-reference)
- [Troubleshooting](#troubleshooting)

---

# Installing and Configuring Git

Before starting the course, you need to install Git and configure it with your name and email address.

## 1. Create a GitHub account

If you do not already have one, create an account at GitHub:

[GitHub](https://github.com/)

You will need a GitHub account to access your private course repository.

## 2. Install Git

Download and install Git for your operating system:

[Download Git](https://git-scm.com/downloads)

After installation, open a **Terminal** (macOS/Linux) or **Git Bash** (Windows) and check that Git is available:

```bash
git --version
```

You should see something similar to:

```text
git version 2.x.x
```

## 3. Configure your name and email

Configure the name that should appear on your commits:

```bash
git config --global user.name "Your Name"
```

Configure the email address associated with your GitHub account:

```bash
git config --global user.email "your.email@example.com"
```

The name and email are stored with your commits. GitHub uses the email address to associate commits with your GitHub account, so make sure you use an email address that is added to your GitHub account.

Check your configuration:

```bash
git config --global user.name
git config --global user.email
```

## 4. Authenticate with GitHub

When you first clone or push to a GitHub repository, GitHub needs to authenticate you. GitHub supports both **HTTPS and SSH** for Git operations.

When Git asks you to authenticate, follow the GitHub/browser authentication instructions. GitHub no longer accepts your normal account password for Git operations over HTTPS. SSH setup is the most convenient.

If you have trouble authenticating, the [GitHub authentication documentation](https://docs.github.com/en/authentication) provides further instructions.

## 5. Test your setup

You can check your Git configuration with:

```bash
git config --global --list
```

You are now ready to set up your course repository. Continue with [Setup Git for the Course](#setup-git-for-the-course).


---


# Setup Git for the Course

Each student will use two GitHub repositories:

* **Course repository (`upstream`)** — the public repository containing course material and homework.
* **Your repository (`origin`)** — your private repository containing your work and submissions.

Your private repository must remain **private** and should give the instructor and TA **write access**.

The setup is:

```text
Public course repository
          │
       upstream
          │
          ▼
    Your local clone
          │
        origin
          ▼
Your private GitHub repository
```

## 1. Create your private repository

Create a **new private repository** on GitHub. Do not initialize it with a README, `.gitignore`, or license.

## 2. Clone the course repository

For ssh authentication:
```bash
git clone git@github.com:spetrat/sml_2026.git
cd sml_2026
```
For https authentication:
```bash
git clone https://github.com/spetrat/sml_2026.git
cd sml_2026
```

The repository you cloned is initially called `origin`. Rename it to `upstream`:

```bash
git remote rename origin upstream
```

## 3. Add your private repository as `origin`

For ssh authentication:
```bash
git remote add origin git@github.com:YOUR-USERNAME/YOUR-PRIVATE-REPOSITORY.git```

For https authentication:
```bash
git remote add origin https://github.com/YOUR-USERNAME/YOUR-PRIVATE-REPOSITORY.git
```

Check that everything is correct:

```bash
git remote -v
```

You should see:

```text
origin    https://github.com/YOUR-USERNAME/YOUR-PRIVATE-REPOSITORY.git
upstream  https://github.com/spetrat/sml_2026.git
```

Finally, push the course repository to your private repository:

```bash
git push -u origin main
```

## 4. Give the instructor and TA access

On GitHub, add the instructor (spetrat) and TA (subediarnav) as collaborators on your **private repository**, with **write access**.

---

# Normal Workflow

### Get updates from the course

Before starting new work, update your local repository from the public course repository:

```bash
git pull upstream main
```

Then update your private repository:

```bash
git push origin main
```

### Do your work

Please put the homework solution into the respective homework folder. Add/edit your files and commit your changes:

```bash
git add .
git commit -m "Complete homework 01"
```

You can make as many commits as you like while working.

### Submit your homework

Push your work to your private repository:

```bash
git push origin main
```

The contents of your private repository at the submission deadline are your submission.

### Get grades and feedback

The TA/instructor may add grades or feedback to your repository. To retrieve their changes:

```bash
git pull origin main
```

---

# Quick Reference

| Task                | Command                                 |
| ------------------- | --------------------------------------- |
| Get course updates  | `git pull upstream main`                |
| Save your work      | `git add .` + `git commit -m "message"` |
| Submit homework     | `git push origin main`                  |
| Get grades/feedback | `git pull origin main`                  |

The most important thing to remember is:

```text
upstream = public course repository
origin   = your private repository
```

**Pull from `upstream`; push your work to `origin`.**

---

# Troubleshooting

If something goes wrong, **`git status` is usually the best place to start**:

```bash
git status
```

It tells you which branch you are on and whether you have uncommitted changes.

### Check your remotes

Make sure `origin` and `upstream` point to the right repositories:

```bash
git remote -v
```

You should have:

```text
origin    → your private repository
upstream  → public course repository
```

### Check what has changed

To see which files have been modified:

```bash
git status
```

To see the actual changes:

```bash
git diff
```

### "I have changes that I haven't committed"

If you want to keep your changes, commit them:

```bash
git add .
git commit -m "Describe your changes"
```

Then push them:

```bash
git push origin main
```

### "Git won't let me pull from upstream"

You may have local changes that conflict with updates from the course repository. First check:

```bash
git status
```

If you have uncommitted work, commit it before pulling:

```bash
git add .
git commit -m "Save my current work"
git pull upstream main
```

If you encounter a **merge conflict**, don't panic. Git will tell you which files are affected. Ask the instructor or TA for help if you are unsure how to resolve it.

### "I don't know what branch I'm on"

Run:

```bash
git branch
```

The current branch is marked with `*`. Normally, you should be working on `main`.

### "Did my homework actually get pushed?"

Check:

```bash
git status
```

and then:

```bash
git push origin main
```

If Git says:

```text
Everything up-to-date
```

your local commits have already been pushed to `origin`.

### Useful commands at a glance

```bash
git status       # What is going on?
git remote -v   # Where are origin and upstream?
git branch       # What branch am I on?
git diff         # What have I changed?
git log --oneline # What have I committed?
```

**When in doubt, don't delete or reset anything. Run `git status` and ask the instructor or TA for help.**

---
title: "The Tale of Two Gits"
date: "2025-02-20"
summary: "Ever juggled with having to manage two different git accounts?"
# description: ""
toc: true
readTime: true
autonumber: true
math: true
tags: ["git", "two git", "identity management"]
showTags: false
hideBackToTop: false
---

# The Tale of Two Git Accounts: A Developer's Identity Crisis

Picture this: It's 2 AM, and I'm sitting in my dimly lit room, staring at my laptop screen in horror. I just pushed my personal project's code - complete with comments about how my day job's codebase is a "prehistoric spaghetti monster" - to my work repository. Talk about a Monday morning conversation I'm not looking forward to!

If you've ever juggled personal and work Git accounts on the same machine, you've probably experienced that moment of panic when you realize you just committed with the wrong identity. It's like accidentally sending a text meant for your best friend to your boss - but with more semicolons and merge conflicts.

But fear not, fellow code jugglers! Let me show you how to maintain your split coding personality without losing your sanity.

## The Problem: A Tale of Mixed Identities

We developers live double lives: the professional ones where we write clean, well-documented code (right?), and the personal ones where we name variables like `thisThingHere` and `iHopeThisWorks`. Having both accounts on the same laptop is like having Batman and Bruce Wayne share the same closet - things can get messy.

## The Solution: Your Personal Git Identity Management System

### Step 1: Creating Your Secret Identities (SSH Keys)

First, let's create separate SSH keys for your work and personal lives:

```bash
# For your personal coding adventures
ssh-keygen -t ed25519 -C "your.personal@email.com" -f ~/.ssh/personal_key

# For your professional persona
ssh-keygen -t ed25519 -C "your.work@email.com" -f ~/.ssh/work_key
```

### Step 2: Awakening the Keymaster (SSH Agent)

Time to summon the SSH agent (think of it as your personal butler for keys):

```bash
# Wake up, Alfred!
eval "$(ssh-agent -s)"

# Hand over the keys
ssh-add ~/.ssh/personal_key
ssh-add ~/.ssh/work_key
```

### Step 3: Setting Up Your Secret Base (~/.ssh/config)

Create your SSH config file that would make Bruce Wayne proud:

```
# Your after-hours coding identity
Host github.com-personal
   HostName github.com
   User git
   IdentityFile ~/.ssh/personal_key

# Your professional superhero identity
Host github.com-work
   HostName github.com
   User git
   IdentityFile ~/.ssh/work_key
```

### Step 4: The Costume Change (Git Configurations)

Now, let's set up your different personas:

For your work repositories:
```bash
git config user.name "Professional Dev"
git config user.email "serious.coder@work.com"
```

For your personal projects:
```bash
git config user.name "Code Ninja"
git config user.email "awesome.dev@personal.com"
```

### Step 5: Automatic Identity Switching

Want Git to automatically switch identities based on which directory you're in? Create these config files:

~/.gitconfig:
```ini
[includeIf "gitdir:~/work/"]
    path = ~/.gitconfig-work
[includeIf "gitdir:~/personal/"]
    path = ~/.gitconfig-personal
```

~/.gitconfig-work:
```ini
[user]
    name = Professional Dev
    email = serious.coder@work.com
[url "git@github.com-work:"]
    insteadOf = https://github.com/
```

~/.gitconfig-personal:
```ini
[user]
    name = Code Ninja
    email = awesome.dev@personal.com
[url "git@github.com-personal:"]
    insteadOf = https://github.com/
```

### Step 6: Using Your New Powers

When cloning repositories, use your new identities:

For personal projects:
```bash
git clone git@github.com-personal:username/repo.git
```

For work projects:
```bash
git clone git@github.com-work:username/repo.git
```

## The Happy Ending

Now you can freely switch between your work and personal coding personas without fear of accidentally revealing your secret identity. No more 2 AM panic attacks, no more hastily deleted repositories, and no more explaining to your boss why your commit message says "Finally fixed this stupid bug! 🎉🍺".

Remember, with great Git powers comes great responsibility. Use these powers wisely, and may your commits always land in the right repository!

P.S. If you still manage to commit to the wrong repository, well... we've all been there. At least now you can blame it on your evil twin! 😉

Shoutout to Adwaith, btw.

---
*This blog post was written by a developer who has definitely never accidentally pushed personal code to a work repository. Trust me.*

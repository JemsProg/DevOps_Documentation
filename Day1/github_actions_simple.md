# GitHub Actions (Explained Simply)

## 1. What it is
GitHub Actions is like a **robot assistant inside GitHub**.  
Every time you push code or open a pull request, this robot can do jobs for you — like checking your code, installing things, running tests, or even building the app.  

You tell the robot what to do by writing a **workflow file** (a `.yml` file in `.github/workflows/`).  

---

## 2. Why it’s important
- **Catches mistakes early** – if your code breaks, the robot tells you before merging.  
- **Saves time** – you don’t need to test everything on your own computer every time.  
- **Keeps things fair** – the same rules run for every developer’s code.  
- **Helps deploy automatically** – later, this robot can even publish your app online.  

So in groupwork terms: GitHub Actions is like a classmate who double-checks everyone’s paper before it goes into the final draft.

---

## 3. How to use it
1. Make a folder: `.github/workflows/`  
2. Create a file like `ci.yml`  
3. Add this simple workflow:

```yaml
name: Say Hello

on:
  push:
    branches: [ main, develop ]
  pull_request:

jobs:
  hello:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Say hello
        run: echo "Hello from GitHub Actions 👋"
```

👉 Every time you push, it prints a message. That’s the robot saying hi.  

---

### Example with real projects

#### For Next.js (Node)
The robot will:
1. Install Node.
2. Install dependencies (`npm ci`).
3. Run tests (`npm test`).
4. Build the app (`npm run build`).

#### For Python
The robot will:
1. Install Python.
2. Install dependencies (`pip install -r requirements.txt`).
3. Run tests with `pytest`.

---

## Quick mental model
- **GitFlow** = when to push and where (which branch).  
- **GitHub Actions** = what happens automatically when you push (checks, builds, tests).  

---

## Quick Check
If your Python project has a `requirements.txt`, which command should you put in the GitHub Actions workflow to install your dependencies?

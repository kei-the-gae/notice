## ✅ Group Git Workflow (Collaborators Use `upstream`, Rebase _Optional_)

### 👤 **1. Repo Owner Setup**

- One person (e.g. **Alice**) creates a GitHub repo.
- Adds the others (**Bob and Carol**) as **collaborators**.
- Alice manages the central `main` branch via the `origin` remote.

---

### 👥 **2. Collaborators Clone and Configure Remotes**

1. Clone your personal fork (or the central repo):

   ```bash
   git clone https://github.com/your-username/repo-name.git
   cd repo-name
   ```

2. Add the shared repository (Alice's) as `upstream`:

   ```bash
   git remote add upstream https://github.com/alice/repo-name.git
   ```

3. Check remotes:

   ```bash
   git remote -v
   ```

> **Note:** the owner of the repository will not have an `upstream` remote, as they are the source of truth. They will only have `origin` pointing to their own repository.

---

### 🌿 **3. Start a New Feature Branch**

Always create feature branches from the latest upstream `main`:

```bash
git fetch upstream
git checkout -b feature-bob upstream/main
```

Work on your feature as usual:

```bash
git add .
git commit -m "Add new feature"
```

---

### 🔄 **4. Sync with `upstream/main` (Merge or Rebase — Your Choice)**

#### Option A — **Merge** (preserves full history with merge commits):

```bash
git fetch upstream
git merge upstream/main
```

#### Option B — **Rebase** (cleaner, linear history):

```bash
git fetch upstream
git rebase upstream/main
```

> **Tip**: Choose rebase if you want a tidy commit history. Choose merge if you want to preserve the exact sequence of events.

> **Note:** If you or someone in your team haven't finished the Learn Git 2 course or know what rebase is from elsewhere, you should probably choose to merge for ease of use.

> **Reminder:** the repository owner will not have an upstream, so they will be fetching from `origin` and merge/rebasing their local repository from `origin/main`

---

### 🚀 **5. Push to `origin`, Open a Pull Request**

Push your branch to your own `origin`:

```bash
git push origin feature-bob
```

Then open a **Pull Request** to **`upstream/main`** on GitHub.

---

### ⚔️ **6. Handle Merge Conflicts**

If you run into conflicts:

- Fix conflicts in your editor.
- Then:
  - If you used **merge**:

    ```bash
    git add .
    git commit
    ```

  - If you used **rebase**:

    ```bash
    git add .
    git rebase --continue
    ```

---

### 🤝 **7. Collaborate Smoothly**

- Use **clear branch names** (`feature-name`, `fix-bug`, etc.).
- Communicate often (Slack, GitHub Issues, etc.).
- Only merge to `main` after **pull request review**.
- The repo owner (e.g., Alice) manages merges to `main`.

---

### ✅ Example Summary

| Step         | Alice            | Bob & Carol                                   |
| ------------ | ---------------- | --------------------------------------------- |
| Create Repo  | ✅               |                                               |
| Add Remotes  | N/A              | Add `upstream` to Alice’s repo                |
| Start Work   | From `main`      | From `upstream/main`                          |
| Sync Updates | Push to `origin` | Pull from `upstream`, use merge **or** rebase |
| Share Work   | Push to `origin` | Push to `origin`, open PR to `upstream/main`  |
| Merge PRs    | ✅               | Request review                                |

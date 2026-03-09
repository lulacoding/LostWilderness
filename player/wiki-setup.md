# Setting up Plugin/docs as a GitHub Wiki

This folder is already structured for a GitHub-style wiki. To publish it as your repo’s wiki:

## 1. Create / use a GitHub repo and enable the Wiki

- Create a repository for your project on GitHub (if you don’t have one).
- In the repo: **Settings → General → Features** → enable **Wiki**.
- (Optional) Under **Settings → General → Wikis**, uncheck “Allow editing only from the default branch” if you want to edit the wiki by pushing from your machine.

## 2. Clone the wiki repository

GitHub creates a separate git repo for the wiki. Clone it (replace `OWNER` and `REPO` with your GitHub username and repo name):

```bash
git clone https://github.com/OWNER/REPO.wiki.git
cd REPO.wiki
```

## 3. Copy the docs into the wiki repo

From your **project root** (parent of `Plugin`):

**Windows (PowerShell):**
```powershell
Copy-Item -Path "Plugin\docs\*" -Destination ".\REPO.wiki\" -Recurse -Force
```

**Windows (cmd) / cross-platform:**
```bash
xcopy /E /Y "Plugin\docs\*" "REPO.wiki\"
```

**Linux / macOS / Git Bash:**
```bash
cp -r Plugin/docs/* REPO.wiki/
```

Or copy the contents of `Plugin/docs` into `REPO.wiki` manually (all `.md` files, including `sidebar.md` and `footer.md`).

## 4. Set the wiki Home page

- In the wiki repo, the **Home** page is the one named **Home** (from `home.md`). GitHub uses the filename (without `.md`) as the page title.
- After your first push, on GitHub open the wiki → **Pages** and set **Home** as the home page if it isn’t already.

## 5. Commit and push

```bash
cd REPO.wiki
git add .
git commit -m "Import wiki from Plugin/docs"
git push origin main
```

(If your wiki was created earlier, the default branch might be `master`; use that if `main` doesn’t exist.)

## 6. View the wiki

Open: **https://github.com/OWNER/REPO/wiki**

---

## Notes

- **Internal links** in these docs use lowercase filenames with `.md` (e.g. `[Home](home.md)`, `[Calendar and Time](calendar-and-time.md)`). See [Style guide](../style-guide.md) for the file-naming convention.
- **Sidebar / footer:** If your wiki expects special names for sidebar/footer, rename or copy `sidebar.md` and `footer.md` to match (e.g. some wikis use `_Sidebar` and `_Footer`).
- **Syncing later:** To update the wiki from `Plugin/docs`, run the same copy step into your local `REPO.wiki` clone, then commit and push.

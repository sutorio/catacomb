#sysadim


For this to be effective I need a specific setup:

1. Obsidian app on personal computer on Windows itself.
2. Obsidian app on Android.
3. Neovim on Linux on personal computer.

Then I want a tool for [[managing references]]: this is currently Zotero, which is available on Windows/Linux/etc. It is *not* available on Android atm, so need something done about that. Obsidian supports Zotero via a plugin.

The Obsidian vault is in the Dropbox folder so is automatically synced between machines.

Android does not *directly* allow this, so the [DropSync]() application is also required. This creates an actual folder on the device that can sync everything in it with Dropbox. The free version only allows for syncing of a single folder, but as the only thing I'm interested in is the Obsidian vault, that's not an issue.

Then I need to involve git. I only ideally want to push from a single machine: I'm not really using git in this case as intended.

Firstly, I tell Dropbox to ignore the `.git/` folder and the `.gitignore` using the Dropbox CLI tool. I `cd` into the `Dropbox/` folder, then: 

```
dropbox.py exclude add .git .gitignore
```

> [!note] This doesn't seem to actually work as intended because I just got a message on my phone that these had finished syncing, but anyway.

In the `.gitignore`, I'm ignoring anything I don't want to be public: `TASKS.md` for example.

Then I can `git add` and `git commit` and `git push` yadda yadda yadda.

---

- [ ] check for sync issues asap (@2023-11-14)
- [ ] set up automatic pushing to github asap. Need it post-Dropbox-sync. Is this possible? (@2023-11-14)

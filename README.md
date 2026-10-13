# Diskling rules

The public list of what [Diskling](https://diskling.com) knows about the files and folders on a Mac: what each one is, which app or tool owns it, whether it is safe to remove, and the right way to remove it.

Diskling is a Mac app that explains why your disk is full and gets the space back safely. These rules are how it decides. They are public so anyone can check them, question them, and suggest new ones.

**Status:** early. The rule format below is a draft, and the first rules land before the Diskling beta.

## Why the rules are public

- **You can see why Diskling suggests something** before you trust it with your files.
- **Mistakes get caught faster.** A wrong rule is a bug anyone can report.
- **Apps change where they store data.** Many eyes keep the rules current.

## Safety labels

Every rule has one of three labels. Diskling never pre-selects anything labeled "Review first".

| Label | Meaning | Example |
|---|---|---|
| Safe | Caches and temporary files that rebuild on their own | Browser caches, `npm` cache |
| Rebuilds on next use | Downloads or builds that come back when needed, sometimes after a wait | Xcode DerivedData, Playwright browsers |
| Review first | Your data, backups, or anything that cannot come back on its own | iOS device backups, Mail downloads |

## Removal methods

| Method | What happens |
|---|---|
| `trash` | Moved to the Trash. Can be restored. |
| `command` | Removed with the owning tool's own command, shown before it runs. |
| `online-only` | Kept in iCloud Drive, Dropbox, Google Drive, or OneDrive, and removed only from this Mac. |
| `explain` | Explained, never removed. For example swap files and the sleep image. |

## Rule format (draft)

One YAML file per owner, grouped by folder.

```
id: xcode.simulator-runtimes
owner: Xcode
name: iOS simulator runtimes
description: >
  Copies of iOS that Xcode uses to test apps. Each one is 7 to 8 GB.
  Xcode can download any of them again from Settings > Components.
paths:
  - /Library/Developer/CoreSimulator/Volumes/*
safety: rebuilds-on-next-use
removal:
  method: command
  command: xcrun simctl runtime delete {runtime-id}
last_used_from: xcrun simctl runtime list -v
```

## Suggest a rule or report a problem

Open an issue with:

1. The app or tool, and its version.
2. The full path (replace your username with `~`).
3. What the folder is, and how you know.
4. Whether it comes back after removal, and how.

Please do not include personal file names or anything private in an issue.

## License

The rules are licensed under [Creative Commons Attribution-NonCommercial-ShareAlike 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). You can use and share them for non-commercial purposes with credit to Diskling. Commercial use needs permission.

By opening an issue or pull request, you agree that Diskling may use your contribution in the Diskling app, including in the paid version.

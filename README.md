zypper-what-would
===

An experimental plugin to answer: "what would happen?" on certain `zypper`
operations.

Supported operations:

- `install` // `i`
- `upgrade` // `u`
- `dist-upgrade` // `du`

This plugin must be in your `$PATH` for `zypper` to pick it up.


Usage
-----
```
USAGE: zypper what-would <operation> [-C] [-D cache_dir] [-h] [-Z <zypper-global-flags>] [...command args]
---
Supported operations:
 - in
 - up
 - dup
```

Modus Operandi
--------------

`zypper` will download all necessary packages involved in the operation, after it
we extract information out of the RPM files and cross check it with the state
of the filesystem.

The result is a series of reports (on the works) that answer the questions:

- What new files are gonna be created?
- What files are gonna be modified?
- Which files already match the new package version file?
- Are there any pending vulns I should pay attention to?

⚠ This plugin is **highly** experimental and messy. Use at your own risk. I don't take any responsibility if you break your system with it.

TODO:
----

- Maybe unified reports?
    * I mean I splat them for convenience, but maybe could be toggleable.
- Maybe per-package reports make sense? 🤔
	* `zypper` doesn't really work in a per-package basis but rather in a whole operation. There should be a way to get more information out of `zypper`... Or improve my text processing skills, same thing 🤷.
- Maybe per-operation (Unchanged, Additions, Mismatches) reports?
- Summarized reports? (exclude the hash, just tell me what's new and doesn't match)
- Do not assume everything is sha256, some packages have sha1 or even MD5.
- Find a way to know what zypper really downloaded to avoid having to clean/create cache dirs.

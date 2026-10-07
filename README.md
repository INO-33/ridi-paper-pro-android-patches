# RIDI Android changes

One private repository for the 23 modified Android projects outside the separate
RIDI kernel/device repositories. The manifest pins each upstream base commit;
binary-safe patches here preserve all source/resource changes from the earlier
individual snapshots. Apply/verify compares complete Git trees, including file
modes, deletions and binary resources. Patches are readable and reviewable in Git.

Use INO-33/RIDI_ANDROID8_MANIFEST's consolidated-20261007 checkpoint to restore.
Its prepare script synchronizes upstream projects and runs apply.py automatically.
Manual entry point: python3 apply.py /path/to/android-source; use --verify to check.
Modified source trees are refused; no reset, clean or forced overwrite is used.
Historical per-project GitHub repositories remain archived read-only backups,
and the new restoration path does not depend on them.

This preserves sources, not a verified clean-environment Android build. Upstream
sources/host packages still need long-term mirrors and fresh-build validation.

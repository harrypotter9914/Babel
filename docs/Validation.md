# Publication and verification scope

[Project overview](../README.md) · [Code walkthrough](Code.md) · [Build guide](Building.md)

## Source first

On 2 November 2026, `main` was fast-forwarded from `bbff197` to the existing v0.57 commit [`8e65618`](https://github.com/harrypotter9914/Babel/commit/8e656185ec6c473ea309d0418762acb49f1673f3) before this presentation was changed. History was preserved; no force push was used.

On 4 November 2026, the existing repository was renamed from `game` to `Babel`. Its repository ID, default branch and existing commit history were preserved. The local remote and source-cloning instructions use the new canonical address.

The Unity source had no outstanding tracked gameplay edits. Local LFS integrity checks passed. Historical TypeScript source remains at the root. Installed `node_modules` dependencies are removed from the current tracked tree, without deleting the local installation or rewriting history.

## Fresh executable checks

Both Windows players were rebuilt through `BablePlayerBuilds.Both`. `tools/Test-Players.ps1` passed for both exported executables using isolated `-bableSaveRoot` directories. It checks campaign/practice separation and runtime systems; practice checks include all five guardian chambers.

The earlier [48 v0.57 camera checks](Release-0.57.md) remain historical evidence, not a newly rerun full campaign traversal.

## Focused capture checks

The new campaign capture verified isolated storage; eight collected runes versus four active slots; rejection of a fifth power; removal of Harvest and equipment of Sun through the actual altar UI; retention of Star, Flight and Moon; and four occupied final sockets.

The range multiplier changed from 1.0 to 1.4 and the shop multiplier from 0.8 to 1.0. Actual beam traces reached 10 and 14 world units from the same player starting position. A cast consumed one Spirit and destroyed existing fractured campaign terrain. No combat settings were changed.

These are deterministic mechanical examples with nearby enemies inactive. They do not establish encounter difficulty, preferred loadouts, full progression validity or economic balance.

## Versions and open questions

The selected PDF has seven pages; the complete PDF has twelve. Both preserve the final v0.56 design edition, with the current public film link. The public itch.io Windows download, current source and new captures are v0.57; its camera revision is described separately rather than silently relabelling an older PDF.

The free v0.57 campaign ZIP was uploaded on 2 November 2026. A fresh unauthenticated HTTP request verified the updated description, installation instructions, trailer and sole public package `babel-0.57.0-windows-x64.zip`; previous uploads are hidden rather than deleted. The submitted archive is 282,193,709 bytes, passed its ZIP integrity check, and contains the freshly tested campaign executable. Its SHA-256 is `2a1019f49ad5893b2438da4e9b184e06fe73378d63ddb0f7616d5d2fea16fa49`.

The published ZIP was downloaded through the public page. Its full-file SHA-256 matches the submitted archive, and its ZIP integrity check passed. The extracted campaign executable also passed a fresh runtime smoke check with isolated save storage. Browser download notifications were delayed; verification used the completed file on disk.

Further observation is needed for first-time gate recognition, resource pressure on long returns, rune choice frequency and guardian recovery-window readability. No formal study, completion rate or new end-to-end campaign playthrough is claimed.

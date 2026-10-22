# vrsns

Remote configuration for the [BattleCraft Launcher](https://github.com/pers1k1/BattleCraft-Remake).
The launcher polls the raw files in this repository on every start to decide what
needs updating, and reads the changelogs shown in its ChangeLogs window.

## Version files

| File | Drives |
| --- | --- |
| `launcher_version.txt` | Launcher self-update (downloads `BCR.exe` from the launcher release) |
| `modpack_version.txt` | Client modpack (`pers1k1/modpack`) |
| `battlecraft_mod_version.txt` | BattleCraft mod (`pers1k1/BattleCraft-mod`) |
| `server_modpack_version.txt` | Server mods (`pers1k1/server`) |
| `server_map_version.txt` | Server world (`pers1k1/server`) |

Each file holds one version string and nothing else. A version is only bumped
when the content it points at actually changed - bumping it otherwise makes every
client redownload for nothing.

## Version format

Launcher versions are dates in sortable `yyyy.MM.dd` form:

```
2026.08.03
2026.08.03hotfix
2026.08.03v2
```

The date is the release day. A second build on the same day adds `hotfix` or
`v2`, `v3`, and so on (`hotfix` ranks the same as `v2`, so use one style per
day). The launcher shows the same version as `03.08.26` in its interface.

Modpack, mod, server and map versions are still plain numbers (`1.6.4`); they
move to the dated format when their content next changes. The launcher
understands both and always treats a dated version as newer than a numbered one.

## Changelogs

Since launcher 22.10.26 every changelog entry is a file of its own:

```
changelog/
  launcher/            Launcher tab
    index.txt
    2026.09.26.ru.txt
    2026.09.26.en.txt
  modpack/             ModPack & ServerMap tab
    index.txt
    mod-2026.10.17hotfix.ru.txt
    mod-2026.10.17hotfix.en.txt
```

- `index.txt` lists entry ids one per line, **oldest first, newest last**. A new
  release appends one line and never rewrites the file.
- An id is `A-Z a-z 0-9 . _ -`, up to 64 characters, no `..`. Launcher entries
  use the canonical version (`2026.10.22`), pack entries `mod-<version>` for a
  mod-only build and `pack-<version>` when the pack itself changed.
- `<id>.ru.txt` and `<id>.en.txt`: the first line is the title shown in accent
  colour (`22.10.26`, `Мод BattleCraft 17.10.26hotfix PRE-ALPHA`), the rest is
  the body. A missing `.en.txt` falls back to the Russian one.
- An entry is capped at 32 KB, the index at 64 KB. All files are UTF-8 without BOM.

Adding a release entry is three steps: write `<id>.ru.txt`, write `<id>.en.txt`,
append `<id>` to `index.txt`. The launcher fetches the index and only the six
newest entries, then six more per "Show more" click.

The old single files (`Launcher_changelog.txt`, `Launcher_changelog_en.txt`,
`ModPack_ServerMap_Changelog.txt`, `ModPack_ServerMap_Changelog_en.txt`) are
frozen at 22.10.26 and only serve launchers older than 22.10.26. Do not add
entries to them; they can be deleted once no such launcher is left.

## License and attribution

Released under the [GNU Affero General Public License v3.0](LICENSE) with the
attribution terms in [NOTICE](NOTICE): forks and derivative works must publish
their source under the same license and keep a visible credit to the author -
pers1k1, https://github.com/pers1k1.

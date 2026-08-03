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

| File | Shown in |
| --- | --- |
| `Launcher_changelog.txt` | Launcher tab, Russian interface |
| `Launcher_changelog_en.txt` | Launcher tab, English interface |
| `ModPack_ServerMap_Changelog.txt` | ModPack & ServerMap tab, Russian interface |
| `ModPack_ServerMap_Changelog_en.txt` | ModPack & ServerMap tab, English interface |

Newest entry goes on top, and both language files get the same entry. All files
are UTF-8 without BOM.

## License and attribution

Released under the [GNU Affero General Public License v3.0](LICENSE) with the
attribution terms in [NOTICE](NOTICE): forks and derivative works must publish
their source under the same license and keep a visible credit to the author -
pers1k1, https://github.com/pers1k1.

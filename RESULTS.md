# `npx skills` migration experiment

Tested with `skills@1.7.0`.

## Scenario

1. An existing user installed `old-admin` from `skills/old-admin/SKILL.md`.
2. The publisher moved it to `retired/old-admin/SKILL.md` and changed its contents to a deprecation notice.
3. The publisher added the replacement at `skills/shopify/SKILL.md`.

## Results

- A fresh `npx skills add durga256/skills-migration-test-20260924-171833 --list` discovered only `shopify`.
- A fresh explicit request for `--skill old-admin` failed with `No matching skills found`.
- For an existing installation, `npx skills update -p` found `old-admin` at its new path and updated its local contents to the deprecation notice.
- The lock entry's `skillPath` changed from `skills/old-admin/SKILL.md` to `retired/old-admin/SKILL.md`.
- The replacement `shopify` skill was not installed automatically.

## Conclusion

Moving a legacy skill outside the normal discovery tree provides a migration bridge: new users do not see it, while existing users receive updated deprecation instructions when they run `npx skills update`. They must still install the replacement skill themselves.

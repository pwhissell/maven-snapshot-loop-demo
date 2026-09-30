# Grouped Java Snapshot Loop Reproduction

This two-module Maven project demonstrates the grouped Java snapshot PR loop
described by the release-please bug skill.

## Reproduce

1. Copy this directory to a new GitHub repository with `main` as its default
   branch, then push the initial files.
2. Push commits with these messages:

   ```text
   fix(alpha): add alpha behavior
   fix(beta): add beta behavior
   ```

3. Merge the grouped release PR created by release-please.
4. Merge the grouped `autorelease: snapshot` PR that follows.
5. Push another commit:

   ```text
   fix(alpha): correct alpha behavior
   ```

Expected: release-please opens a regular release PR for `alpha`.

Affected behavior: release-please opens another snapshot PR with no file
changes instead. The grouped snapshot PR title has no component name, so
component-level Java snapshot detection does not recognize the snapshot from
its title. Merging that PR can repeat the cycle.

The included workflow grants the GitHub token permission to create releases
and pull requests. Ensure repository Actions settings allow workflows to
create pull requests.
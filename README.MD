# GeoMop custom GitHub Actions

This repository contains custom GitHub Actions used across GeoMop projects.

## Versioning and Tagging

All Actions follow [Semantic Versioning](https://semver.org/).
Always add **v** prefix before version number.
Each release includes three types of tags:

| Tag type | Example | Description   |
|----------|---------|---------------|
| Path     | v1.0.5  | Immutable tag |
| Minor    | v1.5    | Floating tag  |
| Major    | v1      | Latest stable |

## Tag Management

When a new release (e.g., v4.1.6) is published, the following happens automatically:
- A permanent tag v4.1.6 is created for that specific version.
- Floating tags v4 and v4.1 are moved to point to this new release.

This ensures that:
- v4 always points to the latest v4.*.* release.
- v4.1 always points to the latest v4.1.* release.

## 💡 Recommendations

- Use @v4 or @v4.1 if you want automatic minor/patch updates.
- Use a fixed tag or SHA if you need fully deterministic builds.
- Tags are digitally signed and automatically updated by CI during each release.

## Example
If you want to release a new patch version manually, follow these steps:

```bash
# Make sure your local branch is up to date
git checkout main
git pull origin main

# Create an immutable tag for the new patch version
git tag -s v1.1.6 -m "Release v1.1.6"

# Push the new patch tag to GitHub
git push origin v1.1.6

# Update floating tags to point to this version
git tag -fa v1 v1.1.6^{}
git tag -fa v1.1 v1.1.6^{}

# Push the updated floating tags (force is needed because they move)
git push origin v1 v1.1 --force
```

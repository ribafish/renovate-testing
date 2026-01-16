# Renovate Testing

Test repository for Maven wrapper checksum updates (GitHub issue #33444).

## Current Versions
- Maven: 3.9.6
- Maven Wrapper: 3.3.1

Both have SHA-256 checksums configured in `.mvn/wrapper/maven-wrapper.properties`.

## Testing Renovate

Run Renovate locally against this repo:

```bash
# First install dependencies
pnpm install

# Then build Renovate to verify it builds
pnpm build

# Then run
LOG_LEVEL=debug pnpm start  --platform=github --token=$(gh auth token) --pr-hourly-limit=0 ribafish/renovate-testing
```

## Expected Behavior

When Renovate detects newer versions:
1. **Maven 3.9.9 update**: Should update `distributionUrl` and `distributionSha256Sum`
2. **Maven Wrapper 3.3.2 update**: Should update `wrapperUrl` and `wrapperSha256Sum`

The checksums should be computed by downloading the new artifacts and calculating SHA-256.

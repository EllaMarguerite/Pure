# CloudCannon Build Configuration

## Node.js Version Setup

This project requires Node.js 20+ to build successfully. To configure CloudCannon to use the correct Node.js version:

### Option 1: Use .nvmrc file (Recommended)

1. Go to your CloudCannon site dashboard
2. Navigate to **Site Settings** → **Build configuration**
3. Under **Library versions**, find **Node version**
4. Select **"Use my .nvmrc file"** option
5. Click **Update Site**

The `.nvmrc` file in this repository specifies Node.js 20.19.5, which CloudCannon supports.

### Option 2: Manual Version Selection

If you prefer to manually select the version:

1. Go to **Site Settings** → **Build configuration**
2. Under **Library versions**, set **Node version** to **20.19.5** (or **22.20.0**)
3. Click **Update Site**

## Build Command

The build command should be:
```
npm install && npm run build
```

Or if you're using npm ci for more reliable builds:
```
npm ci && npm run build
```

**Note:** The build script has been updated to call the `astro-pure check` script directly, bypassing the need for bin script permissions. This resolves the `EPERM` chmod error in CloudCannon.

## Troubleshooting Permission Errors

If you encounter `EPERM` (permission) errors during `npm install`:

1. **Ensure Node.js 20+ is configured** - This is the most important step
2. **The bin script has been removed** - The build script now calls the check script directly using `node packages/pure/scripts/check.mjs`, which bypasses npm's bin linking and avoids permission errors
3. The permission error should be resolved with the updated build script
4. If issues persist, contact CloudCannon support as it may be a platform-specific permission configuration

## Available Node.js Versions in CloudCannon

CloudCannon supports these Node.js versions:
- 14.21.3
- 16.20.2
- 18.20.8 (default - **not compatible with this project**)
- 20.19.5 ✅ (recommended for this project)
- 22.20.0 ✅ (also compatible)
- 24.10.0 ✅ (also compatible)

## Verification

After updating the Node.js version, trigger a new build. The build logs should show:
- Node version: `v20.19.5` (or your selected version)
- No `EBADENGINE` warnings
- Successful `npm install` completion

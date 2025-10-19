# GitHub Actions for Data API Builder

This repository includes GitHub Actions workflows for building, testing, and publishing the Data API Builder NuGet package.

## Workflows

### 1. Build and Publish NuGet Package (`nuget-publish.yml`)

This workflow builds the solution, runs tests, creates a NuGet package, and publishes it to NuGet.org and optionally to GitHub Packages.

**Triggers:**
- **Push to main branch**: Creates and publishes a pre-release package (e.g., `1.7.0-123`)
- **Tagged release** (e.g., `v1.7.0`): Creates and publishes a stable release package
- **Manual trigger**: Allows manual publishing with a toggle option

**Features:**
- Multi-stage build with dependency caching
- Automated versioning based on git tags and build numbers
- Test execution and result reporting
- NuGet package creation and publishing
- GitHub release creation for tagged versions
- Artifact upload for debugging

### 2. Build and Test (`build-test.yml`)

This workflow builds and tests the solution across multiple operating systems for pull requests and development branches.

**Triggers:**
- Pull requests to main/develop branches
- Pushes to develop, feature/*, bugfix/* branches

**Features:**
- Cross-platform testing (Ubuntu, Windows, macOS)
- Code quality analysis
- Format checking
- Test result reporting

## Setup Instructions

### 1. Required Secrets

Add the following secrets to your GitHub repository (Settings → Secrets and variables → Actions):

- **`NUGET_API_KEY`**: Your NuGet.org API key for publishing packages
  - Go to [NuGet.org](https://www.nuget.org) → Account Settings → API Keys
  - Create a new API key with push permissions for your package
  - Copy the key and add it as a repository secret

### 2. Environment Protection (Optional but Recommended)

For additional security, set up an environment for NuGet publishing:

1. Go to Settings → Environments
2. Create an environment named `nuget-publishing`
3. Add protection rules:
   - Required reviewers (for manual approval before publishing)
   - Restrict to main branch only
   - Add the `NUGET_API_KEY` secret to this environment

### 3. GitHub Packages (Optional)

If you want to also publish to GitHub Packages, ensure your repository has the correct permissions:

1. The workflow uses `GITHUB_TOKEN` (automatically provided)
2. Make sure the repository has package write permissions enabled

## Package Versioning Strategy

The workflow uses the following versioning strategy:

- **Tagged releases** (`v1.7.0`): Clean version number (`1.7.0`)
- **Main branch**: Base version + build number (`1.7.0-123`)
- **PR/Feature branches**: Base version + PR/build info (`1.7.0-pr45-123`)

Version numbers are read from `src/Directory.Build.props`.

## Manual Publishing

You can manually trigger a package build and publish:

1. Go to Actions → "Build and Publish NuGet Package"
2. Click "Run workflow"
3. Choose the branch
4. Toggle "Publish package to NuGet.org" if you want to publish
5. Click "Run workflow"

## Monitoring

- **Build status**: Check the Actions tab for build results
- **Package publishing**: Monitor the NuGet.org dashboard for new packages
- **Test results**: View test artifacts in the workflow runs
- **Releases**: Check the Releases section for automatic releases

## Troubleshooting

### Common Issues

1. **NuGet API Key Expired**
   - Generate a new API key on NuGet.org
   - Update the `NUGET_API_KEY` secret

2. **Package Already Exists**
   - NuGet.org doesn't allow overwriting existing versions
   - Increment version in `Directory.Build.props` or create a new tag

3. **Test Failures**
   - Check test results in the workflow artifacts
   - Tests must pass before package publishing

4. **Permission Denied for GitHub Packages**
   - Ensure the repository has package write permissions
   - Check that `GITHUB_TOKEN` has the necessary scopes

### Debugging

- Download workflow artifacts to examine build outputs
- Check the detailed logs in each workflow step
- Verify that all required dependencies are properly restored

## Local Testing

To test the package build locally:

```bash
# Restore dependencies
dotnet restore src/Azure.DataApiBuilder.sln --configfile Nuget.config

# Build solution
dotnet build src/Azure.DataApiBuilder.sln --configuration Release

# Run tests
dotnet test src/Azure.DataApiBuilder.sln --configuration Release

# Create package
dotnet pack src/Cli/Cli.csproj --configuration Release --output ./packages
```
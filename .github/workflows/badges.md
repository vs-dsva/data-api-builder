# GitHub Actions Badges

Add these badges to your README.md to show the status of your GitHub Actions workflows:

## Build and Publish Status
```markdown
[![Build and Publish NuGet Package](https://github.com/vs-dsva/data-api-builder/actions/workflows/nuget-publish.yml/badge.svg)](https://github.com/vs-dsva/data-api-builder/actions/workflows/nuget-publish.yml)
```

## Build and Test Status
```markdown
[![Build and Test](https://github.com/vs-dsva/data-api-builder/actions/workflows/build-test.yml/badge.svg)](https://github.com/vs-dsva/data-api-builder/actions/workflows/build-test.yml)
```

## NuGet Package
```markdown
[![NuGet Version](https://img.shields.io/nuget/v/Microsoft.DataApiBuilder.svg)](https://www.nuget.org/packages/Microsoft.DataApiBuilder/)
[![NuGet Downloads](https://img.shields.io/nuget/dt/Microsoft.DataApiBuilder.svg)](https://www.nuget.org/packages/Microsoft.DataApiBuilder/)
```

## Combined Badge Example

```markdown
[![Build and Publish](https://github.com/vs-dsva/data-api-builder/actions/workflows/nuget-publish.yml/badge.svg)](https://github.com/vs-dsva/data-api-builder/actions/workflows/nuget-publish.yml)
[![Build and Test](https://github.com/vs-dsva/data-api-builder/actions/workflows/build-test.yml/badge.svg)](https://github.com/vs-dsva/data-api-builder/actions/workflows/build-test.yml)
[![NuGet](https://img.shields.io/nuget/v/Microsoft.DataApiBuilder.svg)](https://www.nuget.org/packages/Microsoft.DataApiBuilder/)
```

Replace `vs-dsva/data-api-builder` with your actual GitHub repository path if different.
---
date created: 2024-08-21
date modified: 2024-08-21
---
# FileVersion

FileVersion vs AssemblyVersion:
- FileVersion is typically used for informational purposes and can be changed more frequently.
- AssemblyVersion is used by the .NET runtime for binding and should change less frequently to avoid breaking dependencies.

While Visual Studio doesn't auto-increment it, you can set up build scripts or CI/CD pipelines to update this value automatically if needed.

# libgit2sharp4unity

This repository doesn't do much apart from serving as a possible google search result for someone failing to run [libgit2sharp](https://github.com/libgit2/libgit2sharp) in Unity, I spent three days looking for a solution because other unity-related search results were quite misleading and pointing to a different set of problems before Unity allowed for `.NET Framework` [Api Compatibility Level](https://docs.unity3d.com/Manual/dotnetProfileSupport.html).

You can watch this youtube video: https://www.youtube.com/watch?v=G4XlZC2S07Y for a quick tut on how to properly pull packages from `nuget` (with all their necessary dependencies) for their use in Unity.

.csproj then `dotnet restore`

```
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Library</OutputType>
    <TargetFramework>net48</TargetFramework>
    <RuntimeIdentifiers>win-x64;linux-x64;osx-x64</RuntimeIdentifiers>
    <SelfContained>false</SelfContained>
    <CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>
    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="LibGit2Sharp" Version="0.30.0" />
  </ItemGroup>

  <ItemGroup>
    <Content Include="$(UserProfile)\.nuget\packages\libgit2sharp.nativebinaries\2.0.322\runtimes\**\*" CopyToOutputDirectory="PreserveNewest" />
  </ItemGroup>

</Project>

```

In short its:
- create a new `Class Library` solution while making sure you select the template for `.NET Framework` if that is your api compatibility level (choose one for `.NET Standard` otherwise)
- pull the desired packages and accept the dependencies through `Tools -> Nuget ...`
- right click in the solution explorer on the solution and press open in terminal
- `.csproj` is important
- remove bin and obj directories
- run `dotnet build -c Release` in solution terminal
- generated dlls will all be in `/bin/` subdirectory of the solution
- put them in Unity
- make sure to properly set up those dlls for specific platforms (sould be ok out of the box but check)
- mark all those dlls as `Load on startup` through such checkbox in that lib file in unity
- likely be happy cos it might be working now

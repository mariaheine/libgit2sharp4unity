# libgit2sharp4unity6

Since Unity 6 supports dlls with net4.8 profile on both `.NET Framework` and `.NET Standard 2.1` [Api Compatibility Levels](https://docs.unity3d.com/Manual/dotnetProfileSupport.html) (see the table), we can easily use `0.30.0` LibGit2Sharp version (`0.31.0` being the very latest but targetting net8.0).

To get dlls simply clone this repo, open it in Visual Studio, right click solution and open it in terminal, then:
- $ `dotnet restore`
- $ `dotnet build -c Release`

Then all the dlls you need will be in `../bin/Release` directory.

Put them in Unity `Plugins` directory and make sure they are properly assigned for different platforms, don't forget to set them to `Load on startup` after you do that.

Should work already.

So far tried only building with mono on windows though, good luck!

## post scriptum

The only really important file here is the `libgit2sharp4unity6.csproj` one:

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

Once unity supports net8.0 we will be able to update to `0.31.0` LibGit2Sharp: https://github.com/libgit2/libgit2sharp.
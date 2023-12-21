# libgit2sharp4unity

This repository doesn't do much apart from serving as a possible google search result for someone failing to run `libgit2sharp` in Unity, I spent three days looking for a solution because other unity-related search results were quite misleading and pointing to a different set of problems before Unity allowed for `.NET Framework` [Api Compatibility Level](https://docs.unity3d.com/Manual/dotnetProfileSupport.html).

You can watch this youtube video: https://www.youtube.com/watch?v=G4XlZC2S07Y for a quick tut on how to properly pull packages from `nuget` (with all their necessary dependencies) for their use in Unity.

In short its:
- create a new `Class Library` solution while making sure you select the template for `.NET Framework` if that is your api compatibility level (choose one for `.NET Standard` otherwise)
- pull the desired packages and accept the dependencies through `Tools -> Nuget ...`
- run `dotnet publish` in solution terminal
- generated dlls will all be in `/bin/` subdirectory of the solution
- put them in Unity
- likely be happy cos it might be working now

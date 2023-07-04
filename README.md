# FarCry
This is mostly unchanged original [leaked Far Cry source tree](https://archive.org/details/far-cry-1.34-complete).
Some modifications were made to original sources and project configuration in order to make it able to be built using Visual Studio 2022 for x64 v143 target.  
This repository has 2 branches:
* [leak](https://github.com/n1f7/FarCry/tree/leak) - contains the original leaked source with project files overwritten by `AMD64_ProjectFiles_VS2005` contents
* [win32_x64 (default)](https://github.com/n1f7/FarCry/tree/win32_x64) - check out this branch if you want to build from sources using Visual Studio 2022

## Building from source
Bundled DirectX SDK was removed, so in order to build from sources you need to install [DirectX 9 SDK from Microsoft](https://www.microsoft.com/en-gb/download/details.aspx?id=6812).  
Just load `Game01.sln`, select `Release64` solution configuration and run `Build solution`.
20 out of 22 project will compile and link, only 2 will fail (`XRenderOGL` and `Editor`), you can unload them for the present if you wish.
## Running the binaries
X64 build was tested using assets from the latest Steam version of the game patched with [64-bit Upgrade Patch from PC Gaming Wiki](https://community.pcgamingwiki.com/files/file/442-far-cry-amd64-64-bit-upgrade-patch/).
Saves work fine, game still has some unhandled exceptions on shutdown only noticeable during debugging.  
1. Create some directory alongside `Bin32` or `Bin64` directories, for example `CustomBuild`
2. Place compiled binaries from `FarCry/x64/Release64/` folder (16 `DLL`s ans 3 `EXE`s in total)
3. You still need to copy the following 5 DLLs from `Bin64` folder: `DivxDecoder.dll`, `DivxMediaLib.dll`, `FileParser.dll`, `msvcr71.dll`, `crysound64.dll`
4. You can optionally copy some `*.pdb` files to aid debugging
   
The resultant file tree should look something like this:
```
CustomBuild
├── Cry3DEngine.dll
├── CryAISystem.dll
├── CryAnimation.dll
├── CryEntitySystem.dll
├── CryFont.dll
├── CryGame.dll
├── CryInput.dll
├── CryMovie.dll
├── CryNetwork.dll
├── CryPhysics.dll
├── CryScriptSystem.dll
├── CrySoundSystem.dll
├── CrySystem.dll
├── DivxDecoder.dll
├── DivxMediaLib.dll
├── FarCry.exe
├── FarCry_WinSV.exe
├── FileParser.dll
├── ResourceCompilerPC64.dll
├── XRenderD3D9.dll
├── XRenderNULL.dll
├── crysound64.dll
├── msvcr71.dll
└── rc64.exe
```

# Editor
Editor builds fine but linking stage still fails due to it still dependent on closed source proprietory XTreme Toolkit for MFC

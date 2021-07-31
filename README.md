# Pre-built Windows dependencies for [VCMI](https://github.com/vcmi/vcmi)

Built and exported by [Vcpkg](https://github.com/Microsoft/vcpkg).

## Instructions

* Install Vcpkg and it's dependencies.
* Build all required packages for one or both architectures:
```
vcpkg install tbb:x64-windows fuzzylite:x64-windows sdl2:x64-windows sdl2-image:x64-windows sdl2-ttf:x64-windows sdl2-mixer:x64-windows boost:x64-windows qt5:x64-windows ffmpeg:x64-windows
vcpkg install tbb:x86-windows fuzzylite:x86-windows sdl2:x86-windows sdl2-image:x86-windows sdl2-ttf:x86-windows sdl2-mixer:x86-windows boost:x86-windows qt5:x86-windows ffmpeg:x86-windows
```
* Export packages so 7z archive will be produced:
```
vcpkg export tbb:x64-windows fuzzylite:x64-windows sdl2:x64-windows sdl2-image:x64-windows sdl2-ttf:x64-windows sdl2-mixer:x64-windows boost:x64-windows qt5:x64-windows ffmpeg:x64-windows --7zip
vcpkg export tbb:x86-windows fuzzylite:x86-windows sdl2:x86-windows sdl2-image:x86-windows sdl2-ttf:x86-windows sdl2-mixer:x86-windows boost:x86-windows qt5:x86-windows ffmpeg:x86-windows --7zip
```
* Rename archives appropriately. Bevare that Vcpkg use newest MSVC available by default, but [it's possible to enforce certain version with custom triplet](https://github.com/Microsoft/vcpkg/issues/1207).  
```
vcpkg-export-20170802-233045.7z -> vcpkg-export-x86-windows-v140.7z
vcpkg-export-20170802-233045.7z -> vcpkg-export-x64-windows-v140.7z
```
* Rename root directory inside archive from ```vcpkg-export-20170802-233045``` to ```vcpkg```. Can be done via command line 7-zip:
```
# Linux
7za rn vcpkg-export-x64-windows-v140.7z vcpkg-export-20170802-233045 vcpkg
# Windows. Fail for some reason.
7z.exe rn vcpkg-export-x64-windows-v140.7z vcpkg-export-20170802-233045 vcpkg
```
* Archives can be uploaded to releases using [github-release](https://github.com/aktau/github-release):
```
github-release upload --user vcmi --repo vcmi-deps-windows --tag v1 --name "vcpkg-export-x86-windows-v140.7z" --file vcpkg-export-x86-windows-v140.7z --security-token 9eatokentokentokentokentoken6e
```
* Package list can be generated with:
```
echo -e "\n| Package | Version |\n| --- | --- |"; ./vcpkg list | grep x86 | grep -v static | awk '{ print "| " $1 " | " $2 " |"}' | sed -r 's/:x86-windows//'
```

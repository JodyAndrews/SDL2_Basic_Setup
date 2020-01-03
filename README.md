# SDL2 Basic Setup with Demo for OSX Mojave and Catalina

### December 2019

This project is still valid, and should build and run but just let me know if not.

### December 2018

This repo is simply a basic SDL2 setup and demo that finds and uses the latest brew installs of SDL2 libraries you'd most likely desire for a game. Please do fork and call it your own, or feel free to raise an issue, and include the CMake output.

Don't expect too much :) All it does is demo initialising SDL2, loading a texture as a background, draw a rectangle that we can drag with the mouse, ttf with an external font, mixer and play ogg 'music' (some free walking sound I found), and changes the app icon in the Dock, and has a _game loop_ with fixed timing.

The main reason I wrote this is because PKG_SEARCH_MODULE stopped working for me and I was fed up with broken apps, this looked a better cross platform(ish) solution, so this works as a nice starter project on new OS installs. 

## Installation

Xcode Command Line Tools ( if not already installed )

- xcode-select --install

SDL2 Installs

- brew install sdl2
- brew install sdl2_image
- brew install sdl2_mixer
- brew install sdl2_ttf

## Building with CLion

I use CLion although it's not required ( see a below step for building without CLion ). 

You should be able to clone this repo and open the root folder in CLion. This will auto run CMake against the root _CMakeLists.txt_ file and create a _cmake_build_debug_ folder, within which will be a _bin_ folder and sample resources. Once you've built the project the executable will be compiled to there.

You can either use CLion's debug/run or run the executable in finder. I recommend lldb for debugging. 

[lldb cheat sheet](https://www.nesono.com/sites/default/files/lldb%20cheat%20sheet.pdf)

Useful common lldb command examples.. 

Show contents of global variable _whatever_ `ta v whatever`  
Show global/static variables in current file `ta v`  
Show contents of variable _whatever_ `fr v whatever`  

### Copying Resources to Bin Location ###

Changes to the root _resources_ folder will require CMake to be ran again as it copies the resources folder to the bin folder, in CLion just use _File -> Reload CMake Project_

## Command Line Build

- mkdir out
- cd out
- cmake ../
- make

## Runtime Oddities (Important)

With the SDL installs always make sure you're using either Brew **or** a Framework, not both, or you'll receive a warning about not knowing which to use and also potentially hit an obnoxious runtime error, this isn't specific to this project. 

I would suggest **only** using the brew installs mentioned in the **Installation** step above and removing their respective SDL frameworks from _/library/frameworks_ to get around this. Your mileage may vary, but on a clean install I've had no issue with this setup.

## Notes

The Find CMAKE files are written by others, the only change I've made is to FindSDL2Mixer as it uses the SDL2 lib location for it's search. I've changed this to pick up the location returned from FindSDL2 which means there's a dependency between the two, which also means you can't copy FindSDL2Mixer.cmake to another project and expect it to work by itself. I should probably add a comment to that file.

My understanding of these Find CMAKE files is still slim, so I'll rewrite these for my own use in time and get a better understanding. If you've written your own then please get in touch or send a pull request.

Feedback is always very welcome. Happy building :)


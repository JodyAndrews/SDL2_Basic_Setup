# SDL2_Basic_Setup for OSX Mojave

### December 2018

This repo is very simply a basic SDL2 setup and demo that finds and uses the latest brew installs of SDL2 libraries you'd most likely desire for a game.

Don't expect too much :) All it does is demo initialising SDL2, loading a texture as a background, draw a rectangle that we can drag with the mouse, ttf with an external font, mixer and play ogg 'music' (some free walking sound I found), and changes the app icon in the Dock, and has a _game loop_ with fixed timing.

The code is rough but should work. Open an issue if there's any problems or suggestions though and I'll take a look asap. Or just fork and call it your own. Include the CMake output in any issue. It's **very** verbose and welcome!

The main reason I wrote this is because PKG_SEARCH_MODULE stopped working for me and was fed up with broken apps, this looked a better cross platform(ish) solution, so this works as a nice testbed on new installs.

## Installation

Xcode Command Line Tools ( if not already installed )

- xcode-select --install

SDL2 Installs

- brew install sdl2
- brew install sdl2_image
- brew install sdl2_mixer
- brew install sdl2_ttf

## Building with CLion

I use CLion although it's not required ( see below step instead for CLI ). You should be able to clone this repo and open the root folder in CLion. This will auto run CMake against the CMakeLists.txt file and create a _cmake_build_debug_ folder, within which will be a _bin_ folder and sample resources. Once you've built the project the executable will be compiled to there.

You can either use CLion's debug/run or run the executable in finder. Just use lldb for debugging. There was some kerfuffle about gdb and osx a while back, just go with the flow and use lldb on osx - or let me know why not, genuinely interested.

Changes to the root resource folder will require CMake to be ran again as it copies resources to the bin folder, in CLion just use _File -> Reload CMake Project_

## Command Line Build

- mkdir out
- cd out
- cmake ../
- make

## Runtime Oddities

With the SDL installs always make sure you're using either Brew **or** a framework, not both, or you'll receive a warning about not knowing which to use and potentially hit an obnoxious runtime error, this isn't specific to this project, _the code isn't that bad_. I trust brew more, so I would suggest using the brew installs mentioned above and removing the SDL frameworks from /library/frameworks to get around this. Your mileage may vary, but on a clean install I've had no issue with this setup.

## Notes

The Find CMAKE files are written by others, I've tested them and they work fine on OSX Mojave. The only change I've made is to FindSDL2Mixer as it uses the SDL2 lib location for it's search. I've changed this to pick up the location returned from FindSDL2 which means there's a dependency between the two, which also means you can't copy FindSDL2Mixer.cmake to another project and expect it to work. I probably should add a comment to that file.

My understanding of these Find CMAKE files is very slim, so I'll rewrite these for my own use in time and get a better understanding.

Feedback is always very welcome. Happy building :)


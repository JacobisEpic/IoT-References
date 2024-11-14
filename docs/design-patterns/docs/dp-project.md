# Setting up a new project

By setting up a project we mean -- writing a new program somewhere
else than in your copy of the ESP software distribution that you
downloaded. For example, you probably want to write your new code in
one of the skill directories. Here is how to do it.

This all assumes you are set up, your install environment works
(including setting up paths), and you are editing local (on your
laptop) files.

Here are the basic steps:

1. Find a good program example to copy (e.g., Blink) from the ESP distro examples.
2. Copy this to your code subfolder in your local copy of your skills folder. This brings everything over.
3. Rename the folder and the files with your new stuff (e.g., new-blink)
4. idf.py set-target esp32 clears the build directory and regenerates sdkconfig
5. idf.py menuconfig sets up your build environment including port speed
6. idf.py build does the build
7. If the ESP is connected. idf.py -p PORT flash builds and flashes etc.
8. idf.py clean removes the build directory (idf.py fullclean also removes the config and sdkconf files)

## References
- [Sample project](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html#example-project)
- [Using the Build System](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html#using-the-build-system)


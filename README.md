> Only a compound can be beautiful, never anything devoid of parts; and only a whole;<br>
> the several parts will have beauty, not in themselves,<br>
> but only as working together to give a comely total.<br>
> Yet beauty in an aggregate demands beauty in details:<br>
> it cannot be constructed out of ugliness; its law must run throughout.

– [Plotinus](https://en.wikipedia.org/wiki/Plotinus), *First Ennead*


<h1 align="center">Plotinus</h1>
<h3 align="center">A searchable command palette in every modern GTK+ application</h3>
<br>

Have you used Sublime Text's or Atom's "Command Palette"? It's a list of everything those editors can do that opens at the press of a key and finds the action you are looking for just by typing a few letters. It's raw power at your fingertips.

Plotinus brings that power ***to every application on your system*** (that is, to those that use the GTK+ 3 toolkit). It automatically extracts all available commands by introspecting a running application, instantly adapting to UI changes and showing only relevant actions. Using Plotinus requires *no modifications* to the application itself!

Just press <kbd>Ctrl+Shift+P</kbd> ([configurable](#configuration)) and you're in business – it feels so natural you'll soon wonder how you ever lived without it.

![Nautilus screencast](https://cloud.githubusercontent.com/assets/2702526/20246717/454a1a9a-a9e3-11e6-8b19-4db092348793.gif)

![gedit screencast](https://cloud.githubusercontent.com/assets/2702526/20246718/5397bed6-a9e3-11e6-8023-aa9a318820e3.gif)


## Installation

### Prerequisites

To build Plotinus from source, you need Git, CMake, Vala, and the GTK+ 3 development files. All of these are easily obtained on most modern Linux distributions:

#### Fedora / RHEL / etc.

```
sudo dnf install git cmake vala gtk3-devel
```

#### Ubuntu / Mint / Elementary / etc.

```
sudo apt-get install git cmake valac libgtk-3-dev
```

### Building

```
git clone https://github.com/p-e-w/plotinus.git
cd plotinus
mkdir build
cd build
cmake ..
make
sudo make install
```

### Enabling Plotinus in applications

Because of the complexity and clumsiness surrounding Linux environment variables, Plotinus is currently not enabled automatically. The easiest way to enable Plotinus for all applications on the system is to add the line

```
GTK3_MODULES=[libpath]
```

to `/etc/environment`, where `[libpath]` is the *full, absolute* path of `libplotinus.so`, which can be found using the command

```
whereis -b libplotinus
```

Alternatively, you can try Plotinus with individual applications by running them with

```
GTK3_MODULES=[libpath] application
```

from a terminal.


## Configuration

Plotinus can be configured both globally and per application. Application settings take precedence over global settings. In the commands below, `[application]` can be either

* `default`, in which case the setting is applied globally, or
* the path of an application executable, without the leading slash and with all other slashes replaced by periods (e.g. `/usr/bin/gedit` -> `usr.bin.gedit`).

Note that the relevant path is the path of the *process executable*, which is not always identical to the executable being launched. For example, all GNOME JavaScript applications run the process `/usr/bin/gjs`.

### Enabling/disabling Plotinus

```
gsettings set com.worldwidemann.plotinus:/com/worldwidemann/plotinus/[application]/ enabled [true/false]
```

### Changing the keyboard shortcut

```
gsettings set com.worldwidemann.plotinus:/com/worldwidemann/plotinus/[application]/ hotkeys '[keys]'
```

`[keys]` must be an array of strings in the format expected by [`gtk_accelerator_parse`](https://developer.gnome.org/gtk3/stable/gtk3-Keyboard-Accelerators.html#gtk-accelerator-parse), e.g. `["<Primary><Shift>P", "<Primary>P"]`. Each shortcut in the array activates Plotinus.


## Acknowledgments

Documentation on GTK+ modules is essentially nonexisting. Without [gtkparasite](https://github.com/chipx86/gtkparasite) and [gnome-globalmenu](https://github.com/gnome-globalmenu/gnome-globalmenu) to learn from, it would have been a lot harder to get this project off the ground.

The CMake modules are copied verbatim from Elementary's [pantheon-installer](https://github.com/elementary/pantheon-installer) repository.

Vala is still the greatest thing ever to happen to Linux Desktop development.


## Contributing

Contributors are always welcome. However, **please file an issue describing what you intend to add before opening a pull request,** *especially* for new features! I have a clear vision of what I want (and do not want) Plotinus to be, so discussing potential additions might help you avoid duplication and wasted work.

By contributing, you agree to release your changes under the same license as the rest of the project (see below).


## License

Copyright &copy; 2016-2017 Philipp Emanuel Weidmann (<pew@worldwidemann.com>)

Released under the terms of the [GNU General Public License, version 3](https://gnu.org/licenses/gpl.html)

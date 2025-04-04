
k so if ur on arch(like me) and want to get ros2-foxy(this is what our actual car is on) going, its going to be a bit of a pain. 
the AUR(arch user repository) was only really made to have latest versions, and even if you did find stuff theres going to be tons of
dependancy issues since alot of them are likely abandoned and deperecated.


im going to be documenting what it took for me to get ros2foxy going on my machine(arch linux).

if you are on ubuntu your life is easy(DONT FOLLOW THIS).

Obviously, if you dont care about running this natively, just make a docker image and follow the windows steps.


# Step 1
## installing system dependancies

```
sudo pacman -S --needed git base-devel cmake \
  python-pip python-setuptools python-yaml \
  asio tinyxml2 qt5-base curl \
  python-rosdep python-colcon-common-extensions \
  python-empy python-argcomplete
```


running this may result in a target not found error. this just means the libraries areint in the official arch pacman repo. could be in aur or elsewhere. i chose to install via pip. the two that didnt show up for me are python-rosdep, and python-colcon-common-extensions.

first off, make sure pip is installed

```
sudo pacman -S python-pip
```


pacman didnt like me installing a package not in their directory. this is my insalling it though.

```
pip install --break-system-packages -U rosdep colcon-common-extensions


```

ive also never had any package not downloaded via pacman or yay yet, so i added this line to my zshrc file so these packages downloaded via pip are included in the path

`export PATH="$HOME/.local/bin:$PATH"`

make sure all is good after installing the two using

```
which rosdep
which colcon
```
wait i guess that was it. thought it was going to be longer than that.

from here im going to show you how to create a new ws. i like creating a new ws for every separate project i work on, but this is not necessary whatsoever.
```                                                 ─╯
mkdir -p [nameofws]/src
colcon build
```
 honestly man i already know its just one person going to be using this sanil just come talk to me if u get to this point
 

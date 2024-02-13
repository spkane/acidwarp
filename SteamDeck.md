# Acidwarp

Now, you can have a pseudo-screensaver for your SteamDeck.

**WARNING** Please only do this if you understand each step. These are advanced directions and it could break your SteamDeck. I am not responsible for what happens...

`"It worked for me..."`

## SteamDeck

# Build `acidwarp` for the SteamDeck

- SSH into the SteamDeck or launch a terminal in Desktop mode.

```sh
sudo steamos-readonly disable
sudo pacman-key --init
sudo pacman-key --populate archlinux
sudo pacman -Syy
vi /etc/pacman.conf
```

- Add a new `SigLevel` line and comment out the original one.
  
```ini
#SigLevel    = Required DatabaseOptional
SigLevel = Never
```

```sh
sudo pacman -Sy base-devel glibc linux-api-headers lib32-sdl12-compat
vi /etc/pacman.conf
```

- Comment out the new `SigLevel` line and enable the original one.

```ini
SigLevel    = Required DatabaseOptional
#SigLevel = Never
```

- Make the root filesystem readonly again.

```sh
sudo steamos-readonly enable
```

- Build `acidwarp` on the SteamDeck

```sh
mkdir ~/dev
cd ~/dev
git clone https://github.com/spkane/acidwarp
cd acidwarp
git checkout steamdeck
make SDL=2
mkdir ~/bin
cp acidwarp ~/bin
cd ~/bin
```

- From Desktop mode test it out.

```sh
~/bin/acidwarp -n -f -k
```

- Now add it as a non-steam game if you want. I suggest using the command arguments listed above.
  - e.g. [how-to-add-non-steam-games-to-steam-deck](https://www.dexerto.com/tech/how-to-add-non-steam-games-to-steam-deck-2082992/)
  - **NOTE**: You do not need to enable compatibility mode, since this is a native Linux application.
  - Feel free to add any `acidwarp` images that you like to the entry in your library.


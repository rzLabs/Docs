# Notice

The process detailed below will **NOT** work for any client that has **Game Guard** enabled! This documentation is founded on using `Arch/Manjaro` Linux but should be easily adaptable to any distribution that supports `Wine`

# Requirements

- [Wine-Staging](https://wiki.winehq.org/Wine-Staging)
- [Winetricks](https://github.com/Winetricks/winetricks)
- Rappelz Client

# Setup

## Install `wine-staging`

```console
sudo pacman -S wine-staging winetricks wine-mono wine_gecko
```

## Create and initialize a 32bit prefix

Many `verb` or `package` can/will only install as `32 bit` so we must create an environment or `prefix` to make this distinction.

```console
WINEPREFIX=~/win32 WINEARCH=win32 winecfg
```

> **Note:** Creating the prefix will create a `win32` folder in your home directory *(e.g. `~/win32` or `/home/iSmokeDrow/win32`)*

## Install required dependencies via `wine`

### [DXVK](https://github.com/doitsujin/dxvk)

```console
WINEPREFIX=~/win32 winetricks dxvk
```

### Corefonts

```console
WINEPREFIX=~/win32 winetricks corefonts
```

# Run Client

* CD into directory of your client.
  * ```console
    cd ~/rappelz_73`
    ```
* Launch the client

```console
WINEPREFIX=~/win32 wine SFrame.exe "/country:US" "/locale:windows-1252" "/notenc" "/auth_ip:127.0.0.1" "/auth_port:4601"
```

> **Note:** launch arguments must be wrapped individually as in the example above or they will be ignored!

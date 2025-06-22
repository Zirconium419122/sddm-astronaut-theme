# sddm-astronaut-theme

A theme for the [SDDM login manager](https://github.com/sddm/sddm) based on [`Sugar Dark for SDDM`](https://github.com/MarianArlt/sddm-sugar-dark).
Screen resolution: 1440p.

### Preview
![Preview](./Previews/preview.png)

### Dependencies

```sh
qt6-multimedia qt6-virtualkeyboard qt6-svg qt6 sddm
```

### Install NixOS

1. Change `sddm.package` to `pkgs.kdePackages.sddm`;

2. Add these packages to `services.displayManager.sddm.extraPackages`:

    ```nix
    kdePackages.qtsvg
    kdePackages.qtvirtualkeyboard
    kdePackages.qtmultimedia
    ```

3. Create a `sddm-theme.nix` file with these contents:

    ```nix
    { pkgs, ... }:

    pkgs.stdenv.mkDerivation {
      name = "sddm-theme";

      src = pkgs.fetchFromGitHub {
        owner = "Zirconium419122";
        repo = "sddm-astronaut-theme";
        rev = "500c3b55558c8d4d8628cad3029b53cad838edb6";
        hash = "sha256-AboJtc0e+1DBN3nwmsGtcNzqPLg0x7dI6xdc1AQZZIQ=";
      };

      installPhase = ''
        mkdir -p $out
        cp -R ./* $out/
      '';
    }
    ```

4. Add this line to `services.displayManager.sddm`:

    ```nix
    theme = "${import ../path/to/sddm-theme.nix { inherit pkgs; }}";
    ```

### Install non NixOS

1. Clone this repository, copy fonts to `/usr/share/fonts/`:

    ```sh
    sudo git clone https://github.com/keyitdev/sddm-astronaut-theme.git /usr/share/sddm/themes/sddm-astronaut-theme
    sudo cp /usr/share/sddm/themes/sddm-astronaut-theme/Fonts/* /usr/share/fonts/
    ```

2. Then edit `/etc/sddm.conf`, so that it looks like this:

    ```sh
    echo "[Theme]
    Current=sddm-astronaut-theme" | sudo tee /etc/sddm.conf
    ```

### Credits

Based on the theme [`Sugar Dark for SDDM`](https://github.com/MarianArlt/sddm-sugar-dark) by **MarianArlt**.

### License

Distributed under the [GPLv3+](https://www.gnu.org/licenses/gpl-3.0.html) License.

# theming-video

```nix
qt.enable = true;

# platform theme "gtk" or "gnome"
qt.platformTheme = "gtk";

# name of the qt theme
qt.style.name = "adwaita-dark";

# detected automatically:
# adwaita, adwaita-dark, adwaita-highcontrast,
# adwaita-highcontrastinverse, breeze,
# bb10bright, bb10dark, cde, cleanlooks,
# gtk2, motif, plastique

# package to use
qt.style.package = pkgs.adwaita-qt;

```
```nix
gtk.enable = true;

gtk.cursorTheme.package = pkgs.bibata-cursors;
gtk.cursorTheme.name = "Bibata-Modern-Ice";

gtk.theme.package = pkgs.adw-gtk3;
gtk.theme.name = "adw-gtk3";

gtk.iconTheme.package = gruvboxPlus;
gtk.iconTheme.name = "GruvboxPlus";
```
```nix
gtk.cursorTheme.package = pkgs.bibata-cursors;

# basically, same as above
home.file = {
  ".icons/bibata".source = "${pkgs.bibata-cursors}/share/icons/Bibata-Modern-Classic";
};

# both cases still need you to select theme name declaratively,
# or imperatively like on other distros
gtk.cursorTheme.name = "Bibata-Modern-Ice";
```
```nix
let
  gruvboxplus = import ./gruvbox-plus.nix { inherit pkgs; };
in
{
  gtk.enable = true;
  
  gtk.cursorTheme.package = pkgs.bibata-cursors;
  gtk.cursorTheme.name = "Bibata-Modern-Ice";
  
  gtk.theme.package = pkgs.adw-gtk3;
  gtk.theme.name = "adw-gtk3";
  
  gtk.iconTheme.package = gruvboxPlus;
  gtk.iconTheme.name = "GruvboxPlus";
}
```
```nix
{ pkgs }:

let
  imgLink = "https://YOURIMAGELINK/image.png";

  image = pkgs.fetchurl {
    url = imgLink;
    sha256 = "sha256-HrcYriKliK2QN02/2vFK/osFjTT1NamhGKik3tozGU0=";
  };
in
pkgs.stdenv.mkDerivation {
  name = "sddm-theme";
  src = pkgs.fetchFromGitHub {
    owner = "MarianArlt";
    repo = "sddm-sugar-dark";
    rev = "ceb2c455663429be03ba62d9f898c571650ef7fe";
    sha256 = "0153z1kylbhc9d12nxy9vpn0spxgrhgy36wy37pk6ysq7akaqlvy";
  };
  installPhase = ''
    mkdir -p $out
    cp -R ./* $out/
    cd $out/
    rm Background.jpg
    cp -r ${image} $out/Background.jpg
   '';
}
```
```nix
environment.systempackages = with pkgs; [
  libsforqt5.qt5.qtquickcontrols2   
  libsforqt5.qt5.qtgraphicaleffects
];
```

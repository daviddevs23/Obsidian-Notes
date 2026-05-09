Make sure you are in the directory of you current nix config then run:
``` bash
nix flake update
sudo nixos-rebuild switch --flake .#devStation
home-manager switch -b backup --flake .#david
nix-collect-garbage -d 
```
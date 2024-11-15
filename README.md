# Run

Ce dossier contient les images de sortie du programme. Voici quelques-unes d'entre elles :

1 : Affichage de la premiere image ![1](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/1.gif)<br>
2 : Affichage de la deuxieme image ![2](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/2.gif)<br>
3 : Affichage de la troisieme image ![3](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/3.gif)<br>
4 : Affichage de la quatrieme image ![4](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/4.gif)<br>
5 : Affichage de la cinquieme image ![5](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/5.gif)<br>
6 : Affichage de la sixieme image ![6](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/6.gif)<br>
7 : Affichage de la septieme image ![7](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/7.gif)<br>
8 : Affichage de la huitieme image ![8](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/8.gif)<br>
9 : Affichage de la neuvieme image ![9](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/9.gif)<br>
10 : Affichage de la dixieme image ![10](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/10.gif)<br>
11 : Affichage de la onzieme image ![11](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/11.gif)<br>
12 : Affichage de la douzieme image ![12](https://github.com/M-U-C-K-A/image-ft_lock/blob/main/12.gif)<br>

<style>
    img {
        width: 800px;
    }
</style>

```sh
#!/bin/bash
# Lancer ft_lock
ft_lock &

SCRIPT_DIR="$(dirname "$(realpath "$0")")"
LOCK_DIR="$SCRIPT_DIR/lock"
export PATH="$PATH:$LOCK_DIR/usr/bin"
export LD_LIBRARY_PATH="$LOCK_DIR/usr/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH"

FTLOCK_PID=$!
sleep 0.5

pkill -9 eog
random_number=$((RANDOM % 12 + 1))
image_url="https://raw.githubusercontent.com/M-U-C-K-A/image-ft_lock/main/$random_number.gif"
image_path="$SCRIPT_DIR/lock/image.gif"

wget -O "$image_path" "$image_url" || curl -o "$image_path" "$image_url"
eog -f "$image_path" &

while true; do
    xdotool key Control_L
    sleep 6
    read -r x y < <(xdotool getmouselocation --shell | grep -E 'X=|Y=' | cut -d'=' -f2)
    if (( x >= 10 || y >= 10 )); then
        kill $FTLOCK_PID
        rm -f "$image_path"
        exit 0
    fi
done
```


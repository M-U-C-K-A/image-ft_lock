# Run

Ce dossier contient les images de sortie du programme. Voici quelques-unes d'entre elles :

1 : Affichage de la premiere image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/1.gif" width="800"><br>
2 : Affichage de la deuxieme image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/2.gif" width="800"><br>
3 : Affichage de la troisieme image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/3.gif" width="800"><br>
4 : Affichage de la quatrieme image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/4.gif" width="800"><br>
5 : Affichage de la cinquieme image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/5.gif" width="800"><br>
6 : Affichage de la sixieme image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/6.gif" width="800"><br>
7 : Affichage de la septieme image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/7.gif" width="800"><br>
8 : Affichage de la huitieme image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/8.gif" width="800"><br>
9 : Affichage de la neuvieme image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/9.gif" width="800"><br>
10 : Affichage de la dixieme image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/10.gif" width="800"><br>
11 : Affichage de la onzieme image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/11.gif" width="800"><br>
12 : Affichage de la douzieme image  
<img src="https://github.com/M-U-C-K-A/image-ft_lock/blob/main/12.gif" width="800"><br>


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


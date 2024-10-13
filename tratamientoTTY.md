Para hacer el tratamiento de la tty cuando recibimos una reverse shell, tendremos que hacer lo siguiente:

Primero ejecutamos este comando:

```css
script /dev/null -c bash
```

Luego de eso, presionamos la tecla `ctrl` y la letra `Z` al mismo tiempo (ctrl+Z)

Esto pasará a segundo plano la shell y estaremos en la máquina donde la recibimos. Ahora ejecutamos lo siguiente:

```css
stty raw -echo; fg
```

Ahora se nos quedará como "colgado" y nos mostrará un mensaje parecido a este:

```css
stty raw -echo;fg
[1]  + continued  sudo nc -nlvp 443
```

En este mensaje escribiremos el siguiente comando:

```css
reset xterm
```

Ahora veremos la shell como tal y parece que ya está pero todavia nos falta ejecutar 3 comandos más. Primero, este:

```css
export TERM=xterm
```

Esto hará que la variable "TERM" se comporte como un terminal "xterm"

```css
export SHELL=bash
```

Esto hará que use "bash" como shell predeterminado

Finalmente:

```css
stty rows 36 cols 131
```

Esto va a ajustar las filas y columnas del terminal para que tenga el correcto tamaño (Para ver cual debes usar solo ejecuta `stty size` en tu terminal normal).
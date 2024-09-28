#### Este script en Bash se encarga de limpiar Docker. A pesar de que el script `auto_deploy.sh` de dockerlabs funciona correctamente, las máquinas pueden quedar en un estado de pausa, ocupando espacio innecesario. Con este script, podemos eliminar las imágenes y contenedores que no usamos o que se encuentran en ese estado.

# Uso:

El uso es bastante simple, solo hay que ejecutarlo de la siguiente manera:

```css
sudo ./Dockerlabs-clean
```

o

```css
sudo bash Dockerlabs-clean
```

el script iniciará y luego de limpiar los contenedores nos preguntará si queremos borrar las imágenes.
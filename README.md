Solo subo mis writeups de algunas maquinas de [DockerLabs](https://dockerlabs.es)



[Instagram](https://instagram.com/macim0_)

¿Como desplegar las maquinas?
 Primero descomprimimos el `.zip` con la maquina, para hacerlo solo debemos instalar zip y luego ejecutar el comando.

```css
sudo apt install zip
```

para descomprimir:

```css
unzip <maquina>.zip
```

Esto nos dejará *dos archivos*, `auto_deploy.sh` y la maquina como tal en un `.tar`. Una vez hecho eso solo ejecutamos:

```css
sudo bash auto_deploy.sh <maquina>.tar
```


para confirmar que esta desplegada:

```css
ping 172.17.0.2 #o la ip que nos den
```

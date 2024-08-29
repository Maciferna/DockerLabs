Solo subo mis writeups de algunas maquinas de [DockerLabs](https://dockerlabs.es)

¿Como desplegar las maquinas?

 Primero hay que descomprimir el `.zip` con la maquina, para hacerlo solo debemos instalar `zip` con apt y luego ejecutar el comando.

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


Para confirmar que esta desplegada:

```css
ping 172.17.0.2 #o la ip que nos den
```


[ElPingüinoDeMario](https://youtube.com/@ElPinguinoDeMario)
Mi [Instagram](https://instagram.com/macim0_)


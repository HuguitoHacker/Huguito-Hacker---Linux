# 🐧 Guía Completa de Comandos de Linux Terminal

<div align="center">

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Nivel](https://img.shields.io/badge/Nivel-Básico_a_Avanzado-green?style=for-the-badge)

**La guía más completa de comandos para Terminal de Linux**

[🚀 Inicio Rápido](#-inicio-rápido) • [📖 Índice](#-índice-de-comandos) • [⚠️ Comandos Peligrosos](#️-comandos-peligrosos) • [🆘 Troubleshooting](#-troubleshooting)

[![Estrellas](https://img.shields.io/github/stars/tuusuario/comandos-linux?style=social)](https://github.com/tuusuario/comandos-linux)
[![Contribuir](https://img.shields.io/badge/Contribuciones-Bienvenidas-brightgreen)](CONTRIBUTING.md)

</div>

---

## 🚀 Inicio Rápido

### ¿Nuevo en la terminal de Linux?

1. **Abre la Terminal**: Presiona `Ctrl + Alt + T` (Ubuntu/Debian)
2. **O desde el menú**: Busca "Terminal" en tus aplicaciones
3. **Como root**: Usa `sudo` antes del comando o `sudo su` para modo root

### 🎯 Los 5 Comandos Esenciales

```bash
su usuario
```

**Cambiar a root:**
```bash
su -
sudo su
```

---

## 9️⃣ Ver usuarios conectados

```bash
who
w
users
```

**Historial de logins:**
```bash
last
```

---

## 🔟 Configurar contraseña

**Cambiar tu propia contraseña:**
```bash
passwd
```

**Cambiar contraseña de otro usuario (como root):**
```bash
sudo passwd nombre_usuario
```

**Forzar cambio de contraseña en el próximo login:**
```bash
sudo passwd -e usuario
```

</details>

---

<details>
<summary><h1>📦 GESTIÓN DE PAQUETES</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Intermedio-orange)

## Debian/Ubuntu (APT)

### 1️⃣ Actualizar lista de paquetes

```bash
sudo apt update
```

### 2️⃣ Actualizar paquetes instalados

```bash
sudo apt upgrade
```

**Actualización completa (incluye remover paquetes si es necesario):**
```bash
sudo apt full-upgrade
```

### 3️⃣ Instalar paquete

```bash
sudo apt install nombre_paquete
```

**Múltiples paquetes:**
```bash
sudo apt install paquete1 paquete2 paquete3
```

### 4️⃣ Desinstalar paquete

```bash
sudo apt remove nombre_paquete
```

**Eliminar también archivos de configuración:**
```bash
sudo apt purge nombre_paquete
```

### 5️⃣ Buscar paquetes

```bash
apt search nombre
```

### 6️⃣ Ver información de un paquete

```bash
apt show nombre_paquete
```

### 7️⃣ Limpiar caché de paquetes

```bash
sudo apt clean
sudo apt autoclean
sudo apt autoremove
```

### 8️⃣ Ver paquetes instalados

```bash
apt list --installed
dpkg -l
```

---

## CentOS/RHEL (YUM/DNF)

### 1️⃣ Actualizar sistema

```bash
sudo yum update
# O en versiones nuevas
sudo dnf update
```

### 2️⃣ Instalar paquete

```bash
sudo yum install nombre_paquete
sudo dnf install nombre_paquete
```

### 3️⃣ Desinstalar paquete

```bash
sudo yum remove nombre_paquete
sudo dnf remove nombre_paquete
```

### 4️⃣ Buscar paquetes

```bash
yum search nombre
dnf search nombre
```

### 5️⃣ Limpiar caché

```bash
sudo yum clean all
sudo dnf clean all
```

---

## Arch Linux (Pacman)

### 1️⃣ Actualizar sistema

```bash
sudo pacman -Syu
```

### 2️⃣ Instalar paquete

```bash
sudo pacman -S nombre_paquete
```

### 3️⃣ Desinstalar paquete

```bash
sudo pacman -R nombre_paquete
```

**Con dependencias:**
```bash
sudo pacman -Rs nombre_paquete
```

### 4️⃣ Buscar paquetes

```bash
pacman -Ss nombre
```

### 5️⃣ Limpiar caché

```bash
sudo pacman -Sc
```

---

## Snap (Universal)

```bash
sudo snap install nombre_paquete
sudo snap remove nombre_paquete
sudo snap list
sudo snap refresh
```

---

## Flatpak (Universal)

```bash
flatpak install nombre_paquete
flatpak uninstall nombre_paquete
flatpak list
flatpak update
```

</details>

---

<details>
<summary><h1>🔧 MANTENIMIENTO Y REPARACIÓN</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Avanzado-red)
![Admin](https://img.shields.io/badge/Requiere-Root/Sudo-orange)

## 1️⃣ Verificar sistema de archivos (fsck)

**⚠️ SOLO ejecutar en particiones desmontadas**

```bash
sudo fsck /dev/sda1
```

**Reparación automática:**
```bash
sudo fsck -y /dev/sda1
```

**💡 Para verificar la partición raíz:**
Se debe hacer desde un Live USB o en modo de recuperación.

---

## 2️⃣ Ver logs del sistema

**Logs generales:**
```bash
sudo tail -f /var/log/syslog
```

**Con journalctl (systemd):**
```bash
journalctl -xe
journalctl -f              # En tiempo real
journalctl -b              # Desde el último boot
journalctl -u servicio     # De un servicio específico
```

**Logs de autenticación:**
```bash
sudo tail /var/log/auth.log
```

**Logs del kernel:**
```bash
dmesg
dmesg | grep -i error
```

---

## 3️⃣ Montar y desmontar particiones

**Ver particiones montadas:**
```bash
mount
df -h
```

**Montar partición:**
```bash
sudo mount /dev/sdb1 /mnt/usb
```

**Desmontar:**
```bash
sudo umount /mnt/usb
```

**Montar ISO:**
```bash
sudo mount -o loop imagen.iso /mnt/iso
```

**Montar automático en el boot:**
Editar `/etc/fstab`

---

## 4️⃣ Verificar uso de disco

**Espacio en disco:**
```bash
df -h
```

**Archivos grandes:**
```bash
du -h --max-depth=1 / | sort -hr | head -20
```

**Usar herramienta interactiva:**
```bash
ncdu /
```
(Instalar: `sudo apt install ncdu`)

---

## 5️⃣ Backup con rsync

**Sincronizar directorios:**
```bash
rsync -av /origen/ /destino/
```

**Con progreso:**
```bash
rsync -av --progress /origen/ /destino/
```

**Excluir archivos:**
```bash
rsync -av --exclude='*.tmp' /origen/ /destino/
```

**Backup incremental:**
```bash
rsync -av --delete /origen/ /destino/
```

**Backup a servidor remoto:**
```bash
rsync -av /origen/ usuario@servidor:/destino/
```

---

## 6️⃣ Clonar disco con dd

**⚠️ EXTREMADAMENTE PELIGROSO - Verificar dos veces**

```bash
sudo dd if=/dev/sda of=/dev/sdb bs=4M status=progress
```

**Crear imagen de disco:**
```bash
sudo dd if=/dev/sda of=disco.img bs=4M status=progress
```

**Restaurar desde imagen:**
```bash
sudo dd if=disco.img of=/dev/sda bs=4M status=progress
```

**🎯 Flags:**
- `if` = Input File (origen)
- `of` = Output File (destino)
- `bs` = Block Size (tamaño de bloque)
- `status=progress` = Mostrar progreso

---

## 7️⃣ Verificar memoria RAM

```bash
sudo memtest86+
```

O desde el menú de GRUB al iniciar.

---

## 8️⃣ Actualizar GRUB

```bash
sudo update-grub
```

**Reinstalar GRUB:**
```bash
sudo grub-install /dev/sda
sudo update-grub
```

---

## 9️⃣ Reparar paquetes rotos

**Debian/Ubuntu:**
```bash
sudo apt --fix-broken install
sudo dpkg --configure -a
```

---

## 🔟 Limpiar espacio en disco

**Limpiar caché de paquetes:**
```bash
sudo apt clean
sudo apt autoclean
sudo apt autoremove
```

**Limpiar journald logs:**
```bash
sudo journalctl --vacuum-time=7d
sudo journalctl --vacuum-size=100M
```

**Limpiar thumbnails:**
```bash
rm -rf ~/.cache/thumbnails/*
```

**Buscar archivos temporales:**
```bash
sudo find /tmp -type f -atime +7 -delete
```

</details>

---

<details>
<summary><h1>⚡ PROCESOS Y RENDIMIENTO</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Intermedio-orange)

## 1️⃣ Ver procesos activos

**Lista simple:**
```bash
ps aux
```

**Árbol de procesos:**
```bash
ps auxf
pstree
```

**Procesos de un usuario:**
```bash
ps -u usuario
```

**Buscar proceso específico:**
```bash
ps aux | grep nombre_proceso
```

---

## 2️⃣ Monitor en tiempo real

**Top (básico):**
```bash
top
```

**Htop (mejorado):**
```bash
htop
```

**Gtop (moderno con gráficos):**
```bash
gtop
```

**Atajo en top:**
- `k` = Kill proceso
- `r` = Renice (cambiar prioridad)
- `M` = Ordenar por memoria
- `P` = Ordenar por CPU
- `q` = Salir

---

## 3️⃣ Terminar procesos

**Por PID:**
```bash
kill 1234
```

**Forzar terminación:**
```bash
kill -9 1234
sudo kill -9 1234
```

**Por nombre:**
```bash
killall nombre_proceso
pkill nombre_proceso
```

**Matar todos los procesos de un usuario:**
```bash
sudo pkill -u usuario
```

**🎯 Señales comunes:**
- `15` o `TERM` = Terminación normal (default)
- `9` o `KILL` = Forzar terminación inmediata
- `1` o `HUP` = Recargar configuración
- `2` o `INT` = Interrupción (Ctrl+C)

---

## 4️⃣ Prioridad de procesos (nice)

**Ejecutar con prioridad baja:**
```bash
nice -n 19 comando
```

**Cambiar prioridad de proceso existente:**
```bash
renice -n 10 -p 1234
```

**Valores de nice:**
- `-20` = Mayor prioridad
- `0` = Prioridad normal
- `19` = Menor prioridad

---

## 5️⃣ Ejecutar en segundo plano

**Ejecutar en background:**
```bash
comando &
```

**Ver trabajos en background:**
```bash
jobs
```

**Traer a foreground:**
```bash
fg %1
```

**Enviar a background:**
```bash
bg %1
```

**Suspender proceso actual:**
Presiona `Ctrl + Z`

---

## 6️⃣ Mantener proceso después de cerrar terminal

**Con nohup:**
```bash
nohup comando &
```

**Con screen:**
```bash
screen -S sesion
# Ejecutar comandos
# Ctrl+A, D para detach
screen -r sesion    # Para volver
```

**Con tmux:**
```bash
tmux new -s sesion
# Ejecutar comandos
# Ctrl+B, D para detach
tmux attach -t sesion    # Para volver
```

---

## 7️⃣ Ver archivos abiertos

**Por proceso:**
```bash
lsof -p 1234
```

**Por archivo:**
```bash
lsof /ruta/archivo
```

**Por usuario:**
```bash
lsof -u usuario
```

**Por puerto:**
```bash
lsof -i :80
```

---

## 8️⃣ Estadísticas de CPU

**Por núcleo:**
```bash
mpstat -P ALL
```

**Uso general:**
```bash
vmstat 1
```

---

## 9️⃣ Uso de memoria detallado

```bash
free -h
cat /proc/meminfo
```

**Procesos por uso de memoria:**
```bash
ps aux --sort=-%mem | head
```

---

## 🔟 Benchmark del sistema

**CPU:**
```bash
sysbench cpu run
```

**Memoria:**
```bash
sysbench memory run
```

**Disco:**
```bash
hdparm -t /dev/sda
dd if=/dev/zero of=testfile bs=1G count=1 oflag=direct
```

</details>

---

<details>
<summary><h1>🔌 GESTIÓN DE DISCOS</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Avanzado-red)
![Admin](https://img.shields.io/badge/Requiere-Root/Sudo-orange)

## 1️⃣ Listar discos y particiones

```bash
lsblk
fdisk -l
parted -l
```

**Con detalles UUID:**
```bash
blkid
```

---

## 2️⃣ Particionar disco (fdisk)

**⚠️ CUIDADO: Puede borrar datos**

```bash
sudo fdisk /dev/sdb
```

**Comandos dentro de fdisk:**
- `m` = Ayuda
- `p` = Ver particiones
- `n` = Nueva partición
- `d` = Eliminar partición
- `t` = Cambiar tipo
- `w` = Guardar cambios y salir
- `q` = Salir sin guardar

---

## 3️⃣ Particionar con parted (GPT)

```bash
sudo parted /dev/sdb
```

**Comandos:**
```
print                                    # Ver particiones
mklabel gpt                              # Crear tabla GPT
mkpart primary ext4 0% 100%              # Crear partición
quit                                     # Salir
```

---

## 4️⃣ Formatear particiones

**ext4:**
```bash
sudo mkfs.ext4 /dev/sdb1
```

**NTFS:**
```bash
sudo mkfs.ntfs /dev/sdb1
```

**FAT32:**
```bash
sudo mkfs.vfat -F 32 /dev/sdb1
```

**XFS:**
```bash
sudo mkfs.xfs /dev/sdb1
```

---

## 5️⃣ Verificar salud del disco

**SMART status:**
```bash
sudo smartctl -a /dev/sda
```

**Test rápido:**
```bash
sudo smartctl -t short /dev/sda
```

**Ver resultados:**
```bash
sudo smartctl -l selftest /dev/sda
```

---

## 6️⃣ Montar partición automáticamente

**Editar /etc/fstab:**
```bash
sudo nano /etc/fstab
```

**Añadir línea:**
```
UUID=xxx-xxx  /mnt/disco  ext4  defaults  0  2
```

**Obtener UUID:**
```bash
sudo blkid /dev/sdb1
```

**Probar configuración:**
```bash
sudo mount -a
```

---

## 7️⃣ LVM (Logical Volume Manager)

**Ver volúmenes físicos:**
```bash
sudo pvdisplay
```

**Ver grupos de volúmenes:**
```bash
sudo vgdisplay
```

**Ver volúmenes lógicos:**
```bash
sudo lvdisplay
```

**Crear volumen físico:**
```bash
sudo pvcreate /dev/sdb1
```

**Crear grupo de volúmenes:**
```bash
sudo vgcreate mi_vg /dev/sdb1
```

**Crear volumen lógico:**
```bash
sudo lvcreate -L 10G -n mi_lv mi_vg
```

---

## 8️⃣ RAID por software

**Ver status:**
```bash
cat /proc/mdstat
sudo mdadm --detail /dev/md0
```

**Crear RAID 1:**
```bash
sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
```

---

## 9️⃣ Swap

**Crear archivo swap:**
```bash
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

**Hacer permanente (añadir a /etc/fstab):**
```
/swapfile none swap sw 0 0
```

**Ver swap:**
```bash
swapon --show
free -h
```

---

## 🔟 Borrado seguro

**⚠️ IRREVERSIBLE**

```bash
sudo shred -vfz -n 3 /dev/sdb
```

**Más rápido (un solo pase):**
```bash
sudo dd if=/dev/zero of=/dev/sdb bs=4M status=progress
```

</details>

---

<details>
<summary><h1>🔗 PIPES Y REDIRECCIONES</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Intermedio-orange)

## Operadores de redirección

### 1️⃣ Pipe (|) - Encadenar comandos

Envía la salida de un comando como entrada de otro.

```bash
comando1 | comando2
```

**📌 Ejemplos:**

**Buscar en resultados:**
```bash
ps aux | grep firefox
```

**Contar líneas:**
```bash
ls -l | wc -l
```

**Ordenar y mostrar únicos:**
```bash
cat archivo.txt | sort | uniq
```

**Top 10 archivos más grandes:**
```bash
du -h | sort -rh | head -10
```

---

### 2️⃣ Redirección de salida (>)

Guarda la salida en un archivo (sobrescribe).

```bash
comando > archivo.txt
```

**📌 Ejemplos:**
```bash
ls -l > listado.txt
echo "Hola" > saludo.txt
```

---

### 3️⃣ Append (>>)

Agrega al final del archivo sin sobrescribir.

```bash
comando >> archivo.txt
```

**📌 Ejemplo:**
```bash
echo "Nueva línea" >> archivo.txt
date >> log.txt
```

---

### 4️⃣ Redirección de entrada (<)

Usa un archivo como entrada del comando.

```bash
comando < archivo.txt
```

**📌 Ejemplo:**
```bash
sort < lista.txt
wc -l < archivo.txt
```

---

### 5️⃣ Redirección de errores (2>)

Redirige solo mensajes de error.

```bash
comando 2> errores.txt
```

**Descartar errores:**
```bash
comando 2> /dev/null
```

---

### 6️⃣ Redirigir todo (salida y errores)

```bash
comando &> todo.txt
comando > salida.txt 2>&1
```

---

### 7️⃣ Here Document (<<)

Permite múltiples líneas como entrada.

```bash
cat << EOF > archivo.txt
Línea 1
Línea 2
Línea 3
EOF
```

---

### 8️⃣ Tee - Salida dual

Muestra en pantalla Y guarda en archivo.

```bash
comando | tee archivo.txt
```

**Append:**
```bash
comando | tee -a archivo.txt
```

**📌 Ejemplo:**
```bash
ls -la | tee listado.txt
```

---

## Ejemplos combinados

**Log de instalación:**
```bash
sudo apt install paquete 2>&1 | tee install.log
```

**Buscar y guardar:**
```bash
find / -name "*.conf" 2>/dev/null > configs.txt
```

**Procesos consumiendo CPU:**
```bash
ps aux --sort=-%cpu | head -10 | tee top_cpu.txt
```

</details>

---

<details>
<summary><h1>📜 VARIABLES Y ENTORNO</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Intermedio-orange)

## 1️⃣ Ver variables de entorno

```bash
env
printenv
```

**Variable específica:**
```bash
echo $HOME
echo $USER
echo $PATH
```

---

## 2️⃣ Variables comunes

| Variable | Descripción | Ejemplo |
|----------|-------------|---------|
| `$HOME` | Directorio home | `/home/usuario` |
| `$USER` | Usuario actual | `usuario` |
| `$PATH` | Rutas de ejecutables | `/usr/bin:/bin:...` |
| `$PWD` | Directorio actual | `/home/usuario/Documentos` |
| `$SHELL` | Shell actual | `/bin/bash` |
| `$HOSTNAME` | Nombre del host | `mi-pc` |
| `$LANG` | Idioma del sistema | `es_ES.UTF-8` |
| `$EDITOR` | Editor predeterminado | `nano` o `vim` |

---

## 3️⃣ Crear variables temporales

**Para la sesión actual:**
```bash
MIVAR="Hola Mundo"
echo $MIVAR
```

**Exportar para subprocesos:**
```bash
export MIVAR="Hola Mundo"
```

---

## 4️⃣ Variables permanentes

**Para el usuario (bash):**
Editar `~/.bashrc`:
```bash
export JAVA_HOME=/usr/lib/jvm/java-11
export PATH=$PATH:$JAVA_HOME/bin
```

**Aplicar cambios:**
```bash
source ~/.bashrc
```

**Para todo el sistema:**
Editar `/etc/environment` o crear archivo en `/etc/profile.d/`

---

## 5️⃣ Modificar PATH

**Temporal:**
```bash
export PATH=$PATH:/nueva/ruta
```

**Permanente (~/.bashrc):**
```bash
echo 'export PATH=$PATH:/nueva/ruta' >> ~/.bashrc
source ~/.bashrc
```

---

## 6️⃣ Variables especiales en scripts

```bash
$0    # Nombre del script
$1    # Primer argumento
$2    # Segundo argumento
$#    # Número de argumentos
$@    # Todos los argumentos
$?    # Código de salida del último comando
$    # PID del script actual
```

**📌 Ejemplo de script:**
```bash
#!/bin/bash
echo "Script: $0"
echo "Primer argumento: $1"
echo "Todos los argumentos: $@"
echo "Número de argumentos: $#"
```

---

## 7️⃣ Eliminar variable

```bash
unset MIVAR
```

---

## 8️⃣ Verificar si variable existe

```bash
if [ -z "$MIVAR" ]; then
    echo "Variable vacía o no existe"
fi
```

</details>

---

<details>
<summary><h1>🔥 SERVICIOS Y SYSTEMD</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Avanzado-red)

## 1️⃣ Ver servicios activos

```bash
systemctl list-units --type=service
systemctl list-units --type=service --state=running
```

---

## 2️⃣ Gestionar servicios

**Ver status:**
```bash
systemctl status nombre_servicio
```

**Iniciar servicio:**
```bash
sudo systemctl start nombre_servicio
```

**Detener servicio:**
```bash
sudo systemctl stop nombre_servicio
```

**Reiniciar servicio:**
```bash
sudo systemctl restart nombre_servicio
```

**Recargar configuración (sin reiniciar):**
```bash
sudo systemctl reload nombre_servicio
```

---

## 3️⃣ Habilitar/Deshabilitar inicio automático

**Habilitar:**
```bash
sudo systemctl enable nombre_servicio
```

**Deshabilitar:**
```bash
sudo systemctl disable nombre_servicio
```

**Ver si está habilitado:**
```bash
systemctl is-enabled nombre_servicio
```

---

## 4️⃣ Ver logs de servicio

```bash
journalctl -u nombre_servicio
```

**En tiempo real:**
```bash
journalctl -u nombre_servicio -f
```

**Últimas 50 líneas:**
```bash
journalctl -u nombre_servicio -n 50
```

**Desde el último boot:**
```bash
journalctl -u nombre_servicio -b
```

---

## 5️⃣ Crear servicio personalizado

Crear `/etc/systemd/system/mi_servicio.service`:

```ini
[Unit]
Description=Mi Servicio Personalizado
After=network.target

[Service]
Type=simple
User=usuario
WorkingDirectory=/ruta/proyecto
ExecStart=/ruta/proyecto/script.sh
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

**Activar:**
```bash
sudo systemctl daemon-reload
sudo systemctl enable mi_servicio
sudo systemctl start mi_servicio
```

---

## 6️⃣ Targets (runlevels)

**Ver target actual:**
```bash
systemctl get-default
```

**Cambiar target:**
```bash
sudo systemctl set-default multi-user.target
```

**Targets comunes:**
- `graphical.target` = Modo gráfico
- `multi-user.target` = Modo consola
- `rescue.target` = Modo de rescate

---

## 7️⃣ Logs del sistema (journalctl)

**Ver todos los logs:**
```bash
journalctl
```

**Últimos logs:**
```bash
journalctl -n 100
```

**Desde cierta fecha:**
```bash
journalctl --since "2025-01-01"
journalctl --since "1 hour ago"
```

**Por prioridad:**
```bash
journalctl -p err
```

**Limpiar logs antiguos:**
```bash
sudo journalctl --vacuum-time=7d
sudo journalctl --vacuum-size=100M
```

</details>

---

<details>
<summary><h1>⚠️ COMANDOS PELIGROSOS</h1></summary>

![Peligro](https://img.shields.io/badge/⚠️-PELIGRO-red?style=for-the-badge)

## ☠️ Estos comandos pueden DESTRUIR tu sistema

### 1️⃣ rm -rf / - EL MÁS PELIGROSO

```bash
rm -rf /
sudo rm -rf /*
```

**🔥 PELIGRO EXTREMO:**
- Borra TODO el sistema de archivos
- Sin papelera ni recuperación
- Sistema completamente destruido

**⚠️ NUNCA ejecutes esto**

---

### 2️⃣ dd - Sobrescribir disco

```bash
dd if=/dev/zero of=/dev/sda
```

**🔥 PELIGRO:**
- Borra completamente un disco
- Irreversible
- Un error en `of=` puede destruir el disco equivocado

---

### 3️⃣ mkfs - Formatear partición

```bash
mkfs.ext4 /dev/sda
```

**🔥 PELIGRO:**
- Formatea y borra todo el contenido
- Sin confirmación
- Verificar dos veces el dispositivo

---

### 4️⃣ chmod 777 recursivo

```bash
chmod -R 777 /
```

**🔥 PELIGRO:**
- Rompe la seguridad del sistema
- Cualquiera puede modificar archivos críticos
- Sistema vulnerable

---

### 5️⃣ chown recursivo en /

```bash
chown -R usuario:grupo /
```

**🔥 PELIGRO:**
- Rompe permisos del sistema
- Servicios dejarán de funcionar
- Difícil de recuperar

---

### 6️⃣ Fork bomb

```bash
:(){ :|:& };:
```

**🔥 PELIGRO:**
- Crea procesos infinitos
- Congela el sistema
- Requiere reinicio forzado

---

### 7️⃣ Sobrescribir archivos críticos

```bash
> /etc/passwd
> /boot/vmlinuz
```

**🔥 PELIGRO:**
- Destruye archivos del sistema
- Sistema no arrancará
- Pérdida de usuarios

---

### 8️⃣ Comandos descargados de internet

```bash
curl http://sitio.com/script.sh | bash
wget -O - http://sitio.com/script | sh
```

**🔥 PELIGRO:**
- Puede ejecutar malware
- Sin revisión del código
- Acceso root completo

---

### 9️⃣ Eliminar kernel

```bash
sudo rm -rf /boot
sudo rm /vmlinuz
```

**🔥 PELIGRO:**
- Sistema no arrancará
- Requiere reinstalación

---

### 🔟 Scripts con sudo sin revisar

```bash
sudo bash script_desconocido.sh
```

**🔥 PELIGRO:**
- Acceso root completo
- Puede instalar backdoors
- Robar información

---

## 🛡️ Reglas de seguridad

✅ **SIEMPRE:**
- Lee el comando completo antes de ejecutar
- Verifica dispositivos (/dev/sdX) dos veces
- Haz backup antes de comandos destructivos
- Usa `--dry-run` si está disponible
- Prueba en máquina virtual primero
- Entiende qué hace cada parte del comando

❌ **NUNCA:**
- Ejecutes comandos que no entiendes
- Uses `rm -rf` con sudo sin estar 100% seguro
- Copies comandos de internet sin revisar
- Trabajes como root innecesariamente
- Desactives protecciones del sistema
- Ejecutes scripts descargados sin leer

## 📋 Checklist antes de comandos destructivos

- [ ] ¿He hecho backup?
- [ ] ¿Estoy en el directorio correcto?
- [ ] ¿Es el dispositivo correcto?
- [ ] ¿Entiendo completamente el comando?
- [ ] ¿Hay una forma más segura de hacerlo?

cd          # Navegar entre directorios
ls          # Listar archivos y carpetas
pwd         # Mostrar directorio actual
clear       # Limpiar la pantalla
man         # Manual de cualquier comando
```

---

## 📖 Índice de Comandos

### 🔰 Nivel Básico
- [📁 Navegación y Exploración](#-navegación-y-exploración) - `cd`, `ls`, `pwd`, `tree`
- [🗂️ Gestión de Archivos](#️-gestión-de-archivos-y-directorios) - `cp`, `mv`, `rm`, `touch`
- [🧹 Comandos de Utilidad](#-comandos-de-utilidad) - `clear`, `man`, `history`

### 🔶 Nivel Intermedio
- [🖥️ Información del Sistema](#️-información-del-sistema) - `uname`, `df`, `free`, `top`
- [🌐 Comandos de Red](#-comandos-de-red) - `ip`, `ping`, `netstat`, `ss`
- [👤 Usuarios y Permisos](#-usuarios-y-permisos) - `chmod`, `chown`, `useradd`
- [📦 Gestión de Paquetes](#-gestión-de-paquetes) - `apt`, `yum`, `dnf`, `pacman`

### 🔴 Nivel Avanzado
- [🔧 Mantenimiento y Reparación](#-mantenimiento-y-reparación) - `fsck`, `dd`, `mount`
- [⚡ Procesos y Rendimiento](#-procesos-y-rendimiento) - `ps`, `kill`, `htop`, `nice`
- [🔌 Gestión de Discos](#-gestión-de-discos) - `fdisk`, `lsblk`, `parted`
- [🔗 Pipes y Redirecciones](#-pipes-y-redirecciones) - `|`, `>`, `>>`, `2>`
- [📜 Variables y Entorno](#-variables-y-entorno) - `export`, `$PATH`, `env`
- [🔥 Servicios y Systemd](#-servicios-y-systemd) - `systemctl`, `journalctl`

---

## 🆚 Bash vs Otras Shells: Comparativa Rápida

| Acción | Bash | Zsh | Fish | Descripción |
|--------|------|-----|------|-------------|
| Listar archivos | `ls` | `ls` | `ls` | Ver contenido |
| Autocompletado | Tab | Tab mejorado | Tab inteligente | Completar comandos |
| Historial | `history` | `history` con búsqueda | Historial visual | Ver comandos anteriores |
| Configuración | `~/.bashrc` | `~/.zshrc` | `~/.config/fish/config.fish` | Archivo de config |
| Plugins | Manual | Oh-My-Zsh | Built-in | Sistema de plugins |
| Sintaxis | POSIX | Compatible | Propia | Lenguaje de scripting |

---

<details>
<summary><h1>📁 NAVEGACIÓN Y EXPLORACIÓN</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Básico-green)

## 1️⃣ Mostrar directorio actual

Muestra la ruta completa del directorio donde te encuentras (Print Working Directory).

```bash
pwd
```

**📌 Ejemplo de salida:**
```
/home/usuario/Documentos
```

---

## 2️⃣ Cambiar de directorio

Navega a un directorio específico.

```bash
cd ruta/del/directorio
```

**📌 Ejemplos:**
```bash
cd /home/usuario/Documentos
cd Descargas                    # Directorio relativo
cd ~/Documentos                 # ~ es tu carpeta home
cd ..                           # Subir un nivel
cd ../..                        # Subir dos niveles
cd -                            # Volver al directorio anterior
cd                              # Ir a tu home (~)
```

**💡 Tip:** Usa `cd` sin argumentos para volver a tu carpeta personal.

---

## 3️⃣ Listar archivos y directorios

Muestra el contenido del directorio actual.

```bash
ls
```

**🎯 Variantes más útiles:**

**Formato detallado:**
```bash
ls -l
```

**Incluir archivos ocultos:**
```bash
ls -a
```

**Todo junto (detallado + ocultos):**
```bash
ls -la
```

**Ordenar por fecha:**
```bash
ls -lt
```

**Tamaño legible:**
```bash
ls -lh
```

**Recursivo (subdirectorios):**
```bash
ls -R
```

**Colorear output:**
```bash
ls --color=auto
```

**📌 Combinación más usada:**
```bash
ls -lah
```
Muestra: permisos, propietario, tamaño legible, archivos ocultos.

**💡 Alias común en ~/.bashrc:**
```bash
alias ll='ls -lah'
```

---

## 4️⃣ Ver árbol de directorios

Muestra la estructura de directorios en formato árbol.

```bash
tree
```

**📌 Ejemplos útiles:**
```bash
tree -L 2              # Solo 2 niveles de profundidad
tree -d                # Solo directorios
tree -a                # Incluir archivos ocultos
tree -h                # Tamaño legible
tree -C                # Con colores
```

**⚠️ Instalación si no está disponible:**
```bash
# Ubuntu/Debian
sudo apt install tree

# CentOS/RHEL
sudo yum install tree

# Arch Linux
sudo pacman -S tree
```

---

## 5️⃣ Buscar archivos

**Buscar por nombre:**
```bash
find /ruta -name "archivo.txt"
```

**📌 Ejemplos prácticos:**

**Buscar archivos .log:**
```bash
find /var/log -name "*.log"
```

**Buscar sin case-sensitive:**
```bash
find . -iname "archivo.TXT"
```

**Buscar por tamaño (mayores a 100MB):**
```bash
find . -size +100M
```

**Buscar y ejecutar comando:**
```bash
find . -name "*.tmp" -exec rm {} \;
```

**Buscar archivos modificados hace menos de 7 días:**
```bash
find . -mtime -7
```

**💡 Alternativa más rápida - locate:**
```bash
locate archivo.txt
```
Primero actualiza la base de datos: `sudo updatedb`

---

## 6️⃣ Buscar comando en el historial

```bash
history | grep comando
```

**O usa Ctrl + R** para búsqueda interactiva.

---

## 7️⃣ Ver tipo de archivo

Determina el tipo de un archivo.

```bash
file nombre_archivo
```

**📌 Ejemplo:**
```bash
file documento.pdf
# Salida: documento.pdf: PDF document, version 1.4
```

---

## 8️⃣ Calcular tamaño de directorio

**Tamaño de un directorio:**
```bash
du -sh directorio
```

**📌 Opciones:**
- `-s` = Resumen total
- `-h` = Tamaño legible (KB, MB, GB)

**Ver tamaños de subdirectorios:**
```bash
du -h --max-depth=1
```

**Top 10 directorios más grandes:**
```bash
du -h | sort -rh | head -10
```

---

## 9️⃣ Espacio en disco

Ver espacio disponible en todas las particiones.

```bash
df -h
```

**💡 Más legible:**
```bash
df -h --output=source,size,used,avail,pcent,target
```

</details>

---

<details>
<summary><h1>🗂️ GESTIÓN DE ARCHIVOS Y DIRECTORIOS</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Básico-green)

## 1️⃣ Crear archivo vacío

```bash
touch archivo.txt
```

**📌 Crear múltiples archivos:**
```bash
touch archivo1.txt archivo2.txt archivo3.txt
```

**💡 También actualiza la fecha de modificación** de archivos existentes.

---

## 2️⃣ Crear directorio

```bash
mkdir nombre_directorio
```

**📌 Crear estructura anidada:**
```bash
mkdir -p proyecto/src/components
```
El flag `-p` crea todos los directorios padres necesarios.

**Crear múltiples directorios:**
```bash
mkdir dir1 dir2 dir3
```

---

## 3️⃣ Copiar archivos

```bash
cp origen destino
```

**📌 Ejemplos:**

**Copiar archivo:**
```bash
cp archivo.txt /home/usuario/Backup/
```

**Copiar con otro nombre:**
```bash
cp archivo.txt archivo_backup.txt
```

**Copiar directorio recursivamente:**
```bash
cp -r directorio/ /ruta/destino/
```

**Copiar preservando atributos:**
```bash
cp -a origen destino
```

**Copiar con confirmación:**
```bash
cp -i archivo.txt destino/
```

**🎯 Flags importantes:**
- `-r` = Recursivo (para directorios)
- `-i` = Interactivo (pide confirmación)
- `-v` = Verbose (muestra progreso)
- `-a` = Archive (preserva todo: permisos, timestamps, etc.)
- `-u` = Update (solo si es más nuevo)

---

## 4️⃣ Mover/Renombrar archivos

```bash
mv origen destino
```

**📌 Ejemplos:**

**Mover archivo:**
```bash
mv archivo.txt /home/usuario/Documentos/
```

**Renombrar archivo:**
```bash
mv archivo_viejo.txt archivo_nuevo.txt
```

**Mover múltiples archivos:**
```bash
mv *.txt /destino/
```

**Mover con confirmación:**
```bash
mv -i archivo.txt destino/
```

---

## 5️⃣ Eliminar archivos

```bash
rm archivo.txt
```

**⚠️ CUIDADO: No va a la papelera, se borra permanentemente**

**📌 Opciones:**

**Eliminar con confirmación:**
```bash
rm -i archivo.txt
```

**Eliminar directorio:**
```bash
rm -r directorio/
```

**Forzar eliminación:**
```bash
rm -f archivo.txt
```

**Eliminar directorio con contenido (SIN CONFIRMACIÓN):**
```bash
rm -rf directorio/
```

**💡 Alternativa más segura - mover a papelera:**
```bash
# Instalar trash-cli
sudo apt install trash-cli

# Usar
trash archivo.txt
trash-list
trash-restore
```

---

## 6️⃣ Ver contenido de archivos

**Ver archivo completo:**
```bash
cat archivo.txt
```

**Ver con paginación:**
```bash
less archivo.txt
```
(Usa flechas para navegar, `q` para salir)

**Ver primeras líneas:**
```bash
head archivo.txt
head -n 20 archivo.txt    # Primeras 20 líneas
```

**Ver últimas líneas:**
```bash
tail archivo.txt
tail -n 50 archivo.txt    # Últimas 50 líneas
```

**Ver en tiempo real (logs):**
```bash
tail -f /var/log/syslog
```

**Ver con números de línea:**
```bash
cat -n archivo.txt
```

---

## 7️⃣ Editar archivos

**Nano (fácil para principiantes):**
```bash
nano archivo.txt
```
Atajos: `Ctrl+O` guardar, `Ctrl+X` salir

**Vim (más potente):**
```bash
vim archivo.txt
```
Presiona `i` para insertar, `Esc` luego `:wq` para guardar y salir

**Gedit (interfaz gráfica):**
```bash
gedit archivo.txt &
```

---

## 8️⃣ Buscar texto dentro de archivos

```bash
grep "texto_a_buscar" archivo.txt
```

**📌 Ejemplos potentes:**

**Buscar en múltiples archivos:**
```bash
grep "error" *.log
```

**Buscar recursivamente en directorios:**
```bash
grep -r "TODO" /proyecto/
```

**Case-insensitive:**
```bash
grep -i "error" archivo.txt
```

**Mostrar número de línea:**
```bash
grep -n "error" archivo.txt
```

**Contar ocurrencias:**
```bash
grep -c "error" archivo.txt
```

**Invertir búsqueda (líneas que NO contienen):**
```bash
grep -v "debug" archivo.log
```

**Buscar palabras completas:**
```bash
grep -w "root" /etc/passwd
```

**Con contexto (líneas antes/después):**
```bash
grep -C 3 "error" archivo.log    # 3 líneas antes y después
```

---

## 9️⃣ Crear enlaces simbólicos

```bash
ln -s /ruta/origen /ruta/enlace
```

**📌 Ejemplo:**
```bash
ln -s /var/www/html/proyecto ~/proyecto
```

**💡 Uso:** Acceso rápido a carpetas o archivos sin duplicar.

---

## 🔟 Comprimir y descomprimir

**Crear archivo .tar.gz:**
```bash
tar -czf archivo.tar.gz directorio/
```

**Extraer .tar.gz:**
```bash
tar -xzf archivo.tar.gz
```

**Ver contenido sin extraer:**
```bash
tar -tzf archivo.tar.gz
```

**Extraer .zip:**
```bash
unzip archivo.zip
```

**Crear .zip:**
```bash
zip -r archivo.zip directorio/
```

**🎯 Flags de tar:**
- `c` = Create (crear)
- `x` = eXtract (extraer)
- `z` = gZip (comprimir con gzip)
- `f` = File (especificar archivo)
- `v` = Verbose (mostrar progreso)
- `t` = lisT (listar contenido)

**📌 Combinación completa con progreso:**
```bash
tar -czvf backup.tar.gz directorio/
```

---

## 1️⃣1️⃣ Comparar archivos

```bash
diff archivo1.txt archivo2.txt
```

**Más legible:**
```bash
diff -u archivo1.txt archivo2.txt
```

**Ignorar espacios:**
```bash
diff -w archivo1.txt archivo2.txt
```

---

## 1️⃣2️⃣ Cambiar permisos de archivos

Ver sección [👤 Usuarios y Permisos](#-usuarios-y-permisos)

</details>

---

<details>
<summary><h1>🖥️ INFORMACIÓN DEL SISTEMA</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Intermedio-orange)

## 1️⃣ Información del sistema operativo

```bash
uname -a
```

**📌 Opciones específicas:**
```bash
uname -s    # Nombre del kernel (Linux)
uname -r    # Versión del kernel
uname -m    # Arquitectura (x86_64, arm64, etc.)
```

**Información de la distribución:**
```bash
cat /etc/os-release
lsb_release -a
```

---

## 2️⃣ Información de hardware

**CPU:**
```bash
lscpu
cat /proc/cpuinfo
```

**Memoria RAM:**
```bash
free -h
cat /proc/meminfo
```

**Dispositivos PCI (tarjeta gráfica, etc.):**
```bash
lspci
lspci | grep VGA    # Solo tarjeta gráfica
```

**Dispositivos USB:**
```bash
lsusb
```

**Discos duros:**
```bash
lsblk
fdisk -l
```

**Todo el hardware (resumen):**
```bash
sudo lshw
sudo lshw -short    # Versión resumida
```

---

## 3️⃣ Uso de memoria

**Memoria RAM:**
```bash
free -h
```

**Memoria con actualización continua:**
```bash
watch -n 1 free -h
```

**Procesos que más memoria usan:**
```bash
ps aux --sort=-%mem | head -10
```

---

## 4️⃣ Uso de CPU

**Monitoreo en tiempo real:**
```bash
top
```

**Versión mejorada:**
```bash
htop
```
(Si no está: `sudo apt install htop`)

**Uso promedio de CPU:**
```bash
uptime
```

---

## 5️⃣ Temperatura del sistema

**Sensores (requiere instalación):**
```bash
sudo apt install lm-sensors
sudo sensors-detect
sensors
```

**GPU (NVIDIA):**
```bash
nvidia-smi
```

---

## 6️⃣ Información de red

```bash
ip addr show
ifconfig
```

**Hostname:**
```bash
hostname
```

**DNS actual:**
```bash
cat /etc/resolv.conf
```

---

## 7️⃣ Fecha y hora

```bash
date
```

**Hora del sistema:**
```bash
timedatectl
```

**Cambiar zona horaria:**
```bash
sudo timedatectl set-timezone America/Mexico_City
```

---

## 8️⃣ Uptime del sistema

Tiempo que lleva encendido el sistema.

```bash
uptime
```

---

## 9️⃣ Información de la batería (laptops)

```bash
upower -i /org/freedesktop/UPower/devices/battery_BAT0
```

**O más simple:**
```bash
cat /sys/class/power_supply/BAT0/capacity
```

---

## 🔟 Kernel y módulos cargados

**Versión del kernel:**
```bash
uname -r
```

**Módulos cargados:**
```bash
lsmod
```

**Información de un módulo:**
```bash
modinfo nombre_modulo
```

</details>

---

<details>
<summary><h1>🌐 COMANDOS DE RED</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Intermedio-orange)

## 1️⃣ Ver configuración de red

**Comando moderno:**
```bash
ip addr show
ip a
```

**Comando tradicional:**
```bash
ifconfig
```

**Solo IPv4:**
```bash
ip -4 addr
```

**Solo una interfaz:**
```bash
ip addr show eth0
```

---

## 2️⃣ Ver tabla de enrutamiento

```bash
ip route show
route -n
```

---

## 3️⃣ Ping - Verificar conectividad

```bash
ping google.com
```

**📌 Opciones útiles:**

**Número limitado de pings:**
```bash
ping -c 4 google.com
```

**Ping con timestamp:**
```bash
ping -D google.com
```

**Ping solo IPv4:**
```bash
ping -4 google.com
```

**Ping solo IPv6:**
```bash
ping6 google.com
```

---

## 4️⃣ Traceroute - Rastrear ruta

```bash
traceroute google.com
```

**Alternativa más rápida:**
```bash
mtr google.com
```
(Combina ping y traceroute)

---

## 5️⃣ Ver conexiones activas

**Comando moderno:**
```bash
ss -tuln
```

**Comando tradicional:**
```bash
netstat -tuln
```

**📌 Flags:**
- `-t` = TCP
- `-u` = UDP  
- `-l` = Listening (puertos en escucha)
- `-n` = Numérico (no resolver nombres)
- `-p` = Program (mostrar programa)

**Ver todas las conexiones:**
```bash
ss -tupan
```

**Ver qué está usando un puerto:**
```bash
sudo ss -tlnp | grep :80
sudo lsof -i :80
```

---

## 6️⃣ DNS Lookup

**Resolver nombre a IP:**
```bash
nslookup google.com
dig google.com
host google.com
```

**Dig con más detalles:**
```bash
dig google.com +short
dig google.com ANY
```

**Reverse DNS (IP a nombre):**
```bash
dig -x 8.8.8.8
```

---

## 7️⃣ Descargar archivos

**wget:**
```bash
wget https://ejemplo.com/archivo.zip
```

**curl:**
```bash
curl -O https://ejemplo.com/archivo.zip
```

**Con barra de progreso:**
```bash
wget --progress=bar https://ejemplo.com/archivo.zip
```

**Continuar descarga interrumpida:**
```bash
wget -c https://ejemplo.com/archivo.zip
```

---

## 8️⃣ Configurar IP estática

**Temporal (hasta reiniciar):**
```bash
sudo ip addr add 192.168.1.100/24 dev eth0
sudo ip route add default via 192.168.1.1
```

**Permanente (Ubuntu):**
Edita `/etc/netplan/01-netcfg.yaml`

---

## 9️⃣ Activar/Desactivar interfaz de red

```bash
sudo ip link set eth0 down
sudo ip link set eth0 up
```

**O con ifconfig:**
```bash
sudo ifconfig eth0 down
sudo ifconfig eth0 up
```

---

## 🔟 Ver estadísticas de red

```bash
ifstat
iftop
nethogs
```

**Instalar si no están disponibles:**
```bash
sudo apt install ifstat iftop nethogs
```

---

## 1️⃣1️⃣ Flush DNS cache

**systemd-resolved:**
```bash
sudo systemd-resolve --flush-caches
```

**nscd:**
```bash
sudo /etc/init.d/nscd restart
```

---

## 1️⃣2️⃣ Firewall (UFW)

**Ver estado:**
```bash
sudo ufw status
```

**Habilitar:**
```bash
sudo ufw enable
```

**Permitir puerto:**
```bash
sudo ufw allow 80
sudo ufw allow 22/tcp
```

**Denegar puerto:**
```bash
sudo ufw deny 23
```

**Ver reglas numeradas:**
```bash
sudo ufw status numbered
```

**Eliminar regla:**
```bash
sudo ufw delete 2
```

---

## 1️⃣3️⃣ SSH

**Conectar a servidor remoto:**
```bash
ssh usuario@servidor.com
ssh usuario@192.168.1.100
```

**Con puerto específico:**
```bash
ssh -p 2222 usuario@servidor.com
```

**Copiar archivos (SCP):**
```bash
scp archivo.txt usuario@servidor:/ruta/destino/
scp usuario@servidor:/ruta/archivo.txt ./
```

**Copiar directorios:**
```bash
scp -r directorio/ usuario@servidor:/ruta/
```

**SFTP (transferencia interactiva):**
```bash
sftp usuario@servidor.com
```

---

## 1️⃣4️⃣ Ver hostname

```bash
hostname
```

**Cambiar hostname:**
```bash
sudo hostnamectl set-hostname nuevo-nombre
```

</details>

---

<details>
<summary><h1>👤 USUARIOS Y PERMISOS</h1></summary>

![Nivel](https://img.shields.io/badge/Nivel-Intermedio-orange)

## 1️⃣ Ver usuario actual

```bash
whoami
```

**Con más detalles:**
```bash
id
```

---

## 2️⃣ Cambiar permisos (chmod)

**Sintaxis numérica:**
```bash
chmod 755 archivo.sh
chmod 644 documento.txt
```

**📊 Tabla de permisos:**

| Número | Permisos | Descripción |
|--------|----------|-------------|
| 7 | rwx | Leer, escribir, ejecutar |
| 6 | rw- | Leer, escribir |
| 5 | r-x | Leer, ejecutar |
| 4 | r-- | Solo leer |
| 3 | -wx | Escribir, ejecutar |
| 2 | -w- | Solo escribir |
| 1 | --x | Solo ejecutar |
| 0 | --- | Sin permisos |

**Formato:** `[dueño][grupo][otros]`

**📌 Ejemplos comunes:**
```bash
chmod 755 script.sh     # rwxr-xr-x (ejecutable para todos)
chmod 644 archivo.txt   # rw-r--r-- (común para archivos)
chmod 600 clave.pem     # rw------- (solo dueño lee/escribe)
chmod 777 archivo       # rwxrwxrwx (todos los permisos - NO RECOMENDADO)
```

**Sintaxis simbólica:**
```bash
chmod +x script.sh          # Agregar ejecución
chmod u+x script.sh         # Ejecutable solo para usuario
chmod g-w archivo.txt       # Quitar escritura al grupo
chmod o-r archivo.txt       # Quitar lectura a otros
chmod a+r archivo.txt       # Lectura para todos
```

**Recursivo:**
```bash
chmod -R 755 directorio/
```

---

## 3️⃣ Cambiar propietario (chown)

```bash
sudo chown usuario archivo.txt
```

**Cambiar usuario y grupo:**
```bash
sudo chown usuario:grupo archivo.txt
```

**Recursivo:**
```bash
sudo chown -R usuario:grupo directorio/
```

**Solo cambiar grupo:**
```bash
sudo chgrp grupo archivo.txt
```

---

## 4️⃣ Ver permisos detallados

```bash
ls -l archivo.txt
```

**Ejemplo de salida:**
```
-rw-r--r-- 1 usuario grupo 1234 Oct 22 10:30 archivo.txt
```

**Explicación:**
- `-` = Tipo (- archivo, d directorio, l link)
- `rw-` = Permisos del dueño
- `r--` = Permisos del grupo
- `r--` = Permisos de otros
- `usuario` = Propietario
- `grupo` = Grupo
- `1234` = Tamaño en bytes

---

## 5️⃣ Gestión de usuarios

**Crear usuario:**
```bash
sudo useradd nombre_usuario
sudo useradd -m -s /bin/bash nombre_usuario    # Con home y shell
```

**Crear con contraseña:**
```bash
sudo useradd -m nombre_usuario
sudo passwd nombre_usuario
```

**Eliminar usuario:**
```bash
sudo userdel nombre_usuario
sudo userdel -r nombre_usuario    # También elimina su home
```

**Modificar usuario:**
```bash
sudo usermod -aG sudo nombre_usuario    # Agregar a grupo sudo
sudo usermod -s /bin/zsh usuario        # Cambiar shell
```

**Ver todos los usuarios:**
```bash
cat /etc/passwd
```

---

## 6️⃣ Gestión de grupos

**Crear grupo:**
```bash
sudo groupadd nombre_grupo
```

**Agregar usuario a grupo:**
```bash
sudo usermod -aG nombre_grupo usuario
```

**Ver grupos de un usuario:**
```bash
groups usuario
```

**Ver todos los grupos:**
```bash
cat /etc/group
```

---

## 7️⃣ Sudo - Ejecutar como root

**Ejecutar comando con privilegios:**
```bash
sudo comando
```

**Ejecutar múltiples comandos como root:**
```bash
sudo su
```

**Ejecutar como otro usuario:**
```bash
sudo -u otro_usuario comando
```

**Editar archivo con permisos de root:**
```bash
sudo nano /etc/archivo
```

**Ver permisos sudo:**
```bash
sudo -l
```

---

## 8️⃣ Cambiar de usuario

**Cambiar a otro usuario:**
```bash

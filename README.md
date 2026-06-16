# alpine-installer

## Examples

If you're also using Raspberry Pi 5 'Network Boot' like me, don't forget to:
1. Add the following lines to your dnsmasq config  
   If you're using Pi-hole as your DHCP server, look for `misc.dnsmasq_lines` under Settings -> All settings -> Miscellaneous (https://<PIHOLE_IP>/admin/settings/all)  
   Otherwise, just add a /etc/dnsmasq.d/99-pxe.conf file
  ```
  enable-tftp
  tftp-root=/srv/tftpboot
  pxe-service=0,"Raspberry Pi Boot"
  ```
2. Fire up a http file server, feel free to change the port, but don't forget to change it in the cmdline too
```sh
python3 -m http.server 8888 --directory /srv/tftpboot/
```
3. Make sure all the needed files are available under /srv/tftpboot/  
  **EXAMPLE**
  ```sh
  root@pihole:/srv/tftpboot/a8aa4364# ls -lah /srv/tftpboot/a8aa4364/
  total 4.5M
  drwxr-xr-x 5 root root   41 Jun 15 18:49 .
  drwxr-xr-x 4 root root    4 Jun 15 16:36 ..
  drwxr-xr-x 3 root root    4 Jun 15 16:36 apks
  -rw-r--r-- 1 root root   81 Jun 15 17:19 authorized_keys
  -rwxr-xr-x 1 root root  32K Jun 15 16:36 bcm2710-rpi-2-b.dtb
  -rwxr-xr-x 1 root root  34K Jun 15 16:36 bcm2710-rpi-3-b.dtb
  -rwxr-xr-x 1 root root  35K Jun 15 16:36 bcm2710-rpi-3-b-plus.dtb
  -rwxr-xr-x 1 root root  33K Jun 15 16:36 bcm2710-rpi-cm0.dtb
  -rwxr-xr-x 1 root root  32K Jun 15 16:36 bcm2710-rpi-cm3.dtb
  -rwxr-xr-x 1 root root  33K Jun 15 16:36 bcm2710-rpi-zero-2.dtb
  -rwxr-xr-x 1 root root  33K Jun 15 16:36 bcm2710-rpi-zero-2-w.dtb
  -rwxr-xr-x 1 root root  56K Jun 15 16:36 bcm2711-rpi-400.dtb
  -rwxr-xr-x 1 root root  56K Jun 15 16:36 bcm2711-rpi-4-b.dtb
  -rwxr-xr-x 1 root root  56K Jun 15 16:36 bcm2711-rpi-cm4.dtb
  -rwxr-xr-x 1 root root  39K Jun 15 16:36 bcm2711-rpi-cm4-io.dtb
  -rwxr-xr-x 1 root root  53K Jun 15 16:36 bcm2711-rpi-cm4s.dtb
  -rwxr-xr-x 1 root root  77K Jun 15 16:36 bcm2712d0-rpi-5-b.dtb
  -rwxr-xr-x 1 root root  77K Jun 15 16:36 bcm2712-d-rpi-5-b.dtb
  -rwxr-xr-x 1 root root  77K Jun 15 16:36 bcm2712-rpi-500.dtb
  -rwxr-xr-x 1 root root  77K Jun 15 16:36 bcm2712-rpi-5-b.dtb
  -rwxr-xr-x 1 root root  78K Jun 15 16:36 bcm2712-rpi-cm5-cm4io.dtb
  -rwxr-xr-x 1 root root  78K Jun 15 16:36 bcm2712-rpi-cm5-cm5io.dtb
  -rwxr-xr-x 1 root root  78K Jun 15 16:36 bcm2712-rpi-cm5l-cm4io.dtb
  -rwxr-xr-x 1 root root  78K Jun 15 16:36 bcm2712-rpi-cm5l-cm5io.dtb
  -rwxr-xr-x 1 root root  21K Jun 15 16:36 bcm2837-rpi-2-b.dtb
  -rwxr-xr-x 1 root root  21K Jun 15 16:36 bcm2837-rpi-3-a-plus.dtb
  -rwxr-xr-x 1 root root  22K Jun 15 16:36 bcm2837-rpi-3-b.dtb
  -rwxr-xr-x 1 root root  22K Jun 15 16:36 bcm2837-rpi-3-b-plus.dtb
  -rwxr-xr-x 1 root root  21K Jun 15 16:36 bcm2837-rpi-cm3-io3.dtb
  -rwxr-xr-x 1 root root  21K Jun 15 16:36 bcm2837-rpi-zero-2-w.dtb
  drwxr-xr-x 2 root root   12 Jun 15 16:46 boot
  -rwxr-xr-x 1 root root  52K Jun 15 16:36 bootcode.bin
  -rwxr-xr-x 1 root root  225 Jun 15 17:19 cmdline.txt
  -rwxr-xr-x 1 root root  264 Jun 15 16:36 config.txt
  -rwxr-xr-x 1 root root 5.4K Jun 15 16:36 fixup4.dat
  -rwxr-xr-x 1 root root 7.2K Jun 15 16:36 fixup.dat
  drwxr-xr-x 2 root root  374 Jun 15 16:36 overlays
  -rwxr-xr-x 1 root root  126 Jun 15 17:11 setup.sh
  -rwxr-xr-x 1 root root 2.2M Jun 15 16:36 start4.elf
  -rwxr-xr-x 1 root root 2.9M Jun 15 16:36 start.elf
  -rw-r--r-- 1 root root    0 Jun 15 16:37 usercfg.txt

  root@pihole:/srv/tftpboot/a8aa4364# ls -lah /srv/tftpboot/a8aa4364/boot/
  total 142M
  drwxr-xr-x 2 root root   12 Jun 15 16:46 .
  drwxr-xr-x 5 root root   41 Jun 15 18:49 ..
  -rw-r--r-- 1 root root 249K Jun 15 16:46 config-6.18.35-0-rpi
  -rwxr-xr-x 1 root root 249K Jun 15 16:36 config-6.18.35-0-rpi~
  -rw-r--r-- 1 root root 6.3M Jun 15 16:45 initramfs-rpi
  -rwxr-xr-x 1 root root 6.7M Jun 15 16:36 initramfs-rpi~
  -rw-r--r-- 1 root root  49M Jun 15 16:46 modloop-rpi
  -rwxr-xr-x 1 root root  49M Jun 15 16:36 modloop-rpi~
  -rw-r--r-- 1 root root 4.4M Jun 15 16:45 System.map-6.18.35-0-rpi
  -rwxr-xr-x 1 root root 4.4M Jun 15 16:36 System.map-6.18.35-0-rpi~
  -rw-r--r-- 1 root root  23M Jun 15 16:45 vmlinuz-rpi
  -rwxr-xr-x 1 root root  23M Jun 15 16:36 vmlinuz-rpi~
  ```
4. Make sure your cmdline.txt is correct
```
modules=loop,squashfs quiet console=tty1 ip=dhcp alpine_repo=http://dl-cdn.alpinelinux.org/alpine/edge/main modloop=http://192.168.15.4:8888/a8aa4364/boot/modloop-rpi ssh_key=http://192.168.15.4:8888/a8aa4364/authorized_keys
```
5. Turn your Raspberry Pi 5 on, press Space, press 2, wait

Use the `install` playbook:
```sh
ansible-playbook -i hosts.yaml install.yaml
```

Run the `configure` playbook + ask for the `become_password` (`-K`):
```sh
ansible-playbook -K -i hosts.yaml configure.yaml
```

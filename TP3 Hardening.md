# Part I : A bit of exploration

Commençons par un peu d'exploration manuelle des pseudo-filesystems que sont `/proc` et `/sys`.

## Sommaire

- [Part I : A bit of exploration](#part-i--a-bit-of-exploration)
  - [Sommaire](#sommaire)
  - [1. /proc](#1-proc)
  - [2. /sys](#2-sys)

## 1. /proc

🌞 **Afficher...** :

- l'état complet de la mémoire (RAM)
```
[ju@efrei-xmg4agau1 proc]$ cat meminfo
MemTotal:         468976 kB
MemFree:          240856 kB
MemAvailable:     336256 kB
Buffers:            2708 kB
Cached:            82540 kB
SwapCached:            0 kB
Active:           121460 kB
Inactive:          16952 kB
Active(anon):      53100 kB
Inactive(anon):     2092 kB
Active(file):      68360 kB
Inactive(file):    14860 kB
Unevictable:           0 kB
Mlocked:               0 kB
SwapTotal:        839676 kB
SwapFree:         839676 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:                 0 kB
Writeback:             0 kB
AnonPages:         53192 kB
Mapped:            39508 kB
Shmem:              2028 kB
KReclaimable:      24200 kB
Slab:              51888 kB
SReclaimable:      24200 kB
SUnreclaim:        27688 kB
KernelStack:        1712 kB
PageTables:         1448 kB
SecPageTables:         0 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     1074164 kB
Committed_AS:     185020 kB
VmallocTotal:   34359738367 kB
VmallocUsed:       21292 kB
VmallocChunk:          0 kB
Percpu:              372 kB
HardwareCorrupted:     0 kB
AnonHugePages:         0 kB
ShmemHugePages:        0 kB
ShmemPmdMapped:        0 kB
FileHugePages:         0 kB
FilePmdMapped:         0 kB
CmaTotal:              0 kB
CmaFree:               0 kB
Unaccepted:            0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
Hugetlb:               0 kB
DirectMap4k:       83904 kB
DirectMap2M:      440320 kB
```
- le nombre de coeurs que votre CPU a (uniquement ce nombre)
```
[ju@efrei-xmg4agau1 proc]$ cat cpuinfo
...
cpu cores       : 1
```
- le nombre de processus lancés (uniquement ce nombre)
```
[ju@efrei-xmg4agau1 proc]$ ls /proc | grep -E '^[0-9]+$' | wc -l
102
```
- la ligne de commande utilisée pour lancer le kernel actuel
```
[ju@efrei-xmg4agau1 proc]$ cat cmdline
BOOT_IMAGE=(hd0,msdos1)/vmlinuz-5.14.0-427.13.1.el9_4.x86_64 root=/dev/mapper/rl-root ro crashkernel=1G-4G:192M,4G-64G:256M,64G-:512M resume=/dev/mapper/rl-swap rd.lvm.lv=rl/root rd.lvm.lv=rl/swap
```
- la liste des connexions TCP actuelles (même si c'est un peu imbuvable avec nos p'tits yeux)
```
[ju@efrei-xmg4agau1 proc]$ cat net/tcp
  sl  local_address rem_address   st tx_queue rx_queue tr tm->when retrnsmt   uid  timeout inode
   0: 00000000:0016 00000000:0000 0A 00000000:00000000 00:00000000 00000000     0        0 19934 1 0000000000000000 100 0 0 10 0
   1: 1738A8C0:0016 0138A8C0:E142 01 00000000:00000000 02:0007B563 00000000     0        0 20800 3 0000000000000000 24 6 23 10 -1
```
- la valeur actuelle de la *swappiness* (cf le tip ci-dessous)
```
[ju@efrei-xmg4agau1 proc]$ cat sys/vm/swappiness
60
```

## 2. /sys



🌞 **Afficher...** :

- la liste des périphériques de types bloc reconnus par l'OS (genre les disques durs par exemple koa)
```
[ju@efrei-xmg4agau1 block]$ ls
dm-0  dm-1  sda
```
- la liste des modules kernel qui sont actuellement en cours d'utilisation
```
[ju@efrei-xmg4agau1 sys]$ ls module
8250              firmware_class       nf_reject_ipv4   shpchp
acpi              fuse                 nf_reject_ipv6   spurious
acpiphp           ghash_clmulni_intel  nf_tables        srcutree
ahci              gpiolib_acpi         nft_chain_nat    suspend
ata_generic       haltpoll             nft_ct           syscopyarea
ata_piix          hid                  nft_fib          sysfillrect
battery           hid_magicmouse       nft_fib_inet     sysimgblt
blk_cgroup        hid_ntrig            nft_fib_ipv4     sysrq
block             i2c_piix4            nft_fib_ipv6     t10_pi
button            i8042                nft_reject       tcp_cubic
clocksource       ima                  nft_reject_inet  thermal
configfs          intel_idle           nmi_backtrace    thunderbolt
cpufreq           intel_pmc_core       page_alloc       tls
cpuidle           intel_powerclamp     page_reporting   tpm
cpuidle_haltpoll  intel_rapl_common    pcie_aspm        tpm_crb
crc32c_intel      intel_rapl_msr       pciehp           tpm_tis
crc32_pclmul      intel_vsec           pci_hotplug      tpm_tis_core
crc64_rocksoft    ip_set               pcmcia_core      ttm
crc_t10dif        ipv6                 pcspkr           udmabuf
crct10dif_pclmul  kdb                  pmt_class        uhci_hcd
cryptomgr         kernel               pmt_telemetry    usbcore
damon_reclaim     keyboard             printk           usbhid
debug_core        kfence               processor        uv_nmi
device_hmem       kgdboc               psmouse          video
dm_log            kgdbts               pstore           virtio_pci
dm_mirror         libahci              random           virtio_pci_legacy_dev
dm_mod            libata               rapl             virtio_pci_modern_dev
dm_region_hash    libcrc32c            rcupdate         vmd
drm               md_mod               rcutree          vmwgfx
drm_kms_helper    memory_hotplug       rfkill           vt
drm_ttm_helper    module               rng_core         watchdog
dynamic_debug     mousedev             rtc_cmos         wmi
e1000             msr                  scsi_dh_alua     workqueue
edac_core         netpoll              scsi_dh_rdac     xen
efi_pstore        nf_conntrack         scsi_mod         xfs
efivars           nf_defrag_ipv4       sd_mod           xhci_hcd
ehci_hcd          nf_defrag_ipv6       secretmem        xz_dec
fb                nf_nat               serio_raw        zswap
fb_sys_fops       nfnetlink            sg
```
- la liste des cartes réseau
```
[ju@efrei-xmg4agau1 class]$ ls net
enp0s3  enp0s8  lo
```
# Part II. Gotta get chrooty


Il est là depuis si longtemps le frérot, ça marche toujours aussi bien, mais c'est vrai qu'il paraît limité pour les standards d'isolation d'aujourd'hui.


Le principe de `chroot` c'est de changer l'emplacement de la racine du disque pour un processus donné.

Genre on fait croire à un programme que son dossier `/` c'est genre `/toto/super_chroot/`. Comme ça quand il fait `ls /`, il l'ignore, mais en réalité, il liste le contenu du dossier `/toto/super_chroot/`.


## Sommaire

- [Part II. Gotta get chrooty](#part-ii-gotta-get-chrooty)
  - [Sommaire](#sommaire)
  - [1. Play manually](#1-play-manually)
  - [2. SSH old friend](#2-ssh-old-friend)

## 1. Play manually

🌞 **Créez le dossier `/srv/get_chrooted/`**
```
[ju@efrei-xmg4agau1 ~]$ mkdir srv
[ju@efrei-xmg4agau1 ~]$ cd srv
[ju@efrei-xmg4agau1 srv]$ mkdir get_chrooted
[ju@efrei-xmg4agau1 srv]$ cd get_chrooted/
[ju@efrei-xmg4agau1 get_chrooted]$
```

🌞 **Essayez de `chroot` à l'intérieur en lançant un shell**

- possible que ça fonctionne pas immédiatement car y'a pas de shells dans votre `chroot` :d
- déplacez le nécessaire dans `/srv/get_chrooted/` pour pouvoir lancé un shell `chroot`é à l'intérieur
```
mkdir -p /home/ju/srv/get_chrooted/{bin,lib64,dev,proc}
sudo cp -v /bin/bash /home/ju/srv/get_chrooted/bin/
sudo cp -v /bin/sh /home/ju/srv/get_chrooted/bin/
sudo cp -v /lib64/libtinfo.so.6 /home/ju/srv/get_chrooted/lib64/
sudo cp -v /lib64/libc.so.6 /home/ju/srv/get_chrooted/lib64/
sudo cp -v /lib64/ld-linux-x86-64.so.2 /home/ju/srv/get_chrooted/lib64/
mkdir -p /home/ju/srv/get_chrooted/dev /home/ju/srv/get_chrooted/proc
sudo mount --bind /dev /home/ju/srv/get_chrooted/dev
sudo mount --bind /proc /home/ju/srv/get_chrooted/proc
sudo chroot /home/ju/srv/get_chrooted/ /bin/bash

```
## 2. SSH old friend

Keskivien foutr là tu vas me dire. OpenSSH, ce bro, comme d'hab, va nous faire le café.

On peut indiquer dans la conf OpenSSH qu'un nouvel utilisateur doit être automatiquement `chroot`é dans un dossier donné quand il se connecte.

🌞 **Créez un user `imsad`**
```
[ju@efrei-xmg4agau1 get_chrooted]$ sudo useradd imsad
[ju@efrei-xmg4agau1 get_chrooted]$
```

🌞 **Modifier la configuration du serveur SSH**

- uniquement quand le user `imsad` se connecte en SSH :
  - il est `chroot`é dans `/srv/get_chrooted/`
  - son shell doit fonctionner normalement
  - il se connecte avec une clé SSH
  - il ne doit pas pouvoir remarquer qu'il est `chroot`é dans un dossier particulier
- dans le compte-rendu :
  - montrez une connexion SSH fonctionnelle sur le user `imsad`
```
C:\Users\jjelsch>ssh imsad@192.168.56.23
imsad@192.168.56.23's password:
Last login: Tue Feb 25 15:16:16 2025 from 192.168.56.1
-bash-5.1$
```
  - prouvez que le `bash` ouvert est bien `chroot`
```

```

  
  
# Part III : CGroup

➜ **Les *CGroup* c'est un mécanisme du noyau Linux pour faire des groupes de processus et restreindre leur accès aux ressources de la machine.**

On parle ici notamment de restreindre l'accès à :

- la mémoire (par exemple : on définit une quantité de mémoire maximum que le groupe de processus aura le droit d'utiliser)
- le CPU (par exemple : on définit un poids pour qu'un groupe de processus soit prioritaire)
- écriture/lecture (par exemple : limitation des écritures sur le disque)
- d'autres trucs, c'pour vous donner une idée

➜ **Les *CGroup* permettent aussi de monitorer en temps réel l'accès aux ressources d'un groupe de processus.**

Vous pouvez constater ça avec les commandes `systemd-cgls` et `systemd-cgtop` notamment.

![Cgroups](./img/cgroup.jpg)

> C'est dessiné par **[Julia Evans](https://jvns.ca/)**, elle a fait plein de ptites illustrations tech de ce genre, je recommande :D

## Sommaire

- [Part III : CGroup](#part-iii--cgroup)
  - [Sommaire](#sommaire)
  - [1. Explore](#1-explore)
  - [2. Do it](#2-do-it)
  - [3. systemd](#3-systemd)
    - [A. One-shot](#a-one-shot)
    - [B. Real service](#b-real-service)

## 1. Explore

Pour rappel : la configuration actuelle des *CGroups* est dispo dans `/sys/fs/cgroup`.

🌞 **Afficher...** :

- la liste des controllers *CGroups* dispos sur le système
```
[ju@efrei-xmg4agau1 cgroup]$ cat cgroup.controllers
cpuset cpu io memory hugetlb pids rdma misc
```
- la quantité de mémoire max que vous êtes autorisés à utiliser dans votre session utilisateur
  - par défaut, sous Rocky, le *controller* memory n'est pas activé : normal si vous ne voyez aucun fichier `memory.max`
  - si c'est le cas, ça veut dire qu'aucune restriction RAM est en place (vous devez justement constater ça)
```
[ju@efrei-xmg4agau1 cgroup]$ cat user.slice/memory.max
max
```
- les noms de tous les *CGroups* créés
  - ce sont tous les sous-dossiers de `/sys/fs/cgroup`
  - il devrait y avoir au moins les slices et scopes de systemd, on en parle plus bas
```
[ju@efrei-xmg4agau1 cgroup]$ ls
cgroup.controllers      cpuset.mems.effective  misc.capacity
cgroup.max.depth        cpu.stat               misc.current
cgroup.max.descendants  dev-hugepages.mount    sys-fs-fuse-connections.mount
cgroup.procs            dev-mqueue.mount       sys-kernel-config.mount
cgroup.stat             init.scope             sys-kernel-debug.mount
cgroup.subtree_control  io.stat                sys-kernel-tracing.mount
cgroup.threads          memory.numa_stat       system.slice
cpuset.cpus.effective   memory.reclaim         user.slice
cpuset.cpus.isolated    memory.stat
```

## 2. Do it

🌞 **Créer un nouveau *CGroup*** :

- appelez-le `meow`
```
[ju@efrei-xmg4agau1 cgroup]$ ls
cgroup.controllers      cpuset.mems.effective  meow
cgroup.max.depth        cpu.stat               misc.capacity
cgroup.max.descendants  dev-hugepages.mount    misc.current
cgroup.procs            dev-mqueue.mount       sys-fs-fuse-connections.mount
cgroup.stat             init.scope             sys-kernel-config.mount
cgroup.subtree_control  io.stat                sys-kernel-debug.mount
cgroup.threads          memory.numa_stat       sys-kernel-tracing.mount
cpuset.cpus.effective   memory.reclaim         system.slice
cpuset.cpus.isolated    memory.stat            user.slice
```
- activez les controllers `cpu` `cpuset` et `memory` s'ils ne le sont pas déjà
```
[ju@efrei-xmg4agau1 cgroup]$ cat /sys/fs/cgroup/cgroup.controllers
cpuset cpu io memory hugetlb pids rdma misc
```

> Vous devez donc créer le dossier `/sys/fs/cgroup/meow/` avec un simple `mkdir`, puis interagir avec les fichiers qui s'y trouvent (le dossier a été automatiquement populé). Pour supprimer un CGroup, utilisez `rmdir` (pas `rm -rf` qui va essayer de supprimer le contenu, ce qui n'a pas de sens, car ce ne sont pas des fichiers).

🌞 **Créer un nouveau sous-CGroup** :

- appelez-le `task1`
- on parle de créer le dossier `/sys/fs/cgroup/meow/task1/` 
- prouvez que les controllers activés sur `meow` ont bien été hérités
```
[ju@efrei-xmg4agau1 meow]$ sudo mkdir task1
[ju@efrei-xmg4agau1 meow]$ cat /sys/fs/cgroup/meow/task1/cgroup.controllers
cpuset cpu memory
```

🌞 **Mettez en place une limitation RAM**

- définissez une limite de 150M de RAM pour ce CGroup `task1`
```
[ju@efrei-xmg4agau1 cgroup]$ cat /sys/fs/cgroup/meow/task1/memory.max
157286400
```
> Il sera nécessaire d'ajouter le controller `memory` au CGroup `task1`. **Pour que ce CGroup `task1` puisse avoir le controller `memory` actif, il faut que son CGroup-parent l'ait aussi, et qu'ils puisse le faire hériter.** C'est le fichier **`cgroup.subtree_control`** qui est utilisé pour faire hériter des CGroup aux CGroups enfants, vous devez donc notamment interagir avec le fichier `/sys/fs/cgroup/cgroup.subtree_control` pour que tous les groupes enfant puissent en hériter.

🌞 **Prouvez que la limite est effective**

1. utilisez la commande `stress-ng` pour remplir la mémoire de la machine
2. constatez que la RAM est pleine
3. ajoutez votre shell `bash` actuel au *CGroup* `task1`
4. utilisez de nouveau `stress-ng`
5. constatez que le processus `stress-ng` est tué en boucle dès qu'il remplit la RAM au delà de la limite
```
very 0.1s: ps -eo cmd,pid,rss | grep stress        efrei-xmg4agau1.etudiants.campus.villejuif: Thu Feb 27 12:11:13 2025
stress-ng --vm 1 --vm-bytes   15510  4608
stress-ng --vm 1 --vm-bytes   15511  1724
stress-ng --vm 1 --vm-bytes   38135 153344
grep stress                   38147  2176
```

> On rappelle que tout processus lancé par un processus existant se retrouvera par défaut dans le même *CGroup* que son parent. C'est pour ça que vous ajoutez votre shell `bash` au *CGroup* : tout ce que vous exécuterez depuis ce `bash` sera exécuté dans le même *CGroup* que lui. Ha et le truc qui tue votre processus quand il prendre trop de RAM, c'est le [**OOM-killer**](https://en.wikipedia.org/wiki/Out_of_memory).

🌞 **Créer un nouveau sous-*CGroup*** :

- appelez-le `task2`

🌞 **Appliquer des restrictions CPU** :

- utilisez la mécanique de `cpu.weight` pour définir des priorités différentes à `task1` et `task2`
- utilisez `stress-ng` ou un bon vieux `cat /dev/random` pour lancer un processus CPU-intensive, et pour prouver que la restriction est en place
- pour tester, vous devez :
  - lancer deux shells en même temps
  - ajouter le premier au *CGroup* `task1`
  - ajouter le deuxième au *CGroup* `task2`
  - dans les deux shells, lancer un processus CPU-intensive
  - constatez avec un `htop` par exemple que les deux processus ne se répartissent pas équitablement la puissance du CPU

## 3. systemd

Par défaut, sous Linux, y'a systemd (ouais encore lui). Il utilise pas mal les *CGroup* nativement. Il fait naturellement deux trucs :

- **il met les `service` dans des `slice`s**
  - créer un `slice` systemd, c'est juste créer un cgroup (dont le nom se terminera par `.slice`)
  - tous les `service`s sont forcément dans un `slice`
- **il met des programmes lancés à l'extérieur (genre des trucs qui sont pas des `services`) dans des `scope`**
  - c'est pareil : un `scope` c'est juste un CGroup créé automatiquement par systemd, dont le nom se termine par `.scope`
  - ça permet à systemd de gérer certains processus même si c'est pas lui qui les lance
  - par exemple quand t'ouvres une session SSH n_n

Bref, l'un des rôles principaux de systemd c'est lancer et gérer des processus (services). Il est donc tout naturel qu'il utilise les *CGroups* Linux pour mener à bien ce job.

### A. One-shot

Y'a une commande rigolote et parfois pratique qui permet de jouer avec tout ça. Une commande qui permet de créer un service système temporaire à la volée en une seule ligne de commande : `systemd-run`.

> Pour plusieurs tests dans le TP, on se servira du serveur Web embarqué par Python. Il se lance en une seule commande, fait des trucs sur le système (serveur web, donc il lit des fichiers, fait des connexions réseau), c'est parfait pour faire des tests ! Pour le lancer : `python -m http.server 8888`.

🌞 **Lancer un serveur Web Python sous forme de service temporaire**

- avec la commande `python -m http.server <PORT>`
- n'oubliez pas d'ouvrir ce port dans le firewall pour tester
- il faudra le lancer avec la commande `systemd-run` pour en faire un service temporaire
- affichez le `status` du service pour prouver qu'il run


```bash
# lancer un sleep sous la forme d'un service nommé meow_test.service
sudo systemd-run -u meow_test sleep 9999
```

🌞 **Appliquer à la volée des restrictions**

- avec l'option `-p` de `systemd-run` vous pouvez préciser des paramètres pour le service
- utilisez le paramètre `MemoryMax` pour mettre en place une limite à 234M
```
[ju@efrei-xmg4agau1 ~]$ sudo systemd-run -u python_web --property=MemoryMax=234M python3 -m http.server 68
[ju@efrei-xmg4agau1 ~]$ cat /sys/fs/cgroup/system.slice/python_web.service/memory.max
245366784
```

> En vrai, `systemd-run` est un tool vraiment pratique pour limiter l'accès aux ressources d'un process qu'on lance oneshot.

🌞 **Restrictions *CGroup* ?**

- prouvez que la restriction à 234M de `systemd-run` est mise en place avec les *CGroups* Linux
```
[ju@efrei-xmg4agau1 ~]$ cat /sys/fs/cgroup/system.slice/python_web.service/memory.current
9539584
```
> Les montants de RAM chelous c'pour vous permettre de faire des `grep` pour trouver facilement. Attention par contre, les restrictions automatiques appliquées par systemd sont exprimées en octets (pas KB ni MB) donc faut faire une ptite multiplication pour le trouver facilement. En l'occurence, un `grep -nri $(( 234 * 1024 * 1024 ))` depuis `/sys/fs/cgroup` fera le taff ;)

### B. Real service

🌞 **Créez un service `web.service`**

- habitués nan ? Faut créer un fichier dans `/etc/systemd/system/`
- n'oubliez pas de `sudo systemctl daemon-reload` à chaque modification
- ce service doit lancer un serveur web python sur le port 9999/tcp


🌞 **Restriction *CGroup***

- modifier le fichier `web.service` pour inclure des limitations mises en place par des CGroups :
  - mémoire max : 321M
  - limitation d'écriture disque : 1M
  - limitation de lecture disque : 1M
  - limitation CPU : 50% d'utilisation

🌞 **Prouvez que ces restrictions ont été mises en place avec les *CGroups***

- en explorant le dossier `/sys/` toujours !

```
[ju@efrei-xmg4agau1 sys]$ cat /sys/fs/cgroup/system.slice/web.service/memory.max
336592896
[ju@efrei-xmg4agau1 sys]$ watch -n 1 cat /sys/fs/cgroup/system.slice/web.service/memory.current
[ju@efrei-xmg4agau1 sys]$ cat /sys/fs/cgroup/system.slice/web.service/cpu.max
50000 100000
[ju@efrei-xmg4agau1 sys]$ cat /sys/fs/cgroup/system.slice/web.service/io.max
8:0 rbps=1000000 wbps=1000000 riops=max wiops=max
[ju@efrei-xmg4agau1 sys]$
```
# Part IV : Linux Namespaces

> Le terme *namespace* est utilisé dans plein plein de contextes différents en informatique. Ici, on parle des *namespaces* du noyau Linux (qui n'a rien à votre avec les *namespaces* Java ou Kubernetes ou autres.)

➜ **Les Linux namespaces permettent d'isoler les processus les uns des autres, en leur proposant une vue limitée et restreinte de l'OS.**

Ici on parle pas de l'accès aux ressources (matérielles) de la machine comme avec les CGroups, mais plutôt de l'accès aux features de l'OS.

➜ **Les namespaces isolent notamment les processus en terme de** (liste non-exhaustive) :

- **PID** : les processus voient qu'une partie des autres processus qui s'exécutent
- **network** : les processus ne voient pas toutes les cartes réseau du système
- **user** : les processus n'ont pas les même users (pas les même fichiers `/etc/passwd` et `/etc/shadow` par exemple)
- **mount** : les processus ne voient pas les même partitions et points de montage que les autres

> On peut choisir d'isoler un processus uniquement en terme de network ou uniquement en terme de PID, ou tout à la fois, y'a pas de contraintes à ce niveau là.

![container](./img/container.png)

## Sommaire

- [Part IV : Linux Namespaces](#part-iv--linux-namespaces)
  - [Sommaire](#sommaire)
  - [1. Explore](#1-explore)
  - [2. Create](#2-create)
    - [A. net](#a-net)
    - [B. pid](#b-pid)
  - [3. AND MY CONTAINERS](#3-and-my-containers)
    - [A. Quick install](#a-quick-install)
    - [B. A simple container](#b-a-simple-container)
    - [C. CGroup](#c-cgroup)

## 1. Explore

🌞 **Utiliser /proc**

- déterminer les *namespaces* de votre `bash` actuel
- déterminer les *namespaces* du processuis qui porte l'identifiant PID 1
- ils devraient être identiques
```
[ju@vbox ~]$ ls -l /proc/$$/ns
total 0
lrwxrwxrwx. 1 ju ju 0 Mar  9 19:45 cgroup -> 'cgroup:[4026531835]'
lrwxrwxrwx. 1 ju ju 0 Mar  9 19:45 ipc -> 'ipc:[4026531839]'
lrwxrwxrwx. 1 ju ju 0 Mar  9 19:45 mnt -> 'mnt:[4026531841]'
lrwxrwxrwx. 1 ju ju 0 Mar  9 19:45 net -> 'net:[4026531840]'
lrwxrwxrwx. 1 ju ju 0 Mar  9 19:45 pid -> 'pid:[4026531836]'
lrwxrwxrwx. 1 ju ju 0 Mar  9 19:45 pid_for_children -> 'pid:[4026531836]'
lrwxrwxrwx. 1 ju ju 0 Mar  9 19:45 time -> 'time:[4026531834]'
lrwxrwxrwx. 1 ju ju 0 Mar  9 19:45 time_for_children -> 'time:[4026531834]'
lrwxrwxrwx. 1 ju ju 0 Mar  9 19:45 user -> 'user:[4026531837]'
lrwxrwxrwx. 1 ju ju 0 Mar  9 19:45 uts -> 'uts:[4026531838]'
```
```
[ju@vbox ~]$ sudo ls -l /proc/1/ns
total 0
lrwxrwxrwx. 1 root root 0 Mar  9 19:39 cgroup -> 'cgroup:[4026531835]'
lrwxrwxrwx. 1 root root 0 Mar  9 19:48 ipc -> 'ipc:[4026531839]'
lrwxrwxrwx. 1 root root 0 Mar  9 19:48 mnt -> 'mnt:[4026531841]'
lrwxrwxrwx. 1 root root 0 Mar  9 19:48 net -> 'net:[4026531840]'
lrwxrwxrwx. 1 root root 0 Mar  9 19:48 pid -> 'pid:[4026531836]'
lrwxrwxrwx. 1 root root 0 Mar  9 19:48 pid_for_children -> 'pid:[4026531836]'
lrwxrwxrwx. 1 root root 0 Mar  9 19:48 time -> 'time:[4026531834]'
lrwxrwxrwx. 1 root root 0 Mar  9 19:48 time_for_children -> 'time:[4026531834]'
lrwxrwxrwx. 1 root root 0 Mar  9 19:48 user -> 'user:[4026531837]'
lrwxrwxrwx. 1 root root 0 Mar  9 19:48 uts -> 'uts:[4026531838]'
```

🌞 **Lister tous les *namespaces* en cours d'utilisation**

- avec une simple commande `lsns`
```
[ju@vbox ~]$ lsns
        NS TYPE   NPROCS   PID USER COMMAND
4026531834 time        4  1241 ju   /usr/lib/systemd/systemd --user
4026531835 cgroup      4  1241 ju   /usr/lib/systemd/systemd --user
4026531836 pid         4  1241 ju   /usr/lib/systemd/systemd --user
4026531837 user        4  1241 ju   /usr/lib/systemd/systemd --user
4026531838 uts         4  1241 ju   /usr/lib/systemd/systemd --user
4026531839 ipc         4  1241 ju   /usr/lib/systemd/systemd --user
4026531840 net         4  1241 ju   /usr/lib/systemd/systemd --user
4026531841 mnt         4  1241 ju   /usr/lib/systemd/systemd --user
```

## 2. Create

### A. net

🌞 **Créer un nouveau *namespace* `network`**

- avec une commande `unshare`
- lancez un `bash` à l'intérieur
```
[ju@vbox ~]$ sudo unshare --net bash
[root@vbox ju]# ip a
1: lo: <LOOPBACK> mtu 65536 qdisc noop state DOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
[root@vbox ju]# lsns | grep net
4026531840 net       110     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 31
4026532163 net         3  1314 root   bash
```

> `unshare` est aussi le nom de l'appel système (syscall) qui permet de demander au kernel de créer un *namespace*. Ainsi, cette commande, c'est vraiment juste appeler ce syscall depuis la ligne de commande.

🌞 **Prouvez que votre nouveau *namespace* est bien là**

- déjà un `ip a` devrait montrer aucune des cartes réseau depuis l'intérieur du *namespace*
- et on peut `lsns` pour voir ce nouveau *namespace*
- et on peut voir avec un `ls -al` dans `/proc` que ce nouveau terminal est dans un autre *namespace* `network`
```
[root@vbox ju]# lsns
        NS TYPE   NPROCS   PID USER   COMMAND
4026531834 time      112     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 31
4026531835 cgroup    112     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 31
4026531836 pid       112     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 31
4026531837 user      112     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 31
4026531838 uts       109     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 31
4026531839 ipc       112     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 31
4026531840 net       110     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 31
4026531841 mnt       102     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 31
4026531862 mnt         1    29 root   kdevtmpfs
4026532119 mnt         1   585 root   /usr/lib/systemd/systemd-udevd
4026532120 uts         1   585 root   /usr/lib/systemd/systemd-udevd
4026532155 mnt         1   653 root   /sbin/auditd
4026532156 mnt         2   674 dbus   /usr/bin/dbus-broker-launch --scope system --audit
4026532157 mnt         1   683 chrony /usr/sbin/chronyd -F 2
4026532158 uts         1   683 chrony /usr/sbin/chronyd -F 2
4026532159 mnt         1   679 root   /usr/sbin/irqbalance --foreground
4026532160 mnt         1   684 root   /usr/lib/systemd/systemd-logind
4026532161 uts         1   684 root   /usr/lib/systemd/systemd-logind
4026532162 mnt         1   688 root   /usr/sbin/NetworkManager --no-daemon
4026532163 net         2  1314 root   bash
4026532240 mnt         1   785 root   /usr/sbin/rsyslogd -n
```
```
[root@vbox ju]# ls -al
total 28
drwx------. 5 ju   ju     142 Feb 27 13:00 .
drwxr-xr-x. 5 root root    40 Feb 25 13:48 ..
-rw-------. 1 ju   ju   10581 Feb 27 13:14 .bash_history
-rw-r--r--. 1 ju   ju      18 Apr 30  2024 .bash_logout
-rw-r--r--. 1 ju   ju     141 Apr 30  2024 .bash_profile
-rw-r--r--. 1 ju   ju     492 Apr 30  2024 .bashrc
drwx------. 3 ju   ju      20 Feb 27 13:00 .config
drwxr-xr-x. 2 ju   ju      23 Feb  6 18:21 Downloads
-rw-------. 1 ju   ju      40 Feb 27 12:51 .lesshst
drwxr-xr-x. 3 ju   ju      26 Feb 25 13:29 srv
```
### B. pid

🌞 **Créer un nouveau *namespace* `pid`**

- avec une commande `unshare`
- lancez un `bash` à l'intérieur
```
[ju@vbox ~]$ sudo unshare --pid --fork bash
```

🌞 **Prouvez que votre nouveau *namespace* est bien là**

- déjà un `ps -ef` devrait pas montrer grand chose
- et on peut `lsns` pour voir ce nouveau *namespace*
- et on peut voir avec un `ls -al` dans `/proc` que ce nouveau terminal est dans un autre *namespace* `pid`
```
[root@vbox proc]# lsns | grep pid
4026531836 pid       112     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 31
4026532163 pid         3  1370 root   bash
```
```
[root@vbox proc]# ls -al
total 0
drwxr-xr-x. 2 ju ju  6 Feb 25 13:35 .
drwxr-xr-x. 6 ju ju 73 Feb 25 13:45 ..
```
## 3. AND MY CONTAINERS

Oèoè les conteneurs les conteneurs, ils arrivent ils arrivent.

Un outil comme Docker repose **complètement** sur les *namespaces* et les *CGroups* pour lancer des processus de façon isolée sur la machine.

> Maintenant vous comprenez pourquoi j'me vénère quand on me dit que c'est des ptites VMs (genre non, mais alors pas du tout). Aussi pourquoi le conteneur est "isolé" du reste du système. Aussiiiiiiii pourquoi Docker est une techno fondamentalement Linux : Linux *namespaces* + Linux *CGroups* bois&gyals.

### A. Quick install

🌞 **Installer Docker sur la machine**

- suivez les instructions de la doc officielle spécifique pour notre OS !
- une fois installé, ajoutez votre user au groupe docker : `sudo usermod -aG docker $(whoami)`
- et démarrez le service docker ! `sudo systemctl enable --now docker
```
[ju@vbox ~]$ sudo systemctl status docker
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: disabled)
     Active: active (running) since Sun 2025-03-09 20:06:43 CET; 23s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 2295 (dockerd)
      Tasks: 9
     Memory: 25.9M
        CPU: 155ms
     CGroup: /system.slice/docker.service
             └─2295 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Mar 09 20:06:42 vbox dockerd[2295]: time="2025-03-09T20:06:42.241098643+01:00" level=info msg="OTEL tracing is not configured, using no-op tracer provider"
Mar 09 20:06:42 vbox dockerd[2295]: time="2025-03-09T20:06:42.280346993+01:00" level=info msg="Loading containers: start."
Mar 09 20:06:42 vbox dockerd[2295]: time="2025-03-09T20:06:42.306420303+01:00" level=info msg="Firewalld: created docker-forwarding policy"
Mar 09 20:06:43 vbox dockerd[2295]: time="2025-03-09T20:06:43.364754288+01:00" level=info msg="Loading containers: done."
Mar 09 20:06:43 vbox dockerd[2295]: time="2025-03-09T20:06:43.382813097+01:00" level=info msg="Docker daemon" commit=bbd0a17 containerd-snapshotter=false storage-driver=overlay2 version=28.0.1
Mar 09 20:06:43 vbox dockerd[2295]: time="2025-03-09T20:06:43.383091714+01:00" level=info msg="Initializing buildkit"
Mar 09 20:06:43 vbox dockerd[2295]: time="2025-03-09T20:06:43.414792781+01:00" level=info msg="Completed buildkit initialization"
Mar 09 20:06:43 vbox dockerd[2295]: time="2025-03-09T20:06:43.423792188+01:00" level=info msg="Daemon has completed initialization"
Mar 09 20:06:43 vbox dockerd[2295]: time="2025-03-09T20:06:43.423887418+01:00" level=info msg="API listen on /run/docker.sock"
Mar 09 20:06:43 vbox systemd[1]: Started Docker Application Container Engine.
```
### B. A simple container

🌞 **Lancer un simple conteneur qui sleep**

- utilisez la commande suivante :

```bash
docker run -d debian sleep 9999
```
```
[ju@vbox ~]$ sudo docker run -d debian sleep 9999
7e2b0a46cf1a59e4929402c7d306194458d498c2c3920a5470f02cc89e4b9802
```

🌞 **Avez les commandes de votre choix, avec le plus de détails possible, prouvez-que :**

- ce processus `sleep` est bien lancé sur votre machine, par votre utilisateur courant
- ce processus `sleep` est isolé à l'aide de *namespaces*
- un *CGroup* a été attribué à ce conteneur
- tout nouveau processus "dans" le conteneur est lui aussi isolé (voir ci-dessous pour lancer d'autres process dans le conteneur)

```bash
# pour obtenir un shell dans un conteneur existant
docker exec -it <conteneur> bash
# par exemple, si le conteneur est nommé "toto"
docker exec -it toto bash

# depuis là, vous pouvez lancez des nouveaux programmes
apt update -y
## procps contient la commande ps
## iproute2 contient la commande ip
## iputils-ping contient la commande ping
apt install -h procps iproute2 iputils-ping
```
```
[ju@vbox proc]$ docker inspect --format '{{.State.Pid}}' kind_dubinsky
2630
```
```
[ju@vbox proc]$ sudo ls -l /proc/2630/ns
total 0
lrwxrwxrwx. 1 root root 0 Mar  9 20:35 cgroup -> 'cgroup:[4026532253]'
lrwxrwxrwx. 1 root root 0 Mar  9 20:35 ipc -> 'ipc:[4026532251]'
lrwxrwxrwx. 1 root root 0 Mar  9 20:12 mnt -> 'mnt:[4026532249]'
lrwxrwxrwx. 1 root root 0 Mar  9 20:12 net -> 'net:[4026532254]'
lrwxrwxrwx. 1 root root 0 Mar  9 20:35 pid -> 'pid:[4026532252]'
lrwxrwxrwx. 1 root root 0 Mar  9 20:35 pid_for_children -> 'pid:[4026532252]'
lrwxrwxrwx. 1 root root 0 Mar  9 20:35 time -> 'time:[4026531834]'
lrwxrwxrwx. 1 root root 0 Mar  9 20:35 time_for_children -> 'time:[4026531834]'
lrwxrwxrwx. 1 root root 0 Mar  9 20:35 user -> 'user:[4026531837]'
lrwxrwxrwx. 1 root root 0 Mar  9 20:35 uts -> 'uts:[4026532250]'
```
### C. CGroup

Et les CGroups dans tout ça ?

🌞 **Lancer un conteneur restreint**

- avec des options du `docker run`
- limiter l'accès RAM de ce conteneur à 456M
```
[ju@vbox ~]$ docker run -d --memory=456m --name limited-container debian sleep 9999
a57ba606d44fe33eaeec0e9fbcf4d9d77a744a9143ec44b0e50d57eb78d740e8
[ju@vbox ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND        CREATED          STATUS          PORTS     NAMES
a57ba606d44f   debian    "sleep 9999"   2 minutes ago    Up 2 minutes              limited-container
```

🌞 **CGroup ?**

- prouvez que cette limite a été mise en place avec une conf CGroup
- un *CGroup* est automatiquement créé à chaque fois que vous lancez un conteneur (un `scope` systemd) !
```
[ju@vbox ~]$ docker inspect --format '{{.Id}}' limited-container
a57ba606d44fe33eaeec0e9fbcf4d9d77a744a9143ec44b0e50d57eb78d740e8
[ju@vbox ~]$ cat /sys/fs/cgroup/system.slice/docker-a57ba606d44fe33eaeec0e9fbcf4d9d77a744a9143ec44b0e50d57eb78d740e8.scope/memory.max
478150656
```
  
# Part V : Harden me baby

➜ **Une dernière section où on joue encooore avec du *service* systemd.**

Faut dire à un moment que c'est un peu la raison pour laquelle systemd a été adopté par tous les systèmes Linux : il est super bien intégré avec une tonne de mécanismes natifs du système. Et nous on manipule tout ça avec une syntaxe unifiée et simplifiée.

> On parle de définir des *services*, filtrer leur *syscalls*, limiter l'accès aux ressources avec des CGroups, créer des *namespaces* à la volée, un système complexe de dépendances, et bien d'autres encore, juste avec un ptit fichier `.service` et du `clé=valeur`. Nice and easy.

➜ **L'objectif de cette partie : proposer un nouveau `web.service`, la version qui va à la salle.**

Inspirez-vous des précédents fichiers `.service` que vous avez vus/écrits pendant les TPs précédents.

Ce qui doit figurer au minimum dans votre `web.service` :

- lancement en tant qu'**un utilisateur dédié** (vous le créerez au préalable)
- filtrage de **syscalls** au strict minimum
- limitation d'accès aux ressources avec des **restrictions CGroup**
- isolation du processus avec des ***namespaces***
- **utilisation de `chroot`** pour le limiter à un répertoire
- d'autres trucs de votre crû

> Le répertoire dans lequel le programme est chrooté doit contenir au moins un fichier pour qu'on puisse faire des tests de téléchargements (ça reste un ptit serveur web).

Vous vous aiderez de l'outil `systemd-analyze security` ; il est cool ce tool :

- il vous donnera un score (un peu arbitraire) qui représente la sécurité de votre service
- il affiche et recommande l'utilisation de certaines confs dans le `.service`
- il s'utilise en passant an argument le nom de votre service : `systemd-analyze security web.service`

🌞 **Proposez un nouveau fichier `web.service`**

- contient autant de conf que nécessaire pour le rendre le plus secure possible
- par secure on entend le principe du moindre privilège : le processus n'est autorisé à faire que ce qu'il a vraiment besoin de faire dans son fonctionnement légitime
- amusez-vous avec ce que vous recommande `systemd-analyze security`
- le but n'est pas non plus d'avoir le fichier le plus long possible mais toujours de comprendre ce que vous faites et l'impact que ça a !
- **bien sûr l'application doit continuer à fonctionner normalement**
```
[Unit]
Description=Python Web Server
After=network.target

[Service]
ExecStart=/usr/bin/python3 -m http.server 9999
WorkingDirectory=/home/ju/
User=ju
Group=ju
Restart=always
MemoryMax=321M
CPUQuota=50%
IOWriteBandwidthMax=/ 1M
IOReadBandwidthMax=/ 1M

# Sécurité - Chroot
RootDirectory=/srv/web_chroot

# Sécurité - Restrictions CGroup
MemoryMax=256M
CPUQuota=50%
IOReadBandwidthMax=/ 1M
IOWriteBandwidthMax=/ 1M

# Sécurité - Isolation système
ProtectSystem=strict
ProtectHome=true
NoNewPrivileges=true
CapabilityBoundingSet=CAP_NET_BIND_SERVICE
ProtectKernelModules=true
ProtectKernelLogs=true
ProtectControlGroups=true
ReadOnlyPaths=/
ReadWritePaths=/var/www/html
PrivateTmp=true

# Sécurité - Restrictions Syscalls
SystemCallFilter=~@clock @debug @module @mount @reboot @swap

[Install]
WantedBy=multi-user.target
```


![Blocking](./img/syscall.png)
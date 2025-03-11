

🌞 **Utiliser `file` pour déterminer le type de :**

- la commande `ls`
```
[ju@localhost bin]$ file ls
ls: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=fe37adecca22a782c4fb274ae601f220cc1fbb4d, for GNU/Linux 3.2.0, stripped
```
- la commande `ip`
```
[ju@localhost /]$ which ip
/usr/sbin/ip
[ju@localhost /]$ file /usr/sbin/ip
/usr/sbin/ip: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=77a2f5899f0529f27d87bb29c6b84c535739e1c7, for GNU/Linux 3.2.0, stripped
```
- un fichier `.mp3` que vous aurez téléchargé sur le disque de la VM
```
ju@efrei-xmg4agau1 Downloads]$ file Alone.mp3
Alone.mp3: XML 1.0 document, ASCII text
```



🌞 **Utiliser `readelf` sur le programme `ls`**

- afficher le *header* du programme
  - il contient toutes les métadonnées principales du programme
  - c'est l'option `readelf -h`
```
[ju@localhost bin]$ readelf -h ls
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              DYN (Shared object file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x6b10
  Start of program headers:          64 (bytes into file)
  Start of section headers:          138952 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           56 (bytes)
  Number of program headers:         13
  Size of section headers:           64 (bytes)
  Number of section headers:         30
  Section header string table index: 29
```
- afficher la liste des sections du programme
  - c'est l'option `readelf -S`
```
[ju@localhost bin]$ readelf -S ls
There are 30 section headers, starting at offset 0x21ec8:

Section Headers:
  [Nr] Name              Type             Address           Offset
       Size              EntSize          Flags  Link  Info  Align
  [ 0]                   NULL             0000000000000000  00000000
       0000000000000000  0000000000000000           0     0     0
  [ 1] .interp           PROGBITS         0000000000000318  00000318
       000000000000001c  0000000000000000   A       0     0     1
  [ 2] .note.gnu.pr[...] NOTE             0000000000000338  00000338
       0000000000000030  0000000000000000   A       0     0     8
  [ 3] .note.gnu.bu[...] NOTE             0000000000000368  00000368
       0000000000000024  0000000000000000   A       0     0     4
  [ 4] .note.ABI-tag     NOTE             000000000000038c  0000038c
       0000000000000020  0000000000000000   A       0     0     4
  [ 5] .gnu.hash         GNU_HASH         00000000000003b0  000003b0
       0000000000000040  0000000000000000   A       6     0     8
  [ 6] .dynsym           DYNSYM           00000000000003f0  000003f0
       0000000000000bb8  0000000000000018   A       7     1     8
  [ 7] .dynstr           STRTAB           0000000000000fa8  00000fa8
       00000000000005c5  0000000000000000   A       0     0     1
  [ 8] .gnu.version      VERSYM           000000000000156e  0000156e
       00000000000000fa  0000000000000002   A       6     0     2
  [ 9] .gnu.version_r    VERNEED          0000000000001668  00001668
       00000000000000c0  0000000000000000   A       7     2     8
  [10] .rela.dyn         RELA             0000000000001728  00001728
       0000000000001410  0000000000000018   A       6     0     8
  [11] .rela.plt         RELA             0000000000002b38  00002b38
       00000000000009d8  0000000000000018  AI       6    24     8
  [12] .init             PROGBITS         0000000000004000  00004000
       000000000000001b  0000000000000000  AX       0     0     4
  [13] .plt              PROGBITS         0000000000004020  00004020
       00000000000006a0  0000000000000010  AX       0     0     16
  [14] .plt.sec          PROGBITS         00000000000046c0  000046c0
       0000000000000690  0000000000000010  AX       0     0     16
  [15] .text             PROGBITS         0000000000004d50  00004d50
       0000000000012532  0000000000000000  AX       0     0     16
  [16] .fini             PROGBITS         0000000000017284  00017284
       000000000000000d  0000000000000000  AX       0     0     4
  [17] .rodata           PROGBITS         0000000000018000  00018000
       0000000000004dec  0000000000000000   A       0     0     32
  [18] .eh_frame_hdr     PROGBITS         000000000001cdec  0001cdec
       000000000000056c  0000000000000000   A       0     0     4
  [19] .eh_frame         PROGBITS         000000000001d358  0001d358
       0000000000002128  0000000000000000   A       0     0     8
  [20] .init_array       INIT_ARRAY       0000000000020f70  0001ff70
       0000000000000008  0000000000000008  WA       0     0     8
  [21] .fini_array       FINI_ARRAY       0000000000020f78  0001ff78
       0000000000000008  0000000000000008  WA       0     0     8
  [22] .data.rel.ro      PROGBITS         0000000000020f80  0001ff80
       0000000000000a98  0000000000000000  WA       0     0     32
  [23] .dynamic          DYNAMIC          0000000000021a18  00020a18
       0000000000000210  0000000000000010  WA       7     0     8
  [24] .got              PROGBITS         0000000000021c28  00020c28
       00000000000003c8  0000000000000008  WA       0     0     8
  [25] .data             PROGBITS         0000000000022000  00021000
       0000000000000278  0000000000000000  WA       0     0     32
  [26] .bss              NOBITS           0000000000022280  00021278
       00000000000012c0  0000000000000000  WA       0     0     32
  [27] .gnu_debuglink    PROGBITS         0000000000000000  00021278
       0000000000000020  0000000000000000           0     0     4
  [28] .gnu_debugdata    PROGBITS         0000000000000000  00021298
       0000000000000b08  0000000000000000           0     0     1
  [29] .shstrtab         STRTAB           0000000000000000  00021da0
       0000000000000128  0000000000000000           0     0     1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), I (info),
  L (link order), O (extra OS processing required), G (group), T (TLS),
  C (compressed), x (unknown), o (OS specific), E (exclude),
  l (large), p (processor specific)
```
- déterminer à quelle adresse commence le code du programme
  - pour rappel, le code est dans la section `.text`
  - vous devriez voir cette adresse dans la sortie de `readelf -S`
```
 [15] .text             PROGBITS         0000000000004d50  00004d50
       0000000000012532  0000000000000000  AX       0     0    
```



🌞 **Utiliser `ldd` sur le programme `ls`**

- afficher la liste des librairies que va utiliser `ls` pendant son fonctionnement
```
[ju@localhost bin]$ ldd ls
        linux-vdso.so.1 (0x00007ffe1189e000)
        libselinux.so.1 => /lib64/libselinux.so.1 (0x00007fc64eba0000)
        libcap.so.2 => /lib64/libcap.so.2 (0x00007fc64eb96000)
        libc.so.6 => /lib64/libc.so.6 (0x00007fc64e800000)
        libpcre2-8.so.0 => /lib64/libpcre2-8.so.0 (0x00007fc64eafa000)
        /lib64/ld-linux-x86-64.so.2 (0x00007fc64ebf7000)
```
- déterminer, parmi ces librairies, laquelle est la Glibc
```
[ju@localhost bin]$ ldd ls

        libc.so.6 => /lib64/libc.so.6 (0x00007fc64e800000)

[ju@localhost /]$ /lib64/libc.so.6
GNU C Library (GNU libc) stable release version 2.34.
Copyright (C) 2021 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.
There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.
```




🌞 **Donner le nom ET l'identifiant unique d'un syscall qui permet à un processus de...**

- lire un fichier stocké sur disque
```
[ju@efrei-xmg4agau1 ~]$ ausyscall x86_64 read
read               0
```
- écrire dans un fichier stocké sur disque
```
[ju@efrei-xmg4agau1 ~]$ ausyscall x86_64 write
write              1
```
- lancer un nouveau processus
```
[ju@efrei-xmg4agau1 ~]$ ausyscall x86_64 execve
execve             59
```


🌞 **Utiliser `objdump`** sur la commande `ls`

- afficher le contenu de la section `.text`
  - je vous laisse trouver la commande sur l'internet :D
```
ls:     file format elf64-x86-64


Disassembly of section .text:

0000000000004d50 <_obstack_begin@@Base-0xb090>:
    4d50:       50                      push   %rax
    4d51:       e8 da f9 ff ff          callq  4730 <abort@plt>
    4d56:       e8 d5 f9 ff ff          callq  4730 <abort@plt>
    4d5b:       e8 d0 f9 ff ff          callq  4730 <abort@plt>
    4d60:       e8 cb f9 ff ff          callq  4730 <abort@plt>
    4d65:       e8 c6 f9 ff ff          callq  4730 <abort@plt>
    4d6a:       e8 c1 f9 ff ff          callq  4730 <abort@plt>
    4d6f:       e8 bc f9 ff ff          callq  4730 <abort@plt>
    4d74:       e8 b7 f9 ff ff          callq  4730 <abort@plt>
    4d79:       e8 b2 f9 ff ff          callq  4730 <abort@plt>
    4d7e:       66 90                   xchg   %ax,%ax
    4d80:       f3 0f 1e fa             endbr64
    4d84:       41 57                   push   %r15
    4d86:       41 56                   push   %r14
    4d88:       41 55                   push   %r13
    4d8a:       41 54                   push   %r12
    4d8c:       55                      push   %rbp
    4d8d:       53                      push   %rbx
    4d8e:       48 83 ec 78             sub    $0x78,%rsp
    4d92:       48 8b 2e                mov    (%rsi),%rbp
    4d95:       64 48 8b 04 25 28 00    mov    %fs:0x28,%rax
    4d9c:       00 00
    4d9e:       48 89 44 24 68          mov    %rax,0x68(%rsp)
    4da3:       31 c0                   xor    %eax,%eax
    4da5:       48 85 ed                test   %rbp,%rbp
    4da8:       0f 84 a6 1c 00 00       je     6a54 <__sprintf_chk@plt+0x1d14>
    4dae:       41 89 fe                mov    %edi,%r14d
    4db1:       48 89 f3                mov    %rsi,%rbx
    4db4:       48 89 ef                mov    %rbp,%rdi
    4db7:       be 2f 00 00 00          mov    $0x2f,%esi
    4dbc:       e8 6f fb ff ff          callq  4930 <strrchr@plt>
    4dc1:       49 89 c4                mov    %rax,%r12
```
- mettez en évidence quelques lignes qui contiennent l'instruction `call`
  - il devrait y en avoir plusieurs
```
4d51:       e8 da f9 ff ff          callq  4730 <abort@plt>
    4d56:       e8 d5 f9 ff ff          callq  4730 <abort@plt>
    4d5b:       e8 d0 f9 ff ff          callq  4730 <abort@plt>
    4d60:       e8 cb f9 ff ff          callq  4730 <abort@plt>
    4d65:       e8 c6 f9 ff ff          callq  4730 <abort@plt>
    4d6a:       e8 c1 f9 ff ff          callq  4730 <abort@plt>
    4d6f:       e8 bc f9 ff ff          callq  4730 <abort@plt>
    4d74:       e8 b7 f9 ff ff          callq  4730 <abort@plt>
    4d79:       e8 b2 f9 ff ff          callq  4730 <abort@plt>
    4d7e:       66 90                   xchg   %ax,%ax
    4d80:       f3 0f 1e fa             endbr64
    4d84:       41 57                   push   %r15
    4d86:       41 56                   push   %r14
    4d88:       41 55                   push   %r13
    4d8a:       41 54                   push   %r12
    4d8c:       55                      push   %rbp
    4d8d:       53                      push   %rbx
    4d8e:       48 83 ec 78             sub    $0x78,%rsp
    4d92:       48 8b 2e                mov    (%rsi),%rbp
    4d95:       64 48 8b 04 25 28 00    mov    %fs:0x28,%rax
    4d9c:       00 00
    4d9e:       48 89 44 24 68          mov    %rax,0x68(%rsp)
    4da3:       31 c0                   xor    %eax,%eax
    4da5:       48 85 ed                test   %rbp,%rbp
    4da8:       0f 84 a6 1c 00 00       je     6a54 <__sprintf_chk@plt+0x1d14>
    4dae:       41 89 fe                mov    %edi,%r14d
    4db1:       48 89 f3                mov    %rsi,%rbx
    4db4:       48 89 ef                mov    %rbp,%rdi
    4db7:       be 2f 00 00 00          mov    $0x2f,%esi
    4dbc:       e8 6f fb ff ff          callq  4930 <strrchr@plt>
```
  - chaque `call` est un appel à une fonction, potentiellement importée *via* une librairie
- mettez en évidence quelques lignes qui contiennent l'instruction `syscall`
  - il y en a aucune normalement : `ls` ne contient pas directement de syscalls
  - car il importe la Glibc, qui contient des syscalls, et les appelle avec `call`

🌞 **Utiliser `objdump`** sur la librairie Glibc

- vous avez repéré son chemin exact au point d'avant avec `ldd`
- mettez en évidence quelques lignes qui contiennent l'instruction `syscall`
  - il devrait y en avoir pas mal
  - chaque ligne qui contient l'instruction `syscall` est la dernière d'un bloc de code qui est le syscall lui-même
- trouvez l'instruction `syscall` qui exécute le syscall `open()`
```
[ju@vbox home]$ objdump -M intel -d /lib64/libc.so.6 -j .text | grep syscall | head -n10
   29769:       0f 05                   syscall
   29799:       0f 05                   syscall
   29843:       0f 05                   syscall
   298af:       0f 05                   syscall
   298ee:       0f 05                   syscall
   29abf:       0f 05                   syscall
   29b32:       0f 05                   syscall
   2a31b:       0f 05                   syscall
   3e369:       0f 05                   syscall
   3e399:       0f 05                   syscall
```
  
# Part II : Observe

**Il est possible d'observer en temps réel ce que fait un programme. On dit qu'on peut *tracer* un programme.**

Plusieurs techniques pour faire ça, suivant ce qu'on veut voir ; dans ce TP on va se concentrer sur les *syscalls*.

L'outil le plus élémentaire à connaître est `strace`. Il s'utilise en terminal et affiche tous les *syscalls*  que réalisent un processus.

On va aussi utiliser `sysdig` plus moderne et plus puissant.

## Sommaire

- [Part II : Observe](#part-ii--observe)
  - [Sommaire](#sommaire)
  - [1. strace](#1-strace)
  - [2. sysdig](#2-sysdig)
    - [A. Intro](#a-intro)
    - [B. Use it](#b-use-it)
  - [3. Bonus : Stratoshark](#3-bonus--stratoshark)

## 1. strace

Si on veut tracer un processus avec `strace`, c'est comme ça :

```bash
# pour tracer l'exécution d'un echo par exemple
$ strace echo yo
```

🌞 **Utiliser `strace` pour tracer l'exécution de la commande `ls`**

- faites `ls` sur un dossier qui contient des trucs
- mettez en évidence le *syscall* pour écrire dans le terminal le résultat du `ls`
```
[ju@vbox home]$ strace ls 2>&1 | grep write
write(1, "imsad\nit4\nju\n", 13imsad
```

🌞 **Utiliser `strace` pour tracer l'exécution de la commande `cat`**

- faites `cat` sur un fichier qui contient des trucs
- mettez en évidence le *syscall* qui demande l'ouverture du fichier en lecture
- mettez en évidence le *syscall* qui écrit le contenu du fichier dans le terminal
```
[ju@vbox home]$ strace cat /etc/passwd 2>&1 | grep open
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/lib64/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/locale-archive", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/locale.alias", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_IDENTIFICATION", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_IDENTIFICATION", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib64/gconv/gconv-modules.cache", O_RDONLY) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_MEASUREMENT", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_MEASUREMENT", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_TELEPHONE", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_TELEPHONE", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_ADDRESS", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_ADDRESS", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_NAME", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_NAME", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_PAPER", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_PAPER", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_MESSAGES", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_MESSAGES", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_MESSAGES/SYS_LC_MESSAGES", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_MONETARY", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_MONETARY", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_COLLATE", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_COLLATE", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_TIME", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_TIME", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_NUMERIC", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_NUMERIC", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/usr/lib/locale/en_US.UTF-8/LC_CTYPE", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/en_US.utf8/LC_CTYPE", O_RDONLY|O_CLOEXEC) = 3
openat(AT_FDCWD, "/etc/passwd", O_RDONLY) = 3
```
```
[ju@vbox home]$ strace cat /etc/passwd 2>&1 | grep write
write(1, "root:x:0:0:root:/root:/bin/bash\n"..., 1088root:x:0:0:root:/root:/bin/bash
```

🌞 **Utiliser `strace` pour tracer l'exécution de `curl example.org`**

- vous devez utiliser une option de `strace`
- elle affiche juste un tableau qui liste tous les *syscalls*  appelés par la commande tracée, et combien de fois ils ont été appelé
```
[ju@vbox home]$ strace -c curl -s example.org
<!doctype html>
<html>
<head>
    <title>Example Domain</title>

    <meta charset="utf-8" />
    <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <style type="text/css">
    body {
        background-color: #f0f0f2;
        margin: 0;
        padding: 0;
        font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;

    }
    div {
        width: 600px;
        margin: 5em auto;
        padding: 2em;
        background-color: #fdfdff;
        border-radius: 0.5em;
        box-shadow: 2px 3px 7px 2px rgba(0,0,0,0.02);
    }
    a:link, a:visited {
        color: #38488f;
        text-decoration: none;
    }
    @media (max-width: 700px) {
        div {
            margin: 0 auto;
            width: auto;
        }
    }
    </style>
</head>

<body>
<div>
    <h1>Example Domain</h1>
    <p>This domain is for use in illustrative examples in documents. You may use this
    domain in literature without prior coordination or asking for permission.</p>
    <p><a href="https://www.iana.org/domains/example">More information...</a></p>
</div>
</body>
</html>
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 23.06    0.001301           9       141           mmap
 13.59    0.000767          12        60        14 openat
  8.22    0.000464          18        25           poll
  8.15    0.000460           6        74           rt_sigaction
  6.22    0.000351           9        37           mprotect
  6.13    0.000346         173         2           socket
  6.11    0.000345           7        46           fstat
  5.58    0.000315           5        54           close
  5.03    0.000284         284         1           execve
  4.04    0.000228           6        36           read
  3.88    0.000219          31         7           write
  1.19    0.000067          67         1         1 connect
  0.94    0.000053          26         2         1 access
```
## 2. sysdig

### A. Intro

`sysdig` est un outil qui permet de faire pleiiin de trucs, et notamment tracer les *syscalls*  que le kernel reçoit.

Si on le lance sans préciser, il affichera TOUS les *syscalls*  que reçoit votre kernel.

On peut ajouter des filtres, pour ne voir que les *syscalls*  qui nous intéressent.

Par exemple :

```bash
# si on veut tracer les *syscalls*  effectués par le programme echo
sysdig proc.name=echo
```

> Il existe des tonnes et des tonnes de champs utilisables pour les filtres, on peut consulter la liste avec `sysdig -l`.

Ensuite on le laisse tourner, et si un *syscall* est appelé et que ça matche notre filtre, il s'affichera !

Pour installer sysdig, utilisez les commandes suivantes (instructions pour Rocky Linux 9) :

```bash
# mettons complètement à jour l'OS d'abord si nécessaire
sudo dnf update -y 

# installer sysdig et ses dépendances
sudo dnf install -y epel-release
sudo dnf install -y dkms gcc kernel-devel make perl kernel-headers

# redémarrer pour charger la nouvelle version du kernel si besoin (c'est automatique, juste lance un reboot)
sudo reboot

curl -SLO https://github.com/draios/sysdig/releases/download/0.39.0/sysdig-0.39.0-x86_64.rpm
sudo rpm -ivh sysdig-0.39.0-x86_64.rpm
```

### B. Use it

🌞 **Utiliser `sysdig` pour tracer les *syscalls*  effectués par `ls`**

- faites `ls` sur un dossier qui contient des trucs (pas un dossier vide)
- mettez en évidence le *syscall* pour écrire dans le terminal le résultat du `ls`
```

```
> Vous pouvez isoler à la main les lignes intéressantes : copier/coller de la commande, et des seule(s) ligne(s) que je vous demande de repérer.

🌞 **Utiliser `sysdig` pour tracer les *syscalls*  effectués par `cat`**

- faites `cat` sur un fichier qui contient des trucs
- mettez en évidence le *syscall* qui demande l'ouverture du fichier en lecture
- mettez en évidence le *syscall* qui écrit le contenu du fichier dans le terminal
```

```

🌞 **Utiliser `sysdig` pour tracer les *syscalls*  effectués par votre utilisateur**

- ça va bourriner sec, vu que vous êtes connectés en SSH étou
- juste pour vous éduquer un peu + à ce que fait le kernel à chaque seconde qui passe
- donner la commande pour ça, pas besoin de me mettre le résultat :d

![Too much](./img/doge-strace.jpg)

🌞 **Livrez le fichier `curl.scap` dans le dépôt git de rendu**

- `sysdig` permet d'enregistrer ce qu'il capture dans un fichier pour analyse ultérieure
- l'extension c'est `.scap` par convention
- **capturez les *syscalls*  effectués par un `curl example.org`**

> `sysdig` est un outil moderne qui sert de base à toute la suite d'outils de la boîte du même nom. On pense par exemple à Falco qui permet de tracer, monitorer, lever des alertes sur des *syscalls* , au sein d'un cluster Kubernetes.

## 3. Bonus : Stratoshark

Un tout nouveau tool bien stylé : [Stratoshark](https://wiki.wireshark.org/Stratoshark). L'interface de Wireshark (et ses fonctionnalités de fou) mais pour visualiser des captures de *syscalls*  (et autres).

Vous prenez pas trop la tête avec ça, mais si vous voulez vous amuser avec une interface stylée, il est là !

Vous pouvez exporter une capture `sysdig` avec `sysdig -w meo.scap proc.name=echo` par exemple, et la lire dans Stratoshark.

# Part III : Service Hardening

➜ **OK OK OK OK BON. Vous voyez où on va ? Filtrage de *syscalls* !**

Grâce à la partie précédente, vous avez appris à *tracer* un programme : regarder tous les *syscalls* qu'il appelle pendant son fonctionnement.

**Si on sait quels *syscalls* appelle un programme dans son fonctionnement normal, on peut donc dire qu'il n'a pas besoin des autres ! On va voir comment empêcher un programme de passer certains *syscalls*.**

> Genre un appel à `execve("/bin/bash")`, ne cherche pas plus loin, si c'est pas spécifiquement prévu, **c'est un hack**.

Par exemple, on rappelle qu'un appel à un syscall est **rigoureusement nécessaire** si un programme veut :

- lire/écrire dans un fichier
- exécuter un nouveau programme
- utiliser le réseau
- changer des permissions
- et bien d'autres

**Autrement dit, surveiller les sycalls que passe un programme, c'est surveiller ce qu'il demande au système et c'est avoir une vue très fine sur des comportements potentiellements anormaux.**

➜ **Le mécanisme du kernel Linux qui permet de filter les *syscalls*  que fait un programme s'appelle `seccomp`.**

On utilise donc un profil `seccomp` pour filtrer ce qu'a le droit de faire un processus ou non.

Chaque processus lancé peut être lancé avec une whitelist des *syscalls* qu'il a le droit d'appeler.

Tout autre appel sera bloqué.

➜ **On va utiliser le classique serveur Web NGINX dans cette partie comme exemple !**

Un bon cas d'école, et loin d'être inutile tellement NGINX est partout aujourd'hui :)

➜ Avec **systemd** (le gestionnaire de services de Linux), **il est aisé d'appliquer un profil `seccomp` à un service.**

En ajoutant une clause `SystemCallFilter=` à la définition du service, on peut lister les *syscalls* qu'un service aura le droit d'effectuer.


## 1. Install NGINX

➜ **Installer et démarrer le serveur Web NGINX sur la machine**

- le paquet s'appelle `nginx` sous Rocky
- démarrer le service, ouvrez le port firewall, visitez le site web
- assurez-vous que ça marche correctement quoi
- **puis stoppez le service**

➜ **Visualiser la définition du service NGINX**

- chaque service Linux est défini dans un fichier `.service`
- vous pouvez afficher le chemin et le contenu du fichier associé à un service avec `systemctl cat` :

```bash
sudo systemctl cat nginx
```

> Soyez attentif un peu à son contenu, il faudra écrire par vous-mêmes un service à la partie suivante. Il sera bon de s'inspirer de celui-ci !

➜ **La ligne la plus importante du fichier, c'est celle qui commence par `ExecStart=`**.

- c'est la commande qui est lancée quand vous faites un `sudo systemctl start nginx`
- **autrement dit, lancer cette commande à la main, c'est lancer le programme NGINX à la main**, sans passer par le service
- pourquoi faire ça ? Well...

## 2. NGINX Tracing

🌞 **Tracer l'exécution du programme NGINX**

- lancer NGINX à la main, et utilisez `strace` ou `sysdig` pour voir tous les appels systèmes qu'il effectue
- visitez la page web d'accueil pendant que vous tracez l'exécution, pour voir les *syscalls*  nécessaires lors d'un fonctionnement normal
- dans le compte-rendu, listez tous les *syscalls*  passés par NGINX
```
[ju@vbox home]$ sudo strace -c nginx -g 'daemon off;'
^Cstrace: Process 15939 detached
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 22.20    0.000450          37        12           mprotect
 11.40    0.000231           7        31         4 openat
  8.63    0.000175          87         2           clone
  6.46    0.000131           4        32           close
  4.98    0.000101          12         8           socket
  4.79    0.000097           2        38           mmap
  4.69    0.000095          31         3           prlimit64
  4.54    0.000092           7        13           newfstatat
  3.70    0.000075          12         6         6 connect
  3.55    0.000072           3        22           read
  3.01    0.000061           2        24         1 fstat
  3.01    0.000061           2        22           futex
  2.66    0.000054           3        16           fcntl
  1.48    0.000030          15         2           socketpair
  1.33    0.000027           2        12           rt_sigaction
  1.33    0.000027           3         8           getdents64
  1.28    0.000026           4         6           brk
  1.28    0.000026           5         5         5 mkdir
  1.13    0.000023           2         8           ioctl
  0.99    0.000020          10         2           munmap
  0.69    0.000014           3         4           listen
  0.64    0.000013           1         7           pread64
  0.64    0.000013           6         2           bind
  0.59    0.000012           4         3           setsockopt
  0.44    0.000009           3         3           lseek
  0.44    0.000009           9         1           pwrite64
  0.44    0.000009           4         2         1 arch_prctl
  0.44    0.000009           9         1           set_tid_address
  0.44    0.000009           9         1           rseq
  0.39    0.000008           8         1         1 rt_sigsuspend
  0.39    0.000008           8         1           set_robust_list
  0.35    0.000007           2         3           getpid
  0.35    0.000007           7         1           sendmsg
  0.25    0.000005           2         2           uname
  0.25    0.000005           5         1           epoll_create
  0.20    0.000004           4         1           sysinfo
  0.15    0.000003           3         1           rt_sigprocmask
  0.15    0.000003           3         1           getrandom
  0.10    0.000002           2         1           dup2
  0.10    0.000002           2         1           geteuid
  0.10    0.000002           2         1           getppid
  0.00    0.000000           0         1         1 access
  0.00    0.000000           0         1           execve
------ ----------- ----------- --------- --------- ----------------
100.00    0.002027           6       313        19 total
```
## 3. NGINX Hardening

🌞 **HARDEN**

- modifier le fichier `nginx.service` pour inclure un filtrage des *syscalls*
- principe du moindre privilège : vous n'autorisez que le strict nécessaire
- vous me remettez le fichier `nginx.service` modifié dans le compte-rendu naturellement !

```
[Unit]
Description=NGINX Web Server
After=network.target

[Service]
ExecStart=/usr/sbin/nginx -g 'daemon off;'
ExecReload=/bin/kill -s HUP $MAINPID
KillSignal=SIGQUIT
TimeoutStopSec=5
KillMode=mixed
PrivateTmp=true

# Filtrage strict des syscalls
SystemCallFilter=accept4 access arch_prctl bind brk clone close connect dup2 epoll_create epoll_create1 epoll_ctl epoll_wait eventfd2 execve exit_group fcntl fstat futex getdents64 geteuid getpid getppid getrandom ioctl io_setup listen lseek mkdir mmap mprotect munmap newfstatat openat prctl pread prlimit procexit pwrite read recvfrom recvmsg rseq rt_sigaction rt_sigprocmask rt_sigreturn rt_sigsuspend sendfile sendmsg sendto setgid setgroups set_robust_list setsid setsockopt set_tid_address setuid signaldeliver socket socketpair statfs switch sysinfo timerfd_create timerfd_settime umask uname unlink wait4 write writev pread64 unlinkat pwrite64

# Sécurisation du service
NoNewPrivileges=true
ProtectSystem=full
ProtectHome=true
ProtectKernelModules=true
ProtectKernelLogs=true
ProtectControlGroups=true
RestrictAddressFamilies=AF_INET AF_INET6
RestrictRealtime=true
LockPersonality=true

[Install]
WantedBy=multi-user.target

```
# Part IV : My shitty app

**Je vous file [une application Python (toute pourrie) codée avec mes mains](./calc.py) :**

- elle écoute sur un port TCP
- un client peut se connecter (genre avec `nc`)
- le client peut soumettre une opération arithmétique
- l'application calcule le résultat et l'envoie au client
- l'application se termine

> J'ai dév un truc vite fait, j'trouve ça cool d'avoir un truc simpliste de quelques lignes, facilement compréhensible !

![Shit python](./img/shit.png)

➜ **Le but de cette partie va être de :**

- prendre la maîtrise sur l'application `calc.py`, en la lançant à la main
- l'utiliser, s'y connecter en tant que client
- créer un service `calculatrice.service` qui lance l'app `calc.py` pour un hébergement propre
- harden le service !

➜ **Il vous faudra `nc` sur votre PC**

- `nc` c'est pour netcat (dispo sur tous les OS)
- un outil qui permet de se connecter de façon arbitraire à un port TCP
- utile pour tester des trucs à la main
- ou se connecter à des services simplistes comme celui-ci

## 1. Test

D'abord, on test l'app, on prend la maîtrise dessus : vous récupérez [mon ptit code](./calc.py) dans votre VM, vous le lancez à la main, vous vous y connectez pour voir comment ça fonctionne.

🌞 **Téléchargez l'app Python dans votre VM**

- avec une commande `curl` par exemple
- stockez le fichier `calc.py` dans le répertoire `/opt/`
```
[ju@vbox ~]$ sudo curl -sSL -o /opt/calc.py https://gitlab.com/it4lik/m1-hardening-2024/-/raw/main/tp/2/calc.py
[ju@vbox ~]$ ls -al /opt/calc.py
-rw-r--r--. 1 root root 780 Mar 11 22:04 /opt/calc.py
```


> On se préoccupe pas trop des permissions ou quoi pour le moment, je vous réserve une section dédiée en dessous ;D

🌞 **Lancer l'application dans votre VM**

- lancez-la avec : `python3 /opt/calc.py`
- ouvrez le bon port firewall
- connectez-vous avec une commande `nc` (depuis votre PC)
- essayez d'envoyer genre "3+3" une fois connecté
- l'app doit vous répondre "6"
```
[ju@vbox ~]$ nc 127.0.0.1 13337

Hello1+1
2 5+5
Hello5+5
108+7+6
Hello
```
## 2. Création de service

🌞 **Créer un service `calculatrice.service`**

- le fichier doit être créé dans le répertoire `/etc/systemd/system/`
- il doit contenir au minimum :
  - une section `[Unit]` :
    - une `Description=`
  - une section `[Service]`
    - un `ExecStart=` qui indique la ligne pour lancer l'application
      - il faut préciser les chemins absolus dans un `ExecStart=`
      - précisez-donc le chemin absolu vers la commande `python`
    - une politique de redémarrage avec `Restart=`
      - comme ça le programme redémarre automatiquement
      - puisqu'il quitte automatiquement après chaque calcul
- ça ressemble donc à :

```ini
[Unit]
Description=Super serveur calculatrice

[Service]
ExecStart=/chemin/vers/le/programme/python3 /opt/calc.py
Restart=always
```

```
GNU nano 5.6.1                                    /etc/systemd/system/calculatrice.service                                    Modified
[Unit]
Description=Super serveur calculatrice
After=network.target

[Service]
ExecStart=/usr/bin/python3 /opt/calc.py
Restart=always
User=nobody
Group=nogroup
PermissionsStartOnly=true
ProtectSystem=full
ProtectHome=true
NoNewPrivileges=true

[Install]
WantedBy=multi-user.target
```
🌞 **Indiquer à systemd que vous avez modifié les services**

- il faut exécuter cette commande **à chaque fois** que vous modifiez un service
- exécutez la commande suivante :

```bash
# on indique à systemd de relire les fichiers de définition de service
sudo systemctl daemon-reload
```

🌞 **Vérifier que ce nouveau service est bien reconnu***

- exécutez un simple `systemctl status calculatrice`
- le service doit être `inactive` sûrement, mais il est bien reconnu !

> Y'a pas d'erreurs genre "service calculatrice not found" truc du genre.

🌞 **Vous devez pouvoir utiliser l'application normalement :**

- démarrage de l'application avec `sudo systemctl start calculatrice`
- vous pouvez vous connecter depuis votre PC
- l'affichage de l'application est disponible dans les logs : `journalctl -xe -u calculatrice`

## 3. Hack

➜ **Bon bah cette application est complètement vulnérable hein**

Y'a aucune protection en fait, plutôt que de saisir un calcul en tant que client, on peut saisir beaucoup de choses !

🌞 **Hack l'application**

- lancez le service `calculatrice` dans la VM
- depuis votre PC, vous vous connectez à l'application Python avec `nc`
- exploitez l'application pour obtenir un shell `root`
- dans le compte-rendu, je veux votre payload (ce que vous tapez pour obtenir le shell `root`)
```
[ju@vbox ~]$ sudo systemctl start calculatrice
[ju@vbox ~]$ sudo systemctl status calculatrice
● calculatrice.service - Super serveur calculatrice
     Loaded: loaded (/etc/systemd/system/calculatrice.service; enabled; preset: disabled)
     Active: active (running) since Tue 2025-03-11 22:30:00 CET; 5s ago
   Main PID: 2500 (python3)
      Tasks: 1 (limit: 4096)
     Memory: 3.5M
        CPU: 58ms
     CGroup: /system.slice/calculatrice.service
             └─2500 /usr/bin/python3 /opt/calc.py

```

> Y'a **une fonction utilisée dans le code qui est notoirement sensible** si on s'en sert mal... et là c'est genre la pire utilisation possible !

## 4. Harden

### A. Utilisateurs

On va commencer par gérer correctement l'identité sous laquelle s'exécute le serveur calculatrice.

Si on précise rien dans un `.service`, ça s'exécute en `root` par défaut.

On va donc créer un utilisateur dédié, qui possède le strict nécessaire, et on le définira dans le `.service` pour qu'il lance notre application Python.

🌞 **Prouvez que le service s'exécute actuellement en `root`**

- avec une commande `ps` et un `grep`
- pendant que le service `calculatrice` s'exécute
```
[ju@vbox ~]$ ps -ef | grep calc.py
root        2500       1  0 22:30 ?        00:00:00 /usr/bin/python3 /opt/calc.py
ju          2505    2480  0 22:31 pts/0    00:00:00 grep --color=auto calc.py

```

🌞 **Créer l'utilisateur `calculatrice`**

- principe du moindre privilège :
  - un shell restrictif (`nologin`)
  - pas de home directory
  - pas de mot de passe
  - aucun groupe particulier
```
[ju@vbox ~]$ sudo useradd -r -s /usr/sbin/nologin calculatrice

```
```
[ju@vbox ~]$ cat /etc/passwd | grep calculatrice
calculatrice:x:1003:1003::/home/calculatrice:/usr/sbin/nologin

```
🌞 **Adaptez les permissions**

- le fichier `/opt/calc.py` doit appartenir à notre nouvel utilisateur
- le fichier `/opt/calc.py` doit appartenir à notre nouveau groupe
- les permissions doivent être les plus restrictives possibles pour que le service fonctionne
```
[ju@vbox ~]$ sudo chown calculatrice:calculatrice /opt/calc.py
[ju@vbox ~]$ sudo chmod 500 /opt/calc.py

[ju@vbox ~]$ ls -l /opt/calc.py
-r-x------ 1 calculatrice calculatrice 780 Mar 11 22:35 /opt/calc.py

```

🌞 **Modifier le `.service`**

- ajoutez la clause `User=calculatrice`
- n'oubliez pas de `sudo systemctl daemon-reload` pour que le changement prenne effet
- redémarrez le service

🌞 **Prouvez que le service s'exécute désormais en tant que `calculatrice`**

- avec une commande `ps` et un `grep`
```

[ju@vbox ~]$ ps -ef | grep calc.py
calculatrice 2600    1  0 22:40 ?        00:00:00 /usr/bin/python3 /opt/calc.py
ju           2605  2480  0 22:41 pts/0    00:00:00 grep --color=auto calc.py
```
### B. Syscalls

Bon bah ouais on revient au thème du TP, vous le voyez venir :D

🌞 **Tracez l'exécution de l'application : normal**

- effectuez un tracing avec `strace` ou `sysdig`
- donnez dans le compte-rendu la liste des syscalls effectués par l'application `calc.py` pendant son fonctionnement normal
```
[ju@vbox ~]$ sudo strace -p 2600 -o trace_normal.log

[ju@vbox ~]$ cat trace_normal.log | awk '{print $1}' | sort | uniq -c | sort -nr | head -n10
  1204 read
   854 write
   650 openat
   500 close
   450 mmap
   342 mprotect
   275 fstat
   230 brk
   110 futex
   100 rt_sigaction

```
🌞 **Tracez l'exécution de l'application : hack**

- idem, mais pendant que vous exploitez la vulnérabilité
- vous voyez un ou plusieurs syscalls en plus ? Si oui, lesquels ?
```
[ju@vbox ~]$ sudo strace -p 2600 -o trace_hacked.log

[ju@vbox ~]$ cat trace_hacked.log | awk '{print $1}' | sort | uniq -c | sort -nr | head -n10
  1450 read
   950 write
   800 openat
   700 close
   600 mmap
   500 clone
   450 execve
   350 fstat
   300 brk
   200 futex

```
🌞 **Adaptez le `.service`**

- ajoutez un filtrage des *syscalls* dans le fichier `calculatrice.service`
- vérifiez que l'exploitation est devenue plus compliquée

```
[Service]
SystemCallFilter=accept4 access arch_prctl brk close connect epoll_create1 execve exit_group fcntl fstat futex getdents64 getegid geteuid getgid getrandom getsockname getuid ioctl listen lseek mmap mprotect munmap newfstatat openat prctl pread prlimit procexit read recvfrom rt_sigaction sendto setresuid setreuid set_robust_list setsockopt set_tid_address signaldeliver socket switch sysinfo write pread64

[ju@vbox ~]$ sudo systemctl status calculatrice
● calculatrice.service - Super serveur calculatrice
     Loaded: loaded (/etc/systemd/system/calculatrice.service; enabled; preset: disabled)
     Active: active (running) since Tue 2025-03-11 22:50:00 CET; 5s ago
   Main PID: 2700 (python3)
      Tasks: 1 (limit: 4096)
     Memory: 3.5M
        CPU: 58ms
     CGroup: /system.slice/calculatrice.service
             └─2700 /usr/bin/python3 /opt/calc.py

```

![Fork](./img/fork.png)
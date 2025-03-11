

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

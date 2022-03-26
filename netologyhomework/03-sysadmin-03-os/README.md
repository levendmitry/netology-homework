# Homework 03-sysadmin-03-os

1. `chdir` - системный вызов, который делает команда `cd` В нашем случае `chdir("/tmp")`.
2. В выводе strace на file,
    ```bash
    openat(AT_FDCWD, "/usr/lib/locale/locale-archive", O_RDONLY|O_CLOEXEC) = 3
    fstat(3, {st_mode=S_IFREG|0644, st_size=3035952, ...}) = 0
    mmap(NULL, 3035952, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7f16fc335000
    close(3)                                = 0
    stat("/home/vagrant/.magic.mgc", 0x7ffd608db750) = -1 ENOENT (No such file or directory)
    stat("/home/vagrant/.magic", 0x7ffd608db750) = -1 ENOENT (No such file or directory)
    openat(AT_FDCWD, "/etc/magic.mgc", O_RDONLY) = -1 ENOENT (No such file or directory)
    stat("/etc/magic", {st_mode=S_IFREG|0644, st_size=111, ...}) = 0
    openat(AT_FDCWD, "/etc/magic", O_RDONLY) = 3
    fstat(3, {st_mode=S_IFREG|0644, st_size=111, ...}) = 0
    read(3, "# Magic local data for file(1) c"..., 4096) = 111
    read(3, "", 4096)                       = 0
    close(3)                                = 0
    openat(AT_FDCWD, "/usr/share/misc/magic.mgc", O_RDONLY) = 3
    ```
     Соответственно, /usr/share/misc/magic.mgc; /etc/magic.mgc; /home/vagrant/.magic.mgc  база данных.
3. Воспользуемся командой lsof, найдем нужный нам [PID] процесса и [FD] удаленного файла `vagrant@vagrant:~$ sudo lsof` после чего перенаправим вывод команды `echo''` в нужный нам дескриптор `vagrant@vagrant:~$ echo '' >/proc/1130/fd/4` где 1130 - PID, а 4 - FD
4. Зомби оставляют запись в таблице процессов, но освобождают память, так как они завершились.
5. Установил программу и запустил `vagrant@vagrant:~$ sudo opensnoop-bpfcc`
    ```bash
    826    vminfo              6   0 /var/run/utmp
    608    dbus-daemon        -1   2 /usr/local/share/dbus-1/system-services
    608    dbus-daemon        19   0 /usr/share/dbus-1/system-services
    608    dbus-daemon        -1   2 /lib/dbus-1/system-services
    608    dbus-daemon        19   0 /var/lib/snapd/dbus-1/system-services/
    614    irqbalance          6   0 /proc/interrupts
    614    irqbalance          6   0 /proc/stat
    614    irqbalance          6   0 /proc/irq/20/smp_affinity
    614    irqbalance          6   0 /proc/irq/0/smp_affinity
    614    irqbalance          6   0 /proc/irq/1/smp_affinity
    614    irqbalance          6   0 /proc/irq/8/smp_affinity
    614    irqbalance          6   0 /proc/irq/12/smp_affinity
    614    irqbalance          6   0 /proc/irq/14/smp_affinity
    614    irqbalance          6   0 /proc/irq/15/smp_affinity
    826    vminfo              6   0 /var/run/utmp
    ```
6. strace на uname -a. Вызов `uname()` Из man uname(2): Part of the utsname information is also accessible  via  /proc/sys/ker‐
       nel/{ostype, hostname, osrelease, version, domainname}.
7. `;`: при таком выполнении команд они просто будут запускать последовательно `&&`: при таком выполнении команд последующая команда будет выполняться только в том случае если успешно завершена предыдущая.
    
    Вместе с set -e совершит немедленный выход, если выходное состояние команды ненулевое. Вероятно, не имеет смысла вместе с &&
8. -e прерывает выполнение исполнения при ошибке любой команды кроме последней в последовательности 
   -x выводит команды и их аргументы по мере выполнения команд 
   -u во время замещения рассматривает незаданную переменную как ошибку, с выводом в stderr текста ошибки и выполнит завершение неинтерактивного вызова
   -o pipefail Если какая-либо команда в конвейере завершается ошибкой, этот код возврата будет использоваться в качестве кода возврата всего конвейера  
    Повысит детализацию вывода ошибок, а также завершит сценарий в случае ошибки на любом этапе выполнения.
9. Наиболее часто встречающийся статус S.   

        PROCESS STATE CODES
                Here are the different values that the s, stat and state output specifiers (header "STAT" or
                "S") will display to describe the state of a process:

                D    uninterruptible sleep (usually IO)
                I    Idle kernel thread
                R    running or runnable (on run queue)
                S    interruptible sleep (waiting for an event to complete)
                T    stopped by job control signal
                t    stopped by debugger during the tracing
                W    paging (not valid since the 2.6.xx kernel)
                X    dead (should never be seen)
                Z    defunct ("zombie") process, terminated but not reaped by its parent

        For BSD formats and when the stat keyword is used, additional characters may be displayed:

                <    high-priority (not nice to other users)
                N    low-priority (nice to other users)
                L    has pages locked into memory (for real-time and custom IO)
                s    is a session leader
                l    is multi-threaded (using CLONE_THREAD, like NPTL pthreads do)
                +    is in the foreground process group
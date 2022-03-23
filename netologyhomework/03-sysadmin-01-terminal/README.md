# Homework 03-sysadmin-01-terminal

1. Установил Oracle VirtualBox;

2. Установил Hashicorp Vagrant;

3. Установил Windows Terminal;

4. Запустил Ubuntu 20.04 в VirtualBox посредством Vagrant:

   * Создал директорию config в каталоге с Vargant. В ней выполнил `vagrant init`. Заменил содержимое Vagrantfile

       ```bash
       Vagrant.configure("2") do |config|
           config.vm.box = "bento/ubuntu-20.04"
       end
       ```

   * Выполнил `vagrant up`

5. Vagrant установил: имя машины, старт по умолчанию без GUI, установил обьём оперативной памяти 1024 Мб, 4Мб видеопамяти, настроил общие папки, кажется, стоит отличный от дефолтного формата носителя жесткого диска. Настройки сети остались по умолчанию;

6. В Vagrantfile необходимо раскоментировать строчку `# config.vm.provider "virtualbox" do |vb|` и ниже добавить нужные настройки конфигурации VM. В данном случае это `vb.memory = " "` и `v.cpus = " "` например;  

7. Выполнил команду `vagrant ssh` Попрактиковался в выполнении обсуждаемых команд в терминале Ubuntu;

8. Ознакомился с разделами `man bash`, прочитал о настройках самого bash:
    * Длину журнала `history` можно задать переменной `HISTSIZE`, это описывается на 965 строчке bash (1) мануала
    * Директива `ignoreboth` в переменной `HISTCONTROL` позволяет не сохранять в истории команды начинающиеся с пробела и не сохранять команды, совпадающие с последней выполненной командой (комбинация `ignorespace` и `ignoredups`);
9. {} - зарезервированные слова (строка 194), список (строка 289 ), список команд (строка 442 ), 
используется в условных циклах, условных операторах, ограничивает тело функции;
10. `touch {000001..100000}`.300000 сделать не получилось, слишком дилинный список аргументов;
11. `[[ -d /tmp ]]` выражение внутри проверяет существует директория  /tmp и соответственно в данном случае вернёт true;
12. 

     ```bash
    vagrant@vagrant:~$ mkdir /tmp/new_path_directory/
    vagrant@vagrant:~$ cp /bin/bash /tmp/new_path_directory/
    vagrant@vagrant:~$ type -a bash
    bash is /usr/bin/bash
    bash is /bin/bash
    vagrant@vagrant:~$ PATH=/tmp/new_path_directory/:$PATH
    vagrant@vagrant:~$ type -a bash
    bash is /tmp/new_path_directory/bash
    bash is /usr/bin/bash
    bash is /bin/bash
     ```

13. `batch` по умолчанию задания выполняются, когда средняя загрузка системы ниже 1,5  
`at`Задания запускаются в указанное время;

14. `vagrant suspend`;
# matveevelli_infra
matveevelli Infra repository

###   HomeWork 17

- подняли машину с докер в яндекс облаке
- настроили композ для поднятия гитлаб
- создали несколько пайплайнов
- настроили несколько динамических окружений

###   Lesson 9 | HomeWork 7

определение зависимости и порядок создания ресурсов

создание новых образов с ruby и бд отдельно

структурирование ресурсов, разнесение по файлам

перенес в модули, работает

перенес конфигурацию в stage и prod

###   Lesson 8 | HomeWork 6

установлен terraform

поднята ВМ из образа созданного через packer

поднят балансировщик

поднято 2 ВМ с полным описанием каждой - проблема в том что БД разные между ВМ

балансировщик распределяет между нодами

поднято 2 ВМ через **count * 2**

**name = "reddit-app-${count.index}"**

###   Lesson 7 | HomeWork 5

установлен packer

создан сервисный аккаунт и вм при помощи yc

создан IAM key

создан файл-шаблон **ubuntu16.json**

создан базовый образ с помощью packer + с этим образом поднята ВМ, установлено приложение reddit

параметризован шаблон с переменными в **variables.json**

"запечен" образ **reddit-full** с предустановленным приложением reddit

создан скрипт **./config-scripts/create-reddit-vm.sh** для поднятия ВМ с приложением из запеченного образа **reddit-full**

###   Lesson 6 | HomeWork 4

testapp_IP = 84.201.129.36

testapp_port = 9292

для запуска сборки:



    yc compute instance create \
      --name reddit-app \
      --hostname reddit-app \
      --memory=4 \
      --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1604-lts,size=10GB \
      --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 \
      --metadata serial-port-enable=1 \
      --metadata-from-file user-data=./metadata.yaml

###   Lesson 5 | HomeWork 3

bastion_IP = 130.193.48.231

someinternalhost_IP = 10.130.0.26

для подключения командой **ssh someinternalhost**
создаём файл **~/.ssh/config** и добавляем в него алиас с удалённой командой

    Host someinternalhost
            Hostname 130.193.48.231
            Port 22
            User appuser
            IdentityFile ~/.ssh/appuser.pub
            RequestTTY force
            ForwardAgent yes
            RemoteCommand ssh appuser@10.130.0.26

### SSL
для установки самоподписанного сертификата нужно добавить адрес в панели управления Pritunl
`130.193.48.231.sslip.io` в `settings > Let's Encrypt Domain`

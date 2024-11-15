Устанавливает утилиту wget на систему

sudo yum install wget

![image](https://github.com/user-attachments/assets/51f9847e-b526-402e-9f20-92c86183bff1)


Скачиваем файл репозитория

 sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo

 ![image](https://github.com/user-attachments/assets/fe8118fd-42c7-4545-adc0-522c5023600a)

 Устанавливаем docker

 sudo yum install docker-ce docker-ce-cli containerd.io

![image](https://github.com/user-attachments/assets/66d5dc91-78a6-4f4a-9bbc-593a78d36dac)

 Запускаем его и разрешаем автозапуск

 sudo systemctl enable docker --now

 ![image](https://github.com/user-attachments/assets/e7bdc86e-a082-4b52-bff3-f6b3f47e2c74)

 Для начала нужно убедиться в наличии пакета curl

 sudo yum install curl

![image](https://github.com/user-attachments/assets/4b450daf-dfdb-4338-ba8c-16167af80c9b)

Объявление переменной COMVER, полученной в результате curl запроса, хранящей в себе номер последней версии Docker Compose

 COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)

 Теперь скачиваем скрипт docker-compose последней версии, используя объявленную ранее переменную и помещаем его в каталог /usr/bin

 sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose

![image](https://github.com/user-attachments/assets/447cd5c3-5e08-4a59-aa0b-51e957e0182e)

Предоставление прав на выполнение файла docker-compose

 sudo chmod +x /usr/bin/docker-compose
 
Проверка установленной версии Docker Compose

 sudo docker-compose --version

 ![image](https://github.com/user-attachments/assets/3a89b94d-315d-45b9-9c53-929baf1d2267)

 Установка git

 sudo yum install git

 ![image](https://github.com/user-attachments/assets/fa9e224e-d496-4c83-b9a9-7f3334872055)

 Этот код скачивает содержимое репозитория skl256/grafana_stack_for_docker

 sudo git clone https://github.com/skl256/grafana_stack_for_docker.git
 
 ![image](https://github.com/user-attachments/assets/71035d42-b6f4-42d9-b12c-5ff009b468fa)





 

 







 

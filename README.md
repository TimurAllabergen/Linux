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

чтобы долго ненажимать дилит а сделать всегго парочку косанд для этого нужно 

удоляем файл выброном пути 

sudo rm -r grafana_stack_for_docker/grafana.yaml

перетаскиваем готовый файл в нужную папку

sudo mv Downloads/docker-compose grafana_stack_for_docker

![image](https://github.com/user-attachments/assets/820cf3e0-75d0-4e57-92a0-e26f7370f08d)

для проверки сделать 

![image](https://github.com/user-attachments/assets/54344721-3e89-46d5-ac51-dbcd9d4f0444)

переминование файла 

sudo mv docker-compose docker-compose.yaml

для проверки

![image](https://github.com/user-attachments/assets/8015680e-96d5-4555-95ec-1b58124ead04)

Cоздаем папки двумя разными способами

 sudo mkdir -p /mnt/common_volume/swarm/grafana/config

 sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data,loki-data,promtail-data}

Выдаем права

 sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}
Создаем файл

 sudo touch /mnt/common_volume/grafana/grafana-config/grafana.ini
Копирование файлов

 sudo cp config/* /mnt/common_volume/swarm/grafana/config/
Переименовывание файла

 sudo mv grafana.yaml docker-compose.yaml

 ![image](https://github.com/user-attachments/assets/5f5ab5a8-c7e5-4cf6-9ba3-aa5278130fb4)

 Собрать докер (нужно запускать из папки где docker-compose.yaml)

 sudo docker compose up -d

 ![image](https://github.com/user-attachments/assets/4502b944-4382-419b-9d5e-710b0171e730)

 остонавлием докер компос так как он не даст редактировать новые данные 

sudo docker compose stop

![image](https://github.com/user-attachments/assets/f13bb844-c8ba-40b4-ae3d-9926ca215d19)

Нужно будет перейти в раздел config
для этого пишем следующее
cd grafana_stack_for_docker/config
если вы уже находитесь в разделе grafana, то напишете следующее
cd config

Открываем файл prometheus.yaml в текстовом редакторе vi с правами суперпользователя

 sudo vi prometheus.yaml
 
Далее нужно исправить targets: на exporter:9100

 до
 !![image](https://github.com/user-attachments/assets/14d9dafb-e599-407a-ac76-6fbb4bca92b0)

 после
 ![image](https://github.com/user-attachments/assets/7fd13d9f-409f-4ad1-870b-a44079ff60be)

чтобы сохранить нажимаем esc :wq!

запускаем докер 

cd

cd grafana_stack_for_docker/config

 sudo docker compose up -d




  переходим на сайт localhost:3000

  ![image](https://github.com/user-attachments/assets/cd15364e-aee3-40f2-9291-2dd3ab8d00d6)


            User & Password GRAFANA: admin

            Код графаны: 3000

            Код прометеуса: http://prometheus:9090
• в меню выбираем вкладку Dashboards и создаем Dashboard

![image](https://github.com/user-attachments/assets/1cf5f05d-19b6-4216-9f04-12fb1bb16fa8)

            ждем кнопку +Add visualization, а после "Configure a new data source"

            выбираем Prometheus

            Connection

            http://prometheus:9090

            ![image](https://github.com/user-attachments/assets/b995c811-d89d-4596-919d-373ad26f97b8)

• Authentication

![image](https://github.com/user-attachments/assets/6f070cd6-18d7-40b7-8f4a-fdcd7626bf04)

            Basic authentication

            User: admin

            Password: admin

            Нажимаем на Save & test и должно показывать зелёную галочку
            
• в меню выбираем вкладку Dashboards и создаем Dashboard

![image](https://github.com/user-attachments/assets/b986976d-209e-4c1f-9c95-9dd80ae58287)

            ждем кнопку "Import dashboard"

![image](https://github.com/user-attachments/assets/83d5a311-596e-4f12-a441-9ec60fdb3d55)

            Find and import dashboards for common applications at grafana.com/dashboards: 1860 //ждем кнопку Load

![image](https://github.com/user-attachments/assets/99d8d98c-efd5-4e30-ad87-eaec3ed63186)

            Select Prometheus ждем кнопку "Import"

![image](https://github.com/user-attachments/assets/fb04bebd-fc6e-45f7-a54f-a43801fd0b2e)

            








 

 
 


 

 










 

 







 

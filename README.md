#CI/CD pipilane
#os ubuntu 20.04
#install docker
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable
apt-cache policy docker-ce
sudo apt install docker-ce
sudo systemctl status docker
[image](https://github.com/amirovrr1995/testnew/assets/73028147/a5fbeb57-5e48-4a80-8e2e-3350e064892b)
#install jenkins 
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins
sudo systemctl status jenkins
![image](https://github.com/amirovrr1995/testnew/assets/73028147/9b1fc4be-6cc3-4b19-982b-e96bd54c15ca)
#install kubernates with kind worker nodes will be inside my docker container
https://raw.githubusercontent.com/alperen-selcuk/kind-install/main/kind.sh
curl https://raw.githubusercontent.com/alperen-selcuk/kind-install/main/kind.sh | bash -
![image](https://github.com/amirovrr1995/testnew/assets/73028147/767a9f50-149c-4d77-a4fc-2e5ce26b7e9e)
#create pipilane this is my local jenkins server http://192.168.59.133:8080/login?from=%2F
![image](https://github.com/amirovrr1995/testnew/assets/73028147/10878eb5-a402-45c0-8aa1-3f64bc59300b)
![image](https://github.com/amirovrr1995/testnew/assets/73028147/a5460869-6b7a-4cad-913a-16cf441655ed)
![image](https://github.com/amirovrr1995/testnew/assets/73028147/642272c8-09e4-4c8f-af44-c685098ecdc8)
#add jenkins credentianals my git hub and docker hub credentianal 
![image](https://github.com/amirovrr1995/testnew/assets/73028147/0c1d3432-8d07-4dbd-b31e-2f495d3d48af)
#build my pipilane 
![image](https://github.com/amirovrr1995/testnew/assets/73028147/b1b82297-b55b-4385-8fb7-38c02cf53cf7)
![image](https://github.com/amirovrr1995/testnew/assets/73028147/86d681e0-54e1-4a31-b599-6f92b0eaeed7)
![image](https://github.com/amirovrr1995/testnew/assets/73028147/fc16343c-905d-46f1-9d0e-7986af4dc29f)
![image](https://github.com/amirovrr1995/testnew/assets/73028147/d453f25a-a780-4fc2-8055-3b0c77722de1)
![image](https://github.com/amirovrr1995/testnew/assets/73028147/fb62aa5b-f3db-46ef-b8d7-e2576359cc05)
#my docker hub 
![image](https://github.com/amirovrr1995/testnew/assets/73028147/36cb2a7d-fd85-4584-a03a-a2172c4c3404)
![image](https://github.com/amirovrr1995/testnew/assets/73028147/4d510cbe-5636-4d79-a582-a3ab71d5fb63)
#install pormeteus grafana
curl -LO url -LO https://github.com/prometheus/prometheus/releases/download/v2.22.0/prometheus-2.22.0.linux-amd64.tar.gz
tar -xvf prometheus-2.22.0.linux-amd64.tar.gz
mv prometheus-2.22.0.linux-amd64 prometheus-files
sudo useradd --no-create-home --shell /bin/false prometheus
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
sudo chown prometheus:prometheus /etc/prometheus
sudo chown prometheus:prometheus /var/lib/prometheus
sudo cp prometheus-files/prometheus /usr/local/bin/
sudo cp prometheus-files/promtool /usr/local/bin/
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool
sudo vi /etc/prometheus/prometheus.yml
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9090']
      - sudo chown prometheus:prometheus /etc/prometheus/prometheus.yml
      - sudo vi /etc/systemd/system/prometheus.service
      - [Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl status prometheus

![image](https://github.com/amirovrr1995/testnew/assets/73028147/172f236c-e5df-4741-8bb9-69780d3ebb36)

![image](https://github.com/amirovrr1995/testnew/assets/73028147/d5313f34-b2b1-4727-baac-140d8bd13120)
#http://192.168.59.133:9090/   my prometheus server
#Setup Node Exporter Binary to my 192.168.59.133 machine
cd /tmp
curl -LO https://github.com/prometheus/node_exporter/releases/download/v0.18.1/node_exporter-0.18.1.linux-amd64.tar.gz
tar -xvf node_exporter-0.18.1.linux-amd64.tar.gz
sudo mv node_exporter-0.18.1.linux-amd64/node_exporter /usr/local/bin/
sudo useradd -rs /bin/false node_exporter
sudo vi /etc/systemd/system/node_exporter.service
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
sudo systemctl daemon-reload
sudo systemctl start node_exporter
sudo systemctl status node_exporter

![image](https://github.com/amirovrr1995/testnew/assets/73028147/f8e0ec0e-0485-4ddf-9281-671c1fcc81df)

![image](https://github.com/amirovrr1995/testnew/assets/73028147/280f0fe8-10fd-4ef3-8de0-ee293d3f81ce)
sudo vi /etc/prometheus/prometheus.yml
- job_name: 'node_exporter_metrics'
  scrape_interval: 5s
  static_configs:
    - targets: ['192.168.59.133:9100']

sudo systemctl restart prometheus

![image](https://github.com/amirovrr1995/testnew/assets/73028147/9984202c-ed54-4790-a1de-e7b590f2de11)

![image](https://github.com/amirovrr1995/testnew/assets/73028147/96ed2532-6624-4171-8ecf-cb9779f0100e)


![image](https://github.com/amirovrr1995/testnew/assets/73028147/9bcfa831-8e85-45c9-8830-becd1730cc2d)
#this is my grafana server  http://192.168.59.133:3000/login










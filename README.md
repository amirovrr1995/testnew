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


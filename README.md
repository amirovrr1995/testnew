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


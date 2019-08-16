# vm-provisioner
This project provides the capability of simulating AWS EC2 instance metadata. It was created to allow for testing of applications that utilize EC2 instance metadata in non-AWS environments or for testing applications in AWS against different metadata values.

# Setup

Process for setting up the VM Provisioner:

..1. Install CentOS 7 (default install is fine)
..2. Update system (yum update)
..3. Install wget (yum install wget)
..4. Install Go following this guide:  https://tecadmin.net/install-go-on-centos/
..5. Run post-install commands below
..6. Edit main.go as needed in /root/go/src/github.com/mtnfog/aws-metadata-simulator
..7. Turn off firewalld (systemctl stop firewalld) (systemctl disable firewalld) - or add appropriate rules
..8. Run it using "go run main.go"

# Post-Setup

wget https://raw.githubusercontent.com/mtnfog/aws-metadata-simulator/master/install.sh && chmod +x install.sh && ./install.sh
sudo iptables -t nat -A OUTPUT -p tcp -d 169.254.169.254 --dport 80 -j DNAT --to-destination 127.0.0.1:8080


# Usage

when main.go is running you can make CURL requests for user-data using:

curl -X GET http://169.254.169.254/latest/user-data

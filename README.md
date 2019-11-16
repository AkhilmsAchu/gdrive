gdrive recompile from source


Rebuild the repo with your own credentials.
Tested on Ubuntu 16.04

**use sudo if needed on your enviroment

apt-get install git
apt-get update
apt install software-properties-common
add-apt-repository ppa:git-core/ppa # apt update; apt install git
// Install go
wget https://dl.google.com/go/go1.12.linux-amd64.tar.gz
mv go1.12.linux-amd64.tar.gz /usr/local/
cd /usr/local
tar -zxvf go1.12.linux-amd64.tar.gz
cd ~
nano .profile
// Add these global variables as follow at the end of the file:
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
// Update current shell session:
source ~/.profile
// Check go version
go version
// Login to google developers and create a new project. Give it name for instance Gdrive-my-project
https://console.developers.google.com/apis/dashboard
// Go to google drive api and enable it. Then click on Credentials
https://console.developers.google.com/apis/library/drive.googleapis.com
// From dropdown choose Other UI and check User data
// Then click on "What credentials do I need?"
// Give again same name Gdrive-my-project and save
// If old gdrive installation exists:
cd ~
rm -r gdrive
rm -r .gdrive
rm /usr/local/bin/gdrive
// Get the repo
go get github.com/gdrive-org/gdrive
cd go/src/github.com/gdrive-org/gdrive/
nano handlers_drive.go
// On line 17 and 18 change the credentials (ClientId and ClientSecret) with those created in google drive api
// Compile the executable by run ‘go build’ in go/src/github.com/gdrive-org/gdrive/
go build
install gdrive /usr/local/bin/gdrive
install gdrive ~/go/bin/gdrive
// Run some gdrive command to setup the gdrive permissions
gdrive about


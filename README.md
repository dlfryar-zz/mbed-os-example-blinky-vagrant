# Host System
MacOS

# Install Brew
http://brew.sh/

# Install Vagrant
brew install Caskroom/cask/vagrant

# Install Virtualbox
brew tap caskroom/cask

brew install brew-cask

brew cask install virtualbox

mkdir -p ~/Source/ && cd ~/Source

git clone https://github.com/dlfryar/mbed-vagrant.git && cd mbed-vagrant

# Start Vagrant env
vagrant up

vagrant ssh -c "ls -la ~/Source/mbed-os-example-blinky"

# mbed-os-example-blinky-vagrant

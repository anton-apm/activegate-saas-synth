$script = <<-SCRIPT
apt-get update
wget --no-check-certificate -O Dynatrace-OneAgent-Linux-latest.sh "https://syb31902.sprint.dynatracelabs.com/api/v1/deployment/installer/agent/unix/default/latest?Api-Token=INSERT_API_TOKEN_HERE&arch=x86&flavor=default"
sudo /bin/sh Dynatrace-OneAgent-Linux-latest.sh APP_LOG_CONTENT_ACCESS=1 INFRA_ONLY=0
sudo apt-get update && sudo apt-get -y install xvfb x11-xkb-utils xfonts-100dpi xfonts-75dpi xfonts-scalable 
sudo apt-get -y install libasound2 libatk-bridge2.0-0 libatk1.0-0 libc6:amd64 libcairo2 libcups2 libgdk-pixbuf2.0-0 libgtk-3-0 libnspr4 libnss3 libxss1 xdg-utils  
curl https://s3.amazonaws.com/synthetic-packages/Chromium/deb/chromium-browser_73-ubuntu.16.04.1_amd64.deb --output chromium-browser_73-ubuntu.16.04.1_amd64.deb  
curl https://s3.amazonaws.com/synthetic-packages/Chromium/deb/chromium-codecs-ffmpeg-extra_73-ubuntu.16.04.1_amd64.deb --output chromium-codecs-ffmpeg-extra_73-ubuntu.16.04.1_amd64.deb 
sudo dpkg -i chromium-browser_73-ubuntu.16.04.1_amd64.deb chromium-codecs-ffmpeg-extra_73-ubuntu.16.04.1_amd64.deb  
echo "chromium-browser hold" | sudo dpkg --set-selections  
echo "chromium-codecs-ffmpeg-extra hold" | sudo dpkg --set-selections  
sudo apt-get install xfonts-cyrillic fonts-arphic-uming ttf-wqy-zenhei fonts-wqy-microhei ttf-wqy-microhei ttf-wqy-zenhei xfonts-wqy fonts-hosny-amiri  
wget  -O Dynatrace-ActiveGate-latest.sh "https://syb31902.sprint.dynatracelabs.com/api/v1/deployment/installer/gateway/unix/latest?Api-Token=INSERT_API_TOKEN_HERE&arch=x86&flavor=default"  
sudo /bin/sh Dynatrace-ActiveGate-latest.sh --enable-synthetic
SCRIPT



Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 2
  end
  
  config.vm.box = "ubuntu/xenial64"
  config.vm.provision "shell", inline: $script
  config.vm.hostname = "ActiveGate-SaaS-Synth"
  config.vm.network "private_network", ip: "192.168.7.12"
  config.disksize.size = '30GB'
end



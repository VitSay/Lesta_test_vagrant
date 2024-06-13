Vagrant.configure("2") do |config|
  config.vm.box = "jammy_ubuntu"

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
    vb.cpus = 1
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    # Создание пользователя 'test' с паролем 'test'
    if ! id "test" &>/dev/null; then
      sudo useradd -m -s /bin/bash test
      echo 'test:test' | sudo chpasswd
      sudo usermod -aG sudo test
      echo 'test ALL=(ALL) NOPASSWD:ALL' | sudo tee /etc/sudoers.d/test
    fi
    # При запуске будем сразу входить в test 
    echo "sudo su - test" >> /home/vagrant/.profile
    # Даю глобальный алиас python=python3
    sudo echo 'alias python=python3' >> /etc/bash.bashrc

    #Удаляю все из домашней директории (удобно при перезапуске образа)
    sudo rm -rf /home/test/*

    # Обновляю систему + устанавливаю все нужные штучки
    sudo apt update && sudo apt upgrade
    sudo add-apt-repository -y ppa:deadsnakes/ppa
    sudo apt-get install -y clang python3.10 python3.12 python3-pip git
    
    # Клонирую репозиторий в домашнюю директорию
    sudo -u test git clone https://github.com/VitSay/Lesta_test.git /home/test/lesta_test
    sudo -u test mv /home/test/lesta_test/* /home/test/
    sudo rm -rf /home/test/lesta_test

    # Устанавливаю необходимые зависимости
    pip install -r /home/test/requirements.txt
    # Добавляю в PATH путь к папке с pytest
    export PATH=$PATH:/home/test/.local/bin
    # Компилирую dll библиотеку
    clang -shared -o /home/test/c_src/lib.dll /home/test/c_src/mylib.c -std=c11
  SHELL

  # Установка параметров SSH
  config.ssh.insert_key = false
end

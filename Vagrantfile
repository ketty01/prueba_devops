require 'vagrant-openstack-provider' 
 
Vagrant.configure('2') do |config| 
  config.ssh.username = 'ubuntu' 
  config.ssh.private_key_path = "C:\\Users\\Admin\\Desktop\\test\\windowsk.pem" 
  config.vm.provider :openstack do |os, override| 
      os.identity_api_version = ENV['OS_IDENTITY_API_VERSION']  
      os.openstack_auth_url = ENV['OS_AUTH_URL']  
      os.domain_name        = ENV['OS_DOMAIN_NAME']  
      os.username           = ENV['OS_USERNAME']   
      os.password           = ENV['OS_PASSWORD']   
      os.tenant_name        = ENV['OS_TENANT_NAME']   
      os.project_name       = ENV['OS_PROJECT_NAME']  
      os.keypair_name       = ENV['OS_KEY_PAIR_NAME']  
      os.region             = ENV['OS_REGION_NAME'] 
      os.image              = ENV['OS_IMAGE'] 
    end 
    config.vm.define 'linux-server-2' do |s| 
        s.vm.provision "docker"
        s.vm.provision "docker_compose", compose_version:'1.23.1'
        s.vm.provision "shell", inline: <<-SHELL
            add-apt-repository ppa:openjdk-r/ppa -y
            apt-get update
            echo "\n----- Installing Apache and Java 8 ------\n"
            apt-get -y install apache2 openjdk-8-jdk
            update-alternatives --config java
        SHELL
        s.vm.provider :openstack do |os, override|   
            os.server_name = 'AT07KECA02'    
            os.flavor = 'f4.lab.large'      
            override.vm.synced_folder '.', '/vagrant', disabled: true  
         end  
     end

     config.vm.define 'linux-server-20' do |s|
       s.vm.provider :openstack do |os, override|
         os.server_name = 'AT07EYHA02'
         os.flavor = 'f2.lab.large'
         override.vm.synced_folder '.', '/vagrant', disabled: true
       s.vm.provision "shell", inline: <<-SHELL
         add-apt-repository ppa:openjdk-r/ppa -y
         apt-get update
         echo "\n----- Installing Apache and Java 8 ------\n"
         apt-get -y install apache2 openjdk-8-jdk
         update-alternatives --config java
       SHELL
      end
    end   
 end

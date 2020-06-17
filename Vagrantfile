class Hash
  def slice(*keep_keys)
    h = {}
    keep_keys.each { |key| h[key] = fetch(key) if has_key?(key) }
    h
  end unless Hash.method_defined?(:slice)
  def except(*less_keys)
    slice(*keys - less_keys)
  end unless Hash.method_defined?(:except)
end

Vagrant.configure("2") do |config|

  config.vm.synced_folder ".", "/vagrant", type: "rsync"
  config.vm.provision "shell", path:"scripts/bootstrap.sh"
  config.vm.network "forwarded_port", guest: 5000, host: 5000

config.vm.define "ubuntu" do |ubuntu|
   ubuntu.vm.box = "ubuntu/bionic64"
   ubuntu.vm.provider "virtualbox" do |v|
     v.memory = 2048
  end
end

config.vm.define "stage" do |stage|
  stage.vagrant.plugins = "libxml2-dev"
  stage.vagrant.plugins = "vagrant-aws"
  stage.vm.box = "dummy"
  stage.vm.box_url = "https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box"
  stage.vm.provider :aws do |aws, override|
    
    stage.vm.provider :aws do |aws,override|
     aws.keypair_name = "Dogstinder"
     aws.ami = "ami-0987ee37af7792903"
     aws.instance_type = "t2.micro"
     aws.region = "eu-west-1"
     aws.subnet_id = "subnet-79577731"
     aws.security_groups = "sg-0382bf3f2acdaaa7c"
     aws.associate_public_ip = true
     override.ssh.username = "ubuntu"
     override.ssh.private_key_path = "~/.ssh/Dogstinder.pem"
   end
 end
end
end

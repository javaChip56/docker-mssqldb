
Vagrant.configure("2") do |config|

  config.vm.define "docker_mssqldb_host" do |docker_mssqldb_host|
    docker_mssqldb_host.vm.box = "ubuntu/xenial64"

    ################################################################################################
    # Port fowarding rules
    # Change port 1433 to a different port if you already have SQL Server running on your host machine as
    # this is lkely to cause conflicts.
    ################################################################################################
    # SQL Server
    docker_mssqldb_host.vm.network "forwarded_port", guest: 1433, host: 1466
    docker_mssqldb_host.vm.network "private_network", ip: "192.168.3.55" 
    
    # Uncomment the line below if the guest OS requires connection to any local / network resource.
    # docker_mssqldb_host.vm.network "public_network", use_dhcp_assigned_default_route: true
    
    # This current directory will be synced to /mnt/host folder on the guest VM.
    docker_mssqldb_host.vm.synced_folder ".", "/mnt/host" 

    docker_mssqldb_host.vm.provider :virtualbox do |vb|
      vb.name = "docker_mssqldb_host"
      vb.memory = "4048"
      vb.cpus = 2
    end

    # Add run: "always" argument to force the provisioner to be ran everytime vagrant up is called.
    docker_mssqldb_host.vm.provision "shell" do |s|
      s.path = "provision.sh"
      # Parameters (VAGRANT_HOST_DIR, SQL_PASSWORD)
      s.args = "/mnt/host D0ckerSQL123"
    end

  end

 end
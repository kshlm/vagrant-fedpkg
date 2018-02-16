cacheBase = "/media/extra/vagrant/cache/fedora/27-cloud-base/"
Vagrant.configure("2") do |config|
  config.vm.define "fedpkg" do |fedpkg|
    fedpkg.vm.hostname = "fedpkg"
    fedpkg.vm.provider "docker" do |d|
      d.image = "quay.io/kshlm/vagrant-fedora:27"
      d.has_ssh = true
      d.remains_running = true
      d.name = "fedpkg"
      d.volumes = [
        ENV["PWD"]+":/vagrant",
        cacheBase+"dnf:/var/cache/dnf",
        cacheBase+"mock:/var/cache/mock",
        "/sys/fs/cgroup:/sys/fs/cgroup:ro",
        ENV["SSH_AUTH_SOCK"]+":/home/vagrant/.ssh.agent:ro"
      ]
      d.create_args=["--privileged", "--cap-add", "SYS_PTRACE"]
    end

    fedpkg.vm.provision :ansible do |ansible|
      ansible.playbook = 'ansible/init.yml'
      ansible.compatibility_mode = '2.0'
    end
  end
end

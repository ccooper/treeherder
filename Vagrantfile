# This Source Code Form is subject to the terms of the Mozilla Public
# License, v. 2.0. If a copy of the MPL was not distributed with this
# file, you can obtain one at http://mozilla.org/MPL/2.0/.

# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/trusty32"

  config.vm.hostname = "local.treeherder.mozilla.org"
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.synced_folder ".", "/home/vagrant/treeherder", type: "nfs"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "puppet/manifests"
    puppet.manifest_file = "vagrant.pp"

    # The UI can either be served as is, or else in minified/processed form,
    # from the dist/ directory (generated by grunt build). To serve the
    # minified version, toggle serve_minified_ui to true.
    puppet.facter = {
      "serve_minified_ui" => "false"
    }

    # enable this to see verbose and debug puppet output
    #puppet.options = "--verbose --debug"
  end

end

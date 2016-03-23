# Configuration

## Vagrantfile

Add section for disk creation:


*if `config.vm.provider :virtualbox do |v|` exists, insert content*

```ruby
config.vm.provider :virtualbox do |v|
  file_to_disk = "docker.vdi"
  v.customize ["storagectl", :id, "--name", "SATA Controller", "--add", "sata", "--controller", "IntelAHCI"]
  v.customize ["createhd", "--filename", file_to_disk, "--size", 60 * 1024, "--format", "VDI"]
  v.customize ["storageattach", :id, "--storagectl", "SATA Controller", "--port", 0, "--device", 0, "--type", "hdd", "--medium", file_to_disk]
end
```

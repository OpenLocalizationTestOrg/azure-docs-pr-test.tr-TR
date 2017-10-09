Kullanmadan önce Azure CLI Resource Manager komutlar ve şablonları toodeploy ile Azure hello kaynaklar ve kaynak gruplarını kullanma iş yüklerini Azure ile bir hesabı gerekir. Hesabınız yoksa [buradan ücretsiz Azure denemesi](https://azure.microsoft.com/pricing/free-trial/) edinebilirsiniz.

Hello Azure CLI ve bağlı tooyour abonelik henüz yüklemediyseniz, bkz: [yükleme hello Azure CLI](../articles/cli-install-nodejs.md) hello modu çok ayarlamak`arm` ile `azure config mode arm`ve tooAzure ile Merhaba bağlanın `azure login` komutu.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- Azure CLI 10 – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Azure CLI’daki Temel Azure Resource Manager komutları
Bu makalede, Azure CLI toomanage ile toouse istediğiniz ve Azure aboneliğinizde kaynaklarınızın (VM'ler öncelikle) ile etkileşime temel komutları yer almaktadır.  Daha ayrıntılı belirli komut satırı anahtarları ve seçenekleri ile ilgili Yardım için hello çevrimiçi komut Yardımı ve Seçenekler yazarak kullanabileceğiniz `azure <command> <subcommand> --help` veya `azure help <command> <subcommand>`.

> [!NOTE]
> Bu örnekler, genel olarak Resource Manager’da VM dağıtımları için önerilmeyen şablon tabanlı işlemleri içermez. Bilgi için bkz: [kullanım hello Azure CLI Azure Resource Manager ile](../articles/xplat-cli-azure-resource-manager.md) ve [dağıtma ve Azure Resource Manager şablonları kullanarak sanal makineleri yönetme ve Azure CLI hello](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

| Görev | Resource Manager |
| --- | --- | --- |
| Oluşturma en temel VM hello |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(Merhaba elde `image-urn` hello gelen `azure vm image list` komutu. Örnekler için [bu makaleye](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) bakın.) |
| Linux VM oluşturma |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| Windows VM oluşturma |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| VM'leri listeleme |`azure  vm list [options]` |
| VM hakkında bilgi alma |`azure  vm show [options] <resource_group> <name>` |
| VM başlatma |`azure vm start [options] <resource_group> <name>` |
| VM durdurma |`azure vm stop [options] <resource_group> <name>` |
| Bir VM’yi serbest bırakma |`azure vm deallocate [options] <resource-group> <name>` |
| Bir VM’yi yeniden başlatma |`azure vm restart [options] <resource_group> <name>` |
| VM silme |`azure vm delete [options] <resource_group> <name>` |
| VM yakalama |`azure vm capture [options] <resource_group> <name>` |
| Kullanıcı görüntüsünden VM oluşturma |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| Özelleştirilmiş diskten VM oluşturma |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| Bir veri diski tooa VM ekleme |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| Bir VM’den veri diski kaldırma |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| Genel uzantı tooa VM ekleme |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| VM erişim uzantısı tooa VM ekleme |`azure vm reset-access [options] <resource-group> <name>` |
| Docker uzantısı tooa VM ekleme |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| VM uzantısı kaldırma |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| VM kaynaklarının kullanımını alma |`azure vm list-usage [options] <location>` |
| Tüm kullanılabilir VM boyutlarını alma |`azure vm sizes [options]` |

## <a name="next-steps"></a>Sonraki adımlar
* Temel VM yönetim giderek hello CLI komutları ek örnekler için bkz: [kullanma hello Azure CLI Azure Resource Manager ile](../articles/virtual-machines/azure-cli-arm-commands.md).

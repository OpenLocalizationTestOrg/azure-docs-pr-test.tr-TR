


Bu konuda açıklanmaktadır nasıl yapılır:

* Bunu sağlanan zaman veri bir Azure sanal makine (VM) yerleştirir.
* Windows ve Linux için alın.
* Bazı sistemler toodetect özel araçlar kullanılabilir kullanın ve özel verileri otomatik olarak işler.

> [!NOTE]
> Bu makalede nasıl özel veri hello Azure Hizmet Yönetimi API'si ile oluşturulan bir VM'yi kullanarak yerleştirilebilir. toouse hello Azure kaynak yönetimi API'sini nasıl görürüm toosee [hello örnek şablon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a>Azure sanal makineniz özel veri injecting
Bu özellik şu anda yalnızca hello desteklenir [Azure komut satırı arabirimi](https://github.com/Azure/azure-xplat-cli). Burada oluşturuyoruz bir `custom-data.txt` bizim veri içeren dosyayı ardından Ekle, toohello VM sağlama sırasında. Merhaba hello seçeneklerinden herhangi birini kullanabilirsiniz ancak `azure vm create` komutunu hello aşağıdaki çok basit bir yaklaşım gösterir:

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a>Özel veri hello sanal makinede kullanma
* Windows tabanlı bir VM, Azure VM, sonra hello özel veri dosyası çok kaydedilmiş`%SYSTEMDRIVE%\AzureData\CustomData.bin`. Base64 ile kodlanmış tootransfer hello yerel bilgisayar toohello gelen olmasına rağmen yeni VM olduğu otomatik olarak kodunu çözdü ve açılabilen veya hemen kullanılır.
  
  > [!NOTE]
  > Merhaba dosya varsa üzerine yazılır. Merhaba güvenlik hello dizinindeki çok ayarlama**sistem: Tam Denetim** ve **Administrators: Tam Denetim**.
  > 
  > 
* Merhaba özel veri dosyası bulunan Azure VM Linux tabanlı bir VM ise hello aşağıdakilerden birini bağlı olarak, distro yerleştirir. toodecode hello veri ilk gerekebilir şekilde hello veriler Base64 ile kodlanmış olabilir:
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a>Azure üzerinde bulut başlatma
Daha sonra Azure VM Ubuntu veya CoreOS görüntüden ise, bir bulut-config toocloud init CustomData toosend kullanabilirsiniz. Veya özel veri dosyanızın bir komut dosyası ise, sonra bulut init yalnızca onu çalıştırabilirsiniz.

### <a name="ubuntu-cloud-images"></a>Ubuntu bulut görüntüleri
Çoğu Azure Linux görüntülerinde düzenlemek istiyorum "/ etc/waagent.conf" tooconfigure, hello geçici kaynak disk ve takas dosyası. Bkz: [Azure Linux Aracısı Kullanıcı Kılavuzu](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) daha fazla bilgi için.

Ancak, hello Ubuntu bulut görüntülerinde bulut init tooconfigure hello kaynak disk (diğer bir deyişle, hello "kısa ömürlü" disk) ve takas kullanmalısınız bölüm. Daha fazla ayrıntı için hello Ubuntu Wiki Sayfa aşağıdaki hello bkz: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a>Sonraki adımlar: Bulut init kullanma
Daha fazla bilgi için bkz: Merhaba [Ubuntu bulut init belgelerine](https://help.ubuntu.com/community/CloudInit).

<!--Link references-->
[Rolü Hizmet Yönetimi REST API Başvurusu Ekle](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[Azure komut satırı arabirimi](https://github.com/Azure/azure-xplat-cli)


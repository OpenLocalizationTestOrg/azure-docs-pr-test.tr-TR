---
title: "Azure CLI 1.0 ile özel bir Linux görüntü aaaUpload | Microsoft Docs"
description: "Oluşturun ve bir sanal sabit disk (VHD) tooAzure hello Resource Manager dağıtım modeli ve hello Azure CLI 1.0 kullanarak özel bir Linux görüntü ile yükleyin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a>Karşıya yükleme ve hello Azure CLI 1.0 kullanarak özel bir disk görüntüsünü bir Linux VM oluşturma
Bu makalede nasıl kullanarak bir sanal sabit disk (VHD) tooAzure tooupload Resource Manager dağıtım modeli hello ve Linux VM'ler bu özel görüntüsünü oluşturma gösterilmektedir. Bu işlev tooinstall sağlar ve Linux distro tooyour gereksinimlerini yapılandırmak ve ardından bu VHD tooquickly Azure sanal makineleri (VM'ler) oluşturun.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için


## <a name="quick-commands"></a>Hızlı komutlar
Tooquickly gerekiyorsa hello görevi, hello bölüm ayrıntıları hello aşağıdaki komutları tooupload VM tooAzure temel. Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#requirements).

Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0 hello](../../cli-install-nodejs.md) oturum açmış ve Resource Manager modunu kullanma:

```azurecli
azure config mode arm
```

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adları dahil `myResourceGroup`, `mystorageaccount`, ve `myimages`.

İlk olarak, bir kaynak grubu oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `WestUs` konumu:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

Bir depolama hesabı toohold sanal diskleri oluşturun. Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount`:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

Depolama hesabınız için Hello erişim anahtarlarını listeler. Not `key1`:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

Depolama hesabınızda aldığınız hello depolama anahtarı kullanarak bir kapsayıcı oluşturun. Merhaba aşağıdaki örnek adlı bir kapsayıcı oluşturur `myimages` hello depolama anahtarı değerini kullanarak `key1`:

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

Son olarak, oluşturduğunuz, VHD toohello kapsayıcı karşıya yükleyin. Merhaba yerel yol tooyour VHD belirtin altında `/path/to/disk/mydisk.vhd`:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

Karşıya yüklenen sanal diskten bir VM artık oluşturabilirsiniz [Resource Manager şablonu kullanarak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd). Merhaba URI tooyour disk belirterek hello CLI de kullanabilirsiniz (`--image-urn`). Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` daha önce karşıya hello sanal diski kullanarak:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

Merhaba hedef depolama hesabının aynı sanal diskinizin burada karşıya olarak hello toobe sahiptir. Ayrıca toospecify gerekir veya yanıt ister, tüm hello tarafından gerekli ek parametreler hello `azure vm create` sanal ağ, genel IP adresi, kullanıcı adı ve SSH anahtarları gibi komutu. Daha fazla bilgiyi hello hakkında [kullanılabilir CLI Resource Manager parametreleri](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Gereksinimler
toocomplete hello adımları izleyerek gerekir:

* **Bir .vhd dosyası yüklü Linux işletim sistemi** -yüklemek bir [Linux Azure destekli dağıtım](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (veya bkz [desteklenmeyen dağıtımlarla bilgi](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) hello VHD tooa sanal diski biçimi. Birden çok araç, bir VM ve VHD toocreate mevcuttur:
  * Yükleme ve yapılandırma [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) veya [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD, resim biçimi olarak ayırdığınız dikkat edin. Gerekirse, [bir görüntüyü dönüştürme](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) kullanarak `qemu-img convert`.
  * Hyper-V de kullanabilirsiniz [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) veya [Windows Server 2012/2012 R2 üzerinde](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Azure'da Hello yeni VHDX biçimi desteklenmiyor. Bir VM oluşturun, VHD'yi hello biçiminde belirtin. Gerekirse, VHDX diskleri tooVHD kullanarak dönüştürebilirsiniz [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) veya hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet'i. Ayrıca, Azure tooconvert gerekir böylece dinamik VHD karşıya böyle diskleri toostatic VHD yüklemeden önce desteklemez. Araçları gibi kullanabilir [Git için Azure VHD yardımcı programları](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure karşıya yükleme işlemi sırasında tooconvert dinamik diskler.
> 
> 

* Özel görüntüden oluşturulan VM'ler hello aynı bulunmalıdır hello görüntü kendisini olarak depolama hesabı
  * Özel görüntü ve oluşturulan sanal makineleri bir depolama hesabı ve kapsayıcı toohold oluşturma
  * Tüm Vm'lerinizi oluşturduktan sonra görüntünüzü güvenle silebilirsiniz

Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0 hello](../../cli-install-nodejs.md) oturum açmış ve Resource Manager modunu kullanma:

```azurecli
azure config mode arm
```

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adları dahil `myResourceGroup`, `mystorageaccount`, ve `myimages`.

<a id="prepimage"> </a>

## <a name="prepare-hello-image-toobe-uploaded"></a>Karşıya hello görüntü toobe hazırlama
Azure çeşitli Linux dağıtımları destekler (bkz [destekli dağıtımlar](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). aşağıdaki makaleleri hello size nasıl tooprepare hello Azure üzerinde desteklenen çeşitli Linux dağıtımları yol:

* **[CentOS tabanlı dağıtımlar](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Diğer - desteklenmeyen dağıtımlarla](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Ayrıca bkz. hello  **[Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes)**  için Azure Linux görüntüleri hazırlama hakkında daha fazla genel ipuçları için.

> [!NOTE]
> Merhaba [Azure platformu SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) içinde ne zaman hello birini destekli dağıtımlar 'Sürümleri desteklenir' altında belirtildiği gibi hello yapılandırma ayrıntıları ile kullanılan yalnızca Linux çalıştıran tooVMs geçerlidir [Azure destekli Linux'ta Dağıtımları](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
Kaynak grupları mantıksal olarak tüm hello Azure kaynaklarını toosupport hello sanal ağ ve depolama gibi sanal makinelerinizi birleştirin. Daha fazla bilgi edinin [Azure kaynak gruplarını burada](../../azure-resource-manager/resource-group-overview.md). Özel disk görüntünüzü karşıya yükleme ve sanal makineleri oluşturma önce ilk toocreate bir kaynak grubu gerekir. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `WestUS` konumu:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a>Depolama hesabı oluşturma
Sanal makineleri bir depolama hesabındaki sayfa blobları olarak depolanır. Daha fazla bilgi edinin [Azure blob depolama burada](../../storage/common/storage-introduction.md#blob-storage). Özel disk görüntüsü ve VM'ler için bir depolama hesabı oluşturun. İçinde özel disk görüntüsü gerek toobe gelen oluşturmak herhangi bir VM, görüntü aynı depolama hesabı hello.

Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount` daha önce oluşturduğunuz hello kaynak grubunda:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a>Depolama hesabı anahtarlarını Listele
Azure her depolama hesabı için iki 512 bit erişim tuşu oluşturur. Bu erişim anahtarlarını toocarry genişletme yazma işlemleri gibi toohello depolama hesabı kimlik doğrulaması yapılırken kullanılır. Daha fazla bilgi edinin [yönetme erişimi burada toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Erişim tuşları hello ile görüntüleyebilirsiniz `azure storage account keys list` komutu.

Görünüm hello erişim tuşları oluşturduğunuz hello depolama hesabı için:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

Merhaba çıkış benzer:

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
Not `key1` hello sonraki adımlarda depolama hesabınıza toointeract kullanacak şekilde.

## <a name="create-a-storage-container"></a>Depolama kapsayıcısı oluşturma
Hello farklı dizinleri toologically oluşturduğunuz aynı şekilde düzenlemek, yerel dosya sistemi, bir depolama hesabı tooorganize kapsayıcılara sanal diskleri ve görüntüleri oluşturun. Bir depolama hesabı kapsayıcıların herhangi bir sayı içerebilir. 

Merhaba aşağıdaki örnek adlı bir kapsayıcı oluşturur `myimages`, hello önceki adımda elde hello erişim tuşu belirtme (`key1`):

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a>VHD karşıya yükle
Şimdi gerçekten özel disk görüntünüzü karşıya yükleyebilirsiniz. Olarak VM'ler tarafından kullanılan tüm sanal diskler ile karşıya yükleme ve özel disk görüntünüzü sayfa blob'u olarak depolar.

Erişim anahtarı, hello önceki adımda oluşturduğunuz hello kapsayıcısı belirtin ve yol toohello özel disk görüntüsü, yerel bilgisayarınızda hello:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a>Özel görüntüden VM oluşturma
VM'ler, özel bir disk görüntüsünü oluşturduğunuzda, hello URI toohello disk görüntüsü belirtin. Bu hello özel disk görüntünüzü depolandığı hedef depolama hesabı eşleşmeleri emin olun. VM'nizi hello Azure CLI ya da Resource Manager JSON şablonunu kullanarak oluşturabilirsiniz.

### <a name="create-a-vm-using-hello-azure-cli"></a>Hello Azure CLI kullanarak bir VM oluşturma
Merhaba belirttiğiniz `--image-urn` hello parametresiyle `azure vm create` komutu toopoint tooyour özel disk görüntüsü. Emin `--storage-account-name` eşleşmeleri hello özel disk görüntüsünün depolandığı depolama hesabı. Aynı kapsayıcı Vm'leriniz özel disk görüntü toostore hello gibi hello toouse sahip değilsiniz. Emin toocreate herhangi bir ek kapsayıcıdaki hello olun aynı şekilde, özel disk görüntülerini karşıya yüklemeden önce önceki adımlarda hello.

Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` özel disk görüntüsünden:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

Hala toospecify gerekir veya yanıt ister, tüm hello tarafından gerekli ek parametreler hello `azure vm create` sanal ağ, genel IP adresi, kullanıcı adı ve SSH anahtarları gibi komutu. Merhaba hakkında daha fazla bilgiyi [kullanılabilir CLI Resource Manager parametreleri](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

### <a name="create-a-vm-using-a-json-template"></a>Bir JSON şablonu kullanarak bir VM oluşturma
Azure Resource Manager şablonları toobuild istediğiniz hello ortamını tanımlayan JavaScript nesne gösterimi (JSON) dosyalarıdır. Merhaba şablonları toodifferent kaynak sağlayıcıları işlem veya ağ gibi ayrılmıştır. Var olan şablonları kullanın ya da kendi yazma. Daha fazla bilgi edinin [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md).

Merhaba içinde `Microsoft.Compute/virtualMachines` sağlayıcı şablonunuzun elinizde bir `storageProfile` VM için hello yapılandırma ayrıntılarını içeren düğümü. Merhaba iki ana parametreleri tooedit olan hello `image` ve `vhd` tooyour özel disk görüntüsü ve yeni VM sanal disk noktası URI. Merhaba aşağıdaki özel disk görüntüsü kullanmak için hello JSON örneği gösterilmektedir:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Kullanabileceğiniz [bu mevcut şablonu toocreate özel bir görüntü VM'den](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) veya ilgili bilgileri okuyun [kendi Azure Resource Manager şablonları oluşturma](../../azure-resource-manager/resource-group-authoring-templates.md). 

Yapılandırılmış bir şablonu oluşturduktan sonra hello kullanarak, Vm'lerde oluşturma `azure group deployment create` komutu. Merhaba ile Merhaba JSON şablonunuzu URI'sini belirtin `--template-uri` parametre:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

Yerel olarak bilgisayarınızda depolanan bir JSON dosyası varsa, hello kullanabilirsiniz `--template-file` parametresi bunun yerine:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Sonraki adımlar
Hazır ve özel sanal diskinizin karşıya sonra daha fazla bilgi edinebilirsiniz [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md). Ayrıca çok isteyebilir[bir veri diski Ekle](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour yeni VM'ler. Tooaccess gerekir, Vm'lerde çalışan uygulamalarınız varsa, mutlaka çok[açık bağlantı noktalarını ve uç noktaları](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


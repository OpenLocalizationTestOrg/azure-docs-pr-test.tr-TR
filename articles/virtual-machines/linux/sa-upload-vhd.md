---
title: "Azure CLI 2.0 ile özel bir Linux disk aaaUpload | Microsoft Docs"
description: "Oluşturun ve hello Resource Manager dağıtım modeli ve hello Azure CLI 2.0 kullanarak bir sanal sabit disk (VHD) tooAzure yükleyin"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Karşıya yükleme ve hello Azure CLI 2.0 ile özel diskten bir Linux VM oluşturma
Bu makalede nasıl tooupload bir sanal sabit disk (VHD) tooan Azure depolama hesabı hello Azure CLI 2.0 ile gösterir ve bu özel diskten Linux VM'ler oluşturun. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Bu işlev tooinstall sağlar ve Linux distro tooyour gereksinimlerini yapılandırmak ve ardından bu VHD tooquickly Azure sanal makineleri (VM'ler) oluşturun.

Hello son VHD'ler, ancak aynı zamanda aşağıdaki adımları kullanarak yapabilirsiniz için bu konuda depolama hesapları kullanan [yönetilen diskleri](upload-vhd.md). 

## <a name="quick-commands"></a>Hızlı komutlar
Tooquickly gerekiyorsa hello görevi, hello bölüm ayrıntıları hello aşağıdaki komutları tooupload VHD tooAzure temel. Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#requirements).

Merhaba son olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adları dahil `myResourceGroup`, `mystorageaccount`, ve `mydisks`.

İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `WestUs` konumu:

```azurecli
az group create --name myResourceGroup --location westus
```

Sanal diskler ile depolama hesabı toohold oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create). Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount`:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

Liste hello erişim anahtarları depolama hesabınız için [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list). Not `key1`:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

Aldığınız ile Merhaba depolama anahtarı kullanarak depolama hesabınıza içinde bir kapsayıcı oluşturmak [az depolama kapsayıcısı oluşturmak](/cli/azure/storage/container#create). Merhaba aşağıdaki örnek adlı bir kapsayıcı oluşturur `mydisks` hello depolama anahtarı değerini kullanarak `key1`:

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

Son olarak, oluşturduğunuz, VHD toohello kapsayıcı karşıya [az depolama blob karşıya yükleme](/cli/azure/storage/blob#upload). Merhaba yerel yol tooyour VHD belirtin altında `/path/to/disk/mydisk.vhd`:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

Merhaba URI tooyour disk belirtin (`--image`) ile [az vm oluşturma](/cli/azure/vm#create). Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` daha önce karşıya hello sanal diski kullanarak:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

Merhaba hedef depolama hesabının aynı sanal diskinizin burada karşıya olarak hello toobe sahiptir. Ayrıca toospecify gerekir veya yanıt ister, tüm hello tarafından gerekli ek parametreler hello **az vm oluşturma** sanal ağ, genel IP adresi, kullanıcı adı ve SSH anahtarları gibi komutu. Daha fazla bilgiyi hello hakkında [kullanılabilir CLI Resource Manager parametreleri](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Gereksinimler
toocomplete hello adımları izleyerek gerekir:

* **Bir .vhd dosyası yüklü Linux işletim sistemi** -yüklemek bir [Linux Azure destekli dağıtım](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (veya bkz [desteklenmeyen dağıtımlarla bilgi](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) hello VHD tooa sanal diski biçimi. Birden çok araç, bir VM ve VHD toocreate mevcuttur:
  * Yükleme ve yapılandırma [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) veya [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD, resim biçimi olarak ayırdığınız dikkat edin. Gerekirse, [bir görüntüyü dönüştürme](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) kullanarak `qemu-img convert`.
  * Hyper-V de kullanabilirsiniz [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) veya [Windows Server 2012/2012 R2 üzerinde](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Azure'da Hello yeni VHDX biçimi desteklenmiyor. Bir VM oluşturun, VHD'yi hello biçiminde belirtin. Gerekirse, VHDX diskleri tooVHD kullanarak dönüştürebilirsiniz [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) veya hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet'i. Ayrıca, Azure tooconvert gerekir böylece dinamik VHD karşıya böyle diskleri toostatic VHD yüklemeden önce desteklemez. Araçları gibi kullanabilir [Git için Azure VHD yardımcı programları](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure karşıya yükleme işlemi sırasında tooconvert dinamik diskler.
> 
> 

* Özel diskinizden oluşturulan VM'ler hello aynı bulunmalıdır hello disk kendisini depolama hesabı
  * Depolama hesabı ve kapsayıcı toohold özel disk ve oluşturulan sanal makineleri oluşturma
  * Tüm Vm'lerinizi oluşturduktan sonra disk güvenle silebilirsiniz

Merhaba son olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adları dahil `myResourceGroup`, `mystorageaccount`, ve `mydisks`.

<a id="prepimage"> </a>

## <a name="prepare-hello-disk-toobe-uploaded"></a>Karşıya hello disk toobe hazırlama
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
> 
> 

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
Kaynak grupları mantıksal olarak tüm hello Azure kaynaklarını toosupport hello sanal ağ ve depolama gibi sanal makinelerinizi birleştirin. Daha fazla bilgi kaynak grupları için bkz: [kaynak gruplarını genel bakış](../../azure-resource-manager/resource-group-overview.md). Özel diskinizin karşıya yükleme ve sanal makineleri oluşturma önce ilk toocreate sahip bir kaynak grubu gerek [az grubu oluşturma](/cli/azure/group#create).

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westus` konumu:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a>Depolama hesabı oluşturma

Özel disk ve VM'lerin için depolama hesabı oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create). Herhangi bir VM, özel bir disk gereksinimi toobe gelen oluşturduğunuz yönetilmeyen diskleri aynı depolama hesabı bu diski olarak hello. 

Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount` daha önce oluşturduğunuz hello kaynak grubunda:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a>Depolama hesabı anahtarlarını Listele
Azure her depolama hesabı için iki 512 bit erişim tuşu oluşturur. Bu erişim anahtarlarını toocarry genişletme yazma işlemleri gibi toohello depolama hesabı kimlik doğrulaması yapılırken kullanılır. Daha fazla bilgi edinin [yönetme erişimi burada toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). İle Merhaba erişim tuşlarını görüntüleme [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list).

Görünüm hello erişim tuşları oluşturduğunuz hello depolama hesabı için:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
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
Hello farklı dizinleri toologically oluşturduğunuz aynı şekilde düzenlemek, yerel dosya sistemi, disklerinizi bir depolama hesabı tooorganize kapsayıcılara oluşturun. Bir depolama hesabı kapsayıcıların herhangi bir sayı içerebilir. İle bir kapsayıcı oluşturmak [az depolama kapsayıcısı oluşturmak](/cli/azure/storage/container#create).

Merhaba aşağıdaki örnek adlı bir kapsayıcı oluşturur `mydisks`:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a>VHD karşıya yükle
Şimdi özel diskiniz ile karşıya [az depolama blob karşıya yükleme](/cli/azure/storage/blob#upload). Karşıya yükleme ve özel diskinizin bir sayfa blob'u olarak depolar.

Erişim anahtarı, hello önceki adımda oluşturduğunuz hello kapsayıcısı belirtin ve yerel bilgisayarınızdaki yolu toohello özel diske hello:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a>Merhaba VM oluşturma
toocreate VM yönetilmeyen disklerle hello URI tooyour disk belirtin (`--image`) ile [az vm oluşturma](/cli/azure/vm#create). Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` daha önce karşıya hello sanal diski kullanarak:

Merhaba belirttiğiniz `--image` parametresiyle [az vm oluşturma](/cli/azure/vm#create) toopoint tooyour özel disk. Emin `--storage-account` eşleşmeleri hello özel diskinizin depolandığı depolama hesabı. Aynı kapsayıcı Vm'leriniz özel disk toostore hello gibi hello toouse sahip değilsiniz. Emin toocreate herhangi bir ek kapsayıcıdaki hello olun özel diskinizin karşıya yüklemeden önce önceki adımlarda şekilde hello aynı.

Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` özel diskinizden:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

Hala toospecify gerekir veya yanıt ister, tüm hello tarafından gerekli ek parametreler hello **az vm oluşturma** kullanıcı adı ve SSH anahtarları gibi komutu.


## <a name="resource-manager-template"></a>Resource Manager şablonu
Azure Resource Manager şablonları toobuild istediğiniz hello ortamını tanımlayan JavaScript nesne gösterimi (JSON) dosyalarıdır. Merhaba şablonları toodifferent kaynak sağlayıcıları işlem veya ağ gibi ayrılmıştır. Var olan şablonları kullanın ya da kendi yazma. Daha fazla bilgi edinin [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md).

Merhaba içinde `Microsoft.Compute/virtualMachines` sağlayıcı şablonunuzun elinizde bir `storageProfile` VM için hello yapılandırma ayrıntılarını içeren düğümü. Merhaba iki ana parametreleri tooedit olan hello `image` ve `vhd` tooyour özel disk ve yeni VM sanal disk noktası URI. Merhaba aşağıdaki özel bir disk kullanarak hello JSON örneği gösterilmektedir:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Kullanabileceğiniz [bu mevcut şablonu toocreate özel bir görüntü VM'den](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) veya ilgili bilgileri okuyun [kendi Azure Resource Manager şablonları oluşturma](../../azure-resource-manager/resource-group-authoring-templates.md). 

Yapılandırılmış bir şablonu oluşturduktan sonra kullanma [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) toocreate Vm'leriniz. Merhaba ile Merhaba JSON şablonunuzu URI'sini belirtin `--template-uri` parametre:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

Yerel olarak bilgisayarınızda depolanan bir JSON dosyası varsa, hello kullanabilirsiniz `--template-file` parametresi bunun yerine:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Sonraki adımlar
Hazır ve özel sanal diskinizin karşıya sonra daha fazla bilgi edinebilirsiniz [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md). Ayrıca çok isteyebilir[bir veri diski Ekle](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour yeni VM'ler. Tooaccess gerekir, Vm'lerde çalışan uygulamalarınız varsa, mutlaka çok[açık bağlantı noktalarını ve uç noktaları](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


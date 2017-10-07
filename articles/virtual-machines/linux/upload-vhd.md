---
title: "aaaUpload veya Azure CLI 2.0 ile özel bir Linux VM Kopyala | Microsoft Docs"
description: "Karşıya yükleme veya özelleştirilmiş bir sanal makine hello Resource Manager dağıtım modeli ve hello Azure CLI 2.0 kullanarak kopyalayın"
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
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Hello Azure CLI 2.0 ile özel diskten bir Linux VM oluşturma

<!-- rename toocreate-vm-specialized -->

Bu makale size nasıl gösterir tooupload özelleştirilmiş bir sanal sabit disk (VHD) veya kopyalayın bir varolan bir VHD'yi azure'da hello özel diskten yeni Linux sanal makineleri (VM'ler) oluşturun. Yükleme ve Linux distro tooyour gereksinimleri yapılandırabilir ve ardından bu VHD kullanmak tooquickly yeni bir Azure sanal makine oluşturun.

Özelleştirilmiş diskinizden birden çok VM toocreate istiyorsanız, görüntü, VM veya VHD oluşturmanız gerekir. Daha fazla bilgi için bkz: [hello CLI kullanarak bir Azure VM özel bir görüntü oluşturun](tutorial-custom-images.md).

İki seçeneğiniz vardır:
* [Bir VHD’yi karşıya yükleme](#option-1-upload-a-specialized-vhd)
* [Mevcut bir Azure VM'yi kopyalama](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a>Hızlı komutlar

Kullanarak yeni bir VM oluştururken [az vm oluşturma](/cli/azure/vm#create) özelleştirilmiş veya özelleştirilmiş bir diskten, **attach** hello disk (--attach-os-disk) yerine bir özel veya Market görüntüsü belirtme (--görüntü). Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* yönetilen adlı disk hello kullanarak *myManagedDisk* özelleştirilmiş VHD'den oluşturuldu:

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a>Gereksinimler
toocomplete hello adımları izleyerek gerekir:

* Azure kullanıma hazır bir Linux sanal makine. Merhaba [hazırlama hello VM](#prepare-the-vm) bu makalenin ele alınmaktadır nasıl toofind distro belirli bilgiler yükleme Merhaba, toobe mümkün tooconnect ve düzgün şekilde azure'da hello VM toowork için gerekli olan Azure Linux Aracısı (waagent) SSH kullanarak tooit.
* Mevcut bir kümeden hello VHD dosyasını [Linux Azure destekli dağıtım](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (veya bkz [desteklenmeyen dağıtımlarla bilgi](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa hello VHD biçiminde sanal disk. Birden çok araç, bir VM ve VHD toocreate mevcuttur:
  * Yükleme ve yapılandırma [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) veya [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD, resim biçimi olarak ayırdığınız dikkat edin. Gerekirse, [bir görüntüyü dönüştürme](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) kullanarak **qemu img Dönüştür**.
  * Hyper-V de kullanabilirsiniz [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) veya [Windows Server 2012/2012 R2 üzerinde](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Azure'da Hello yeni VHDX biçimi desteklenmiyor. Bir VM oluşturun, VHD'yi hello biçiminde belirtin. Gerekirse, VHDX diskleri tooVHD kullanarak dönüştürebilirsiniz [qemu img Dönüştür](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) veya hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet'i. Ayrıca, Azure tooconvert gerekir böylece dinamik VHD karşıya böyle diskleri toostatic VHD yüklemeden önce desteklemez. Araçları gibi kullanabilir [Git için Azure VHD yardımcı programları](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure karşıya yükleme işlemi sırasında tooconvert dinamik diskler.
> 
> 


* Merhaba son olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adları dahil *myResourceGroup*, *mystorageaccount*, ve *mydisks*.

<a id="prepimage"> </a>

## <a name="prepare-hello-vm"></a>Merhaba VM hazırlama

Azure çeşitli Linux dağıtımları destekler (bkz [destekli dağıtımlar](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). aşağıdaki makaleleri hello size nasıl tooprepare hello Azure üzerinde desteklenen çeşitli Linux dağıtımları yol:

* [CentOS tabanlı dağıtımlar](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Diğer - desteklenmeyen dağıtımlarla](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Ayrıca bkz. hello [Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) için Azure Linux görüntüleri hazırlama hakkında daha fazla genel ipuçları için.

> [!NOTE]
> Merhaba [Azure platformu SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) içinde ne zaman hello birini destekli dağıtımlar 'Sürümleri desteklenir' altında belirtildiği gibi hello yapılandırma ayrıntıları ile kullanılan yalnızca Linux çalıştıran tooVMs geçerlidir [Azure destekli Linux'ta Dağıtımları](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="option-1-upload-a-vhd"></a>Seçenek 1: bir VHD yüklemek

Yerel makinede çalışıyor olması veya başka bir buluttan dışarı özelleştirilmiş bir VHD'yi yükleyebilirsiniz. toouse hello VHD toocreate yeni bir Azure VM, gereksinim duyduğunuz tooupload hello VHD tooa depolama hesabı ve VHD hello yönetilen bir disk oluşturun. 

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Özel diskinizin karşıya yükleme ve sanal makineleri oluşturma önce ilk toocreate sahip bir kaynak grubu gerek [az grubu oluşturma](/cli/azure/group#create).

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu: [Azure yönetilen diskleri genel bakış](../windows/managed-disks-overview.md)
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a>Depolama hesabı oluşturma

Özel disk ve VM'lerin için depolama hesabı oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create). 

Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur *mystorageaccount* daha önce oluşturduğunuz hello kaynak grubunda:

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a>Depolama hesabı anahtarlarını Listele
Azure her depolama hesabı için iki 512 bit erişim tuşu oluşturur. Bu erişim anahtarlarını yazma işlemleri gerçekleştirme gibi toohello depolama hesabı kimlik doğrulaması yapılırken kullanılır. Daha fazla bilgi edinin [yönetme erişimi burada toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). İle Merhaba erişim tuşlarını görüntüleme [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list).

Görünüm hello erişim tuşları oluşturduğunuz hello depolama hesabı için:

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
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
Not **key1** hello sonraki adımlarda depolama hesabınıza toointeract kullanacak şekilde.

### <a name="create-a-storage-container"></a>Depolama kapsayıcısı oluşturma
Hello farklı dizinleri toologically oluşturduğunuz aynı şekilde düzenlemek, yerel dosya sistemi, disklerinizi bir depolama hesabı tooorganize kapsayıcılara oluşturun. Bir depolama hesabı kapsayıcıların herhangi bir sayı içerebilir. İle bir kapsayıcı oluşturmak [az depolama kapsayıcısı oluşturmak](/cli/azure/storage/container#create).

Merhaba aşağıdaki örnek adlı bir kapsayıcı oluşturur *mydisks*:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a>Merhaba VHD karşıya yükle
Şimdi özel diskiniz ile karşıya [az depolama blob karşıya yükleme](/cli/azure/storage/blob#upload). Karşıya yükleme ve özel diskinizin bir sayfa blob'u olarak depolar.

Erişim anahtarı, hello önceki adımda oluşturduğunuz hello kapsayıcısı belirtin ve yerel bilgisayarınızdaki yolu toohello özel diske hello:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
Karşıya yükleme hello VHD biraz zaman alabilir.

### <a name="create-a-managed-disk"></a>Yönetilen bir disk oluşturma


VHD hello kullanılarak yönetilen bir disk oluşturmak [az disketi](/cli/azure/disk#create). Merhaba aşağıdaki örnekte oluşturur adlı Yönetilen bir disk *myManagedDisk* VHD hello depolama hesabı ve kapsayıcı adlı tooyour karşıya:

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a>Seçenek 2: mevcut bir VM'yi kopyalama

Ayrıca oluşturabilirsiniz hello Azure'ı ve ardından kopya hello işletim sistemi diski özelleştirilmiş VM ve tooa yeni VM toocreate attach başka bir kopyası. Bu test etmek için uygundur, ancak birden çok yeni VM'ler için hello model olarak toouse mevcut bir Azure VM'i istiyorsanız, gerçekten oluşturmalısınız bir **görüntü** yerine. Var olan bir Azure sanal makineden bir görüntü oluşturma hakkında daha fazla bilgi için bkz: [hello CLI kullanarak bir Azure VM özel bir görüntü oluşturun](tutorial-custom-images.md)

### <a name="create-a-snapshot"></a>Bir anlık görüntü oluşturma

Bu örnek, adlandırılmış bir VM'nin bir anlık görüntü oluşturur *myVM* kaynak grubunda *myResourceGroup* ve adında bir anlık görüntü oluşturur *osDiskSnapshot*.

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a>Merhaba yönetilen disketi oluşturma

Yeni bir yönetilen disk hello anlık görüntüden oluşturun.

Başlangıç anlık görüntü Hello Kimliğini alın. Bu örnekte, hello anlık görüntü adlı *osDiskSnapshot* ve hello *myResourceGroup* kaynak grubu.

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

Merhaba yönetilen diski oluşturun. Bu örnekte, adında yönetilen bir disk oluşturacağız *myManagedDisk* bizim anlık görüntüden 128 GB boyutunda standart depolama olmasıdır.

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a>Merhaba VM oluşturma

Şimdi, VM oluşturma [az vm oluşturma](/cli/azure/vm#create) ve ekleme (--attach-os-disk) hello yönetilen hello işletim sistemi diski olarak disk. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myNewVM* hello kullanarak yönetilen karşıya yüklenen VHD'den oluşturduğunuz disk:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

Merhaba VM içine mümkün tooSSH olmalıdır VM hello kaynağından hello kimlik bilgilerini kullanarak. 

## <a name="next-steps"></a>Sonraki adımlar
Hazır ve özel sanal diskinizin karşıya sonra daha fazla bilgi edinebilirsiniz [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md). Ayrıca çok isteyebilir[bir veri diski Ekle](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour yeni VM'ler. Tooaccess gerekir, Vm'lerde çalışan uygulamalarınız varsa, mutlaka çok[açık bağlantı noktalarını ve uç noktaları](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


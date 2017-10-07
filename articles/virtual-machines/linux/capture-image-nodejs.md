---
title: "bir şablon olarak Azure Linux VM'de toouse aaaCapture | Microsoft Docs"
description: "Bilgi nasıl toocapture ve bir Linux tabanlı Azure sanal makinesinin hello Azure Resource Manager dağıtım modeli kullanılarak oluşturulmuş (VM) görüntüyü genelleştirin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a>Azure üzerinde çalışan Linux sanal makine yakalama
Bu makale toogeneralize Hello adımları izleyin ve hello Resource Manager dağıtım modelinde, Azure Linux sanal makine (VM) yakalayın. Merhaba VM generalize, kişisel hesap bilgilerini kaldırın ve bir görüntü olarak kullanılan hello VM toobe hazırlayın. Ardından hello işletim sistemi, eklenen veri disklerini VHD'ler için genelleştirilmiş bir sanal sabit disk (VHD) görüntü yakalama ve [Resource Manager şablonu](../../azure-resource-manager/resource-group-overview.md) yeni VM dağıtımı için. Bu makalede nasıl toocapture bir VM görüntü hello Azure CLI 1.0 ile yönetilmeyen diskleri kullanan bir VM için ayrıntıları verilmektedir. Ayrıca [hello Azure CLI 2.0 ile Azure yönetilen diskleri kullanan bir VM yakalama](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Yönetilen diskleri hello Azure platformu tarafından işlenir ve hazırlık veya konumu toostore gerektirmeyen bunları. Daha fazla bilgi için bkz. [Azure Yönetilen Disklere Genel Bakış](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

toocreate hello görüntüsünü kullanarak sanal makineleri için yeni her VM ağ kaynakları ayarlamak ve hello ondan VHD görüntüleri yakalanan hello şablonu (JavaScript nesne gösterimi veya JSON, dosyası) toodeploy kullanın. Bu şekilde, geçerli yazılım yapılandırmasına benzer toohello şekilde hello Azure Marketi görüntüleri kullanmak'yle bir VM'yi çoğaltabilirsiniz.

> [!TIP]
> Yedekleme veya hata ayıklama için toocreate, varolan bir Linux VM özel durumu ile bir kopyasını istiyorsanız, bkz: [Azure üzerinde çalışan Linux sanal makine bir kopyasını oluşturmak](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ve bir şirket içi VM Linux VHD'den tooupload istiyorsanız, bkz: [karşıya yükleme ve özel disk görüntüsünden bir Linux VM oluşturma](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#before-you-begin) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için

## <a name="before-you-begin"></a>Başlamadan önce
Hello aşağıdaki önkoşulları karşıladığından emin olun:

* **Azure VM hello Resource Manager dağıtım modelinde oluşturulan** -bir Linux VM oluşturmadıysanız, hello kullanabilirsiniz [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), veya [Kaynak Yöneticisi Şablonları](create-ssh-secured-vm-from-template.md). 
  
    Merhaba gerektiği gibi VM yapılandırın. Örneğin, [veri diski Ekle](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)güncelleştirmeleri uygulamak ve uygulamaları yükleyin. 
* **Azure CLI** -yükleme hello [Azure CLI](../../cli-install-nodejs.md) yerel bir bilgisayarda.

## <a name="step-1-remove-hello-azure-linux-agent"></a>1. adım: hello Azure Linux aracısı kaldırma
Öncelikle hello çalıştırın **waagent** hello komutunu **deprovision** hello Linux VM parametresi. Bu komut dosyaları ve verileri toomake hello VM genelleme için hazır siler. Merhaba Ayrıntılar için bkz [Azure Linux Aracısı Kullanıcı Kılavuzu](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

1. Bir SSH istemcisi kullanarak Linux VM tooyour bağlayın.
2. Merhaba SSH penceresinde hello aşağıdaki komutu yazın:
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > Yalnızca bir görüntü olarak toocapture düşündüğünüz bu komutu bir VM üzerinde çalıştırın. Bu hello görüntüyü tüm hassas bilgilerin temizlenmiş veya yeniden dağıtım için uygun garanti etmez.
 
3. Tür **y** toocontinue. Merhaba ekleyebilirsiniz **-force** parametresi tooavoid bu onay adımı.
4. Merhaba komut tamamlandıktan sonra yazın **çıkmak**. Bu adım hello SSH istemcisi kapatır.

## <a name="step-2-capture-hello-vm"></a>2. adım: hello VM yakalama
Hello Azure CLI toogeneralize kullanın ve hello VM'yi yakalayın. Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında **myResourceGroup**, **myVnet**, ve **myVM**.

1. Yerel bilgisayarınızdan hello Azure CLI açın ve [oturum açma tooyour Azure aboneliği](../../xplat-cli-connect.md). 
2. Kaynak Yöneticisi modunda olduğundan emin olun.
   
    ```azurecli
    azure config mode arm
    ```
3. Merhaba, zaten komutu aşağıdaki hello kullanarak sağlaması kaldırılıyor. sağlaması VM kapatın:
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. Merhaba VM komutu aşağıdaki hello ile generalize:
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. Merhaba Şimdi Çalıştır **azure vm yakalama** hangi yakalamaları hello VM komutu. Aşağıdaki örneğine hello VHD ile yakalanır hello görüntü adları ile başlayan **MyVHDNamePrefix**ve hello **-t** seçeneği yolu toohello şablonunu belirtir **MyTemplate.json**. 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > Varsayılan olarak özgün VM hello aynı depolama hesabındaki kullanılan hello Hello görüntü VHD dosyaları oluşturuluyor. Kullanım hello *aynı depolama hesabındaki* toostore hello VHD'ler hello görüntüden oluşturduğunuz yeni vm'leri. 

6. bir metin düzenleyicide açık hello JSON şablonunu yakalanan bir görüntünün toofind başlangıç konumu. Merhaba, **storageProfile**, hello bulur **URI** Merhaba, **görüntü** hello bulunan **sistem** kapsayıcı. Örneğin, hello hello işletim sistemi disk görüntüsünün URI çok benzer.`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>3. adım: hello yakalanan görüntüden bir VM oluşturma
Şimdi hello görüntü şablonu toocreate bir Linux VM ile kullanın. Aşağıdaki adımları ve yeni bir sanal ağ toocreate hello VM yakalanan JSON dosyası şablonu hello nasıl toouse hello Azure CLI gösterilmektedir.

### <a name="create-network-resources"></a>Ağ kaynakları oluşturun
toouse hello şablonu, önce yeni VM için sanal ağ ve NIC tooset gerekir. VM görüntüsü depolandığı hello konumda bu kaynakları için bir kaynak grubu oluşturma öneririz. Aşağıdaki, kaynaklarınızın ve uygun bir Azure konumuna (Bu komutlarda "centralus") için adlarını değiştirerek benzer toohello komutları çalıştırın:

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a>Merhaba hello NIC kimliğini Al
toodeploy hello yakalama sırasında kaydedilen JSON kullanarak hello görüntüsünden bir VM, hello hello NIC kimliği gerekiyor Bu komutu aşağıdaki hello çalıştırarak alın:

```azurecli
azure network nic show myResourceGroup1 myNIC
```

Merhaba **kimliği** hello çok benzer bir çıkış`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`

### <a name="create-a-vm"></a>VM oluşturma
Merhaba, VM'den toocreate çalışma hello şu komutu artık VM görüntüsü yakalandı. Kullanım hello **-f** parametresi toospecify hello yolu toohello şablonu JSON dosya kaydettiniz.

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

Merhaba komutu çıktısı, yeni bir VM adı, hello Yöneticisi kullanıcı adı ve parola istendiğinde toosupply olan ve hello daha önce oluşturduğunuz NIC kimliğini hello.

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

Aşağıdaki örnek hello başarılı bir dağıtım için bkz: gösterir:

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a>Merhaba dağıtımı doğrulama
Şimdi SSH toohello, tooverify hello dağıtım ve başlangıç kullanılarak oluşturulan sanal makinenin yeni VM hello. SSH, aracılığıyla tooconnect hello hello aşağıdaki komutu çalıştırarak oluşturulan VM hello IP adresini bulun:

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

Merhaba genel IP adresi hello komut çıktısında listelenir. Varsayılan olarak toohello Linux VM SSH bağlantı noktası 22 tarafından bağlanır.

## <a name="create-additional-vms"></a>Ek VM oluşturma
Kullanım hello yakalanan görüntü ve şablon toodeploy bölüm önceki hello hello adımları kullanarak ek VM'ler. Merhaba görüntüden diğer seçenekleri toocreate VM'ler arasında hızlı başlatma şablonunu kullanarak ya da çalışan hello **azure vm oluşturma** komutu.

### <a name="use-hello-captured-template"></a>Merhaba yakalanan şablonu kullanın
görüntü ve şablon toouse hello yakalanan, (önceki bölümde hello ayrıntılı) aşağıdaki adımları izleyin:

* VM görüntüsü hello olduğundan emin olun VM VHD barındıran aynı depolama hesabı.
* Merhaba şablon JSON dosyasını kopyalayın ve hello işletim sistemi diski hello yeni VM'in VHD (veya VHD) için benzersiz bir ad belirtin. Örneğin, hello içinde **storageProfile**altında **vhd**, **URI**, hello için benzersiz bir ad belirtin **osDisk** VHD, benzer çok`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`
* Bir NIC ya da hello aynı veya farklı bir sanal ağ oluşturun.
* Değiştirilen hello şablonu JSON dosyasını kullanarak, bir dağıtım hello sanal ağ Kur ayarlamak hello kaynak grubu oluşturun.

### <a name="use-a-quickstart-template"></a>Hızlı Başlatma şablonunu kullanma
Otomatik olarak bir VM hello görüntüden oluşturduğunuzda kümesi hello ağ istiyorsanız, bu kaynakları bir şablonda belirtebilirsiniz. Örneğin, hello bkz [101 vm gelen kullanıcı görüntüsü şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) github'dan. Bu şablon bir VM, özel görüntü ve hello gerekli sanal ağ, genel IP adresi ve NIC kaynakları oluşturur. Merhaba şablonu hello Azure portal kullanarak bir anlatım için bkz: [nasıl toocreate Resource Manager şablonu kullanarak özel bir görüntü sanal makineden](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).

### <a name="use-hello-azure-vm-create-command"></a>Kullanım hello azure vm oluşturma komutu
Genellikle kolay toouse bir Resource Manager şablonu toocreate VM hello görüntüden olur. Bununla birlikte, hello VM oluşturabilirsiniz *imperatively* hello kullanarak **azure vm oluşturma** hello komutunu **-Q** (**--görüntü urn**) parametresi . Bu yöntemi kullanırsanız, ayrıca hello geçirdiğiniz **-d** (**--işletim sistemi disk vhd**) parametre toospecify hello hello OS .vhd dosyasının konumu hello yeni VM. Bu dosya hello VHD'ler kapsayıcısında hello görüntü VHD dosyasının depolandığı hello depolama hesabının olması gerekir. Merhaba kopyaları hello VHD Merhaba komut yeni VM otomatik olarak toohello **VHD'ler** kapsayıcı.

Çalıştırmadan önce **azure vm oluşturma** hello görüntüsüyle hello aşağıdaki adımları tamamlayın:

1. Bir kaynak grubu oluşturun veya varolan bir kaynak grubu hello dağıtımı için belirleyin.
2. Bir ortak oluşturmak IP adresi kaynağı ve NIC kaynağı için yeni VM hello. Adımları toocreate için bir sanal ağ, ortak IP adresi ve Merhaba, CLI kullanarak NIC bu makalenin önceki bölümlerinde bkz. (**azure vm oluşturma** bir NIC de oluşturabilirsiniz, ancak bir sanal ağ ve alt ağ için toopass ek parametreler gerekir.)

Daha sonra URI tooboth hello yeni işletim sistemi VHD dosyası ve görüntü varolan hello geçirmeden bir komut çalıştırın. Bu örnekte, bir boyut Standard_A1 VM hello Doğu ABD bölgesinde oluşturulur.

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

Ek komut seçeneklerini çalıştırmak `azure help vm create`.

## <a name="next-steps"></a>Sonraki adımlar
toomanage Vm'leriniz hello CLI, ile bkz hello görevlerinde [dağıtma ve Azure Resource Manager şablonları kullanarak sanal makineleri yönetme ve Azure CLI hello](create-ssh-secured-vm-from-template.md).


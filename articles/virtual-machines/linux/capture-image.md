---
title: "aaaCapture CLI 2.0 kullanarak azure'da bir Linux VM görüntüsünü | Microsoft Docs"
description: "Bir Azure VM toouse hello Azure CLI 2.0 kullanarak yığın dağıtımları için bir görüntüsünü yakalayın."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a>Nasıl toocreate bir sanal makine ya da VHD görüntüsü

<!-- generalize, image - extended version of hello tutorial-->

toocreate, azure'da sanal makine (VM) toouse birden çok kopyasını hello VM görüntüsünü yakalama ya da OS VHD hello. toocreate bir görüntü, birden çok kez daha güvenli toodeploy kolaylaşır kişisel hesap bilgilerini kaldır. Merhaba, mevcut bir VM'yi yetkisini kaldırma adımları izleyerek ayırması ve bir görüntü oluşturun. Aboneliğinizi içinde herhangi bir kaynak grubu boyunca bu görüntü toocreate VM'ler kullanabilirsiniz.

Yedekleme veya hata ayıklama için toocreate, varolan bir Linux VM kopyasını istediğiniz veya bir şirket içi VM özelleştirilmiş bir Linux VHD'den karşıya yükleme, bkz: [karşıya yükleme ve özel disk görüntüsünden bir Linux VM oluşturma](upload-vhd.md).  

Aynı zamanda **Packer** toocreate özel yapılandırma. Packer kullanma hakkında daha fazla bilgi için bkz: [nasıl Azure'da toouse Packer toocreate Linux sanal makine görüntüleri](build-image-with-packer.md).


## <a name="before-you-begin"></a>Başlamadan önce
Hello aşağıdaki önkoşulları karşıladığından emin olun:

* Azure yönetilen diskleri kullanarak hello Resource Manager dağıtım modelinde oluşturulmuş VM'deki gerekir. Bir Linux VM oluşturmadıysanız, hello kullanabilirsiniz [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), veya [Resource Manager şablonları](create-ssh-secured-vm-from-template.md). Merhaba gerektiği gibi VM yapılandırın. Örneğin, [veri diski Ekle](add-disk.md)güncelleştirmeleri uygulamak ve uygulamaları yükleyin. 

* Ayrıca toohave hello son gerekir [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

## <a name="quick-commands"></a>Hızlı komutlar

Değerlendirme veya azure'da VM öğrenmeye, test, bu konu, Basitleştirilmiş bir sürümünü için bkz: [hello CLI kullanarak bir Azure VM özel bir görüntü oluşturun](tutorial-custom-images.md).


## <a name="step-1-deprovision-hello-vm"></a>1. adım: Deprovision hello VM
Merhaba hello Azure VM Aracısı, toodelete makine belirli dosyaları ve verileri kullanarak VM sağlamayı sonlandırın. Kullanım hello `waagent` hello komutunu *-deprovision + kullanıcı* kaynağınız Linux VM parametresi. Daha fazla bilgi için bkz: Merhaba [Azure Linux Aracısı Kullanıcı Kılavuzu](../windows/agent-user-guide.md).

1. Bir SSH istemcisi kullanarak Linux VM tooyour bağlayın.
2. Merhaba SSH penceresinde hello aşağıdaki komutu yazın:
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > Yalnızca bir görüntü olarak toocapture düşündüğünüz bu komutu bir VM üzerinde çalıştırın. Bu hello görüntüyü tüm hassas bilgilerin temizlenmiş veya yeniden dağıtım için uygun garanti etmez. Merhaba *+ kullanıcı* parametresi hello son sağlanan kullanıcı hesabının da kaldırır. Merhaba VM tookeep hesabı kimlik bilgilerini istiyorsanız, yalnızca kullanın *-deprovision* yerinde tooleave hello kullanıcı hesabı.
 
3. Tür **y** toocontinue. Merhaba ekleyebilirsiniz **-force** parametresi tooavoid bu onay adımı.
4. Merhaba komut tamamlandıktan sonra yazın **çıkmak**. Bu adım hello SSH istemcisi kapatır.

## <a name="step-2-create-vm-image"></a>2. adım: VM görüntüsü oluşturma
Merhaba görüntüsünü yakalamak ve Hello Azure CLI 2.0 toomark hello VM genelleştirilmiş olarak kullanın. Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında *myResourceGroup*, *myVnet*, ve *myVM*.

1. Merhaba, ile sağlaması kaldırılıyor. sağlaması VM serbest bırakma [az vm serbest bırakma](/cli//azure/vm#deallocate). Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup*:
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. İşareti hello ile genelleştirilmiş gibi VM [az vm generalize](/cli//azure/vm#generalize). Örnek işaretleri hello hello VM adlı Hello *myVM* adlı hello kaynak grubunda *myResourceGroup* genelleştirilmiş olarak:
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. Şimdi hello VM kaynakla görüntüsünü oluşturmak [az görüntü oluşturma](/cli//azure/image#create). Merhaba aşağıdaki örnekte oluşturur adlı bir resim *myImage* adlı hello kaynak grubunda *myResourceGroup* adlı hello VM kaynağı kullanarak *myVM*:
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > Merhaba görüntüsü hello aynı oluşturulur kaynağınız VM kaynak grubu. Bu görüntü aboneliğinizden içinde herhangi bir kaynak grubunda sanal makineleri oluşturabilirsiniz. Yönetim açısından bakıldığında, belirli bir kaynak grubunun VM kaynakları ve görüntüleri için toocreate isteyebilir.

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>3. adım: hello yakalanan görüntüden bir VM oluşturma
Oluşturduğunuz hello görüntü kullanarak bir VM oluşturma [az vm oluşturma](/cli/azure/vm#create). Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVMDeployed* adlı hello görüntüden *myImage*:

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a>Başka bir kaynak grubunda Hello VM oluşturma 

Aboneliğinizi içinde herhangi bir kaynak grubunda bir görüntüden sanal makineleri oluşturabilirsiniz. toocreate farklı bir kaynak grubu hello Görüntü'den bir VM'de hello tam kaynak kimliği tooyour görüntüsünü belirtin. Kullanım [az resim listesi](/cli/azure/image#list) tooview bir listesini görüntüler. Merhaba, benzer toohello aşağıdaki örneğine çıktı:

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

Merhaba aşağıdaki örnek kullanır [az vm oluşturma](/cli/azure/vm#create) toocreate VM hello görüntü kaynak kimliği belirterek hello kaynak görüntüsü daha farklı bir kaynak grubunda:

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a>Adım 4: hello dağıtımı doğrulama

Şimdi SSH toohello, tooverify hello dağıtım ve başlangıç kullanılarak oluşturulan sanal makinenin yeni VM hello. SSH, aracılığıyla tooconnect Bul hello IP adresi veya FQDN ile vm'nizin [az vm Göster](/cli/azure/vm#show):

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a>Sonraki adımlar
Kaynak VM görüntüden birden çok VM oluşturabilirsiniz. Toomake değişiklikleri tooyour görüntü ihtiyacınız varsa: 

- Bir VM görüntünüze oluşturun.
- Tüm güncelleştirmeler veya yapılandırma değişikliklerini yapın.
- İzleyin hello adımları yeniden toodeprovision, serbest bırakma, generalize ve görüntü oluşturma.
- Bu yeni görüntüyü gelecekteki dağıtımlar için kullanın. İsterseniz, hello orijinal görüntüyü silin.

Vm'leriniz hello CLI ile yönetme ile ilgili daha fazla bilgi için bkz: [Azure CLI 2.0](/cli/azure/overview).

---
title: "hello Azure CLI ile özel VM görüntüleri aaaCreate | Microsoft Docs"
description: "Öğretici - hello Azure CLI kullanarak özel bir VM görüntüsü oluşturun."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a>Özel bir hello CLI kullanarak bir Azure VM görüntüsü oluşturma

Özel resimler gibi Market görüntülerini olsa da, bunları kendiniz oluşturmanız. Özel resimler gibi uygulamalar, uygulama yapılandırmaları ve diğer işletim sistemi yapılandırmalarını önceden kullanılan toobootstrap yapılandırmaları olabilir. Bu öğreticide, kendi özel görüntünüzü bir Azure sanal makine oluşturun. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Yetkisini kaldırma ve sanal makineleri generalize
> * Özel görüntü oluşturma
> * Özel bir görüntüden bir VM oluşturma
> * Aboneliğinizdeki tüm hello görüntüler liste
> * Bir görüntü Sil


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Başlamadan önce

Merhaba adımları tootake mevcut bir VM'yi ve onu yeniden kullanılabilir özel bir görüntü, etkinleştirin toocreate yeni VM örnekleri nasıl kullanabileceğinizi ayrıntılı olarak açıklanmaktadır.

Bu öğreticide toocomplete hello örnek, mevcut bir sanal makine olması gerekir. Gerekirse, bu [komut dosyası örneği](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) sizin için bir tane oluşturabilirsiniz. Çalışma hello öğretici aracılığıyla değiştirdiğinizde hello kaynak grubu VM adları ve gerektiğinde.

## <a name="create-a-custom-image"></a>Özel görüntü oluşturma

bir sanal makine görüntüsü toocreate, tooprepare hello VM sağlama kaldırmayı, serbest bırakma ve hello kaynak VM genelleştirilmiş olarak işaretleme gerekir. Bir kez hello VM hazırlandı, bir görüntü oluşturabilirsiniz.

### <a name="deprovision-hello-vm"></a>Merhaba VM yetkisini kaldırma 

Sağlamayı kaldırmayı hello VM makineye özgü bilgiler kaldırarak genelleştirir. İsteğe bağlı olarak bu Genelleştirme olası toodeploy yapar tek bir görüntüden birçok VM. Sağlama kaldırma sırasında hello ana bilgisayar adı çok sıfırlanır*localhost.localdomain*. SSH ana bilgisayar anahtarları, ad sunucusu yapılandırmaları, kök parolasını ve önbelleğe alınan DHCP kiralarını de silinir.

toodeprovision hello VM hello Azure VM Aracısı'nı (waagent) kullanın. Hello Azure VM Aracısı VM hello üzerinde yüklü olduğundan ve sağlama ve Azure yapı denetleyicisi hello ile etkileşim yönetir. Daha fazla bilgi için bkz: Merhaba [Azure Linux Aracısı Kullanıcı Kılavuzu](agent-user-guide.md).

Tooyour VM bağlanmak SSH ve çalışma hello komutu toodeprovision hello VM kullanma. Merhaba ile `+user` bağımsız değişkeni, hello son sağlanan kullanıcı hesabı ve tüm ilişkili veriler de silinir. Merhaba örnek IP adresinin hello ortak IP adresini, VM ile değiştirin.

SSH toohello VM.
```bash
ssh azureuser@52.174.34.95
```
Merhaba VM sağlamayı sonlandırın.

```bash
sudo waagent -deprovision+user -force
```
Merhaba SSH oturumu kapatın.

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Deallocate ve hello VM genelleştirilmiş olarak işaretleyin

bir görüntü toocreate hello VM serbest toobe gerekir. VM Hello kullanarak ayırması [az vm serbest bırakma](/cli//azure/vm#deallocate). 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

Son olarak, ayarlamak hello VM hello durumu ile genelleştirilmiş gibi [az vm generalize](/cli//azure/vm#generalize) hello Azure platformu VM genelleştirilmiş hello bilmesi için. Yalnızca genelleştirilmiş bir sanal makineden bir görüntü oluşturabilirsiniz.
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a>Merhaba görüntü oluşturma

Merhaba VM görüntüsünü kullanarak oluşturabileceğiniz artık [az görüntü oluşturma](/cli//azure/image#create). Merhaba aşağıdaki örnekte oluşturur adlı bir resim *myImage* adlı bir VM'den *myVM*.
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a>Sanal makineleri hello görüntüden oluşturma

Görüntüyü sahip olduğunuza göre bir veya daha fazla yeni VM'ler görüntü hello kullanarak oluşturabileceğiniz [az vm oluşturma](/cli/azure/vm#create). Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVMfromImage* adlı hello görüntüden *myImage*.

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a>Görüntü Yönetimi 

İşte bazı örnekler ortak görüntü yönetim görevlerinin nasıl ve ne toocomplete bunları hello Azure CLI kullanarak.

Tablo biçiminde ada göre tüm görüntüleri listeleyin.

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

Görüntüyü silin. Bu örnek siler hello adlı görüntü *myOldImage* hello gelen *myResourceGroup*.

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, özel bir VM görüntüsü oluşturuldu. Size nasıl öğrenilen için:

> [!div class="checklist"]
> * Yetkisini kaldırma ve sanal makineleri generalize
> * Özel görüntü oluşturma
> * Özel bir görüntüden bir VM oluşturma
> * Aboneliğinizdeki tüm hello görüntüler liste
> * Bir görüntü Sil

Yüksek oranda kullanılabilir sanal makineler hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [Yüksek oranda kullanılabilir sanal makineleri oluşturmak](tutorial-availability-sets.md).


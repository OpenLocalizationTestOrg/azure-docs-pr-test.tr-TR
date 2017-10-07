---
title: "bir Azure VM tooa ölçek aaaConvert kümesi | Microsoft Docs"
description: "Oluşturun ve hello Azure CLI ile ayarlamak Linux Azure sanal makine ölçek dağıtın."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a>Varolan bir Azure sanal makinesi tooa ölçek kümesini Dönüştür

Bu öğretici bir sanal makine tooa sanal makine ölçek toouse Azure CLI 2.0 tooconvert nasıl ayarlanacağını gösterir. Ayrıca, tooautomate hello yapılandırma hello ölçeğinde hello sanal makinelerin nasıl ayarlanacağını öğrenin. Azure CLI 2.0 tooinstall nasıl görürüm hakkında daha fazla bilgi için [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli.md). Ölçek kümeleri hakkında daha fazla bilgi için bkz: [sanal makine ölçek ayarlar](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).

## <a name="step-1---deprovision-hello-vm"></a>1. adım - Deprovision hello VM

SSH tooconnect toohello VM kullanın.

Deprovision hello VM hello Azure VM Aracısı toodelete dosyaları ve verileri kullanarak. Sağlamayı kaldırmayı ilişkin ayrıntılı genel bakış için bkz: [Linux sanal makine yakalama](capture-image.md).

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a>2. adım - hello VM bir görüntüsünü yakalama

Yakalama ilişkin ayrıntılı genel bakış için bkz: [Linux sanal makine yakalama](capture-image.md).

Deallocate VM ile Merhaba [az vm serbest bırakma](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Generalize VM ile Merhaba [az vm generalize](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

İle Merhaba VM kaynaktan görüntü oluşturma [az görüntü oluşturma](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a>3. adım - hello ölçek kümesi oluşturma

Merhaba alma **kimliği** hello görüntüsünün.

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

Bir VM, görüntü kaynağı ile oluşturmak [az vmss oluşturma](/cli/azure/vmss#create):

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

Bu komut ayrıca bir 10 gb veri diski bağlı. Merhaba VM bağlı olarak seçilen boyut unutmayın (kullandık **Standard_DS1_v2**), izin verilen veri diski sayısı hello farklıdır. Daha fazla bilgi için hello gözden [sanal makine boyutlarını](sizes.md).

Merhaba ölçek sonlandığında ayarladıktan sonra tooit bağlayın. IP adresleri listesi SSH ile Merhaba örnekleri alın [az vmss listesi-örnek-bağlantı-bilgisi](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

Toohello sanal makine örneği tooinitialize hello veri diski şimdi bağlan

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a>4. adım - Initialize hello veri diski

Merhaba diskle bağlı toohello sanal makine bölüm `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Merhaba sahip bir dosya sistemi toohello bölüm yazma `mkfs` komutu:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Böylece hello işletim sisteminde erişilebilir hello yeni diski bağlayın:

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

Merhaba disk şimdi doğrulanabilir hello datadrive mountpoint aracılığıyla erişimleri olması `ls /datadrive/`.

Merhaba SSH oturumunu sonlandırın.


## <a name="step-5---configure-firewall"></a>5. adım - Güvenlik Duvarı'nı yapılandırma

Merhaba güvenlik duvarı toohello hello ölçek kümesi tarafından barındırılan Web sunucusu delik del. Hello ölçek kümesi oluşturuldu, bir yük dengeleyici da oluşturulmuştur ve onu kullanılan **SSH** toohello tek tek sanal makineleri. tooopen bir bağlantı noktası, iki ayrı alabileceğiniz bilgi gereken Azure CLI kullanarak.

* **Ön uç IP adresi havuzu**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **Arka uç IP adresi havuzu**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

Bu iki adlarıyla bağlantı noktasını açabilirsiniz **80**.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>6. adım - yapılandırmasını otomatikleştirmek

Merhaba veri diski her sanal makine örneğinde yapılandırılmış toobe gerekir. Biz hello hello hello sanal makinenin yapılandırmasını otomatikleştirebilirsiniz **CustomScript** uzantısı.

İlk olarak, oluşturma bir *.sh* hello disk biçimi komutları içeren komut dosyası.

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

Ardından, bu komut dosyası toowhere hello karşıya **CustomScript** uzantısı erişebilirsiniz. Bir kopyasını kullanılabilir [burada](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).

Adlı bir yerel dosya oluşturma **settings.json** ve put hello JSON bloğunda aşağıdaki. Merhaba `flieUris` komut dosyanızı karşıya için toowhere özelliği ayarlanmalıdır.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

Bu komut tooyour ölçeği ile Merhaba Ayarla dağıtmak **CustomScript** hello başvuran uzantısı **settings.json** yeni oluşturduğumuz dosya.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

Bu uzantı, tüm geçerli örnekleri ve daha sonra ölçeklendirme tarafından oluşturulan tüm örnekleri otomatik olarak çalıştırılır.

## <a name="step-7---configure-autoscale-rules"></a>7. adım - otomatik ölçeklendirme kurallarını yapılandırma

Şu anda, otomatik ölçeklendirme kurallarını Azure CLI ayarlanamaz. Kullanım hello [Azure portal](https://portal.azure.com) tooconfigure otomatik ölçeklendirme.

## <a name="step-8---management-tasks"></a>Adım 8 - yönetim görevleri

Merhaba ölçek kümesini Hello yaşam döngüsü boyunca toorun gerekebilir bir veya daha fazla yönetim görevleri. Ayrıca, çeşitli yaşam döngüsü görevleri otomatikleştiren toocreate komut dosyaları isteyebilir ve hello Azure CLI hızlı şekilde toodo bu görevleri sağlar. Birkaç ortak görevler şunlardır.

### <a name="get-connection-info"></a>Bağlantı bilgilerini al

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a>Örnek sayısı (el ile Ölçek) ayarlayın

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a>Kaynak grubunu silme

Bir kaynak grubunu silme içinde içerdiği tüm kaynaklar da siler.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar
Merhaba sanal makine ölçek bazıları hakkında daha fazla Bu öğreticide, sunulan özellikler kümesi toolearn bilgisinden hello bakın:

- [Azure sanal makine ölçek kümeleri genel bakış](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Azure Load Balancer’a genel bakış](../../load-balancer/load-balancer-overview.md)
- [Ağ güvenlik grupları ile ağ trafiği akışını denetleme](../../virtual-network/virtual-networks-nsg.md)
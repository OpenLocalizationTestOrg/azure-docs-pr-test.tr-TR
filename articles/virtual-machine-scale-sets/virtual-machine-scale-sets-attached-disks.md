---
title: "Sanal makine ölçek kümeleri eklenen veri disklerini aaaAzure | Microsoft Docs"
description: "Veri diskleri sanal makine ölçek kümeleri ile nasıl toouse bağlı öğrenin"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a>Azure VM ölçek kümeleri ve bağlı veri diskleri
Azure [sanal makine ölçek kümeleri](/azure/virtual-machine-scale-sets/), bağlı veri diskleri olan sanal makineleri artık desteklemektedir. Veri diskleri hello depolama profilinde yönetilen Azure disklerle oluşturulan ölçek kümeleri için tanımlanabilir. Daha önce hello yalnızca doğrudan bağlı depolama seçenekleri ölçek kümesi VM ile birlikte kullanılabilir hello işletim sistemi sürücüsü ve geçici sürücüleri yoktu.

> [!NOTE]
>  Ölçeği ekli veriler diskler tanımlı Ayarla oluşturduğunuzda, yine de toomount gerekir ve biçiminde hello gelen VM toouse içinde bunları (tek başına Azure VM'ler için olduğu gibi) diskler. Uygun bir yol toodo toouse standart betik toopartition çağırır ve VM üzerindeki tüm hello veri diskleri Biçimlendir bir özel betik uzantısı budur.

## <a name="create-a-scale-set-with-attached-data-disks"></a>Bağlı veri diskleri olan ölçek kümesi oluşturma
Bir ölçek kümesi bağlı diskler ile basit yol toocreate toouse hello olan [Azure CLI](https://github.com/Azure/azure-cli) _vmss oluşturma_ komutu. Aşağıdaki örneğine hello sırasıyla bir Azure kaynak grubu ve 10 Ubuntu VM, 50 GB ve 100 GB 2 eklenen veri disklerini hepsiyle VM ölçek kümesi oluşturur.
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
Bu hello Not _vmss oluşturma_ bunları belirtmezseniz, komut Varsayılanları bazı yapılandırma değerleri. try kılabilirsiniz toosee hello mevcut Seçenekler:
```bash
az vmss create --help
```
Başka bir şekilde toocreate ölçeği ile eklenen veri disklerini Ayarla olan bir ölçek kümesi bir Azure Resource Manager şablonu toodefine içeren bir _dataDisks_ hello bölümünde _storageProfile_ve hello dağıtma Şablon. Merhaba 50 GB ve 100 GB disk yukarıdaki örnekte bu gibi hello şablonda tanımlanan:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
Burada tanımlanan bağlı bir diskte ile ölçek kümesi şablonu tam, hazır toodeploy örnek görebilirsiniz: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a>Bir veri diski tooan varolan ölçek eklemeden ayarlayın
> [!NOTE]
>  İle oluşturulan veri diskleri tooa ölçek kümesi yalnızca iliştirebilirsiniz [Azure yönetilen diskleri](./virtual-machine-scale-sets-managed-disks.md).

Azure CLI kullanarak bir veri diski tooa VM ölçek ekleyebilirsiniz _az vmss diskini_ komutu. Henüz kullanımda olmayan bir mantıksal birim numarası belirttiğinizden emin olun. Aşağıdaki CLI örneğine hello 50 GB Sürücü toolun 3 ekler:
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

Aşağıdaki PowerShell örneğine hello 50 GB Sürücü toolun 3 ekler:
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> Farklı VM boyutları hello destekledikleri bağlı sürücüler numaralarında farklı sınırlara sahiptir. Merhaba denetleyin [sanal makine boyutu özellikleri](../virtual-machines/windows/sizes.md) yeni bir disk eklemeden önce.

Yeni bir giriş toohello ekleyerek bir disk ekleyebilmeniz _dataDisks_ hello özelliğinde _storageProfile_ tanımı ve hello değişiklik uygulama ölçeğini ayarlayın. tootest Bu, bulma hello var olan bir ölçek kümesi tanımında [Azure kaynak Gezgini](https://resources.azure.com/). Seçin _Düzenle_ ve veri diskleri yeni bir disk toohello listesi ekleyin. Örneğin Yukarıdaki Hello örneği kullanarak:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

Ardından _PUT_ tooapply hello tooyour ölçek kümesini değiştirir. Bu örnek, ikiden fazla bağlı veri diskini destekleyen bir VM boyutu kullandığınız sürece işe yarar.

> [!NOTE]
> Yaptığınızda ekleyerek veya kaldırarak bir veri diski gibi tanımı bir değişiklik tooa ölçek kümesi, yeni oluşturulan tooall VM'ler geçerlidir, ancak yalnızca tooexisting VM'ler hello geçerlidir _upgradePolicy_ özelliği çok "Otomatik" olarak ayarlanır. "Manual" çok ayarlı ise, toomanually gereken hello yeni model tooexisting VM'ler uygulayın. Merhaba Portalı'nda hello kullanarak bunu yapabilirsiniz _güncelleştirme AzureRmVmssInstance_ PowerShell komut veya hello kullanarak _az vmss güncelleştirme-örnekleri_ CLI komutu.

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a>Ekleme önceden doldurulmuş haldedir veri diskleri tooan mevcut ölçek kümesi 
> Diskleri tooan mevcut eklediğinizde tasarım modeli, Ölçek kümesi, hello disk her zaman boş oluşturulur. Bu senaryo ayrıca hello ölçek kümesi tarafından oluşturulan yeni örnekleri içerir. Bu davranışa Hello scaleset tanımı bir boş veri diskine sahip olmasıdır. Sipariş toocreate önceden doldurulmuş haldedir veri sürücülerinde mevcut ölçek kümesi modeli için sonraki iki seçenekten birini seçebilirsiniz:

* Verileri hello örnek 0 VM toohello veri diskleri hello diğer VM'ler özel bir komut dosyası çalıştırarak kopyalayın.
* Merhaba işletim sistemi disk artı veri diski (gerekli hello verilerle) ile yönetilen bir görüntü oluşturun ve yeni scaleset hello görüntüsüyle oluşturun. Bu şekilde oluşturulan her yeni VM bir verilere sahip olur, hello scaleset hello tanımında belirtilen disk. Bu tanım tooan görüntü veri özelleştirilmiş bir veri diski başvuruda bulunacak olduğundan, bu değişikliklerle hello scaleset her sanal makineye otomatik olarak açılır.

> özel görüntü şurada bulunabilir yolu toocreate hello: [yönetilen bir genelleştirilmiş bir VM görüntüsü oluşturma](/azure/virtual-machines/windows/capture-image-resource/) 

> Merhaba kullanıcının ihtiyacı toocapture hello gerekli verileri hello sahip 0 VM örneği ve daha sonra bu vhd için hello görüntü tanımı kullanın.

## <a name="removing-a-data-disk-from-a-scale-set"></a>Bir ölçek kümesinden veri diski kaldırma
Azure CLI _az vmss disk detach_ komutunu kullanarak bir VM ölçek kümesinden veri diski kaldırabilirsiniz. Örneğin hello aşağıdaki komut hello diski lun 2 tanımlı kaldırır.
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
Benzer şekilde, aynı zamanda bir diski bir ölçeği hello bir giriş kaldırarak Ayarla kaldırabilirsiniz _dataDisks_ hello özelliğinde _storageProfile_ ve hello değişiklik uygulama. 

## <a name="additional-notes"></a>Ek notlar
Destek eklenen veri disklerini Azure yönetilen diskleri ve ölçek kümesi için kullanılabilir'API sürümünde [ _2016-04-30-Önizleme_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) veya daha sonraki hello Microsoft.Compute API sürümü.

Merhaba ilk uygulamasında ölçek kümeleri bağlı disk desteğinin iliştiremezsiniz ya da veri diskleri için/ölçek kümesindeki tek tek sanal makineleri ayırma.

Ölçek kümelerindeki bağlı veri diskleri için Azure portalı desteği başlangıçta sınırlıydı. Azure şablonları kullanabilirsiniz gereksinimlerinize bağlı olarak, CLI, PowerShell, SDK'ları ve REST API toomanage diskleri bağlı.



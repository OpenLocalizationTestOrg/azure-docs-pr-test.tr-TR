---
title: "aaaUsing yönetilen diskler ile Azure sanal makine ölçek kümeleri | Microsoft Docs"
description: "Neden ve nasıl toouse diskler sanal makine ölçek kümesi ile yönetilen öğrenin"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a>Azure VM ölçek kümeleri ve yönetilen diskler

Azure [sanal makine ölçek kümeleri](/azure/virtual-machine-scale-sets/), yönetilen disklere sahip sanal makineleri destekler. Ölçek kümeleri ile birlikte yönetilen disklerin kullanılması aşağıdakiler gibi birçok avantaj sunar:

* Toopre artık ihtiyaç duymadığınız-oluşturun ve VM'ler hello ölçek kümesi için depolama hesapları toostore hello OS diskleri yönetme.

* Yönetilen veri diskleri toohello ölçek kümesi ekleyebilirsiniz.

* Yönetilen diskler sayesinde ölçek kümesinin kapasitesi, platform görüntüsü tabanlıysa 1.000 VM'e veya özel bir görüntü tabanlıysa 100 VM'e kadar çıkabilir.

## <a name="get-started"></a>başlarken

Basit bir yol yönetilen disk ölçek kümeleri ile başlatılan tooget hello Azure Portalı'ndan toodeploy değil. Daha fazla bilgi için [bu makaleye](./virtual-machine-scale-sets-portal-create.md) bakın. Başka bir basit yol başlatılan tooget olan toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy bir ölçek kümesi. Merhaba aşağıdaki örnekte nasıl toocreate bir Ubuntu ölçeği her bir 50 GB ve 100 GB veri diski 10 VM'ler ile Ayarla dayalı gösterilmektedir:

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

Alternatif olarak, hello görünebilir [Azure hızlı başlangıç şablonlarını GitHub deposuna](https://github.com/Azure/azure-quickstart-templates) içeren klasörleri için `vmss` toosee ölçek kümeleri dağıtmak şablonları örnekleri önceden oluşturulmuş. Hangi şablonları zaten yönetilen diskleri kullanarak tootell başvurabilirsiniz çok[bu listeyi](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).

## <a name="next-steps"></a>Sonraki adımlar

Yönetilen diskler hakkında daha fazla genel bilgi edinmek için [bu makaleye](../virtual-machines/windows/managed-disks-overview.md) bakın.

diskler, Resource Manager şablonu tooprovision ölçek ayarlar ile tooconvert yönetilen nasıl toosee bkz [bu makalede](./virtual-machine-scale-sets-convert-template-to-md.md). Merhaba aynı değişiklikleri toohello Resource Manager şablonları toohello Azure REST API de geçerlidir.

yönetilen veri diskleri ölçek kümeleri ile kullanma hakkında daha fazla toolearn bkz [bu makalede](./virtual-machine-scale-sets-attached-disks.md).

büyük ölçekli kümeleriyle çalışmak toobegin başvurmak çok[bu makalede](./virtual-machine-scale-sets-placement-groups.md).



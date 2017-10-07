---
title: "Azure yönetilen yukarı yedekleme için Disk aaaCopy | Microsoft Docs"
description: "Azure yönetilen diski toouse geri yukarı veya sorun giderme disk için bir kopyasını toocreate nasıl sorunları hakkında bilgi edinin."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Yönetilen bir Azure diski yönetilen anlık görüntülerini kullanarak tarafından depolanan VHD bir kopyasını oluşturun
Yönetilen disk yedekleme için bir anlık görüntüsünü veya yönetilen bir Disk hello anlık görüntüden oluşturmak ve tooa test sanal makinesi tootroubleshoot ekleyin. Yönetilen bir anlık görüntü yönetilen bir VM Disk noktası zaman tam kopyasıdır. Bu, VHD salt okunur bir kopyasını oluşturur ve isteğe bağlı olarak varsayılan olarak, standart yönetilen Disk olarak depolar. 

Fiyatlandırma hakkında daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/managed-disks/). <!--Add link tootopic or blog post that explains managed disks. -->

Her iki hello Azure portal veya hello Azure CLI 2.0 tootake hello yönetilen Disk görüntüsünü kullanın.

## <a name="use-azure-cli-20-tootake-a-snapshot"></a>Azure CLI 2.0 tootake bir anlık görüntü kullanın

> [!NOTE] 
> Merhaba aşağıdaki örnek hello Azure CLI 2.0 yüklü ve Azure hesabınızda oturum gerektirir.

Merhaba aşağıdaki adımları nasıl tooobtain Al yönetilen bir işletim sistemi görüntüsünü hello kullanarak disk ve Göster `az snapshot create` hello komutunu `--source-disk` parametresi. Merhaba aşağıdaki örneği adlı bir VM olduğunu varsayar `myVM` hello olarak yönetilen bir işletim sistemi diski ile oluşturulan `myResourceGroup` kaynak grubu.

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

Merhaba çıktı gibi görünmelidir:

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a>Azure portal tootake bir anlık görüntü kullanın 

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba sol üst köşede başlayarak, tıklatın **yeni** arayın ve **anlık görüntü**.
3. Başlangıç anlık görüntü dikey penceresinde tıklayın **oluşturma**.
4. Girin bir **adı** hello anlık görüntü için.
5. Var olan seçin [kaynak grubu](../../azure-resource-manager/resource-group-overview.md#resource-groups) veya yeni bir hello adını yazın. 
6. Azure veri merkezi konum seçin.  
7. İçin **kaynak disk**, hello yönetilen Disk toosnapshot seçin.
8. Select hello **hesap türü** toouse toostore hello anlık görüntü. Öneririz **Standard_LRS** yüksek performanslı bir diskte depolanan gerekmedikçe.
9. **Oluştur**'a tıklayın.

Yönetilen bir Disk toouse hello anlık görüntü toocreate planlamak ve toobe yüksek performanslı gereken VM ekleme, hello parametresini kullanmanız `--sku Premium_LRS` hello ile `az snapshot create` komutu. Bu hello anlık görüntü oluşturur, böylece yönetilen bir Premium Disk depolanır. Katı hal sürücüleri (SSD) olan ancak birden çok standart diskler (HDD'ler) maliyet premium yönetilen diskleri daha iyi gerçekleştirilemiyor.



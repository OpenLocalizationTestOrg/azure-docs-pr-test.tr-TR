---
title: "aaaAzure CLI komut dosyası örneği - yönetilen bir disk işletim sistemi diski olarak ekleyerek bir VM oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - yönetilen bir disk işletim sistemi diski olarak ekleyerek bir VM oluşturma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a>Mevcut yönetilen işletim sistemi diski ile CLI kullanarak bir sanal makine oluşturun

Bu komut dosyasını varolan yönetilen disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturur. Senaryolar önceki içinde bu komut dosyasını kullanın:
* Yönetilen bir diskten farklı Abonelikteki kopyalanan var olan bir diskten yönetilen işletim sistemi bir VM oluşturma
* Özel bir VHD dosyasından oluşturulmuş var olan bir diskten yönetilen bir VM oluşturma 
* Bir anlık görüntüden oluşturulmuş var olan bir diskten yönetilen işletim sistemi bir VM oluşturma 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını aşağıdaki komutları yönetilen tooget disk özelliklere hello kullanıyorsa, yönetilen disk tooa ekleme yeni VM ve VM oluşturun. Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az disk Göster](https://docs.microsoft.com/cli/azure/disk#show) | Disk adı ve kaynak grubu adı kullanarak yönetilen disk özelliklerini alır. ID özelliği olan kullanılan tooattach yönetilen disk tooa yeni VM |
| [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) | Yönetilen bir işletim sistemi diski kullanarak VM oluşturur |
## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

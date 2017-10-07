---
title: "aaaCreate ve DevTest Labs Azure CLI ile sanal makineleri yönetme | Microsoft Docs"
description: "Bilgi nasıl toouse Azure DevTest Labs toocreate ve Azure CLI 2.0 ile sanal makineleri yönetme"
services: devtest-lab,virtual-machines
documentationcenter: na
author: lisawong19
manager: douge
editor: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: liwong
ms.openlocfilehash: 98ea3aa7b2489bff61971573aaf584984cd811e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a>Oluşturma ve sanal makineleri DevTest Labs hello Azure CLI kullanarak yönetme
Bu hızlı başlangıç oluşturma, başlatma, bağlanma, güncelleştirme ve geliştirme makine laboratuvarınızda temizleniyor size yol gösterecektir. 

Başlamadan önce:

* Bir laboratuvar oluşturulmadığında, yönergeler bulunabilir [burada](devtest-lab-create-lab.md).

* [CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli). toostart, çalışma az oturum açma toocreate Azure ile bir bağlantı. 

## <a name="create-and-verify-hello-virtual-machine"></a>Oluşturma ve hello sanal makine doğrulayın 
Bir VM ile bir Market görüntüsünden ssh kimlik doğrulaması oluşturun.
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> Merhaba put **Laboratuvar'ın kaynak grubu** hello--kaynak-grubu parametre adı.
>

Bir formülü kullanılarak bir VM toocreate istiyorsanız, hello--formül parametresinde kullanın [az Laboratuvar vm oluşturma](https://docs.microsoft.com/cli/azure/lab/vm#create).


Bu hello VM kullanılabilir olduğunu doğrulayın.
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-toohello-virtual-machine"></a>Başlatın ve toohello sanal makineye bağlanın
VM başlatmak.
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> Merhaba put **Laboratuvar'ın kaynak grubu** hello--kaynak-grubu parametre adı.
>

Tooa VM bağlanın: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) veya [Uzak Masaüstü](../virtual-machines/windows/connect-logon.md).
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a>Güncelleştirme hello sanal makine
Yapıları tooa VM uygulayın.
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

Liste yapıları hello laboratuar ortamında kullanılabilir.
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a>Durdurun ve hello sanal makineyi silin    
Bir VM'yi durdurun.
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

Bir VM silin.
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]
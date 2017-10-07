---
title: "Linux için Azure sanal makine uzantısı aaaOMS | Microsoft Docs"
description: "Merhaba OMS Aracısı'nı bir sanal makine uzantısını kullanarak Linux sanal makine dağıtın."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a>Linux için OMS sanal makine uzantısı

## <a name="overview"></a>Genel Bakış

Operations Management Suite (OMS) bulut izleme, uyarma ve uyarı düzeltme özellikleri sağlar ve şirket içi varlıklar. Merhaba OMS Aracısı sanal makine uzantısı Linux için yayımlanan ve Microsoft tarafından desteklenmiyor. Merhaba uzantısı Azure sanal makinelerde hello OMS Aracısı'nı yükler ve sanal makineleri olan bir OMS çalışma kaydeder. Bu belge ayrıntıları hello platformları, yapılandırmaları ve dağıtım seçenekleri Linux için OMS sanal makine uzantısı hello için desteklenir.

## <a name="prerequisites"></a>Ön koşullar

### <a name="operating-system"></a>İşletim sistemi

Merhaba OMS Aracısı uzantısı bu Linux dağıtımları karşı çalıştırabilirsiniz.

| Dağıtım | Sürüm |
|---|---|
| CentOS Linux | 5, 6 ve 7 |
| Oracle Linux | 5, 6 ve 7 |
| Red Hat Enterprise Linux Server | 5, 6 ve 7 |
| Debian GNU/Linux | 6, 7 ve 8 |
| Ubuntu | 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS |
| SUSE Linux Enterprise Server | 11 ve 12 |

### <a name="internet-connectivity"></a>İnternet bağlantısı

Linux için OMS aracısının uzantısı Hello gerektirir hello hedef sanal makinenin bağlı toohello Internet. 

## <a name="extension-schema"></a>Uzantı Şeması

Merhaba aşağıdaki JSON hello OMS Aracısı uzantısı için hello şema gösterir. Merhaba uzantısı hello hedef OMS çalışma alanından hello çalışma alanı kimliği ve çalışma alanı anahtarı gerekiyor; Bu değerleri hello OMS portalında bulunabilir. Merhaba çalışma alanı anahtarı hassas verileri olarak değerlendirilmesi için bir korumalı ayarı yapılandırmasında depolanması gerekir. Azure VM uzantısının korumalı ayarı veri şifrelenir ve yalnızca hello hedef sanal makineye şifresi. Unutmayın **Workspaceıd** ve **workspaceKey** büyük küçük harfe duyarlıdır.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a>Özellik değerleri

| Ad | Değer / örnek |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Yayımcı | Microsoft.EnterpriseCloud.Monitoring |
| type | OmsAgentForLinux |
| typeHandlerVersion | 1.4 |
| Workspaceıd (örneğin) | 6f680a37-00c6-41C7-a93f-1437e3462574 |
| workspaceKey (örneğin) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ == |


## <a name="template-deployment"></a>Şablon dağıtımı

Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir. Şablonları, bir veya daha fazla ekleme tooOMS gibi dağıtım yapılandırma sonrası gerektiren sanal makineler dağıtırken idealdir. Merhaba OMS Aracısı VM uzantısı içeren bir örnek Resource Manager şablonunu hello üzerinde bulunabilir [Azure hızlı başlangıç Galerisi](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm). 

sanal makine uzantısı Hello JSON yapılandırması hello sanal makine kaynağı içinde iç içe geçmiş veya hello kök veya Resource Manager JSON şablonu en üst düzeyinde yerleştirilir. Merhaba JSON yapılandırma Hello yerleşimini hello değeri hello kaynak adı ve türü etkiler. Daha fazla bilgi için bkz: [Ayarla alt kaynakları için ad ve tür](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Merhaba aşağıdaki örneği hello OMS uzantısı hello sanal makine kaynağı içinde iç içe geçmiş varsayar. Merhaba uzantısı kaynak iç içe geçirme sırasında hello JSON hello yerleştirilir `"resources": []` hello sanal makinenin nesnesi.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

Merhaba uzantısı JSON hello hello şablon kökünde yerleştirirken başvuru toohello üst sanal makinesini hello kaynak adı içerir ve hello türü hello iç içe geçmiş yapılandırma yansıtır.  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a>Azure CLI dağıtım

Hello Azure CLI kullanılan toodeploy hello OMS Aracısı VM uzantısı tooan varolan sanal makine olabilir. Merhaba OMS anahtarı ve OMS kimliği bu OMS çalışma alanınız ile değiştirin. 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a>Sorun giderme ve Destek

### <a name="troubleshoot"></a>Sorun giderme

Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure CLI kullanarak alınabilir. toosee hello dağıtım durumu uzantılarının komutunu kullanarak aşağıdaki hello çalıştırmak, belirli bir VM için Azure CLI hello.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Uzantı yürütme oturum toohello aşağıdaki dosyasına çıktı:

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a>Hata kodları ve anlamları

| Hata kodu | Anlamı | Olası eylemi |
| :---: | --- | --- |
| 10 | VM zaten bağlı tooan OMS çalışma | tooconnect hello VM toohello çalışma Hello uzantısı şemasında belirtilen stopOnMultipleConnections toofalse ortak ayarlar bölümünden veya bu özelliği kaldırın. Bu VM için bağlı her çalışma alanı için bir kez fatura. |
| 11 | Sağlanan geçersiz config toohello uzantısı | Örnekler tooset dağıtımı için gerekli tüm özellik değerlerini önceki hello izleyin. |
| 12 | Merhaba dpkg Paket Yöneticisi kilitli | Tamamlandı ve yeniden deneyin tüm dpkg güncelleştirme makine üzerindeki işlemleri hello emin olun. |
| 20 | Erken adlı etkinleştir | [Güncelleştirme hello Azure Linux Aracısı](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello en son sürüme. |
| 51 | Bu uzantı hello VM'in işlemi sistemde desteklenmiyor | |
| 55 | Toohello Microsoft Operations Management Suite hizmetine bağlanılamıyor | Hello sistem ya da Internet erişimi veya geçerli bir HTTP proxy sağlanmış sahip olduğunu denetleyin. Ayrıca, hello çalışma alanı kimliği hello doğruluğunu denetleyin |

Ek sorun giderme bilgileri hello üzerinde bulunabilir [Linux için OMS Aracısı sorun giderme kılavuzu](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).

### <a name="support"></a>Destek

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz hello Azure uzmanlarıyla hello [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin. Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).

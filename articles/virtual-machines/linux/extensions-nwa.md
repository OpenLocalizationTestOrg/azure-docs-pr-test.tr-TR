---
title: "Linux için Ağ İzleyicisi Aracısı sanal makine uzantısı aaaAzure | Microsoft Docs"
description: "Bir sanal makine uzantısını kullanarak Linux sanal makine üzerinde Ağ İzleyicisi Aracısı Hello dağıtın."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a>Linux için Ağ İzleyicisi Aracısı sanal makine uzantısı

## <a name="overview"></a>Genel Bakış

[Azure Ağ İzleyicisi](https://review.docs.microsoft.com/en-us/azure/network-watcher/) Azure ağları için izleme sağlayan bir ağ performans izleme, tanılama ve analiz hizmetidir. Ağ İzleyicisi Aracısı sanal makine uzantısı Hello Azure sanal makinelerde hello Ağ İzleyicisi özelliklerinden bazıları için gerekli değildir. Bu, isteğe bağlı ve diğer gelişmiş işlevler üzerindeki ağ trafiğini yakalama içerir.

Bu belge ayrıntıları hello platformları ve dağıtım seçenekleri Linux için Ağ İzleyicisi Aracısı sanal makine uzantısı hello için desteklenmiyor.

## <a name="prerequisites"></a>Ön koşullar

### <a name="operating-system"></a>İşletim sistemi

Ağ İzleyicisi Aracısı uzantısı Hello bu Linux dağıtımları karşı çalıştırabilirsiniz:

| Dağıtım | Sürüm |
|---|---|
| Ubuntu | 16.04 LTS, 14.04 LTS ve 12.04 LTS |
| Debian | 7 ve 8 |
| RedHat | 6.x ve 7.x |
| Oracle Linux | 7 x |
| SuSE | 11 ve 12 |
| OpenSuse | 7.0 |
| CentOS | 7.0 |

CoreOS şu anda desteklenmediğini unutmayın.

### <a name="internet-connectivity"></a>İnternet bağlantısı

Merhaba Ağ İzleyicisi Aracısı işlevleri bazıları hello hedef sanal makinenin bağlı toohello Internet olması gerekir. Merhaba özelliği tooestablish giden bağlantılar hello Ağ İzleyicisi Aracısı özelliklerden bazıları düzgün çalışmamasına veya kullanılamaz hale. Daha fazla ayrıntı için lütfen bkz hello [Ağ İzleyicisi belgeleri](https://review.docs.microsoft.com/en-us/azure/network-watcher/).

## <a name="extension-schema"></a>Uzantı Şeması

Merhaba aşağıdaki JSON hello Ağ İzleyicisi Aracısı uzantısı için hello şema gösterir. Merhaba uzantısı ne gerektirir ya da şu anda herhangi bir kullanıcı tarafından sağlanan ayarını destekler ve kendi varsayılan yapılandırmasına dayanır.

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>Özellik değerleri

| Ad | Değer / örnek |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Yayımcı | Microsoft.Azure.NetworkWatcher |
| type | NetworkWatcherAgentLinux |
| typeHandlerVersion | 1.4 |

## <a name="template-deployment"></a>Şablon dağıtımı

Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir. Merhaba JSON şeması Hello önceki bölümde ayrıntılı bir Azure Resource Manager şablon dağıtımı sırasında bir Azure Resource Manager şablonu toorun hello Ağ İzleyicisi Aracısı uzantısı kullanılabilir.

## <a name="azure-cli-deployment"></a>Azure CLI dağıtım

Hello Azure CLI kullanılan toodeploy hello Ağ İzleyicisi Aracısı VM uzantısı tooan varolan sanal makine olabilir.

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a>Sorun giderme ve destek

### <a name="troubleshooting"></a>Sorun giderme

Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure CLI kullanarak alınabilir. toosee hello dağıtım durumu uzantılarının komutunu kullanarak aşağıdaki hello çalıştırmak, belirli bir VM için Azure CLI hello.

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

Uzantı yürütme hello bulunan oturum toofiles directory aşağıdaki çıktı:

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a>Destek

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, toohello Ağ İzleyicisi belgelere bakın veya hello Azure başvurun hello uzmanlarıyla [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin. Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).

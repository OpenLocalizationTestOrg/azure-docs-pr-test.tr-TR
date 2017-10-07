---
title: "aaaEnable veya Azure VM izleme devre dışı bırakma"
description: "Açıklar nasıl tooEnable veya Azure VM izlemeyi devre dışı bırak"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Etkinleştirmek veya Azure VM izleme devre dışı bırakma

Bu bölümde, nasıl Azure üzerinde çalışan tooenable veya izleme devre dışı üzerinde sanal makineleri açıklanmaktadır. Etkinleştirmek veya Mac, Linux ve Windows (hello Azure CLI) için hello portalı veya Azure komut satırı arabirimi kullanarak izlemeyi devre dışı bırakın.

> [!IMPORTANT]
> Bu belgede hello Linux tanılama kullanım dışı bırakılmış uzantısının 2.3 sürümü açıklanmaktadır. Sürüm 2.3 30 Haziran 2018 kadar desteklenmez.
>
> Merhaba Linux tanılama uzantısını 3.0 sürümü yerine etkinleştirilebilir. Daha fazla bilgi için bkz: [hello belgelerine](./diagnostic-extension.md).

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a>Etkinleştir / Azure portal hello izlemeyi devre dışı bırak

1 dakikalık dönemlerini örneğinizi hakkında veriler sağlayan Azure VM'yi, izlemeyi etkinleştirebilirsiniz. (depolama değişiklikler uygulanır). Ayrıntılı tanılama verilerini, ardından hello VM hello portal grafiklerde veya hello API aracılığıyla kullanılabilir. Varsayılan olarak, Azure portal, ölçümleri sınırlı sayıda ana bilgisayar tabanlı izleme sağlar. VM çalıştıran hello veya durdurulmuş durumdaki bir VM içinde ölçümleri izleme etkinleştirebilirsiniz.

* Açık hello Azure portal adresindeki [https://portal.azure.com](https://portal.azure.com).
* Sol gezinti hello, sanal makineleri'ı tıklatın.
* Hello listesi sanal makinelerde çalışan veya durdurulmuş bir örnek seçin. Merhaba "Sanal makine" dikey pencere açılır.
* Tüm ayarlar'ı tıklatın.
* Tanılama'yı tıklatın.
* Değişiklik durumu tooOn veya kapalı. Ayrıntılar için sanal makine tooenable ister misiniz izleme bu dikey penceresinde hello düzeyindeki seçebilirsiniz.

![Etkinleştir / hello Azure portal izleme devre dışı bırakın.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Etkinleştir / Azure CLI ile izleme devre dışı bırak

tooenable bir Azure VM için izleme.

* (PrivateConfig.json gibi adlandırılmış) dosyası oluşturun:

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* Azure CLI aracılığıyla Hello uzantıyı etkinleştirin.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

Daha fazla bilgi için bkz: [Linux tanılama uzantısını kullanarak tooMonitor Linux sanal makinenin performans ve tanılama verilerini](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png

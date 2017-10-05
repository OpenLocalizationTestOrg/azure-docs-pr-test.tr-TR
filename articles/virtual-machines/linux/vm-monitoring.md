---
title: "Etkinleştirme veya Azure VM izleme devre dışı bırakma"
description: "Etkinleştirmek veya Azure VM izlemeyi devre dışı açıklar"
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
ms.openlocfilehash: 9b2fe579113d6ca6bfd27d82eb9d4657657d44ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Etkinleştirmek veya Azure VM izleme devre dışı bırakma

Bu bölümde, etkinleştirme veya Azure üzerinde çalışan sanal makinelerde izleme devre dışı açıklar. Etkinleştirmek veya Mac, Linux ve Windows (Azure CLI) için portal veya Azure komut satırı arabirimi kullanarak izlemeyi devre dışı bırakın.

> [!IMPORTANT]
> Bu belge Linux tanılama kullanım dışı bırakılmış uzantısının 2.3 sürümünü açıklar. Sürüm 2.3 30 Haziran 2018 kadar desteklenmez.
>
> Linux tanılama uzantısını 3.0 sürümü yerine etkinleştirilebilir. Daha fazla bilgi için bkz: [belgelerine](./diagnostic-extension.md).

## <a name="enable--disable-monitoring-through-the-azure-portal"></a>Etkinleştir / Azure portalı üzerinden izleme devre dışı bırak

1 dakikalık dönemlerini örneğinizi hakkında veriler sağlayan Azure VM'yi, izlemeyi etkinleştirebilirsiniz. (depolama değişiklikler uygulanır). Ayrıntılı tanılama verilerini sonra portal grafiklerde veya API'si aracılığıyla sanal makine için kullanılabilir. Varsayılan olarak, Azure portal, ölçümleri sınırlı sayıda ana bilgisayar tabanlı izleme sağlar. Ölçümleri VM çalışırken bir VM içinde veya durdurulmuş durumdaki izlemesini etkinleştirebilirsiniz.

* Azure portalında açmak [https://portal.azure.com](https://portal.azure.com).
* Sol gezinti bölmesinde, sanal makineleri'ı tıklatın.
* Liste sanal makineleri bir çalışıyor veya durdurulmuştur örneği seçin. "Sanal makine" dikey pencere açılır.
* Tüm ayarlar'ı tıklatın.
* Tanılama'yı tıklatın.
* Durum açık veya kapalı değiştirin. Bu dikey pencerede etkinleştirmek için sanal makine istediğiniz ayrıntıları izleme düzeyini de seçebilirsiniz.

![Etkinleştir / Azure portalı üzerinden izleme devre dışı bırakın.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Etkinleştir / Azure CLI ile izleme devre dışı bırak

Bir Azure VM için izlemeyi etkinleştirmek için.

* (PrivateConfig.json gibi adlandırılmış) dosyası oluşturun:

```json
{
        "storageAccountName":"the storage account to receive data",
        "storageAccountKey":"the key of the account"
}
```

* Azure CLI aracılığıyla uzantıyı etkinleştirin.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

Daha fazla bilgi için bkz: [Linux tanılama uzantısını kullanarak İzleyici Linux sanal makinenin performans ve tanı veri](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png

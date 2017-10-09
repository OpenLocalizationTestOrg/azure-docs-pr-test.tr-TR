---
title: "aaaAzure CLI komut dosyası örneği - uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>Uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme

Bu komut dosyası, bir kaynak grubu, iki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur. Merhaba uygulaması hello birincil bölgede kullanılamaz duruma geldiğinde traffic Manager trafik toohello uygulamada hello birincil bölge olarak tek bir bölge ve toohello ikincil bölge yönlendirir. Hello betiği yürütülürken önce hello mywebapp şeklindedir, MyWebAppL1 değiştirmeniz gerekir ve Azure arasında toounique değerleri MyWebAppL2 değerleri. Hello komut dosyasını çalıştırdıktan sonra hello birincil bölge hello URL mywebapp.trafficmanager.net ile Merhaba uygulamasında erişebilir.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Merhaba komut dosyası örneği çalıştırdıktan sonra hello izleyin komutu kullanılan tooremove hello kaynak grubu, App Service uygulaması ve tüm ilişkili kaynakları olabilir.

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını aşağıdaki komutları toocreate bir kaynak grubu, web uygulaması, trafik Yöneticisi profili hello kullanır ve ilişkili tüm kaynakları. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) | App Service planı oluşturur. Bu, Azure web uygulamanız için bir sunucu grubu gibidir. |
| [az appservice web oluşturma](https://docs.microsoft.com/cli/azure/appservice/web#create) | Merhaba uygulama hizmeti planı içinde Azure web uygulaması oluşturur. |
| [az ağ trafik Yöneticisi profili oluştur](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Bir Azure Traffic Manager profilini oluşturur. |
| [az ağ trafik Yöneticisi uç noktası oluşturma](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | Uç nokta tooan Azure trafik Yöneticisi profili ekler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure ağ belgeleri](../cli-samples.md).

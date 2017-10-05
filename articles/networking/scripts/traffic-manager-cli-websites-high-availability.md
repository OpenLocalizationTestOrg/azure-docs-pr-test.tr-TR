---
title: "Azure CLI komut dosyası örneği - uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme | Microsoft Docs"
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
ms.openlocfilehash: 0593d063a4935d02aae124d83b62b11e37aa3c33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>Uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme

Bu komut dosyası, bir kaynak grubu, iki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur. Birincil bölge uygulamada kullanılamadığında trafik Yöneticisi bir bölgede birincil bölge olarak uygulama ve ikincil bölge trafiğini yönlendirir. Komut yürütülmeden önce Azure arasında benzersiz değerler mywebapp şeklindedir, MyWebAppL1 ve MyWebAppL2 değerleri değiştirmelisiniz. Betiği çalıştırdıktan sonra uygulama URL'si mywebapp.trafficmanager.net ile birincil bölgede erişebilir.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[Ana](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "yüksek kullanılabilirlik için trafiği yönlendirmek")]


## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Komut dosyası örneği çalıştırdıktan sonra izleme komutu kaynak grubu, App Service uygulaması kaldırmak için kullanılabilir ve tüm kaynakları ilgili.

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut, bir kaynak grubu, web uygulaması, trafik Yöneticisi profili ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) | App Service planı oluşturur. Bu, Azure web uygulamanız için bir sunucu grubu gibidir. |
| [az appservice web oluşturma](https://docs.microsoft.com/cli/azure/appservice/web#create) | Uygulama hizmeti planı içinde Azure web uygulaması oluşturur. |
| [az ağ trafik Yöneticisi profili oluştur](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Bir Azure Traffic Manager profilini oluşturur. |
| [az ağ trafik Yöneticisi uç noktası oluşturma](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | Bir uç noktası için bir Azure Traffic Manager profili ekler. |

## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek uygulama hizmeti CLI kod örnekleri bulunabilir [Azure ağ belgeleri](../cli-samples.md).

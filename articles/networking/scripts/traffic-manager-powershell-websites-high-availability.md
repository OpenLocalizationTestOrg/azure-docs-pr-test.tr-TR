---
title: "PowerShell komut dosyası örneği - uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme aaaAzure | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>Uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme

Bu komut dosyası, bir kaynak grubu, iki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur. Merhaba uygulaması hello birincil bölgede kullanılamaz duruma geldiğinde traffic Manager trafik toohello uygulamada hello birincil bölge olarak tek bir bölge ve toohello ikincil bölge yönlendirir. Hello betiği yürütülürken önce hello mywebapp şeklindedir, MyWebAppL1 değiştirmeniz gerekir ve Azure arasında toounique değerleri MyWebAppL2 değerleri. Hello komut dosyasını çalıştırdıktan sonra hello birincil bölge hello URL mywebapp.trafficmanager.net ile Merhaba uygulamasında erişebilir.

Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını aşağıdaki komutları toocreate bir kaynak grubu, web uygulaması, trafik Yöneticisi profili hello kullanır ve ilişkili tüm kaynakları. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [AzureRmAppServicePlan yeni](/powershell/module/azurerm.websites/new-azurermappserviceplan) | App Service planı oluşturur. Bu, Azure web uygulamanız için bir sunucu grubu gibidir. |
| [AzureRmWebApp yeni](/powershell/module/azurerm.websites/new-azurermwebapp) | Merhaba uygulama hizmeti planı içinde Azure web uygulaması oluşturur. |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/new-azurermresource) | Merhaba uygulama hizmeti planı içinde Azure web uygulaması oluşturur. |
| [AzureRmTrafficManagerProfile yeni](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | Bir Azure Traffic Manager profilini oluşturur. |
| [AzureRmTrafficManagerEndpoint yeni](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | Uç nokta tooan Azure trafik Yöneticisi profili ekler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).

Ek ağ PowerShell komut dosyası örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).

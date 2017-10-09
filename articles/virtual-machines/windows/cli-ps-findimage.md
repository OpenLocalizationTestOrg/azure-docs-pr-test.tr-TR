---
title: "aaaSelect Windows VM görüntüleri Azure'da | Microsoft Docs"
description: "Toouse Azure PowerSHell toodetermine nasıl hello publisher, teklif, SKU ve sürümü Market VM görüntüleri öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a>Nasıl hello Azure PowerShell ile Azure Marketi içinde toofind Windows VM görüntüleri

Bu konuda nasıl hello Azure Marketi toouse Azure PowerShell toofind VM görüntüleri açıklanmaktadır. Bir Windows VM oluşturduğunuzda, bu bilgileri toospecify bir Market görüntüsü kullanın.

Yüklü ve hello son yapılandırıldığından emin olun [Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).



## <a name="table-of-commonly-used-windows-images"></a>Yaygın olarak kullanılan Windows görüntülerinin tablosu
| PublisherName | Sunduğu | Sku |
|:--- |:--- |:--- |:--- |
| MicrosoftWindowsServer |WindowsServer |2016 Datacenter |
| MicrosoftWindowsServer |WindowsServer |Veri Merkezi Sunucu Çekirdek 2016 |
| MicrosoftWindowsServer |WindowsServer |Kapsayıcılar ile 2016 Datacenter |
| MicrosoftWindowsServer |WindowsServer |2016 Nano Server |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2008 R2 SP1 |
| MicrosoftDynamicsNAV |DynamicsNAV |2017 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2016 |
| MicrosoftSQLServer |SQL2016 WS2016 |Enterprise |
| MicrosoftSQLServer |SQL2014SP2 WS2012R2 |Enterprise |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |

## <a name="find-specific-images"></a>Belirli görüntüleri bulma


Azure Resource Manager ile yeni bir sanal makine oluştururken, bazı durumlarda, toospecify görüntünün görüntü özelliklerini aşağıdaki hello hello birlikte gerekir:

* Yayımcı
* Sunduğu
* SKU

Örneğin, bu değerleri ile Merhaba kullanın [kümesi AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet'ini veya bir kaynak grubu şablonu içinde belirtmelisiniz oluşturulan VM toobe hello türü.

Bu değerleri toodetermine gerekiyorsa, hello çalıştırabilirsiniz [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), ve [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlet'leri toonavigate hello görüntüler. Bu değerler belirler:

1. Liste hello görüntü yayımcılar.
2. Belirli bir yayımcı varsa yayımcının tekliflerini listeleyin.
3. Belirli bir teklif varsa SKU’larını listeleyin.

İlk olarak, aşağıdaki komutları hello ile hello yayımcılar listesi:

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

Seçilen yayımcı adınızı doldurmanız ve hello aşağıdaki komutları çalıştırın:

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Seçilen teklif adınızı doldurun ve hello aşağıdaki komutları çalıştırın:

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Merhaba, hello çıktısından `Get-AzureRMVMImageSku` komut, tüm hello bilgilerin için yeni bir sanal makine toospecify hello görüntü gerekir.

Merhaba aşağıdaki tam bir örnek gösterilmektedir:

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

Çıktı:

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

Merhaba "MicrosoftWindowsServer" publisher için:

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Çıktı:

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

"Windows Server" Merhaba sunar:

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Çıktı:

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

Bu listeden SKU Adı Seçilen hello kopyalayın ve hello tüm hello bilgisine sahip `Set-AzureRMVMSourceImage` PowerShell cmdlet'ini veya bir kaynak grubu şablonu için.

## <a name="next-steps"></a>Sonraki adımlar
Tam olarak hello görüntüsünü seçebilirsiniz artık toouse istiyor. yalnızca bulundu, hello görüntü bilgileri kullanarak hızlı bir şekilde bir sanal makine toocreate bkz [PowerShell ile Windows sanal makine oluşturma](quick-create-powershell.md).

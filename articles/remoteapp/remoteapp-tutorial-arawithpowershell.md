---
title: Azure RemoteApp PowerShell cmdlet'leriyle aaaUse | Microsoft Docs
description: "Bilgi nasıl toouse Azure RemoteApp Windows PowerShell cmdlet'leri."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Azure RemoteApp ile Windows PowerShell cmdlet'lerini kullanma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

 Koleksiyonunuz korumak ve hello Azure RemoteApp PowerShell cmdlet'leri tooadminister kullanın. Başlatılan bilgi tooget aşağıdaki hello kullanın.

## <a name="get-hello-cmdlets"></a>Merhaba cmdlet'lerini alma
- - -
İlk hello Azure Powershell cmdlet'lerini indirin [burada](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlet'lerini içine dahil edilir. 

Merhaba denetleyin [Azure RemoteApp cmdlet Yardım](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a>Aboneliğiniz Azure cmdlet'lerini toouse yapılandırın
- - -
İzleyin [bu kılavuzda](/powershell/azure/overview) hello cmdlet'leri, Azure aboneliğinizin karşı kullanabilirsiniz.

Bu adımları tooget hızlı şekilde kullanmaya kullanabilirsiniz:

1. Merhaba yükleyip [Azure PowerShell cmdlet'lerini](http://go.microsoft.com/?linkid=9811175).
2. Microsoft Azure PowerShell'i başlatın.
3. Çalıştırma **Add-AzureAccount** tooauthenticate tooyour Azure aboneliği. İstendiğinde, girin hello aynı kullanıcı adı ve parola tooAzure Portalı'nda toosign kullanın.  
4. Çalıştırma **Get-AzureSubscription** kullanıcı hesabınızla ilişkili toolist hello abonelik. 
5. Çalıştırma **Select-AzureSubscription - varlığıyla SubscriptionName &lt;abonelik adı&gt;**  veya **Select-AzureSubscription - Subscriptionıd &lt;abonelik kimliği&gt;**  toospecify hello abonelik toouse.

Tebrikler, Azure PowerShell konsolunuza yapılandırılmış ve hazır toouse. Merhaba hello Azure PowerShell konsolunda her başlattığınızda toorepeate adımları 2'den 5 gerekir unutmayın.  


## <a name="list-all-collections"></a>Tüm koleksiyonları listesi
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Bir koleksiyonu silin
- - -
    Remove-AzureRemoteAppCollection<enter collection name>

Örnek: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Bulut koleksiyonu oluşturma
- - -
Merhaba aşağıdaki komutu çalıştırın, basittir:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

Yukarıdaki komut Hello Microsoft Office 365 uygulamaları (Excel, OneNote, Outlook, PowerPoint, Visio ve Word) otomatik olarak yayımlar.

Koleksiyon oluşturma 30 dakika veya daha uzun toocomplete alabilir. Bu nedenle, bu komut aşağıdaki gibi kullanabilirsiniz izleme kimliği döndürür:

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Merhaba koleksiyonu yapıldıktan sonra komutu aşağıdaki hello ile kullanıcı toohello toplama ekleyebilirsiniz:

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

Ve bitirdiniz! Bu kullanıcının bulunan hello Azure RemoteApp istemcisini kullanarak mümkün tooconnect toohello application olmalıdır. [burada](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Kullanılabilen cmdlet'ler
Çok sayıda sahibiz diğer komutlar vardır, bunları hello belgelerine kısa bir süre sonra gelen:

Temel RemoteApp koleksiyonu cmdlet: 

* New-AzureRemoteAppCollection
* Get-AzureRemoteAppCollection
* Set-AzureRemoteAppCollection
* Update-AzureRemoteAppCollection
* Remove-AzureRemoteAppCollection
* Add-AzureRemoteAppUser
* Get-AzureRemoteAppUser
* Remove-AzureRemoteAppUser
* Get-AzureRemoteAppSession
* Disconnect-AzureRemoteAppSession
* Invoke-AzureRemoteAppSessionLogoff
* Send-AzureRemoteAppSessionMessage
* Get-AzureRemoteAppProgram
* Get-AzureRemoteAppStartMenuProgram
* Publish-AzureRemoteAppProgram
* Unpublish-AzureRemoteAppProgram
* Get-AzureRemoteAppCollectionUsageDetails
* Get-AzureRemoteAppCollectionUsageSummary
* Get-AzureRemoteAppPlan

RemoteApp sanal ağı cmdlet:

* New-AzureRemoteAppVNet
* Get-AzureRemoteAppVNet
* Set-AzureRemoteAppVNet
* Remove-AzureRemoteAppVNet
* Get-AzureRemoteAppVpnDevice
* Get--AzureRemoteAppVpnDeviceConfigScript
* Reset-AzureRemoteAppVpnSharedKey

RemoteApp şablon görüntüsü cmdlet:

* New-AzureRemoteAppTemplateImage
* Get-AzureRemoteAppTemplateImage
* Rename-AzureRemoteAppTemplateImage
* Remove-AzureRemoteAppTemplateImage

Diğer RemoteApp cmdlet'lerini:

* Get-AzureRemoteAppLocation
* Get-AzureRemoteAppWorkspace
* Set-AzureRemoteAppWorkspace
* Get-AzureRemoteAppOperationResult


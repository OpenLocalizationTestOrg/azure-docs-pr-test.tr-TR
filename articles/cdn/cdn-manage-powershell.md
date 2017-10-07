---
title: PowerShell ile Azure CDN aaaManage | Microsoft Docs
description: "Nasıl toouse hello Azure PowerShell cmdlet'leri toomanage Azure CDN öğrenin."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: fb6f57a5-6e26-4847-8fd9-b51fb05a79eb
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269373136d4ef018e4d31f147456b4be2253b463
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-with-powershell"></a>Azure CDN PowerShell ile yönetme
PowerShell hello en esnek yöntemler toomanage birini Azure CDN profili ve uç noktaları sağlar.  Etkileşimli olarak veya tooautomate yönetim görevlerini komut dosyaları yazarak PowerShell'i kullanabilirsiniz.  Bu öğretici birkaç gösterir hello en yaygın görevlerin PowerShell toomanage ile Azure CDN profili ve uç noktaları gerçekleştirebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar
toouse PowerShell toomanage Azure CDN profili ve uç noktaları, hello Azure PowerShell Modülü yüklü olması gerekir.  toolearn nasıl tooinstall Azure PowerShell ve tooAzure hello kullanarak bağlanmak `Login-AzureRmAccount` cmdlet'ini bkz [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

> [!IMPORTANT]
> İle oturum açmanız gerekir `Login-AzureRmAccount` Azure PowerShell cmdlet'lerini çalıştırmadan önce.
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a>Hello Azure CDN cmdlet'leri listeleme
Hello kullanarak tüm hello Azure CDN cmdlet'leri listelediğiniz `Get-Command` cmdlet'i.

```text
PS C:\> Get-Command -Module AzureRM.Cdn

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Get-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpointNameAvailability             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfileSsoUrl                        2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Publish-AzureRmCdnEndpointContent                  2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnCustomDomain                      2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnEndpoint                          2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnProfile                           2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Start-AzureRmCdnEndpoint                           2.0.0      AzureRm.Cdn
Cmdlet          Stop-AzureRmCdnEndpoint                            2.0.0      AzureRm.Cdn
Cmdlet          Test-AzureRmCdnCustomDomain                        2.0.0      AzureRm.Cdn
Cmdlet          Unpublish-AzureRmCdnEndpointContent                2.0.0      AzureRm.Cdn
```

## <a name="getting-help"></a>Yardım alma
Herhangi bir hello kullanarak bu cmdlet'leri ile Yardım alabilirsiniz `Get-Help` cmdlet'i.  `Get-Help`Kullanım ve sözdizimi sağlar ve isteğe bağlı olarak örnekler gösterilmektedir.

```text
PS C:\> Get-Help Get-AzureRmCdnProfile

NAME
    Get-AzureRmCdnProfile

SYNOPSIS
    Gets an Azure CDN profile.


SYNTAX
    Get-AzureRmCdnProfile [-ProfileName <String>] [-ResourceGroupName <String>] [-InformationAction
    <ActionPreference>] [-InformationVariable <String>] [<CommonParameters>]


DESCRIPTION
    Gets an Azure CDN profile and all related information.


RELATED LINKS

REMARKS
    toosee hello examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a>Liste mevcut Azure CDN profili
Merhaba `Get-AzureRmCdnProfile` cmdlet parametre olmadan tüm mevcut CDN profili alır.

```powershell
Get-AzureRmCdnProfile
```

Bu çıktı yöneltilen toocmdlets numaralandırması için olabilir.

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

Ayrıca hello profilinin adını ve kaynak grubu belirterek tek bir profil geri dönebilirsiniz.

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> Farklı kaynak gruplarında oldukları sürece birden çok CDN ile aynı adı, hello profilleri olası toohave olur.  Merhaba atlama `ResourceGroupName` parametresi eşleşen bir ada sahip tüm profillerini döndürür.
> 
> 

## <a name="listing-existing-cdn-endpoints"></a>Liste mevcut CDN uç noktası
`Get-AzureRmCdnEndpoint`tek bir uç nokta veya bir profildeki tüm hello uç noktaları alabilir.  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of hello endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of hello endpoints on all of hello profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of hello endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a>CDN profili ve uç noktaları oluşturma
`New-AzureRmCdnProfile`ve `New-AzureRmCdnEndpoint` kullanılan toocreate CDN profili ve uç noktaları.

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a>Uç nokta ad kullanılabilirliğini denetleme
`Get-AzureRmCdnEndpointNameAvailability`bir uç nokta adı olup olmadığını gösteren bir nesne döndürür.

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a>Özel bir etki alanı ekleme
`New-AzureRmCdnCustomDomain`bir özel etki alanı adı tooan mevcut uç ekler.

> [!IMPORTANT]
> CNAME hello açıklandığı gibi DNS sağlayıcınız ile ayarlamalısınız [nasıl toomap özel etki alanı tooContent teslim ağı (CDN) uç noktası](cdn-map-content-to-custom-domain.md).  Merhaba eşleme kullanan uç noktasını değiştirmeden önce sınayabilirsiniz `Test-AzureRmCdnCustomDomain`.
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check hello mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create hello custom domain on hello endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a>Bir uç nokta değiştirme
`Set-AzureRmCdnEndpoint`Mevcut bir uç noktası değiştirir.

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a>Temizleme/öncesi-loading CDN varlıklar
`Unpublish-AzureRmCdnEndpointContent`temizler varlıklar, önbelleğe alınmış durumdayken `Publish-AzureRmCdnEndpointContent` desteklenen uç noktasında varlıkları önceden yükler.

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a>Başlatma/durdurma CDN uç noktası
`Start-AzureRmCdnEndpoint`ve `Stop-AzureRmCdnEndpoint` kullanılan toostart kullanılabilir ve tekil uç noktalarını ya da grupları uç noktaları durdurun.

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a>CDN kaynakları silme
`Remove-AzureRmCdnProfile`ve `Remove-AzureRmCdnEndpoint` kullanılan tooremove profilleri ve uç noktaları olabilir.

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a>Sonraki Adımlar
Bilgi nasıl tooautomate Azure CDN ile [.NET](cdn-app-dev-net.md) veya [Node.js](cdn-app-dev-node.md).

toolearn CDN özellikleri hakkında bkz [CDN'ye genel bakış](cdn-overview.md).


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
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="c531b-103">Azure CDN PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="c531b-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="c531b-104">PowerShell hello en esnek yöntemler toomanage birini Azure CDN profili ve uç noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="c531b-104">PowerShell provides one of hello most flexible methods toomanage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="c531b-105">Etkileşimli olarak veya tooautomate yönetim görevlerini komut dosyaları yazarak PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c531b-105">You can use PowerShell interactively or by writing scripts tooautomate management tasks.</span></span>  <span data-ttu-id="c531b-106">Bu öğretici birkaç gösterir hello en yaygın görevlerin PowerShell toomanage ile Azure CDN profili ve uç noktaları gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c531b-106">This tutorial demonstrates several of hello most common tasks you can accomplish with PowerShell toomanage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c531b-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c531b-107">Prerequisites</span></span>
<span data-ttu-id="c531b-108">toouse PowerShell toomanage Azure CDN profili ve uç noktaları, hello Azure PowerShell Modülü yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c531b-108">toouse PowerShell toomanage your Azure CDN profiles and endpoints, you must have hello Azure PowerShell module installed.</span></span>  <span data-ttu-id="c531b-109">toolearn nasıl tooinstall Azure PowerShell ve tooAzure hello kullanarak bağlanmak `Login-AzureRmAccount` cmdlet'ini bkz [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c531b-109">toolearn how tooinstall Azure PowerShell and connect tooAzure using hello `Login-AzureRmAccount` cmdlet, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c531b-110">İle oturum açmanız gerekir `Login-AzureRmAccount` Azure PowerShell cmdlet'lerini çalıştırmadan önce.</span><span class="sxs-lookup"><span data-stu-id="c531b-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a><span data-ttu-id="c531b-111">Hello Azure CDN cmdlet'leri listeleme</span><span class="sxs-lookup"><span data-stu-id="c531b-111">Listing hello Azure CDN cmdlets</span></span>
<span data-ttu-id="c531b-112">Hello kullanarak tüm hello Azure CDN cmdlet'leri listelediğiniz `Get-Command` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c531b-112">You can list all hello Azure CDN cmdlets using hello `Get-Command` cmdlet.</span></span>

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

## <a name="getting-help"></a><span data-ttu-id="c531b-113">Yardım alma</span><span class="sxs-lookup"><span data-stu-id="c531b-113">Getting help</span></span>
<span data-ttu-id="c531b-114">Herhangi bir hello kullanarak bu cmdlet'leri ile Yardım alabilirsiniz `Get-Help` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c531b-114">You can get help with any of these cmdlets using hello `Get-Help` cmdlet.</span></span>  <span data-ttu-id="c531b-115">`Get-Help`Kullanım ve sözdizimi sağlar ve isteğe bağlı olarak örnekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c531b-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

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

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="c531b-116">Liste mevcut Azure CDN profili</span><span class="sxs-lookup"><span data-stu-id="c531b-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="c531b-117">Merhaba `Get-AzureRmCdnProfile` cmdlet parametre olmadan tüm mevcut CDN profili alır.</span><span class="sxs-lookup"><span data-stu-id="c531b-117">hello `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="c531b-118">Bu çıktı yöneltilen toocmdlets numaralandırması için olabilir.</span><span class="sxs-lookup"><span data-stu-id="c531b-118">This output can be piped toocmdlets for enumeration.</span></span>

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="c531b-119">Ayrıca hello profilinin adını ve kaynak grubu belirterek tek bir profil geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c531b-119">You can also return a single profile by specifying hello profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="c531b-120">Farklı kaynak gruplarında oldukları sürece birden çok CDN ile aynı adı, hello profilleri olası toohave olur.</span><span class="sxs-lookup"><span data-stu-id="c531b-120">It is possible toohave multiple CDN profiles with hello same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="c531b-121">Merhaba atlama `ResourceGroupName` parametresi eşleşen bir ada sahip tüm profillerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="c531b-121">Omitting hello `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="c531b-122">Liste mevcut CDN uç noktası</span><span class="sxs-lookup"><span data-stu-id="c531b-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="c531b-123">`Get-AzureRmCdnEndpoint`tek bir uç nokta veya bir profildeki tüm hello uç noktaları alabilir.</span><span class="sxs-lookup"><span data-stu-id="c531b-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all hello endpoints on a profile.</span></span>  

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

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="c531b-124">CDN profili ve uç noktaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c531b-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="c531b-125">`New-AzureRmCdnProfile`ve `New-AzureRmCdnEndpoint` kullanılan toocreate CDN profili ve uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="c531b-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used toocreate CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="c531b-126">Uç nokta ad kullanılabilirliğini denetleme</span><span class="sxs-lookup"><span data-stu-id="c531b-126">Checking endpoint name availability</span></span>
<span data-ttu-id="c531b-127">`Get-AzureRmCdnEndpointNameAvailability`bir uç nokta adı olup olmadığını gösteren bir nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="c531b-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="c531b-128">Özel bir etki alanı ekleme</span><span class="sxs-lookup"><span data-stu-id="c531b-128">Adding a custom domain</span></span>
<span data-ttu-id="c531b-129">`New-AzureRmCdnCustomDomain`bir özel etki alanı adı tooan mevcut uç ekler.</span><span class="sxs-lookup"><span data-stu-id="c531b-129">`New-AzureRmCdnCustomDomain` adds a custom domain name tooan existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c531b-130">CNAME hello açıklandığı gibi DNS sağlayıcınız ile ayarlamalısınız [nasıl toomap özel etki alanı tooContent teslim ağı (CDN) uç noktası](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="c531b-130">You must set up hello CNAME with your DNS provider as described in [How toomap Custom Domain tooContent Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="c531b-131">Merhaba eşleme kullanan uç noktasını değiştirmeden önce sınayabilirsiniz `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="c531b-131">You can test hello mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
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

## <a name="modifying-an-endpoint"></a><span data-ttu-id="c531b-132">Bir uç nokta değiştirme</span><span class="sxs-lookup"><span data-stu-id="c531b-132">Modifying an endpoint</span></span>
<span data-ttu-id="c531b-133">`Set-AzureRmCdnEndpoint`Mevcut bir uç noktası değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c531b-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="c531b-134">Temizleme/öncesi-loading CDN varlıklar</span><span class="sxs-lookup"><span data-stu-id="c531b-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="c531b-135">`Unpublish-AzureRmCdnEndpointContent`temizler varlıklar, önbelleğe alınmış durumdayken `Publish-AzureRmCdnEndpointContent` desteklenen uç noktasında varlıkları önceden yükler.</span><span class="sxs-lookup"><span data-stu-id="c531b-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="c531b-136">Başlatma/durdurma CDN uç noktası</span><span class="sxs-lookup"><span data-stu-id="c531b-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="c531b-137">`Start-AzureRmCdnEndpoint`ve `Stop-AzureRmCdnEndpoint` kullanılan toostart kullanılabilir ve tekil uç noktalarını ya da grupları uç noktaları durdurun.</span><span class="sxs-lookup"><span data-stu-id="c531b-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used toostart and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="c531b-138">CDN kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="c531b-138">Deleting CDN resources</span></span>
<span data-ttu-id="c531b-139">`Remove-AzureRmCdnProfile`ve `Remove-AzureRmCdnEndpoint` kullanılan tooremove profilleri ve uç noktaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="c531b-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used tooremove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="c531b-140">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c531b-140">Next Steps</span></span>
<span data-ttu-id="c531b-141">Bilgi nasıl tooautomate Azure CDN ile [.NET](cdn-app-dev-net.md) veya [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="c531b-141">Learn how tooautomate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="c531b-142">toolearn CDN özellikleri hakkında bkz [CDN'ye genel bakış](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c531b-142">toolearn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>


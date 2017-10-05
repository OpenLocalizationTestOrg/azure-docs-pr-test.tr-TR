---
title: "PowerShell ile Azure CDN yönetme | Microsoft Docs"
description: "Azure CDN yönetmek için Azure PowerShell cmdlet'lerini kullanmayı öğrenin."
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
ms.openlocfilehash: 5bd2eed7b34cafa43e8f38279890405d4ae55568
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="ce671-103">Azure CDN PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="ce671-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="ce671-104">PowerShell Azure CDN profili ve uç noktaları yönetmek için en esnek yöntemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ce671-104">PowerShell provides one of the most flexible methods to manage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="ce671-105">Yönetim görevlerini otomatikleştirmek için etkileşimli olarak veya komut dosyaları yazarak PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce671-105">You can use PowerShell interactively or by writing scripts to automate management tasks.</span></span>  <span data-ttu-id="ce671-106">Bu öğretici birkaç gösterir Azure CDN profili ve uç noktaları yönetmek için PowerShell ile en yaygın görevleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce671-106">This tutorial demonstrates several of the most common tasks you can accomplish with PowerShell to manage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce671-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ce671-107">Prerequisites</span></span>
<span data-ttu-id="ce671-108">Azure CDN profili ve uç noktaları yönetmek için PowerShell kullanmak için Azure PowerShell Modülü yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce671-108">To use PowerShell to manage your Azure CDN profiles and endpoints, you must have the Azure PowerShell module installed.</span></span>  <span data-ttu-id="ce671-109">Azure PowerShell'i yükleyin ve Azure kullanarak bağlanma hakkında bilgi edinmek için `Login-AzureRmAccount` cmdlet'ini bkz [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ce671-109">To learn how to install Azure PowerShell and connect to Azure using the `Login-AzureRmAccount` cmdlet, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce671-110">İle oturum açmanız gerekir `Login-AzureRmAccount` Azure PowerShell cmdlet'lerini çalıştırmadan önce.</span><span class="sxs-lookup"><span data-stu-id="ce671-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-the-azure-cdn-cmdlets"></a><span data-ttu-id="ce671-111">Azure CDN cmdlet'leri listeleme</span><span class="sxs-lookup"><span data-stu-id="ce671-111">Listing the Azure CDN cmdlets</span></span>
<span data-ttu-id="ce671-112">Tüm Azure CDN cmdlet'leri kullanma listeleyebilirsiniz `Get-Command` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ce671-112">You can list all the Azure CDN cmdlets using the `Get-Command` cmdlet.</span></span>

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

## <a name="getting-help"></a><span data-ttu-id="ce671-113">Yardım alma</span><span class="sxs-lookup"><span data-stu-id="ce671-113">Getting help</span></span>
<span data-ttu-id="ce671-114">Herhangi bir kullanarak bu cmdlet'leri ile Yardım alabilirsiniz `Get-Help` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ce671-114">You can get help with any of these cmdlets using the `Get-Help` cmdlet.</span></span>  <span data-ttu-id="ce671-115">`Get-Help`Kullanım ve sözdizimi sağlar ve isteğe bağlı olarak örnekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ce671-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

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
    To see the examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="ce671-116">Liste mevcut Azure CDN profili</span><span class="sxs-lookup"><span data-stu-id="ce671-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="ce671-117">`Get-AzureRmCdnProfile` Hiçbir parametre olmadan cmdlet'i tüm mevcut CDN profili alır.</span><span class="sxs-lookup"><span data-stu-id="ce671-117">The `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="ce671-118">Numaralandırma için cmdlet'leri yöneltilen bu çıkış.</span><span class="sxs-lookup"><span data-stu-id="ce671-118">This output can be piped to cmdlets for enumeration.</span></span>

```powershell
# Output the name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="ce671-119">Profil adı ve kaynak grubu belirterek tek bir profil de döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="ce671-119">You can also return a single profile by specifying the profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="ce671-120">Farklı kaynak gruplarında oldukları sürece aynı ada sahip birden çok CDN profili olması mümkündür.</span><span class="sxs-lookup"><span data-stu-id="ce671-120">It is possible to have multiple CDN profiles with the same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="ce671-121">Atlama `ResourceGroupName` parametresi eşleşen bir ada sahip tüm profillerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ce671-121">Omitting the `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="ce671-122">Liste mevcut CDN uç noktası</span><span class="sxs-lookup"><span data-stu-id="ce671-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="ce671-123">`Get-AzureRmCdnEndpoint`tek bir uç nokta veya bir profildeki tüm uç noktaları alabilir.</span><span class="sxs-lookup"><span data-stu-id="ce671-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all the endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of the endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of the endpoints on all of the profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of the endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="ce671-124">CDN profili ve uç noktaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce671-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="ce671-125">`New-AzureRmCdnProfile`ve `New-AzureRmCdnEndpoint` CDN profili ve uç noktaları oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ce671-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used to create CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="ce671-126">Uç nokta ad kullanılabilirliğini denetleme</span><span class="sxs-lookup"><span data-stu-id="ce671-126">Checking endpoint name availability</span></span>
<span data-ttu-id="ce671-127">`Get-AzureRmCdnEndpointNameAvailability`bir uç nokta adı olup olmadığını gösteren bir nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="ce671-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message to the console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="ce671-128">Özel bir etki alanı ekleme</span><span class="sxs-lookup"><span data-stu-id="ce671-128">Adding a custom domain</span></span>
<span data-ttu-id="ce671-129">`New-AzureRmCdnCustomDomain`özel etki alanı için mevcut bir uç noktası ekler.</span><span class="sxs-lookup"><span data-stu-id="ce671-129">`New-AzureRmCdnCustomDomain` adds a custom domain name to an existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce671-130">CNAME açıklandığı gibi DNS sağlayıcınız ile ayarlamalısınız [özel etki alanını içerik teslim ağı (CDN) uç noktasına eşleme nasıl](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ce671-130">You must set up the CNAME with your DNS provider as described in [How to map Custom Domain to Content Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="ce671-131">Eşleme kullanan uç noktasını değiştirmeden önce sınayabilirsiniz `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="ce671-131">You can test the mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check the mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create the custom domain on the endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="ce671-132">Bir uç nokta değiştirme</span><span class="sxs-lookup"><span data-stu-id="ce671-132">Modifying an endpoint</span></span>
<span data-ttu-id="ce671-133">`Set-AzureRmCdnEndpoint`Mevcut bir uç noktası değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ce671-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save the changed endpoint and apply the changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="ce671-134">Temizleme/öncesi-loading CDN varlıklar</span><span class="sxs-lookup"><span data-stu-id="ce671-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="ce671-135">`Unpublish-AzureRmCdnEndpointContent`temizler varlıklar, önbelleğe alınmış durumdayken `Publish-AzureRmCdnEndpointContent` desteklenen uç noktasında varlıkları önceden yükler.</span><span class="sxs-lookup"><span data-stu-id="ce671-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="ce671-136">Başlatma/durdurma CDN uç noktası</span><span class="sxs-lookup"><span data-stu-id="ce671-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="ce671-137">`Start-AzureRmCdnEndpoint`ve `Stop-AzureRmCdnEndpoint` tekil uç noktalarını ya da grupları uç noktaları durdurmak ve başlatmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ce671-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used to start and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop the cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="ce671-138">CDN kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="ce671-138">Deleting CDN resources</span></span>
<span data-ttu-id="ce671-139">`Remove-AzureRmCdnProfile`ve `Remove-AzureRmCdnEndpoint` profilleri ve uç noktaları kaldırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ce671-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used to remove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all the endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="ce671-140">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ce671-140">Next Steps</span></span>
<span data-ttu-id="ce671-141">Azure CDN’yi [.NET](cdn-app-dev-net.md) veya [Node.js](cdn-app-dev-node.md) ile nasıl otomatik hale getireceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ce671-141">Learn how to automate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="ce671-142">CDN özellikleri hakkında bilgi edinmek için [CDN'ye genel bakış](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce671-142">To learn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>


---
title: "PowerShell ile Azure Media Services hesaplarını yönetme"
description: "Azure Media Services hesapları PowerShell cmdlet'leri ile yönetmeyi öğrenin."
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: 3d999d9e27844bc0164cc3572522b9ec022118a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="cb128-103">PowerShell ile Azure Media Services hesaplarını yönetme</span><span class="sxs-lookup"><span data-stu-id="cb128-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb128-104">Portal</span><span class="sxs-lookup"><span data-stu-id="cb128-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="cb128-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb128-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="cb128-106">REST</span><span class="sxs-lookup"><span data-stu-id="cb128-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="cb128-107">Azure Media Services hesabı oluşturmak için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb128-107">To be able to create an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="cb128-108">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb128-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cb128-109">Ayrıntılı bilgi için bkz. <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Ücretsiz Deneme Sürümü</a>.</span><span class="sxs-lookup"><span data-stu-id="cb128-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="cb128-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cb128-110">Overview</span></span>
<span data-ttu-id="cb128-111">Bu makale Azure PowerShell cmdlet'lerini Azure Resource Manager framework Azure Media Services (AMS) listeler.</span><span class="sxs-lookup"><span data-stu-id="cb128-111">This article lists the Azure PowerShell cmdlets for Azure Media Services (AMS) in the Azure Resource Manager framework.</span></span> <span data-ttu-id="cb128-112">Cmdlet'leri mevcut **Microsoft.Azure.Commands.Media** ad alanı.</span><span class="sxs-lookup"><span data-stu-id="cb128-112">The cmdlets exist in the **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="cb128-113">Sürümler</span><span class="sxs-lookup"><span data-stu-id="cb128-113">Versions</span></span>
<span data-ttu-id="cb128-114">**ApiVersion**: "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="cb128-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="cb128-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="cb128-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="cb128-116">Medya hizmeti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cb128-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="cb128-117">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="cb128-117">Syntax</span></span>
<span data-ttu-id="cb128-118">Parametre kümesi: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="cb128-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="cb128-119">Parametre kümesi: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="cb128-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="cb128-120">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cb128-120">Parameters</span></span>
<span data-ttu-id="cb128-121">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-122">Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-122">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="cb128-123">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-123">Aliases</span></span> | <span data-ttu-id="cb128-124">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-125">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-125">Required?</span></span> |<span data-ttu-id="cb128-126">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-126">true</span></span> |
| <span data-ttu-id="cb128-127">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-127">Position?</span></span> |<span data-ttu-id="cb128-128">0</span><span class="sxs-lookup"><span data-stu-id="cb128-128">0</span></span> |
| <span data-ttu-id="cb128-129">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-129">Default value</span></span> |<span data-ttu-id="cb128-130">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-130">none</span></span> |
| <span data-ttu-id="cb128-131">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-131">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-132">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-133">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-133">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-134">False</span><span class="sxs-lookup"><span data-stu-id="cb128-134">false</span></span> |

<span data-ttu-id="cb128-135">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-136">Medya hizmeti adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-136">Specifies the name of the media service.</span></span>

| <span data-ttu-id="cb128-137">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-137">Aliases</span></span> | <span data-ttu-id="cb128-138">Ad</span><span class="sxs-lookup"><span data-stu-id="cb128-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-139">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-139">Required?</span></span> |<span data-ttu-id="cb128-140">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-140">true</span></span> |
| <span data-ttu-id="cb128-141">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-141">Position?</span></span> |<span data-ttu-id="cb128-142">1</span><span class="sxs-lookup"><span data-stu-id="cb128-142">1</span></span> |
| <span data-ttu-id="cb128-143">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-143">Default value</span></span> |<span data-ttu-id="cb128-144">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-144">none</span></span> |
| <span data-ttu-id="cb128-145">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-145">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-146">False</span><span class="sxs-lookup"><span data-stu-id="cb128-146">false</span></span> |
| <span data-ttu-id="cb128-147">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-147">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-148">False</span><span class="sxs-lookup"><span data-stu-id="cb128-148">false</span></span> |

<span data-ttu-id="cb128-149">**-Location &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-150">Medya hizmeti kaynak konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-150">Specifies the resource location of the media service.</span></span>

| <span data-ttu-id="cb128-151">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-151">Aliases</span></span> | <span data-ttu-id="cb128-152">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-153">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-153">Required?</span></span> |<span data-ttu-id="cb128-154">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-154">true</span></span> |
| <span data-ttu-id="cb128-155">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-155">Position?</span></span> |<span data-ttu-id="cb128-156">2</span><span class="sxs-lookup"><span data-stu-id="cb128-156">2</span></span> |
| <span data-ttu-id="cb128-157">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-157">Default value</span></span> |<span data-ttu-id="cb128-158">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-158">none</span></span> |
| <span data-ttu-id="cb128-159">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-159">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-160">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-161">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-161">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-162">False</span><span class="sxs-lookup"><span data-stu-id="cb128-162">false</span></span> |

<span data-ttu-id="cb128-163">**-StorageAccountId &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-164">Medya hizmeti ile ilişkili bir birincil depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-164">Specifies a primary storage account that associated with the media service.</span></span>

* <span data-ttu-id="cb128-165">Yalnızca desteklenen (Resource Manager API ile) yeni depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cb128-165">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="cb128-166">Depolama hesabı bulunmalı ve medya hizmeti ile aynı konumda yok.</span><span class="sxs-lookup"><span data-stu-id="cb128-166">The storage account must exist and has the same location with the media service.</span></span>

| <span data-ttu-id="cb128-167">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-167">Aliases</span></span> | <span data-ttu-id="cb128-168">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-169">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-169">Required?</span></span> |<span data-ttu-id="cb128-170">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-170">true</span></span> |
| <span data-ttu-id="cb128-171">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-171">Position?</span></span> |<span data-ttu-id="cb128-172">3</span><span class="sxs-lookup"><span data-stu-id="cb128-172">3</span></span> |
| <span data-ttu-id="cb128-173">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-173">Default value</span></span> |<span data-ttu-id="cb128-174">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-174">none</span></span> |
| <span data-ttu-id="cb128-175">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-175">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-176">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-177">Parametre kümesi adı</span><span class="sxs-lookup"><span data-stu-id="cb128-177">Parameter set name</span></span> |<span data-ttu-id="cb128-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="cb128-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="cb128-179">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-179">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-180">False</span><span class="sxs-lookup"><span data-stu-id="cb128-180">false</span></span> |

<span data-ttu-id="cb128-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="cb128-182">Medya hizmeti ile ilişkilendirilmiş depolama hesaplarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-182">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="cb128-183">Yalnızca desteklenen (Resource Manager API ile) yeni depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cb128-183">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="cb128-184">Depolama hesabı bulunmalı ve medya hizmeti ile aynı konumda yok.</span><span class="sxs-lookup"><span data-stu-id="cb128-184">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="cb128-185">Yalnızca bir depolama hesabı birincil olarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="cb128-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="cb128-186">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-186">Aliases</span></span> | <span data-ttu-id="cb128-187">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-188">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-188">Required?</span></span> |<span data-ttu-id="cb128-189">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-189">true</span></span> |
| <span data-ttu-id="cb128-190">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-190">Position?</span></span> |<span data-ttu-id="cb128-191">3</span><span class="sxs-lookup"><span data-stu-id="cb128-191">3</span></span> |
| <span data-ttu-id="cb128-192">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-192">Default value</span></span> |<span data-ttu-id="cb128-193">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-193">none</span></span> |
| <span data-ttu-id="cb128-194">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-194">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-195">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-196">Parametre kümesi adı</span><span class="sxs-lookup"><span data-stu-id="cb128-196">Parameter set name</span></span> |<span data-ttu-id="cb128-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="cb128-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="cb128-198">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-198">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-199">False</span><span class="sxs-lookup"><span data-stu-id="cb128-199">false</span></span> |

<span data-ttu-id="cb128-200">**-Etiketler &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="cb128-201">Bir karma tablosu medya hizmeti ile ilişkilendirilmiş etiketleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-201">Specifies a hash table of the tags that are associated with the media service.</span></span>

* <span data-ttu-id="cb128-202">Örnek: @{"tag1"="value1";" tag2 "=: value2"}</span><span class="sxs-lookup"><span data-stu-id="cb128-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="cb128-203">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-203">Aliases</span></span> | <span data-ttu-id="cb128-204">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-205">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-205">Required?</span></span> |<span data-ttu-id="cb128-206">False</span><span class="sxs-lookup"><span data-stu-id="cb128-206">false</span></span> |
| <span data-ttu-id="cb128-207">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-207">Position?</span></span> |<span data-ttu-id="cb128-208">Adlı</span><span class="sxs-lookup"><span data-stu-id="cb128-208">named</span></span> |
| <span data-ttu-id="cb128-209">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-209">Default value</span></span> |<span data-ttu-id="cb128-210">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-210">none</span></span> |
| <span data-ttu-id="cb128-211">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-211">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-212">False</span><span class="sxs-lookup"><span data-stu-id="cb128-212">false</span></span> |
| <span data-ttu-id="cb128-213">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-213">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-214">False</span><span class="sxs-lookup"><span data-stu-id="cb128-214">false</span></span> |

<span data-ttu-id="cb128-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="cb128-216">Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cb128-216">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="cb128-217">Girişleri</span><span class="sxs-lookup"><span data-stu-id="cb128-217">Inputs</span></span>
<span data-ttu-id="cb128-218">Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-218">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="cb128-219">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="cb128-219">Outputs</span></span>
<span data-ttu-id="cb128-220">Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-220">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="cb128-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="cb128-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="cb128-222">Bir medya hizmeti güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="cb128-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="cb128-223">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="cb128-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="cb128-224">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cb128-224">Parameters</span></span>
<span data-ttu-id="cb128-225">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-226">Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-226">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="cb128-227">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-227">Aliases</span></span> | <span data-ttu-id="cb128-228">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-229">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-229">Required?</span></span> |<span data-ttu-id="cb128-230">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-230">true</span></span> |
| <span data-ttu-id="cb128-231">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-231">Position?</span></span> |<span data-ttu-id="cb128-232">0</span><span class="sxs-lookup"><span data-stu-id="cb128-232">0</span></span> |
| <span data-ttu-id="cb128-233">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-233">Default Value</span></span> |<span data-ttu-id="cb128-234">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-234">none</span></span> |
| <span data-ttu-id="cb128-235">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="cb128-236">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-237">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-237">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-238">False</span><span class="sxs-lookup"><span data-stu-id="cb128-238">false</span></span> |

<span data-ttu-id="cb128-239">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-240">Medya hizmeti adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-240">Specifies the name of the media service.</span></span>

| <span data-ttu-id="cb128-241">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-241">Aliases</span></span> | <span data-ttu-id="cb128-242">Ad</span><span class="sxs-lookup"><span data-stu-id="cb128-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-243">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-243">Required?</span></span> |<span data-ttu-id="cb128-244">True</span><span class="sxs-lookup"><span data-stu-id="cb128-244">True</span></span> |
| <span data-ttu-id="cb128-245">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-245">Position?</span></span> |<span data-ttu-id="cb128-246">1</span><span class="sxs-lookup"><span data-stu-id="cb128-246">1</span></span> |
| <span data-ttu-id="cb128-247">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-247">Default value</span></span> |<span data-ttu-id="cb128-248">None</span><span class="sxs-lookup"><span data-stu-id="cb128-248">None</span></span> |
| <span data-ttu-id="cb128-249">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-249">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-250">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-251">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-251">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-252">False</span><span class="sxs-lookup"><span data-stu-id="cb128-252">False</span></span> |

<span data-ttu-id="cb128-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="cb128-254">Medya hizmeti ile ilişkilendirilmiş depolama hesaplarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-254">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="cb128-255">Yalnızca desteklenen (Resource Manager API ile) yeni depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cb128-255">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="cb128-256">Depolama hesabı bulunmalı ve medya hizmeti ile aynı konumda yok.</span><span class="sxs-lookup"><span data-stu-id="cb128-256">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="cb128-257">Yalnızca bir depolama hesabı birincil olarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="cb128-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="cb128-258">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-258">Aliases</span></span> | <span data-ttu-id="cb128-259">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-260">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-260">Required?</span></span> |<span data-ttu-id="cb128-261">False</span><span class="sxs-lookup"><span data-stu-id="cb128-261">false</span></span> |
| <span data-ttu-id="cb128-262">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-262">Position?</span></span> |<span data-ttu-id="cb128-263">Adlı</span><span class="sxs-lookup"><span data-stu-id="cb128-263">Named</span></span> |
| <span data-ttu-id="cb128-264">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-264">Default value</span></span> |<span data-ttu-id="cb128-265">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-265">none</span></span> |
| <span data-ttu-id="cb128-266">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-266">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-267">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-268">Parametre kümesi adı</span><span class="sxs-lookup"><span data-stu-id="cb128-268">Parameter set name</span></span> |<span data-ttu-id="cb128-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="cb128-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="cb128-270">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-270">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-271">False</span><span class="sxs-lookup"><span data-stu-id="cb128-271">false</span></span> |

<span data-ttu-id="cb128-272">**-Etiketler &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="cb128-273">Bu medya hizmeti ile ilişkilendirilmiş etiketleri karma tablosu belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-273">Specifies a hash table of the tags that are associated with this media service.</span></span>

* <span data-ttu-id="cb128-274">Medya hizmeti ile ilişkilendirilmiş etiketleri, müşteri tarafından belirtilen değeri ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="cb128-274">The tags that are associated with the media service are replaced with value specified by the customer.</span></span>

| <span data-ttu-id="cb128-275">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-275">Aliases</span></span> | <span data-ttu-id="cb128-276">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-277">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-277">Required?</span></span> |<span data-ttu-id="cb128-278">False</span><span class="sxs-lookup"><span data-stu-id="cb128-278">False</span></span> |
| <span data-ttu-id="cb128-279">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-279">Position?</span></span> |<span data-ttu-id="cb128-280">Adlı</span><span class="sxs-lookup"><span data-stu-id="cb128-280">Named</span></span> |
| <span data-ttu-id="cb128-281">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-281">Default value</span></span> |<span data-ttu-id="cb128-282">None</span><span class="sxs-lookup"><span data-stu-id="cb128-282">None</span></span> |
| <span data-ttu-id="cb128-283">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-283">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-284">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-285">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-285">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-286">False</span><span class="sxs-lookup"><span data-stu-id="cb128-286">false</span></span> |

<span data-ttu-id="cb128-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="cb128-288">Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cb128-288">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="cb128-289">Girişleri</span><span class="sxs-lookup"><span data-stu-id="cb128-289">Inputs</span></span>
<span data-ttu-id="cb128-290">Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-290">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="cb128-291">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="cb128-291">Outputs</span></span>
<span data-ttu-id="cb128-292">Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-292">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="cb128-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="cb128-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="cb128-294">Medya hizmeti kaldırır.</span><span class="sxs-lookup"><span data-stu-id="cb128-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="cb128-295">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="cb128-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="cb128-296">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cb128-296">Parameters</span></span>
<span data-ttu-id="cb128-297">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-298">Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-298">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="cb128-299">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-299">Aliases</span></span> | <span data-ttu-id="cb128-300">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-301">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-301">Required?</span></span> |<span data-ttu-id="cb128-302">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-302">true</span></span> |
| <span data-ttu-id="cb128-303">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-303">Position?</span></span> |<span data-ttu-id="cb128-304">0</span><span class="sxs-lookup"><span data-stu-id="cb128-304">0</span></span> |
| <span data-ttu-id="cb128-305">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-305">Default value</span></span> |<span data-ttu-id="cb128-306">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-306">none</span></span> |
| <span data-ttu-id="cb128-307">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-307">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-308">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-309">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-309">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-310">False</span><span class="sxs-lookup"><span data-stu-id="cb128-310">false</span></span> |

<span data-ttu-id="cb128-311">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-312">Medya hizmeti adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-312">Specifies the name of the media service.</span></span>

| <span data-ttu-id="cb128-313">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-313">Aliases</span></span> | <span data-ttu-id="cb128-314">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-315">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-315">Required?</span></span> |<span data-ttu-id="cb128-316">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-316">true</span></span> |
| <span data-ttu-id="cb128-317">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-317">Position?</span></span> |<span data-ttu-id="cb128-318">2</span><span class="sxs-lookup"><span data-stu-id="cb128-318">2</span></span> |
| <span data-ttu-id="cb128-319">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-319">Default value</span></span> |<span data-ttu-id="cb128-320">None</span><span class="sxs-lookup"><span data-stu-id="cb128-320">None</span></span> |
| <span data-ttu-id="cb128-321">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-321">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-322">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-323">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-323">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-324">False</span><span class="sxs-lookup"><span data-stu-id="cb128-324">False</span></span> |

<span data-ttu-id="cb128-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="cb128-326">Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cb128-326">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="cb128-327">Girişleri</span><span class="sxs-lookup"><span data-stu-id="cb128-327">Inputs</span></span>
<span data-ttu-id="cb128-328">Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-328">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="cb128-329">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="cb128-329">Outputs</span></span>
<span data-ttu-id="cb128-330">Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-330">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="cb128-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="cb128-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="cb128-332">Bir kaynak grubunda tüm medya Hizmetleri veya belirli bir ada sahip bir medya hizmeti alır.</span><span class="sxs-lookup"><span data-stu-id="cb128-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="cb128-333">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="cb128-333">Syntax</span></span>
<span data-ttu-id="cb128-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="cb128-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="cb128-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="cb128-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="cb128-336">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cb128-336">Parameters</span></span>
<span data-ttu-id="cb128-337">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-338">Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-338">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="cb128-339">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-339">Aliases</span></span> | <span data-ttu-id="cb128-340">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-341">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-341">Required?</span></span> |<span data-ttu-id="cb128-342">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-342">true</span></span> |
| <span data-ttu-id="cb128-343">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-343">Position?</span></span> |<span data-ttu-id="cb128-344">0</span><span class="sxs-lookup"><span data-stu-id="cb128-344">0</span></span> |
| <span data-ttu-id="cb128-345">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-345">Default value</span></span> |<span data-ttu-id="cb128-346">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-346">none</span></span> |
| <span data-ttu-id="cb128-347">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-347">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-348">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-349">Parametre kümesi adı</span><span class="sxs-lookup"><span data-stu-id="cb128-349">Parameter set name</span></span> |<span data-ttu-id="cb128-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="cb128-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="cb128-351">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-351">Accept wildcard characters?</span></span>   <span data-ttu-id="cb128-352">False</span><span class="sxs-lookup"><span data-stu-id="cb128-352">false</span></span>

<span data-ttu-id="cb128-353">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-354">Medya hizmeti adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-354">Specifies the name of the media service.</span></span>

| <span data-ttu-id="cb128-355">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-355">Aliases</span></span> | <span data-ttu-id="cb128-356">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-357">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-357">Required?</span></span> |<span data-ttu-id="cb128-358">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-358">true</span></span> |
| <span data-ttu-id="cb128-359">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-359">Position?</span></span> |<span data-ttu-id="cb128-360">1</span><span class="sxs-lookup"><span data-stu-id="cb128-360">1</span></span> |
| <span data-ttu-id="cb128-361">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-361">Default value</span></span> |<span data-ttu-id="cb128-362">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-362">none</span></span> |
| <span data-ttu-id="cb128-363">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-363">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-364">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-365">Parametre kümesi adı</span><span class="sxs-lookup"><span data-stu-id="cb128-365">Parameter set name</span></span> |<span data-ttu-id="cb128-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="cb128-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="cb128-367">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-367">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-368">False</span><span class="sxs-lookup"><span data-stu-id="cb128-368">false</span></span> |

<span data-ttu-id="cb128-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="cb128-370">Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cb128-370">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="cb128-371">Girişleri</span><span class="sxs-lookup"><span data-stu-id="cb128-371">Inputs</span></span>
<span data-ttu-id="cb128-372">Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-372">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="cb128-373">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="cb128-373">Outputs</span></span>
<span data-ttu-id="cb128-374">Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-374">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="cb128-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="cb128-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="cb128-376">Medya hizmeti anahtarları alır.</span><span class="sxs-lookup"><span data-stu-id="cb128-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="cb128-377">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="cb128-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="cb128-378">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cb128-378">Parameters</span></span>
<span data-ttu-id="cb128-379">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-380">Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-380">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="cb128-381">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-381">Aliases</span></span> | <span data-ttu-id="cb128-382">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-383">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-383">Required?</span></span> |<span data-ttu-id="cb128-384">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-384">true</span></span> |
| <span data-ttu-id="cb128-385">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-385">Position?</span></span> |<span data-ttu-id="cb128-386">0</span><span class="sxs-lookup"><span data-stu-id="cb128-386">0</span></span> |
| <span data-ttu-id="cb128-387">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-387">Default value</span></span> |<span data-ttu-id="cb128-388">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-388">none</span></span> |
| <span data-ttu-id="cb128-389">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-389">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-390">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-391">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-391">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-392">False</span><span class="sxs-lookup"><span data-stu-id="cb128-392">false</span></span> |

<span data-ttu-id="cb128-393">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-394">Medya hizmeti adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-394">Specifies the name of the media service.</span></span>

| <span data-ttu-id="cb128-395">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-395">Aliases</span></span> | <span data-ttu-id="cb128-396">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-397">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-397">Required?</span></span> |<span data-ttu-id="cb128-398">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-398">true</span></span> |
| <span data-ttu-id="cb128-399">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-399">Position?</span></span> |<span data-ttu-id="cb128-400">1</span><span class="sxs-lookup"><span data-stu-id="cb128-400">1</span></span> |
| <span data-ttu-id="cb128-401">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-401">Default value</span></span> |<span data-ttu-id="cb128-402">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-402">none</span></span> |
| <span data-ttu-id="cb128-403">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-403">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-404">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-405">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-405">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-406">False</span><span class="sxs-lookup"><span data-stu-id="cb128-406">false</span></span> |

<span data-ttu-id="cb128-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="cb128-408">Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cb128-408">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="cb128-409">Girişleri</span><span class="sxs-lookup"><span data-stu-id="cb128-409">Inputs</span></span>
<span data-ttu-id="cb128-410">Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-410">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="cb128-411">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="cb128-411">Outputs</span></span>
<span data-ttu-id="cb128-412">Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-412">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="cb128-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="cb128-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="cb128-414">Medya hizmeti birincil veya ikincil anahtarı yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cb128-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="cb128-415">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="cb128-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="cb128-416">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cb128-416">Parameters</span></span>
<span data-ttu-id="cb128-417">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-418">Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-418">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="cb128-419">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-419">Aliases</span></span> | <span data-ttu-id="cb128-420">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-421">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-421">Required?</span></span> |<span data-ttu-id="cb128-422">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-422">true</span></span> |
| <span data-ttu-id="cb128-423">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-423">Position?</span></span> |<span data-ttu-id="cb128-424">0</span><span class="sxs-lookup"><span data-stu-id="cb128-424">0</span></span> |
| <span data-ttu-id="cb128-425">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-425">Default value</span></span> |<span data-ttu-id="cb128-426">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-426">none</span></span> |
| <span data-ttu-id="cb128-427">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-427">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-428">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-429">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-429">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-430">False</span><span class="sxs-lookup"><span data-stu-id="cb128-430">false</span></span> |

<span data-ttu-id="cb128-431">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-432">Medya hizmeti adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-432">Specifies the name of the media service.</span></span>

| <span data-ttu-id="cb128-433">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-433">Aliases</span></span> | <span data-ttu-id="cb128-434">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-435">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-435">Required?</span></span> |<span data-ttu-id="cb128-436">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-436">true</span></span> |
| <span data-ttu-id="cb128-437">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-437">Position?</span></span> |<span data-ttu-id="cb128-438">1</span><span class="sxs-lookup"><span data-stu-id="cb128-438">1</span></span> |
| <span data-ttu-id="cb128-439">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-439">Default value</span></span> |<span data-ttu-id="cb128-440">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-440">none</span></span> |
| <span data-ttu-id="cb128-441">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-441">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-442">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-443">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-443">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-444">False</span><span class="sxs-lookup"><span data-stu-id="cb128-444">false</span></span> |

<span data-ttu-id="cb128-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="cb128-446">Medya hizmeti anahtar türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-446">Specifies the key type of the media service.</span></span>

* <span data-ttu-id="cb128-447">Birincil veya ikincil</span><span class="sxs-lookup"><span data-stu-id="cb128-447">Primary or Secondary</span></span>

| <span data-ttu-id="cb128-448">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-448">Aliases</span></span> | <span data-ttu-id="cb128-449">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-450">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-450">Required?</span></span> |<span data-ttu-id="cb128-451">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-451">true</span></span> |
| <span data-ttu-id="cb128-452">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-452">Position?</span></span> |<span data-ttu-id="cb128-453">2</span><span class="sxs-lookup"><span data-stu-id="cb128-453">2</span></span> |
| <span data-ttu-id="cb128-454">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-454">Default value</span></span> |<span data-ttu-id="cb128-455">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-455">none</span></span> |
| <span data-ttu-id="cb128-456">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-456">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-457">False</span><span class="sxs-lookup"><span data-stu-id="cb128-457">false</span></span> |
| <span data-ttu-id="cb128-458">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-458">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-459">False</span><span class="sxs-lookup"><span data-stu-id="cb128-459">false</span></span> |

<span data-ttu-id="cb128-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="cb128-461">Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cb128-461">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="cb128-462">Girişleri</span><span class="sxs-lookup"><span data-stu-id="cb128-462">Inputs</span></span>
<span data-ttu-id="cb128-463">Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-463">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="cb128-464">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="cb128-464">Outputs</span></span>
<span data-ttu-id="cb128-465">Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-465">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="cb128-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="cb128-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="cb128-467">Medya hizmeti ile ilişkilendirilmiş bir depolama hesabı için depolama hesabı anahtarları eşitler.</span><span class="sxs-lookup"><span data-stu-id="cb128-467">Synchronizes storage account keys for a storage account associated with the media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="cb128-468">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="cb128-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="cb128-469">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cb128-469">Parameters</span></span>
<span data-ttu-id="cb128-470">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-471">Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-471">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="cb128-472">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-472">Aliases</span></span> | <span data-ttu-id="cb128-473">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-474">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-474">Required?</span></span> |<span data-ttu-id="cb128-475">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-475">true</span></span> |
| <span data-ttu-id="cb128-476">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-476">Position?</span></span> |<span data-ttu-id="cb128-477">0</span><span class="sxs-lookup"><span data-stu-id="cb128-477">0</span></span> |
| <span data-ttu-id="cb128-478">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-478">Default value</span></span> |<span data-ttu-id="cb128-479">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-479">none</span></span> |
| <span data-ttu-id="cb128-480">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-480">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-481">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-482">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-482">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-483">False</span><span class="sxs-lookup"><span data-stu-id="cb128-483">false</span></span> |

<span data-ttu-id="cb128-484">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-485">Medya hizmeti adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-485">Specifies the name of the media service.</span></span>

| <span data-ttu-id="cb128-486">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-486">Aliases</span></span> | <span data-ttu-id="cb128-487">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-488">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-488">Required?</span></span> |<span data-ttu-id="cb128-489">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-489">true</span></span> |
| <span data-ttu-id="cb128-490">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-490">Position?</span></span> |<span data-ttu-id="cb128-491">1</span><span class="sxs-lookup"><span data-stu-id="cb128-491">1</span></span> |
| <span data-ttu-id="cb128-492">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-492">Default value</span></span> |<span data-ttu-id="cb128-493">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-493">none</span></span> |
| <span data-ttu-id="cb128-494">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-494">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-495">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-496">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-496">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-497">False</span><span class="sxs-lookup"><span data-stu-id="cb128-497">false</span></span> |

<span data-ttu-id="cb128-498">**-StorageAccountId &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="cb128-499">Medya hizmeti ile ilişkilendirilmiş depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cb128-499">Specifies the storage account associated with the media service.</span></span>

| <span data-ttu-id="cb128-500">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="cb128-500">Aliases</span></span> | <span data-ttu-id="cb128-501">Kimlik</span><span class="sxs-lookup"><span data-stu-id="cb128-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="cb128-502">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="cb128-502">Required?</span></span> |<span data-ttu-id="cb128-503">TRUE</span><span class="sxs-lookup"><span data-stu-id="cb128-503">true</span></span> |
| <span data-ttu-id="cb128-504">Konum?</span><span class="sxs-lookup"><span data-stu-id="cb128-504">Position?</span></span> |<span data-ttu-id="cb128-505">2</span><span class="sxs-lookup"><span data-stu-id="cb128-505">2</span></span> |
| <span data-ttu-id="cb128-506">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="cb128-506">Default value</span></span> |<span data-ttu-id="cb128-507">Yok</span><span class="sxs-lookup"><span data-stu-id="cb128-507">none</span></span> |
| <span data-ttu-id="cb128-508">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-508">Accept pipeline input?</span></span> |<span data-ttu-id="cb128-509">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="cb128-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="cb128-510">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="cb128-510">Accept wildcard characters?</span></span> |<span data-ttu-id="cb128-511">False</span><span class="sxs-lookup"><span data-stu-id="cb128-511">false</span></span> |

<span data-ttu-id="cb128-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="cb128-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="cb128-513">Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cb128-513">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="cb128-514">Girişleri</span><span class="sxs-lookup"><span data-stu-id="cb128-514">Inputs</span></span>
<span data-ttu-id="cb128-515">Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-515">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="cb128-516">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="cb128-516">Outputs</span></span>
<span data-ttu-id="cb128-517">Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.</span><span class="sxs-lookup"><span data-stu-id="cb128-517">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="cb128-518">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="cb128-518">Next step</span></span>
<span data-ttu-id="cb128-519">Media Services'i öğrenme yolları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="cb128-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cb128-520">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="cb128-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


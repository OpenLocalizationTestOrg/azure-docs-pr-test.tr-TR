---
title: "aaaManage PowerShell ile Azure Media Services hesapları"
description: "PowerShell cmdlet'leri ile nasıl toomanage Azure Media Services hesapları öğrenin."
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
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="5f2cb-103">PowerShell ile Azure Media Services hesaplarını yönetme</span><span class="sxs-lookup"><span data-stu-id="5f2cb-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f2cb-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5f2cb-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="5f2cb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f2cb-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="5f2cb-106">REST</span><span class="sxs-lookup"><span data-stu-id="5f2cb-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="5f2cb-107">toobe mümkün toocreate Azure Media Services hesabı, bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-107">toobe able toocreate an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="5f2cb-108">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5f2cb-109">Ayrıntılı bilgi için bkz. <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Ücretsiz Deneme Sürümü</a>.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="5f2cb-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5f2cb-110">Overview</span></span>
<span data-ttu-id="5f2cb-111">Bu makalede, Azure Media Services (AMS) hello Azure Resource Manager framework hello Azure PowerShell cmdlet'leri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-111">This article lists hello Azure PowerShell cmdlets for Azure Media Services (AMS) in hello Azure Resource Manager framework.</span></span> <span data-ttu-id="5f2cb-112">Merhaba cmdlet'leri mevcut hello **Microsoft.Azure.Commands.Media** ad alanı.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-112">hello cmdlets exist in hello **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="5f2cb-113">Sürümler</span><span class="sxs-lookup"><span data-stu-id="5f2cb-113">Versions</span></span>
<span data-ttu-id="5f2cb-114">**ApiVersion**: "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="5f2cb-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="5f2cb-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="5f2cb-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="5f2cb-116">Medya hizmeti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5f2cb-117">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5f2cb-117">Syntax</span></span>
<span data-ttu-id="5f2cb-118">Parametre kümesi: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="5f2cb-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="5f2cb-119">Parametre kümesi: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="5f2cb-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5f2cb-120">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5f2cb-120">Parameters</span></span>
<span data-ttu-id="5f2cb-121">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-122">Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-122">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="5f2cb-123">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-123">Aliases</span></span> | <span data-ttu-id="5f2cb-124">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-125">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-125">Required?</span></span> |<span data-ttu-id="5f2cb-126">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-126">true</span></span> |
| <span data-ttu-id="5f2cb-127">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-127">Position?</span></span> |<span data-ttu-id="5f2cb-128">0</span><span class="sxs-lookup"><span data-stu-id="5f2cb-128">0</span></span> |
| <span data-ttu-id="5f2cb-129">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-129">Default value</span></span> |<span data-ttu-id="5f2cb-130">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-130">none</span></span> |
| <span data-ttu-id="5f2cb-131">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-131">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-132">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-133">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-133">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-134">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-134">false</span></span> |

<span data-ttu-id="5f2cb-135">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-136">Merhaba medya hizmeti Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-136">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="5f2cb-137">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-137">Aliases</span></span> | <span data-ttu-id="5f2cb-138">Ad</span><span class="sxs-lookup"><span data-stu-id="5f2cb-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-139">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-139">Required?</span></span> |<span data-ttu-id="5f2cb-140">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-140">true</span></span> |
| <span data-ttu-id="5f2cb-141">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-141">Position?</span></span> |<span data-ttu-id="5f2cb-142">1</span><span class="sxs-lookup"><span data-stu-id="5f2cb-142">1</span></span> |
| <span data-ttu-id="5f2cb-143">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-143">Default value</span></span> |<span data-ttu-id="5f2cb-144">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-144">none</span></span> |
| <span data-ttu-id="5f2cb-145">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-145">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-146">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-146">false</span></span> |
| <span data-ttu-id="5f2cb-147">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-147">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-148">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-148">false</span></span> |

<span data-ttu-id="5f2cb-149">**-Location &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-150">Merhaba medya hizmeti Hello kaynak konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-150">Specifies hello resource location of hello media service.</span></span>

| <span data-ttu-id="5f2cb-151">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-151">Aliases</span></span> | <span data-ttu-id="5f2cb-152">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-153">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-153">Required?</span></span> |<span data-ttu-id="5f2cb-154">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-154">true</span></span> |
| <span data-ttu-id="5f2cb-155">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-155">Position?</span></span> |<span data-ttu-id="5f2cb-156">2</span><span class="sxs-lookup"><span data-stu-id="5f2cb-156">2</span></span> |
| <span data-ttu-id="5f2cb-157">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-157">Default value</span></span> |<span data-ttu-id="5f2cb-158">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-158">none</span></span> |
| <span data-ttu-id="5f2cb-159">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-159">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-160">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-161">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-161">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-162">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-162">false</span></span> |

<span data-ttu-id="5f2cb-163">**-StorageAccountId &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-164">Merhaba medya hizmeti ile ilişkili bir birincil depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-164">Specifies a primary storage account that associated with hello media service.</span></span>

* <span data-ttu-id="5f2cb-165">Yalnızca desteklenen (Merhaba Resource Manager API ile) yeni depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-165">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="5f2cb-166">Merhaba depolama hesabının var olmalıdır ve hello hello medya hizmeti ile aynı konum.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-166">hello storage account must exist and has hello same location with hello media service.</span></span>

| <span data-ttu-id="5f2cb-167">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-167">Aliases</span></span> | <span data-ttu-id="5f2cb-168">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-169">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-169">Required?</span></span> |<span data-ttu-id="5f2cb-170">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-170">true</span></span> |
| <span data-ttu-id="5f2cb-171">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-171">Position?</span></span> |<span data-ttu-id="5f2cb-172">3</span><span class="sxs-lookup"><span data-stu-id="5f2cb-172">3</span></span> |
| <span data-ttu-id="5f2cb-173">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-173">Default value</span></span> |<span data-ttu-id="5f2cb-174">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-174">none</span></span> |
| <span data-ttu-id="5f2cb-175">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-175">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-176">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-177">Parametre kümesi adı</span><span class="sxs-lookup"><span data-stu-id="5f2cb-177">Parameter set name</span></span> |<span data-ttu-id="5f2cb-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="5f2cb-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="5f2cb-179">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-179">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-180">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-180">false</span></span> |

<span data-ttu-id="5f2cb-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="5f2cb-182">Merhaba medya hizmeti ile ilişkilendirilmiş depolama hesaplarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-182">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="5f2cb-183">Yalnızca desteklenen (Merhaba Resource Manager API ile) yeni depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-183">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="5f2cb-184">Merhaba depolama hesabının var olmalıdır ve hello hello medya hizmeti ile aynı konum.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-184">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="5f2cb-185">Yalnızca bir depolama hesabı birincil olarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="5f2cb-186">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-186">Aliases</span></span> | <span data-ttu-id="5f2cb-187">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-188">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-188">Required?</span></span> |<span data-ttu-id="5f2cb-189">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-189">true</span></span> |
| <span data-ttu-id="5f2cb-190">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-190">Position?</span></span> |<span data-ttu-id="5f2cb-191">3</span><span class="sxs-lookup"><span data-stu-id="5f2cb-191">3</span></span> |
| <span data-ttu-id="5f2cb-192">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-192">Default value</span></span> |<span data-ttu-id="5f2cb-193">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-193">none</span></span> |
| <span data-ttu-id="5f2cb-194">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-194">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-195">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-196">Parametre kümesi adı</span><span class="sxs-lookup"><span data-stu-id="5f2cb-196">Parameter set name</span></span> |<span data-ttu-id="5f2cb-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="5f2cb-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="5f2cb-198">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-198">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-199">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-199">false</span></span> |

<span data-ttu-id="5f2cb-200">**-Etiketler &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="5f2cb-201">Bir karma tablosu hello medya hizmeti ile ilişkilendirilmiş hello etiketlerin belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-201">Specifies a hash table of hello tags that are associated with hello media service.</span></span>

* <span data-ttu-id="5f2cb-202">Örnek: @{"tag1"="value1";" tag2 "=: value2"}</span><span class="sxs-lookup"><span data-stu-id="5f2cb-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="5f2cb-203">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-203">Aliases</span></span> | <span data-ttu-id="5f2cb-204">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-205">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-205">Required?</span></span> |<span data-ttu-id="5f2cb-206">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-206">false</span></span> |
| <span data-ttu-id="5f2cb-207">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-207">Position?</span></span> |<span data-ttu-id="5f2cb-208">Adlı</span><span class="sxs-lookup"><span data-stu-id="5f2cb-208">named</span></span> |
| <span data-ttu-id="5f2cb-209">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-209">Default value</span></span> |<span data-ttu-id="5f2cb-210">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-210">none</span></span> |
| <span data-ttu-id="5f2cb-211">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-211">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-212">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-212">false</span></span> |
| <span data-ttu-id="5f2cb-213">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-213">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-214">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-214">false</span></span> |

<span data-ttu-id="5f2cb-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5f2cb-216">Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-216">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5f2cb-217">Girişleri</span><span class="sxs-lookup"><span data-stu-id="5f2cb-217">Inputs</span></span>
<span data-ttu-id="5f2cb-218">Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-218">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5f2cb-219">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="5f2cb-219">Outputs</span></span>
<span data-ttu-id="5f2cb-220">Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-220">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="5f2cb-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="5f2cb-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="5f2cb-222">Bir medya hizmeti güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5f2cb-223">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5f2cb-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5f2cb-224">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5f2cb-224">Parameters</span></span>
<span data-ttu-id="5f2cb-225">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-226">Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-226">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="5f2cb-227">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-227">Aliases</span></span> | <span data-ttu-id="5f2cb-228">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-229">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-229">Required?</span></span> |<span data-ttu-id="5f2cb-230">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-230">true</span></span> |
| <span data-ttu-id="5f2cb-231">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-231">Position?</span></span> |<span data-ttu-id="5f2cb-232">0</span><span class="sxs-lookup"><span data-stu-id="5f2cb-232">0</span></span> |
| <span data-ttu-id="5f2cb-233">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-233">Default Value</span></span> |<span data-ttu-id="5f2cb-234">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-234">none</span></span> |
| <span data-ttu-id="5f2cb-235">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="5f2cb-236">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-237">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-237">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-238">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-238">false</span></span> |

<span data-ttu-id="5f2cb-239">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-240">Merhaba medya hizmeti Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-240">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="5f2cb-241">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-241">Aliases</span></span> | <span data-ttu-id="5f2cb-242">Ad</span><span class="sxs-lookup"><span data-stu-id="5f2cb-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-243">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-243">Required?</span></span> |<span data-ttu-id="5f2cb-244">True</span><span class="sxs-lookup"><span data-stu-id="5f2cb-244">True</span></span> |
| <span data-ttu-id="5f2cb-245">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-245">Position?</span></span> |<span data-ttu-id="5f2cb-246">1</span><span class="sxs-lookup"><span data-stu-id="5f2cb-246">1</span></span> |
| <span data-ttu-id="5f2cb-247">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-247">Default value</span></span> |<span data-ttu-id="5f2cb-248">None</span><span class="sxs-lookup"><span data-stu-id="5f2cb-248">None</span></span> |
| <span data-ttu-id="5f2cb-249">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-249">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-250">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-251">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-251">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-252">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-252">False</span></span> |

<span data-ttu-id="5f2cb-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="5f2cb-254">Merhaba medya hizmeti ile ilişkilendirilmiş depolama hesaplarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-254">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="5f2cb-255">Yalnızca desteklenen (Merhaba Resource Manager API ile) yeni depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-255">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="5f2cb-256">Merhaba depolama hesabının var olmalıdır ve hello hello medya hizmeti ile aynı konum.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-256">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="5f2cb-257">Yalnızca bir depolama hesabı birincil olarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="5f2cb-258">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-258">Aliases</span></span> | <span data-ttu-id="5f2cb-259">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-260">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-260">Required?</span></span> |<span data-ttu-id="5f2cb-261">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-261">false</span></span> |
| <span data-ttu-id="5f2cb-262">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-262">Position?</span></span> |<span data-ttu-id="5f2cb-263">Adlı</span><span class="sxs-lookup"><span data-stu-id="5f2cb-263">Named</span></span> |
| <span data-ttu-id="5f2cb-264">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-264">Default value</span></span> |<span data-ttu-id="5f2cb-265">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-265">none</span></span> |
| <span data-ttu-id="5f2cb-266">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-266">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-267">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-268">Parametre kümesi adı</span><span class="sxs-lookup"><span data-stu-id="5f2cb-268">Parameter set name</span></span> |<span data-ttu-id="5f2cb-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="5f2cb-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="5f2cb-270">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-270">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-271">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-271">false</span></span> |

<span data-ttu-id="5f2cb-272">**-Etiketler &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="5f2cb-273">Bu medya hizmeti ile ilişkilendirilmiş hello etiketleri karma tablosu belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-273">Specifies a hash table of hello tags that are associated with this media service.</span></span>

* <span data-ttu-id="5f2cb-274">Merhaba medya hizmeti ile ilişkilendirilmiş hello etiketleri hello müşteri tarafından belirtilen değeri ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-274">hello tags that are associated with hello media service are replaced with value specified by hello customer.</span></span>

| <span data-ttu-id="5f2cb-275">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-275">Aliases</span></span> | <span data-ttu-id="5f2cb-276">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-277">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-277">Required?</span></span> |<span data-ttu-id="5f2cb-278">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-278">False</span></span> |
| <span data-ttu-id="5f2cb-279">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-279">Position?</span></span> |<span data-ttu-id="5f2cb-280">Adlı</span><span class="sxs-lookup"><span data-stu-id="5f2cb-280">Named</span></span> |
| <span data-ttu-id="5f2cb-281">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-281">Default value</span></span> |<span data-ttu-id="5f2cb-282">None</span><span class="sxs-lookup"><span data-stu-id="5f2cb-282">None</span></span> |
| <span data-ttu-id="5f2cb-283">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-283">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-284">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-285">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-285">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-286">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-286">false</span></span> |

<span data-ttu-id="5f2cb-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5f2cb-288">Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-288">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5f2cb-289">Girişleri</span><span class="sxs-lookup"><span data-stu-id="5f2cb-289">Inputs</span></span>
<span data-ttu-id="5f2cb-290">Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-290">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5f2cb-291">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="5f2cb-291">Outputs</span></span>
<span data-ttu-id="5f2cb-292">Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-292">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="5f2cb-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="5f2cb-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="5f2cb-294">Medya hizmeti kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5f2cb-295">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5f2cb-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5f2cb-296">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5f2cb-296">Parameters</span></span>
<span data-ttu-id="5f2cb-297">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-298">Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-298">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="5f2cb-299">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-299">Aliases</span></span> | <span data-ttu-id="5f2cb-300">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-301">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-301">Required?</span></span> |<span data-ttu-id="5f2cb-302">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-302">true</span></span> |
| <span data-ttu-id="5f2cb-303">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-303">Position?</span></span> |<span data-ttu-id="5f2cb-304">0</span><span class="sxs-lookup"><span data-stu-id="5f2cb-304">0</span></span> |
| <span data-ttu-id="5f2cb-305">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-305">Default value</span></span> |<span data-ttu-id="5f2cb-306">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-306">none</span></span> |
| <span data-ttu-id="5f2cb-307">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-307">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-308">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-309">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-309">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-310">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-310">false</span></span> |

<span data-ttu-id="5f2cb-311">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-312">Merhaba medya hizmeti Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-312">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="5f2cb-313">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-313">Aliases</span></span> | <span data-ttu-id="5f2cb-314">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-315">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-315">Required?</span></span> |<span data-ttu-id="5f2cb-316">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-316">true</span></span> |
| <span data-ttu-id="5f2cb-317">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-317">Position?</span></span> |<span data-ttu-id="5f2cb-318">2</span><span class="sxs-lookup"><span data-stu-id="5f2cb-318">2</span></span> |
| <span data-ttu-id="5f2cb-319">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-319">Default value</span></span> |<span data-ttu-id="5f2cb-320">None</span><span class="sxs-lookup"><span data-stu-id="5f2cb-320">None</span></span> |
| <span data-ttu-id="5f2cb-321">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-321">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-322">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-323">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-323">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-324">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-324">False</span></span> |

<span data-ttu-id="5f2cb-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5f2cb-326">Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-326">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5f2cb-327">Girişleri</span><span class="sxs-lookup"><span data-stu-id="5f2cb-327">Inputs</span></span>
<span data-ttu-id="5f2cb-328">Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-328">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5f2cb-329">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="5f2cb-329">Outputs</span></span>
<span data-ttu-id="5f2cb-330">Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-330">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="5f2cb-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="5f2cb-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="5f2cb-332">Bir kaynak grubunda tüm medya Hizmetleri veya belirli bir ada sahip bir medya hizmeti alır.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="5f2cb-333">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5f2cb-333">Syntax</span></span>
<span data-ttu-id="5f2cb-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="5f2cb-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="5f2cb-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="5f2cb-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5f2cb-336">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5f2cb-336">Parameters</span></span>
<span data-ttu-id="5f2cb-337">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-338">Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-338">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="5f2cb-339">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-339">Aliases</span></span> | <span data-ttu-id="5f2cb-340">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-341">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-341">Required?</span></span> |<span data-ttu-id="5f2cb-342">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-342">true</span></span> |
| <span data-ttu-id="5f2cb-343">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-343">Position?</span></span> |<span data-ttu-id="5f2cb-344">0</span><span class="sxs-lookup"><span data-stu-id="5f2cb-344">0</span></span> |
| <span data-ttu-id="5f2cb-345">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-345">Default value</span></span> |<span data-ttu-id="5f2cb-346">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-346">none</span></span> |
| <span data-ttu-id="5f2cb-347">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-347">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-348">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-349">Parametre kümesi adı</span><span class="sxs-lookup"><span data-stu-id="5f2cb-349">Parameter set name</span></span> |<span data-ttu-id="5f2cb-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="5f2cb-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="5f2cb-351">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-351">Accept wildcard characters?</span></span>   <span data-ttu-id="5f2cb-352">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-352">false</span></span>

<span data-ttu-id="5f2cb-353">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-354">Merhaba medya hizmeti Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-354">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="5f2cb-355">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-355">Aliases</span></span> | <span data-ttu-id="5f2cb-356">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-357">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-357">Required?</span></span> |<span data-ttu-id="5f2cb-358">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-358">true</span></span> |
| <span data-ttu-id="5f2cb-359">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-359">Position?</span></span> |<span data-ttu-id="5f2cb-360">1</span><span class="sxs-lookup"><span data-stu-id="5f2cb-360">1</span></span> |
| <span data-ttu-id="5f2cb-361">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-361">Default value</span></span> |<span data-ttu-id="5f2cb-362">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-362">none</span></span> |
| <span data-ttu-id="5f2cb-363">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-363">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-364">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-365">Parametre kümesi adı</span><span class="sxs-lookup"><span data-stu-id="5f2cb-365">Parameter set name</span></span> |<span data-ttu-id="5f2cb-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="5f2cb-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="5f2cb-367">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-367">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-368">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-368">false</span></span> |

<span data-ttu-id="5f2cb-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5f2cb-370">Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-370">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5f2cb-371">Girişleri</span><span class="sxs-lookup"><span data-stu-id="5f2cb-371">Inputs</span></span>
<span data-ttu-id="5f2cb-372">Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-372">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5f2cb-373">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="5f2cb-373">Outputs</span></span>
<span data-ttu-id="5f2cb-374">Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-374">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="5f2cb-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="5f2cb-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="5f2cb-376">Medya hizmeti anahtarları alır.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5f2cb-377">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5f2cb-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5f2cb-378">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5f2cb-378">Parameters</span></span>
<span data-ttu-id="5f2cb-379">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-380">Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-380">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="5f2cb-381">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-381">Aliases</span></span> | <span data-ttu-id="5f2cb-382">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-383">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-383">Required?</span></span> |<span data-ttu-id="5f2cb-384">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-384">true</span></span> |
| <span data-ttu-id="5f2cb-385">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-385">Position?</span></span> |<span data-ttu-id="5f2cb-386">0</span><span class="sxs-lookup"><span data-stu-id="5f2cb-386">0</span></span> |
| <span data-ttu-id="5f2cb-387">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-387">Default value</span></span> |<span data-ttu-id="5f2cb-388">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-388">none</span></span> |
| <span data-ttu-id="5f2cb-389">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-389">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-390">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-391">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-391">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-392">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-392">false</span></span> |

<span data-ttu-id="5f2cb-393">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-394">Merhaba medya hizmeti Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-394">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="5f2cb-395">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-395">Aliases</span></span> | <span data-ttu-id="5f2cb-396">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-397">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-397">Required?</span></span> |<span data-ttu-id="5f2cb-398">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-398">true</span></span> |
| <span data-ttu-id="5f2cb-399">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-399">Position?</span></span> |<span data-ttu-id="5f2cb-400">1</span><span class="sxs-lookup"><span data-stu-id="5f2cb-400">1</span></span> |
| <span data-ttu-id="5f2cb-401">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-401">Default value</span></span> |<span data-ttu-id="5f2cb-402">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-402">none</span></span> |
| <span data-ttu-id="5f2cb-403">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-403">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-404">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-405">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-405">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-406">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-406">false</span></span> |

<span data-ttu-id="5f2cb-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5f2cb-408">Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-408">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5f2cb-409">Girişleri</span><span class="sxs-lookup"><span data-stu-id="5f2cb-409">Inputs</span></span>
<span data-ttu-id="5f2cb-410">Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-410">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5f2cb-411">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="5f2cb-411">Outputs</span></span>
<span data-ttu-id="5f2cb-412">Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-412">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="5f2cb-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="5f2cb-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="5f2cb-414">Medya hizmeti birincil veya ikincil anahtarı yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5f2cb-415">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5f2cb-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5f2cb-416">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5f2cb-416">Parameters</span></span>
<span data-ttu-id="5f2cb-417">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-418">Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-418">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="5f2cb-419">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-419">Aliases</span></span> | <span data-ttu-id="5f2cb-420">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-421">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-421">Required?</span></span> |<span data-ttu-id="5f2cb-422">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-422">true</span></span> |
| <span data-ttu-id="5f2cb-423">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-423">Position?</span></span> |<span data-ttu-id="5f2cb-424">0</span><span class="sxs-lookup"><span data-stu-id="5f2cb-424">0</span></span> |
| <span data-ttu-id="5f2cb-425">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-425">Default value</span></span> |<span data-ttu-id="5f2cb-426">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-426">none</span></span> |
| <span data-ttu-id="5f2cb-427">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-427">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-428">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-429">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-429">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-430">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-430">false</span></span> |

<span data-ttu-id="5f2cb-431">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-432">Merhaba medya hizmeti Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-432">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="5f2cb-433">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-433">Aliases</span></span> | <span data-ttu-id="5f2cb-434">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-435">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-435">Required?</span></span> |<span data-ttu-id="5f2cb-436">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-436">true</span></span> |
| <span data-ttu-id="5f2cb-437">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-437">Position?</span></span> |<span data-ttu-id="5f2cb-438">1</span><span class="sxs-lookup"><span data-stu-id="5f2cb-438">1</span></span> |
| <span data-ttu-id="5f2cb-439">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-439">Default value</span></span> |<span data-ttu-id="5f2cb-440">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-440">none</span></span> |
| <span data-ttu-id="5f2cb-441">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-441">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-442">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-443">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-443">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-444">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-444">false</span></span> |

<span data-ttu-id="5f2cb-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="5f2cb-446">Merhaba anahtar hello medya hizmeti türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-446">Specifies hello key type of hello media service.</span></span>

* <span data-ttu-id="5f2cb-447">Birincil veya ikincil</span><span class="sxs-lookup"><span data-stu-id="5f2cb-447">Primary or Secondary</span></span>

| <span data-ttu-id="5f2cb-448">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-448">Aliases</span></span> | <span data-ttu-id="5f2cb-449">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-450">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-450">Required?</span></span> |<span data-ttu-id="5f2cb-451">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-451">true</span></span> |
| <span data-ttu-id="5f2cb-452">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-452">Position?</span></span> |<span data-ttu-id="5f2cb-453">2</span><span class="sxs-lookup"><span data-stu-id="5f2cb-453">2</span></span> |
| <span data-ttu-id="5f2cb-454">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-454">Default value</span></span> |<span data-ttu-id="5f2cb-455">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-455">none</span></span> |
| <span data-ttu-id="5f2cb-456">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-456">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-457">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-457">false</span></span> |
| <span data-ttu-id="5f2cb-458">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-458">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-459">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-459">false</span></span> |

<span data-ttu-id="5f2cb-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5f2cb-461">Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-461">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5f2cb-462">Girişleri</span><span class="sxs-lookup"><span data-stu-id="5f2cb-462">Inputs</span></span>
<span data-ttu-id="5f2cb-463">Merhaba giriş toothe cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-463">hello input type is hello type of hello objects that you can pipe toothe cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5f2cb-464">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="5f2cb-464">Outputs</span></span>
<span data-ttu-id="5f2cb-465">Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-465">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="5f2cb-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="5f2cb-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="5f2cb-467">Merhaba medya hizmeti ile ilişkilendirilmiş bir depolama hesabı için depolama hesabı anahtarları eşitler.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-467">Synchronizes storage account keys for a storage account associated with hello media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5f2cb-468">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5f2cb-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5f2cb-469">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5f2cb-469">Parameters</span></span>
<span data-ttu-id="5f2cb-470">**-ResourceGroupName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-471">Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-471">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="5f2cb-472">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-472">Aliases</span></span> | <span data-ttu-id="5f2cb-473">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-474">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-474">Required?</span></span> |<span data-ttu-id="5f2cb-475">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-475">true</span></span> |
| <span data-ttu-id="5f2cb-476">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-476">Position?</span></span> |<span data-ttu-id="5f2cb-477">0</span><span class="sxs-lookup"><span data-stu-id="5f2cb-477">0</span></span> |
| <span data-ttu-id="5f2cb-478">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-478">Default value</span></span> |<span data-ttu-id="5f2cb-479">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-479">none</span></span> |
| <span data-ttu-id="5f2cb-480">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-480">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-481">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-482">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-482">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-483">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-483">false</span></span> |

<span data-ttu-id="5f2cb-484">**-AccountName &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-485">Merhaba medya hizmeti Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-485">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="5f2cb-486">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-486">Aliases</span></span> | <span data-ttu-id="5f2cb-487">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-488">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-488">Required?</span></span> |<span data-ttu-id="5f2cb-489">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-489">true</span></span> |
| <span data-ttu-id="5f2cb-490">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-490">Position?</span></span> |<span data-ttu-id="5f2cb-491">1</span><span class="sxs-lookup"><span data-stu-id="5f2cb-491">1</span></span> |
| <span data-ttu-id="5f2cb-492">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-492">Default value</span></span> |<span data-ttu-id="5f2cb-493">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-493">none</span></span> |
| <span data-ttu-id="5f2cb-494">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-494">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-495">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-496">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-496">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-497">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-497">false</span></span> |

<span data-ttu-id="5f2cb-498">**-StorageAccountId &lt;dize&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="5f2cb-499">Merhaba medya hizmeti ile ilişkili hello depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-499">Specifies hello storage account associated with hello media service.</span></span>

| <span data-ttu-id="5f2cb-500">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="5f2cb-500">Aliases</span></span> | <span data-ttu-id="5f2cb-501">Kimlik</span><span class="sxs-lookup"><span data-stu-id="5f2cb-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="5f2cb-502">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-502">Required?</span></span> |<span data-ttu-id="5f2cb-503">TRUE</span><span class="sxs-lookup"><span data-stu-id="5f2cb-503">true</span></span> |
| <span data-ttu-id="5f2cb-504">Konum?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-504">Position?</span></span> |<span data-ttu-id="5f2cb-505">2</span><span class="sxs-lookup"><span data-stu-id="5f2cb-505">2</span></span> |
| <span data-ttu-id="5f2cb-506">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="5f2cb-506">Default value</span></span> |<span data-ttu-id="5f2cb-507">Yok</span><span class="sxs-lookup"><span data-stu-id="5f2cb-507">none</span></span> |
| <span data-ttu-id="5f2cb-508">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-508">Accept pipeline input?</span></span> |<span data-ttu-id="5f2cb-509">TRUE(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5f2cb-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5f2cb-510">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5f2cb-510">Accept wildcard characters?</span></span> |<span data-ttu-id="5f2cb-511">False</span><span class="sxs-lookup"><span data-stu-id="5f2cb-511">false</span></span> |

<span data-ttu-id="5f2cb-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5f2cb-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5f2cb-513">Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-513">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5f2cb-514">Girişleri</span><span class="sxs-lookup"><span data-stu-id="5f2cb-514">Inputs</span></span>
<span data-ttu-id="5f2cb-515">Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-515">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5f2cb-516">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="5f2cb-516">Outputs</span></span>
<span data-ttu-id="5f2cb-517">Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-517">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="5f2cb-518">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="5f2cb-518">Next step</span></span>
<span data-ttu-id="5f2cb-519">Media Services'i öğrenme yolları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="5f2cb-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5f2cb-520">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="5f2cb-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


---
title: "aaaAzure Kurumsal API'leri - faturalama kullanım ayrıntılarını | Microsoft Docs"
description: "Azure kaynak tüketimini ve eğilimleri kullanılan tooprovide Öngörüler olan Azure faturalama kullanımını ve RateCard API'ları hakkında bilgi edinin."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a><span data-ttu-id="eecbf-103">Kurumsal müşteriler - kullanım ayrıntıları için raporlama API'leri</span><span class="sxs-lookup"><span data-stu-id="eecbf-103">Reporting APIs for Enterprise customers - Usage Details</span></span>

<span data-ttu-id="eecbf-104">Merhaba kullanım ayrıntı API'si tüketilen miktarları ve bir kayıt tarafından tahmini ücretleri günlük bir dökümü sunar.</span><span class="sxs-lookup"><span data-stu-id="eecbf-104">hello Usage Detail API offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="eecbf-105">Merhaba sonuç ayrıca örnekleri, Ölçümler ve Departmanlar hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="eecbf-105">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="eecbf-106">Merhaba API, faturalama dönemi veya belirtilen başlangıç ve bitiş tarihi tarafından sorgulanabilir.</span><span class="sxs-lookup"><span data-stu-id="eecbf-106">hello API can be queried by Billing period or by a specified start and end date.</span></span> 
## <a name="consumption-apis"></a><span data-ttu-id="eecbf-107">Tüketim API'leri</span><span class="sxs-lookup"><span data-stu-id="eecbf-107">Consumption APIs</span></span>


##<a name="request"></a><span data-ttu-id="eecbf-108">İstek</span><span class="sxs-lookup"><span data-stu-id="eecbf-108">Request</span></span> 
<span data-ttu-id="eecbf-109">Eklenen toobe gereken ortak üstbilgi özelliklerini belirtilen [burada](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="eecbf-109">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="eecbf-110">Fatura döneminde belirtilmezse, veriler hello geçerli faturalama dönemi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="eecbf-110">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="eecbf-111">Özel zaman aralıkları ile Merhaba başlangıç belirtilebilir ve hello yyyy-aa-gg biçiminde içinde olan tarih parametrelerine bitiş</span><span class="sxs-lookup"><span data-stu-id="eecbf-111">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd.</span></span> <span data-ttu-id="eecbf-112">Merhaba desteklenen en fazla süre 36 ay aralıktır.</span><span class="sxs-lookup"><span data-stu-id="eecbf-112">hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="eecbf-113">Yöntem</span><span class="sxs-lookup"><span data-stu-id="eecbf-113">Method</span></span> | <span data-ttu-id="eecbf-114">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="eecbf-114">Request URI</span></span>|
|-|-|
|<span data-ttu-id="eecbf-115">AL</span><span class="sxs-lookup"><span data-stu-id="eecbf-115">GET</span></span>|<span data-ttu-id="eecbf-116">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / usagedetails</span><span class="sxs-lookup"><span data-stu-id="eecbf-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails</span></span> 
|<span data-ttu-id="eecbf-117">AL</span><span class="sxs-lookup"><span data-stu-id="eecbf-117">GET</span></span>|<span data-ttu-id="eecbf-118">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / usagedetails</span><span class="sxs-lookup"><span data-stu-id="eecbf-118">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails</span></span>|
|<span data-ttu-id="eecbf-119">AL</span><span class="sxs-lookup"><span data-stu-id="eecbf-119">GET</span></span>|<span data-ttu-id="eecbf-120">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / usagedetailsbycustomdate? startTime 2017-01-01 = & endTime 2017-01-10 =</span><span class="sxs-lookup"><span data-stu-id="eecbf-120">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="eecbf-121">API, toouse hello önizleme sürümünü v2 URL yukarıdaki hello v1 ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="eecbf-121">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="eecbf-122">Yanıt</span><span class="sxs-lookup"><span data-stu-id="eecbf-122">Response</span></span>

> <span data-ttu-id="eecbf-123">Toohello olası büyük miktarda veri hello sonuç kümesi havuzda.</span><span class="sxs-lookup"><span data-stu-id="eecbf-123">Due toohello potentially large volume of data hello result set is paged.</span></span> <span data-ttu-id="eecbf-124">Merhaba nextLink özelliği, veri hello sonraki sayfaya hello bağlantı varsa, belirtir.</span><span class="sxs-lookup"><span data-stu-id="eecbf-124">hello nextLink property, if present, specifies hello link for hello next page of data.</span></span> <span data-ttu-id="eecbf-125">Merhaba bağlantı boşsa, hello son sayfasına olan gösterir.</span><span class="sxs-lookup"><span data-stu-id="eecbf-125">If hello link is empty, it denotes that is hello last page.</span></span> 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/><span data-ttu-id="eecbf-126">
**Yanıt özellik tanımları**</span><span class="sxs-lookup"><span data-stu-id="eecbf-126">
**Response property definitions**</span></span>

|<span data-ttu-id="eecbf-127">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="eecbf-127">Property Name</span></span>| <span data-ttu-id="eecbf-128">Tür</span><span class="sxs-lookup"><span data-stu-id="eecbf-128">Type</span></span>| <span data-ttu-id="eecbf-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eecbf-129">Description</span></span>
|-|-|-|
|<span data-ttu-id="eecbf-130">id</span><span class="sxs-lookup"><span data-stu-id="eecbf-130">id</span></span>| <span data-ttu-id="eecbf-131">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-131">string</span></span>| <span data-ttu-id="eecbf-132">Merhaba hello API çağrısı için benzersiz kimlik.</span><span class="sxs-lookup"><span data-stu-id="eecbf-132">hello unique Id for hello API call.</span></span> |
|<span data-ttu-id="eecbf-133">Veri</span><span class="sxs-lookup"><span data-stu-id="eecbf-133">data</span></span>| <span data-ttu-id="eecbf-134">JSON dizisi</span><span class="sxs-lookup"><span data-stu-id="eecbf-134">JSON array</span></span>| <span data-ttu-id="eecbf-135">Merhaba her instance\meter günlük kullanım ayrıntılarını dizisi.</span><span class="sxs-lookup"><span data-stu-id="eecbf-135">hello Array of daily usage details for every instance\meter.</span></span>|
|<span data-ttu-id="eecbf-136">nextLink</span><span class="sxs-lookup"><span data-stu-id="eecbf-136">nextLink</span></span>| <span data-ttu-id="eecbf-137">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-137">string</span></span>| <span data-ttu-id="eecbf-138">Veri sayfasının hello nextLink noktaları toohello URL tooreturn hello sonraki verilerin daha fazla sayfa olduğunda.</span><span class="sxs-lookup"><span data-stu-id="eecbf-138">When there are more pages of data hello nextLink points toohello URL tooreturn hello next page of data.</span></span> |
|<span data-ttu-id="eecbf-139">Hesap Kimliği</span><span class="sxs-lookup"><span data-stu-id="eecbf-139">accountId</span></span>| <span data-ttu-id="eecbf-140">Int</span><span class="sxs-lookup"><span data-stu-id="eecbf-140">int</span></span>| <span data-ttu-id="eecbf-141">Kullanılmayan alan.</span><span class="sxs-lookup"><span data-stu-id="eecbf-141">Obsolete field.</span></span> <span data-ttu-id="eecbf-142">Geriye dönük uyumluluk için mevcut.</span><span class="sxs-lookup"><span data-stu-id="eecbf-142">Present for backward compatibility.</span></span> |
|<span data-ttu-id="eecbf-143">ProductID</span><span class="sxs-lookup"><span data-stu-id="eecbf-143">productId</span></span>| <span data-ttu-id="eecbf-144">Int</span><span class="sxs-lookup"><span data-stu-id="eecbf-144">int</span></span>| <span data-ttu-id="eecbf-145">Kullanılmayan alan.</span><span class="sxs-lookup"><span data-stu-id="eecbf-145">Obsolete field.</span></span> <span data-ttu-id="eecbf-146">Geriye dönük uyumluluk için mevcut.</span><span class="sxs-lookup"><span data-stu-id="eecbf-146">Present for backward compatibility.</span></span> |
|<span data-ttu-id="eecbf-147">resourceLocationId</span><span class="sxs-lookup"><span data-stu-id="eecbf-147">resourceLocationId</span></span>| <span data-ttu-id="eecbf-148">Int</span><span class="sxs-lookup"><span data-stu-id="eecbf-148">int</span></span>| <span data-ttu-id="eecbf-149">Kullanılmayan alan.</span><span class="sxs-lookup"><span data-stu-id="eecbf-149">Obsolete field.</span></span> <span data-ttu-id="eecbf-150">Geriye dönük uyumluluk için mevcut.</span><span class="sxs-lookup"><span data-stu-id="eecbf-150">Present for backward compatibility.</span></span> |
|<span data-ttu-id="eecbf-151">consumedServiceID</span><span class="sxs-lookup"><span data-stu-id="eecbf-151">consumedServiceID</span></span>| <span data-ttu-id="eecbf-152">Int</span><span class="sxs-lookup"><span data-stu-id="eecbf-152">int</span></span>| <span data-ttu-id="eecbf-153">Kullanılmayan alan.</span><span class="sxs-lookup"><span data-stu-id="eecbf-153">Obsolete field.</span></span> <span data-ttu-id="eecbf-154">Geriye dönük uyumluluk için mevcut.</span><span class="sxs-lookup"><span data-stu-id="eecbf-154">Present for backward compatibility.</span></span> |
|<span data-ttu-id="eecbf-155">departmentId</span><span class="sxs-lookup"><span data-stu-id="eecbf-155">departmentId</span></span>| <span data-ttu-id="eecbf-156">Int</span><span class="sxs-lookup"><span data-stu-id="eecbf-156">int</span></span>| <span data-ttu-id="eecbf-157">Kullanılmayan alan.</span><span class="sxs-lookup"><span data-stu-id="eecbf-157">Obsolete field.</span></span> <span data-ttu-id="eecbf-158">Geriye dönük uyumluluk için mevcut.</span><span class="sxs-lookup"><span data-stu-id="eecbf-158">Present for backward compatibility.</span></span> |
|<span data-ttu-id="eecbf-159">accountOwnerEmail</span><span class="sxs-lookup"><span data-stu-id="eecbf-159">accountOwnerEmail</span></span>| <span data-ttu-id="eecbf-160">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-160">string</span></span>| <span data-ttu-id="eecbf-161">Merhaba hesabı sahibinin e-posta hesabı.</span><span class="sxs-lookup"><span data-stu-id="eecbf-161">Email account of hello account owner.</span></span> |
|<span data-ttu-id="eecbf-162">accountName</span><span class="sxs-lookup"><span data-stu-id="eecbf-162">accountName</span></span>| <span data-ttu-id="eecbf-163">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-163">string</span></span>| <span data-ttu-id="eecbf-164">Merhaba hesabının girilen müşteri adı.</span><span class="sxs-lookup"><span data-stu-id="eecbf-164">Customer entered name of hello account.</span></span> |
|<span data-ttu-id="eecbf-165">serviceAdministratorId</span><span class="sxs-lookup"><span data-stu-id="eecbf-165">serviceAdministratorId</span></span>| <span data-ttu-id="eecbf-166">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-166">string</span></span>| <span data-ttu-id="eecbf-167">E-posta adresi, Hizmet Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="eecbf-167">Email Address of Service Administrator.</span></span> |
|<span data-ttu-id="eecbf-168">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="eecbf-168">subscriptionId</span></span>| <span data-ttu-id="eecbf-169">Int</span><span class="sxs-lookup"><span data-stu-id="eecbf-169">int</span></span>| <span data-ttu-id="eecbf-170">Kullanılmayan alan.</span><span class="sxs-lookup"><span data-stu-id="eecbf-170">Obsolete field.</span></span> <span data-ttu-id="eecbf-171">Geriye dönük uyumluluk için mevcut.</span><span class="sxs-lookup"><span data-stu-id="eecbf-171">Present for backward compatibility.</span></span> |
|<span data-ttu-id="eecbf-172">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="eecbf-172">subscriptionGuid</span></span>| <span data-ttu-id="eecbf-173">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-173">string</span></span>| <span data-ttu-id="eecbf-174">Merhaba abonelik için genel benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="eecbf-174">Global Unique Identifier for hello subscription.</span></span> |
|<span data-ttu-id="eecbf-175">varlığıyla subscriptionName</span><span class="sxs-lookup"><span data-stu-id="eecbf-175">subscriptionName</span></span>| <span data-ttu-id="eecbf-176">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-176">string</span></span>| <span data-ttu-id="eecbf-177">Merhaba abonelik adı.</span><span class="sxs-lookup"><span data-stu-id="eecbf-177">Name of hello subscription.</span></span> |
|<span data-ttu-id="eecbf-178">Tarih</span><span class="sxs-lookup"><span data-stu-id="eecbf-178">date</span></span>| <span data-ttu-id="eecbf-179">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-179">string</span></span>| <span data-ttu-id="eecbf-180">Tüketim gerçekleştiği başlangıç tarihi.</span><span class="sxs-lookup"><span data-stu-id="eecbf-180">hello date on which consumption occurred.</span></span> |
|<span data-ttu-id="eecbf-181">Ürün</span><span class="sxs-lookup"><span data-stu-id="eecbf-181">product</span></span>| <span data-ttu-id="eecbf-182">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-182">string</span></span>| <span data-ttu-id="eecbf-183">Merhaba ölçer hakkında daha fazla ayrıntı.</span><span class="sxs-lookup"><span data-stu-id="eecbf-183">Additional details on hello meter.</span></span> <span data-ttu-id="eecbf-184">Örnek: A1 (VM) Windows - AP Doğu</span><span class="sxs-lookup"><span data-stu-id="eecbf-184">Example: A1(VM)Windows - AP East</span></span>|
|<span data-ttu-id="eecbf-185">meterId</span><span class="sxs-lookup"><span data-stu-id="eecbf-185">meterId</span></span>| <span data-ttu-id="eecbf-186">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-186">string</span></span>| <span data-ttu-id="eecbf-187">Kullanım yayılan hello ölçer Hello tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="eecbf-187">hello identifier for hello meter which emitted usage.</span></span> |
|<span data-ttu-id="eecbf-188">meterCategory</span><span class="sxs-lookup"><span data-stu-id="eecbf-188">meterCategory</span></span>| <span data-ttu-id="eecbf-189">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-189">string</span></span>| <span data-ttu-id="eecbf-190">Merhaba kullanılan Azure platformu hizmeti.</span><span class="sxs-lookup"><span data-stu-id="eecbf-190">hello Azure platform service that was used.</span></span> |
|<span data-ttu-id="eecbf-191">meterSubCategory</span><span class="sxs-lookup"><span data-stu-id="eecbf-191">meterSubCategory</span></span>| <span data-ttu-id="eecbf-192">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-192">string</span></span>| <span data-ttu-id="eecbf-193">Merhaba hızını etkileyebilir hello Azure hizmet türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="eecbf-193">Defines hello Azure service type that can affect hello rate.</span></span> <span data-ttu-id="eecbf-194">Örnek: A1 VM (Windows dışı</span><span class="sxs-lookup"><span data-stu-id="eecbf-194">Example: A1 VM (Non-Windows</span></span>|
|<span data-ttu-id="eecbf-195">meterRegion</span><span class="sxs-lookup"><span data-stu-id="eecbf-195">meterRegion</span></span>| <span data-ttu-id="eecbf-196">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-196">string</span></span>| <span data-ttu-id="eecbf-197">Veri merkezi konum temelinde fiyatlandırılır belirli hizmetleri için hello datacenter Hello konumunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="eecbf-197">Identifies hello location of hello datacenter for certain services that are priced based on datacenter location.</span></span> |
|<span data-ttu-id="eecbf-198">meterName</span><span class="sxs-lookup"><span data-stu-id="eecbf-198">meterName</span></span>| <span data-ttu-id="eecbf-199">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-199">string</span></span>| <span data-ttu-id="eecbf-200">Merhaba ölçüm adı.</span><span class="sxs-lookup"><span data-stu-id="eecbf-200">Name of hello meter.</span></span> |
|<span data-ttu-id="eecbf-201">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="eecbf-201">consumedQuantity</span></span>| <span data-ttu-id="eecbf-202">Çift</span><span class="sxs-lookup"><span data-stu-id="eecbf-202">double</span></span>| <span data-ttu-id="eecbf-203">Merhaba kullanılmış hello ölçer miktarı.</span><span class="sxs-lookup"><span data-stu-id="eecbf-203">hello amount of hello meter that has been consumed.</span></span> |
|<span data-ttu-id="eecbf-204">resourceRate</span><span class="sxs-lookup"><span data-stu-id="eecbf-204">resourceRate</span></span>| <span data-ttu-id="eecbf-205">Çift</span><span class="sxs-lookup"><span data-stu-id="eecbf-205">double</span></span>| <span data-ttu-id="eecbf-206">Merhaba oranı Faturalanabilir birim başına uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="eecbf-206">hello rate applicable per billable unit.</span></span> |
|<span data-ttu-id="eecbf-207">Maliyet</span><span class="sxs-lookup"><span data-stu-id="eecbf-207">cost</span></span>| <span data-ttu-id="eecbf-208">Çift</span><span class="sxs-lookup"><span data-stu-id="eecbf-208">double</span></span>| <span data-ttu-id="eecbf-209">Merhaba ölçer ücrete hello gider.</span><span class="sxs-lookup"><span data-stu-id="eecbf-209">hello charge that has been incurred for hello meter.</span></span> |
|<span data-ttu-id="eecbf-210">resourceLocation</span><span class="sxs-lookup"><span data-stu-id="eecbf-210">resourceLocation</span></span>| <span data-ttu-id="eecbf-211">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-211">string</span></span>| <span data-ttu-id="eecbf-212">Merhaba ölçer çalıştığı hello datacenter tanımlar.</span><span class="sxs-lookup"><span data-stu-id="eecbf-212">Identifies hello datacenter where hello meter is running.</span></span> |
|<span data-ttu-id="eecbf-213">consumedService</span><span class="sxs-lookup"><span data-stu-id="eecbf-213">consumedService</span></span>| <span data-ttu-id="eecbf-214">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-214">string</span></span>| <span data-ttu-id="eecbf-215">Merhaba kullanılan Azure platformu hizmeti.</span><span class="sxs-lookup"><span data-stu-id="eecbf-215">hello Azure platform service that was used.</span></span> |
|<span data-ttu-id="eecbf-216">örnek kimliği</span><span class="sxs-lookup"><span data-stu-id="eecbf-216">instanceId</span></span>| <span data-ttu-id="eecbf-217">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-217">string</span></span>| <span data-ttu-id="eecbf-218">Bu tanımlayıcı hello hello kaynak adıdır veya hello tam kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="eecbf-218">This identifier is hello name of hello resource or hello fully qualified Resource ID.</span></span> <span data-ttu-id="eecbf-219">Daha fazla bilgi için bkz: [Azure Kaynak Yöneticisi API'si](https://docs.microsoft.com/rest/api/resources/resources)</span><span class="sxs-lookup"><span data-stu-id="eecbf-219">For more information, see [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)</span></span> |
|<span data-ttu-id="eecbf-220">serviceInfo1</span><span class="sxs-lookup"><span data-stu-id="eecbf-220">serviceInfo1</span></span>| <span data-ttu-id="eecbf-221">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-221">string</span></span>| <span data-ttu-id="eecbf-222">İç Azure hizmeti meta verileri.</span><span class="sxs-lookup"><span data-stu-id="eecbf-222">Internal Azure Service Metadata.</span></span> |
|<span data-ttu-id="eecbf-223">serviceInfo2</span><span class="sxs-lookup"><span data-stu-id="eecbf-223">serviceInfo2</span></span>| <span data-ttu-id="eecbf-224">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-224">string</span></span>| <span data-ttu-id="eecbf-225">Örneğin, bir görüntü türü için bir sanal makine ve ExpressRoute ISS adı.</span><span class="sxs-lookup"><span data-stu-id="eecbf-225">For example, an image type for a virtual machine and ISP name for ExpressRoute.</span></span> |
|<span data-ttu-id="eecbf-226">additionalınfo alanına</span><span class="sxs-lookup"><span data-stu-id="eecbf-226">additionalInfo</span></span>| <span data-ttu-id="eecbf-227">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-227">string</span></span>| <span data-ttu-id="eecbf-228">Hizmete özgü meta veriler.</span><span class="sxs-lookup"><span data-stu-id="eecbf-228">Service-specific metadata.</span></span> <span data-ttu-id="eecbf-229">Örneğin, bir görüntü türü için bir sanal makine.</span><span class="sxs-lookup"><span data-stu-id="eecbf-229">For example, an image type for a virtual machine.</span></span> |
|<span data-ttu-id="eecbf-230">etiketler</span><span class="sxs-lookup"><span data-stu-id="eecbf-230">tags</span></span>| <span data-ttu-id="eecbf-231">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-231">string</span></span>| <span data-ttu-id="eecbf-232">Müşteri etiketleri eklendi.</span><span class="sxs-lookup"><span data-stu-id="eecbf-232">Customer added tags.</span></span> <span data-ttu-id="eecbf-233">Daha fazla bilgi için bkz: [etiketlerle Azure kaynaklarınızı düzenleme](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags).</span><span class="sxs-lookup"><span data-stu-id="eecbf-233">For more information, see [Organize your Azure resources with tags](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags).</span></span> |
|<span data-ttu-id="eecbf-234">storeServiceIdentifier</span><span class="sxs-lookup"><span data-stu-id="eecbf-234">storeServiceIdentifier</span></span>| <span data-ttu-id="eecbf-235">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-235">string</span></span>| <span data-ttu-id="eecbf-236">Bu sütunlar kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="eecbf-236">This columns is not used.</span></span> <span data-ttu-id="eecbf-237">Geriye dönük uyumluluk için mevcut.</span><span class="sxs-lookup"><span data-stu-id="eecbf-237">Present for backward compatibility.</span></span> |
|<span data-ttu-id="eecbf-238">departmentName</span><span class="sxs-lookup"><span data-stu-id="eecbf-238">departmentName</span></span>| <span data-ttu-id="eecbf-239">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-239">string</span></span>| <span data-ttu-id="eecbf-240">Merhaba bölüm adı.</span><span class="sxs-lookup"><span data-stu-id="eecbf-240">Name of hello department.</span></span> |
|<span data-ttu-id="eecbf-241">costCenter</span><span class="sxs-lookup"><span data-stu-id="eecbf-241">costCenter</span></span>| <span data-ttu-id="eecbf-242">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-242">string</span></span>| <span data-ttu-id="eecbf-243">Merhaba kullanımı ile ilişkili hello maliyet merkezi.</span><span class="sxs-lookup"><span data-stu-id="eecbf-243">hello cost center that hello usage is associated with.</span></span> |
|<span data-ttu-id="eecbf-244">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="eecbf-244">unitOfMeasure</span></span>| <span data-ttu-id="eecbf-245">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-245">string</span></span>| <span data-ttu-id="eecbf-246">Merhaba hizmet içinde doludur hello birimi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="eecbf-246">Identifies hello unit that hello service is charged in.</span></span> <span data-ttu-id="eecbf-247">Örnek: GB, saat, 10.000 s.</span><span class="sxs-lookup"><span data-stu-id="eecbf-247">Example: GB, hours, 10,000 s.</span></span> |
|<span data-ttu-id="eecbf-248">kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="eecbf-248">resourceGroup</span></span>| <span data-ttu-id="eecbf-249">Dize</span><span class="sxs-lookup"><span data-stu-id="eecbf-249">string</span></span>| <span data-ttu-id="eecbf-250">Merhaba kaynak grubu hangi hello dağıtılan ölçer çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="eecbf-250">hello resource group in which hello deployed meter is running in.</span></span> <span data-ttu-id="eecbf-251">Daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="eecbf-251">For more information, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span> |
<br/>
## <a name="see-also"></a><span data-ttu-id="eecbf-252">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="eecbf-252">See also</span></span>

* [<span data-ttu-id="eecbf-253">Faturalama nokta API</span><span class="sxs-lookup"><span data-stu-id="eecbf-253">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="eecbf-254">Bakiye ve özeti API</span><span class="sxs-lookup"><span data-stu-id="eecbf-254">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="eecbf-255">Market deposu ücret API</span><span class="sxs-lookup"><span data-stu-id="eecbf-255">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="eecbf-256">Fiyat listesi API'si</span><span class="sxs-lookup"><span data-stu-id="eecbf-256">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)

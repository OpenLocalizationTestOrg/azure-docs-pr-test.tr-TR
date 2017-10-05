---
title: "Logic Apps B2B listesi hatalar ve çözümleri: Azure App Service | Microsoft Docs"
description: "Logic Apps B2B listesi hatalar ve çözümleri"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1865d75f1b4c2aa18d5a3130f639572d19563b3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="244ee-103">Logic Apps B2B listesi hatalar ve çözümleri</span><span class="sxs-lookup"><span data-stu-id="244ee-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="244ee-104">Bu makalede mantığını uygulamaları B2B senaryolarda oluşabilir ve bu hataların düzeltilmesi için uygun eylemleri öneren hatalarında sorun giderme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="244ee-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="244ee-105">Anlaşma çözümleme</span><span class="sxs-lookup"><span data-stu-id="244ee-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="244ee-106">* Hiçbir sözleşmesi bulunamadı</span><span class="sxs-lookup"><span data-stu-id="244ee-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="244ee-107">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-107">Error description</span></span> | <span data-ttu-id="244ee-108">Anlaşma çözümleme parametrelerle bulunan hiçbir Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="244ee-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="244ee-109">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-109">User action</span></span> | <span data-ttu-id="244ee-110">Üzerinde anlaşılan iş kimliklerle tümleştirme hesabına sözleşmesi eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="244ee-110">The agreement should be added to the integration account with agreed business identities.</span></span></br> <span data-ttu-id="244ee-111">İş kimlikleri için giriş iletisi kimlikleri eşleşmelidir</span><span class="sxs-lookup"><span data-stu-id="244ee-111">The business identities should match to the input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="244ee-112">* Kimliklerle bulunan hiçbir Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="244ee-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="244ee-113">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-113">Error description</span></span> | <span data-ttu-id="244ee-114">Kimliklerle bulunan hiçbir sözleşmesi: 'AS2Identity':: 'Partner1' ve 'AS2Identity':: 'Partner3'</span><span class="sxs-lookup"><span data-stu-id="244ee-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="244ee-115">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-115">User action</span></span> | <span data-ttu-id="244ee-116">Geçersiz AS2-gelen veya AS2-anlaşma için için yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="244ee-116">Invalid AS2-From or AS2-To configured for agreement.</span></span> </br> <span data-ttu-id="244ee-117">Doğru AS2 ileti AS2-gelen veya AS2-üstbilgileri veya AS2 AS2 kimlikleriyle eşleşen anlaşma ileti sözleşmesi yapılandırmalarla üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="244ee-117">Correct AS2 message AS2-From or AS2-To headers or agreement to match AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="244ee-118">AS2</span><span class="sxs-lookup"><span data-stu-id="244ee-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="244ee-119">* AS2 ileti üstbilgilerini eksik</span><span class="sxs-lookup"><span data-stu-id="244ee-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="244ee-120">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-120">Error description</span></span>| <span data-ttu-id="244ee-121">Geçersiz AS2 üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="244ee-121">Invalid AS2 headers.</span></span> <span data-ttu-id="244ee-122">Aşağıdakilerden birini ' AS2-için ' veya ' AS2-gelen ' üstbilgileri boş</span><span class="sxs-lookup"><span data-stu-id="244ee-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="244ee-123">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-123">User action</span></span> | <span data-ttu-id="244ee-124">AS2 içermeyen bir AS2 iletisi alındı-gelen veya AS2-için veya her iki üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="244ee-124">An AS2 message was received that did not contain the AS2-From or AS2-To or both headers.</span></span> </br> <span data-ttu-id="244ee-125">AS2 ileti AS2 denetleyin-gelen ve AS2-üstbilgileri ve doğru bunları sözleşmesi yapılandırmasını temel alarak</span><span class="sxs-lookup"><span data-stu-id="244ee-125">Check AS2 message AS2-From and AS2-To headers and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="244ee-126">* Eksik AS2 ileti gövdesi ve üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="244ee-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="244ee-127">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-127">Error description</span></span>| <span data-ttu-id="244ee-128">İstek içeriği null veya boş</span><span class="sxs-lookup"><span data-stu-id="244ee-128">The request content is null or empty</span></span> | 
| <span data-ttu-id="244ee-129">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-129">User action</span></span> | <span data-ttu-id="244ee-130">İleti gövdesi içermeyen bir AS2 iletisi alındı</span><span class="sxs-lookup"><span data-stu-id="244ee-130">An AS2 message was received that did not contain the message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="244ee-131">* AS2 ileti şifre çözme hatası</span><span class="sxs-lookup"><span data-stu-id="244ee-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="244ee-132">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-132">Error description</span></span> |  <span data-ttu-id="244ee-133">[işlenen hata: şifre çözme başarısız oldu]</span><span class="sxs-lookup"><span data-stu-id="244ee-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="244ee-134">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-134">User action</span></span> | <span data-ttu-id="244ee-135">Ekleme @base64ToBinary göndermeden önce AS2Message için ortağına</span><span class="sxs-lookup"><span data-stu-id="244ee-135">Add @base64ToBinary to AS2Message before sending to partner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="244ee-136">* MDN şifre çözme hatası</span><span class="sxs-lookup"><span data-stu-id="244ee-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="244ee-137">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-137">Error description</span></span> |  <span data-ttu-id="244ee-138">[işlenen hata: şifre çözme başarısız oldu]</span><span class="sxs-lookup"><span data-stu-id="244ee-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="244ee-139">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-139">User action</span></span> | <span data-ttu-id="244ee-140">Ekleme @base64ToBinary göndermeden önce MDN için ortağına</span><span class="sxs-lookup"><span data-stu-id="244ee-140">Add @base64ToBinary to MDN before sending to partner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="244ee-141">* Eksik imzalama sertifikası</span><span class="sxs-lookup"><span data-stu-id="244ee-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="244ee-142">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-142">Error description</span></span>| <span data-ttu-id="244ee-143">İmzalama sertifikası AS2 taraf için yapılandırılmadı.</span><span class="sxs-lookup"><span data-stu-id="244ee-143">The Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="244ee-144">AS2-gelen: partner1 AS2-için: partner2</span><span class="sxs-lookup"><span data-stu-id="244ee-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="244ee-145">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-145">User action</span></span> | <span data-ttu-id="244ee-146">İmza için doğru sertifika ile AS2 sözleşmesi ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="244ee-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="244ee-147">X12 ve EDIFACT</span><span class="sxs-lookup"><span data-stu-id="244ee-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="244ee-148">* Baştaki veya sondaki boşlukları bulundu</span><span class="sxs-lookup"><span data-stu-id="244ee-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="244ee-149">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-149">Error description</span></span> | <span data-ttu-id="244ee-150">Ayrıştırma sırasında ile karşılaşıldı.</span><span class="sxs-lookup"><span data-stu-id="244ee-150">Error encountered during parsing.</span></span> <span data-ttu-id="244ee-151">EDIFACT işlem kümesi ' 123456 kimliği ile 'kimlikli ' 987654 (olmadan, Grup) değişim, gönderen Kimliği 'Partner1' içindeki', 'Partner2' alıcının kimliği şu hatalarla askıya: baştaki boşlukları ayırıcısı bulundu</span><span class="sxs-lookup"><span data-stu-id="244ee-151">The Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="244ee-152">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-152">User action</span></span> | <span data-ttu-id="244ee-153">Baştaki ve sondaki boşlukları izin verecek şekilde yapılandırılması sözleşmesi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="244ee-153">The agreement settings to be configured to allow leading and trailing space.</span></span> </br> <span data-ttu-id="244ee-154">Baştaki ve sondaki boşluk izin vermek üzere anlaşma ayarlarını Düzenle</span><span class="sxs-lookup"><span data-stu-id="244ee-154">Edit agreement settings to allow leading and trailing space</span></span> |
|   |   |

![alan izin ver](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-the-agreement"></a><span data-ttu-id="244ee-156">* Yinelenen onay anlaşmasında etkinleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="244ee-156">* Duplicate check has enabled in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="244ee-157">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-157">Error description</span></span> | <span data-ttu-id="244ee-158">Yinelenen denetim sayısı</span><span class="sxs-lookup"><span data-stu-id="244ee-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="244ee-159">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-159">User action</span></span> | <span data-ttu-id="244ee-160">Bu hata, yinelenen denetim numaraları alınan ileti olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="244ee-160">This error indicates the received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="244ee-161">Denetim numarayı düzeltin ve iletiyi yeniden gönderin</span><span class="sxs-lookup"><span data-stu-id="244ee-161">Correct the control number and resend the message</span></span> |
|   |   |

### <a name="-missing-schema-in-the-agreement"></a><span data-ttu-id="244ee-162">* Eksik şema Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="244ee-162">* Missing schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="244ee-163">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-163">Error description</span></span> | <span data-ttu-id="244ee-164">Ayrıştırma sırasında ile karşılaşıldı.</span><span class="sxs-lookup"><span data-stu-id="244ee-164">Error encountered during parsing.</span></span> <span data-ttu-id="244ee-165">Kimliğine sahip '564220001' bulunan işlevsel grubunda Kimliği '56422', '000056422' Gönderen Kimliği ' 12345678 kimlikli değişim içinde', alıcı kimliği ' 87654321' işlem kümesi şu hatalarla askıya X12 "iletisi bir bilinmeyen belge türüne sahip bir ND anlaşmasında yapılandırılmış mevcut şemaları hiçbirine çözümlenmedi"</span><span class="sxs-lookup"><span data-stu-id="244ee-165">The X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement"</span></span> |
| <span data-ttu-id="244ee-166">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-166">User action</span></span> | <span data-ttu-id="244ee-167">Şema sözleşmesi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="244ee-167">Configure schema in the agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-the-agreement"></a><span data-ttu-id="244ee-168">* Yanlış şema Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="244ee-168">* Incorrect schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="244ee-169">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-169">Error description</span></span> | <span data-ttu-id="244ee-170">İleti bir bilinmeyen belge türüne sahip ve herhangi bir anlaşmayı yapılandırılmış mevcut şemaları çözümlenmedi.</span><span class="sxs-lookup"><span data-stu-id="244ee-170">The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement.</span></span> |
| <span data-ttu-id="244ee-171">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-171">User action</span></span> | <span data-ttu-id="244ee-172">Doğru şemayı sözleşmesi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="244ee-172">Configure correct schema in the agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="244ee-173">Düz dosya</span><span class="sxs-lookup"><span data-stu-id="244ee-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="244ee-174">* Hiçbir gövde ile giriş iletisi</span><span class="sxs-lookup"><span data-stu-id="244ee-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="244ee-175">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="244ee-175">Error description</span></span> | <span data-ttu-id="244ee-176">InvalidTemplate.</span><span class="sxs-lookup"><span data-stu-id="244ee-176">InvalidTemplate.</span></span> <span data-ttu-id="244ee-177">İşlem şablonu dili '1' satır ve sütun '1902' eylemi 'Flat_File_Decoding' girişleri ifadelerinde alınamıyor: ' özelliği 'content' bekler bir değer ancak taşınmadığını null gerekli.</span><span class="sxs-lookup"><span data-stu-id="244ee-177">Unable to process template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="244ee-178">Yol ''.'.</span><span class="sxs-lookup"><span data-stu-id="244ee-178">Path ''.'.</span></span> |
| <span data-ttu-id="244ee-179">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="244ee-179">User action</span></span> | <span data-ttu-id="244ee-180">Bu hata, giriş iletisi bir gövdesi içermiyor belirtir.</span><span class="sxs-lookup"><span data-stu-id="244ee-180">This error indicates the input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="244ee-181">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="244ee-181">Learn more</span></span>
[<span data-ttu-id="244ee-182">Enterprise Integration Pack hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="244ee-182">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
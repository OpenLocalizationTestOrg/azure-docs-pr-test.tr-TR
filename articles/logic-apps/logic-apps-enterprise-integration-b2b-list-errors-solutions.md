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
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="227c4-103">Logic Apps B2B listesi hatalar ve çözümleri</span><span class="sxs-lookup"><span data-stu-id="227c4-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="227c4-104">Bu makalede mantığını uygulamaları B2B senaryolarda oluşabilir ve bu hataların düzeltilmesi için uygun eylemleri öneren hatalarında sorun giderme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="227c4-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="227c4-105">Anlaşma çözümleme</span><span class="sxs-lookup"><span data-stu-id="227c4-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="227c4-106">* Hiçbir sözleşmesi bulunamadı</span><span class="sxs-lookup"><span data-stu-id="227c4-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="227c4-107">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-107">Error description</span></span> | <span data-ttu-id="227c4-108">Anlaşma çözümleme parametrelerle bulunan hiçbir Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="227c4-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="227c4-109">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-109">User action</span></span> | <span data-ttu-id="227c4-110">Merhaba anlaşma toohello tümleştirme hesap üzerinde anlaşılan iş kimliklerle eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="227c4-110">hello agreement should be added toohello integration account with agreed business identities.</span></span></br> <span data-ttu-id="227c4-111">Merhaba iş kimlikleri toohello giriş iletisi kimlikleri eşleşmelidir</span><span class="sxs-lookup"><span data-stu-id="227c4-111">hello business identities should match toohello input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="227c4-112">* Kimliklerle bulunan hiçbir Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="227c4-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="227c4-113">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-113">Error description</span></span> | <span data-ttu-id="227c4-114">Kimliklerle bulunan hiçbir sözleşmesi: 'AS2Identity':: 'Partner1' ve 'AS2Identity':: 'Partner3'</span><span class="sxs-lookup"><span data-stu-id="227c4-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="227c4-115">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-115">User action</span></span> | <span data-ttu-id="227c4-116">Geçersiz AS2-gelen veya AS2 tooconfigured anlaşması için.</span><span class="sxs-lookup"><span data-stu-id="227c4-116">Invalid AS2-From or AS2-tooconfigured for agreement.</span></span> </br> <span data-ttu-id="227c4-117">Doğru AS2 ileti AS2-gelen veya AS2 AS2 tooheaders veya anlaşma toomatch AS2 kimlikleri ileti sözleşmesi yapılandırmalarla üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="227c4-117">Correct AS2 message AS2-From or AS2-tooheaders or agreement toomatch AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="227c4-118">AS2</span><span class="sxs-lookup"><span data-stu-id="227c4-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="227c4-119">* AS2 ileti üstbilgilerini eksik</span><span class="sxs-lookup"><span data-stu-id="227c4-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="227c4-120">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-120">Error description</span></span>| <span data-ttu-id="227c4-121">Geçersiz AS2 üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="227c4-121">Invalid AS2 headers.</span></span> <span data-ttu-id="227c4-122">Aşağıdakilerden birini ' AS2-için ' veya ' AS2-gelen ' üstbilgileri boş</span><span class="sxs-lookup"><span data-stu-id="227c4-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="227c4-123">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-123">User action</span></span> | <span data-ttu-id="227c4-124">Merhaba AS2 içermeyen bir AS2 iletisi alındı-gelen veya AS2 tooor hem üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="227c4-124">An AS2 message was received that did not contain hello AS2-From or AS2-tooor both headers.</span></span> </br> <span data-ttu-id="227c4-125">AS2 ileti AS2 denetleyin-gelen ve AS2 tooheaders ve anlaşma yapılandırmasını temel alarak düzeltin</span><span class="sxs-lookup"><span data-stu-id="227c4-125">Check AS2 message AS2-From and AS2-tooheaders and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="227c4-126">* Eksik AS2 ileti gövdesi ve üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="227c4-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="227c4-127">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-127">Error description</span></span>| <span data-ttu-id="227c4-128">Merhaba istek içeriği null veya boş</span><span class="sxs-lookup"><span data-stu-id="227c4-128">hello request content is null or empty</span></span> | 
| <span data-ttu-id="227c4-129">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-129">User action</span></span> | <span data-ttu-id="227c4-130">Merhaba ileti gövdesi içermeyen bir AS2 iletisi alındı</span><span class="sxs-lookup"><span data-stu-id="227c4-130">An AS2 message was received that did not contain hello message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="227c4-131">* AS2 ileti şifre çözme hatası</span><span class="sxs-lookup"><span data-stu-id="227c4-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="227c4-132">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-132">Error description</span></span> |  <span data-ttu-id="227c4-133">[işlenen hata: şifre çözme başarısız oldu]</span><span class="sxs-lookup"><span data-stu-id="227c4-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="227c4-134">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-134">User action</span></span> | <span data-ttu-id="227c4-135">Ekleme @base64ToBinary toopartner göndermeden önce tooAS2Message</span><span class="sxs-lookup"><span data-stu-id="227c4-135">Add @base64ToBinary tooAS2Message before sending toopartner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="227c4-136">* MDN şifre çözme hatası</span><span class="sxs-lookup"><span data-stu-id="227c4-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="227c4-137">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-137">Error description</span></span> |  <span data-ttu-id="227c4-138">[işlenen hata: şifre çözme başarısız oldu]</span><span class="sxs-lookup"><span data-stu-id="227c4-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="227c4-139">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-139">User action</span></span> | <span data-ttu-id="227c4-140">Ekleme @base64ToBinary toopartner göndermeden önce tooMDN</span><span class="sxs-lookup"><span data-stu-id="227c4-140">Add @base64ToBinary tooMDN before sending toopartner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="227c4-141">* Eksik imzalama sertifikası</span><span class="sxs-lookup"><span data-stu-id="227c4-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="227c4-142">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-142">Error description</span></span>| <span data-ttu-id="227c4-143">Merhaba imzalama sertifikası AS2 taraf için yapılandırılmadı.</span><span class="sxs-lookup"><span data-stu-id="227c4-143">hello Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="227c4-144">AS2-gelen: partner1 AS2-için: partner2</span><span class="sxs-lookup"><span data-stu-id="227c4-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="227c4-145">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-145">User action</span></span> | <span data-ttu-id="227c4-146">İmza için doğru sertifika ile AS2 sözleşmesi ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="227c4-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="227c4-147">X12 ve EDIFACT</span><span class="sxs-lookup"><span data-stu-id="227c4-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="227c4-148">* Baştaki veya sondaki boşlukları bulundu</span><span class="sxs-lookup"><span data-stu-id="227c4-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="227c4-149">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-149">Error description</span></span> | <span data-ttu-id="227c4-150">Ayrıştırma sırasında ile karşılaşıldı.</span><span class="sxs-lookup"><span data-stu-id="227c4-150">Error encountered during parsing.</span></span> <span data-ttu-id="227c4-151">'değişim (olmadan, Grup) kimliğine sahip ' 987654 bulunan' ID ' 123456 kümesiyle EDIFACT işlem Merhaba, gönderen Kimliği 'Partner1' ile 'Partner2' alıcının kimliği şu hatalarla askıya alındı: baştaki boşlukları ayırıcısı bulundu</span><span class="sxs-lookup"><span data-stu-id="227c4-151">hello Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="227c4-152">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-152">User action</span></span> | <span data-ttu-id="227c4-153">Merhaba sözleşmesi ayarları toobe baştaki ve sondaki boşlukları tooallow yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="227c4-153">hello agreement settings toobe configured tooallow leading and trailing space.</span></span> </br> <span data-ttu-id="227c4-154">Baştaki ve sondaki boşlukları sözleşmesi ayarları tooallow Düzenle</span><span class="sxs-lookup"><span data-stu-id="227c4-154">Edit agreement settings tooallow leading and trailing space</span></span> |
|   |   |

![alan izin ver](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a><span data-ttu-id="227c4-156">* Yinelenen onay hello anlaşmasında etkinleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="227c4-156">* Duplicate check has enabled in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="227c4-157">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-157">Error description</span></span> | <span data-ttu-id="227c4-158">Yinelenen denetim sayısı</span><span class="sxs-lookup"><span data-stu-id="227c4-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="227c4-159">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-159">User action</span></span> | <span data-ttu-id="227c4-160">Bu hata, yinelenen denetim numaraları alınan selamlama iletisine olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="227c4-160">This error indicates hello received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="227c4-161">Merhaba denetim numarayı düzeltin ve selamlama iletisine yeniden gönderin</span><span class="sxs-lookup"><span data-stu-id="227c4-161">Correct hello control number and resend hello message</span></span> |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a><span data-ttu-id="227c4-162">* Eksik şema hello Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="227c4-162">* Missing schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="227c4-163">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-163">Error description</span></span> | <span data-ttu-id="227c4-164">Ayrıştırma sırasında ile karşılaşıldı.</span><span class="sxs-lookup"><span data-stu-id="227c4-164">Error encountered during parsing.</span></span> <span data-ttu-id="227c4-165">kimliğine sahip '564220001' kimlikli '56422', '000056422' kimlikli Gönderen Kimliği ' 12345678 değişim içinde', işlevsel grubu alıcı kimliği ' 87654321 yer alan' hello X12 işlem kümesi şu hatalarla "Merhaba ileti bilinmeyen belge ty var askıya alındı PE ve tooany hello varolan şema hello anlaşmasında yapılandırılmış çözümlenmedi "</span><span class="sxs-lookup"><span data-stu-id="227c4-165">hello X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement"</span></span> |
| <span data-ttu-id="227c4-166">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-166">User action</span></span> | <span data-ttu-id="227c4-167">Şema hello sözleşmesi ayarları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="227c4-167">Configure schema in hello agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a><span data-ttu-id="227c4-168">* Yanlış şema hello Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="227c4-168">* Incorrect schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="227c4-169">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-169">Error description</span></span> | <span data-ttu-id="227c4-170">Merhaba ileti bilinmeyen belge türüne sahip ve tooany hello varolan şema hello anlaşmasında yapılandırılmış çözümlenmedi.</span><span class="sxs-lookup"><span data-stu-id="227c4-170">hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement.</span></span> |
| <span data-ttu-id="227c4-171">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-171">User action</span></span> | <span data-ttu-id="227c4-172">Doğru şemayı hello sözleşmesi ayarlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="227c4-172">Configure correct schema in hello agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="227c4-173">Düz dosya</span><span class="sxs-lookup"><span data-stu-id="227c4-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="227c4-174">* Hiçbir gövde ile giriş iletisi</span><span class="sxs-lookup"><span data-stu-id="227c4-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="227c4-175">Hata açıklaması</span><span class="sxs-lookup"><span data-stu-id="227c4-175">Error description</span></span> | <span data-ttu-id="227c4-176">InvalidTemplate.</span><span class="sxs-lookup"><span data-stu-id="227c4-176">InvalidTemplate.</span></span> <span data-ttu-id="227c4-177">'1' satır ve sütun '1902' eylemi 'Flat_File_Decoding' girişleri oluşturulamıyor tooprocess şablon dili ifadelerinde: ' özelliği 'content' bekler bir değer ancak taşınmadığını null gerekli.</span><span class="sxs-lookup"><span data-stu-id="227c4-177">Unable tooprocess template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="227c4-178">Yol ''.'.</span><span class="sxs-lookup"><span data-stu-id="227c4-178">Path ''.'.</span></span> |
| <span data-ttu-id="227c4-179">Kullanıcı eylemi</span><span class="sxs-lookup"><span data-stu-id="227c4-179">User action</span></span> | <span data-ttu-id="227c4-180">Bu hata hello giriş ileti Gövde içermiyor belirtir.</span><span class="sxs-lookup"><span data-stu-id="227c4-180">This error indicates hello input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="227c4-181">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="227c4-181">Learn more</span></span>
[<span data-ttu-id="227c4-182">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="227c4-182">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)

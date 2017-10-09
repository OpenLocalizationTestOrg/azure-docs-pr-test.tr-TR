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
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a>Logic Apps B2B listesi hatalar ve çözümleri  
Bu makalede mantığını uygulamaları B2B senaryolarda oluşabilir ve bu hataların düzeltilmesi için uygun eylemleri öneren hatalarında sorun giderme yardımcı olur.


## <a name="agreement-resolution"></a>Anlaşma çözümleme

### <a name="no-agreement-found"></a>* Hiçbir sözleşmesi bulunamadı 

|   |   |  
|---|---|
| Hata açıklaması | Anlaşma çözümleme parametrelerle bulunan hiçbir Sözleşmesi|    
| Kullanıcı eylemi | Merhaba anlaşma toohello tümleştirme hesap üzerinde anlaşılan iş kimliklerle eklenmelidir.</br> Merhaba iş kimlikleri toohello giriş iletisi kimlikleri eşleşmelidir|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a>* Kimliklerle bulunan hiçbir Sözleşmesi

|   |   | 
|---|---|
| Hata açıklaması | Kimliklerle bulunan hiçbir sözleşmesi: 'AS2Identity':: 'Partner1' ve 'AS2Identity':: 'Partner3'| 
| Kullanıcı eylemi | Geçersiz AS2-gelen veya AS2 tooconfigured anlaşması için. </br> Doğru AS2 ileti AS2-gelen veya AS2 AS2 tooheaders veya anlaşma toomatch AS2 kimlikleri ileti sözleşmesi yapılandırmalarla üstbilgileri |
|   |   |     

## <a name="as2"></a>AS2

### <a name="-missing-as2-message-headers"></a>* AS2 ileti üstbilgilerini eksik  

|   |   |  
|---|---|
| Hata açıklaması| Geçersiz AS2 üstbilgileri. Aşağıdakilerden birini ' AS2-için ' veya ' AS2-gelen ' üstbilgileri boş| 
| Kullanıcı eylemi | Merhaba AS2 içermeyen bir AS2 iletisi alındı-gelen veya AS2 tooor hem üstbilgileri. </br> AS2 ileti AS2 denetleyin-gelen ve AS2 tooheaders ve anlaşma yapılandırmasını temel alarak düzeltin |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a>* Eksik AS2 ileti gövdesi ve üstbilgileri    

|   |   |  
|---|---|
| Hata açıklaması| Merhaba istek içeriği null veya boş | 
| Kullanıcı eylemi | Merhaba ileti gövdesi içermeyen bir AS2 iletisi alındı |
|  |  | 

### <a name="-as2-message-decryption-failure"></a>* AS2 ileti şifre çözme hatası

|   |   | 
|---|---|
| Hata açıklaması |  [işlenen hata: şifre çözme başarısız oldu] | 
| Kullanıcı eylemi | Ekleme @base64ToBinary toopartner göndermeden önce tooAS2Message 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a>* MDN şifre çözme hatası

|   |   | 
|---|---|
| Hata açıklaması |  [işlenen hata: şifre çözme başarısız oldu] | 
| Kullanıcı eylemi | Ekleme @base64ToBinary toopartner göndermeden önce tooMDN 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a>* Eksik imzalama sertifikası

|   |   |  
|---|---|
| Hata açıklaması| Merhaba imzalama sertifikası AS2 taraf için yapılandırılmadı. </br> AS2-gelen: partner1 AS2-için: partner2 | 
| Kullanıcı eylemi | İmza için doğru sertifika ile AS2 sözleşmesi ayarlarını yapılandırma |
|  |  | 

## <a name="x12-and-edifact"></a>X12 ve EDIFACT

### <a name="-leading-or-trailing-space-found"></a>* Baştaki veya sondaki boşlukları bulundu    
    
|   |   | 
|---|---|
| Hata açıklaması | Ayrıştırma sırasında ile karşılaşıldı. 'değişim (olmadan, Grup) kimliğine sahip ' 987654 bulunan' ID ' 123456 kümesiyle EDIFACT işlem Merhaba, gönderen Kimliği 'Partner1' ile 'Partner2' alıcının kimliği şu hatalarla askıya alındı: baştaki boşlukları ayırıcısı bulundu |
| Kullanıcı eylemi | Merhaba sözleşmesi ayarları toobe baştaki ve sondaki boşlukları tooallow yapılandırılmış. </br> Baştaki ve sondaki boşlukları sözleşmesi ayarları tooallow Düzenle |
|   |   |

![alan izin ver](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a>* Yinelenen onay hello anlaşmasında etkinleştirilmiş

|   |   | 
|---|---| 
| Hata açıklaması | Yinelenen denetim sayısı |
| Kullanıcı eylemi | Bu hata, yinelenen denetim numaraları alınan selamlama iletisine olduğunu gösterir. </br> Merhaba denetim numarayı düzeltin ve selamlama iletisine yeniden gönderin |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a>* Eksik şema hello Sözleşmesi

|   |   | 
|---|---| 
| Hata açıklaması | Ayrıştırma sırasında ile karşılaşıldı. kimliğine sahip '564220001' kimlikli '56422', '000056422' kimlikli Gönderen Kimliği ' 12345678 değişim içinde', işlevsel grubu alıcı kimliği ' 87654321 yer alan' hello X12 işlem kümesi şu hatalarla "Merhaba ileti bilinmeyen belge ty var askıya alındı PE ve tooany hello varolan şema hello anlaşmasında yapılandırılmış çözümlenmedi " |
| Kullanıcı eylemi | Şema hello sözleşmesi ayarları yapılandırabilirsiniz.  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a>* Yanlış şema hello Sözleşmesi

|   |   | 
|---|---| 
| Hata açıklaması | Merhaba ileti bilinmeyen belge türüne sahip ve tooany hello varolan şema hello anlaşmasında yapılandırılmış çözümlenmedi. |
| Kullanıcı eylemi | Doğru şemayı hello sözleşmesi ayarlarını yapılandırın  |
|   |   |

## <a name="flat-file"></a>Düz dosya

### <a name="-input-message-with-no-body"></a>* Hiçbir gövde ile giriş iletisi

|   |   | 
|---|---|
| Hata açıklaması | InvalidTemplate. '1' satır ve sütun '1902' eylemi 'Flat_File_Decoding' girişleri oluşturulamıyor tooprocess şablon dili ifadelerinde: ' özelliği 'content' bekler bir değer ancak taşınmadığını null gerekli. Yol ''.'. |
| Kullanıcı eylemi | Bu hata hello giriş ileti Gövde içermiyor belirtir. |
|   |   | 

## <a name="learn-more"></a>Daha fazla bilgi edinin
[Merhaba Enterprise Integration Pack hakkında daha fazla bilgi edinin](logic-apps-enterprise-integration-overview.md)

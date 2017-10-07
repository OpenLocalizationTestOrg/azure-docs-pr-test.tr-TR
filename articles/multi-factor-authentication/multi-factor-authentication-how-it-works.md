---
title: "çok faktörlü kimlik doğrulaması - aaaAzure nasıl çalışır?"
description: "Azure multi-Factor Authentication kullanıcı talebine basit bir oturum açma işlemi için buluştururken koruma erişim toodata ve uygulamaları yardımcı olur. İkinci bir form kimlik doğrulama isteyerek ek güvenlik sağlar ve bir dizi kolay doğrulama seçeneklerini aracılığıyla güçlü kimlik doğrulaması sunar."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a>Azure multi-Factor Authentication nasıl çalışır
iki aşamalı doğrulamayı Hello güvenliğini, katmanlı yaklaşımın arasındadır. Birden çok kimlik doğrulama faktörleri tehlikeye saldırganlar için önemli bir sınama gösterir. Bir saldırgan toolearn hello kullanıcının parolasını yönetir olsa bile, onu da hello güvenilir cihaz elinde gerek kalmadan gereksizdir. 

![Proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

Azure multi-Factor Authentication kullanıcı talebine basit bir oturum açma işlemi için buluştururken koruma erişim toodata ve uygulamaları yardımcı olur.  İkinci bir form kimlik doğrulama isteyerek ek güvenlik sağlar ve bir dizi kolay doğrulama seçeneklerini aracılığıyla güçlü kimlik doğrulaması sunar.


## <a name="methods-available-for-two-step-verification"></a>İki aşamalı doğrulama için kullanılabilen yöntemler
Bir kullanıcı oturum açtığında ek doğrulama toohello kullanıcı gönderilir.  Merhaba, bu ikinci doğrulama için kullanılabilir yöntemlerin listesi verilmiştir.

| Doğrulama yöntemi | Açıklama |
| --- | --- |
| Telefon araması |Çağrı tooa kullanıcının kayıtlı telefon yerleştirilir. Merhaba kullanıcı bir PIN gerekli olduğunda girer sonra hello # tuşuna basar. |
| SMS mesajı |Tooa kullanıcının cep telefonu altı rakamlı kodu içeren bir kısa mesaj gönderilir. Merhaba kullanıcı oturum açma hello sayfasında bu kodu girer. |
| Mobil uygulama bildirimi |Doğrulama isteği tooa kullanıcının Akıllı telefonu gönderilir. Merhaba kullanıcı bir PIN gerekli olduğunda girer sonra seçer **doğrula** hello mobil uygulama üzerinde. |
| Mobil uygulama doğrulama kodu |bir kullanıcının Akıllı telefonu üzerinde çalıştığından, hello mobil uygulama değişiklikleri her 30 saniyede bir doğrulama kodu görüntüler. Merhaba kullanıcı hello en son kod bulur ve oturum açma hello sayfasında girer. |
| Üçüncü taraf OATH belirteçleri | Azure multi-Factor Authentication Sunucusu'nda yapılandırılan tooaccept üçüncü taraf doğrulaması yöntemleri olabilir. |

Azure çok faktörlü kimlik doğrulaması, hem bulut hem de sunucu için seçilebilir doğrulama yöntemlerini sağlar. Hangi yöntemler, kullanıcılarınız için kullanılabilir seçebilirsiniz: telefon araması, metin, uygulama bildirimi veya uygulama kodları. Daha fazla bilgi için bkz: [seçilebilir doğrulama yöntemlerini](multi-factor-authentication-whats-next.md#selectable-verification-methods).

## <a name="next-steps"></a>Sonraki adımlar

- Merhaba farklı hakkında okuyun [sürümleri ve Azure çok faktörlü kimlik doğrulaması için tüketim yöntemi](multi-factor-authentication-versions-plans.md)

- Seçin olup olmadığını toodeploy Azure MFA [hello Bulut veya şirket içi](multi-factor-authentication-get-started.md)

- Okuma yanıtlar için [sık sorulan sorular](multi-factor-authentication-faq.md)
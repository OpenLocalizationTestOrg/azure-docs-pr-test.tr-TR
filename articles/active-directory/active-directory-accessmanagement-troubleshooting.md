---
title: "gruplar için dinamik üyelik aaaTroubleshooting | Microsoft Docs"
description: "Azure AD grupları için dinamik üyelik için sorun giderme ipuçları."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Gruplar için dinamik üyelik sorunlarını giderme
**I bir kural bir grup üzerinde yapılandırılmış ancak hiçbir üyelik hello grubunda güncelleştirilmesi**<br/>Bu hello doğrulayın **etkinleştir Temsilcili Grup Yönetimi** ayar çok**Evet** hello içinde **yapılandırma** sekmesi. Bir kullanıcı toowhom bir Azure Active Directory Premium lisansı atanmış olarak yalnızca, oturum açarsanız, bu ayar görürsünüz. Kullanıcı öznitelikleri hello kuralında Hello değerlerini doğrulayın: hello kural karşılayan kullanıcılar vardır?

**Bir kural yapılandırılmış, ancak şimdi hello kuralı var olan üyelerine hello kaldırılır**<br/>Bu beklenen bir davranıştır. Bir kural etkin veya değiştirildiğinde hello grubunun varolan üyeleri kaldırılır. Merhaba kural değerlendirme sürümünden döndürülen hello kullanıcılar üyeleri toohello grup olarak eklenir.     

**Ne zaman eklemek veya bir kural neden değiştirmek instantly üyeliği değiştiğinde görmüyorum?**<br/>Ayrılmış üyeliği değerlendirmesi düzenli aralıklarla bir zaman uyumsuz arka planda gerçekleştirilir. Ne kadar süreyle hello işlem alır belirlenir başlangıç dizini ve hello boyutunuz hello kural sonucu olarak oluşturulan hello grubunun kullanıcıların sayısı. Genellikle, kullanıcıların küçük sayıda dizinlerle hello grup üyeliği değişikliklerinin değerinden birkaç dakika içinde görürsünüz. Çok sayıda kullanıcı dizinlerle 30 dakika veya daha uzun toopopulate alabilir.

### <a name="next-steps"></a>Sonraki adımlar
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Azure Active Directory grupları ile erişim tooresources yönetme](active-directory-manage-groups.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Azure Active Directory nedir?](active-directory-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)

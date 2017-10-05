---
title: "Gruplar için dinamik üyelik sorunlarını giderme | Microsoft Docs"
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
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Gruplar için dinamik üyelik sorunlarını giderme
**I bir kural bir grup üzerinde yapılandırılmış ancak hiçbir üyelik grubunda güncelleştirilmesi**<br/>Doğrulayın **etkinleştir Temsilcili Grup Yönetimi** ayar **Evet** içinde **yapılandırma** sekmesi. Yalnızca, bir Azure Active Directory Premium lisansı atandığı kullanıcı olarak oturum açarsanız, bu ayar görürsünüz. Kullanıcı öznitelikleri kuralda değerlerini doğrulayın: kural karşılayan kullanıcılar vardır?

**Bir kural yapılandırılmış, ancak şimdi kuralının var olan üyeleri kaldırılır**<br/>Bu beklenen bir davranıştır. Bir kural etkin veya değiştirildiğinde varolan grubun üyeleri kaldırılır. Kural değerlendirme sürümünden döndürülen kullanıcılar grubuna üye olarak eklenir.     

**Ne zaman eklemek veya bir kural neden değiştirmek instantly üyeliği değiştiğinde görmüyorum?**<br/>Ayrılmış üyeliği değerlendirmesi düzenli aralıklarla bir zaman uyumsuz arka planda gerçekleştirilir. İşlem için gereken süreyi dizininizdeki kullanıcı sayısı ve kural sonucu olarak oluşturulan grubu boyutu tarafından belirlenir. Genellikle, kullanıcıların küçük sayıda dizinlerle grup üyeliği değişikliklerinin değerinden birkaç dakika içinde görürsünüz. Çok sayıda kullanıcı dizinlerle 30 dakika alabilir veya doldurmak için daha uzun.

### <a name="next-steps"></a>Sonraki adımlar
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Azure Active Directory grupları ile kaynaklara erişimi yönetme](active-directory-manage-groups.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Azure Active Directory nedir?](active-directory-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)

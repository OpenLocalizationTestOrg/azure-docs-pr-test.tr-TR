---
title: "Azure Active Directory'deki bir gruba aaaResolve lisans sorunları | Microsoft Docs"
description: "Azure Active Directory grup tabanlı lisans kullanırken tooidentify ve çözümleme atama sorunları nasıl lisans"
services: active-directory
keywords: Azure AD lisanslama
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ec9c74214a9e246f21fcf767b0bbd586ae702445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Belirleyin ve Azure Active Directory'deki bir gruba için lisans atama sorunları çözün

Grup tabanlı Azure Active Directory (Azure AD) lisans kullanıcıların Lisans hata durumuna hello kavramını sunmaktadır. Bu makalede, kullanıcıların bu durumda neden bitirebilirsiniz hello nedenleri açıklanmaktadır.

Grup tabanlı lisans kullanmadan doğrudan tooindividual kullanıcılar, lisans atadığınızda, hello atama işlemi başarısız olabilir. Örneğin, hello PowerShell cmdlet'ini çalıştırdığınızda `Set-MsolUserLicense` bir kullanıcı, pek çok ilgili toobusiness mantığı olan hello cmdlet'i başarısız olabilir. Örneğin, olabilir lisansları veya aynı hello atanamaz iki hizmet planları arasında bir çakışma sayısı yetersiz zaman. Merhaba sorunu hemen bildirilen tooyou yedekleyin.

Grup tabanlı kullanırken hello Azure AD hizmeti lisans atama lisans, hello aynı hatalar oluşabilir, ancak bunlar hello arka planda meydana gelir. Bu nedenle, hello hataları iletildiğinden tooyou hemen olamaz. Bunun yerine, bunlar hello kullanıcı nesnesinde kaydedilen ve hello Yönetim Portalı üzerinden bildirdi. Merhaba özgün hedefi toolicense hello kullanıcı asla kaybolur, ancak gelecekte araştırmak ve çözümleme için bir hata durumuna kaydedilen unutmayın.

## <a name="how-toofind-license-assignment-errors"></a>Nasıl toofind lisans atama hataları

1. bir hata durumunda belirli bir grup, açık hello dikey penceresinde hello grubu için toofind kullanıcılar. Altında **lisansları**, bir hata durumunda tüm kullanıcıların olduğunda görüntülenen bir bildirim olacaktır.

![Grup, hata bildirimi](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Merhaba bildirim tooopen tüm etkilenen kullanıcıların bir listesini tıklatın. Her bir kullanıcı tek tek tıklatın toosee daha ayrıntıları.

![Hata durumunda kullanıcı grubu listesi](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. toofind hello üzerinde en az bir hata içeren tüm grupları **Azure Active Directory** dikey seçin **lisansları** ve ardından **genel bakış**. Bazı gruplar dikkat etmeniz gereken durumlarda bir bilgi kutusu görüntülenir.

![Genel bakış, hata durumunda grupları hakkında bilgi](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Merhaba kutusunu toosee üzerinde hataları olan tüm grupların listesini tıklatın. Daha fazla ayrıntı için her grubu tıklatabilirsiniz.

![Genel bakış, hatalarla gruplarının listesi](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


Aşağıda her olası sorun ve hello yolu tooresolve açıklamasıdır onu.

## <a name="not-enough-licenses"></a>Yeterli lisans yok

**Sorun:** hello grubunda belirtilen hello ürünlerden birinin için yeterli kullanılabilir lisans yok. Tooeither ihtiyacınız hello ürünü için daha fazla lisans satın alma ya da diğer kullanıcılara veya gruplara kullanılmayan lisanslarını boşaltın.

toosee kaç tane kullanılabilir, çok Git**Azure Active Directory** > **lisansları** > **tüm ürünleri**.

hangi kullanıcıların ve grupların lisansları, kullanıyor toosee bir ürün'ı tıklatın. Altında **lisanslı kullanıcıların**, doğrudan veya bir veya daha fazla grupları üzerinden atanan lisansları aranızdaki tüm kullanıcılar görürsünüz. Altında **lisans grupları**, bu ürünü atanmış olan tüm grupları görürsünüz.

**PowerShell:** PowerShell cmdlet'leri bu hata olarak rapor _CountViolation_.

## <a name="conflicting-service-plans"></a>Çakışan hizmet planları

**Sorun:** çakışan bir hizmet planı farklı bir ürün aracılığıyla atanan toohello kullanıcı zaten başka bir hizmet planı ile Merhaba grubunda belirtilen hello ürünleri içerir. Bazı hizmet planları bunlar toohello atanamaz bir şekilde yapılandırılmış olan aynı kullanıcı başka bir ilgili hizmet planı olarak.

Aşağıdaki örnek hello göz önünde bulundurun. Bir kullanıcı için Office 365 Enterprise lisansının **E1** doğrudan, etkinleştirilmiş tüm hello planlarıyla atanmış. Merhaba kullanıcı hello Office 365 Kurumsal olan tooa grubuna eklendi **E3** atanan ürün tooit. Bu ürün çakışamaz hizmet planları hello Grup lisans atamasını hello "Çakışan hizmet planları" hatası ile başarısız olacak şekilde E1 dahil hello planına sahip içerir. Bu örnekte, hello çakışan hizmet planları şunlardır:

-   SharePoint Online (planlama 1) ile SharePoint Online (2 planlama) çakışıyor.
-   Exchange Online (planlama 1) ile Exchange Online (2 planlama) çakışıyor.

toosolve bu çakışma hello E1 üzerinde ya da lisans o doğrudan atanan toohello kullanıcı bu iki planları toodisable gerekir. Veya, toomodify hello grubun tamamı lisans ataması gerekir ve hello E3 lisans hello planları devre dışı bırakın. Alternatif olarak, hello hello E3 lisans bağlamında yedekli ise tooremove hello E1 lisans hello kullanıcıdan karar verebilirsiniz.

nasıl tooresolve çakışan ürün her zaman lisansları hakkında hello karar toohello yönetici aittir. Azure AD otomatik olarak lisans çakışmaları değil.

**PowerShell:** PowerShell cmdlet'leri bu hata olarak rapor _MutuallyExclusiveViolation_.

## <a name="other-products-depend-on-this-license"></a>Bu lisansa bağımlı olan başka ürünler var

**Sorun:** işlevi için başka bir ürün içinde başka bir hizmet planı için etkinleştirilmesi gereken bir hizmet planına hello grubunda belirtilen hello ürünleri içerir. Azure AD tooremove hello temel alınan hizmet planı çalıştığında bu hata oluşur. Örneğin, bu hello gruptan kaldırılan hello kullanıcı sonucu olarak ortaya çıkabilir.

toosolve bu sorunu toomake bu hello gerekli planı toousers başka bir yöntem aracılığıyla veya hello bağımlı hizmetleri bu kullanıcılar için devre dışı bırakılır hala atanan emin olmanız gerekir. Yaptıktan sonra bu kullanıcılardan hello Grup lisans düzgün kaldırabilirsiniz.

**PowerShell:** PowerShell cmdlet'leri bu hata olarak rapor _DependencyViolation_.

## <a name="usage-location-isnt-allowed"></a>Kullanım konumu izin verilmiyor

**Sorun:** bazı Microsoft Hizmetleri tüm konumlarda yerel yasalarına ve düzenlemelerine nedeniyle kullanılamaz. Bir lisans tooa kullanıcı atamadan önce hello kullanıcı için toospecify hello "Kullanım konumu" özelliğine sahip. Merhaba altında bunu yapabilirsiniz **kullanıcı** > **profil** > **ayarları** hello Azure portalı bölümünde.

Azure AD, kullanım konumu desteklenmiyor Grup lisans tooa kullanıcı tooassign çalıştığında başarısız ve bu hata hello kullanıcı kaydedin.

toosolve Bu sorun, lisanslı hello grubundan ekranla konumlardan Kaldır kullanıcılar. Hello geçerli kullanım konumu değerlerinin hello gerçek kullanıcı konumu temsil eden yok, (Merhaba yeni konum destekleniyorsa) hello lisansları doğru sonraki kalmayacak şekilde alternatif olarak, bunları değiştirebilirsiniz.

**PowerShell:** PowerShell cmdlet'leri bu hata olarak rapor _ProhibitedInUsageLocationViolation_.

> [!NOTE]
> Azure AD Grup lisansları atarken, belirtilen bir kullanım konumu olmayan tüm kullanıcılar hello dizininin hello konumu devralır. Yöneticiler hello doğru kullanım konumu değerlerinin kullanıcıları yerel yasa ve yönetmeliklere grup tabanlı lisans toocomply kullanmadan önce ayarlamanızı öneririz.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>Bir gruba birden fazla ürün lisans olmadığında ne olur?

Birden fazla ürün lisans tooa grubu atayabilirsiniz. Örneğin, Office 365 Kurumsal E3 atayabilir ve Enterprise Mobility + güvenlik tooa Grup tooeasily tüm dahil Hizmetleri kullanıcıları etkinleştirin.

Azure AD tooassign hello Grup tooeach kullanıcı belirtilen tüm lisanslar çalışır. Varsa Azure AD olamaz Ata hello ürünlerden birinin iş mantığı sorunları nedeniyle (örneğin, tüm için yeterli lisans yoksa veya hello kullanıcı etkin diğer hizmetlerle çakışma varsa), onu hello hello grubundaki diğer lisansları Ata olmaz Her iki.

Mümkün toosee hello atanan tooget başarısız kullanıcılar başarısız oldu ve bu tarafından hangi ürünlerin etkilendiğini onay olması.

## <a name="license-assignment-fails-silently-for-a-user-due-tooduplicate-proxy-addresses-in-exchange-online"></a>Exchange Online'da tooduplicate proxy adreslerini son kullanıcı lisans atamasını sessizce başarısız olur

Exchange Online kullanıyorsanız, bazı kullanıcılar kiracınızda hatalı hello ile yapılandırılmış olabilir aynı proxy adresi değeri. Grup tabanlı lisans tooassign lisans toosuch kullanıcı çalıştığında başarısız olur ve bir hata kaydedilmeyecek (farklı olarak, yukarıda açıklanan diğer hata durumlarında hello) - bu hello Önizleme sürümünde bu özellik, bir sınırlama ve biz tooaddress geçmeden önce  *Genel kullanılabilirlik*.

> [!TIP]
> Bazı kullanıcılar, bir lisans almamış olabilir ve bu kullanıcılar kaydedilmiş bir hata görürseniz, ilk yinelenen proxy adresi olup olmadığını denetleyin.
> Bu, Exchange Online karşı PowerShell cmdlet'i aşağıdaki hello yürüterek yapılabilir:
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [Bu makalede](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) bilgileri dahil olmak üzere bu sorun hakkında daha fazla ayrıntı içeren [nasıl çevrimiçi uzak PowerShell kullanarak tooconnect tooExchange](https://technet.microsoft.com/library/jj984289.aspx).

Proxy adresi sorunları hello etkilenen kullanıcıların için çözümlendi sonra hello Grup toomake üzerinde lisansları şimdi yeniden uygulanabilir emin işleme emin tooforce lisans yapın.

## <a name="how-do-you-force-license-processing-in-a-group-tooresolve-errors"></a>Nasıl bir grup tooresolve hataları işleme lisans zorla?

Hangi adımları üzerinde bağlı olarak tooresolve hataları yapılan, bir grup tooupdate hello kullanıcı durumunu gerekli toomanually tetikleyici işleme olabilir.

Örneğin, kullanıcıların doğrudan lisans anlaşmalarını kaldırarak bazı lisansları serbest, daha önce tüm kullanıcı üyeler toofully lisans başarısız grupları tootrigger işlenmesi gerekir. Merhaba grubu dikey penceresine, bulmak, toodo açmak **lisansları**ve select hello **yeniden işleyin** hello araç çubuğu düğmesi.

## <a name="next-steps"></a>Sonraki adımlar

Diğer senaryolar için grupları aracılığıyla lisans yönetimi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Active Directory'de lisansları tooa grup atama](active-directory-licensing-group-assignment-azure-portal.md)
* [Grup tabanlı Azure Active Directory lisanslaması nedir?](active-directory-licensing-whatis-azure-portal.md)
* [Toomigrate tek tek kullanıcılar toogroup tabanlı Azure Active Directory'de lisanslama nasıl lisanslı](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory grup tabanlı ilave senaryolar lisanslama](active-directory-licensing-group-advanced.md)

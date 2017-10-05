---
title: "Azure Active Directory'deki bir gruba lisans sorunlarını gidermek | Microsoft Docs"
description: "Tanımlamak ve Azure Active Directory grup tabanlı lisans kullanırken lisans atama sorunları gidermek nasıl"
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
ms.openlocfilehash: bfa951a897c9b383072c0d29c9a4266c163fe753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Belirleyin ve Azure Active Directory'deki bir gruba için lisans atama sorunları çözün

Grup tabanlı Azure Active Directory (Azure AD) lisans kullanıcıların Lisans hata durumuna kavramını sunmaktadır. Bu makalede, kullanıcıların bu durumda neden bitirebilirsiniz nedenleri açıklanmaktadır.

Grup tabanlı lisans kullanmadan doğrudan bireysel kullanıcılara lisans atadığınızda, atama işlemi başarısız olabilir. Örneğin, PowerShell cmdlet'ini çalıştırdığınızda `Set-MsolUserLicense` bir kullanıcı, iş mantığı için ilgili nedenlerden biri için cmdlet başarısız olabilir. Örneğin, lisans ya da aynı anda atanamaz iki hizmet planları arasında bir çakışma sayısı yetersiz olabilir. Sorun hemen geri size bildirilir.

Grup tabanlı kullanırken lisanslama, aynı hatalar oluşabilir, ancak Azure AD hizmeti lisansları atarken bunlar arka planda gerçekleşir. Bu nedenle, hataları için hemen bildirilmesi olamaz. Bunun yerine, bunlar kullanıcı nesnesindeki kaydedilen ve Yönetim Portalı üzerinden bildirdi. Kullanıcı lisansı için özgün amacı hiçbir zaman kaybolur, ancak gelecekte araştırmak ve çözümleme için bir hata durumuna kaydedilen unutmayın.

## <a name="how-to-find-license-assignment-errors"></a>Lisans atama hataları bulma

1. Belirli bir grubunun hata durumunda kullanıcıları bulmak için grubu için dikey penceresini açın. Altında **lisansları**, bir hata durumunda tüm kullanıcıların olduğunda görüntülenen bir bildirim olacaktır.

![Grup, hata bildirimi](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Tüm etkilenen kullanıcıların bir listesini açmak için bildirime tıklayın. Daha fazla ayrıntı için ayrı ayrı her bir kullanıcı tıklatabilirsiniz.

![Hata durumunda kullanıcı grubu listesi](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. Üzerinde en az bir hata içeren tüm grupları bulmak için **Azure Active Directory** dikey seçin **lisansları** ve ardından **genel bakış**. Bazı gruplar dikkat etmeniz gereken durumlarda bir bilgi kutusu görüntülenir.

![Genel bakış, hata durumunda grupları hakkında bilgi](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Hataları olan tüm gruplarının bir listesini görmek için kutuyu tıklatın. Daha fazla ayrıntı için her grubu tıklatabilirsiniz.

![Genel bakış, hatalarla gruplarının listesi](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


Aşağıda her olası bir sorunu çözmek için yolu ve bir açıklama bulunmaktadır.

## <a name="not-enough-licenses"></a>Yeterli lisans yok

**Sorun:** grubunda belirtilen ürünlerin biri için kullanılabilir yeterli lisans yok. Ürünü için daha fazla lisans satın ya da diğer kullanıcılara veya gruplara kullanılmayan lisanslarını boşaltmak gerekir.

Kaç tane kullanılabilir olduğunu görmek için şu adrese gidin **Azure Active Directory** > **lisansları** > **tüm ürünleri**.

Hangi kullanıcıların ve grupların lisansları kullanıyor görmek için bir ürün Ek Yardım düğmesini tıklatın. Altında **lisanslı kullanıcıların**, doğrudan veya bir veya daha fazla grupları üzerinden atanan lisansları aranızdaki tüm kullanıcılar görürsünüz. Altında **lisans grupları**, bu ürünü atanmış olan tüm grupları görürsünüz.

**PowerShell:** PowerShell cmdlet'leri bu hata olarak rapor _CountViolation_.

## <a name="conflicting-service-plans"></a>Çakışan hizmet planları

**Sorun:** zaten farklı bir ürün aracılığıyla kullanıcıya atanmış başka bir hizmet planı olan çakışan bir hizmet planı grubunda belirtilen ürünleri içerir. Bazı hizmet planları, aynı kullanıcıya başka bir ilgili hizmet planı olarak atanamaz şekilde yapılandırılır.

Aşağıdaki örnek göz önünde bulundurun. Bir kullanıcı için Office 365 Enterprise lisansının **E1** doğrudan sahip tüm planlar etkin atanmış. Kullanıcı Office 365 Kurumsal olan bir gruba eklenen **E3** ürün atanmış. Bu ürün çakışamaz hizmet planları Grup lisans atamasını "Çakışan hizmet planları" hatasıyla başarısız olacak şekilde E1 dahil planına sahip içerir. Bu örnekte, çakışan hizmet planları şunlardır:

-   SharePoint Online (planlama 1) ile SharePoint Online (2 planlama) çakışıyor.
-   Exchange Online (planlama 1) ile Exchange Online (2 planlama) çakışıyor.

Bu çakışmayı çözmek için bu devre dışı bırakmanız gerekir ya da doğrudan kullanıcıya atanan E1 lisans üzerindeki iki planları. Veya, tüm Grup lisans atamasını değiştirmek ve E3 lisans planları devre dışı bırakmak gerekir. Alternatif olarak, E1 lisans E3 lisans bağlamında yedek varsa kullanıcıyı kaldırmak isteyebilirsiniz.

Çakışan ürün lisansları her zaman çözümü hakkındaki kararınızı yöneticiye aittir. Azure AD otomatik olarak lisans çakışmaları değil.

**PowerShell:** PowerShell cmdlet'leri bu hata olarak rapor _MutuallyExclusiveViolation_.

## <a name="other-products-depend-on-this-license"></a>Bu lisansa bağımlı olan başka ürünler var

**Sorun:** işlevi için başka bir ürün içinde başka bir hizmet planı için etkinleştirilmesi gereken bir hizmet planına grubunda belirtilen ürünleri içerir. Azure AD temel alınan hizmet planını kaldırmanız çalıştığında bu hata oluşur. Örneğin, bu gruptan kaldırılan kullanıcı sonucu olarak ortaya çıkabilir.

Bu sorunu çözmek için başka bir yöntem kullanıcılara, gerekli planı hala atanır veya bağımlı hizmetler bu kullanıcılar için devre dışı bırakılır emin olmak gerekir. Yaptıktan sonra bu kullanıcılardan Grup lisans düzgün kaldırabilirsiniz.

**PowerShell:** PowerShell cmdlet'leri bu hata olarak rapor _DependencyViolation_.

## <a name="usage-location-isnt-allowed"></a>Kullanım konumu izin verilmiyor

**Sorun:** bazı Microsoft Hizmetleri tüm konumlarda yerel yasalarına ve düzenlemelerine nedeniyle kullanılamaz. Bir kullanıcıya bir lisans atamak için önce kullanıcı için "Kullanım konumu" özelliği belirtmeniz gerekir. Altında bunu yapabilirsiniz **kullanıcı** > **profil** > **ayarları** Azure portalı bölümünde.

Azure AD, kullanım konumu desteklenmiyor kullanıcıya bir Grup lisans atama girişiminde bulunduğunda, başarısız ve kullanıcının bu hatayı kaydedin.

Bu sorunu çözmek için kullanıcılar ekranla konumları lisanslı grubundan kaldırın. Geçerli kullanım konumu değerlerinin gerçek kullanıcı konumu temsil eden yok, lisansları (yeni konumu destekleniyorsa) doğru sonraki kalmayacak şekilde alternatif olarak, bunları değiştirebilirsiniz.

**PowerShell:** PowerShell cmdlet'leri bu hata olarak rapor _ProhibitedInUsageLocationViolation_.

> [!NOTE]
> Azure AD Grup lisansları atarken, belirtilen bir kullanım konumu olmayan tüm kullanıcılar dizininin konumunu devralır. Yöneticiler doğru kullanım konumu değerlerinin kullanıcıları grup tabanlı lisans yerel yasa ve yönetmeliklere uymak için kullanmadan önce ayarlamanızı öneririz.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>Bir gruba birden fazla ürün lisans olmadığında ne olur?

Bir gruba birden fazla ürün lisans atayabilirsiniz. Örneğin, tüm dahil Hizmetleri kullanıcıları kolayca etkinleştirmek için bir grubu için Office 365 Kurumsal E3 ve Enterprise Mobility + Security atayabilirsiniz.

Azure AD grubundaki her kullanıcı için belirtilen tüm lisansları atama dener. Varsa Azure AD atayamazsınız ürünlerden birinin iş mantığı sorunları nedeniyle (örneğin, tüm için yeterli lisans yoksa veya kullanıcıya etkin diğer hizmetlerle çakışma varsa), diğer lisans grubunda ya da Ata olmaz.

Bu tarafından hangi ürünlerin etkilendiğini denetlemek ve atanan için başarısız olan kullanıcılara başarısız olduğunu görmek mümkün olur.

## <a name="license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online"></a>Lisans atamasını sessizce yinelenen proxy adreslerini nedeniyle bir kullanıcı için Exchange Online başarısız

Exchange Online kullanıyorsanız, kiracınızdaki bazı kullanıcılar yanlışlıkla ayrı proxy adres değeriyle yapılandırılmış olabilir. Grup tabanlı lisans böyle bir kullanıcıya bir lisans atamak çalıştığında başarısız olur ve bir hata kaydedilmeyecek (aksine yukarıda açıklanan diğer hata durumlarda) - Bu bir kısıtlamadır bu özellik Önizleme sürümünde ve biz önceelealınacaktır*</c0>Genelkullanılabilirlik<spanclass="notranslate">*.</span>

> [!TIP]
> Bazı kullanıcılar, bir lisans almamış olabilir ve bu kullanıcılar kaydedilmiş bir hata görürseniz, ilk yinelenen proxy adresi olup olmadığını denetleyin.
> Bu, Exchange Online karşı aşağıdaki PowerShell cmdlet'ini çalıştırarak yapılabilir:
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [Bu makalede](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) bilgileri dahil olmak üzere bu sorun hakkında daha fazla ayrıntı içeren [Exchange Online'a uzak PowerShell kullanarak için bağlanma](https://technet.microsoft.com/library/jj984289.aspx).

Etkilenen kullanıcılar için proxy adresi sorunları üzere çözdükten sonra lisans işleme lisansları şimdi yeniden uygulanabilir emin olmak için grubu hakkında zorlar emin olun.

## <a name="how-do-you-force-license-processing-in-a-group-to-resolve-errors"></a>Lisans işleme hataları gidermek için bir grup içinde nasıl zorla?

Hataları gidermek için ayırdıktan hangi adımları bağlı olarak, el ile kullanıcı durumunu güncelleştirmek için bir grup işlenmesini tetiklemek gerekli olabilir.

Örneğin, kullanıcıların doğrudan lisans anlaşmalarını kaldırarak bazı lisansları serbest, tam olarak tüm kullanıcı üyeler lisans için daha önce başarısız grupları işlenmesini tetiklemek gerekir. Bunu yapmak için açık grup dikey Bul **lisansları**seçip **yeniden işleyin** araç çubuğu düğmesi.

## <a name="next-steps"></a>Sonraki adımlar

Lisans Yönetimi grupları üzerinden diğer senaryolar hakkında daha fazla bilgi için aşağıdakilere bakın:

* [Azure Active Directory'deki bir gruba lisans atama](active-directory-licensing-group-assignment-azure-portal.md)
* [Grup tabanlı Azure Active Directory lisanslaması nedir?](active-directory-licensing-whatis-azure-portal.md)
* [Azure Active Directory'de Grup tabanlı lisans için tek tek lisanslı kullanıcıları geçirme](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory grup tabanlı ilave senaryolar lisanslama](active-directory-licensing-group-advanced.md)

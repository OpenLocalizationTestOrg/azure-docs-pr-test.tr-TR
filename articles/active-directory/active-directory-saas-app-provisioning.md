---
title: "aaaAutomated SaaS uygulama kullanıcı Azure AD'de sağlama | Microsoft Docs"
description: "Azure AD tooautomatically sağlamanıza, kullanabileceğiniz bir giriş toohow sağlanmasını ve sürekli olarak kullanıcı hesaplarını birden çok üçüncü taraf SaaS uygulamalarında güncelleştirin."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: a1f3ecdd513e2b603f8ad9901e9f551b3b982b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-toosaas-applications-with-azure-active-directory"></a>Sağlama ve Azure Active Directory ile tooSaaS uygulamaları etkinleştirmektir kullanıcı otomatikleştirme
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>SaaS uygulamaları için kullanıcı sağlamayı otomatik nedir?
Azure Active Directory (Azure AD) verir tooautomate hello oluşturma, Bakım ve kullanıcı kimliklerinin bulutta kaldırma ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) Dropbox, Salesforce, ServiceNow ve daha fazlası gibi uygulamalar.

**Aşağıda ne bu özellik, toodo sağlar ilişkin bazı örnekler şunlardır:**

* Ekibinizin katıldığınızda otomatik olarak yeni hesaplar hello doğru SaaS uygulamaları için yeni kişiler oluşturun.
* Otomatik olarak kişiler kaçınılmaz olarak hello takım ayrıldığında SaaS uygulamaları hesaplarından devre dışı bırakın.
* SaaS uygulamalarınıza Hello kimliklerini hello dizininde değişikliklere göre toodate yukarı kalmasını sağlamak.
* Grupları, bunları destekleyen tooSaaS uygulamaları gibi kullanıcı olmayan nesneler sağlayın.

**Otomatik kullanıcı sağlamayı işlevselliği aşağıdaki hello içerir:**

* Merhaba özelliği toomatch varolan kimlikler Azure AD arasında ve SaaS uygulamaları.
* Özelleştirme seçenekleri toohelp Azure AD hello geçerli yapılandırmaları kuruluşunuzun şu anda kullanmakta olduğu hello SaaS uygulamalarının uygun.
* Hazırlama hataları için isteğe bağlı bir e-posta uyarıları.
* İzleme ve sorun giderme ile raporlama ve etkinlik günlükleri toohelp.

## <a name="why-use-automated-provisioning"></a>Otomatik sağlama neden kullanılır?
Bu özelliği kullanmak için bazı ortak sözleri şunları içerir:

* tooavoid hello maliyetleri, verimsiz ve işlemler sağlama el ile ilişkili İnsan hatası.
* toosecure kuruluşunuz kullanıcıların kimliklerden anında kaldırarak anahtar SaaS uygulamaları hello kuruluştan ayrılan.
* tooeasily toplu sayısı, kullanıcı belirli bir SaaS uygulamasına içeri aktarın.
* Merhaba dışına çalıştırmak sağlama çözümünüzü sahip olmanın tooenjoy hello kolaylık Azure AD çoklu oturum açma için tanımlanan aynı uygulama erişim ilkeleri.

## <a name="frequently-asked-questions"></a>Sık Sorulan Sorular
**Azure AD directory değişiklikleri toohello SaaS uygulama ne sıklıkta yazma?**

Azure AD değişikliklerini beş tooten dakikada denetler. Merhaba SaaS uygulama çeşitli hatalar (örn. geçersiz yönetici kimlik bilgileri hello durumunun) döndürmesi durumunda, Azure AD kademeli olarak kendi sıklığı tooup tooonce hello hataları çözülene kadar günlük yavaşlatır.

**Ne kadar süreyle tooprovision Kullanıcılarım sürer?**

Artımlı değişiklikler meydana neredeyse anında tooprovision çalışıyorsanız ancak dizininizin, çoğu sonra kullanıcıların ve sahip olduğunuz grupların hello sayısına bağlıdır. Küçük dizinler yalnızca birkaç dakika sürebilir, orta ölçekli dizinleri birkaç dakika sürebilir ve çok büyük dizinler birkaç saat sürebilir.

**Merhaba işinin ilerleme durumunu hello geçerli sağlama nasıl izleyebilir miyim?**

Dizininizin hello Raporlar bölümünde hello hesap sağlama raporu gözden geçirebilirsiniz. Başka bir seçenek toovisit hello Pano sekmesi hello için sağlama SaaS uygulaması için ve altında hello hello sayfanın hello "Tümleştirme durumu" kısmına bakın.

**Kullanıcıların düzgün sağlanan tooget başarısız olursa nasıl anlarım?**

Merhaba hello sonunda sağlama Yapılandırma Sihirbazı hataları sağlama için bir seçenek toosubscribe tooemail bildirimler olur. Hangi kullanıcıların başarısız sağlanan toobe hello sağlama hataları rapor toosee kontrol edebilirsiniz ve neden.

**Azure AD değişiklikleri hello SaaS uygulama arka toohello dizininden yazabilirim?**

Birçok SaaS uygulamaları için sağlama kullanıcılar hello dizin toohello uygulamadan yazılır ve hello uygulamasından değişiklikleri geri toohello dizini yazılamıyorsa yani giden salt okunurdur. İçin [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), Bununla birlikte, sağlama gelen yalnızca hangi kullanıcıların Workday hello dizine alınan olduğu anlamına gelir ve benzer şekilde, hello dizinde değişiklik geri iş günü içinde yazılmaz.

**Geri bildirim toohello mühendislik ekibi nasıl gönderebilir miyim?**

Lütfen bize ulaşın hello [Azure Active Directory geri bildirim Forumunda](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="how-does-automated-provisioning-work"></a>Nasıl yapılır otomatik sağlama iş?
Azure AD, her uygulama satıcısı tarafından sağlanan tooprovisioning uç noktaları bağlanarak kullanıcılar tooSaaS uygulamaları sağlamasını yapar. Bu uç noktalar Azure izin AD tooprogrammatically oluşturmak, güncelleştirmek ve Kullanıcıları Kaldır. Kısa bir genel bakış hello Azure AD tooautomate sağlama aldığını farklı adımlar aşağıdadır.

1. Bir uygulama için hello için ilk kez sağlama etkinleştirdiğinizde, aşağıdaki eylemler hello gerçekleştirilir:
   * Azure AD toomatch karşılık gelen kimliklerini hello dizininde hello SaaS uygulama mevcut tüm kullanıcıların deneyecek. Bir kullanıcı eşleştiğinde oldukları *değil* çoklu oturum açma için otomatik olarak etkinleştirilmiş. Bir kullanıcı toohave erişim toohello uygulaması sırayla açıkça toohello uygulama Azure AD içinde doğrudan veya grup üyeliği üzerinden atanmaları gerekir.
   * Hangi kullanıcıların toohello uygulama atanmalıdır zaten belirttiyseniz, ve toofind var olan hesapları olan kullanıcılar için Azure AD başarısız olursa, Azure AD yeni hesapları için bunları hello uygulamada hazırlayacağınız.
2. Yukarıda açıklandığı gibi Hello ilk eşitleme tamamlandıktan sonra Azure AD her 10 dakikada hello aşağıdaki değişiklikler için kontrol eder:
   * Yeni kullanıcılar atanan toohello uygulama (doğrudan veya grup üyeliği aracılığıyla), ardından olmaları durumunda hello SaaS uygulama yeni bir hesap sağlandı.
   * Bir kullanıcının erişimi kaldırıldıktan sonra hello SaaS uygulama hesabında devre dışı olarak işaretlenir (kullanıcıların hiçbir zaman tamamen silinir, hangi hello olay bir yanlış veri kaybına karşı korur).
   * Bir kullanıcıya son toohello uygulama atandığı ve zaten sahip oldukları hesabı etkin olarak işaretlenecek ve güncel karşılaştırılan toohello dizin olmaları durumunda belirli kullanıcı özelliklerini güncelleştirilebilir bir hesapta hello SaaS uygulaması, değilse.
   * Bir kullanıcının bilgilerini (örneğin, telefon numarası, ofis konumu, vb.) hello dizininde değiştirildiğinde, bu bilgileri de hello SaaS uygulamasına güncelleştirilir.

Öznitelikler Azure AD arasında nasıl eşlendiğini hakkında daha fazla bilgi ve üzerinde hello makalesine bakın SaaS uygulamanız [öznitelik eşlemelerini özelleştirme](active-directory-saas-customizing-attribute-mappings.md).

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>Otomatik kullanıcı sağlamayı destekleyen uygulamalar listesi
Merhaba "Öne çıkan" uygulamaları hello Azure AD uygulama galerisinde tümünün otomatik kullanıcı sağlamayı destekler. [Merhaba öne çıkan uygulamalar listesini burada görüntülenebilir.](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

Bir uygulama toosupport otomatik kullanıcı hazırlama için sırayla, ilk hello dış programları tooautomate hello oluşturma, Bakım ve kullanıcıların kaldırılması için izin gerekli uç noktaları sağlamanız gerekir. Bu nedenle, tüm SaaS uygulamaları bu özellik ile uyumlu değildir. Bunu destekleyen uygulamalar için hello Azure AD mühendislik ekibi olur ardından mümkün toobuild sağlama bağlayıcı toothose uygulamalar olması ve bu iş geçerli ve olası müşteriler hello gereksinimlerinize göre öncelik.

toocontact hello Azure AD mühendislik ek uygulamalar için destek sağlama toorequest ekip, lütfen hello üzerinden bir ileti gönderme [Azure Active Directory geri bildirim Forumunda](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Kullanıcı sağlama öznitelik eşlemelerini özelleştirme](active-directory-saas-customizing-attribute-mappings.md)
* [Özellik eşlemeleri için ifade yazma](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Kapsam belirleme filtreleri kullanıcı sağlama](active-directory-saas-scoping-filters.md)
* [SCIM'yi tooenable otomatik kullanıcıların ve grupların Azure Active Directory tooapplications sağlama kullanma](active-directory-scim-provisioning.md)
* [Hesap sağlama bildirimleri](active-directory-saas-account-provisioning-notifications.md)
* [İlgili nasıl öğreticiler listesi tooIntegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md)


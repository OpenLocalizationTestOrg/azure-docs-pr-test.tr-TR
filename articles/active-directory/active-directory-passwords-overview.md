---
title: "aaaAzure AD Self Servis parola sıfırlama genel bakış | Microsoft Docs"
description: "Self Servis parola sıfırlama Azure AD içinde kuruluşunuz için ne yapabilir?"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 0efc291b1eeec0b7ae33ff5a7d9ed38e70c8be6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-self-service-password-reset-for-hello-it-professional"></a>BT Uzmanı hello için Azure AD Self Servis parola sıfırlama

"Self-Servis" geçici değişen anlamları ile Merhaba dünya genelinde içinde birçok BT departmanları durum buzzword olur. Merhaba Pazar toomanage şirket içi grupları, parolalar veya hello Bulut veya şirket içi kullanıcı profilleri izin ürünlerle taşan ' dir.

Azure Active Directory (Azure AD) Self Servis parola sıfırlama (SSPR) kendisi parçalayın kullanım kolaylığı ve dağıtım ile ayarlar. Azure AD Self Servis parola sıfırlama birleştiren bir özellikler kümesi:

* Kullanıcıların toomanage kendi parolaya izin ver
  * Herhangi bir aygıttan
  * Herhangi bir konuma
  * Herhangi bir zamanda
* Yönetici olarak tanımladığınız ilkeleriyle uyumluluğunu korumak

Hazır olduğunuzda, Azure AD SSPR'yi ile başlayabilirsiniz kullanarak bizim [Hızlı Başlangıç Kılavuzu](active-directory-passwords-getting-started.md) ve hızlı bir şekilde kullanıcılarınızın kendi parolalarını sıfırlama sahip.

## <a name="what-is-possible"></a>Olası nedir

* **Self Servis parola değişikliği** son kullanıcılar veya yöneticilerin toochange parolalarını yönetici Yardım almadan sağlar
* **Self Servis hesabının kilidini** yönetici Yardım almadan kendi hesabı son kullanıcıların toounlock sağlar
* **Self Servis parola sıfırlama** son kullanıcılar veya yöneticilerin tooreset parolalarını Yönetici Yardımı olmadan otomatik olarak sağlar. Self Servis parola sıfırlama için Azure AD Premium veya Basic - [Azure Active Directory sürümleri](active-directory-editions.md).
* **Yönetici tarafından başlatılan parola sıfırlama** bir son kullanıcının ya da başka bir yöneticinin paroladan hello içinde bir yönetici tooreset sağlayan [Azure portalı](https://docs.microsoft.com/azure/azure-portal-overview)
* **Parola yönetimi etkinlik raporları** parola sıfırlama ve kayıt etkinliği verin Yöneticiler Öngörüler kuruluşlarında - gerçekleşen [yönetim raporları](active-directory-passwords-reporting.md)
* **Parola geri yazma** tarafından ya da hello adına senaryoları gerçekleştirilebilecek tüm hello önceki federe veya parola eşitlenen kullanıcılar için şirket içi parolaları hello buluta yönetilmesine izin verir. Parola geri yazma gerektirir [Azure AD Premium](active-directory-get-started-premium.md).

## <a name="why-choose-azure-ad-self-service-password-reset"></a>Neden Azure seçin AD Self Servis parola sıfırlama

* **Maliyetleri azaltmak** Yardım Masası ve Destek Yardımlı parola sıfırlama genellikle BT kuruluşun % 20 harcamanız
* **Son kullanıcı deneyimleri geliştirmek** ve **Yardım Masası miktarının azaltılmasını** vererek son kullanıcıların hello güç tooresolve kendi parola sorunları aynı anda bir Yardım Masası çağırma veya bir destek isteği açma.
* **Mobility sürücü** kullanıcılar oldukları yerlerde gelen parolalarını sıfırlayabilir gibi.

## <a name="azure-ad-self-service-password-reset-availability"></a>Kullanılabilirlik Azure AD Self Servis parola sıfırlama

Azure AD Self Servis parola sıfırlama, aboneliğinize bağlı olarak üç katmanı de vardır.

* **Azure AD serbest** – yalnızca bulut yöneticiler kendi parolalarını sıfırlama
* **Azure AD temel** veya tüm **Ücretli Office 365 aboneliği** – yalnızca bulut kullanıcıların ve yöneticilerin yalnızca bulut kendi parolalarını sıfırlamak
* **Azure AD Premium** – herhangi bir kullanıcı veya yönetici salt bulut dahil olmak üzere, Federasyon veya parola kullanıcılar eşitlenmiş, kendi parolalarını sıfırlayabilir. Şirket içi parolaları, parola geri yazma toobe etkin gerektirir.

## <a name="azure-ad-self-service-password-reset-a-sum-of-hello-parts"></a>Azure AD Self Servis parola sıfırlama, hello bölümleri toplamı

Self Servis parola sıfırlama Azure AD'de bileşenleri aşağıdaki Merhaba oluşur:

* **Parola yönetimi yapılandırma portalı** burada denetleyebilirsiniz parolalar hello Azure portal aracılığıyla kiracınızda nasıl yönetilir seçenekleri
* **Parola sıfırlama kayıt portalı** burada kullanıcılar kendi kendine kaydolabilir parola sıfırlama için
* **Parola sıfırlama portalı** burada kullanıcılar hello Yöneticisi tarafından tanımlanmış hello zorluklar kullanarak parolalarını sıfırlamak ve hello yanıtlar kullanıcılar olması koşuluyla
* **Kullanıcı parola değişikliği portalı** burada kullanıcılar değiştirebilir kendi parolalarını eski parolalarını girerek ve yeni bir parola sağlama
* **Parola yönetimi raporları** burada yöneticiler görüntüleyebilir ve parola etkinliği analiz raporları hello Azure portal'ın kiracıları için
* **Parola geri yazma tooon Azure AD Connect kullanarak şirket içi** , Federasyon, şirket tooenable yönetilmesine izin verir veya parola eşitlenen hello bulut kullanıcıları

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a>Azure AD fiyatlandırma, SLA, güncelleştirmeleri ve yol haritası

Bu konular hakkında daha fazla ayrıntı sayfaları aşağıdaki hello üzerinde bulunabilir.

* [**Azure AD fiyatlandırma ayrıntıları**](https://azure.microsoft.com/pricing/details/active-directory/)
* [**Office 365 fiyatlandırma**](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [**Azure hizmet düzeyi sözleşmeleri**](https://azure.microsoft.com/support/legal/sla/)
* [**Microsoft Çevrimiçi Hizmetler için hizmet düzeyi sözleşmesi**](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [**Azure güncelleştirmeleri**](https://azure.microsoft.com/updates/)
* [**Azure yol haritası**](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a>Sonraki adımlar

bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi
* [**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma
* [**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? -Her zaman tooask istediğinizi tooquestions yanıtlar
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin


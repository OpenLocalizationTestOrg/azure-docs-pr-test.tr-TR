---
title: "Azure AD kullanarak aaaManaging erişim tooapps | Microsoft Docs"
description: "Azure Active Directory kuruluş toospecify hello uygulamaları toowhich nasıl sağladığını açıklar her kullanıcının erişimi vardır."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: b0829f18-9e57-4107-925d-5f0457d81671
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: b9461b7a1cc8913cd8fb4a4ce0778afe03274935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-access-tooapps"></a>Erişim tooapps yönetme
Bir uygulama, kuruluşunuzun kimlik sisteme tümleştirildikten sonra devam eden erişim yönetimi, kullanım değerlendirme ve raporlama toobe bir sınama devam eder. Çoğu durumda, BT yöneticileri veya Yardım Masası sahip tootake erişim tooyour uygulamaları yönetme bir devam eden etkin rol. Bazı durumlarda, atama genel veya bölümsel BT ekibi tarafından gerçekleştirilir. Genellikle, hello atama onaylarını BT yapar önce gerektiren hedeflenen toobe temsilci toohello iş karar veren, karardır hello atama.  Varolan otomatik kimlik ve erişim yönetimi sistemi kullanarak, rol tabanlı erişim denetimi (RBAC) veya öznitelik tabanlı erişim denetimi (ABAC) gibi tümleştirme, diğer kuruluşların yatırım. Merhaba tümleştirme ve kural geliştirme toobe özelleştirilmiş ve pahalı eğilimi gösterir. İzleme veya raporlama ya da Yönetim yaklaşımını kendi ayrı, pahalı ve karmaşık bir yatırımdır.

## <a name="how-does-azure-active-directory-help"></a>Azure Active Directory nasıl yardımcı olur?
 Yapılandırılan uygulamalar, kuruluşların tooeasily etkinleştirme için Azure AD destekler kapsamlı erişim yönetimi elde hello doğru erişim ilkeleri de dahil olmak üzere ve temsilci aracılığıyla otomatik, öznitelik tabanlı atama (ABAC veya RBAC senaryolarında) arasında değişen Yönetici Yönetimi. Azure AD ile kolayca karmaşık ilkeleri, tek bir uygulama için birden fazla yönetim modeli birleştirme elde edebilirsiniz ve hatta yeniden kullanma Yönetim kuralları ile uygulamalar arasında aynı izleyicileri hello.

* [Uygulamaların mevcut veya yeni ekleme](active-directory-sso-integrate-saas-apps.md)

 Azure AD uygulama atama iki birincil atama modlarını odaklanır:

* **Tek tek atama** directory genel yönetici izinlerine sahip bir BT yöneticisi bireysel kullanıcı hesapları seçin ve bunları erişim toohello uygulama.
* **Grup tabanlı atama (yalnızca Azure AD Ücretli)** directory genel yönetici izinlerine sahip bir BT yöneticisi, bir grup toohello uygulaması atayabilirsiniz. Belirli kullanıcıların erişimini hello zaman hello grubunun üyesi olup FS.fabrikam.com'u çözümlemeye tooaccess Merhaba uygulaması tarafından belirlenir. Diğer bir deyişle, bir yönetici etkili bir şekilde "Merhaba grubuna atanmış herhangi bir geçerli üye erişimi toohello uygulama var" belirten bir atama kuralı oluşturabilirsiniz. Bu atama seçeneğini kullanarak, yöneticiler de dahil olmak üzere, Azure AD Grup Yönetim seçeneklerinden birini yararlanabilir [öznitelik tabanlı dinamik grupların](active-directory-accessmanagement-manage-groups.md), dış sistem grupları (örneğin, şirket içi Active Directory veya Workday) veya yönetici tarafından yönetilen veya self-servis yönetilen grupları. Tek bir grup kolayca toomultiple uygulamalar atama benzeşim uygulamalarla atama kurallarının paylaşabilirsiniz azaltma sağlama atanabilir hello genel yönetim karmaşıklığı. Lütfen unutmayın. Bu iç içe geçmiş grup üyelikleri grup tabanlı atama tooapplications için şu anda desteklenmiyor.

Bu iki atama modlarını kullanarak, Yöneticiler tüm arzu atama yönetim yaklaşım elde edebilirsiniz.

Azure AD ile kullanım ve atama raporlama tam olarak tümleşiktir, yöneticiler tooeasily raporda atama durumu, atama hataları ve hatta kullanımını etkinleştirme.

## <a name="complex-application-assignment-with-azure-ad"></a>Azure AD ile karmaşık bir uygulama atama
Salesforce gibi bir uygulamayı göz önünde bulundurun. Birçok kuruluşta, Salesforce öncelikle hello pazarlama ve satış kuruluşlar tarafından kullanılır. Genellikle, hello pazarlama ekibinin üyeleri yüksek oranda hello satış ekibinin üyeleri Sınırlı erişime sırada erişim tooSalesforce ayrıcalıklı olan. Çoğu durumda, bilgi çalışanı geniş bir popülasyonun bir kısıtlı erişim toohello uygulama. Özel durumlar toothese kuralları da zorlaştırabilir. Merhaba prerogative hello pazarlama veya satış liderlik takımlar toogrant kullanıcı erişimi, görülür veya rollerine genel kurallar bağımsız olarak değiştirin.

Azure AD ile uygulamaları Salesforce gibi tek oturum açma (SSO) ve otomatik sağlama için önceden yapılandırılmış olabilir. Merhaba uygulaması yapılandırıldıktan sonra yönetici hello tek seferlik eylem toocreate alın ve hello uygun gruplara atayın. Bu örnekte, bir yönetici atamaları aşağıdaki hello yürütebilir:

* [Dinamik grupların](active-directory-accessmanagement-manage-groups.md) olması tanımlı tooautomatically temsil edebilen hello pazarlama ve satış takımları bölüm ya da rolü gibi özniteliklere kullanarak tüm üyeleri:
  
  * Pazarlama grupların tüm üyelerinin Salesforce toohello "Pazarlama" rolü atanmış olur
  * Tüm üyeleri satış, ekip grupları toohello "Satış" Salesforce rolünde atanması. Daha fazla iyileştirme toodifferent Salesforce rolleri atanmış bölgesel satış ekipleri temsil eden birden çok gruplarını kullanabilirsiniz.
* tooenable hello özel durum mekanizması, her rol için bir Self Servis Grup oluşturulamadı. Örneğin, bir Self Servis grup olarak hello "özel durum pazarlama Salesforce" Grup oluşturulabilir. Merhaba Grup toohello Salesforce pazarlama rolü atanabilir ve hello pazarlama liderlik ekibindeki sahipleri yapılabilir. Hello pazarlama liderlik ekibinin üyeleri ekleyin veya kullanıcıları Kaldır, bir birleşim İlkesi ayarlamak bile onaylamak veya bireysel kullanıcılar istekleri toojoin reddet. Bu, özel eğitim sahipleri veya üyeleri için gerektirmez bir bilgi çalışanı uygun deneyimi aracılığıyla desteklenir.

Bu durumda, kendi rol ataması Salesforce'ta güncelleştirilmesi eklenen toodifferent grupları oldukları gibi tüm atanan kullanıcılar otomatik olarak sağlanan tooSalesforce olacaktır. Kullanıcılar mümkün toodiscover olması ve ancak Salesforce yoluyla hello Microsoft uygulama erişim paneli, Office web istemcileri veya hatta tootheir kuruluş Salesforce oturum açma sayfasına giderek erişim. Yöneticiler kullanarak Azure AD raporlama mümkün tooeasily kullanım ve atama durumu görüntüle olacaktır.

Yöneticiler işe [Azure AD koşullu erişimi](active-directory-conditional-access.md) belirli roller için tooset erişim ilkeleri. Bu ilkeler, erişim hello şirket ortamında ve hatta çok faktörlü kimlik doğrulaması veya cihaz gereksinimleri tooachieve erişim çeşitli durumlarda dışında yüklenmesine izin verilmeyeceğini içerebilir.

## <a name="how-can-i-get-started"></a>Çalışmaya nasıl?
İlk Azure AD zaten kullanmadığınız ve bir BT yöneticisi misiniz:

* [Deneyin!](https://azure.microsoft.com/trial/get-started-active-directory/) -bir ücretsiz 30 günlük deneme için kaydolabilirsiniz Bugün ve ilk bulut çözümünüzü altında 5 bu bağlantıyı kullanarak dakika içinde dağıtma

Hesap paylaşımını etkinleştir azure AD özellikleri içerir:

* [Grup ataması](active-directory-accessmanagement-self-service-group-management.md)
* Uygulamaları tooAzure AD ekleme
* Atama ile çalışmaya başlama
* Uygulama atama hakkında SSS
* [Uygulama kullanım Pano/raporları](active-directory-passwords-get-insights.md)

## <a name="where-can-i-learn-more"></a>Burada daha fazla bilgi edinebilirsiniz?
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Koşullu erişim ile uygulamaları koruma](active-directory-conditional-access.md)
* [Self Servis Grup Yönetimi/SSAA](active-directory-accessmanagement-self-service-group-management.md)


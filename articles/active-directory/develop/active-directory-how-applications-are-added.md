---
title: "aaaHow uygulamaları tooAzure Active Directory eklenir."
description: "Bu makalede, Azure Active Directory tooan örneğini uygulamaları nasıl eklenir açıklanmaktadır."
services: active-directory
documentationcenter: 
author: shoatman
manager: kbrint
editor: 
ms.assetid: 3321d130-f2a8-4e38-b35e-0959693f3576
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: shoatman
ms.custom: aaddev
ms.openlocfilehash: 3ca710c58a403b52e8b728202ad9010f4873bcea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-and-why-applications-are-added-tooazure-ad"></a>Uygulamaları tooAzure AD neden ve nasıl eklenir
Başlangıçta şeyler uygulamaların bir listesini, Azure Active Directory örneğinde görüntülerken puzzling hello birini hello uygulamaları nereden geldiğini ve orada bulunma anlamaktır.  Bu makalede uygulamaların nasıl hello dizininde sunulur ve nasıl uygulama dizininizde toobe gelen anlamak yardımcı olacak bağlamına sahip sağlamak bir üst düzey genel bakış sağlar.

## <a name="what-services-does-azure-ad-provide-tooapplications"></a>Hangi hizmetlerin Azure AD tooapplications sağlar?
Uygulamaları tooAzure AD tooleverage bir veya daha fazla hello hizmetlerinin sağladığı eklenir.  Bu hizmetler şunlardır:

* Uygulama kimlik doğrulaması ve yetkilendirme
* Kullanıcı kimlik doğrulaması ve yetkilendirme
* Çoklu oturum Federasyon veya parola kullanarak açma (SSO)
* Kullanıcı sağlama ve eşitleme
* Rol tabanlı erişim denetimi; Kullanım hello dizin toodefine uygulama rolleri tooperform rolleri bir uygulamada yetkilendirme denetimleri temel.
* oAuth yetkilendirme Hizmetleri (Office 365 ve diğer Microsoft uygulamaları tooauthorize tooAPIs/kaynaklara erişmesi tarafından kullanılır.)
* Uygulama yayımlama & proxy; Özel ağ toohello uygulama yayımlama Internet

## <a name="how-are-applications-represented-in-hello-directory"></a>Nasıl uygulamaları hello dizininde sunulur?
Merhaba 2 nesneleri kullanarak Azure AD uygulamaları temsil edilen: uygulama nesnesi ve bir hizmet sorumlusu nesnesi.  "Home" kayıtlı bir uygulama nesnesi / "sahip" veya "yayımlama" dizini ve bir veya daha içinde davranır her dizin hello uygulamada temsil eden asıl nesneleri hizmet.  

Merhaba uygulama nesnesi hello uygulama tooAzure AD (Merhaba çok kiracılı hizmeti) açıklar ve hello aşağıdakilerden herhangi birini içerebilir: (*Not*: Bu kapsamlı bir liste değildir.)

* Adı, logosu ve yayımcı
* Gizli (simetrik ve/veya asimetrik anahtarlar tooauthenticate hello uygulama kullanılır)
* API bağımlılıkları (oAuth)
* API/kaynakları/yayımlanan kapsamları (oAuth)
* Uygulama rolleri (RBAC)
* SSO meta verileri ve yapılandırma (SSO)
* Kullanıcı meta verileri ve yapılandırma hazırlama
* Proxy meta verileri ve yapılandırma

Merhaba hizmet sorumlusu burada kendi ana dizini de dahil olmak üzere Merhaba uygulaması davranır her dizin hello uygulamada kaydıdır.  Merhaba hizmet sorumlusu:

* Geri tooan uygulama nesnesi hello uygulama kimliği özelliği aracılığıyla başvurur
* Kayıtları yerel kullanıcı ve Grup uygulama rol atamaları
* Toohello uygulama kayıtları yerel kullanıcı ve yönetici izinlerine sahip
  * Örneğin: hello uygulama tooaccess belirli kullanıcılara e-posta izni
* Koşullu erişim ilkesi dahil olmak üzere kayıtları yerel ilkeler
* Kayıtları yerel alternatif yerel ayarları bir uygulama için
  * Talep dönüştürme kuralları
  * Özellik eşlemeleri (kullanıcı hazırlama)
  * (Merhaba uygulama özel roller destekliyorsa) belirli uygulama rolleri Kiracı
  * Ad/logosu

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a>Uygulama nesneleri ve hizmet asıl adı dizinler genelinde diyagramı
![Nasıl uygulama nesneleri ve Azure AD örnekleriyle varolan ilkeleri hizmet gösteren diyagram.][apps_service_principals_directory]

Diyagram hello yukarıdaki görebileceğiniz gibi.  Microsoft'un iki dizini toopublish uygulamaları dahili olarak (Merhaba sol tarafta) kullanır.

* Bir Microsoft Apps (Microsoft Hizmetleri dizini)
* Önceden tümleştirilmiş 3 taraf uygulamaları (uygulama Galerisi dizin) için bir tane

Azure AD ile tümleştirmek uygulama yayımcıları/satıcıları gerekli toohave yayımlama dizini var.  (Bazı SAAS dizin).

Kendinizi ekleyin uygulamalar şunlardır:

* Geliştirilmiş uygulamalara (AAD ile tümleşik)
* Uygulamaları bağlı için çoklu oturum açma
* Kullanılarak yayımlanan uygulamaları Azure AD uygulama proxy'si hello.

### <a name="a-couple-of-notes-and-exceptions"></a>Birkaç notlar ve özel durumlar
* Tüm hizmet asıl adı geri tooapplication nesneleri gelin.  Huh? Azure AD ilk olarak yapılandırıldığında hello Hizmetleri tooapplications çok daha kısıtlı ve hello hizmet sorumlusu bir uygulama kimliği oluşturmak için yeterli sağlanan.  Merhaba özgün hizmet sorumlusu şekli toohello Windows Server Active Directory hizmet hesabı yakın.  Hala olası toocreate olduğundan bu nedenle, uygulama nesnesi oluşturmadan, Azure AD PowerShell kullanarak hizmet asıl adı hello.  Merhaba grafik API'si, bir hizmet asıl oluşturmadan önce bir uygulama nesnesi gerektirir.
* Yukarıda açıklanan hello bilgilerin tümünü şu anda açık program aracılığıyla.  Merhaba yalnızca hello UI kullanılabilir şunlardır:
  * Talep dönüştürme kuralları
  * Özellik eşlemeleri (kullanıcı hazırlama)
* Daha fazla bilgi için ilgili hello hizmet sorumlusu ayrıntılı bilgi ve uygulama nesneleri Lütfen toohello Azure AD grafik REST API başvuru belgelerine bakın.  *İpucu*: hello Azure AD Graph API belgelerine olduğu hello en yakın şey tooa şema başvurusu için şu anda Azure AD.  
  * [Uygulama](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [Hizmet sorumlusu](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-toomy-azure-ad-instance"></a>Uygulamaları toomy Azure AD örneğinde nasıl eklenir?
Bir uygulama tooAzure AD eklenebilir birçok yolu vardır:

* Merhaba bir uygulama ekleyin [Azure Active Directory Uygulama Galerisi](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)
* Oturum/taraf uygulama Azure Active Directory ile tümleşik 3 halinde (örneğin: [Smartsheet](https://app.smartsheet.com/b/home) veya [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))
  * Yukarı/kullanıcılar oturum sırasında sorulan toogive izin toohello uygulama tooaccess profillerini ve diğer izinler markalarıdır.  Merhaba ilk kişinin toogive hello uygulama toobe eklenen toohello dizini temsil eden bir hizmet sorumlusu nedenler olursunuz.
* Oturum/Microsoft çevrimiçi hizmetlerine ister [Office 365](http://products.office.com/)
  * Hizmetine abone olduğunuzda tooOffice 365 deneme bir başlatmak veya daha fazla hizmet asıl adı Office 365 ile ilişkili tüm hello işlevlerin kullanılan toodeliver çeşitli hizmetler hello temsil eden hello dizininde oluşturulur.
  * SharePoint gibi bazı Office 365 Hizmetleri hizmet asıl adı bir iş akışları dahil olmak üzere bileşenler arasındaki iletişimi güvenli devam eden temel tooallow oluşturun.
* Azure Yönetim Portalı bkz hello geliştirme bir uygulama ekleyin: https://msdn.microsoft.com/library/azure/dn132599.aspx
* Visual Studio kullanarak geliştirirken bir uygulama görmek ekleyin:
  * [ASP.Net kimlik doğrulama yöntemleri](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [Bağlı hizmetler](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* Bir uygulama toouse toouse hello eklemek [Azure AD uygulama proxy'si](https://msdn.microsoft.com/library/azure/dn768219.aspx)
* SAML ya da parola SSO kullanma tek oturum için bir uygulamaya Bağlan
* Diğer birçok Azure içinde çeşitli Geliştirici deneyimleri de dahil olmak üzere ve/içinde API'si Gezgini Geliştirici merkezleri arasında deneyimleri

## <a name="who-has-permission-tooadd-applications-toomy-azure-ad-instance"></a>Kimin izni tooadd uygulamaları toomy Azure AD örneğinde var?
Yalnızca genel yöneticiler şunları yapabilir:

* Hello Azure AD uygulama Galerisi'nden (önceden tümleştirilmiş 3 taraf uygulamaları) uygulama ekleme
* Hello Azure AD uygulama ara sunucusu kullanarak uygulama yayımlama

Dizininizdeki tüm kullanıcılara, geliştirmekte olduğunuz hakları tooadd uygulamaları ve hangi uygulamaların bunlar paylaşım/erişim tootheir kuruluş verilerini verin tedbirli sahip.  *Bir hizmet sorumlusu oluşturuluyor izni veriliyor izinler neden olabilir ve kullanıcı oturum yukarı/uygulamasında tooan unutmayın.*

Bu kaybolabileceğini başlangıçta ses ilgili, ancak göz önünde aşağıdaki Koru hello:

* Uygulamaları mümkün tooleverage Windows Server Active Directory kullanıcı kimlik doğrulaması için kayıtlı/kaydedilen hello dizininde hello uygulama toobe gerektirmeden yıllardır olmuştur.  Merhaba kuruluş görünürlük tooexactly geliştirilmiş artık kaç uygulamaları başlangıç dizini ve neler için kullanıyorsunuz.
* Uygulama yayımlama/kayıt sürecine kullanımlı yönetici gerek yoktur.  Active Directory Federasyon Hizmetleri ile bir yönetici tooadd uygulama geliştiricilerin adına bağlı olan taraf olarak olduğunu büyük olasılıkla.  Şimdi geliştiriciler Self Servis edebilirsiniz.
* Oturum/iş amaçlı kuruluş hesaplarını kullanarak tooapps yukarı kullanıcılar iyi bir şeydir.  Daha sonra hello kuruluş bırakırsanız erişim tootheir hesabı kullanmakta oldukları hello uygulamada kaybederler.
* Hangi verilerin uygulama dâhil olduğu paylaşıldı kaydını sahip.  Veri zamankinden daha aktarılabilir ve kimlerin hangi uygulamaları ile hangi verilerin paylaşılan Temizle kaydını sahip yararlıdır.
* Azure AD için oAuth kullanan uygulamalar mümkün toogrant tooapplications kullanıcılardır ve bir yönetici tooagree hangi izinleri gerektiren tam olarak hangi izinlerin karar verin.  Yalnızca Yöneticiler toolarger kapsamlar ve daha önemli izinleri onaylaması gerektiğini söyleyen olmadan tamamlamalıdır.
* Ekleme ve hello Denetim raporları hello Azure Yönetimi portalı toodetermine içinde görüntüleyebilmeniz verilerine olan uygulamalar tooaccess olayları denetlenen vererek kullanıcıların nasıl toohello dizin uygulama eklendi.

**Not:** *Microsoft kendisini işletim şimdi birçok ay hello varsayılan yapılandırması'nı kullanarak.*

Tüm bu olası tooprevent kullanıcılar dizininizde uygulama ekleme ve dizin yapılandırma hello Azure Yönetim Portalı'nda değiştirerek uygulamalarla paylaştıkları hangi bilgilerin üzerinden tedbirli kullanan olduğu belirtti.  Merhaba aşağıdaki yapılandırma hello Azure Yönetim Portalı, dizinin "Yapılandırma" sekmesinde içinde erişilebilir.

![Tümleşik uygulama ayarlarını yapılandırma UI hello ekran görüntüsü][app_settings]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
Hakkında daha fazla bilgi tooadd uygulamaları tooAzure AD ve tooconfigure uygulamalar için hizmetleri nasıl.

* Geliştiricileri: [öğrenin nasıl toointegrate AAD ile bir uygulama](https://msdn.microsoft.com/library/azure/dn151122.aspx)
* Geliştiricileri: [github'da Azure Active Directory ile tümleşik uygulamalar için örnek kod gözden geçirme](https://github.com/AzureADSamples)
* Geliştiriciler ve BT uzmanlarının: [hello hello Azure Active Directory grafik API'si için REST API belgeleri gözden geçirin](https://msdn.microsoft.com/library/azure/hh974478.aspx)
* BT uzmanları: [nasıl toouse Azure Active Directory Uygulama galerisinde hello uygulamalardan önceden tümleştirilmiş öğrenin](https://msdn.microsoft.com/library/azure/dn308590.aspx)
* BT uzmanları: [Bul belirli önceden tümleştirilen uygulamalar yapılandırma öğreticileri](https://msdn.microsoft.com/library/azure/dn893637.aspx)
* BT uzmanları: [nasıl kullanarak bir uygulama toopublish hello Azure Active Directory Uygulama proxy'si öğrenin](https://msdn.microsoft.com/library/azure/dn768219.aspx)

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](../active-directory-apps-index.md)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg

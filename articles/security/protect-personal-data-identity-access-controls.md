---
title: "Azure kimlik ve erişim denetimleri ile kişisel veriler aaaProtect | Microsoft Docs"
description: "Azure kimlik ve erişim denetimleri toohelp kullanarak kişisel verilerinizi koruyun"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a>Azure Active Directory ve çok faktörlü kimlik doğrulaması: kimlik ve erişim denetimleri ile kişisel verileri koruma

Bu makalede bilgi ve Azure Active Directory ve çok faktörlü kimlik doğrulama güvenlik özellikleri ve Hizmetleri kullanarak tooprotect kişisel verileri kullanabileceğiniz yordamlar sağlar.

## <a name="scenario"></a>Senaryo

Merhaba Amerika Birleşik Devletleri'nde yönetim büyük seyahat şirket, kendi işlemleri toooffer programlarıyla hello Akdeniz, Adriatic ve Baltık seas yanı sıra hello İngiliz Adaları arasında içinde genişletmektedir. toosupport bu çaba İtalya, dayanarak birkaç küçük seyahat satırları geçirmiş Almanya, Danimarka ve hello İngiltere 

Merhaba şirket hello bulutta Microsoft Azure toostore şirket verileri kullanır. Bu ad, adres, telefon numaraları gibi kişisel olarak tanımlanabilir bilgileri ve genel müşteri tabanı, kredi kartı bilgilerini içerir. Ayrıca tüm konumlarda adresleri, telefon numaralarını, vergi kimlik numaraları ve şirket çalışanlarının tıbbi bilgi gibi geleneksel İnsan Kaynakları bilgileri içerir. Merhaba seyahat satır Ayrıca, kişisel bilgi tootrack ilişkileri geçerli ve geçmiş müşterilerle içeren büyük bir veritabanını ödül ve bağlılık programı üyeleri korur.

Şirket çalışanları erişim hello ağdan hello şirketin şubelere ve seyahat aracılar bulunan Merhaba Dünya toosome şirket kaynaklarına sahip.

## <a name="problem-statement"></a>Sorun bildirimi

Merhaba şirket müşterilerin ve çalışanların kişisel verilerin hello gizliliği tehlikeye toouse kimlikleri toogain erişim aramayı saldırganlardan korumanız gerekir. Bunlar ayrıca veri yasal kullanıcılar tarafından yalnızca toodo ihtiyacınız olan olanlar için sınırlı bu erişim toopersonal işlerini emin olmalısınız.

## <a name="company-goal"></a>Şirket hedefi

Merhaba şirketin toopersonal veri erişim tooensure kesinlikle denetlenir hedeftir. Erişim toopersonal veri ile kullanıcıların kimliklerini güçlü kimlik doğrulamasıyla korunması önemlidir. Bir ilke [en az ayrıcalık] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) gerekir zorunlu böylece yasal kullanıcıların ihtiyaç duydukları erişim ve artık yalnızca hello düzeyi.

## <a name="solutions"></a>Çözümler

Microsoft Azure kimlik ve erişim yönetimi araçları kişisel verileri içeren erişim tooresources sahip toohelp şirketler denetimi sağlar.

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) kimlikleri yönetir ve sair şirket içi ve diğer bulut kaynakları, veri ve uygulamaları tooAzure erişimi kontrol eder. [Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) Azure Yöneticiler toominimize hello kişisel verileri gibi erişim toocertain bilgileri olan kişiler sayısı yardımcı olur. Bu toodiscover sağlar, kısıtlamak ve ayrıcalıklı kimliklerinizi ve bunların erişim tooresources tooassign geçici, Just-In-Time (JIT) yönetici hakları tooeligible kullanıcıların ve izleme. Ayrıca, kullanıcılar AAD yönetici ayrıcalıklarına sahip bir anlayış sağlar.

AAD PIM kullanarak söz konusu Hello etkinlikleri içerir:

- Privileged Identity Management dizininiz için etkinleştirme

- Privileged Identity Management Yönetim Panosu toosee önemli bilgileri bir bakışta kullanma

- Merhaba ayrıcalıklı kimlikleri (Yöneticiler) ekleyerek veya kaldırarak kalıcı veya uygun Yöneticiler tooeach rolünü yönetme

- Merhaba rol etkinleştirme ayarlarını yapılandırma

- Rol etkinleştirme

- Rol etkinliği gözden geçirme

#### <a name="how-do-i-enable-aad-pim"></a>AAD PIM nasıl etkinleştirebilirim?

PIM dizininiz için kullanarak toostart aşağıdaki hello:

1. Toohello Azure portal dizininizin genel yönetici olarak oturum açın.

2. Kuruluşunuz birden fazla dizine sahipse, kullanıcı adınızı hello sağ üst köşesinde hello Azure portalı içinde seçin. Burada, Azure AD Privileged Identity Management kullanacağınız hello dizini seçin.

3. Seçin **daha fazla hizmet** ve hello **filtre** textbox toosearch Azure AD Privileged Identity Management için.

4. Denetleme **PIN toodashboard** ve ardından **oluşturma**. Merhaba Privileged Identity Management uygulaması açılır.

Azure AD Privileged Identity Management ayarladıktan sonra hello uygulamayı her açtığınızda hello Gezinti dikey penceresine bakın.

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

Daha fazla bilgi ve AAD PIM ile çalışmaya başlama hakkında yönergeler için bkz: [Başlat kullanarak Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)

### <a name="azure-role-based-access-control"></a>Azure rol tabanlı erişim denetimi

[Azure rol tabanlı erişim denetimi](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) tooAzure kaynaklarına erişim hello hello kullanıcının atanan rolüne dayalı erişim verme etkinleştirerek Azure yönetmesine yardımcı olur. Ekip içinde görevlerini kurabilmeleri ve erişim toousers, grupları ve tooperform işlerini gereken uygulamalar, yalnızca hello miktarını verebilirsiniz.

Rol tabanlı erişim toousers hello Azure portal, Azure komut satırı araçları ve Azure Management API'leri kullanılarak verilebilir.

Azure RBAC temel kavramları hakkında daha fazla bilgi için bkz: [hello Azure Portal'ın rol tabanlı erişim denetimi kullanmaya başlayın.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a>PowerShell ile Azure RBAC nasıl yönetebilirim?

PowerShell cmdlet'leri toomanage Azure RBAC, yönetim görevleri aşağıdaki hello dahil olmak üzere kullanabilirsiniz:

- Liste rolleri

- Kimlerin erişebileceğini bakın

- Erişim verme

- Erişimi kaldırma

- Özel bir rol oluşturun

- Bir kaynak sağlayıcısı için Eylemler Al

- Özel bir rol değiştirme

- Bir özel rolü silmeyi

- Liste özel roller

Yönergeler için nasıl toomanage PowerShell ile Azure RBAC bkz [yönetmek rol tabanlı erişim Azure PowerShell ile](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).

### <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication

[Azure çok faktörlü kimlik doğrulaması](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA), koruma erişim toodata ve uygulamalar, basit bir oturum açma işlemi için kullanıcı talebine buluştururken yardımcı olan iki aşamalı doğrulama çözüm. Bir dizi doğrulama yöntemi (ör. telefon çağrısı, metin mesajı veya mobil uygulama doğrulaması) aracılığıyla güçlü kimlik doğrulaması sunar.

MFA toodeploy hello Azure bulut içinde toofirst ihtiyacınız etkinleştirmek ve kullanıcılar için iki aşamalı doğrulamayı etkinleştirin.

#### <a name="how-do-i-enable-azure-toouse-mfa"></a>Azure toouse MFA nasıl etkinleştirebilirim?

Kullanıcılarınızın Azure çok faktörlü kimlik doğrulamasını içeren lisansına sahipseniz, hiçbir şey Azure MFA üzerinde toodo tooturn gerek yoktur. Yoksa, dizininizde toocreate multi-Factor Auth sağlayıcısı gerekir. toodo Bu, şu adımları izleyin:

1. Seçin **Active Directory** hello (yönetici olarak oturum açmış) Klasik Azure Portalı'nda.

2. Seçin **çok faktörlü kimlik doğrulama sağlayıcıları.**

3. Seçin **yeni** altında ve **uygulama hizmetleri,** seçin **multi-Factor Auth sağlayıcısı.**

4. Seçin **hızlı oluştur.**

5. Merhaba ad alanını doldurun ve kullanım modeli (kimlik doğrulaması veya etkin kullanıcı başına) seçin.

6. MFA sağlayıcısı hangi hello ile ilişkili bir dizin belirleyin.

7. Merhaba tıklatın **oluşturma** düğmesi.

![](media/protect-personal-data-identity-access-controls/quick-create.png)

Hakkında daha fazla yönerge için toomanage, çok faktörlü yetki sağlayıcı bkz [Azure multi-Factor Auth sağlayıcısı ile çalışmaya başlama.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a>Kullanıcılar için iki aşamalı doğrulamayı nasıl kapatırım?

Tüm oturum açma işlemleri için iki aşamalı doğrulama zorunlu kılabilir veya yalnızca belirli koşullar geçerli olduğunda, koşullu erişim ilkeleri toorequire iki aşamalı doğrulamayı oluşturabilirsiniz.

Azure MFA kullanıcı durumları değiştirerek etkinleştirme iki aşamalı doğrulama gerektirme hello geleneksel bir yaklaşımdır. Etkinleştirmeniz tüm hello kullanıcıların gerekir oturum her zaman aynı gereksinim tooperform iki aşamalı doğrulamayı hello. Bir kullanıcının kullanıcı etkileyebilecek herhangi bir koşullu erişim ilkeleri geçersiz kılar.

Koşullu erişim ilkesi ile Azure MFA'yı etkinleştirerek, iki aşamalı doğrulama gerektirme daha esnek bir yaklaşımdır. Tek tek kullanıcılar yanı sıra toogroups uygulamak koşullu erişim ilkeleri oluşturabilirsiniz. Daha fazla kısıtlama düşük riskli grupları daha yüksek riskli grupları verilebilir veya iki aşamalı doğrulamayı yalnızca yüksek riskli bulut uygulamaları için gereklidir ve düşük riskli için olanları atlandı. Ancak, koşullu erişim Azure Active Directory, ücretli bir özelliğidir.

kullanıcı durumunu değiştirerek MFA tooenable hello aşağıdaki:

1. İçinde toohello Azure portalında yönetici olarak oturum açın.
2. Çok Git**Azure Active Directory \> kullanıcılar ve gruplar \> tüm kullanıcılar**.
3. Seçin **çok faktörlü kimlik doğrulaması**.
4. Azure MFA için tooenable istediğiniz Bul hello kullanıcı. Toochange gerekebilir hello hello üstünde görüntüle.
5. Merhaba kutusunu sonraki toohello kullanıcının adını kontrol edin.
6. Hızlı adımlar altında sağ Hello üzerinde seçin **etkinleştirmek**.

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. Açılır hello açılır pencerede Seçiminizi onaylayın.  MFA kendisi için etkinleştirilmiş kullanıcılar oturum açtığında tooregister hello istenir.

bir koşullu erişim ilkesi ile Azure MFA tooenable hello aşağıdaki:

1. İçinde toohello Azure portalında yönetici olarak oturum açın.

2. Çok Git**Azure Active Directory \> koşullu erişim**.

3. Seçin **yeni ilke**.

4. Altında **atamaları**seçin **kullanıcılar ve gruplar**. Kullanım hello **INCLUDE** ve **hariç** hangi kullanıcıların ve grupların hello İlkesi tarafından yönetilecek toospecify sekmeler.

5. Altında **atamaları**seçin **bulut uygulamaları.** Çok seçin**tüm bulut uygulamaları dahil**.
6.  Altında **erişim denetimleri**seçin **Grant**. Seçin **çok faktörlü kimlik doğrulaması gerektiren**.
7.  Kapatma **ilkesini etkinleştir** çok**üzerinde** ve ardından **kaydetmek**.

Hakkında bilgi için bir kerelik geçiş tooconfigure Azure MFA ayarları tooset sahtekarlık uyarısı yukarı oluşturmak nasıl özel sesli mesajları kullanın, önbelleğe alınmasını yapılandırmak, güvenilen IP'leri belirtin, uygulama parolaları oluşturma, kullanıcıların güven cihazlar ve select için MFA hatırlama etkinleştir doğrulama yöntemlerini görmek [Azure çok faktörlü kimlik doğrulama ayarlarını yapılandırın.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)

## <a name="next-steps"></a>Sonraki adımlar

- [Azure AD'de ayrıcalıklı erişimi güvenli hale getirme](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [Azure Multi-Factor Authentication hakkında sık sorulan sorular](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [Rol tabanlı erişim denetimi sorunlarını giderme](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [Azure Active Directory kimlik koruması](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)

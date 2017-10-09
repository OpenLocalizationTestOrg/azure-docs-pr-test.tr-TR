---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - karma kimlik yaşam döngüsü benimseme stratejinizi belirleme | Microsoft Docs"
description: "Merhaba karma kimlik yönetimi görevleri her yaşam döngüsü aşaması için toohello seçenekleri göre tanımlamasına yardımcı olur."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 420b6046-bd9b-4fce-83b0-72625878ae71
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 86ec0a9896f069bc93e49e06006954848f8e4d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-hybrid-identity-lifecycle-adoption-strategy"></a>Karma kimlik yaşam döngüsü benimseme stratejinizi belirleme
Bu görevde tanımlanan karma kimlik çözümü toomeet hello iş gereksinimleriniz için hello Kimlik Yönetimi stratejisini tanımlayın [karma kimlik yönetimi görevleri belirlemek](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md).

Bu adım tarafından sunulan toohello uçtan uca kimlik yaşam döngüsü göre toodefine hello karma kimlik yönetimi görevleri, her yaşam döngüsü aşaması için kullanılabilir tooconsider hello seçenekleri gerekir.

## <a name="access-management-and-provisioning"></a>Erişim yönetimi ve sağlama
İyi hesap erişim yönetimi çözümüyle kuruluşunuzun tam olarak erişim toowhat bilgileri hello kuruluş genelinde sahip izleyebilirsiniz.

Erişim denetimi, bir merkezi, tek noktası sağlama sistemin kritik bir işlevdir. Hassas bilgileri koruma yanı sıra erişim denetimleri sahip var olan hesapları kullanıma onaylanmamış yetkilerini veya artık gerekli olan. toocontrol eski hesapları sağlama sistem bağlantılar birlikte hesap bilgileri hello hesapları sahibi hello kullanıcılara yetkili bilgilerle hello. Yetkili kullanıcı kimlik bilgileri genellikle hello veritabanları ve İnsan Kaynakları dizinleri korunur.

Gelişmiş BT kuruluşları hesaplarında hello yetkilileri tanımlayan parametreleri yüzlerce içerir ve bu ayrıntıları sağlama sisteminiz tarafından denetlenebilir. Yeni kullanıcılar hello yetkili kaynaktan sağladığınız hello verilerle tanımlanabilir. Merhaba erişim isteği onay özelliği kendileri için sağlama kaynak Onayla (veya reddetme) hello süreçlerini başlatır.

| Yaşam döngüsü yönetimi aşaması | Şirket içinde | Bulut | Karma |
| --- | --- | --- | --- |
| Hesap Yönetimi ve sağlama |Merhaba Active Directory® etki alanı Hizmetleri (AD DS) sunucu rolünü kullanarak, kullanıcı ve kaynak yönetimi için ölçeklenebilir, güvenli ve yönetilebilir bir altyapı oluşturabilir ve Microsoft® Exchange Server gibi dizin özellikli uygulamalar için destek sağlayabilirsiniz. <br><br> [Bir kimlik Yöneticisi aracılığıyla AD DS'deki gruplarının sağlayabilirsiniz](https://technet.microsoft.com/library/ff686261.aspx) <br>[Kullanıcıların AD DS'de sağlayabilirsiniz](https://technet.microsoft.com/library/ff686263.aspx) <br><br> Yöneticiler güvenlik amacıyla erişim denetimi toomanage kullanıcı erişimi tooshared kaynakları kullanabilir. Active Directory'de erişim denetimi hello nesne düzeyinde erişim ya da izinlere tooobjects farklı düzeylerde ayarı tarafından yönetilen gibi tam denetim, okuma, yazma ya da erişim yok. Active Directory'de erişim denetimini tanımlar nasıl farklı kullanıcılar Active Directory nesnelerini kullanabilirsiniz. Varsayılan olarak, Active Directory içindeki nesneleri izinlerini toohello en güvenli ayar ayarlanır. |Toocreate bir Microsoft bulut hizmeti erişen her kullanıcı için bir hesabınız yok. Ayrıca, kullanıcı hesaplarını değiştirmek veya artık gerekmediğinde silin. Varsayılan olarak, kullanıcı yönetici izinlerine sahip değilse, ancak bunları isteğe bağlı olarak atayabilirsiniz. Daha fazla bilgi için bkz: [yöneten kullanıcılar Azure AD'de](active-directory-create-users.md). <br><br> Azure Active Directory içinde hello önemli özelliklerin hello özelliği toomanage erişim tooresources biridir. Bu kaynaklar hello dizin ya da SaaS uygulamaları, Azure Hizmetleri ve SharePoint siteleri veya şirket içi gibi dış toohello directory kaynaklarını rolleri aracılığıyla izinleri toomanage nesnelerin hello durumda olduğu gibi hello dizin parçası olabilir kaynaklar. <br><br> Merhaba Merkezi, Azure Active Directory'nin erişim yönetimi çözümü hello güvenlik grubudur. Merhaba kaynak sahibi (veya hello dizinin hello Yöneticisi) bir grup tooprovide oldukları bir belirli erişim sağ toohello kaynakları atayabilirsiniz. Merhaba grubunun üyeleri, hello hello erişim sağlanması ve hello kaynak sahibi hello sağ toomanage hello üyeleri bir bölüm Yöneticisi'ni veya bir Yardım Masası Yöneticisi gibi başka – bir grup toosomeone listesi atayabilirsiniz<br> <br> Azure AD konudaki Hello yönetme grupları grupları üzerinden erişimi yönetme hakkında daha fazla bilgi sağlar. |Active Directory kimlik eşitleme ve Federasyon aracılığıyla hello buluta genişletme |

## <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi
Rol tabanlı erişim denetimi (RBAC) rollerini kullanır ve ilkeleri tooevaluate sağlama, test ve iş süreçlerini ve erişim toousers verme için kurallar zorlar. Anahtar Yöneticiler sağlama ilkeleri oluşturun ve kullanıcıların tooroles atayın ve bu rolleri yetkilendirmeler tooresources kümelerini tanımlayın. RBAC hello kimlik yönetimi çözümü toouse işlemleri yazılım tabanlı genişletir ve kullanıcı el ile etkileşimini sağlama işlemi hello azaltır.
Azure AD RBAC hello şirket toorestrict hello kendisine erişim tooAzure Yönetim Portalı olduğunda, bir kişinin yapabileceği işlemleri miktarını sağlar. RBAC toocontrol erişim toohello portal kullanarak, BT yöneticilerinin ca temsilci erişimi erişim yönetimi aşağıdaki hello kullanarak yaklaşır:

* **Grup tabanlı rol ataması**: eşitlenebilen tooAzure AD grupları yerel Active Directory'den erişim atayabilirsiniz. Bu, kuruluşunuzun araçları ve grupları yönetmek için işlemlerdeki yaptı tooleverage hello mevcut yatırımların sağlar. Azure AD Premium hello temsilci Grup Yönetimi özelliği de kullanabilirsiniz.
* **Azure rollerinde yerleşik Dengeleme**: üç rol kullanabilirsiniz — sahibi, katkıda bulunan ve okuyucu tooensure kullanıcılar ve gruplar ihtiyaç duydukları toodo işlerini izni toodo yalnızca hello görevler sahiptir.
* **Ayrıntılı erişim tooresources**: roller toousers ve belirli bir abonelik, kaynak grubu veya bir Web sitesi veya veritabanı gibi ayrı bir Azure kaynak grupları atayabilirsiniz. Bu şekilde, kullanıcıların ihtiyaç duydukları tooall hello kaynaklarına erişmek ve toomanage gerekmez hiçbir erişim tooresources sahip olduğunuzdan emin olabilirsiniz.

## <a name="provisioning-and-other-customization-options"></a>Sağlama ve diğer özelleştirme seçenekleri
Ekibinizin iş planları ve gereksinimleri toodecide ne kadar toocustomize hello kimlik çözümü kullanabilirsiniz. Örneğin, büyük bir kuruluş, iş akışları ve artımlı olarak coğrafyalara yaygın olarak kullanılan uygulamaların sağlama için bir zaman çizgisi dayalı özel bağdaştırıcıları için aşamalı bir üretimini planı gerektirebilir. Başka bir planı özelleştirme başarılı test sonra tüm kuruluş, sağlanan iki veya daha fazla uygulamaları toobe için sağlayabilir. Uygulama kullanıcı etkileşimi özelleştirilebilir ve kaynakları hazırlamaya yönelik yordamlar değiştirilen tooaccommodate otomatik sağlama olabilir.

Bir hizmet veya bileşenin tooremove sağlamayı sonlandırın. Örneğin, bir hesap sağlamayı hello hesap bir kaynaktan silinir anlamına gelir.

Kaynak sağlama hello karma modeli istek ve her ikisi de Azure AD tarafından desteklenen rol tabanlı yaklaşımlar birleştirir. Bir alt kümesi çalışanlar veya yönetilen sistemler için bir iş rol tabanlı atama ile tooautomate erişim isteyebilirsiniz. Bir iş ayrıca diğer tüm erişim isteklerini veya istek tabanlı modeli aracılığıyla özel durumları işlemek. Bazı işletmeler el ile atama ile başlamalı ve bir sonraki seferde tam rol tabanlı bir dağıtım amacı ile karma bir modelinin doğru gelişmesi.

Diğer şirketler, pratik iş nedenleri tooachieve tam rol tabanlı sağlama ve hedef karma bir yaklaşım için istenen hedef olarak bulabilirsiniz. Hala diğer şirketlerin yalnızca istek tabanlı sağlamada memnun ve değil tooinvest ek çaba toodefine istediğiniz rol tabanlı, otomatik sağlama ilkeleri ve yönetin.

## <a name="license-management"></a>Lisans Yönetimi
Azure AD'de grup tabanlı lisans yönetimi, yöneticilerin kullanıcıların tooa güvenlik grubu atayın sağlar ve Azure AD lisanslarını tooall hello hello grubunun üyeleri otomatik olarak atar.. Bir kullanıcı daha sonra eklenen veya hello grubundan kaldırılmış, bir lisans otomatik olarak atanmış veya kaldırılacak uygun şekilde kaldırıldı.

Grupları, eşitleme kullanabilirsiniz şirket içi AD veya Azure AD içinde yönetin. Bu Azure AD premium Self Servis Grup Yönetimi ile birlikte kullanılması lisans atama toohello uygun karar alıcılar kolayca devredebilirsiniz. Lisans çakışmaları ve eksik konum verileri gibi sorunları otomatik olarak sıralandığını olabilirsiniz.

## <a name="self-regulating-user-administration"></a>Kendi kendine regulating kullanıcı yönetimi
Kuruluşunuzun tüm iç kuruluşlar arasında tooprovision kaynakları başladığında hello kendi kendine regulating kullanıcı yönetim özelliği uygulayın. Kuruluş sınırları boyunca hello avantajları ve sağlama kullanıcılar avantajlarını sağlarsınız. Bu ortamda otomatik olarak erişim haklarını kullanıcının durumundaki bir değişiklik, kuruluş sınırları ve coğrafyalara arasında yansıtılır. Sağlama maliyetlerini azaltma ve hello erişim ve onay işlemlerini kolaylaştırır. Merhaba uygulama rol tabanlı erişim denetimi uçtan uca erişim yönetimi, kuruluşunuzda uygulamanın tam olası hello gerçekleştirir. Kullanıcı sağlamayı yöneten otomatik yordamlar üzerinden yönetim maliyetlerini azaltabilir. Güvenlik İlkesi zorlaması otomatikleştirerek güvenliğini artırmak ve kolaylaştırmak ve kullanıcının yaşam döngüsü yönetimi ve büyük kullanıcı yerleştirme için kaynak sağlama merkezileştirme.

> [!NOTE]
> Daha fazla bilgi için bkz: self servis uygulamaya erişim yönetimi için Azure AD kurma
> 
> 

Lisans tabanlı Azure AD (yetkilendirme tabanlı), Azure AD directory/hizmet kiracınız abonelikte etkinleştirerek iş Hizmetleri. Merhaba abonelik etkinleştirildikten sonra hello hizmet özellikleri dizin/hizmet yöneticileri tarafından yönetilen ve lisanslı kullanıcılar tarafından kullanılır. Daha fazla bilgi için bkz: Azure AD iş lisanslama nasıl yapar?
Diğer 3. taraf sağlayıcılar ile tümleştirme

Azure Active Directory çoklu oturum sağlar ve SaaS uygulamaları ve şirket içi web uygulamaları, uygulama erişim güvenlik toothousands Gelişmiş. Azure Active Directory Federasyon Uyumluluğu Listesi desteklenen SaaS uygulamaları için Azure Active Directory Uygulama galerisinde ayrıntılı bir listesi için bkz: kullanılan tooimplement olabilecek üçüncü taraf kimlik sağlayıcıları çoklu oturum açma

## <a name="define-synchronization-management"></a>Eşitleme management tanımlama
Şirket içi dizinlerinizin Azure AD ile tümleştirilmesi, kullanıcılarınızın hem bulut kaynaklarına hem de şirket içi kaynaklara erişmesi için ortak bir kimlik oluşturarak daha üretken olmalarını sağlar. İle tümleştirme, kullanıcıların ve kuruluşların hello aşağıdaki özelliklerden yararlanabilirsiniz:

* Kuruluşlar, şirket içi veya Windows Server Active Directory yararlanan ve tooAzure Active Directory bağlanma bulut tabanlı hizmetleri arasında ortak bir karma kimlik kullanıcılarla sağlayabilir.
* Yöneticiler, Uygulama kaynağı, aygıt ve kullanıcı kimliği, ağ konumu ve çok faktörlü kimlik doğrulaması göre koşullu erişim sağlayabilir.
* Kullanıcılar kendi ortak bir kimlik aracılığıyla Azure AD tooOffice 365, Intune, SaaS uygulamaları ve üçüncü taraf uygulamalar hesaplarında yararlanabilirsiniz.
* Geliştiriciler, uygulamaları içi Active Directory veya Azure içinde bulut tabanlı uygulamalar için tümleştirme hello ortak kimlik modeli yararlanan uygulamalar oluşturabilir

Merhaba aşağıdaki şekilde kimlik eşitleme işlemi üst düzey bir görünümünü örneği vardır.

![](./media/hybrid-id-design-considerations/identitysync.png)

Kimlik eşitleme işlemi

Aşağıdaki tablo toocompare hello eşitleme seçenekleri şu hello gözden geçirin:

| Eşitleme yönetim seçeneği | Avantajları | Olumsuz yönleri |
| --- | --- | --- |
| Eşitleme tabanlı (aracılığıyla, DirSync veya AADConnect) |Kullanıcılar ve gruplar şirket içi ve bulut eşitlendi <br>  **İlke denetimi**: Merhaba yönetici hello özelliği toomanage parola ilkeleri, iş istasyonu, kısıtlamalar, kilitleme denetimleri sağlar, Active Directory üzerinden ve tooperform ek kalmadan daha, hesap ilkeleri ayarlanabilir Görevler hello bulutta.  <br>  **Erişim denetimi**: hello Hizmetleri çevrimiçi sunucuları veya her ikisi de aracılığıyla hello şirket ortamında aracılığıyla erişilebilir böylece erişim toohello bulut hizmeti kısıtlayabilirsiniz. <br>  Destek aramaları azaltılmış: olasılığını tooforget oldukları kullanıcıların daha az parolaları tooremember varsa, bunları. <br>  Güvenliği: Kullanıcı kimlik bilgileri tüm hello sunucuları ve çoklu oturum açma içinde kullanılan hizmetler yönetilen çünkü korumalı ve şirket içi denetlenebilir. <br>  Güçlü kimlik doğrulaması için destek: hello bulut hizmetiyle güçlü kimlik doğrulaması (iki öğeli kimlik doğrulama olarak da bilinir) kullanabilirsiniz. Ancak, güçlü kimlik doğrulaması kullanırsanız, çoklu oturum açma kullanmanız gerekir. | |
| Federasyon tabanlı (aracılığıyla AD FS) |Güvenlik belirteci hizmeti (STS) tarafından etkinleştirilmiş. Bir Microsoft bulut hizmeti ile oturum açma bir STS tooprovide tek erişimi yapılandırdığınızda, şirket içi STS, Azure AD kiracınızda belirttiğiniz hello Federasyon etki alanı arasında federe güven oluşturma. <br> Son kullanıcıların aynı kimlik bilgilerini tooobtain erişim toomultiple kaynakları ayarlamak toouse hello sağlar <br>Son kullanıcılar toomaintain birden çok kimlik bilgileri kümesi yok. Henüz hello tooprovide kendi kimlik bilgilerini tooeach bir hello katılımcı kaynakları., kullanıcılar desteklenen B2B ve B2C senaryoları. |Dağıtım ve içi adanmış bakım için uzman personeli gerektirir AD FS sunucuları. Toouse AD FS için STS düşünüyorsanız, güçlü kimlik doğrulama hello kullanma kısıtlamaları vardır. Daha fazla bilgi için bkz: [AD FS 2.0 için Gelişmiş Seçenekleri yapılandırma](http://go.microsoft.com/fwlink/?linkid=235649). |

> [!NOTE]
> Daha fazla bilgi için [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).
> 
> 

## <a name="see-also"></a>Ayrıca Bkz.
[Tasarım konularına genel bakış](active-directory-hybrid-identity-design-considerations-overview.md)


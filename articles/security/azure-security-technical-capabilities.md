---
title: "aaaAzure güvenlik Teknik Özellikleri | Microsoft Docs"
description: "Geniş işlem örnekleri dahil bulut tabanlı bilgi işlem Hizmetleri & otomatik olarak toomeet hello ihtiyaçlarını uygulamanızı veya Kurumsal yukarı ve aşağı ölçeklenebilen hizmetleri hakkında bilgi edinin."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/26/2017
ms.author: TomSh
ms.openlocfilehash: a0ef17883be54dab4cb6b597204f3197dc05c28c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-technical-capabilities"></a>Azure güvenlik Teknik Özellikleri

tooassist geçerli ve gelecekteki Azure müşterilerine anlamak ve hello kullanma çeşitli güvenlikle ilgili özellikleri bulunan ve çevresindeki Azure platformu Merhaba, Microsoft teknik incelemeler, güvenlik genel bakışlar, en iyi yöntemler, bir dizi geliştirilen ve Denetim listeleri. Merhaba konuları avantajlarına ve derinliği bakımından aralığı ve düzenli aralıklarla güncelleştirilir. Bu belge serisi hello soyut aşağıdaki bölümde özetlendiği gibi bir parçasıdır. Bu Azure güvenlik seri hakkında daha fazla bilgi (URL'de) bulunabilir.

## <a name="azure-platform"></a>Azure platformu

[Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure/) bulut platformu altyapısı oluşur ve uygulama hizmetleriyle tümleşik Veri Hizmetleri gelişmiş analizler ve geliştirici araçları ve Hizmetleri, barındırılan içinde Microsoft'un genel bulut veri merkezleri. Müşteriler çok sayıda farklı kapasiteler ve senaryolarından temel bilgi işlem, ağ ve depolama, toomobile ve web uygulama hizmetleri, nesnelerin interneti gibi toofull bulut senaryosu için Azure kullanın ve açık kaynaklı teknolojilerle kullanılır ve karma dağıtılan Bulut veya bir müşterinin veri merkezi içinde barındırılan. Yapı taşları toohelp şirketler maliyet tasarrufu, hızlı bir şekilde yenilik ve sistemler proaktif olarak yönetirken azure bulut teknolojisi sağlar. Derleme ya da BT varlıklar tooa bulut sağlayıcısı geçirmek hello Hizmetleri ve bulut tabanlı varlıklarınızın toomanage hello güvenlik sağladıkları hello denetimleri ile veri ve uygulamaları, bir kuruluşun yeteneklerini tooprotect üzerinde bağlı.

Microsoft Azure güvenli, tutarlı bir uygulama platformu ve altyapı-bir hizmet olarak farklı bir bulut skillsets ve tümleşik verilerle proje karmaşıklık düzeyi dahilinde takımlar toowork için sunduğu hello yalnızca bulut bilgi işlem Sağlayıcısı'dır Hizmetleri ve, hem Microsoft hem de Microsoft olmayan platformlar mevcut olduğunda, veri'ten açığa analytics çerçeveler ve şirket içi de Azure bulut hizmetlerine içinde dağıtma ile bulut tümleştirme için seçim sağlayan araçlar açın Böylece, şirket içi veri merkezleri. Merhaba Microsoft güvenilir bulutun bir parçası olarak, müşteriler endüstri lideri güvenlik, güvenilirlik, uyumluluk, gizlilik ve hello büyük ağ kişiler, iş ortakları ve işlemler toosupport kuruluşların hello bulutta Azure üzerinde kullanır.

Microsoft Azure ile şunları yapabilirsiniz:

- Merhaba bulut ile yenilik hızlandırmak.

- Güç iş kararları & Öngörüler uygulamalarla.

- Ücretsiz olarak oluşturun ve her yerden dağıtın.

- İşlerini koruyun.

## <a name="scope"></a>Kapsam

Bu teknik Hello odak noktası işlemiyle ilgili güvenlik özellikleri ve işlevleri Microsoft Azure'nın temel bileşenleri, yani destekleyen [Microsoft Azure depolama](https://docs.microsoft.com/azure/storage/storage-introduction), [Microsoft Azure SQL veritabanları](https://docs.microsoft.com/azure/sql-database/), [Microsoft Azure'nın sanal makine modeli](https://docs.microsoft.com/azure/virtual-machines/  )ve hello araçları ve tüm yönetmek altyapı. Bu teknik incelemede müşteriler toofulfil Microsoft Azure teknik özellikler kullanılabilir tooyou hello güvenlik ve gizlilik verilerini koruma konusunda rolleri odaklanın.

Bu paylaşılan sorumluluk modelini anlama hello önemini toohello bulut taşıma müşteriler için gereklidir. Bulut sağlayıcıları için güvenlik ve uyumluluk çalışmalarını önemli avantajlar sunar, ancak bu avantajlar, kullanıcılar, uygulamaları ve hizmet teklifleri koruma gelen hello müşteri muaf olmasını değil.

Iaas çözümleri için hello müşteri sorumludur veya güvenli hale getirme ve hello işletim sistemi, ağ yapılandırması, uygulamalar, kimlik, istemciler ve verilerin yönetilmesi için paylaşılan bir sorumluluğa sahiptir.  Iaas dağıtımları PaaS çözümleri oluşturmak, hello müşteri hala sorumludur veya güvenli hale getirme ve uygulamalar, kimlik, istemciler ve verilerin yönetilmesi için paylaşılan bir sorumluluğa sahiptir. SaaS çözümleri, Nonetheless, hello müşteri toobe sorumlu devam eder. Bunlar veri doğru şekilde sınıflandırılır ve Sorumluluk toomanage, kullanıcılar ve son nokta cihazları paylaştıkları emin olmalısınız.

Bu belge herhangi bir hello ayrıntılı kapsamı sağlamaz ilgili Azure Web siteleri, Azure Active Directory, Hdınsight, Media Services ve hello çekirdek bileşenleri üzerinde katmanlanmış diğer hizmetler gibi Microsoft Azure platform bileşenleri. Genel bilgiler en düşük düzeyde bulunmakla okuyucular Microsoft tarafından sağlanan ve bu teknik yazıda sağlanan bağlantılar dahil diğer başvuruları açıklandığı gibi Azure temel kavramlarını varsayılır.


## <a name="available-security-technical-capabilities-toofulfil-user-customer-responsibility---big-picture"></a>Kullanılabilir güvenlik teknik özellikler toofulfil kullanıcı (müşteri) sorumluluk - büyük resmi

Microsoft Azure, müşterilere yardımcı olmak Hizmetleri hello güvenlik, gizlilik ve uyumluluk gereksinimlerini karşılayacak sağlar. Resim yardımcı olan çeşitli Azure hizmetlerine kullanılabilir kullanıcılar toobuild güvenli ve uyumlu uygulama altyapısı için sektör standartlarında açıklayan aşağıdaki hello.

![Kullanılabilir güvenlik teknik özellikleri büyük resmi](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig1.png)

## <a name="manage-and-control-identity-and-user-access-protect"></a>Yönetmek ve denetlemek kimlik ve kullanıcı erişimi (Koru)

Azure, toomanage kullanıcı kimlikleri ve kimlik bilgilerini ve Denetim erişim sağlayarak iş ve kişisel bilgilerinizin korunmasına yardımcı olur.

### <a name="azure-active-directory"></a>Azure active directory

Microsoft kimlik ve erişim yönetimi çözümlerini Yardım BT erişim tooapplications ve kaynakları hello kurumsal veri merkezi genelinde ve hello buluta doğrulama çok faktörlü kimlik doğrulama ve koşullu gibi ek düzeylerini etkinleştirme koruma erişim ilkeleri. Raporlama, Denetim ve yardımcı olası güvenlik sorunlarını azaltmak uyarı Gelişmiş Güvenlik ile izleme şüpheli etkinlik. [Azure Active Directory Premium](https://docs.microsoft.com/azure/active-directory/active-directory-editions) bulut (SaaS) uygulamaların ve şirket içi çalıştırdığınız erişim tooweb uygulamaların tek oturum açma toothousands sağlar.

Güvenlik, Azure Active Directory (AD) hello yeteneği yararları:

- Oluşturun ve her kullanıcı için tek bir kimliği kullanıcıları, grupları ve aygıtları eşitlenmiş şekilde kalmasının karma kuruluşunuz yönetin.

- Çoklu oturum açma erişimini SaaS uygulamaları önceden tümleştirilmiş binlerce de dahil olmak üzere tooyour uygulamaları sağlar.

- Uygulama erişimi güvenliğini kural tabanlı çok faktörlü kimlik doğrulamasını hem şirket içi zorlayarak etkinleştirmek ve bulut uygulamalarında.

- Sağlama güvenli uzaktan erişim tooon içi web uygulamaları Azure AD uygulama proxy'si aracılığıyla.

[Azure active directory portalında](http://aad.portal.azure.com/) kullanılabilir azure portalında bir parçası. Bu panodan, kuruluşunuzun hello durumu özetini almak ve kolayca hello dizini, kullanıcılar ya da uygulama erişimini yönetme içine daha yakından inceleyin.

![Azure active directory](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig2.png)

Aşağıdaki çekirdek Azure kimlik yönetimi özellikleri:

- Çoklu oturum açma

- Multi-factor authentication

- Güvenlik İzleme, uyarılar ve makine öğrenme tabanlı raporlar

- Tüketici kimliği ve erişim yönetimi

- Cihaz kaydı

- Ayrıcalıklı Kimlik Yönetimi

- Kimlik koruması

#### <a name="single-sign-on"></a>Çoklu oturum açma

[Çoklu oturum açma (SSO)](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) mümkün tooaccess olan tüm hello uygulamaları ve yalnızca bir kez tek bir kullanıcı hesabı kullanarak oturum açma tarafından toodo iş ihtiyacınız kaynakları anlamına gelir. Oturum açtıktan sonra ihtiyaç gerekli tooauthenticate olmadan tüm hello uygulamalara erişmek için (örneğin, bir parola yazın) ikinci kez.

Birçok kuruluş yazılım son kullanıcının üretkenliği için Office 365, kutusunu ve Salesforce gibi bir hizmet (SaaS) uygulamaları olarak kullanır. Tarihsel olarak, BT personeli gerekli tooindividually oluşturun ve her SaaS uygulamasının kullanıcı hesaplarında güncelleştirin ve kullanıcıların her SaaS uygulaması için bir parola tooremember gerekiyordu.

[Azure AD şirket içi Active Directory hello bulutunu genişletir](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis), kuruluş kendi birincil kullanıcıları toouse etkinleştirme toonot yalnızca oturum açma tootheir etki alanına katılmış aygıtlar ve şirket kaynaklarına hesap, ancak aynı zamanda tüm web ve SaaS uygulamaları hello işlerini için gerekli.

Yalnızca kullanıcıların birden çok kullanıcı adları ve parolalar kümesini toomanage sahip değilse, uygulama erişimini otomatik olarak sağlanan veya XML'deki sağlanan dayalı olarak kuruluş grupları ve durumlarını çalışan olarak olabilir. [Azure AD güvenlik ve erişim yönetimi denetimleri tanıtır](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) sağlamak toocentrally SaaS uygulamalarında kullanıcıların erişimini yönetin.

#### <a name="multi-factor-authentication"></a>Multi-factor authentication

[Azure çok faktörlü kimlik doğrulaması (MFA)](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) hello birden fazla doğrulama yöntemi kullanılmasını gerektiren ve güvenlik toouser oturum açmalarına ve işlemlerine önemli bir ikinci katmanı ekleyen kimlik doğrulama yöntemidir. [MFA koruma sağlanmasına yardımcı olan](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-how-it-works) erişim toodata ve uygulamaları basit bir oturum açma işlemi için kullanıcı talebine buluştururken. Güçlü kimlik doğrulama seçeneklerini çeşitli aracılığıyla sunar — telefon araması, SMS mesajı veya mobil uygulama bildirimi veya doğrulama kodu ve üçüncü taraf OAuth belirteçleri.

#### <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Güvenlik İzleme, uyarılar ve makine öğrenme tabanlı raporlar

Güvenlik İzleme ve uyarılar ve tutarsız erişim desenlerini tanımlamak makine öğrenme tabanlı raporlar, işinizin korunmasına yardımcı olabilir. Azure Active Directory'nin erişim ve kullanım raporları toogain görünürlük hello bütünlüğü ve güvenlik kuruluşunuzun dizininin kullanabilirsiniz. Bu bilgileri kullanarak bir dizin yönetici böylece bunlar yeterli bu riskleri toomitigate planlayabilirsiniz olası güvenlik riskleri burada bulunan daha iyi belirleyebilirsiniz.

Merhaba Klasik Azure portalı veya aracılığıyla [Azure Active directory portalında](http://aad.portal.azure.com/), [raporları](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) hello yolları aşağıdaki kategorilere ayrılır:

- Anomali raporları – oturum açma olayları toobe anormal bulduk olduğunu içerir. Amacımız toomake olduğundan, bu tür etkinliğini kullanan ve bir olay şüpheli olup olmadığına dair toobe mümkün toodecide etkinleştirin.

- Tümleşik uygulama raporları – bulut uygulamalarını, kuruluşunuzda nasıl kullanıldığını içine Öngörüler sağlar. Azure Active Directory bulut uygulamalarını binlerce ile tümleştirme sağlar.

- Hata raporlarını – hesapları tooexternal uygulamaları sağlamada oluşabilecek hatalar gösterir.

- Kullanıcıya özgü raporları – belirli bir kullanıcı için etkinlik verilerdeki aygıt/oturum görüntüler.

- Etkinlik günlükleri – son 24 saat hello içindeki tüm Denetlenen olayları kaydını içermediğinden, son 7 gün veya son 30 gün ve Grup etkinlik değişikliklerini ve parola sıfırlama ve kayıt etkinliği.

#### <a name="consumer-identity-and-access-management"></a>Tüketici kimliği ve erişim yönetimi

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) toohundreds kimlikleri milyonlarca ölçeklendirilebilen bir yüksek oranda kullanılabilir, genel Identity management hizmeti tüketiciye yönelik uygulamalar için. Bu hizmet mobil platformlar ve web platformlarıyla tümleştirilebilir. Tüketicileriniz üzerinde tooall uygulamalarınızı özelleştirilebilir deneyimler aracılığıyla var olan sosyal hesaplarını kullanarak veya yeni kimlik bilgileri oluşturarak oturum açabilir.

Geçmiş, çok isteyen uygulama geliştiricileri hello içinde[kaydolun ve tüketici oturumlarını](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview) uygulamalarına kendi kodlarını yazardı. Ve şirket içi veritabanlarını veya sistemleri toostore kullanıcı adları ve parolalar kullandığı. Azure Active Directory B2C, kuruluşunuzun bir daha iyi şekilde toointegrate tüketici kimlik yönetimini uygulamalarına hello Yardım güvenli, standartlara dayalı bir platform ve bir büyük Genişletilebilir ilke kümesi sunar.

Azure Active Directory B2C kullandığınızda tüketicileriniz uygulamalarınız için var olan sosyal hesaplarını (Facebook, Google, Amazon, LinkedIn) kullanarak veya yeni kimlik bilgileri (e-posta adresi ve parola veya kullanıcı adı ve parola) oluşturarak kaydolabilir.

Cihaz kaydı

[Azure AD cihaz kaydı](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) hello temelidir aygıt tabanlı [koşullu erişim](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) senaryoları. Bir cihaz kaydedildiğinde Azure Active Directory cihaz kaydı hello kullanıcı oturum açtığında kullanılan tooauthenticate hello aygıt olan bir kimliğe sahip hello cihazı sağlar. Kimliği doğrulanmış hello cihaz ve hello cihazın hello öznitelikleri hello bulutta ve şirket içi barındırılan uygulamalar için kullanılan tooenforce koşullu erişim ilkeleri olabilir.

İle birlikte kullanıldığında bir [mobil cihaz Yönetimi (MDM)](https://www.microsoft.com/itshowcase/Article/Content/588/Mobile-device-management-at-Microsoft) Intune, Azure Active Directory'de hello cihaz öznitelikleri gibi çözüm hello cihaz hakkındaki ek bilgilerle güncelleştirilir. Bu, cihazları toomeet erişimden zorunlu toocreate koşullu erişim kuralları, güvenlik ve uyumluluğa yönelik standartlarınızı sağlar.

#### <a name="privileged-identity-management"></a>Ayrıcalıklı Kimlik Yönetimi

[Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) yönetmenize, denetlemenize ve ayrıcalıklı kimliklerinizi izlemek ve tooresources Azure AD'de de gibi diğer Microsoft online services Office 365 veya Microsoft Intune gibi erişim sağlar.

Bazen kullanıcıların Azure veya Office 365 kaynakları veya diğer SaaS uygulamaları ayrıcalıklı işlemleri çıkışı toocarry gerekir. Bu, genellikle kuruluşlar sahip toogive anlamına bunları kalıcı ayrıcalıklı erişim Azure AD'de. Kuruluşlar, yeterince yönetici ayrıcalıklarını bu kullanıcıların ne yaptıklarını izleyemez bulutta barındırılan kaynaklar için büyüyen bir güvenlik riski olmasıdır. Ayrıca, ayrıcalıklı erişimi olan bir kullanıcı hesabı ihlal edilmesi durumunda, bir ihlali, genel bulutun güvenlik etkileyebilir. Azure AD Privileged Identity Management tooresolve bu riski yardımcı olur.

Azure AD Privileged Identity Management sağlar:

- Hangi kullanıcıların Azure AD admins olduğuna bakın

- İsteğe bağlı, "Office 365 ve Intune yönetim erişimi tooMicrosoft çevrimiçi hizmetler gibi tam zamanında" etkinleştirme

- Yönetici erişim geçmişine ve değişiklikler hakkında raporlar yönetici atamaları alma

- Erişim tooa ayrıcalıklı rol hakkında uyarı alın

#### <a name="identity-protection"></a>Kimlik koruması

[Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) , birleştirilmiş görünüme risk olaylarına ve olası güvenlik açıklarını kuruluşunuzdaki kimlikleri etkileyen sağlayan bir güvenlik hizmetidir. Kimlik koruma, var olan Azure Active Directory'nin anomali algılama özellikleri (Azure AD anormal etkinlik raporları kullanılabilir) kullanır ve anormallikleri gerçek zamanlı olarak algılayabilir yeni risk olayı türleri sunar.

## <a name="secured-resource-access-in-azure"></a>Azure'da güvenli kaynak erişimi

Azure erişim denetimi faturalandırma açısından başlatır. Merhaba hello ziyaret ederek erişilen bir Azure hesabı sahibinin [Azure hesaplar Merkezi](https://account.windowsazure.com/subscriptions), hello Hesap Yöneticisi (AA) değil. Abonelik faturalama için bir kapsayıcı olsa da, bunlar aynı zamanda bir güvenlik sınırı hareket: her abonelik bir Hizmet Yöneticisi (kimin eklemek, kaldırmak ve bu abonelik Azure kaynaklarında hello kullanarak değiştirme SA) sahip [Klasik Azure portalı](https://manage.windowsazure.com/). Yeni bir abonelik Hello varsayılan SA, hello AA olmakla birlikte hello AA hello SA'hello Azure hesaplar merkezi değiştirebilirsiniz.

![Azure'da güvenli kaynak erişimi](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig3.png)

Abonelikler, bir dizin ile bir ilişkilendirme de vardır. Merhaba dizin, bir kullanıcı kümesini tanımlar. Bu kullanıcıları hello iş veya hello dizin oluşturulmuş okul veya dış kullanıcıların (yani, Microsoft Accounts) olabilir. Abonelikler, bir alt kümesini Hizmet Yöneticisi (SA) veya ortak yönetici (CA) olarak atanmış olan dizin kullanıcılar tarafından erişilebilir; Merhaba yalnızca eski nedeniyle, Microsoft Accounts (eskiden Windows Live kimliği) SA veya CA hello dizinde bulunduğundan olmadan atanabilir, istisnadır.

Güvenlik odaklı şirketler çalışanlar gereksinim duydukları hello tam izinleri vermiş odaklanmanız gerekir. Çok fazla izinleri bir hesap tooattackers getirebilir. Çok az izinleri çalışanlar verimli bir şekilde işlerini alınamıyor anlamına gelir. [Azure rol tabanlı erişim denetimi (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) yardımcı olur, Azure için ayrıntılı erişim yönetimi sunarak bu sorunu gidermek.

![Güvenli kaynak erişimi ](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig4.png)

RBAC kullanarak, ekibiniz içinde görevleri kurabilmeleri ve tooperform işlerini gereksinim yalnızca hello miktarını erişim toousers verin. Kısıtlanmamış izinlerini herkes vermek yerine, Azure aboneliği veya kaynakları yalnızca belirli eylemleri izin verebilirsiniz. Örneğin, kullanım RBAC toolet bir çalışan bir Abonelikteki sanal makineleri yönetmek için başka yönetebilirsiniz sırada SQL hello içinde aynı veritabanları abonelik.

![Azure(RBAC) içinde güvenli kaynak erişimi](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig5.png)

## <a name="azure-data-security-and-encryption-protect"></a>Azure veri güvenliği ve şifreleme (koruma)

Hello anahtarları toodata koruma hello bulutta birini hello olası durumlar verilerinizi ortaya çıkabilecek ve bu durum için hangi denetimlerin kullanılabilir hesap. Azure veri güvenliği ve şifreleme için en iyi uygulama hello önerilerini verilerinin durumları aşağıdaki hello olabilir.

- : Çalışmıyorken Bu depolama nesneleri, kapsayıcıları ve statik olarak fiziksel medyada mevcut türleri manyetik veya optik disk olması tüm bilgileri içerir.

- Aktarım sırasında: Ne zaman veri aktarılmakta olan bileşenleri, konumlara veya programları arasında gibi hello ağ üzerinden bir hizmet veri yolundan (şirket içi toocloud ve ExpressRoute gibi karma bağlantılar dahil olmak üzere tersi,) üzerinden veya bir giriş/çıkış sırasında işlem, bu düşündüğünüz olarak hareket halinde.

### <a name="encryption--rest"></a>Rest @ şifreleme

Bekleyen şifreleme her hello aşağıdaki tooachieve:

En az bir tablo tooencrypt verileri aşağıdaki hello ayrıntılı şifreleme modelleri önerilen hello destekler.

| Şifreleme modeli |  |  |  |
| ----------------  | ----------------- | ----------------- | --------------- |
| Sunucu şifreleme | Sunucu şifreleme | Sunucu şifreleme | İstemci şifreleme
| Sunucu tarafı şifreleme hizmeti yönetilen anahtarları kullanma | Azure anahtar kasası Customer-Managed tuşlarını kullanarak sunucu tarafı şifreleme | Şirket içi müşteri kullanarak sunucu tarafı şifreleme anahtarları yönetilen |
| • Azure kaynak sağlayıcıları hello şifreleme ve şifre çözme işlemi gerçekleştirir <br> • Microsoft hello anahtarları yönetir <br>• Tam bulut işlevi | • Azure kaynak sağlayıcıları hello şifreleme ve şifre çözme işlemi gerçekleştirir<br>• Müşteri anahtarları Azure anahtar kasası aracılığıyla denetler<br>• Tam bulut işlevi | • Azure kaynak sağlayıcıları hello şifreleme ve şifre çözme işlemi gerçekleştirir <br>• Müşteri anahtarları şirket içi denetler <br> • Tam bulut işlevi| • Azure Hizmetleri şifresi çözülmüş verileri göremezsiniz <br>• Müşterilerin anahtarlarını şirket içi tutun (veya diğer depoları güvenli). Anahtarları kullanılabilir tooAzure Hizmetleri olup olmadığı <br>• Azaltılmış bulut işlevi|

### <a name="enabling-encryption-at-rest"></a>Bekleyen şifreleme etkinleştirme

**Tüm konumlarını depoları verilerinizi belirle**

Bekleyen şifreleme Hello amacı tooencrypt tüm verilerdir. Bunun yapılması, önemli veri ya da tüm kalıcı konumları eksik hello olasılığını ortadan kaldırır. Uygulamanız tarafından depolanan tüm verileri sıralar. 

> [!Note] 
> Yalnızca "uygulama verileri" veya "PII' ancak meta veriler (abonelik eşlemeleri, sözleşme bilgileri PII) tooapplication dahil olmak üzere ilgili herhangi bir veri hesap.

Ne depolar göz önünde bulundurun toostore veri kullanıyor. Örneğin:

- Harici depolama (örneğin, SQL Azure, belge DB, Hdınsights, Data Lake, vb.)

- Geçici depolama (Kiracı verileri içeren tüm yerel önbelleği)

- Bellek içi önbellek (Merhaba sayfa dosyasına konmuş.)

### <a name="leverage-hello-existing-encryption-at-rest-support-in-azure"></a>Rest destek azure'da Hello varolan şifreleme yararlanın

Kullandığınız her deposu için şifreleme Rest destek varolan hello yararlanın.

- Azure Storage: Bkz [bekleyen veri için Azure Storage hizmeti şifreleme](https://docs.microsoft.com/azure/storage/storage-service-encryption),

- SQL Azure: Bkz [saydam veri şifreleme (TDE), her zaman şifreli SQL](https://msdn.microsoft.com/library/mt163865.aspx)

- VM & yerel disk depolama ([Azure Disk şifrelemesi](https://docs.microsoft.com/azure/security/azure-security-disk-encryption))

VM ve yerel disk depolama için Azure Disk şifrelemesi kullanan desteklendiği yerlerde:

IaaS

Iaas VM'ler (Windows veya Linux) hizmetleriyle kullanması gereken [Azure Disk şifrelemesi](https://microsoft.sharepoint.com/teams/AzureSecurityCompliance/Security/SitePages/Azure%20Disk%20Encryption.aspx) müşteri verilerini içeren tooencrypt birimler.

PaaS v2

Çalışan hizmetleri üzerinde PaaS v2 Service Fabric kullanarak Azure disk şifrelemesi için sanal makine ölçek kümesi [VMSS] tooencrypt PaaS v2 Vm'leri kullanabilirsiniz.

PaaS v1

Azure Disk şifrelemesi PaaS v1 üzerinde şu anda desteklenmiyor. Bu nedenle, uygulama düzeyinde kullanmalısınız şifreleme tooencrypt kalıcı veri şifrelenir.  Bu, içerir, ancak uygulama verilerini, geçici dosyaları, günlükler ve kilitlenme bilgi dökümleri için sınırlı değildir.

Çoğu Hizmetleri tooleverage hello şifreleme bir depolama kaynak sağlayıcısı denemeniz gerekir. Bazı hizmetler toodo açık şifreleme vardır, örneğin, herhangi bir anahtar malzemesi kalıcı (Sertifikalar, kök / ana anahtarları) anahtar kasasında depolanan gerekir.

Hizmet tarafı şifreleme müşteri tarafından yönetilen anahtarlarla destekliyorsa toobe şekilde hello müşteri tooget hello anahtarı için toous gerekir. Hello desteklenir ve yol toodo Azure anahtar kasası (AKV) ile tümleştirerek olan önerilir. Bu durumda müşteriler ekleyin ve bunların anahtarları Azure anahtar Kasası'yönetin. Bir müşteri öğrenebilirsiniz nasıl toouse AKV aracılığıyla [anahtar kasası ile çalışmaya başlama](http://go.microsoft.com/fwlink/?linkid=521402).

Azure anahtar kasası ile toointegrate, şifre çözme için gerektiğinde AKV gelen kod toorequest bir anahtar eklersiniz.

- Bkz: [Azure anahtar kasası – adım adım](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) nasıl ilişkin bilgi için AKV ile toointegrate.

Yönetilen müşteri anahtarları destekliyorsa, tooprovide bir UX hangi anahtar kasası (veya anahtar kasası URI) toouse hello müşteri toospecify için gerekir.

Konak, altyapı ve Kiracı verilerin şifrelenmesi hello bekleyen şifreleme içerir gibi hello kaybı son toosystem hatası veya kötü amaçlı etkinliği hello anahtarların hello şifrelenmiş verilerin tümü kaybolur anlamına gelir. Bu nedenle, Rest çözüm, şifreleme dayanıklı toosystem hataları ve kötü amaçlı etkinliği Öykü kapsamlı olağanüstü durum kurtarma olan kritik önem taşır.

Bekleyen şifreleme uygulayan genellikle hala uygulanmadıkça toohello şifreleme anahtarları hizmetlerdir veya bırakılıyor veri sürücüsünde hello ana bilgisayar (örneğin, başlangıç sayfa dosyası hello ana bilgisayarın OS.) şifrelenmemiş Bu nedenle, hizmetleri, hizmetlerini hello konak birimi şifrelenir emin olmalısınız. toofacilitate bu işlem takım kullandığı ana şifreleme hello dağıtımını etkinleştirilmiş [Bitlocker](https://technet.microsoft.com/library/dn306081.aspx) NKP ve uzantıları toohello DCM hizmeti ve aracı tooencrypt hello konak birimi.

Çoğu hizmetler standart Azure Vm'lerinde uygulanır. Bu tür hizmetlerin almalısınız [ana şifreleme](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) otomatik olarak zaman işlem etkinleştirir. İşlem içinde çalışan hizmetler için yönetilen kümeleri ana şifreleme Windows Server 2016 toplu olarak otomatik olarak etkinleştirilir.

### <a name="encryption-in-transit"></a>Şifreleme aktarım sırasında

Aktarımdaki verileri koruma temel veri koruma stratejinizin parçası olmalıdır. Verileri geri ve İleri birçok konumlardan geçtiğinden hello genel SSL/TLS protokolleri tooexchange verileri her zaman farklı konumlar arasında kullanmanız önerilir. Bazı durumlarda, şirket içi ve bulut arasındaki tooisolate hello tüm iletişim kanalını isteyebilirsiniz sanal özel ağ (VPN) kullanarak altyapı.

Şirket içi altyapınızı ve Azure arasında taşıma verileri için HTTPS veya VPN gibi uygun güvenlik önlemleri göz önünde bulundurmalısınız.

Birden çok iş istasyonları şirket içi tooAzure toosecure erişimden gereken kuruluşlar için kullanmak [Azure siteden siteye VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Bir iş istasyonundan toosecure erişmeniz kuruluşlar için şirket içi tooAzure, kullanım bulunan [noktası siteye VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Büyük veri kümeleri taşınabilir ayrılmış bir yüksek hızlı WAN bağlantısı üzerinden gibi [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Toouse ExpressRoute seçerseniz, ayrıca uygulama düzeyi hello kullanarak hello verileri şifreleyebilir [SSL/TLS](https://support.microsoft.com/kb/257591) veya diğer protokoller için ek koruma.

Hello Azure portalı Azure Storage ile etkileşim, tüm işlemleri HTTPS oluşur. [Storage REST API'sini](https://msdn.microsoft.com/library/azure/dd179355.aspx) HTTPS üzerinden de ile kullanılan toointeract olabilir [Azure Storage](https://azure.microsoft.com/services/storage/) ve [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/).

Aktarım tooprotect verileri başarısız kuruluşlar için daha açıktır [man-in--middle saldırıları](https://technet.microsoft.com/library/gg195821.aspx), [gizli dinleme](https://technet.microsoft.com/library/gg195641.aspx)ve oturumu ele geçirme. Bu saldırıların erişim tooconfidential veri sağlamasını hello ilk adımı olabilir.

Merhaba makale okuyarak Azure VPN seçeneği hakkında daha fazla bilgiyi [planlama ve tasarım VPN ağ geçidi için](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design).

### <a name="enforce-file-level-data-encryption"></a>Dosya düzeyinde veri şifrelemeyi zorunlu kılma

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) kullandığı şifreleme, kimlik ve yetkilendirme ilkeleri toohelp güvenli dosyalarınızın ve e-posta. Azure RMS birden çok cihazda çalışır — telefonları, Tablet ve PC'leri hem kuruluşunuz içinde hem de kuruluşunuz dışındaki koruma tarafından. Azure RMS bile, kuruluşunuzun sınırları dışına çıktığında hello veriler devam koruma düzeyini eklediğinden bu olası bir yetenektir.

Azure RMS tooprotect dosyalarınızı kullandığınızda, endüstri standardı şifreleme ile tam destek kullanmakta olduğunuz [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Veri koruma için Azure RMS yararlanan, hello denetimi altında olmayan kopyalanan toostorage olsa bile hello koruma hello dosyayla kalır hello güvence sahip bir bulut depolama hizmeti gibi BT'nin. Merhaba aynı e-posta ile paylaşılan dosyaları için gerçekleşir, hello dosya eki tooan e-posta eki olarak korunur, yönergelerle ek nasıl tooopen hello korumalı.
Azure RMS benimseme için planlama yaparken hello şunları öneririz:

- Merhaba yüklemek [RMS sharing uygulaması](https://technet.microsoft.com/library/dn339006.aspx). Bu uygulama tarafından bir Office Eklentisi-kullanıcıların kolayca dosyaları doğrudan koruyabilmeniz için Office uygulamalarıyla ile tümleşir.

- Uygulamaları ve Hizmetleri toosupport Azure RMS yapılandırma

- Oluşturma [özel şablonlar](https://technet.microsoft.com/library/dn642472.aspx) iş gereksinimlerinizi yansıtır. Örneğin: tüm üst gizliliği uygulanması gereken üst gizli veriler için bir şablon ilgili e-postaları.

Üzerinde zayıf kuruluşlar [veri sınıflandırması](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) ve dosya koruması daha açıktır. toodata sızıntısı olabilir. Uygun dosya koruma, kuruluşların iş öngörüleri, uygunsuz kullanım izleme mümkün tooobtain olmalı ve kötü amaçlı erişime toofiles önlemek olmaz.

> [!Note]
> Merhaba makale okuyarak Azure RMS hakkında daha fazla bilgiyi [Azure Rights Management ile çalışmaya başlama](https://technet.microsoft.com/library/jj585016.aspx).

## <a name="secure-your-application-protect"></a>Uygulamanızı güvenlik altına (koruma)
Azure hello altyapı ve uygulamanızın üzerinde çalıştığı platform güvenliğini sağlamak için sorumlu olsa da, sorumluluk toosecure olduğundan, uygulamanızın. Toodevelop, gereken diğer bir deyişle, dağıtma ve uygulama kodu ve içerik güvenli bir şekilde yönetme. Bu, uygulama kodu veya içeriği hala savunmasız toothreats olabilir.

### <a name="web-application-firewall-waf"></a>Web uygulaması güvenlik duvarı (WAF)
[Web uygulaması Güvenlik Duvarı (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) özelliğidir [uygulama ağ geçidi](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) web uygulamalarınızdan ortak açığından yararlanma girişimi ve güvenlik açıkları merkezi korunmasını sağlar.

Web uygulaması güvenlik duvarı kuralları hello temel [OWASP çekirdek kural kümeleri](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 veya 2.2.9. Web uygulamaları, bilinen yaygın güvenlik açıklarından yararlanan kötü amaçlı saldırıların giderek daha fazla hedefi olmaktadır. SQL ekleme saldırıları bu açıkları arasında ortak olan, siteler arası komut dosyası tooname birkaç saldırıları. Uygulama kodundaki böyle saldırılarını önleme zor olabilir ve düzeltme eki uygulama ve hello uygulama topolojisinin birden çok katmanına izleme sıkı bakımını gerektirebilir. Bir merkezi web uygulaması Güvenlik Duvarı güvenlik yönetimi daha kolay hale getirir ve tooapplication Yöneticiler tehditleri veya yetkisiz erişimlere karşı daha iyi güvence verir. WAF Çözüm Merkezi bir konumda her tek tek web uygulamalarının güvenliğini sağlama karşı bilinen bir güvenlik açığı düzeltme eki uygulama tarafından tooa güvenlik tehdidi daha hızlı ayrıca tepki. Mevcut uygulama ağ geçitleri dönüştürülmüş tooa web uygulaması Güvenlik Duvarı etkin uygulama ağ geçidi kolayca olabilir.

Hangi web uygulaması güvenlik duvarı korur hello ortak web güvenlik açıkları bazıları içerir:

- SQL ekleme koruması

- Siteler arası komut dosyası koruması

- Komut ekleme, HTTP isteği kaçakçılığı, HTTP yanıtı bölme ve uzak dosya ekleme saldırıcı gibi Yaygın Web Saldırıları Koruması

- HTTP protokolü ihlallerine karşı koruma

- Eksik konak kullanıcısı-aracısı ve kabul üst bilgileri gibi HTTP protokolü anormalliklerine karşı koruma

- Robotlar, gezginler ve tarayıcıları önleme

- Ortak uygulama yapılandırma hataları (diğer bir deyişle, Apache, IIS, vb.) algılanması

> [!Note]
> Kuralları daha ayrıntılı bir listesi ve bunların korumaları hello aşağıdaki görmek için [çekirdek kural kümeleri](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview#core-rule-sets):

Azure de birkaç kullanımı kolay özellikleri toohelp sağlar, uygulamanız için hem gelen hem de giden trafiği güvenli. Azure de dışarıdan sağlayarak müşteriler kendi uygulama kodu güvenli yardımcı işlevselliği tooscan web uygulamanız güvenlik açıkları için sağlanır.

- [Kimlik doğrulama ve yetkilendirme çeşitli yollardan web uygulamanızın güvenliğini sağlayın](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization)

    - [Uygulamanız için Azure Active Directory kimlik doğrulaması kurulumu](https://azure.microsoft.com/blog/azure-websites-authentication-authorization/)


- [Aktarım Katmanı Güvenliği (TLS/SSL) - HTTPS etkinleştirerek trafiği tooyour uygulama güvenli](https://docs.microsoft.com/azure/app-service-web/web-sites-configure-ssl-certificate)

    - [Tüm gelen trafiği HTTPS bağlantısı üzerinden zorla](http://microsoftazurewebsitescheatsheet.info/)

  - [Katı taşıma güvenliği (HSTS) etkinleştir](http://microsoftazurewebsitescheatsheet.info/#enable-http-strict-transport-security-hsts)


- [İstemcinin IP adresine göre erişim tooyour uygulama kısıtlama](http://microsoftazurewebsitescheatsheet.info/#filtering-traffic-by-ip)

- [İstemcinin davranıştan - istek sıklığı ve eşzamanlılık erişim tooyour uygulama kısıtlama](http://microsoftazurewebsitescheatsheet.info/#dynamic-ip-restrictions)

- [Web uygulaması kodunuza Tinfoil Security Scanning kullanarak güvenlik açıkları için tarama](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)

- [TLS karşılıklı kimlik doğrulaması toorequire istemci sertifikaları tooconnect tooyour web uygulamasını yapılandırma](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth)

- [Uygulama toosecurely kullanımdan bağlanmak için tooexternal kaynakları bir istemci sertifikası yapılandırma](https://azure.microsoft.com/blog/using-certificates-in-azure-websites-applications/)

- [Uygulamanızı sağlayan standart sunucu üstbilgileri tooavoid Araçları Kaldır](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)

- [Uygulamanızı noktadan siteye VPN kullanarak özel bir ağdaki kaynaklara güvenli bir şekilde bağlanın](https://docs.microsoft.com/azure/app-service-web/web-sites-integrate-with-vnet)

- [Uygulamanızı karma bağlantılar kullanarak özel bir ağdaki kaynaklara güvenli bir şekilde bağlanın](https://docs.microsoft.com/azure/app-service-web/web-sites-hybrid-connection-get-started)

Azure uygulama hizmeti kullanan Azure Cloud Services ve sanal makineler tarafından kullanılan aynı kötü amaçlı yazılımdan koruma çözümünü hello. Bu hakkında daha fazla toolearn başvuran tooour [kötü amaçlı yazılımdan koruma belgelerine](https://docs.microsoft.com/azure/security/azure-security-antimalware).

## <a name="secure-your-network-protect"></a>Ağınızın güvenliğini sağlamaya (koruma)
Microsoft Azure, uygulama ve hizmet bağlantı gereksinimleri sağlam bir ağ altyapısı toosupport içerir. Azure'da, şirket içi arasında bulunan kaynaklar arasındaki ağ bağlantısı mümkündür ve Azure kaynakları ve hello Internet gelen tooand ve Azure barındırılır.

Merhaba [Azure ağ altyapısı](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) etkinleştirir, toosecurely bağlanmak tooeach Azure kaynakları ile diğer [sanal ağlar (Vnet'ler)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Bir VNet kendi ağ hello bulutta gösterimidir. VNet mantıksal ayırma hello Azure bulut ayrılmış ağ tooyour aboneliğin ' dir. Sanal ağlar tooyour şirket içi ağlara bağlanabilir.

![Ağınızın güvenliğini sağlamaya (koruma)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig6.png)

Temel ağ düzeyinde erişim denetimi (IP adresi ve hello TCP veya UDP protokollerini temel alan) ihtiyacınız sonra kullanabileceğiniz [ağ güvenlik grupları](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg). Ağ güvenlik grubu (NSG) temel bir durum bilgisi olan paket güvenlik duvarı filtreleme olduğundan ve temel toocontrol erişim bir [5-tanımlama grubu](https://www.techopedia.com/definition/28190/5-tuple).

Azure ağı hello özelliği toocustomize hello yönlendirme davranışı, Azure sanal ağlarda ağ trafiğini destekler. Bunu yapılandırarak yapmak [kullanıcı tanımlı rotaları](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) azure'da.

[Zorlanan tünel](https://www.petri.com/azure-forced-tunneling) olan hizmetlerinizi olmayan tooensure kullanabileceğiniz bir mekanizma hello Internet üzerinde bir bağlantı toodevices tooinitiate izin.

Azure destekler, WAN bağlantısının bağlantı tooyour şirket içi ağ ve bir Azure sanal ağı ile ayrılmış [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). Azure ile siteniz arasında Hello bağlantısını kullanan hello geçmez adanmış bir bağlantı genel Internet. Azure uygulamanız birden çok veri merkezlerinde çalıştığından, kullanabileceğiniz [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) kullanıcıların akıllıca hello uygulama örnekleri arasında tooroute isteklerini. Ayrıca Internet hello erişilebilir olup olmadığını Azure üzerinde çalışmayan trafiği tooservices yönlendirebilirsiniz.

## <a name="virtual-machine-security-protect"></a>Sanal makine güvenliği (koruma)

[Azure sanal makineleri](https://docs.microsoft.com/azure/virtual-machines/) çözümleri Çevik bir şekilde bilgi işlem çok çeşitli dağıtmanıza olanak tanır. Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP ve Azure BizTalk Hizmetleri desteği sayesinde, istediğiniz iş yükünü istediğiniz dilde ve neredeyse tüm işletim sistemlerinde dağıtabilirsiniz.

Azure ile kullandığınız [kötü amaçlı yazılımdan koruma yazılımı](https://docs.microsoft.com/azure/security/azure-security-antimalware) Microsoft, Symantec, eğilim mikro ve Kaspersky tooprotect gibi güvenlik satıcılardan sanal makinelerinizi kötü amaçlı dosyalar, reklam ve diğer tehditlere.

Azure Cloud Services ve sanal makineleri için Microsoft Antimalware tanımlamak ve virüsler, casus yazılım ve diğer kötü amaçlı yazılım kaldırma yardımcı olan gerçek zamanlı koruma bir özelliktir. Microsoft Antimalware bilinen kötü amaçlı veya istenmeyen yazılım girişimleri tooinstall kendisini veya Azure sistemlerinize çalıştırdığınızda yapılandırılabilir uyarılar sağlar.

[Azure yedekleme](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) sıfır sermaye yatırımı ve en az uygulama verilerinizi korur ölçeklenebilir bir çözüm işletim maliyetlerini. Uygulama hataları verilerinizi bozabilir ve insan hataları, uygulamalarınızda hatalar oluşturabilir. Azure Backup ile Windows ve Linux çalıştıran sanal makinelerinizi korunur.

[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) yardımcı olur, çoğaltma, yük devretme ve kurtarma iş yükleri ve uygulamalar, birincil konumunuzun çökmesi durumunda ikincil konum kullanılabilir; böylece düzenlemek.

## <a name="ensure-compliance-cloud-services-due-diligence-checklist-protect"></a>Uyumluluk sağlamak: Bulut hizmetlerini son tespitlerini denetim listesi (koruma)

Geliştirilmiş Microsoft [bulut Hizmetleri son Tespitlerini denetim hello](https://aka.ms/cloudchecklist.download) toohelp kuruluşlar çalışma son tespitlerini gibi bunlar taşıma toohello Bulutu dikkate alın. Tüm boyutunu ve türünü, bir kuruluş için bir yapı sağlar — özel işletmelerin ve kamu tüm düzeyleri ve kar amacı gütmeyen kuruluşlar dahil, ortak kesimli kuruluşlar — tooidentify kendi performansını, hizmet, veri yönetimi ve idare hedefleri ve gereksinimleri. Bu farklı bir bulut hizmet sağlayıcılarının, sonuçta bir bulut hizmet sözleşmesi hello temelini oluşturan toocompare hello teklifleri sağlar.

Başlangıç denetim listesi yan tümcesi by yan için yeni bir uluslararası standart bulut hizmet sözleşmelerini, ISO/IEC 19086 ile hizalar bir çerçeve sağlar. Bu standart, kuruluşların toohelp bulut benimseme hakkında kararlar ve bulut hizmet teklifleri karşılaştırma için bir ortak yerdeki oluşturmak için dikkat edilecek noktalar birleştirilmiş bir dizi sunar.

Başlangıç denetim listesi, bulut hizmet sağlayıcısı seçme için yapılandırılmış yönerge ve tutarlı, tekrarlanabilir bir yaklaşım sağlayan bir baştan sona vetted taşıma toohello bulut yükseltir.

Bulut benimseme artık yalnızca bir teknoloji bir karardır. Denetim listesi gereksinimleri kuruluş her yönüyle touch çünkü tooconvene tüm anahtar iç karar-alıcılar verdikleri — hello yasal, yanı sıra CIO ve CISO risk yönetimi, tedarik ve uyumluluk uzmanları. Merhaba karar verme işlemi ve yerdeki getirerek beklenmeyen roadblocks tooadoption hello olasılığını azaltır, akıl ses kararlarında hello verimliliğini artırır.

Buna ek olarak, Denetim listesi hello:

- Merhaba bulut benimseme işlemini hello başında karar verenler için anahtar tartışma konularını gösterir.

- Düzenlemelere ve hello kuruluşun kendi hedefleri hakkında kapsamlı iş tartışmalara gizlilik, kişisel bilgileri (PII) ve veri güvenliği için destekler.

- Kuruluşların bir bulut projesi etkileyebilecek olası sorunları tanımlamaya yardımcı olur.

- Sorularla hello tutarlı bir dizi sağlar aynı koşulları, tanımları, ölçümleri ve farklı bir bulut hizmet sağlayıcılarının sunduğu karşılaştırma toosimplify hello işlemi her sağlayıcı için teslim edilebilir.

## <a name="azure-infrastructure-and-application-security-validation-detect"></a>Azure altyapı ve uygulama güvenlik doğrulaması (Algıla)

[Azure işlem güvenliği](https://docs.microsoft.com/azure/security/azure-operational-security) verilerini, uygulamaları ve diğer Microsoft Azure varlıkları korumak için toohello Hizmetleri, denetimleri ve özellikler kullanılabilir toousers başvuruyor.

![Güvenlik doğrulaması (Algıla)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig7.png)

Azure işlem güvenliği hello Microsoft Security Development Lifecycle (SDL), Microsoft Güvenlik Yanıt Merkezi hello dahil olmak üzere benzersiz tooMicrosoft olan üzerinden çeşitli özellikleri elde edilen hello bilgi içeren bir çerçevesi üzerine inşa edilmiştir Program ve hello siber güvenlik tehdit derin tanıma.

### <a name="microsoft-operations-management-suiteoms"></a>Microsoft operations management suite(OMS)

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) hello hello karma bulut BT yönetimi çözümü olan. Tek başına kullanıldığında veya var olan System Center dağıtımınızı OMS verir tooextend hello en fazla esneklik ve bulut tabanlı yönetim altyapınızın denetim.

![Microsoft operations management suite(OMS)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig8.png)

OMS ile şirket içi, Azure, AWS, Windows Server, Linux, VMware ve OpenStack, rekabet çözümleri daha düşük bir maliyetle de dahil olmak üzere tüm bulut örnek yönetebilirsiniz. Merhaba bulut ilk dünya için yerleşik, OMS toomeet yeni iş sınar ve yeni iş yükleri, uygulamaları ve bulut ortamlarını uyum hello en hızlı ve en ekonomik yoludur, kuruluşunuzdaki yeni bir yaklaşım toomanaging sunar.

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics), yönetilen kaynaklardan toplanan verileri merkezi bir depoda birleştirerek OMS için izleme hizmetleri sağlar. Bu veriler, olayları, performans verileri veya hello API sağlanan özel verileri içerebilir. Toplandığında, hello veri uyarı, analiz ve dışarı aktarma için kullanılabilir.

![Log Analytics](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig9.png)

Bu yöntem, çeşitli kaynaklardan tooconsolidate verilerden tanır, birleştirebilirsiniz şekilde varolan ile Azure hizmetlerinizi verilerden ortamı şirket. Aynı zamanda açıkça hello hello veri koleksiyonunu tüm eylemleri kullanılabilir tooall veri türlerini; böylece bu veriler üzerinde gerçekleştirilecek hello eylemden ayırır.

### <a name="azure-security-center"></a>Azure Güvenlik Merkezi

[Azure Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-intro) hello Azure kaynaklarınızın güvenlik engellemek, algılamak, artırılmış görünürlük aracılığı ile toothreats yanıt ve üzerinden denetlemesine yardımcı olur. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

Güvenlik Merkezi, Azure kaynaklarını tooidentify olası güvenlik açıklarını hello güvenlik durumunu çözümler. Öneriler listesi gerekli denetimlerin yapılandırılması hello işleminde size rehberlik eder.

Örneklere şunlar dahildir:

- Kötü amaçlı yazılımdan koruma sağlama toohelp tanımlamak ve kötü amaçlı yazılım kaldırma

- Ağ güvenlik gruplarını ve kurallarını toocontrol trafiği tooVMs yapılandırma

- Web uygulaması güvenlik duvarı toohelp, web uygulamalarınızı hedefleyen saldırılara karşı korumaya sağlama

- Eksik sistem güncelleştirmelerini dağıtma

- Önerilen taban çizgileri hello eşleşmeyen işletim sistemi yapılandırmalarını ele alma

Güvenlik Merkezi otomatik olarak toplar, analiz eder ve Azure kaynakları, hello ağ ve kötü amaçlı yazılımdan koruma programları ve güvenlik duvarları gibi iş ortağı çözümlerinden günlük verilerini tümleştirir. Tehditler algılandığında bir güvenlik uyarısı oluşturulur. Örneklere şunların algılanması dahildir:

- Bilinen kötü amaçlı IP adresleri ile iletişim kuran tehlikeye atılmış VM'ler

- Windows hata raporlama kullanılarak algılanan gelişmiş kötü amaçlı yazılım

- Sanal makineleri karşı deneme yanılma saldırıları

- Tümleşik kötü amaçlı yazılımdan koruma programlarından ve güvenlik duvarlarından güvenlik uyarıları

### <a name="azure-monitor"></a>Azure İzleyicisi

[Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) kaynakları belirli türlerdeki işaretçileri tooinformation sağlar. Görselleştirme, sorgu, yönlendirme, uyarı, otomatik ölçeklendirme ve Otomasyon verilerden hem hello Azure altyapısı (Etkinlik günlüğü) ve tek tek her Azure kaynak (tanılama günlükleri) sunar.

Bulut uygulamalarını birçok taşıma bölümleriyle karmaşıktır. İzleme, uygulamanızı kurma kalır veri tooensure ve sistem durumu iyi çalışan sağlar. Olası sorunlar kapalı veya olanları sorun giderme, toostave yardımcı olur.

![Azure İzleyici](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig10.png) Ayrıca, uygulamanız hakkında izleme verileri toogain ayrıntılı Öngörüler kullanabilir. Bu bilgi tooimprove uygulama performansı veya bakım yardımcı veya aksi halde el ile müdahale gerektiren Eylemler otomatik hale getirme.

Ağınızda güvenlik denetimi, ağ güvenlik açıklarını algılama ve BT güvenliği ve Mevzuat idare modeli ile uyumluluğu sağlamak için önemlidir. Güvenlik grubu görünümü ile yapılandırılmış hello ağ güvenlik grubu ve güvenlik kuralları almak yanı etkin güvenlik kuralları hello. Uygulanacak kurallar Hello listesiyle ağ güvenlik açığı açık hello bağlantı noktaları ve ss belirleyebilirsiniz.

### <a name="network-watcher"></a>Ağ İzleyicisi

[Ağ İzleyicisi](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) bir ağ düzeyinde içinde için ve azure'dan koşullar tanılamak ve toomonitor sağlayan bölgesel bir hizmettir. Ağ Tanılama ve görselleştirme Ağ İzleyicisi ile kullanılabilen araçlar anlamak, tanılama ve Öngörüler tooyour Azure ağında geçirmesine yardımcı olur. Bu hizmet içeren paket yakalama, sonraki atlama IP akış, güvenlik grubu görünümü, NSG akış günlükleri doğrulayın. Senaryo düzeyi izleme Karşıtlık tooindividual ağ kaynak izleme ağ kaynaklarına bir uçtan tooend görünümünü sağlar.

### <a name="storage-analytics"></a>Depolama analizi

[Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) istekleri tooa depolama hizmeti hakkında toplu işlem istatistiklerini ve kapasite verilerini dahil ölçümleri depolayabilirsiniz. İşlemler her iki hello API işlemi düzeyinde ve aynı zamanda hello depolama hizmeti düzeyinde bildirilir ve kapasite hello depolama hizmet düzeyinde bildirilir. Ölçüm verilerini kullanılan tooanalyze depolama hizmeti kullanım olması, hello depolama hizmeti ve tooimprove hello bir hizmeti kullanan uygulamaların performansını karşı yapılan istekleri ile sorunları tanılayın.

### <a name="application-insights"></a>Application ınsights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) birden çok platformdaki web geliştiricileri için genişletilebilir bir uygulama performansı Yönetimi (APM) hizmetidir. Toomonitor kullanmak canlı web uygulamanızı. Performans anormalliklerini otomatik olarak algılar. Sorunları ve hangi kullanıcıların uygulamanızı yerine toounderstand tanılamak güçlü analytics araçları toohelp içerir. Bunun tasarlandığından toohelp sürekli olarak artırmak performans ve kullanılabilirlik. Uygulamalar için çalışır platformları .NET, Node.js ve J2EE dahil olmak üzere çeşitli şirket içi barındırılan veya hello bulutta. DevOps işleminizi ile tümleşir ve bağlantı noktaları tooa çeşitli geliştirme araçlarına sahiptir.

Şunları izler:

- **İstek oranları, yanıt süreleri ve hata oranları**: Hangi sayfaların günün hangi saatlerinde popüler olduğunu ve kullanıcılarınızın konumunu öğrenin. En iyi performansı hangi sayfaların gösterdiğini görün. Daha fazla istek olduğunda yanıt süreleriniz ve hata oranlarınız yükseliyorsa bir kaynak atama sorununuz olabilir.

- **Bağımlılık oranları, yanıt süreleri ve hata oranları**: Dış hizmetlerin sizi yavaşlatıp yavaşlatmadığını öğrenin.

- **Özel durumlar** - hello toplanan istatistikleri çözümlemek veya belirli örnekleri seçin ve hello yığın izleme ve ilgili istekleri ayrıntıya gidin. Hem sunucu hem de tarayıcı özel durumları raporlanır.

- **Sayfa görüntüleme sayısı ve yükleme performansı**: Kullanıcılarınızın tarayıcıları tarafından gerçekleştirilir.

- **AJAX çağrılarından web sayfaları** -oranları, yanıt sürelerini ve başarısızlık oranları.

- **Kullanıcı ve oturum sayısı.**

- Windows veya Linux sunucu makinelerinizden CPU, bellek ve ağ kullanımı gibi **performans sayaçları**.

- Docker veya Azure’dan **konak tanılama**.

- Uygulamanızdan **tanılama izleme günlükleri**: İzleme olayları ile istekler arasında bağıntı kurmanıza imkan tanır.

- **Özel olayları ve ölçümleri** , kendiniz hello istemci veya sunucu kodu, tootrack iş öğeleri satılan olaylarına veya Kazanılan oyun yazma.
Uygulamanız için Hello altyapısı genellikle birçok bileşenlerinin – belki de bir sanal makine, depolama hesabı ve sanal ağ veya bir web uygulaması, veritabanı, veritabanı sunucusu ve 3 taraf hizmetleri oluşur. Bu bileşenleri ayrı varlıklar olarak değerlendirmez, bunun yerine bunları tek bir varlığın ilgili ve birbirine bağımlı parçaları olarak kabul edersiniz. Toodeploy istediğiniz, yönetmek ve bunları bir grup olarak izleyebilirsiniz. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) hello kaynaklarla bir grup olarak çözümünüzdeki toowork sağlar.

Dağıtma, güncelleştirme veya tek ve eşgüdümlü bir işlemle, çözümünüz için tüm hello kaynakları silin. Dağıtım için bir şablon kullanabilirsiniz. Üstelik bu şablon test, hazırlık ve üretim gibi farklı ortamlarda da çalışabilir. Resource Manager Güvenlik denetimi sağlar ve özellikleri toohelp etiketleme, kaynaklarınızın dağıtımdan sonra yönetin.

**Kaynak Yöneticisi'ni kullanarak hello avantajları**

Resource Manager çeşitli avantajlar sunar:

- Dağıtmak, yönetmek ve bir grubu yerine bu kaynakları ayrı ayrı ele çözümünüz için tüm hello kaynakları izle.

- Art arda çözümünüzü hello geliştirme yaşam döngüsü boyunca dağıtmak ve kaynaklarınızın tutarlı bir durumda dağıtılması da size güven verir.

- Altyapınızı betikler yerine bildirim temelli şablonları kullanarak yönetebilirsiniz.

- Merhaba doğru sırayla dağıtılmalarını sağlamak kaynakları arasındaki hello bağımlılıkları tanımlayabilirsiniz.

- Rol tabanlı erişim denetimi (RBAC) yerel olarak hello yönetim platformuyla doğrudan tümleşik olduğundan, kaynak grubuna erişim denetimi tooall Hizmetleri uygulayabilirsiniz.

- Etiketleri uygulayabilirsiniz tooresources toologically aboneliğinizdeki tüm hello kaynakları düzenleyin.

- Kaynak grubu için maliyetleri görüntüleyerek kuruluşunuzun fatura açıklık getirebilir paylaşımı hello aynı etiketi.

> [!Note]
> Resource Manager çözümlerinizi yönetmek ve yeni bir yolu toodeploy sağlar. Kullandıysanız Merhaba önceki dağıtım modelini ve hello değişiklikler hakkında toolearn istediğiniz, bkz: [anlama Resource Manager dağıtımını ve klasik dağıtımı](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="next-steps"></a>Sonraki adımlar

Güvenlik hakkında daha fazla bizim kapsamlı güvenlik konuların bazıları okuyarak bulun:

- [Denetme ve günlüğe kaydetme](https://www.microsoft.com/en-us/trustcenter/security/auditingandlogging)

- [Siber Suçlar](https://www.microsoft.com/en-us/trustcenter/security/cybercrime)

- [Tasarım ve işlem güvenliği](https://www.microsoft.com/en-us/trustcenter/security/designopsecurity)

- [Şifreleme](https://www.microsoft.com/en-us/trustcenter/security/encryption)

- [Kimlik ve erişim yönetimi](https://www.microsoft.com/en-us/trustcenter/security/identity)

- [Ağ güvenliği](https://www.microsoft.com/en-us/trustcenter/security/networksecurity)

- [Tehdit yönetimi](https://www.microsoft.com/en-us/trustcenter/security/threatmanagement)

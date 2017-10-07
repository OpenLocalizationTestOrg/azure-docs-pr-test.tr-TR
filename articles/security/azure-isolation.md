---
title: hello Azure genel bulut aaaIsolation | Microsoft Docs
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
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 271e5f0d00abcfd404ce6c50cfb7d1ac26360c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="isolation-in-hello-azure-public-cloud"></a>Hello Azure genel bulut ayırma
##  <a name="introduction"></a>Giriş
### <a name="overview"></a>Genel Bakış
tooassist geçerli ve gelecekteki Azure müşterilerine anlamak ve hello kullanma çeşitli güvenlikle ilgili özellikleri bulunan ve çevresindeki Azure platformu Merhaba, Microsoft teknik incelemeler, güvenlik genel bakışlar, en iyi yöntemler, bir dizi geliştirilen ve Denetim listeleri.
Merhaba konuları avantajlarına ve derinliği bakımından aralığı ve düzenli aralıklarla güncelleştirilir. Bu belge aşağıdaki hello soyut bölümünde özetlenen serisi bir parçası değil.

### <a name="azure-platform"></a>Azure platformu
Azure işletim sistemlerinin programlama dilleri, çerçeveleri, Araçlar, veritabanları ve cihazları, en geniş seçim hello destekleyen açık ve esnek bir bulut hizmeti platformudur. Örneğin, şunları yapabilirsiniz:
- Linux kapsayıcıları Docker Tümleştirmesi ile çalıştırın;
- JavaScript, Python, .NET, PHP, Java ve Node.js ile uygulamalar oluşturma; ve
- Yapı geri-iOS, Android ve Windows cihazları sona erer.

Microsoft Azure, geliştiriciler ve BT uzmanları, aynı teknolojileri milyonlarca zaten kullanır ve güven hello destekler.

Oluşturmanıza veya BT varlıklar bir genel bulut hizmeti sağlayıcısına geçiş yapma, uygulamalarınızı, bir kuruluşun yeteneklerini tooprotect üzerinde bağlı ve hizmetler ve hello denetimleri ile veri hello olduğunda, bulut tabanlı toomanage hello güvenliğini sağlarlar. varlıklar.

Azure'nın altyapı hello tesis tooapplications aynı anda milyonlarca müşteri barındırmak için gelen tasarlanmıştır ve güvenlik gereksinimlerine bağlı işletmeler karşılayabilecek güvenilir bir temel sağlar. Ayrıca, Azure, çok çeşitli yapılandırılabilir güvenlik seçenekleri ve hello özelliği toocontrol sağlar bunları böylece güvenlik toomeet hello benzersiz gereksinimlerini dağıtımlarınızı özelleştirebilirsiniz. Bu belge, bu gereksinimleri karşılayan yardımcı olur.

### <a name="abstract"></a>Özet

Microsoft Azure üzerinde paylaşılan fiziksel altyapı toorun uygulamalar ve sanal makineleri (VM'ler) sağlar. Merhaba prime ekonomik sözleri toorunning uygulamaları bir bulut ortamında hello özelliği toodistribute hello paylaşılan kaynakları birden çok müşteri arasında maliyetini biridir. Bu yöntem, çok kiracılı çoğullama kaynaklar arasında düşük maliyetler farklı müşterilerine tarafından verimliliği artırır. Ne yazık ki, bu aynı zamanda hello riski fiziksel sunucuların ve diğer altyapı kaynakları toorun paylaşımı duyarlı uygulamalar ve rasgele tooan ve kötü amaçlı kullanıcı ait VM'ler sunar.

Bu makalede, Microsoft Azure kötü amaçlı ve kötü amaçlı olmayan kullanıcılara karşı yalıtımı sağlar ve bulut çözümleri çeşitli yalıtım seçenekleri tooarchitects sunarak mimariden için bir kılavuz olarak hizmet veren nasıl özetlenmektedir. Bu teknik incelemede Azure platformu ve müşteri dönük güvenlik denetimleri hello teknolojisi üzerine odaklanır ve tooaddress fiyatlandırma modelleri ve DevOps yöntem değerlendirmeleri SLA denemez.

## <a name="tenant-level-isolation"></a>Kiracı düzeyinde yalıtım
Paylaşılan ortak bir altyapının çeşitli müşterilerin arasında aynı anda kavramdır bilgi işlem, Ölçek tooeconomies baştaki bulutun hello birincil avantajlarından biri. Bu kavram çoklu kiracı adı verilir. Microsoft, Microsoft bulut Azure hello çok kiracılı mimarisi güvenlik, gizlilik, gizlilik, bütünlük ve kullanılabilirlik standartlarını destekler tooensure sürekli çalışmaktadır.

Merhaba bulut etkin olduğu çalışma alanında, bir kiracı istemcisi veya sahip ve bu bulut hizmeti belirli bir örneği yöneten kuruluş olarak tanımlanabilir. Microsoft Azure tarafından sağlanan hello kimlik ile bir Kiracı yalnızca Azure Active kuruluşunuz alır ve bir Microsoft bulut hizmeti için oturum kaydolduğunda sahibi Directory (Azure AD) adanmış örneği platformudur.

Her Azure AD dizini, diğer Azure AD dizinlerinden farklı ve ayrıdır. Kurumsal ofis binasının yalnızca gibi güvenli varlık belirli tooonly kuruluşunuz, Azure AD dizini de güvenli bir varlık yalnızca kuruluşunuz tarafından kullanılmak üzere tasarlanmış toobe oluştu. Hello Azure AD mimarisi ortak karıştırma alanından müşteri verileri ve kimlik bilgileri yalıtır. Bu, bir Azure AD dizinindeki kullanıcıların ve yöneticilerin yanlışlıkla veya kötü amaçlı olarak başka bir dizindeki verilere erişemeyeceği anlamına gelir.

### <a name="azure-tenancy"></a>Azure kiralama
Azure kiralama (Azure abonelik) başvuruyor tooa "Müşteri/faturalama" ilişkisi ve benzersiz bir [Kiracı](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) içinde [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis). Kiracı düzeyinde yalıtım Microsoft Azure, Azure Active Directory'yi kullanarak gerçekleştirilir ve [rol tabanlı denetimler](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) tarafından sunulan. Her Azure aboneliği bir Azure Active Directory (AD) dizin ile ilişkilendirilir.

Kullanıcılar, gruplar ve uygulamalar bu dizinden hello Azure aboneliği kaynaklarında yönetebilirsiniz. Hello Azure portal, Azure komut satırı araçları ve Azure Management API'leri kullanılarak bu erişim haklarını atayabilirsiniz. Azure AD kiracısı böylece hiçbir müşterinin erişmek veya kötü amaçlı olarak veya yanlışlıkla ortak kiracılar tehlikeye güvenlik sınırları kullanarak mantıksal olarak ayrı tutulur. İstenmeyen bağlantılar ve trafik burada ana bilgisayar düzeyinde paket filtreleme ve Windows Güvenlik Duvarı Engelleme "tam" sunuculara ayrı ağ kesiminde yalıtılmış Azure AD çalışır.

- Azure AD'de erişim toodata aracılığıyla kullanıcı kimlik doğrulaması gerektiren bir [güvenlik belirteci hizmeti (STS)](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization). Merhaba istenen erişim toohello hedef Kiracı bu kullanıcı için bu oturumda yetkilendirilip yetkilendirilmediğini hello kullanıcının varlığı, etkin durumunu ve rol bilgilerini hello yetkilendirme sistem toodetermine tarafından kullanılır.

![Azure kiralama](./media/azure-isolation/azure-isolation-fig1.png)


- Kiracılar ayrık kapsayıcılardır ve ilişkisi yoktur. Bunlar arasında.

- Kiracı yönetici Federasyon veya diğer kiracıdan kullanıcı hesapları sağlama aracılığıyla verir sürece üzerinden erişim yok Kiracı.

- Hello Azure AD hizmeti ve doğrudan erişim tooAzure Reklamın arka uç sistemleri oluşturan fiziksel erişimi tooservers sınırlıdır.

- Azure AD kullanıcıların hiçbir toophysical varlıklarına erişmek veya konumları sahip ve bu nedenle aşağıdaki belirtildiği bunları toobypass hello mantıksal RBAC İlkesi denetimleri için mümkün değildir.

Tanılama ve Bakım gereksinimlerini için yalnızca zaman ayrıcalık yükseltme sistem kullanan bir çalışma modeline gereken ve kullanılır. Azure AD Privileged Identity Management (PIM) hello kavramı uygun bir yönetici, tanıtır [Uygun admins](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) ayrıcalıklı olması gereken kullanıcılar erişim şimdi yapıp ancak her gün olmalıdır. bir etkinleştirme işlemini tamamlamak ve önceden belirlenen bir süre için etkin bir yönetim hale hello kullanıcının erişim, gerektiği kadar hello rolü etkin değil.

![Azure AD Privileged Identity Management](./media/azure-isolation/azure-isolation-fig2.png)

Azure Active Directory ilkeleri ve izinlerini tooand yalnızca ait ve hello Kiracı tarafından yönetilen hello kapsayıcı içindeki ile korunan kendi kapsayıcıdaki her bir kiracı barındırır.

Kiracı kapsayıcıları Hello kavramı hello dizin hizmetindeki tüm katmanları en son derece þeklimize, portallar tüm yolu toopersistent depolama hello.

Birden çok Azure Active Directory Kiracı meta verilerini bile depolanır, aynı fiziksel hello disk, sırayla hello Kiracı Yöneticisi tarafından dikte hello dizin hizmeti tarafından tanımlanan dışında Merhaba kapsayıcılara arasında ilişkisi yoktur.

### <a name="azure-role-based-access-control-rbac"></a>Azure rol tabanlı erişim denetimi (RBAC)
[Azure rol tabanlı erişim denetimi (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) Azure için ayrıntılı erişim yönetimi sağlayarak, tooshare bir Azure aboneliği kullanılabilen çeşitli bileşenler yardımcı olur. Azure RBAC toosegregate görevlerini kuruluşunuzdaki etkinleştirir ve erişime dayalı işlerini hangi kullanıcıların tooperform gerekir. Kısıtlanmamış izinlerini herkes vermek yerine Azure aboneliği veya kaynakları, yalnızca belirli eylemleri izin verebilirsiniz.

Azure RBAC tooall kaynak türleri geçerli üç temel rol vardır:

- **Sahibi** hello sağ toodelegate erişim tooothers dahil olmak üzere tam erişim tooall kaynaklara sahip.

- **Katkıda bulunan** olabilir oluşturun ve tüm türlerini Azure kaynaklarını yönetmek ancak erişim tooothers veremezsiniz.

- **Okuyucu** mevcut Azure kaynaklarını görüntüleyebilirsiniz.

![Azure rol tabanlı erişim denetimi](./media/azure-isolation/azure-isolation-fig3.png)

azure'da hello RBAC rollerin Hello rest belirli Azure kaynaklarının yönetimini sağlar. Örneğin, hello sanal makine katkıda bulunan rolü hello kullanıcı toocreate verir ve sanal makineleri yönetme. Bunları erişim toohello Azure Virtual Network vermez veya sanal makine hello hello alt ağa bağlanır.

[RBAC yerleşik rolleri](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) Azure'da kullanılabilir hello rolleri listeler. Merhaba işlemler ve her yerleşik rol toousers verir kapsam belirtir. Daha fazla denetim için kendi rolleri toodefine arıyorsanız, bkz. nasıl toobuild [Azure rbac'de özel roller](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles).

Azure Active Directory için başka bazı özellikleri şunlardır:
- Azure AD burada barındırılan bağımsız olarak SSO tooSaaS uygulamaları etkinleştirir. Bazı uygulamalar Azure AD federasyonu kullanırken diğerleri parola SSO hizmetinden yararlanır. Federasyon uygulamalarına, kullanıcı sağlamayı da destekleyebilir ve [parola kasası oluşturma](https://www.techopedia.com/definition/31415/password-vault).

- Erişim toodata [Azure Storage](https://azure.microsoft.com/services/storage/) kimlik doğrulaması denetlenir. Her Depolama hesabı bir birincil anahtara sahip ([depolama hesabı anahtarı](https://docs.microsoft.com/azure/storage/storage-create-storage-account), veya SAK) ve ikincil bir gizli anahtar (Merhaba paylaşılan erişim imzası veya SAS).

- Azure AD kimlik Federasyon üzerinden bir hizmet olarak kullanarak sağlar [Active Directory Federasyon Hizmetleri](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-azure-adfs), eşitleme ve çoğaltma ile şirket içi dizinleri.

- [Azure çok faktörlü kimlik doğrulaması](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) bir mobil uygulama, telefon araması veya kısa mesaj kullanarak kullanıcıların tooverify oturum açma işlemleri gerektiren hello çok faktörlü kimlik doğrulama hizmetidir. Hello Azure multi-Factor Authentication sunucusu ile ve özel uygulamalar ve dizinler hello SDK kullanarak Azure AD toohelp güvenli şirket içi kaynaklar ile kullanılabilir.

- [Azure AD etki alanı Hizmetleri](https://azure.microsoft.com/services/active-directory-ds/) , etki alanı denetleyicilerini dağıtmaya olmadan Azure sanal makineleri tooan Active Directory etki alanına olanak tanır. Toothese sanal makinelerinizde Kurumsal Active Directory kimlik bilgilerinizle oturum açın ve etki alanına katılmış sanal makineler, Azure virtual machines tüm Grup İlkesi tooenforce güvenlik temelleri kullanarak yönetebilirsiniz.

- [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) toohundreds kimlikleri milyonlarca ölçeklendirilebilen bir yüksek oranda kullanılabilir kimlik genel yönetim hizmeti tüketiciye yönelik uygulamalar için sağlar. Bu hizmet mobil platformlar ve web platformlarıyla tümleştirilebilir. Tüketicileriniz, var olan sosyal hesaplarını kullanarak veya kimlik bilgileri oluşturma uygulamalarınızı özelleştirilebilir deneyimler aracılığıyla tooall içinde imzalayabilirsiniz.

### <a name="isolation-from-microsoft-administrators--data-deletion"></a>Yalıtım Microsoft Yöneticiler & veri silme
Microsoft güçlü ölçüleri tooprotect uygunsuz erişim ya da yetkisiz kişilerin kullanımına verilerinizden alır. Bu işlem süreçlerini ve denetimleri hello tarafından yedeklenen [çevrimiçi Hizmet Koşulları'nı](http://aka.ms/Online-Services-Terms), erişim tooyour veri yöneten sözleşme taahhüt sunar.

-   Microsoft mühendisleri varsayılan erişim tooyour veri hello buluta sahip değilsiniz. Bunun yerine, bunlar yönetim gözetim, yalnızca gerekli olduğunda altında erişimi verilir. Bu erişim olduğunu dikkatle denetlenen ve oturum açmış ve artık gerekli olmadığında iptal.

-   Microsoft, diğer şirketler tooprovide sınırlı hizmetleri kendi adına işe. Alt yüklenicilerimiz için müşteri verileri yalnızca toodeliver hello Hizmetleri erişebilir biz bunları tooprovide işe ve başka bir amaçla kullanmaları yasaktır. Ayrıca, müşterilerimizin bilgi kapsamındaki ilişkili toomaintain hello gizliliğini oldukları.

ISO/IEC 27001 düzenli olarak Microsoft tarafından doğrulandı ve accredited gibi iş denetlenen sertifikalar ile örnek denetimleri tooattest gerçekleştirmek firmalarından yasal İşletme amaçları için yalnızca bu erişim denetim hizmetleri. Müşteri verilerini her zaman, dilediğiniz zaman ve herhangi bir nedenle da erişebilirsiniz.

Herhangi bir veri silerseniz, Microsoft Azure önbelleğe alınmış veya yedek kopyaları dahil hello verileri siler. Kapsam hizmetler için bu silme hello saklama dönemi hello bitişinden sonra 90 gün içinde ortaya çıkar. (Kapsam içinde Hizmetleri hello veri işleme koşulları bölümünde tanımlanmış bizim [çevrimiçi Hizmet Koşulları'nı](http://aka.ms/Online-Services-Terms).)

Depolama için kullanılan bir disk sürücüsü bir donanım hatası varsa, güvenli bir şekilde olan [silinmesi veya tahrip](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data) isteğe bağlı olarak Microsoft değiştirme veya Onar toohello üreticisini döndürmeden önce. Merhaba hello sürücüdeki verilerin üzerine veri hello tooensure herhangi bir yolla kurtarılamıyor.

## <a name="compute-isolation"></a>Yalıtım işlem
Microsoft Azure, geniş işlem örnekleri içeren çeşitli bulut tabanlı bilgi işlem hizmetler & otomatik olarak toomeet hello ihtiyaçlarını uygulamanızı veya Kurumsal yukarı ve aşağı ölçeklenebilen hizmetleri sağlar. Bu işlem örneğinde ve hizmet yalıtım birden çok düzeyleri toosecure veri yapılandırma hello esneklik ödün vermeden, müşterilerinizin talep sunar.

### <a name="hyper-v--root-os-isolation-between-root-vm--guest-vms"></a>Kök VM & Konuk VM'ler arasında Hyper-V & kök işletim sistemi yalıtımı
Azure işlem platformu makine sanallaştırmayı temel — yani bir Hyper-V sanal makinesinde tüm müşteri kodu yürütür. Her Azure düğümü (veya ağ uç noktası), doğrudan hello donanımın üzerinde çalışır ve değişken sayıya Konuk sanal makineleri (VM'ler), bir düğüm böler bir hiper yoktur.


![Kök VM & Konuk VM'ler arasında Hyper-V & kök işletim sistemi yalıtımı](./media/azure-isolation/azure-isolation-fig4.jpg)


Her düğüm, bir özel kök hello ana bilgisayar işletim sistemi çalıştıran VM da sahiptir. Merhaba yalıtım hello Konuk VM'ler VM kökünden hello hello Konuk sanal makineleri birbirinden, hello hiper yönetici ve hello kök işletim sistemi tarafından yönetilir ve bir kritik sınırıdır. Hiper yönetici/kök işletim sistemi Hello eşleştirme Microsoft'un on yılları işletim sistemi güvenlik deneyimi ve Microsoft Hyper-V'ye, tooprovide güçlü yalıtım Konuk VM'ler, daha yeni öğrenme yararlanır.

Hello Azure platformu, sanallaştırılmış bir ortam kullanır. Tek başına sanal makineler erişim tooa fiziksel ana bilgisayar sunucusu olmayan kullanıcı örnekleri çalıştırmak ve fiziksel işlemci (halka-0/halkası-3) ayrıcalık düzeylerini kullanarak bu yalıtım zorlanır.

Halka 0 hello en ayrıcalıklı ve 3 hello az olmasıdır. daha düşük ayrıcalıklı halkası 1'de Hello konuk işletim sistemi çalışır ve en az ayrıcalıklı Halka 3 çalışan uygulamaların hello. Bu sanallaştırma fiziksel kaynakların, konuk işletim sistemi ve hiper yönetici, ek güvenlik ayrımı hello iki arasında sonuçta arasında tooa açıkça birbirinden yol açar.

Hello Azure hiper yönetici mikro çekirdek gibi davranır ve tüm donanım erişim isteklerini işlemek için konuk sanal makineleri toohello ana bilgisayardan VMBus adında bir paylaşılan bellek arabirimi kullanarak geçirir. Bu, kullanıcıların ham okuma/yazma/yürütme erişim toohello sistem elde etmesini engeller ve sistem kaynaklarını paylaşımı hello riskini azaltır.

### <a name="advanced-vm-placement-algorithm--protection-from-side-channel-attacks"></a>Gelişmiş VM yerleştirme algoritması & yan kanal saldırılarına karşı koruma
Çapraz VM saldırı iki adımdan oluşur: aynı konak hello kurban VM'ler biri olarak hello etkilemeyi denetimli VM yerleştirerek ve hello yalıtım sınır tooeither ihlal kurban hassas bilgilerinizi çalan veya greed veya vandalism için kendi performansını etkiler. Microsoft Azure, Gelişmiş bir VM yerleştirme algoritması ve gürültülü komşu Vm'leri de dahil olmak üzere tüm bilinen yan kanal saldırılarına karşı koruma kullanarak her iki adımın korumasının sağlar.

### <a name="hello-azure-fabric-controller"></a>Hello Azure yapı denetleyicisi
Hello Azure yapı denetleyicisi altyapı kaynaklarını tootenant iş yükleri için ayırma sorumludur ve tek yönlü iletişim hello konak toovirtual makinelerden yönetir. Merhaba VM yerleştirme hello Azure yapı denetleyicisi yüksek oranda karmaşık ve neredeyse imkansız toopredict fiziksel ana bilgisayar düzeyinde algoritmasıdır.

![Hello Azure yapı denetleyicisi](./media/azure-isolation/azure-isolation-fig5.png)

Hello Azure hiper yönetici bellek zorunlu kılan ve ağ trafiğini tooguest OS kiracılar işlem ayırma ve sanal makineler arasında güvenli bir şekilde yönlendirir. Bu olasılığını ve yan kanal saldırı VM düzeyinde ortadan kaldırır.

Azure'da hello kök VM özeldir: bir sıkı işletim hello kök işletim sistemi olarak adlandırılan bir doku Aracısı (FA) barındıran sistem çalıştırır. SK'lar müşteri sanal makineleri konuk işletim sistemleri içinde Aç toomanage Konuk aracıları (GA) kullanılır. SK'lar depolama düğümleri da yönetebilirsiniz.

Hello Azure hiper yönetici topluluğu kök işletim sistemi/FA ve müşteri sanal makineleri/gaz bir işlem düğümünde oluşur. SK'lar (bilgi işlem ve depolama kümeleri ayrı FCs tarafından yönetilen) işlem ve depolama düğümleri dışında var olan bir yapı denetleyicisi (FC) tarafından yönetilir. Çalışırken bir müşteri, uygulamanın yapılandırma dosyasına güncelleştirmeleri olursa hello FC hangi hello yapılandırma değişikliği hello uygulamasının bildir, ardından gaz kişiler, hello ile FA, iletişim kurar. Bir donanım hatası Hello olayda hello FC otomatik olarak kullanılabilir donanım bulmak ve Merhaba VM yeniden başlatın.

![Azure yapı denetleyicisi](./media/azure-isolation/azure-isolation-fig6.jpg)

Bir doku denetleyicisi tooan Aracısı iletişimi tek yönlüdür. Merhaba aracı yalnızca toorequests hello denetleyicisinden yanıt SSL korumalı bir hizmet uygular. Bağlantıları toohello denetleyicisi veya ayrıcalıklı başka iç düğümleri başlatamaz. Güvenilmeyen sanki hello FC tüm yanıtları değerlendirir.


![Yapı denetleyicisi](./media/azure-isolation/azure-isolation-fig7.png)

Merhaba kök VM Konuk vm'lerden ve hello Konuk VM'ler birbirinden yalıtım genişletir. İşlem düğümleri artan koruma için depolama düğümlerinden de yalıtılır.


Merhaba hiper yönetici ve hello konak işletim sistemi için ağ paketi sağlar - filtreleri toohelp güvenilmeyen sanal makineleri olamaz sahte trafik oluşturabilir veya ele alınmayan trafiği toothem, doğrudan trafiği tooprotected altyapı uç noktaları veya gönderme ve alma almaya güvence altına alır uygunsuz yayın trafiği.


### <a name="additional-rules-configured-by-fabric-controller-agent-tooisolate-vm"></a>Yapı denetleyicisi Aracısı tooIsolate VM tarafından yapılandırılır ek kuralları
Varsayılan olarak, tüm trafik, bir sanal makine oluşturulduğunda ve ardından hello doku Denetleyicisi aracı hello paket filtre tooadd kuralları ve özel durumları yetkili tooallow trafiği yapılandırır engellenir.

Programlanmış kuralları iki kategorisi vardır:

-   **Makine yapılandırma veya altyapı kuralları:** varsayılan olarak, tüm iletişimin engellenir. Var. özel durumları tooallow olan bir sanal makine toosend ve DHCP ve DNS trafiği alabilir. Sanal makineler ayrıca trafiği toohello "Genel" Internet ve gönderme trafiği tooother içindeki sanal makineleri aynı Azure sanal ağ hello ve işletim sistemi Etkinleştirme sunucusu hello gönderebilirsiniz. izin verilen giden hedefleri Hello sanal makineler listesi Azure yönlendirici alt ağlar, Azure yönetim ve diğer Microsoft özellikleri içermez.

-   **Rol yapılandırma dosyası:** bu gelen erişim denetim listeleri (ACL'ler) tabanlı hello kiracının hizmet modelinde hello tanımlar.

### <a name="vlan-isolation"></a>VLAN yalıtımı
Her kümedeki üç VLAN'ları vardır:

![VLAN yalıtımı](./media/azure-isolation/azure-isolation-fig8.jpg)


-   Merhaba ana VLAN – bağlantılar güvenilmeyen müşteri düğümler

-   Merhaba FC VLAN – içeren güvenilir FCs ve sistemler destekleme

-   cihaz VLAN hello – güvenilir ağ ve diğer altyapı aygıtları içerir

Merhaba FC VLAN toohello iletişimi izin verilen ana VLAN, ancak hello ana VLAN toohello FC VLAN başlatılamaz. İletişim hello ana VLAN toohello aygıttan VLAN de engellenir. Bu, bir düğümde müşteri kodu çalışan tehlikede olsa bile, onu hello FC veya aygıt VLAN'lar düğümlerinde saldırı olamaz emin olmasını sağlar.

## <a name="storage-isolation"></a>Depolama ayırma
### <a name="logical-isolation-between-compute-and-storage"></a>İşlem ve depolama arasında mantıksal ayırma
Temel tasarımını bir parçası olarak, Microsoft Azure VM tabanlı hesaplama depolama biriminden ayırır. Bu ayrım hesaplama ve depolama tooscale bağımsız olarak, daha kolay tooprovide çoklu kiracı ve yalıtım hale sağlar.

Bu nedenle, Azure Storage yok ağ bağlantısı tooAzure ile ayrı donanımda dışında mantıksal işlem çalışır. [Bu](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf) bir sanal disk oluşturulduğunda, disk alanı için tüm kapasitesi atanmadı anlamına gelir. Bunun yerine, bir tablo hello sanal disk tooareas hello fiziksel diskte adreslerini eşleştiren oluşturulur ve bu başlangıçta boş bir tablodur. **Merhaba ilk kez bir müşteri hello fiziksel disk alanı ayrılır ve bir işaretçi tooit hello tabloda yerleştirilir hello sanal disk üzerinde veri yazar.**
### <a name="isolation-using-storage-access-control"></a>Yalıtım kullanılarak depolama erişim denetimi
**Erişim denetimi Azure storage'da** basit erişim denetimi modeli vardır. Her Azure aboneliği bir veya daha fazla depolama hesabı oluşturabilirsiniz. Her Depolama hesabı kullanılan toocontrol erişim tooall bu depolama hesabı verilerde tek bir gizli anahtar vardır.

![Yalıtım kullanılarak depolama erişim denetimi](./media/azure-isolation/azure-isolation-fig9.png)

**(Tablolar dahil) tooAzure depolama verilere** aracılığıyla denetlenen bir [SAS (paylaşılan erişim imzası)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) hangi verir kapsamlı erişim belirteci. Merhaba SAS hello ile imzalanmış bir sorgu şablonu (URL) aracılığıyla oluşturulan [SAK (depolama hesabı anahtarı)](https://msdn.microsoft.com/library/azure/ee460785.aspx). [URL imzalı](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) sonra hello sorgusunun hello ayrıntıları doldurun ve hello isteği hello depolama hizmetinin yapabilirsiniz (yani temsilci) tooanother işleminin verilebilir. Bir SAS hello depolama hesabının gizli anahtarı göstermeden toogrant zamana dayalı erişim tooclients sağlar.

Merhaba SAS biz istemci sınırlı izinleri, süre ve belirtilen bir izin kümesi ile belirli bir süre için bizim depolama hesabındaki tooobjects verebilirsiniz anlamına gelir. Hesap erişim tuşlarınızı tooshare gerek kalmadan Biz bu sınırlı izinleri verebilirsiniz.

### <a name="ip-level-storage-isolation"></a>IP düzey depolama yalıtımı
Güvenlik duvarları kurmak ve güvenilir istemcileriniz için bir IP adresi aralığı tanımlayabilirsiniz. Bir IP adresi aralığı ile tanımlanan hello aralığında bir IP adresine sahip yalnızca istemcileri çok bağlanabilir[Azure Storage](https://docs.microsoft.com/azure/storage/storage-security-guide).

IP depolama veri kullanılan tooallocate adanmış veya ayrılmış tüneli trafik tooIP depolama ağ bir mekanizma aracılığıyla yetkisiz kullanıcılara karşı korunur.

### <a name="encryption"></a>Şifreleme
Azure şifreleme tooprotect veri türleri sunar:
-   Aktarımdaki şifreleme

-   Bekleme sırasında şifreleme

#### <a name="encryption-in-transit"></a>Aktarımdaki şifreleme
Şifreleme Aktarımdaki ağlar üzerinden iletilirken veri koruma, bir mekanizmadır. Azure Storage ile verileri kullanarak güvenliğini sağlayabilirsiniz:

-   [Aktarım düzeyinde şifreleme](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), içine veya dışına Azure Storage veri aktarırken HTTPS gibi.

-   [Şifreleme wire](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), Azure dosya paylaşımları için SMB 3.0 şifreleme gibi.

-   [İstemci tarafı şifreleme](https://docs.microsoft.com/azure/storage/storage-security-guide#using-client-side-encryption-to-secure-data-that-you-send-to-storage), depolama alanı biterse aktarıldıktan sonra depolama ve toodecrypt hello verisine transfer edilmeden önce tooencrypt hello veri.

#### <a name="encryption-at-rest"></a>Bekleyen şifreleme
Çoğu kuruluş için [bekleyen verileri şifreleme](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) veri gizliliği, uyumluluk ve veri egemenliği doğru zorunlu bir adımdır. "Bekleyen" olan verilerin şifrelenmesini sağlayan üç Azure özellikleri şunlardır:

-   [Depolama hizmeti şifrelemesi](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-at-rest) toorequest hello depolama hizmeti otomatik olarak veri tooAzure depolama yazılırken şifrelemenizi sağlar.

-   [İstemci tarafı şifreleme](https://docs.microsoft.com/azure/storage/storage-security-guide#client-side-encryption) bekleyen şifreleme hello özelliği de sağlar.

-   [Azure Disk şifrelemesi](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) tooencrypt hello işletim sistemi ve bir Iaas sanal makine tarafından kullanılan veri disklerle sağlar.

#### <a name="azure-disk-encryption"></a>Azure Disk Şifrelemesi
[Azure Disk şifrelemesi](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) sanal makineleri (VM'ler) adresi kuruluş güvenlik ve uyumluluk gereksinimleri (önyükleme ve veri diskleri dahil), VM diskleri şifreleyerek anahtarları ve, denetim ilkeleri ile yardımcı olan [Azure anahtarı Kasa](https://azure.microsoft.com/services/key-vault/).

Disk şifrelemesi çözüm için Windows Hello temel [Microsoft BitLocker Sürücü Şifrelemesi](https://technet.microsoft.com/library/cc732774.aspx), ve hello Linux çözüm temel [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).

Microsoft Azure'da etkinleştirildiğinde senaryoları Iaas VM'ler için aşağıdaki hello Hello çözümünü destekler:
-   Azure anahtar kasası ile tümleştirme

-   Standart katmanı VMs: A, D, DS, G, GS ve benzeri serisi Iaas VM'ler

-   Windows ve Linux Iaas VM'ler üzerinde şifrelemeyi etkinleştirme

-   Windows Iaas VM'ler için sürücüler işletim sistemi ve veri şifreleme devre dışı bırakma

-   Veri sürücülerini şifreleme Linux Iaas VM'ler için devre dışı bırakma

-   Windows istemci işletim sistemi çalıştıran bir Iaas Vm'leri üzerinde şifrelemeyi etkinleştirme

-   Bağlama yolları birimlerle şifrelemeyi etkinleştirme

-   Kullanarak Linux (RAID) bölümlemesine diskle yapılandırılmış sanal makineleri üzerinde şifrelemeyi etkinleştirme [mdadm](https://en.wikipedia.org/wiki/Mdadm)

-   Kullanarak Linux VM'ler üzerinde şifrelemeyi etkinleştirme [LVM (mantıksal birim Yöneticisi)](https://msdn.microsoft.com/library/windows/desktop/bb540532) , veri diskleri

-   Depolama alanları kullanılarak yapılandırılan Windows VM'ler üzerinde şifrelemeyi etkinleştirme

-   Tüm Azure genel bölgeleri desteklenir

Merhaba çözüm senaryoları, özellikleri ve teknoloji hello sürümde aşağıdaki hello desteklemez:

-   Temel katman Iaas VM'ler

-   Bir işletim sistemi sürücüsünde Linux Iaas VM'ler için şifrelemeyi devre dışı bırakma

-   Merhaba Klasik VM oluşturma yöntemini kullanarak oluşturduğunuz Iaas VM'ler

-   Şirket içi anahtar yönetimi hizmeti ile tümleştirme

-   Azure dosyaları (paylaşılan dosya sistemi), ağ dosya sistemi (NFS), dinamik birimler ve yazılım tabanlı RAID sistemler ile yapılandırılmış Windows VM'ler

## <a name="sql-azure-database-isolation"></a>SQL Azure veritabanı yalıtımı
SQL veritabanı hello Microsoft bulut hello piyasaya öncülük eden Microsoft SQL Server altyapısını göre ve kritik iş yükleri işleme yeteneği olan bir ilişkisel veritabanı hizmetidir. SQL veritabanı sunar tahmin edilebilir veri yalıtımı hesap düzeyinde Coğrafya / bölge ve ağ üzerinde dayalı — yönetime neredeyse tüm ile.

### <a name="sql-azure-application-model"></a>SQL Azure uygulama modeli

[Microsoft SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-get-started) veritabanı olan SQL Server teknolojilerinde kurulu bir bulut tabanlı ilişkisel veritabanı hizmeti. Bulutta Microsoft tarafından barındırılan bir yüksek oranda kullanılabilir, ölçeklenebilir, çok Kiracı veritabanı hizmeti sağlar.

Bir uygulama açısından SQL Azure hiyerarşi aşağıdaki hello sağlar: bir çok kapsama aşağıdaki düzeylerinin her düzeyine sahip.

![SQL Azure uygulama modeli](./media/azure-isolation/azure-isolation-fig10.png)

Hello hesabı ve aboneliği olduğundan Microsoft Azure platform kavramları tooassociate faturalama ve yönetim.

Mantıksal sunucular ve veritabanları SQL Azure özgü kavramlar ve OData ve TSQL arabirimleri sağlanan SQL Azure kullanarak veya Azure portalına tümleşik SQL Azure portalı üzerinden yönetilir.

SQL Azure sunucusu fiziksel veya VM örnekleri olmayan, bunun yerine, veritabanları, bu nedenle çağrılan "mantıksal yöneticisinde" depolanır, yönetim ve güvenlik ilkeleriyle paylaşımı koleksiyonlarıdır veritabanı.

![SQL Azure](./media/azure-isolation/azure-isolation-fig11.png)

Mantıksal asıl veritabanını içerir:

-   SQL oturum açma tooconnect toohello sunucusu kullanılan

-   Güvenlik duvarı kuralları

Aynı mantıksal sunucu olmayan fatura ve kullanımı ile ilgili bilgi için SQL Azure hello veritabanlarından garanti toobe hello üzerinde SQL Azure küme aynı fiziksel örneğinde, bunun yerine uygulamaların sağlamalıdır hello hedef veritabanı adı bağlanırken.

Merhaba gerçek hello sunucusunun oluşturulması hello kümeleri hello bölgede birinde gerçekleşirken Müşteri açısından bakıldığında, bir mantıksal sunucu bir grafik coğrafi bölgede oluşturulur.

### <a name="isolation-through-network-topology"></a>Ağ topolojisi yalıtımı

Bir mantıksal sunucu oluşturduğunuzda ve DNS adını kayıtlı hello DNS adı "Ağ geçidi VIP" adresi hello sunucusu nereye yerleştirilir hello belirli veri merkezinde böylece adlı toohello işaret eder.

Hello VIP (sanal IP adresi), durum bilgisiz ağ geçidi hizmetler koleksiyonu vardır. Genel olarak, birden çok veri kaynağı arasında (ana veritabanı, kullanıcı veritabanı, vb.) gerekli koordinasyon olduğunda ağ geçitleri dahil. Ağ Geçidi Hizmetleri hello aşağıdakileri uygulayın:
-   **TDS bağlantı proxy.** Bu kullanıcı veritabanı hello arka uç kümesinde bulma, hello oturum açma sırası uygulama ve hello TDS paketleri toohello arka uç ve arka iletme içerir.

-   **Veritabanı yönetimi.** Bu iş akışları toodo CREATE/ALTER/DROP veritabanı işlemlerden uygulama içerir. Merhaba veritabanı işlemleri algılaması TDS paketleri veya açık OData API tarafından çağrılabilir.

-   CREATE/ALTER/DROP oturum açma/kullanıcı işlemleri

-   OData API aracılığıyla mantıksal sunucu yönetimi işlemleri

![Ağ topolojisi yalıtımı](./media/azure-isolation/azure-isolation-fig12.png)

Merhaba katmanı hello ağ geçitleri arkasında "arka uç" adı verilir. Yüksek oranda kullanılabilir bir şekilde tüm hello verilerin depolandığı budur. Her veri parçası olan konusu toobelong tooa "Bölüm" veya "Yük devretme birimi", her birinin en az üç çoğaltmaları sahip. Çoğaltmaları depolanan ve SQL Server altyapısı tarafından çoğaltılır ve yük devretme genellikle adlandırılan sistem tooas "doku" tarafından yönetilir.

Genellikle, hello arka uç sistem giden tooother sistemleri bir güvenlik önlemi olarak iletişim kurmaz. Ayrılmış toohello sistemleri hello ön uç (ağ geçidi) katmanındaki budur. Merhaba ağ geçidi katman makinelerde savunma mekanizması olarak sınırlı hello arka uç makineler toominimize hello saldırı yüzeyinde ayrıcalıklarına sahip.

### <a name="isolation-by-machine-function-and-access"></a>Yalıtım makine işlevi ve erişim
SQL Azure (başka bir makine işlevler üzerinde çalışan hizmetleri oluşur. "Arka uç" bulut veritabanı ve trafik yalnızca giderek arka uç giriş ve çıkışı değil, hello genel ilkesine sahip "ön uç" (ağ geçidi/Yönetimi) ortamları SQL Azure ayrılmıştır. Merhaba ön uç ortamı dışındaki diğer hizmetlerin world toohello iletişim kurabilir ve genel olarak, sadece (yeterli toocall hello girişi onu, gereksinimlerini tooinvoke'noktaları) hello uç izinler sınırlı.

## <a name="networking-isolation"></a>Ağ yalıtımı
Azure dağıtımı, ağ yalıtımı çok katmanlı sahiptir. Merhaba Aşağıdaki diyagramda Azure toocustomers sağlayan ağ yalıtımı çeşitli katmanları gösterilmektedir. Bu, hem yerel hello Azure platformu kendisi de hem de müşteri tarafından tanımlanan özellikler katmanlardır. Gelen hello Internet Azure DDoS Azure karşı büyük ölçekli saldırılarına karşı yalıtım sağlar. Merhaba sonraki yalıtım hangi trafiğin hello bulut hizmeti toohello sanal ağ üzerinden geçebilmesi kullanılan toodetermine olan müşteri tanımlı genel IP adresleri (Bitiş) katmanıdır. Yerel Azure sanal ağ yalıtımı diğer ağlarla tam yalıtımı sağlar ve trafik yalnızca yapılandırılan kullanıcı yolları ve yöntemleri akar. Bu yolları ve yöntemleri Nsg'ler, UDR ve ağ sanal Gereçleri kullanılan toocreate yalıtım sınırlarını tooprotect hello uygulama dağıtımları korumalı hello ağındaki burada olabilir hello İleri, katmandır.

![Ağ yalıtımı](./media/azure-isolation/azure-isolation-fig13.png)

**Trafik yalıtımı:** A [sanal ağ](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) hello trafik yalıtımı sınırıdır'hello Azure platformu üzerinde. Farklı bir sanal ağ, her iki sanal ağ tarafından oluşturulan olsa bile tooVMs aynı müşteri hello doğrudan bir sanal ağdaki sanal makinelerden (VM'ler) iletişim kuramıyor. Yalıtım müşteri sanal makineleri sağlar önemli bir özelliktir ve iletişim bir sanal ağ içindeki özel kalır.

[Alt ağ](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#subnets) IP aralığı tabanlı sanal ağ yalıtımı ile bir ek katmanı sunar. Merhaba sanal ağdaki IP adresleri, birden çok alt ağı organizasyon ve güvenlik için sanal bir ağa bölebilirsiniz. VM'ler ve PaaS rol örnekleri dağıtılan toosubnets (aynı veya farklı) bir sanal ağ içindeki ek bir yapılandırma gerektirmeden birbirleriyle iletişim kurabilir. Ayrıca yapılandırabilirsiniz [ağ güvenlik grubu (Nsg'ler)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#network-security-groups-nsg) tooallow veya ağ trafiği tooa VM örnek tabanlı erişim denetimi listesinde NSG (ACL) yapılandırılmış kurallarında reddedin. NSG'ler alt ağlarla veya bu alt ağların içindeki tekil VM örnekleriyle ilişkili olabilir. Bir NSG'yi bir alt ağ ile ilişkili olduğunda hello ACL kuralları bu alt ağdaki tooall hello VM örnekleri uygulayın.

## <a name="next-steps"></a>Sonraki Adımlar

- [Ağ yalıtımı seçenekleri makineler Windows için Azure sanal ağlar](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/)

Burada makineler belirli arka uç ağ veya alt ağ yalnızca belirli istemciler veya IP adreslerini beyaz üzerinde bağlı diğer bilgisayarlara tooconnect tooa belirli uç nokta izin verebilir hello Klasik ön uç ve arka uç senaryo içerir.

- [Yalıtım işlem](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure, geniş işlem örnekleri içeren bir çeşitli bulut tabanlı bilgi işlem hizmetler & otomatik olarak toomeet hello ihtiyaçlarını uygulamanızı veya Kurumsal yukarı ve aşağı ölçeklenebilen hizmetleri sağlar.

- [Depolama ayırma](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure müşteri hesaplama VM tabanlı depolama biriminden ayırır. Bu ayrım hesaplama ve depolama tooscale bağımsız olarak, daha kolay tooprovide çoklu kiracı ve yalıtım hale sağlar. Bu nedenle, Azure Storage yok ağ bağlantısı tooAzure ile ayrı donanımda dışında mantıksal işlem çalışır. HTTP ya da Müşteri'nin tercihine bağlı HTTPS üzerinden tüm istekleri çalıştırın.


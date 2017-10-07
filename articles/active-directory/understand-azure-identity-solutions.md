---
title: aaaUnderstand Azure kimlik | Microsoft Docs
description: "Microsoft Azure kimlik çözümü koşulları, kavramlar ve öneriler, toomake hello en iyi Kimlik Yönetimi kararı, kuruluşunuz için temel bir anlayış alın."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/17/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4d9c90bd7a6bcc9637be3107998f9da5bd4cbdae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-identity-solutions"></a>Azure kimlik çözümleri anlama
Microsoft Azure Active Directory (Azure AD) dizin hizmetleri, kimlik yönetimi ve uygulamaya erişim yönetimi sağlayan bir kimlik ve erişim yönetimi bulut çözümüdür. Azure AD hızla [çoklu oturum açma (SSO) etkinleştirir](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-sso) too1, 000 ait hello önceden tümleştirilmiş ticari ve özel uygulamaların [Azure AD uygulama galerisinde](https://azure.microsoft.com/marketplace/active-directory/all/). Çoğu bu uygulamaların, büyük olasılıkla zaten Office 365, Salesforce.com, kutusunu, ServiceNow ve Workday gibi kullanın.

Tek bir oluşturulduğunda Azure AD dizini otomatik olarak bir Azure aboneliğiyle ilişkili. Azure'da Hello kimlik hizmet olarak sonra Azure AD bulut tabanlı kaynaklar için tüm kimlik yönetimi ve erişim denetim işlevleri sağlar. Bu kaynaklar kullanıcılar, uygulamalara ve grupları tek bir kiracıya (kuruluş) için hello Aşağıdaki diyagramda gösterildiği gibi içerebilir:

![Azure Active Directory](./media/understand-azure-identity-solutions/azure-ad.png)

Microsoft Azure tek tek kuruluşunuzun ihtiyaçlarına karmaşıklık toomeet değişen düzeylerde service (Idaas) çeşitli şekillerde tooleverage kimlik sunar. Merhaba, bu makalenin kalanında, toomake hello en iyi seçim'hello kullanılabilir seçenekler için öneriler yanı sıra temel Azure kimlik terminolojisi ve kavramları anlamanıza yardımcı olur.

## <a name="terms-tooknow"></a>Koşulları tooknow

Kuruluşunuz için Azure kimlik çözümünü karar verebilirsiniz önce hello koşulları Azure kimlik hizmetleri hakkında konuşurken sık kullanılan temel bir anlayış gerekir.

|Terim tooknow| Açıklama|
|-----|-----|
|Azure aboneliği |Abonelikleri Azure bulut Hizmetleri için kullanılan toopay ve genellikle bağlantılı tooa kredi kartı. Birden fazla abonelik olabilir, ancak zor tooshare kaynakları abonelikler arasında olabilir.|
|Azure Kiracı | Azure AD kiracısı tek bir kuruluşun temsilcisidir. Kuruluş Azure, Intune veya Office 365 gibi Microsoft bulut hizmeti aboneliği kaydolduğunda, otomatik olarak oluşturulan Azure AD ayrılmış, güvenilen bir örneği değil. Kiracılar erişim tooservices ya da bir ortamda ayrılmış (tek kiracılı) veya diğer kuruluşlarla (çok kullanıcılı) paylaşılan bir ortamda elde edebilirsiniz.|
|Azure AD dizini | Her bir Azure Kiracı ayrılmış, güvenilen bir Azure sahip hello kiracının kullanıcılar, gruplar ve uygulamalar içeren AD dizini. Bu, Kiracı kaynaklarına kullanılan tooperform kimlik ve erişim yönetimi işlevleri olur. Çünkü benzersiz bir Azure AD dizini olan otomatik olarak sağlanan toorepresent Azure, Microsoft Intune veya Office 365 gibi Microsoft bulut hizmeti için kaydolduğunuzda, kuruluşunuz hello koşulları bazen görürsünüz *Kiracı*, *Azure AD*, ve *Azure AD dizini* birbirinin yerine kullanılır. |
|Özel etki alanı | Önce bir Microsoft bulut hizmeti aboneliği için kaydolduğunuzda, kiracınız (kuruluş) kullanan bir *. onmicrosoft.com* etki alanı adı. Bununla birlikte, çoğu kuruluşun kullanılan toodo iş ve son kullanıcıların tooaccess şirket kaynaklarını kullanmak bir veya daha fazla etki alanı adları vardır. Özel etki alanı adı tooAzure AD ekleyebilirsiniz, böylece Hello etki alanı adı tanıdık tooyour kullanıcılar, olduğu gibi  *alice@contoso.com*  yerine  *alice@contoso.onmicrosoft.com* . |
|Azure AD hesabı | Azure AD kullanarak oluşturulan kimlikleri bunlar veya Office 365 gibi başka bir Microsoft bulut hizmeti. Azure AD'de depolanan ve hello kuruluşunuzun bulut hizmeti aboneliklerinizde, erişilebilir tooany. |
|Azure Abonelik Yöneticisi| Merhaba Hesap Yöneticisi kaydolup veya hello Azure aboneliği satın hello kullanıcıdır. Merhaba kullanabileceklerini [hesap Merkezi'nde](https://account.windowsazure.com/Home/Index) tooperform çeşitli yönetim görevlerini abonelikleri oluşturma, aboneliklerinizi iptal edin, bir abonelik için hello fatura değiştirmek veya değiştirme gibi hello Hizmet Yöneticisi. |
|Azure AD genel yönetici | Azure AD genel Yöneticiler tam erişim tooall Azure AD yönetim özelliklerine sahiptir. bir Microsoft bulut hizmeti aboneliği için otomatik olarak kaydolduğunda hello kişiye varsayılan olarak genel yönetici olur. Birden çok genel yönetici olabilir, ancak yalnızca genel Yöneticiler herhangi birini atayabilirsiniz [diğer yönetici rollerini hello](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) toousers. |
|Microsoft hesabı | Microsoft hesapları (tarafından kişisel kullanım için oluşturduğunuz) erişim tooconsumer yönelik Microsoft ürünleri sağlayın ve Outlook (Hotmail), OneDrive, Xbox LIVE veya Office 365 gibi hizmetler bulut. Bu kimlikleri oluşturulur ve hello Microsoft tarafından çalıştırılan Microsoft tüketici kimlik hesap sistemi depolanır.|
|İş veya Okul hesapları | İş veya Okul hesapları (iş/akademik kullanmak için bir yönetici tarafından verilen) tooenterprise iş düzeyinde gibi Microsoft bulut Hizmetleri, Azure, Intune veya Office 365 erişim sağlar.|


## <a name="concepts-toounderstand"></a>Kavramları toounderstand

Merhaba temel Azure kimlik koşulları bildiğinize göre bunlar hakkında daha fazla bilgi yardımcı Azure kimlik kavramları hakkında bilgi sahibi Azure kimlik hizmet karar olun.

|Kavram toounderstand |Açıklama|
|-----|-----|
|[Azure aboneliklerinin Azure Active Directory ile ilişkisi](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) |Her Azure aboneliği bir Azure ile bir güven ilişkisine sahip AD directory tooauthenticate kullanıcılar, hizmetler ve cihazlar. *Birden çok abonelik hello aynı Azure AD directory güvenebilir ancak bir abonelik yalnızca tek bir güvenecek Azure AD dizini*. Bu güven ilişkisi, daha fazla abonelik alt kaynakları gibi diğer Azure kaynaklarının (Web siteleri, veritabanları ve benzeri) sahip bir aboneliğe sahip hello ilişki benzemez. Bir aboneliğin süresi dolarsa Azure AD dışında hello aboneliğiyle ilişkili erişim tooresources de durdurulur. Ancak, siz de başka bir aboneliği bu dizinle ilişkilendirebilir ve toomanage Kiracı kaynaklarına devam hello Azure AD dizin Azure içinde kalır.|
|[Works lisanslama nasıl Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-get-started-azure-portal) | Ne zaman satın alma veya Enterprise Mobility Suite, Azure AD Premium veya Azure AD temel, dizininize etkinleştirme geçerlilik süresinin dahil olmak üzere hello abonelikle güncelleştirilir ve lisansları ön ödemeli. Merhaba abonelik etkinleştirildikten sonra hello hizmeti Azure AD genel yönetici tarafından yönetilen ve lisanslı kullanıcılar tarafından kullanılır. Merhaba atanan veya kullanılabilir lisans sayısı gibi abonelik bilgilerinizi hello hello Azure portalından kullanılabilir **Azure Active Directory** > **lisansları** dikey. Bu olduğunu da hello en iyi yeri toomanage lisans atamalarınızı.|
|[Hello Azure portalı içinde rol tabanlı erişim denetimi](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)|Azure rol tabanlı erişim denetimi (RBAC) Azure kaynakları için ayrıntılı erişim yönetimini sağlamaya yardımcı olur. Çok fazla izinler, kullanıma ve tooattackers hesap. Çok az izinleri anlamına gelir çalışanlar verimli bir şekilde işlerini alınamıyor. RBAC kullanarak, çalışanların tooall kaynak grupları uygulanan üç temel rollere göre ihtiyaç duydukları hello tam izinleri verebilirsiniz: sahibi, katkıda bulunan, okuyucu. Too2, kendi 000 oluşturabilirsiniz [özel RBAC rolleri](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) özel toomeet gerekiyor. |
|[Karma kimlik](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)|Karma kimlik elde edilir, şirket içi Windows Server Active Directory (AD DS) ile tümleştirerek Azure AD kullanarak [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). Kullanıcılarınız Office 365, Azure ve şirket içi uygulamalar veya SaaS uygulamaları için ortak bir kimlik Azure AD ile tümleşik tooprovide sağlar. Karma kimlik ile etkili bir şekilde ortamı toohello bulut kimlik ve erişim için şirket içi genişletir.|

### <a name="hello-difference-between-windows-server-ad-ds-and-azure-ad"></a>Windows Server AD DS ve Azure AD arasındaki Hello fark
Azure Active Directory (Azure AD) ve şirket içi Active Directory (Active Directory etki alanı Hizmetleri veya AD DS), dizin verilerini depolar ve kullanıcılar ve kullanıcı oturum açma işlemleri, kimlik ve dizin aramaları gibi kaynakları arasındaki iletişimi yönetme sistemleridir.

Zaten şirket içi Windows Server Active Directory etki alanı Hizmetleri ile (AD DS) biliyorsanız, büyük olasılıkla bir kimlik hizmeti temel kavramı hello anlamak daha sonra ilk Windows 2000 Server ile kullanıma sunuldu. Ancak, önemli toounderstand Azure AD yalnızca bir etki alanı denetleyicisi hello bulutta değil de olabilir. Identity service (Idaas) sağlama tamamen yeni bir yol, tamamen yeni bir yol bulut tabanlı düşünmeye toofully embrace yeteneklerini gerektirir ve kuruluşunuzun modern tehditlere karşı korumaya Azure ayarlanır. 

AD DS, Windows Server'da, fiziksel veya sanal makinelerde dağıtılabilir anlamına gelir, bir sunucu rolüdür. Üzerinde X.500 göre hiyerarşik bir yapı vardır. Nesneleri bulmak bulunulması LDAP kullanarak ve birincil kimlik doğrulaması için Kerberos kullanan DNS kullanır. Ayrıca Active Directory etkinleştirir kuruluş birimlerini (OU) ve Grup İlkesi nesneleri (GPO'lar) toojoining makineler toohello etki alanı ve güvenler etki alanları arasında oluşturulur.

BT kendi güvenlik çevre AD DS kullanılarak yıl, ancak çalışanlar, müşterileri ve ortakları yeni bir denetim düzlemi olabilmesi kimlik gereksinimlerini destekleyen modern, çevre-daha küçük kuruluşlar için korumalı. Azure AD, kimlik denetim Düzlemi ' dir. Güvenlik, burada Azure AD şirket kaynaklarına ve korur erişim kullanıcılar için ortak bir kimlik sağlayarak hello Kurumsal güvenlik duvarı toohello bulut ötesinde taşındı (ya da şirket içi veya hello bulutta). Bu, kullanıcıların hello esneklik toosecurely tooget neredeyse her aygıttan işlerini gereksinim duydukları erişim hello uygulamaları sağlar. Sorunsuz risk tabanlı veri koruması denetimleri, Machine learning yetenekleri ve kapsamlı raporlama tarafından yedeklenen verileri güvenli o BT gereksinimlerini tookeep şirket de sağlanır.

Azure AD içinde Azure AD bulut sunucuları ve Office 365 gibi uygulamalar için bir kiracı oluşturabileceğiniz anlamına gelir çoklu müşteri ortak dizin hizmetidir. Kullanıcılar ve gruplar, düz bir yapı OU veya GPO'ları olmadan oluşturulur. Kimlik doğrulaması, SAML gibi protokoller üzerinden gerçekleştirilir WS-Federation ve OAuth. Olası tooquery Azure AD olduğu, ancak LDAP kullanmak yerine, AD grafik API'si olarak adlandırılan bir REST API'si kullanmanız gerekir. Bu tüm iş HTTP ve HTTPS.

### <a name="extend-office-365-management-and-security-capabilities"></a>Office 365 Yönetim ve güvenlik yetenekleri genişletme
Zaten Office 365 kullanıyor? Sayısal dönüşüm tüm iş gücüne yönelik güvenli üretkenliği etkinleştirirken, kaynaklarınızı Azure AD toosecure yerleşik Office 365 özellikleriyle genişleterek hızlandırabilir. Ayrıca tooOffice 365 özellikleri, Azure AD kullandığınızda, tüm uygulama Portföy tüm uygulamalar için çoklu oturum açmayı etkinleştiren bir kimlikle alabilecek. Yalnızca cihaz durumu, ancak kullanıcı, konum, uygulama ve risk de göre koşullu erişim özelliklerinizi genişletebilirsiniz. Gerektiğinde çok faktörlü kimlik doğrulama (MFA) özellikleri daha da fazla koruma sağlar. Kullanıcı ayrıcalıkları, ek gözetim elde ve isteğe bağlı, yalnızca zaman yönetimsel erişim sağlar. Kullanıcılarınızın daha üretken ve daha az Yardım Masası biletleri oluşturan, teşekkürler toohello Self Servis kapasitelerini Azure AD unutulmuş parola, uygulama erişim isteklerini sıfırlama ve grup oluşturma ve yönetme gibi sağlar.

> [!TIP]
> Office 365 ile Azure AD Kimlik Yönetimi'ni kullanma hakkında daha fazla toolearn istiyorsunuz? [Merhaba e-kitap almak](https://info.microsoft.com/Extend-Office-365-security-with-EMS.html).

## <a name="microsoft-azure-identity-solutions"></a>Microsoft Azure kimlik çözümleri

Microsoft Azure bunlar korunur olup olmadığını bu çeşitli şekillerde toomanage, kullanıcıların kimliklerini sunar tam olarak şirket içi, yalnızca bulut hello ve hatta bir yere arasında. Bu seçenekler şunlardır: yazılanları (DIY) AD DS'de Azure, Azure Active Directory (Azure AD), karma kimlik ve Azure AD etki alanı Hizmetleri.

### <a name="do-it-yourself-diy-ad-ds"></a>Yazılanları (Dıy) AD DS
Merhaba bulut, yalnızca küçük bir yer ihtiyaç duyan şirketler için **yazılanları (DIY) AD DS** Azure içinde kullanılabilir. Bu seçenek Azure sanal makinelerde (VM'ler) olarak dağıtım için oldukça uygun olan birçok Windows Server AD DS senaryolarını destekler. Örneğin, bir Azure VM bağlı toohello uzak ağ olan bir uzak veri merkezinde çalışan bir etki alanı denetleyicisi olarak oluşturabilirsiniz. Buradan, hello VM mümkün toosupport uzak kullanıcıların kimlik doğrulama isteklerini olmalı ve kimlik doğrulama performansını iyileştiren. Bu seçenek ayrıca az sayıda etki alanı denetleyicileri ve Azure üzerinde tek bir sanal ağa barındırarak nispeten düşük maliyetli alternatif toootherwise maliyetli olağanüstü durum kurtarma siteler olarak iyi uygundur. Son olarak, Azure, Windows Server AD DS gerektirir, ancak hiçbir bağımlılık hello şirket içi ağda sahip SharePoint gibi bir uygulama toodeploy gerekir veya şirket Windows Server Active Directory hello. Bu durumda, ayrı bir ormanda Azure toomeet hello SharePoint sunucu grubuna ait gereksinimleri dağıtabilirsiniz. Ayrıca bağlantı toohello şirket içi ağ gerektiren toodeploy ağ uygulamalar desteklenen ve hello içi Active Directory.

### <a name="azure-active-directory-azure-ad"></a>Azure Active Directory (Azure AD)
**Azure AD tek başına** bir tam olarak bulut tabanlı kimlik ve erişim yönetimi Service (Idaas) çözümü olarak. Azure AD, bir dizi sağlam yetenekleri toomanage kullanıcılar ve gruplar sağlar. Güvenli erişim tooon içi ve bulut uygulamalarında hizmet (SaaS) uygulamaları olarak Office 365 ve birçok Microsoft olmayan yazılımlar gibi Microsoft web hizmetlerini de dahil olmak üzere, yardımcı olur. Azure AD gelen üç sürümlerinde: ücretsiz, temel ve Premium. Azure AD kuruluş verimliliğini artırır ve Gelişmiş güvenlik özelliklerini hello çevre güvenlik duvarı tooa yeni denetim düzlemi Azure machine learning tarafından korunan ve diğer güvenlik genişletir.

### <a name="hybrid-identity"></a>Karma kimlik
Şirket içi veya bulut tabanlı kimlik çözümleri arasında seçim yapın yerine birçok İleri düşünmeye Cıo'lar ve şirketin uzun vadeli yönü bekleme başlamıştır, işletmeler, şirket içi dizinleri toohello bulut üzerindengenişletme**karma kimlik** çözümler. Karma kimlik ile kullanan müşteriler tamamıyla küresel bir kimliği alma ve toohello uygulamaları kullanıcılara güvenli ve verimli erişim sağlayan erişim yönetimi çözümü işlerini toodo gerekir.

> [!TIP]
> toolearn hakkında daha fazla bilgi CIO Azure Active Directory kendi BT stratejilerini merkezi bir parçası yapmış olduğunuz nasıl hello karşıdan [CIO'ın Kılavuzu tooAzure Active Directory](https://aka.ms/AzureADCIOGuide).

### <a name="azure-ad-domain-services"></a>Azure AD Domain Services
**Azure AD etki alanı Hizmetleri** ağ uygulama geliştirme ve test amacıyla bir bulut tabanlı seçeneği toouse AD DS basit Azure VM yapılandırma denetimi ve bir şekilde toomeet için şirket içi kimlik gereksinimleri sağlar. Azure AD etki alanı Hizmetleri toolift değildir ve şirket içi shift AD DS altyapı tooAzure VM'ler Azure AD etki alanı Hizmetleri tarafından yönetilir. Bunun yerine, hello Azure VM'ler yönetilen etki alanlarında kullanılan toosupport hello geliştirme, test ve AD DS kimlik doğrulama yöntemleri toohello bulut gerektiren şirket içi uygulamalar hareketini olmalıdır.

## <a name="common-scenarios-and-recommendations"></a>Yaygın senaryolar ve öneriler

Toowhich Azure kimlik seçeneği her biri için en uygun olabileceği bazı öneriler ortak kimlik ve erişim senaryolar verilmiştir.

|Kimlik senaryosu| Öneri|
|-----|-----|
|Kuruluşumun içi Windows Server Active Directory içinde büyük yatırımlar yaptı, ancak tooextend kimlik toohello bulut istiyoruz.| en yaygın olarak kullanılan hello Azure kimlik çözümüdür [karma kimlik](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Zaten Yatırımlar şirket içi AD DS yaptıysanız, Azure AD Connect'i kullanarak kimlik toohello bulut kolayca genişletebilirsiniz.|
|İşimi hello bulutta doğdu ve şirket içi kimlik çözümleri hiçbir Yatırımlar sunuyoruz.| [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) hiçbir yalnızca bulut işletmeler için en iyi seçim hello şirket içi Yatırımlar.|
|Uygulama geliştirme ve test amacıyla basit Azure VM yapılandırması ve denetim toomeet şirket içi kimlik gereksinimleri ihtiyacım.|[Azure AD etki alanı Hizmetleri](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) toouse AD DS için basit Azure VM yapılandırma denetimi gerekir veya toodevelop aradığınız veya eski, dizin kullanan şirket içi uygulamalar toohello bulut geçirmek iyi bir seçimdir.|  
|Azure'daki bazı sanal makinelerde toosupport ihtiyacım, ancak Şirketim hala yoğun bir şekilde şirket içi Active Directory (AD DS) yatırım.|Kullanım [Dıy AD DS](https://msdn.microsoft.com/library/azure/jj156090.aspx) toouse Azure Vm'leri toosupport birkaç sanal makinelerin gerekir ve büyük AD DS Yatırımlar içi zamanı. |

## <a name="where-can-i-learn-more"></a>Burada daha fazla bilgi edinebilirsiniz?
Tüm Azure AD hakkında bilgi edinin harika kaynakları çevrimiçi toohelp çok sunuyoruz. Başlattığınız harika makaleleri tooget listesi aşağıdadır:

* [Dizininizi Azure AD Connect ile karma yönetimi için etkinleştirme](active-directory-aadconnect.md)
* [Şimdiye kadar bağlı dünya için ek güvenlik](../multi-factor-authentication/multi-factor-authentication.md)
* [Kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS Azure Active Directory ile uygulamaları otomatikleştirme](active-directory-saas-app-provisioning.md)
* [Azure AD Raporlama ile çalışmaya başlama](active-directory-reporting-getting-started.md)
* [Her yerden, parolaları yönetme](active-directory-passwords.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS Azure Active Directory ile uygulamaları otomatikleştirme](active-directory-saas-app-provisioning.md)
* [Nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamalar](active-directory-application-proxy-get-started.md)
* [Azure Active Directory grupları ile erişim tooresources yönetme](active-directory-manage-groups.md)
* [Hangi Microsoft Azure Active Directory lisanslaması nedir?](active-directory-licensing-what-is.md)
* [Nasıl ı Kuruluşum içinde kullanılan onaylanmamış bulut uygulamaları bulabilir](active-directory-cloudappdiscovery-whatis.md)

## <a name="next-steps"></a>Sonraki adımlar

Azure kimlik kavramları ve hello seçenekleri kullanılabilir tooyou anladığınıza göre seçtiğiniz kaynaklar başlatılan tooget uygulayan hello seçeneğini aşağıdaki hello kullanabilirsiniz:

[Azure karma kimlik çözümleri hakkında daha fazla bilgi edinin](https://docs.microsoft.com/azure/active-directory/choose-hybrid-identity-solution)

[Bir Azure kavram kanıtı ortamda daha fazla bilgi edinin](https://aka.ms/aad-poc)

[Üretimde Azure AD dağıtma](https://aka.ms/aad-onboard)

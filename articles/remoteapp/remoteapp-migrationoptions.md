---
title: "Azure RemoteApp geçirmek için aaaOptions | Microsoft Docs"
description: "Azure RemoteApp geçirmeye hello seçenekleri hakkında bilgi edinin."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a>Azure RemoteApp geçiş seçenekleri
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.


Hello nedeniyle Azure RemoteApp kullanarak durduruldu durumunda [devre dışı bırakma Duyurusu](https://go.microsoft.com/fwlink/?linkid=821148) veya değerlendirmeniz bitirdikten sonra olduğundan, Azure RemoteApp tooanother uygulama hizmeti dışına toomigrate gerekir. Geçirmek için iki farklı yaklaşım vardır: bir kendi kendine yönetilen (genellikle [Iaas] hizmet olarak altyapı olarak adlandırılır) bir tam olarak yönetilen (genellikle çağrılan hizmet olarak Platform) veya [PaaS/SaaS] hizmet olarak yazılım dağıtımı veya sunar. 

Self Servis Iaas olan yönetilen işletilen ve dağıttığınız, doğrudan sanal makineleri (VM'ler) veya fiziksel sistemleri tarafından sahip olunan yazılanları bir dağıtımıdır. Merhaba diğer end, bir tam olarak yönetilen PaaS/olduğundan daha fazla Azure RemoteApp ister - iş ortağı işlemsel işleme remoting çözüm üzerinde bir hizmet katmanı sağlar sunumu SaaS ve hizmet verme sırasında hello müşterisi olarak, bazı görüntü ve uygulama yönetimi bunu.

[Geçiş seçenekleri hello Azure RemoteApp Web Seminerlerini görüntüleyebilir](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), veya (Merhaba seçenekleri barındırma farklı örnekleri dahil) daha fazla bilgi için okumaya devam edin.

## <a name="self-managed-iaas-solutions"></a>Kendi kendine yönetilen (Iaas) çözümleri
### <a name="rds-on-iaas"></a>**RDS Iaas üzerinde**
RemoteApp veya Masaüstü şirket içi kullanarak bir yerel oturum tabanlı (Windows Server)'deki Uzak Masaüstü Hizmetleri dağıtımı dağıtabilir veya barındırılan bir ortamda (like Azure vm'lerinde). RDS Iaas dağıtımlarda zaten aşina müşteriler için en iyi ve RDS dağıtımlar ile var olan teknik uzmanlığı olan. 

> [!NOTE]
> Toplu Lisanslama Yazılım Güvencesi (SA) ile RDS istemci erişim lisansları toouse için bu dağıtım seçeneğini gerekir.

Azure vm'lerinde RDS dağıtma sürekli dağıtımı ve şablonları düzeltme eki uygulama kullandığınızda, daha kolay (okuma bir [genel bakış](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) ve ardından [bunları getirmek Git](https://aka.ms/rdautomation)). Merhaba hello kullanarak Azure RemoteApp içinde Azure Klasik dağıtım modeli kaynakları (Azure kaynak modeli kaynakları değil) ile aynı esnek ölçeklendirme özelliklerinden elde edebilirsiniz [otomatik komut dosyası ölçeklendirme](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), büyük/küçük vardır, ancak daha fazla Özelleştirmeleri ve yapılandırmaları. Azure vm'lerinde RDS dağıttığınızda, Destek aracılığıyla sağlanır [Azure Destek](https://azure.microsoft.com/support/plans/), hello Azure RemoteApp ile desteklenen aynı destek uzmanları. İle iletişim kurarak mevcut kullanımınıza bağlı alarak tahmin maliyeti olabilir [Azure Destek](https://azure.microsoft.com/support/plans/), veya kendiniz hesaplamalar gerçekleştirebilir kullanarak bir en kısa sürede toobe maliyet hesaplayıcı yayımlanan.  Ayrıca, N-serisi Vm'lerde (şu anda özel olarak incelenmektedir) ile vGPU - ekleyebilirsiniz ve vGPU ekleme hakkında daha fazla çok duymak[kadar yararlanmak istiyorsanız, Windows Server 2016 RDS yenilikleri](https://myignite.microsoft.com/videos/2794) bizim Ignite oturumunda.   

Adım adım dağıtım kılavuzları için sahip olduğumuz [Windows Server 2012 R2](http://aka.ms/rdsonazure) ve [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist dağıtımınız ile. Merhaba denetleyin [Uzak Masaüstü blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) hello en son haberler için.

### <a name="citrix-on-iaas"></a>**Citrix Iaas üzerinde**
Şirket içi dağıtımı oturum tabanlı XenApp ya da XenDesktop olabilir yerel bir Citrix dağıtılmış veya barındırılan bir ortamda içinde (gibi Azure vm'lerinde). 

Merhaba adım adım Dağıtım Kılavuzu'na göz, denetleme [Citrix XA 7.6 Azure üzerinde](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), daha fazla bilgi için. Daha fazla bilgi edinin [Citrix Azure üzerinde](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), fiyat hesaplayıcısını dahil olmak üzere. Bulabileceğiniz bir [Citrix kişi](http://citrix.com/English/contact/index.asp) toodiscuss seçeneklerinizi ile.

## <a name="fully-managed-paassaas-offerings"></a>Tam olarak yönetilen (PaaS/SaaS) teklifleri

### <a name="citrix-xenapp-essentials-released-april-2017"></a>Citrix XenApp (Nisan 2017 yayımlanan) Temelleri
Merhaba üzerinde şu anda kullanılabilir [Azure Marketi](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials hizmettir hello yeni uygulama sanallaştırma, hello güç birleştirme ve esnekliğini hello hello basit, düzenleyici, Citrix bulut platformu ve Microsoft Azure RemoteApp görme kolay kullanabilir. 

Var olan Azure RemoteApp müşterileri için [ücretsiz deneme için kayıt](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).  Not: Yalnızca Citrix kullanıcı servis ücreti ücretsizdir, Azure işlem ve depolama ücretleri

Daha fazla bilgi edinin:
- [Azure RemoteApp tooCitrix XenApp Essentials ' geçiş](remoteapp-migrate-citrix.md)
- [Citrix ve Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- [Citrix XenApp Essentials sunu](https://www.youtube.com/watch?v=91Z7CCfQ-9k).  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a>Citrix bulut XenApp hizmeti ve XenDesktop hizmeti 

[Citrix bulut XenApp hizmeti ve XenDesktop hizmeti](https://www.citrix.com/products/citrix-cloud/services.html) hello teslimini hem uygulamalar ve masaüstü bilgisayarlar, artı Gelişmiş Yönetim ve izleme kapasiteleri için hello en iyi çözümdür. 

#### <a name="conexlink-platform-name-mycloudit"></a>Conexlink (Platform ad: MyCloudIT)
[MyCloudIT](https://mycloudit.com) bir Otomasyon platformudur BT şirketler toosimplify için en iyi duruma getirme ve ölçeklendirme hello geçiş ve Uzak Masaüstü, uzak uygulamaları ve altyapısında teslimini hello Microsoft Azure bulut. 

Merhaba MyCloudIT platform % 95, 30 oranında maliyeti Azure tarafından dağıtım süresini azaltır ve bunların istemcinin tüm BT altyapı sağlasa da, birkaç tuş vuruşlarını hello buluta taşır. İş ortakları bir genel panodan müşteriler artık yönetebilir, hizmet son kullanıcıların Merhaba Dünya bambaşka ister ve ek yükü veya Azure kapsamlı eğitim eklemeden gelirleri büyümesine.  

> Birincil konumu: Dallas, TX, ABD
> 
> İşlemi bölgesi: dünya çapında
> 
> İş ortağı, durum: [altın](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)
> 
> Microsoft bulut hizmeti sağlayıcısı: Evet
> 
> Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi
> 
> Azure RemoteApp geçiş çözümleri: Evet, [daha fazla bilgi edinin](https://mycloudit.com/remote-app-microsoft/)
> 
> Brian Garoutte, VP iş geliştirme
> 
> Telefon: 972-218-0741
>   
> E-posta:[brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)

### <a name="frame"></a>Çerçeve

BT kuruluşları Kurumsal ve resmi, yönetilen hizmet sağlayıcıları ve önde gelen yazılım satıcıları çerçeve toocreate seçin ve kendi güvenli, yazılım tanımlı çalışma hello bulutta yönetin. Küçük toolarge kuruluşlardan çerçeve son derece kolay toolet kullanıcılar kolaylaştırır herhangi bir tarayıcıda Windows uygulamaları herhangi bir aygıttan erişim. Merhaba çerçeve platform her şeyi hello bulut hello Azure altyapı ve RDS lisansları dahil olmak üzere bir yönetim gereksinimlerini toodeploy uygulamalardan içeren (kendi Azure hesabı ve lisansları getiren isteğe bağlı). 

Daha fazla bilgi edinmek [Azure çerçevesi](https://www.fra.me/ara). 

> Birincil konumu: San Mateo, CA, ABD
>
> İşlemi bölgesi: dünya çapında
>
> Microsoft iş ortağı: Evet
> 
> Telefon: 1-480-269-4668

### <a name="awingu"></a>Awingu
Awingu eski uygulamalar, SaaS ve belgeleri bir html5 tarayıcıdan çalıştıran bir basit çevrimiçi çalışma çözümü sağlar. Bu nedenle, tüm uygulamaları güvenli bir şekilde kullanılabilir cihaz herhangi bir türde hale getirme. SaaS Hizmetleri için çoklu oturum açma çeşitli op seçenekleri kullanılabilir. Ayrıca farklı (bulut) dosya sistemleri iç çalışma alanınıza tümleştirilebilir. Sonraki toofull mobility (örneğin indirme/karşıya), ayrıntılı denetimler ile tam kullanımını denetleme, çok faktörlü kimlik doğrulaması (örneğin, Azure MFA), oturum kaydı ve daha fazlasını en iyi güvenlik Awingu'nın zengin çevrimiçi çalışma verin. Out-of--box, belge ve en iyi duruma getirilmiş ve güvenli işbirliği için uygulama paylaşım oturumu Awingu sağlar.
Awingu'nin, çok kiracılı, birden çok AD ve açık API çözümüdür. Küçük ve büyük işletmeler tarafından bulut hizmet sağlayıcılarının kullanılır ve [ISV'ler](http://www.isv2saas.com). Bu müşterilerden Merhaba, kullanımı kolay, özellikle yönetilmesinde kolaylığı yükleme ve düşük toplam sahip olma maliyeti.

Awingu hepsi bir arada olan [hello Azure Marketi'nde bulunan](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) 2 yerleşik eşzamanlı kullanıcılarla. Ek lisanslar aracılığıyla kullanılabilen bir [Dağıtıcıları ve yetkili satıcılar çeşitli](http://www.awingu.com/reseller).

Daha fazla bilgi edinmek [üzerinde Awingu alternatif tooAzure RemoteApp olarak](http://alternative-for-azure-remoteapp.awingu.com/).


> Birincil konumu: Belçika
> 
> Bölgeler işletim: EMEA, Kuzey Amerika ve Brezilya
> 
> Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi 
> 
> **Genel**:
> 
> Arnaud Marlière, CMO
> 
> E-posta:[arnaud@awingu.com](mailto:arnaud@awingu.com)
> 
> Telefon: +1 646 583 3025
> 
> **Belçika denetim merkezini**:
> 
> Ottergemsesteenweg Zuid 808 B44
> 
> 9000 Gent
> 
> E-posta:[info@awingu.com](mailto:info@awingu.com) 
> 
> Telefon: + 32 9 296 40 11
> 
> **ABD**:
> 
> 7 floor, hello Americas, 1177 Ave,
> 
> New York, NY 10036
> 
> E-posta:[info.us@awingu.com](mailto:info.us@awingu.com)

### <a name="microsoft-hosted-service-provider"></a>Microsoft hizmet sağlayıcısı barındırılan
Barındırma ortakları genellikle sunma tam olarak yönetilen Windows Masaüstü barındırılan ve yönetme içerebilir uygulama hizmeti hello Azure kaynaklarını, işletim sistemleri, uygulamaları ve Yardım Masası hello ortağı kullanarak Microsoft anlaşmalarıyla lisans ve bir hizmet sağlayıcısı lisans sözleşmenize tooallow abone erişim lisansı (SAL), satılması olan yanı sıra diğer yazılım sağlayıcıları. Merhaba aşağıdaki bilgileri ayrıntılarını ve bunların Azure RemoteApp geçiş müşterilerle yardımcı olarak specialize hello barındırıcıların bazıları için kişi bilgilerini sağlar. Kullanıma [hello geçerli barındırılan hizmet sağlayıcıların listesini](http://aka.ms/rdsonazurecertified) hello yolu ve değerlendirme öğrenme Iaas üzerinde RDS tamamlanmıştır.  

### <a name="citrix-service-provider-program"></a>Citrix hizmet sağlayıcısı programı
Merhaba Citrix hizmet sağlayıcısı programı tooSMBs bilgi işlem, bir kolay, Kullandıkça Öde modelinde istedikleri hello hizmetleri sunan sanal bulut hizmeti sağlayıcıları toodeliver hello basitliği kolaylaştırır. Citrix hizmet sağlayıcıları, Microsoft SPLA işlerini büyümesine ve kendi RDS platform Yatırımlar ile herhangi bir aygıtı genişletin, her yerden erişim, en geniş uygulama desteği, bir zengin deneyim, ek güvenlik ve daha yüksek ölçeklenebilirliği hello. Buna karşılık, Citrix hizmet sağlayıcıları daha fazla aboneleri çekebilir, müşteri memnuniyetini artırmak ve kendi işletim maliyetlerini düşürme. [Daha fazla bilgi edinin](http://www.citrix.com/products/service-providers.html) veya [bir iş ortağı bulmak](https://www.citrix.com/buy/partnerlocator.html).

#### <a name="acuutech"></a>Acuutech
[Acuutech](http://www.acuutech.com) tam masaüstü ve ISV uygulamaları teslim etmek barındırılan Masaüstü çözümleri sağlama uzmanlaşmış Microsoft teknolojisi tooa genel istemcide temel Azure ve kendi veri merkezlerini yerleşik deneyimleri.

> Birincil konumu: Londra, İngiltere; Singapur; Houston, TX
> 
> İşlemi bölgesi: dünya çapında
> 
> İş ortağı durumu: altın
> 
> Microsoft bulut hizmeti sağlayıcısı: Evet
> 
> Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi
> 
> Azure RemoteApp geçiş çözümleri: Evet, [daha fazla bilgi edinin](http://www.acuutech.com/ara-migration/)
> 
> **Birleşik Krallık**:
>   
> 5/6 York House, Langston yol,
>   
> Loughton, Essex IG10 3TQ
>   
> Telefon: + 44 (0) 20 8502 2155
> 
> **Singapur**:
>   
> 100 CECIL Sokak, #09-02, 
>   
> Merhaba Dünya, Singapur 069532
> 
> Telefon: + 65 6709 4933
>   
> **Kuzey Amerika**:
>   
> 3601 S. Sandman St.
>   
> Paketi 200, Houston, TX 77098
>   
> Telefon: +1 713 691 0800

#### <a name="aspex"></a>ASPEX
[ASPEX](http://www.aspex.be/en) toohello Bulut ve ISV geçiş ISV'ler içinde uzmanlaşmış ' toooptimize geçerli kendi bulut kurulumları aranıyor. ASPEX çok çeşitli yönetilen Hizmetleri, devops ve danışmanlık hizmetleri sunar.  

> Birincil konumu: Antwerp, Belçika
> 
> İşlemi bölgesi: Batı Avrupa
> 
> İş ortağı, durum: [Gümüş](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)
> 
> Microsoft bulut hizmeti sağlayıcısı: Evet
> 
> Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi
> 
> Azure RemoteApp geçiş çözümleri: Evet, [daha fazla bilgi edinin](https://www.aspex.be/en/azure-remote-apps)
> 
> Telefon: +3232202198
> 
> Posta:[info@aspex.be](mailto:info@aspex.be)
> 
> Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)

#### <a name="caasecom"></a>Caase.com
[Caase.com](http://www.caase.com/) işletmeler, yerel hükümetler, kamu olmayan gövdeleri ve bunların gezisine hello Microsoft Cloud iş daha verimli bir şekilde doğru sağlık kuruluşlarına yardımcı olur. Herhangi bir aygıt ile herhangi bir yerdeki ve düşük BT maliyetle güvenli ve verimli olması. Caase.com Microsoft Office365, Azure, Enterprise Mobility ve güvenlik ve Windows için doğru Uzmanı ' dir. Bizim danışmanlık firması, yükseltme Hizmetleri, benimseme programlar, eğitim ile yönetim ve Destek Caase.com işbirliği hem müşterilerin çalışanlar, iş ortakları ve hangi tedarikçilerin en iyi duruma getirilmiş ve güvenli bir platform oluşturur.
Caase.com hello beyin hello Azure uzak çalışma alanı (mobil çalışma alanı) ve hello dijital çalışma alanına (sosyal Intranet) olur. – Benimseme elde her iki çözüm – bu çözümlerin hello kullanıcılar kendi rota toohello Microsoft Cloud hello en eğlenceli, başarılı ve etkili deneyim sahibi olduğunuzu sağlayan hello temelidir.
Felemenkçe çeviri ánd burada üzerinden destekleyen bir filmi: http://caase.com/over-ons/

> İşlemi bölgesi: Felemenkçe bağlı olarak, genel erişim
> 
> İş ortağı, durum: [altın](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)
> 
> Microsoft bulut hizmeti sağlayıcısı: Evet
> 
> Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi
> 
> Azure RemoteApp geçiş çözümleri: Evet, [daha fazla bilgi edinin](http://caase.com/diensten/microsoft-azure/).
> 
> 
> Hollanda:
> 
> Rigtersbleek Zandvoort 10 (De Spinnerij)
> 
> 7521 BE, Enschede
> 
> Telefon: +31 (0) 88 4320 000


#### <a name="nerdio"></a>Nerdio
[Azure için Nerdio](http://getnerdio.com/nfa/) gerçekten basit sağlama, yönetim ve tam BT ortamları en iyi duruma getirilmesi hello Microsoft bulut sunan bir BT Otomasyon platformudur. Sanal Masaüstlerini, uzak uygulamalar ve sunucuları birkaç saat bekleyin. Üç tıklama Hello ortamında yönetmek veya Nerdio Yönetim Portalı ile daha az. Akıllı otomatik ölçeklendirme kullanın ve Azure Iaas kaynaklarında 40 too60% kaydedin.

> Birincil konumu: Chicago, IL işlemi bölgesi: dünya çapında iş ortağı durumu: [altın](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft bulut hizmeti sağlayıcısı: Evet
> 
> Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi
> 
> Azure RemoteApp geçiş çözümleri: Evet
> 
> 
> 8001 Lincoln Ave
> 
> Paketi 212
> 
> IL Skokie, 60077
> 
> ABD
> 
> (844) 4NERDIO dahili 6
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a>**SaaSplaza**
[SaaSplaza](http://www.saasplaza.com/) tam Microsoft Dynamics Portföy (NAV, AX, GP, SL, CRM) özel ve genel buluta (Azure'a) sunar.

> Birincil konumu: Hollanda
> 
> İşlemi bölgesi: dünya çapında
> 
> İş ortağı, durum: [altın](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)
> 
> Microsoft bulut hizmeti sağlayıcısı: Evet
> 
> Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi
> 
> **EMEA**:
> 
> Prins Mauritslaan 29-35
> 
> 71 LP Badhoevedorp
> 
> Merhaba Hollanda
> 
> Telefon: +31 20 547 8060 
> 
>  **Kuzey ve Güney Amerika**:
> 
> 171 Sakson yol, paketi 105
> 
> Encinitas, CA 92024
> 
> San Diego
> 
> Amerika Birleşik Devletleri
> 
> Telefon: +1 858 385 8900 
> 
> **APAC**:
> 
> 105 CECIL Sokak
>    
> \#11-08 hello Sekizgene
> 
> Singapur 069534
> 
> Singapur
>   
> Telefon - Singapur: + 65 6222 6591
> 
> Telefon - Avustralya: +61 2 8310 5568 
>    
> Telefon - Yeni Zelanda: + 64 4 488 0321
> 
## <a name="need-more-help"></a>Daha fazla yardım gerekiyor mu?
Hala seçme Yardım veya başka sorularınız mı var? Yöntemleri tooget Yardım aşağıdaki hello birini kullanın. 

1. Adresinden bize e-posta [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).
2. Kişi [Azure Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Başlangıç açarak bir [Azure destek servis talebi](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
3. Bizi arayın. [Yerel bir satış numarasını bulmak](https://azure.microsoft.com/overview/sales-number/).


---
title: "Site kurtarma aaaTest yük devretme tooAzure | Microsoft Docs"
description: "Şirket içi tooAzure bir yük devretme testi çalıştırma hakkında bilgi edinin"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: fa0a93f409cc9f2c2c06c2d91c65971dc90c507f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="test--failover-tooazure-in-site-recovery"></a>Yük devretme tooAzure Site kurtarma sınama



Bu makalede bilgiler sağlanmaktadır ve yük devretme testi ya da bir DR detayı sanal makinelerin ve fiziksel sunucuları, yapmaya yönelik yönergeler hello kurtarma sitesi olarak Azure kullanarak Site Recovery ile korunur.

Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Test yük devretme toovalidate çoğaltma stratejinizi çalıştırabilir veya bir olağanüstü durum kurtarma ayrıntıya herhangi bir veri kaybı veya kapalı kalma süresi olmadan gerçekleştirin. Yük devretme testi yapılması etkilerini hello devam eden çoğaltmayı veya üretim ortamınıza sahip değil. Yük devretme sınaması yapılabilir ya da üzerinde bir sanal makine veya bir [kurtarma planı](site-recovery-create-recovery-plans.md). Yük devretme testi tetiklendiğinde toospecify hello ağ toowhich test sanal makineleri bağlanacağı gerekir. Yük devretme testi tetiklenir sonra hello ediyor izleyebilirsiniz **işleri** sayfası.  


## <a name="supported-scenarios"></a>Desteklenen senaryolar
Yük devretme testi desteklenen tüm dağıtım senaryolarında dışında [eski VMware sitesi tooAzure](site-recovery-vmware-to-azure-classic-legacy.md). Sanal makine üzerinde tooAzure başarısız olduğunda yük devretme sınaması da desteklenmiyor.  


## <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma
Bu yordam açıklar nasıl toorun bir yük devretme sınaması için bir kurtarma planı. Alternatif olarak üzerindeki hello uygun seçeneği kullanılarak tek bir makine için yük devretme testi de çalıştırabilirsiniz.

![Yük devretme sınaması](./media/site-recovery-test-failover-to-azure/TestFailover.png)


1. Seçin **kurtarma planları** > *recoveryplan_name*. Tıklatın **yük devretme testi**.
1. Seçin bir **kurtarma noktası** toofailover için. Seçenekler aşağıdaki hello birini kullanabilirsiniz:
    1.  **En son işlenen**: Site Recovery hizmeti tarafından işlenmiş olan hello kurtarma planı toohello en son kurtarma noktası tüm sanal makinelerin bu seçenek yöneltilir. Bir sanal makine yük devretme yapılırken hello son işlenen kurtarma noktasının zaman damgası da gösterilir. Bir kurtarma planı yük devretme yapıyorsanız, tooindividual sanal makineye gidin ve bakmak **en son kurtarma noktası** bu bilgileri tooget döşeme. Hiçbir zaman harcanan şekilde işlenmemiş verileri tooprocess Merhaba, bu seçenek, bir düşük RTO (Kurtarma süresi hedefi) yük devretme seçeneği sağlar.
    1.  **Son uygulama tutarlı**: Bu seçenek, Site Recovery hizmeti tarafından işlenmiş olan hello kurtarma planı toohello en son uygulama tutarlı bir kurtarma noktası tüm sanal makinelerin yöneltilir. Bir sanal makine yük devretme yapılırken hello son uygulamayla tutarlı kurtarma noktasının zaman damgası da gösterilir. Bir kurtarma planı yük devretme yapıyorsanız, tooindividual sanal makineye gidin ve bakmak **en son kurtarma noktası** bu bilgileri tooget döşeme.
    1.  **En son**: Bu seçenek ilk gönderilen tooSite kurtarma hizmeti toocreate her bir sanal makine için bir kurtarma noktası tooit başarısız olmadan önce yapılmış tüm hello verileri işler. Bu seçenek hello sağlar hello yük devretme tetiklendiğinde düşük RPO (kurtarma noktası hedefi) hello yük devretme tüm hello veri sonra oluşturulan sanal boyunca makinenin olarak çoğaltılmış tooSite kurtarma hizmeti.
    1.  **En son çoklu işlenen VM**: Bu seçenek yalnızca çoklu VM tutarlılığını en az bir sanal makineyle sahip kurtarma planları için kullanılabilir. Bir çoğaltma grubu yük devretme toohello son ortak çoklu VM tutarlı kurtarma parçası olan sanal makineleri gelin. Diğer sanal makineler yük devretme tootheir son işlenen kurtarma noktası.  
    1.  **En son çoklu VM uygulamayla tutarlı**: Bu seçenek yalnızca çoklu VM tutarlılığı ON ile en az bir sanal makinenin kurtarma planları için kullanılabilir. Bir çoğaltma parçası olan sanal makinelere yük devretme toohello son ortak çoklu VM uygulamaları tutarlı kurtarma noktası gruplandırın. Diğer sanal makineler yük devretme tootheir en son uygulama tutarlı kurtarma noktası. 
    1.  **Özel**: bir sanal makinenin yük devretme testi yapmakta olduğunuz sonra bu seçeneği toofailover tooa belirli kurtarma noktası kullanabilirsiniz.
1. Seçin bir **Azure sanal ağı**: Burada hello test sanal makineleri oluşturulacaktır bir Azure sanal ağı sağlar. Site Recovery toocreate test sanal makineleri aynı adlı bir alt ağda çalışır ve kullanarak hello olarak sağlanan aynı IP **işlem ve ağ** hello sanal makinenin ayarlarını. Test sanal makinesi hello ilk alt ağda alfabetik olarak oluşturulduktan sonra aynı adlı alt ağ hello yük devretme sınaması için sağlanan Azure sanal ağı kullanılabilir değilse. Aynı IP hello alt ağda kullanılabilir durumda değilse, sanal makine hello alt ağda kullanılabilir başka bir IP adresi alır. Bu bölüm için okuma [daha fazla ayrıntı](#creating-a-network-for-test-failover)
1. TooAzure çalıştırma işlemini gerçekleştiriyorsanız ve veri şifrelemesi etkin olduğunda, buna **şifreleme anahtarı** sağlayıcı yüklemesi sırasında veri şifrelemesi etkin olduğunda veren select hello sertifika. Merhaba sanal makine üzerinde şifrelemeyi etkinleştirmediyseniz, bu adımı yoksayabilirsiniz.
1. Merhaba üzerinde yük devretme işleminin ilerleyişini izlemek **işleri** sekmesi. Mümkün toosee hello test çoğaltma makinesi hello Azure portalı içinde olmalıdır.
1. tooinitiate hello sanal makine üzerinde RDP bağlantısı, gereksinim duyacağınız çok[bir ortak IP eklemek](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) üzerinde hello hello ağ arabirimi sanal makine başarısız oldu. Tooa Klasik sanal makine üzerinde başarısız olan sonra çok ihtiyacınız[bir uç nokta ekleyin](../virtual-machines/windows/classic/setup-endpoints.md) 3389 numaralı bağlantı noktasında
1. İşiniz bittiğinde tıklatın **temizleme yük devretme testi** hello kurtarma planı üzerinde. İçinde **notları** kaydedin ve hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek. Yük devretme testi sırasında oluşturulan hello sanal makineleri siler.


> [!TIP]
> Site Recovery toocreate test sanal makineleri aynı adlı bir alt ağda çalışır ve kullanarak hello olarak sağlanan aynı IP **işlem ve ağ** hello sanal makinenin ayarlarını. Test sanal makinesi hello ilk alt ağda alfabetik olarak oluşturulduktan sonra aynı adlı alt ağ hello yük devretme sınaması için sağlanan Azure sanal ağı kullanılabilir değilse. Merhaba hedef IP alt ağı seçilen hello parçası ise, site kurtarma hello hedef IP kullanarak toocreate hello test yük devretme sanal makine çalışır. Merhaba hedef IP alt ağı seçilen hello parçası değilse, test yük devretme sanal makine kullanılabilir bir IP alt ağı seçilen hello kullanarak oluşturulur.
>
>

## <a name="test-failover-job"></a>Test yük devretme işi

![Yük devretme sınaması](./media/site-recovery-test-failover-to-azure/TestFailoverJob.png)

Yük devretme testi tetiklendiğinde, aşağıdaki adımları içerir:

1. Önkoşul denetimi: Bu adım, yük devretme için gerekli tüm koşulların karşılandığından sağlar
1. Yük devretme: Bu adım hello verilerini işler ve böylece dışında bir Azure sanal makinesi oluşturulabilir hazır yapar. Seçmiş olmanız durumunda **son** kurtarma noktası, bu adımı oluşturur bir kurtarma noktası toohello hizmeti gönderilen hello verileri.
1. Başlangıç: Bu adım hello önceki adımda işlenen hello verileri kullanarak bir Azure sanal makinesi oluşturur.

## <a name="time-taken-for-failover"></a>Yük devretme için harcanan süre

Bazı durumlarda, sanal makinelerin yük devretme genellikle, yaklaşık 8 too10 dakika toocomplete alır bir ek ara adım gerektirir. Bu durumların olarak olan aşağıdaki:

* Merhaba Mobility hizmeti 9.8 eski bir sürümünü kullanarak VMware sanal makineleri
* Fiziksel sunucuları
* VMware Linux sanal makineleri
* Fiziksel sunucuları olarak korunan Hyper-V sanal makineler
* Burada aşağıdaki sürücüleri önyükleme sürücüler olarak mevcut olmayan VMware sanal makineler
    * storvsc
    * VMBus
    * storflt
    * Intelide
    * ATAPI
* VMware sanal makineleri'de, DHCP hizmeti, DHCP veya statik kullanarak yedeklemiş etkin olmayan IP adresleri

Tüm hello diğer durumlarda bu ara adım gerekli değildir ve hello yük devretme için harcanan hello süre önemli ölçüde düşebilir.


## <a name="creating-a-network-for-test-failover"></a>Yük devretme sınaması için bir ağ oluşturma
Bir test yük devretme yapılırken sağladığınız üretim ağınızdan kurtarma sitesi yalıtılmış bir ağ seçmeniz önerilir **işlem ve ağ** hello sanal makine için ayarları. Bir Azure sanal ağı oluşturduğunuzda varsayılan olarak, diğer ağlardan yalıtılır. Bu ağın üretim ağınızdan taklit etmelidir:

1. Test ağı alt ağlar olarak, üretim ağınıza ve bu, üretim ağınıza hello alt ağ olarak aynı ad hello ile aynı sayıda olmalıdır.
1. Test ağı kullanması gereken Merhaba, üretim ağınıza olarak aynı IP aralığı.
1. Güncelleştirme hello hello Test IP altında hello DNS sanal makine için hedef olarak verdiğiniz IP hello gibi ağ DNS **işlem ve ağ** ayarlar. Git üzerinden [test active directory için yük devretme konuları](site-recovery-active-directory.md#test-failover-considerations) daha fazla ayrıntı için bölüm.


## <a name="test-failover-tooa-production-network-on-recovery-site"></a>Kurtarma sitesinde test yük devretme tooa üretim ağı
Bir test yük devretme yapılırken sağladığınız üretim ağınızdan kurtarma sitesini farklı bir ağ seçmeniz önerilir **işlem ve ağ** hello sanal makine için ayarları. Ancak gerçekten toovalidate son tooend ağ bağlantısına başarısız istiyorsanız, sanal makine üzerinde noktaları aşağıdaki hello dikkat edin:

1. Merhaba test yük devretme yapılırken hello birincil sanal makinenin kapatma olduğundan emin olun. Bunu yapmazsanız, hello iki sanal makinelerle olacaktır hello çalıştıran aynı kimlik, aynı ağ hello aynı anda ve, tooundesired sonuçlara yol açabilir.
1. Merhaba test yük devretme sanal makinelerine yaptığınız tüm değişiklikler olduğunda kayıp, temizleme hello test yük devretme sanal makineler. Bu değişiklikler, çoğaltılmış geri toohello birincil sanal makine olmaz.
1. Bu şekilde test yapmanın tooa kapalı kalma süresi, üretim uygulamanızın yol açar. Merhaba uygulama kullanıcılarının hello DR ayrıntısına gittiğinizde toonot kullanım hello uygulama sürüyor sorulan.  



## <a name="prepare-active-directory-and-dns"></a>Active Directory ve DNS hazırlama
bir yük devretme sınaması için sınama uygulama toorun, test ortamınızda hello üretim Active Directory ortamında bir kopyasını gerekir. Git üzerinden [test active directory için yük devretme konuları](site-recovery-active-directory.md#test-failover-considerations) daha fazla ayrıntı için bölüm.

## <a name="prepare-tooconnect-tooazure-vms-after-failover"></a>Yük devretme sonrasında tooAzure VM'ler tooconnect hazırlama

Tooconnect tooAzure VM'ler istiyorsanız, yük devretme işleminden sonra RDP kullanarak hello tabloda özetlenen Eylemler hello emin olun.

**Yük devretme** | **Konum** | **Eylemler**
--- | --- | ---
**Windows çalıştıran azure VM** | Yük devretmeden önce şirket içi makinede | tooaccess üzerinden Azure VM hello Internet Merhaba, RDP etkinleştirmek, TCP emin olun ve UDP kurallarının Merhaba eklenir **ortak**, ve bu seçeneklerinde RDP'ye izin **Windows Güvenlik Duvarı** > **izin verildi Uygulamaları**, tüm profiller için.<br/><br/> bir siteden siteye bağlantı üzerinden tooaccess hello makinede RDP etkinleştirmek ve RDP hello izin verildiğinden emin olun **Windows Güvenlik Duvarı** -> **verilen uygulamalar ve Özellikler** için  **Etki alanı ve özel** ağlar.<br/><br/>  Merhaba işletim sisteminin SAN ilkesinin çok ayarlandığından emin olun**OnlineAll**. [Daha fazla bilgi edinin](https://support.microsoft.com/kb/3031135).<br/><br/> Bekleyen hiçbir Windows güncelleştirmeleri hello sanal makineye bir yük devretme tetiklemek zaman olmadığından emin olun. Windows update Hello güncelleştirme tamamlanana kadar yük devretme ve mümkün toologin toohello sanal makine olmaz başlayabilir. <br/><br/>
**Windows çalıştıran azure VM** | Yük devretme sonrasında Azure VM'de | Klasik sanal makine için [genel bir uç nokta ekleme](../virtual-machines/windows/classic/setup-endpoints.md) hello RDP Protokolü (3389 numaralı bağlantı noktası) için<br/><br/>  Resource Manager sanal makinesi [bir ortak IP eklemek](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) üzerindeki.<br/><br/> Ağ güvenlik grubu kurallarının VM başarısız hello hello ve hello bağlı olduğundan, Azure alt toowhich gerekiyor tooallow gelen bağlantıları toohello RDP bağlantı.<br/><br/> Bir Resource Manager sanal makine için kontrol edebilirsiniz **önyükleme tanılama** toolook adresindeki hello sanal makinenin bir ekran görüntüsü<br/><br/> Bağlanamıyorsanız, VM çalıştıran bu hello denetleyin ve bunlara Ara [sorun giderme ipuçları](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).<br/><br/>
**Linux çalıştıran azure VM** | Yük devretmeden önce şirket içi makinede | Bu hello hello Azure VM'de Secure Shell hizmetinin sistem önyüklemesinde otomatik olarak toostart ayarlandığından emin olun.<br/><br/> Güvenlik duvarı kuralları bir SSH bağlantısı tooit izin verdiğinden emin olun.
**Linux çalıştıran azure VM** | Yük devretme sonrasında Azure VM | Ağ güvenlik grubu kurallarının VM başarısız hello hello ve hello bağlı olduğundan, Azure alt toowhich gerekiyor tooallow gelen bağlantıları toohello SSH bağlantı.<br/><br/> Klasik sanal makine için [genel bir uç nokta ekleme](../virtual-machines/windows/classic/setup-endpoints.md) oluşturulmalıdır, tooallow gelen bağlantıları hello SSH bağlantı noktası (TCP bağlantı noktası 22 varsayılan olarak).<br/><br/> Resource Manager sanal makinesi [bir ortak IP eklemek](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) üzerindeki.<br/><br/> Bir Resource Manager sanal makine için kontrol edebilirsiniz **önyükleme tanılama** toolook adresindeki hello sanal makinenin bir ekran görüntüsü<br/><br/>



## <a name="next-steps"></a>Sonraki adımlar
Yük devretme testi başarıyla denediyseniz sonra yapılması deneyebilirsiniz bir [yük devretme](site-recovery-failover.md).

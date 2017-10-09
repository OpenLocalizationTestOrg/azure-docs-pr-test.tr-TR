---
title: "Azure Güvenlik Merkezi'nde aaaSecurity izleme | Microsoft Docs"
description: "Bu makalede Azure Güvenlik Merkezi'nde yetenekleri izleme ile çalışmaya tooget yardımcı olur."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 43c2a8864d5fe27ba44b0d7bc979db970305ec17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde güvenlik durumunu izleme
Bu makalede, Azure Güvenlik Merkezi toomonitor uyumluluk ilkeleriyle izleme kapasiteleri hello kullanmanıza yardımcı olur.

## <a name="what-is-security-health-monitoring"></a>Güvenlik durumunu izleme nedir?
Genellikle izlemeyi ve biz toohello duruma tepki verme için bir olay toooccur bekliyor olarak izlemeyi düşünün. Güvenlik İzleme toohaving kuruluş standartlarıyla veya en iyi yöntemler karşılamayan kaynakları tooidentify sistemlerinizi denetimleri öngörülü bir stratejiye başvuruyor.

## <a name="monitoring-security-health"></a>Güvenlik durumunu izleme
Etkinleştirdikten sonra [güvenlik ilkeleri](security-center-policies.md) bir aboneliğin kaynakları için Güvenlik Merkezi, kaynakları tooidentify olası güvenlik açıklarını hello güvenliğini analiz eder. Ağ yapılandırmanız ile ilgili bilgiler hemen kullanımınıza sunulur. Bir saat sürebilir veya daha fazla bilgi güvenliği gibi sanal makine yapılandırma hakkında bilgi için güncelleştirme durumu ve işletim sistemi yapılandırması, toobecome kullanılabilir. Hello hello güvenlik durumunu, kaynaklarınızı ve sorunları görüntüleyebilirsiniz **önleme** bölümü. Bu sorunların bir listesi üzerinde hello görüntüleyebilirsiniz **önerileri** döşeme.

Hakkında daha fazla bilgi için okuma tooapply önerileri [Azure Güvenlik Merkezi'nde güvenlik önerilerini uygulama](security-center-recommendations.md).

Merhaba altında **önleme** bölümünde hello kaynaklarınızın güvenlik durumunu izleyebilirsiniz. Aşağıdaki örneğine hello gördüğünüz her kaynağın döşemesinin (işlem, ağ, depolama ve veri ve uygulama) olan hello belirlendi sorunları toplam sayısı.

![Kaynaklar güvenlik durumu kutucuğu](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a>İzleyici işlemi
Tıkladığınızda **işlem** , hello döşeme **işlem** açar dikey üç sekme gösterir:

- **Genel Bakış**: izleme ve sanal makine önerileri.
- **Sanal Makineler**: tüm sanal makineleri ve geçerli güvenlik durumunu listeler.
- **Cloud Services**: Güvenlik Merkezi tarafından izlenen tüm web ve çalışan rollerinin listesi.

![Sanal makine tarafından eksik sistem güncelleştirmesi](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

Her bir sekmede, birden çok bölüm olabilir ve her bir bölümünde, bir tek tek seçenek toosee seçebilirsiniz hello hakkında daha fazla ayrıntı adımları tooaddress bu belirli sorun önerilir. 

#### <a name="monitoring-recommendations"></a>İzleme önerileri
Bu bölümde hello veri toplama ve bunların geçerli durumları için başlatılan sanal makinelerin toplam sayısını gösterir. Tüm sanal makinelerin veri toplama başlatıldıktan sonra bunların hazır tooreceive Güvenlik Merkezi güvenlik ilkelerini olacaktır. Bu giriş'e tıkladığınızda, hello **VM Aracısı eksik veya yanıt vermiyor** dikey pencere açılır. 

![Sanal makine tarafından eksik sistem güncelleştirmesi](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a>Sanal makine önerileri
Bu bölümde, Azure Güvenlik Merkezi’nin izlediği [her bir sanal makine için bir öneri](security-center-virtual-machine-recommendations.md) kümesi bulunur. Merhaba ilk sütun hello öneri listeler. Merhaba ikinci sütun bu önerisi tarafından etkilenen sanal makineleri hello toplam sayısını gösterir. Merhaba üçüncü sütun hello ekran aşağıdaki gösterildiği gibi hello sorunu hello önemini gösterir.

![Sanal makine önerileri](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> Yalnızca en az bir ortak uç nokta olan makineleri hello gösterilen **ağ durumu** dikey penceresinde hello **ağ topolojisi** listesi.
>
>

Her öneride, tıkladıktan sonra gerçekleştirebileceğiniz bir eylemler kümesi bulunur. Örneğin, tıklatırsanız **eksik sistem güncelleştirmeleri**, hello **eksik sistem güncelleştirmeleri** dikey pencere açılır. Yamaları eksik olan ve hello aşağıda gösterildiği gibi hello eksik güncelleştirmenin önem hello hello sanal makineleri listeler ekran görüntüsü.

![Sanal makineler için eksik sistem güncelleştirmeleri](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

Merhaba **eksik sistem güncelleştirmeleri** dikey penceresinde hello aşağıdaki bilgilerle bir tablo gösterir:

* **SANAL makine**: hello hello sanal makinenin adı, güncelleştirmeleri eksik.
* **Sistem güncelleştirmeleri**: Merhaba eksik sistem güncelleştirmeleri sayısı.
* **En son tarama zamanı**: Güvenlik Merkezi'nin son hello sanal makine güncelleştirmeleri için tarama hello zaman.
* **Durum**: Merhaba hello öneri geçerli durumu:
  * **Açık**: hello öneri ele alınmayan henüz.
  * **Devam eden**: hello öneri yüklenmekte olduğu uygulanan toothose kaynakları ve herhangi bir işlem yapmanız gerekmez.
  * **Çözümlenen**: hello öneri zaten tamamlandı. (Merhaba sorunu Çözümlendi, hello girişi soluk).
* **Önem DERECESİ**: belirli bir önerinin hello önemini açıklar:
  * **Yüksek**: Anlamlı bir kaynakta (uygulama, sanal makine veya ağ güvenlik grubu) güvenlik açığı var ve ilgilenilmesi gerekiyor.
  * **Orta**: kritik olmayan veya ek adımlar gerekli toocomplete bir işlem olan veya bir güvenlik açığının ortadan kaldırılması.
  * **Düşük**: Bir güvenlik açığının ele alınması gerekiyor ancak hemen ilgilenilmesi gerekmiyor. (Varsayılan olarak, düşük öneriler sunulmaz ancak tooview istiyorsanız düşük öneriler filtresini kullanabilirsiniz bunları.)

tooview hello öneri ayrıntılarını hello hello sanal makinenin adını tıklatın. Bu sanal makine için yeni bir dikey pencere Merhaba güncelleştirme listesiyle hello ekran aşağıdaki gösterildiği gibi açılır.

![Belirli bir sanal makine için eksik sistem güncelleştirmeleri](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> Merhaba buradaki güvenlik önerileri aynı hello de olarak hello olan **önerileri** dikey. Merhaba bkz [Azure Güvenlik Merkezi'nde güvenlik önerilerini uygulama](security-center-recommendations.md) hakkında daha fazla bilgi için makalenin tooresolve öneriler. Bu aynı zamanda hello kullanılabilen tüm kaynaklar için sanal makineler için yalnızca geçerli **kaynak durumu** döşeme.
>
>

#### <a name="virtual-machines-section"></a>Sanal makineler bölümü
Merhaba sanal makineler bölümü tüm sanal makineler ve öneriler genel bir bakış sağlar. Her sütun hello ekran aşağıdaki gösterildiği gibi bir dizi öneriyi temsil eder:

![Tüm sanal makinelere ve önerilere genel bakış](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

Her öneri yardımcı altında görüntülenen hello simgesini dikkat etmeniz gereken ve önerinin türünü hello hello sanal makineler, tooquickly tanımlayın.

Merhaba önceki örnekte, bir sanal makine uç nokta koruma ile ilgili kritik bir önerisi yok. tooget hello sanal makine hakkında daha fazla bilgi tıklayın. Açılan yeni bir dikey pencere hello ekran aşağıdaki gösterildiği gibi bu sanal makine temsil eder.

![Sanal makine güvenlik ayrıntıları](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

Bu dikey hello sanal makine için hello güvenlik sorunları vardır. Bu dikey penceresinde Hello altındaki hello önerilen eylem ve hello sorunların önem derecesini görebilirsiniz.

#### <a name="cloud-services-section"></a>Bulut hizmetleri bölümü
Bulut Hizmetleri için bir öneri oluşturulduğunda Hello işletim sistemi sürümü hello ekran aşağıdaki gösterildiği gibi tarihi geçmiş:

![Bulut hizmetlerinin sistem durumu](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

(Hangi hello hello önceki örnek için geçerli değildir) öneri sahip olduğu bir senaryoda hello öneri tooupdate hello işletim sistemi sürümü toofollow hello adımları gerekir. Bir güncelleştirme kullanıma hazır olduğunda bir uyarı olacaktır (kırmızı veya turuncu - bağlıdır hello sorunu hello önem derecesi). Bu uyarı hello WebRole1 (Windows Server, web uygulaması otomatik olarak dağıtılan tooIIS ile çalışır) veya (Windows Server, web uygulaması otomatik olarak dağıtılan tooIIS ile çalışır) WorkerRole1 satırlardaki tıkladığınızda, bu konu hakkında daha fazla ayrıntı içeren yeni bir dikey pencere açılır hello ekran aşağıdaki gösterildiği gibi öneri:

![Bulut hizmeti ayrıntıları](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

Bu öneri hakkında daha fazla düzenleyici bir açıklama toosee tıklatın **güncelleştirme işletim sistemi sürümü** hello altında **açıklama** sütun. Merhaba **güncelleştirme işletim sistemi sürümü (Önizleme)** ile daha fazla ayrıntı dikey pencere açılır.

![Bulut hizmeti önerileri](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a>Sanal ağları izleme
Tıkladığınızda **ağ** , hello döşeme **ağ** hello ekran aşağıdaki gösterildiği gibi daha fazla ayrıntı içeren dikey pencere açılır:

![Ağ dikey penceresi](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a>Ağ önerileri
Sanal makinenin kaynak durumu bilgilerine hello gibi bu dikey pencere hello alta özetlenen hello en üstündeki hello dikey ve izlenen ağların bir listesini sorunların listesini sağlar.

ağ durumu döküm bölümü hello olası güvenlik sorunlarını listeler ve sunar [önerileri](security-center-network-recommendations.md). Olası sorunlar şunları içerebilir:

* Yeni Nesil Güvenlik Duvarı (NGFW) yüklü değil
* Alt ağlardaki ağ güvenlik grupları etkin değil
* Sanal makinelerdeki ağ güvenlik grupları etkin değil
* Genel dış uç nokta aracılığıyla harici erişimi kısıtlama
* İnternet’e yönelik sorunsuz çalışan uç noktalar

Bir öneri tıkladığınızda, yeni bir dikey pencere hello öneri hakkında daha fazla ayrıntı hello aşağıdaki örnekte gösterildiği gibi açılır.

![Merhaba ağ dikey penceresinde bir öneri ayrıntılarını](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

Bu örnekte, hello **eksik ağ güvenlik gruplarını yapılandırma alt ağlar için** dikey penceresinde alt ağların bir listesine sahip ve eksik olan sanal makinelerin ağ güvenlik grubu koruması. Merhaba alt toowhich tooapply hello ağ güvenlik grubu istediğiniz tıklarsanız, başka bir dikey pencere açılır.

Merhaba, **ağ güvenlik grubunu seçme** dikey penceresinde hello en uygun ağ güvenlik grubu hello alt ağ için seçebilir veya yeni bir ağ güvenlik grubu oluşturabilirsiniz.

#### <a name="internet-facing-endpoints-section"></a>İnternet'e yönelik uç noktalar bölümü
Merhaba, **Internet'e yönelik uç noktalar** bölümünde, uç nokta ve geçerli durumunu Internet'e yönelik ile şu anda yapılandırılmış hello sanal makineleri görebilirsiniz.

![İnternet'e yönelik uç nokta ve durumu ile yapılandırılan sanal makineler](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

Bu tablo hello sanal makine hello Internet'e yönelik IP adresini temsil eden hello uç nokta adına sahip ve hello ağ güvenlik grubu geçerli önem derecesi durumu hello ve NGFW'nun hello. Merhaba tablo önem derecesine göre sıralanır:

* Kırmızı (en üstte): Yüksek önceliklidir ve hemen ilgilenilmesi gerekir
* Turuncu: Orta önceliklidir ve olabildiğince yakın zamanda ilgilenilmesi gerekir
* Yeşil (sonuncu): Sorunsuz çalışma durumu

#### <a name="networking-topology-section"></a>Ağ topolojisi bölümü
Merhaba **ağ topolojisi** bölümde hello ekran aşağıdaki gösterildiği gibi hello kaynakların hiyerarşik bir görünümü bulunur:

![Ağ topolojisi bölümünde kaynakların hiyerarşik görünümü](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

Bu tablo, önem derecesine göre sıralanır (sanal makineler ve alt ağlar):

* Kırmızı (en üstte): Yüksek önceliklidir ve hemen ilgilenilmesi gerekir
* Turuncu: Orta önceliklidir ve olabildiğince yakın zamanda ilgilenilmesi gerekir
* Yeşil (sonuncu): Sorunsuz çalışma durumu

Bu topoloji görünümünde hello ilk düzeyine sahip [sanal ağlar](../virtual-network/virtual-networks-overview.md), [sanal ağ geçitlerini](/vpn-gateway/vpn-gateway-site-to-site-create.md), ve [sanal ağları (Klasik)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md). Merhaba ikinci düzeyde alt ağlar, ve hello üçüncü düzey toothose alt ait hello sanal makinelere sahip. Merhaba sağ sütun hello aşağıdaki örnekte gösterildiği gibi hello ağ güvenlik grubu bu kaynaklar için geçerli durumunu hello sahiptir:

![Ağ topolojisi bölümü içinde hello ağ güvenlik grubu durumu](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

Merhaba bu dikey pencerenin alt kısmı hello için öneriler benzeyen bu sanal makine, içerir toowhat önceden tanımlanmıştır. Daha fazla bir öneri toolearn'ı tıklatın veya hello gerekli güvenlik denetimini veya yapılandırma uygulayın.

### <a name="monitor-storage--data"></a>Depolama ve verileri izleme

Tıkladığınızda **depolama & veri** hello içinde **önleme** hello bölümünde **veri kaynakları** SQL ve depolama için öneriler dikey pencere açılır. Ayrıca sahip [önerileri](security-center-sql-service-recommendations.md) hello veritabanının hello genel sistem durumu için. Depolama şifrelemesi hakkında daha fazla bilgi için [Azure Güvenlik Merkezi'ndeki Azure depolama hesabı için şifrelemeyi etkinleştirme](security-center-enable-encryption-for-storage-account.md) bölümünü okuyun.

![Veri Kaynakları](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

Altında **SQL önerileri**, herhangi bir önerisi'ı tıklatın ve get daha ilgili bir sorun hakkında daha fazla eylem tooresolve ayrıntıları. Merhaba aşağıdaki örnekte gösterilir hello hello genişlemesi **SQL veritabanlarında veritabanı denetim ve tehdit algılama** öneri.

![SQL önerisi hakkındaki ayrıntılar](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

Merhaba **SQL veritabanlarında denetimi etkinleştirme ve tehdit algılama** dikey penceresinde aşağıdaki bilgilerle hello vardır:

* SQL veritabanlarının bir listesi
* Merhaba sunucu üzerinde bulundukları
* Bu ayar olup hello sunucudan devralınmış olduğuna veya bu veritabanında benzersiz olup olmadığını hakkında bilgi
* Merhaba geçerli durumu
* Merhaba önem derecesi hello sorunu

Bu öneri hello veritabanı tooaddress tıklattığınızda hello **denetim ve tehdit algılama** hello ekran aşağıdaki gösterildiği gibi dikey pencere açılır.

![Denetim ve Tehdit algılama dikey penceresi](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

tooenable denetim, select **ON** hello altında **denetim** seçeneği.

### <a name="monitor-applications"></a>Uygulamaları izleme

Azure İş yükünüzün bulunan uygulamaları varsa [(Azure Resource Manager aracılığıyla oluşturulan) sanal makinelerin](../azure-resource-manager/resource-manager-deployment-model.md) sağlanmış web bağlantı noktaları ile (TCP bağlantı noktaları 80 ve 443), Güvenlik Merkezi bu tooidentify olası güvenlik sorunlarını izleyebilirsiniz ve düzeltme adımları öneririz. Merhaba tıkladığınızda **uygulamaları** , hello döşeme **uygulamaları** dikey pencere açılır hello önerileri bir dizi **uygulama önerileri** bölümü. Ayrıca hello ekran aşağıdaki gösterildiği gibi hello ana bilgisayar/sanal IP başına uygulama dökümünü gösterir.

![Uygulamaların güvenlik durumu](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

Yalnızca, ile diğer öneriler hello gibi bir öneri toosee hello sorun hakkında daha fazla ayrıntı tıklatabilirsiniz ve nasıl tooremediate. Aşağıdaki şekilde hello gösterilen hello örnek güvenli olmayan bir web uygulaması olarak tanımlanan bir uygulamadır. Güvenli kabul edilmeyen hello uygulama seçtiğinizde, aşağıdaki seçenek kullanılabilir hello ile başka bir dikey pencere açılır:

![Güvenli olmayan bir uygulama hakkındaki ayrıntılar](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

Bu dikey pencerede bu uygulamaya ilişkin tüm önerilerin bir listesi bulunur. Merhaba tıkladığınızda **bir web uygulaması güvenlik duvarı ekleme** öneri, hello **bir Web uygulaması güvenlik duvarı ekleme** dikey pencere açılır, tooinstall için seçeneklerle bir web uygulaması Güvenlik Duvarı (WAF) ortağından Aşağıdaki ekran görüntüsü hello gösterilir.

![Web Uygulaması Güvenlik Duvarı Ekleme iletişim kutusu](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a>Ayrıca bkz.
Bu makalede, nasıl öğrenilen izleme kapasiteleri Azure Güvenlik Merkezi'nde toouse. Azure Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md): öğrenin nasıl tooconfigure Azure Güvenlik Merkezi'nde güvenlik ayarları.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md): öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md): nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md): hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/): Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

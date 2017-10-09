---
title: "aaaUse hello Operations Management Suite hizmet Haritası çözümde | Microsoft Docs"
description: "Linux sistemleri ve haritalar Hizmetleri arasındaki iletişimi hello ve hizmet Haritası Windows uygulama bileşenleri otomatik olarak bulur bir Operations Management Suite çözümüdür. Bu makalede hizmet Haritası ortamınıza dağıtmak ve çeşitli senaryolarda içinde kullanma ile ilgili ayrıntıları sağlar."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: f7c209182c9171cc520192ac13ca4d85174081b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-map-solution-in-operations-management-suite"></a>Operations Management Suite Hello hizmet Haritası çözümü kullanın
Hizmet eşlemesi sistemlerde, Windows ve Linux uygulama bileşenleri otomatik olarak bulur ve Hizmetleri arasındaki iletişimi eşlemeleri hello. Hizmet eşlemesi ile bunları düşündüğünüz hello şekilde sunucularınızı görüntüleyebilirsiniz: kritik Hizmetleri sunmak birbirine bağlı sistemler. Hizmet eşlemesi arasında herhangi bir TCP bağlı mimarideki sunucuları, işlemleri ve bağlantı noktaları arasındaki bağlantıları gösterir, herhangi bir yapılandırma gerekmez dışında bir aracı yüklemesini hello.

Bu makalede hizmet eşlemesi kullanarak hello Ayrıntılar açıklanmaktadır. Hizmet Haritası ve ekleme aracıları yapılandırma hakkında daha fazla bilgi için bkz: [Operations Management Suite yapılandırma hizmet Haritası çözümde](operations-management-suite-service-map-configure.md).


## <a name="use-cases-make-your-it-processes-dependency-aware"></a>Kullanım: BT'niz olun bağımlılık kullanan işler

### <a name="discovery"></a>Bulma
Hizmet eşlemesi bağımlılıkları ortak başvuru haritasını sunucularınızı, işlemleri ve üçüncü taraf hizmetleri otomatik olarak oluşturur. Bulur ve beklenmedik biçimde bağlantıları, uzak üçüncü taraf sistemleri üzerinde bağlı ve Active Directory gibi ağınızın bağımlılıkları tootraditional koyu alanlarını tanımlayan tüm TCP bağımlılıkları eşler. Hizmet eşlemesi olası sunucu yanlış yapılandırma, hizmet kesintisi ve ağ sorunları belirlemenize yardımcı yönetilen sistemlerinizde toomake, çalıştığınız başarısız ağ bağlantılarını bulur.

### <a name="incident-management"></a>Olay yönetimi
Hizmet eşlemesi sistemleri nasıl bağlandığını gösteren ve birbirlerine etkileyen sorun yalıtım hello konusunda güvenilir bilgiler önlenmesine yardımcı olur. Ayrıca tooidentifying başarısız bağlantılar, yanlış yapılandırılmış yük Dengeleyiciler, önemli hizmetler, şaşırtıcı veya aşırı yükünü belirleyin ve istemciler, geliştirici makineleri tooproduction sistemleri konuşuyormuş gibi standart dışı yardımcı olur. Tümleşik iş akışları, Operations Management Suite değiştirmek izleme ile birlikte kullanarak, bir arka uç makine ya da hizmet üzerinde değişiklik olayı olay hello kök nedenini açıklar olup olmadığını da görebilirsiniz.

### <a name="migration-assurance"></a>Geçiş güvence
Hizmet eşlemesi kullanarak, etkili bir şekilde planlayabilir, hızlandırmak ve hiçbir şey geride bıraktığı beklenmedik biçimde kesintiler meydana gelmediğinden emin olun ve yardımcı olan Azure geçişler doğrulayın. Tüm bağımlı sistemleri bu gereksinimi toomigrate birlikte bulmak, sistem yapılandırmanıza ve kapasite değerlendirmek ve çalışan bir sistemi kullanıcılar hala sunma veya geçiş yerine yetkisini için bir adaydır olup olmadığını belirleyin. Hello taşıma işlemi tamamlandıktan sonra sistemleri test istemci yükleme ve kimlik tooverify üzerinde denetleyebilir ve müşteriler bağlanma. Alt ağ planlama ve güvenlik duvarı tanımlarınızın sorunlarınız varsa, hizmet Haritası Maps başarısız bağlantıları, bağlantı gereken toohello sistemleri gelin.

### <a name="business-continuity"></a>İş sürekliliği
Azure Site Recovery kullanıyorsanız ve uygulama ortamınız hizmet eşlemesi için hello kurtarma dizisi tanımlama Yardım otomatik olarak şunları yapabilecek nasıl kurtarma planını güvenilirdir sistemleri birbirine tooensure kullanan gösterir. Geri yüklenen ve kullanılabilir Hello sunucusudur sonra veya bir grup kritik sunucu seçme ve istemcilerine görüntüleme, hangi ön uç sistemleri toorecover belirleyebilir. Odağı sistemlerinizi geri önce buna karşılık, kritik sunucularının arka uç bağımlılıkları bakarak, hangi sistemleri toorecover tanımlayabilirsiniz.

### <a name="patch-management"></a>Düzeltme Eki Yönetimi
Hizmet eşlemesi, düzeltme eki uygulama sistemlerinizi aşağı olabilmesi bunları önceden bildirebilir şekilde diğer ekipler ve sunucular hizmetinizi üzerinde bağlı olan göstererek hello Operations Management Suite Sistem Güncelleştirme değerlendirmesi kullanımınız geliştirir. Hizmet eşlemesi, hizmetlerinizin kullanılabilir ve sonra düzgün biçimde bağlı olup bunların düzeltme eki yeniden ve göstererek Operations Management Suite, düzeltme eki yönetimi de geliştirir.


## <a name="mapping-overview"></a>Eşleme genel bakış
Hizmet eşlemesi aracıları burada yüklü ve her işlem için gelen ve giden bağlantılara ayrıntılarını hello hello sunucusundaki tüm TCP bağlı işlemler hakkında bilgi toplayın. Merhaba sol bölmede Hello listesinde makineler veya hizmet Haritası aracıları toovisualize bağımlılıklarını belirtilen zaman aralığı üzerinde sahip grupları seçebilirsiniz. Belirli bir makine odaklanmak makine bağımlılık eşler ve doğrudan TCP istemciler veya sunucular bu makinenin tüm hello makinelerde göster.  Makine grubu eşlemeleri sunucular ve onların bağımlılıkları kümelerini gösterir.

![Hizmet eşlemesi'ne genel bakış](media/oms-service-map/service-map-overview.png)

Makineler hello harita tooshow hello etkin ağ bağlantıları ile Merhaba seçili zaman aralığı içinde çalışan işlemleri içinde genişletilebilir. Bir hizmet Haritası Aracısı ile uzak makineye genişletilmiş tooshow işlem ayrıntılarını olduğunda, yalnızca hello odak makineyle iletişim işlemleri gösterilmektedir. Merhaba odak makinesine bağlanma aracısız ön uç makineler Hello sayısı bağlandıkları hello işlemlerin hello sol tarafında belirtilir. Merhaba odak makine aracı olan bir bağlantı tooa arka uç makine değiştirirken, hello arka uç sunucu bir sunucu bağlantı noktası grubuna dahil, diğer bağlantılar toohello yanı sıra aynı bağlantı noktası numarası.

Varsayılan olarak, hizmet eşlemesinde Göster hello bağımlılık bilgi son 30 dakika eşler. Merhaba üst sol tarafında Hello zamanı denetimlerini kullanarak nasıl bağımlılıkları hello'Aranan tooone saat tooshow yukarı geçmiş zaman aralıkları için eşlemeleri sorgulayabilirsiniz Geçmiş (örneğin, bir olay sırasında veya bir değişiklik oluşmadan önce). Hizmet eşlemesi veri Ücretli çalışma alanlarında 30 gün ve ücretsiz çalışma alanlarında 7 gün için depolanır.

## <a name="status-badges-and-border-coloring"></a>Durum rozetleri ve kenarlık renklendirme
Merhaba alt hello eşlemesindeki her sunucunun hello sunucu hakkındaki durum bilgilerini saymayı durum rozetleri listesi olabilir. Merhaba rozetleri hello Operations Management Suite çözüm tümleştirmeler birini hello sunucudan ilgili bazı bilgiler olduğunu gösterir. Bir gösterge tıklamak, doğrudan hello durum toohello ayrıntılarını hello sağ bölmede götürür. Merhaba şu anda kullanılabilir durum rozetleri uyarılar, hizmet Masası, değişiklikleri, güvenlik ve güncelleştirmeleri içerir.

Merhaba durum rozetleri Hello önem derecesine bağlı olarak makine düğümünü kenarlık renkli kırmızı (kritik), sarı (uyarı) olması veya (bilgilendirme) mavi. Merhaba renk hello en ciddi herhangi birinin durumunu hello durum rozetleri temsil eder. Gri kenarlık hiç durum göstergesi olan bir düğüm gösterir.

![Durum rozetleri](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a>Makine grupları
Makine grupları yalnızca bir tane değil bir eşleminde çok katmanlı uygulama veya sunucu kümesinin tüm hello üyelerinin görebilmeleri sunucular kümesi kalmaz, toosee eşlemeleri izin verin.

Kullanıcıların hangi sunucuların birlikte bir gruba ait ve hello grup için bir ad seçin seçin.  Tüm işlemler ve bağlantıları ile tooview hello grubu seçin veya diğer hello grubunun üyeleri yalnızca hello işlemleri ve doğrudan toohello ilgili bağlantılarla görüntüleme.

![Makine grubu](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a>Makine grubu oluşturma
toocreate bir grup, select hello makine ya da makineleri istediğiniz hello makinelerinizde listelemek ve tıklatın **toogroup eklemek**.

![Grup oluşturma](media/oms-service-map/machine-groups-create.png)

Burada, seçebileceğiniz **Yeni Oluştur** ve hello grubuna bir ad verin.

![Ad grubu](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
>Makine grupları şu anda sınırlı too10 sunucuları, ancak biz tooincrease bu sınırı yakında planlayın.

### <a name="viewing-a-group"></a>Bir grup görüntüleme
Bazı grupları oluşturduktan sonra bunları hello grupları sekmesini seçerek görüntüleyebilirsiniz.

![Grupları sekmesi](media/oms-service-map/machine-groups-tab.png)

Ardından bu makine grubu için hello grup adı tooview hello harita seçin.
![Makine grubu](media/oms-service-map/machine-group.png) toohello grubuna hello makineler özetlenen hello eşlemesi beyaz.

Makine grubu hello hello makinelere genişleyen hello Grup listeler.

![Makine grubu makineleri](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a>İşleme göre filtre uygulama
Tüm işlemler ve bağlantıları hello Grup gösteren arasında hello harita görünümünü açın ve yalnızca doğrudan toohello makine grubu ile ilgili olanları hello.  Varsayılan görünüm Hello tooshow tüm işlemler olduğundan.  Merhaba harita yukarıda hello filtre simgesini tıklatarak hello görünümü değiştirebilirsiniz.

![Filtre grubu](media/oms-service-map/machine-groups-filter.png)

Zaman **tüm işlemler** olan seçili hello harita tüm işlemleri ve her hello makinelerin bağlantıları hello Grup dahil edilir.

![Makine grubu tüm işler](media/oms-service-map/machine-groups-all.png)

Merhaba görünüm yalnızca tooshow değiştirirseniz **Grup bağlı işlemler**, hello harita daraltıldığı tooonly bu işlemleri ve doğrudan bağlantılar tooother makineler basitleştirilmiş bir görünümü oluşturma hello grubundaki bağlı.

![Makine grubu işlemleri filtrelenir](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-tooa-group"></a>Ekleme makineler tooa grubu
tooadd makineleri tooan varolan bir grubu, hello kutular istediğiniz ve ardından sonraki toohello makineler denetleyin **toogroup eklemek**.  Ardından, tooadd hello makinelerine hello grubu seçin.
 
### <a name="removing-machines-from-a-group"></a>Makineler bir gruptan kaldırma
Hello grupları listesi, hello grup adı toolist hello makinelerinizde hello makine grubunu genişletin.  Tooremove istediğiniz ve seçin hello üç nokta menü sonraki toohello makinede ardından **kaldırmak**.

![Makineyi grubundan Kaldır](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a>Kaldırma veya bir grubu yeniden adlandırma
Merhaba üç nokta menü sonraki toohello grup adı'hello Grup listesi tıklayın.

![Makine grubu menüsü](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a>Rol simgesi
Belirli işlemleri belirli rolleri makinelerde hizmet: web sunucuları, uygulama sunucuları, veritabanı ve benzeri. Hizmet eşlemesi işlem açıklama ekler ve rol simgeler toohelp makine kutularıyla yürütür bir bakışta hello rol bir işlem veya sunucu tanımlayın.

| Rol simgesi | Açıklama |
|:--|:--|
| ![Web sunucusu](media/oms-service-map/role-web-server.png) | Web sunucusu |
| ![Uygulama sunucusu](media/oms-service-map/role-application-server.png) | Uygulama sunucusu |
| ![Veritabanı sunucusu](media/oms-service-map/role-database.png) | Veritabanı sunucusu |
| ![LDAP sunucusu](media/oms-service-map/role-ldap.png) | LDAP sunucusu |
| ![SMB sunucusu](media/oms-service-map/role-smb.png) | SMB sunucusu |

![Rol simgesi](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a>Başarısız bağlantı sayısı
Başarısız bağlantı gösterilmiştir hizmet Haritası eşlemeleri işlemleri ve bilgisayarlar için bir istemci sistemi tooreach başarısız olduğunu belirten kesikli kırmızı bir çizgi bir işlem veya bağlantı noktası. Bu sistem hello bir çalışırken başarısız hello bağlantısı ise başarısız bağlantıları dağıtılan bir hizmet Haritası Aracısı ile herhangi bir sistemden raporlanır. Hizmet eşlemesi bağlantı tooestablish başarısız TCP yuvaları izlenerek bu işlem ölçer. Bir güvenlik duvarı, hello istemci veya sunucu, bir yanlış yapılandırılmasından'ndan bu hataya neden olabilir veya bir uzak hizmeti kullanılabilir durumda.

![Başarısız bağlantı sayısı](media/oms-service-map/failed-connections.png)

Başarısız bağlantı sorunlarını giderme ile geçiş doğrulama, güvenlik analizi ve genel mimari anlama yardımcı olabilir anlama. Başarısız bağlantı bazen zararsız, ancak bunlar genellikle doğrudan aniden ulaşılamaz olmadan bir yük devretme ortamında veya Bulut geçişten sonra oluşturulamıyor tootalk olan iki uygulama katmanı gibi tooa sorun noktası.

## <a name="client-groups"></a>İstemci grupları
İstemci, bağımlılık aracıları olmayan istemci makineler temsil eden kutuları hello haritaya gruplarıdır. Tek bir istemci grubundaki hello istemciler için bir bireysel işlem veya makine temsil eder.

![İstemci grupları](media/oms-service-map/client-groups.png)

toosee hello sunucularının IP adreslerini hello bir istemci grubundaki select hello grubu. Merhaba Grup Merhaba içeriğine hello listelenen **istemci grubu özellikleri** bölmesi.

![İstemci grubu özellikleri](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a>Sunucu bağlantı noktası grupları
Sunucu bağlantı noktası, sunucu bağlantı noktaları bağımlılık aracıları olan değil sunucularda temsil eden kutuları gruplarıdır. Merhaba kutusu hello sunucu bağlantı noktası ve sunucu bağlantıları toothat bağlantı noktası ile Merhaba sayısını sayısını içerir. Merhaba kutusunu toosee hello tek tek sunucular ve bağlantıları genişletin. Merhaba kutusunda tek bir sunucu ise hello adı veya IP adresi listelenir.

![Sunucu bağlantı noktası grupları](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a>Bağlam menüsü
Merhaba üstünde Hello üç nokta (...) tıklayarak herhangi bir sunucu sağındaki bu sunucu için hello bağlam menüsünde görüntüler.

![Başarısız bağlantı sayısı](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a>Yük sunucu eşleme
Tıklatarak **yük Server haritasını** tooa yeni eşleme hello seçili sunucusu hello yeni odak makine olarak alır.

### <a name="show-self-links"></a>Göster kendine bağlantılar
Tıklatarak **Göster Self-Links** herhangi dahil olmak üzere, çizer hello sunucu düğümü kendine bağlantılar, başlangıç ve bitiş hello sunucu içindeki işlemler üzerinde TCP bağlantılarını olduğu. Varsa kendine bağlantılar olan gösterilen menü komutu değişikliklerini çok hello**Gizle Self-Links**, böylece, bunları kapatabilirsiniz.

## <a name="computer-summary"></a>Bilgisayar özeti
Merhaba **makine Özet** bölmesinde bir sunucunun işletim sistemi, bağımlılık sayısı ve diğer Operations Management Suite çözümleri verilerden genel bakış içerir. Bu tür veriler performans ölçümleri, hizmet Masası anahtarları, değişiklik izleme, güvenlik ve güncelleştirmeleri içerir.

![Makine Özet bölmesi](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a>Bilgisayar ve işlem özellikleri
Bir hizmet eşlemini gittiğinizde özellikleri hakkında toogain ek bağlam makineler ve işlemleri seçebilirsiniz. Makineler DNS adı, IPv4 adresleri, CPU ve bellek kapasitesi, VM türü, işletim sistemi ve sürümü, en son yeniden zaman ve bunların Operations Management Suite ve hizmet eşlemesi aracıların hello kimlikleri hakkında bilgi sağlar.

![Makine Özellikler bölmesi](media/oms-service-map/machine-properties.png)

Çalışan işlemleri, işlem adı, işlem açıklaması, kullanıcı adı ve etki alanına katana (Windows), şirket adı, ürün adı, ürün sürümü, çalışma dizini, komut satırı ve işlem de dahil olmak üzere ilgili işletim sistemi meta verilerden işlem ayrıntılarını toplayın Başlangıç zamanı.

![İşlem Özellikler bölmesi](media/oms-service-map/process-properties.png)

Merhaba **işlem özeti** bölmesinde hello işlemin bağlantı, ilişkili bağlantı noktaları, gelen ve giden bağlantılar dahil olmak üzere ilgili ek bilgi sağlar ve bağlantıları başarısız oldu.

![İşlem Özet bölmesi](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a>Operations Management Suite uyarıları tümleştirme
Hizmet eşlemesi hello seçili zaman aralığı içinde seçili sunucusunun hello Operations Management Suite uyarıları harekete tooshow uyarıları ile tümleştirir. Merhaba sunucusu geçerli uyarıları varsa bir simge görüntüler ve hello **makine uyarıları** bölmesi hello uyarıları listeler.

![Makine uyarıları bölmesi](media/oms-service-map/machine-alerts.png)

tooenable hizmet Haritası toodisplay ilgili uyarıları, belirli bir bilgisayar için tetiklenen uyarı kuralı oluşturun. toocreate uygun uyarılar:
- Bilgisayar tarafından yan tümcesi toogroup içerir (örneğin, **bilgisayar aralığı 1 dakika**).
- Ölçüm Ölçümde dayalı tooalert seçin.

![Uyarı yapılandırma](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a>Operations Management Suite günlük olayları tümleştirme
Hizmet eşlemesi ile günlük arama tooshow hello seçilen sunucu için tüm kullanılabilir günlük olaylarının sayısını hello seçili zaman aralığı içinde tümleştirir. Olay sayıları toojump tooLog arama hello listesindeki tüm satır tıklayın ve hello ayrı günlük olaylara bakın.

![Makine günlük olaylarının bölmesi](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a>Operations Management Suite hizmeti Masası tümleştirme
Her iki çözüm de etkin ve Operations Management Suite çalışma alanınızda yapılandırılan hizmet Haritası tümleştirme hello BT Hizmet Yönetimi Bağlayıcısı ile otomatik olarak yapılır. Hizmet eşlemesinde Hello tümleştirme "Hizmet Masasına." olarak etiketlenmiş Daha fazla bilgi için bkz: [merkezi olarak ITSM iş öğelerini BT Hizmet Yönetimi Bağlayıcısı'nı kullanarak yönetme](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview).

Merhaba **makine hizmet Masası** bölmesi hello Seçtiğiniz sunucu hello seçili zaman aralığı içinde tüm BT Hizmet Yönetimi olayları listeler. Geçerli öğe ve bunları hello makine hizmet masasına bölmesinde listeler, simge Hello sunucu görüntüler.

![Makine hizmet masasına bölmesi](media/oms-service-map/service-desk.png)

bağlı ITSM çözümünüzdeki tooopen hello öğesini **görünümü iş öğesi**.

Günlük arama hello öğesinin tooview hello ayrıntılarını tıklatın **Göster günlük aramada**.


## <a name="operations-management-suite-change-tracking-integration"></a>Operations Management Suite değişiklik izleme tümleştirme
Her iki çözüm de etkin ve Operations Management Suite çalışma alanınızda yapılandırılan değişiklik izleme ile hizmet Haritası tümleştirme otomatik olarak yapılır.

Merhaba **makine değişiklik izleme** bölmesi listeler hello en son ile tüm değişiklikler önce bağlantı toodrill tooLog ek ayrıntılar için arama aşağı yanı sıra.

![Makine değişiklik izleme bölmesi](media/oms-service-map/change-tracking.png)

Merhaba aşağıdaki görebileceğiniz bir ConfigurationChange olay ayrıntılı görünümünü görüntüdür seçtikten sonra **Göster günlük analizi**.

![ConfigurationChange olayı](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a>Operations Management Suite performans tümleştirme
Merhaba **makine performansını** bölmesi hello seçili sunucu için standart performans ölçümlerini görüntüler. Merhaba ölçümleri CPU kullanımı, bellek kullanımı, gönderilen ve alınan ağ bayt ve hello üst işlemlerin listesini tarafından gönderilen ve alınan ağ bayt içerir. tooget hello ağ performans verileri, siz de hello Operations Management Suite kablo verileri 2.0 çözümde etkinleştirmiş olmanız gerekir.

![Makine performans bölmesi](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a>Operations Management Suite güvenlik tümleştirme
Her iki çözüm de etkin ve Operations Management Suite çalışma alanınızda yapılandırılmış güvenlik ve Denetim ile hizmet Haritası tümleştirme otomatik olarak yapılır.

Merhaba **makine güvenliği** bölmesi hello hello seçili sunucu için Operations Management Suite güvenlik ve denetim çözümü verileri gösterir. Hello bölmesini hello seçili zaman aralığı içinde hello sunucu için bekleyen güvenlik sorunları özetini listeler. Merhaba güvenlik sorunları ayrıntısına hiçbirini aşağı içine bunları hakkındaki ayrıntılar için günlük arama'yı tıklatın.

![Makine güvenlik bölmesi](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a>Operations Management Suite güncelleştirmeleri tümleştirme
Her iki çözüm de etkin ve Operations Management Suite çalışma alanınızda yapılandırılan güncelleştirme yönetimi ile hizmet Haritası tümleştirme otomatik olarak yapılır.

Merhaba **Makinesi Güncelleştirmeleri** bölmesi hello hello seçili sunucu için Operations Management Suite güncelleştirme yönetimi çözümü verileri görüntüler. Hello bölmesini hello seçili zaman aralığı içinde hello sunucu için eksik güncelleştirmeleri özetini listeler.

![Makine değişiklik izleme bölmesi](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a>Log Analytics kayıtları
Hizmet eşlemesi bilgisayar ve işlem Envanter verileri için kullanılabilir [arama](../log-analytics/log-analytics-log-searches.md) günlük analizi içinde. Geçiş planlaması, kapasite analizi, bulma ve isteğe bağlı performans sorunlarını giderme dahil bu verileri tooscenarios uygulayabilirsiniz.

Her benzersiz bir bilgisayar ve işlem için saat başına bir kayıt oluşturulur ve ayrıca bir işlem veya bilgisayar başlatıldığında veya dahil edilmiş tooService olduğundan, oluşturulan toohello kayıtları eşleştirir. Bu kayıtları tabloları aşağıdaki hello hello özelliklere sahiptir. Merhaba alanlar ve değerler hello ServiceMapComputer_CL olaylarda hello hello ServiceMap Azure Kaynak Yöneticisi API'si makine kaynağında toofields eşleyin. Merhaba alanlar ve değerler hello ServiceMapProcess_CL olaylarda hello hello ServiceMap Azure Kaynak Yöneticisi API'si işlem kaynak toohello alanlarının eşleyin. Merhaba ResourceName_s alan hello karşılık gelen Resource Manager kaynak hello ad alanına eşleşir. 

>[!NOTE]
>Hizmet eşleme özellikleri arttıkça, bu konu toochange alanlardır.

Tooidentify benzersiz işlemleri ve bilgisayarları kullanabileceğiniz dahili olarak oluşturulan özellikleri şunlardır:

- Bilgisayarı: Kullanım ResourceId veya ResourceName_s toouniquely bir Operations Management Suite çalışma alanı içindeki bir bilgisayarı belirleyin.
- İşlem: Kullanım ResourceId toouniquely Operations Management Suite çalışma alanı içindeki bir işlem tanımlayın. ResourceName_s hello makine üzerinde hangi hello (MachineResourceName_s) işlemi çalışmıyor hello bağlamı içinde benzersizdir 

Belirtilen işlem ve belirtilen zaman aralığında bilgisayar için birden çok kayıt bulunabileceğinden sorgular hello için birden fazla kayıt döndürebilir aynı bilgisayarda veya işlemi. tooinclude yalnızca en son kaydına hello Ekle "| Yinelenenleri kaldırma ResourceId"toohello sorgu.

### <a name="servicemapcomputercl-records"></a>ServiceMapComputer_CL kayıtları
Bir tür kayıtlarıyla *ServiceMapComputer_CL* hizmet Haritası aracıları olan sunucular için Envanter verilerini sahip. Bu kayıtları, aşağıdaki tablonun hello hello özelliklere sahiptir:

| Özellik | Açıklama |
|:--|:--|
| Tür | *ServiceMapComputer_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Merhaba hello çalışma alanı içindeki bir makine için benzersiz tanımlayıcı |
| ResourceName_s | Merhaba hello çalışma alanı içindeki bir makine için benzersiz tanımlayıcı |
| ComputerName_s | Merhaba bilgisayar FQDN'si |
| Ipv4Addresses_s | Merhaba sunucunun IPv4 adresleri listesi |
| Ipv6Addresses_s | Merhaba sunucunun IPv6 adresleri listesi |
| DnsNames_s | DNS adları dizisi |
| OperatingSystemFamily_s | Windows veya Linux |
| OperatingSystemFullName_s | Merhaba hello işletim sisteminin tam adı  |
| Bitness_s | Merhaba verileri hello makinenin (32 bit veya 64 bit)  |
| PhysicalMemory_d | Merhaba MB fiziksel bellek |
| Cpus_d | Merhaba CPU sayısı |
| CpuSpeed_d | Merhaba MHz CPU hızı|
| VirtualizationState_s | *Bilinmeyen*, *fiziksel*, *sanal*, *hiper yönetici* |
| VirtualMachineType_s | *hyperv*, *vmware*, vb. |
| VirtualMachineNativeMachineId_g | Merhaba, hiper yönetici tarafından atanan VM kimliği |
| VirtualMachineName_s | Merhaba VM Hello adı |
| BootTime_t | Merhaba önyükleme saati |



### <a name="servicemapprocesscl-type-records"></a>ServiceMapProcess_CL türünde kayıtları
Bir tür kayıtlarıyla *ServiceMapProcess_CL* hizmet Haritası aracılarıyla sunucularında TCP bağlı işlemler için Envanter verilerini sahip. Bu kayıtları, aşağıdaki tablonun hello hello özelliklere sahiptir:

| Özellik | Açıklama |
|:--|:--|
| Tür | *ServiceMapProcess_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Merhaba hello çalışma alanı içindeki bir işlem için benzersiz tanımlayıcı |
| ResourceName_s | Merhaba üzerinde çalıştığı hello makine içinde bir işlem için benzersiz tanımlayıcı|
| MachineResourceName_s | Merhaba makinenin Hello kaynak adı |
| ExecutableName_s | Merhaba işlem yürütülebilir dosyası Hello adı |
| StartTime_t | Merhaba işlem havuzu başlangıç zamanı |
| FirstPid_d | Merhaba ilk PID hello işlem havuzunda |
| Description_s | Merhaba işlem açıklaması |
| CompanyName_s | Merhaba şirketin Hello adı |
| InternalName_s | Merhaba iç adı |
| ProductName_s | Merhaba ürün Hello adı |
| ProductVersion_s | Merhaba ürün sürümü |
| FileVersion_s | Merhaba dosya sürümü |
| CommandLine_s | Merhaba komut satırı |
| ExecutablePath _Yanları | Merhaba yol toohello yürütülebilir dosya |
| WorkingDirectory_s | Merhaba çalışma dizini |
| Kullanıcı adı | Merhaba hesabı altında hangi hello işlemi yürütülüyor |
| UserDomain | Merhaba etki alanı altında hangi hello işlemi yürütülüyor |


## <a name="sample-log-searches"></a>Örnek günlük aramaları

### <a name="list-all-known-machines"></a>Bilinen tüm makineler listesi
Tür ServiceMapComputer_CL = | Yinelenenleri kaldırma ResourceId

### <a name="list-hello-physical-memory-capacity-of-all-managed-computers"></a>Yönetilen tüm bilgisayarlara Hello fiziksel bellek kapasitesi listeleyin.
Tür ServiceMapComputer_CL = | PhysicalMemory_d, ComputerName_s seçin | Yinelenenleri kaldırma ResourceId

### <a name="list-computer-name-dns-ip-and-os"></a>Liste bilgisayar adı, DNS, IP ve işletim sistemi.
Tür ServiceMapComputer_CL = | seçin ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s | Yinelenenleri kaldırma ResourceId

### <a name="find-all-processes-with-sql-in-hello-command-line"></a>Tüm işlemlerle "sql" Merhaba komut satırında Bul
Tür ServiceMapProcess_CL CommandLine_s = = \*sql\* | ResourceId yinelenenleri kaldırma

### <a name="find-a-machine-most-recent-record-by-resource-name"></a>Bir makine (en son kayıt) tarafından kaynak adı bulunamadı
Türü ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" = | Yinelenenleri kaldırma ResourceId

### <a name="find-a-machine-most-recent-record-by-ip-address"></a>IP adresini kullanarak bir makine (en son kayıt) bulunamadı
Türü ServiceMapComputer_CL "10.229.243.232" = | Yinelenenleri kaldırma ResourceId

### <a name="list-all-known-processes-on-a-specified-machine"></a>Belirtilen bir makinedeki tüm bilinen işlemleri listele
Tür ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b =" | Yinelenenleri kaldırma ResourceId

### <a name="list-all-computers-running-sql"></a>SQL çalıştıran tüm bilgisayarları listeleyin
Tür ServiceMapComputer_CL ResourceName_s IN = {türü ServiceMapProcess_CL = \*sql\* | Ayrı MachineResourceName_s} | Yinelenenleri kaldırma ResourceId | Farklı ComputerName_s

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a>My veri merkezinde curl tüm benzersiz ürün sürümleri listesi
Tür ServiceMapProcess_CL ExecutableName_s = curl = | Farklı ProductVersion_s

### <a name="create-a-computer-group-of-all-computers-running-centos"></a>CentOS çalıştıran tüm bilgisayarları bir bilgisayar grubu oluştur
Tür ServiceMapComputer_CL OperatingSystemFullName_s = = \*CentOS\* | Farklı ComputerName_s


## <a name="rest-api"></a>REST API
Tüm hello sunucu, işlem ve bağımlılık verileri hizmet Haritası hello kullanılabilir [hizmet eşlemesi REST API](https://docs.microsoft.com/rest/api/servicemap/).


## <a name="diagnostic-and-usage-data"></a>Tanılama ve kullanım verileri
Microsoft otomatik olarak hello hizmet Haritası hizmet kullanımınız vasıtasıyla kullanım ve performans verilerini toplar. Microsoft hello kalite, güvenlik ve hello hizmet Haritası hizmet bütünlüğünü geliştirmek ve bu verileri tooprovide kullanır. hello verileri tooprovide doğru ve etkili sorun giderme özellikleri, işletim sistemi ve sürümü, IP adresi, DNS adı ve iş istasyonu adı gibi yazılımınızın hello yapılandırma hakkında bilgi içerir. Microsoft, ad, adres veya diğer kişi bilgilerini toplamaz.

Veri toplama ve kullanım hakkında daha fazla bilgi için bkz: Merhaba [Microsoft Online Services gizlilik bildirimi](https://go.microsoft.com/fwlink/?LinkId=512132).


## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [oturum aramaları](../log-analytics/log-analytics-log-searches.md) hizmet Haritası tarafından toplanan günlük analizi tooretrieve veri.


## <a name="troubleshooting"></a>Sorun giderme
Merhaba bkz [sorun giderme bölümüne hello yapılandırma hizmet Haritası belgenin](operations-management-suite-service-map-configure.md#troubleshooting).


## <a name="feedback"></a>Geri Bildirim
Tüm geri bildirim bize hizmet haritası veya bu belge hakkında var?  Ziyaret bizim [kullanıcı sesi sayfa](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), buradan özellikleri önermek veya varolan önerileri oy verin.

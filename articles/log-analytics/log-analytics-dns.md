---
title: "aaaDNS Azure günlük analizi Analytics çözümde | Microsoft Docs"
description: "Ayarlama ve DNS altyapısının güvenlik, performans ve işlem günlük analizi toogather Öngörüler hello DNS analiz çözümü kullanın."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f44a40c4-820a-406e-8c40-70bd8dc67ae7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: be7982c54b65ba0c4b1c15ae7516d02eced313f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="gather-insights-about-your-dns-infrastructure-with-hello-dns-analytics-preview-solution"></a>DNS altyapınızın hello DNS Analytics Önizleme çözüm ile ilgili Öngörüler toplayın

![DNS Analytics simgesi](./media/log-analytics-dns/dns-analytics-symbol.png)

Bu makalede, nasıl Azure günlük analizi toogather DNS altyapısının güvenlik, performans ve işlemleri hakkında fikir Azure DNS Analytics çözümde tooset ayarlama ve kullanma hello açıklanmaktadır.

DNS Analytics size yardımcı olur:

- Tooresolve kötü amaçlı etki alanı adlarını deneyin istemcileri belirleyin.
- Eski kaynak kayıtları tanımlayın.
- Sık sık sorgulanan etki alanı adları ve talkative DNS istemcileri belirleyin.
- DNS sunucuları üzerindeki görünüm isteği yükü.
- Dinamik DNS kayıt hataları görüntüleyin.

Merhaba çözüm toplar, analiz eder ve Windows DNS Analitik ve Denetim günlükleri ve diğer ilgili veriler, DNS sunucularınızın karşılık gelen.

## <a name="connected-sources"></a>Bağlı kaynaklar

Aşağıdaki tablonun hello bu çözümü tarafından desteklenen hello bağlı kaynakları açıklanmaktadır:

| **Bağlı kaynak** | **Destek** | **Açıklama** |
| --- | --- | --- |
| [Windows aracıları](log-analytics-windows-agents.md) | Evet | Merhaba çözüm Windows aracılardan DNS bilgilerini toplar. |
| [Linux aracıları](log-analytics-linux-agents.md) | Hayır | Merhaba çözüm doğrudan Linux aracılarını DNS bilgilerini toplamaz. |
| [System Center Operations Manager yönetim grubu](log-analytics-om-agents.md) | Evet | Merhaba çözüm aracıları bağlı Operations Manager yönetim grubunda DNS bilgilerini toplar. Merhaba Operations Manager Aracısı toohello Operations Management Suite arasında doğrudan bağlantı gerekli değildir. Veri hello yönetim grubu toohello Operations Management Suite depodan iletilir. |
| [Azure depolama hesabı](log-analytics-azure-storage.md) | Hayır | Azure depolama hello çözümü tarafından kullanılmaz. |

### <a name="data-collection-details"></a>Veri toplama ayrıntıları

Merhaba çözüm DNS envanteri ve DNS olay ilgili verileri hello DNS sunucularından günlük analizi Aracısı yüklendiği toplar. Bu veriler sonra tooLog Analytics karşıya ve hello çözüm panosunda görüntülenir. DNS sunucuları, bölge ve kaynak kayıtları, hello sayısı gibi envanterle ilişkili veri hello DNS PowerShell cmdlet'lerini çalıştırarak toplanır. Merhaba veriler iki günde bir kez güncelleştirilir. Merhaba olayı ile ilgili veriler hello gerçek zamanlı toplanan [Analitik ve Denetim günlükleri](https://technet.microsoft.com/library/dn800669.aspx#enhanc) Gelişmiş DNS günlüğe kaydetme ve tanılama Windows Server 2012 R2 tarafından sağlanan.

## <a name="configuration"></a>Yapılandırma

Bilgi tooconfigure hello çözümü aşağıdaki hello kullan:

- Bilmeniz gereken bir [Windows](log-analytics-windows-agents.md) veya [Operations Manager](log-analytics-om-agents.md) toomonitor istediğiniz her DNS sunucusunda Aracısı.
- Merhaba DNS analiz çözümü tooyour Operations Management Suite çalışma hello ekleyebilirsiniz [Azure Marketi](https://aka.ms/dnsanalyticsazuremarketplace). Açıklanan hello işlemi de kullanabilirsiniz [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).

Merhaba çözüm başka yapılandırmasının hello gerek kalmadan veri toplamayı başlatır. Bununla birlikte, yapılandırma toocustomize veri toplama aşağıdaki hello kullanabilirsiniz.

### <a name="configure-hello-solution"></a>Merhaba çözümünüzü yapılandırma

Merhaba çözüm panosunda tıklatın **yapılandırma** tooopen hello DNS Analytics yapılandırma sayfası. Yaptığınız yapılandırma değişikliklerini iki tür vardır:

- **Güvenilenler listesine etki alanı adları**. Merhaba çözüm tüm hello arama sorguları işlemez. Etki alanı adı soneklerinin beyaz liste tutar. etki alanı adı soneklerinin bu beyaz liste içinde eşleşen toohello etki alanı adlarını çözümlemek hello arama sorguları hello çözümü tarafından işlenmez. Güvenilenler listesine etki alanı adları işlenmiyor tooLog Analytics gönderilen toooptimize hello veri yardımcı olur. Merhaba varsayılan beyaz liste www.google.com ve www.facebook.com gibi popüler ortak etki alanı adlarını içerir. Kaydırarak hello tam varsayılan listesini görüntüleyebilirsiniz.

 Merhaba listesi tooadd tooview arama öngörüleri için istediğiniz herhangi bir etki alanı adı soneki değiştirebilirsiniz. Ayrıca tooview arama öngörüleri için istemediğiniz tüm etki alanı adı soneki kaldırabilirsiniz.

- **Talkative istemci eşiği**. Arama istekleri Hello sayısı hello vurgulanmıştır için hello eşiğini aşan DNS istemcilerini **DNS istemcileri** dikey. Merhaba varsayılan eşik 1. 000 ' dir. Merhaba eşik düzenleyebilirsiniz.

    ![Güvenilenler listesine etki alanı adları](./media/log-analytics-dns/dns-config.png)

## <a name="management-packs"></a>Yönetim paketleri

Merhaba Microsoft İzleme Aracısı tooconnect tooyour Operations Management Suite çalışma kullanıyorsanız, hello aşağıdaki yönetim paketi yüklenir:

- Microsoft DNS veri toplayıcı zeka Paketi'ni (Microsft.IntelligencePacks.Dns)

Operations Manager yönetim grubunuzu bağlı tooyour Operations Management Suite çalışma ise, bu çözüm eklediğinizde hello aşağıdaki yönetim paketleri Operations Manager'da yüklenir. Gerekli yapılandırma veya bu yönetim paketlerinin bakım yoktur:

- Microsoft DNS veri toplayıcı zeka Paketi'ni (Microsft.IntelligencePacks.Dns)
- Microsoft System Center Advisor DNS Analizi Yapılandırması (Microsoft.IntelligencePack.Dns.Configuration)

Çözüm yönetim paketleri güncelleştirilme biçimini daha fazla bilgi için bkz: [Operations Manager bağlanmak tooLog Analytics](log-analytics-om-agents.md).

## <a name="use-hello-dns-analytics-solution"></a>Merhaba DNS analiz çözümü kullanın

Bu bölümde, tüm hello Pano işlevleri açıklanır ve nasıl toouse bunları.

Merhaba çözüm tooyour çalışma ekledikten sonra hello çözüm kutucuğu hello Operations Management Suite'e genel bakış sayfasında DNS altyapınızın kısa bir Özet sağlar. Burada hello veri toplanırken DNS sunucularının sayısı hello içerir. Ayrıca istemcileri tooresolve kötü amaçlı etki alanı tarafından hello son 24 saat yapılan istekleri hello sayısını içerir. Merhaba kutucuğa tıkladığınızda hello çözüm panosu açılır.

![DNS Analytics döşeme](./media/log-analytics-dns/dns-tile.png)

### <a name="solution-dashboard"></a>Çözüm panosu

Hello çözüm Panosu hello çözümünün çeşitli özelliklerini hello özet bilgilerini gösterir. Ayrıca bağlantılarını içerir toohello ayrıntılı görünümünü adli çözümleme ve tanılama. Varsayılan olarak, son yedi gün için hello hello veri gösterilmektedir. Hello kullanarak hello tarih ve saat aralığı değiştirebilirsiniz **tarih-saat seçim denetimi**hello görüntü aşağıdaki gösterildiği gibi:

![Zamanı seçim denetimi](./media/log-analytics-dns/dns-time.png)

Merhaba çözüm Panosu Kanatlar aşağıdaki hello gösterir:

**DNS güvenliği**. Kötü amaçlı etki alanlarıyla toocommunicate çalıştığınız hello DNS istemcileri raporlar. Microsoft tehdit bilgisi akışlarını kullanarak DNS Analytics istemci tooaccess kötü amaçlı etki alanları çalıştığınız IP'leri algılayabilir. Çoğu durumda, kötü amaçlı yazılımdan etkilenen aygıtların "çevirme" toohello "komut ve Denetim" merkezi çözme tarafından hello kötü amaçlı etki alanının hello kötü amaçlı yazılım etki alanı adı.

![DNS güvenlik dikey penceresi](./media/log-analytics-dns/dns-security-blade.png)

İstemci IP hello listesinde tıkladığınızda, günlük arama açar ve hello ilgili sorgu hello arama ayrıntılarını gösterir. Merhaba iletişimi ile yapıldığı DNS Analytics aşağıdaki örneğine hello, algılanan bir [Ircbot](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=Win32/IRCbot):

![Ircbot gösteren bir günlük arama sonuçları](./media/log-analytics-dns/ircbot.png)

Merhaba bilgi tooidentify sağlar:

- İstemci hello iletişimi başlatan IP.
- Toohello kötü amaçlı IP çözümler etki alanı adı.
- Etki alanı adı çözümlenecek şekilde hello IP adresleri.
- Kötü amaçlı IP adresi.
- Merhaba sorunun önem derecesi.
- Merhaba kötü amaçlı IP kara liste nedeni.
- Algılama zamanı.

**Sorgulanan etki alanları**. Merhaba, ortamınızdaki hello DNS istemcileri tarafından sorgulanan en sık rastlanan etki alanı adlarını sağlar. Sorgulanan tüm hello etki alanı adlarının hello listesini görüntüleyebilirsiniz. Ayrıca aşağı hello arama istek ayrıntıları günlük arama belirli etki alanı adı ayrıntılarına geçebilir.

![Etki alanları sorgulanan dikey penceresi](./media/log-analytics-dns/domains-queried-blade.png)

**DNS istemcileri**. Raporları hello istemcileri *ihlal hello eşik* süre seçilen hello sorguları sayısı. Merhaba listesini tüm hello DNS istemcileri ve onlar tarafından günlük aramada yapılan hello sorguları hello ayrıntılarını görüntüleyebilirsiniz.

![DNS istemcileri dikey penceresi](./media/log-analytics-dns/dns-clients-blade.png)

**Dinamik DNS kayıtları**. Raporları kayıt hataları adı. Adres için tüm kayıt hataları [kaynak kayıtları](https://en.wikipedia.org/wiki/List_of_DNS_record_types) (tür A ve AAAA) hello istemci hello kayıt istekleri IP'leri birlikte vurgulanır. Ardından, aşağıdaki adımları izleyerek bu bilgileri toofind hello kök nedenini hello kayıt hatası kullanarak şunları yapabilirsiniz:

1. İstemci hello hello ad için yetkiliyse hello bölge tooupdate çalışıyor bulun.

2. Bu bölgenin Hello çözüm toocheck hello Envanter bilgileri kullanın.

3. Merhaba bölge etkinleştirilmişse hello dinamik güncelleştirmenin doğrulayın.

4. Merhaba bölge güvenli dinamik güncelleştirme için yapılandırılmış olup olmadığı olup olmadığını denetleyin.

    ![Dinamik DNS kayıtları dikey penceresi](./media/log-analytics-dns/dynamic-dns-reg-blade.png)

**Ad kaydı istekleri**. Merhaba üst döşemeyi başarılı ve başarısız DNS dinamik güncelleştirme isteklerinin bir eğilim çizgisi gösterir. Merhaba alt bölme başarısız DNS güncelleştirme isteklerini toohello DNS sunucuları, hataları hello sayısına göre sıralanmış gönderme hello ilk 10 istemcilerini listeler.

![Ad kaydı istekleri dikey penceresi ](./media/log-analytics-dns/name-reg-req-blade.png)

**Örnek DDI analitik sorguları**. Ham analiz verileri doğrudan fetch hello en yaygın arama sorguları listesini içerir.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Örnek sorgular](./media/log-analytics-dns/queries.png)

Özelleştirilmiş raporlama için kendi sorguları oluşturmak için bu sorguları bir başlangıç noktası olarak kullanabilirsiniz. Merhaba sorgu sonuçları görüntülendiği toohello DNS Analytics günlük arama sayfası Bağla:

- **DNS sunucularının listesini**. Bunların ilişkili FQDN, etki alanı adı, orman adı ve sunucu IP'leri ile tüm DNS sunucularının bir listesini gösterir.
- **DNS bölgelerinin listesi**. Tüm DNS bölgelerini hello ilişkili bölge adı, dinamik güncelleştirme durumu, ad sunucuları ve DNSSEC imzalama durumu ile bir listesini gösterir.
- **Kullanılmayan kaynak kayıtları**. Tüm hello kullanılmayan/eski kaynak kayıtlarının bir listesini gösterir. Bu liste hello kaynak kayıt adı, kaynak kaydı türü, ilişkili hello DNS sunucusu, kayıt oluşturma zamanı ve bölge adını içerir. Artık kullanımda olmayan bu liste tooidentify hello DNS kaynak kayıtlarını kullanabilirsiniz. Bu bilgilere dayanarak, ardından girişler hello DNS sunucularından silebilirsiniz.
- **DNS sunucularını sorgulamak yük**. Böylece, DNS sunucularınızın DNS yük hello açısından alabilir bilgileri gösterir. Bu bilgiler hello kapasite hello sunucuları için planlama yapmanıza yardımcı olabilir. Toohello gidebilirsiniz **ölçümleri** sekmesinde toochange hello görünüm tooa grafik görselleştirme. Bu görünüm, hello DNS yüklemek, DNS sunucularınızın arasında nasıl dağıtıldığını anlamanıza yardımcı olur. Bu DNS sorgusu her sunucu için oranı eğilimlerini gösterir.

    ![DNS sunucuları sorgu günlüğü arama sonuçları](./media/log-analytics-dns/dns-servers-query-load.png)

- **DNS bölgelerini sorgu yük**. Merhaba çözümü tarafından yönetilen hello DNS sunucularında Hello tüm hello bölgeleri DNS bölge sorgu başına saniye istatistiklerini gösterir. Merhaba tıklatın **ölçümleri** sekmesinde toochange hello görünümünden ayrıntılı kayıtları tooa grafik görselleştirme hello sonuçları.
- **Yapılandırma olayları**. Tüm hello DNS yapılandırma değişikliği olayları ve ilişkili iletileri gösterir. Daha sonra bu olayları hello olay, olay kimliği, DNS sunucusunun zamana dayalı filtre ya da görev kategorisi. Merhaba veri değişikliklerinin toospecific DNS sunucuları belirli zamanlarda denetim yardımcı olabilir.
- **DNS analitik günlük**. Merhaba çözümü tarafından yönetilen tüm hello DNS sunucularındaki tüm hello analitik olayları gösterir. Sonra bu olayları hello olay, olay kimliği, DNS sunucusu, arama sorgusu hello ve türü görev kategorisi sorgu yapılan istemci IP zamanında göre filtreleyebilirsiniz. DNS sunucusu analitik olaylarını etkinlik hello DNS sunucusunda izlemeyi etkinleştirin. Analitik olaya hello sunucu gönderdiğinde veya DNS bilgilerini aldığında her zaman günlüğe kaydedilir.

### <a name="search-by-using-dns-analytics-log-search"></a>DNS Analytics günlük arama kullanarak arama

Merhaba günlük arama sayfasında, bir sorgu oluşturabilirsiniz. Model denetimlerini kullanarak arama sonuçlarınızı filtreleyebilirsiniz. Gelişmiş sorgular tootransform, filtre ve rapor sonuçlarınıza oluşturabilirsiniz. Sorguları aşağıdaki hello kullanarak başlatın:

1. Merhaba, **arama sorgusu kutusunu**, türü `Type=DnsEvents` tüm hello hello çözümü tarafından yönetilen hello DNS sunucuları tarafından oluşturulan DNS olayları tooview. Merhaba sonuçlar hello günlük verilerini tüm olayları ilgili toolookup sorgular, dinamik kayıtlar ve yapılandırma değişiklikleri listeler.

    ![DnsEvents günlük arama](./media/log-analytics-dns/log-search-dnsevents.png)  

    a. arama sorguları için tooview hello günlük verileri seçin **LookUpQuery** hello olarak **alt** hello soldaki hello modeli denetiminden filtre. Seçilen zaman aralığı hello için tüm hello arama sorgusu olayları listeleyen bir tablo görüntülenir.

    b. dinamik kayıtlar için tooview hello günlük verileri seçin **DynamicRegistration** hello olarak **alt** hello soldaki hello modeli denetiminden filtre. Seçilen zaman aralığı hello için tüm hello dinamik kayıt olayları listeleyen bir tablo görüntülenir.

    c. yapılandırma değişiklikleri için tooview hello günlük verileri seçin **ConfigurationChange** hello olarak **alt** hello soldaki hello modeli denetiminden filtre. Zaman aralığı seçili hello için tüm hello yapılandırma değişikliği olayları listeleyen bir tablo görüntülenir.

2. Merhaba, **arama sorgusu kutusunu**, türü `Type=DnsInventory` tüm hello hello çözümü tarafından yönetilen hello DNS sunucuları için DNS envanterle ilişkili veri tooview. Merhaba sonuçlar DNS sunucuları, DNS bölgeleri ve kaynak kayıtları için hello günlük verileri listeler.

    ![DnsInventory günlük arama](./media/log-analytics-dns/log-search-dnsinventory.png)

## <a name="feedback"></a>Geri Bildirim

Geri bildirimde iki yolu vardır:

- **UserVoice**. Fikir DNS Analytics özellikleri toowork için ileti. Merhaba ziyaret [Operations Management Suite UserVoice sayfa](https://aka.ms/dnsanalyticsuservoice).
- **Bizim kohort katılma**. Her zaman bizim cohorts tooget erken erişim toonew özelliklerini birleştirme ve DNS Analytics iyileştirmemize yardımcı olun yeni müşteriler sahip ilginizi çalışıyoruz. Bizim cohorts birleştirme ilgileniyorsanız doldurmak [hızlı anketi](https://aka.ms/dnsanalyticssurvey).

## <a name="next-steps"></a>Sonraki adımlar

[Arama günlüklerini](log-analytics-log-searches.md) tooview ayrıntılı DNS günlüğüne kaydeder.

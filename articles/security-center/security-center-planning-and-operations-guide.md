---
title: "aaaSecurity merkezi planlama ve işlemler Kılavuzu | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi ve günlük işlemlere ilişkin dikkat edilecek noktalar benimsemeden önce tooplan sağlar."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Azure Güvenlik Merkezi planlama ve işlemler kılavuzu
Bu kılavuz, bilgi teknolojisi (BT) uzmanları, BT mimarları, bilgi güvenlik Çözümleyicileri ve bulut Yöneticiler, kuruluşlarının toouse Azure Güvenlik Merkezi planlama için ' dir.

>[!NOTE] 
>İçinde erken Haziran 2017'den itibaren Güvenlik Merkezi hello Microsoft İzleme Aracısı toocollect kullanmak ve verileri depolamak. Bkz: [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md) toolearn daha fazla. Bu makaledeki Hello bilgiler geçiş toohello sonra Microsoft İzleme Aracısı Güvenlik Merkezi işlevlerini temsil eder.
>

## <a name="planning-guide"></a>Planlama Kılavuzu
Bu kılavuz, bir dizi adımı ve Güvenlik Merkezi kullanımınızı, kuruluşunuzun güvenlik gereksinimlerine ve bulut Yönetimi modeline göre toooptimize izleyebileceğiniz kapsar. Güvenlik Merkezi tam anlamıyla tootake, önemli toounderstand nasıl farklı kişilerin olduğu, ya da içinde ekipleri kuruluşunuz hello hizmet toomeet güvenli geliştirme ve, sıra işlem, izleme, kullanma ve olay yanıtı gereksinimlerini. toouse Güvenlik Merkezi planlama yaparken hello önemli alanlar tooconsider şunlardır:

* Güvenlik Rolleri ve Erişim Denetimleri
* Güvenlik İlkeleri ve Öneriler
* Veri Koleksiyonu ve Storage
* Devam Eden Güvenlik İzleme
* Olay Yanıtı

Merhaba sonraki bölümde, öğreneceksiniz nasıl tooplan bu alanların her biri için ve bu önerileri gereksinimlerinize göre geçerlidir.

> [!NOTE]
> Okuma [Azure Güvenlik Merkezi sık sorulan sorular (SSS)](security-center-faq.md) tasarlama ve planlama aşaması hello sırasında da faydalı olabilecek sık sorulan sorular listesi.
> 

## <a name="security-roles-and-access-controls"></a>Güvenlik rolleri ve erişim denetimleri
Merhaba boyutuna ve kuruluşunuzun yapısına bağlı olarak, birden çok kişi ve ekip Güvenlik Merkezi tooperform farklı güvenlikle ilgili görevleri kullanabilir. Aşağıdaki diyagramda hello kurgusal kişiler ve ilgili rollerin ve güvenlik sorumluluklarının örneği vardır:

![Roller](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

Güvenlik Merkezi bu kişiler toomeet çeşitli bu Sorumluluklar sağlar. Örneğin:

**Ömer (Bulut İş Yükü Sahibi)**

* Bir bulut iş yükünü ve onunla ilgili kaynakları yönetme
* Korumaları şirket güvenlik ilkesiyle uyumlu bir şekilde uygulamak ve sürdürmekle sorumlu

**Emel (CISO/CIO)**

* Merhaba şirket için güvenliği tüm yönleriyle sorumlu
* Bulut iş yüklerinde toounderstand hello şirketin güvenlik tutumunu istediği
* Ana saldırıları ve riskleri haberdar toobe gerekiyor

**Ali (BT Güvenliği)**

* Güvenlik ilkeleri tooensure hello uygun korumalar yerinde olduğundan kümeleri şirket
* İlkelerle uyumluluğu izler
* Yöneticiler veya denetçiler için raporlar oluşturur

**Zehra (Güvenlik İşlemleri)**

* İzler ve toosecurity uyarıları 7/24 yanıt verir
* TooCloud iş yükü sahibi ya da BT güvenlik Analistin iletir

**Salih (Güvenlik Analisti)**

* Atakları araştırır
* Bulut iş yükü sahibi tooapply düzeltme ile çalışma 

Güvenlik Merkezi kullanır [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md), sağlayan [yerleşik roller](../active-directory/role-based-access-built-in-roles.md) atanabilen toousers, grupları ve Azure Hizmetleri. Güvenlik Merkezi bir kullanıcı oturum açtığında, bunlar yalnızca bilgi ilgili sahip oldukları erişim tooresources. Hangi hello kullanıcı bir kaynağa ait olduğu sahibi, katkıda bulunan veya okuyucu toohello abonelik veya kaynak grubu hello rolü atanmış anlamına gelir. Toplama toothese rollerinde iki belirli Güvenlik Merkezi rolü vardır:

- **Güvenlik okuyucu**: toothis rolüne ait kullanıcı mümkün tooview hakları tooSecurity öneriler, uyarılar, ilke ve durumunu içeren, merkezi olması ancak mümkün toomake değişiklikler kaydedilmeyecek.
- **Güvenlik Yönetim**: güvenlik okuyucu ancak hello güvenlik ilkesi güncelleştirebilirsiniz gibi aynı önerileri ve uyarılar yok sayın.

Yukarıda açıklanan hello Güvenlik Merkezi rolleri Azure depolama, Web ve mobil veya nesnelerin interneti gibi erişim tooother hizmet alanlarına sahip değilsiniz.  

> [!NOTE]
> Bir kullanıcının en az bir abonelik, kaynak grubunun sahibi veya katkıda bulunan toobe mümkün toosee Azure Güvenlik Merkezi'nde toobe gerekir. 
> 
> 

Merhaba kişiler kullanarak hello önceki diyagramda şu RBAC gerekir hello açıklanmıştır:

**Ömer (Bulut İş Yükü Sahibi)**

* Kaynak Grubu Sahibi/Ortak Çalışanı

**Ali (BT Güvenliği)**

* Abonelik Sahibi/Ortak Çalışan veya Güvenlik Yöneticisi

**Zehra (Güvenlik İşlemleri)**

* Abonelik okuyucusu veya güvenlik okuyucu tooview uyarıları
* Abonelik sahibi/ortak çalışanı ya da güvenlik Admin toodismiss uyarıları gerekli

**Salih (Güvenlik Analisti)**

* Abonelik okuyucusu tooview uyarıları
* Abonelik sahibi/ortak çalışanı toodismiss uyarıları gerekli
* Erişim toohello çalışma gerekli olabilir

Bazı diğer önemli bilgiler tooconsider:

* Güvenlik ilkesini yalnızca abonelik Sahipleri/Katkıda Bulunanları ve Güvenlik Yöneticileri düzenleyebilir
* Yalnızca abonelik ve kaynak grubu Sahipleri ve Katkıda bulunanları bir kaynak için güvenlik önerilerini uygulayabilir.

Güvenlik Merkezi için RBAC kullanarak erişim denetimini planlarken kuruluşunuzda kimlerin Güvenlik Merkezi'ni kullanarak toounderstand emin olun. Ayrıca, bunların hangi türde görevler gerçekleştireceğini anlayın ve daha sonra RBAC’yi buna göre yapılandırın.

> [!NOTE]
> Merhaba atamanızı öneririz az izin veren rol görevlerini kullanıcılar toocomplete için gerekli. Örneğin, kullanıcılar yalnızca kaynakların güvenlik durumu hello hakkında tooview bilgi gerekir ancak önerileri uygulamak veya ilkeleri düzeltmek gibi bir eylemde bulunmamasını hello okuyucu rolüne atanmaları gerekir.
> 
> 

## <a name="security-policies-and-recommendations"></a>Güvenlik ilkeleri ve öneriler
Bir güvenlik ilkesi belirtilen hello içindeki kaynaklar için önerilen denetimleri hello kümesini tanımlayan abonelik. Güvenlik Merkezi'nde tooyour şirketinizin güvenlik gereksinimleri ve uygulamaların hello türü veya hello verilerin duyarlılığına göre ilkeleri tanımlarsınız.

Merhaba abonelik düzeyinde otomatik olarak etkinleştirilen ilkeler hello Aşağıdaki diyagramda gösterildiği gibi hello abonelik içindeki tooall kaynak gruplarına yayılması:

![Güvenlik İlkeleri](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> Hangi ilkelerin değiştirildi tooreview gerekiyorsa, kullanabileceğiniz [Azure denetim günlükleri](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/). İlke değişiklikleri her zaman Azure Denetim Günlükleri'ne kaydedilir.
> 
> 

### <a name="security-recommendations"></a>Güvenlik önerileri
Güvenlik ilkelerini yapılandırmadan önce her hello gözden [güvenlik önerileri](security-center-recommendations.md)ve bu ilkeler çeşitli Abonelikleriniz ve kaynak grupları için uygun olup olmadığını belirler. Hangi eylemi tooaddress gerçekleştirilmelidir da önemli toounderstand olan [güvenlik önerileri](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) ve kuruluşunuzda kimlerin yeni önerileri ve alma hello adımları gerektiği için izlemekten sorumlu.

Güvenlik Merkezi, Azure aboneliğiniz için güvenlik kişi ayrıntılarını sağlamanızı önerir. Bu bilgiler Microsoft toocontact tarafından kullanılır, hello Microsoft Güvenlik Yanıt Merkezi (MSRC) müşteri verilerinizi yasadışı veya yetkisiz bir şirket tarafından erişilen olduğunu belirlerse. Okuma [Azure Güvenlik Merkezi'nde güvenlik iletişim ayrıntılarını sağlamak](security-center-provide-security-contact-details.md) hakkında daha fazla bilgi için tooenable Bu öneri.

## <a name="data-collection-and-storage"></a>Veri koleksiyonu ve depolama
Azure Güvenlik Merkezi, Microsoft Monitoring Agent hello kullanır – aynı aracı kullanılan hello hello Operations Management Suite ve günlük analizi hizmeti – toocollect güvenlik verileri, sanal makineleriniz tarafından budur. Bu aracıdan toplanan veriler, Log Analytics çalışma alanlarınızda depolanır.

### <a name="agent"></a>Aracı

Veri toplama hello güvenlik ilkesinde etkinleştirildikten sonra Microsoft Monitoring Agent hello (için [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) veya [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) tüm desteklenen Azure Vm'leri ve oluşturulan yeni bir tane yüklenir.  VM hello yüklü, Microsoft İzleme Aracısı zaten hello Azure Güvenlik Merkezi hello geçerli özelliğinden yararlanır aracısının yüklü. Merhaba aracının işlemi tasarlanmış toobe bozucu olan ve VM performans üzerinde çok az etkisi.

Microsoft İzleme Aracısı için Windows Hello kullan TCP bağlantı noktası 443'ü gerektirir. Merhaba bkz [sorun giderme makalesi](security-center-troubleshooting-guide.md) ek ayrıntılar için.

Belirli bir noktada toodisable veri toplama istiyorsanız, bunu hello güvenlik ilkesinde kapatabilirsiniz. Ancak, çünkü hello Microsoft Monitoring Agent diğer Azure Yönetimi tarafından kullanılabilir ve hizmetlerini izleme, hello Aracısı otomatik olarak kaldırılmayacak zaman Güvenlik Merkezi'nde veri koleksiyonunu devre dışı. Merhaba aracısını, gerektiğinde el ile kaldırabilirsiniz.

> [!NOTE]
> toofind hello okuma desteklenen VM'lerin listesini [Azure Güvenlik Merkezi sık sorulan sorular (SSS)](security-center-faq.md).
> 

### <a name="workspace"></a>Çalışma alanı

Microsoft Monitoring Agent (adına, Azure Güvenlik Merkezi) ya da bir var olan günlük analizi çalışma alanları depolanacak hello toplanan veri, hesap hello hello VM coğrafi alma, Azure aboneliğinizin veya yeni bir çalışma alanları ile ilişkili. 

Hello Azure portal, toosee herhangi Azure Güvenlik Merkezi tarafından oluşturulan dahil olmak üzere, günlük analizi çalışma alanları listesini göz atabilirsiniz. Yeni çalışma alanları için bir ilgili kaynak grubu oluşturulur. İkisi de şu adlandırma kuralını izler: 

* Çalışma Alanı: *DefaultWorkspace-[abonelik-kimliği]-[bölge]*
* Kaynak Grubu: *DefaultResouceGroup-[bölge]*

Azure Güvenlik Merkezi tarafından oluşturulan çalışma alanları için veriler 30 gün boyunca tutulur. Çalışma alanları çıkma için bekletme hello çalışma alanında fiyatlandırma katmanı temel alır.

> [!NOTE]
> Microsoft bu verileri güvenlik ve önemli taahhütlerde tooprotect hello gizlilik olun. Microsoft aynılarını toostrict uyumluluk ve güvenlik yönergelerine — toooperating hizmet kodlama gelen. Veri işleme ve gizlilik hakkında daha fazla bilgi için [Azure Güvenlik Merkezi Veri Güvenliği](security-center-data-security.md) makalesini okuyun.
> 

## <a name="ongoing-security-monitoring"></a>Devam eden güvenlik izleme
Merhaba sonraki adım, başlangıç yapılandırmasını ve Güvenlik Merkezi önerilerini uygulama sonra Güvenlik Merkezi işlem süreçlerini dikkate almaktır.

tooaccess Güvenlik Merkezi hello tıklayabilirsiniz Azure Portalı'ndan **Gözat** ve türü **Güvenlik Merkezi** hello içinde **filtre** alan. Merhaba görünümler, Hello kullanıcı alır toothese uygulanan filtreler göre yapılır aşağıdaki hello örnek, bir ortam birçok sorunları toobe ele gösterir:

![pano](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> Güvenlik Merkezi, normal işlem yordamlarınıza müdahale etmez, pasif olarak dağıtımlarınızı izler ve etkinleştirilmiş hello güvenlik ilkelerine bağlı olarak öneriler sağlar.

Toouse Güvenlik Merkezi, geçerli Azure ortamınız için tercih aktarırken hello yapılabilir tüm önerileri gözden emin olun **önerileri** döşeme veya her bir kaynak (**işlem** **Ağ**, **depolama & veri**, **uygulama**).

Tüm önerilere değindikten sonra hello **önleme** bölümünde ele alınan tüm kaynaklar için yeşil. Yalnızca Merhaba, kaynak güvenlik durumu ve öneriler kutucuklarındaki değişikliklere göre eyleme geçeceğiniz için devam eden izleme bu noktada daha kolay hale gelir.

Merhaba **algılama** bölümü daha reaktiftir; bunlar ya sunulmuştur veya hello geçmiş oluştu ve Güvenlik Merkezi denetimleri ile 3. taraf sistemi tarafından algılanan sorunları ilgili uyarılar. Merhaba güvenlik uyarıları kutucuğu hello her gün ve bunların hello farklı önem derecesi kategorilerine (düşük, Orta, yüksek) dağılımlarını bulundu tehlike algılama uyarıları sayısını temsil eden çubuk grafiklerini gösterir. Güvenlik Uyarıları hakkında daha fazla bilgi için okuma [yönetme ve yanıt toosecurity Azure Güvenlik Merkezi'nde uyarıları](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> Ayrıca, Güvenlik Merkezi verilerinizi Microsoft Power BI toovisualize yararlanabilirsiniz. Bkz. [Power BI ile Azure Güvenlik Merkezi verilerinden öngörü alma](security-center-powerbi.md).
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>Yeni veya değiştirilmiş kaynakları izleme
Çoğu Azure ortamı, düzenli olarak çalışmaya başlatılan ve yavaşlatılan yeni kaynaklarla dinamiktir (örneğin, yapılandırmalar veya değişiklikler vb.) Güvenlik Merkezi, bu yeni kaynakların güvenlik durumu hello görünürlüğe sahip sağlamaya yardımcı olur.

Yeni kaynaklar (VM'ler, SQL DB'leri) tooyour Azure ortamı eklediğinizde, Güvenlik Merkezi otomatik olarak bu kaynakları keşfeder ve bunların güvenlik toomonitor başlayın. Buna PaaS web rolleri ve çalışan rolleri de dahildir. Veri toplama hello etkinleştirilirse [Güvenlik İlkesi](security-center-policies.md), ek izleme kapasiteleri etkinleştirilecek otomatik olarak sanal makineleriniz için.

![Temel alanlar](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. Sanal makineler için **Önleme** bölümü altındaki **İşlem**’e tıklayın. Veri veya ilgili öneriler etkinleştirme ile ilgili sorunları hello ortaya çıkması **genel bakış** sekmesinde ve **izleme önerileri** bölümü.
2. Görünüm hello **önerileri** toosee ne, varsa, güvenlik riskleri hello yeni kaynak için belirlendi.
3. Yalnızca hello işletim sistemi tooyour ortamı yeni VM'ler eklendiğinde, başlangıçta yüklendikten çok yaygındır. Merhaba kaynak sahibi bazı zaman toodeploy bu VM'ler tarafından kullanılacak diğer uygulamaları gerekebilir.  İdeal olarak, bu iş yükünün son amacını hello bilmeniz gerekir. Bir uygulama sunucusu toobe geçiyor? Hangi bunu temel alarak yeni iş yükü giderek toobe, uygun hello etkinleştirebilirsiniz **Güvenlik İlkesi**, bu iş akışındaki üçüncü adım hello olduğu.
4. Yeni kaynaklar Azure ortamı tooyour eklendikçe yeni uyarılar hello görünür mümkündür **güvenlik uyarıları** döşeme. Her zaman bu kutucukta yeni uyarılar olup olmadığını doğrulayın ve tooSecurity merkezi önerilerine göre eylemleri gerçekleştirin.

Ayrıca tooregularly İzleyicisi Merhaba durumu kayması önerilen taban çizgileri ve güvenlik uyarıları, güvenlik riskleri, oluşturduğunuz var olan kaynakları tooidentify yapılandırma değişikliklerinin isteyeceksiniz. Merhaba Güvenlik Merkezi Panosu'nda başlatın. Buradan, üç temel alanları tooreview tutarlı olarak vardır.

![İşlemler](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. Merhaba **önleme** bölüm paneli tooyour temel kaynaklarınıza hızlı erişim sağlar. Bu seçenek toomonitor işlem, ağ, depolama ve veri ve uygulamaları kullanın.
2. Merhaba **önerileri** Masası tooreview Güvenlik Merkezi önerileri sağlar. Devam eden izleme sırasında önerileri hello ilk Güvenlik Merkezi Kurulum tüm öneriler ele bu durum normaldir günlük olarak almadığınızı fark edebilirsiniz. Bu nedenle, yeni bilgiler bu bölümde her gün olmayabilir ve yalnızca tooaccess gerekir, gerektiğinde.
3. Merhaba **algılama** bölüm üzerinde ya da bir bir çok sık veya çok seyrek aralıklarla değişebilir. Güvenlik uyarılarınızı her zaman gözden geçirin ve Güvenlik Merkezi önerilerine göre eyleme geçin.

## <a name="incident-response"></a>Olay yanıtı
Güvenlik Merkezi algılar ve bunlar ortaya çıktığında toothreats uyarır. Kuruluşlar yeni güvenlik uyarılarını izlemeli ve daha fazla gerekli tooinvestigate olarak eylemde veya gerekir hello saldırıyı düzeltmek. Güvenlik Merkezi tehdit algılama özelliğinin nasıl çalıştığı hakkında daha fazla bilgi için [Azure Güvenlik Merkezi algılama özellikleri](security-center-detection-capabilities.md) konusunu okuyun.

Bu makale, kendi olay yanıtı planınızı oluşturmanız hello hedefi tooassist yok ancak biz toouse Microsoft Azure Security Response hello bulut yaşam döngüsü içinde hello temel olarak olay yanıtlama aşamaları adımıdır. Merhaba aşamaları diyagramı aşağıdaki hello gösterilmektedir:

![Şüpheli etkinlik](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> Merhaba National Institute of Standards ve Technology (NIST) kullanabileceğiniz [bilgisayar Security Incident Handling Guide](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) başvuru tooassist olarak kendi planınızı.
> 

Güvenlik Merkezi uyarılarını aşamaları aşağıdaki hello sırasında kullanabilirsiniz:

* **Algılama**: bir veya daha fazla kaynakta şüpheli bir etkinliği tanımlayın. 
* **Değerlendirme**: hello ilk değerlendirme tooobtain hello şüpheli etkinlik hakkında daha fazla bilgi gerçekleştirin.
* **Tanılama**: hello düzeltme adımları tooconduct hello teknik yordamı tooaddress hello sorunu kullanın.

Her güvenlik uyarısı kullanılabilir bilgileri sağlayan toobetter hello saldırı hello yapısını anlamanız ve olası risk azaltmalarını önermek. Bazı uyarılar bağlantılar tooeither bilgi Azure içinde daha fazla bilgi veya tooother kaynakları da sağlar. Daha fazla araştırma ve toobegin azaltma için sağlanan hello bilgilerini kullanabilirsiniz ve çalışma alanınızda depolanır güvenlikle ilgili veri arama yapabilirsiniz.

Merhaba aşağıdaki örnek şüpheli bir RDP etkinliğinin gerçekleşmesini gösterir:

![Şüpheli etkinlik](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

Gördüğünüz gibi bu dikey hello saldırı gerçekleşen hello zamanı ile ilgili ayrıntıları gösterir, kaynak ana bilgisayar adı Merhaba, hedef VM hello ve ayrıca öneri adımları sunar. Bazı durumlarda hello hello saldırının kaynak bilgileri boş olabilir. Bu türden bir davranış hakkında daha fazla bilgi için bkz. [Azure Güvenlik Merkezi Uyarıları'nda Eksik Kaynak Bilgileri](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/).

Merhaba, [nasıl tooLeverage hello Azure Güvenlik Merkezi & Microsoft Operations Management Suite bir olay yanıtı için](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) nasıl Güvenlik Merkezi kullanılabilir her toounderstand yardımcı olabilecek bazı gösterim görebilirsiniz video Bu aşamalar biri.

> [!NOTE]
> Okuma [Leveraging Azure Güvenlik Merkezi olay yanıtı için](security-center-incident-response.md) toouse Güvenlik Merkezi özellikleri tooassist, olay yanıtınız sırasında işleminin nasıl daha fazla bilgi için. 
> 
> 

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, nasıl öğrenilen Güvenlik Merkezi'ni benimsemeyi tooplan. Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Yönetme ve Azure Güvenlik Merkezi'nde toosecurity uyarılarını yanıt](security-center-managing-and-responding-alerts.md)
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) — nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) — nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.


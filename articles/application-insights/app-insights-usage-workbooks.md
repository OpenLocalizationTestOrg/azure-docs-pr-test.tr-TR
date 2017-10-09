---
title: "Azure Application Insights etkileşimli çalışma kitapları ile aaaInvestigate ve paylaşımı kullanım verilerini | Microsoft docs"
description: "Kullanıcılar, web uygulamanızın demografik analizini."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a>Araştırmak ve kullanım verilerini Application Insights etkileşimli çalışma kitaplarında paylaşın

Çalışma kitapları birleştirmek [Azure Application Insights](app-insights-overview.md) veri görselleştirmeleri [analitik sorguları](app-insights-analytics.md)ve etkileşimli belgeleri metin. Çalışma kitapları erişim toohello ile diğer takım üyeleri tarafından düzenlenebilir aynı Azure kaynak. Bu hello sorgular ve denetimleri kullanılan toocreate bir çalışma kitabı hello çalışma kitabı okuma kullanılabilir tooother kişiler kolay tooexplore hale gelir, genişletme ve hataları olup olmadığını denetleyin.

Çalışma kitapları gibi senaryolar için yararlı olur:

* Merhaba ölçümleri ilgi önceden tanımadığınız olduğunda, uygulamanızın hello kullanım keşfetme: kullanıcılar, saklama hızları, dönüştürme oranları vb. sayısı. Application ınsights'ta diğer kullanım analiz araçları çalışma kitapları, Görselleştirme ve çözümlemeleri de serbest biçimli araştırması bu tür için harika yapmadan birden çok türde birleştirmek olanak tanır.
* Yeni yayımlanmış bir özelliğin nasıl gerçekleştirmekte tooyour takım açıklayan, kullanıcı tarafından gösteren anahtar etkileşimleri ve diğer ölçümleri için sayar.
* Merhaba sonuçlarını bir paylaşım / B denemeler ekibinizin diğer üyeleriyle, uygulamanızda. Hello hello hedeflerini metinle denemeler yapın ve ardından her kullanım ölçümü Göster ve analizi sorgu tooevaluate hello deneme Temizle çağrı-her ölçümü üstüne veya altına-hedefi olup için aşımı ayarlarına birlikte kullanılan açıklayabilir.
* Bir kesinti Hello etkisini hello kullanım verileri, açıklama metnini ve sonraki adımları tooprevent kesilmelerini hello gelecekteki tartışması birleştirerek, uygulamanızın raporlama.

> [!NOTE]
> Application Insights kaynağınıza, sayfa görünümleri veya özel olaylar toouse çalışma kitaplarını içermesi gerekir. [Uygulama toocollect sayfasını tooset hello Application Insights JavaScript SDK'sı ile otomatik olarak nasıl görünümleri öğrenin](app-insights-javascript.md).
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a>Düzenleme, yeniden düzenleme, kopyalama ve çalışma kitabını bölümleri silme

Bir çalışma kitabı bölümlerini yapılmış bir durumda: bağımsız olarak düzenlenebilir kullanım görselleştirmeleri, grafikler, tablolar, metin veya Analytics sorgu sonuçları.

bir çalışma kitabı bölümü tooedit Merhaba içeriğine tıklatın hello **Düzenle** düğmeye ve hello çalışma kitabı bölümünün sağ toohello.

![Düzenleme denetimleri uygulama Öngörüler çalışma kitaplarını bölümü](./media/app-insights-usage-workbooks/editing-controls.png)

1. Tamamladığınızda, bir bölümü düzenleme'ı tıklatın **yapılan düzenleme** hello sol alt köşesindeki hello bölüm içinde.

2. toocreate yinelenen bir bölümün tıklatın hello **bu bölümü kopyalama** simgesi. Yinelenen bölümleri oluşturma harika tooway tooiterate önceki yineleme kaybetmeden sorguda bağlıdır.

3. bir çalışma kitabı bölümünde yukarı toomove tıklatın hello **Yukarı Taşı** veya **Aşağı Taşı** simgesi.

4. tooremove bölüm kalıcı olarak hello tıklatın **kaldırmak** simgesi.

## <a name="adding-usage-data-visualization-sections"></a>Kullanım verileri görselleştirme bölümleri ekleme

Çalışma kitapları yerleşik kullanım analizi görselleştirmeleri dört tür sunar. Her bir soru hello kullanımı hakkında uygulamanızın yanıtlar. tooadd tablolar ve grafikler bu dört bölüm dışında Analytics sorgu bölümleri (aşağıda görebilirsiniz) ekleyin.

tooadd kullanıcılar, oturumlar, olayları veya bekletme bölümünde tooyour çalışma kitabı, kullanım hello **Kullanıcı Ekle** veya diğer karşılık gelen bir düğme hello çalışma kitabının hello altındaki ya da hello altındaki herhangi bir bölümü.

![Kullanıcılar bölümünde çalışma kitapları](./media/app-insights-usage-workbooks/users-section.png)

**Kullanıcıların** bölümleri yanıt "kaç kullanıcının bazı sayfa görüntülenemez veya Sitem bazı özelliği kullanılan?"

**Oturumları** bölümleri yanıt "kaç oturumları kullanıcılar bazı sayfa görüntüleme veya Sitem bazı özelliğini kullanarak harcamanız?"

**Olayları** bölümleri yanıt "kaç kez kullanıcılar bazı sayfasını görüntüleyebilir veya Sitem bazı özelliğini kullanın?"

Bu üç bölüm türleri hello denetimleri ve görselleştirmeleri aynı kümesi sunar:

* [Kullanıcıları, oturumlar ve olayları bölümleri düzenleme hakkında daha fazla bilgi edinin](app-insights-usage-segmentation.md)
* Geçiş hello ana grafik, çubuk grafik kılavuzları, otomatik Öngörüler ve örnek kullanıcılar görselleştirmeleri hello kullanarak **Göster grafik**, **Göster kılavuz**, **Göster Öngörüler**ve **Bu kullanıcılar örnek** onay kutularını her bölümün hello üstünde.

![Çalışma kitapları bekletme bölümünde](./media/app-insights-usage-workbooks/retention-section.png)

**Bekletme** bölümleri yanıt "bazı sayfa görüntülenemez veya bir gün veya hafta bazı özellik kullanılan kişiler kaç tane geri bir sonraki gün veya hafta gelen?"

* [Bekletme bölümleri düzenleme hakkında daha fazla bilgi edinin](app-insights-usage-retention.md)
* Hello kullanarak geçiş hello isteğe bağlı genel saklama grafik **Göster genel saklama grafik** onay kutusunu hello bölümünün hello üstünde.

## <a name="adding-application-insights-analytics-sections"></a>Uygulama Öngörüler Analytics bölümleri ekleme

![Çalışma kitapları Analytics bölümünde](./media/app-insights-usage-workbooks/analytics-section.png)

tooadd bir uygulama Öngörüler Analytics sorgu bölüm tooyour çalışma kitabı, hello kullan **eklemek Analytics sorgu** düğmesi hello çalışma kitabının hello altındaki ya da hello altındaki herhangi bir bölümü.

Analytics sorgu bölümleri rasgele sorguları Application Insights verilerinizi çalışma kitaplarına eklemenize olanak sağlar. Bu esneklik Analytics sorgu bölümleri siteniz hello kullanıcıları, oturumlar, olayları ve bekletme, gibi yukarıda dört dışında hakkında tüm sorulara yanıt verilmesi, Git toofor olmalıdır anlamına gelir:

* Kaç tane özel durumların mı, site throw hello sırasında aynı zaman dilimi kullanımı Reddet olarak?
* Kullanıcılar bazı sayfasını görüntülemek için sayfa yükleme sürelerinin hello dağıtımını neydi?
* Kaç kullanıcının bazı sayfalar kümesi sitenizde görüntülenebilir, ancak olmayan bazı diğer sayfalarında ayarlamak? Sitenizin işlevselliğin farklı alt kümelerini kullanan kullanıcılar, kümeleri varsa, bu yararlı toounderstand olabilir (Merhaba kullanmak `join` hello işleciyle `kind=leftanti` hello günlük analizi sorgu dili değiştiricisi).

Kullanım hello [günlük analizi sorgu dili başvurusu](https://docs.loganalytics.io/) toolearn sorguları yazma hakkında daha fazla bilgi.

## <a name="adding-text-and-markdown-sections"></a>Metin ve Markdown bölümleri ekleme

Başlıklar, açıklamalar ve Yorumlar tooyour çalışma kitaplarına ekleme, tablolar ve grafikler kümesi biçiminde anlatı kapatma yardımcı olur. Çalışma kitapları metin bölümlerde destek hello [Markdown söz dizimi](https://daringfireball.net/projects/markdown/) başlıklar, kalın, italik ve madde işaretli listeler gibi biçimlendirme metin.

tooadd bir metin bölüm tooyour çalışma kullanmak hello **metin ekleme** düğmesi hello çalışma kitabının hello altındaki ya da hello altındaki herhangi bir bölümü.

## <a name="saving-and-sharing-workbooks-with-your-team"></a>Kaydetme ve takımınızla çalışma kitaplarını paylaşma

Çalışma kitapları, Application Insights kaynağı, ya da hello içinde kaydedilir **raporlarım** özel tooyou bölümüne veya hello **paylaşılan raporları** erişimi olan erişilebilir tooeveryone bölümü toohello Application Insights kaynağı. tooview hello kaynak tüm hello kitaplarında tıklatın hello **açık** hello eylem çubuğunda düğmesi.

şu anda kullanımda bir çalışma kitabı tooshare **raporlarım**:

1. Tıklatın **açık** hello eylem çubuğunda
2. Merhaba "..." düğmesini tıklatın tooshare istediğiniz hello çalışma kitabı
3. Tıklatın **taşıma tooShared raporları**.

tooshare bir çalışma kitabını bir bağlantıyla veya e-posta, yoluyla tıklatın **paylaşımı** hello eylem çubuğunda. Merhaba bağlantının alıcıları hello Azure portal tooview hello çalışma kitabındaki toothis kaynağa erişim aklınızda bulundurun. toomake düzenlemeler, alıcılar gereken en az hello kaynak katkıda bulunan izinleri.

bir bağlantı tooa çalışma kitabı tooan Azure Pano toopin:

1. Tıklatın **açık** hello eylem çubuğunda
2. Merhaba "..." düğmesini tıklatın toopin istediğiniz hello çalışma kitabı
3. Tıklatın **PIN toodashboard**.

## <a name="next-steps"></a>Sonraki adımlar

## <a name="next-steps"></a>Sonraki adımlar
- tooenable kullanımı deneyimleri, göndermeye Başla [özel olaylar](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) veya [sayfa görünümleri](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Özel olaylar ya da sayfa görünümleri keşfedin hello kullanım araçları toolearn zaten gönderirseniz kullanıcılar hizmetinizi kullanma.
    - [Kullanıcılar, Oturumlar, Etkinlikler](app-insights-usage-segmentation.md)
    - [Huniler](usage-funnels.md)
    - [Bekletme](app-insights-usage-retention.md)
    - [Kullanıcı Akışları](app-insights-usage-flows.md)
    - [Kullanıcı bağlamı Ekle](app-insights-usage-send-user-context.md)
    

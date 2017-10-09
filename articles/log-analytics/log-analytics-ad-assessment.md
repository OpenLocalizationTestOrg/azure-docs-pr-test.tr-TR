---
title: "aaaOptimize, Active Directory ortamınızı Azure günlük analizi ile | Microsoft Docs"
description: "Merhaba Active Directory değerlendirme çözümü tooassess risk ve sunucu ortamlarınızın durumunu düzenli aralıklarla hello kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 63290d95302a9e1d243cd993ac50556ed42b97bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-active-directory-environment-with-hello-active-directory-assessment-solution-in-log-analytics"></a>Active Directory ortamınızı hello Active Directory değerlendirme çözümde günlük analizi ile en iyi duruma getirme

![AD değerlendirmesi simgesi](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

Merhaba Active Directory değerlendirme çözümü tooassess risk ve sunucu ortamlarınızın durumunu düzenli aralıklarla hello kullanabilirsiniz. Bu makalede, yükleme ve olası sorunlar için düzeltme eylemleri yararlanabilmeniz hello çözüm kullanma yardımcı olur.

Bu çözüm önerileri belirli tooyour dağıtılan sunucu altyapısı öncelikli listesi sağlar. Merhaba önerileri risk hello ve eyleme hızlı bir şekilde Yardım alanları anlamak dört odak arasında ayrılır.

Merhaba önerileri hello bilgi ve müşteri ziyaretleriniz binlerce Microsoft mühendisleri tarafından elde edilen deneyimlerden dayanır. Her bir öneri, bir sorun tooyou neden önemli ve nasıl tooimplement hello değişiklikleri önerilen hakkında rehberlik sağlar.

En önemli tooyour kuruluş ve ücretsiz ve sağlam bir risk ortam çalıştıran doğru ilerleme durumunuzu izlemenize odak alanlarına seçebilirsiniz.

Merhaba çözüm ekledik ve bir değerlendirme tamamlanan, Özet sonra bilgi odak alanlarına odaklanmak için hello üzerinde gösterilen **AD değerlendirme** Panosu ortamınızdaki hello altyapısını için. Merhaba aşağıdaki nasıl toouse hello hello hakkında bilgi bölümlerde **AD değerlendirme** Pano, burada görüntüleyebilir ve ardından uygulayın önerilen eylemler için Active Directory sunucu altyapınızı.

![SQL değerlendirmesi döşeme görüntüsü](./media/log-analytics-ad-assessment/ad-tile.png)

![SQL değerlendirmesi Pano görüntüsü](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-hello-solution"></a>Yükleme ve yapılandırma hello çözümü
Bilgi tooinstall aşağıdaki hello kullanın ve hello çözümleri yapılandırın.

* Aracıları hello etki alanı toobe hesaplanan üyeleri olan etki alanı denetleyicilerinde yüklü olması gerekir.
* Merhaba Active Directory değerlendirme çözümü .NET Framework 4'ün desteklenen bir sürümünü gerektirir (4.5.2 veya üstü) bir OMS aracısı olan her bilgisayarda yüklü.
* Merhaba Active Directory değerlendirme çözümü tooyour OMS çalışma alanından eklemek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).  Başka bir yapılandırma işlemi gerekmez.

  > [!NOTE]
  > Merhaba çözüm ekledikten sonra hello AdvisorAssessment.exe dosyası tooservers aracılarıyla eklenir. Yapılandırma verilerini okuma ve işleme hello bulutta toohello OMS hizmetine gönderilir. Mantığı uygulanan toohello alınan veri ve hello bulut hizmeti hello verilerini kaydeder.
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a>Active Directory değerlendirme veri toplama ayrıntıları

Active Directory değerlendirme aşağıdaki kaynaklar etkinleştirdiğiniz hello aracıları kullanarak hello veri toplar:

- Kayıt defteri toplayıcıları
- LDAP toplayıcıları
- .NET framework
- Olay günlüğü toplayıcıları
- Active Directory Hizmeti Arabirimleri (ADSI)
- Windows PowerShell
- Dosya veri toplayıcıları
- Windows Yönetim Araçları (WMI)
- DCDIAG aracı API'si
- Dosya Çoğaltma Hizmeti (NTFRS) API'si
- Özel C# kodu


Merhaba aşağıdaki tabloda veri toplama yöntemleri aracılar için Operations Manager (SCOM) gerekli olup olmadığını ve nasıl gösterilmektedir genellikle veri bir aracı tarafından toplanır.

| Platform | Doğrudan Aracısı | SCOM Aracısı | Azure Storage | SCOM gerekli? | Yönetim grubu gönderilen SCOM Aracısı verileri | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |7 gün |

## <a name="understanding-how-recommendations-are-prioritized"></a>Önerilerin nasıl önceliklendirilir anlama
Yapılan her öneri hello öneri göreceli önemini hello tanımlayan bir ağırlıklı değer verilir. Yalnızca hello 10 en önemli öneriler gösterilir.

### <a name="how-weights-are-calculated"></a>Ağırlıkları nasıl hesaplanır
Ağırlık belirlemeyi üç anahtar faktörlerini temel alarak toplam değerler şunlardır:

* Merhaba *olasılık* tanımlanan bir sorunun sorunlara neden olur. Daha yüksek olasılık büyük genel puan hello öneri tooa karşılık gelir.
* Merhaba *etkisi* kuruluşunuzdaki bir soruna neden olursa hello sorun. Daha yüksek bir etkisi, büyük genel puan hello öneri tooa karşılık gelir.
* Merhaba *çaba* tooimplement hello öneri gerekli. Daha yüksek çaba küçük genel puan hello öneri tooa karşılık gelir.

Her bir öneri ağırlığı hello hello toplam puanı her odak alanı için kullanılabilir bir yüzdesi olarak ifade edilir. Örneğin, bu öneri uygulama hello güvenlik ve uyumluluk odaklanılan alan bir öneri %5 puanı varsa, genel güvenlik ve uyumluluk puan tarafından %5 artırır.

### <a name="focus-areas"></a>Odak alanları
**Güvenlik ve Uyumluluk** -bu odak alanı olası güvenlik tehditlerini ve ihlallerinden, şirket ilkelerini ve teknik ve yasal uyumluluk gereksinimleri için öneriler gösterir.

**Kullanılabilirlik ve iş sürekliliği** -bu odaklanılan alan hizmet kullanılabilirliği, altyapı ve iş koruması dayanıklılık için öneriler gösterir.

**Performans ve ölçeklenebilirlik** -bu odaklanılan alan önerileri toohelp kuruluşunuzun gösterir BT altyapısı arttıkça, BT ortamınız geçerli performans gereksinimlerini karşıladığından ve mümkün toorespond toochanging olduğundan emin olun Altyapı gerekir.

**Yükseltme, geçiş ve dağıtım** - bu odak alanı yükseltme önerileri toohelp gösterir, geçirmek ve Active Directory tooyour mevcut altyapıyı.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Her odak alanında % 100 tooscore hedeflemeniz gerektiğini?
Olmayabilir. Merhaba önerileri hello bilgi ve müşteri ziyaretleriniz binlerce arasında Microsoft mühendisleri tarafından elde edilen deneyimleri temel alır. Ancak, iki sunucu altyapılar aynı hello ve belirli öneriler fazla veya az ilgili tooyou olabilir değildir. Örneğin, bazı güvenlik önerileri sanal makinelerinizi gösterilen toohello Internet değilseniz, daha az ilgili olabilir. Bazı kullanılabilirlik öneriler düşük öncelik geçici veri toplama ve raporlama sağladığı hizmetler için daha az uygun olmayabilir. Önemli tooa olgun iş sorunlarını daha az önemli tooa başlatma olabilir. Önceliklerinizden hangi odak alanlarıdır tooidentify istediğiniz ve, puanları zamanla nasıl değiştiğini adresindeki bakın.

Her öneri neden önemli olduğu hakkında yönergeler içerir. Merhaba öneri uygulama BT Hizmetleri ve hello iş gereksinimlerinizi kuruluşunuzun hello yapısını verilen sizin için uygun olup, bu kılavuzu tooevaluate kullanmanız gerekir.

## <a name="use-assessment-focus-area-recommendations"></a>Değerlendirme odak alanı önerileri kullanın
OMS içinde bir değerlendirme çözümü kullanmadan önce hello çözümü yüklenmiş olması gerekir. çözümler, yükleme hakkında daha fazla tooread bkz [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md). Yüklendikten sonra hello genel bakış sayfasında OMS hello değerlendirme kutucuğu kullanarak önerileri hello özetini görüntüleyebilirsiniz.

Görünüm hello altyapınızı ve ardından-ayrıntıya önerileri için Uyumluluk değerlendirmesi özetlenir.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>bir odak alanı ve Al düzeltme eylemi için tooview önerileri
1. Merhaba üzerinde **genel bakış** hello sayfasında, **değerlendirme** döşeme sunucusu altyapınız için.
2. Merhaba üzerinde **değerlendirme** sayfasında hello odak alanı Kanatlar birinde hello özet bilgileri gözden geçirin ve aşağıdakilerden tooview önerileri bu odaklanılan alan için tıklatın.
3. Merhaba odak alanı sayfaları hiçbirinde ortamınız için öncelik hello önerilerin görüntüleyebilirsiniz. Önerinin altında tıklatın **etkilenen nesneler** tooview hakkında ayrıntılı hello öneri yapılan neden.  
    ![Değerlendirmesi önerileri görüntüsü](./media/log-analytics-ad-assessment/ad-focus.png)
4. Önerilen düzeltici eylemleri gerçekleştirebilirsiniz **önerilen eylemleri**. Merhaba öğesi ele önerilen eylemleri sonraki değerlendirmeleri kayıtları gerçekleştirilen ve uyumluluk puan artmasına neden olur. Düzeltilmiş öğeler görünür olarak **geçirilen nesneleri**.

## <a name="ignore-recommendations"></a>Öneriler yoksay
Tooignore istediğiniz önerileri varsa, OMS değerlendirme sonuçlarında görünmesini tooprevent önerileri kullanacağı bir metin dosyası oluşturabilirsiniz.

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>göz ardı eder tooidentify önerileri
1. Tooyour çalışma alanında oturum ve günlük arama açın. Aşağıdaki, ortamınızdaki bilgisayarları için başarısız olan sorgu toolist önerileri hello kullanın.

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorgu yukarıda hello toohello aşağıdaki değişeceğinden sonra.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   Bir ekran görüntüsü gösteren hello günlük arama sorgusu şöyledir: ![önerileri başarısız oldu](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)
2. Öneriler tooignore istediğinizi seçin. Merhaba sonraki yordamda Recommendationıd için hello değerleri kullanacaksınız.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate ve IgnoreRecommendations.txt metin dosyayı kullan
1. IgnoreRecommendations.txt adlı bir dosya oluşturun.
2. Her Recommendationıd, günlük analizi tooignore ayrı bir satırda istediğiniz ve ardından hello dosyasını kaydedip kapatın, her bir öneri için yazın veya yapıştırın.
3. Merhaba dosya klasörü OMS tooignore önerileri istediğiniz her bilgisayarda aşağıdaki hello yerleştirin.
   * Microsoft Monitoring Agent (doğrudan veya Operations Manager aracılığıyla bağlı) - hello olan bilgisayarlarda *SystemDrive*: \Program izleme Agent\Agent
   * Merhaba Operations Manager yönetim sunucusunda - *SystemDrive*: \Program System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify önerileri göz ardı edilir
Varsayılan olarak 7 günde Hello sonraki zamanlanmış değerlendirme çalıştıktan sonra öneriler işaretlenir hello belirtilen *yoksayıldı* ve hello değerlendirme Panoda görünmez.

1. Tüm göz ardı hello önerileri günlük arama sorguları toolist aşağıdaki hello kullanabilirsiniz.

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorgu yukarıda hello toohello aşağıdaki değişeceğinden sonra.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. Daha sonra göz ardı toosee önerileri istemediğinize karar verirseniz, tüm IgnoreRecommendations.txt dosyaları silin veya bunları RecommendationIDs kaldırabilirsiniz.

## <a name="ad-assessment-solutions-faq"></a>AD değerlendirmesi çözümleri hakkında SSS
*Sıklıkla bir değerlendirme çalışıyor mu?*

* Merhaba değerlendirme 7 günde bir çalışır.

*Merhaba değerlendirme çalıştıran bir şekilde tooconfigure ne sıklıkta var mı?*

* Şu anda değil.

*I değerlendirme çözümünü ekledikten sonra başka bir sunucu için belirlediyseniz değerlendirileceğini?*

* Evet, bunu daha sonra gelen her 7 günde değerlendirildiği bulunduktan sonra.

*Ne zaman bir sunucu kullanımdan alındığında hello değerlendirme kaldırılacak?*

* Bir sunucu için 3 hafta veri göndermez, kaldırılır.

*Veri toplama hello hello işlemin hello adı nedir?*

* AdvisorAssessment.exe

*Ne kadar süreyle için toplanan verileri toobe sürer?*

* Merhaba gerçek veri toplama hello sunucuda yaklaşık 1 saat sürer. Bu çok sayıda Active Directory sunucularını sahip sunucularda uzun sürebilir.

*Verileri toplandığında yolu tooconfigure var mı?*

* Şu anda değil.

*Neden yalnızca hello ilk 10 önerileri görüntülemek?*

* Görevler kapsamlı bir zorlamayı listesi vermek yerine, öncelik hello önerileri adresleme odaklanmak öneririz. Bunları çözün sonra ek öneriler kullanılabilir hale gelir. Toosee hello ayrıntılı liste tercih ederseniz, tüm önerileri günlük arama özelliğini kullanarak görüntüleyebilirsiniz.

*Herhangi bir şekilde tooignore bir öneri var mı?*

* Evet, bkz: [önerileri yoksay](#ignore-recommendations) yukarıdaki bölümde.

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) tooview ayrıntılı AD Değerlendirme verileri ve öneriler.

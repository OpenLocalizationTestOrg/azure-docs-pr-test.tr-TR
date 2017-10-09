---
title: "aaaOptimize Azure günlük analizi ile SQL Server ortamınızın | Microsoft Docs"
description: "Azure günlük analizi ile Merhaba SQL çözüm tooassess risk ve SQL server ortamlarınızın durumunu düzenli aralıklarla hello değerlendirme kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a>SQL Server ortamınızın hello SQL değerlendirmesi çözümde günlük analizi ile en iyi duruma getirme

![SQL değerlendirmesi simgesi](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

Merhaba SQL çözüm tooassess risk ve sunucu ortamlarınızın durumunu düzenli aralıklarla hello değerlendirme kullanabilirsiniz. Bu makalede, olası sorunlar için düzeltme eylemleri yararlanabilmeniz hello çözüm yüklemenize yardımcı olur.

Bu çözüm önerileri belirli tooyour dağıtılan sunucu altyapısı öncelikli listesi sağlar. Merhaba önerileri hızla yardımcı alanları risk hello ve düzeltici işlemleri anlamak altı odak arasında ayrılır.

Merhaba önerilerin hello bilgi ve müşteri ziyaretleriniz binlerce Microsoft mühendisleri tarafından elde edilen deneyimlerden dayanır. Her bir öneri, bir sorun tooyou neden önemli ve nasıl tooimplement hello değişiklikleri önerilen hakkında rehberlik sağlar.

En önemli tooyour kuruluş ve ücretsiz ve sağlam bir risk ortam çalıştıran doğru ilerleme durumunuzu izlemenize odak alanlarına seçebilirsiniz.

Merhaba çözüm ekledik ve bir değerlendirme tamamlanan, Özet sonra bilgi odak alanlarına odaklanmak için hello üzerinde gösterilen **SQL değerlendirmesi** Panosu ortamınızdaki hello altyapısını için. Merhaba aşağıdaki nasıl toouse hello hello hakkında bilgi bölümlerde **SQL değerlendirmesi** Pano, burada görüntüleyebilir ve ardından uygulayın Eylemler SQL server altyapınızı için önerilir.

![SQL değerlendirmesi döşeme görüntüsü](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![SQL değerlendirmesi Pano görüntüsü](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a>Yükleme ve yapılandırma hello çözümü
SQL Server hello standart, Developer ve Enterprise sürümleri için şu anda desteklenen tüm sürümleri ile SQL değerlendirmesi çalışır.

Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.

* Aracıları SQL Server'ın yüklü olması sunucularda yüklü olması gerekir.
* Hello SQL değerlendirme çözümü bir OMS aracısı olan her bilgisayarda yüklü .NET Framework 4'ün desteklenen bir sürümünü gerektirir.
* Kullanarak hello Azure portal sipariş tooinstall hello çözümde hello kullanıcı bir yönetici veya katkıda toohello Azure aboneliğiniz olmalıdır. Ayrıca, hello kullanıcı rolünün bir üyesi hello OMS çalışma katkıda bulunan veya yönetici hello OMS portalında olmalıdır.
* Merhaba Operations Manager aracısı SQL değerlendirmesi ile kullanırken, toouse bir Operations Manager Run-As hesabı gerekir. Bkz: [Operations Manager Çalıştır hesapları için OMS](#operations-manager-run-as-accounts-for-oms) altında daha fazla bilgi için.

  > [!NOTE]
  > Merhaba MMA aracı Operations Manager Run-As hesaplarını desteklemez.
  >
  >
* Merhaba işlemi kullanarak OMS çalışma açıklanan hello SQL değerlendirme çözümü tooyour eklemek [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md). Başka bir yapılandırma işlemi gerekmez.

> [!NOTE]
> Merhaba çözüm ekledikten sonra hello AdvisorAssessment.exe dosyası tooservers aracılarıyla eklenir. Yapılandırma verilerini okuma ve işleme hello bulutta toohello OMS hizmetine gönderilir. Mantığı uygulanan toohello alınan veri ve hello bulut hizmeti hello verilerini kaydeder.

## <a name="sql-assessment-data-collection-details"></a>SQL değerlendirmesi veri toplama ayrıntıları
SQL değerlendirmesi WMI verilerini, kayıt defteri verilerini, performans verilerini ve etkinleştirdiğiniz hello aracıları kullanarak SQL Server dinamik yönetim görünümünü sonuçları toplar.

Merhaba aşağıdaki tabloda veri toplama yöntemleri aracılar için Operations Manager (SCOM) gerekli olup olmadığını ve nasıl gösterilmektedir genellikle veri bir aracı tarafından toplanır.

| Platform | Doğrudan Aracısı | SCOM Aracısı | Azure Storage | SCOM gerekli? | Yönetim grubu gönderilen SCOM Aracısı verileri | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  | &#8226; |7 gün |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Operations Manager hesapları OMS için Çalıştır
OMS günlük analizi hello Operations Manager aracısı ve yönetim grubu toocollect kullanır ve veri toohello OMS hizmetine gönderir. Yönetim paketleri için iş yüklerini tooprovide bağlı OMS derlemeleri değeri-hizmetlerini ekleyin. Her iş yükü, bir etki alanı hesabı gibi farklı güvenlik bağlamında iş yüküne özgü ayrıcalıkları toorun yönetim paketleri gerektirir. Bir Operations Manager farklı çalıştır hesabı yapılandırarak tooprovide kimlik bilgileri gerekir.

SQL değerlendirmesi için Çalıştır bilgiler tooset hello Operations Manager hesabı aşağıdaki hello kullanın.

### <a name="set-hello-run-as-account-for-sql-assessment"></a>SQL değerlendirmesi için Hello farklı çalıştır hesabı ayarlama
 Merhaba SQL Server Yönetim Paketi zaten kullanıyorsanız, bu farklı çalıştır hesabı kullanmanız gerekir.

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a>tooconfigure hello hello işletim Konsolu SQL farklı çalıştır hesabı
> [!NOTE]
> Kullanıyorsanız hello OMS hello SCOM Aracısı yerine, aracı doğrudan, hello Yönetim Paketi hello güvenlik bağlamında hello yerel sistem hesabı her zaman çalışır. Atla adım 1-5 aşağıdaki ve çalıştırma ya da NT AUTHORITY\SYSTEM hello kullanıcı adı olarak belirterek, T-SQL veya Powershell örnek hello.
>
>

1. Operations Manager'da hello işletim konsolunu açın ve ardından **Yönetim**.
2. Altında **Çalıştır Yapılandırması**, tıklatın **profilleri**, açarak **OMS SQL değerlendirmesi farklı çalıştır profili**.
3. Merhaba üzerinde **farklı çalıştır hesapları** sayfasında, **Ekle**.
4. SQL Server için gereken hello kimlik bilgilerini içeren bir Windows farklı çalıştır hesabı seçin veya tıklatın **yeni** toocreate biri.

   > [!NOTE]
   > Windows Hello farklı çalıştır hesap türü olmalıdır. Merhaba farklı çalıştır hesabı, aynı zamanda SQL Server örneklerini barındıran tüm Windows sunucularında yerel Administrators grubunun bir parçası olması gerekir.
   >
   >
5. **Kaydet** düğmesine tıklayın.
6. Değiştirin ve sonra her SQL Server örneği toogrant minimum izinleri gerekli tooRun üzerinde hesabı tooperform SQL değerlendirmesi T-SQL örneği aşağıdaki hello yürütün. Ancak, bir farklı çalıştır hesabı SQL Server örnekleri üzerindeki hello sysadmin sunucu rolünün bir parçası ise bu toodo ihtiyacınız yoktur.

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a>tooconfigure hello Windows PowerShell kullanarak SQL farklı çalıştır hesabı
Bir PowerShell penceresi açın ve bilgilerinizle güncelleştirdikten sonra komut dosyası izleyen hello çalıştırın:

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a>Önerilerin nasıl önceliklendirilir anlama
Yapılan her öneri hello öneri göreceli önemini hello tanımlayan bir ağırlıklı değer verilir. Yalnızca hello on en önemli öneriler gösterilir.

### <a name="how-weights-are-calculated"></a>Ağırlıkları nasıl hesaplanır
Ağırlık belirlemeyi üç anahtar faktörlerini temel alarak toplam değerler şunlardır:

* Merhaba *olasılık* tanımlanan bir sorunun sorunlara neden. Daha yüksek olasılık büyük genel puan hello öneri tooa karşılık gelir.
* Merhaba *etkisi* kuruluşunuzdaki bir soruna neden olursa hello sorun. Daha yüksek bir etkisi, büyük genel puan hello öneri tooa karşılık gelir.
* Merhaba *çaba* tooimplement hello öneri gerekli. Daha yüksek çaba küçük genel puan hello öneri tooa karşılık gelir.

Her bir öneri ağırlığı hello hello toplam puanı her odak alanı için kullanılabilir bir yüzdesi olarak ifade edilir. Bir öneri hello güvenlik ve uyumluluk odaklanılan alan %5 puanı varsa, örneğin, bu öneri uygulama, genel güvenlik ve uyumluluk puan tarafından %5 artacaktır.

### <a name="focus-areas"></a>Odak alanları
**Güvenlik ve Uyumluluk** -bu odak alanı olası güvenlik tehditlerini ve ihlallerinden, şirket ilkelerini ve teknik ve yasal uyumluluk gereksinimleri için öneriler gösterir.

**Kullanılabilirlik ve iş sürekliliği** -bu odaklanılan alan hizmet kullanılabilirliği, altyapı ve iş koruması dayanıklılık için öneriler gösterir.

**Performans ve ölçeklenebilirlik** -bu odaklanılan alan önerileri toohelp kuruluşunuzun gösterir BT altyapısı arttıkça, BT ortamınız geçerli performans gereksinimlerini karşıladığından ve mümkün toorespond toochanging olduğundan emin olun Altyapı gerekir.

**Yükseltme, geçiş ve dağıtım** - bu odak alanı yükseltme önerileri toohelp gösterir, geçirme ve SQL Server tooyour mevcut altyapıyı.

**İşlemler ve izleme** - bu odaklanılan alan önerileri toohelp daha verimli hale BT işlemlerinizi gösterir önleyici bakım uygulamak ve performansı en üst düzeye çıkarın.

**Değişiklik ve yapılandırma yönetimi** -bu odak alanı öneriler gösterir toohelp günlük işlemlerini korumak, değişiklikleri yok olumsuz altyapınızı etkiler, değişiklik denetim yordamları ve tootrack oluşturun ve denetim emin olun Sistem yapılandırması.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Her odak alanında % 100 tooscore hedeflemeniz gerektiğini?
Olmayabilir. Merhaba önerileri hello bilgi ve müşteri ziyaretleriniz binlerce arasında Microsoft mühendisleri tarafından elde edilen deneyimleri temel alır. Ancak, iki sunucu altyapılar aynı hello ve belirli öneriler fazla veya az ilgili tooyou olabilir değildir. Örneğin, bazı güvenlik önerileri sanal makinelerinizi gösterilen toohello Internet değilseniz, daha az ilgili olabilir. Bazı kullanılabilirlik öneriler düşük öncelik geçici veri toplama ve raporlama sağladığı hizmetler için daha az uygun olmayabilir. Önemli tooa olgun iş sorunlarını daha az önemli tooa başlatma olabilir. Önceliklerinizden hangi odak alanlarıdır tooidentify istediğiniz ve, puanları zamanla nasıl değiştiğini adresindeki bakın.

Her öneri neden önemli olduğu hakkında yönergeler içerir. Merhaba öneri uygulama BT Hizmetleri ve hello iş gereksinimlerinizi kuruluşunuzun hello yapısını verilen sizin için uygun olup, bu kılavuzu tooevaluate kullanmanız gerekir.

## <a name="use-assessment-focus-area-recommendations"></a>Değerlendirme odak alanı önerileri kullanın
OMS içinde bir değerlendirme çözümü kullanmadan önce hello çözümü yüklenmiş olması gerekir. çözümler, yükleme hakkında daha fazla tooread bkz [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md). Yüklendikten sonra hello genel bakış sayfasında OMS hello SQL değerlendirmesi kutucuğu kullanarak önerileri hello özetini görüntüleyebilirsiniz.

Görünüm hello altyapınızı ve ardından-ayrıntıya önerileri için Uyumluluk değerlendirmesi özetlenir.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>bir odak alanı ve Al düzeltme eylemi için tooview önerileri
1. Merhaba üzerinde **genel bakış** hello sayfasında, **SQL değerlendirmesi** döşeme.
2. Merhaba üzerinde **SQL değerlendirmesi** sayfasında hello odak alanı Kanatlar birinde hello özet bilgileri gözden geçirin ve aşağıdakilerden tooview önerileri bu odaklanılan alan için tıklatın.
3. Merhaba odak alanı sayfaları hiçbirinde ortamınız için öncelik hello önerilerin görüntüleyebilirsiniz. Önerinin altında tıklatın **etkilenen nesneler** tooview hakkında ayrıntılı hello öneri yapılan neden.  
    ![SQL değerlendirmesi önerileri görüntüsü](./media/log-analytics-sql-assessment/sql-assess-focus.png)
4. Önerilen düzeltici eylemleri gerçekleştirebilirsiniz **önerilen eylemleri**. Merhaba öğesi ele, önerilen eylemler gerçekleştirilen ve uyumluluk puan artıracaktır sonraki değerlendirmeleri kaydeder. Düzeltilmiş öğeler görünür olarak **geçirilen nesneleri**.

## <a name="ignore-recommendations"></a>Öneriler yoksay
Tooignore istediğiniz önerileri varsa, OMS değerlendirme sonuçlarında görünmesini tooprevent önerileri kullanacağı bir metin dosyası oluşturabilirsiniz.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>göz ardı eder tooidentify önerileri
1. Tooyour çalışma alanında oturum ve günlük arama açın. Aşağıdaki, ortamınızdaki bilgisayarları için başarısız olan sorgu toolist önerileri hello kullanın.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   Bir ekran görüntüsü gösteren hello günlük arama sorgusu şöyledir: ![önerileri başarısız oldu](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)
2. Öneriler tooignore istediğinizi seçin. Merhaba sonraki yordamda Recommendationıd için hello değerleri kullanacaksınız.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate ve IgnoreRecommendations.txt metin dosyayı kullan
1. IgnoreRecommendations.txt adlı bir dosya oluşturun.
2. Her Recommendationıd, OMS tooignore ayrı bir satırda istediğiniz ve ardından hello dosyasını kaydedip kapatın, her bir öneri için yazın veya yapıştırın.
3. Merhaba dosya klasörü OMS tooignore önerileri istediğiniz her bilgisayarda aşağıdaki hello yerleştirin.
   * Microsoft Monitoring Agent (doğrudan veya Operations Manager aracılığıyla bağlı) - hello olan bilgisayarlarda *SystemDrive*: \Program izleme Agent\Agent
   * Merhaba Operations Manager yönetim sunucusunda - *SystemDrive*: \Program System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify önerileri göz ardı edilir
1. Merhaba Hello sonraki zamanlanmış değerlendirme, varsayılan olarak 7 günde çalıştıktan sonra belirtilen önerileri yoksayıldı işaretlenir ve hello değerlendirme Panoda görünmez.
2. Tüm göz ardı hello önerileri günlük arama sorguları toolist aşağıdaki hello kullanabilirsiniz.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. Daha sonra göz ardı toosee önerileri istemediğinize karar verirseniz, tüm IgnoreRecommendations.txt dosyaları silin veya bunları RecommendationIDs kaldırabilirsiniz.

## <a name="sql-assessment-solution-faq"></a>SQL değerlendirme çözümü hakkında SSS
*Sıklıkla bir değerlendirme çalışıyor mu?*

* Merhaba değerlendirme 7 günde bir çalışır.

*Merhaba değerlendirme çalıştıran bir şekilde tooconfigure ne sıklıkta var mı?*

* Şu anda değil.

*I hello SQL değerlendirme çözümü ekledikten sonra başka bir sunucuya belirlediyseniz değerlendirileceğini?*

* Evet, bunu daha sonra gelen her 7 günde değerlendirildiği bulunduktan sonra.

*Ne zaman bir sunucu kullanımdan alındığında hello değerlendirme kaldırılacak?*

* Bir sunucu için 3 hafta veri göndermez, kaldırılır.

*Veri toplama hello hello işlemin hello adı nedir?*

* AdvisorAssessment.exe

*Ne kadar süreyle için toplanan verileri toobe sürer?*

* Merhaba gerçek veri toplama hello sunucuda yaklaşık 1 saat sürer. Bu çok sayıda SQL örnekleri veya veritabanlarına sahip sunucularda uzun sürebilir.

*Hangi türde veri toplanır?*

* veri türleri aşağıdaki hello toplanır:
  * WMI
  * Kayıt defteri
  * Performans sayaçları
  * SQL Dinamik Yönetim görünümlerini (DMV).

*Verileri toplandığında yolu tooconfigure var mı?*

* Şu anda değil.

*Bir farklı çalıştır hesabı neden tooconfigure var mı?*

* SQL Server için SQL sorguları az sayıda çalıştırılır. Bunları sırayla toorun, bir farklı çalıştır hesabı VIEW SERVER STATE izinleri tooSQL birlikte kullanılmalıdır.  Ayrıca, sipariş tooquery WMI'da, yerel yönetici kimlik bilgileri gereklidir.

*Neden yalnızca hello ilk 10 önerileri görüntülemek?*

* Görevler kapsamlı bir zorlamayı listesi vermek yerine, öncelik hello önerileri adresleme odaklanmak öneririz. Bunları çözün sonra ek öneriler kullanılabilir hale gelir. Toosee hello ayrıntılı liste tercih ederseniz, tüm öneriler hello OMS günlük arama özelliğini kullanarak görüntüleyebilirsiniz.

*Herhangi bir şekilde tooignore bir öneri var mı?*

* Evet, bkz: [önerileri yoksay](#ignore-recommendations) yukarıdaki bölümde.

## <a name="next-steps"></a>Sonraki adımlar
* [Arama günlüklerini](log-analytics-log-searches.md) tooview ayrıntılı SQL Değerlendirme verileri ve öneriler.

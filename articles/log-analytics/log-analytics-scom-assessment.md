---
title: "aaaOptimize, System Center Operations Manager ortamınızı Azure günlük analizi ile | Microsoft Docs"
description: "Merhaba sistem Center Operations Manager çözüm tooassess risk ve sunucu ortamlarınızın durumunu düzenli aralıklarla hello değerlendirmesi kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a>Ortamınızı hello System Center Operations Manager değerlendirme (Önizleme) çözümü ile en iyi duruma getirme

![System Center Operations Manager değerlendirme simgesi](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

Merhaba sistem Center Operations Manager çözüm tooassess risk ve System Center Operations Manager server ortamlarınızın durumunu düzenli aralıklarla hello değerlendirmesi kullanabilirsiniz. Bu makalede, yükleme, yapılandırma ve olası sorunlar için düzeltme eylemleri yararlanabilmeniz hello çözümü kullanan yardımcı olur.

Bu çözüm önerileri belirli tooyour dağıtılan sunucu altyapısı öncelikli listesi sağlar. Merhaba önerileri hızlı bir şekilde Yardım alanları risk hello ve düzeltici işlemleri anlamak dört odak arasında ayrılır.

Merhaba önerilerin hello bilgi ve müşteri ziyaretleriniz binlerce Microsoft mühendisleri tarafından elde edilen deneyimlerden dayanır. Her bir öneri, bir sorun tooyou neden önemli ve nasıl tooimplement hello değişiklikleri önerilen hakkında rehberlik sağlar.

En önemli tooyour kuruluş ve ücretsiz ve sağlam bir risk ortam çalıştıran doğru ilerleme durumunuzu izlemenize odak alanlarına seçebilirsiniz.

Merhaba çözüm ekledik ve bir değerlendirme tamamlanan, Özet sonra bilgi odak alanlarına odaklanmak için hello üzerinde gösterilen **System Center Operations Manager değerlendirme** altyapınız için Pano. Merhaba aşağıdaki nasıl toouse hello hello hakkında bilgi bölümlerde **System Center Operations Manager değerlendirme** Pano, burada görüntüleyebilir ve ardından uygulayın Eylemler SCOM altyapınız için önerilir.

![System Center Operations Manager çözüm döşeme](./media/log-analytics-scom-assessment/scom-tile.png)

![System Center Operations Manager değerlendirme Panosu](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a>Yükleme ve yapılandırma hello çözümü

Merhaba çözüm, Microsoft System Operations Manager 2012 R2 ve 2012 SP1 ile çalışır.

Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.

 - OMS içinde bir değerlendirme çözümü kullanmadan önce hello çözümü yüklenmiş olması gerekir. Merhaba çözümden yüklemek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) veya hello yönergeleri izleyerek [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).

 - Merhaba çözüm toohello çalışma ekledikten sonra hello panosundaki hello System Center Operations Manager değerlendirme bölümünden hello ek yapılandırma gerekli iletisi görüntüler. Merhaba kutucuğuna tıklayın ve hello sayfasında belirtilen hello yapılandırma adımlarını izleyin

 ![System Center Operations Manager Pano kutucuğu](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 Merhaba System Center Operations Manager yapılandırmasını OMS hello çözümde hello yapılandırma sayfasında belirtilen hello adımları izleyerek hello komut dosyası aracılığıyla gerçekleştirilebilir.

 Bunun yerine, tooconfigure hello değerlendirmesi SCOM konsoldan izleyin hello aşağıdaki hello aynı adımları sırası
1. [System Center Operations Manager değerlendirmesi için Hello farklı çalıştır hesabı ayarlama](#operations-manager-run-as-accounts-for-oms)  
2. [Merhaba System Center Operations Manager değerlendirme kuralı yapılandırma](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a>System Center Operations Manager değerlendirme veri toplama ayrıntıları

System Center Operations Manager değerlendirme Hello WMI verilerini, kayıt defteri verilerini, olay günlüğü verilerini, Windows PowerShell, SQL sorguları, dosya bilgileri Toplayıcı etkinleştirdiğiniz hello sunucusu kullanarak Operations Manager veri toplar.

Merhaba aşağıdaki tabloda veri toplama yöntemleri System Center Operations Manager değerlendirmesi için gösterir ve ne sıklıkta bir aracı tarafından toplanan veriler.

| Platform | Doğrudan Aracısı | SCOM Aracısı | Azure Storage | SCOM gerekli? | Yönetim grubu gönderilen SCOM Aracısı verileri | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | | | | &#8226; | | yedi gün |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Operations Manager hesapları OMS için Çalıştır

Yönetim paketleri iş yükleri tooprovide için OMS derlemelerinde değeri-hizmetlerini ekleyin. Her iş yükü, bir etki alanı hesabı gibi farklı güvenlik bağlamında iş yüküne özgü ayrıcalıkları toorun yönetim paketleri gerektirir. Bir Operations Manager farklı çalıştır hesabı tooprovide kimlik bilgilerini yapılandırın.

Aşağıdaki bilgilerle tooset System Center Operations Manager değerlendirmesi için Operations Manager farklı çalıştırma hesabını hello hello kullanın.

### <a name="set-hello-run-as-account"></a>Set hello farklı çalıştır hesabı

1. Toohello Hello Operations Manager konsolu, Git **Yönetim** sekmesi.
2. Merhaba altında **Çalıştır Yapılandırması**, tıklatın **hesapları**.
3. Merhaba Çalıştır hello bir Windows hesabı oluşturma Sihirbazı'nı aşağıdaki hesabı, oluşturun. Merhaba hesap toouse hello bir tanımlanan tüm hello Önkoşullar aşağıdaki sahip değildir:

    >[!NOTE]
    Merhaba farklı çalıştır hesabı gereksinimleri karşılaması gerekir:
    - Etki alanı hesabı hello yerel Yöneticiler grubunun üyesi hello ortamında (tüm işlem yöneticisi rolleri - yönetim sunucusu, OpsMgr veritabanı, veri ambarı, raporlama, Web konsolu, ağ geçidi) tüm sunucularda
    - İşlem yöneticisi rolü incelenen hello yönetim grubu için
    - Merhaba yürütme [betik](#sql-script-to-grant-granular-permissions-to-the-run-as-account) toogrant ayrıntılı izinler toohello hesabı Operations Manager tarafından kullanılan SQL örneğinde.
      Not: Bu hesap sysadmin hakları zaten varsa, ardından hello komut dosyası yürütme atlayın.

4. Altında **dağıtım güvenliği**seçin **daha güvenli**.
5. Merhaba hesap dağıtılacağı yeri hello yönetim sunucusu belirtin.
3. Toohello Çalıştır yapılandırması geri dönün ve tıklatın **profilleri**.
4. Merhaba Ara *SCOM değerlendirme profili*.
5. Hello profil adı olmalıdır: *Microsoft System Center Advisor SCOM değerlendirme farklı çalıştır profili*.
6. Sağ tıklayın ve özelliklerini güncelleştirmek ve 3. adımda oluşturduğunuz hesap olarak çalıştır kısa süre önce oluşturuldu hello ekleyin.

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a>SQL komut dosyası toogrant ayrıntılı izinler toohello farklı çalıştır hesabı

SQL komut dosyası toogrant gerekli izinleri toohello farklı çalıştır hesabı Operations Manager tarafından kullanılan hello SQL örneğinde aşağıdaki hello yürütün.

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a>Merhaba değerlendirme kuralı yapılandırma

Merhaba System Center Operations Manager çözümün Yönetim Paketi, adında bir kural içerir değerlendirme *Microsoft System Center Advisor SCOM değerlendirme değerlendirme kural çalıştırma*. Bu kural, hello değerlendirme çalıştırmaktan sorumludur. tooenable kural hello ve hello sıklığı, aşağıdaki kullanım hello yordamlar yapılandırın.

Varsayılan olarak, Microsoft System Center Advisor SCOM değerlendirme değerlendirme kural çalıştırma hello devre dışıdır. toorun hello değerlendirmesi, bir yönetim sunucusunda hello kural etkinleştirmeniz gerekir. Merhaba aşağıdaki adımları kullanın.

#### <a name="enable-hello-rule-for-a-specific-management-server"></a>Belirli yönetim sunucusuna ilişkin Hello kuralını etkinleştir

1. Merhaba, **yazma** hello Operations Manager konsolunun, hello kuralını arayın çalışma *Microsoft System Center Advisor SCOM değerlendirme değerlendirme kural çalıştırma* hello içinde **kuralları** bölmesi.
2. Merhaba arama sonuçlarında seçin hello hello metin içeren bir *türü: Yönetim sunucusu*.
3. Merhaba kuralı sağ tıklatın ve ardından **geçersiz kılmaları** > **sınıfın belirli bir nesnesi için: Yönetim sunucusu**.
4.  Merhaba kullanılabilir yönetim sunucuları listesinde hello kural çalıştırdığı hello yönetim sunucusu seçin.
5.  Geçersiz kılma değeri çok değiştirdiğinizden emin olun**True** hello için **etkin** parametre değeri.  
    ![parametresi geçersiz kıl](./media/log-analytics-scom-assessment/rule.png)

Hala penceresinde bu sırada hello sonraki yordamı kullanarak çalıştırmak hello hello sıklığını yapılandırın.

#### <a name="configure-hello-run-frequency"></a>Merhaba çalıştırma sıklığı Yapılandır

Merhaba değerlendirme yapılandırılmış toorun her 10.080 dakikadır (veya yedi gün) hello varsayılan aralığıdır. Merhaba değeri tooa en düşük değer 1440 dakika (veya bir gün) geçersiz kılabilirsiniz. Merhaba değeri art arda değerlendirme çalışmaları arasında gerekli hello en düşük zaman aralığı temsil eder. toooverride hello aralığı, aşağıdaki hello adımları kullanın.

1. Merhaba, **yazma** hello Operations Manager konsolunun, hello kuralını arayın çalışma *Microsoft System Center Advisor SCOM değerlendirme değerlendirme kural çalıştırma* hello içinde **kuralları** bölmesi.
2. Merhaba arama sonuçlarında seçin hello hello metin içeren bir *türü: Yönetim sunucusu*.
3. Merhaba kuralı sağ tıklatın ve ardından **geçersiz kılma hello kural** > **sınıfın tüm nesneleri için: Yönetim sunucusu**.
4. Değişiklik hello **aralığı** parametre değeri tooyour İstenen aralık değeri. Merhaba aşağıdaki örnekte, hello değer too1440 (bir gün) dakika ayarlanır.  
    ![aralığı parametresi](./media/log-analytics-scom-assessment/interval.png)  
    Merhaba değer 1440 dakika daha tooless ayarlanırsa hello kuralı bir gün aralığında çalışır. Bu örnekte, hello kural hello aralık değeri göz ardı eder ve bir gün sıklığında çalıştırır.


## <a name="understanding-how-recommendations-are-prioritized"></a>Önerilerin nasıl önceliklendirilir anlama

Yapılan her öneri hello öneri göreceli önemini hello tanımlayan bir ağırlıklı değer verilir. Yalnızca hello 10 en önemli öneriler gösterilir.

### <a name="how-weights-are-calculated"></a>Ağırlıkları nasıl hesaplanır

Ağırlık belirlemeyi üç anahtar faktörlerini temel alarak toplam değerler şunlardır:

- Merhaba *olasılık* tanımlanan bir sorunun sorunlara neden. Daha yüksek olasılık büyük genel puan hello öneri tooa karşılık gelir.
- Merhaba *etkisi* kuruluşunuzdaki bir soruna neden olursa hello sorun. Daha yüksek bir etkisi, büyük genel puan hello öneri tooa karşılık gelir.
- Merhaba *çaba* tooimplement hello öneri gerekli. Daha yüksek çaba küçük genel puan hello öneri tooa karşılık gelir.

Her bir öneri ağırlığı hello hello toplam puanı her odak alanı için kullanılabilir bir yüzdesi olarak ifade edilir. Örneğin, bu öneri uygulama bir öneri hello kullanılabilirlik ve iş sürekliliği odaklanılan alan de bir puan % 5 varsa, genel kullanılabilirlik ve iş sürekliliği puan tarafından %5 artırır.

### <a name="focus-areas"></a>Odak alanları

**Kullanılabilirlik ve iş sürekliliği** -bu odaklanılan alan hizmet kullanılabilirliği, altyapı ve iş koruması dayanıklılık için öneriler gösterir.

**Performans ve ölçeklenebilirlik** -bu odaklanılan alan önerileri toohelp kuruluşunuzun gösterir BT altyapısı arttıkça, BT ortamınız geçerli performans gereksinimlerini karşıladığından ve mümkün toorespond toochanging olduğundan emin olun Altyapı gerekir.

**Yükseltme, geçiş ve dağıtım** - bu odak alanı yükseltme önerileri toohelp gösterir, geçirme ve SQL Server tooyour mevcut altyapıyı.

**İşlemler ve izleme** - bu odaklanılan alan önerileri toohelp daha verimli hale BT işlemlerinizi gösterir önleyici bakım uygulamak ve performansı en üst düzeye çıkarın.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Her odak alanında % 100 tooscore hedeflemeniz gerektiğini?

Olmayabilir. Merhaba önerileri hello bilgi ve müşteri ziyaretleriniz binlerce arasında Microsoft mühendisleri tarafından elde edilen deneyimleri temel alır. Ancak, iki sunucu altyapılar aynı hello ve belirli öneriler fazla veya az ilgili tooyou olabilir değildir. Örneğin, bazı güvenlik önerileri sanal makinelerinizi gösterilen toohello Internet değilseniz, daha az ilgili olabilir. Bazı kullanılabilirlik öneriler düşük öncelik geçici veri toplama ve raporlama sağladığı hizmetler için daha az uygun olmayabilir. Önemli tooa olgun iş sorunlarını daha az önemli tooa başlatma olabilir. Önceliklerinizden hangi odak alanlarıdır tooidentify istediğiniz ve, puanları zamanla nasıl değiştiğini adresindeki bakın.

Her öneri neden önemli olduğu hakkında yönergeler içerir. Bu kılavuz tooevaluate Hello öneri uygulama BT Hizmetleri ve hello iş gereksinimlerinizi kuruluşunuzun hello yapısını verilen sizin için uygun olup olmadığını kullanın.

## <a name="use-assessment-focus-area-recommendations"></a>Değerlendirme odak alanı önerileri kullanın

OMS içinde bir değerlendirme çözümü kullanmadan önce hello çözümü yüklenmiş olması gerekir. çözümler, yükleme hakkında daha fazla tooread bkz [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md). Yüklendikten sonra hello genel bakış sayfasında OMS hello System Center Operations Manager değerlendirme kutucuğu kullanarak önerileri hello özetini görüntüleyebilirsiniz.

Görünüm hello altyapınızı ve ardından-ayrıntıya önerileri için Uyumluluk değerlendirmesi özetlenir.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>bir odak alanı ve Al düzeltme eylemi için tooview önerileri

1. Merhaba üzerinde **genel bakış** hello sayfasında, **System Center Operations Manager değerlendirme** döşeme.
2. Merhaba üzerinde **System Center Operations Manager değerlendirme** sayfasında hello odak alanı Kanatlar birinde hello özet bilgileri gözden geçirin ve aşağıdakilerden tooview önerileri bu odaklanılan alan için tıklatın.
3. Merhaba odak alanı sayfaları hiçbirinde ortamınız için öncelik hello önerilerin görüntüleyebilirsiniz. Önerinin altında tıklatın **etkilenen nesneler** tooview hakkında ayrıntılı hello öneri yapılan neden.  
    ![Odaklanılan alan](./media/log-analytics-scom-assessment/focus-area.png)
4. Önerilen düzeltici eylemleri gerçekleştirebilirsiniz **önerilen eylemleri**. Merhaba öğesi ele, önerilen eylemler gerçekleştirilen ve uyumluluk puan artıracaktır sonraki değerlendirmeleri kaydeder. Düzeltilmiş öğeler görünür olarak **geçirilen nesneleri**.

## <a name="ignore-recommendations"></a>Öneriler yoksay

Tooignore istediğiniz önerileri varsa, değerlendirme sonuçlarında görünmesini tooprevent önerileri OMS kullanan bir metin dosyası oluşturabilirsiniz.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a>tooignore istediğiniz tooidentify önerileri

1. Tooyour çalışma alanında oturum ve günlük arama açın. Aşağıdaki, ortamınızdaki bilgisayarları için başarısız olan sorgu toolist önerileri hello kullanın.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    Bir ekran görüntüsü gösteren hello günlük arama sorgusu şöyledir:  
    ![günlük araması](./media/log-analytics-scom-assessment/scom-log-search.png)

2. Öneriler tooignore istediğinizi seçin. Merhaba sonraki yordamda Recommendationıd için hello değerleri kullanacaksınız.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate ve IgnoreRecommendations.txt metin dosyayı kullan

1. IgnoreRecommendations.txt adlı bir dosya oluşturun.
2. Her Recommendationıd, OMS tooignore ayrı bir satırda istediğiniz ve ardından hello dosyasını kaydedip kapatın, her bir öneri için yazın veya yapıştırın.
3. Merhaba dosya klasörü OMS tooignore önerileri istediğiniz her bilgisayarda aşağıdaki hello yerleştirin.
4. Merhaba Operations Manager yönetim sunucusunda - *SystemDrive*: \Program System Center 2012 R2\Operations Manager\Server.

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify önerileri göz ardı edilir

1. Merhaba Hello sonraki zamanlanmış değerlendirme, varsayılan olarak yedi günde çalıştıktan sonra belirtilen önerileri yoksayıldı işaretlenir ve hello değerlendirme Panoda görünmez.
2. Tüm göz ardı hello önerileri günlük arama sorguları toolist aşağıdaki hello kullanabilirsiniz.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. Daha sonra göz ardı toosee önerileri istemediğinize karar verirseniz, tüm IgnoreRecommendations.txt dosyaları silin veya bunları RecommendationIDs kaldırabilirsiniz.

## <a name="system-center-operations-manager-assessment-solution-faq"></a>System Center Operations Manager değerlendirme çözümü hakkında SSS

*Merhaba değerlendirme çözümü toomy OMS çalışma ekledim. Ancak hello önerilerini görmek yok. Neden olmasın?* Merhaba çözüm eklendikten sonra aşağıdaki adımları görünüm hello önerileri hello OMS Panoda hello kullanın.  

- [System Center Operations Manager değerlendirmesi için Hello farklı çalıştır hesabı ayarlama](#operations-manager-run-as-accounts-for-oms)  
- [Merhaba System Center Operations Manager değerlendirme kuralı yapılandırma](#configure-the-assessment-rule)


*Merhaba değerlendirme çalıştıran bir şekilde tooconfigure ne sıklıkta var mı?* Evet. Bkz: [çalıştırma sıklığı Yapılandır hello](#configure-the-run-frequency).

*I hello System Center Operations Manager değerlendirme çözümü ekledikten sonra başka bir sunucuya belirlediyseniz değerlendirileceğini?* Evet, bulma sonra onu sonra itibaren--varsayılan olarak, her yedi günde değerlendirildiği.

*Veri toplama hello hello işlemin hello adı nedir?* AdvisorAssessment.exe

*Burada hello AdvisorAssessment.exe işlemi çalışıyor mu?* AdvisorAssessment.exe hello değerlendirme kural etkinleştirdiğiniz hello HealthService hello management server'ın altında çalışır. Bu işlemi kullanarak, tüm ortamınız keşfinin uzak veri toplulukta elde edilir.

*Ne kadar veri toplamaya yönelik sürer?* Veri toplama hello sunucuda yaklaşık bir saat sürer. Bu, pek çok Operations Manager örnekleri veya veritabanlarına sahip ortamlarda daha uzun sürebilir.

*Ne hello değerlendirme tooless 1440 dakika daha hello aralığı ayarlarım?*  hello değerlendirme olan en fazla günde bir kez önceden yapılandırılmış toorun. Küçüktür 1440 dakika hello aralık değeri tooa değeri geçersiz kılarsanız hello değerlendirme 1440 dakika hello aralık değeri kullanır.

*Nasıl önkoşul hata varsa tooknow?* Ardından Hello değerlendirme çalıştırdı ve sonuçları görmüyorsanız, hello değerlendirmesi için ön koşullar hello bazıları başarısız olabilir. Sorguları çalıştırabilirsiniz: `Type=Operation Solution=SCOMAssessment` ve `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` günlük arama toosee hello ön koşullar başarısız oldu.

*Var olan bir `Failed tooconnect toohello SQL Instance (….).` önkoşul hatası iletisi. Merhaba sorun nedir?* AdvisorAssessment.exe, verileri toplar hello işlem hello HealthService hello management server'ın altında çalışır. Merhaba değerlendirme bir parçası olarak hello işlem tooconnect toohello hello Operations Manager veritabanı mevcut olduğu SQL Server çalışır. Güvenlik duvarı kuralları hello bağlantı toohello SQL Server örneği engellediğinizde bu hata oluşabilir.

*Hangi türde veri toplanır?*  veri türleri aşağıdaki hello toplanır: - WMI verilerini - kayıt defteri - olay günlüğü verilerini - Operations Manager verilerini Windows PowerShell, SQL sorguları ve dosya bilgileri Toplayıcı aracılığıyla.

*Bir farklı çalıştır hesabı neden tooconfigure var mı?* Bir Operations Manager sunucusu için çeşitli SQL sorguları çalıştırılır. Bunları sırayla toorun, gerekli izinlere sahip bir farklı çalıştır hesabı kullanmanız gerekir. Ayrıca, yerel yönetici kimlik bilgileri gerekli tooquery WMI bağlıdır.

*Neden yalnızca hello ilk 10 önerileri görüntülemek?* Görevlerin kapsamlı, zorlamayı listesi vermek yerine, öncelik hello önerileri adresleme odaklanmak öneririz. Bunları çözün sonra ek öneriler kullanılabilir hale gelir. Toosee hello ayrıntılı liste tercih ederseniz, tüm önerileri günlük arama özelliğini kullanarak görüntüleyebilirsiniz.

*Herhangi bir şekilde tooignore bir öneri var mı?* Evet, hello bkz [önerileri yoksay](#Ignore-recommendations).


## <a name="next-steps"></a>Sonraki adımlar

- [Arama günlüklerini](log-analytics-log-searches.md) tooview ayrıntılı System Center Operations Manager Değerlendirme verileri ve öneriler.

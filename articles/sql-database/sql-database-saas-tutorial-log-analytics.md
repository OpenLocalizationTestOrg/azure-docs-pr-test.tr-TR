---
title: "bir SQL veritabanı çok kiracılı uygulama ile aaaUse günlük analizi | Microsoft Docs"
description: "Kurulum ve günlük analizi (OMS) hello Azure SQL Database örnek Wingtip SaaS uygulaması ile kullanma"
keywords: "sql veritabanı öğreticisi"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a>Kurulum ve günlük analizi (OMS) hello Wingtip SaaS uygulama ile kullanma

Bu öğreticide ayarlama ve kullanma *günlük analizi ([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* esnek havuzlar ve veritabanları izleme. Merhaba üzerinde derlemeler [performans izleme ve yönetim öğretici](sql-database-saas-tutorial-performance-monitoring.md)ve gösterir nasıl toouse *günlük analizi* tooaugment hello izleme ve uyarma sağlanan hello Azure portalı. Log Analytics, yüzlerce havuz ve yüz binlerce veritabanını desteklediğinden özellikle büyük ölçekli izleme ve uyarı özellikleri için uygundur. Ayrıca, birden fazla Azure aboneliği genelinde farklı uygulamaların ve Azure hizmetlerinin izlenmesini tümleştiren tek bir izleme çözümü sağlar.

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Log Analytics’i yükleme ve yapılandırma (OMS)
> * Günlük analizi toomonitor havuzları ve veritabanları kullanın

Bu öğretici, Önkoşullar aşağıdaki yapma emin hello tamamlanır toocomplete:

* Merhaba Wingtip SaaS uygulaması dağıtılır. beş dakikadan kısa toodeploy bakın [dağıtma ve Merhaba Wingtip SaaS uygulaması keşfedin.](sql-database-saas-tutorial.md)
* Azure PowerShell’in yüklendiğinden. Ayrıntılar için bkz. [Azure PowerShell’i kullanmaya başlama](https://docs.microsoft.com/powershell/azure/get-started-azureps)

Merhaba bkz [performans izleme ve yönetim öğretici](sql-database-saas-tutorial-performance-monitoring.md) hello SaaS senaryolar ve desenleri ve bir izleme çözümü hello gereksinimleri nasıl etkilediklerini Tartışması için.

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a>Log Analytics (OMS) ile performansı izleme ve yönetme

SQL Veritabanı için veritabanı ve havuzlarda izleme ve uyarı özellikleri kullanılabilir. Bu yerleşik izleme ve uyarma kaynak özgü ve kaynak küçük sayılar için uygun olmakla birlikte uygun toomonitoring büyük yüklemeleri daha az veya farklı kaynaklar ve abonelikler arasında birleştirilmiş bir görünümünü sağlamak için.

Yüksek hacimli senaryolar için Log Analytics kullanılabilir. Bu analytics verilmiş tanılama günlüklerini sağlayan ayrı bir Azure hizmeti ve telemetri birçok özellikten toplayabilirsiniz günlük analizi çalışma alanındaki toplanan telemetri Hizmetleri ve kullanılan tooquery olması ve Uyarıları ayarlayın. Log Analytics, işlem verilerinin analiz edilmesini ve görselleştirilmesini sağlayan yerleşik bir sorgu dili ve veri görselleştirme araçları sunar. Hello SQL analiz çözümü çeşitli ön tanımlı esnek havuz ve izleme ve görünümleri ve sorguları uyarı veritabanı sağlar ve kendi geçici sorgular eklemek ve bunları gerektiği gibi kaydetmenize olanak tanır. OMS, özel bir görünüm tasarımcısı da sağlar.

Günlük analizi çalışma alanları ve analiz çözümleri hello Azure portalında hem de OMS açılabilir. Hello Azure portal hello yeni erişim noktası ancak bazı alanlar hello OMS portalında arkasında olabilir.

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a>Merhaba yük Oluşturucu toocreate veri tooanalyze Başlat

1. Açık **Demo PerformanceMonitoringAndManagement.ps1** hello içinde **PowerShell ISE**. Toorun isteyebileceğinizden bu komut dosyası açık hello yük nesil senaryolarından sırasında Bu öğretici tutun.
1. Beşten küçük kiracılar varsa, kiracılar tooprovide daha ilginç bir izleme bağlamı toplu sağlayın:
   1. **$DemoScenario = 1,** **Kiracı grubu sağlama** değerini ayarlayın
   1. Tuşuna **F5** toorun hello komut dosyası.

1. **$DemoScenario** = 2, **Normal yoğunlukta yük (yaklaşık 40 DTU) oluşturma**’yı ayarlayın.
1. Tuşuna **F5** toorun hello komut dosyası.

## <a name="get-hello-wingtip-application-scripts"></a>Merhaba Wingtip uygulama komut dosyaları alma

Merhaba Wingtip biletleri komut dosyaları ve uygulama kaynak koduna hello kullanılabilir [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github depo. Komut dosyaları hello bulunan [öğrenme modüller klasörüne](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules). Merhaba karşıdan **öğrenme modülleri** klasör yapısını koruma klasör tooyour yerel bilgisayar.

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a>Günlük analizi ve hello Azure SQL analiz çözümü yükleme ve yapılandırma

Günlük analizi yapılandırılmış toobe gerektiren ayrı bir hizmettir. Log Analytics, log analytics çalışma alanında günlük veriler, telemetri ve ölçümleri toplar. Çalışma alanı, Azure’daki diğer kaynaklara benzer bir kaynaktır ve oluşturulması gerekir. Merhaba çalışma hello oluşturulan toobe gerekmez ancak aynı kaynak grubunda izleme hello uygulamaları bu genellikle hello en anlamlı. Merhaba Wingtip SaaS uygulamasının Hello durumda bu hello kaynak grubunu silerek hello uygulama ile kolayca silinmiş hello çalışma toobe sağlar.

1. Aç... \\Öğrenme modülleri\\performans izleme ve Yönetim\\günlük analizi\\*Demo LogAnalytics.ps1* hello içinde **PowerShell ISE**.
1. Tuşuna **F5** toorun hello komut dosyası.

Bu noktada mümkün açık günlük analizi hello Azure portal (veya hello OMS portalı) olmalıdır. Merhaba günlük analizi çalışma alanı ve toobecome görünür toplanan telemetri toobe birkaç dakika sürer. Merhaba veri daha ilginç hello deneyimi hello toplama hello sistem bırakın daha uzun olur. Şimdi toograb içecek - yalnızca hello yük Oluşturucu hala çalıştığından emin olun zamanıdır!


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a>SQL analizi çözüm toomonitor havuzları ve veritabanları Merhaba ve günlük analizi kullanın


Bu alıştırmada, günlük analizi ve hello veritabanları ve havuzları için toplanan hello telemetri toolook hello OMS Portalı'nı açın.

1. Toohello Gözat [Azure portal](https://portal.azure.com) ve daha fazla hizmet tıklayarak günlük analizi açın ve ardından aramak için günlük analizi:

   ![log analytics’i aç](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. Adlı hello çalışma alanını seçin *wtploganalytics -&lt;kullanıcı&gt;*.

1. Seçin **genel bakış** tooopen hello hello Azure portalında günlük analizi çözümde.
   ![genel bakış-bağlantı](media/sql-database-saas-tutorial-log-analytics/click-overview.png)

    **Önemli**: birkaç hello çözüm etkinleştirilmeden önce dakika sürebilir. Sabırlı olun!

1. Azure SQL analizi döşeme tooopen Hello üzerinde tıklatın.

    ![genel bakış](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![analizler](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. kendi kaydırma çubuğu hello altındaki (gerekirse yenileme hello dikey) ile Merhaba çözüm dikey kayarken betiklerdeki görünümünde hello.

1. Burada kullanabileceğiniz hello zaman-kaydırıcı hello ayrıntıya Gezgini, bunları veya kaynakların tooopen tıklatarak çeşitli görünümleri üst sol veya tıklatın hello üzerinde dikey keşfedin üzerinde daha dar bir zaman dilimi içinde toofocus çubuğu. Bu görünüm ile belirli kaynaklar üzerinde tek tek veritabanlarını veya havuzları toofocus seçebilirsiniz:

    ![grafik](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. Geri hello çözüm dikey penceresinde, üzerinde tooopen tıklayın ve Araştır kaydedilmiş bazı sorgular toohello sağ kaydırma görürsünüz. Bunları değiştirmeyi deneyebilir ve oluşturduğunuz ilgi çekici sorguları daha sonra tekrar açıp diğer kaynaklarla kullanmak üzere kaydedebilirsiniz.

1. Geri hello günlük analizi çalışma alanı dikey penceresinde, OMS portalı tooopen hello çözümü vardır seçin.

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. Merhaba OMS portalında uyarılar yapılandırabilirsiniz. Merhaba uyarı kısmı hello veritabanı DTU görünümünü üzerinde'ı tıklatın.

1. Merhaba günlük arama görünür görünüm hello ölçümleri temsil ettiği bir çubuk grafik görürsünüz.

    ![günlük araması](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. Merhaba araç çubuğunda uyarıdaki tıklarsanız mümkün toosee hello uyarı yapılandırma olacaktır ve değiştirebilirsiniz.

    ![uyarı kuralı ekle](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

İzleme ve günlük analizi ve OMS uyarı hello sorgulamaları hello çalışma alanında, kaynak özgü olan her kaynak dikey penceresinde, uyarı hello aksine hello veriler üzerinde temel alır. Bu nedenle, veritabanı başına bir uyarı tanımlamak yerine tüm veritabanları için geçerli bir uyarı tanımlayabilirsiniz. İsterseniz birden fazla kaynak türü üzerinde birleşik bir sorgu kullanan bir uyarı da yazabilirsiniz. Sorgular yalnızca hello çalışma alanında kullanılabilir hello veri ile sınırlıdır.

SQL veritabanı için günlük analizi için hello veri birimi hello çalışma alanında göre ücretlendirilir. Bu öğreticide, günde sınırlı too500MB olduğu boş bir çalışma alanı oluşturuldu. Bu sınıra ulaşıldığında veri toohello çalışma alanı artık eklenir.


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunları öğrendiniz:

> [!div class="checklist"]
> * Log Analytics’i yükleme ve yapılandırma (OMS)
> * Günlük analizi toomonitor havuzları ve veritabanları kullanın

[Kiracı analizi öğreticisi](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a>Ek kaynaklar

* [Derleme hello ilk Wingtip SaaS uygulama dağıtımı sırasında ek öğreticileri](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Azure Log Analytics](../log-analytics/log-analytics-azure-sql.md)
* [OMS](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)

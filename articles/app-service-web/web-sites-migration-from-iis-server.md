---
title: aaaMigrate bir kurumsal web uygulama tooAzure uygulama hizmeti
description: "Var olan IIS Web siteleri tooAzure App Service Web Apps toouse Web Apps geçiş Yardımcısı tooquickly geçirmek nasıl gösterir"
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: 
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 7d66c5b799f0eefe85cbd9ba596ee0a05167f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-enterprise-web-app-tooazure-app-service"></a>Bir kurumsal web uygulama tooAzure uygulama hizmeti geçirme
Internet bilgi hizmeti (IIS) üzerinde 6 veya sonrası, var olan Web sitelerinizi kolayca geçirebilirsiniz çok[App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). 

> [!IMPORTANT]
> Windows Server 2003 Destek 14 Temmuz 2015 tarihinde sonuna ulaşıldı. Bir IIS sunucusundaki Windows Server 2003, Web sitelerinizi barındırıyorsanız, Web uygulamaları, çevrimiçi Web siteleri ve Web uygulamaları geçiş Yardımcısı yardımcı olabilecek tookeep otomatikleştirmek hello geçiş işlemi sizin için bir düşük riskli, düşük maliyetli ve düşük uyuşmazlık yoludur. 
> 
> 

[Web uygulamaları geçiş Yardımcısı](https://www.movemetothecloud.net/) IIS server yüklemenizin çözümlemek, hangi siteleri geçirilen tooApp hizmet olması, geçirilemez veya hello platformda desteklenmeyen herhangi bir öğenin vurgulayın ve sitelerinizi geçirmek tanımlamak ve ilişkili veritabanlarını tooAzure.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a>Uyumluluk Çözümleme sırasında doğrulandı öğeleri
Merhaba geçiş Yardımcısı olası herhangi bir sorun veya şirket içi IIS tooAzure App Service Web Apps başarılı bir geçiş engel engelleyici soruna neden olan bir hazırlık raporu tooidentify oluşturur. Merhaba anahtar öğeleri toobe farkında bazıları şunlardır:

* Bağlantı noktası bağlamalar – Web uygulamaları yalnızca bağlantı noktası 80 HTTP ve bağlantı noktası 443'tür için HTTPS trafiği için destekler. Farklı bir bağlantı noktası yapılandırmaları göz ardı edilir ve trafik yönlendirilmiş too80 veya 443 olacaktır. 
* Kimlik doğrulaması – Web uygulamaları destekleyen anonim kimlik doğrulaması varsayılan ve Forms kimlik doğrulaması tarafından bir uygulama tarafından belirtilen yerlerde. Windows kimlik doğrulaması, yalnızca Azure Active Directory ve ADFS ile tümleştirerek kullanılabilir. Diğer forms kimlik doğrulaması - Örneğin, temel kimlik doğrulaması - şu anda desteklenmemektedir. 
* Genel Derleme Önbelleği (GAC) – hello GAC Web uygulamalarında desteklenmiyor. Derlemeleri uygulamanızı başvuruyorsa, genellikle toohello GAC dağıtmak için Web uygulamaları'nde toodeploy toohello uygulama bin klasörü gerekir. 
* IIS5 Uyumluluk modunda – Web uygulamalarında desteklenmiyor. 
* Uygulama havuzlarında – Web uygulamaları, her site ve onun alt uygulamaları çalıştıran hello aynı uygulama havuzu. Sitenizin birden çok uygulama havuzları kullanan birden çok alt uygulamalar varsa, bunları ortak ayarlarla tooa tek bir uygulama havuzunda birleştirebilir veya her uygulama tooa ayrı bir web uygulaması geçirmek.
* COM bileşenlerini – Web Apps COM bileşenlerini hello kayıt hello platformunda izin vermiyor. Web siteleri veya uygulamaları herhangi COM bileşenlerini kullanmak yaparsanız, yönetilen kodda yeniden ve hello Web sitesi veya uygulama ile dağıtın.
* ISAPI uzantıları – Web Apps hello ISAPI uzantıları kullanımını destekler. Toodo hello aşağıdaki gerekir:
  
  * web uygulamanız ile Merhaba DLL'leri dağıtma 
  * Merhaba DLL'leri kullanarak kaydetmek [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)
  * "Arbitrart ISAPI uzantıları toobe izin vererek yüklenen içinde" özetlenen hello içerikle hello site kökünde bir applicationHost.xdt dosyası yerleştirin [bu makalenin](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples) 
    
  
    
    Daha fazla ilgili örnekler için Web sitesi ile XML dönüştürmeleri toouse bakın [Microsoft Azure Web sitenizi dönüştürme](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).
* SharePoint, FrontPage sunucu uzantılarını (FPSE) FTP diğer bileşenleri ister, SSL sertifikaları geçirilmez.

## <a name="how-toouse-hello-web-apps-migration-assistant"></a>Nasıl toouse hello Web Apps geçiş Yardımcısı
Bu bölüm bir örnek tootoomigrate birkaç Web siteleri bir SQL Server veritabanı kullanan ve bir şirket içi Windows Server 2003 R2 (IIS 6.0) makinede çalışan adımları:

1. Sunucu veya istemci makinenizde Hello IIS üzerinde gidin çok[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/) 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. Web uygulamaları geçiş Yardımcısı hello üzerinde tıklatarak yükleyin **ayrılmış IIS sunucusu** düğmesi. Daha fazla seçenek yakın hello seçeneklerinde olacaktır. 
3. Hello tıklatın **yükleme aracı** makinenizde Web Apps geçiş Yardımcısı tooinstall düğmesine tıklayın.
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > Tıklatarak **çevrimdışı yükleme için karşıdan** toodownload bir ZIP dosyası toohello bağlı sunucuları üzerinde yüklenmiyor Internet. Ya da tıklayabilirsiniz **var olan bir geçiş hazırlık raporu karşıya**, Gelişmiş seçenek toowork (daha sonra açıklanmıştır) daha önce oluşturulan mevcut bir geçiş hazırlık raporu sahip olduğu.
   > 
   > 
4. Merhaba, **uygulamayı yüklemek** ekranında **yükleme** makinenizde tooinstall. Gerekirse bunlara karşılık gelen bağımlılıklar gibi Web dağıtımı, DacFX ve IIS de yüklenir. 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   Yüklendikten sonra Web uygulamaları geçiş Yardımcısı otomatik olarak başlar.
5. Seçin **uzak sunucu tooAzure siteleri ve veritabanları geçirmek**. Hello uzak sunucu için Hello yönetici kimlik bilgilerini girin ve tıklayın **devam**. 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   Elbette, toomigrate hello yerel sunucudan seçebilirsiniz. Merhaba uzak seçenek, bir üretim IIS sunucusu toomigrate sitelerinden istediğinizde yararlıdır.
   
   Bu noktada hello geçiş aracı araştırmasını siteler, uygulamalar, uygulama havuzları ve bağımlılıkları tooidentify adayı Web siteleri gibi geçiş için IIS sunucunuzun yapılandırması hello. 
6. Merhaba ekran görüntüsü Aşağıda, üç Web siteleri – gösterir **varsayılan Web sitesi**, **TimeTracker**, ve **CommerceNet4**. Bunların tümünün toomigrate istiyoruz ilişkilendirilmiş bir veritabanı sahip. İster tooassess ve ardından hello siteleri seçin **sonraki**.
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. Tıklatın **karşıya** tooupload hello hazırlık raporu. Tıklatırsanız **dosyasını yerel olarak Kaydet**karşıya yükleme hello kaydedilmiş hazırlık raporu daha önce belirtildiği gibi ve hello geçiş aracı daha sonra yeniden çalıştırabilirsiniz.
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   Merhaba hazırlık raporu karşıya yükledikten sonra Azure hazır olma durumunu analiz ve sonuçları hello gösterir gerçekleştirir. Merhaba değerlendirme ayrıntıları her Web sitesi için okuma ve anlamak veya devam etmeden önce tüm sorunları ele olduğundan emin olun. 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. Tıklatın **başlamak geçiş** toostart hello geçiş. Yeniden yönlendirilen tooAzure toolog hesabınızda şimdi olacaktır. Etkin bir Azure aboneliği olan bir hesapla oturum açmanız önemlidir. Bir Azure hesabı olmayan sonra ücretsiz deneme için kaydolabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_). 
9. Merhaba Kiracı hesabı, Azure aboneliği ve geçirilen Azure web uygulamaları ve veritabanları için bölge toouse seçin ve ardından **Başlat geçiş**. Daha sonra hello Web siteleri toomigrate seçebilirsiniz.
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. Merhaba sonraki ekranda toohello varsayılan geçiş ayarları gibi değişiklik yapabilirsiniz:
    
    * Mevcut bir Azure SQL veritabanını kullan veya yeni bir Azure SQL veritabanı oluşturun ve kimlik bilgilerini yapılandırma
    * Merhaba Web siteleri toomigrate seçin
    * hello Azure web uygulamaları ve bunların bağlantılı SQL veritabanları için ad tanımlama
    * Merhaba genel ve site düzeyinde ayarlarını özelleştirme
    
    Merhaba ekran görüntüsü aşağıda hello varsayılan ayarlarla geçiş için seçilen tüm hello Web siteleri gösterir.
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > Merhaba **Azure Active Directory etkinleştirme** özel ayarları onay kutusu hello Azure web uygulaması ile tümleşir [Azure Active Directory](../active-directory/active-directory-whatis.md) (Merhaba **varsayılan dizin**). Azure Active Directory, şirket içi Active Directory ile eşitlenmesi ile ilgili daha fazla bilgi için bkz: [dizin tümleştirme](http://msdn.microsoft.com/library/jj573653).
    > 
    > 
11. Tüm istenen hello değişiklikleri yaptıktan sonra tıklatın **oluşturma** toostart hello geçiş işlemi. Merhaba geçiş aracı hello Azure SQL Database ve Azure web uygulaması oluşturabilir ve ardından hello Web sitesi içeriğini ve veritabanları yayımlayabilirsiniz. Merhaba geçiş ilerleme açıkça hello geçiş aracının gösterilir ve hangi ayrıntıları hello siteleri geçirilen hello son, bunların başarılı olup olmadığını, bağlantılar toohello yeni oluşturulan Azure web uygulamaları Özet bir ekran görürsünüz. 
    
    Herhangi bir geçiş işlemi sırasında hata oluşursa geçiş aracı açıkça hello varsa hello hatası ve geri alma hello değişiklikleri gösterir. Aynı zamanda toohello mühendislik ekibi doğrudan hello tıklayarak mümkün toosend hello hata raporu olacaktır **hata raporu gönder** düğmesi, hello yakalanan hatası çağrı yığını ile ve ileti gövdesi oluşturun. 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    Varsa geçirmek başarılı hata olmadan hello de tıklayabilirsiniz **görüş** doğrudan Microsoft'a tooprovide düğmesine tıklayın. 
12. Hello bağlantılar toohello Azure web uygulamaları'ı tıklatın ve hello geçiş başarılı olduğunu doğrulayın.
13. Artık yönetebilir hello Azure App Service'te web uygulamalarını geçişi. toodo Bu, günlük hello içine [Azure Portal](https://portal.azure.com).
14. Hello Azure Portal, hello Web Apps dikey toosee geçirilen sitelerinizi (web uygulamaları olarak gösterilir) açın ve herhangi bir tanesine tıklatın sürekli yayımlama, yedeklemeleri, otomatik ölçeklendirmeyi oluşturma ve kullanım izleme yapılandırma gibi hello web uygulamasını yönetme toostart veya performans.
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)


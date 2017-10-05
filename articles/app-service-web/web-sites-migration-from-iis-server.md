---
title: "Bir kuruluş web uygulamasını Azure App Service'a geçirme"
description: "Web uygulamaları geçiş Yardımcısı Azure App Service Web Apps için var olan IIS Web sitelerini hızlı bir şekilde geçirmek için nasıl kullanılacağını gösterir"
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
ms.openlocfilehash: 18d6a8da38b42dcf5c1500f7fc26638aea26a809
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-enterprise-web-app-to-azure-app-service"></a>Bir kuruluş web uygulamasını Azure App Service'a geçirme
Üzerinde Internet Information Service (IIS) 6 veya sonraki sürümünü çalıştıran, var olan Web sitelerinizi kolayca geçirebilirsiniz [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). 

> [!IMPORTANT]
> Windows Server 2003 Destek 14 Temmuz 2015 tarihinde sonuna ulaşıldı. Sitelerinizi bir IIS sunucusunda şu anda barındırıyorsa, Windows Server 2003 ', Web uygulamaları bir düşük riskli, düşük maliyetli olduğundan ve Web siteleri çevrimiçi tutmanın düşük uyuşmazlık yolu ve Web uygulamaları geçiş Yardımcısı, sizin için geçiş işlemini otomatikleştirmek yardımcı olabilir. 
> 
> 

[Web uygulamaları geçiş Yardımcısı](https://www.movemetothecloud.net/) IIS server yüklemenizin çözümlemek, hangi siteleri App Service'e geçirilmesi, geçirilemez veya platformda desteklenmeyen herhangi bir öğenin vurgulayın ve sitelerinizi geçirmek tanımlamak ve Azure ilişkili veritabanlarını.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a>Uyumluluk Çözümleme sırasında doğrulandı öğeleri
Geçiş Yardımcısı'nı ilgi veya şirket içi IIS'den başarılı bir geçiş Azure App Service Web Apps için engel engelleyici soruna herhangi olası nedenlerini tanımlamak için hazırlık raporu oluşturur. Dikkat edilmesi gereken önemli öğelerin bazıları şunlardır:

* Bağlantı noktası bağlamalar – Web uygulamaları yalnızca bağlantı noktası 80 HTTP ve bağlantı noktası 443'tür için HTTPS trafiği için destekler. Farklı bir bağlantı noktası yapılandırmaları göz ardı edilir ve trafiği 80 veya 443 yönlendirilir. 
* Kimlik doğrulaması – Web uygulamaları destekleyen anonim kimlik doğrulaması varsayılan ve Forms kimlik doğrulaması tarafından bir uygulama tarafından belirtilen yerlerde. Windows kimlik doğrulaması, yalnızca Azure Active Directory ve ADFS ile tümleştirerek kullanılabilir. Diğer forms kimlik doğrulaması - Örneğin, temel kimlik doğrulaması - şu anda desteklenmemektedir. 
* Genel Derleme Önbelleği (GAC) – GAC Web uygulamalarında desteklenmiyor. Uygulamanızı genellikle GAC'ye dağıttığınız derlemelerini başvuruyorsa, Web uygulamaları uygulama bin klasörüne dağıtmanız gerekir. 
* IIS5 Uyumluluk modunda – Web uygulamalarında desteklenmiyor. 
* Uygulama Havuzları – Web uygulamaları, her site ve onun alt uygulamaları, aynı uygulama havuzunda çalışacak. Birden çok uygulama havuzları kullanan birden çok alt uygulamaları siteniz varsa, bunları ortak ayarlar ile tek bir uygulama havuzuna birleştirebilir veya ayrı bir web uygulaması için her bir uygulama geçirmek.
* COM bileşenlerini – Web Apps COM bileşenlerini kayıt platformunda izin vermiyor. Web siteleri veya uygulamaları herhangi COM bileşenlerini kullanmak yaparsanız, yönetilen kodda yeniden ve Web sitesinin veya uygulamanın dağıtın.
* ISAPI uzantıları – Web Apps ISAPI uzantıları kullanımını destekler. Aşağıdakileri yapmanız gerekir:
  
  * web uygulamanız ile DLL'leri dağıtma 
  * DLL dosyaları kullanarak kaydetme [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)
  * "yüklenecek verme arbitrart ISAPI Uzantılarında" özetlenen içerikle sitesinin kök dizininde bir applicationHost.xdt dosyası yerleştirin [bu makalenin](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples) 
    
  
    
    Daha fazla ile Web sitenizi XML dönüştürmeleri kullanma örnekleri için bkz [Microsoft Azure Web sitenizi dönüştürme](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).
* SharePoint, FrontPage sunucu uzantılarını (FPSE) FTP diğer bileşenleri ister, SSL sertifikaları geçirilmez.

## <a name="how-to-use-the-web-apps-migration-assistant"></a>Web uygulamaları geçiş Yardımcısı'nı kullanma
Bu örnek için birkaç Web siteleri kullanan bir SQL Server veritabanı ve bir şirket içi Windows Server 2003 R2 (IIS 6.0) makinede çalışan geçirmek için bölüm adımları:

1. Sunucu veya istemci makinenizde IIS gidin [https://www.movemetothecloud.net/](https://www.movemetothecloud.net/) 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. Web uygulamaları geçiş Yardımcısı'nı tıklatarak yüklemek **ayrılmış IIS sunucusu** düğmesi. Daha fazla seçenek seçenekleri yakın gelecekte olacaktır. 
3. Tıklatın **yükleme aracı** düğmesi Web Apps geçiş Yardımcısı makinenize yükleyin.
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > Tıklatarak **indirmek için çevrimdışı yükleme** internet'e bağlı değil sunucularda yüklemek için bir ZIP dosyası indirilemedi. Ya da tıklayabilirsiniz **var olan bir geçiş hazırlık raporu karşıya**, (daha sonra açıklanmıştır) daha önce oluşturulan mevcut bir geçiş hazırlık raporu ile çalışmak için Gelişmiş bir seçenek değil.
   > 
   > 
4. İçinde **uygulamayı yüklemek** ekranında **yükleme** makinenize yüklemek için. Gerekirse bunlara karşılık gelen bağımlılıklar gibi Web dağıtımı, DacFX ve IIS de yüklenir. 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   Yüklendikten sonra Web uygulamaları geçiş Yardımcısı otomatik olarak başlar.
5. Seçin **uzak bir sunucudan siteleri ve veritabanları için Azure geçirmek**. Uzak sunucu için yönetici kimlik bilgilerini girin ve tıklayın **devam**. 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   Elbette, yerel sunucudan geçirmek seçebilirsiniz. Uzak seçeneği, bir üretim IIS sunucusundan Web siteleri geçirmek istediğiniz yararlıdır.
   
   Bu noktada geçiş aracı araştırmasını gibi siteler, uygulamalar, uygulama havuzları ve bağımlılıkları geçiş için aday Web siteleri belirlemek için IIS sunucunuzun yapılandırması. 
6. Üç Web sitelerinin – aşağıdaki ekran görüntüsünde gösterildiği **varsayılan Web sitesi**, **TimeTracker**, ve **CommerceNet4**. Bunların tümünün biz geçirmek istediğiniz bir ilişkili veritabanı sahip. İstediğiniz değerlendirmek ve ardından siteleri seçin **sonraki**.
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. Tıklatın **karşıya** hazırlık raporu karşıya yüklemek için. Tıklatırsanız **dosyasını yerel olarak Kaydet**, geçiş aracı daha sonra yeniden çalıştırın ve daha önce belirtildiği gibi kaydedilmiş hazırlık raporu karşıya yükleyin.
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   Hazırlık raporu karşıya yükledikten sonra Azure hazırlık çözümleme yapar ve sonuçları gösterir. Her Web sitesi için değerlendirme ayrıntıları okuyun ve anlamak veya devam etmeden önce tüm sorunları ele olduğundan emin olun. 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. Tıklatın **başlamak geçiş** geçişi başlatmak için. Artık Azure hesabınızda oturum yönlendirilirsiniz. Etkin bir Azure aboneliği olan bir hesapla oturum açmanız önemlidir. Bir Azure hesabı olmayan sonra ücretsiz deneme için kaydolabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_). 
9. Kiracı hesabı, Azure aboneliği ve geçirilen Azure web uygulamaları ve veritabanları için kullanın ve ardından bölge seçin **Başlat geçiş**. Daha sonra geçirmek için Web siteleri seçebilirsiniz.
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. Sonraki ekranda değişiklikleri varsayılan geçiş ayarları için aşağıdaki gibi yapabilirsiniz:
    
    * Mevcut bir Azure SQL veritabanını kullan veya yeni bir Azure SQL veritabanı oluşturun ve kimlik bilgilerini yapılandırma
    * geçirmek için Web siteleri seçin
    * Azure web uygulamaları ve bunların bağlantılı SQL veritabanları için ad tanımlama
    * Genel ayarları ve site düzeyinde ayarlarını Özelleştir
    
    Aşağıdaki ekran görüntüsünde varsayılan ayarlarla geçiş için seçilen tüm Web siteleri gösterir.
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > **Azure Active Directory etkinleştirme** özel ayarları onay kutusu Azure web uygulaması ile tümleşir [Azure Active Directory](../active-directory/active-directory-whatis.md) ( **varsayılan dizin**). Azure Active Directory, şirket içi Active Directory ile eşitlenmesi ile ilgili daha fazla bilgi için bkz: [dizin tümleştirme](http://msdn.microsoft.com/library/jj573653).
    > 
    > 
11. İstediğiniz değişiklikleri yaptıktan sonra tıklatın **oluşturma** geçiş işlemini başlatmak üzere. Geçiş Aracı Azure SQL Database ve Azure web uygulaması oluşturun ve veritabanları ve Web sitesi içeriğini yayımlama. Geçişin ilerleme durumunu açıkça geçiş aracının gösterilir ve başarılı olup olmadığını siteler geçirilen ayrıntılandıran bağlantılar için yeni oluşturulan Azure web uygulamaları sonunda Özet bir ekran görürsünüz. 
    
    Geçiş sırasında herhangi bir hata meydana gelirse, geçiş aracı açıkça değişiklikleri geri alma ve hata gösterir. Aynı zamanda tıklayarak doğrudan mühendislik Takımı'na hata raporu göndermek mümkün olacaktır **hata raporu gönder** düğmesi, yakalanan hatayla çağrı yığını ve ileti gövdesi yapı. 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    Varsa geçirmek başarılı hata olmadan tıklatabilirsiniz **görüş** herhangi görüşünüzü doğrudan düğmesi. 
12. Azure web uygulamalarının bağlantılarını tıklatın ve geçiş başarılı olduğunu doğrulayın.
13. Artık Azure App Service'te geçirilen web uygulamalarını yönetebilir. Bunu yapmak için oturum açın [Azure Portal](https://portal.azure.com).
14. Azure Portalı'nı (web uygulamaları olarak gösterilir), geçirilen Web sitelerinizi görmek için Web Apps dikey penceresini açın ve ardından herhangi biri sürekli yayımlama yedeklemeler, otomatik ölçeklendirmeyi ve izleme kullanım veya performans oluşturma, yapılandırma gibi web uygulaması yönetmeye başlamak için tıklayın.
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)


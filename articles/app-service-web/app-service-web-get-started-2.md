---
title: "İlk web uygulamanıza işlevsellik ekleme | Microsoft Docs"
description: "Birkaç dakika içinde ilk web uygulamanıza harika özellikler ekleyin."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 542671c2-22f0-4f20-8b4b-fa477264c492
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2016
ms.author: cephalin
ms.openlocfilehash: cf07c4142d025517637e31b27f1f34b6d402d6fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="add-functionality-to-your-first-web-app"></a>İlk web uygulamanıza işlevsellik ekleme
[Beş dakikada Azure’a ilk web uygulamanızı dağıtma](app-service-web-get-started-dotnet.md) bölümünde [Azure Uygulama Hizmeti](../app-service/app-service-value-prop-what-is.md)’ne örnek bir web uygulaması dağıttınız. Bu makalede dağıtılmış web uygulamanıza hızla harika özellikler ekleyeceksiniz. Birkaç dakika içinde:

* kullanıcılarınız için kimlik doğrulaması zorlayacaksınız
* uygulamanızı otomatik olarak ölçeklendireceksiniz
* uygulamanızın performansı ile ilgili uyarılar alacaksınız

Önceki makalede dağıttığınız örnek uygulamadan bağımsız olarak öğreticiyi izleyebilirsiniz.

Bu öğreticideki üç etkinlik, web uygulamanızı App Service’e eklediğinizde yararlanabileceğiniz çok sayıda kullanışlı özellikle ilgili bazı örneklerdir. Özelliklerin bir kısmı **Ücretsiz** katmanında yer alır (ilk web uygulamanız bu katmanda çalıştırılır) ve daha yüksek fiyatlandırma katmanı gerektiren özellikleri denemek için deneme kredinizi kullanabilirsiniz. Özellikle farklı bir fiyatlandırma katmanında yer alacak şekilde değiştirilmediği sürece web uygulamanızın **Ücretsiz** katmanda kalacağından emin olabilirsiniz.

> [!NOTE]
> Azure CLI ile oluşturduğunuz web uygulaması, kaynak kotalı yalnızca bir paylaşılan VM örneğine izin veren **Ücretsiz** katmanında çalıştırılır. **Ücretsiz** katmanı ile elde ettikleriniz hakkında daha fazla bilgi edinmek için bkz [App Service sınırları](../azure-subscription-service-limits.md#app-service-limits).
> 
> 

## <a name="authenticate-your-users"></a>Kullanıcılarınızın kimliklerini doğrulama
Şimdi uygulamanıza kimlik doğrulama eklemenin ne kadar kolay olduğuna bir göz atalım (ayrıntılı bilgi için [App Service Kimlik Doğrulama/Yetkilendirme](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)’ye bakın).

1. Az önce açtığınız uygulamanızın portal dikey penceresinde **Ayarlar** > **Kimlik Doğrulama/ Yetkilendirme**’ye tıklayın.  
    ![Kimlik doğrulama - ayarlar dikey penceresi](./media/app-service-web-get-started/aad-login-settings.png)
2. Kimlik doğrulamayı açmak için **Açık**’a tıklayın.  
3. **Kimlik Doğrulama Sağlayıcıları** altında **Azure Active Directory**’ye tıklayın.  
    ![Kimlik doğrulama - Azure AD’yi seçin](./media/app-service-web-get-started/aad-login-config.png)
4. **Azure Active Directory Ayarları** dikey penceresinde **Hızlı**’ya ve ardından **Tamam**’a tıklayın. Varsayılan ayarlar, varsayılan dizininizde yeni bir Azure Ad uygulaması oluşturur.  
    ![Kimlik doğrulama - hızlı yapılandırma](./media/app-service-web-get-started/aad-login-express.png)
5. **Kaydet** düğmesine tıklayın.  
    ![Kimlik doğrulama - yapılandırmayı kaydetme](./media/app-service-web-get-started/aad-login-save.png)
   
    Değiştirme başarılı olduğunda kolay bir bildirimle bildirim zilinin yeşile döndüğünü göreceksiniz.
6. Uygulamanızın portal dikey penceresinde **URL** bağlantısına (veya menü çubuğundaki **Gözat**’a) tıklayın. Bağlantı bir HTTP adresidir.  
    ![Kimlik doğrulama - URL’ye göz atma](./media/app-service-web-get-started/aad-login-browse-click.png)  
    Ancak uygulamayı yeni bir sekmede açtığında, URL kutusu birkaç kez yeniden yönlendirir ve bir HTTPS adresi ile uygulamanızda tamamlar. Şu anda, Azure aboneliğinizde zaten oturum açtığınızı ve uygulamada kimliğinizin otomatik olarak doğrulandığını görüyorsunuz.  
    ![Kimlik doğrulama - oturum açıldı](./media/app-service-web-get-started/aad-login-browse-http-postclick.png)  
    Böylece, eğer farklı bir tarayıcıda kimliği doğrulanmamış oturum açarsanız, aynı URL’ye gittiğinizde oturum açma ekranını göreceksiniz.  
    <!-- ![Authenticate - login page](./media/app-service-web-get-started/aad-login-browse.png)  -->
    Azure Active Directory ile daha önce hiçbir şey yapmadıysanız, varsayılan dizininizde Azure AD kullanıcısı olmayabilir. Bu durumda burada olması muhtemel tek hesap, Azure aboneliğinizle birlikte Microsoft hesabıdır. Bu nedenle daha önce aynı tarayıcıdan uygulamada otomatik olarak oturum açtınız.
    Bu sayfada oturum açmak için aynı Microsoft hesabını da kullanabilirsiniz.

Tebrikler, web uygulamanıza gelen tüm trafik için kimlik doğrulama yapıyorsunuz.

**Kimlik Doğrulama / Yetkilendirme** dikey penceresinde çok daha fazlasını yapabileceğinizi görmüşsünüzdür; örneğin:

* Sosyal oturum açmayı etkinleştirme
* Birden çok oturum açma seçeneği etkinleştirme
* Kullanıcılar uygulamanıza ilk kez eriştiğinde varsayılan davranışı değiştirme

App Service, kimlik doğrulama mantığını sizin sağlamanıza gerek kalmaması için bazı genel kimlik doğrulama ihtiyaçlarına yönelik anahtar teslim bir çözüm sunar.
Daha fazla bilgi için bkz. [App Service Kimlik Doğrulama/Yetkilendirme](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

## <a name="scale-your-app-automatically-based-on-demand"></a>Uygulamanızı talep doğrultusunda otomatik olarak ölçeklendirme
Şimdi, kapasitesini kullanıcı talebine yanıt verecek şekilde otomatik olarak ayarlaması için uygulamanızı otomatik olarak ölçeklendirelim (daha fazla bilgi için [Azure’da uygulamanızı ölçeklendirme](web-sites-scale.md) ve [Örnek sayısını elle veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md)).

Kısaca, web uygulamanızı iki şekilde ölçeklendirebilirsiniz:

* [Ölçeği artırma](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Daha fazla CPU, bellek, disk alanı ve özel VM’ler, özel etki alanları ve sertifikalar, hazırlama yuvaları, otomatik ölçeklendirme ve daha fazla özellikten yararlanın. Uygulamanızın dahil olduğu App Service planının fiyatlandırma katmanını değiştirerek ölçeği artırabilirsiniz.
* [Ölçeği genişletme](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Uygulamanızı çalıştıran VM örneği sayısını artırır.
  Fiyatlandırma katmanınıza bağlı olarak en fazla 50 örnek ile ölçek genişletme yapabilirsiniz.

Daha fazla beklemeden otomatik ölçeklendirmeyi ayarlayalım.

1. İlk olarak otomatik ölçeklendirmeyi etkinleştirmek üzere ölçeği artıralım. Uygulamanızın portal dikey penceresinde **Ayarlar** > **Ölçeği Artır (App Service Planı)** seçeneğine tıklayın.  
    ![Ölçeği artırma - ayarlar dikey penceresi](./media/app-service-web-get-started/scale-up-settings.png)
2. Aşağı kaydırın ve otomatik ölçeklendirmeyi destekleyen en düşük katman olan **S1 Standart** katmanını seçin (ekran görüntüsünde yuvarlak içine alınmıştır), ardından **Seç**’e tıklayın.  
    ![Ölçeği artırma - katman seçme](./media/app-service-web-get-started/scale-up-select.png)
   
    Ölçeği artırdınız.
   
   > [!IMPORTANT]
   > Bu katman ücretsiz deneme kredinizi harcar. Kullandıkça öde hesabınız varsa, bu hesabınızdan düşülecektir.
   > 
   > 
3. Ardından, otomatik ölçeklendirmeyi yapılandıralım. Uygulamanızın portal dikey penceresinde **Ayarlar** > **Ölçeği Genişlet (App Service Planı)**’a tıklayın.  
    ![Ölçeği genişletme - ayarlar dikey penceresi](./media/app-service-web-get-started/scale-out-settings.png)
4. **Ölçeklendirme yöntemi**’ni **CPU Yüzdesi** olarak değiştirin. Açılır menünün altındaki kaydırıcılar uygun şekilde güncelleştirilir. Ardından **1** ile **2** arasında **Örnekler** aralığı, **40** ile **80** arasında **Hedef aralık** belirleyin. Bunu, kutuların içine yazarak veya kaydırıcıları hareket ettirerek gerçekleştirin.  
    ![Ölçeği genişletme - otomatik ölçeklendirmeyi yapılandırma](./media/app-service-web-get-started/scale-out-configure.png)
   
    Bu yapılandırmaya göre CPU kullanımı %80’in üzerine çıktığında uygulamanız ölçeği genişletecek, CPU kullanımı %40’ın altına düştüğünde ölçeği daraltacaktır.
5. Menü çubuğunda **Kaydet**’e tıklayın.

Tebrikler, uygulamanız otomatik ölçeklendirme yapıyor.

**Ölçeklendirme Ayarları** dikey penceresinde çok daha fazlasını yapabilirsiniz; örneğin:

* Belirli sayıda örneğe elle ölçeklendirme
* Bellek yüzdesi veya disk kuyruğu gibi diğer performans ölçümlerine göre ölçeklendirme
* Bir performans kuralı tetiklendiğinde ölçeklendirme davranışını özelleştirme
* Bir takvime göre otomatik ölçeklendirme
* Gelecekteki bir etkinlik için otomatik ölçeklendirme davranışını ayarlama

Uygulamanızın ölçeğini genişletme ile ilgili daha fazla bilgi için bkz. [Azure’da uygulamanızı ölçeklendirme](web-sites-scale.md). Ölçeği artırma ile ilgili daha fazla bilgi için bkz. [Örnek sayacını elle veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md).

## <a name="receive-alerts-for-your-app"></a>Uygulamanız için uyarılar alma
Artık uygulamanız otomatik ölçeklendirme yapıyor; maksimum örnek sayısı (2) ve CPU’nun istenilen kullanımın (%80) üzerine çıkması durumunda ne olur?
Örneğin bu durumda daha fazla ölçek genişletme/artırma yapabilmeniz için sizi durumdan haberdar edecek bir alarm kurabilirsiniz (daha fazla bilgi için [Uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)). Bu senaryo için hemen bir uyarı ayarlayalım.

1. Uygulamanızın portal dikey penceresinde **Araçlar** > **Uyarılar**’a tıklayın.  
    ![Uyarılar - ayarlar dikey penceresi](./media/app-service-web-get-started/alert-settings.png)
2. **Uyarı ekle**’ye tıklayın. Ardından **Kaynaklar** kutusunda **(serverfarms)** ile biten kaynağı seçin. Bu, App Service planınızdır.  
    ![Uyarılar - App Service planınız için uyarı ekleme](./media/app-service-web-get-started/alert-add.png)
3. **Ad** olarak `CPU Maxed`, **Ölçüm** olarak **CPU Yüzdesi** ve **Eşik** olarak `90` değerlerini belirleyin ve ardından **E-posta sahipleri, katkıda bulunanlar ve okuyucular**ı seçip **Tamam**’a tıklayın.   
    ![Uyarılar - uyarı yapılandırma](./media/app-service-web-get-started/alert-configure.png)
   
    Azure uyarı oluşturmayı tamamladığında bu uyarıyı **Uyarılar** dikey penceresinde göreceksiniz.  
    ![Uyarılar - tamamlanmış görünüm](./media/app-service-web-get-started/alert-done.png)

Tebrikler, artık uyarı alıyorsunuz.

Bu uyarı ayarı beş dakikada bir CPU kullanımını denetler. Bu rakam %90’ın üzerine çıkarsa, size ve yetkisi olan herkese bir e-posta uyarısı gönderilecektir. Uyarıları alma yetkisi bulunanları görmek için uygulamanızın portal dikey penceresine geri giderek **Erişim** düğmesine tıklayın.  
![Uyarıları alan kişileri görme](./media/app-service-web-get-started/alert-rbac.png)

**Abonelik yöneticilerinin** halihazırda uygulamada **Sahip** durumunda olduklarını görmüş olmalısınız. Azure aboneliğinizin (örneğin deneme aboneliğinizin) hesap yöneticisiyseniz bu grupta siz de yer alacaksınız. Azure rol tabanlı erişim denetimi ile ilgili daha fazla bilgi için bkz [Azure Rol Tabanlı Erişim Denetimi](../active-directory/role-based-access-control-configure.md).

> [!NOTE]
> Uyarı kuralları bir Azure özelliğidir. Daha fazla bilgi için bkz. [Uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar
Uyarı yapılandırırken **Araçlar** dikey penceresinde zengin bir araç kümesi olduğunu fark etmiş olabilirsiniz. Burada sorunları giderebilir, performansı izleyebilir, güvenlik açıklarına karşı test yürütebilir, kaynakları yönetebilir, VM konsolu ile etkileşime geçebilir ve kullanışlı uzantılar ekleyebilirsiniz. Parmaklarınızın ucundaki basit ve güçlü araçları keşfetmek için bu araçların her birine tıklamanızı öneriyoruz.

Dağıttığınız uygulama ile daha fazlasını nasıl başarabileceğinizi öğrenin. Burada, yapabileceklerinizden yalnızca bazıları yer almaktadır:

* [Özel bir etki alanı adı satın alma ve yapılandırma](custom-dns-web-site-buydomains-web-app.md) - web uygulamanız için *.azurewebsites.net etki alanı yerine çekici bir etki alanı satın alın. Veya sahip olduğunuz bir etki alanını kullanın.
* [Hazırlık ortamları ayarlama](web-sites-staged-publishing.md) - Uygulamanızı üretime geçirmeden önce bir hazırlık URL’sine dağıtın. Canlı web uygulamanızı güvenle güncelleştirin. Birden çok dağıtım yuvası ile kapsamlı bir DevOps çözümü ayarlayın.
* [Sürekli dağıtım ayarlama](app-service-continuous-deployment.md) - Uygulama dağıtımınızı kaynak denetim sisteminizle tümleştirin. Her işleme ile Azure’a dağıtma
* [Şirket içi kaynaklara erişim](web-sites-hybrid-connection-get-started.md) - Mevcut şirket içi veritabanına veya CRM sistemine erişin.
* [Uygulamanızı yedekleme](web-sites-backup.md) - Web uygulamanız için yedekleme ve geri yükleme ayarlayın. Beklenmedik arızalara hazırlıklı olun ve arızalardan kurtulun.
* [Tanılama günlüklerini etkinleştirme](web-sites-enable-diagnostic-log.md) - Azure veya uygulama izlemelerinden IIS günlüklerini okuyun. Bir akış içinde okuyun, indirin veya anahtar teslim analizler için [Application Insights](../application-insights/app-insights-overview.md)’a aktarın.
* [Güvenlik açıklarına karşı tarama](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) -
  tarafından sağlanan hizmetle modern tehditlere karşı web uygulamanızı tarayın [Tinfoil Security](https://www.tinfoilsecurity.com/).
* [Arka plan işleri çalıştırma](../azure-functions/functions-overview.md) - Veri işleme, raporlama vb. için iş çalıştırın.
* [App Service’ın nasıl çalıştığını öğrenin](../app-service/app-service-how-works-readme.md)


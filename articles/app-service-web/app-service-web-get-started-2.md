---
title: "aaaAdd işlevselliği tooyour ilk web uygulaması | Microsoft Docs"
description: "Harika özellikler tooyour ilk web uygulamanızı birkaç dakika içinde ekleyin."
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
ms.openlocfilehash: 46c9b118c2c188508cb0a369c691a79073b7d7b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-functionality-tooyour-first-web-app"></a>İşlevselliği tooyour ilk web uygulaması Ekle
İçinde [beş dakika içinde ilk web uygulama tooAzure dağıtmak](app-service-web-get-started-dotnet.md), örnek bir web uygulaması için dağıtılan [Azure App Service](../app-service/app-service-value-prop-what-is.md). Bu makaledeki bazı harika özellikler tooyour dağıtılan web uygulaması hızlı bir şekilde ekleyeceksiniz. Birkaç dakika içinde:

* kullanıcılarınız için kimlik doğrulaması zorlayacaksınız
* uygulamanızı otomatik olarak ölçeklendireceksiniz
* Uygulamanızın hello performansı uyarıları alma

Merhaba önceki makalede dağıttığınız örnek uygulamadan bağımsız olarak, size hello öğreticide izleyebilirsiniz.

Bu öğretici olan App Service'te web uygulamanızı eklediğinizde yararlanabileceğiniz çok sayıda kullanışlı özellikle yalnızca birkaç örnekleri hello Hello üç etkinlikler. Merhaba özelliklerinin çoğunu hello kullanılabilir **serbest** Katmanı (olmayan ilk web uygulamanızı çalıştıran), ve daha yüksek fiyatlandırma katmanı gerektiren özellikleri çıkışı, deneme krediler tootry kullanabilirsiniz. REST web uygulamanızı kalan olabilirsiniz **serbest** açıkça tooa fiyatlandırma katmanı farklı değiştirilmediği sürece katmanı.

> [!NOTE]
> Azure CLI ile oluşturduğunuz hello web uygulaması çalıştıran **serbest** bir paylaşılan VM örneğine kaynak Kotalı yalnızca izin veren katmanı. **Ücretsiz** katmanı ile elde ettikleriniz hakkında daha fazla bilgi edinmek için bkz [App Service sınırları](../azure-subscription-service-limits.md#app-service-limits).
> 
> 

## <a name="authenticate-your-users"></a>Kullanıcılarınızın kimliklerini doğrulama
Şimdi, ne kadar kolay tooadd kimlik doğrulaması tooyour uygulama olduğunu görelim (daha fazla bilgi [App Service kimlik doğrulama/yetkilendirme](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)).

1. Merhaba portal dikey penceresinde uygulamanız için az önce açtığınız, **ayarları** > **kimlik doğrulama / yetkilendirme**.  
    ![Kimlik doğrulama - ayarlar dikey penceresi](./media/app-service-web-get-started/aad-login-settings.png)
2. Tıklatın **üzerinde** tooturn kimlik doğrulaması.  
3. **Kimlik Doğrulama Sağlayıcıları** altında **Azure Active Directory**’ye tıklayın.  
    ![Kimlik doğrulama - Azure AD’yi seçin](./media/app-service-web-get-started/aad-login-config.png)
4. Merhaba, **Azure Active Directory ayarları** dikey penceresinde tıklatın **Express**, ardından **Tamam**. Merhaba varsayılan ayarlarını yeni oluşturun, varsayılan dizininizde Azure AD uygulaması.  
    ![Kimlik doğrulama - hızlı yapılandırma](./media/app-service-web-get-started/aad-login-express.png)
5. **Kaydet** düğmesine tıklayın.  
    ![Kimlik doğrulama - yapılandırmayı kaydetme](./media/app-service-web-get-started/aad-login-save.png)
   
    Merhaba değiştirme başarılı olduğunda kolay bir ileti ile birlikte yeşile hello bildirim zil görürsünüz.
6. Geri hello portal dikey, uygulamanızın penceresinde hello tıklayın **URL** bağlantısı (veya **Gözat** hello menü çubuğunda). Merhaba, bir HTTP adresi bağlantısıdır.  
    ![Kimlik doğrulama - tooURL Gözat](./media/app-service-web-get-started/aad-login-browse-click.png)  
    Ancak hello uygulama yeni bir sekmede açılır sonra birkaç kez URL kutusu yeniden yönlendirmeleri hello ve bir HTTPS adresi ile uygulamanızda tamamlanır. Ne tooyour Azure aboneliği zaten olduğunuz kaydedilir ve hello uygulamada otomatik olarak kimliği doğrulanmış görüyorsunuz.  
    ![Kimlik doğrulama - oturum açıldı](./media/app-service-web-get-started/aad-login-browse-http-postclick.png)  
    Şimdi, farklı bir tarayıcıda kimliği doğrulanmamış oturum açarsanız toohello gittiğinizde oturum açma ekranı görürsünüz aynı URL.  
    <!-- ![Authenticate - login page](./media/app-service-web-get-started/aad-login-browse.png)  -->
    Azure Active Directory ile daha önce hiçbir şey yapmadıysanız, varsayılan dizininizde Azure AD kullanıcısı olmayabilir. Bu durumda, muhtemelen hello yalnızca hesap burada olan hello Azure aboneliğinizle Microsoft hesabı. Toohello uygulamada otomatik olarak kaydedilmiş neden aynı, hello sahip tarayıcı daha önce.
    Bu oturum açma sayfasında da o aynı Microsoft hesabı toolog kullanabilirsiniz.

Tebrikler, tüm trafik tooyour web uygulaması kimlik doğrulaması.

Hello fark etmiş olabilirsiniz **kimlik doğrulama / yetkilendirme** gibi bir çok şey yapabilirsiniz dikey penceresinde:

* Sosyal oturum açmayı etkinleştirme
* Birden çok oturum açma seçeneği etkinleştirme
* Kişiler tooyour uygulama ilk kez gittiğinizde hello varsayılan davranışı değiştirme

Uygulama hizmeti tooprovide hello kimlik doğrulaması mantığı kendiniz gerekmeyen şekilde gereksinimlerine bazı hello ortak kimlik doğrulaması için bir anahtar teslim çözümü sağlar.
Daha fazla bilgi için bkz. [App Service Kimlik Doğrulama/Yetkilendirme](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

## <a name="scale-your-app-automatically-based-on-demand"></a>Uygulamanızı talep doğrultusunda otomatik olarak ölçeklendirme
Daha sonra şirketinizdeki otomatik ölçeklendirme şekilde otomatik olarak onu kapasite toorespond toouser isteğe bağlı ayarlar için uygulamanızı (daha fazla bilgi [Azure uygulamanızda ölçeklendirin](web-sites-scale.md) ve [örnek sayısı el ile veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md)).

Kısaca, web uygulamanızı iki şekilde ölçeklendirebilirsiniz:

* [Ölçeği artırma](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Daha fazla CPU, bellek, disk alanı ve özel VM’ler, özel etki alanları ve sertifikalar, hazırlama yuvaları, otomatik ölçeklendirme ve daha fazla özellikten yararlanın. Fiyatlandırma katmanı uygulamanızın ait olduğu uygulama hizmeti planının hello değiştirerek ölçeği.
* [Ölçeği genişletme](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): uygulamanızı çalıştıran VM örneği hello sayısını artırma.
  Fiyatlandırma katmanınıza bağlı 50 örnek kadar tooas ölçeklendirebilirsiniz.

Daha fazla beklemeden otomatik ölçeklendirmeyi ayarlayalım.

1. İlk olarak, tooenable otomatik ölçeklendirmeyi ayarlayalım şimdi ölçeklendirin. Merhaba portal dikey penceresinde, uygulamanızın içinde tıklatın **ayarları** > **ölçeği Artır (App Service planı)**.  
    ![Ölçeği artırma - ayarlar dikey penceresi](./media/app-service-web-get-started/scale-up-settings.png)
2. Kaydırma ve select hello **S1 standart** katmanı, hello (ekran görüntüsünde yuvarlak içine alınmıştır) otomatik ölçeklendirmeyi destekleyen en düşük katman ve ardından **seçin**.  
    ![Ölçeği artırma - katman seçme](./media/app-service-web-get-started/scale-up-select.png)
   
    Ölçeği artırdınız.
   
   > [!IMPORTANT]
   > Bu katman ücretsiz deneme kredinizi harcar. Kullanım başına ödeme hesabınız varsa, ücretleri tooyour hesabı doğurur.
   > 
   > 
3. Ardından, otomatik ölçeklendirmeyi yapılandıralım. Merhaba portal dikey penceresinde, uygulamanızın içinde tıklatın **ayarları** > **ölçeği Genişlet (App Service planı)**.  
    ![Ölçeği genişletme - ayarlar dikey penceresi](./media/app-service-web-get-started/scale-out-settings.png)
4. Değişiklik **göre Ölçeklendirmeniz** çok**CPU yüzdesi**. Merhaba açılır altında Hello kaydırıcılar uygun şekilde güncelleştirin. Ardından **1** ile **2** arasında **Örnekler** aralığı, **40** ile **80** arasında **Hedef aralık** belirleyin. Bunu hello kutularına yazarak veya hello kaydırıcıları hareket ettirerek gerçekleştirin.  
    ![Ölçeği genişletme - otomatik ölçeklendirmeyi yapılandırma](./media/app-service-web-get-started/scale-out-configure.png)
   
    Bu yapılandırmaya göre CPU kullanımı %80’in üzerine çıktığında uygulamanız ölçeği genişletecek, CPU kullanımı %40’ın altına düştüğünde ölçeği daraltacaktır.
5. Tıklatın **kaydetmek** hello menü çubuğunda.

Tebrikler, uygulamanız otomatik ölçeklendirme yapıyor.

Hello fark etmiş olabilirsiniz **ölçek ayarları** gibi bir çok şey yapabilirsiniz dikey penceresinde:

* Tooa belirli sayıda örneğe elle ölçeklendirme
* Bellek yüzdesi veya disk kuyruğu gibi diğer performans ölçümlerine göre ölçeklendirme
* Bir performans kuralı tetiklendiğinde ölçeklendirme davranışını özelleştirme
* Bir takvime göre otomatik ölçeklendirme
* Gelecekteki bir etkinlik için otomatik ölçeklendirme davranışını ayarlama

Uygulamanızın ölçeğini genişletme ile ilgili daha fazla bilgi için bkz. [Azure’da uygulamanızı ölçeklendirme](web-sites-scale.md). Ölçeği artırma ile ilgili daha fazla bilgi için bkz. [Örnek sayacını elle veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md).

## <a name="receive-alerts-for-your-app"></a>Uygulamanız için uyarılar alma
Uygulamanız otomatik ölçeklendirme yapıyor, hello en fazla örnek sayısı (2) ulaştığında ve CPU istenilen kullanımın (% 80) olduğunda ne olur?
Bir alarm kurabilirsiniz (daha fazla bilgi [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)) daha fazla şekilde bu durumun ölçeklendirmek genişletme/artırma uygulamanızı, örneğin tooinform. Bu senaryo için hemen bir uyarı ayarlayalım.

1. Merhaba portal dikey penceresinde, uygulamanızın içinde tıklatın **Araçları** > **uyarıları**.  
    ![Uyarılar - ayarlar dikey penceresi](./media/app-service-web-get-started/alert-settings.png)
2. **Uyarı ekle**’ye tıklayın. Ardından hello **kaynak** kutusunda ile biten select hello kaynak **(serverfarms)**. Bu, App Service planınızdır.  
    ![Uyarılar - App Service planınız için uyarı ekleme](./media/app-service-web-get-started/alert-add.png)
3. **Ad** olarak `CPU Maxed`, **Ölçüm** olarak **CPU Yüzdesi** ve **Eşik** olarak `90` değerlerini belirleyin ve ardından **E-posta sahipleri, katkıda bulunanlar ve okuyucular**ı seçip **Tamam**’a tıklayın.   
    ![Uyarılar - uyarı yapılandırma](./media/app-service-web-get-started/alert-configure.png)
   
    Azure hello uyarı oluşturmayı tamamladığında, hello görürsünüz **uyarıları** dikey.  
    ![Uyarılar - tamamlanmış görünüm](./media/app-service-web-get-started/alert-done.png)

Tebrikler, artık uyarı alıyorsunuz.

Bu uyarı ayarı beş dakikada bir CPU kullanımını denetler. Bu rakam %90’ın üzerine çıkarsa, size ve yetkisi olan herkese bir e-posta uyarısı gönderilecektir. toosee yetkili tooreceive hello uyarılar herkes Git hello'ı tıklatın ve geri toohello, uygulamanızın portal dikey penceresinde **erişim** düğmesi.  
![Uyarıları alan kişileri görme](./media/app-service-web-get-started/alert-rbac.png)

Görmelisiniz **abonelik yöneticileri** hello durumda **sahibi** hello uygulamasının. Azure aboneliğinizin (örneğin Deneme aboneliğinizin bir) hello Hesap Yöneticisi iseniz bu grup, içerir. Azure rol tabanlı erişim denetimi ile ilgili daha fazla bilgi için bkz [Azure Rol Tabanlı Erişim Denetimi](../active-directory/role-based-access-control-configure.md).

> [!NOTE]
> Uyarı kuralları bir Azure özelliğidir. Daha fazla bilgi için bkz. [Uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar
Yol tooconfigure hello üzerinde uyarı, zengin bir hello araçlarında fark etmiş **Araçları** dikey. Burada, giderebileceğinizi sorunları, performansı izleyebilir, güvenlik açıklarına karşı test, kaynakları yönetmek, hello VM konsolu ile etkileşime ve kullanışlı uzantılar ekleyebilirsiniz. Her birinde bu toodiscover hello basit ancak güçlü araçlar parmaklarınızın tooclick davet ediyoruz.

Öğrenin toodo dağıttığınız uygulama ile daha fazla. Burada, yapabileceklerinizden yalnızca bazıları yer almaktadır:

* [Özel bir etki alanı adı satın alma ve yapılandırma](custom-dns-web-site-buydomains-web-app.md) - web uygulamanız için *.azurewebsites.net etki alanı yerine çekici bir etki alanı satın alın. Veya sahip olduğunuz bir etki alanını kullanın.
* [Hazırlık ortamları ayarlama](web-sites-staged-publishing.md) -URL üretime geçirmeden önce hazırlama, uygulama tooa dağıtın. Canlı web uygulamanızı güvenle güncelleştirin. Birden çok dağıtım yuvası ile kapsamlı bir DevOps çözümü ayarlayın.
* [Sürekli dağıtım ayarlama](app-service-continuous-deployment.md) - Uygulama dağıtımınızı kaynak denetim sisteminizle tümleştirin. Her işleme ile Azure’a dağıtma
* [Şirket içi kaynaklara erişim](web-sites-hybrid-connection-get-started.md) - Mevcut şirket içi veritabanına veya CRM sistemine erişin.
* [Uygulamanızı yedekleme](web-sites-backup.md) - Web uygulamanız için yedekleme ve geri yükleme ayarlayın. Beklenmedik arızalara hazırlıklı olun ve arızalardan kurtulun.
* [Tanılama günlüklerini etkinleştirme](web-sites-enable-diagnostic-log.md) -okunur hello IIS Azure veya uygulama izlemelerinden günlüğe kaydeder. Bir akış içinde okuyun, indirin veya anahtar teslim analizler için [Application Insights](../application-insights/app-insights-overview.md)’a aktarın.
* [Güvenlik açıklarına karşı tarama](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) -
  tarafından sağlanan hizmetle modern tehditlere karşı web uygulamanızı tarayın [Tinfoil Security](https://www.tinfoilsecurity.com/).
* [Arka plan işleri çalıştırma](../azure-functions/functions-overview.md) - Veri işleme, raporlama vb. için iş çalıştırın.
* [App Service’ın nasıl çalıştığını öğrenin](../app-service/app-service-how-works-readme.md)


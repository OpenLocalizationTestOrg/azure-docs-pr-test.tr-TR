---
title: "aaaOpen kaynak teknolojileri SSS Azure web uygulamaları | Microsoft Docs"
description: "Azure App Service Web Apps özelliğini hello açık kaynak teknolojileri hakkında sorular yanıtlar toofrequently alın."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a>Açık kaynak teknolojileri Azure Web uygulamaları için sık sorulan sorular

Bu makalede hello için açık kaynak teknolojileri ile ilgili sorunlar hakkında sorulan sorular (SSS) yanıtlar toofrequently sahip [Azure App Service Web Apps özelliğini](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a>ClearDB veritabanı kullanılamıyor. Bu nasıl giderebilirim?

Veritabanı ile ilgili sorunlar için başvurun [ClearDB Destek](https://www.cleardb.com/developers/help/support). 

ClearDB ilgili yanıtlar toocommon sorular için bkz: [ClearDB SSS](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a>ClearDB veritabanı hello Portalı'nda neden listede yok?

Hello bir ClearDB veritabanı oluşturursanız [Azure portal](http://portal.azure.com/), hello veritabanı hello görünmüyor [Klasik Azure portalı](http://manage.windowsazure.com/). toowork bu geçici veritabanı toohello web uygulamanızı elle bağlantı kurabilir.

Benzer şekilde, bir ClearDB veritabanı hello oluşturursanız [Klasik Azure portalı](http://manage.windowsazure.com/), hello veritabanınızda görmezsiniz [Azure portal](http://portal.azure.com/). Bu durumda, geçici bir çözüm kullanılabilir değildir. 

Daha fazla bilgi için bkz: [ClearDB MySQL veritabanları için SSS Azure uygulama hizmeti ile](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a>Neden ClearDB veritabanı my abonelik geçişi sırasında geçirilen değildi?

Abonelikler arasında kaynak geçiş gerçekleştirdiğinizde, bazı sınırlamalar uygulanır. ClearDB MySQL veritabanı bir üçüncü taraf hizmeti ve Azure abonelik geçişi sırasında geçirilmez.

Azure kaynaklarınızı geçirmeden önce MySQL veritabanınızı hello geçişini yönetmiyorsanız ClearDB MySQL veritabanı kullanılamıyor olabilir. tooavoid Bu, ilk olarak, el ile ClearDB veritabanınızı geçirin ve ardından hello web uygulamanız için Azure aboneliği geçirin.

Daha fazla bilgi için bkz: [ClearDB MySQL veritabanları için SSS Azure uygulama hizmeti ile](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a>Üzerinde PHP tootroubleshoot PHP sorunları günlüğü nasıl kapatırım?

PHP günlüğünü tooturn:

1. İçinde tooyour oturum [Kudu Web sitesi](https://*yourwebsitename*.scm.azurewebsites.net).
2. Merhaba üst menüde seçin **hata ayıklama Konsolu'nda** > **CMD**.
3. Select hello **Site** klasör.
4. Select hello **wwwroot** klasör.
5. Select hello  **+**  simgesine ve ardından **yeni dosya**.
6. Merhaba dosya adı çok ayarlamak**. user.ini**.
7. Merhaba Kurşun Kalem simgesini seçin sonraki çok**. user.ini**.
8. Merhaba dosyasında bu kodu ekleyin:`log_errors=on`
9. **Kaydet**’i seçin.
10. Merhaba Kurşun Kalem simgesini seçin sonraki çok**wp-config.php**.
11. Merhaba metin toohello kod aşağıdaki gibi değiştirin:
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. Hello hello web uygulama menüsünde, Azure portal, web uygulamanızı yeniden başlatın.

Daha fazla bilgi için bkz: [etkinleştirmek WordPress Hata günlüklerini](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a>App Service içinde barındırılan uygulamalar, Python uygulama hatalarını nasıl oturum?

toocapture Python uygulama hatalarını:

1. Hello Azure portalında, web uygulamanızı seçin **ayarları**.
2. Merhaba üzerinde **ayarları** sekmesine **uygulama ayarları**.
3. Altında **uygulama ayarları**, anahtar/değer çifti aşağıdaki hello girin:
    * Anahtar: WSGI_LOG
    * Değer: D:\home\site\wwwroot\logs.txt (dosya adı seçiminizi girin)

Şimdi hello wwwroot klasöründe hello logs.txt dosyasındaki hatalar görmeniz gerekir.

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a>Merhaba App Service içinde barındırılan bir Node.js uygulaması hello sürümünü nasıl değişiyor?

Merhaba Node.js uygulaması toochange hello sürümü, aşağıdaki seçenekleri şu hello birini kullanabilirsiniz:

*   Hello Azure portal, kullanın **uygulama ayarları**.
    1. Hello Azure portal, tooyour web uygulamasına gidin.
    2. Merhaba üzerinde **ayarları** dikey penceresinde, select **uygulama ayarları**.
    3. İçinde **uygulama ayarları**WEBSITE_NODE_DEFAULT_VERSION başlangıç anahtarı olarak içerebilir ve hello Node.js sürümünü hello değeri olarak istiyor.
    4. Tooyour Git [Kudu konsol](https://*yourwebsitename*.scm.azurewebsites.net).
    5. toocheck Node.js sürümünü Merhaba, komutu aşağıdaki hello girin:  
   ```
   node -v
   ```
*   Merhaba iisnode.yml dosyasını değiştirin. Merhaba iisnode.yml dosyasını değişen hello Node.js sürümünde yalnızca o iisnode hello çalışma zamanı ortamı ayarlar kullanır. Kudu cmd ve diğerleri kümesinde hello Node.js sürümünü kullanmaya devam **uygulama ayarları** hello Azure Portalı'nda.

    tooset hello iisnode.yml uygulama kök klasörünüzde el ile bir iisnode.yml dosyasını oluşturun. Merhaba dosyasında aşağıdaki satırı hello şunlardır:
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   Merhaba iisnode.yml dosyasını kaynak denetimi dağıtımı sırasında package.json kullanarak ayarlayın.
    Hello Azure kaynak denetimi dağıtım işlemi hello aşağıdaki adımları içerir:
    1. İçerik toohello Azure web uygulaması taşır.
    2. Hiç yoksa (deploy.cmd, .deployment dosyaları) hello web uygulaması kök klasöründe bir varsayılan dağıtım betiğini oluşturur.
    3. Hangi oluşturduğu bir iisnode.yml dosyasını hello Node.js sürümünü hello package.json dosyasında Bahsediyor, bir dağıtım betiği çalıştıran > altyapısı`"engines": {"node": "5.9.1","npm": "3.7.3"}`
    4. Merhaba iisnode.yml dosyasını aşağıdaki kod hello sahiptir:
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a>App Service içinde barındırılan my WordPress uygulamasında selamlama iletisine "veritabanı bağlantısı kurma hatası" görüyorum. Bu nasıl giderebilirim?

Tam hello adımları Azure WordPress uygulaması, tooenable php_errors.log ve debug.log bu hatayı görürseniz, ayrıntılı [etkinleştirmek WordPress Hata günlüklerini](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

Merhaba günlükleri etkinleştirildiğinde, hello hatayı yeniden oluşturmaya ve bağlantıları dışında çalıştırıyorsanız hello günlükleri toosee kontrol edin:
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

Debug.log veya php_errors.log dosyalarınızı bu hatayı görürseniz, uygulamanızı bağlantı hello sayısını aşıyor. ClearDB üzerinde koyduysanız hello kullanılabilir olan bağlantı sayısı doğrulayın, [hizmet planı](https://www.cleardb.com/pricing.view).

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a>App Service içinde barındırılan bir Node.js uygulaması nasıl hata?

1.  Tooyour Git [Kudu konsol](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).
2.  Git tooyour uygulama günlükleri klasöründe (D:\home\LogFiles\Application).
3.  Merhaba logging_errors.txt dosyasında içerik için denetleyin.

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a>Yerel Python modüllerini nasıl bir App Service web uygulaması veya API uygulaması yükleme?

Bazı paketler, Azure'da PIP kullanarak yüklemeyebilir. Merhaba paket Python paket dizinini hello üzerinde kullanılabilir olabilir ya da bir derleyici gerekli olabilir (derleyici hello web uygulaması App Service içinde çalışan hello bilgisayarda kullanılabilir değildir). App Service web apps ve API apps yerel modülleri yükleme hakkında daha fazla bilgi için bkz: [uygulama hizmeti yükleme Python modülleri](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a>Django uygulama tooApp hizmet Python Git ve hello yeni sürümünü kullanarak nasıl dağıtıldığına?

Django yükleme hakkında daha fazla bilgi için bkz: [Django uygulama tooApp hizmet dağıtma](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).

## <a name="where-are-hello-tomcat-log-files-located"></a>Bulunan hello Tomcat günlük dosyalarının nerede?

Azure Market ve özel dağıtımlar için:

* Klasör konumu: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs
* İlgilenilen dosyalar:
    * catalina. *yyyy-aa-gg*.log
    * ana bilgisayar-yöneticisi. *yyyy-aa-gg*.log
    * localhost. *yyyy-aa-gg*.log
    * Yöneticisi. *yyyy-aa-gg*.log
    * site_access_log. *yyyy-aa-gg*.log


Portal için **uygulama ayarları** dağıtımlar:

* Klasör konumu: D:\home\LogFiles
* İlgilenilen dosyalar:
    * catalina. *yyyy-aa-gg*.log
    * ana bilgisayar-yöneticisi. *yyyy-aa-gg*.log
    * localhost. *yyyy-aa-gg*.log
    * Yöneticisi. *yyyy-aa-gg*.log
    * site_access_log. *yyyy-aa-gg*.log

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a>Nasıl JDBC sürücüsü bağlantı hatalarını giderme?

Tomcat günlüklerinizi iletisinde aşağıdaki hello görebilirsiniz:

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

tooresolve hello hata:

1. Merhaba sqljdbc*.jar dosyasını uygulama/lib klasörünüzden kaldırın.
2. Merhaba özel Tomcat veya Azure Market Tomcat web sunucusu kullanıyorsanız, bu .jar dosya toohello Tomcat lib klasörüne kopyalayın.
3. Azure portal Java'dan etkinleştiriyorsanız hello (seçin **Java 1.8** > **Tomcat sunucusunu**), paralel tooyour uygulama hello klasör hello sqljdbc.* jar dosya kopyala. Ardından, aşağıdaki sınıf ayarı toohello web.config dosyasına hello ekleyin:

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a>Toocopy dinamik günlük dosyalarını çalıştığınızda neden hataları görüyor?

Java uygulama (örneğin, Tomcat) için toocopy dinamik günlük dosyaları çalışırsanız, bu FTP hata görebilirsiniz:

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

Merhaba hata iletisi, FTP hello istemci bağlı olarak değişebilir.

Tüm Java uygulamalarını bu bir kilitleme sorunu var. Yalnızca Kudu hello uygulama çalışırken bu dosya indirme destekler.

Durdurma hello uygulamanın toothese dosyaları FTP erişimi verir.

Başka bir çözüm toowrite bir zamanlamaya göre çalışır ve bu dosyaları tooa farklı dizine kopyalar bir Web işi ' dir. Örnek proje için bkz: hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) projesi.

## <a name="where-do-i-find-hello-log-files-for-jetty"></a>Merhaba günlük dosyaları için Jetty nerede bulabilirim?

Market ve özel dağıtımlar için hello günlük dosyası hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs klasöründe bulunur. Merhaba klasör konumu, kullanmakta olduğunuz Jetty hello sürümü bağlı olduğunu unutmayın. Örneğin, hello yolu buraya 9.1.2 Jetty için sağlanır. Jetty_ için Ara*YYYY_MM_DD*. stderrout.log.

Portal uygulama ayarı dağıtımları için D:\home\LogFiles hello günlük dosyasıdır. Jetty_ için Ara*YYYY_MM_DD*. stderrout.log

## <a name="can-i-send-email-from-my-azure-web-app"></a>My Azure web uygulamasından e-posta gönderebilir miyim?

Uygulama hizmeti yerleşik e-posta özelliği yoktur. Uygulamanızdan, e-posta göndermek için bazı iyi alternatifleri görmek için bu [yığın taşması tartışma](http://stackoverflow.com/questions/17666161/sending-email-from-azure).

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a>Neden WordPress Sitem tooanother URL yeniden yönlendirme?

TooAzure son geçiş yaptıysanız, WordPress toohello eski etki alanı URL'si yönlendirebilir. Bu ayar hello MySQL veritabanında kaynaklanır.

WordPress arkadaş + Azure Site doğrudan hello veritabanında tooupdate hello yeniden yönlendirme URL'sini kullanabileceğiniz uzantısıdır. WordPress arkadaş + kullanma hakkında daha fazla bilgi için bkz: [WordPress araçları ve MySQL geçiş ile WordPress arkadaş +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

Alternatif olarak, SQL sorguları veya PHPMyAdmin kullanarak toomanually güncelleştirme hello yeniden yönlendirme URL'sini tercih ederseniz, bkz. [WordPress: toowrong URL yeniden yönlendirme](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a>Oturum açma WordPress parolamı nasıl değişiyor?

Oturum açma WordPress parolanızı unuttuysanız, WordPress arkadaş + tooupdate kullanabilirsiniz. Parola, yükleme hello WordPress arkadaş + Azure Site uzantısı ve ardından tam hello adımları açıklanan tooreset [WordPress araçları ve MySQL geçiş ile WordPress arkadaş +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a>İçinde tooWordPress oturum açamazsınız. Bu nasıl giderebilirim?

Kendiniz WordPress dışında bir eklenti yükledikten sonra son kilitli bulursanız, hatalı bir eklenti olabilir. WordPress arkadaş + yardımcı olabilecek bir Azure Site uzantısı, WordPress eklentileri devre dışı bırak'dır. Daha fazla bilgi için bkz: [WordPress araçları ve MySQL geçiş ile WordPress arkadaş +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="how-do-i-migrate-my-wordpress-database"></a>WordPress Veritabanım nasıl geçişini?

Bağlı tooyour WordPress Web sitesidir geçirme hello MySQL veritabanı için birçok seçeneğiniz vardır:

* Geliştiricileri: Kullanım hello [komut istemi veya PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)
* Olmayan-Geliştiriciler: [WordPress arkadaş +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)

## <a name="how-do-i-help-make-wordpress-more-secure"></a>WordPress daha güvenli hale getirmenize nasıl yardımcı?

toolearn WordPress için önerilen güvenlik uygulamaları hakkında bkz [azure'da WordPress güvenlik için en iyi uygulamaları](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a>Toouse PHPMyAdmin çalışıyorum ve selamlama iletisine "erişim engellendi." bakın Bu nasıl giderebilirim?

Bu uygulama hizmeti örnek Hello MySQL uygulama özelliği henüz çalışmıyorsa bu sorunla karşılaşabilirsiniz. tooresolve Web sitenizi sorunu, try tooaccess hello. Bu hello uygulama MySQL işlemi dahil olmak üzere gerekli hello işlemleri başlatır. Uygulama çalışıyor, işlem Explorer'da MySQL bu mysqld.exe olun tooverify hello işlemlerde listelenir.

Uygulama MySQL çalıştığından emin olduktan sonra toouse PHPMyAdmin deneyin.

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a>Tooimport deneyin veya MySQL uygulama Veritabanım PHPMyadmin kullanarak dışarı HTTP 403 hata alın. Bu nasıl giderebilirim?

Chrome eski bir sürümünü kullanıyorsanız, bilinen hata yaşıyor. tooresolve hello sorunu, Chrome yükseltme tooa sürümü. Ayrıca Internet Explorer veya Edge'i, burada hello sorun oluşmaz gibi farklı bir tarayıcı kullanarak deneyin.

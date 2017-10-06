---
title: "Merhaba Node.js arka uç sunucusu için Mobile Apps SDK'sı ile aaaHow toowork | Microsoft Docs"
description: "Nasıl toowork ile Merhaba Node.js arka uç sunucusu SDK Azure App Service Mobile Apps için öğrenin."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a>Nasıl toouse hello Azure Mobile Apps Node.js SDK'sı
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Bu makalede ayrıntılı bilgi ve örnekler gösteren sağlar nasıl toowork Azure App Service Mobile Apps Node.js arka ucu ile.

## <a name="Introduction"></a>Giriş
Azure App Service Mobile Apps hello yetenek tooadd mobil iyileştirilmiş veri erişimi Web API tooa web uygulaması sağlar.  Hello Azure App Service Mobile Apps SDK'sı, ASP.NET ve Node.js web uygulamaları için sağlanır.  Merhaba SDK işlemleri aşağıdaki hello sağlar:

* Veri erişimi için tablo işlemleri (okuma, INSERT, Update, Delete)
* Özel API işlemleri

İki işlem kimlik doğrulaması için Kurumsal kimlik için Facebook, Twitter, Google ve Microsoft yanı sıra Azure Active Directory gibi sosyal kimlik sağlayıcıları dahil olmak üzere Azure App Service tarafından izin verilen tüm kimlik sağlayıcıları üzerinden sağlar.

Her için örnek kullanım örneği hello bulabilirsiniz [örnekler dizini github'da].

## <a name="supported-platforms"></a>Desteklenen platformlar
Hello Azure Mobile Apps düğümü SDK sürüm düğümünün ve daha sonra geçerli LTS hello destekler.  Makalenin yazıldığı sırada hello son LTS düğümü v4.5.0 sürümüdür.  Düğüm'ın diğer sürümleri çalışabilir, ancak desteklenmez.

iki veritabanı sürücüleri Hello Azure Mobile Apps düğümü SDK destekler - hello düğümü mssql sürücü SQL Azure ve yerel SQL Server örnekleri destekler.  Merhaba sqlite3 sürücü üzerinde yalnızca tek bir örneği SQLite veritabanlarını destekler.

### <a name="howto-cmdline-basicapp"></a>Nasıl yapılır: hello komut satırını kullanarak bir temel Node.js arka ucu oluşturma
Her Azure App Service Mobile uygulama Node.js arka ucu bir ExpressJS uygulamayı başlatır.  ExpressJS hello en popüler web service Node.js için kullanılabilir çerçevesidir.  Temel bir oluşturabileceğiniz [Express] şekilde uygulama:

1. Bir komut veya PowerShell penceresi projeniz için bir dizin oluşturun.

        mkdir basicapp
2. Npm init tooinitialize hello paket yapısı çalıştırın.

        cd basicapp
        npm init

    Merhaba npm init komutu soruları tooinitialize hello proje kümesi sorar.  Merhaba örnek çıktı bakın:

    ![Merhaba npm init çıktı][0]
3. Merhaba express ve azure mobile apps kitaplıkları hello npm depodan yükleyin.

        npm install --save express azure-mobile-apps
4. Bir app.js dosya tooimplement hello temel mobil sunucusu oluşturun.

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

Bu uygulama ile tek bir uç noktası mobil iyileştirilmiş Webapı oluşturur (`/tables/TodoItem`) SQL veri deposu dinamik Şeması'nı kullanarak temel kimliği doğrulanmamış erişim tooan sağlar.  İstemci Kitaplığı hızlı başlangıçlar izlemek için uygundur:

* [Android istemci hızlı başlangıç]
* [Apache Cordova istemci hızlı başlangıç]
* [iOS istemci hızlı başlangıç]
* [Windows mağazası istemci hızlı başlangıç]
* [Xamarin.iOS istemcisi hızlı başlangıç]
* [Xamarin.Android istemcisi hızlı başlangıç]
* [Xamarin.Forms istemci hızlı başlangıç]

Merhaba temel bu uygulamada hello kod bulabilirsiniz [basicapp örnek github'da].

### <a name="howto-vs2015-basicapp"></a>Nasıl yapılır: Visual Studio 2015 ile birlikte bir düğüm arka ucu oluşturma
Visual Studio 2015 uzantısı toodevelop Node.js uygulamalarını hello IDE içinde gerektirir.  toostart, yükleme hello [Visual Studio için Node.js araçları 1.1].  Merhaba Visual Studio için Node.js araçları yüklendikten sonra bir Express 4.x uygulaması oluşturun:

1. Açık hello **yeni proje** iletişim (gelen **dosya** > **yeni** > **proje...** ).
2. Genişletme **şablonları** > **JavaScript** > **Node.js**.
3. Select hello **temel Azure Node.js Express 4 uygulama**.
4. Merhaba proje adı girin.  *Tamam*’a tıklayın.

    ![Visual Studio 2015 yeni proje][1]
5. Sağ hello **npm** düğümü ve select **yüklemek yeni npm paketler...** .
6. İlk Node.js uygulamanızı oluşturma toorefresh hello npm katalog gerekebilir.  Tıklatın **yenileme** gerekiyorsa.
7. Girin *azure mobile apps* hello arama kutusuna.  Merhaba tıklatın **azure mobile apps 2.0.0** paketini ve ardından **paket yükleme**.

    ![Yeni npm paket yüklemek için][2]
8. **Kapat**’a tıklayın.
9. Açık hello *app.js* dosya hello Azure Mobile Apps SDK tooadd desteği.  Satır 6 at hello sonundaki hello kitaplığı deyimleri gerektirir, hello aşağıdaki kodu ekleyin:

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    Diğer app.use ifadeleri satırında yaklaşık 27 hello sonra hello aşağıdaki kodu ekleyin:

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    Merhaba dosyasını kaydedin.
10. Yerel olarak Merhaba uygulaması (Merhaba API http://localhost: 3000 üzerinde sunulur) çalıştırabilir veya tooAzure yayımlayın.

### <a name="create-node-backend-portal"></a>Nasıl yapılır: hello Azure portal kullanarak bir Node.js arka ucu oluşturma
Bir mobil uygulama arka uç hakkı hello oluşturabilirsiniz [Azure portal]. Aşağıdaki adımlar ya da istemci ve sunucu tarafından aşağıdaki hello birlikte oluşturmak hello ya da izleyebilirsiniz [mobil uygulama oluşturma](app-service-mobile-ios-get-started.md) Öğreticisi. Başlangıç Öğreticisi bu yönergeleri basitleştirilmiş bir sürümünü içerir ve kavram projeleri kanıtı için en iyisidir.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Merhaba edilene *başlama* dikey altında **tablo API Oluştur**, seçin **Node.js** olarak, **arka uç dilinizi**.
Merhaba kutuyu "**bu tüm site içeriğini. üzerine yazacağını kabul ediyorum**", ardından **Todoıtem tablosu oluştur**.

### <a name="download-quickstart"></a>Nasıl yapılır: indirme hello Node.js arka uç hızlı başlangıç kod projesi Git kullanma
Merhaba portalını kullanarak bir Node.js mobil uygulama arka ucu oluşturduğunuzda **Hızlı Başlangıç** dikey penceresinde bir Node.js projesi ve dağıtılan tooyour sitesi için oluşturulur. Tabloları ve API'ları ekleyin ve hello portalında hello Node.js arka ucu için kod dosyaları düzenleyin. Böylece ekleyin veya tablolar ve API'ları değiştirmek sonra Merhaba projeyi yeniden yayımlamanız çeşitli dağıtım araçları toodownload hello arka uç projesi de kullanabilirsiniz. Daha fazla bilgi için bkz: [Azure App Service Deployment Guide]. Merhaba aşağıdaki yordam bir Git deposu toodownload hello hızlı başlangıç proje kodunu kullanır.

1. Zaten yapmadıysanız Git'i, yükleyin. Merhaba adımları gerekli tooinstall Git işletim sistemleri arasında farklılık gösterir. Bkz: [yükleme Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) işletim sistemine özgü dağıtımları ve yükleme yönergeleri için.
2. Merhaba adımları [etkinleştir hello uygulama hizmeti uygulama havuzu](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git deposu hello dağıtım kullanıcı adı ve parola Not yapmadan arka uç siteniz için.
3. Mobil uygulama arka ucu için Hello dikey penceresinde hello Not **Git kopyalama URL'si** ayarı.
4. Merhaba yürütme `git clone` hello Git kopyalama URL'si, gerektiğinde, aşağıdaki örnekte olduğu gibi parolanızı girmeden kullanarak komutu:

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. Olan örnek önceki hello içinde /todolist Gözat toolocal dizin ve dosyaların proje bildirimi indirildi. Merhaba bulun `todoitem.json` hello dosyasında `/tables` dizin.  Bu dosya, tablo üzerinde izinleri tanımlar.  Ayrıca hello bulur `todoitem.js` hello aynı dosyayı CRUD işlemi hello tablosu için komut dosyası tanımlar dizin.
6. Tooproject dosyaları değişiklikleri yaptıktan sonra tooadd, yürütme ve ardından değişiklikleri toohello site karşıya yükleme komutları aşağıdaki hello yürütün:

        $ git commit -m "updated hello table script"
        $ git push origin master

    Yeni dosyalar toohello proje eklediğinizde tooexecute hello ilk gerekir `git add .` komutu.

işlemeleri yeni bir dizi toohello site gönderilen her zaman hello site yeniden yayımlanacak.

### <a name="howto-publish-to-azure"></a>Nasıl yapılır: Node.js arka uç tooAzure yayımlama
Microsoft Azure yayımlama hello Azure hizmeti için Azure App Service Mobile Apps Node.js arka ucuna birçok mekanizma sağlar.  Bunlar, Visual Studio'ya tümleşik dağıtım araçları, komut satırı araçları ve kaynak denetimine bağlı sürekli dağıtım seçenekleri kullanılarak içerir.  Bu konu hakkında daha fazla bilgi için bkz: [Azure App Service Deployment Guide].

Azure uygulama hizmeti dağıtmadan önce gözden geçirmeniz gereken Node.js uygulama için ilgili bir uzmana sahiptir:

* Nasıl çok[hello düğümü sürümü belirtin]
* Nasıl çok[düğümü modüllerini kullanma]

### <a name="howto-enable-homepage"></a>Nasıl yapılır: bir giriş sayfası, uygulamanız için etkinleştirme
Birçok uygulama web ve mobil uygulamaları bir bileşimidir ve hello ExpressJS framework toocombine iki modelleri sağlar.  Bazı durumlarda, ancak, tooonly uygulayan Mobil arabirimi isteyebilir.  Bir giriş sayfası tooensure hello uygulama hizmeti çalışır durumda olduğundan yararlı tooprovide olur.  Giriş sayfası sağlayın veya geçici bir giriş sayfası etkinleştirin.  tooenable geçici bir giriş sayfası tooinstantiate Azure Mobile Apps aşağıdaki hello kullan:

    var mobile = azureMobileApps({ homePage: true });

Yalnızca kullanılabilen bu seçenek yerel olarak geliştirirken istiyorsanız, bu ayar tooyour ekleyebilirsiniz `azureMobile.js` dosya.

## <a name="TableOperations"></a>Tablo işlemleri
Hello azure mobile apps Node.js sunucusu SDK'sı mekanizmaları tooexpose veri sağlayan bir Webapı olarak Azure SQL veritabanında depolanan tabloları.  Beş işlem sağlanır.

| İşlem | Açıklama |
| --- | --- |
| GET /tables/*tablename* |Merhaba tabloda tüm kayıtları Al |
| GET /tables/*tablename*/:id |Belirli bir kayıt hello tabloda Al |
| POST /tables/*tablename* |Merhaba tabloda bir kayıt oluşturun |
| Düzeltme eki /tables/*tablename*/:id |Güncelleştirme hello tablosundan bir kayıt |
| DELETE /tables/*tablename*/:id |Merhaba tablosundan bir kayıt silme |

Bu Webapı destekleyen [OData] ve hello tablo şemasını toosupport genişletir [çevrimdışı veri eşitlemeye].

### <a name="howto-dynamicschema"></a>Nasıl yapılır: dinamik bir şema kullanarak tabloları tanımlayın
Bir tablo kullanılabilmesi için tanımlanmalıdır.  Tabloları (burada hello sütunları hello şeması içindeki tanımlar hello Geliştirici) statik bir şema veya dinamik olarak tanımlanabilir (burada hello SDK gelen istekleri temel alan hello şema denetler). Ayrıca, hello Geliştirici Javascript kodu toohello tanımı ekleyerek hello Webapı belirli yönlerini kontrol edebilir.

En iyi uygulama, hello tabloları dizindeki Javascript dosyasında her tablo tanımlamanız sonra tables.import() yöntemi tooimport hello tabloları kullanın.  Merhaba basic uygulama genişletme, hello app.js dosya ayarlanması:

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

Merhaba tabloda tanımlayın. / tables/TodoItem.js:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

Tablolar, varsayılan olarak dinamik şema kullanın.  dinamik şema kapalı tooturn genel olarak, hello uygulama ayarı ayarlamak **MS_DynamicSchema** toofalse hello Azure portalı içinde.

Hello tam bir örnek bulabilirsiniz [Yapılacaklar örneği github'daki].

### <a name="howto-staticschema"></a>Nasıl yapılır: statik Şeması'nı kullanarak tabloları tanımlayın
Merhaba sütunları tooexpose hello Webapı aracılığıyla açıkça tanımlayabilirsiniz.  hello Azure mobile apps Node.js SDK'sı, sağladığınız çevrimdışı veri eşitlemeyi toohello listesi için gerekli ek sütunlar otomatik olarak ekler.  Örneğin, hızlı başlangıç istemci uygulamaları iki sütun içeren bir tablo gerektirir: metin (dize) ve (Boole) tamamlayın.  
Merhaba tablosu (Merhaba tabloları dizininde yer alan) hello tablo tanımı JavaScript dosyasında şu şekilde tanımlanabilir:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

Sonra tabloları statik olarak tanımlarsanız, başlangıçta hello tables.initialize() yöntemi toocreate hello veritabanı şemasını da çağırmalıdır.  Merhaba tables.initialize() yöntemi döndürür bir [Promise] böylece hello web hizmeti isteklerinin başlatılmakta hello veritabanı önce sunmuyor.

### <a name="howto-sqlexpress-setup"></a>Nasıl yapılır: yerel makinenizde geliştirme veri deposu olarak kullanmak SQL Express'i
Hello Azure Mobile Apps hello AzureMobile uygulamaları düğümü SDK hello kutu dışı veri hizmet için üç seçenek sunar: SDK, veri hello kutu dışı hizmet veren için üç seçenek sağlar:

* Kullanım hello **bellek** sürücü tooprovide bir kalıcı olmayan örnek deposuna
* Kullanım hello **mssql** sürücü tooprovide geliştirme için SQL Express veri deposu
* Kullanım hello **mssql** sürücü tooprovide üretim için bir Azure SQL veritabanı veri deposu

Hello Azure Mobile Apps Node.js SDK'sını kullanır hello [mssql Node.js paket] tooestablish ve bağlantı tooboth SQL Express ve SQL veritabanını kullan.  Bu paket, SQL Express örneği üzerinde TCP bağlantılarını etkinleştirmenizi istemektedir.

> [!TIP]
> Merhaba bellek sürücüsü eksiksiz test olanaklarının sağlamaz.  Arka ucunu yerel olarak tootest isterseniz, biz SQL Express veri deposu hello kullanımını önerilir ve mssql sürücü hello.
>
>

1. İndirme ve yükleme [Microsoft SQL Server 2014 Express].  Araçlar Edition'la hello SQL Server 2014 Express yükleme emin olun.  64-bit desteği açıkça gerektirmedikçe hello 32-bit sürümü çalışırken daha az bellek kullanır.
2. SQL Server 2014 Configuration Manager Hello çalıştırın.

   1. Merhaba genişletin **SQL Server Ağ Yapılandırması** hello sol ağaç menü düğümünde.
   2. Tıklatın **SQLEXPRESS protokolleri**.
   3. Sağ **TCP/IP'yi** seçip **etkinleştirmek**.  Tıklatın **Tamam** hello açılan iletişim kutusunda.
   4. Sağ **TCP/IP'yi** seçip **özellikleri**.
   5. Merhaba tıklatın **IP adreslerini** sekmesi.
   6. Hello bulur **IPAll** düğümü.  Merhaba, **TCP bağlantı noktası** alanına, **1433**.

          ![Configure SQL Express for TCP/IP][3]
   7. **Tamam** düğmesine tıklayın.  Tıklatın **Tamam** hello açılan iletişim kutusunda.
   8. Tıklatın **SQL Server Hizmetleri** hello sol ağaç menüsünde.
   9. Sağ **SQL Server (SQLEXPRESS)** seçip **yeniden başlatın**
   10. Merhaba SQL Server 2014 Yapılandırma Yöneticisi'ni kapatın.
3. Merhaba SQL Server 2014 Management Studio'yu çalıştırın ve tooyour yerel SQL Express örneği bağlanın

   1. Örneğinizi hello Object Explorer'ın sağ tıklatıp **özellikleri**
   2. Select hello **güvenlik** sayfası.
   3. Merhaba olun **SQL Server ve Windows kimlik doğrulaması modu** seçilir
   4. **Tamam**’a tıklayın.

          ![Configure SQL Express Authentication][4]
   5. Genişletme **güvenlik** > **oturumları** hello Nesne Gezgini içinde
   6. Sağ **oturumları** seçip **yeni oturum açma...**
   7. Bir oturum açma adı girin.  **SQL Server kimlik doğrulaması**’nı seçin.  Bir parola girin ve ardından hello girin aynı parolayı **parolayı onayla**.  Merhaba parola Windows karmaşıklık gereksinimlerini karşılaması gerekir.
   8. **Tamam**’a tıklayın.

          ![Add a new user tooSQL Express][5]
   9. Yeni oturum açma sağ tıklatıp **özellikleri**
   10. Select hello **sunucu rolleri** sayfası
   11. Merhaba kutusunu sonraki toohello denetleyin **dbcreator** sunucu rolü
   12. **Tamam**’a tıklayın.
   13. Merhaba SQL Server 2015 Management Studio'yu kapatın

Kayıt hello kullanıcı adı ve parola seçtiğiniz emin olun.  Belirli bir veritabanını gereksinimlerinize bağlı olarak tooassign ek sunucu rollerini veya izinleri gerekebilir.

Merhaba Node.js uygulaması okur hello **SQLCONNSTR_MS_TableConnectionString** hello bağlantı dizesi bu veritabanı için ortam değişkeni.  Ortamınızda bu değişkeni ayarlayabilirsiniz.  Örneğin, bu ortam değişkenini PowerShell tooset kullanabilirsiniz:

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

Bir TCP/IP bağlantısı üzerinden Hello veritabanına erişmek ve hello bağlantı için bir kullanıcı adı ve parola sağlayın.

### <a name="howto-config-localdev"></a>Nasıl yapılır: projeniz yerel geliştirme için yapılandırma
Azure Mobile Apps okur adlandırılan bir JavaScript dosyası *azureMobile.js* hello yerel dosya sistemi gelen.  Değil üretimde bu dosya tooconfigure hello Azure Mobile Apps SDK'sını kullanın - uygulaması ayarları içinde hello kullan [Azure portal] yerine.  Merhaba *azureMobile.js* dosyasına bir yapılandırma nesnesi.  Merhaba en yaygın ayarlar şunlardır:

* Veritabanı ayarları
* Tanılama günlük ayarları
* Alternatif CORS ayarları

Örnek *azureMobile.js* veritabanı ayarlarını aşağıdaki önceki hello uygulama dosyası:

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

Eklediğiniz öneririz *azureMobile.js* tooyour *.gitignore* dosya (veya diğer kaynak kodu denetimi dosyayı yoksay) hello bulutta saklanmasını tooprevent parolalar.  Her zaman üretim ayarlarını hello uygulama ayarlarında yapılandırmak [Azure portal].

### <a name="howto-appsettings"></a>: Mobil uygulamanız için uygulama ayarlarını yapılandır
Merhaba çoğu ayarlarında *azureMobile.js* dosyanız eşdeğer bir uygulama ayarı hello [Azure portal].  Liste tooconfigure aşağıdaki hello uygulama ayarlarında, uygulamanızın kullanın:

| Uygulama ayarı | *azureMobile.js* ayarı | Açıklama | Geçerli Değerler |
|:--- |:--- |:--- |:--- |
| **MS_MobileAppName** |ad |Merhaba uygulamasının Hello adı |Dize |
| **MS_MobileLoggingLevel** |Logging.level |İletileri toolog en küçük günlük düzeyi |hata, uyarı, bilgi, ayrıntılı, hata ayıklama, saçma |
| **MS_DebugMode** |Hata ayıklama |Etkinleştirme veya devre dışı bırak hata ayıklama modu |TRUE, false |
| **MS_TableSchema** |Data.Schema |SQL tablolarının varsayılan şema adı |dize (varsayılan: dbo) |
| **MS_DynamicSchema** |data.dynamicSchema |Etkinleştirme veya devre dışı bırak hata ayıklama modu |TRUE, false |
| **MS_DisableVersionHeader** |Sürüm (kümesi tooundefined) |Merhaba X-ZUMO-Server-Version üstbilgi devre dışı bırakır |TRUE, false |
| **MS_SkipVersionCheck** |skipversioncheck |Merhaba İstemcisi API sürümü denetimi devre dışı bırakır |TRUE, false |

tooset bir uygulama ayarı:

1. İçinde toohello oturum [Azure portal].
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** mobil uygulamanızın hello adını tıklatın.
3. Varsayılan olarak Hello ayarları dikey penceresini açar. ' I içermiyorsa tıklatırsanız **ayarları**.
4. Tıklatın **uygulama ayarları** hello genel menüsünde.
5. Toohello uygulama ayarları bölümüne kaydırın.
6. Uygulamanızı ayarı zaten varsa, hello değerini hello uygulama ayarı tooedit hello'ı tıklatın.
7. Uygulama ayarı yoksa hello uygulama ayarı hello anahtar kutusuna ve hello değer kutusuna hello değeri girin.
8. Tamamlandıktan sonra tıklatın **kaydetmek**.

Çoğu uygulama ayarlarını değiştirme hizmetini yeniden başlatma gerektirir.

### <a name="howto-use-sqlazure"></a>Nasıl yapılır: SQL Database üretim veri deposu olarak kullanın
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

Bir veri deposu olarak Azure SQL veritabanı kullanan tüm Azure App Service uygulama türlerine aynıdır. Henüz yapmadıysanız, bu adımları toocreate bir mobil uygulama arka ucu izleyin.

1. İçinde toohello oturum [Azure portal].
2. Merhaba hello pencerenin sol üst, hello tıklatın **+ yeni** düğmesi > **Web + mobil** > **mobil uygulama**, mobil uygulama arka ucu için bir ad sağlayın.
3. Merhaba, **kaynak grubu** kutusunda, aynı ad hello uygulamanızı girin.
4. Merhaba varsayılan uygulama hizmeti planı seçilir.  Uygulama hizmeti planınızı toochange isterseniz, uygulama hizmeti planı hello tıklayarak bunu yapabilirsiniz > **+ Yeni Oluştur**.  Merhaba yeni uygulama hizmeti planının adı sağlayın ve uygun bir konum seçin.  Merhaba fiyatlandırma Katmanı'nı tıklatın ve hello hizmeti için uygun bir fiyatlandırma katmanı seçin. Seçin **tüm görüntüle** daha seçenekleri gibi fiyatlandırma tooview **serbest** ve **paylaşılan**.  Fiyatlandırma katmanı seçildiğinde hello tıklatın **seçin** düğmesi.  Merhaba edilene **uygulama hizmeti planı** dikey penceresinde tıklatın **Tamam**.
5. **Oluştur**'a tıklayın. Bir mobil uygulama arka ucu sağlama birkaç dakika sürebilir.  Merhaba mobil uygulama arka ucu sağlandıktan sonra hello portal hello açar **ayarları** dikey penceresinde hello mobil uygulama arka ucu için.

Merhaba mobil uygulama arka ucu oluşturulduktan sonra tooeither seçebilirsiniz varolan bir SQL veritabanı tooyour mobil uygulama arka bağlayın veya yeni bir SQL veritabanı oluşturun.  Bu bölümde, bir SQL veritabanı oluşturun.

> [!NOTE]
> Bir veritabanı hello zaten varsa hello mobil uygulama arka ucu ile aynı konumda, bunun yerine seçebilirsiniz **varolan veritabanını kullan** sonra bu veritabanını seçin. bir veritabanı farklı bir konumda Hello kullanımını daha yüksek gecikme nedeniyle önerilmez.
>
>

1. Merhaba yeni mobil uygulama arka ucunda tıklatın **ayarları** > **mobil uygulama** > **veri** > **+ Ekle**.
2. Merhaba, **veri bağlantısı Ekle** dikey penceresinde tıklatın **SQL veritabanı - gerekli ayarları Yapılandır** > **yeni bir veritabanı oluşturmak**.  Hello Hello hello yeni veritabanının adını girin **adı** alan.
3. Tıklatın **Server**.  Merhaba, **yeni sunucu** dikey penceresinde hello bir benzersiz sunucu adı girin **sunucu adı** alan ve uygun bir sağlamak **Sunucu Yöneticisi oturum açma** ve **parola**.  Olun **izin azure Hizmetleri tooaccess sunucusu** denetlenir.  **Tamam** düğmesine tıklayın.

    ![Bir Azure SQL veritabanı oluşturma][6]
4. Merhaba üzerinde **yeni veritabanı** dikey penceresinde tıklatın **Tamam**.
5. Merhaba üzerinde geri **veri bağlantısı Ekle** dikey penceresinde, select **bağlantı dizesi**, hello oturum açma ve hello veritabanı oluşturulurken sağlanan parola girin.  Varolan bir veritabanını kullanıyorsanız, bu veritabanı için hello oturum açma kimlik bilgilerini sağlayın.  Girilen sonra tıklayın **Tamam**.
6. Merhaba üzerinde geri **veri bağlantısı Ekle** dikey penceresinde tekrar tıklatın **Tamam** toocreate hello veritabanı.

<!--- END OF ALTERNATE INCLUDE -->

Merhaba veritabanı oluşturulması birkaç dakika sürebilir.  Kullanım hello **bildirimleri** alanı toomonitor hello hello dağıtımının ilerlemesini.  Merhaba veritabanı başarıyla dağıtıldığını kadar ilerleme değil.  Başarılı bir şekilde dağıtıldığında, bir bağlantı dizesi hello SQL veritabanı örneğinde mobil arka uç uygulama ayarları için oluşturulur.  Bu uygulama ayarını hello görebilirsiniz **ayarları** > **uygulama ayarları** > **bağlantı dizeleri**.

### <a name="howto-tables-auth"></a>Nasıl yapılır: kimlik doğrulaması için erişim tootables gerektir
Merhaba tabloları uç noktası ile App Service kimlik doğrulaması toouse isterseniz, App Service kimlik doğrulaması hello yapılandırmalısınız [Azure portal] ilk.  Bir Azure uygulama hizmetinde kimlik doğrulaması yapılandırma hakkında daha fazla ayrıntı gözden geçirmek için hello Yapılandırma Kılavuzu hello kimlik sağlayıcısı için toouse düşündüğünüz:

* [Nasıl tooconfigure Azure Active Directory kimlik doğrulaması]
* [Nasıl tooconfigure Facebook kimlik doğrulaması]
* [Nasıl tooconfigure Google kimlik doğrulama]
* [Nasıl tooconfigure Microsoft Authentication]
* [Nasıl tooconfigure Twitter kimlik doğrulaması]

Her tablo kullanılan toocontrol erişim toohello tablo olabilir bir erişim özelliğine sahiptir.  Aşağıdaki örnek hello statik olarak tanımlanmış bir tablo ile kimlik doğrulaması gerekli gösterir.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Merhaba erişim özellik üç değerden birini alabilir

* *Anonim* Merhaba istemci uygulaması tooread veri kimlik doğrulaması olmadan izin verildiğini gösterir
* *Kimliği doğrulanmış* Merhaba istemci uygulaması geçerli bir kimlik doğrulama belirteci hello isteğiyle göndermelidir gösterir
* *devre dışı* Bu tablo şu anda devre dışı olduğunu gösterir

Merhaba erişim özelliği tanımsız ise, kimliği doğrulanmamış erişim verilir.

### <a name="howto-tables-getidentity"></a>Nasıl yapılır: tablolarınızı ile kimlik doğrulaması talep kullanın
Kimlik doğrulama ayarlarken, istenen çeşitli talep ayarlayabilirsiniz.  Bu talep hello normalde kullanılamaz `context.user` nesnesi.  Ancak, bunlar hello kullanılarak alınabilir `context.user.getIdentity()` yöntemi.  Merhaba `getIdentity()` yöntemi tooan nesne çözümler Promise döndürür.  Merhaba nesne kimlik doğrulama yöntemi (facebook, google, twitter, microsoftaccount veya aad) anahtarlanır.

Örneğin, Microsoft Account kimlik doğrulaması ve istek hello e-posta adresleri talep ayarlama, aşağıdaki tablo denetleyici hello ile Merhaba e-posta adresi toohello kaydı ekleyebilirsiniz:

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

toosee hangi talepleri kullanılabilen, bir web tarayıcısı tooview hello kullan `/.auth/me` uç noktası, sitenizin.

### <a name="howto-tables-disabled"></a>Nasıl yapılır: devre dışı bırak erişim toospecific tablo işlemleri
Merhaba tablosundaki toplama tooappearing içinde kullanılan toocontrol tek tek işlemleri hello erişim özelliği olabilir.  Dört işlemleri şunlardır:

* *Okuma* hello tablosundaki hello RESTful alma işlemi
* *INSERT* hello tablo bir hello RESTful POST işlem
* *Güncelleştirme* hello tablosundaki hello RESTful düzeltme eki işlemi
* *silme* hello tablosundaki hello RESTful silme işlemi

Örneğin, bir salt okunur kimliği doğrulanmamış tablo tooprovide isteyebilir:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a>Nasıl yapılır: Tablo işlemleriyle kullanılan hello sorgu Ayarla
Bir ortak tablo işlemleri için tooprovide hello veri kısıtlanmış bir görünümü gereksinimdir.  Örneğin, yalnızca okuma veya kendi kayıtlarını güncelleştirmek gibi kullanıcı kimliği ile Merhaba etiketli bir tablo kimliğinin sağlayabilir.  Aşağıdaki tablo tanımı hello bu işlevleri sağlar:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

Normalde bir sorgu yürütme işlemleri bulunduğu yerle ayarlayabilirsiniz bir sorgu özelliğe sahip yan tümcesi. Merhaba sorgu özelliği bir [QueryJS] diğer bir deyişle kullanılan tooconvert veri arka uç hello bir OData sorgu toosomething işlenebilecek nesne.  Bir harita (gibi bir önceki hello) basit eşitlik durumlar için kullanılabilir. Belirli SQL yan tümceleri de ekleyebilirsiniz:

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a>Nasıl yapılır: bir tablo üzerinde geçici silme Yapılandır
Geçici silme kayıtları silmez.  Bunun yerine, bunları silinmiş hello sütun tootrue ayarlayarak hello veritabanında silindi olarak işaretler.  Merhaba mobil istemci SDK'sı IncludeDeleted() kullanmadıkça hello Azure Mobile Apps SDK sonuçlarından geçici olarak silinen kayıtları otomatik olarak kaldırır.  Tablo yazılımla için silme, tooconfigure ayarlamak hello `softDelete` hello tablo tanımı dosyasında özellik:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Kayıt - bir istemci uygulamasından bir Webjob'un Azure işlevi aracılığıyla veya özel bir API aracılığıyla ya da Temizleme için bir mekanizma oluşturmanız gerekir.

### <a name="howto-tables-seeding"></a>Nasıl yapılır: veri veritabanınızla çekirdek
Yeni bir uygulama oluştururken, veri içeren bir tablo tooseed isteyebilir.  Bu gibi hello tablo tanımı JavaScript dosyası içinde yapılabilir:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Merhaba tablo hello Azure Mobile Apps SDK'sı tarafından oluşturulduğunda verileri dengeli yalnızca yapılır.  Hello tablo içinde hello veritabanı zaten varsa, hiçbir veri hello tabloya eklenen.  Dinamik şema açıksa, şema dağıtılan hello verileri algılanır.

Merhaba açıkça çağırın öneririz `tables.initialize()` hello hizmeti çalışmaya başladığında yöntemi toocreate hello tablo.

### <a name="Swagger"></a>Nasıl yapılır: Swagger desteğini etkinleştir
Azure App Service Mobile Apps ile yerleşik gelen [Swagger] destekler.  tooenable Swagger desteği, bir bağımlılık olarak ilk hello swagger kullanıcı arabirimini yükleyin:

    npm install --save swagger-ui

Yüklendikten sonra Swagger destek hello Azure Mobile Apps oluşturucuda etkinleştirebilirsiniz:

    var mobile = azureMobileApps({ swagger: true });

Büyük olasılıkla yalnızca istediğiniz tooenable geliştirme sürümlerindeki Swagger desteği.  Bunu yararlanarak yapmak `NODE_ENV` uygulama ayarı:

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

Merhaba swagger uç nokta http:// bulunduğu*yoursite*.azurewebsites.net/swagger.  Merhaba Swagger kullanıcı arabirimini hello aracılığıyla erişebilirsiniz `/swagger/ui` uç noktası.  Tüm uygulamanız toorequire kimlik doğrulamasını seçerseniz, Swagger bir hata oluşturur.  En iyi sonuçlar için kimliği doğrulanmamış tooallow istekleri üzerinden hello Azure App Service kimlik doğrulaması seçin / yetkilendirme ayarları, ardından hello kullanarak kimlik doğrulaması denetimi `table.access` özelliği.

Merhaba Swagger seçeneği tooyour de ekleyebilirsiniz `azureMobile.js` yalnızca Swagger desteği yerel olarak geliştirirken istiyorsanız, dosya.

## <a name="a-namepushpush-notifications"></a><a name="push">Anında iletme bildirimleri
Azure Notification Hubs tooenable ile Mobile Apps, tüm ana platformlarda hedeflenen toosend anında iletme bildirimleri toomillions aygıtların tümleştirir. Bildirim hub'ları kullanarak gönderimi gönderebilir bildirimleri tooiOS, Android ve Windows cihazları. Bildirim hub'ları tüm hakkında daha fazla ile yapabilir toolearn bkz [Notification Hubs'a genel bakış](../notification-hubs/notification-hubs-push-notification-overview.md).

### </a><a name="send-push"></a>Nasıl yapılır: anında iletme bildirimleri gönderme
koddan hello nasıl toouse hello itme nesne toosend yayın anında bildirim tooregistered iOS cihazları gösterir:

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Hello istemciden bir şablon İtme kaydı oluşturarak, bunun yerine bir şablon anında iletme iletisi toodevices tüm desteklenen platformlarda gönderebilirsiniz. kodun gösterdiği nasıl aşağıdaki hello toosend bir şablon bildirim:

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <a name="push-user"></a>Nasıl yapılır: gönderme anında iletme bildirimleri tooan etiketleri kullanarak kullanıcı kimlik doğrulaması
Kimliği doğrulanmış bir kullanıcı için anında iletme bildirimleri kaydolduğunda, bir kullanıcı kimliği etiketi toohello kayıt otomatik olarak eklenir. Bu etiketi kullanarak anında iletme bildirimleri tooall aygıtları belirli bir kullanıcı tarafından kaydedilen gönderebilirsiniz. Merhaba aşağıdaki kod hello hello isteği yapan kullanıcı SID'si alır ve bu kullanıcı için bir şablon anında iletme bildirimi tooevery aygıt kaydı gönderir:

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Kimliği doğrulanmış bir istemci anında iletme bildirimleri için kaydolurken kayıt denemeden önce kimlik doğrulamasının tam olduğundan emin olun.

## <a name="CustomAPI"></a>Özel API'leri
### <a name="howto-customapi-basic"></a>Nasıl yapılır: özel bir API tanımlayın
Ayrıca toohello API hello /tables uç noktası aracılığıyla verilere, Azure Mobile Apps özel API kapsamı sağlayabilir.  Özel API'leri benzer bir şekilde toohello tablo tanımları tanımlanır ve tüm erişebilir hello aynı olanakları, kimlik doğrulaması dahil.

App Service kimlik doğrulaması özel API ile toouse isterseniz, App Service kimlik doğrulaması hello yapılandırmalısınız [Azure portal] ilk.  Bir Azure uygulama hizmetinde kimlik doğrulaması yapılandırma hakkında daha fazla ayrıntı gözden geçirmek için hello Yapılandırma Kılavuzu hello kimlik sağlayıcısı için toouse düşündüğünüz:

* [Nasıl tooconfigure Azure Active Directory kimlik doğrulaması]
* [Nasıl tooconfigure Facebook kimlik doğrulaması]
* [Nasıl tooconfigure Google kimlik doğrulama]
* [Nasıl tooconfigure Microsoft Authentication]
* [Nasıl tooconfigure Twitter kimlik doğrulaması]

Özel API'leri çok tanımlanan şekilde tabloları API hello aynı hello.

1. Oluşturma bir **API** dizini
2. Hello bir API tanımı JavaScript dosyası oluşturun **API** dizin.
3. Kullanım hello alma yöntemini tooimport hello **API** dizin.

Daha önce kullandık hello basic uygulama örneği temel alarak hello prototip API tanımı aşağıda verilmiştir.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

Bir örnek hello kullanarak hello sunucu tarihi döndürür API atalım *Date.now()* yöntemi.  Merhaba api/date.js dosya şöyledir:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

Her bir parametreyi hello standart RESTful fiiller - GET, POST, düzeltme eki veya DELETE biridir.  Merhaba yöntemdir standart bir [ExpressJS Ara] gerekli hello çıkış gönderir işlevi.

### <a name="howto-customapi-auth"></a>Nasıl yapılır: erişim tooa özel API için kimlik doğrulaması gerektirir
Azure Mobile Apps SDK'sı hello kimlik doğrulaması uygulayan hello tabloları endpoint ve özel API'leri ile aynı şekilde.  Merhaba önceki bölümde geliştirilmiş kimlik doğrulaması toohello API eklemek için Ekle bir **erişim** özelliği:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

Ayrıca, kimlik doğrulama belirli işlemleri belirtebilirsiniz:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

Merhaba hello tabloları uç noktası için kullanılan aynı belirteci kimlik doğrulaması gerektiren özel API'leri için kullanılması gerekir.

### <a name="howto-customapi-auth"></a>Nasıl yapılır: işlemek büyük dosya yüklemeleri
Azure Mobile Apps SDK'sı hello kullanır [gövde ayrıştırıcı Ara](https://github.com/expressjs/body-parser) tooaccept ve gönderiminiz gövdesi içeriği kodunu çözer.  Gövde ayrıştırıcı tooaccept büyük dosya yüklemeleriyle önceden yapılandırabilirsiniz:

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

Merhaba, Aktarımdan önce kodlanmış base-64 dosyasıdır.  Bu hello gerçek karşıya yükleme hello boyutu artar (ve bu nedenle boyut için hesap hello).

### <a name="howto-customapi-sql"></a>Nasıl yapılır: özel SQL deyimlerini yürütmek
Hello Azure Mobile Apps SDK'sı sağlar erişim toohello tooexecute izin vererek tüm içerik hello istek nesnesi aracılığıyla parametreli SQL deyimleri toohello tanımlanmış veri sağlayıcısı kolayca:

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <a name="Debugging"></a>Hata ayıklama, kolay tablolar ve kolay API'leri
### <a name="howto-diagnostic-logs"></a>Nasıl yapılır: hata ayıklama, tanılama ve Azure Mobile apps sorunlarını giderme
Hello Azure App Service birkaç hata ayıklama ve sorun giderme tekniklerini Node.js uygulamaları için sağlar.
Node.js mobil arka uç sorun giderme makaleleri tooget aşağıdaki toohello bakın:

* [Bir Azure uygulama hizmeti izleme]
* [Azure uygulama hizmetinde tanılama günlük kaydını etkinleştir]
* [Visual Studio'da bir Azure uygulama hizmeti sorunlarını giderme]

Node.js uygulamalarını erişiminiz tanılama günlük araçları tooa çeşitli.  Dahili olarak, Azure Mobile Apps Node.js SDK'sı hello [Winston] tanılama günlük için.  Günlüğü otomatik olarak etkin hata ayıklama modunu etkinleştirme veya ayarı hello tarafından **MS_DebugMode** uygulama ayarı tootrue hello içinde [Azure portal]. Merhaba tanılama günlüklerini hello üzerinde oluşturulan günlüklerin görünür [Azure portal].

### <a name="in-portal-editing"></a><a name="work-easy-tables"></a>Nasıl yapılır: hello Azure portalında kolay tabloları ile çalışma
Merhaba portalında kolay tabloları oluşturma ve tabloları doğrudan hello portalında çalışmak sağlar. Tablo işlemleri hello App Service Düzenleyicisi'ni kullanarak da düzenleyebilirsiniz.

Tıkladığınızda **kolay tabloları** arka uç site ayarlarınızda ekleyebilir, değiştirebilir veya bir tablo silme. Merhaba tablodaki verileri de görebilirsiniz.

![Kolay tablolarla çalışma](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

Merhaba aşağıdaki komutlar hello komut çubuğunda bir tablo için kullanılabilir:

* **İzinleri Değiştir** - hello Okuma izinlerini değiştirmek, Ekle, Güncelleştir ve hello tablosunda silme işlemleri.
  Seçeneklerdir tooallow anonim erişim, toorequire kimlik doğrulaması veya toodisable tüm erişim toohello işlemi.
* **Komut dosyasını Düzenle** -hello komut dosyası Merhaba tablonun hello App Service Düzenleyicisi açılır.
* **Şemayı yönetmek** - ekleme veya sütunları silin veya hello tablosu dizini değiştirin.
* **Düz tablo** -var olan bir tabloyu kesen değişmeden tüm veri satırları silme ancak hello şema bırakarak olabilir.
* **Satırları Sil** -tek tek veri satırı silin.
* **Akış günlükleri Görünüm** -günlük hizmeti siteniz için akış toohello bağlanır.

### <a name="work-easy-apis"></a>Nasıl yapılır: hello Azure portalında kolay API'leri ile çalışma
Merhaba portalında kolay API'leri, oluşturma ve özel API'lerini doğrudan hello portalında çalışmak olanak tanır. API komut dosyalarını hello App Service Düzenleyicisi'ni kullanarak düzenleyebilirsiniz.

Tıkladığınızda **kolay API'leri** arka uç site ayarlarınızda ekleyebilir, değiştirebilir veya özel bir API uç noktasını silmek.

![Kolay API'leri ile çalışma](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

Merhaba Portalı'nda belirli bir HTTP eylemi hello erişim izinlerini değiştirmek, hello API komut dosyası App Service Düzenleyicisi'ni düzenleyin veya hello akış günlükleri görüntüleyin.

### <a name="online-editor"></a>Nasıl yapılır: Düzenle hello App Service Düzenleyicisi kodda
Hello Azure portal hello proje tooyour yerel bilgisayar yüklemeye gerek kalmadan Node.js arka uç komut dosyalarınızı hello App Service Düzenleyicisi'ni düzenlemenizi sağlar. Merhaba çevrimiçi düzenleyicisinde tooedit komut dosyaları:

1. Mobil uygulama arka uç dikey penceresinde tıklayın **tüm ayarları** > ya da **kolay tablolar** veya **kolay API'leri**, bir tablo veya API'ı tıklatın **Düzenle betik**. Merhaba komut dosyası hello App Service Düzenleyicisi açılır.

    ![Uygulama hizmeti Düzenleyicisi](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. Değişiklikleri toohello kodu dosyanızda hello çevrimiçi düzenleyicisinde olun. Siz yazarken değişiklikler otomatik olarak kaydedilir.

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Android istemci hızlı başlangıç]: app-service-mobile-android-get-started.md
[Apache Cordova istemci hızlı başlangıç]: app-service-mobile-cordova-get-started.md
[iOS istemci hızlı başlangıç]: app-service-mobile-ios-get-started.md
[Xamarin.iOS istemcisi hızlı başlangıç]: app-service-mobile-xamarin-ios-get-started.md
[Xamarin.Android istemcisi hızlı başlangıç]: app-service-mobile-xamarin-android-get-started.md
[Xamarin.Forms istemci hızlı başlangıç]: app-service-mobile-xamarin-forms-get-started.md
[Windows mağazası istemci hızlı başlangıç]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[çevrimdışı veri eşitlemeye]: app-service-mobile-offline-data-sync.md
[Nasıl tooconfigure Azure Active Directory kimlik doğrulaması]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Nasıl tooconfigure Facebook kimlik doğrulaması]: app-service-mobile-how-to-configure-facebook-authentication.md
[Nasıl tooconfigure Google kimlik doğrulama]: app-service-mobile-how-to-configure-google-authentication.md
[Nasıl tooconfigure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Nasıl tooconfigure Twitter kimlik doğrulaması]: app-service-mobile-how-to-configure-twitter-authentication.md
[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md
[Bir Azure uygulama hizmeti izleme]: ../app-service-web/web-sites-monitor.md
[Azure uygulama hizmetinde tanılama günlük kaydını etkinleştir]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Visual Studio'da bir Azure uygulama hizmeti sorunlarını giderme]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[hello düğümü sürümü belirtin]: ../nodejs-specify-node-version-azure-apps.md
[düğümü modüllerini kullanma]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[Azure portal]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp örnek github'da]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[Yapılacaklar örneği github'daki]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[örnekler dizini github'da]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Visual Studio için Node.js araçları 1.1]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js paket]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Ara]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston

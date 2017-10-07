---
title: Mobile Services tooAzure - App Service Node.js gelen aaaUpgrade
description: "Nasıl tooeasily yükseltme Mobile Services uygulama tooan mobil uygulama hizmeti öğrenin"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a>Varolan Node.js Azure mobil hizmeti tooApp hizmet yükseltme
App Service Mobile Microsoft Azure kullanarak bir yeni yolu toobuild mobil uygulamaları ' dir. toolearn daha, fazla [Mobile Apps nedir?].

Bu konuda açıklanmaktadır nasıl Azure Mobile Services tooa varolan Node.js arka uç uygulamasından tooupgrade yeni App Service Mobile Apps. Bu yükseltme gerçekleştirirken mevcut Mobile Services uygulamanızı toooperate devam edebilirsiniz.  Tooupgrade bir Node.js arka uç uygulaması gereksinim duyarsanız, çok başvurun[.NET Mobile Services yükseltme](app-service-mobile-net-upgrading-from-mobile-services.md).

Bir mobil arka uç yükseltilmiş tooAzure uygulama hizmeti olduğunda, uygulama hizmeti özellikler ve öğeler faturalandırılır çok according erişim tooall sahip[uygulama hizmeti fiyatlandırma], fiyatlandırma değil Mobile Services.

## <a name="migrate-vs-upgrade"></a>Yükseltme geçirme
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Önerilir Bu, [bir geçiş gerçekleştirmek](app-service-mobile-migrating-from-mobile-services.md) yükseltme geçmeden önce. Bu şekilde, her iki sürümü, uygulamanızın koyabilirsiniz aynı App Service planı hello ve ek bir maliyet doğurur.
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>Mobile Apps Node.js sunucusu SDK yenilikleri
Yeni toohello yükseltme [Mobile Apps SDK'sı](https://www.npmjs.com/package/azure-mobile-apps) iyileştirmeler de dahil olmak üzere birçok sağlar:

* Merhaba üzerinde temel [Express framework](http://expressjs.com/en/index.html), hello yeni bir düğüm SDK hafif ve yeni düğümü sürümleriyle gelen yukarı tookeep tasarlanmıştır. Express ara yazılımını ile Merhaba uygulama davranışını özelleştirebilirsiniz.
* Önemli performans geliştirmeleri toohello Mobile Services SDK'sı karşılaştırılan.
* Bir Web sitesi ile birlikte mobil arka şimdi barındırabilir; benzer şekilde, bu kolay tooadd hello Azure Mobile SDK tooany varolan express.v4 uygulamasıdır.
* Platformlar arası ve yerel geliştirme için oluşturulan hello Mobile Apps SDK'sı geliştirilen ve yerel olarak Windows, Linux ve OSX platformlarda çalıştırmak kullanabilirsiniz. Kolay toouse ortak düğüm geliştirme teknikleri çalışıyor gibi sunulmuştur [Mocha](https://mochajs.org/) önceki toodeployment sınar.

## <a name="overview"></a>Temel yükseltmeye genel bakış
Azure App Service'te bir Node.js arka ucu yükseltme sırasında tooaid uyumluluk paketi sağlamıştır.  Yükseltmeden sonra dağıtılan tooa yeni uygulama hizmeti site olabilir bir niew sitesi olur.

Merhaba Mobile Services istemci SDK'ları olan **değil** hello yeni mobil uygulamalar sunucusu SDK ile uyumlu. Sipariş tooprovide kesintisiz hizmet devamlılığı uygulamanız için, değişiklikleri tooa site şu anda yayımlanan istemciler hizmet veren yayınlamalıdır değil. Bunun yerine, yinelenen hizmet veren yeni bir mobil uygulama oluşturmanız gerekir. Bu uygulama koyabilirsiniz hello üzerinde ek finansal masraf tooavoid aynı uygulama hizmeti planı.

Merhaba uygulaması iki sürümü sonra gerekir: kalır bir hello aynı görevi görür yayımlanan uygulamalar hello joker ve diğeri, ardından yükseltin ve yeni bir istemci ile hedef sürüm. Taşıma ve kodunuzu test etmek, hızı, ancak yaptığınız tüm hata düzeltmeleri uygulanan tooboth alma emin olmanız gerekir. Düşündüğünüz sonra joker istemci uygulamalarında istenen sayısını toohello en son sürümünü güncelleştirilen, istediğiniz hello özgün geçirilen uygulama silebilirsiniz. Mobil uygulamanızın aynı uygulama hizmeti planı hello barındırılıyorsa, tüm ek para ücrete neden değil.

Merhaba tam anahat hello yükseltme işlemi için aşağıdaki gibidir:

1. Mevcut (geçirilen) Azure mobil hizmetiniz indirin.
2. Merhaba proje tooan Azure mobil uygulaması Dönüştür hello uyumluluk paketini kullanarak.
3. Farkları (örneğin, kimlik doğrulama ayarları) düzeltin.
4. Dönüştürülmüş Azure mobil uygulama projesi tooa dağıtmak yeni uygulama hizmeti.
5. Yeni bir sürüm kullanmak yeni mobil uygulama hello istemci uygulamanızın serbest bırakın.
6. (İsteğe bağlı) Özgün geçirilen mobil hizmet uygulamanızı silin.

Özgün geçirilen mobil hizmette herhangi bir trafik görmüyorum silme ortaya çıkabilir.

## <a name="install-npm-package"></a>Merhaba Önkoşulları Yükleme
Yerel makinenizde [Node] yüklemeniz gerekir.  Merhaba uyumluluğu paketi de yüklemeniz gerekir.  Düğüm yüklendikten sonra hello bir yeni cmd veya PowerShell komut isteminde aşağıdaki komutu çalıştırabilirsiniz:

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a>Azure mobil hizmetler komut dosyalarınız alın
* İçinde toohello oturum [Azure Portal].
* Kullanarak **tüm kaynakları** veya **uygulama hizmetleri**, Mobile Services sitenizi bulun.
* Merhaba sitede tıklayın **Araçları** -> **Kudu** -> **Git** tooopen hello Kudu site.
* Tıklayın **hata ayıklama Konsolu'nda** -> **PowerShell** tooopen hello Hata Ayıkla Konsolu.
* Çok gidin`site/wwwroot/App_Data/config` her bir dizinin sırayla tıklayarak
* Merhaba indirme simgesi sonraki toohello tıklatıldığında `scripts` dizin.

Bu ZIP biçiminde hello komut dosyaları indirir.  Yerel makinenizde yeni bir dizin oluşturun ve hello paket `scripts.ZIP` hello dizini içindeki dosya.  Bu oluşturacak bir `scripts` dizin.

## <a name="scaffold-app"></a>İskele hello yeni Azure Mobile Apps arka uç
Merhaba betikleri dizinini içeren hello dizininden komutu aşağıdaki hello çalıştırın:

```scaffold-mobile-app scripts out```

Bu kurulmuş bir Azure Mobile Apps arka uç hello oluşturacak `out` dizin.  Gerekli değildir, ancak bir fikir toocheck hello olduğu `out` tercih ettiğiniz bir kaynak kod havuzunda dizin.

## <a name="deploy-ama-app"></a>Azure Mobile Apps arka dağıtma
Dağıtım sırasında toodo hello aşağıdaki gerekir:

1. Yeni bir mobil uygulaması hello oluşturma [Azure Portal].
2. Merhaba çalıştırmak `createViews.sql` bağlı veritabanınızı komut.
3. Bağlantılı tooyour mobil hizmeti tooyour bağlantı hello veritabanını yeni uygulama hizmeti.
4. Diğer kaynaklar (örneğin, bildirim hub'ları) toohello bağlantı yeni uygulama hizmeti.
5. Oluşturulan hello kod tooyour yeni site dağıtın.

### <a name="create-a-new-mobile-app"></a>Yeni bir mobil uygulaması oluşturma
1. Merhaba oturum açma [Azure Portal].
2. **+YENİ** > **Web + Mobil** > **Mobil Uygulama**’ya tıklayıp Mobile Uygulama arka ucu için bir ad verin.
3. Hello için **kaynak grubu**, varolan bir kaynak grubu seçin veya yeni bir tane oluşturun (kullanarak Merhaba, uygulamanızın adıyla aynı.)

    Başka bir App Service planı seçin veya yeni bir tane oluşturun. Uygulama Hizmetleri planları ve nasıl toocreate farklı fiyatlandırma içinde yeni bir plan katmanı ve tercih ettiğiniz konumda bkz hakkında daha fazla bilgi için [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Hello için **uygulama hizmeti planı**, hello varsayılan plan (Merhaba içinde [standart katmanı](https://azure.microsoft.com/pricing/details/app-service/)) seçilidir. Aynı zamanda başka bir plan da seçebilir veya [yeni bir tane oluşturabilirsiniz](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). Merhaba uygulama hizmeti planının ayarları belirlemek hello [konumu, özellikleri, maliyeti ve işlem kaynaklarını](https://azure.microsoft.com/pricing/details/app-service/) uygulamanızla ilişkili.

    Merhaba planla ilgili kararı verdikten sonra tıklayın **oluşturma**. Merhaba mobil uygulama arka ucu oluşturur.

### <a name="run-createviewssql"></a>CreateViews.SQL Çalıştır
Merhaba kurulmuş uygulama adlı bir dosyayı içeren `createViews.sql`.  Bu komut dosyasını hedef veritabanında yürütülmelidir.  Merhaba hello hedef veritabanı için bağlantı dizesini elde edilebilir geçirilen mobil hizmetinizden hello gelen **ayarları** altında dikey **bağlantı dizeleri**.  Bu adlı `MS_TableConnectionString`.

Bu komut dosyasından SQL Server Management Studio veya Visual Studio içinde çalıştırabilirsiniz.

### <a name="link-hello-database-tooyour-app-service"></a>Bağlantı hello veritabanı tooyour uygulama hizmeti
Merhaba varolan veritabanı tooyour uygulama hizmeti bağlantı:

* Merhaba, [Azure Portal], uygulama hizmetiniz açın.
* Seçin **tüm ayarları** -> **veri bağlantıları**.
* Tıklayın **+ Ekle**.
* Hello açılır, seçin **SQL veritabanı**
* Altında **SQL veritabanı**mevcut veritabanını seçin, ardından tıklayın **seçin**.
* Altında **bağlantı dizesi**, hello veritabanı için hello kullanıcı adını ve parolasını girin, ardından tıklayın **Tamam**.
* Merhaba, **veri bağlantıları ekleme** dikey penceresinde, tıklatıldığında **Tamam**.

Merhaba kullanıcı adı ve parola geçirilen mobil hizmetinizi hello hedef veritabanı için bağlantı dizesi hello görüntüleyerek bulunabilir.

### <a name="set-up-authentication"></a>Kimlik doğrulamasını ayarlama
Azure Mobile Apps tooconfigure Azure Active Directory, Facebook, Google, Microsoft ve Twitter kimlik doğrulaması hello hizmet içinde verir.  Özel kimlik doğrulama ayrı olarak geliştirilen toobe gerekir.  Hello başvuran [kimlik doğrulaması kavramlarını] belgelerine ve [kimlik doğrulaması Hızlı Başlangıç] daha fazla bilgi için.  

## <a name="updating-clients"></a>Mobil istemcilerin güncelleştir
İşletimsel bir mobil uygulama arka ucu olduktan sonra hangi içereceği tükettiği istemci uygulamanızı yeni bir sürümünü çalışabilirsiniz. Mobile Apps istemci SDK'in hello yeni bir sürümünü de içerir ve benzer toohello sunucu yükseltme yukarıdaki, tüm başvurular toohello Mobile Services SDK'ları önce tooremove gerekir Mobile Apps sürümler yükleme.

Merhaba ana değişiklikleri hello sürümleri arasında hello oluşturucular artık bir uygulama anahtarı iste biridir.
Artık yalnızca mobil uygulamanızın hello URL'de geçirdiğiniz. Örneğin, hello .NET istemcilerde hello `MobileServiceClient` Oluşturucusu olan şimdi:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

Yükleme hakkında bilgi edinebilirsiniz yeni SDK'ları hello ve aşağıdaki hello bağlantıları üzerinden hello yeni yapısını kullanarak:

* [Android 2.2 veya sonraki sürümü](app-service-mobile-android-how-to-use-client-library.md)
* [iOS sürüm 3.0.0 veya daha yenisi](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) sürüm 2.0.0 veya daha yenisi](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova sürüm 2.0 veya üstü](app-service-mobile-cordova-how-to-use-client-library.md)

Olmuştur gibi bazı değişiklikler vardır de uygulamanız anında iletme bildirimleri kullanın, her platform için belirli kayıt yönergeleri hello Not yapıyorsa.

Merhaba yeni istemci sürümü hazır olduğunda, yükseltilen sunucu projenizi karşı deneyin. Çalışır durumda olduğunu doğrulandıktan sonra uygulama toocustomers yeni bir sürümü serbest bırakabilirsiniz. Sonuç olarak, müşterilerinizin bu güncelleştirmeler bir fırsat tooreceive beklendiğinden sonra hello Mobile Services sürümü, uygulamanızın silebilirsiniz. Bu noktada, tamamen tooan mobil uygulama hizmeti yükselttikten hello en son mobil uygulamalar sunucusu SDK kullanarak.

<!-- URLs. -->

[Azure portal]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[Mobile Apps nedir?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[uygulama hizmeti fiyatlandırma]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[kimlik doğrulaması kavramlarını]: ../app-service/app-service-authentication-overview.md
[kimlik doğrulaması Hızlı Başlangıç]: app-service-mobile-auth.md

[Azure Portal]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston

---
title: App Service Mobile Services tooAzure gelen aaaUpgrade
description: "Nasıl tooeasily yükseltme Mobile Services uygulama tooan mobil uygulama hizmeti öğrenin"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a>Var olan .NET Azure mobil hizmeti tooApp hizmet yükseltme
App Service Mobile Microsoft Azure kullanarak bir yeni yolu toobuild mobil uygulamaları ' dir. toolearn daha, fazla [Mobile Apps nedir?].

Bu konuda açıklanmaktadır nasıl Azure Mobile Services tooa varolan .NET arka uç uygulamasından tooupgrade yeni App Service Mobile Apps. Bu yükseltme gerçekleştirirken mevcut Mobile Services uygulamanızı toooperate devam edebilirsiniz.   Tooupgrade bir Node.js arka uç uygulaması gereksinim duyarsanız, çok başvurun[Node.js Mobile Services yükseltme](app-service-mobile-node-backend-upgrading-from-mobile-services.md).

Bir mobil arka uç yükseltilmiş tooAzure uygulama hizmeti olduğunda, uygulama hizmeti özellikler ve öğeler faturalandırılır çok according erişim tooall sahip[uygulama hizmeti fiyatlandırma], fiyatlandırma değil Mobile Services.

## <a name="migrate-vs-upgrade"></a>Yükseltme geçirme
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Önerilir Bu, [bir geçiş gerçekleştirmek](app-service-mobile-migrating-from-mobile-services.md) yükseltme geçmeden önce. Bu şekilde, her iki sürümü, uygulamanızın koyabilirsiniz aynı App Service planı hello ve ek bir maliyet doğurur.
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a>Mobile Apps .NET sunucusu SDK yenilikleri
Yeni toohello yükseltme [Mobile Apps SDK'sı](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) hello aşağıdaki avantajları sağlar:

* NuGet bağımlılıkları hakkında daha fazla esneklik sağlar. Alternatif uyumlu sürümlerini kullanabilmek için barındırma ortamı artık hello NuGet paketleri, kendi sürümlerini sağlar. Ancak, yeni kritik bugfixes veya güvenlik güncelleştirmeleri toohello mobil Server SDK veya bağımlılıkları varsa, hizmetinizi el ile güncelleştirmeniz gerekir.
* Daha fazla esneklik sağlayan mobil SDK hello. Hangi özellikleri açıkça kontrol edebilirsiniz ve yolları, kimlik doğrulaması gibi tablo API'leri, ayarlanır ve anında iletme kayıt uç noktasını hello. toolearn daha, fazla [nasıl toouse hello .NET sunucusu SDK Azure Mobile Apps için](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).
* Diğer ASP.NET proje türleri ve yollar için destek. Mobil arka uç projeniz aynı proje hello MVC ve Web API denetleyicilerinin şimdi barındırabilir.
* Web ve mobil uygulamalar arasında toouse ortak bir kimlik doğrulama yapılandırması izin veren yeni uygulama hizmeti kimlik doğrulama özellikleri için destek.

## <a name="overview"></a>Temel yükseltmeye genel bakış
Çoğu durumda, yükseltme toohello yeni mobil uygulamalar sunucusu SDK değiştirme ve kodunuzu yeni bir mobil uygulama örneği üzerine yeniden yayımlanması olarak basit olacaktır. Vardır, ancak Gelişmiş kimlik doğrulama senaryoları ve çalışmak gibi bazı ek yapılandırma gerektiren bazı senaryolar zamanlanmış iş. Bunların her biri hello kapsamında daha sonra bölümler.

> [!TIP]
> Okuma ve bu konunun geri kalanında hello tamamen bir yükseltme işlemine başlamadan önce anlamanız önerilir. Not alın, aşağıda belirtilir tüm özelliklerini kullanabilirsiniz.
>
>

Merhaba Mobile Services istemci SDK'ları olan **değil** hello yeni mobil uygulamalar sunucusu SDK ile uyumlu. Sipariş tooprovide kesintisiz hizmet devamlılığı uygulamanız için, değişiklikleri tooa site şu anda yayımlanan istemciler hizmet veren yayınlamalıdır değil. Bunun yerine, yinelenen hizmet veren yeni bir mobil uygulama oluşturmanız gerekir. Bu uygulama koyabilirsiniz hello üzerinde ek finansal masraf tooavoid aynı uygulama hizmeti planı.

Ardından hello uygulamanın iki sürümleri gerekir: biri hangi kalır aynı hello ve yeni istemci sürümde hello joker ve hello yayımlanan uygulamalar, ardından yükseltebilirsiniz diğer ve hedef sunar. Taşıma ve kodunuzu test etmek, hızı, ancak yaptığınız tüm hata düzeltmeleri uygulanan tooboth alma emin olmanız gerekir. Düşündüğünüz sonra hello joker istemci uygulamalarında istenen sayısını toohello en son sürümünü güncelleştirilen, istediğiniz hello özgün geçirilen uygulama silebilirsiniz.

Merhaba tam anahat hello yükseltme işlemi için aşağıdaki gibidir:

1. Yeni bir mobil uygulaması oluşturma
2. Güncelleştirme hello proje toouse hello yeni sunucu SDK'ları
3. İstemci uygulamanızı yeni bir sürümü kullanıma
4. (İsteğe bağlı) Özgün geçirilen örneğinizi Sil

## <a name="mobile-app-version"></a>İkinci bir uygulama örneği oluşturma
Merhaba yükseltme ilk adımı, uygulamanızın yeni sürümünü hello barındıracak toocreate hello mobil uygulama kaynaktır. Varolan bir mobil hizmet zaten geçiş yaptıysanız, bu sürümünde hello toocreate isteyeceksiniz aynı barındırma planı. Açık hello [Azure portal] tooyour giderek uygulama geçişi. Merhaba üzerinde çalıştırıldığı App Service planı not edin.

Ardından, aşağıdaki hello tarafından hello ikinci uygulama örneği oluşturmayı [.NET arka ucu oluşturma yönergeleri](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app). Ne zaman, uygulama hizmeti planı veya "barındırma planı" seçin istendiğinde tooselect geçirilen uygulamanızın planı hello.

Büyük olasılıkla toouse hello aynı veritabanını ve Mobile Services ' bildirim hub'ı, olarak mı istersiniz. Bu değerleri açarak kopyalayabilirsiniz [Azure portal] ve toohello özgün uygulama gezinme, ardından **ayarları** > **uygulama ayarları**. Altında **bağlantı dizeleri**, kopya `MS_NotificationHubConnectionString` ve `MS_TableConnectionString`. Tooyour yeni yükseltme sitesine gidin ve tüm var olan değerlerin üzerine yazar, yapıştırın. Başka bir uygulama ayarları için bu işlemi yineleyin uygulama gereksinimlerinizi. Geçirilen hizmet kullanılmıyorsa, bağlantı dizeleri ve uygulama ayarlarını hello okuyabilirsiniz **yapılandırma** hello hello Mobile Services bölümünde sekmesinde [Klasik Azure portalı].

Merhaba ASP.NET projesi, uygulamanız için bir kopyasını alın ve tooyour yeni site yayımlayın. Merhaba yeni URL ile güncelleştirilmiş istemci uygulamanız bir kopyasını kullanarak, her şeyin beklendiği gibi çalıştığını doğrulayın.

## <a name="updating-hello-server-project"></a>Merhaba sunucu projesini güncelleştirmek
Mobile Apps sağlayan yeni bir [mobil uygulama sunucusu SDK'sı] hello çoğunu sağlayan hello Mobile Services çalışma zamanı ile aynı işlevselliği. İlk olarak, tüm başvuruları toohello Mobile Services paketlerini kaldırmanız gerekir. Merhaba NuGet Paket Yöneticisi'nde arayın `WindowsAzure.MobileServices.Backend`. Çoğu uygulamalar dahil olmak üzere çeşitli paketler burada görürsünüz `WindowsAzure.MobileServices.Backend.Tables` ve `WindowsAzure.MobileServices.Backend.Entity`. Böyle bir durumda hello bağımlılığı ağacı, en düşük paketinde hello gibi başlatın `Entity`ve bunu kaldırın. İstendiğinde, tüm bağımlı paketler kaldırmayın. Kaldırdığınız kadar bu işlemi yineleyin `WindowsAzure.MobileServices.Backend` kendisi.

Bu noktada artık Mobile Services SDK'ları başvuruda bulunan bir proje sahip olur.

Sonra başvuruları hello Mobile Apps SDK'sı ekleyeceksiniz. Bu yükseltme, çoğu Geliştirici toodownload istediğiniz ve hello yüklemek `Microsoft.Azure.Mobile.Server.Quickstart` paketi bu hello tüm gerekli kümesinde çeker gibi.

Merhaba SDK'ları arasındaki farklar kaynaklanan oldukça birkaç derleyici hataları olacaktır, ancak bunlar kolay tooaddress ve bu bölümün hello kalanında ele alınmıştır.

### <a name="base-configuration"></a>Temel yapılandırma
Ardından, WebApiConfig.cs içinde değiştirebilirsiniz:

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

İle

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> Merhaba toolearn hello yeni .NET sunucusu SDK ve nasıl tooadd/Kaldır uygulamanızdan özellikleri hakkında daha fazla bilgi istiyorsanız, lütfen bkz [nasıl toouse hello .NET sunucusu SDK] konu.
>
>

Uygulamanızı yaparsa hello kimlik doğrulama özelliklerini kullanmak, tooregister bir OWIN ara yazılımını de gerekir. Bu durumda, yapılandırma kodu yukarıdaki hello yeni bir OWIN başlangıç sınıfı taşımanız gerekir.

1. Merhaba NuGet paketi ekleme `Microsoft.Owin.Host.SystemWeb` , zaten projenizde dahil değilse.
2. Visual Studio'da, sağ, proje seçin tıklayın ve **Ekle** -> **yeni öğe**. Seçin **Web** -> **genel** -> **OWIN başlangıç sınıfı**.
3. MobileAppConfiguration için kod yukarıda Hello taşıma `WebApiConfig.Register()` toohello `Configuration()` yeni başlangıç sınıfınızın yöntemi.

Merhaba emin olun `Configuration()` yöntemi ile biter:

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

Aşağıdaki hello tam kimlik doğrulaması bölümünde ele alınan ek değişiklikler ilgili tooauthentication vardır.

### <a name="working-with-data"></a>Verilerle çalışma
Mobile Services ' hello mobil uygulama adı hello Entity Framework kurulumunda hello varsayılan şema adı olarak sundu.

sahip olduğunuz tooensure aynı hello şema başvuruda önceki gibi tooset hello hello DbContext uygulamanız için şemada aşağıdaki kullanım hello:

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

Lütfen yukarıdaki hello ayarlamanız MS_MobileServiceName olduğundan emin olun. Uygulamanız bu önceden özelleştirdiyseniz, başka bir şema adı da sağlayabilirsiniz.

### <a name="system-properties"></a>Sistem Özellikleri
#### <a name="naming"></a>Adlandırma
Hello Azure Mobile Services sunucusu SDK, Sistem özellikleri her zaman çift alt çizgi içerebilir (`__`) hello özellikleri öneki:

* __createdAt
* __updatedAt
* __deleted
* __version

Merhaba Mobile Services istemci SDK'ları bu biçimde Sistem özellikleri ayrıştırma için özel bir mantığı vardır.

Azure Mobile Apps'de Sistem özellikleri artık biçimlendirmek ve adlarından hello sahip özel bir vardır:

* CreatedAt
* updatedAt
* silindi
* Sürüm

Merhaba değişiklik yok; Bu nedenle Mobile Apps istemci SDK'ları kullanmak hello yeni Sistem özellikleri adları, tooclient kodu gereklidir. Ancak, doğrudan varsa KALAN yapma tooyour hizmetini çağırır sonra sorgularınızı uygun şekilde değiştirmeniz gerekir.

#### <a name="local-store"></a>Yerel depolama
Sistem özellikleri Hello değişiklikleri toohello adlarını çevrimdışı eşitleme yerel veritabanı Mobile Services için Mobile Apps ile uyumlu değil anlamına gelir. Mümkünse, toohello sunucu uygulamaları kadar sonra bekleyen değişiklikler gönderildikten Mobile Services tooMobile istemci uygulamaları yükseltme kaçınmalısınız. Ardından, hello yükseltilmiş uygulama yeni bir veritabanı dosya adı kullanmanız gerekir.

Merhaba işlemi sırasındaki çevrimdışı, bekleyen değişiklikler varken bir istemci uygulaması Mobile Services tooMobile uygulamaları ' yükseltilmiş ise hello sistem veritabanı güncelleştirilmiş toouse hello yeni sütun adlarının olması gerekir. İos'ta, bu basit geçişler toochange hello sütun adları kullanarak elde edilebilir. Android ve hello .NET yönetilen istemci üzerinde veri nesnesi tablolarınız için hello sütunları özel SQL toorename yazmalısınız.

İos'ta, veri varlıkları toomatch hello şunlar için çekirdek veri şemanızı değiştirmeniz gerekir. Özellikler hello Not `createdAt`, `updatedAt` ve `version` artık bir `ms_` öneki:

| Öznitelik | Tür | Not |
| --- | --- | --- |
| id |Dize, gerekli olarak işaretlenmiş |Uzak Depolama birincil anahtar |
| CreatedAt |Tarih |(isteğe bağlı) eşlemeleri toocreatedAt sistem özelliği |
| updatedAt |Tarih |(isteğe bağlı) eşlemeleri tooupdatedAt sistem özelliği |
| Sürüm |Dize |(isteğe bağlı) kullanılan toodetect çakışmaları, maps tooversion |

#### <a name="querying-system-properties"></a>Sistem özellikleri sorgulama
Azure Mobile Services ' Sistem özellikleri varsayılan olarak, ancak yalnızca hello sorgu dizesi kullanılarak istendiklerinde gönderilmez `__systemProperties`. Buna karşılık, Azure Mobile Apps sistemde özelliklerdir **her zaman seçili** hello server SDK nesne modeli parçası olduğundan.

Bu değişiklik çoğunlukla uzantılarını gibi etki alanı yöneticileri özel uygulamaları etkiler `MappedEntityDomainManager`. Bir istemci hiçbir zaman tüm sistem özelliklerini istediğinde Mobile Services ' olası toouse olmasına bir `MappedEntityDomainManager` gerçekten tüm özellikleri eşleşmiyor. Ancak, Azure Mobile Apps'de eşlenmemiş bu özellikleri GET sorgularda hataya neden olur.

Merhaba en kolay yolu tooresolve hello sorunu toomodify, DTOs, bunlar devralınmalıdır böylelikle `ITableData` yerine `EntityData`. Ardından, hello ekleyin `[NotMapped]` alınmamalıdır toohello alanları özniteliği.

Örneğin, hello aşağıdakileri tanımlar `TodoItem` hiçbir sistem özelliklere sahip:

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

Not: hataları alırsanız, `NotMapped`, bir başvuru toohello derleme ekleyin `System.ComponentModel.DataAnnotations`.

### <a name="cors"></a>CORS
Mobile Services hello ASP.NET CORS çözüm kaydırma tarafından bazı CORS desteği dahil. Doğrudan yararlanabilirsiniz şekilde bu kaydırma katman daha fazla denetim, kaldırılan toogive hello Geliştirici bırakıldı [ASP.NET CORS desteğini](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

Merhaba CORS kullanıyorsanız sorun ana alanlarını olan bu hello `eTag` ve `Location` üstbilgileri gerekir izin hello istemci SDK'ları toowork sırada düzgün.

### <a name="push-notifications"></a>Anında İletme Bildirimleri 
Göndermenin Server SDK hello eksik bulabilirsiniz hello ana öğesi hello PushRegistrationHandler sınıftır. Kayıtlar biraz farklı mobil uygulamalarda işlenir ve tagless kayıtlar varsayılan olarak etkinleştirilir. Etiketler yönetme özel API'lerini kullanarak bunu. Lütfen hello bakın [için etiketler kaydetme](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) daha fazla bilgi için yönergeler.

### <a name="scheduled-jobs"></a>Zamanlanan işler
.NET arka ucuna sahip var olan tüm işleri toobe ayrı ayrı yükseltilmesi gerekir zamanlanmış işler mobil uygulamasında yerleşiktir böylece değil. Bir seçenektir toocreate zamanlanmış bir [Web işi] hello mobil uygulama kodu sitesinde. Ayrıca iş kodunuzu tutan kurma denetleyicisi ve hello yapılandırma [Azure Scheduler] toohit beklenen hello zamanlamaya göre bu bitiş noktası.

### <a name="miscellaneous-changes"></a>Çeşitli değişiklikler
Mobil istemci tarafından kullanılan tüm ApiControllers şimdi hello olmalıdır `[MobileAppController]` özniteliği. Diğer ApiControllers toogo tarafından etkilenmemesini hello mobil biçimlendiricileri böylece bu artık varsayılan olarak dahil edilir.

Merhaba `ApiServices` nesnesidir artık hello SDK parçası. Mobil uygulama ayarlarını tooaccess hello aşağıdakileri kullanabilirsiniz:

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

Benzer şekilde, günlük şimdi hello standart ASP.NET izleme yazma kullanılarak gerçekleştirilir:

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <a name="authentication"></a>Kimlik doğrulama konuları
Mobile Services Hello kimlik doğrulama bileşenleri şimdi hello App Service kimlik doğrulama/yetkilendirme özelliğini taşınmıştır. Bu, siteniz için okuma hello tarafından etkinleştirme hakkında bilgi edinebilirsiniz [Ekle kimlik doğrulama tooyour mobil uygulama](app-service-mobile-ios-get-started-users.md) konu.

AAD, Facebook ve Google, gibi bazı sağlayıcılar için kopyalama uygulamanızdan mümkün tooleverage hello mevcut kayıt olması gerekir. Sadece toonavigate toohello kimlik sağlayıcısının portalında gerekir ve yeni bir yeniden yönlendirme URL'si toohello kaydı ekleyin. Daha sonra App Service kimlik doğrulama/yetkilendirme hello istemci kimliği ve parolası ile yapılandırın.

### <a name="controller-action-authorization"></a>Denetleyici eylem yetkilendirme
Merhaba'nın tüm örneklerini `[AuthorizeLevel(AuthorizationLevel.User)]` özniteliği değiştirilmiş toouse şimdi olmalıdır standart ASP.NET hello `[Authorize]` özniteliği. Ayrıca, denetleyicileri anonim diğer ASP.NET uygulamaları olduğu gibi varsayılan olarak sunulmuştur.
Yönetici veya uygulama gibi diğer AuthorizeLevel seçenekleri hello birini kullanıyorsanız, bunlar kaldırılmıştır olduğunu unutmayın. Bunun yerine AuthorizationFilters için paylaşılan gizli kod dizeleri ayarlayın veya bir AAD hizmet sorumlusu tooenable hizmet-hizmet çağrıları güvenli bir şekilde yapılandırın.

### <a name="getting-additional-user-information"></a>Ek kullanıcı bilgilerini alma
Hello üzerinden erişim belirteçleri gibi ek kullanıcı bilgi alabileceğiniz `GetAppServiceIdentityAsync()` yöntemi:

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

Ayrıca, uygulamanızı bağımlılıkları kimlikleri, kullanıcı, bir veritabanında saklamak gibi alırsa, kullanıcı kimliklerini Mobile Services ve App Service Mobile Apps arasında hello toonote farklı önem taşır. Ancak hello Mobile Services kullanıcı kimliği, elde edebilirsiniz. Tüm hello ProviderCredentials alt sınıfların, bir kullanıcı kimliği özelliği vardır. Bu nedenle önce hello örneğindeki etmeden:

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

Uygulamanızı bağımlılıkları kullanıcı kimlikleri izlerseniz, kullanırsanız kullanın önemli bir kimlik sağlayıcısı ile aynı kayıt mümkünse hello. Kullanıcı kimliklerini kullanıldı, genellikle kapsamlı toohello uygulama kaydı olduğundan, yeni bir kayıt Tanıtımı eşleşen kullanıcıları tootheir veri sorunları oluşturabilirsiniz.

### <a name="custom-authentication"></a>Özel kimlik doğrulama
Uygulamanızı bir özel kimlik doğrulama çözümü kullanıyorsanız, toomake erişim toohello sistem hello yükseltilmiş site olduğundan emin isteyeceksiniz. Merhaba özel kimlik doğrulama için Hello yeni yönergeleri [.NET sunucusu SDK Genel Bakış] toointegrate çözümünüzü. Lütfen hello özel kimlik doğrulama bileşenleri hala önizlemede olduğuna dikkat edin.

## <a name="updating-clients"></a>İstemcileri güncelleştirme
İşletimsel bir mobil uygulama arka ucu olduktan sonra hangi içereceği tükettiği istemci uygulamanızı yeni bir sürümünü çalışabilirsiniz. Mobile Apps istemci SDK'in hello yeni bir sürümünü de içerir ve benzer toohello sunucu yükseltme yukarıdaki, tüm başvurular toohello Mobile Services SDK'ları önce tooremove gerekir hello Mobile Apps sürümler yükleme.

Merhaba ana değişiklikleri hello sürümleri arasında hello oluşturucular artık bir uygulama anahtarı iste biridir. Artık yalnızca mobil uygulamanızın hello URL'de geçirdiğiniz. Örneğin, hello .NET istemcilerde hello `MobileServiceClient` Oluşturucusu olan şimdi:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

Yükleme hakkında bilgi edinebilirsiniz yeni SDK'ları hello ve aşağıdaki hello bağlantıları üzerinden hello yeni yapısını kullanarak:

* [iOS sürüm 3.0.0 veya daha yenisi](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) sürüm 2.0.0 veya daha yenisi](app-service-mobile-dotnet-how-to-use-client-library.md)

Olmuştur gibi bazı değişiklikler vardır de uygulamanız anında iletme bildirimleri kullanın, her platform için belirli kayıt yönergeleri hello Not yapıyorsa.

Merhaba yeni istemci sürümü hazır olduğunda, yükseltilen sunucu projenizi karşı deneyin. Çalışır durumda olduğunu doğrulandıktan sonra uygulama toocustomers yeni bir sürümü serbest bırakabilirsiniz. Sonuç olarak, müşterilerinizin bu güncelleştirmeler bir fırsat tooreceive beklendiğinden sonra hello Mobile Services sürümü, uygulamanızın silebilirsiniz. Bu noktada, tamamen tooan mobil uygulama hizmeti yükselttikten hello en son mobil uygulamalar sunucusu SDK kullanarak.

<!-- URLs. -->

[Azure portal]: https://portal.azure.com/
[Klasik Azure portalı]: https://manage.windowsazure.com/
[Mobile Apps nedir?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[mobil uygulama sunucusu SDK'sı]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web işi]: ../app-service-web/websites-webjobs-resources.md
[nasıl toouse hello .NET sunucusu SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[uygulama hizmeti fiyatlandırma]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET sunucusu SDK Genel Bakış]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md

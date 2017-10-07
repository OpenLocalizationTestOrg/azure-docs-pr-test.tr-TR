---
title: "aaaWindows Phone Silverlight Reach SDK tümleştirmesi"
description: "Nasıl tooIntegrate Azure Mobile Engagement Reach Windows Phone Silverlight uygulamaları ile"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a>Windows Phone Silverlight Reach SDK tümleştirmesi
Merhaba tümleştirme hello yordamını izleyin [Windows Phone Silverlight Engagement SDK tümleştirmesi](mobile-engagement-windows-phone-integrate-engagement.md) bu kılavuz aşağıdaki önce.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a>Windows Phone Silverlight projenize Hello Engagement Reach SDK'sı ekleme
Herhangi bir şey yok tooadd. `EngagementReach`Projenizde başvuruları ve kaynak zaten var.

> [!TIP]
> Hello bulunan görüntüleri özelleştirebilirsiniz `Resources` klasörü projenizin, özellikle hello marka simgesini (Bu varsayılan toohello katılım simge).
> 
> 

## <a name="add-hello-capabilities"></a>Merhaba yetenekleri ekleme
Merhaba Engagement Reach SDK'SININ bazı ek yetenekler gerekir.

Açık, `WMAppManifest.xml` dosya ve yetenekleri aşağıdaki o hello bildirildiğinden emin olun:

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

Merhaba ilk hello MPNS hizmet tooallow hello görüntüsünü bildirim tarafından kullanılır. Merhaba ikinci kullanılan tooembed tarayıcı görev hello SDK içine adrestir.

Merhaba Düzenle `WMAppManifest.xml` dosya ve hello ekleyin `<Capabilities />` etiketi:

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a>Merhaba Microsoft anında bildirim hizmeti etkinleştirme
Sipariş toouse hello içinde **Microsoft anında bildirim hizmeti** (MPNS adlandırılır), `WMAppManifest.xml` dosya olmalıdır bir `<App />` ile etiketi bir `Publisher` özniteliğini toohello projenizin adını ayarlayın.

## <a name="initialize-hello-engagement-reach-sdk"></a>Merhaba Engagement Reach SDK'sını başlatma
### <a name="engagement-configuration"></a>Katılım yapılandırma
Merhaba katılım yapılandırma hello Merkezi `Resources\EngagementConfiguration.xml` projenizin dosya.

Bu dosya toospecify ulaşma yapılandırmasını düzenleyin:

* *İsteğe bağlı*, hello yerel gönderim (MPNS) etkin olup olmadığını veya arasında değil belirtmek `<enableNativePush>` ve `</enableNativePush>` etiketleri (`true` varsayılan olarak).
* *İsteğe bağlı*, arasında hello itme kanal hello adını belirtmek `<channelName>` ve `</channelName>` etiketleri, sağlar hello uygulamanız şu anda kullanın veya bu alanı boş bırakın, aynı.

Çalışma zamanında, bunun yerine, çağırabilirsiniz hello aşağıdaki toospecify istiyorsanız yöntemi hello katılım aracı başlatmadan önce:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> Merhaba MPNS anında iletme kanal uygulamanızın hello adını belirtebilirsiniz. Varsayılan olarak, katılım hello AppID üzerinde tabanlı bir ad oluşturur. Katılım dışında toouse hello itme kanal düşünüyorsanız dışında hiçbir gerek toospecify hello adına kendiniz sahip.
> 
> 

### <a name="engagement-initialization"></a>Katılım başlatma
Merhaba değiştirme `App.xaml.cs`:

* Tooyour ekleme `using` deyimleri:
  
      using Microsoft.Azure.Engagement;
* INSERT `EngagementReach.Instance.Init` hemen sonra `EngagementAgent.Instance.Init` içinde `Application_Launching` :
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* INSERT `EngagementReach.Instance.OnActivated` hello içinde `Application_Activated` yöntemi:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> Merhaba `EngagementReach.Instance.Init` adanmış bir iş parçacığı çalıştırır. Toodo sahip değil, kendiniz.
> 
> 

## <a name="app-store-submission-considerations"></a>Uygulama mağazası gönderimi dikkat edilecek noktalar
Microsoft, hello anında iletme bildirimleri kullanırken bazı kuralları uygular:

Merhaba Microsoft gelen [uygulama ilkeleri] belgeleri, bölüm 2.9:

1) Merhaba kullanıcı tooaccept tooreceive anında iletme bildirimleri kaldırmasını isteyebilirsiniz. Ardından, ayarlarınızda bir şekilde toodisable hello anında iletme bildirimleri ekleme.

Merhaba EngagementReach nesne sağlayan iki yöntem toomanage hello içinde/opt-çevirin, `EnableNativePush()` ve `DisableNativePush()`. , Örneğin, bir seçenek hello ayarları değiştir toodisable ile oluşturduğunuz veya MPNS etkinleştirin.

Merhaba katılım yapılandırma yoluyla toodeactivate MPNS karar verebilirsiniz\<windows phone-sdk-reach-yapılandırma\>.

> 2.9.1) hello uygulamayı sağlanan hello bildirimleri toobe ilk tanımlayan gerekir ve **hello kullanıcının express iznini (katılımı) elde**, ve **hangi hello kullanıcı kabul alma dışında bir mekanizma sağlamanız gerekir anında iletme bildirimleri**. Sağlanan Hello Microsoft anında bildirim hizmeti kullanarak tüm bildirimleri hello sağlanan açıklama toohello kullanıcı ile tutarlı olmalıdır ve tüm ile uymalıdır geçerli [uygulama ilkeleri] [ Content Policies]ve [belirli uygulama türleri için ek gereksinimler].
> 
> 

2) Çok fazla anında iletme bildirimleri kullanmamanız gerekir. Katılım bildirimleri sizin için işler.

> 2.9.2) hello uygulama ve hello Microsoft anında bildirim hizmeti kullanımı değil aşırı ağ kapasitesi veya bant genişliği hello Microsoft anında bildirim hizmeti veya kullanmanız gerekir, aksi takdirde unduly bir Windows Phone veya diğer Microsoft cihaz veya hizmet yük aşırı ile anında iletme bildirimleri, Microsoft tarafından makul kendi takdirine bağlı olarak belirlenen ve değil zarar veya gerekir herhangi Microsoft ağları veya sunucuları veya tüm üçüncü taraf sunucular ya da ağlara bağlı toohello Microsoft anında bildirim hizmeti ile müdahale.
> 
> 

3) MPNS toosend criticals bilgi kullanmayın. Katılım MPNS, kullanır, bu nedenle bu kural katılım hello içinde ön uç oluşturulan hello kampanyaları için de geçerlidir.

> 2.9.3) Microsoft anında bildirim hizmeti, kritik veya aksi takdirde görev kullanılan toosend bildirimleri olmayabilir hello yaşam veya sınırlaması kritik bildirimleri ilgili tooa tıbbi cihaz veya koşulu dahil olmak üzere ölüm önemlidir etkileyen. MICROSOFT açıkça reddeder herhangi garanti olduğunu hello kullan, hello MICROSOFT anında bildirim hizmeti veya teslim, MICROSOFT anında bildirim hizmeti bildirimleri olacak olması kesintisiz hata boş veya aksi halde garanti tooOCCUR ON A gerçek zamanlı olarak.
> 
> 

**Bu öneriler dikkate almaz, uygulamanızın hello doğrulama işlemi geçer garanti edemez.**

## <a name="handle-data-push-optional"></a>Veri gönderimi (isteğe bağlı) işleme
Uygulama toobe mümkün tooreceive ulaşma veri gönderimleri isterseniz, iki olayları hello EngagementReach sınıfı tooimplement vardır:

    EngagementReach.Instance.DataPushStringReceived += (body) =>
    {
       Debug.WriteLine("String data push message received: " + body);
       return true;
    };

    EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
    {
       Debug.WriteLine("Base64 data push message received: " + encodedBody);
       // Do something useful with decodedBody like updating an image view
       return true;
    };

Her yöntem döndürür bir Boole değeri, bu hello geri çağırma görebilirsiniz. Katılım hello veri gönderimi gönderdikten sonra bir geri bildirim tooits arka uç gönderir. Merhaba geri çağırma false değeri döndürülürse, hello `exit` geri bildirim gönder olacaktır. Aksi durumda olur `action`. Geri arama yok hello olaylarını ayarlarsanız hello `drop` geri bildirim tooEngagement döndürülecek.

> [!WARNING]
> Katılım mümkün tooreceive katları geribildirimler veri gönderimi için değil. Bir olayda birçok işleyicileri tooset planlıyorsanız, hello geri bildirim sonuncu gönderilen toohello karşılık unutmayın. Bu durumda, tooalways öneririz hello kafa karıştırıcı geri bildirim hello ön uç sahip aynı değeri tooavoid döndürür.
> 
> 

## <a name="customize-ui-optional"></a>(İsteğe bağlı) kullanıcı arabirimini özelleştirme
### <a name="first-step"></a>İlk adım
Biz toocustomize hello ulaşma kullanıcı Arabirimi sağlar.

toodo bu nedenle, toocreate hello öğesinin bir alt kümesi olan `EngagementReachHandler` sınıfı.

**Örnek kod:**

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

Sonra hello Merhaba içeriğine ayarlayın `EngagementReach.Instance.Handler` özel nesnesinde ile alan, `App.xaml.cs` hello sınıfında `Application_Launching` yöntemi.

**Örnek kod:**

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> Varsayılan olarak, kendi uyarlamasını katılım kullanır `EngagementReachHandler`. Toocreate yoksa, kendi ve bunu yaparsanız, her yöntemi toooverride yok. tooselect hello katılım temel nesne Hello varsayılan davranıştır.
> 
> 

### <a name="layouts"></a>Düzenleri
Varsayılan olarak, ulaşma hello DLL toodisplay hello bildirimleri ve sayfalarının katıştırılmış hello kaynakları kullanır.

Ancak, kendi kaynaklarını tooreflect toouse karar verebilirsiniz, marka bu bileşenlerde.

Geçersiz kılabilirsiniz `EngagementReachHandler` alt tootell katılım toouse yöntemleri, düzenler:

**Örnek kod:**

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> Merhaba `CreateNotification` yöntemi null dönebilirsiniz. Merhaba bildirim görüntülenmez ve hello reach kampanya bırakılacak.
> 
> 

toosimplify düzeni uygulamanızı ayrıca kodunuz için temel olarak hizmet verebilir kendi xaml sağlıyoruz. Merhaba Engagement SDK'sı arşivindeki bulundukları (/ src/reach /).

> [!WARNING]
> Merhaba kullandığımız tam aynı olanlardır sağladığımız hello kaynakları. Bu nedenle toomodify istiyorsanız, bunları doğrudan yok toochange hello ad alanı unutursanız ve ad hello.
> 
> 

### <a name="notification-position"></a>Bildirim konumu
Varsayılan olarak, bir uygulama bildirimi hello sayfanın sol tarafında Merhaba uygulaması görüntülenir. Merhaba geçersiz kılarak bu davranışı değiştirebilirsiniz `GetNotificationPosition` hello yöntemi `EngagementReachHandler` nesnesi.

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

Şu anda hello arasında seçim yapabilirsiniz `BOTTOM` (varsayılan) ve `TOP` konumlar.

### <a name="launch-message"></a>İleti Başlatma
Bir kullanıcı bir sistem bildirimi (bildirim) tıkladığında, katılım başlatır uygulama Merhaba, yük hello Merhaba içeriğine iletileri gönderme ve kampanya karşılık gelen hello hello sayfayı görüntüleme.

Merhaba başlatma (bağlı olarak, ağ hızına hello) hello sayfasının hello uygulama ve hello görüntüsünün arasında bir gecikme yoktur.

bir şey yüklüyor tooindicate toohello kullanıcı, bir ilerleme çubuğu veya bir İlerleme göstergesi gibi görsel bir bilgi sağlamalıdır. Katılım kendisi, ancak sağladığı birkaç işleyicileri sizin için işleyemez.

tooimplement geri çağırma Merhaba, yapın:

    /* hello application has launched and hello content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* hello application has finished loading hello content and hello page
     * is about toobe displayed.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* hello content has been loaded, but an error has occurred.
     * You can provide an information toohello user.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

Merhaba geri çağırma ayarlayabileceğiniz, `Application_Launching` yöntemi, `App.xaml.cs` dosya, tercihen hello önce `EngagementReach.Instance.Init()` çağırın.

> [!TIP]
> Her işleyici hello tarafından kullanıcı Arabirimi iş parçacığı denir. MessageBox veya bir şey UI ilgili kullanırken tooworry yok.
> 
> 

[uygulama ilkeleri]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[belirli uygulama türleri için ek gereksinimler]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx


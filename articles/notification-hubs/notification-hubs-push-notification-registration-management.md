---
title: "aaaRegistration Yönetimi"
description: "Bu konuda nasıl tooregister aygıtları sipariş tooreceive notification hubs ile anında iletme bildirimleri açıklanmaktadır."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a>Kayıt yönetimi
## <a name="overview"></a>Genel Bakış
Bu konuda nasıl tooregister aygıtları sipariş tooreceive notification hubs ile anında iletme bildirimleri açıklanmaktadır. Merhaba konu kayıtlar yüksek düzeyde açıklanır ve ardından aygıtları kaydetmeye yönelik hello iki ana desenleri sunar: hello aygıttan kaydetme doğrudan toohello bildirim hub'ı ve bir uygulama arka ucu kaydediliyor. 

## <a name="what-is-device-registration"></a>Cihaz kaydı nedir
Bildirim hub'ı ile cihaz kaydı kullanarak gerçekleştirilir bir **kayıt** veya **yükleme**.

#### <a name="registrations"></a>Kayıtlar
Bir kayıt etiketleri ve büyük olasılıkla bir şablonu ile bir aygıt için Platform bildirim hizmeti (PNS) işlemek hello ilişkilendirir. Merhaba PNS tanıtıcısını ChannelURI, cihaz belirteci veya GCM kayıt kimliği olabilir. Etiketler kullanılan tooroute bildirimleri toohello doğru cihaz tanıtıcılarını kümesidir. Daha fazla bilgi için bkz: [Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md). Kullanılan tooimplement kayıt başına dönüştürme şablonlarıdır. Daha fazla bilgi için bkz: [şablonları](notification-hubs-templates-cross-platform-push-messages.md).

#### <a name="installations"></a>Yüklemeleri
Yüklemesi geliştirilmiş olabilir itme paketi içeren kayıt ilgili özellikler. Bu, en son ve en iyi yaklaşımı tooregistering aygıtlarınızı hello olur. Ancak, istemci tarafı .NET SDK'sı tarafından desteklenmiyor ([Notification Hub SDK'sı arka uç işlemleri için](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) henüz dağıtmadığı.  Hello istemci CİHAZDAN kaydediyorsunuz varsa toouse hello yani [Notification Hubs REST API'si](https://msdn.microsoft.com/library/mt621153.aspx) yaklaşımını toosupport yüklemeleri. Bir arka uç hizmeti kullanıyorsanız, mümkün toouse olmalıdır [Notification Hub SDK'sı arka uç işlemleri için](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Merhaba, bazı önemli avantajı toousing yüklemeler şunlardır:

* Oluşturma veya bir yüklemeyi güncelleştirme ıdempotent tam değil. Bu nedenle tüm yinelenen kayıtları endişeniz olmadan deneyebilirsiniz.
* Merhaba yükleme modeli kolay toodo tek tek iter - belirli bir aygıtı hedefleme kolaylaştırır. Bir sistem etiketi **"$InstallationId: [InstallationID]"** her bağlı yükleme kaydı otomatik olarak eklenir. Bu nedenle hiçbir ek kodlama toodo gerek kalmadan belirli bir aygıt gönderme toothis etiketi tootarget çağırabilirsiniz.
* Yüklemeleri kullanarak, toodo kısmi kayıt güncelleştirmeler sağlar. Merhaba kısmi güncelleştirme yüklemesinin hello kullanarak bir düzeltme eki yöntemiyle istenmeden [JSON düzeltme eki standart](https://tools.ietf.org/html/rfc6902). Bu, özellikle hello kayıt tooupdate etiketlerini istediğinizde kullanışlıdır. Merhaba tüm kayıt aşağı toopull yoksa ve tüm hello önceki etiketleri tekrar tekrar gönderin.

Yüklemenin aşağıdaki özelliklere hello hello içerebilir. Merhaba yükleme özellikleri bakın, tam bir listesi için [oluşturmak veya bir yükleme ile REST API üzerine](https://msdn.microsoft.com/library/azure/mt621153.aspx) veya [yükleme özellikleri](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) hello için.

    // Example installation format tooshow some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



Bu kayıtlar ve varsayılan olarak yüklemeleri artık sona önemli toonote olur.

Kayıtlar ve yüklemeleri her cihaz/kanal için geçerli bir PNS tanıtıcısını içermelidir. PNS tanıtıcılarını yalnızca hello aygıttaki istemci uygulamasında alınabilir, bir desen hello istemci uygulaması ile bir cihazda doğrudan tooregister olmasıdır. Merhaba üzerinde tootags hello uygulama arka uç toomanage cihaz kaydında gerektirebilir diğer yandan, güvenlik konuları ve iş mantığı ilgili. 

#### <a name="templates"></a>Şablonlar
Toouse istiyorsanız [şablonları](notification-hubs-templates-cross-platform-push-messages.md), hello aygıt yüklemesi de JSON bu aygıt ile ilişkili tüm şablonları tutun (Yukarıdaki örnek bakın) biçimlendirin. Merhaba şablon adları farklı şablonları hello için hedef Yardım aynı aygıt.

Her bir şablon adı tooa şablon gövde ve etiketleri isteğe bağlı bir dizi unutmayın. Ayrıca, her platform ek şablon özelliklere sahip olabilir. Windows Mağazası'nın (WNS kullanarak) ve Windows Phone 8 (MPNS kullanarak) için ek bir üstbilgi kümesi hello şablonunun parçası olabilir. APNs Hello durumda sabit veya tooa şablon ifadesi bir süre sonu özelliği tooeither ayarlayabilirsiniz. Merhaba yükleme özellikleri bakın, tam bir listesi için [oluşturmak veya bir yükleme ile REST üzerine](https://msdn.microsoft.com/library/azure/mt621153.aspx) konu.

#### <a name="secondary-tiles-for-windows-store-apps"></a>Windows mağazası uygulamaları için ikincil döşeme
Windows mağazası istemci uygulamaları için gönderen bildirimleri toosecondary döşeme olduğu aynı toohello birincil bir gönderme olarak hello. Bu ayrıca yüklemelerde desteklenir. İkincil döşeme hangi ' % s'hello SDK istemci uygulamanızdan şeffaf bir şekilde işler farklı bir ChannelUri gerektiğini unutmayın.

Merhaba SecondaryTiles sözlük kullanan Windows mağazası uygulamanızı kullanılan toocreate hello SecondaryTiles nesne aynı TileId hello.
Olarak ile Merhaba birincil ChannelUri, ikincil döşeme ChannelUris herhangi bir anda değiştirebilirsiniz. Sipariş tookeep hello yüklemelerde hello bildirim hub'ı güncelleştirilmiş hello aygıt bunları hello ile yenilemeniz gerekir hello ikincil döşeme geçerli ChannelUris.

## <a name="registration-management-from-hello-device"></a>Merhaba aygıttan kayıt yönetimi
Cihaz kaydı istemci uygulamaları yönetirken hello arka uç yalnızca bildirim göndermek için sorumludur. İstemci uygulamaları PNS tanıtıcılarını toodate yukarı tutmak ve etiketleri kaydedin. Resim aşağıdaki hello bu deseni gösterilmektedir.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

Merhaba cihaz ilk PNS hello hello PNS ele alır ve sonra hello bildirim hub'ı doğrudan kaydeder. Merhaba kaydı başarılı olduktan sonra hello uygulama arka ucu o kayıt hedefleyen bir bildirim gönderebilirsiniz. Hakkında daha fazla bilgi için toosend bildirimleri bkz [Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).
Bu durumda, kullanacağınız Not hello aygıttan bildirim hub'larınız yalnızca hakları tooaccess dinler. Daha fazla bilgi için bkz: [güvenlik](notification-hubs-push-notification-security.md).

Merhaba aygıttan kaydetme hello basit bir yöntemdir, ancak bazı kısıtlamaları vardır.
Merhaba ilk dezavantajı hello uygulama etkin durumdayken bir istemci uygulaması yalnızca kendi etiketleri güncelleştirebilirsiniz olmasıdır. Bir kullanıcının hello ilk aygıt bir ek etiketi (örneğin, takımınız) kaydettiğinde etiketleri ilgili toosport ekipleri, kayıt iki cihazlar varsa, örneğin, hello ikinci bir cihaz hello takımınız hakkında hello bildirimler hello hello uygulamasını kadar almaz İkinci bir cihaz ikinci bir kez çalıştırılır. Etiketler birden çok aygıt tarafından etkilenir, daha genel olarak, etiketleri hello arka ucundan yönetme bir arzu seçenektir.
Hello ikinci dezavantajı hello istemci uygulamasından kayıt yönetimi, uygulamaları ele olduğundan, hello kayıt toospecific etiketleri güvenliğini sağlama fazladan bakımı, "etiketi düzeyi güvenlik." Merhaba bölümünde açıklandığı gibi gerektirmesidir

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a>Örnek kod tooregister bir bildirim hub'ından bir yükleme kullanarak bir cihazı ile
Şu anda yalnızca hello kullanarak destekleniyorsa [Notification Hubs REST API'si](https://msdn.microsoft.com/library/mt621153.aspx).

Hello kullanarak hello düzeltme eki yöntemini de kullanabilirsiniz [JSON düzeltme eki standart](https://tools.ietf.org/html/rfc6902) hello yükleme güncelleştirmek için.

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine hello targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a>Örnek kod tooregister bir bildirim hub'ından bir kaydı kullanarak bir cihazı ile
Bu yöntemler oluşturun veya bunlar adı verilir hello cihaz için bir kayıt güncelleştirin. Bu sipariş tooupdate hello tanıtıcısı veya hello etiketlerinde, hello tüm kayıt üzerine yazmalıdır anlamına gelir. Her zaman belirli bir aygıt gereklidir hello geçerli etiketler güvenilir deposuyla gerekir böylece kayıtlar geçici olduğunu unutmayın.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a>Kayıt Yönetimi'nden bir arka uç
Kayıtlar hello arka ucundan yönetme ek kod yazma gerektirir. Merhaba CİHAZDAN Hello uygulamasını hello uygulama (etiketleri ve şablonlar ile birlikte) her başlatıldığında güncelleştirilmiş PNS tanıtıcı toohello arka uç hello ve hello arka uç bu tanıtıcıyı hello bildirim hub'ındaki güncelleştirmeniz gerekir sağlamanız gerekir. Bu tasarım resim aşağıdaki hello gösterilmektedir.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

hello yararları hello arka ucundan kayıtlarını yönetme, etiket tooits kayıt eklemeden önce hello karşılık gelen uygulamasını hello cihazda devre dışı olduğunda bile hello özelliği toomodify etiketleri tooregistrations ve tooauthenticate hello istemci uygulamasını içerir.

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a>Örnek kod tooregister bir bildirim hub'ından bir yükleme seçeneğini kullanarak bir arka uç ile
Hello istemci aygıt hala alır PNS tanıtıcısını ve ilgili yükleme özellikleri eskisi ve özel bir API hello kaydı gerçekleştirmek ve onları yetkilendirmek hello arka uç üzerinde etiketler vb. hello arka uç çağrıları hello yararlanabilir [Notification Hub SDK'sı arka uç işlemleri](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Hello kullanarak hello düzeltme eki yöntemini de kullanabilirsiniz [JSON düzeltme eki standart](https://tools.ietf.org/html/rfc6902) hello yükleme güncelleştirmek için.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a>Örnek kod tooregister bildirim hub'ı bir kayıt kimliği kullanılarak bir aygıttan ile
Uygulama arka ucunuzdan, kayıtlar üzerinde temel CRUDS işlemler gerçekleştirebilirsiniz. Örneğin:

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


Merhaba arka uç kaydı güncelleştirmeleri arasındaki eşzamanlılık işlemelidir. Hizmet veri yolu iyimser eşzamanlılık denetimini kayıt yönetimi sunar. Merhaba HTTP düzeyde, bu kayıt yönetim işlemlerini ETag, hello kullanımıyla uygulanır. Bu özellik, saydam bir güncelleştirme eşzamanlılık nedenlerle reddedilirse, bir özel durum SDKs tarafından kullanılır. Merhaba uygulama arka ucu, bu özel durumları işleme ve gerekirse hello güncelleştirme yeniden deneniyor sorumludur.


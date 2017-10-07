---
title: "aaaHow toouse Azure Service Bus konuları ve abonelikleri Node.js ile | Microsoft Docs"
description: "Bilgi nasıl toouse Service Bus konuları ve bir Node.js uygulaması Azure aboneliklerinde."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="78706-103">Nasıl tooUse Service Bus konuları ve abonelikleri Node.js ile</span><span class="sxs-lookup"><span data-stu-id="78706-103">How tooUse Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="78706-104">Bu kılavuzda açıklanmaktadır nasıl toouse Service Bus konuları ve abonelikleri Node.js uygulamalardan.</span><span class="sxs-lookup"><span data-stu-id="78706-104">This guide describes how toouse Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="78706-105">Merhaba kapsanan senaryolar dahil **konuları ve abonelikleri oluşturma**, **abonelik filtreleri oluşturma**, **ileti gönderme** tooa konu **alma bir abonelik iletilerden**, ve **konuları ve abonelikleri silmeyi**.</span><span class="sxs-lookup"><span data-stu-id="78706-105">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="78706-106">Merhaba konu başlıkları ve abonelikler hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="78706-106">For more information about topics and subscriptions, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="78706-107">Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="78706-107">Create a Node.js application</span></span>
<span data-ttu-id="78706-108">Boş bir Node.js uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="78706-108">Create a blank Node.js application.</span></span> <span data-ttu-id="78706-109">Bir Node.js uygulaması oluşturma ile ilgili yönergeler için bkz: [oluşturma ve bir Node.js uygulaması tooan Azure Web sitesi dağıtma], [Node.js bulut hizmeti] [ Node.js Cloud Service] Windows kullanma PowerShell veya Web sitesini WebMatrix ile.</span><span class="sxs-lookup"><span data-stu-id="78706-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooan Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="78706-110">Uygulama toouse Service Bus yapılandırın</span><span class="sxs-lookup"><span data-stu-id="78706-110">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="78706-111">Hizmet veri yolu, toouse hello Node.js Azure paketini indirin.</span><span class="sxs-lookup"><span data-stu-id="78706-111">toouse Service Bus, download hello Node.js Azure package.</span></span> <span data-ttu-id="78706-112">Bu paket hello Service Bus REST Hizmetleri ile iletişim kitaplıkları kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="78706-112">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="78706-113">Düğüm paketi Yöneticisi (NPM) tooobtain hello paketini kullanın</span><span class="sxs-lookup"><span data-stu-id="78706-113">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="78706-114">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows) **Terminal** (Mac) veya **Bash** (UNIX) örnek uygulamanızı oluşturulduğu toohello klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="78706-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="78706-115">Tür **npm yükleme azure** hello komut penceresinde, neden çıktı aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="78706-115">Type **npm install azure** in hello command window, which should result in hello following output:</span></span>

   ```
       azure@0.7.5 node_modules\azure
   ├── dateformat@1.0.2-1.2.3
   ├── xmlbuilder@0.4.2
   ├── node-uuid@1.2.0
   ├── mime@1.2.9
   ├── underscore@1.4.4
   ├── validator@1.1.1
   ├── tunnel@0.0.2
   ├── wns@0.5.3
   ├── xml2js@0.2.7 (sax@0.5.2)
   └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
   ```
3. <span data-ttu-id="78706-116">Merhaba el ile çalıştırabilirsiniz **ls** komutu tooverify, bir **düğümü\_modülleri** klasörü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="78706-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="78706-117">Bu klasöre Bul **azure** tooaccess Service Bus konu başlıklarını ihtiyacınız hello kitaplıklarını içeren paket.</span><span class="sxs-lookup"><span data-stu-id="78706-117">Inside that folder find the **azure** package, which contains hello libraries you need tooaccess Service Bus topics.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="78706-118">İçeri aktarma hello Modülü</span><span class="sxs-lookup"><span data-stu-id="78706-118">Import hello module</span></span>
<span data-ttu-id="78706-119">Not Defteri'nde veya başka bir metin düzenleyicisi kullanarak eklemek hello toohello üstündeki aşağıdaki hello **server.js** hello uygulama dosyası:</span><span class="sxs-lookup"><span data-stu-id="78706-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="78706-120">Hizmet veri yolu bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="78706-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="78706-121">Hello Azure modül okur hello ortam değişkenleri `AZURE_SERVICEBUS_NAMESPACE` ve `AZURE_SERVICEBUS_ACCESS_KEY` için bilgi tooconnect tooService veri yolu gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="78706-121">hello Azure module reads hello environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required tooconnect tooService Bus.</span></span> <span data-ttu-id="78706-122">Bu ortam değişkenleri ayarlanmamışsa çağrılırken hello hesap bilgileri belirtmelisiniz `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="78706-122">If these environment variables are not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="78706-123">Azure bulut hizmeti için hello ortam değişkenlerini ayarlama örneği için bkz: [depolama Node.js bulut hizmetiyle][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="78706-123">For an example of setting hello environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="78706-124">Bir Azure Web sitesi için hello ortam değişkenlerini ayarlama örneği için bkz: [Node.js Web uygulaması depolama ile][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="78706-124">For an example of setting hello environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="78706-125">Konu başlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="78706-125">Create a topic</span></span>
<span data-ttu-id="78706-126">Merhaba **ServiceBusService** nesne konuları ile toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="78706-126">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="78706-127">Aşağıdaki kod oluşturur bir **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="78706-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="78706-128">Merhaba en üstüne yakın eklemek **server.js** hello deyimi tooimport hello azure modülü sonra dosyayı:</span><span class="sxs-lookup"><span data-stu-id="78706-128">Add it near the top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="78706-129">Çağırarak `createTopicIfNotExists` hello üzerinde **ServiceBusService** nesnesi, hello belirtilen konu döndürülecek (varsa) veya hello belirtilen ada sahip yeni bir konu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="78706-129">By calling `createTopicIfNotExists` on hello **ServiceBusService** object, hello specified topic will be returned (if it exists,) or a new topic with hello specified name will be created.</span></span> <span data-ttu-id="78706-130">Merhaba aşağıdaki kod kullanır `createTopicIfNotExists` toocreate veya toohello konu adlı bağlantı `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="78706-130">hello following code uses `createTopicIfNotExists` toocreate or connect toohello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="78706-131">Merhaba `createServiceBusService` yöntemi de ileti yaşam süresi veya en büyük konu boyutu gibi toooverride varsayılan konu ayarlarını etkinleştir ek seçenekleri destekler.</span><span class="sxs-lookup"><span data-stu-id="78706-131">hello `createServiceBusService` method also supports additional options, which enable you toooverride default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="78706-132">Merhaba aşağıdaki örnek hello en fazla konu boyutu too5GB süresi olan 1 dakika toolive ayarlar:</span><span class="sxs-lookup"><span data-stu-id="78706-132">hello following example sets hello maximum topic size too5GB with a time toolive of 1 minute:</span></span>

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="78706-133">Filtreler</span><span class="sxs-lookup"><span data-stu-id="78706-133">Filters</span></span>
<span data-ttu-id="78706-134">İsteğe bağlı filtreleme operations kullanılarak gerçekleştirilen uygulanan toooperations olabilir **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="78706-134">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="78706-135">İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. Filtreleri hello imza yöntemiyle uygulayan nesneler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="78706-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="78706-136">Yöntem çağrıları hello Hello isteği seçenekleri ön işleme gerçekleştirdikten sonra `next`, bir geri çağırma imza aşağıdaki hello ile geçirme:</span><span class="sxs-lookup"><span data-stu-id="78706-136">After performing preprocessing on hello request options, hello method calls `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="78706-137">İşleme hello sonra bu geri çağırma `returnObject` (Merhaba isteği toohello sunucudan yanıt hello) hello geri çağırma tooeither gereken diğer filtreleri işleme toocontinue varsa sonraki çağırma veya çağırma `finalCallback` Aksi takdirde tooend hello Hizmet başlatma.</span><span class="sxs-lookup"><span data-stu-id="78706-137">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or invoke `finalCallback` otherwise, tooend hello service invocation.</span></span>

<span data-ttu-id="78706-138">Yeniden deneme mantığını uygulaması iki filtre hello Node.js için Azure SDK ile birlikte **ExponentialRetryPolicyFilter** ve **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="78706-138">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="78706-139">Merhaba aşağıdaki oluşturur bir **ServiceBusService** hello kullanan nesneyi **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="78706-139">hello following creates a **ServiceBusService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="78706-140">Abonelikleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="78706-140">Create subscriptions</span></span>
<span data-ttu-id="78706-141">Konu aboneliklerini ayrıca hello ile oluşturulan **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="78706-141">Topic subscriptions are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="78706-142">Abonelikler adlandırılır ve hello toohello aboneliğin sanal kuyruğuna teslim edilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.</span><span class="sxs-lookup"><span data-stu-id="78706-142">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="78706-143">Abonelikleri kalıcı ve tooexist ya da bunlar kadar devam eder veya hello konu bunların ilişkili silinir.</span><span class="sxs-lookup"><span data-stu-id="78706-143">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="78706-144">Uygulama mantığı toocreate bir abonelik içeriyorsa, ilk hello abonelik zaten kullanarak olup olmadığını kontrol edin `getSubscription` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="78706-144">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="78706-145">Merhaba varsayılan (MatchAll) filtreyle abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="78706-145">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="78706-146">Merhaba **MatchAll** yeni bir abonelik oluşturulurken filtre belirtilmeyen varsa, kullanılan hello varsayılan filtre filtredir.</span><span class="sxs-lookup"><span data-stu-id="78706-146">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="78706-147">Ne zaman hello **MatchAll** filtre kullanıldığında, tüm iletileri yayımlanan toohello konu aboneliğin sanal kuyruğuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="78706-147">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="78706-148">Merhaba aşağıdaki örnekte 'AllMessages' adlı bir abonelik oluşturur ve kullanır hello varsayılan **MatchAll** Filtresi.</span><span class="sxs-lookup"><span data-stu-id="78706-148">hello following example creates a subscription named 'AllMessages' and uses hello default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="78706-149">Filtre içeren abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="78706-149">Create subscriptions with filters</span></span>
<span data-ttu-id="78706-150">Ayrıca hangi iletilerin tooa konu içinde belirli konu aboneliği göstermelidir gönderilen tooscope izin filtreler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78706-150">You can also create filters that allow you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="78706-151">Merhaba en esnek filtre abonelikler tarafından desteklenen türünde **SqlFilter**, SQL92 alt kümesi uygular.</span><span class="sxs-lookup"><span data-stu-id="78706-151">hello most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="78706-152">SQL filtreleri yayımlanan toohello konu hello iletilerinin hello özelliklerini çalışır.</span><span class="sxs-lookup"><span data-stu-id="78706-152">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="78706-153">Merhaba SQL Filtresi ile kullanılabilen hello ifadeler hakkında daha fazla ayrıntı için gözden [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sözdizimi.</span><span class="sxs-lookup"><span data-stu-id="78706-153">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="78706-154">Filtreler eklenebilir tooa abonelik hello kullanarak `createRule` hello yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="78706-154">Filters can be added tooa subscription by using hello `createRule` method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="78706-155">Bu yöntem yeni filtreleri tooan varolan abonelik eklemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="78706-155">This method allows you to add new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="78706-156">Merhaba varsayılan filtre otomatik olarak uygulandığından tooall yeni abonelikler, ilk hello varsayılan filtreyi kaldırmalısınız veya **MatchAll** belirttiğiniz diğer filtreleri geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="78706-156">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="78706-157">Hello kullanarak hello varsayılan kural kaldırabilirsiniz `deleteRule` yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="78706-157">You can remove hello default rule by using hello `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="78706-158">Merhaba aşağıdaki örnek adlı bir abonelik oluşturulur `HighMessages` ile bir **SqlFilter** özel iletileri yalnızca seçer `messagenumber` özelliği 3'ten büyük:</span><span class="sxs-lookup"><span data-stu-id="78706-158">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="78706-159">Benzer şekilde, hello aşağıdaki örnek adlı bir abonelik oluşturur `LowMessages` ile bir **SqlFilter** olan iletiler yalnızca seçer bir `messagenumber` özelliği daha az veya bu değere eşit too3:</span><span class="sxs-lookup"><span data-stu-id="78706-159">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="78706-160">Ne zaman bir ileti artık gönderilir çok`MyTopic`, her zaman alıcılara toohello teslim `AllMessages` konu aboneliği ve abone olunan seçmeli olarak teslim tooreceivers toohello `HighMessages` ve `LowMessages` konu abonelikleri (Merhaba ileti içeriği bağlı olarak).</span><span class="sxs-lookup"><span data-stu-id="78706-160">When a message is now sent too`MyTopic`, it will always be delivered to receivers subscribed toohello `AllMessages` topic subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="how-toosend-messages-tooa-topic"></a><span data-ttu-id="78706-161">Nasıl toosend tooa konu iletileri</span><span class="sxs-lookup"><span data-stu-id="78706-161">How toosend messages tooa topic</span></span>
<span data-ttu-id="78706-162">toosend ileti tooa Service Bus konu, uygulamanızı kullanmalıdır `sendTopicMessage` hello yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="78706-162">toosend a message tooa Service Bus topic, your application must use the `sendTopicMessage` method of hello **ServiceBusService** object.</span></span>
<span data-ttu-id="78706-163">Gönderilen iletileri tooService veri yolu konuları **BrokeredMessage** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="78706-163">Messages sent tooService Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="78706-164">**BrokeredMessage** nesneleri olan bir standart özellikler kümesi (gibi `Label` ve `TimeToLive`), kullanılan toohold özel uygulamaya özgü özellikler sözlüğü bir ve dize verileri gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="78706-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="78706-165">Bir uygulama hello bir dize değeri geçirerek hello hello ileti gövdesini ayarlayabilir `sendTopicMessage` ve gereken tüm standart özellikleri varsayılan değerlerle doldurulmuş.</span><span class="sxs-lookup"><span data-stu-id="78706-165">An application can set hello body of hello message by passing a string value to hello `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="78706-166">Merhaba aşağıdaki örnekte nasıl toosend beş için sınama iletilerini gösterir `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="78706-166">hello following example demonstrates how toosend five test messages to `MyTopic`.</span></span> <span data-ttu-id="78706-167">Bu hello Not `messagenumber` her ileti özelliği değeri değişir hello döngü hello yinelemesi (Bu alacak abonelikleri belirler):</span><span class="sxs-lookup"><span data-stu-id="78706-167">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

<span data-ttu-id="78706-168">Service Bus konu başlıklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="78706-168">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="78706-169">Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="78706-169">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="78706-170">Merhaba konu başlığında tutulan ileti sayısına bir sınır yoktur ancak konu başlığı tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="78706-170">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="78706-171">Bu konu başlığı boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="78706-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="78706-172">Abonelikten ileti alma</span><span class="sxs-lookup"><span data-stu-id="78706-172">Receive messages from a subscription</span></span>
<span data-ttu-id="78706-173">İletileri kullanarak bir abonelik alınan `receiveSubscriptionMessage` hello yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="78706-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="78706-174">Varsayılan olarak, bunlar okurken iletiler hello abonelikten silinir; Ancak, (Özet) okuma ve kilitleme selamlama iletisine hello isteğe bağlı parametre ayarı tarafından hello abonelikten silmeden `isPeekLock` çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="78706-174">By default, messages are deleted from hello subscription as they are read; however, you can read (peek) and lock hello message without deleting it from hello subscription by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="78706-175">Okuma ve alma işleminin parçası hello en basit modeldir ve uygulamanın bir hatanın hello Olay iletisinde işlenmiyor dayanabileceği senaryoları için en iyi şekilde hello iletisi siliniyor hello varsayılan davranışı.</span><span class="sxs-lookup"><span data-stu-id="78706-175">hello default behavior of reading and deleting hello message as part of the receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="78706-176">toounderstand Bu, tüketici sorunları hello isteği alma bir senaryo düşünün ve işlemeden önce çöküyor.</span><span class="sxs-lookup"><span data-stu-id="78706-176">toounderstand this, consider a scenario in which the consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="78706-177">Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.</span><span class="sxs-lookup"><span data-stu-id="78706-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="78706-178">Merhaba, `isPeekLock` parametresi çok ayarlanırsa**true**, hello alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur.</span><span class="sxs-lookup"><span data-stu-id="78706-178">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="78706-179">Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur.</span><span class="sxs-lookup"><span data-stu-id="78706-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span>
<span data-ttu-id="78706-180">Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), çağırarak hello alma işleminin ikinci aşamasını tamamlar **deleteMessage** yöntemi ve ileti toobe sağlama parametre olarak silindi.</span><span class="sxs-lookup"><span data-stu-id="78706-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of the receive process by calling **deleteMessage** method and providing the message toobe deleted as a parameter.</span></span> <span data-ttu-id="78706-181">Merhaba **deleteMessage** yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello abonelikten Kaldır.</span><span class="sxs-lookup"><span data-stu-id="78706-181">hello **deleteMessage** method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="78706-182">Merhaba aşağıdaki örnekte nasıl iletilerin alındığını ve işlenen kullanarak gösteren `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="78706-182">hello following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="78706-183">Merhaba örnek ilk alır ve bir ileti hello 'LowMessages' abonelik ' siler ve sonra abonelik 'HighMessages' hello kullanarak bir ileti alır `isPeekLock` tootrue ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78706-183">hello example first receives and deletes a message from hello 'LowMessages' subscription, and then receives a message from hello 'HighMessages' subscription using `isPeekLock` set tootrue.</span></span> <span data-ttu-id="78706-184">Ardından hello kullanarak iletiyi siler `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="78706-184">It then deletes hello message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="78706-185">Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri</span><span class="sxs-lookup"><span data-stu-id="78706-185">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="78706-186">Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar.</span><span class="sxs-lookup"><span data-stu-id="78706-186">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="78706-187">Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlockMessage` yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="78706-187">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="78706-188">Bu hizmet veri yolu toounlock hello abonelik içindeki ileti neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.</span><span class="sxs-lookup"><span data-stu-id="78706-188">This will cause Service Bus toounlock the message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="78706-189">Ayrıca abonelikte kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus hello iletinin kilidini açar hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe yapar.</span><span class="sxs-lookup"><span data-stu-id="78706-189">There is also a timeout associated with a message locked within the subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="78706-190">Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `deleteMessage` yöntemi çağrıldıktan sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="78706-190">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="78706-191">Bu genellikle adlandırılır *en az bir kez işleme*, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="78706-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="78706-192">Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="78706-192">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="78706-193">Bu genellikle kullanılarak elde edilen **MessageID** teslimat denemelerinde hello iletinin özelliği.</span><span class="sxs-lookup"><span data-stu-id="78706-193">This is often achieved using the **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="78706-194">Konu başlıklarını ve abonelikleri silme</span><span class="sxs-lookup"><span data-stu-id="78706-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="78706-195">Konu başlıkları ve abonelikler kalıcıdır ve açıkça olmalıdır hello aracılığıyla ya da silinmiş [Azure portal] [ Azure portal] veya program aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="78706-195">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="78706-196">Merhaba aşağıdaki örnekte nasıl toodelete hello konu adlı gösteren `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="78706-196">hello following example demonstrates how toodelete hello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="78706-197">Konu başlığı silindiğinde hello konu başlığıyla kaydedilen tüm abonelikler de silinir.</span><span class="sxs-lookup"><span data-stu-id="78706-197">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="78706-198">Ayrıca, abonelikler bağımsız olarak da silinebilir.</span><span class="sxs-lookup"><span data-stu-id="78706-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="78706-199">Aşağıdaki örnek, nasıl bir abonelik toodelete adlı gösterir `HighMessages` hello gelen `MyTopic` konu:</span><span class="sxs-lookup"><span data-stu-id="78706-199">The following example shows how toodelete a subscription named `HighMessages` from hello `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="78706-200">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="78706-200">Next Steps</span></span>
<span data-ttu-id="78706-201">Artık Service Bus konu başlıklarını hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="78706-201">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="78706-202">Bkz: [kuyruklar, konu başlıkları ve abonelikler][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="78706-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="78706-203">[SqlFilter][SqlFilter] için API başvurusu.</span><span class="sxs-lookup"><span data-stu-id="78706-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="78706-204">Merhaba ziyaret [düğümü için Azure SDK] [ Azure SDK for Node] github'daki.</span><span class="sxs-lookup"><span data-stu-id="78706-204">Visit hello [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[oluşturma ve bir Node.js uygulaması tooan Azure Web sitesi dağıtma]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md

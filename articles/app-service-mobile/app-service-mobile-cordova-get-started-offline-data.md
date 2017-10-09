---
title: "aaaEnable çevrimdışı eşitleme Azure mobil uygulamanızın (Cordova) | Microsoft Docs"
description: "Bilgi nasıl toouse mobil uygulama hizmeti toocache ve eşitleme çevrimdışı veri Cordova uygulamanızda"
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="c02b2-103">Cordova mobil uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c02b2-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="c02b2-104">Bu öğretici Azure Mobile Apps hello çevrimdışı eşitleme özelliği için Cordova tanıtır.</span><span class="sxs-lookup"><span data-stu-id="c02b2-104">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="c02b2-105">Çevrimdışı eşitleme sağlayan bir mobil uygulama ile son kullanıcılar toointeract&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.</span><span class="sxs-lookup"><span data-stu-id="c02b2-105">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="c02b2-106">Değişiklikler yerel bir veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="c02b2-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="c02b2-107">Merhaba aygıt yeniden çevrimiçi olduktan sonra bu değişiklikleri hello uzak hizmeti ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="c02b2-107">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="c02b2-108">Öğreticiyi tamamladığınızda oluşturduğunuz mobil uygulamalar hello için bu öğreticiyi hello Cordova hızlı başlangıç çözüm üzerinde temel [Apache Cordova Hızlı Başlangıç].</span><span class="sxs-lookup"><span data-stu-id="c02b2-108">This tutorial is based on hello Cordova quickstart solution for Mobile Apps that you create when you complete hello tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="c02b2-109">Bu öğreticide, hello hızlı başlangıç çözüm tooadd çevrimdışı özelliklerini Azure Mobile Apps güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c02b2-109">In this tutorial, you update hello quickstart solution tooadd offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="c02b2-110">Biz de hello çevrimdışı özgü hello uygulama kodunda vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="c02b2-110">We also highlight hello offline-specific code in hello app.</span></span>

<span data-ttu-id="c02b2-111">Merhaba çevrimdışı eşitleme özelliği hakkında daha fazla toolearn hello konusuna bakın [Azure Mobile Apps çevrimdışı veri eşitleme].</span><span class="sxs-lookup"><span data-stu-id="c02b2-111">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="c02b2-112">Merhaba API kullanım ayrıntıları için bkz [API belgelerine](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="c02b2-112">For details of API usage, see hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-toohello-quickstart-solution"></a><span data-ttu-id="c02b2-113">Çevrimdışı eşitleme toohello hızlı başlangıç çözüme ekleyin</span><span class="sxs-lookup"><span data-stu-id="c02b2-113">Add offline sync toohello quickstart solution</span></span>
<span data-ttu-id="c02b2-114">Merhaba çevrimdışı eşitleme kodu toohello uygulama eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c02b2-114">hello offline sync code must be added toohello app.</span></span> <span data-ttu-id="c02b2-115">Çevrimdışı eşitleme hello Azure Mobile Apps eklentisi hello projeye dahil bağlandığınızda tooyour uygulama otomatik olarak eklenen hello cordova sqlite depolama eklentisi gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="c02b2-115">Offline sync requires hello cordova-sqlite-storage plugin, which automatically gets added tooyour app when hello Azure Mobile Apps plugin is included in hello project.</span></span> <span data-ttu-id="c02b2-116">Merhaba hızlı başlangıç projesi bu eklenti her ikisi de içerir.</span><span class="sxs-lookup"><span data-stu-id="c02b2-116">hello Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="c02b2-117">Visual Studio'nun Çözüm Gezgini'nde, index.js açın ve aşağıdaki kodu hello değiştirin</span><span class="sxs-lookup"><span data-stu-id="c02b2-117">In Visual Studio's Solution Explorer, open index.js and replace hello following code</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    <span data-ttu-id="c02b2-118">Bu kodu:</span><span class="sxs-lookup"><span data-stu-id="c02b2-118">with this code:</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. <span data-ttu-id="c02b2-119">Ardından, kod aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c02b2-119">Next, replace hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="c02b2-120">Bu kodu:</span><span class="sxs-lookup"><span data-stu-id="c02b2-120">with this code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    <span data-ttu-id="c02b2-121">Merhaba önceki kod eklemeler hello yerel deposunu başlatmak ve kullanılan hello sütun değerlerini eşleşen yerel bir tablo tanımlayın Azure son yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="c02b2-121">hello preceding code additions initialize hello local store and define a local table that matches hello column values used in your Azure back end.</span></span> <span data-ttu-id="c02b2-122">(Bu kodda tüm sütun değerlerini tooinclude gerekmez.)  Merhaba `version` alan hello mobil arka uç tarafından korunur ve Çakışma çözümlemesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c02b2-122">(You don't need tooinclude all column values in this code.)  hello `version` field is maintained by hello mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="c02b2-123">Bir başvuru toohello eşitleme bağlamı çağırarak alma **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="c02b2-123">You get a reference toohello sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="c02b2-124">Merhaba eşitleme bağlamı tablo ilişkileri izleme ve bir istemci uygulaması değiştiren tüm tablolarda değişiklikleri Ftp'den korunmasına yardımcı olur `.push()` olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="c02b2-124">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="c02b2-125">Merhaba uygulama tooyour mobil uygulamayı uygulama URL'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c02b2-125">Update hello application URL tooyour Mobile App application URL.</span></span>

4. <span data-ttu-id="c02b2-126">Ardından, bu kodu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c02b2-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    <span data-ttu-id="c02b2-127">Bu kodu:</span><span class="sxs-lookup"><span data-stu-id="c02b2-127">with this code:</span></span>

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="c02b2-128">Merhaba önceki kod hello eşitleme bağlamını başlatır ve ardından (yerine getTable) getSyncTable tooget başvuru toohello yerel tablo çağırır.</span><span class="sxs-lookup"><span data-stu-id="c02b2-128">hello preceding code initializes hello sync context and then calls getSyncTable (instead of getTable) tooget a reference toohello local table.</span></span>

    <span data-ttu-id="c02b2-129">Kod bu kullanır hello yerel veritabanı tüm oluşturmak okuma, güncelleştirme ve Sil (CRUD) tablo işlemleri.</span><span class="sxs-lookup"><span data-stu-id="c02b2-129">This code uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="c02b2-130">Bu örnekte basit hata eşitleme çakışmalarını işleme gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="c02b2-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="c02b2-131">Gerçek bir uygulamada işlemek ağ koşulları, sunucu çakışmaları ve diğerleri gibi çeşitli hatalar hello.</span><span class="sxs-lookup"><span data-stu-id="c02b2-131">A real application would handle hello various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="c02b2-132">Kod örnekleri için bkz: Merhaba [çevrimdışı eşitleme örnek].</span><span class="sxs-lookup"><span data-stu-id="c02b2-132">For code examples, see hello [offline sync sample].</span></span>

5. <span data-ttu-id="c02b2-133">Ardından, bu işlevi tooperform hello gerçek eşitleme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c02b2-133">Next, add this function tooperform hello actual sync.</span></span>

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="c02b2-134">Toopush toohello mobil uygulama arka ucu çağırarak değiştiğinde karar **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="c02b2-134">You decide when toopush changes toohello Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="c02b2-135">Örneğin, çağırabilirsiniz **syncBackend** düğmesi olay işleyicisi bağlı tooa Eşitle düğmesi içinde.</span><span class="sxs-lookup"><span data-stu-id="c02b2-135">For example, you could call **syncBackend** in a button event handler tied tooa sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="c02b2-136">Çevrimdışı eşitleme konuları</span><span class="sxs-lookup"><span data-stu-id="c02b2-136">Offline sync considerations</span></span>

<span data-ttu-id="c02b2-137">Merhaba örnek hello **itme** yöntemi **syncContext** yalnızca uygulama başlangıç oturum açma için hello geri çağırma işlevi adı verilir.</span><span class="sxs-lookup"><span data-stu-id="c02b2-137">In hello sample, hello **push** method of **syncContext** is only called on app startup in hello callback function for login.</span></span>  <span data-ttu-id="c02b2-138">Gerçek dünya uygulamada el ile tetiklenen bu eşitleme işlevine veya hello ağ durumu değiştiğinde de yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c02b2-138">In a real-world application, you could also make this sync functionality triggered manually or when hello network state changes.</span></span>

<span data-ttu-id="c02b2-139">Çekme beklemede olan bir tabloda karşı çalıştırıldığında yerel güncelleştirmeleri bir anında iletme işlemi otomatik olarak Tetikleyicileri çekme hello bağlam tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="c02b2-139">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="c02b2-140">Yenileme, ekleme ve bu örnek öğelerde Tamamlanıyor, atlayabilirsiniz olduğunda açık hello **itme** yedek olabileceğinden çağırın.</span><span class="sxs-lookup"><span data-stu-id="c02b2-140">When refreshing, adding, and completing items in this sample, you can omit hello explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="c02b2-141">Sağlanan hello kodda hello uzak Todoıtem tablosu tüm kayıtları seçmeleri istenir, ancak bu da olası toofilter kayıtları sorgu kimliği ve sorgu geçirerek çok**itme**.</span><span class="sxs-lookup"><span data-stu-id="c02b2-141">In hello provided code, all records in hello remote todoItem table are queried, but it is also possible toofilter records by passing a query id and query too**push**.</span></span> <span data-ttu-id="c02b2-142">Daha fazla bilgi için hello bölümüne bakın *Artımlı eşitleme* içinde [Azure Mobile Apps çevrimdışı veri eşitleme].</span><span class="sxs-lookup"><span data-stu-id="c02b2-142">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="c02b2-143">(İsteğe bağlı) Kimlik doğrulaması devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="c02b2-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="c02b2-144">Yok tooset çevrimdışı eşitleme sınama önce kimlik doğrulamasını kurmak istediğiniz, oturum açma için hello geri çağırma işlevi çıkışı açıklama, ancak içinde hello kod bırakın hello geri çağırma işlevi uncommented.</span><span class="sxs-lookup"><span data-stu-id="c02b2-144">If you don't want tooset up authentication before testing offline sync, comment out hello callback function for login, but leave hello code inside hello callback function uncommented.</span></span>  <span data-ttu-id="c02b2-145">Merhaba oturum açma çizgi yorum sonra hello kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="c02b2-145">After commenting out hello login lines, hello code follows:</span></span>

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="c02b2-146">Merhaba uygulama eşitlemeler hello hello uygulama çalıştırdığınızda Azure arka uç ile şimdi.</span><span class="sxs-lookup"><span data-stu-id="c02b2-146">Now, hello app syncs with hello Azure backend when you run hello app.</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="c02b2-147">Merhaba istemci uygulaması çalıştırın</span><span class="sxs-lookup"><span data-stu-id="c02b2-147">Run hello client app</span></span>
<span data-ttu-id="c02b2-148">Şu anda etkin çevrimdışı eşitleme ile Merhaba istemci uygulaması en az bir kez hello yerel deposu veritabanı doldurmak için her platformda çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c02b2-148">With offline sync now enabled, you can run hello client application at least once on each platform to populate hello local store database.</span></span> <span data-ttu-id="c02b2-149">Daha sonra çevrimdışı bir senaryo benzetimini hello uygulama çevrimdışı durumdayken hello verileri ve hello Yerel Depodaki değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c02b2-149">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="optional-test-hello-sync-behavior"></a><span data-ttu-id="c02b2-150">(İsteğe bağlı) Test hello eşitleme davranışı</span><span class="sxs-lookup"><span data-stu-id="c02b2-150">(Optional) Test hello sync behavior</span></span>
<span data-ttu-id="c02b2-151">Bu bölümde, arka ucunuz için geçersiz uygulama URL'si kullanarak hello istemci projesi toosimulate çevrimdışı bir senaryo değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c02b2-151">In this section, you modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="c02b2-152">Veri öğeleri ekleyin veya değiştirildiğinde, bu değişiklikler yerel depoda tutulur, ancak hello bağlantı yeniden kurulur kurulmaz kadar eşitlenen toohello arka uç veri deposu olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="c02b2-152">When you add or change data items, these changes are held in the local store, but are not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="c02b2-153">Çözüm Gezgini hello, hello index.js proje dosyasını açın ve koddan hello gibi geçersiz bir URL'ye hello uygulama URL'si toopoint değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c02b2-153">In hello Solution Explorer, open hello index.js project file and change hello application URL toopoint to  an invalid URL, like hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="c02b2-154">Merhaba CSP index.HTML içinde güncelleştirme `<meta>` öğeyle hello aynı geçersiz URL.</span><span class="sxs-lookup"><span data-stu-id="c02b2-154">In index.html, update hello CSP `<meta>` element with hello same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="c02b2-155">Derleme ve hello istemci uygulamayı çalıştırın ve hello uygulama hello arka ucuyla oturum açtıktan sonra eşitleme girişiminde bulunduğunda bir özel durum hello konsolunda kaydedilir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c02b2-155">Build and run hello client app and notice that an exception is logged in hello console when hello app attempts to sync with hello backend after login.</span></span> <span data-ttu-id="c02b2-156">Bunlar toohello mobil arka uç gönderilen kadar eklediğiniz tüm yeni öğeler hello yerel depoda yalnızca mevcut.</span><span class="sxs-lookup"><span data-stu-id="c02b2-156">Any new items you add exist only in hello local store until they are pushed toohello mobile backend.</span></span> <span data-ttu-id="c02b2-157">Merhaba istemci uygulaması bağlı toohello arka uç olduğu gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="c02b2-157">hello client app behaves as if it is connected toohello backend.</span></span>

4. <span data-ttu-id="c02b2-158">Merhaba uygulamasını kapatın ve oluşturduğunuz hello yeni öğeler kalıcı toohello yerel deposu olduğunu tooverify yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="c02b2-158">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>

5. <span data-ttu-id="c02b2-159">(İsteğe bağlı) Visual Studio tooview hello arka uç veritabanı hello verilerde değişmediğini, Azure SQL veritabanı tablosu toosee kullanın.</span><span class="sxs-lookup"><span data-stu-id="c02b2-159">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="c02b2-160">Visual Studio'da açın **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="c02b2-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="c02b2-161">Tooyour veritabanında gidin **Azure**->**SQL veritabanları**.</span><span class="sxs-lookup"><span data-stu-id="c02b2-161">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="c02b2-162">Veritabanınıza sağ tıklatıp **SQL Server nesne Gezgini'nde Aç**.</span><span class="sxs-lookup"><span data-stu-id="c02b2-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="c02b2-163">Şimdi tooyour SQL veritabanı tablosunda ve içeriği göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c02b2-163">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a><span data-ttu-id="c02b2-164">(İsteğe bağlı) Test hello yeniden bağlanmayı tooyour mobil arka uç</span><span class="sxs-lookup"><span data-stu-id="c02b2-164">(Optional) Test hello reconnection tooyour mobile backend</span></span>

<span data-ttu-id="c02b2-165">Bu bölümde, çevrimiçi duruma gelmeye hello uygulama benzetim hello uygulama toohello mobil arka uç, yeniden bağlanın.</span><span class="sxs-lookup"><span data-stu-id="c02b2-165">In this section, you reconnect hello app toohello mobile backend, which simulates hello app coming back to an online state.</span></span> <span data-ttu-id="c02b2-166">Oturum açtığınızda, eşitlenen tooyour mobil arka uç verilerdir.</span><span class="sxs-lookup"><span data-stu-id="c02b2-166">When you log in, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="c02b2-167">İndex.js yeniden açın ve hello uygulama URL'si geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c02b2-167">Reopen index.js and restore hello application URL.</span></span>
2. <span data-ttu-id="c02b2-168">İndex.HTML yeniden açın ve hello CSP hello uygulama URL'SİNDE düzeltmek `<meta>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="c02b2-168">Reopen index.html and correct hello application URL in hello CSP `<meta>` element.</span></span>
3. <span data-ttu-id="c02b2-169">Yeniden oluşturma ve hello istemci uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c02b2-169">Rebuild and run hello client app.</span></span> <span data-ttu-id="c02b2-170">Merhaba uygulama toosync hello mobil uygulama arka ucu ile oturum açtıktan sonra çalışır.</span><span class="sxs-lookup"><span data-stu-id="c02b2-170">hello app attempts toosync with hello mobile app backend after login.</span></span> <span data-ttu-id="c02b2-171">Hiçbir özel durum hello hata ayıklama konsolunda tutulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c02b2-171">Verify that no exceptions are logged in hello debug console.</span></span>
4. <span data-ttu-id="c02b2-172">(İsteğe bağlı) SQL Server Nesne Gezgini veya Fiddler gibi bir REST araç kullanarak veri görünümü hello güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="c02b2-172">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="c02b2-173">Bildirim hello veri hello arka uç veritabanı ve hello yerel deposu arasında eşitlendi.</span><span class="sxs-lookup"><span data-stu-id="c02b2-173">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="c02b2-174">Merhaba veri hello yerel deposu hello veritabanı arasında eşitlenen ve uygulamanızı değilken eklediğiniz hello öğelerini içeren dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c02b2-174">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c02b2-175">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c02b2-175">Additional resources</span></span>
* <span data-ttu-id="c02b2-176">[Azure Mobile Apps çevrimdışı veri eşitleme]</span><span class="sxs-lookup"><span data-stu-id="c02b2-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="c02b2-177">[Apache Cordova için Visual Studio Araçları]</span><span class="sxs-lookup"><span data-stu-id="c02b2-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="c02b2-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c02b2-178">Next steps</span></span>
* <span data-ttu-id="c02b2-179">Çevrimdışı eşitleme özelliklerini hello çakışma çözümlemesinde gibi daha gelişmiş gözden [çevrimdışı eşitleme örnek]</span><span class="sxs-lookup"><span data-stu-id="c02b2-179">Review more advanced offline sync features such as conflict resolution in hello [offline sync sample]</span></span>
* <span data-ttu-id="c02b2-180">Gözden hello çevrimdışı eşitleme hello API başvuru [API belgelerine](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="c02b2-180">Review hello offline sync API reference in hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[Apache Cordova Hızlı Başlangıç]: app-service-mobile-cordova-get-started.md
[çevrimdışı eşitleme örnek]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[Azure Mobile Apps çevrimdışı veri eşitleme]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Apache Cordova için Visual Studio Araçları]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md

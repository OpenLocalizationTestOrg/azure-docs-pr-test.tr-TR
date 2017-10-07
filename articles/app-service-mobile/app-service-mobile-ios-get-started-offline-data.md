---
title: "iOS mobil uygulamaları ile aaaEnable çevrimdışı eşitleme | Microsoft Docs"
description: "Bilgi nasıl toouse Azure App Service mobile apps toocache ve eşitleme çevrimdışı verileri iOS uygulamaları."
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="4dbe1-103">Çevrimdışı iOS mobil uygulamaları ile eşitlemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="4dbe1-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="4dbe1-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4dbe1-104">Overview</span></span>
<span data-ttu-id="4dbe1-105">Bu öğretici, iOS için Azure App Service'in hello Mobile Apps özelliğini çevrimdışı eşitleme kapsar.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-105">This tutorial covers offline syncing with hello Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="4dbe1-106">Çevrimdışı eşitleme son kullanıcılar ile mobil uygulama tooview ile etkileşim, ekleyin veya bile ağ bağlantısı olduğunda veri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-106">With offline syncing end-users can interact with a mobile app tooview, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="4dbe1-107">Değişiklikler yerel bir veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-107">Changes are stored in a local database.</span></span> <span data-ttu-id="4dbe1-108">Merhaba cihaz yeniden çevrimiçi olduktan sonra hello değişiklikler hello uzak arka ucu ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-108">After hello device is back online, hello changes are synced with hello remote back end.</span></span>

<span data-ttu-id="4dbe1-109">Mobile Apps ile ilk deneyiminizi varsa hello öğretici ilk tamamlanmalıdır [iOS uygulaması oluştur].</span><span class="sxs-lookup"><span data-stu-id="4dbe1-109">If this is your first experience with Mobile Apps, you should first complete hello tutorial [Create an iOS App].</span></span> <span data-ttu-id="4dbe1-110">Merhaba indirilen hızlı başlangıç sunucu projesi kullanmazsanız hello veri erişimi uzantı paketleri tooyour projesi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-110">If you do not use hello downloaded quick-start server project, you must add hello data-access extension packages tooyour project.</span></span> <span data-ttu-id="4dbe1-111">Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4dbe1-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="4dbe1-112">toolearn hello çevrimdışı eşitleme özelliği hakkında daha fazla bilgi görmek [mobil uygulamalarda çevrimdışı veri eşitlemeye].</span><span class="sxs-lookup"><span data-stu-id="4dbe1-112">toolearn more about hello offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="4dbe1-113"><a name="review-sync"></a>Merhaba istemci eşitleme kodu gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="4dbe1-113"><a name="review-sync"></a>Review hello client sync code</span></span>
<span data-ttu-id="4dbe1-114">Merhaba indirdiğiniz hello istemci projesi [iOS uygulaması oluştur] öğretici zaten bir yerel çekirdek veri tabanlı veritabanı çevrimdışı eşitlemeyi destekleyen kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-114">hello client project that you downloaded for hello [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="4dbe1-115">Bu bölümde hello Eğitmen kodu zaten dahil özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-115">This section summarizes what is already included in hello tutorial code.</span></span> <span data-ttu-id="4dbe1-116">Merhaba özelliği kavramsal bir genel bakış için bkz: [mobil uygulamalarda çevrimdışı veri eşitlemeye].</span><span class="sxs-lookup"><span data-stu-id="4dbe1-116">For a conceptual overview of hello feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="4dbe1-117">Merhaba ağ erişilemez durumda olduğunda bile Mobile Apps hello çevrimdışı veri eşitleme özelliğini kullanarak, son kullanıcılar ile yerel bir veritabanı etkileşimli olarak çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-117">Using hello offline data-sync feature of Mobile Apps, end-users can interact with a local database even when hello network is inaccessible.</span></span> <span data-ttu-id="4dbe1-118">toouse bu özellikler, uygulamanızda hello eşitleme bağlamı başlatma `MSClient` ve yerel bir depo başvuru.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-118">toouse these features in your app, you initialize hello sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="4dbe1-119">Tablonuz hello aracılığıyla başvuru sonra **MSSyncTable** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-119">Then you reference your table through hello **MSSyncTable** interface.</span></span>

<span data-ttu-id="4dbe1-120">İçinde **QSTodoService.m** (Objective-C) veya **ToDoTableViewController.swift** hello üye türü hello (Swift), bildirim **syncTable** olan  **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that hello type of hello member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="4dbe1-121">Çevrimdışı eşitleme kullanan bu eşitleme tablo arabirimi yerine **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="4dbe1-122">Bir eşitleme tablo kullanıldığında, tüm işlemleri yalnızca uzak arka uç açık itme hello eşitlendiğini toohello yerel deposu gidin ve işlemleri çekme.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-122">When a sync table is used, all operations go toohello local store and are synchronized only with hello remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="4dbe1-123">tooget bir başvuru tooa eşitleme tablosu kullanmak hello **syncTableWithName** yöntemi `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-123">tooget a reference tooa sync table, use hello **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="4dbe1-124">tooremove çevrimdışı eşitleme işlevselliği, kullanım **tableWithName** yerine.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-124">tooremove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="4dbe1-125">Tablo işlemleri gerçekleştirilmeden önce hello yerel depolama başlatılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-125">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="4dbe1-126">Merhaba ilgili kod aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-126">Here is hello relevant code:</span></span>

* <span data-ttu-id="4dbe1-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-127">**Objective-C**.</span></span> <span data-ttu-id="4dbe1-128">Merhaba, **QSTodoService.init** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-128">In hello **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="4dbe1-129">**SWIFT**.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-129">**Swift**.</span></span> <span data-ttu-id="4dbe1-130">Merhaba, **ToDoTableViewController.viewDidLoad** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-130">In hello **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="4dbe1-131">Bu yöntem hello kullanarak yerel bir depo oluşturur `MSCoreDataStore` Mobile Apps SDK'sı hello arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-131">This method creates a local store by using hello `MSCoreDataStore` interface, which hello Mobile Apps SDK provides.</span></span> <span data-ttu-id="4dbe1-132">Merhaba uygulayarak farklı bir yerel deposu alternatif olarak, sağlayabilir `MSSyncContextDataSource` protokolü.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-132">Alternatively, you can provide a different local store by implementing hello `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="4dbe1-133">Ayrıca, ilk parametresinin hello **MSSyncContext** kullanılan toospecify çakışma işleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-133">Also, hello first parameter of **MSSyncContext** is used toospecify a conflict handler.</span></span> <span data-ttu-id="4dbe1-134">Biz başarılı olduğundan `nil`, biz üzerinde herhangi bir çakışmanın başarısız hello varsayılan çakışma işleyici alın.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-134">Because we have passed `nil`, we get hello default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="4dbe1-135">Şimdi, şimdi hello gerçek eşitleme işlemi gerçekleştirmek ve verileri hello uzak arka uçtan alın:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-135">Now, let's perform hello actual sync operation, and get data from hello remote back end:</span></span>

* <span data-ttu-id="4dbe1-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-136">**Objective-C**.</span></span> <span data-ttu-id="4dbe1-137">`syncData`Yeni değişiklikler ilk iter ve çağırır **pullData** hello uzak arka uçtan tooget veri.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-137">`syncData` first pushes new changes and then calls **pullData** tooget data from hello remote back end.</span></span> <span data-ttu-id="4dbe1-138">Buna karşılık, hello **pullData** yöntemi bir sorguyla eşleşen yeni verileri alır:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-138">In turn, hello **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="4dbe1-139">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="4dbe1-140">Merhaba Objective-C sürümünde, içinde `syncData`, ilk diyoruz **pushWithCompletion** üzerinde hello eşitleme bağlamı.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-140">In hello Objective-C version, in `syncData`, we first call **pushWithCompletion** on hello sync context.</span></span> <span data-ttu-id="4dbe1-141">Bu yöntem bir üyesi olan `MSSyncContext` (ve hello eşitleme tablonun kendisini değil) tüm tablolar arasında değişiklikleri iter olduğundan.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-141">This method is a member of `MSSyncContext` (and not hello sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="4dbe1-142">Yerel olarak (CUD işlemleri üzerinden) şekilde değiştirilmiş kayıtları toohello sunucu gönderilir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-142">Only records that have been modified in some way locally (through CUD operations) are sent toohello server.</span></span> <span data-ttu-id="4dbe1-143">Yardımcı hello **pullData** çağrıldığında hangi çağrıları **MSSyncTable.pullWithQuery** tooretrieve uzak veri ve hello yerel veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-143">Then hello helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** tooretrieve remote data and store it in hello local database.</span></span>

<span data-ttu-id="4dbe1-144">Merhaba SWIFT sürümünde hello gönderme işlemi kesinlikle gerekli olmadığından yoktur çağrı yok çok**pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-144">In hello Swift version, because hello push operation was not strictly necessary, there is no call too**pushWithCompletion**.</span></span> <span data-ttu-id="4dbe1-145">Gönderme işlemi yapıyor Merhaba tablonun hello eşitleme bağlamındaki bekleyen tüm değişiklikleri varsa, çekme her zaman bir itme ilk verir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-145">If there are any changes pending in hello sync context for hello table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="4dbe1-146">Ancak, birden fazla eşitleme tablo varsa, en iyi tooexplicitly çağrı anında tooensure her şeyi ilişkili tablolar arasında tutarlı olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-146">However, if you have more than one sync table, it is best tooexplicitly call push tooensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="4dbe1-147">Merhaba Objective-C hem SWIFT sürümleri hello kullanabilirsiniz **pullWithQuery** yöntemi toospecify sorgu toofilter hello tooretrieve istediğiniz kaydeder.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-147">In both hello Objective-C and Swift versions, you can use hello **pullWithQuery** method toospecify a query toofilter hello records you want tooretrieve.</span></span> <span data-ttu-id="4dbe1-148">Bu örnekte, hello sorgu hello uzak tüm kayıtları alır `TodoItem` tablo.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-148">In this example, hello query retrieves all records in hello remote `TodoItem` table.</span></span>

<span data-ttu-id="4dbe1-149">ikinci parametresi, hello **pullWithQuery** için kullanılan bir sorgu kimliği *Artımlı eşitleme*. Artımlı eşitleme hello kaydın kullanarak hello son eşitlemeden sonra değiştirilen kayıtları alır `UpdatedAt` zaman damgası (adlı `updatedAt` hello yerel depolama alanındaki) hello sorgu kimliği her mantıksal sorgu için benzersiz tanımlayıcı bir dize olmalıdır Uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-149">hello second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since hello last sync, using hello record's `UpdatedAt` time stamp (called `updatedAt` in hello local store.) hello query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="4dbe1-150">tooopt Artımlı eşitleme dışına geçirmek `nil` sorgu kimliği hello gibi</span><span class="sxs-lookup"><span data-stu-id="4dbe1-150">tooopt out of incremental sync, pass `nil` as hello query ID.</span></span> <span data-ttu-id="4dbe1-151">Her çekme işlemi tüm kayıtları aldığı için bu yaklaşım olası verimsiz olabilir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="4dbe1-152">Merhaba Objective-C uygulama değiştirmek veya bir kullanıcı hello yenileme hareketi gerçekleştirdiğinde veri eklediğinizde ve başlatma eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-152">hello Objective-C app syncs when you modify or add data, when a user performs hello refresh gesture, and on launch.</span></span>

<span data-ttu-id="4dbe1-153">Merhaba SWIFT uygulama hello kullanıcı hello yenileme hareketi gerçekleştirdiğinde ve başlatma eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-153">hello Swift app syncs when hello user performs hello refresh gesture and on launch.</span></span>

<span data-ttu-id="4dbe1-154">Merhaba veri olduğunda uygulama eşitlemeler (Objective-C) değiştirdiğinden ya da hello uygulama (Objective-C ve Swift) başlattığında hello uygulama hello kullanıcının çevrimiçi olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-154">Because hello app syncs whenever data is modified (Objective-C) or whenever hello app starts (Objective-C and Swift), hello app assumes that hello user is online.</span></span> <span data-ttu-id="4dbe1-155">Sonraki bölümde, böylece kullanıcılar çevrimdışı olsalar bile düzenleyebilirsiniz hello uygulamayı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-155">In a later section, you will update hello app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="4dbe1-156"><a name="review-core-data"></a>Gözden geçirme hello çekirdek veri modeli</span><span class="sxs-lookup"><span data-stu-id="4dbe1-156"><a name="review-core-data"></a>Review hello Core Data model</span></span>
<span data-ttu-id="4dbe1-157">Merhaba çekirdek veri çevrimdışı deposu kullandığınızda, veri modelinizi belirli tabloları ve alanları tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-157">When you use hello Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="4dbe1-158">Merhaba örnek uygulaması zaten hello doğru biçime sahip bir veri modeli içerir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-158">hello sample app already includes a data model with hello right format.</span></span> <span data-ttu-id="4dbe1-159">Bu bölümde, nasıl kullanıldıkları Biz bu tablolar tooshow yol.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-159">In this section, we walk through these tables tooshow how they are used.</span></span>

<span data-ttu-id="4dbe1-160">Açık **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-160">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="4dbe1-161">Dört tablolar tanımlanan--tarafından kullanılan üç SDK hello ve hello Yapılacaklar için kullanılan bir öğelerini kendilerini:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-161">Four tables are defined--three that are used by hello SDK and one that's used for hello to-do items themselves:</span></span>
  * <span data-ttu-id="4dbe1-162">MS_TableOperations: Parçaları toobe hello eşitlenmesi gereken öğeleri hello.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-162">MS_TableOperations: Tracks hello items that need toobe synchronized with hello server.</span></span>
  * <span data-ttu-id="4dbe1-163">MS_TableOperationErrors: Çevrimdışı eşitleme sırasında gerçekleşen hataları izler.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="4dbe1-164">MS_TableConfig: Hello son eşitleme işlemi tüm çekme işlemleri için güncelleştirilmiş son kez parçaları hello.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-164">MS_TableConfig: Tracks hello last updated time for hello last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="4dbe1-165">Todoıtem: hello Yapılacaklar öğelerini depolar.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-165">TodoItem: Stores hello to-do items.</span></span> <span data-ttu-id="4dbe1-166">Sistem sütunları hello **createdAt**, **updatedAt**, ve **sürüm** isteğe bağlı sistem özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-166">hello system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="4dbe1-167">Merhaba Mobile Apps SDK'sı ile başlayan sütun adları ayırır "**``**".</span><span class="sxs-lookup"><span data-stu-id="4dbe1-167">hello Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="4dbe1-168">Bu ön ek sistem sütunlar dışındaki herhangi bir şeyle kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-168">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="4dbe1-169">Aksi takdirde hello uzak arka uç kullandığınızda, sütun adlarının değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-169">Otherwise, your column names are modified when you use hello remote back end.</span></span>
>
>

<span data-ttu-id="4dbe1-170">Merhaba çevrimdışı eşitleme özelliğini kullandığınızda, hello üç Sistem tabloları ve hello veri tablosu tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-170">When you use hello offline sync feature, define hello three system tables and hello data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="4dbe1-171">Sistem tabloları</span><span class="sxs-lookup"><span data-stu-id="4dbe1-171">System tables</span></span>

<span data-ttu-id="4dbe1-172">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="4dbe1-172">**MS_TableOperations**</span></span>  

![MS_TableOperations tablo öznitelikleri][defining-core-data-tableoperations-entity]

| <span data-ttu-id="4dbe1-174">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="4dbe1-174">Attribute</span></span> | <span data-ttu-id="4dbe1-175">Tür</span><span class="sxs-lookup"><span data-stu-id="4dbe1-175">Type</span></span> |
| --- | --- |
| <span data-ttu-id="4dbe1-176">id</span><span class="sxs-lookup"><span data-stu-id="4dbe1-176">id</span></span> | <span data-ttu-id="4dbe1-177">Tamsayı 64</span><span class="sxs-lookup"><span data-stu-id="4dbe1-177">Integer 64</span></span> |
| <span data-ttu-id="4dbe1-178">öğe kimliği</span><span class="sxs-lookup"><span data-stu-id="4dbe1-178">itemId</span></span> | <span data-ttu-id="4dbe1-179">Dize</span><span class="sxs-lookup"><span data-stu-id="4dbe1-179">String</span></span> |
| <span data-ttu-id="4dbe1-180">properties</span><span class="sxs-lookup"><span data-stu-id="4dbe1-180">properties</span></span> | <span data-ttu-id="4dbe1-181">İkili veriler</span><span class="sxs-lookup"><span data-stu-id="4dbe1-181">Binary Data</span></span> |
| <span data-ttu-id="4dbe1-182">Tablo</span><span class="sxs-lookup"><span data-stu-id="4dbe1-182">table</span></span> | <span data-ttu-id="4dbe1-183">Dize</span><span class="sxs-lookup"><span data-stu-id="4dbe1-183">String</span></span> |
| <span data-ttu-id="4dbe1-184">tableKind</span><span class="sxs-lookup"><span data-stu-id="4dbe1-184">tableKind</span></span> | <span data-ttu-id="4dbe1-185">Tamsayı 16</span><span class="sxs-lookup"><span data-stu-id="4dbe1-185">Integer 16</span></span> |


<span data-ttu-id="4dbe1-186">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="4dbe1-186">**MS_TableOperationErrors**</span></span>

 ![MS_TableOperationErrors tablo öznitelikleri][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="4dbe1-188">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="4dbe1-188">Attribute</span></span> | <span data-ttu-id="4dbe1-189">Tür</span><span class="sxs-lookup"><span data-stu-id="4dbe1-189">Type</span></span> |
| --- | --- |
| <span data-ttu-id="4dbe1-190">id</span><span class="sxs-lookup"><span data-stu-id="4dbe1-190">id</span></span> |<span data-ttu-id="4dbe1-191">Dize</span><span class="sxs-lookup"><span data-stu-id="4dbe1-191">String</span></span> |
| <span data-ttu-id="4dbe1-192">Operationıd</span><span class="sxs-lookup"><span data-stu-id="4dbe1-192">operationId</span></span> |<span data-ttu-id="4dbe1-193">Tamsayı 64</span><span class="sxs-lookup"><span data-stu-id="4dbe1-193">Integer 64</span></span> |
| <span data-ttu-id="4dbe1-194">properties</span><span class="sxs-lookup"><span data-stu-id="4dbe1-194">properties</span></span> |<span data-ttu-id="4dbe1-195">İkili veriler</span><span class="sxs-lookup"><span data-stu-id="4dbe1-195">Binary Data</span></span> |
| <span data-ttu-id="4dbe1-196">tableKind</span><span class="sxs-lookup"><span data-stu-id="4dbe1-196">tableKind</span></span> |<span data-ttu-id="4dbe1-197">Tamsayı 16</span><span class="sxs-lookup"><span data-stu-id="4dbe1-197">Integer 16</span></span> |

 <span data-ttu-id="4dbe1-198">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="4dbe1-198">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="4dbe1-199">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="4dbe1-199">Attribute</span></span> | <span data-ttu-id="4dbe1-200">Tür</span><span class="sxs-lookup"><span data-stu-id="4dbe1-200">Type</span></span> |
| --- | --- |
| <span data-ttu-id="4dbe1-201">id</span><span class="sxs-lookup"><span data-stu-id="4dbe1-201">id</span></span> |<span data-ttu-id="4dbe1-202">Dize</span><span class="sxs-lookup"><span data-stu-id="4dbe1-202">String</span></span> |
| <span data-ttu-id="4dbe1-203">anahtar</span><span class="sxs-lookup"><span data-stu-id="4dbe1-203">key</span></span> |<span data-ttu-id="4dbe1-204">Dize</span><span class="sxs-lookup"><span data-stu-id="4dbe1-204">String</span></span> |
| <span data-ttu-id="4dbe1-205">keyType</span><span class="sxs-lookup"><span data-stu-id="4dbe1-205">keyType</span></span> |<span data-ttu-id="4dbe1-206">Tamsayı 64</span><span class="sxs-lookup"><span data-stu-id="4dbe1-206">Integer 64</span></span> |
| <span data-ttu-id="4dbe1-207">Tablo</span><span class="sxs-lookup"><span data-stu-id="4dbe1-207">table</span></span> |<span data-ttu-id="4dbe1-208">Dize</span><span class="sxs-lookup"><span data-stu-id="4dbe1-208">String</span></span> |
| <span data-ttu-id="4dbe1-209">değer</span><span class="sxs-lookup"><span data-stu-id="4dbe1-209">value</span></span> |<span data-ttu-id="4dbe1-210">Dize</span><span class="sxs-lookup"><span data-stu-id="4dbe1-210">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="4dbe1-211">Veri tablosu</span><span class="sxs-lookup"><span data-stu-id="4dbe1-211">Data table</span></span>

<span data-ttu-id="4dbe1-212">**Todoıtem**</span><span class="sxs-lookup"><span data-stu-id="4dbe1-212">**TodoItem**</span></span>

| <span data-ttu-id="4dbe1-213">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="4dbe1-213">Attribute</span></span> | <span data-ttu-id="4dbe1-214">Tür</span><span class="sxs-lookup"><span data-stu-id="4dbe1-214">Type</span></span> | <span data-ttu-id="4dbe1-215">Not</span><span class="sxs-lookup"><span data-stu-id="4dbe1-215">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4dbe1-216">id</span><span class="sxs-lookup"><span data-stu-id="4dbe1-216">id</span></span> | <span data-ttu-id="4dbe1-217">Dize, gerekli olarak işaretlenmiş</span><span class="sxs-lookup"><span data-stu-id="4dbe1-217">String, marked required</span></span> |<span data-ttu-id="4dbe1-218">Uzak Depolama birincil anahtar</span><span class="sxs-lookup"><span data-stu-id="4dbe1-218">Primary key in remote store</span></span> |
| <span data-ttu-id="4dbe1-219">Tamamlayın</span><span class="sxs-lookup"><span data-stu-id="4dbe1-219">complete</span></span> | <span data-ttu-id="4dbe1-220">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="4dbe1-220">Boolean</span></span> | <span data-ttu-id="4dbe1-221">Yapılacak iş öğesi alanı</span><span class="sxs-lookup"><span data-stu-id="4dbe1-221">To-do item field</span></span> |
| <span data-ttu-id="4dbe1-222">Metin</span><span class="sxs-lookup"><span data-stu-id="4dbe1-222">text</span></span> |<span data-ttu-id="4dbe1-223">Dize</span><span class="sxs-lookup"><span data-stu-id="4dbe1-223">String</span></span> |<span data-ttu-id="4dbe1-224">Yapılacak iş öğesi alanı</span><span class="sxs-lookup"><span data-stu-id="4dbe1-224">To-do item field</span></span> |
| <span data-ttu-id="4dbe1-225">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="4dbe1-225">createdAt</span></span> | <span data-ttu-id="4dbe1-226">Tarih</span><span class="sxs-lookup"><span data-stu-id="4dbe1-226">Date</span></span> | <span data-ttu-id="4dbe1-227">(isteğe bağlı) Çok eşlemeleri**createdAt** sistem özelliği</span><span class="sxs-lookup"><span data-stu-id="4dbe1-227">(optional) Maps too**createdAt** system property</span></span> |
| <span data-ttu-id="4dbe1-228">updatedAt</span><span class="sxs-lookup"><span data-stu-id="4dbe1-228">updatedAt</span></span> | <span data-ttu-id="4dbe1-229">Tarih</span><span class="sxs-lookup"><span data-stu-id="4dbe1-229">Date</span></span> | <span data-ttu-id="4dbe1-230">(isteğe bağlı) Çok eşlemeleri**updatedAt** sistem özelliği</span><span class="sxs-lookup"><span data-stu-id="4dbe1-230">(optional) Maps too**updatedAt** system property</span></span> |
| <span data-ttu-id="4dbe1-231">Sürüm</span><span class="sxs-lookup"><span data-stu-id="4dbe1-231">version</span></span> | <span data-ttu-id="4dbe1-232">Dize</span><span class="sxs-lookup"><span data-stu-id="4dbe1-232">String</span></span> | <span data-ttu-id="4dbe1-233">(isteğe bağlı) Kullanılan toodetect çakışmaları, maps tooversion</span><span class="sxs-lookup"><span data-stu-id="4dbe1-233">(optional) Used toodetect conflicts, maps tooversion</span></span> |

## <span data-ttu-id="4dbe1-234"><a name="setup-sync"></a>Hello uygulama Hello eşitleme davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="4dbe1-234"><a name="setup-sync"></a>Change hello sync behavior of hello app</span></span>
<span data-ttu-id="4dbe1-235">Bu bölümde, uygulama başlatma ya da zaman eklemek ve öğeleri güncelleştirme üzerinde eşitlemez şekilde hello uygulama değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-235">In this section, you modify hello app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="4dbe1-236">Yalnızca hello Yenile hareketi düğmesini gerçekleştirildiğinde eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-236">It syncs only when hello refresh gesture button is performed.</span></span>

<span data-ttu-id="4dbe1-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-237">**Objective-C**:</span></span>

1. <span data-ttu-id="4dbe1-238">İçinde **QSTodoListViewController.m**, hello değiştirme **viewDidLoad** yöntemi tooremove hello çağrısı çok`[self refresh]` hello yöntemi hello sonunda.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-238">In **QSTodoListViewController.m**, change hello **viewDidLoad** method tooremove hello call too`[self refresh]` at hello end of hello method.</span></span> <span data-ttu-id="4dbe1-239">Şimdi, uygulama başlatılırken hello sunucusuyla hello veri eşitlenmedi.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-239">Now hello data is not synced with hello server on app start.</span></span> <span data-ttu-id="4dbe1-240">Bunun yerine, hello yerel deposunun Merhaba içeriğine ile eşitlenip.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-240">Instead, it's synced with hello contents of hello local store.</span></span>
2. <span data-ttu-id="4dbe1-241">İçinde **QSTodoService.m**, hello tanımını değiştirmek `addItem` böylece hello öğesi eklendikten sonra eşitleme değil.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-241">In **QSTodoService.m**, modify hello definition of `addItem` so that it doesn't sync after hello item is inserted.</span></span> <span data-ttu-id="4dbe1-242">Merhaba kaldırmak `self syncData` engelleme ve hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-242">Remove hello `self syncData` block and replace it with hello following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="4dbe1-243">Merhaba tanımını değiştirmek `completeItem` daha önce belirtildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-243">Modify hello definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="4dbe1-244">Başlangıç engellemeyi kaldırmak `self syncData` ve hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-244">Remove hello block for `self syncData` and replace it with hello following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="4dbe1-245">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-245">**Swift**:</span></span>

<span data-ttu-id="4dbe1-246">İçinde `viewDidLoad`, **ToDoTableViewController.swift**, burada, app başlangıç eşitleniyor toostop gösterilen hello iki satırları açıklama.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out hello two lines shown here, toostop syncing on app start.</span></span> <span data-ttu-id="4dbe1-247">Bu yazma hello anda birisi ekler veya öğeyi tamamlandıktan hello Swift Todo uygulaması hello hizmet güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-247">At hello time of this writing, hello Swift Todo app does not update hello service when someone adds or completes an item.</span></span> <span data-ttu-id="4dbe1-248">Merhaba hizmeti yalnızca, uygulama başlatılırken güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-248">It updates hello service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="4dbe1-249"><a name="test-app"></a>Test hello uygulama</span><span class="sxs-lookup"><span data-stu-id="4dbe1-249"><a name="test-app"></a>Test hello app</span></span>
<span data-ttu-id="4dbe1-250">Bu bölümde, tooan geçersiz URL toosimulate çevrimdışı bir senaryo bağlayın.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-250">In this section, you connect tooan invalid URL toosimulate an offline scenario.</span></span> <span data-ttu-id="4dbe1-251">Veri öğeleri eklediğinizde, tutulan hello Yerel Çekirdek veri depolamak, ancak bunlar hello mobil uygulama arka ucu ile eşitlenmedi.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-251">When you add data items, they're held in hello local Core Data store, but they're not synced with hello mobile-app back end.</span></span>

1. <span data-ttu-id="4dbe1-252">Merhaba mobil uygulama URL'sini değiştirmek **QSTodoService.m** tooan geçersiz URL ve yeniden çalışma hello uygulama:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-252">Change hello mobile-app URL in **QSTodoService.m** tooan invalid URL, and run hello app again:</span></span>

   <span data-ttu-id="4dbe1-253">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-253">**Objective-C**.</span></span> <span data-ttu-id="4dbe1-254">QSTodoService.m içinde:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-254">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="4dbe1-255">**SWIFT**.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-255">**Swift**.</span></span> <span data-ttu-id="4dbe1-256">ToDoTableViewController.swift içinde:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-256">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="4dbe1-257">Bazı Yapılacaklar öğelerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-257">Add some to-do items.</span></span> <span data-ttu-id="4dbe1-258">Merhaba simulator (veya zorla kapatma hello uygulama) çıkmanız ve yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-258">Quit hello simulator (or forcibly close hello app), and then restart it.</span></span> <span data-ttu-id="4dbe1-259">Yaptığınız değişiklikleri kalıcı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-259">Verify that your changes persist.</span></span>

3. <span data-ttu-id="4dbe1-260">Görüntüleme hello uzak Merhaba içeriğine **Todoıtem** tablosu:</span><span class="sxs-lookup"><span data-stu-id="4dbe1-260">View hello contents of hello remote **TodoItem** table:</span></span>
   * <span data-ttu-id="4dbe1-261">Node.js arka ucu için toohello Git [Azure portal](https://portal.azure.com/) ve, mobil uygulama arka ucu içinde tıklatın **kolay tabloları** > **Todoıtem**.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-261">For a Node.js back end, go toohello [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="4dbe1-262">Bir .NET geri için sonlandırmak için SQL Server Management Studio gibi bir SQL aracı veya Fiddler veya Postman gibi bir REST istemcisi kullanın.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="4dbe1-263">Merhaba yeni öğelerin bulunduğunu doğrulayın *değil* edilmiş hello sunucusuyla eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-263">Verify that hello new items have *not* been synced with hello server.</span></span>

5. <span data-ttu-id="4dbe1-264">Değişiklik hello URL toohello düzeltmek birinde **QSTodoService.m**ve yeniden çalıştır hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-264">Change hello URL back toohello correct one in **QSTodoService.m**, and rerun hello app.</span></span>

6. <span data-ttu-id="4dbe1-265">Merhaba yenileme hareketi öğeleri hello listede aşağı çekerek gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-265">Perform hello refresh gesture by pulling down hello list of items.</span></span>  
<span data-ttu-id="4dbe1-266">Devam eden değer değiştirici görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-266">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="4dbe1-267">Görünüm hello **Todoıtem** yeniden verileri.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-267">View hello **TodoItem** data again.</span></span> <span data-ttu-id="4dbe1-268">Merhaba yeni ve değiştirilen Yapılacaklar öğelerini şimdi görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-268">hello new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="4dbe1-269">Özet</span><span class="sxs-lookup"><span data-stu-id="4dbe1-269">Summary</span></span>
<span data-ttu-id="4dbe1-270">toosupport hello çevrimdışı eşitleme özelliği kullandık hello `MSSyncTable` arabirim ve başlatıldı `MSClient.syncContext` yerel deposu.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-270">toosupport hello offline sync feature, we used hello `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="4dbe1-271">Bu durumda, hello yerel deposu çekirdek veri tabanlı bir veritabanı oluştu.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-271">In this case, hello local store was a Core Data-based database.</span></span>

<span data-ttu-id="4dbe1-272">Bir çekirdek veri yerel deposu kullandığınızda, hello birkaç tablolarla tanımlamalısınız [düzeltmek Sistem Özellikleri](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="4dbe1-272">When you use a Core Data local store, you must define several tables with hello [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="4dbe1-273">Hello normal oluşturmak okuma, güncelleştirme ve hello uygulama hala bağlı, ancak tüm hello işlemleri hello yerel depo ortaya gibi mobil uygulamaları iş için (CRUD) işlemleridir silme.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-273">hello normal create, read, update, and delete (CRUD) operations for mobile apps work as if hello app is still connected, but all hello operations occur against hello local store.</span></span>

<span data-ttu-id="4dbe1-274">Merhaba yerel deposu hello sunucuyla eşitlendiğinde hello kullandık **MSSyncTable.pullWithQuery** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4dbe1-274">When we synchronized hello local store with hello server, we used hello **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4dbe1-275">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4dbe1-275">Additional resources</span></span>
* <span data-ttu-id="4dbe1-276">[mobil uygulamalarda çevrimdışı veri eşitlemeye]</span><span class="sxs-lookup"><span data-stu-id="4dbe1-276">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="4dbe1-277">[Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme] \(hello video Mobile Services hakkında olmakla birlikte, benzer şekilde Mobile Apps çevrimdışı eşitleme çalışır.\)</span><span class="sxs-lookup"><span data-stu-id="4dbe1-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(hello video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


[iOS uygulaması oluştur]: app-service-mobile-ios-get-started.md
[mobil uygulamalarda çevrimdışı veri eşitlemeye]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

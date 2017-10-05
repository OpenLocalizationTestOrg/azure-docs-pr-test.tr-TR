---
title: "İOS mobil uygulamaları ile çevrimdışı eşitlemeyi etkinleştirme | Microsoft Docs"
description: "Önbellek ve eşitleme çevrimdışı veri için Azure App Service mobile apps'de iOS uygulamalarında kullanmayı öğrenin."
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
ms.openlocfilehash: 44c0d26b2d7d28322d436d4bda319d728c31a635
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="10ade-103">Çevrimdışı iOS mobil uygulamaları ile eşitlemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="10ade-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="10ade-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="10ade-104">Overview</span></span>
<span data-ttu-id="10ade-105">Bu öğretici, Azure App Service Mobile Apps özelliğini iOS için çevrimdışı eşitleme kapsar.</span><span class="sxs-lookup"><span data-stu-id="10ade-105">This tutorial covers offline syncing with the Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="10ade-106">Çevrimdışı eşitleme son kullanıcılara görüntülemek, eklemek veya bile ağ bağlantısı olduğunda verileri değiştirmek için mobil uygulama ile etkileşim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10ade-106">With offline syncing end-users can interact with a mobile app to view, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="10ade-107">Değişiklikler yerel bir veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="10ade-107">Changes are stored in a local database.</span></span> <span data-ttu-id="10ade-108">Cihaz yeniden çevrimiçi olduktan sonra değişiklikler uzak arka uç ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="10ade-108">After the device is back online, the changes are synced with the remote back end.</span></span>

<span data-ttu-id="10ade-109">Mobile Apps ile ilk deneyiminizi varsa öğreticinin ilk tamamlanmalıdır [iOS uygulaması oluştur].</span><span class="sxs-lookup"><span data-stu-id="10ade-109">If this is your first experience with Mobile Apps, you should first complete the tutorial [Create an iOS App].</span></span> <span data-ttu-id="10ade-110">İndirilen hızlı başlangıç sunucu projesi kullanmazsanız, veri erişimi uzantısı paketlerini projenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="10ade-110">If you do not use the downloaded quick-start server project, you must add the data-access extension packages to your project.</span></span> <span data-ttu-id="10ade-111">Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [.NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="10ade-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="10ade-112">Çevrimdışı eşitleme özelliği hakkında daha fazla bilgi için bkz: [mobil uygulamalarda çevrimdışı veri eşitlemeye].</span><span class="sxs-lookup"><span data-stu-id="10ade-112">To learn more about the offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="10ade-113"><a name="review-sync"></a>İstemci eşitleme kodu gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="10ade-113"><a name="review-sync"></a>Review the client sync code</span></span>
<span data-ttu-id="10ade-114">İçin indirdiğiniz istemci projesi [iOS uygulaması oluştur] öğretici zaten bir yerel çekirdek veri tabanlı veritabanı çevrimdışı eşitlemeyi destekleyen kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="10ade-114">The client project that you downloaded for the [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="10ade-115">Bu bölümde, eğitmen kodu zaten dahil özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="10ade-115">This section summarizes what is already included in the tutorial code.</span></span> <span data-ttu-id="10ade-116">Özellik kavramsal bir genel bakış için bkz: [mobil uygulamalarda çevrimdışı veri eşitlemeye].</span><span class="sxs-lookup"><span data-stu-id="10ade-116">For a conceptual overview of the feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="10ade-117">Ağ erişilemez durumda olduğunda bile Mobile Apps çevrimdışı veri eşitleme özelliğini kullanarak, son kullanıcılar ile yerel bir veritabanı etkileşimli olarak çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="10ade-117">Using the offline data-sync feature of Mobile Apps, end-users can interact with a local database even when the network is inaccessible.</span></span> <span data-ttu-id="10ade-118">Bu özellikler, uygulamanızda kullanmak için eşitleme bağlamı başlatma `MSClient` ve yerel bir depo başvuru.</span><span class="sxs-lookup"><span data-stu-id="10ade-118">To use these features in your app, you initialize the sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="10ade-119">Tablonuz aracılığıyla başvuru sonra **MSSyncTable** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="10ade-119">Then you reference your table through the **MSSyncTable** interface.</span></span>

<span data-ttu-id="10ade-120">İçinde **QSTodoService.m** (Objective-C) veya **ToDoTableViewController.swift** (Swift), dikkat üye türü **syncTable** olan **MSSyncTable** .</span><span class="sxs-lookup"><span data-stu-id="10ade-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that the type of the member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="10ade-121">Çevrimdışı eşitleme kullanan bu eşitleme tablo arabirimi yerine **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="10ade-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="10ade-122">Bir eşitleme tablo kullanıldığında, tüm işlemleri yerel mağazaya gidin ve yalnızca açık anında iletme ve çekme işlemleri ile uzaktan arka uç ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="10ade-122">When a sync table is used, all operations go to the local store and are synchronized only with the remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="10ade-123">Bir eşitleme tablo için bir başvuru almak için **syncTableWithName** yöntemi `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="10ade-123">To get a reference to a sync table, use the **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="10ade-124">Çevrimdışı eşitleme işlevselliği kaldırmak için kullanın **tableWithName** yerine.</span><span class="sxs-lookup"><span data-stu-id="10ade-124">To remove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="10ade-125">Tablo işlemleri gerçekleştirilmeden önce yerel deposu başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="10ade-125">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="10ade-126">İlgili kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="10ade-126">Here is the relevant code:</span></span>

* <span data-ttu-id="10ade-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="10ade-127">**Objective-C**.</span></span> <span data-ttu-id="10ade-128">İçinde **QSTodoService.init** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="10ade-128">In the **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="10ade-129">**SWIFT**.</span><span class="sxs-lookup"><span data-stu-id="10ade-129">**Swift**.</span></span> <span data-ttu-id="10ade-130">İçinde **ToDoTableViewController.viewDidLoad** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="10ade-130">In the **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of the Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="10ade-131">Bu yöntemi kullanarak yerel bir depo oluşturur `MSCoreDataStore` Mobile Apps SDK'sı sağlayan arabirim.</span><span class="sxs-lookup"><span data-stu-id="10ade-131">This method creates a local store by using the `MSCoreDataStore` interface, which the Mobile Apps SDK provides.</span></span> <span data-ttu-id="10ade-132">Alternatif olarak, size uygulayarak farklı bir yerel deposu sağlayabilir `MSSyncContextDataSource` protokolü.</span><span class="sxs-lookup"><span data-stu-id="10ade-132">Alternatively, you can provide a different local store by implementing the `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="10ade-133">Ayrıca, ilk parametresinin **MSSyncContext** bir çakışma işleyici belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="10ade-133">Also, the first parameter of **MSSyncContext** is used to specify a conflict handler.</span></span> <span data-ttu-id="10ade-134">Biz başarılı olduğundan `nil`, biz üzerinde herhangi bir çakışmanın başarısız varsayılan çakışma işleyici alın.</span><span class="sxs-lookup"><span data-stu-id="10ade-134">Because we have passed `nil`, we get the default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="10ade-135">Şimdi, şimdi gerçek eşitleme işlemi yapmak ve verileri uzak arka uçtan alın:</span><span class="sxs-lookup"><span data-stu-id="10ade-135">Now, let's perform the actual sync operation, and get data from the remote back end:</span></span>

* <span data-ttu-id="10ade-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="10ade-136">**Objective-C**.</span></span> <span data-ttu-id="10ade-137">`syncData`Yeni değişiklikler ilk iter ve çağırır **pullData** uzak arka uçtan veri almak için.</span><span class="sxs-lookup"><span data-stu-id="10ade-137">`syncData` first pushes new changes and then calls **pullData** to get data from the remote back end.</span></span> <span data-ttu-id="10ade-138">Buna karşılık, **pullData** yöntemi bir sorguyla eşleşen yeni verileri alır:</span><span class="sxs-lookup"><span data-stu-id="10ade-138">In turn, the **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in the sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from the remote server into the local table.
       // We're pulling all items and filtering in the view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets the caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="10ade-139">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="10ade-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via the MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep the server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation to item \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting to server's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="10ade-140">Objective-C sürümünde içinde `syncData`, ilk diyoruz **pushWithCompletion** üzerinde eşitleme bağlamı.</span><span class="sxs-lookup"><span data-stu-id="10ade-140">In the Objective-C version, in `syncData`, we first call **pushWithCompletion** on the sync context.</span></span> <span data-ttu-id="10ade-141">Bu yöntem bir üyesi olan `MSSyncContext` (ve eşitleme tablonun kendisini değil) tüm tablolar arasında değişiklikleri iter olduğundan.</span><span class="sxs-lookup"><span data-stu-id="10ade-141">This method is a member of `MSSyncContext` (and not the sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="10ade-142">Yerel olarak (CUD işlemleri üzerinden) şekilde değiştirilmiş kayıt sunucusuna gönderilir.</span><span class="sxs-lookup"><span data-stu-id="10ade-142">Only records that have been modified in some way locally (through CUD operations) are sent to the server.</span></span> <span data-ttu-id="10ade-143">Ardından yardımcı **pullData** çağrıldığında hangi çağrıları **MSSyncTable.pullWithQuery** uzak verileri almak ve yerel veritabanında depolamak için.</span><span class="sxs-lookup"><span data-stu-id="10ade-143">Then the helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** to retrieve remote data and store it in the local database.</span></span>

<span data-ttu-id="10ade-144">SWIFT sürümde olmadığından zorlama işlemi kesinlikle gerekli yoktur hiçbir çağrısına **pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="10ade-144">In the Swift version, because the push operation was not strictly necessary, there is no call to **pushWithCompletion**.</span></span> <span data-ttu-id="10ade-145">Gönderme işlemi yapıyor tablosu için eşitleme bağlamındaki bekleyen tüm değişiklikleri varsa, çekme her zaman bir itme ilk verir.</span><span class="sxs-lookup"><span data-stu-id="10ade-145">If there are any changes pending in the sync context for the table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="10ade-146">Ancak, birden fazla eşitleme tablo varsa, her şeyi ilişkili tablolar arasında tutarlı olduğundan emin olmak için anında iletme açıkça çağırmak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="10ade-146">However, if you have more than one sync table, it is best to explicitly call push to ensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="10ade-147">Objective-C hem SWIFT sürümleri de, kullanabileceğiniz **pullWithQuery** yöntemi almak istediğiniz kayıtlarını filtrelemek için bir sorgu belirtin.</span><span class="sxs-lookup"><span data-stu-id="10ade-147">In both the Objective-C and Swift versions, you can use the **pullWithQuery** method to specify a query to filter the records you want to retrieve.</span></span> <span data-ttu-id="10ade-148">Bu örnekte sorgu, uzak tüm kayıtları alır `TodoItem` tablo.</span><span class="sxs-lookup"><span data-stu-id="10ade-148">In this example, the query retrieves all records in the remote `TodoItem` table.</span></span>

<span data-ttu-id="10ade-149">Öğesinin ikinci parametresi, **pullWithQuery** için kullanılan bir sorgu kimliği *Artımlı eşitleme*.</span><span class="sxs-lookup"><span data-stu-id="10ade-149">The second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*.</span></span> <span data-ttu-id="10ade-150">Artımlı eşitleme alır kaydın kullanarak en son eşitlemeden sonra değiştirilen kayıtları `UpdatedAt` zaman damgası (adlı `updatedAt` Yerel Depodaki.) Sorgu kimliği, uygulamanızda mantıksal her sorgu için benzersiz tanımlayıcı bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10ade-150">Incremental sync retrieves only records that were modified since the last sync, using the record's `UpdatedAt` time stamp (called `updatedAt` in the local store.) The query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="10ade-151">Artımlı eşitleme dışında kabul etmek için geçirmek `nil` sorgu kimliği olarak</span><span class="sxs-lookup"><span data-stu-id="10ade-151">To opt out of incremental sync, pass `nil` as the query ID.</span></span> <span data-ttu-id="10ade-152">Her çekme işlemi tüm kayıtları aldığı için bu yaklaşım olası verimsiz olabilir.</span><span class="sxs-lookup"><span data-stu-id="10ade-152">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="10ade-153">Objective-C uygulama değiştirmek veya bir kullanıcı yenileme hareketi gerçekleştirdiğinde veri eklediğinizde ve başlatma eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="10ade-153">The Objective-C app syncs when you modify or add data, when a user performs the refresh gesture, and on launch.</span></span>

<span data-ttu-id="10ade-154">SWIFT uygulama kullanıcı yenileme hareketi gerçekleştirdiğinde ve başlatma eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="10ade-154">The Swift app syncs when the user performs the refresh gesture and on launch.</span></span>

<span data-ttu-id="10ade-155">Veri olduğunda uygulama eşitlemeler (Objective-C) değiştirdiğinden veya uygulama (Objective-C ve Swift) başlattığında, uygulama kullanıcının çevrimiçi olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="10ade-155">Because the app syncs whenever data is modified (Objective-C) or whenever the app starts (Objective-C and Swift), the app assumes that the user is online.</span></span> <span data-ttu-id="10ade-156">Sonraki bölümde, böylece kullanıcılar çevrimdışı olsalar bile düzenleyebilirsiniz uygulamayı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="10ade-156">In a later section, you will update the app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="10ade-157"><a name="review-core-data"></a>Çekirdek veri modeli gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="10ade-157"><a name="review-core-data"></a>Review the Core Data model</span></span>
<span data-ttu-id="10ade-158">Çekirdek veri çevrimdışı deposu kullandığınızda, veri modelinizi belirli tabloları ve alanları tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="10ade-158">When you use the Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="10ade-159">Örnek uygulaması zaten doğru biçime sahip bir veri modeli içerir.</span><span class="sxs-lookup"><span data-stu-id="10ade-159">The sample app already includes a data model with the right format.</span></span> <span data-ttu-id="10ade-160">Bu bölümde, nasıl kullanıldıkları göstermek için bu tablolar yol.</span><span class="sxs-lookup"><span data-stu-id="10ade-160">In this section, we walk through these tables to show how they are used.</span></span>

<span data-ttu-id="10ade-161">Açık **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="10ade-161">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="10ade-162">Dört tablonun tanımlanmış--SDK tarafından kullanılan üç ve yapılacaklar için kullanılan bir kendilerini öğeleri:</span><span class="sxs-lookup"><span data-stu-id="10ade-162">Four tables are defined--three that are used by the SDK and one that's used for the to-do items themselves:</span></span>
  * <span data-ttu-id="10ade-163">MS_TableOperations: sunucusuyla eşitlenmesi gereken öğeleri izler.</span><span class="sxs-lookup"><span data-stu-id="10ade-163">MS_TableOperations: Tracks the items that need to be synchronized with the server.</span></span>
  * <span data-ttu-id="10ade-164">MS_TableOperationErrors: Çevrimdışı eşitleme sırasında gerçekleşen hataları izler.</span><span class="sxs-lookup"><span data-stu-id="10ade-164">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="10ade-165">MS_TableConfig: Parçaları tüm çekme işlemleri için son eşitleme işlemi için zaman son güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="10ade-165">MS_TableConfig: Tracks the last updated time for the last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="10ade-166">Todoıtem: Yapılacaklar öğelerini depolar.</span><span class="sxs-lookup"><span data-stu-id="10ade-166">TodoItem: Stores the to-do items.</span></span> <span data-ttu-id="10ade-167">Sistem sütunları **createdAt**, **updatedAt**, ve **sürüm** isteğe bağlı sistem özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="10ade-167">The system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="10ade-168">Mobile Apps SDK'sı ile başlayan sütun adları ayırır "**``**".</span><span class="sxs-lookup"><span data-stu-id="10ade-168">The Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="10ade-169">Bu ön ek sistem sütunlar dışındaki herhangi bir şeyle kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="10ade-169">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="10ade-170">Aksi takdirde, uzak arka uç kullandığınızda, sütun adlarının değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="10ade-170">Otherwise, your column names are modified when you use the remote back end.</span></span>
>
>

<span data-ttu-id="10ade-171">Çevrimdışı eşitleme özelliğini kullandığınızda, üç Sistem tabloları ve veri tablosu tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="10ade-171">When you use the offline sync feature, define the three system tables and the data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="10ade-172">Sistem tabloları</span><span class="sxs-lookup"><span data-stu-id="10ade-172">System tables</span></span>

<span data-ttu-id="10ade-173">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="10ade-173">**MS_TableOperations**</span></span>  

![MS_TableOperations tablo öznitelikleri][defining-core-data-tableoperations-entity]

| <span data-ttu-id="10ade-175">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="10ade-175">Attribute</span></span> | <span data-ttu-id="10ade-176">Tür</span><span class="sxs-lookup"><span data-stu-id="10ade-176">Type</span></span> |
| --- | --- |
| <span data-ttu-id="10ade-177">id</span><span class="sxs-lookup"><span data-stu-id="10ade-177">id</span></span> | <span data-ttu-id="10ade-178">Tamsayı 64</span><span class="sxs-lookup"><span data-stu-id="10ade-178">Integer 64</span></span> |
| <span data-ttu-id="10ade-179">öğe kimliği</span><span class="sxs-lookup"><span data-stu-id="10ade-179">itemId</span></span> | <span data-ttu-id="10ade-180">Dize</span><span class="sxs-lookup"><span data-stu-id="10ade-180">String</span></span> |
| <span data-ttu-id="10ade-181">properties</span><span class="sxs-lookup"><span data-stu-id="10ade-181">properties</span></span> | <span data-ttu-id="10ade-182">İkili veriler</span><span class="sxs-lookup"><span data-stu-id="10ade-182">Binary Data</span></span> |
| <span data-ttu-id="10ade-183">Tablo</span><span class="sxs-lookup"><span data-stu-id="10ade-183">table</span></span> | <span data-ttu-id="10ade-184">Dize</span><span class="sxs-lookup"><span data-stu-id="10ade-184">String</span></span> |
| <span data-ttu-id="10ade-185">tableKind</span><span class="sxs-lookup"><span data-stu-id="10ade-185">tableKind</span></span> | <span data-ttu-id="10ade-186">Tamsayı 16</span><span class="sxs-lookup"><span data-stu-id="10ade-186">Integer 16</span></span> |


<span data-ttu-id="10ade-187">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="10ade-187">**MS_TableOperationErrors**</span></span>

 ![MS_TableOperationErrors tablo öznitelikleri][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="10ade-189">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="10ade-189">Attribute</span></span> | <span data-ttu-id="10ade-190">Tür</span><span class="sxs-lookup"><span data-stu-id="10ade-190">Type</span></span> |
| --- | --- |
| <span data-ttu-id="10ade-191">id</span><span class="sxs-lookup"><span data-stu-id="10ade-191">id</span></span> |<span data-ttu-id="10ade-192">Dize</span><span class="sxs-lookup"><span data-stu-id="10ade-192">String</span></span> |
| <span data-ttu-id="10ade-193">Operationıd</span><span class="sxs-lookup"><span data-stu-id="10ade-193">operationId</span></span> |<span data-ttu-id="10ade-194">Tamsayı 64</span><span class="sxs-lookup"><span data-stu-id="10ade-194">Integer 64</span></span> |
| <span data-ttu-id="10ade-195">properties</span><span class="sxs-lookup"><span data-stu-id="10ade-195">properties</span></span> |<span data-ttu-id="10ade-196">İkili veriler</span><span class="sxs-lookup"><span data-stu-id="10ade-196">Binary Data</span></span> |
| <span data-ttu-id="10ade-197">tableKind</span><span class="sxs-lookup"><span data-stu-id="10ade-197">tableKind</span></span> |<span data-ttu-id="10ade-198">Tamsayı 16</span><span class="sxs-lookup"><span data-stu-id="10ade-198">Integer 16</span></span> |

 <span data-ttu-id="10ade-199">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="10ade-199">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="10ade-200">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="10ade-200">Attribute</span></span> | <span data-ttu-id="10ade-201">Tür</span><span class="sxs-lookup"><span data-stu-id="10ade-201">Type</span></span> |
| --- | --- |
| <span data-ttu-id="10ade-202">id</span><span class="sxs-lookup"><span data-stu-id="10ade-202">id</span></span> |<span data-ttu-id="10ade-203">Dize</span><span class="sxs-lookup"><span data-stu-id="10ade-203">String</span></span> |
| <span data-ttu-id="10ade-204">anahtar</span><span class="sxs-lookup"><span data-stu-id="10ade-204">key</span></span> |<span data-ttu-id="10ade-205">Dize</span><span class="sxs-lookup"><span data-stu-id="10ade-205">String</span></span> |
| <span data-ttu-id="10ade-206">keyType</span><span class="sxs-lookup"><span data-stu-id="10ade-206">keyType</span></span> |<span data-ttu-id="10ade-207">Tamsayı 64</span><span class="sxs-lookup"><span data-stu-id="10ade-207">Integer 64</span></span> |
| <span data-ttu-id="10ade-208">Tablo</span><span class="sxs-lookup"><span data-stu-id="10ade-208">table</span></span> |<span data-ttu-id="10ade-209">Dize</span><span class="sxs-lookup"><span data-stu-id="10ade-209">String</span></span> |
| <span data-ttu-id="10ade-210">değer</span><span class="sxs-lookup"><span data-stu-id="10ade-210">value</span></span> |<span data-ttu-id="10ade-211">Dize</span><span class="sxs-lookup"><span data-stu-id="10ade-211">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="10ade-212">Veri tablosu</span><span class="sxs-lookup"><span data-stu-id="10ade-212">Data table</span></span>

<span data-ttu-id="10ade-213">**Todoıtem**</span><span class="sxs-lookup"><span data-stu-id="10ade-213">**TodoItem**</span></span>

| <span data-ttu-id="10ade-214">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="10ade-214">Attribute</span></span> | <span data-ttu-id="10ade-215">Tür</span><span class="sxs-lookup"><span data-stu-id="10ade-215">Type</span></span> | <span data-ttu-id="10ade-216">Not</span><span class="sxs-lookup"><span data-stu-id="10ade-216">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10ade-217">id</span><span class="sxs-lookup"><span data-stu-id="10ade-217">id</span></span> | <span data-ttu-id="10ade-218">Dize, gerekli olarak işaretlenmiş</span><span class="sxs-lookup"><span data-stu-id="10ade-218">String, marked required</span></span> |<span data-ttu-id="10ade-219">Uzak Depolama birincil anahtar</span><span class="sxs-lookup"><span data-stu-id="10ade-219">Primary key in remote store</span></span> |
| <span data-ttu-id="10ade-220">Tamamlayın</span><span class="sxs-lookup"><span data-stu-id="10ade-220">complete</span></span> | <span data-ttu-id="10ade-221">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="10ade-221">Boolean</span></span> | <span data-ttu-id="10ade-222">Yapılacak iş öğesi alanı</span><span class="sxs-lookup"><span data-stu-id="10ade-222">To-do item field</span></span> |
| <span data-ttu-id="10ade-223">Metin</span><span class="sxs-lookup"><span data-stu-id="10ade-223">text</span></span> |<span data-ttu-id="10ade-224">Dize</span><span class="sxs-lookup"><span data-stu-id="10ade-224">String</span></span> |<span data-ttu-id="10ade-225">Yapılacak iş öğesi alanı</span><span class="sxs-lookup"><span data-stu-id="10ade-225">To-do item field</span></span> |
| <span data-ttu-id="10ade-226">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="10ade-226">createdAt</span></span> | <span data-ttu-id="10ade-227">Tarih</span><span class="sxs-lookup"><span data-stu-id="10ade-227">Date</span></span> | <span data-ttu-id="10ade-228">(isteğe bağlı) Eşlendiği **createdAt** sistem özelliği</span><span class="sxs-lookup"><span data-stu-id="10ade-228">(optional) Maps to **createdAt** system property</span></span> |
| <span data-ttu-id="10ade-229">updatedAt</span><span class="sxs-lookup"><span data-stu-id="10ade-229">updatedAt</span></span> | <span data-ttu-id="10ade-230">Tarih</span><span class="sxs-lookup"><span data-stu-id="10ade-230">Date</span></span> | <span data-ttu-id="10ade-231">(isteğe bağlı) Eşlendiği **updatedAt** sistem özelliği</span><span class="sxs-lookup"><span data-stu-id="10ade-231">(optional) Maps to **updatedAt** system property</span></span> |
| <span data-ttu-id="10ade-232">Sürüm</span><span class="sxs-lookup"><span data-stu-id="10ade-232">version</span></span> | <span data-ttu-id="10ade-233">Dize</span><span class="sxs-lookup"><span data-stu-id="10ade-233">String</span></span> | <span data-ttu-id="10ade-234">(isteğe bağlı) Çakışmaları, maps sürüme algılamak için kullanılan</span><span class="sxs-lookup"><span data-stu-id="10ade-234">(optional) Used to detect conflicts, maps to version</span></span> |

## <span data-ttu-id="10ade-235"><a name="setup-sync"></a>Uygulama eşitleme davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="10ade-235"><a name="setup-sync"></a>Change the sync behavior of the app</span></span>
<span data-ttu-id="10ade-236">Bu bölümde, uygulama başlatma ya da zaman eklemek ve öğeleri güncelleştirme üzerinde eşitlemez şekilde uygulama değiştirin.</span><span class="sxs-lookup"><span data-stu-id="10ade-236">In this section, you modify the app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="10ade-237">Yalnızca Yenile hareketi düğmesini gerçekleştirildiğinde eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="10ade-237">It syncs only when the refresh gesture button is performed.</span></span>

<span data-ttu-id="10ade-238">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="10ade-238">**Objective-C**:</span></span>

1. <span data-ttu-id="10ade-239">İçinde **QSTodoListViewController.m**, değiştirme **viewDidLoad** yöntemi çağrısı kaldırmak için `[self refresh]` yöntemi sonunda.</span><span class="sxs-lookup"><span data-stu-id="10ade-239">In **QSTodoListViewController.m**, change the **viewDidLoad** method to remove the call to `[self refresh]` at the end of the method.</span></span> <span data-ttu-id="10ade-240">Şimdi, uygulama başlatılırken sunucusuyla veri eşitlenmedi.</span><span class="sxs-lookup"><span data-stu-id="10ade-240">Now the data is not synced with the server on app start.</span></span> <span data-ttu-id="10ade-241">Bunun yerine, Yerel Depodaki içeriğini eşitlenip.</span><span class="sxs-lookup"><span data-stu-id="10ade-241">Instead, it's synced with the contents of the local store.</span></span>
2. <span data-ttu-id="10ade-242">İçinde **QSTodoService.m**, tanımını değiştirmek `addItem` böylece öğeyi eklendikten sonra eşitleme değil.</span><span class="sxs-lookup"><span data-stu-id="10ade-242">In **QSTodoService.m**, modify the definition of `addItem` so that it doesn't sync after the item is inserted.</span></span> <span data-ttu-id="10ade-243">Kaldırma `self syncData` engelleme ve şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="10ade-243">Remove the `self syncData` block and replace it with the following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="10ade-244">Tanımını değiştirmek `completeItem` daha önce belirtildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="10ade-244">Modify the definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="10ade-245">Bloğunu kaldırmak `self syncData` ve şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="10ade-245">Remove the block for `self syncData` and replace it with the following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="10ade-246">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="10ade-246">**Swift**:</span></span>

<span data-ttu-id="10ade-247">İçinde `viewDidLoad`, **ToDoTableViewController.swift**, uygulama başlangıç eşitlemeyi durdurma için burada gösterilen iki satırları açıklama.</span><span class="sxs-lookup"><span data-stu-id="10ade-247">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out the two lines shown here, to stop syncing on app start.</span></span> <span data-ttu-id="10ade-248">Bu yazma zaman birisi ekler veya öğeyi tamamlandıktan Swift Todo uygulaması hizmet güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="10ade-248">At the time of this writing, the Swift Todo app does not update the service when someone adds or completes an item.</span></span> <span data-ttu-id="10ade-249">Uygulama başlangıç hizmette yalnızca güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="10ade-249">It updates the service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="10ade-250"><a name="test-app"></a>Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="10ade-250"><a name="test-app"></a>Test the app</span></span>
<span data-ttu-id="10ade-251">Bu bölümde, çevrimdışı bir senaryo benzetimini yapmak için geçersiz bir URL bağlayın.</span><span class="sxs-lookup"><span data-stu-id="10ade-251">In this section, you connect to an invalid URL to simulate an offline scenario.</span></span> <span data-ttu-id="10ade-252">Veri öğeleri eklediğinizde, bunlar içinde tutulan yerel çekirdek verileri depolamak, ancak bunlar mobil uygulama arka ucu ile eşitlenmedi.</span><span class="sxs-lookup"><span data-stu-id="10ade-252">When you add data items, they're held in the local Core Data store, but they're not synced with the mobile-app back end.</span></span>

1. <span data-ttu-id="10ade-253">Mobil uygulama URL'sini değiştirmek **QSTodoService.m** bir geçersiz URL ve uygulamayı yeniden çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="10ade-253">Change the mobile-app URL in **QSTodoService.m** to an invalid URL, and run the app again:</span></span>

   <span data-ttu-id="10ade-254">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="10ade-254">**Objective-C**.</span></span> <span data-ttu-id="10ade-255">QSTodoService.m içinde:</span><span class="sxs-lookup"><span data-stu-id="10ade-255">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="10ade-256">**SWIFT**.</span><span class="sxs-lookup"><span data-stu-id="10ade-256">**Swift**.</span></span> <span data-ttu-id="10ade-257">ToDoTableViewController.swift içinde:</span><span class="sxs-lookup"><span data-stu-id="10ade-257">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="10ade-258">Bazı Yapılacaklar öğelerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="10ade-258">Add some to-do items.</span></span> <span data-ttu-id="10ade-259">Simulator çıkın (veya zorla uygulamayı kapatmak) ve yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="10ade-259">Quit the simulator (or forcibly close the app), and then restart it.</span></span> <span data-ttu-id="10ade-260">Yaptığınız değişiklikleri kalıcı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="10ade-260">Verify that your changes persist.</span></span>

3. <span data-ttu-id="10ade-261">Uzak içeriğini görüntülemek **Todoıtem** tablosu:</span><span class="sxs-lookup"><span data-stu-id="10ade-261">View the contents of the remote **TodoItem** table:</span></span>
   * <span data-ttu-id="10ade-262">Node.js arka ucu için Git [Azure portal](https://portal.azure.com/) ve, mobil uygulama arka ucu içinde tıklatın **kolay tablolar** > **Todoıtem**.</span><span class="sxs-lookup"><span data-stu-id="10ade-262">For a Node.js back end, go to the [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="10ade-263">Bir .NET geri için sonlandırmak için SQL Server Management Studio gibi bir SQL aracı veya Fiddler veya Postman gibi bir REST istemcisi kullanın.</span><span class="sxs-lookup"><span data-stu-id="10ade-263">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="10ade-264">Yeni öğelerin bulunduğunu doğrulayın *değil* edilmiş sunucuyla eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="10ade-264">Verify that the new items have *not* been synced with the server.</span></span>

5. <span data-ttu-id="10ade-265">Doğru bir şekilde geri URL'sini değiştirmek **QSTodoService.m**ve uygulamayı yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="10ade-265">Change the URL back to the correct one in **QSTodoService.m**, and rerun the app.</span></span>

6. <span data-ttu-id="10ade-266">Öğeleri listede aşağı çekerek yenileme hareketi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="10ade-266">Perform the refresh gesture by pulling down the list of items.</span></span>  
<span data-ttu-id="10ade-267">Devam eden değer değiştirici görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="10ade-267">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="10ade-268">Görünüm **Todoıtem** yeniden verileri.</span><span class="sxs-lookup"><span data-stu-id="10ade-268">View the **TodoItem** data again.</span></span> <span data-ttu-id="10ade-269">Yeni ve değiştirilen Yapılacaklar öğelerini şimdi görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="10ade-269">The new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="10ade-270">Özet</span><span class="sxs-lookup"><span data-stu-id="10ade-270">Summary</span></span>
<span data-ttu-id="10ade-271">Çevrimdışı eşitleme özelliğini desteklemek için kullandık `MSSyncTable` arabirim ve başlatıldı `MSClient.syncContext` yerel deposu.</span><span class="sxs-lookup"><span data-stu-id="10ade-271">To support the offline sync feature, we used the `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="10ade-272">Bu durumda, Yerel Depodaki çekirdek veri tabanlı bir veritabanı oluştu.</span><span class="sxs-lookup"><span data-stu-id="10ade-272">In this case, the local store was a Core Data-based database.</span></span>

<span data-ttu-id="10ade-273">Bir çekirdek veri yerel deposu kullandığınızda, birkaç tablolarla tanımlamalısınız [düzeltmek Sistem Özellikleri](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="10ade-273">When you use a Core Data local store, you must define several tables with the [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="10ade-274">Normal oluşturma, okuma, güncelleştirme ve uygulama hala bağlı, ancak yerel depo tüm işlemleri ortaya gibi mobil uygulamaları iş için (CRUD) işlemleridir silin.</span><span class="sxs-lookup"><span data-stu-id="10ade-274">The normal create, read, update, and delete (CRUD) operations for mobile apps work as if the app is still connected, but all the operations occur against the local store.</span></span>

<span data-ttu-id="10ade-275">Yerel depodan sunucuyla eşitlendiğinde kullandık **MSSyncTable.pullWithQuery** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="10ade-275">When we synchronized the local store with the server, we used the **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="10ade-276">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="10ade-276">Additional resources</span></span>
* <span data-ttu-id="10ade-277">[mobil uygulamalarda çevrimdışı veri eşitlemeye]</span><span class="sxs-lookup"><span data-stu-id="10ade-277">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="10ade-278">[Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme] \(video Mobile Services hakkında olmakla birlikte, benzer şekilde Mobile Apps çevrimdışı eşitleme çalışır.\)</span><span class="sxs-lookup"><span data-stu-id="10ade-278">[Cloud Cover: Offline Sync in Azure Mobile Services] \(The video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


<span data-ttu-id="10ade-279">[iOS uygulaması oluştur]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="10ade-279">[Create an iOS App]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="10ade-280">[mobil uygulamalarda çevrimdışı veri eşitlemeye]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="10ade-280">[Offline Data Sync in Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

<span data-ttu-id="10ade-281">[Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="10ade-281">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

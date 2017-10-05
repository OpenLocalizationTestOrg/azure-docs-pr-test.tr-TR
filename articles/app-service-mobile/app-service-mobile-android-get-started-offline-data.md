---
title: "Azure Mobile uygulamanız (Android) için çevrimdışı eşitlemeyi etkinleştirme"
description: "App Service Mobile Apps için önbellek ve eşitleme çevrimdışı veri Android uygulamanızdaki nasıl kullanılacağını öğrenin"
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 304323c1816302e8c1f68f36a029aee55e02c54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="25bad-103">Android mobil uygulamanızı için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="25bad-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="25bad-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="25bad-104">Overview</span></span>
<span data-ttu-id="25bad-105">Bu öğreticide, Android için Azure Mobile Apps, çevrimdışı eşitleme özelliği kapsar.</span><span class="sxs-lookup"><span data-stu-id="25bad-105">This tutorial covers the offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="25bad-106">Çevrimdışı eşitleme son kullanıcıların mobil uygulama ile etkileşim sağlar&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.</span><span class="sxs-lookup"><span data-stu-id="25bad-106">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="25bad-107">Değişiklikler yerel bir veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="25bad-107">Changes are stored in a local database.</span></span> <span data-ttu-id="25bad-108">Cihaz yeniden çevrimiçi olduğunda, bu değişiklikleri uzak arka uç ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="25bad-108">Once the device is back online, these changes are synced with the remote backend.</span></span>

<span data-ttu-id="25bad-109">Bu ilk Azure Mobile Apps deneyiminizi ise, öğreticinin ilk tamamlanmalıdır [Android uygulaması oluşturma].</span><span class="sxs-lookup"><span data-stu-id="25bad-109">If this is your first experience with Azure Mobile Apps, you should first complete the tutorial [Create an Android App].</span></span> <span data-ttu-id="25bad-110">İndirilen hızlı başlangıç sunucu projesi kullanmazsanız, veri erişim uzantısı paketlerini projenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="25bad-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="25bad-111">Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [.NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="25bad-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="25bad-112">Çevrimdışı eşitleme özelliği hakkında daha fazla bilgi için Ek Yardım konusuna [Azure Mobile Apps çevrimdışı veri eşitleme].</span><span class="sxs-lookup"><span data-stu-id="25bad-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-app-to-support-offline-sync"></a><span data-ttu-id="25bad-113">Çevrimdışı eşitleme desteklemek için uygulamayı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="25bad-113">Update the app to support offline sync</span></span>
<span data-ttu-id="25bad-114">Çevrimdışı eşitleme için okuma ve yazma gelen bir *eşitleme tablo* (kullanarak *IMobileServiceSyncTable* arabirimi), parçası olduğu bir **SQLite** aygıtınızda veritabanı.</span><span class="sxs-lookup"><span data-stu-id="25bad-114">With offline sync, you read to and write from a *sync table* (using the *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="25bad-115">İtme ve Azure Mobile Services ve aygıt arasındaki değişiklikleri çekme için kullandığınız bir *eşitleme bağlamı* (*MobileServiceClient.SyncContext*), hangi depolamak için yerel veritabanını başlatılamadı yerel veriler.</span><span class="sxs-lookup"><span data-stu-id="25bad-115">To push and pull changes between the device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with the local database to store data locally.</span></span>

1. <span data-ttu-id="25bad-116">İçinde `TodoActivity.java`, varolan tanımı çıkışı açıklama `mToDoTable` ve eşitleme tablo sürümü açıklamadan çıkarın:</span><span class="sxs-lookup"><span data-stu-id="25bad-116">In `TodoActivity.java`, comment out the existing definition of `mToDoTable` and uncomment the sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="25bad-117">İçinde `onCreate` yöntemi, mevcut başlatılması çıkışı açıklama `mToDoTable` ve bu tanımı açıklamadan çıkarın:</span><span class="sxs-lookup"><span data-stu-id="25bad-117">In the `onCreate` method, comment out the existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="25bad-118">İçinde `refreshItemsFromTable` tanımını çıkışı açıklama `results` ve bu tanımı açıklamadan çıkarın:</span><span class="sxs-lookup"><span data-stu-id="25bad-118">In `refreshItemsFromTable` comment out the definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="25bad-119">Açıklama tanımını çıkışı `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="25bad-119">Comment out the definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="25bad-120">Tanımını açıklamadan çıkarın `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="25bad-120">Uncomment the definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync the data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="25bad-121">Tanımını açıklamadan çıkarın `sync`:</span><span class="sxs-lookup"><span data-stu-id="25bad-121">Uncomment the definition of `sync`:</span></span>
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-the-app"></a><span data-ttu-id="25bad-122">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="25bad-122">Test the app</span></span>
<span data-ttu-id="25bad-123">Bu bölümde, WiFi ile davranışı üzerinde test ve çevrimdışı bir senaryo oluşturmak için WiFi devre dışı bırakma.</span><span class="sxs-lookup"><span data-stu-id="25bad-123">In this section, you test the behavior with WiFi on, and then turn off WiFi to create an offline scenario.</span></span>

<span data-ttu-id="25bad-124">Veri öğeleri eklediğinizde, bunlar yerel SQLite deposunda tutulur, ancak tuşuna kadar mobil hizmete eşitlenmedi **yenileme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="25bad-124">When you add data items, they are held in the local SQLite store, but not synced to the mobile service until you press the **Refresh** button.</span></span> <span data-ttu-id="25bad-125">Diğer uygulamalara veri eşitlenmesi gerektiği zaman ilgili farklı gereksinimlere sahip, ancak tanıtım amacıyla bu öğreticide açıkça isteği kullanıcı vardır.</span><span class="sxs-lookup"><span data-stu-id="25bad-125">Other apps may have different requirements regarding when data needs to be synchronized, but for demo purposes this tutorial has the user explicitly request it.</span></span>

<span data-ttu-id="25bad-126">Bu düğmesine bastığınızda, yeni bir arka plan görevi başlatır.</span><span class="sxs-lookup"><span data-stu-id="25bad-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="25bad-127">İlk eşitleme bağlamı sonra Azure çeken tüm değiştirilen verileri yerel tabloya kullanarak yerel depolama için yapılan tüm değişiklikler de iter.</span><span class="sxs-lookup"><span data-stu-id="25bad-127">It first pushes all changes made to the local store using synchronization context, then pulls all changed data from Azure to the local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="25bad-128">Çevrimdışı test etme</span><span class="sxs-lookup"><span data-stu-id="25bad-128">Offline testing</span></span>
1. <span data-ttu-id="25bad-129">Cihaz veya benzeticisinde yerleştirin *uçak modu*.</span><span class="sxs-lookup"><span data-stu-id="25bad-129">Place the device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="25bad-130">Bu, çevrimdışı bir senaryo doğurur.</span><span class="sxs-lookup"><span data-stu-id="25bad-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="25bad-131">Bazı eklemek *Yapılacaklar* öğeler veya bazı öğeler tamamlandı olarak işaretle.</span><span class="sxs-lookup"><span data-stu-id="25bad-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="25bad-132">Cihaz veya simulator çıkın (veya zorla uygulamayı kapatmak) ve yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="25bad-132">Quit the device or simulator (or forcibly close the app) and restart.</span></span> <span data-ttu-id="25bad-133">Tutuluyor çünkü yaptığınız değişiklikler aygıtta devam ediyor olduğunu doğrulayın yerel SQLite depodaki.</span><span class="sxs-lookup"><span data-stu-id="25bad-133">Verify that your changes have been persisted on the device because they are held in the local SQLite store.</span></span>
3. <span data-ttu-id="25bad-134">Azure içeriğini görüntüleyebilir *Todoıtem* SQL aracıyla ya da gibi tablo *SQL Server Management Studio*, veya bir REST istemcisi gibi *Fiddler* veya  *Postman*.</span><span class="sxs-lookup"><span data-stu-id="25bad-134">View the contents of the Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="25bad-135">Yeni öğelerin bulunduğunu doğrulayın *değil* edilmiş sunucuya eşitlendi</span><span class="sxs-lookup"><span data-stu-id="25bad-135">Verify that the new items have *not* been synced to the server</span></span>
   
       + <span data-ttu-id="25bad-136">Node.js arka ucu için Git [Azure portal](https://portal.azure.com/), tıklatıp mobil uygulamanızın arka uç **kolay tablolar** > **Todoıtem** içeriğinigörüntülemekiçin`TodoItem`tablo.</span><span class="sxs-lookup"><span data-stu-id="25bad-136">For a Node.js backend, go to the [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** to view the contents of the `TodoItem` table.</span></span>
       + <span data-ttu-id="25bad-137">Bir .NET arka ucu için bir SQL ile ya da aracı gibi İçindekiler görüntülemek *SQL Server Management Studio*, veya bir REST istemcisi gibi *Fiddler* veya *Postman*.</span><span class="sxs-lookup"><span data-stu-id="25bad-137">For a .NET backend, view the table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="25bad-138">WiFi üzerinde aygıt ya da simulator açın.</span><span class="sxs-lookup"><span data-stu-id="25bad-138">Turn on WiFi in the device or simulator.</span></span> <span data-ttu-id="25bad-139">Ardından, basın **yenileme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="25bad-139">Next, press the **Refresh** button.</span></span>
5. <span data-ttu-id="25bad-140">Todoıtem verileri Azure portalında yeniden görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="25bad-140">View the TodoItem data again in the Azure portal.</span></span> <span data-ttu-id="25bad-141">Yeni ve değiştirilmiş Todoıtems şimdi gösterilmelidir.</span><span class="sxs-lookup"><span data-stu-id="25bad-141">The new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25bad-142">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="25bad-142">Additional Resources</span></span>
* <span data-ttu-id="25bad-143">[Azure Mobile Apps çevrimdışı veri eşitleme]</span><span class="sxs-lookup"><span data-stu-id="25bad-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="25bad-144">[Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme] \(Not: video Mobile Services'de olsa da, çevrimdışı eşitleme Azure Mobile Apps benzer şekilde çalışır\)</span><span class="sxs-lookup"><span data-stu-id="25bad-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: the video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

<span data-ttu-id="25bad-145">[Azure Mobile Apps çevrimdışı veri eşitleme]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="25bad-145">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

<span data-ttu-id="25bad-146">[Android uygulaması oluşturma]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="25bad-146">[Create an Android App]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="25bad-147">[Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="25bad-147">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/


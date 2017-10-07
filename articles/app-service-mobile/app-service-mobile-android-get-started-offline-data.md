---
title: "aaaEnable çevrimdışı eşitleme için Azure mobil uygulamanız (Android)"
description: "Bilgi nasıl toouse App Service Mobile Apps toocache ve eşitleme çevrimdışı veri Android uygulamanızdaki"
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
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="f8d9e-103">Android mobil uygulamanızı için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f8d9e-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="f8d9e-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f8d9e-104">Overview</span></span>
<span data-ttu-id="f8d9e-105">Bu öğretici, Android için Azure Mobile Apps hello çevrimdışı eşitleme özelliği kapsar.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-105">This tutorial covers hello offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="f8d9e-106">Çevrimdışı eşitleme sağlayan bir mobil uygulama ile son kullanıcılar toointeract&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-106">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="f8d9e-107">Değişiklikler yerel bir veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-107">Changes are stored in a local database.</span></span> <span data-ttu-id="f8d9e-108">Merhaba aygıt yeniden çevrimiçi olduktan sonra bu değişiklikleri hello uzak arka uç ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-108">Once hello device is back online, these changes are synced with hello remote backend.</span></span>

<span data-ttu-id="f8d9e-109">İlk Azure Mobile Apps deneyiminizi varsa hello öğretici ilk tamamlanmalıdır [Android uygulaması oluşturma].</span><span class="sxs-lookup"><span data-stu-id="f8d9e-109">If this is your first experience with Azure Mobile Apps, you should first complete hello tutorial [Create an Android App].</span></span> <span data-ttu-id="f8d9e-110">Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, hello veri erişim uzantı paketleri tooyour projesi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="f8d9e-111">Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="f8d9e-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="f8d9e-112">Merhaba çevrimdışı eşitleme özelliği hakkında daha fazla toolearn hello konusuna bakın [Azure Mobile Apps çevrimdışı veri eşitleme].</span><span class="sxs-lookup"><span data-stu-id="f8d9e-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-app-toosupport-offline-sync"></a><span data-ttu-id="f8d9e-113">Merhaba uygulama toosupport çevrimdışı eşitleme güncelleştir</span><span class="sxs-lookup"><span data-stu-id="f8d9e-113">Update hello app toosupport offline sync</span></span>
<span data-ttu-id="f8d9e-114">Çevrimdışı Eşitleme ile tooand yazma'dan okuma bir *eşitleme tablo* (hello kullanarak *IMobileServiceSyncTable* arabirimi), parçası olduğu bir **SQLite** aygıtınızda veritabanı.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-114">With offline sync, you read tooand write from a *sync table* (using hello *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="f8d9e-115">kullandığınız toopush ve çekme değişiklikleri hello cihaz ve Azure Mobile Services arasında bir *eşitleme bağlamı* (*MobileServiceClient.SyncContext*), hangi hello yerel veritabanını başlatılamadı toostore verilerini yerel olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-115">toopush and pull changes between hello device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with hello local database toostore data locally.</span></span>

1. <span data-ttu-id="f8d9e-116">İçinde `TodoActivity.java`, yorum hello varolan tanımını çıkışı `mToDoTable` ve hello eşitleme tablo sürümü açıklamadan çıkarın:</span><span class="sxs-lookup"><span data-stu-id="f8d9e-116">In `TodoActivity.java`, comment out hello existing definition of `mToDoTable` and uncomment hello sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="f8d9e-117">Merhaba, `onCreate` yöntemi, yorum hello varolan başlatılması çıkışı `mToDoTable` ve bu tanımı açıklamadan çıkarın:</span><span class="sxs-lookup"><span data-stu-id="f8d9e-117">In hello `onCreate` method, comment out hello existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="f8d9e-118">İçinde `refreshItemsFromTable` açıklama hello tanımını çıkışı `results` ve bu tanımı açıklamadan çıkarın:</span><span class="sxs-lookup"><span data-stu-id="f8d9e-118">In `refreshItemsFromTable` comment out hello definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="f8d9e-119">Açıklama hello tanımını çıkışı `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-119">Comment out hello definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="f8d9e-120">Merhaba tanımını açıklamadan çıkarın `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="f8d9e-120">Uncomment hello definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="f8d9e-121">Merhaba tanımını açıklamadan çıkarın `sync`:</span><span class="sxs-lookup"><span data-stu-id="f8d9e-121">Uncomment hello definition of `sync`:</span></span>
   
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

## <a name="test-hello-app"></a><span data-ttu-id="f8d9e-122">Test hello uygulama</span><span class="sxs-lookup"><span data-stu-id="f8d9e-122">Test hello app</span></span>
<span data-ttu-id="f8d9e-123">Bu bölümde, üzerinde hello davranışı WiFi ile test ve sonra çevrimdışı bir senaryo WiFi toocreate açın.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-123">In this section, you test hello behavior with WiFi on, and then turn off WiFi toocreate an offline scenario.</span></span>

<span data-ttu-id="f8d9e-124">Veri öğeleri eklediğinizde, hello basın kadar bunlar hello yerel SQLite mağaza, ancak değil eşitlenen toohello mobil hizmet tutulur **yenileme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-124">When you add data items, they are held in hello local SQLite store, but not synced toohello mobile service until you press hello **Refresh** button.</span></span> <span data-ttu-id="f8d9e-125">Diğer uygulamalara veri eşitlenen toobe gerektiği zaman ilgili farklı gereksinimlere sahip, ancak tanıtım amacıyla bu öğreticide açıkça isteği hello kullanıcı vardır.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-125">Other apps may have different requirements regarding when data needs toobe synchronized, but for demo purposes this tutorial has hello user explicitly request it.</span></span>

<span data-ttu-id="f8d9e-126">Bu düğmesine bastığınızda, yeni bir arka plan görevi başlatır.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="f8d9e-127">Önce tüm değişiklikleri toohello yerel deposu eşitleme bağlamı sonra Azure toohello yerel tablodan tüm çeken değiştirilen verileri kullanarak iter.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-127">It first pushes all changes made toohello local store using synchronization context, then pulls all changed data from Azure toohello local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="f8d9e-128">Çevrimdışı test etme</span><span class="sxs-lookup"><span data-stu-id="f8d9e-128">Offline testing</span></span>
1. <span data-ttu-id="f8d9e-129">Yerleştir hello aygıt ya da benzeticisinde *uçak modu*.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-129">Place hello device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="f8d9e-130">Bu, çevrimdışı bir senaryo doğurur.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="f8d9e-131">Bazı eklemek *Yapılacaklar* öğeler veya bazı öğeler tamamlandı olarak işaretle.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="f8d9e-132">Merhaba cihaz veya benzetici (veya zorla kapatma hello uygulama) çıkmak ve yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-132">Quit hello device or simulator (or forcibly close hello app) and restart.</span></span> <span data-ttu-id="f8d9e-133">Tutuluyor çünkü değişikliklerinizi hello aygıtta devam ediyor olduğunu doğrulayın hello yerel SQLite deposunda.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-133">Verify that your changes have been persisted on hello device because they are held in hello local SQLite store.</span></span>
3. <span data-ttu-id="f8d9e-134">Görüntüleme hello Azure Merhaba içeriğine *Todoıtem* SQL aracıyla ya da gibi tablo *SQL Server Management Studio*, veya REST istemcisi gibi *Fiddler* veya  *Postman*.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-134">View hello contents of hello Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="f8d9e-135">Merhaba yeni öğelerin bulunduğunu doğrulayın *değil* eşitlenen toohello sunucu edildi</span><span class="sxs-lookup"><span data-stu-id="f8d9e-135">Verify that hello new items have *not* been synced toohello server</span></span>
   
       + <span data-ttu-id="f8d9e-136">Node.js arka ucu için toohello Git [Azure portal](https://portal.azure.com/), tıklatıp mobil uygulamanızın arka uç **kolay tablolar** > **Todoıtem** hello tooviewMerhabaiçeriğine`TodoItem` tablo.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-136">For a Node.js backend, go toohello [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** tooview hello contents of hello `TodoItem` table.</span></span>
       + <span data-ttu-id="f8d9e-137">Bir .NET arka ucu için Görünüm hello tablosu bir SQL aracı ile ya da gibi içeriği *SQL Server Management Studio*, veya bir REST istemcisi gibi *Fiddler* veya *Postman*.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-137">For a .NET backend, view hello table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="f8d9e-138">WiFi üzerinde hello aygıt ya da simulator açın.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-138">Turn on WiFi in hello device or simulator.</span></span> <span data-ttu-id="f8d9e-139">Ardından, hello'e basın **yenileme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-139">Next, press hello **Refresh** button.</span></span>
5. <span data-ttu-id="f8d9e-140">Merhaba Todoıtem verileri hello Azure portalında yeniden görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-140">View hello TodoItem data again in hello Azure portal.</span></span> <span data-ttu-id="f8d9e-141">Merhaba yeni ve değiştirilmiş Todoıtems şimdi gösterilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f8d9e-141">hello new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8d9e-142">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f8d9e-142">Additional Resources</span></span>
* <span data-ttu-id="f8d9e-143">[Azure Mobile Apps çevrimdışı veri eşitleme]</span><span class="sxs-lookup"><span data-stu-id="f8d9e-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="f8d9e-144">[Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme] \(Not: hello video Mobile Services'de olsa da, çevrimdışı eşitleme Azure Mobile Apps benzer şekilde çalışır\)</span><span class="sxs-lookup"><span data-stu-id="f8d9e-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: hello video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[Azure Mobile Apps çevrimdışı veri eşitleme]: app-service-mobile-offline-data-sync.md

[Android uygulaması oluşturma]: app-service-mobile-android-get-started.md

[Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/


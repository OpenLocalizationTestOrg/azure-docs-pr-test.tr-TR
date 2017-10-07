---
title: "aaaEnable çevrimdışı eşitleme Azure mobil uygulamanızın (Xamarin.Forms) | Microsoft Docs"
description: "Bilgi nasıl toouse mobil uygulama hizmeti toocache ve eşitleme çevrimdışı veri Xamarin.Forms uygulamanızda"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="82b43-103">Xamarin.Forms mobil uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="82b43-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="82b43-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="82b43-104">Overview</span></span>
<span data-ttu-id="82b43-105">Bu öğretici Azure Mobile Apps hello çevrimdışı eşitleme özelliği için Xamarin.Forms tanıtır.</span><span class="sxs-lookup"><span data-stu-id="82b43-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="82b43-106">Çevrimdışı eşitleme son kullanıcıların görüntüleme, ekleme veya ağ bağlantısı olduğunda bile veri--değiştirme bir mobil uygulamayla--etkileşime olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="82b43-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="82b43-107">Değişiklikler yerel bir veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="82b43-107">Changes are stored in a local database.</span></span> <span data-ttu-id="82b43-108">Merhaba aygıt yeniden çevrimiçi olduktan sonra bu değişiklikleri hello uzak hizmeti ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="82b43-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="82b43-109">Bu öğretici hello Xamarin.Forms hızlı başlangıç çözüm üzerinde Mobile Apps için [bir Xamarin iOS uygulaması oluştur] öğreticiyi tamamladığınızda oluşturduğunuz temel alır.</span><span class="sxs-lookup"><span data-stu-id="82b43-109">This tutorial is based on hello Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="82b43-110">Xamarin.Forms Hello hızlı başlangıç çözüm yalnızca etkin toobe gereken hello kod toosupport çevrimdışı eşitleme, içerir.</span><span class="sxs-lookup"><span data-stu-id="82b43-110">hello quickstart solution for Xamarin.Forms contains hello code toosupport offline sync, which just needs toobe enabled.</span></span> <span data-ttu-id="82b43-111">Bu öğreticide, hello hızlı başlangıç çözüm tooturn hello çevrimdışı Azure Mobile Apps özelliklerini üzerinde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="82b43-111">In this tutorial, you update hello quickstart solution tooturn on hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="82b43-112">Biz de hello çevrimdışı özgü hello uygulama kodunda vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="82b43-112">We also highlight hello offline-specific code in hello app.</span></span> <span data-ttu-id="82b43-113">Merhaba indirilen hızlı başlangıç çözümü kullanmıyorsanız hello veri erişim uzantı paketleri tooyour projesi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="82b43-113">If you do not use hello downloaded quickstart solution, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="82b43-114">Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş][1].</span><span class="sxs-lookup"><span data-stu-id="82b43-114">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="82b43-115">Merhaba çevrimdışı eşitleme özelliği hakkında daha fazla toolearn hello konusuna bakın [Azure Mobile Apps çevrimdışı veri eşitleme][2].</span><span class="sxs-lookup"><span data-stu-id="82b43-115">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a><span data-ttu-id="82b43-116">Çevrimdışı eşitleme işlevselliği hello hızlı başlangıç çözümde etkinleştir</span><span class="sxs-lookup"><span data-stu-id="82b43-116">Enable offline sync functionality in hello quickstart solution</span></span>
<span data-ttu-id="82b43-117">Merhaba çevrimdışı eşitleme kod, C# önişlemci yönergeleri kullanarak hello projesinde eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="82b43-117">hello offline sync code is included in hello project by using C# preprocessor directives.</span></span> <span data-ttu-id="82b43-118">Ne zaman hello **çevrimdışı\_eşitleme\_etkin** simgesiyle tanımlanır, bu kod yolları hello derlemede dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="82b43-118">When hello **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in hello build.</span></span> <span data-ttu-id="82b43-119">Windows uygulamaları için hello SQLite platform de yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="82b43-119">For Windows apps, you must also install hello SQLite platform.</span></span>

1. <span data-ttu-id="82b43-120">Visual Studio'da hello çözüme sağ tıklayın > **çözüm için NuGet paketlerini Yönet...** , ardından arayın ve yükleyin **Microsoft.Azure.Mobile.Client.SQLiteStore** hello Çözümdeki tüm projeleri için NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="82b43-120">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="82b43-121">Hello Çözüm Gezgini, ile Merhaba projenizden hello Todoıtemmanager.cs dosyasını açın **taşınabilir** taşınabilir sınıf kitaplığı proje olan hello ad sonra önişlemci yönergesi aşağıdaki hello açıklamadan çıkarın:</span><span class="sxs-lookup"><span data-stu-id="82b43-121">In hello Solution Explorer, open hello TodoItemManager.cs file from hello project with **Portable** in hello name, which is Portable Class Library project, then uncomment hello following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="82b43-122">(İsteğe bağlı) toosupport Windows cihazları, SQLite çalışma zamanı paketleri aşağıdaki hello birini yükleyin:</span><span class="sxs-lookup"><span data-stu-id="82b43-122">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="82b43-123">**Windows 8.1 çalışma zamanı:** yükleme [Windows 8.1 için SQLite][3].</span><span class="sxs-lookup"><span data-stu-id="82b43-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="82b43-124">**Windows Phone 8.1:** yükleme [Windows Phone 8.1 için SQLite][4].</span><span class="sxs-lookup"><span data-stu-id="82b43-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="82b43-125">**Evrensel Windows platformu** yükleme [hello Evrensel Windows Evrensel SQLite][5].</span><span class="sxs-lookup"><span data-stu-id="82b43-125">**Universal Windows Platform** Install [SQLite for hello Universal Windows Universal][5].</span></span>

     <span data-ttu-id="82b43-126">Merhaba quickstart Evrensel Windows projesi içermiyor rağmen hello Evrensel Windows platformu Xamarin Forms ile desteklenir.</span><span class="sxs-lookup"><span data-stu-id="82b43-126">Although hello quickstart does not contain a Universal Windows project, hello Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="82b43-127">(İsteğe bağlı) Her Windows uygulama projesine sağ **başvuruları** > **Başvuru Ekle...** , hello genişletin **Windows** klasörü > **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="82b43-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="82b43-128">Merhaba uygun etkinleştirmek **SQLite for Windows** SDK ile birlikte hello **için Visual C++ 2013 çalışma zamanı Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="82b43-128">Enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="82b43-129">Merhaba SQLite SDK adları biraz her Windows platformuyla farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="82b43-129">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="82b43-130">Merhaba istemci eşitleme kodu gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="82b43-130">Review hello client sync code</span></span>
<span data-ttu-id="82b43-131">Zaten hello Eğitmen kodu hello içinde içereceği kısa genel bakış işte `#if OFFLINE_SYNC_ENABLED` yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="82b43-131">Here is a brief overview of what is already included in hello tutorial code inside hello `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="82b43-132">Çevrimdışı eşitleme hello Todoıtemmanager.cs proje hello taşınabilir sınıf kitaplığı proje dosyasında bir işlevdir.</span><span class="sxs-lookup"><span data-stu-id="82b43-132">The offline sync functionality is in hello TodoItemManager.cs project file in hello Portable Class Library project.</span></span> <span data-ttu-id="82b43-133">Merhaba özelliği kavramsal bir genel bakış için bkz: [çevrimdışı veri eşitlemeye Azure Mobile Apps içinde][2].</span><span class="sxs-lookup"><span data-stu-id="82b43-133">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="82b43-134">Tablo işlemleri gerçekleştirilmeden önce hello yerel depolama başlatılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="82b43-134">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="82b43-135">Merhaba yerel deposu veritabanı hello başlatılmış **TodoItemManager** koddan hello kullanarak sınıfı oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="82b43-135">hello local store database is initialized in hello **TodoItemManager** class constructor by using hello following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="82b43-136">Bu kod hello kullanarak yeni bir yerel SQLite veritabanı oluşturur **MobileServiceSQLiteStore** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="82b43-136">This code creates a new local SQLite database using hello **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="82b43-137">Merhaba **DefineTable** yöntemi, sağlanan hello türündeki hello alanlar eşleşen hello yerel deposunda bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="82b43-137">hello **DefineTable** method creates a table in hello local store that matches hello fields in hello provided type.</span></span>  <span data-ttu-id="82b43-138">Merhaba türü tooinclude hello uzak veritabanındaki tüm hello sütunları yok.</span><span class="sxs-lookup"><span data-stu-id="82b43-138">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="82b43-139">Bu, olası toostore bir sütun alt kümesi olur.</span><span class="sxs-lookup"><span data-stu-id="82b43-139">It is possible toostore a subset of columns.</span></span>
* <span data-ttu-id="82b43-140">Merhaba **todoTable** alanındaki **TodoItemManager** olan bir **IMobileServiceSyncTable** yerine tür **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="82b43-140">hello **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="82b43-141">Sınıfı bu kullanır hello yerel veritabanı tüm oluşturmak okuyun, Güncelleştir ve Sil (CRUD) tablo işlemleri.</span><span class="sxs-lookup"><span data-stu-id="82b43-141">This class uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="82b43-142">Ne zaman bu değişiklikleri toohello mobil uygulama arka ucu çağırarak gönderilen karar **PushAsync** hello üzerinde **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="82b43-142">You decide when those changes are pushed toohello Mobile App backend by calling **PushAsync** on hello **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="82b43-143">Merhaba eşitleme bağlamı tablo ilişkileri izleme ve bir istemci uygulaması değiştiren tüm tablolarda değişiklikleri Ftp'den korunmasına yardımcı olur **PushAsync** olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="82b43-143">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="82b43-144">Merhaba aşağıdaki **SyncAsync** yöntemi toosync hello mobil uygulama arka ucu ile çağrılır:</span><span class="sxs-lookup"><span data-stu-id="82b43-144">hello following **SyncAsync** method is called toosync with hello Mobile App backend:</span></span>

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting tooserver's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    <span data-ttu-id="82b43-145">Bu örnekte basit hata hello varsayılan eşitleme işleyiciyle işleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="82b43-145">This sample uses simple error handling with hello default sync handler.</span></span> <span data-ttu-id="82b43-146">Gerçek bir uygulamada ağ koşulları ve sunucu gibi çeşitli hatalar çakışmaları özel kullanarak hello işlemek **IMobileServiceSyncHandler** uygulaması.</span><span class="sxs-lookup"><span data-stu-id="82b43-146">A real application would handle hello various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="82b43-147">Çevrimdışı eşitleme konuları</span><span class="sxs-lookup"><span data-stu-id="82b43-147">Offline sync considerations</span></span>
<span data-ttu-id="82b43-148">Merhaba örnek hello **SyncAsync** yöntemi yalnızca adlı başlatma ve ne zaman bir eşitleme istedi.</span><span class="sxs-lookup"><span data-stu-id="82b43-148">In hello sample, hello **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="82b43-149">bir Android veya iOS uygulama hello öğeler listesindeki açılır menüsünden bir eşitleme tooinitiate; Windows için hello kullanma **eşitleme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="82b43-149">tooinitiate a sync in an Android or iOS app, pull down on hello items list; for Windows, use hello **Sync** button.</span></span> <span data-ttu-id="82b43-150">Gerçek dünya uygulamada Hello ağ durumu değiştiğinde hello eşitleme tetikleyici de yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82b43-150">In a real-world application, you could also make hello sync trigger when hello network state changes.</span></span>

<span data-ttu-id="82b43-151">Bir çekme beklemede olan bir tabloda karşı çalıştırıldığında yerel güncelleştirmeleri önceki bağlam push işlemi otomatik olarak Tetikleyicileri çekme hello bağlam tarafından izlenen.</span><span class="sxs-lookup"><span data-stu-id="82b43-151">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="82b43-152">Yenileme, ekleme ve bu örnek öğelerde Tamamlanıyor, atlayabilirsiniz olduğunda açık hello **PushAsync** çağırın.</span><span class="sxs-lookup"><span data-stu-id="82b43-152">When refreshing, adding, and completing items in this sample, you can omit hello explicit **PushAsync** call.</span></span>

<span data-ttu-id="82b43-153">Sağlanan hello kodda hello uzak Todoıtem tablosu tüm kayıtları seçmeleri istenir, ancak bu da olası toofilter kayıtları sorgu kimliği ve sorgu geçirerek çok**PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="82b43-153">In hello provided code, all records in hello remote TodoItem table are queried, but it is also possible toofilter records by passing a query id and query too**PushAsync**.</span></span> <span data-ttu-id="82b43-154">Daha fazla bilgi için hello bölümüne bakın *Artımlı eşitleme* içinde [çevrimdışı veri eşitlemeye Azure Mobile Apps içinde][2].</span><span class="sxs-lookup"><span data-stu-id="82b43-154">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="82b43-155">Merhaba istemci uygulaması çalıştırın</span><span class="sxs-lookup"><span data-stu-id="82b43-155">Run hello client app</span></span>
<span data-ttu-id="82b43-156">Şu anda etkin çevrimdışı eşitleme ile Merhaba istemci uygulaması her platform toopopulate hello yerel deposu veritabanı üzerinde en az bir kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82b43-156">With offline sync now enabled, run hello client application at least once on each platform toopopulate hello local store database.</span></span> <span data-ttu-id="82b43-157">Daha sonra çevrimdışı bir senaryo benzetimini hello uygulama çevrimdışı durumdayken hello verileri ve hello Yerel Depodaki değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82b43-157">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="update-hello-sync-behavior-of-hello-client-app"></a><span data-ttu-id="82b43-158">Merhaba istemci uygulamanın Hello eşitleme davranışı güncelleştir</span><span class="sxs-lookup"><span data-stu-id="82b43-158">Update hello sync behavior of hello client app</span></span>
<span data-ttu-id="82b43-159">Bu bölümde, hello istemci projesi toosimulate çevrimdışı bir senaryo arka ucunuz için geçersiz uygulama URL'si kullanarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="82b43-159">In this section, modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="82b43-160">Alternatif olarak, Cihazınızı çok taşıyarak ağ bağlantıları devre dışı dışı bırakabilirsiniz "Uçak modu."</span><span class="sxs-lookup"><span data-stu-id="82b43-160">Alternatively, you can turn off network connections by moving your device too"Airplane mode."</span></span>  <span data-ttu-id="82b43-161">Veri öğeleri ekleyin veya değiştirildiğinde, bu değişiklikleri hello yerel deposunda tutulan, ancak eşitlenmedi toohello arka uç veri depolamak hello bağlantı yeniden kurulur kurulmaz kadar.</span><span class="sxs-lookup"><span data-stu-id="82b43-161">When you add or change data items, these changes are held in hello local store, but not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="82b43-162">Hello Çözüm Gezgini, hello hello Constants.cs proje dosyasını açın **taşınabilir** proje ve hello değerini değiştirin `ApplicationURL` toopoint tooan geçersiz URL:</span><span class="sxs-lookup"><span data-stu-id="82b43-162">In hello Solution Explorer, open hello Constants.cs project file from hello **Portable** project and change hello value of `ApplicationURL` toopoint tooan invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="82b43-163">Açık hello Todoıtemmanager.cs hello dosyasından **taşınabilir** proje ardından ekleyin bir **catch** hello temel için **özel durum** sınıfı toohello **try... catch** engelleyin **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="82b43-163">Open hello TodoItemManager.cs file from hello **Portable** project, then add a **catch** for hello base **Exception** class toohello **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="82b43-164">Bu **catch** blok hello özel durum iletisi toohello konsolu gibi Yazar:</span><span class="sxs-lookup"><span data-stu-id="82b43-164">This **catch** block writes hello exception message toohello console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="82b43-165">Derleme ve hello istemci uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82b43-165">Build and run hello client app.</span></span>  <span data-ttu-id="82b43-166">Bazı yeni öğeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="82b43-166">Add some new items.</span></span> <span data-ttu-id="82b43-167">Bir özel durum her girişimi toosync hello arka ucu ile için hello konsolunda kaydedilir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="82b43-167">Notice that an exception is logged in hello console for each attempt toosync with hello backend.</span></span> <span data-ttu-id="82b43-168">Toohello mobil arka uç gönderilemez kadar bu yeni öğeler hello yerel depoda yalnızca mevcut.</span><span class="sxs-lookup"><span data-stu-id="82b43-168">These new items exist only in hello local store until they can be pushed toohello mobile backend.</span></span> <span data-ttu-id="82b43-169">Bu gibi bağlı toohello arka uç, tüm oluşturma, okuma destekleyen, güncelleştirme, Sil (CRUD) işlemleri hello istemci uygulaması davranır.</span><span class="sxs-lookup"><span data-stu-id="82b43-169">hello client app behaves as if it is connected toohello backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="82b43-170">Merhaba uygulamasını kapatın ve oluşturduğunuz hello yeni öğeler kalıcı toohello yerel deposu olduğunu tooverify yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="82b43-170">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="82b43-171">(İsteğe bağlı) Visual Studio tooview hello arka uç veritabanı hello verilerde değişmediğini, Azure SQL veritabanı tablosu toosee kullanın.</span><span class="sxs-lookup"><span data-stu-id="82b43-171">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="82b43-172">Visual Studio'da açın **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="82b43-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="82b43-173">Tooyour veritabanında gidin **Azure**->**SQL veritabanları**.</span><span class="sxs-lookup"><span data-stu-id="82b43-173">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="82b43-174">Veritabanınıza sağ tıklatıp **SQL Server nesne Gezgini'nde Aç**.</span><span class="sxs-lookup"><span data-stu-id="82b43-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="82b43-175">Şimdi tooyour SQL veritabanı tablosunda ve içeriği göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82b43-175">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a><span data-ttu-id="82b43-176">Mobil arka Hello istemci uygulaması tooreconnect güncelleştir</span><span class="sxs-lookup"><span data-stu-id="82b43-176">Update hello client app tooreconnect your mobile backend</span></span>
<span data-ttu-id="82b43-177">Bu bölümde, hangi tooan çevrimiçi duruma gelmeye hello uygulama benzetim hello uygulama toohello mobil arka uç, yeniden bağlanın.</span><span class="sxs-lookup"><span data-stu-id="82b43-177">In this section, reconnect hello app toohello mobile backend, which simulates hello app coming back tooan online state.</span></span> <span data-ttu-id="82b43-178">Merhaba yenileme hareketi gerçekleştirdiğinizde, eşitlenen tooyour mobil arka uç verilerdir.</span><span class="sxs-lookup"><span data-stu-id="82b43-178">When you perform hello refresh gesture, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="82b43-179">Constants.cs yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="82b43-179">Reopen Constants.cs.</span></span> <span data-ttu-id="82b43-180">Doğru hello `applicationURL` toopoint toohello URL düzeltin.</span><span class="sxs-lookup"><span data-stu-id="82b43-180">Correct hello `applicationURL` toopoint toohello correct URL.</span></span>
2. <span data-ttu-id="82b43-181">Yeniden oluşturma ve hello istemci uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82b43-181">Rebuild and run hello client app.</span></span> <span data-ttu-id="82b43-182">Merhaba uygulama başlatıldıktan sonra toosync hello mobil uygulama arka ucu ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="82b43-182">hello app attempts toosync with hello mobile app backend after launching.</span></span> <span data-ttu-id="82b43-183">Hiçbir özel durum hello hata ayıklama konsolunda tutulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="82b43-183">Verify that no exceptions are logged in hello debug console.</span></span>
3. <span data-ttu-id="82b43-184">(İsteğe bağlı) Görünüm hello güncelleştirilmiş verileri SQL Server Nesne Gezgini veya Fiddler gibi bir REST araç kullanarak veya [Postman][6].</span><span class="sxs-lookup"><span data-stu-id="82b43-184">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="82b43-185">Bildirim hello veri hello arka uç veritabanı ve hello yerel deposu arasında eşitlendi.</span><span class="sxs-lookup"><span data-stu-id="82b43-185">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="82b43-186">Merhaba veri hello yerel deposu hello veritabanı arasında eşitlenen ve uygulamanızı değilken eklediğiniz hello öğelerini içeren dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="82b43-186">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82b43-187">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="82b43-187">Additional Resources</span></span>
* <span data-ttu-id="82b43-188">[Azure Mobile Apps çevrimdışı veri eşitleme][2]</span><span class="sxs-lookup"><span data-stu-id="82b43-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="82b43-189">[Azure Mobile Apps .NET SDK'sı nasıl yapılır][8]</span><span class="sxs-lookup"><span data-stu-id="82b43-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md

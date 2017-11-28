---
title: "aaaWorking hello App Service Mobile Apps ile yönetilen istemci kitaplığı (Windows | Microsoft Docs"
description: "Bilgi nasıl toouse Azure App Service Mobile Apps ile Windows ve Xamarin uygulamaları için .NET istemcisi."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="7cc7c-103">Nasıl toouse hello Azure Mobile Apps için yönetilen</span><span class="sxs-lookup"><span data-stu-id="7cc7c-103">How toouse hello managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="7cc7c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7cc7c-104">Overview</span></span>
<span data-ttu-id="7cc7c-105">Bu kılavuz size nasıl hello kullanarak tooperform genel senaryolar için Azure App Service Mobile uygulamaları Windows ve Xamarin uygulamaları için istemci kitaplığı yönetilen gösterir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-105">This guide shows you how tooperform common scenarios using hello managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="7cc7c-106">Yeni tooMobile uygulamalar varsa, ilk Tamamlanıyor hello düşünmelisiniz [Azure Mobile Apps quickstart] [ 1] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-106">If you are new tooMobile Apps, you should consider first completing hello [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="7cc7c-107">Bu kılavuzda, biz hello üzerinde odaklanmak istemci-tarafı yönetilen SDK.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-107">In this guide, we focus on hello client-side managed SDK.</span></span> <span data-ttu-id="7cc7c-108">toolearn hakkında daha fazla bilgi mobil uygulamaları için sunucu tarafı SDK'ları Merhaba, hello hello belgelerine bakın [.NET Server SDK] [ 2] veya [Node.js sunucusu SDK] [ 3].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-108">toolearn more about hello server-side SDKs for Mobile Apps, see hello documentation for hello [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="7cc7c-109">Başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="7cc7c-109">Reference documentation</span></span>
<span data-ttu-id="7cc7c-110">Merhaba başvuru belgeleri hello istemci SDK'sı için aşağıda bulunur: [Azure Mobile Apps .NET istemci başvurusu][4].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-110">hello reference documentation for hello client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="7cc7c-111">Hello birkaç istemci örnekleri de bulabilirsiniz [Azure-Samples GitHub deposunu][5].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-111">You can also find several client samples in hello [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="7cc7c-112">Desteklenen platformlar</span><span class="sxs-lookup"><span data-stu-id="7cc7c-112">Supported Platforms</span></span>
<span data-ttu-id="7cc7c-113">Merhaba .NET platformu hello aşağıdaki platformları destekler:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-113">hello .NET Platform supports hello following platforms:</span></span>

* <span data-ttu-id="7cc7c-114">Xamarin Android API 19 için 24 (KitKat Nougat aracılığıyla) aracılığıyla yayımlar.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="7cc7c-115">Xamarin iOS iOS 8.0 ve sonraki sürümler için serbest bırakır</span><span class="sxs-lookup"><span data-stu-id="7cc7c-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="7cc7c-116">Evrensel Windows platformu</span><span class="sxs-lookup"><span data-stu-id="7cc7c-116">Universal Windows Platform</span></span>
* <span data-ttu-id="7cc7c-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="7cc7c-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="7cc7c-118">Windows Phone 8.0 Silverlight uygulamalarının dışında</span><span class="sxs-lookup"><span data-stu-id="7cc7c-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="7cc7c-119">Merhaba "sunucu akış" kimlik doğrulaması için kullanıcı Arabirimi sunulan hello bir Web görünümü kullanır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-119">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="7cc7c-120">Merhaba cihaz mümkün toopresent WebView UI değilse, diğer kimlik doğrulama yöntemlerini gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-120">If hello device is not able toopresent a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="7cc7c-121">Bu SDK böylece Gözcü türü veya benzer şekilde kısıtlı aygıtlar için uygun değil.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="7cc7c-122"><a name="setup"></a>Kurulum ve Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7cc7c-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="7cc7c-123">Zaten oluşturulmuş ve en az bir tablo içeren mobil uygulama arka uç projeniz, yayımlanan olduğunu varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="7cc7c-124">Bu konuda kullanılan hello kodda hello tablo adlı `TodoItem` ve sütunları aşağıdaki hello vardır: `Id`, `Text`, ve `Complete`.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-124">In hello code used in this topic, hello table is named `TodoItem` and it has hello following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="7cc7c-125">Aynı tablo oluşturulan tamamladığınızda hello bu tablodur [Azure Mobile Apps quickstart][1].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-125">This table is hello same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="7cc7c-126">Merhaba karşılık gelen yazılan istemci-tarafı C# sınıfı aşağıdaki hello türüdür:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-126">hello corresponding typed client-side type in C# is hello following class:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

<span data-ttu-id="7cc7c-127">Merhaba [JsonPropertyAttribute] [ 6] kullanılan toodefine hello olan *PropertyName* hello istemci alanı ve hello tablo alanı arasında eşleme.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-127">hello [JsonPropertyAttribute][6] is used toodefine hello *PropertyName* mapping between hello client field and hello table field.</span></span>

<span data-ttu-id="7cc7c-128">nasıl toocreate tabloları, Mobile Apps arka toolearn bkz hello [.NET Server SDK konu] [ 7] veya hello [Node.js sunucusu SDK konusuna] [ 8] .</span><span class="sxs-lookup"><span data-stu-id="7cc7c-128">toolearn how toocreate tables in your Mobile Apps backend, see hello [.NET Server SDK topic][7] or hello [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="7cc7c-129">Mobil uygulama arka oluşturduysanız hello Azure hızlı başlangıç Merhaba portal kullanarak, hello de kullanabilirsiniz **kolay tablolar** hello ayarı [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-129">If you created your Mobile App backend in hello Azure portal using hello QuickStart, you can also use hello **Easy tables** setting in hello [Azure portal].</span></span>

### <a name="how-to-install-hello-managed-client-sdk-package"></a><span data-ttu-id="7cc7c-130">Nasıl yapılır: yükleme hello yönetilen istemci SDK paketi</span><span class="sxs-lookup"><span data-stu-id="7cc7c-130">How to: Install hello managed client SDK package</span></span>
<span data-ttu-id="7cc7c-131">Yöntemleri tooinstall hello aşağıdaki hello birini mobil uygulamaları için İstemci SDK paketi yönetilen [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-131">Use one of hello following methods tooinstall hello managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="7cc7c-132">**Visual Studio** projenize sağ tıklayın, **NuGet paketlerini Yönet**, hello Ara `Microsoft.Azure.Mobile.Client` paketini ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="7cc7c-133">**Xamarin Studio** projenize sağ tıklayın, **Ekle** > **NuGet paketleri Ekle**, hello Ara `Microsoft.Azure.Mobile.Client `paketini ve ardından **Ekle Paket**.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="7cc7c-134">Ana etkinlik dosyanızda tooadd hello aşağıdakileri unutmayın **kullanarak** deyimi:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-134">In your main activity file, remember tooadd hello following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="7cc7c-135"><a name="symbolsource"></a>Nasıl yapılır: Visual Studio'da hata ayıklama simgeleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7cc7c-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="7cc7c-136">Merhaba Microsoft.Azure.Mobile ad alanı Hello simgelerini bulunur [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-136">hello symbols for hello Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="7cc7c-137">Toothe başvuran [SymbolSource yönergeleri] [ 11] toointegrate SymbolSource Visual Studio ile.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-137">Refer toothe [SymbolSource instructions][11] toointegrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="7cc7c-138"><a name="create-client"></a>Merhaba Mobile Apps istemci oluşturma</span><span class="sxs-lookup"><span data-stu-id="7cc7c-138"><a name="create-client"></a>Create hello Mobile Apps client</span></span>
<span data-ttu-id="7cc7c-139">Merhaba aşağıdaki kod oluşturur hello [MobileServiceClient] [ 12] kullanılan tooaccess olan nesne, mobil uygulamanızın arka ucuna.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-139">hello following code creates hello [MobileServiceClient][12] object that is used tooaccess your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="7cc7c-140">Kod önceki hello yerine `MOBILE_APP_URL` hello mobil uygulama arka ucu hello URL'SİYLE hangi bulunursa, mobil uygulamanızın arka ucuna hello içinde dikey [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-140">In hello preceding code, replace `MOBILE_APP_URL` with hello URL of hello Mobile App backend, which is found in the blade for your Mobile App backend in hello [Azure portal].</span></span> <span data-ttu-id="7cc7c-141">Merhaba MobileServiceClient nesne singleton olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-141">hello MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="7cc7c-142">Tablolarla çalışma</span><span class="sxs-lookup"><span data-stu-id="7cc7c-142">Work with Tables</span></span>
<span data-ttu-id="7cc7c-143">Aşağıdaki bölümde ayrıntılara nasıl hello toosearch kayıtlarını almak ve hello tablo içindeki hello verileri değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-143">hello following section details how toosearch and retrieve records and modify hello data within hello table.</span></span>  <span data-ttu-id="7cc7c-144">Aşağıdaki konularda hello ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-144">hello following topics are covered:</span></span>

* [<span data-ttu-id="7cc7c-145">Bir tablo başvurusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7cc7c-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="7cc7c-146">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="7cc7c-146">Query data</span></span>](#querying)
* [<span data-ttu-id="7cc7c-147">Döndürülen veri filtreleme</span><span class="sxs-lookup"><span data-stu-id="7cc7c-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="7cc7c-148">Döndürülen veriler sıralama</span><span class="sxs-lookup"><span data-stu-id="7cc7c-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="7cc7c-149">Dönüş verileri sayfalarında</span><span class="sxs-lookup"><span data-stu-id="7cc7c-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="7cc7c-150">Belirli sütunları seçin</span><span class="sxs-lookup"><span data-stu-id="7cc7c-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="7cc7c-151">Bir kayıt kimliğine göre arama</span><span class="sxs-lookup"><span data-stu-id="7cc7c-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="7cc7c-152">Türsüz sorgularıyla ele alma</span><span class="sxs-lookup"><span data-stu-id="7cc7c-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="7cc7c-153">Veri ekleme</span><span class="sxs-lookup"><span data-stu-id="7cc7c-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="7cc7c-154">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7cc7c-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="7cc7c-155">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="7cc7c-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="7cc7c-156">Çakışma çözümü ve iyimser eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="7cc7c-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="7cc7c-157">Bağlama tooa Windows kullanıcı arabirimi</span><span class="sxs-lookup"><span data-stu-id="7cc7c-157">Binding tooa Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="7cc7c-158">Merhaba sayfa boyutunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="7cc7c-158">Changing hello Page Size</span></span>](#pagesize)

### <span data-ttu-id="7cc7c-159"><a name="instantiating"></a>Nasıl yapılır: bir tablo başvurusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7cc7c-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="7cc7c-160">Erişen ve arka uç tablodaki verileri değiştiren tüm hello kod üzerinde hello işlevleri çağırır `MobileServiceTable` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-160">All hello code that accesses or modifies data in a backend table calls functions on hello `MobileServiceTable` object.</span></span> <span data-ttu-id="7cc7c-161">Bir başvuru toohello tablosu tarafından arama hello elde [GetTable] şekilde yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-161">Obtain a reference toohello table by calling hello [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="7cc7c-162">Merhaba, nesne hello yazılan serileştirme modelini kullanan döndürdü.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-162">hello returned object uses hello typed serialization model.</span></span> <span data-ttu-id="7cc7c-163">Türsüz serileştirme modeli de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="7cc7c-164">Aşağıdaki örnek [başvuru tooan türü belirsiz bir tablo oluşturur]:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-164">The following example [creates a reference tooan untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="7cc7c-165">Türsüz sorgularda OData sorgu dizesi temel hello belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-165">In untyped queries, you must specify hello underlying OData query string.</span></span>

### <span data-ttu-id="7cc7c-166"><a name="querying"></a>Nasıl yapılır: Mobil uygulamanızın veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="7cc7c-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="7cc7c-167">Bu bölümde, nasıl tooissue işlevselliği aşağıdaki hello içeren toohello mobil uygulama arka sorgular açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-167">This section describes how tooissue queries toohello Mobile App backend, which includes hello following functionality:</span></span>

* [<span data-ttu-id="7cc7c-168">Döndürülen veri filtreleme</span><span class="sxs-lookup"><span data-stu-id="7cc7c-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="7cc7c-169">Döndürülen veriler sıralama</span><span class="sxs-lookup"><span data-stu-id="7cc7c-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="7cc7c-170">Dönüş verileri sayfalarında</span><span class="sxs-lookup"><span data-stu-id="7cc7c-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="7cc7c-171">Belirli sütunları seçin</span><span class="sxs-lookup"><span data-stu-id="7cc7c-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="7cc7c-172">Veri Kimliğe göre arayın</span><span class="sxs-lookup"><span data-stu-id="7cc7c-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="7cc7c-173">Bir sunucu tabanlı sayfa boyutu tüm satırları döndürülmesini zorlanan tooprevent ' dir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-173">A server-driven page size is enforced tooprevent all rows from being returned.</span></span>  <span data-ttu-id="7cc7c-174">Disk belleği hello hizmet olumsuz etkileyen büyük veri kümeleri için varsayılan istekleri tutar.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-174">Paging keeps default requests for large data sets from negatively impacting hello service.</span></span>  <span data-ttu-id="7cc7c-175">50 satır birden çok tooreturn kullanmak hello `Skip` ve `Take` açıklandığı gibi yöntemi [veri sayfalarında dönmek](#paging).</span><span class="sxs-lookup"><span data-stu-id="7cc7c-175">tooreturn more than 50 rows, use hello `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="7cc7c-176"><a name="filtering"></a>Nasıl yapılır: Filtre veri döndürdü</span><span class="sxs-lookup"><span data-stu-id="7cc7c-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="7cc7c-177">Merhaba aşağıdaki kod gösterir nasıl toofilter verileri de dahil olmak üzere bir `Where` sorgu yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-177">hello following code illustrates how toofilter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="7cc7c-178">Tüm öğeleri döndürür `todoTable` , `Complete` özelliği eşittir çok`false`.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-178">It returns all items from `todoTable` whose `Complete` property is equal too`false`.</span></span> <span data-ttu-id="7cc7c-179">Merhaba [burada] işlevi hello tablo hello sorgusu koşulu filtreleme bir satır uygular.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-179">hello [Where] function applies a row filtering predicate to hello query against hello table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="7cc7c-180">Tarayıcının geliştirici araçları gibi ileti denetleme yazılımı kullanarak hello hello gönderilen istek toohello arka uç URI'sini görüntüleyebilir veya [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-180">You can view hello URI of hello request sent toohello backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="7cc7c-181">URI hello isteğiyle bakarsanız, hello sorgu dizesi değiştirildiğini dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-181">If you look at hello request URI, notice that hello query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="7cc7c-182">Bu OData isteği hello Server SDK'sı tarafından bir SQL sorgusu çevrilir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-182">This OData request is translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="7cc7c-183">Merhaba toohello geçirilen işlevi `Where` yöntemi koşulları rastgele bir sayı olabilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-183">hello function that is passed toohello `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="7cc7c-184">Bu örnek SQL sorgusu hello Server SDK tarafından çevrilmesi:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-184">This example would be translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="7cc7c-185">Bu sorgu, birden çok yan tümcesine da bölünebilir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="7cc7c-186">Merhaba iki yöntem eşdeğerdir ve birbirlerinin yerine kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-186">hello two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="7cc7c-187">Önceki seçenek Hello&mdash;bir sorgu birden fazla koşullarında birleştirme,&mdash;daha compact ve önerilen.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-187">hello former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="7cc7c-188">Hello `Where` yan tümcesi olması işlemlerini destekleyen hello OData alt çevrilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-188">hello `Where` clause supports operations that be translated into hello OData subset.</span></span> <span data-ttu-id="7cc7c-189">İşlemler şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-189">Operations include:</span></span>

* <span data-ttu-id="7cc7c-190">İlişkisel işleçler (==,! =, <, < =, >, > =),</span><span class="sxs-lookup"><span data-stu-id="7cc7c-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="7cc7c-191">Aritmetik işleçler (+, -, /, *, %),</span><span class="sxs-lookup"><span data-stu-id="7cc7c-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="7cc7c-192">Precision (Math.Floor, Math.Ceiling), numara</span><span class="sxs-lookup"><span data-stu-id="7cc7c-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="7cc7c-193">Dize işlevleri (Uzunluk, Substring, Değiştir, IndexOf, StartsWith, EndsWith)</span><span class="sxs-lookup"><span data-stu-id="7cc7c-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="7cc7c-194">Tarih özellikleri (yıl, ay, gün, saat, dakika, saniye)</span><span class="sxs-lookup"><span data-stu-id="7cc7c-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="7cc7c-195">Erişim, nesne özelliklerini ve</span><span class="sxs-lookup"><span data-stu-id="7cc7c-195">Access properties of an object, and</span></span>
* <span data-ttu-id="7cc7c-196">Bu işlemleri birleştirme ifadeler.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="7cc7c-197">Ne göz önünde bulundurularak sunucusu SDK hello desteklediğinde, hello düşünebilirsiniz [OData v3 belgelerine].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-197">When considering what hello Server SDK supports, you can consider hello [OData v3 Documentation].</span></span>

### <span data-ttu-id="7cc7c-198"><a name="sorting"></a>Nasıl yapılır: sıralama döndürülen verileri</span><span class="sxs-lookup"><span data-stu-id="7cc7c-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="7cc7c-199">Merhaba aşağıdaki kod gösterir nasıl toosort verileri de dahil olmak üzere bir [OrderBy] veya [OrderByDescending] hello sorgusunda işlevi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-199">hello following code illustrates how toosort data by including an [OrderBy] or [OrderByDescending] function in hello query.</span></span> <span data-ttu-id="7cc7c-200">Öğelerden döndürür `todoTable` hello göre artan `Text` alan.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-200">It returns items from `todoTable` sorted ascending by hello `Text` field.</span></span>

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <span data-ttu-id="7cc7c-201"><a name="paging"></a>Nasıl yapılır: veri sayfalarında Döndür</span><span class="sxs-lookup"><span data-stu-id="7cc7c-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="7cc7c-202">Varsayılan olarak, hello arka uç yalnızca hello ilk 50 satırları döndürür.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-202">By default, hello backend returns only hello first 50 rows.</span></span> <span data-ttu-id="7cc7c-203">Arama hello tarafından döndürülen satır sayısını hello artırabilirsiniz [ele] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-203">You can increase hello number of returned rows by calling hello [Take] method.</span></span> <span data-ttu-id="7cc7c-204">Kullanım `Take` hello birlikte [atla] yöntemi toorequest "Merhaba sorgu tarafından döndürülen belirli bir sayfa" Merhaba toplam veri kümesinin.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-204">Use `Take` along with hello [Skip] method toorequest a specific "page" of hello total dataset returned by hello query.</span></span> <span data-ttu-id="7cc7c-205">Merhaba çalıştırıldığında, aşağıdaki sorguyu hello ilk üç öğeleri hello tablodaki döndürür.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-205">hello following query, when executed, returns hello top three items in hello table.</span></span>

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="7cc7c-206">Merhaba aşağıdaki değiştirilen sorgu atlar hello ilk üç sonuçları ve sonraki üç sonuçları döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-206">hello following revised query skips hello first three results and returns hello next three results.</span></span> <span data-ttu-id="7cc7c-207">Bu sorgu hello ikinci "sayfasının" Merhaba sayfa boyutu üç öğe olduğu veri üretir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-207">This query produces hello second "page" of data, where hello page size is three items.</span></span>

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="7cc7c-208">Merhaba [IncludeTotalCount] yöntemi için toplam sayıyı hello ister *tüm* Merhaba, belirtilen herhangi bir disk belleği/sınırı koşul yoksayılıyor verilinceye kaydeder:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-208">hello [IncludeTotalCount] method requests hello total count for *all* hello records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="7cc7c-209">Gerçek dünya uygulamada sayfaları arasında gezinmek için bir çağrı cihazı denetim veya karşılaştırılabilir UI örnekle önceki sorgular benzer toohello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-209">In a real world app, you can use queries similar toohello preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="7cc7c-210">toooverride hello 50 satır sınırı bir mobil uygulama arka ucu, hello de uygulamalısınız [EnableQueryAttribute] toohello genel alma yöntemini ve Başlangıç disk belleği davranışı belirtin.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-210">toooverride hello 50-row limit in a Mobile App backend, you must also apply hello [EnableQueryAttribute] toohello public GET method and specify hello paging behavior.</span></span> <span data-ttu-id="7cc7c-211">Ne zaman uygulanan toohello yöntemi, aşağıdaki hello en fazla döndürülen satır too1000 ayarlar:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-211">When applied toohello method, hello following sets the maximum returned rows too1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="7cc7c-212"><a name="selecting"></a>Nasıl yapılır: Belirli sütunları seçin</span><span class="sxs-lookup"><span data-stu-id="7cc7c-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="7cc7c-213">Özellikler tooinclude hello içinde hangi kümesi ekleyerek sonuçları belirtebilirsiniz bir [seçin] yan tümcesi tooyour sorgu.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-213">You can specify which set of properties tooinclude in hello results by adding a [Select] clause tooyour query.</span></span> <span data-ttu-id="7cc7c-214">Örneğin, kod gösterir nasıl aşağıdaki hello tooselect tek bir alana ve ayrıca nasıl tooselect ve birden çok alan Biçimlendir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-214">For example, hello following code shows how tooselect just one field and also how tooselect and format multiple fields:</span></span>

```
// Select one field -- just hello Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

<span data-ttu-id="7cc7c-215">Tüm işlevleri şimdiye kadar anlatılan hello olan biz zincirleme bunları tutmak için eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-215">All hello functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="7cc7c-216">Her zincirleme çağrı hello sorgusunun daha fazla etkiler.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-216">Each chained call affects more of hello query.</span></span> <span data-ttu-id="7cc7c-217">Daha fazla örnek:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="7cc7c-218"><a name="lookingup"></a>Nasıl yapılır: veri Kimliğe göre arayın</span><span class="sxs-lookup"><span data-stu-id="7cc7c-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="7cc7c-219">Merhaba [LookupAsync] işlevi kullanılan toolook nesneleri belirli bir kimliğe sahip hello veritabanından olabilir</span><span class="sxs-lookup"><span data-stu-id="7cc7c-219">hello [LookupAsync] function can be used toolook up objects from hello database with a particular ID.</span></span>

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="7cc7c-220"><a name="untypedqueries"></a>Nasıl yapılır: türsüz sorgularını Yürüt</span><span class="sxs-lookup"><span data-stu-id="7cc7c-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="7cc7c-221">Türsüz tablo nesneyi kullanarak bir sorgu yürütülürken açıkça hello OData sorgu dizesi çağırarak belirtmeniz gerekir [ReadAsync], aşağıdaki örneğine hello olarak:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-221">When executing a query using an untyped table object, you must explicitly specify hello OData query string by calling [ReadAsync], as in hello following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="7cc7c-222">Bir özellik paketi gibi kullandığınız JSON değerleri ulaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="7cc7c-223">Merhaba JToken ve Newtonsoft Json.NET hakkında daha fazla bilgi için bkz: [Json.NET] site.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-223">For more information on JToken and Newtonsoft Json.NET, see hello [Json.NET] site.</span></span>

### <span data-ttu-id="7cc7c-224"><a name="inserting"></a>Nasıl yapılır: bir mobil uygulama arka ucu veri Ekle</span><span class="sxs-lookup"><span data-stu-id="7cc7c-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="7cc7c-225">Tüm istemci türleri adlı bir üye içermelidir **kimliği**, olduğu varsayılan olarak bir dize.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="7cc7c-226">Bu **kimliği** CRUD işlemleri gerçekleştirmek için gereken ve koddan çevrimdışı eşitleme. Merhaba göstermektedir nasıl toouse hello [InsertAsync] yöntemi tooinsert yeni satırlar bir tabloya.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-226">This **Id** is required to perform CRUD operations and for offline sync. hello following code illustrates how toouse hello [InsertAsync] method tooinsert new rows into a table.</span></span> <span data-ttu-id="7cc7c-227">Merhaba parametresi .NET nesnesi olarak eklenen hello veri toobe içerir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-227">hello parameter contains hello data toobe inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="7cc7c-228">Benzersiz ve özel bir kimlik değeri hello dahil edilmemesi durumunda `todoItem` bir ekleme sırasında bir GUID hello sunucusu tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-228">If a unique custom ID value is not included in hello `todoItem` during an insert, a GUID is generated by hello server.</span></span>
<span data-ttu-id="7cc7c-229">Alabilirsiniz hello hello çağrısı döndükten sonra hello nesne inceleyerek kimliği oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-229">You can retrieve hello generated Id by inspecting hello object after hello call returns.</span></span>

<span data-ttu-id="7cc7c-230">Veri tooinsert türsüz, Json.NET yararlanmak:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-230">tooinsert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="7cc7c-231">Benzersiz bir dize kimliği olarak bir e-posta adresi kullanarak örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-231">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="7cc7c-232">KOD değerleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7cc7c-232">Working with ID values</span></span>
<span data-ttu-id="7cc7c-233">Mobil uygulamaları destekleyen özel benzersiz bir dize değerleri Merhaba tablonun için **kimliği** sütun.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-233">Mobile Apps supports unique custom string values for hello table's **id** column.</span></span> <span data-ttu-id="7cc7c-234">Bir dize değeri uygulamaların hello kimliği kullanıcı adlarını veya e-posta adresleri gibi özel değerler toouse sağlar.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-234">A string value allows applications toouse custom values such as email addresses or user names for hello ID.</span></span>  <span data-ttu-id="7cc7c-235">Dize kimlikleri ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-235">String IDs provide you with hello following benefits:</span></span>

* <span data-ttu-id="7cc7c-236">Gidiş dönüş toohello veritabanı yapmadan kimlikleri üretilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-236">IDs are generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="7cc7c-237">Farklı tablolar veya veritabanlarına daha kolay toomerge kayıtlarıdır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-237">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="7cc7c-238">Kimlikleri değerleri daha iyi bir uygulama mantığı ile tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-238">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="7cc7c-239">Bir dize kimliği değeri eklenen bir kayıtta ayarlanmadığında hello mobil uygulama arka ucu benzersiz bir değer için bir kimlik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-239">When a string ID value is not set on an inserted record, hello Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="7cc7c-240">Merhaba kullanabilirsiniz [Guid.NewGuid] kendi Kimliğinizi değerleri, hello istemcide veya hello arka uç yöntemi toogenerate.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-240">You can use hello [Guid.NewGuid] method toogenerate your own ID values, either on hello client or in hello backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="7cc7c-241"><a name="modifying"></a>Nasıl yapılır: bir mobil uygulama arka ucu verileri değiştirme</span><span class="sxs-lookup"><span data-stu-id="7cc7c-241"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="7cc7c-242">Merhaba aşağıdaki kod gösterir nasıl toouse hello [UpdateAsync] yöntemi tooupdate hello varolan bir kayıtla aynı kimliği yeni bilgilerle.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-242">hello following code illustrates how toouse hello [UpdateAsync] method tooupdate an existing record with hello same ID with new information.</span></span> <span data-ttu-id="7cc7c-243">Merhaba parametresi .NET nesnesi olarak güncelleştirilen hello veri toobe içerir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-243">hello parameter contains hello data toobe updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="7cc7c-244">tooupdate türsüz veri, avantajlarından alabilir [Json.NET] gibi:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-244">tooupdate untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="7cc7c-245">Bir `id` alan bir güncelleştirme yaparken belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-245">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="7cc7c-246">Merhaba arka uç kullanan hello `id` tooupdate satır alan tooidentify.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-246">hello backend uses hello `id` field tooidentify which row tooupdate.</span></span> <span data-ttu-id="7cc7c-247">Merhaba `id` alan hello hello sonucundan elde edilebilir `InsertAsync` çağırın.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-247">hello `id` field can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="7cc7c-248">Bir `ArgumentException` hello sağlamadan tooupdate öğeyi çalışırsanız tetiklenir `id` değeri.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-248">An `ArgumentException` is raised if you try tooupdate an item without providing hello `id` value.</span></span>

### <span data-ttu-id="7cc7c-249"><a name="deleting"></a>Nasıl yapılır: bir mobil uygulama arka ucu verileri Sil</span><span class="sxs-lookup"><span data-stu-id="7cc7c-249"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="7cc7c-250">Merhaba aşağıdaki kod gösterir nasıl toouse hello [DeleteAsync] yöntemi toodelete var olan bir örneği.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-250">hello following code illustrates how toouse hello [DeleteAsync] method toodelete an existing instance.</span></span> <span data-ttu-id="7cc7c-251">Merhaba örneği hello tarafından tanımlanan `id` alan hello kümesinde `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-251">hello instance is identified by hello `id` field set on hello `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="7cc7c-252">Veri toodelete türsüz, Json.NET avantajlarından şekilde alabilir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-252">toodelete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="7cc7c-253">Bir silme isteği yaptığınızda, bir kimliği belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-253">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="7cc7c-254">Diğer özellikler toohello hizmet geçmedi veya hello hizmeti göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-254">Other properties are not passed toohello service or are ignored at hello service.</span></span> <span data-ttu-id="7cc7c-255">Merhaba sonucunu bir `DeleteAsync` çağrıdır genellikle `null`.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-255">hello result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="7cc7c-256">Merhaba kimliği toopass hello hello sonucundan elde edilebilir `InsertAsync` çağırın.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-256">hello ID toopass in can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="7cc7c-257">A `MobileServiceInvalidOperationException` hello belirtmeden toodelete öğeyi çalıştığınızda durum `id` alan.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-257">A `MobileServiceInvalidOperationException` is thrown when you try toodelete an item without specifying hello `id` field.</span></span>

### <span data-ttu-id="7cc7c-258"><a name="optimisticconcurrency"></a>Nasıl yapılır: kullanım iyimser eşzamanlılık çakışması çözümleme</span><span class="sxs-lookup"><span data-stu-id="7cc7c-258"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="7cc7c-259">İki veya daha fazla istemcileri yazma değişiklikleri toohello aynı öğe hello aynı saat.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-259">Two or more clients may write changes toohello same item at hello same time.</span></span> <span data-ttu-id="7cc7c-260">Çakışma algılaması hello son yazma herhangi bir önceki güncelleştirme üzerine yazacak.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-260">Without conflict detection, hello last write would overwrite any previous updates.</span></span> <span data-ttu-id="7cc7c-261">**İyimser eşzamanlılık denetimini** her işlem tamamlayabilir ve bu nedenle hiçbir kaynak kilitleme kullanmaz varsayar.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="7cc7c-262">Bir işlem gerçekleştirmeden önce başka bir işlem hello veri değiştirdi iyimser eşzamanlılık denetimini doğrular.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified hello data.</span></span> <span data-ttu-id="7cc7c-263">Merhaba veri değiştirilirse işlemi sonlandırdı hello geri alınır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-263">If hello data has been modified, hello committing transaction is rolled back.</span></span>

<span data-ttu-id="7cc7c-264">Mobil uygulamaları hello kullanarak değişiklikleri tooeach öğesi izleyerek iyimser eşzamanlılık denetimini destekleyen `version` , mobil uygulamanızın arka ucuna her tablo için tanımlanan sistem özelliği sütun.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-264">Mobile Apps supports optimistic concurrency control by tracking changes tooeach item using hello `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="7cc7c-265">Bir kayıt güncelleştirilir, her zaman Mobile Apps hello ayarlar `version` söz konusu özellik kayıt tooa yeni bir değer.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-265">Each time a record is updated, Mobile Apps sets hello `version` property for that record tooa new value.</span></span> <span data-ttu-id="7cc7c-266">Her güncelleştirme isteği sırasında hello `version` özelliktir hello istekte hello kaydının karşılaştırılan toohello hello sunucuda hello kaydı için aynı özelliği.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-266">During each update request, hello `version` property of hello record included with hello request is compared toohello same property for hello record on hello server.</span></span> <span data-ttu-id="7cc7c-267">Sürüm ile aktarılırsa hello isteği hello arka uç eşleşmiyor sonra hello istemci kitaplığı başlatır bir `MobileServicePreconditionFailedException<T>` özel durum.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-267">If the version passed with hello request does not match hello backend, then hello client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="7cc7c-268">Merhaba özel durumla dahil hello hello kayıt sürümünden hello arka uç içeren hello sunucuları hello kayıt türüdür.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-268">hello type included with hello exception is hello record from hello backend containing hello servers version of hello record.</span></span> <span data-ttu-id="7cc7c-269">Merhaba uygulama daha sonra bu bilgileri toodecide olup kullanabilirsiniz tooexecute hello güncelleştirme isteğini yeniden hello doğru `version` hello arka uç toocommit değişikliklerden değeri.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-269">hello application can then use this information toodecide whether tooexecute hello update request again with hello correct `version` value from hello backend toocommit changes.</span></span>

<span data-ttu-id="7cc7c-270">Merhaba tablo sınıfındaki hello için bir sütun tanımlamak `version` sistem özelliği tooenable iyimser eşzamanlılık.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-270">Define a column on hello table class for hello `version` system property tooenable optimistic concurrency.</span></span> <span data-ttu-id="7cc7c-271">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-271">For example:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

<span data-ttu-id="7cc7c-272">Türsüz tabloları kullanarak uygulamaları etkinleştirme iyimser eşzamanlılık ayarı hello tarafından `Version` üzerinde bayrak `SystemProperties` Merhaba tablo gibi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-272">Applications using untyped tables enable optimistic concurrency by setting hello `Version` flag on the `SystemProperties` of hello table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="7cc7c-273">İçinde toplama tooenabling iyimser eşzamanlılık, siz de hello catch gerekir `MobileServicePreconditionFailedException<T>` kodunuzda çağrılırken özel durum [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-273">In addition tooenabling optimistic concurrency, you must also catch hello `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="7cc7c-274">Merhaba doğru uygulayarak Hello çakışmayı `version` toothe güncelleştirilmiş kayıt ve çağrı [UpdateAsync] kayıt hello ile çözümlendi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-274">Resolve hello conflict by applying hello correct `version` toothe updated record and call [UpdateAsync] with hello resolved record.</span></span> <span data-ttu-id="7cc7c-275">koddan hello nasıl tooresolve bir yazma çakışması kez algılandığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-275">hello following code shows how tooresolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="7cc7c-276">Merhaba daha fazla bilgi için bkz: [çevrimdışı veri eşitlemeye Azure Mobile Apps içinde] konu.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-276">For more information, see hello [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="7cc7c-277"><a name="binding"></a>Nasıl yapılır: bağlama Mobile Apps veri tooa Windows kullanıcı arabirimi</span><span class="sxs-lookup"><span data-stu-id="7cc7c-277"><a name="binding"></a>How to: Bind Mobile Apps data tooa Windows user interface</span></span>
<span data-ttu-id="7cc7c-278">Bu bölüm, nasıl bir Windows uygulamasında kullanıcı Arabirimi öğeleri kullanarak veri nesneleri toodisplay döndürülen gösterir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-278">This section shows how toodisplay returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="7cc7c-279">Aşağıdaki kod örneği, tamamlanmamış öğeleri için bir sorgu ile Merhaba listesi toohello kaynağı bağlar.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-279">The following example code binds toohello source of hello list with a query for incomplete items.</span></span> <span data-ttu-id="7cc7c-280">[MobileServiceCollection] mobil uygulamaları algılayan bir bağlama koleksiyonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="7cc7c-281">Bazı denetimler hello yönetilen bir arabirim adlı çalışma zamanı desteği [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-281">Some controls in hello managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="7cc7c-282">Bu arabirim denetimleri toorequest verir hello kullanıcı kaydırdığında ek veriler.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-282">This interface allows controls toorequest extra data when hello user scrolls.</span></span> <span data-ttu-id="7cc7c-283">Bu arabirim için evrensel Windows uygulamaları için yerleşik destek [MobileServiceIncrementalLoadingCollection], otomatik olarak işleme hello denetimleri gelen çağrıları.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from hello controls.</span></span> <span data-ttu-id="7cc7c-284">Kullanım `MobileServiceIncrementalLoadingCollection` şekilde Windows uygulamalarında:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="7cc7c-285">toouse hello Windows Phone 8 ve "Silverlight" uygulamaları, kullanım hello üzerinde yeni bir koleksiyon `ToCollection` genişletme yöntemleri `IMobileServiceTableQuery<T>` ve `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-285">toouse hello new collection on Windows Phone 8 and "Silverlight" apps, use hello `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="7cc7c-286">Çağrı tooload verileri `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-286">tooload data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="7cc7c-287">Çağrılarak oluşturulan hello koleksiyonu kullandığınızda `ToCollectionAsync` veya `ToCollection`, ilişkili tooUI denetimler olabilir bir koleksiyon alın.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-287">When you use hello collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound tooUI controls.</span></span>  <span data-ttu-id="7cc7c-288">Bu disk belleği algılayan koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-288">This collection is paging-aware.</span></span>  <span data-ttu-id="7cc7c-289">Merhaba koleksiyon verileri ağ üzerinden yüklüyor olduğundan, bazen yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-289">Since hello collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="7cc7c-290">toohandle böyle hataları geçersiz kılma hello `OnException` yöntemi `MobileServiceIncrementalLoadingCollection` gelen çağrıları çok kaynaklanan toohandle özel durumları`LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-290">toohandle such failures, override hello `OnException` method on `MobileServiceIncrementalLoadingCollection` toohandle exceptions resulting from calls too`LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="7cc7c-291">Tablonuzda fazla alan var ancak yalnızca toodisplay istediğiniz göz önünde bulundurun bazıları, denetimi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-291">Consider if your table has many fields but you only want toodisplay some of them in your control.</span></span> <span data-ttu-id="7cc7c-292">Önceki bölümde hello hello kılavuzunu kullanabilir "[belirli sütunları seçmek](#selecting)" Merhaba UI içinde tooselect belirli sütunlardaki toodisplay.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-292">You may use hello guidance in hello preceding section "[Select specific columns](#selecting)" tooselect specific columns toodisplay in hello UI.</span></span>

### <span data-ttu-id="7cc7c-293"><a name="pagesize"></a>Değişiklik hello sayfa boyutu</span><span class="sxs-lookup"><span data-stu-id="7cc7c-293"><a name="pagesize"></a>Change hello Page size</span></span>
<span data-ttu-id="7cc7c-294">Azure mobil uygulamalar varsayılan olarak en fazla istek başına 50 öğe döndürür.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="7cc7c-295">Merhaba istemci ve sunucudaki hello maksimum sayfa boyutunu artırarak Başlangıç disk belleği boyutunu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-295">You can change hello paging size by increasing hello maximum page size on both hello client and server.</span></span>  <span data-ttu-id="7cc7c-296">tooincrease istenen sayfa boyutu Merhaba, belirtin `PullOptions` kullanırken `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-296">tooincrease hello requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="7cc7c-297">Merhaba yaptığınız varsayılarak `PageSize` eşit tooor hello sunucu içindeki 100'den büyük, bir istek en fazla 100 öğeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-297">Assuming you have made hello `PageSize` equal tooor greater than 100 within hello server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="7cc7c-298"><a name="#offlinesync"></a>Çevrimdışı tablolarla çalışma</span><span class="sxs-lookup"><span data-stu-id="7cc7c-298"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="7cc7c-299">Çevrimdışı tabloları yerel bir SQLite deposu toostore veri çevrimdışı olduğunda kullanın.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-299">Offline tables use a local SQLite store toostore data for use when offline.</span></span>  <span data-ttu-id="7cc7c-300">Tüm tablo işlemleri hello karşı yapılır hello uzak sunucu deposu yerine yerel SQLite depolar.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-300">All table operations are done against hello local SQLite store instead of hello remote server store.</span></span>  <span data-ttu-id="7cc7c-301">Çevrimdışı bir tablo toocreate ilk projenizi hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-301">toocreate an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="7cc7c-302">Visual Studio'da hello çözüme sağ tıklayın > **çözüm için NuGet paketlerini Yönet...** , ardından arayın ve yükleyin **Microsoft.Azure.Mobile.Client.SQLiteStore** hello Çözümdeki tüm projeleri için NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-302">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="7cc7c-303">(İsteğe bağlı) toosupport Windows cihazları, SQLite çalışma zamanı paketleri aşağıdaki hello birini yükleyin:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-303">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="7cc7c-304">**Windows 8.1 çalışma zamanı:** yükleme [Windows 8.1 için SQLite][3].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="7cc7c-305">**Windows Phone 8.1:** yükleme [Windows Phone 8.1 için SQLite][4].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="7cc7c-306">**Evrensel Windows platformu** yükleme [Evrensel Windows hello için SQLite][5].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-306">**Universal Windows Platform** Install [SQLite for hello Universal Windows][5].</span></span>
3. <span data-ttu-id="7cc7c-307">(İsteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="7cc7c-307">(Optional).</span></span> <span data-ttu-id="7cc7c-308">Windows cihazlar için tıklatın **başvuruları** > **Başvuru Ekle...** , hello genişletin **Windows** klasörü > **uzantıları**, uygun hello etkinleştirmek **SQLite için Windows** hello birlikteSDK **Windows için Visual C++ 2013 çalışma zamanı** SDK.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-308">For Windows devices, click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**, then enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="7cc7c-309">Merhaba SQLite SDK adları biraz her Windows platformuyla farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-309">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="7cc7c-310">Bir tablo başvurusu oluşturulmadan önce hello yerel depolama karşı hazırlıklı olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-310">Before a table reference can be created, hello local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="7cc7c-311">Merhaba istemci hemen oluşturulduktan sonra depolama başlatma normal olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-311">Store initialization is normally done immediately after hello client is created.</span></span>  <span data-ttu-id="7cc7c-312">Merhaba **OfflineDbPath** filename desteklediğiniz tüm platformlarda kullanmaya uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-312">hello **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="7cc7c-313">Merhaba yol tam nitelenmiş bir yol ise (diğer bir deyişle, bir eğik çizgi ile başlar), bu yolun kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-313">If hello path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="7cc7c-314">Merhaba yolu tam olarak nitelenmiş değil, hello dosya bir platforma özgü konuma yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-314">If hello path is not fully qualified, hello file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="7cc7c-315">İOS ve Android cihazlar için hello varsayılan hello "Kişisel dosyalar" klasör yoludur.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-315">For iOS and Android devices, hello default path is hello "Personal Files" folder.</span></span>
* <span data-ttu-id="7cc7c-316">Windows cihazlar için hello uygulamaya özgü "AppData" klasörü hello varsayılan yoldur.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-316">For Windows devices, hello default path is hello application-specific "AppData" folder.</span></span>

<span data-ttu-id="7cc7c-317">Bir tablo başvurusu hello kullanılarak edinilebilir `GetSyncTable<>` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-317">A table reference can be obtained using hello `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="7cc7c-318">Tooauthenticate toouse çevrimdışı bir tablo gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-318">You do not need tooauthenticate toouse an offline table.</span></span>  <span data-ttu-id="7cc7c-319">Merhaba arka uç hizmeti ile iletişim kurarken tooauthenticate yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-319">You only need tooauthenticate when you are communicating with hello backend service.</span></span>

### <span data-ttu-id="7cc7c-320"><a name="syncoffline"></a>Çevrimdışı bir tablo eşitleniyor</span><span class="sxs-lookup"><span data-stu-id="7cc7c-320"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="7cc7c-321">Çevrimdışı tabloları hello arka ucuyla varsayılan olarak eşitlenmez.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-321">Offline tables are not synchronized with hello backend by default.</span></span>  <span data-ttu-id="7cc7c-322">Eşitleme iki parçalara bölünür.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-322">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="7cc7c-323">Yeni öğeler indirmelerinin değişiklikleri ayrı olarak gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-323">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="7cc7c-324">Tipik eşitleme yöntemi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-324">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
            //Use a different query name for each unique query in your program
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

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
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

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="7cc7c-325">İlk bağımsız değişkeni çok hello`PullAsync` null, artımlı eşitleme değil kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-325">If hello first argument too`PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="7cc7c-326">Her eşitleme işlemi, tüm kayıtları alır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-326">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="7cc7c-327">Merhaba SDK gerçekleştirir örtülü `PushAsync()` kayıtları çekme önce.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-327">hello SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="7cc7c-328">Çakışma işleme olur bir `PullAsync()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-328">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="7cc7c-329">Hello çakışmalı aynı başa çevrimiçi tabloları şekilde.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-329">You can deal with conflicts in hello same way as online tables.</span></span>  <span data-ttu-id="7cc7c-330">Merhaba çakışma üretileceğini zaman `PullAsync()` hello INSERT, update veya delete sırasında yerine olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-330">hello conflict is produced when `PullAsync()` is called instead of during hello insert, update, or delete.</span></span> <span data-ttu-id="7cc7c-331">Birden çok çakışma görülüyorsa, bunların tek MobileServicePushFailedException paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="7cc7c-332">Her hata ayrı olarak işler.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-332">Handle each failure separately.</span></span>

## <span data-ttu-id="7cc7c-333"><a name="#customapi"></a>Özel bir API ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7cc7c-333"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="7cc7c-334">Özel bir API değil tooan INSERT eşleme, güncelleştirme, silme veya okuma işlemi sunucusu işlevselliği kullanıma toodefine özel uç noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-334">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="7cc7c-335">Özel bir API kullanarak, okuma ve HTTP ileti üstbilgilerini ayarlama ve JSON dışında bir ileti gövdesinin biçimi tanımlama gibi Mesajlaşma üzerinde daha fazla denetim olabilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="7cc7c-336">Merhaba birini çağırarak özel bir API çağrısı [InvokeApiAsync] hello istemcide yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-336">You call a custom API by calling one of hello [InvokeApiAsync] methods on hello client.</span></span> <span data-ttu-id="7cc7c-337">Örneğin, aşağıdaki kod hello bir POST isteği toohello gönderir **completeAll** hello arka uç API:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-337">For example, hello following line of code sends a POST request toohello **completeAll** API on hello backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="7cc7c-338">Bu form yazılan yöntem çağrısı ve o hello gerektirir **MarkAllResult** dönüş türü tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-338">This form is a typed method call and requires that hello **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="7cc7c-339">Yazılan ve türsüz yöntemleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-339">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="7cc7c-340">Merhaba InvokeApiAsync() yöntemi toohello hello API ile başlayan sürece toocall istediğiniz '/ api /' API başına bir '/'.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-340">hello InvokeApiAsync() method prepends '/api/' toohello API that you wish toocall unless hello API starts with a '/'.</span></span>
<span data-ttu-id="7cc7c-341">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-341">For example:</span></span>

* <span data-ttu-id="7cc7c-342">`InvokeApiAsync("completeAll",...)`Merhaba arka uçta /api/completeAll çağırır</span><span class="sxs-lookup"><span data-stu-id="7cc7c-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on hello backend</span></span>
* <span data-ttu-id="7cc7c-343">`InvokeApiAsync("/.auth/me",...)`Merhaba arka uçta /.auth/Me çağırır</span><span class="sxs-lookup"><span data-stu-id="7cc7c-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on hello backend</span></span>

<span data-ttu-id="7cc7c-344">Tanımlı değil Bu WebAPIs Azure Mobile Apps ile de dahil olmak üzere tüm Webapı InvokeApiAsync toocall kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-344">You can use InvokeApiAsync toocall any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="7cc7c-345">InvokeApiAsync() kullandığınızda, kimlik doğrulama üstbilgileri dahil olmak üzere hello uygun üstbilgileri hello isteği gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-345">When you use InvokeApiAsync(), hello appropriate headers, including authentication headers, are sent with hello request.</span></span>

## <span data-ttu-id="7cc7c-346"><a name="authentication"></a>Kullanıcıların kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7cc7c-346"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="7cc7c-347">Mobile Apps, kimlik doğrulaması ve çeşitli dış kimlik sağlayıcılarını kullanarak uygulama kullanıcıları yetkilendirmek destekler: Facebook, Google, Microsoft Account, Twitter ve Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="7cc7c-348">Tooonly kimliği doğrulanmış kullanıcıların belirli işlemler için tabloları toorestrict erişim izinlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-348">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="7cc7c-349">Sunucu komut dosyalarında kimliği doğrulanmış kullanıcılar tooimplement yetkilendirme kuralları hello kimliğini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-349">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="7cc7c-350">Merhaba öğretici daha fazla bilgi için bkz [Ekle kimlik doğrulama tooyour uygulama].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-350">For more information, see hello tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="7cc7c-351">İki kimlik doğrulama akışı desteklenir: *istemcisi yönetilen* ve *sunucusu yönetilen* akış.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="7cc7c-352">Merhaba sağlayıcının web kimlik doğrulaması arabirimde alacağından hello akış sunucusu tarafından yönetilen hello Basit kimlik doğrulama deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-352">hello server-managed flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="7cc7c-353">sağlayıcıya özgü aygıta özgü SDK'ları üzerinde alacağından hello istemcisi yönetilen akış aygıta özgü özellikleri ile daha derin tümleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-353">hello client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="7cc7c-354">İstemci tarafından yönetilen bir akış üretim uygulamalarınızı kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-354">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="7cc7c-355">tooset kimlik doğrulaması kurma, bir veya daha fazla kimlik sağlayıcıları ile uygulamanızı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-355">tooset up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="7cc7c-356">Merhaba kimlik sağlayıcısı, bir istemci kimliği ve uygulamanız için bir istemci parolası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-356">hello identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="7cc7c-357">Bu değerler, arka uç tooenable Azure App Service kimlik doğrulama/yetkilendirme sonra ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-357">These values are then set in your backend tooenable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="7cc7c-358">Daha fazla bilgi için izleyin hello ayrıntılı yönergeler öğreticide [Ekle kimlik doğrulama tooyour uygulama].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-358">For more information, follow hello detailed instructions in the tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="7cc7c-359">Aşağıdaki konularda hello Bu bölümde ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-359">hello following topics are covered in this section:</span></span>

* [<span data-ttu-id="7cc7c-360">Yönetilen istemci kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7cc7c-360">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="7cc7c-361">Yönetilen sunucu kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7cc7c-361">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="7cc7c-362">Önbelleğe alma hello kimlik doğrulama belirteci</span><span class="sxs-lookup"><span data-stu-id="7cc7c-362">Caching hello authentication token</span></span>](#caching)

### <span data-ttu-id="7cc7c-363"><a name="clientflow"></a>Yönetilen istemci kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7cc7c-363"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="7cc7c-364">Uygulamanızı bağımsız olarak hello kimlik sağlayıcısı başvurun ve ardından hello döndürülen belirteç ile arka oturum açma sırasında sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-364">Your app can independently contact hello identity provider and then provide hello returned token during login with your backend.</span></span> <span data-ttu-id="7cc7c-365">Bu istemci akışı tooprovide kullanıcılar ya da tooretrieve ek kullanıcı verilerini hello kimlik sağlayıcısı için çoklu oturum açma deneyimini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-365">This client flow enables you tooprovide a single sign-on experience for users or tooretrieve additional user data from hello identity provider.</span></span> <span data-ttu-id="7cc7c-366">Merhaba kimlik sağlayıcısı SDK daha yerel bir UX fikir sağlar ve ek özelleştirme için sağlar istemci akış kimlik doğrulaması tercih edilen toousing server akış aynıdır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-366">Client flow authentication is preferred toousing a server flow as hello identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="7cc7c-367">Akış olmayan istemci kimlik doğrulaması desenler izleyen Merhaba örnekler verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-367">Examples are provided for hello following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="7cc7c-368">Active Directory kimlik doğrulama kitaplığı</span><span class="sxs-lookup"><span data-stu-id="7cc7c-368">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="7cc7c-369">Facebook veya Google</span><span class="sxs-lookup"><span data-stu-id="7cc7c-369">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="7cc7c-370">Live SDK</span><span class="sxs-lookup"><span data-stu-id="7cc7c-370">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="7cc7c-371"><a name="adal"></a>Kullanıcılar hello Active Directory kimlik doğrulama kitaplığı ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7cc7c-371"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="7cc7c-372">Azure Active Directory kimlik doğrulaması kullanarak hello istemciden hello Active Directory Authentication Library (ADAL) tooinitiate kullanıcı kimlik doğrulamasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-372">You can use hello Active Directory Authentication Library (ADAL) tooinitiate user authentication from hello client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="7cc7c-373">Aşağıdaki hello tarafından mobil uygulamanızın arka ucuna AAD oturum açma için yapılandırma [tooconfigure App Service nasıl Active Directory oturum açma için] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-373">Configure your mobile app backend for AAD sign-on by following hello [How tooconfigure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="7cc7c-374">Yerel istemci uygulaması kaydı emin toocomplete hello isteğe bağlı adım olun.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-374">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="7cc7c-375">Visual Studio veya Xamarin Studio, projenizin açın ve bir başvuru toothe ekleyin `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-375">In Visual Studio or Xamarin Studio, open your project and add a reference toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="7cc7c-376">Arama yaparken, yayın öncesi sürümlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-376">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="7cc7c-377">Kod tooyour uygulama aşağıdaki, kullanmakta olduğunuz toohello platform according hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-377">Add hello following code tooyour application, according toohello platform you are using.</span></span> <span data-ttu-id="7cc7c-378">Her, değişiklikleri izleyen hello olun:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-378">In each, make hello following replacements:</span></span>

   * <span data-ttu-id="7cc7c-379">Değiştir **INSERT yetkilisi burada** uygulamanızı sağlanan hello Kiracı hello adı.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-379">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="7cc7c-380">Https://login.microsoftonline.com/contoso.onmicrosoft.com biçiminde olmalıdır. Bu değer hello etki alanı sekmesinden hello Azure Active Directory'yi kopyalanabilir [Klasik Azure portalı].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-380">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="7cc7c-381">Değiştir **Ekle-RESOURCE-kimliği-Buraya** , mobil uygulamanızın arka ucuna için hello istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-381">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="7cc7c-382">Hello hello istemci kimliği elde edebilirsiniz **Gelişmiş** altında sekmesinde **Azure Active Directory ayarları** hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-382">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="7cc7c-383">Değiştir **Ekle-istemci-kimliği-Buraya** hello yerel istemci uygulamasından kopyaladığınız hello istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-383">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="7cc7c-384">Değiştir **Ekle-REDIRECT-URI-Buraya** sitenizin ile */.auth/login/done* hello HTTPS şeması kullanarak uç nokta.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-384">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="7cc7c-385">Bu değer çok benzer olmalıdır*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-385">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="7cc7c-386">Her platform için gereken hello kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-386">hello code needed for each platform follows:</span></span>

     <span data-ttu-id="7cc7c-387">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="7cc7c-387">**Windows:**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     <span data-ttu-id="7cc7c-388">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="7cc7c-388">**Xamarin.iOS**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     <span data-ttu-id="7cc7c-389">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="7cc7c-389">**Xamarin.Android**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <span data-ttu-id="7cc7c-390"><a name="client-facebook"></a>Çoklu oturum Facebook veya Google uygulamasından bir belirteç kullanarak açma</span><span class="sxs-lookup"><span data-stu-id="7cc7c-390"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="7cc7c-391">Facebook veya Google için bu parçacığında gösterildiği gibi hello istemci akışı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-391">You can use hello client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <span data-ttu-id="7cc7c-392"><a name="client-livesdk"></a>Microsoft Account kullanarak çoklu oturum açma Live SDK hello</span><span class="sxs-lookup"><span data-stu-id="7cc7c-392"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with hello Live SDK</span></span>
<span data-ttu-id="7cc7c-393">tooauthenticate kullanıcılar, Microsoft hesabı Geliştirici Merkezi hello uygulamanızı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-393">tooauthenticate users, you must register your app at hello Microsoft account Developer Center.</span></span> <span data-ttu-id="7cc7c-394">Kayıt ayrıntıları, mobil uygulama arka uçta yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-394">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="7cc7c-395">toocreate bir Microsoft hesabı kaydı ve tooyour mobil uygulama arka ucu bağlanın, tam hello adımları [kaydetmek, uygulama toouse bir Microsoft hesabı oturum açma].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-395">toocreate a Microsoft account registration and connect it tooyour Mobile App backend, complete hello steps in [Register your app toouse a Microsoft account login].</span></span> <span data-ttu-id="7cc7c-396">Uygulamanızı Windows mağazası ve Windows Phone 8/Silverlight sürümüne sahipseniz, hello Windows mağazası sürümü ilk kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-396">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register hello Windows Store version first.</span></span>

<span data-ttu-id="7cc7c-397">Merhaba aşağıdaki kod Live SDK'sını kullanarak kimliğini doğrular ve belirteç toosign tooyour mobil uygulama arka ucuna döndürülen hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-397">hello following code authenticates using Live SDK and uses hello returned token toosign in tooyour Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

<span data-ttu-id="7cc7c-398">Daha fazla bilgi için bkz: Merhaba [Windows Live SDK] belgeleri.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-398">For more information, see hello [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="7cc7c-399"><a name="serverflow"></a>Yönetilen sunucu kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7cc7c-399"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="7cc7c-400">Kimlik sağlayıcınızı kaydettiğinizde, hello çağrısı [LoginAsync] hello [MobileServiceClient] hello ile yöntemi [MobileServiceAuthenticationProvider] sağlayıcınız değeri.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-400">Once you have registered your identity provider, call hello [LoginAsync] method on hello [MobileServiceClient] with hello [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="7cc7c-401">Örneğin, hello aşağıdaki kod bir sunucu akış oturum açma Facebook kullanarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-401">For example, hello following code initiates a server flow sign-in by using Facebook.</span></span>

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

<span data-ttu-id="7cc7c-402">Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, hello değerini değiştirme [MobileServiceAuthenticationProvider] sağlayıcınız için toohello değeri.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-402">If you are using an identity provider other than Facebook, change hello value of [MobileServiceAuthenticationProvider] toohello value for your provider.</span></span>

<span data-ttu-id="7cc7c-403">Bir sunucu akışında hello oturum açma sayfası hello seçilen sağlayıcıya görüntüleyerek Azure App Service hello OAuth kimlik doğrulaması akışı yönetir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-403">In a server flow, Azure App Service manages hello OAuth authentication flow by displaying hello sign-in page of hello selected provider.</span></span>  <span data-ttu-id="7cc7c-404">Bir kez hello kimlik sağlayıcısı döndürür, Azure App Service, bir uygulama hizmeti kimlik doğrulama belirteci oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-404">Once hello identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="7cc7c-405">Merhaba [LoginAsync] yöntemi döndürür bir [MobileServiceUser], her iki hello sağlayan [UserID] Merhaba kimliği doğrulanmış kullanıcı ve hello [ MobileServiceAuthenticationToken], JSON web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="7cc7c-405">hello [LoginAsync] method returns a [MobileServiceUser], which provides both hello [UserId] of hello authenticated user and hello [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="7cc7c-406">Bu belirteç önbelleğe alınabilir süresi sona erene kadar yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-406">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="7cc7c-407">Daha fazla bilgi için bkz: [önbelleğe alma hello kimlik doğrulama belirteci](#caching).</span><span class="sxs-lookup"><span data-stu-id="7cc7c-407">For more information, see [Caching hello authentication token](#caching).</span></span>

### <span data-ttu-id="7cc7c-408"><a name="caching"></a>Önbelleğe alma hello kimlik doğrulama belirteci</span><span class="sxs-lookup"><span data-stu-id="7cc7c-408"><a name="caching"></a>Caching hello authentication token</span></span>
<span data-ttu-id="7cc7c-409">Bazı durumlarda, hello çağrısı toohello oturum açma yöntemi hello kimlik doğrulama belirteci hello sağlayıcısından depolayarak hello ilk başarılı kimlik doğrulamasından sonra önlenebilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-409">In some cases, hello call toohello login method can be avoided after hello first successful authentication by storing hello authentication token from hello provider.</span></span>  <span data-ttu-id="7cc7c-410">Windows mağazası ve UWP uygulamalar kullanabilir [PasswordVault] toocache gibi simge bir başarılı oturum açma işleminden sonra geçerli kimlik doğrulama:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-410">Windows Store and UWP apps can use [PasswordVault] toocache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="7cc7c-411">Hello UserID değeri hello hello kimlik bilgileri kullanıcı adı depolanır ve parola hello depolanan hello hello belirtecidir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-411">hello UserId value is stored as hello UserName of hello credential and hello token is hello stored as hello Password.</span></span> <span data-ttu-id="7cc7c-412">Sonraki start-ups üzerinde hello denetleyebilirsiniz **PasswordVault** önbelleğe alınmış kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-412">On subsequent start-ups, you can check hello **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="7cc7c-413">bulunan ve aksi durumda tooauthenticate hello arka ucu ile yeniden deneme hello aşağıdaki örnekte önbelleğe alınmış kimlik bilgilerini kullanır:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-413">hello following example uses cached credentials when they are found, and otherwise attempts tooauthenticate again with hello backend:</span></span>

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

<span data-ttu-id="7cc7c-414">Bir kullanıcı oturum açtığınızda, hello depolanan kimlik bilgileri, aşağıdaki gibi de kaldırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-414">When you sign out a user, you must also remove hello stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="7cc7c-415">Xamarin uygulamaları kullanma hello [Xamarin.Auth] API'leri toosecurely deposu kimlik bir **hesap** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-415">Xamarin    apps use hello [Xamarin.Auth] APIs toosecurely store credentials in an **Account** object.</span></span> <span data-ttu-id="7cc7c-416">Merhaba bu API'leri kullanarak bir örnek için bkz: [AuthStore.cs] hello kod dosyasında [örnek paylaşımı ContosoMoments fotoğraf](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="7cc7c-416">For an example of using these APIs, see hello [AuthStore.cs] code file in hello [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="7cc7c-417">Yönetilen istemci kimlik doğrulaması kullandığınızda, Facebook veya Twitter'da gibi sağlayıcınızdan elde hello erişim belirteci önbelleğe alabilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-417">When you use client-managed authentication, you can also cache hello access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="7cc7c-418">Bu belirteç sağlanan toorequest yeni bir kimlik doğrulama belirteci hello arka aşağıdaki gibi olabilir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-418">This token can be supplied toorequest a new authentication token from hello backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="7cc7c-419"><a name="pushnotifications"></a>Anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="7cc7c-419"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="7cc7c-420">Merhaba aşağıdaki konular anında iletme bildirimleri kapsar:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-420">hello following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="7cc7c-421">Anında iletme bildirimleri için kaydolun</span><span class="sxs-lookup"><span data-stu-id="7cc7c-421">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="7cc7c-422">Windows mağazası paket SID'si alın</span><span class="sxs-lookup"><span data-stu-id="7cc7c-422">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="7cc7c-423">Platformlar arası şablonları ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="7cc7c-423">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="7cc7c-424"><a name="register-for-push"></a>Nasıl yapılır: anında iletme bildirimleri için kaydolun</span><span class="sxs-lookup"><span data-stu-id="7cc7c-424"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="7cc7c-425">Merhaba Mobile Apps istemci tooregister Azure Notification Hubs ile anında iletme bildirimleri için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-425">hello Mobile Apps client enables you tooregister for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="7cc7c-426">Kaydederken, hello platforma özgü elde bir tanıtıcı elde anında bildirim hizmeti (PNS).</span><span class="sxs-lookup"><span data-stu-id="7cc7c-426">When registering, you obtain a handle that you obtain from hello platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="7cc7c-427">Hello kayıt oluşturduğunuzda, ardından tüm etiketlerin yanı sıra bu değer sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-427">You then provide this value along with any tags when you create hello registration.</span></span> <span data-ttu-id="7cc7c-428">Merhaba aşağıdaki kodu Windows uygulamanız anında iletme bildirimleri için hello Windows bildirim Hizmeti'ni (WNS) ile kaydeder:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-428">hello following code registers your Windows app for push notifications with hello Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="7cc7c-429">TooWNS Ftp'den sonra yapmanız gerekenler [Windows mağazası paket SID'si elde](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="7cc7c-429">If you are pushing tooWNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="7cc7c-430">Windows uygulamaları hakkında daha fazla bilgi için şablon kayıtlar için tooregister nasıl görürüm dahil olmak üzere [Ekle anında iletme bildirimleri tooyour uygulama].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-430">For more information on Windows apps, including how tooregister for template registrations, see [Add push notifications tooyour app].</span></span>

<span data-ttu-id="7cc7c-431">Etiketler hello istemciden isteyen desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-431">Requesting tags from hello client is not supported.</span></span>  <span data-ttu-id="7cc7c-432">Etiket istekleri sessizce kaydından bırakılır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-432">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="7cc7c-433">Cihazınızı etiketlerle tooregister istiyorsanız, sizin adınıza hello bildirim hub'ları API tooperform hello kayıt kullanan bir özel API oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-433">If you wish tooregister your device with tags, create a Custom API that uses hello Notification Hubs API tooperform hello registration on your behalf.</span></span>  <span data-ttu-id="7cc7c-434">[Merhaba özel API çağrısı](#customapi) hello yerine `RegisterNativeAsync()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-434">[Call hello Custom API](#customapi) instead of hello `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="7cc7c-435"><a name="package-sid"></a>Nasıl yapılır: Windows mağazası paket SID'si alın</span><span class="sxs-lookup"><span data-stu-id="7cc7c-435"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="7cc7c-436">Bir paket SID'si Windows mağazası uygulamalarında anında iletme bildirimleri etkinleştirmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-436">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="7cc7c-437">tooreceive bir paket SID'si, uygulamanızı Windows mağazası hello ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-437">tooreceive a package SID, register your application with hello Windows Store.</span></span>

<span data-ttu-id="7cc7c-438">tooobtain bu değer:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-438">tooobtain this value:</span></span>

1. <span data-ttu-id="7cc7c-439">Visual Studio Çözüm Gezgini'nde hello Windows mağazası uygulama projesine sağ tıklayın, tıklatın **deposu** > **uygulamayı hello mağaza ile ilişkilendir...** .</span><span class="sxs-lookup"><span data-stu-id="7cc7c-439">In Visual Studio Solution Explorer, right-click hello Windows Store app project, click **Store** > **Associate App with hello Store...**.</span></span>
2. <span data-ttu-id="7cc7c-440">Başlangıç Sihirbazı'nda tıklatın **sonraki**, Microsoft hesabınızla oturum açın, uygulamanız için bir ad yazın **yeni bir uygulama adı yedek**, ardından **ayırma**.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-440">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="7cc7c-441">Merhaba uygulama kaydı başarıyla oluşturuldu, select hello uygulama adı sonra tıklatın **sonraki**ve ardından **ilişkilendirmek**.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-441">After hello app registration is successfully created, select hello app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="7cc7c-442">İçinde toohello oturum [Windows Geliştirme Merkezi] Microsoft Account kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-442">Log in toohello [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="7cc7c-443">Altında **uygulamalarım**, oluşturduğunuz hello uygulama kayıt'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-443">Under **My apps**, click hello app registration you created.</span></span>
5. <span data-ttu-id="7cc7c-444">Tıklatın **Uygulama Yönetimi** > **uygulama kimliği**ve ardından toofind kaydırın, **paket SID'si**.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-444">Click **App management** > **App identity**, and then scroll down toofind your **Package SID**.</span></span>

<span data-ttu-id="7cc7c-445">Merhaba paket SID'si birçok kullanımı, bir URI olarak toouse gerekir; bu durumda kabul *ms-app: / /* hello düzeni olarak.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-445">Many uses of hello package SID treat it as a URI, in which case you need toouse *ms-app://* as hello scheme.</span></span> <span data-ttu-id="7cc7c-446">Paketinizin bir önek olarak bu değer birleştirerek biçimlendirilmiş SID hello sürümünü not edin.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-446">Make note of hello version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="7cc7c-447">Xamarin uygulamaları bazı ek kod toobe mümkün tooregister hello iOS veya Android platformları üzerinde çalışan uygulama gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-447">Xamarin apps require some additional code toobe able tooregister an app running on hello iOS or Android platforms.</span></span> <span data-ttu-id="7cc7c-448">Daha fazla bilgi için platformunuz hello konuya bakın:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-448">For more information, see hello topic for your platform:</span></span>

* [<span data-ttu-id="7cc7c-449">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="7cc7c-449">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="7cc7c-450">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="7cc7c-450">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="7cc7c-451"><a name="register-xplat"></a>Nasıl yapılır: yazmaç anında iletme şablonları toosend platformlar arası bildirimleri</span><span class="sxs-lookup"><span data-stu-id="7cc7c-451"><a name="register-xplat"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="7cc7c-452">tooregister şablonlarını kullanma hello `RegisterAsync()` şekilde hello şablonlarıyla yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-452">tooregister templates, use hello `RegisterAsync()` method with hello templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="7cc7c-453">Şablonlarınızı olmalıdır `JObject` türleri ve birden fazla şablon içinde JSON biçimini izleyen hello içerebilir:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-453">Your templates should be `JObject` types and can contain multiple templates in hello following JSON format:</span></span>

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

<span data-ttu-id="7cc7c-454">Merhaba yöntemi **RegisterAsync()** de ikincil döşeme kabul eder:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-454">hello method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="7cc7c-455">Tüm etiketleri hemen güvenlik için kayıt sırasında kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-455">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="7cc7c-456">tooadd tooinstallations ya da şablon yüklemeleri içinde etiketleri, [hello .NET arka uç sunucusu SDK çalışmak için Azure Mobile Apps] bakın.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-456">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="7cc7c-457">kayıtlı bu şablonları kullanılarak toosend bildirimleri başvuran toohello [bildirim hub'ları API'leri].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-457">toosend notifications utilizing these registered templates, refer toohello [Notification Hubs APIs].</span></span>

## <span data-ttu-id="7cc7c-458"><a name="misc"></a>Çeşitli konuları</span><span class="sxs-lookup"><span data-stu-id="7cc7c-458"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="7cc7c-459"><a name="errors"></a>Nasıl yapılır: hata işleme</span><span class="sxs-lookup"><span data-stu-id="7cc7c-459"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="7cc7c-460">Merhaba arka ucuna bir hata ortaya çıktığında hello istemci SDK başlatır bir `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-460">When an error occurs in hello backend, hello client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="7cc7c-461">Aşağıdaki örnekte gösterildiği nasıl toohandle hello arka ucu tarafından döndürülen bir özel durum:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-461">The following example shows how toohandle an exception that is returned by hello backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

<span data-ttu-id="7cc7c-462">Başka bir örnek hata koşulları postalarla hello bulunabilir [Mobile Apps dosyaları örnek].</span><span class="sxs-lookup"><span data-stu-id="7cc7c-462">Another example of dealing with error conditions can be found in hello [Mobile Apps Files Sample].</span></span> <span data-ttu-id="7cc7c-463">[LoggingHandler] örnek toohello arka uç yapılan işleyici toolog hello istekleri günlüğe kaydetme temsilci sağlar.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-463">The [LoggingHandler] example provides a logging delegate handler toolog hello requests being made toohello backend.</span></span>

### <span data-ttu-id="7cc7c-464"><a name="headers"></a>Nasıl yapılır: özelleştirme istek üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="7cc7c-464"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="7cc7c-465">toosupport belirli uygulama senaryonuz hello mobil uygulama arka ucu ile toocustomize iletişim gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-465">toosupport your specific app scenario, you might need toocustomize communication with hello Mobile App backend.</span></span> <span data-ttu-id="7cc7c-466">Örneğin, bir özel üst bilgi tooevery giden istek tooadd istediğiniz veya bile yanıtları durum kodları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7cc7c-466">For example, you may want tooadd a custom header tooevery outgoing request or even change responses status codes.</span></span> <span data-ttu-id="7cc7c-467">Özel bir kullanabilirsiniz [DelegatingHandler], aşağıdaki örneğine hello olarak:</span><span class="sxs-lookup"><span data-stu-id="7cc7c-467">You can use a custom [DelegatingHandler], as in hello following example:</span></span>

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[Ekle kimlik doğrulama tooyour uygulama]: app-service-mobile-windows-store-dotnet-get-started-users.md
[çevrimdışı veri eşitlemeye Azure Mobile Apps içinde]: app-service-mobile-offline-data-sync.md
[Ekle anında iletme bildirimleri tooyour uygulama]: app-service-mobile-windows-store-dotnet-get-started-push.md
[kaydetmek, uygulama toouse bir Microsoft hesabı oturum açma]: app-service-mobile-how-to-configure-microsoft-authentication.md
[tooconfigure App Service nasıl Active Directory oturum açma için]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[başvuru tooan türü belirsiz bir tablo oluşturur]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[ele]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[seçin]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[atla]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[Kullanıcı Kimliği]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[burada]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[Azure portal]: https://portal.azure.com/
[Klasik Azure portalı]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[Windows Geliştirme Merkezi]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[bildirim hub'ları API'leri]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[Mobile Apps dosyaları örnek]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 belgelerine]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments

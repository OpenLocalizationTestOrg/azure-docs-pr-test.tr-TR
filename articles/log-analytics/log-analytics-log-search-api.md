---
title: "aaaLog Analytics günlük arama REST API | Microsoft Docs"
description: "Bu kılavuz hello nasıl kullanabileceğinizi tanımlayan temel bir öğretici günlük analizi REST API hello Operations Management Suite (OMS) arama yapın ve bunu nasıl yapacağınızı örnekler verilmektedir sağlar toouse hello komutları."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="69311-103">Günlük analizi günlük arama REST API'si</span><span class="sxs-lookup"><span data-stu-id="69311-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="69311-104">Bu kılavuz, hello günlük analizi Search REST API'sini nasıl kullanabileceğinize dair örnekler dahil olmak üzere temel bir öğretici sağlar.</span><span class="sxs-lookup"><span data-stu-id="69311-104">This guide provides a basic tutorial, including examples, of how you can use hello Log Analytics Search REST API.</span></span> <span data-ttu-id="69311-105">Günlük analizi hello Operations Management Suite (OMS) bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="69311-105">Log Analytics is part of hello Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="69311-106">Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sonra da bu makalede açıklanan toouse hello eski sorgu dili hello günlük arama API ile devam etmelidir.</span><span class="sxs-lookup"><span data-stu-id="69311-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue toouse hello legacy query language with hello log search API as described in this article.</span></span>  <span data-ttu-id="69311-107">Yükseltilen çalışma alanları için yeni bir API yayımlanır ve o anda hello belgeleri güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="69311-107">A new API will be released for upgraded workspaces, and hello documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="69311-108">Günlük analizi önceden hello kaynak sağlayıcısındaki kullanılan hello adı olmasının olan Operational Insights çağrıldı.</span><span class="sxs-lookup"><span data-stu-id="69311-108">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello resource provider.</span></span>
>
>

## <a name="overview-of-hello-log-search-rest-api"></a><span data-ttu-id="69311-109">Merhaba günlük Search REST API'sini genel bakış</span><span class="sxs-lookup"><span data-stu-id="69311-109">Overview of hello Log Search REST API</span></span>
<span data-ttu-id="69311-110">Hello günlük analizi Search REST API'sini RESTful olan ve hello Azure Kaynak Yöneticisi API'si erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="69311-110">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager API.</span></span> <span data-ttu-id="69311-111">Bu makalede hello API aracılığıyla erişme örnekler [ARMClient](https://github.com/projectkudu/ARMClient), çağırma basitleştiren bir açık kaynak komut satırı aracı hello Azure Kaynak Yöneticisi API'si.</span><span class="sxs-lookup"><span data-stu-id="69311-111">This article provides examples of accessing hello API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="69311-112">ARMClient Hello kullanımını birçok seçenekleri tooaccess hello günlük analizi arama API biridir.</span><span class="sxs-lookup"><span data-stu-id="69311-112">hello use of ARMClient is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="69311-113">Arama erişmek için cmdlet'leri içerir OperationalInsights için toouse hello Azure PowerShell modülü başka bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="69311-113">Another option is toouse hello Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="69311-114">Bu araçları ile hello Azure Kaynak Yöneticisi API'si toomake çağrıları tooOMS çalışma alanları kullanma ve bunların içindeki arama komutları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="69311-114">With these tools, you can utilize hello Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="69311-115">Arama sonuçları toouse hello arama sonuçları birçok farklı yolla program aracılığıyla sağlayarak JSON biçiminde Hello API çıkarır.</span><span class="sxs-lookup"><span data-stu-id="69311-115">hello API outputs search results in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

<span data-ttu-id="69311-116">Hello Azure Resource Manager aracılığıyla kullanılabilir bir [.NET kitaplığı](https://msdn.microsoft.com/library/azure/dn910477.aspx) ve hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="69311-116">hello Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="69311-117">toolearn daha hello bağlantılı web sayfalarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="69311-117">toolearn more, review hello linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="69311-118">Gibi bir toplama komutunu kullanırsanız `|measure count()` veya `distinct`, her çağrı toosearch fazla 500.000 kayıt geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69311-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call toosearch can return upto 500,000 records.</span></span> <span data-ttu-id="69311-119">Bir toplama komutu dahil etmeyin aramaları fazla 5.000 kayıtları döndürür.</span><span class="sxs-lookup"><span data-stu-id="69311-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="69311-120">Temel günlük analizi Search REST API'sini Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="69311-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="toouse-armclient"></a><span data-ttu-id="69311-121">toouse ARMClient</span><span class="sxs-lookup"><span data-stu-id="69311-121">toouse ARMClient</span></span>
1. <span data-ttu-id="69311-122">Yükleme [Chocolatey](https://chocolatey.org/), Windows için bir açık kaynak Paket Yöneticisi olduğu.</span><span class="sxs-lookup"><span data-stu-id="69311-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="69311-123">Yönetici olarak bir komut istemi penceresi açın ve ardından hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="69311-123">Open a command prompt window as administrator and then run hello following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="69311-124">ARMClient hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="69311-124">Install ARMClient by running hello following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a><span data-ttu-id="69311-125">bir arama ARMClient kullanarak tooperform</span><span class="sxs-lookup"><span data-stu-id="69311-125">tooperform a search using ARMClient</span></span>
1. <span data-ttu-id="69311-126">Microsoft hesabınızı veya iş veya Okul hesabınızı kullanarak oturum açın:</span><span class="sxs-lookup"><span data-stu-id="69311-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="69311-127">Başarılı oturum açma hesabı verilen tüm abonelikleri bağlı toohello listeler:</span><span class="sxs-lookup"><span data-stu-id="69311-127">A successful login lists all subscriptions tied toohello given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="69311-128">Merhaba Operations Management Suite çalışma alanları alın:</span><span class="sxs-lookup"><span data-stu-id="69311-128">Get hello Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="69311-129">Başarılı bir Get çağrısı tüm çalışma alanları toohello abonelik bağlı çıkış:</span><span class="sxs-lookup"><span data-stu-id="69311-129">A successful Get call would output all workspaces tied toohello subscription:</span></span>

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. <span data-ttu-id="69311-130">Arama değişkeni oluşturun:</span><span class="sxs-lookup"><span data-stu-id="69311-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="69311-131">Yeni arama değişkenini kullanarak ara:</span><span class="sxs-lookup"><span data-stu-id="69311-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="69311-132">Günlük analizi arama REST API başvuru örnekleri</span><span class="sxs-lookup"><span data-stu-id="69311-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="69311-133">Örnek hello hello arama API nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="69311-133">hello following examples show you how you can use hello Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="69311-134">Arama - eylem/okuma</span><span class="sxs-lookup"><span data-stu-id="69311-134">Search - Action/Read</span></span>
<span data-ttu-id="69311-135">**Örnek URL'si:**</span><span class="sxs-lookup"><span data-stu-id="69311-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="69311-136">**İsteği:**</span><span class="sxs-lookup"><span data-stu-id="69311-136">**Request:**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
<span data-ttu-id="69311-137">Aşağıdaki tablonun hello kullanılabilir hello özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="69311-137">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="69311-138">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="69311-138">**Property**</span></span> | <span data-ttu-id="69311-139">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="69311-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="69311-140">Sayfanın Üstü</span><span class="sxs-lookup"><span data-stu-id="69311-140">top</span></span> |<span data-ttu-id="69311-141">Merhaba en fazla sonuçları tooreturn sayısı.</span><span class="sxs-lookup"><span data-stu-id="69311-141">hello maximum number of results tooreturn.</span></span> |
| <span data-ttu-id="69311-142">Vurgula</span><span class="sxs-lookup"><span data-stu-id="69311-142">highlight</span></span> |<span data-ttu-id="69311-143">Eşleşen alanları vurgulamak için genellikle kullanılan öncesi ve sonrası parametreleri içerir</span><span class="sxs-lookup"><span data-stu-id="69311-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="69311-144">öncesi</span><span class="sxs-lookup"><span data-stu-id="69311-144">pre</span></span> |<span data-ttu-id="69311-145">Eşleşen tooyour alanlarına verilen hello ekler.</span><span class="sxs-lookup"><span data-stu-id="69311-145">Prefixes hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="69311-146">Yayınla</span><span class="sxs-lookup"><span data-stu-id="69311-146">post</span></span> |<span data-ttu-id="69311-147">Eşleşen tooyour alanlarına verilen hello ekler.</span><span class="sxs-lookup"><span data-stu-id="69311-147">Appends hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="69311-148">sorgu</span><span class="sxs-lookup"><span data-stu-id="69311-148">query</span></span> |<span data-ttu-id="69311-149">Merhaba arama sorgusu toocollect kullanılan ve sonuçları döndürür.</span><span class="sxs-lookup"><span data-stu-id="69311-149">hello search query used toocollect and return results.</span></span> |
| <span data-ttu-id="69311-150">start</span><span class="sxs-lookup"><span data-stu-id="69311-150">start</span></span> |<span data-ttu-id="69311-151">Merhaba gelen bulunan sonuçları toobe istediğiniz hello zaman penceresi başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="69311-151">hello beginning of hello time window you want results toobe found from.</span></span> |
| <span data-ttu-id="69311-152">Bitiş</span><span class="sxs-lookup"><span data-stu-id="69311-152">end</span></span> |<span data-ttu-id="69311-153">Merhaba hello zaman penceresi istediğiniz sonuna gelen bulunan toobe sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="69311-153">hello end of hello time window you want results toobe found from.</span></span> |

<span data-ttu-id="69311-154">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="69311-154">**Response:**</span></span>

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a><span data-ttu-id="69311-155">Arama / {kimliği} - eylem/okuma</span><span class="sxs-lookup"><span data-stu-id="69311-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="69311-156">**Kayıtlı arama Merhaba içeriğine isteyin:**</span><span class="sxs-lookup"><span data-stu-id="69311-156">**Request hello contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="69311-157">Merhaba arama 'Bekleyen' durumuyla döndürürse, yoklama hello güncelleştirilmiş sonuçları bu API aracılığıyla yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="69311-157">If hello search returns with a ‘Pending’ status, then polling hello updated results can be done through this API.</span></span> <span data-ttu-id="69311-158">6 min sonra hello arama hello sonucu hello önbellekten bırakılacak ve HTTP gitti döndürülür.</span><span class="sxs-lookup"><span data-stu-id="69311-158">After 6 min, hello result of hello search will be dropped from hello cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="69311-159">Merhaba ilk arama isteği 'Başarılı' durumunu hemen döndürürse, bu API tooreturn HTTP gitti sorgularsa neden toohello önbellek hello sonuçları eklenmedi.</span><span class="sxs-lookup"><span data-stu-id="69311-159">If hello initial search request returns a ‘Successful’ status immediately, hello results are not added toohello cache causing this API tooreturn HTTP Gone if queried.</span></span> <span data-ttu-id="69311-160">bir HTTP 200 sonuç Merhaba içeriğine aynı hello ilk arama isteği yalnızca güncelleştirilmiş değerlerle olarak biçimi hello arasındadır.</span><span class="sxs-lookup"><span data-stu-id="69311-160">hello contents of an HTTP 200 result are in hello same format as hello initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="69311-161">Kaydedilen aramalar</span><span class="sxs-lookup"><span data-stu-id="69311-161">Saved searches</span></span>
<span data-ttu-id="69311-162">**Kaydedilmiş aramaları listesini isteyin:**</span><span class="sxs-lookup"><span data-stu-id="69311-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="69311-163">Algoritmalardan: GET, PUT Sil</span><span class="sxs-lookup"><span data-stu-id="69311-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="69311-164">Koleksiyon yöntemleri desteklenir: Al</span><span class="sxs-lookup"><span data-stu-id="69311-164">Supported collection methods: GET</span></span>

<span data-ttu-id="69311-165">Aşağıdaki tablonun hello kullanılabilir hello özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="69311-165">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="69311-166">Özellik</span><span class="sxs-lookup"><span data-stu-id="69311-166">Property</span></span> | <span data-ttu-id="69311-167">Açıklama</span><span class="sxs-lookup"><span data-stu-id="69311-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69311-168">Kimlik</span><span class="sxs-lookup"><span data-stu-id="69311-168">Id</span></span> |<span data-ttu-id="69311-169">Merhaba benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="69311-169">hello unique identifier.</span></span> |
| <span data-ttu-id="69311-170">ETag</span><span class="sxs-lookup"><span data-stu-id="69311-170">Etag</span></span> |<span data-ttu-id="69311-171">**Düzeltme eki için gerekli**.</span><span class="sxs-lookup"><span data-stu-id="69311-171">**Required for Patch**.</span></span> <span data-ttu-id="69311-172">Sunucu tarafından her yazma güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="69311-172">Updated by server on each write.</span></span> <span data-ttu-id="69311-173">Değer eşit toohello geçerli depolanan değer olmalıdır veya ' *' tooupdate.</span><span class="sxs-lookup"><span data-stu-id="69311-173">Value must be equal toohello current stored value or ‘*’ tooupdate.</span></span> <span data-ttu-id="69311-174">409 eski/geçersiz değerler için döndürdü.</span><span class="sxs-lookup"><span data-stu-id="69311-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="69311-175">Properties.Query</span><span class="sxs-lookup"><span data-stu-id="69311-175">properties.query</span></span> |<span data-ttu-id="69311-176">**Gerekli**.</span><span class="sxs-lookup"><span data-stu-id="69311-176">**Required**.</span></span> <span data-ttu-id="69311-177">Merhaba arama sorgusu.</span><span class="sxs-lookup"><span data-stu-id="69311-177">hello search query.</span></span> |
| <span data-ttu-id="69311-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="69311-178">properties.displayName</span></span> |<span data-ttu-id="69311-179">**Gerekli**.</span><span class="sxs-lookup"><span data-stu-id="69311-179">**Required**.</span></span> <span data-ttu-id="69311-180">Merhaba sorgu Hello kullanıcı tanımlı görünen adı.</span><span class="sxs-lookup"><span data-stu-id="69311-180">hello user-defined display name of hello query.</span></span> |
| <span data-ttu-id="69311-181">Properties.Category</span><span class="sxs-lookup"><span data-stu-id="69311-181">properties.category</span></span> |<span data-ttu-id="69311-182">**Gerekli**.</span><span class="sxs-lookup"><span data-stu-id="69311-182">**Required**.</span></span> <span data-ttu-id="69311-183">Merhaba kullanıcı tanımlı kategori hello sorgu.</span><span class="sxs-lookup"><span data-stu-id="69311-183">hello user-defined category of hello query.</span></span> |

> [!NOTE]
> <span data-ttu-id="69311-184">Merhaba günlük analizi arama API şu anda kayıtlı bir çalışma alanında Kaydedilmiş aramaları için sorgulanan zaman aramalar kullanıcı tarafından oluşturulan döndürür.</span><span class="sxs-lookup"><span data-stu-id="69311-184">hello Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="69311-185">Merhaba API çözümler tarafından sağlanan Kaydedilmiş aramaları döndürmez.</span><span class="sxs-lookup"><span data-stu-id="69311-185">hello API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="69311-186">Kaydedilen Aramalar oluşturun</span><span class="sxs-lookup"><span data-stu-id="69311-186">Create saved searches</span></span>
<span data-ttu-id="69311-187">**İsteği:**</span><span class="sxs-lookup"><span data-stu-id="69311-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="69311-188">Tüm kayıtlı aramaları, zamanlamaları ve günlük analizi API hello ile oluşturulan eylemler için Hello adı küçük olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="69311-188">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="69311-189">Kaydedilmiş aramaları silin</span><span class="sxs-lookup"><span data-stu-id="69311-189">Delete saved searches</span></span>
<span data-ttu-id="69311-190">**İsteği:**</span><span class="sxs-lookup"><span data-stu-id="69311-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="69311-191">Kaydedilmiş aramaları güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="69311-191">Update saved searches</span></span>
 <span data-ttu-id="69311-192">**İsteği:**</span><span class="sxs-lookup"><span data-stu-id="69311-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="69311-193">Meta veriler - yalnızca JSON</span><span class="sxs-lookup"><span data-stu-id="69311-193">Metadata - JSON only</span></span>
<span data-ttu-id="69311-194">Burada, bir şekilde toosee hello alanları çalışma alanınızda toplanan hello verileri için tüm günlük türleri verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="69311-194">Here’s a way toosee hello fields for all log types for hello data collected in your workspace.</span></span> <span data-ttu-id="69311-195">Örneğin, olay türü hello bilgisayar adında bir alan olup olmadığını bilmek istiyorsanız, bu sorgu tek yönlü toocheck olur.</span><span class="sxs-lookup"><span data-stu-id="69311-195">For example, if you want you know if hello Event type has a field named Computer, then this query is one way toocheck.</span></span>

<span data-ttu-id="69311-196">**İsteği alanları için:**</span><span class="sxs-lookup"><span data-stu-id="69311-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="69311-197">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="69311-197">**Response:**</span></span>

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

<span data-ttu-id="69311-198">Aşağıdaki tablonun hello kullanılabilir hello özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="69311-198">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="69311-199">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="69311-199">**Property**</span></span> | <span data-ttu-id="69311-200">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="69311-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="69311-201">ad</span><span class="sxs-lookup"><span data-stu-id="69311-201">name</span></span> |<span data-ttu-id="69311-202">Alan adı.</span><span class="sxs-lookup"><span data-stu-id="69311-202">Field name.</span></span> |
| <span data-ttu-id="69311-203">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="69311-203">displayName</span></span> |<span data-ttu-id="69311-204">Merhaba hello alanın adını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="69311-204">hello display name of hello field.</span></span> |
| <span data-ttu-id="69311-205">type</span><span class="sxs-lookup"><span data-stu-id="69311-205">type</span></span> |<span data-ttu-id="69311-206">Merhaba hello alan değerin türü.</span><span class="sxs-lookup"><span data-stu-id="69311-206">hello Type of hello field value.</span></span> |
| <span data-ttu-id="69311-207">modellenebilir</span><span class="sxs-lookup"><span data-stu-id="69311-207">facetable</span></span> |<span data-ttu-id="69311-208">'Dizine', geçerli birleşimi ' depolanan ' ve 'model' özellikleri.</span><span class="sxs-lookup"><span data-stu-id="69311-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="69311-209">Görüntüleme</span><span class="sxs-lookup"><span data-stu-id="69311-209">display</span></span> |<span data-ttu-id="69311-210">Geçerli 'display' özelliği.</span><span class="sxs-lookup"><span data-stu-id="69311-210">Current ‘display’ property.</span></span> <span data-ttu-id="69311-211">Alan aramada görünür ise true.</span><span class="sxs-lookup"><span data-stu-id="69311-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="69311-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="69311-212">ownerType</span></span> |<span data-ttu-id="69311-213">Azaltılmış tooonly türleri tooonboarded IP'ın ait.</span><span class="sxs-lookup"><span data-stu-id="69311-213">Reduced tooonly Types belonging tooonboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="69311-214">İsteğe bağlı parametreler</span><span class="sxs-lookup"><span data-stu-id="69311-214">Optional parameters</span></span>
<span data-ttu-id="69311-215">Merhaba bilgisinden isteğe bağlı parametreler kullanılabilir açıklar.</span><span class="sxs-lookup"><span data-stu-id="69311-215">hello following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="69311-216">Vurgulama</span><span class="sxs-lookup"><span data-stu-id="69311-216">Highlighting</span></span>
<span data-ttu-id="69311-217">Merhaba "Highlight" parametresi toorequest hello arama alt kullanabilir isteğe bağlı bir parametre yanıt olarak bir dizi işaretçileri dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="69311-217">hello “Highlight” parameter is an optional parameter you may use toorequest hello search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="69311-218">Bu işaretçileri hello başlangıç belirtmek ve sağlanan arama sorgunuzu hello koşulları eşleşen vurgulanan metin bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="69311-218">These markers indicate hello start and end highlighted text that matches hello terms provided in your search query.</span></span>
<span data-ttu-id="69311-219">Merhaba başlangıç belirtin ve arama toowrap vurgulanmış hello terimi tarafından kullanılan işaretçileri bitiş.</span><span class="sxs-lookup"><span data-stu-id="69311-219">You may specify hello start and end markers that are used by search toowrap hello highlighted term.</span></span>

<span data-ttu-id="69311-220">**Örnek arama sorgusu**</span><span class="sxs-lookup"><span data-stu-id="69311-220">**Example search query**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

<span data-ttu-id="69311-221">**Örnek sonuçları:**</span><span class="sxs-lookup"><span data-stu-id="69311-221">**Sample result:**</span></span>

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

<span data-ttu-id="69311-222">Önceki sonuç hello bildirimi öneki ve eklenmiş olan bir hata iletisi içerir.</span><span class="sxs-lookup"><span data-stu-id="69311-222">Notice that hello preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="69311-223">Bilgisayar grupları</span><span class="sxs-lookup"><span data-stu-id="69311-223">Computer groups</span></span>
<span data-ttu-id="69311-224">Bilgisayar, bir bilgisayar kümesi döndüren özel Kaydedilmiş aramaları gruplarıdır.</span><span class="sxs-lookup"><span data-stu-id="69311-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="69311-225">Bir bilgisayar grubu hello grubundaki diğer sorgular toolimit hello sonuçları toohello bilgisayarlar kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69311-225">You can use a computer group in other queries toolimit hello results toohello computers in hello group.</span></span>  <span data-ttu-id="69311-226">Bir bilgisayar grubu, bilgisayar değerini içeren bir Grup etiketi bir kayıtlı arama olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="69311-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="69311-227">Bir bilgisayar grubu için bir örnek yanıt aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="69311-227">Following is a sample response for a computer group.</span></span>

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a><span data-ttu-id="69311-228">Bilgisayar grupları alınıyor</span><span class="sxs-lookup"><span data-stu-id="69311-228">Retrieving computer groups</span></span>
<span data-ttu-id="69311-229">tooretrieve kullanım hello hello grubuyla Get yöntemi bir bilgisayar grubu kimliği</span><span class="sxs-lookup"><span data-stu-id="69311-229">tooretrieve a computer group, use hello Get method with hello group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="69311-230">Oluştururken veya güncelleştirirken bir bilgisayar grubu</span><span class="sxs-lookup"><span data-stu-id="69311-230">Creating or updating a computer group</span></span>
<span data-ttu-id="69311-231">toocreate bir bilgisayar grubu benzersiz kayıtlı arama kimliği ile Merhaba Put yöntemini kullanın</span><span class="sxs-lookup"><span data-stu-id="69311-231">toocreate a computer group, use hello Put method with a unique saved search ID.</span></span> <span data-ttu-id="69311-232">Var olan bir bilgisayar grubu kimliği kullanırsanız, bir değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="69311-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="69311-233">Merhaba günlük analizi portalında bir bilgisayar grubu oluşturduğunuzda hello kimliği hello grubu ve ad oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="69311-233">When you create a computer group in hello Log Analytics portal, then hello ID is created from hello group and name.</span></span>

<span data-ttu-id="69311-234">Merhaba grubu tanımı için kullanılan hello sorgu hello Grup toofunction için bir bilgisayarlar kümesi düzgün döndürmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="69311-234">hello query used for hello group definition must return a set of computers for hello group toofunction properly.</span></span>  <span data-ttu-id="69311-235">Sorgunuz ile sona önerilir `| Distinct Computer` tooensure hello doğru veriler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="69311-235">It's recommended that you end your query with `| Distinct Computer` tooensure hello correct data is returned.</span></span>

<span data-ttu-id="69311-236">Kaydedilmiş aramayı hello Hello tanımını grup bilgisayar değeri olan bir bilgisayar grubu olarak sınıflandırılmış hello arama toobe adlı bir etiket içermelidir.</span><span class="sxs-lookup"><span data-stu-id="69311-236">hello definition of hello saved search must include a tag named Group with a value of Computer for hello search toobe classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="69311-237">Bilgisayar gruplarını silme</span><span class="sxs-lookup"><span data-stu-id="69311-237">Deleting computer groups</span></span>
<span data-ttu-id="69311-238">toodelete kullanım hello hello Grup Delete yöntemiyle bir bilgisayar grubu kimliği</span><span class="sxs-lookup"><span data-stu-id="69311-238">toodelete a computer group, use hello Delete method with hello group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="69311-239">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="69311-239">Next steps</span></span>
* <span data-ttu-id="69311-240">Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) özel alanlar için ölçüt kullanarak toobuild sorgular.</span><span class="sxs-lookup"><span data-stu-id="69311-240">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>

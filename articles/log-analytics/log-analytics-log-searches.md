---
title: "Azure günlük analizi günlük aramalarda aaaFind verilerle | Microsoft Docs"
description: "Günlük arar ve ortamınızda birden fazla kaynaktan herhangi bir makine verilerin bağıntısını toocombine izin verin."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="01f96-103">Günlük analizi günlük aramaları kullanarak veri bulma</span><span class="sxs-lookup"><span data-stu-id="01f96-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="01f96-104">Bu makalede günlük analizi hello geçerli sorgu dili kullanarak günlük arar.</span><span class="sxs-lookup"><span data-stu-id="01f96-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="01f96-105">Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), çok başvurmalıdır sonra[anlama günlük arar (yeni) günlük analizi](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="01f96-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="01f96-106">Günlük analizi Hello özünde toocombine sağlayan hello günlük arama özelliktir ve ortamınızda birden fazla kaynaktan herhangi bir makine verilerin bağıntısını.</span><span class="sxs-lookup"><span data-stu-id="01f96-106">At hello core of Log Analytics is hello log search feature which allows you toocombine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="01f96-107">Çözüm Ayrıca, ölçümleri belirli sorunu etrafına özetlenebilir günlük arama toobring güç sağlar.</span><span class="sxs-lookup"><span data-stu-id="01f96-107">Solutions are also powered by log search toobring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="01f96-108">Merhaba arama sayfası, bir sorgu oluşturabilirsiniz ve arama yaptığınızda sonra hello sonuçları modeli denetimlerini kullanarak filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-108">On hello Search page, you can create a query, and then when you search, you can filter hello results by using facet controls.</span></span> <span data-ttu-id="01f96-109">Gelişmiş sorgular tootransform, filtre ve rapor sonuçlarınıza oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-109">You can also create advanced queries tootransform, filter, and report on your results.</span></span>

<span data-ttu-id="01f96-110">Ortak günlük arama sorguları çoğu çözüm sayfalarında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="01f96-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="01f96-111">Hello OMS konsol döşeme tıklatın ya da günlük arama kullanarak tooother öğelerde hello öğenin tooview ayrıntılarını incelemek.</span><span class="sxs-lookup"><span data-stu-id="01f96-111">Throughout hello OMS console, you can click tiles or drill in tooother items tooview details about hello item by using log search.</span></span>

<span data-ttu-id="01f96-112">Bu öğreticide, biz günlük arama kullandığınızda örnekler toocover tüm hello temelleri gösterilecektir.</span><span class="sxs-lookup"><span data-stu-id="01f96-112">In this tutorial, we'll walk through examples toocover all hello basics when you use log search.</span></span>

<span data-ttu-id="01f96-113">Biz basit, pratik örnekler başlatın ve böylece nasıl hello verilerden istediğinizi toouse hello sözdizimi tooextract hello Öngörüler hakkında pratik kullanım örnekleri bir anlayış alabilir üzerlerinde yapı.</span><span class="sxs-lookup"><span data-stu-id="01f96-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how toouse hello syntax tooextract hello insights you want from hello data.</span></span>

<span data-ttu-id="01f96-114">Arama teknikleri alışık olduğunuz sonra hello gözden geçirebilirsiniz [günlük analizi oturum Arama başvurusu](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="01f96-114">After you've familiar with search techniques, you can review hello [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="01f96-115">Temel filtreleri kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-115">Use basic filters</span></span>
<span data-ttu-id="01f96-116">Merhaba ilk şey tooknow bu hello ilk önce herhangi bir arama sorgusu parçasıdır "|" dikey çizgi karakteri olan her zaman bir *filtre*.</span><span class="sxs-lookup"><span data-stu-id="01f96-116">hello first thing tooknow is that hello first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="01f96-117">Bunu bir WHERE yan tümcesinde TSQL--olarak bunu belirler düşünün *ne* hello OMS veri deposundaki verileri toopull kısmı.</span><span class="sxs-lookup"><span data-stu-id="01f96-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data toopull out of hello OMS data store.</span></span> <span data-ttu-id="01f96-118">Merhaba veri deposunda arama büyük ölçüde sorguda WHERE yan tümcesi hello ile başladığını doğal şekilde tooextract, istediğiniz hello veri hello özelliklerini belirtme hakkında olur.</span><span class="sxs-lookup"><span data-stu-id="01f96-118">Searching in hello data store is largely about specifying hello characteristics of hello data that you want tooextract, so it is natural that a query would start with hello WHERE clause.</span></span>

<span data-ttu-id="01f96-119">Merhaba kullanabileceğiniz en temel filtreleri şunlardır *anahtar sözcükleri*'error' veya 'zaman aşımı' veya bir bilgisayar adı gibi.</span><span class="sxs-lookup"><span data-stu-id="01f96-119">hello most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="01f96-120">Bu basit sorgu türleri genellikle farklı şekiller dönüş aynı sonuç kümesi hello içindeki verilerin.</span><span class="sxs-lookup"><span data-stu-id="01f96-120">These types of simple queries generally return diverse shapes of data within hello same result set.</span></span> <span data-ttu-id="01f96-121">Bu günlük analizi farklı sahip olmasından *türleri* hello sistem veri.</span><span class="sxs-lookup"><span data-stu-id="01f96-121">This is because Log Analytics has different *types* of data in hello system.</span></span>

### <a name="tooconduct-a-simple-search"></a><span data-ttu-id="01f96-122">tooconduct basit arama</span><span class="sxs-lookup"><span data-stu-id="01f96-122">tooconduct a simple search</span></span>
1. <span data-ttu-id="01f96-123">Merhaba OMS portalında tıklatın **günlük arama**.</span><span class="sxs-lookup"><span data-stu-id="01f96-123">In hello OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="01f96-124">![Ara kutucuğu](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="01f96-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="01f96-125">Merhaba sorgu alanına yazın `error` ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="01f96-125">In hello query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="01f96-126">![Arama hatası](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="01f96-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="01f96-127">Örneğin, hello sorgu için `error` hello aşağıdaki görüntüde 100.000 döndürülen **olay** (günlük yönetimi tarafından toplanan), kayıt 18 **ConfigurationAlert** (yapılandırma tarafından oluşturulan kayıtları Değerlendirme) ile 12 **ConfigurationChange** (Merhaba tarafından değişiklik izleme yakalanan) kaydeder.</span><span class="sxs-lookup"><span data-stu-id="01f96-127">For example, hello query for `error` in hello following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by hello Change Tracking).</span></span>   
    <span data-ttu-id="01f96-128">![Arama sonuçları](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="01f96-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="01f96-129">Bu filtreler gerçekten nesne türleri/sınıfları değildir.</span><span class="sxs-lookup"><span data-stu-id="01f96-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="01f96-130">*Tür* yalnızca bir etiket ya da bir özellik ya da veri tooa parçası bir dize/ad/olan kategoriye ekli.</span><span class="sxs-lookup"><span data-stu-id="01f96-130">*Type* is just a tag, or a property, or a string/name/category, that is attached tooa piece of data.</span></span> <span data-ttu-id="01f96-131">Merhaba sistem bazı belgelerde olarak etiketlenir **türü: ConfigurationAlert** ve bazı olarak etiketlenir **türü: Perf**, veya **türü: olay**ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="01f96-131">Some documents in hello system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="01f96-132">Her bir arama sonucu, belge, kaydı veya giriş tüm hello Ham Özellikler ve değerlerinin her veri bu parçalarını görüntüler ve tooretrieve yalnızca hello kayıtlar istediğinizde, bu alan adları toospecify hello filtrede hello alan verilen bulunduğu kullanabilirsiniz değer.</span><span class="sxs-lookup"><span data-stu-id="01f96-132">Each search result, document, record, or entry displays all hello raw properties and their values for each of those pieces of data, and you can use those field names toospecify in hello filter when you want tooretrieve only hello records where hello field has that given value.</span></span>

<span data-ttu-id="01f96-133">*Tür* aslında tüm kayıtlar varsa, bir alan olup, diğer herhangi bir alandan farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="01f96-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="01f96-134">Bu işlem, başlangıç türü alanının hello değere göre kuruldu.</span><span class="sxs-lookup"><span data-stu-id="01f96-134">This was established based on hello value of hello Type field.</span></span> <span data-ttu-id="01f96-135">Bu kayıt, farklı bir şekil veya form sahip olur.</span><span class="sxs-lookup"><span data-stu-id="01f96-135">That record will have a different shape or form.</span></span> <span data-ttu-id="01f96-136">Arada **türü Perf =**, veya **türü olay =** de performans verisi veya olayları için toolearn tooquery gereksinim hello sözdizimi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="01f96-136">Incidentally, **Type=Perf**, or **Type=Event** is also hello syntax that you need toolearn tooquery for performance data or events.</span></span>

<span data-ttu-id="01f96-137">Merhaba alan adı sonra ve hello değeri önce iki nokta üst üste (:) veya bir eşittir işareti (=) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-137">You can use either a colon (:) or an equal sign (=) after hello field name and before hello value.</span></span> <span data-ttu-id="01f96-138">**Olay türü:** ve **türü olay =** anlamı, seçebileceğiniz eşdeğerdir hello tercih ettiğiniz stili.</span><span class="sxs-lookup"><span data-stu-id="01f96-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose hello style you prefer.</span></span>

<span data-ttu-id="01f96-139">Bu nedenle, hello çalışamazsa Perf = kayıtları 'CounterName' adlı bir alana sahip sonra benzeyen bir sorgu yazabilirsiniz `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="01f96-139">So, if hello Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="01f96-140">Bu size yalnızca hello performans verilerini hello performans sayacı adı "% işlemci zamanı" olduğu sunar.</span><span class="sxs-lookup"><span data-stu-id="01f96-140">This will give you only hello performance data where hello performance counter name is "% Processor Time".</span></span>

### <a name="toosearch-for-processor-time-performance-data"></a><span data-ttu-id="01f96-141">işlemci zamanı performans verileri için toosearch</span><span class="sxs-lookup"><span data-stu-id="01f96-141">toosearch for processor time performance data</span></span>
* <span data-ttu-id="01f96-142">Merhaba arama sorgusu alanına yazın`Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="01f96-142">In hello search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="01f96-143">Ayrıca daha belirli ve kullanabilirsiniz **InstanceName = _ 'Toplam'** hello sorguda olduğu bir Windows performans sayacı.</span><span class="sxs-lookup"><span data-stu-id="01f96-143">You can also be more specific and use **InstanceName=_'Total'** in hello query, which is a Windows performance counter.</span></span> <span data-ttu-id="01f96-144">Bir model ve başka de seçebilirsiniz **alan: değer**.</span><span class="sxs-lookup"><span data-stu-id="01f96-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="01f96-145">Merhaba filtre, hello sorgu çubuğunda tooyour filtre otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="01f96-145">hello filter is automatically added tooyour filter in hello query bar.</span></span> <span data-ttu-id="01f96-146">Bu görüntü aşağıdaki hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-146">You can see this in hello following image.</span></span> <span data-ttu-id="01f96-147">Size gösterir nerede tooclick tooadd **InstanceName: '_Total'** herhangi bir şey yazarak olmadan toohello sorgu.</span><span class="sxs-lookup"><span data-stu-id="01f96-147">It shows you where tooclick tooadd **InstanceName:’_Total’** toohello query without typing anything.</span></span>

![Arama modeli](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="01f96-149">Sorgunuz artık hale gelir`Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="01f96-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="01f96-150">Bu örnekte, toospecify yok **türü Perf =** tooget toothis sonucu.</span><span class="sxs-lookup"><span data-stu-id="01f96-150">In this example, you don't have toospecify **Type=Perf** tooget toothis result.</span></span> <span data-ttu-id="01f96-151">CounterName ve InstanceName Hello alanları türündeki kayıtlar için yalnızca olduğundan Perf, hello sorgu = yeterince spesifik tooreturn hello aynı sonuçları uzun, önceki bir hello aynıdır:</span><span class="sxs-lookup"><span data-stu-id="01f96-151">Because hello fields CounterName and InstanceName only exist for records of Type=Perf, hello query is specific enough tooreturn hello same results as hello longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="01f96-152">Merhaba sorgudaki tüm hello filtreleri olarak değerlendirilir olmasıdır *ve* birbirleriyle.</span><span class="sxs-lookup"><span data-stu-id="01f96-152">This is because all hello filters in hello query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="01f96-153">Etkili bir şekilde hello toohello ölçüt eklemek daha fazla alan daha az size daha belirli ve Gelişmiş sonuçları.</span><span class="sxs-lookup"><span data-stu-id="01f96-153">Effectively, hello more fields you add toohello criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="01f96-154">Örneğin, hello sorgu `Type=Event EventLog="Windows PowerShell"` çok aynıdır`Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="01f96-154">For example, hello query `Type=Event EventLog="Windows PowerShell"` is identical too`Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="01f96-155">Oturum açmış ve hello Windows PowerShell olay günlüğünden toplanan tüm olayları döndürür.</span><span class="sxs-lookup"><span data-stu-id="01f96-155">It returns all events that were logged in and collected from hello Windows PowerShell event log.</span></span> <span data-ttu-id="01f96-156">Birden çok kez art arda aynı modeli, ardından hello sorunu hello arama çubuğunu dağıtmayı, ancak hello örtük AND işleci her zaman olduğu için bunu hala aynı sonuçları hello döner tamamen yüzeysel--hello seçerek bir filtre eklerseniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-156">If you add a filter multiple times by repeatedly selecting hello same facet, then hello issue is purely cosmetic--it might clutter hello Search bar, but it still returns hello same results because hello implicit AND operator is always there.</span></span>

<span data-ttu-id="01f96-157">Merhaba örtük AND işleci açıkça değil işlecini kullanarak kolayca ters çevirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-157">You can easily reverse hello implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="01f96-158">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="01f96-158">For example:</span></span>

<span data-ttu-id="01f96-159">`Type:Event NOT(EventLog:"Windows PowerShell")`ya da eşdeğer `Type=Event EventLog!="Windows PowerShell"` hello Windows PowerShell günlük olmayan tüm diğer günlüklerinden tüm olayları döndürür.</span><span class="sxs-lookup"><span data-stu-id="01f96-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT hello Windows PowerShell log.</span></span>

<span data-ttu-id="01f96-160">Ya da diğer Boole işleci gibi kullanabilir 'Veya'.</span><span class="sxs-lookup"><span data-stu-id="01f96-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="01f96-161">Merhaba aşağıdaki döndürür kayıtları için hangi hello ya da uygulama veya sistem olay günlüğüne olan sorgu.</span><span class="sxs-lookup"><span data-stu-id="01f96-161">hello following query returns records for which hello EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="01f96-162">Sorgu yukarıda Hello kullanarak için her iki günlük girişlerini alırsınız hello aynı sonuç kümesi.</span><span class="sxs-lookup"><span data-stu-id="01f96-162">Using hello above query, you’ll get entries for both logs in hello same result set.</span></span>

<span data-ttu-id="01f96-163">Merhaba veya bırakarak hello örtük ve yerinde kaldırırsanız, tooBOTH günlükleri ait bir olay günlüğü girişi olmadığından Bununla birlikte, ardından hello aşağıdaki sorguyu herhangi bir sonuç oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="01f96-163">However, if you remove hello OR by leaving hello implicit AND in place, then hello following query will not produce any results because there isn’t an event log entry that belongs tooBOTH logs.</span></span> <span data-ttu-id="01f96-164">Her olay günlüğü girişi tooonly hello iki günlükleri birini yazıldı.</span><span class="sxs-lookup"><span data-stu-id="01f96-164">Each event log entry was written tooonly one of hello two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="01f96-165">Ek filtreleri kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-165">Use additional filters</span></span>
<span data-ttu-id="01f96-166">Merhaba aşağıdaki sorguyu veri gönderdiğiniz tüm hello bilgisayarlar için 2 olay günlüğü girişleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="01f96-166">hello following query returns entries for 2 event logs for all hello computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![arama sonuçları](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="01f96-168">Merhaba alanları veya filtreleri birini seçerek, diğer tüm olanlar hariç hello sorgu tooa belirli bilgisayar, daraltın.</span><span class="sxs-lookup"><span data-stu-id="01f96-168">Selecting one of hello fields or filters will narrow hello query tooa specific computer, excluding all other ones.</span></span> <span data-ttu-id="01f96-169">Merhaba sonuçta elde edilen sorgu hello aşağıdaki benzeyecektir.</span><span class="sxs-lookup"><span data-stu-id="01f96-169">hello resulting query would resemble hello following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="01f96-170">Merhaba nedeniyle eşdeğer toohello aşağıdaki olduğu örtük and</span><span class="sxs-lookup"><span data-stu-id="01f96-170">Which is equivalent toohello following, because of hello implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="01f96-171">Her sorgu açık sırasının hello değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="01f96-171">Each query is evaluated in hello following explicit order.</span></span> <span data-ttu-id="01f96-172">Not hello parantez.</span><span class="sxs-lookup"><span data-stu-id="01f96-172">Note hello parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="01f96-173">Merhaba olay günlüğü alanı gibi yalnızca, ekleyerek yalnızca belirli bir bilgisayarlar kümesi için verileri alabilir veya.</span><span class="sxs-lookup"><span data-stu-id="01f96-173">Just like hello event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="01f96-174">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="01f96-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="01f96-175">Benzer şekilde, bu sorgu return aşağıdaki hello **% CPU süresi** hello seçilen iki bilgisayar için.</span><span class="sxs-lookup"><span data-stu-id="01f96-175">Similarly, this hello following query return **% CPU Time** for hello selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="01f96-176">Alan türleri</span><span class="sxs-lookup"><span data-stu-id="01f96-176">Field types</span></span>
<span data-ttu-id="01f96-177">Filtre oluştururken, farklı türde günlük aramaları tarafından döndürülen alanları ile çalışma hello farklar anlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="01f96-177">When creating filters, you should understand hello differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="01f96-178">**Aranabilir alanlara** mavi arama sonuçlarında göster.</span><span class="sxs-lookup"><span data-stu-id="01f96-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="01f96-179">Aranabilir alanları arama koşulları belirli toohello alanı hello aşağıdaki gibi kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="01f96-179">You can use searchable fields in search conditions specific toohello field such as hello following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="01f96-180">**Serbest metin aranabilir alanları** arama sonuçlarında gri gösterilir.</span><span class="sxs-lookup"><span data-stu-id="01f96-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="01f96-181">Arama koşulları belirli toohello alanı aranabilir alanları gibi ile kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="01f96-181">They cannot be used with search conditions specific toohello field like searchable fields.</span></span>  <span data-ttu-id="01f96-182">Yalnızca bir sorgu hello aşağıdaki gibi tüm alanlar boyunca gerçekleştirirken aranır.</span><span class="sxs-lookup"><span data-stu-id="01f96-182">They are only searched when performing a query across all fields such as hello following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="01f96-183">Boole işleçleri</span><span class="sxs-lookup"><span data-stu-id="01f96-183">Boolean operators</span></span>
<span data-ttu-id="01f96-184">DateTime ve sayısal alanlar ile kullanarak değerleri için arama yapabilirsiniz *büyük*, *küçük daha*, ve *küçük veya eşit*.</span><span class="sxs-lookup"><span data-stu-id="01f96-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="01f96-185">Basit işleçleri gibi kullanabilir >, <>, =, < =,! hello sorgu arama çubuğunda =.</span><span class="sxs-lookup"><span data-stu-id="01f96-185">You can use simple operators such as >, < , >=, <= , != in hello query search bar.</span></span>

<span data-ttu-id="01f96-186">Belirli bir süre için belirli bir olay günlüğü sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="01f96-187">Örneğin, hello son 24 saat anımsatıcı ifade aşağıdaki hello ile ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="01f96-187">For example, hello last 24 hours is expressed with hello following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a><span data-ttu-id="01f96-188">Boole işleci kullanılarak toosearch</span><span class="sxs-lookup"><span data-stu-id="01f96-188">toosearch using a boolean operator</span></span>
* <span data-ttu-id="01f96-189">Merhaba arama sorgusu alanına yazın`EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="01f96-189">In hello search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="01f96-190">![Boole değeri ile arama](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="01f96-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="01f96-191">Kontrol edebilirsiniz, ancak zaman aralığı grafik hello ve çoğu kez hello sorgu doğrudan zaman filtresi avantajları tooincluding vardır, toodo isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-191">Although you can control hello time interval graphically, and most times you might want toodo that, there are advantages tooincluding a time filter directly into hello query.</span></span> <span data-ttu-id="01f96-192">Örneğin, bu harika burada kılabilirsiniz hello bağımsız olarak her bölme için hello süresi panolarla çalışır *genel* hello panosu sayfasında Saat Seçici.</span><span class="sxs-lookup"><span data-stu-id="01f96-192">For example, this works great with dashboards where you can override hello time for each tile, regardless of hello *global* time selector on hello dashboard page.</span></span> <span data-ttu-id="01f96-193">Daha fazla bilgi için bkz: [zaman önemlidir panosunda](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span><span class="sxs-lookup"><span data-stu-id="01f96-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="01f96-194">Zamanına göre filtreleme, Merhaba sonuçlar elde göz önünde bulundurmanız *kesişim* Merhaba iki dönemler: hello OMS portalında (S1) belirtilen birinin hello ve biri (S2) hello sorguda belirtilen hello.</span><span class="sxs-lookup"><span data-stu-id="01f96-194">When filtering by time, keep in mind that you get results for hello *intersection* of hello two time periods: hello one specified in hello OMS portal (S1) and hello one specified in hello query (S2).</span></span>

![kesişim](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="01f96-196">Merhaba dönemleri, örneğin burada seçtiğiniz hello OMS portalında kesiştiği yok, bu, gelir **bu hafta** ve burada tanımladığınız hello sorgusunda **geçen hafta**, olmaz ve ardından hiçbir kesişim yoktur herhangi bir sonuç alırsınız.</span><span class="sxs-lookup"><span data-stu-id="01f96-196">This means, if hello time periods don’t intersect, for example in hello OMS portal where you choose **This week** and in hello query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="01f96-197">Karşılaştırma işleçleri Hello TimeGenerated alanı için kullanılan aynı zamanda diğer durumlarda faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="01f96-197">Comparison operators used for hello TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="01f96-198">Örneğin, sayısal alanlar ile.</span><span class="sxs-lookup"><span data-stu-id="01f96-198">For example, with numeric fields.</span></span>

<span data-ttu-id="01f96-199">Örneğin, yapılandırma değerlendirmesi'nin uyarılar önem derecesi değerlerini aşağıdaki hello sahip verilen:</span><span class="sxs-lookup"><span data-stu-id="01f96-199">For example, given that Configuration Assessment’s alerts have hello following severity values:</span></span>

* <span data-ttu-id="01f96-200">0 bilgi =</span><span class="sxs-lookup"><span data-stu-id="01f96-200">0 = Information</span></span>
* <span data-ttu-id="01f96-201">1 uyarı =</span><span class="sxs-lookup"><span data-stu-id="01f96-201">1 = Warning</span></span>
* <span data-ttu-id="01f96-202">2 kritik =</span><span class="sxs-lookup"><span data-stu-id="01f96-202">2 = Critical</span></span>

<span data-ttu-id="01f96-203">Uyarı ve kritik uyarılar için sorgu ve de sorgu aşağıdaki hello bilgilendirme raporlarla hariç:</span><span class="sxs-lookup"><span data-stu-id="01f96-203">You can query for both warning and critical alerts and also exclude informational ones with hello following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="01f96-204">Aralık belirtilen sorguların de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-204">You can also use range queries.</span></span> <span data-ttu-id="01f96-205">Bu değer sırayla hello başlangıcını ve bitişini aralığı sağlayabilir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="01f96-205">This means that you can provide hello beginning and end range of values in a sequence.</span></span> <span data-ttu-id="01f96-206">Örneğin, hello burada hello Operations Manager olay günlüğündeki olaylar istiyorsanız EventID büyük veya ona eşit too2100 ancak değerden daha fazla 2199, sorgu aşağıdaki hello bunları döndürecektir sonra.</span><span class="sxs-lookup"><span data-stu-id="01f96-206">For example, if you want events from hello Operations Manager event log where hello EventID is greater than or equal too2100 but not greater than 2199, then hello following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="01f96-207">kullanmalısınız hello aralığı sözdizimi şöyledir hello iki nokta üst üste (:) alan: değer ayırıcı ve *değil* hello eşittir (=).</span><span class="sxs-lookup"><span data-stu-id="01f96-207">hello range syntax you must use is hello colon (:) field:value separator and *not* hello equal sign (=).</span></span> <span data-ttu-id="01f96-208">Merhaba alt ve üst uç hello aralığının köşeli parantez içine almanız ve bunları iki nokta (.) ile ayırın.</span><span class="sxs-lookup"><span data-stu-id="01f96-208">Enclose hello lower and upper end of hello range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="01f96-209">Arama sonuçları işlemek</span><span class="sxs-lookup"><span data-stu-id="01f96-209">Manipulate search results</span></span>
<span data-ttu-id="01f96-210">Verileri için arama yapıyorsanız, arama sorgunuzu toorefine istediğiniz ve hello sonuçlar üzerinde denetim iyi düzeyine sahip.</span><span class="sxs-lookup"><span data-stu-id="01f96-210">When you're searching for data, you'll want toorefine your search query and have a good level of control over hello results.</span></span> <span data-ttu-id="01f96-211">Sonuçları alınırken, komutları tootransform uygulayabilirsiniz bunları.</span><span class="sxs-lookup"><span data-stu-id="01f96-211">When results are retrieved, you can apply commands tootransform them.</span></span>

<span data-ttu-id="01f96-212">Günlük analizi aramaları komutlarda *gerekir* hello dikey çizgi karakteri (|) sonra izleyin.</span><span class="sxs-lookup"><span data-stu-id="01f96-212">Commands in Log Analytics searches *must* follow after hello vertical pipe character (|).</span></span> <span data-ttu-id="01f96-213">Bir filtre her zaman bir sorgu dizesi hello ilk bölümü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="01f96-213">A filter must always be hello first part of a query string.</span></span> <span data-ttu-id="01f96-214">Merhaba veri kümesi üzerinde çalıştığınız tanımlar ve ardından "Bu sonuçların bir komuta geçirir".</span><span class="sxs-lookup"><span data-stu-id="01f96-214">It defines hello data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="01f96-215">Ardından, hello kanal tooadd ek komutlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-215">You can then use hello pipe tooadd additional commands.</span></span> <span data-ttu-id="01f96-216">Gevşek benzer toohello Windows PowerShell komut zincirini budur.</span><span class="sxs-lookup"><span data-stu-id="01f96-216">This is loosely similar toohello Windows PowerShell pipeline.</span></span>

<span data-ttu-id="01f96-217">Genel olarak, hello günlük analizi arama dili toofollow PowerShell stili ve yönergeleri toomake çalışır BT benzer toohello BT uzmanları ve tooease hello öğrenme eğrisi.</span><span class="sxs-lookup"><span data-stu-id="01f96-217">In general, hello Log Analytics search language tries toofollow PowerShell style and guidelines toomake it similar toohello IT pros, and tooease hello learning curve.</span></span>

<span data-ttu-id="01f96-218">Ne yaptıklarını kolayca anlayabilirsiniz şekilde komutları fiiller adlara sahip.</span><span class="sxs-lookup"><span data-stu-id="01f96-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="01f96-219">Sırala</span><span class="sxs-lookup"><span data-stu-id="01f96-219">Sort</span></span>
<span data-ttu-id="01f96-220">Merhaba sıralama komutu, bir veya birden çok alanlara göre sıralama toodefine hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="01f96-220">hello sort command allows you toodefine hello sorting order by one or multiple fields.</span></span> <span data-ttu-id="01f96-221">Varsayılan olarak kullanmayın olsa bile, azalan bir zorunlu kılınır.</span><span class="sxs-lookup"><span data-stu-id="01f96-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="01f96-222">Merhaba en son sonuçları her zaman arama sonuçları hello üstünde olur.</span><span class="sxs-lookup"><span data-stu-id="01f96-222">hello most recent results are always at hello top of search results.</span></span> <span data-ttu-id="01f96-223">Bunun anlamı ile bir aramayı çalıştırırken `Type=Event EventID=1234` ne gerçekten sizin için yürütülen olan:</span><span class="sxs-lookup"><span data-stu-id="01f96-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="01f96-224">Günlüklerde bilginiz deneyimi hello türü olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="01f96-224">That's because it is hello type of experience you are familiar with in logs.</span></span> <span data-ttu-id="01f96-225">Örneğin, Windows Olay Görüntüleyicisi'ni hello.</span><span class="sxs-lookup"><span data-stu-id="01f96-225">For example, in hello Windows Event Viewer.</span></span>

<span data-ttu-id="01f96-226">Sıralama toochange hello şekilde sonuçların döndürülmesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-226">You can use Sort toochange hello way results are returned.</span></span> <span data-ttu-id="01f96-227">Merhaba aşağıdaki örneklerde bunun nasıl çalıştığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="01f96-227">hello following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="01f96-228">Merhaba basit yukarıdaki, komutları nasıl--örnekler döndürülen filtre hello hello sonuçları hello şeklini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="01f96-228">hello simple examples above show you how commands work--they change hello shape of hello results that hello filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="01f96-229">Ve üst sınırı</span><span class="sxs-lookup"><span data-stu-id="01f96-229">Limit and top</span></span>
<span data-ttu-id="01f96-230">Daha az bilinen başka bir komuta sınırıdır.</span><span class="sxs-lookup"><span data-stu-id="01f96-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="01f96-231">PowerShell benzeri fiil sınırıdır.</span><span class="sxs-lookup"><span data-stu-id="01f96-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="01f96-232">Sınır işlevsel olarak aynı toohello üst komuttur.</span><span class="sxs-lookup"><span data-stu-id="01f96-232">Limit is functionally identical toohello TOP command.</span></span> <span data-ttu-id="01f96-233">Merhaba aşağıdaki sorguları hello aynı sonuçları döndürür.</span><span class="sxs-lookup"><span data-stu-id="01f96-233">hello following queries return hello same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a><span data-ttu-id="01f96-234">üst kullanarak toosearch</span><span class="sxs-lookup"><span data-stu-id="01f96-234">toosearch using top</span></span>
* <span data-ttu-id="01f96-235">Merhaba arama sorgusu alanına yazın`Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="01f96-235">In hello search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="01f96-236">![Arama üst](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="01f96-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="01f96-237">Merhaba görüntüde yukarıdaki EventID 358 bin kayıtlarıyla vardır = 600.</span><span class="sxs-lookup"><span data-stu-id="01f96-237">In hello image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="01f96-238">Merhaba alanları, modelleri ve her zaman döndürülen hello sonuçları hakkında bilgi gösterir sol hello filtreleri *hello filtre bölümü tarafından* tüm dikey çizgi karakterinden önce hello parçasıdır hello sorgu.</span><span class="sxs-lookup"><span data-stu-id="01f96-238">hello fields, facets, and filters on hello left always show information about hello results returned *by hello filter portion* of hello query, which is hello part before any pipe character.</span></span> <span data-ttu-id="01f96-239">Merhaba **sonuçları** bölmesinde çünkü hello örnek komut şeklinde ve hello sonuçları dönüştürülmüş hello en son 1 sonuç, yalnızca döndürür.</span><span class="sxs-lookup"><span data-stu-id="01f96-239">hello **Results** pane only returns hello most recent 1 result, because hello example command shaped and transformed hello results.</span></span>

### <a name="select"></a><span data-ttu-id="01f96-240">Şunu seçin:</span><span class="sxs-lookup"><span data-stu-id="01f96-240">Select</span></span>
<span data-ttu-id="01f96-241">Merhaba SELECT komutu Select-Object PowerShell'de gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="01f96-241">hello SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="01f96-242">Tüm özgün özelliklerine sahip olmayan filtrelenen sonuçları döndürür.</span><span class="sxs-lookup"><span data-stu-id="01f96-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="01f96-243">Bunun yerine, yalnızca belirttiğiniz hello özellikleri seçer.</span><span class="sxs-lookup"><span data-stu-id="01f96-243">Instead, it selects only hello properties that you specify.</span></span>

#### <a name="toorun-a-search-using-hello-select-command"></a><span data-ttu-id="01f96-244">bir arama hello select komutunu kullanarak toorun</span><span class="sxs-lookup"><span data-stu-id="01f96-244">toorun a search using hello select command</span></span>
1. <span data-ttu-id="01f96-245">Aramada, yazın `Type=Event` ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="01f96-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="01f96-246">Tıklatın **+ daha fazla Göster** sonuçları hello tüm hello özelliklere sahip hello sonuçları tooview birinde.</span><span class="sxs-lookup"><span data-stu-id="01f96-246">Click **+ show more** in one of hello results tooview all hello properties that hello results have.</span></span>
3. <span data-ttu-id="01f96-247">Bazıları açıkça hello sorgu değişiklikleri çok seçin ve`Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="01f96-247">Select some of those explicitly, and hello query changes too`Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="01f96-248">![Ara'yı seçin](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="01f96-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="01f96-249">Bu komut, toocontrol arama çıkış ve genellikle hello tam kayıt değil, araştırması için yalnızca gerçekten önemli veri hello bölümleri seçin istediğinizde özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="01f96-249">This command is particularly useful when you want toocontrol search output and choose only hello portions of data that really matter for your exploration, which often isn’t hello full record.</span></span> <span data-ttu-id="01f96-250">Farklı türlerde kayıtlar varsa, bu da yararlıdır *bazı* ortak özellikler, ama *tüm* kendi ortak özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="01f96-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="01f96-251">, Daha doğal olarak bir tablo gibi görünen bir çıktı oluşturmak veya tooa CSV dosyasına dışarı aktardığınız ve Excel'de massaged iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="01f96-251">The, you can generate output that looks more naturally like a table, or work well when exported tooa CSV file and then massaged in Excel.</span></span>

## <a name="use-hello-measure-command"></a><span data-ttu-id="01f96-252">Merhaba ölçü komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-252">Use hello measure command</span></span>
<span data-ttu-id="01f96-253">ÖLÇÜ hello en çok yönlü günlük analizi aramaları komutlarda biridir.</span><span class="sxs-lookup"><span data-stu-id="01f96-253">MEASURE is one of hello most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="01f96-254">Tooapply istatistiksel tanır *işlevleri* tooyour veri ve toplama sonuçları belirli bir alana göre gruplandırılmış.</span><span class="sxs-lookup"><span data-stu-id="01f96-254">It allows you tooapply statistical *functions* tooyour data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="01f96-255">Ölçü destekleyen birden çok istatistik işlevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="01f96-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="01f96-256">Ölçü Count() işlevi</span><span class="sxs-lookup"><span data-stu-id="01f96-256">Measure count()</span></span>
<span data-ttu-id="01f96-257">ilk istatistiksel işlevi toowork ile Merhaba ve hello basit toounderstand biri hello *count()* işlevi.</span><span class="sxs-lookup"><span data-stu-id="01f96-257">hello first statistical function toowork with, and one of hello simplest toounderstand is hello *count()* function.</span></span>

<span data-ttu-id="01f96-258">Bir arama sorgusundan gibi sonuçları `Type=Event`, arama sonuçları tarafında kalan hello üzerinde modelleri olarak da bilinir filtrelerini göster.</span><span class="sxs-lookup"><span data-stu-id="01f96-258">Results from any search query such as `Type=Event`, show filters also called facets on hello left side of search results.</span></span> <span data-ttu-id="01f96-259">Merhaba filtreleri hello sonuçları için belirli bir alan değerleriyle dağıtımını yürütülen hello aramada gösterir.</span><span class="sxs-lookup"><span data-stu-id="01f96-259">hello filters show a distribution of values by a given field for hello results in hello search executed.</span></span>

![Ara ölçü birimi sayısı](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="01f96-261">Örneğin, yukarıdaki görüntü hello hello görürsünüz **bilgisayar** alan ve gösterir hello sonuçlarında hello neredeyse 739 bin olayları içinde olduğunu hello 68 benzersiz ve ayrı değerlerini **bilgisayar** Kayıtların alan.</span><span class="sxs-lookup"><span data-stu-id="01f96-261">For example, in hello image above you'll see hello **Computer** field and it shows that within hello almost 739 thousand events in hello results, there are 68 unique and distinct values for hello **Computer** field in those records.</span></span> <span data-ttu-id="01f96-262">Merhaba kutucuğu yalnızca hello yazılan hello en yaygın 5 değerler üst 5 hello gösterir **bilgisayar** alanları), bu alan belirli değeri içeren belgeleri hello sayısına göre sıralanmış.</span><span class="sxs-lookup"><span data-stu-id="01f96-262">hello tile only shows hello top 5, which are hello most common 5 values that are written in hello **Computer** fields), sorted by hello number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="01f96-263">Merhaba görüntüde neredeyse 369 bin olayları arasında– 90 bin hello OpsInsights04.contoso.com bilgisayardan 83 bin hello DB03.contoso.com bilgisayardan gelen vb. – görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-263">In hello image you can see that – among those almost 369 thousand events – 90 thousand come from hello OpsInsights04.contoso.com computer, 83 thousand from hello DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="01f96-264">Ne Hello kutucuğu, yalnızca hello yalnızca ilk 5 gösterir. bu yana tüm değerlerinin toosee istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="01f96-264">What if you want toosee all values, since hello tile only shows only hello top 5?</span></span>

<span data-ttu-id="01f96-265">Hangi hello ölçü olan komut hello count() işlevini kullanarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-265">That’s what hello measure command can do with hello count() function.</span></span> <span data-ttu-id="01f96-266">Bu işlev, herhangi bir parametre kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="01f96-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="01f96-267">Yalnızca istediğiniz toogroup tarafından – hello hello alan belirttiğiniz **bilgisayar** bu durumda alan:</span><span class="sxs-lookup"><span data-stu-id="01f96-267">You just specify hello field by which you want toogroup by – hello **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![Ara ölçü birimi sayısı](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="01f96-269">Ancak, **bilgisayar** kullanılan bir alan *içinde* veri – her parçası ilişkisel veritabanı dahil olan ve ayrı olmadığından **bilgisayar** herhangi bir yere nesne.</span><span class="sxs-lookup"><span data-stu-id="01f96-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="01f96-270">Yalnızca, değerleri hello *içinde* veri tanımlayabilir hello hangi varlık oluşturulan bunları ve diğer özellikleri sayısı ve hello veri – yönlerini bu nedenle hello terim *modeli*.</span><span class="sxs-lookup"><span data-stu-id="01f96-270">Just hello values *in* hello data can describe which entity generated them, and a number of other characteristics and aspects of hello data – hence hello term *facet*.</span></span> <span data-ttu-id="01f96-271">Ancak, yalnızca de diğer alanlara göre gruplandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="01f96-272">Merhaba özgün hello ölçü komuta yöneltilen neredeyse 739 bin olayları sonuçlarını da adlı bir alan olduğundan **EventID**, uygulayabileceğiniz hello bu alana göre aynı teknik toogroup ve EventID olayların sayısını alın:</span><span class="sxs-lookup"><span data-stu-id="01f96-272">Because hello original results of almost 739 thousand events that are piped into hello measure command also have a field called **EventID**, you can apply hello same technique toogroup by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="01f96-273">Belirli bir değer içeren hello gerçek kayıt sayısı ilgilendiğiniz değil, ancak yalnızca bir listesini istiyorsanız bunun yerine hello kendilerini değerleri varsa, ekleyebileceğiniz bir *seçin* sonunda hello ve yalnızca select hello ilk sütun komutu:</span><span class="sxs-lookup"><span data-stu-id="01f96-273">If you're not interested in hello actual record count that contain a specific value, but instead if you only want a list of hello values themselves, you can add a *Select* command at hello end of it and just select hello first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="01f96-274">Ardından daha karmaşık almak ve hello hello sorgu sonuçlarında önceden sıralama veya hello sütunları hello kılavuzunda çok yalnızca tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01f96-274">Then you can get more intricate and pre-sort hello results in hello query, or you can just click hello columns in hello grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a><span data-ttu-id="01f96-275">Ölçü count kullanarak toosearch</span><span class="sxs-lookup"><span data-stu-id="01f96-275">toosearch using measure count</span></span>
* <span data-ttu-id="01f96-276">Merhaba arama sorgusu alanına yazın`Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="01f96-276">In hello search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="01f96-277">Append `| Select EventID` hello sorgu toohello sonu.</span><span class="sxs-lookup"><span data-stu-id="01f96-277">Append `| Select EventID` toohello end of hello query.</span></span>
* <span data-ttu-id="01f96-278">Son olarak, append `| Sort EventID asc` hello sorgu toohello sonu.</span><span class="sxs-lookup"><span data-stu-id="01f96-278">Finally, append `| Sort EventID asc` toohello end of hello query.</span></span>

<span data-ttu-id="01f96-279">Birkaç önemli noktaları toonotice vardır ve vurgulama:</span><span class="sxs-lookup"><span data-stu-id="01f96-279">There are a couple important points toonotice and emphasize:</span></span>

<span data-ttu-id="01f96-280">İlk olarak, gördüğünüz hello sonuçları hello özgün ham sonuçları artık değildir.</span><span class="sxs-lookup"><span data-stu-id="01f96-280">First, hello results you see are not hello original raw results anymore.</span></span> <span data-ttu-id="01f96-281">Bunun yerine, toplanan sonuçları – oldukları temelde sonuçları grupları.</span><span class="sxs-lookup"><span data-stu-id="01f96-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="01f96-282">Bu bir sorun değildir, ancak çok farklı bir farklı veri şekli hello kolay bir şekilde hello toplama/istatistiksel işlevi sonucu olarak oluşturulan hello özgün ham şeklin ile etkileşim anlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="01f96-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from hello original raw shape that gets created on hello fly as a result of hello aggregation/statistical function.</span></span>

<span data-ttu-id="01f96-283">İkinci, **ölçmek sayısı** şu anda döndürür üst 100 farklı sonuçlar yalnızca hello.</span><span class="sxs-lookup"><span data-stu-id="01f96-283">Second, **Measure count** currently returns only hello top 100 distinct results.</span></span> <span data-ttu-id="01f96-284">Bu sınır toohello diğer istatistik işlevleri geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="01f96-284">This limit does not apply toohello other statistical functions.</span></span> <span data-ttu-id="01f96-285">Bu nedenle, ölçü count() uygulamadan önce belirli öğeleri toouse daha kesin bir filtre ilk toosearch genellikle gerekir.</span><span class="sxs-lookup"><span data-stu-id="01f96-285">So, you'll usually need toouse a more precise filter first toosearch for specific items before you apply measure count().</span></span>

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a><span data-ttu-id="01f96-286">Merhaba ölçü komutuyla Hello maksimum ve minimum işlevlerini kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-286">Use hello max and min functions with hello measure command</span></span>
<span data-ttu-id="01f96-287">Çeşitli senaryolarda nerede **ölçü Max()** ve **ölçü MIN()** yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="01f96-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="01f96-288">Bununla birlikte, her işlev ters olduğundan birbirinden biz Max() göstermeye ve, MIN() ile kendiniz deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="01f96-289">Güvenlik olayları için sorgu, sahip oldukları bir **düzeyi** değişebilir özelliği.</span><span class="sxs-lookup"><span data-stu-id="01f96-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="01f96-290">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="01f96-290">For example:</span></span>

```
Type=SecurityEvent
```

![Ara ölçü sayısı Başlat](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="01f96-292">Tüm hello güvenlik tooview hello en yüksek değer istiyorsanız hello Grup alana göre ortak bir bilgisayarı verilen olayları kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="01f96-292">If you want tooview hello highest value for all of hello security events given a common Computer, hello group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![Ölçü max bilgisayar arama](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="01f96-294">Vardı hello bilgisayarlar için görüntüleyeceği **düzeyi** kayıtları, bunların çoğu sahip en az düzey 8, birçok 16 düzeyini vardı.</span><span class="sxs-lookup"><span data-stu-id="01f96-294">It will display that for hello computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![bilgisayar arama ölçü max süresi oluşturulan](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="01f96-296">Bu işlev numaralarıyla iyi çalışır, ancak DateTime alanları ile de çalışır.</span><span class="sxs-lookup"><span data-stu-id="01f96-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="01f96-297">Hello için yararlı toocheck son olduğu veya her bilgisayar için herhangi bir veri parçası için en son zaman damgasını dizinli.</span><span class="sxs-lookup"><span data-stu-id="01f96-297">It is useful toocheck for hello last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="01f96-298">Örneğin: ne zaman hello en son güvenlik olayı bildirildi her makine için?</span><span class="sxs-lookup"><span data-stu-id="01f96-298">For example: When was hello most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="01f96-299">Merhaba avg işlevi ile Merhaba ölçü komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-299">Use hello avg function with hello measure command</span></span>
<span data-ttu-id="01f96-300">Merhaba Avg() istatistiksel işlevi ölçü ile kullanılan bazı alan için toocalculate hello ortalama değer sağlar ve aynı ya da diğer alan grubu tarafından hello sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="01f96-300">hello Avg() statistical function used with measure allows you toocalculate hello average value for some field, and group results by hello same or other field.</span></span> <span data-ttu-id="01f96-301">Bu durumda, performans verileri gibi çeşitli yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="01f96-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="01f96-302">Performans verileri ile başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="01f96-302">We'll start with performance data.</span></span> <span data-ttu-id="01f96-303">OMS şu anda hem Windows hem de Linux makineler performans sayaçlarını toplar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="01f96-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="01f96-304">için toosearch *tüm* performans verileri, hello en temel sorgudur:</span><span class="sxs-lookup"><span data-stu-id="01f96-304">toosearch for *all* performance data, hello most basic query is:</span></span>

```
Type=Perf
```

![Arama avg Başlat](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="01f96-306">Hello fark ilk şey günlük analizi, üç Perspektifler gösterir.: hangi hello grafikleri; hello gerçek kayıtları gösteren gösterir listesi Tablo, performans sayacı verileri tablo görünümünü gösterir; ve ölçümleri, performans sayaçları hello grafiklerde gösterir.</span><span class="sxs-lookup"><span data-stu-id="01f96-306">hello first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows hello actual records behind hello charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for hello performance counters.</span></span>

<span data-ttu-id="01f96-307">Merhaba görüntüde yukarıdaki hello aşağıdaki belirtmek işaretlenmiş alanlar iki kümesi vardır:</span><span class="sxs-lookup"><span data-stu-id="01f96-307">In hello image above, there are two sets of fields marked that indicate hello following:</span></span>

* <span data-ttu-id="01f96-308">Hello ilk kümesi hello sorgu filtresi Windows performans sayacı adı, nesne adı ve örnek adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="01f96-308">hello first set identifies Windows Performance Counter Name, Object Name, and Instance Name in hello query filter.</span></span> <span data-ttu-id="01f96-309">Bu büyük olasılıkla en yaygın olarak modelleri/filtre olarak kullanacağınız hello alanları</span><span class="sxs-lookup"><span data-stu-id="01f96-309">These are hello fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="01f96-310">**CounterValue** hello gerçek hello sayaç değeri.</span><span class="sxs-lookup"><span data-stu-id="01f96-310">**CounterValue** is hello actual value of hello counter.</span></span> <span data-ttu-id="01f96-311">Bu örnekte, hello değerdir *75*.</span><span class="sxs-lookup"><span data-stu-id="01f96-311">In this example, hello value is *75*.</span></span>
* <span data-ttu-id="01f96-312">**TimeGenerated** 12:51, 24 saatlik zaman biçiminde değil.</span><span class="sxs-lookup"><span data-stu-id="01f96-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="01f96-313">Merhaba ölçümleri grafik bir görünümünü aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="01f96-313">Here's a view of hello metrics in a graph.</span></span>

![Arama avg Başlat](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="01f96-315">Merhaba Perf kayıt şekli okumayı ve diğer arama teknikleri hakkında okuyun sonra bu tür sayısal veriler ölçü Avg() tooaggregate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-315">After reading about hello Perf record shape, and having read about other search techniques, you can use measure Avg() tooaggregate this type of numerical data.</span></span>

<span data-ttu-id="01f96-316">Basit bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="01f96-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![Ortalama görüntülendiğinden arama](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="01f96-318">Bu örnekte, hello toplam CPU süresi performans sayacı ve bilgisayar bazında ortalama seçin.</span><span class="sxs-lookup"><span data-stu-id="01f96-318">In this example, you select hello CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="01f96-319">Sonuçları tooonly hello son 6 saat toonarrow istiyorsanız, başlangıç zamanı filtre denetimi kullanabilir veya sorgunuzda aşağıdaki gibi belirtin:</span><span class="sxs-lookup"><span data-stu-id="01f96-319">If you want toonarrow down your results tooonly hello last 6 hours, you can either use hello time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="01f96-320">Merhaba ölçü komutuyla Hello avg işlevi kullanarak toosearch</span><span class="sxs-lookup"><span data-stu-id="01f96-320">toosearch using hello avg function with hello measure command</span></span>
* <span data-ttu-id="01f96-321">Merhaba arama sorgusu, kutusuna `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="01f96-321">In hello Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="01f96-322">Toplama ve ilişkilendirmek veri *arasında* bilgisayarlar.</span><span class="sxs-lookup"><span data-stu-id="01f96-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="01f96-323">Örneğin, diğeri her düğüm eşit tooany olduğu Grup çeşit konakların kümesine sahiptir ve yalnızca aynı türde çalışma ve yük kabaca dengelenmelidir tüm hello yaparlar düşünün.</span><span class="sxs-lookup"><span data-stu-id="01f96-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal tooany other one and they just do all hello same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="01f96-324">Tek aşağıdaki sorgulamak ve ortalamalar hello tüm grup için alma hello ile Git bunların sayaçlarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-324">You could get their counters all in one go with hello following query and get averages for hello entire farm.</span></span> <span data-ttu-id="01f96-325">Aşağıdaki örneğine hello ile Merhaba bilgisayarlar seçerek başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="01f96-325">You can start by choosing hello computers with hello following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="01f96-326">Merhaba bilgisayarlara sahip olduğunuza göre aynı zamanda yalnızca tooselect iki ana performans göstergelerini (KPI'lar) istediğiniz: CPU kullanımı % ve % boş Disk alanı.</span><span class="sxs-lookup"><span data-stu-id="01f96-326">Now that you have hello computers, you also only want tooselect two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="01f96-327">Bu nedenle, bu hello sorgu parçası haline gelir:</span><span class="sxs-lookup"><span data-stu-id="01f96-327">So, that part of hello query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="01f96-328">Artık aşağıdaki örneğine hello ile bilgisayarları ve sayaçları ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="01f96-328">Now you can add computers and counters with hello following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="01f96-329">Çok belirli bir seçim olduğundan hello **Avg() ölçmek** komutu dönebilirsiniz hello ortalama bilgisayar tarafından değil, ancak hello grubu CounterName gruplandırarak tarafından yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="01f96-329">Because you have a very specific selection, hello **measure Avg()** command can return hello average not by computer, but across hello farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="01f96-330">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="01f96-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="01f96-331">Bu, birkaç ortamınızı ait KPI'ları yararlı compact bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="01f96-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![Arama avg gruplandırma](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="01f96-333">Bir Panoda hello arama sorgusu kolayca kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-333">You can easily use hello search query in a dashboard.</span></span> <span data-ttu-id="01f96-334">Örneğin, hello arama sorgusunu kaydetmek ve Pano adlı ondan oluşturma *Web grubu KPI'ları*.</span><span class="sxs-lookup"><span data-stu-id="01f96-334">For example, you could save hello search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="01f96-335">panoları, kullanma hakkında daha fazla toolearn bkz [günlük analizi özel bir pano oluşturun](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="01f96-335">toolearn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![Arama avg Panosu](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a><span data-ttu-id="01f96-337">Merhaba ölçü komutuyla Hello TOPLA işlevini kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-337">Use hello sum function with hello measure command</span></span>
<span data-ttu-id="01f96-338">Merhaba ölçü komutu benzer tooother işlevlerini Hello toplam işlevdir.</span><span class="sxs-lookup"><span data-stu-id="01f96-338">hello sum function is similar tooother functions of hello measure command.</span></span> <span data-ttu-id="01f96-339">Nasıl toouse hello konumundaki toplam işlev hakkında bir örnek görebilirsiniz [W3C IIS günlüklerini Microsoft Azure operasyonel Öngörüler aramada](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="01f96-339">You can see an example about how toouse hello sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="01f96-340">Sayı, tarih saatler ve metin dizelerini Max() ve MIN() kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="01f96-341">Metin dizelerini ile alfabetik olarak sıralanan ve ilk alın ve en son.</span><span class="sxs-lookup"><span data-stu-id="01f96-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="01f96-342">Ancak, sayısal alanlar dışında herhangi bir şeyle Sum() kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="01f96-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="01f96-343">Bu durum, tooAvg() de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="01f96-343">This also applies tooAvg().</span></span>

### <a name="use-hello-percentile-function-with-hello-measure-command"></a><span data-ttu-id="01f96-344">Merhaba yüzdebirlik işlevi ile Merhaba ölçü komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-344">Use hello percentile function with hello measure command</span></span>
<span data-ttu-id="01f96-345">Bunu yalnızca sayısal alanlarında kullanabilirsiniz hello yüzdebirlik işlevi benzer tooAvg() ve Sum() olmamasıdır.</span><span class="sxs-lookup"><span data-stu-id="01f96-345">hello percentile function is similar tooAvg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="01f96-346">Bir sayısal alana 1 too99 arasında herhangi bir yüzdebirlik kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-346">You can use any percentile between 1 too99 on a numeric field.</span></span> <span data-ttu-id="01f96-347">Her ikisi de kullanabilirsiniz **yüzdelik** ve **pct** komutları.</span><span class="sxs-lookup"><span data-stu-id="01f96-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="01f96-348">Aşağıda birkaç örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="01f96-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a><span data-ttu-id="01f96-349">Komutunu Hello kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-349">Use hello where command</span></span>
<span data-ttu-id="01f96-350">Burada komutu filtresi gibi çalışır, ancak hello ardışık düzen toofurther filtrede uygulanabilir hello ölçü komutu tarafından – bir sorgu hello başında filtrelenen karşılıklı tooraw sonuçları olarak üretilmiş sonuçları bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="01f96-350">hello where command works like a filter, but it can be applied in hello pipeline toofurther filter aggregated results that have been produced by a Measure command – as opposed tooraw results that are filtered at hello beginning of a query.</span></span>

<span data-ttu-id="01f96-351">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="01f96-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="01f96-352">Başka bir kanal Ekle "|" karakter ve hello komutu tooonly, ortalama CPU ile %80 olduğu bilgisayarları nereden hello örnek:</span><span class="sxs-lookup"><span data-stu-id="01f96-352">You can add another pipe "|" character and hello Where command tooonly get computers whose average CPU is above 80%, with hello following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="01f96-353">Microsoft System Center - Operations Manager aşinaysanız komutu burada Yönetim Paketi terimleriyle Merhaba düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of hello where command in management pack terms.</span></span> <span data-ttu-id="01f96-354">Hello örnek kural olsaydı, hello ilk bölümü hello hello veri kaynağı ve hello komutu hello koşul algılama olduğu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="01f96-354">If hello example were a rule, hello first part of hello query would be hello data source and hello where command would be hello condition detection.</span></span>

<span data-ttu-id="01f96-355">Bir kutucuk olarak hello sorgu kullanabilirsiniz **My Pano**, monitör, türlerdeki bilgisayar CPU aşırı kullanılan olduğunda toosee olarak.</span><span class="sxs-lookup"><span data-stu-id="01f96-355">You can use hello query as a tile in **My Dashboard**, as a monitor of sorts, toosee when computer CPUs are over-utilized.</span></span> <span data-ttu-id="01f96-356">panolar, hakkında daha fazla toolearn bkz [günlük analizi özel bir pano oluşturun](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="01f96-356">toolearn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="01f96-357">Ayrıca, oluşturabilir ve hello mobil uygulama kullanarak panoları kullanın.</span><span class="sxs-lookup"><span data-stu-id="01f96-357">You can also create and use dashboards using hello mobile app.</span></span> <span data-ttu-id="01f96-358">Daha fazla bilgi için bkz: [OMS mobil uygulama ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="01f96-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="01f96-359">İçinde Hello alt iki döşeme görüntü aşağıdaki Merhaba, hello İzleyicisi görüntülenen listesini görebilirsiniz ve bir sayı olarak.</span><span class="sxs-lookup"><span data-stu-id="01f96-359">In hello bottom two tiles of hello following image, you can see hello monitor displayed a list and as a number.</span></span> <span data-ttu-id="01f96-360">Aslında, her zaman hello numara toobe sıfır istediğiniz ve boş liste toobe hello.</span><span class="sxs-lookup"><span data-stu-id="01f96-360">Essentially, you always want hello number toobe zero and hello list toobe empty.</span></span> <span data-ttu-id="01f96-361">Aksi halde, bir uyarı koşulu belirtir.</span><span class="sxs-lookup"><span data-stu-id="01f96-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="01f96-362">Gerekirse, hangi makinelerin göz baskısı altında olan tootake kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-362">If needed, you can use it tootake a look at which machines are under pressure.</span></span>

![Mobil Pano](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a><span data-ttu-id="01f96-364">Merhaba işlecinde kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-364">Use hello in operator</span></span>
<span data-ttu-id="01f96-365">Merhaba *IN* işleci ile birlikte *NOT ın* bağımsız değişken olarak başka bir arama dahil aramalar toouse subsearches sağlar.</span><span class="sxs-lookup"><span data-stu-id="01f96-365">hello *IN* operator, along with *NOT IN* allows you toouse subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="01f96-366">Bunların içerdiği içinde başka bir küme ayraçları {} içinde *birincil* veya *dış* arama.</span><span class="sxs-lookup"><span data-stu-id="01f96-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="01f96-367">Merhaba sonucu subsearch, genellikle farklı sonuçlar listesi sonra birincil arama bir bağımsız değişken olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="01f96-367">hello result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="01f96-368">Arama ifadesi, ancak bir aramadan oluşturulabilir, doğrudan açıklamak olamaz, verilerinizi subsearches toomatch alt kümelerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-368">You can use subsearches toomatch subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="01f96-369">Örneğin, bir arama toofind'ın tüm olayları kullanmayı düşünüyorsanız *güvenlik güncelleştirmeleri eksik olan bilgisayarlar*, yeniden toodesign ilk tanımlayan bir subsearch gerekiyor *güvenlik güncelleştirmeleri eksik olan bilgisayarlar*  önce ait toothose konakları olayları bulur.</span><span class="sxs-lookup"><span data-stu-id="01f96-369">For example, if you’re interested in using one search toofind all events from *computers missing security updates*, then you need toodesign a subsearch that first identifies that *computers missing security updates* before it finds events belonging toothose hosts.</span></span>

<span data-ttu-id="01f96-370">Bu nedenle, express *şu anda eksik olan bilgisayarlar gerekli güvenlik güncelleştirmeleri* sorgu aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="01f96-370">So, you could express *computers currently missing required security updates* with hello following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![Arama örnekte](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="01f96-372">Merhaba listesine sahip olduktan sonra bu bilgisayarlar için olayları arar bir dış (birincil) arama içine iç arama toofeed hello bilgisayarların bir listesini hello aramayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-372">Once you have hello list, you can use hello search as an inner search toofeed hello list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="01f96-373">Merhaba iç arama ayraçlar içinde kapsayan ve hello ın işlecini kullanarak hello dış arama filtresi/alan için olası değerler olarak sonuçlarını besleme bunu.</span><span class="sxs-lookup"><span data-stu-id="01f96-373">You do this by enclosing hello inner search in braces and feeding its results as possible values for a filter/field in hello outer search using hello IN operator.</span></span> <span data-ttu-id="01f96-374">Merhaba sorgu benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="01f96-374">hello query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![Arama örnekte](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="01f96-376">Ayrıca hello iç arama için kullanılan filtre hello Sistem Güncelleştirme değerlendirmesi bildirimi hello tüm bilgisayarların bir anlık görüntü her 24 saatte sürüyor.</span><span class="sxs-lookup"><span data-stu-id="01f96-376">Also notice hello time filter used in hello inner search because hello System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="01f96-377">Yalnızca bir gün için arama yaparak daha basit ve hassas hello iç sorgu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-377">You can make hello inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="01f96-378">Merhaba dış arama yerine hello saat seçimini hello kullanıcı arabiriminde, son 7 gün hello olayları alınırken kullanır.</span><span class="sxs-lookup"><span data-stu-id="01f96-378">hello outer search instead uses hello time selection in hello user interface, retrieving events from hello last 7 days.</span></span> <span data-ttu-id="01f96-379">Bkz: [Boole işleçleri](#boolean-operators) zamanı işleçleri hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="01f96-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="01f96-380">Çünkü, dış bir hello iç arama için bir filtre değeri olarak yalnızca kullanım hello sonuçlarını Merhaba, yine de hello dış arama komutlarda uygulayabilir.</span><span class="sxs-lookup"><span data-stu-id="01f96-380">Because you really only use hello results of hello inner search as a filter value for hello outer one, you can still apply commands in hello outer search.</span></span> <span data-ttu-id="01f96-381">Örneğin, hala başka bir ölçü komutuyla olayları yukarıda Grup hello yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="01f96-381">For example, you can still group hello above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![Arama örnekte](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="01f96-383">Günlük analizi Hizmet tarafı zaman aşımları, tooreturn sonuçları az miktarda için de içerdiğinden ve genellikle, iç sorgu tooexecute hızla istersiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-383">Generally, you want your inner query tooexecute quickly because Log Analytics has service-side timeouts for it and also tooreturn a small amount of results.</span></span> <span data-ttu-id="01f96-384">Merhaba iç sorgu daha fazla sonuç döndürürse, hello sonuç listesi, hangi olası hello dış arama tooreturn yanlış sonuçlara neden olabilecek kesilmiş.</span><span class="sxs-lookup"><span data-stu-id="01f96-384">If hello inner query returns more results, hello result list gets truncated, which could potentially cause hello outer search tooreturn incorrect results.</span></span>

<span data-ttu-id="01f96-385">Merhaba iç arama şu anda tooprovide gereken başka bir kuraldır *toplanmış* sonuçları.</span><span class="sxs-lookup"><span data-stu-id="01f96-385">Another rule is that hello inner search currently needs tooprovide *aggregated* results.</span></span> <span data-ttu-id="01f96-386">Diğer bir deyişle, içermesi gereken bir *ölçü* komut; şu anda bir dış arama ham sonuçları akışı olamaz.</span><span class="sxs-lookup"><span data-stu-id="01f96-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="01f96-387">Ayrıca, yalnızca bir ın işleci olabilir ve hello son filtre hello sorgusunda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="01f96-387">Also, there can be only one IN operator and it must be hello last filter in hello query.</span></span> <span data-ttu-id="01f96-388">Bu temelde engeller birden çok subsearches çalıştıran veya birden çok giriş işleç olamaz: hello noktasıdır yalnızca bir alt/iç arama önemli her dış Ara mümkündür.</span><span class="sxs-lookup"><span data-stu-id="01f96-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: hello important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="01f96-389">Bu sınırları olsa da ın pek çok bağlantılı aramalar sağlar ve toodefine sağlar bilgisayarlar, kullanıcılar veya dosyaları – gibi benzeri toogroups verilerinizde ne olursa olsun hello alanları içerir.</span><span class="sxs-lookup"><span data-stu-id="01f96-389">Even with these limits, IN enables many kinds of correlated searches, and allows you toodefine something similar toogroups such as computers, users, or files – whatever hello fields in your data contain.</span></span> <span data-ttu-id="01f96-390">Daha fazla örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="01f96-390">Here are more examples:</span></span>

<span data-ttu-id="01f96-391">**Tüm güncelleştirmeler, otomatik güncelleştirme ayarlarını devre dışı bilgisayarlardan eksik**</span><span class="sxs-lookup"><span data-stu-id="01f96-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="01f96-392">**SQL Server (SQL değerlendirmesi çalıştırdığı =) çalıştıran bilgisayarlardan tüm hata olayları**</span><span class="sxs-lookup"><span data-stu-id="01f96-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="01f96-393">**Etki alanı denetleyicileri (AD değerlendirmesi çalıştırdığı =) bilgisayarlardan tüm güvenlik olayları**</span><span class="sxs-lookup"><span data-stu-id="01f96-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="01f96-394">**Hangi diğer hesapları toohello üzerinde oturum burada hesabı BACONLAND\jochan açmış aynı bilgisayar?**</span><span class="sxs-lookup"><span data-stu-id="01f96-394">**Which other accounts have logged on toohello same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a><span data-ttu-id="01f96-395">Merhaba ayrı komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-395">Use hello distinct command</span></span>
<span data-ttu-id="01f96-396">Merhaba adı da anlaşılacağı gibi bu komut bir alan için farklı değerler listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="01f96-396">As hello name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="01f96-397">Bu, şaşırtıcı basit ancak çok yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="01f96-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="01f96-398">Merhaba aynı ölçü count() komutuyla yanı sıra, aşağıda gösterilen elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="01f96-398">hello same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![FARKLI arama komut örneği](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="01f96-400">Tüm ilgilendiğiniz yalnızca farklı değerleri ve hello olmayıp bu değerlere sahip belgelerin bir listesi ise, ancak ardından DISTINCT çıktı temizleyici ve daha kolay tooread ve kısa sözdizimi, aşağıda gösterildiği gibi sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="01f96-400">However, if all you're interested in is just a list of distinct values and not hello count of documents that have that values, then DISTINCT can provide cleaner and easier tooread output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![FARKLI arama komut örneği](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a><span data-ttu-id="01f96-402">Merhaba ölçü komutuyla Hello countdistinct işlevini kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-402">Use hello countdistinct function with hello measure command</span></span>
<span data-ttu-id="01f96-403">Merhaba countdistinct işlevi hello her grup içindeki farklı değerleri sayar.</span><span class="sxs-lookup"><span data-stu-id="01f96-403">hello countdistinct function counts hello number of distinct values within each group.</span></span> <span data-ttu-id="01f96-404">Örneğin, olabilir toocount hello raporlama her türü için benzersiz bilgisayar sayısı kullanılır:</span><span class="sxs-lookup"><span data-stu-id="01f96-404">For example, it could be used toocount hello number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a><span data-ttu-id="01f96-406">Merhaba ölçü aralığı komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-406">Use hello measure interval command</span></span>
<span data-ttu-id="01f96-407">İle gerçek zamanlı performans verileri toplama toplayabilir ve herhangi bir performans sayacı günlük analizi, görselleştirme.</span><span class="sxs-lookup"><span data-stu-id="01f96-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="01f96-408">Yalnızca girme hello sorgu **türü: Perf** sayaçları ve günlük analizi ortamınızdaki sunucularının hello sayısına dayalı olarak ölçüm grafikleri binlerce döndürür.</span><span class="sxs-lookup"><span data-stu-id="01f96-408">Simply entering hello query **Type:Perf** will return thousands of metric graphs based on hello number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="01f96-409">İsteğe bağlı ölçüm toplama ile Merhaba bakabilirsiniz genel ölçümleri ortamınızda bir yüksek düzeyde ve gerektiği gibi daha ayrıntılı veri derin Dalış.</span><span class="sxs-lookup"><span data-stu-id="01f96-409">With on-demand metric aggregation, you can look at hello overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="01f96-410">Tooknow tüm bilgisayarlar arasında hello ortalama CPU nedir istediğinizi düşünelim.</span><span class="sxs-lookup"><span data-stu-id="01f96-410">Let’s say that you want tooknow what is hello average CPU across all your computers.</span></span> <span data-ttu-id="01f96-411">Sonuçları düzeltilmesini çünkü her bilgisayar için ortalama CPU hello bakarak faydalı olmayabilir. toolook daha fazla ayrıntı içine, Sonuç kümenizi daha küçük birer penceresi öbekleri ve görünüm bir zaman serisinin arasında farklı boyutları toplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-411">Looking at hello average CPU for every computer might not be helpful because results may get smoothed out. toolook into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="01f96-412">Örneğin, hello saatlik CPU kullanımı ortalaması tüm bilgisayarlar arasında şu şekilde gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="01f96-412">For example, you can perform hello hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![Ölçü ortalama aralığı](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="01f96-414">Varsayılan olarak bu sonuçları çok serisi etkileşimli satırı grafik görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="01f96-414">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="01f96-415">Bu grafik serisi (y ekseni rescaling ile), yakınlaştırma ve vurgulama geçiş destekler.</span><span class="sxs-lookup"><span data-stu-id="01f96-415">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="01f96-416">Merhaba tablo görüntüleme seçeneği gerekirse hello ham verileri görüntülemek için kullanılabilir durumda kalır.</span><span class="sxs-lookup"><span data-stu-id="01f96-416">hello table display option is still available for viewing hello raw data if necessary.</span></span>

<span data-ttu-id="01f96-417">Diğer alanlara göre de gruplandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-417">You can also group by other fields.</span></span> <span data-ttu-id="01f96-418">Bu örnekte, belirli bir bilgisayar için tüm hello % sayaçları adresindeki arayan ve her sayacın hello saatlik 70 yüzdebirlik değeri nedir tooknow istiyorum:</span><span class="sxs-lookup"><span data-stu-id="01f96-418">In this example, I am looking at all hello % counters for one specific computer, and I want tooknow what is hello hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="01f96-419">Bir şey toonote bu sorgular değil sınırlı tooperformance sayaçları olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="01f96-419">One thing toonote is that these queries are not limited tooperformance counters.</span></span> <span data-ttu-id="01f96-420">Bunları tooany ölçüm uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-420">You can apply them tooany metric.</span></span> <span data-ttu-id="01f96-421">Bu örnekte, ı W3C IIS günlüklerine arayan.</span><span class="sxs-lookup"><span data-stu-id="01f96-421">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="01f96-422">Her isteği işlemek için bir 5 dakikalık aralık boyunca sürer hello en uzun süre nedir tooknow istiyorum:</span><span class="sxs-lookup"><span data-stu-id="01f96-422">I want tooknow what is hello maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="01f96-423">Tek bir sorguda birden çok toplamalar kullanın</span><span class="sxs-lookup"><span data-stu-id="01f96-423">Use multiple aggregates in one query</span></span>
<span data-ttu-id="01f96-424">Birden çok toplama yan tümcesi bir ölçü komutta belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f96-424">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="01f96-425">Her biri bağımsız olarak diğer adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="01f96-425">Each one can be aliased independently.</span></span>  <span data-ttu-id="01f96-426">Bir diğer ad hello kaynaklanan verilmemişse alan adı kullanıldı hello toplama işlevi olur (yani, avg(CounterValue)) için "avg(CounterValue)".</span><span class="sxs-lookup"><span data-stu-id="01f96-426">If it is not given an alias hello resulting field name will be hello aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="01f96-428">Bir örnek daha:</span><span class="sxs-lookup"><span data-stu-id="01f96-428">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="01f96-429">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="01f96-429">Next steps</span></span>
<span data-ttu-id="01f96-430">Günlük aramaları hakkında ek bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="01f96-430">For additional information about log searches, see:</span></span>

* <span data-ttu-id="01f96-431">Kullanım [günlük analizi özel alanları](log-analytics-custom-fields.md) tooextend günlük arar.</span><span class="sxs-lookup"><span data-stu-id="01f96-431">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
* <span data-ttu-id="01f96-432">Gözden geçirme hello [günlük analizi oturum Arama başvurusu](log-analytics-search-reference.md) tooview tüm hello arama alanları ve modelleri günlük analizi içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="01f96-432">Review hello [Log Analytics log search reference](log-analytics-search-reference.md) tooview all of hello search fields and facets available in Log Analytics.</span></span>

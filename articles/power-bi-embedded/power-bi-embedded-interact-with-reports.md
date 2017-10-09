---
title: Merhaba JavaScript API kullanarak raporlarla aaaInteract | Microsoft Docs
description: "Power BI Embedded, hello JavaScript API kullanarak raporlarla etkileşim"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a><span data-ttu-id="aebc6-103">Merhaba JavaScript API kullanarak Power BI raporları ile etkileşim</span><span class="sxs-lookup"><span data-stu-id="aebc6-103">Interact with Power BI reports using hello JavaScript API</span></span>
<span data-ttu-id="aebc6-104">tooeasily katıştırmak Power BI raporları uygulamalarınıza hello Power BI JavaScript API sağlar.</span><span class="sxs-lookup"><span data-stu-id="aebc6-104">hello Power BI JavaScript API enables you tooeasily embed Power BI reports into your applications.</span></span> <span data-ttu-id="aebc6-105">Merhaba API uygulamalarınızı programlı olarak farklı rapor öğeleri sayfa ve filtreleri gibi etkileşim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aebc6-105">With hello API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="aebc6-106">Bu etkileşim Power BI raporlarını uygulamanızın daha tümleşik bir parçası yapar.</span><span class="sxs-lookup"><span data-stu-id="aebc6-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="aebc6-107">Uygulamanızda barındırılan IFRAME Merhaba uygulaması bir parçası olarak kullanarak bir Power BI raporu ekleme.</span><span class="sxs-lookup"><span data-stu-id="aebc6-107">You embed a Power BI report in your application by using an iframe that is hosted as part of hello application.</span></span> <span data-ttu-id="aebc6-108">Görüntü aşağıdaki hello görebileceğiniz gibi hello IFRAME uygulama ve hello rapor arasında sınırı görevi görür.</span><span class="sxs-lookup"><span data-stu-id="aebc6-108">hello iframe acts as a boundary between your application and hello report, as you can see in hello following image.</span></span> 

![Javascript API’si olmadan Power BI embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="aebc6-110">işlem çok daha kolay katıştırma hello Hello IFRAME yapar, ancak hello JavaScript API hello rapor ve uygulamanızı birbirleriyle etkileşime giremezler.</span><span class="sxs-lookup"><span data-stu-id="aebc6-110">hello iframe makes hello embedding process a lot easier, but without hello JavaScript API hello report and your application can't interact with each other.</span></span> <span data-ttu-id="aebc6-111">Bu etkileşimi eksikliği bunu hello rapor gerçekten hello uygulamanın parçası değil gibi eşitleyerek duruma getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aebc6-111">This lack of interaction can make it feel like hello report is not really part of hello application.</span></span> <span data-ttu-id="aebc6-112">gerçekten Hello rapor ve uygulama İleri ve geri toocommunicate görüntü aşağıdaki hello olduğu gibi gerekir.</span><span class="sxs-lookup"><span data-stu-id="aebc6-112">hello report and application really need toocommunicate back and forth, as in hello following image.</span></span>

![Javascript API’si ile Power BI embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="aebc6-114">Merhaba Power BI JavaScript API hello IFRAME sınır güvenli bir şekilde geçirebilir toowrite kod etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="aebc6-114">hello Power BI JavaScript API enables you toowrite code that can securely pass through hello iframe boundary.</span></span> <span data-ttu-id="aebc6-115">Bu etkinleştirir, uygulama tooprogrammatically bir eylemi gerçekleştirir bir rapor ve kullanıcıların hello rapor içinde açmak eylemlerine olayları için toolisten.</span><span class="sxs-lookup"><span data-stu-id="aebc6-115">This enables your application tooprogrammatically perform an action in a report, and toolisten for events from actions that users make within hello report.</span></span>

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a><span data-ttu-id="aebc6-116">Power BI JavaScript API hello ile neler yapabileceğiniz?</span><span class="sxs-lookup"><span data-stu-id="aebc6-116">What can you do with hello Power BI JavaScript API?</span></span>
<span data-ttu-id="aebc6-117">Merhaba JavaScript API ile raporlarını yönetme, bir raporda toopages gidin, bir raporu filtreleme ve olayları katıştırma işlemek.</span><span class="sxs-lookup"><span data-stu-id="aebc6-117">With hello JavaScript API you can manage reports, navigate toopages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="aebc6-118">Merhaba Aşağıdaki diyagramda hello API hello yapısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="aebc6-118">hello following diagram shows hello structure of hello API.</span></span>

![Power BI JavaScript API’si diyagramı](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="aebc6-120">Raporları yönetme</span><span class="sxs-lookup"><span data-stu-id="aebc6-120">Manage reports</span></span>
<span data-ttu-id="aebc6-121">Merhaba Javascript API hello rapor ve sayfa düzeyinde toomanage davranışı etkinleştirir:</span><span class="sxs-lookup"><span data-stu-id="aebc6-121">hello Javascript API enables you toomanage behavior at hello report and page level:</span></span>

* <span data-ttu-id="aebc6-122">Belirli bir Power BI rapor uygulamanızda güvenli bir şekilde ekleme - hello deneyin [demo uygulama ekleme](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="aebc6-122">Embed a specific Power BI Report securely in your application - try hello [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="aebc6-123">Erişim belirteci ayarlama</span><span class="sxs-lookup"><span data-stu-id="aebc6-123">Set access token</span></span>
* <span data-ttu-id="aebc6-124">Merhaba rapor yapılandırın</span><span class="sxs-lookup"><span data-stu-id="aebc6-124">Configure hello report</span></span>
  * <span data-ttu-id="aebc6-125">Etkinleştirme ve hello filtre bölmesi ve sayfa gezinti bölmesinde devre dışı bırak - hello deneyin [güncelleştirme ayarları demo uygulaması](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="aebc6-125">Enable and disable hello filter pane and page navigation pane - try hello [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="aebc6-126">Sayfalar ve filtreleri için varsayılan değerleri ayarlamak - hello deneyin [kümesi Varsayılanları Tanıtımı](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="aebc6-126">Set defaults for pages and filters - try hello [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="aebc6-127">Tam ekran moduna giriş ve çıkış</span><span class="sxs-lookup"><span data-stu-id="aebc6-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="aebc6-128">Bir raporu ekleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="aebc6-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a><span data-ttu-id="aebc6-129">Bir rapordaki toopages gidin</span><span class="sxs-lookup"><span data-stu-id="aebc6-129">Navigate toopages in a report</span></span>
<span data-ttu-id="aebc6-130">Merhaba JavaScript API enbales bir rapor ve tooset hello geçerli sayfada, toodiscover tüm sayfaları.</span><span class="sxs-lookup"><span data-stu-id="aebc6-130">hello JavaScript API enbales you toodiscover all pages in a report and tooset hello current page.</span></span> <span data-ttu-id="aebc6-131">Merhaba deneyin [Gezinti demo uygulaması](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="aebc6-131">Try hello [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="aebc6-132">Sayfa gezintisi hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="aebc6-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="aebc6-133">Bir raporu filtreleme</span><span class="sxs-lookup"><span data-stu-id="aebc6-133">Filter a report</span></span>
<span data-ttu-id="aebc6-134">Merhaba JavaScript API temel ve Gelişmiş filtreleme katıştırılmış raporlar ve rapor sayfaları için özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="aebc6-134">hello JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="aebc6-135">Merhaba deneyin [demo uygulama filtreleme](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), bazı tanıtım kodu buraya gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="aebc6-135">Try hello [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="aebc6-136">Temel filtreler</span><span class="sxs-lookup"><span data-stu-id="aebc6-136">Basic filters</span></span>
<span data-ttu-id="aebc6-137">Temel bir filtre bir sütun veya hiyerarşi düzeyi yerleştirilir ve değerleri tooinclude veya hariç tutma listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="aebc6-137">A basic filter is placed on a column or hierarchy level and contains a list of values tooinclude or exclude.</span></span>

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a><span data-ttu-id="aebc6-138">Gelişmiş filtreler</span><span class="sxs-lookup"><span data-stu-id="aebc6-138">Advanced filters</span></span>
<span data-ttu-id="aebc6-139">Gelişmiş filtreleri kullanma hello mantıksal işleci veya OR ve her biri kendi işleç ve değer bir veya iki koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="aebc6-139">Advanced filters use hello logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="aebc6-140">Desteklenen koşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aebc6-140">Supported conditions are:</span></span>

* <span data-ttu-id="aebc6-141">None</span><span class="sxs-lookup"><span data-stu-id="aebc6-141">None</span></span>
* <span data-ttu-id="aebc6-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="aebc6-142">LessThan</span></span>
* <span data-ttu-id="aebc6-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="aebc6-143">LessThanOrEqual</span></span>
* <span data-ttu-id="aebc6-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="aebc6-144">GreaterThan</span></span>
* <span data-ttu-id="aebc6-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="aebc6-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="aebc6-146">Contains</span><span class="sxs-lookup"><span data-stu-id="aebc6-146">Contains</span></span>
* <span data-ttu-id="aebc6-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="aebc6-147">DoesNotContain</span></span>
* <span data-ttu-id="aebc6-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="aebc6-148">StartsWith</span></span>
* <span data-ttu-id="aebc6-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="aebc6-149">DoesNotStartWith</span></span>
* <span data-ttu-id="aebc6-150">Is</span><span class="sxs-lookup"><span data-stu-id="aebc6-150">Is</span></span>
* <span data-ttu-id="aebc6-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="aebc6-151">IsNot</span></span>
* <span data-ttu-id="aebc6-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="aebc6-152">IsBlank</span></span>
* <span data-ttu-id="aebc6-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="aebc6-153">IsNotBlank</span></span>

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[<span data-ttu-id="aebc6-154">Filtreleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="aebc6-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="aebc6-155">Olayları işleme</span><span class="sxs-lookup"><span data-stu-id="aebc6-155">Handling events</span></span>
<span data-ttu-id="aebc6-156">Ayrıca hello IFRAME toosending bilgileri, uygulamanız da hello IFRAME gelen olayların aşağıdaki hello hakkında bilgi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aebc6-156">In addition toosending information into hello iframe, your application can also receive information on hello following events coming from hello iframe:</span></span>

* <span data-ttu-id="aebc6-157">Embed</span><span class="sxs-lookup"><span data-stu-id="aebc6-157">Embed</span></span>
  * <span data-ttu-id="aebc6-158">loaded</span><span class="sxs-lookup"><span data-stu-id="aebc6-158">loaded</span></span>
  * <span data-ttu-id="aebc6-159">error</span><span class="sxs-lookup"><span data-stu-id="aebc6-159">error</span></span>
* <span data-ttu-id="aebc6-160">Reports</span><span class="sxs-lookup"><span data-stu-id="aebc6-160">Reports</span></span>
  * <span data-ttu-id="aebc6-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="aebc6-161">pageChanged</span></span>
  * <span data-ttu-id="aebc6-162">dataSelected (yakında)</span><span class="sxs-lookup"><span data-stu-id="aebc6-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="aebc6-163">Olayları işleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="aebc6-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="aebc6-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aebc6-164">Next steps</span></span>
<span data-ttu-id="aebc6-165">Merhaba Power BI JavaScript API hakkında daha fazla bilgi için bağlantılar aşağıdaki hello denetleyin:</span><span class="sxs-lookup"><span data-stu-id="aebc6-165">For more information about hello Power BI JavaScript API, check out hello following links:</span></span>

* [<span data-ttu-id="aebc6-166">JavaScript API’si Wiki</span><span class="sxs-lookup"><span data-stu-id="aebc6-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="aebc6-167">Nesne modeli başvurusu</span><span class="sxs-lookup"><span data-stu-id="aebc6-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="aebc6-168">Örnekler</span><span class="sxs-lookup"><span data-stu-id="aebc6-168">Samples</span></span>
  * [<span data-ttu-id="aebc6-169">Angular</span><span class="sxs-lookup"><span data-stu-id="aebc6-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="aebc6-170">Ember</span><span class="sxs-lookup"><span data-stu-id="aebc6-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="aebc6-171">Canlı tanıtım</span><span class="sxs-lookup"><span data-stu-id="aebc6-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)


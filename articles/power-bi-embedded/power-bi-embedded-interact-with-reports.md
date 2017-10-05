---
title: "JavaScript API’sini kullanarak raporlarla etkileşim kurma | Microsoft Belgeleri"
description: "Power BI Embedded, JavaScript API’si kullanarak raporlarla etkileşim kurma"
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
ms.openlocfilehash: 500462ac835674d80650c02aa7fc629b4a975857
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="interact-with-power-bi-reports-using-the-javascript-api"></a><span data-ttu-id="79719-103">JavaScript API’sini kullanarak Power BI raporlarıyla etkileşim kurma</span><span class="sxs-lookup"><span data-stu-id="79719-103">Interact with Power BI reports using the JavaScript API</span></span>
<span data-ttu-id="79719-104">Power BI JavaScript API’si, Power BI raporlarını uygulamalarınıza kolaylıkla eklemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="79719-104">The Power BI JavaScript API enables you to easily embed Power BI reports into your applications.</span></span> <span data-ttu-id="79719-105">API ile uygulamalarınız sayfalar ve filtreler gibi farklı rapor öğeleri ile program aracılığıyla etkileşim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="79719-105">With the API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="79719-106">Bu etkileşim Power BI raporlarını uygulamanızın daha tümleşik bir parçası yapar.</span><span class="sxs-lookup"><span data-stu-id="79719-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="79719-107">Uygulamanızın bir parçası olarak barındırılacak Power BI raporunu uygulamaya iframe kullanarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="79719-107">You embed a Power BI report in your application by using an iframe that is hosted as part of the application.</span></span> <span data-ttu-id="79719-108">Aşağıdaki görüntüde görebileceğiniz gibi bu iframe uygulamanızla rapor arasında sınır işlevi görür.</span><span class="sxs-lookup"><span data-stu-id="79719-108">The iframe acts as a boundary between your application and the report, as you can see in the following image.</span></span> 

![Javascript API’si olmadan Power BI embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="79719-110">iframe katıştırma işlemini çok daha kolaylaştırır, ancak JavaScript API’si olmadan rapor ve uygulamanız birbiriyle etkileşim kuramaz.</span><span class="sxs-lookup"><span data-stu-id="79719-110">The iframe makes the embedding process a lot easier, but without the JavaScript API the report and your application can't interact with each other.</span></span> <span data-ttu-id="79719-111">Bu etkileşimin kurulamaması raporun uygulamanızın bir parçası değilmiş gibi görünmesine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="79719-111">This lack of interaction can make it feel like the report is not really part of the application.</span></span> <span data-ttu-id="79719-112">Rapor ve uygulama aşağıdaki görüntüde olduğu gibi çift yönlü bir iletişim kurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="79719-112">The report and application really need to communicate back and forth, as in the following image.</span></span>

![Javascript API’si ile Power BI embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="79719-114">Power BI JavaScript API’si iframe sınırından güvenli bir şekilde geçebilecek bir kod yazmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="79719-114">The Power BI JavaScript API enables you to write code that can securely pass through the iframe boundary.</span></span> <span data-ttu-id="79719-115">Bunun yapılması uygulamanızın bir raporda program aracılığıyla eylem gerçekleştirmesini ve kullanıcıların rapor içinde gerçekleştirdiği eylemlerdeki olayları dinlemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="79719-115">This enables your application to programmatically perform an action in a report, and to listen for events from actions that users make within the report.</span></span>

## <a name="what-can-you-do-with-the-power-bi-javascript-api"></a><span data-ttu-id="79719-116">Power BI JavaScript API’si ile neler yapabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="79719-116">What can you do with the Power BI JavaScript API?</span></span>
<span data-ttu-id="79719-117">JavaScript API’si ile raporları yönetebilir, bir rapordaki sayfalarda gezinebilir, raporu filtreleyebilir ve katıştırma olaylarını gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79719-117">With the JavaScript API you can manage reports, navigate to pages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="79719-118">Aşağıdaki diyagramda API’nin yapısı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="79719-118">The following diagram shows the structure of the API.</span></span>

![Power BI JavaScript API’si diyagramı](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="79719-120">Raporları yönetme</span><span class="sxs-lookup"><span data-stu-id="79719-120">Manage reports</span></span>
<span data-ttu-id="79719-121">Javascript API’si rapor ve sayfa düzeyindeki davranışı yönetmenizi sağlar:</span><span class="sxs-lookup"><span data-stu-id="79719-121">The Javascript API enables you to manage behavior at the report and page level:</span></span>

* <span data-ttu-id="79719-122">Belirli bir Power BI Raporunu uygulamanıza güvenli bir şekilde katıştırma - [katıştırma demo uygulamasını](http://azure-samples.github.io/powerbi-angular-client/#/scenario1) deneyin</span><span class="sxs-lookup"><span data-stu-id="79719-122">Embed a specific Power BI Report securely in your application - try the [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="79719-123">Erişim belirteci ayarlama</span><span class="sxs-lookup"><span data-stu-id="79719-123">Set access token</span></span>
* <span data-ttu-id="79719-124">Raporu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="79719-124">Configure the report</span></span>
  * <span data-ttu-id="79719-125">Filtre bölmesini ve sayfa gezinti bölmesini etkinleştirme ve devre dışı bırakma - [ayar güncelleştirme demo uygulamasını](http://azure-samples.github.io/powerbi-angular-client/#/scenario6) deneyin</span><span class="sxs-lookup"><span data-stu-id="79719-125">Enable and disable the filter pane and page navigation pane - try the [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="79719-126">Sayfalar ve filtreler için varsayılanları ayarlama - [varsayılanları ayarlama demosunu](http://azure-samples.github.io/powerbi-angular-client/#/scenario5) deneyin</span><span class="sxs-lookup"><span data-stu-id="79719-126">Set defaults for pages and filters - try the [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="79719-127">Tam ekran moduna giriş ve çıkış</span><span class="sxs-lookup"><span data-stu-id="79719-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="79719-128">Bir raporu ekleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="79719-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-to-pages-in-a-report"></a><span data-ttu-id="79719-129">Rapordaki sayfalarda gezinme</span><span class="sxs-lookup"><span data-stu-id="79719-129">Navigate to pages in a report</span></span>
<span data-ttu-id="79719-130">JavaScript API’si bir rapordaki tüm sayfaları bulmanızı ve geçerli sayfayı ayarlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="79719-130">The JavaScript API enbales you to discover all pages in a report and to set the current page.</span></span> <span data-ttu-id="79719-131">[Gezinti demo uygulamasını](http://azure-samples.github.io/powerbi-angular-client/#/scenario3) deneyin.</span><span class="sxs-lookup"><span data-stu-id="79719-131">Try the [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="79719-132">Sayfa gezintisi hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="79719-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="79719-133">Bir raporu filtreleme</span><span class="sxs-lookup"><span data-stu-id="79719-133">Filter a report</span></span>
<span data-ttu-id="79719-134">JavaScript API’si katıştırılmış raporlar ve rapor sayfaları için temel ve gelişmiş filtreleme özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="79719-134">The JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="79719-135">[Filtreleme demo uygulamasını](http://azure-samples.github.io/powerbi-angular-client/#/scenario4) deneyin ve giriş niteliğindeki bazı kodları burada gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="79719-135">Try the [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="79719-136">Temel filtreler</span><span class="sxs-lookup"><span data-stu-id="79719-136">Basic filters</span></span>
<span data-ttu-id="79719-137">Temel filtre bir sütuna veya hiyerarşi düzeyine yerleştirilir ve dahil edilecek ya da hariç tutulacak değerler listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="79719-137">A basic filter is placed on a column or hierarchy level and contains a list of values to include or exclude.</span></span>

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


#### <a name="advanced-filters"></a><span data-ttu-id="79719-138">Gelişmiş filtreler</span><span class="sxs-lookup"><span data-stu-id="79719-138">Advanced filters</span></span>
<span data-ttu-id="79719-139">Gelişmiş filtreler AND veya OR mantıksal işlecini kullanır ve her biri kendi işlecine ve değerine sahip bir ya da iki koşulu kabul eder.</span><span class="sxs-lookup"><span data-stu-id="79719-139">Advanced filters use the logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="79719-140">Desteklenen koşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="79719-140">Supported conditions are:</span></span>

* <span data-ttu-id="79719-141">None</span><span class="sxs-lookup"><span data-stu-id="79719-141">None</span></span>
* <span data-ttu-id="79719-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="79719-142">LessThan</span></span>
* <span data-ttu-id="79719-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="79719-143">LessThanOrEqual</span></span>
* <span data-ttu-id="79719-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="79719-144">GreaterThan</span></span>
* <span data-ttu-id="79719-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="79719-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="79719-146">Contains</span><span class="sxs-lookup"><span data-stu-id="79719-146">Contains</span></span>
* <span data-ttu-id="79719-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="79719-147">DoesNotContain</span></span>
* <span data-ttu-id="79719-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="79719-148">StartsWith</span></span>
* <span data-ttu-id="79719-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="79719-149">DoesNotStartWith</span></span>
* <span data-ttu-id="79719-150">Is</span><span class="sxs-lookup"><span data-stu-id="79719-150">Is</span></span>
* <span data-ttu-id="79719-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="79719-151">IsNot</span></span>
* <span data-ttu-id="79719-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="79719-152">IsBlank</span></span>
* <span data-ttu-id="79719-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="79719-153">IsNotBlank</span></span>

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
[<span data-ttu-id="79719-154">Filtreleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="79719-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="79719-155">Olayları işleme</span><span class="sxs-lookup"><span data-stu-id="79719-155">Handling events</span></span>
<span data-ttu-id="79719-156">iframe’e bilgi göndermeye ek olarak uygulamanız iframe’den gelen aşağıdaki olaylara ilişkin bilgi de alabilir:</span><span class="sxs-lookup"><span data-stu-id="79719-156">In addition to sending information into the iframe, your application can also receive information on the following events coming from the iframe:</span></span>

* <span data-ttu-id="79719-157">Embed</span><span class="sxs-lookup"><span data-stu-id="79719-157">Embed</span></span>
  * <span data-ttu-id="79719-158">loaded</span><span class="sxs-lookup"><span data-stu-id="79719-158">loaded</span></span>
  * <span data-ttu-id="79719-159">error</span><span class="sxs-lookup"><span data-stu-id="79719-159">error</span></span>
* <span data-ttu-id="79719-160">Reports</span><span class="sxs-lookup"><span data-stu-id="79719-160">Reports</span></span>
  * <span data-ttu-id="79719-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="79719-161">pageChanged</span></span>
  * <span data-ttu-id="79719-162">dataSelected (yakında)</span><span class="sxs-lookup"><span data-stu-id="79719-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="79719-163">Olayları işleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="79719-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="79719-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="79719-164">Next steps</span></span>
<span data-ttu-id="79719-165">Power BI JavaScript API’si hakkında daha fazla bilgi için aşağıdaki bağlantılara göz atın:</span><span class="sxs-lookup"><span data-stu-id="79719-165">For more information about the Power BI JavaScript API, check out the following links:</span></span>

* [<span data-ttu-id="79719-166">JavaScript API’si Wiki</span><span class="sxs-lookup"><span data-stu-id="79719-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="79719-167">Nesne modeli başvurusu</span><span class="sxs-lookup"><span data-stu-id="79719-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="79719-168">Örnekler</span><span class="sxs-lookup"><span data-stu-id="79719-168">Samples</span></span>
  * [<span data-ttu-id="79719-169">Angular</span><span class="sxs-lookup"><span data-stu-id="79719-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="79719-170">Ember</span><span class="sxs-lookup"><span data-stu-id="79719-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="79719-171">Canlı tanıtım</span><span class="sxs-lookup"><span data-stu-id="79719-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)


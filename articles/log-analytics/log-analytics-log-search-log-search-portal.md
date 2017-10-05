---
title: "Azure günlük analizi günlük arama Portalı'nı kullanarak | Microsoft Docs"
description: "Bu makalede günlük aramalar oluşturun ve günlük arama Portalı'nı kullanarak günlük analizi çalışma alanınızda depolanan verileri çözümleyen açıklar bir öğretici içerir.  Öğretici, farklı türdeki veri ve analiz etme sonuçları döndürmek için bazı basit sorgu çalıştırmayı içerir."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 6fc556ceb34cde26d5f3789a2397cdaa34b0b84d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-the-log-search-portal"></a><span data-ttu-id="059b4-104">Günlük arama Portalı'nı kullanarak Azure günlük analizi günlük aramalar oluşturun</span><span class="sxs-lookup"><span data-stu-id="059b4-104">Create log searches in Azure Log Analytics using the Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="059b4-105">Bu makalede Azure günlük analizi yeni sorgu dili kullanarak günlük arama portalında açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="059b4-105">This article describes the Log Search portal in Azure Log Analytics using the new query language.</span></span>  <span data-ttu-id="059b4-106">Yeni dil hakkında daha fazla bilgi ve çalışma alanı yükseltme yordamı elde [Azure günlük analizi çalışma alanınız için yeni günlük arama yükseltme](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="059b4-106">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="059b4-107">Çalışma alanınızı yeni sorgu dili yükseltilmedi, için başvurmalıdır [Bul günlük aramaları günlük analizi kullanarak verileri](log-analytics-log-searches.md) günlük arama Portalı'nın geçerli sürümü hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="059b4-107">If your workspace hasn't been upgraded to the new query language, you should refer to [Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on the current version of the Log Search portal.</span></span>

<span data-ttu-id="059b4-108">Bu makalede günlük aramalar oluşturun ve günlük arama Portalı'nı kullanarak günlük analizi çalışma alanınızda depolanan verileri çözümleyen açıklar bir öğretici içerir.</span><span class="sxs-lookup"><span data-stu-id="059b4-108">This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics workspace using the Log Search portal.</span></span>  <span data-ttu-id="059b4-109">Öğretici, farklı türdeki veri ve analiz etme sonuçları döndürmek için bazı basit sorgu çalıştırmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="059b4-109">The tutorial includes running some simple queries to return different types of data and analyzing results.</span></span>  <span data-ttu-id="059b4-110">Doğrudan değiştirmek yerine sorgu değiştirmek için günlük arama portal özelliklerinde odaklanır.</span><span class="sxs-lookup"><span data-stu-id="059b4-110">It focuses on features in the Log Search portal for modifying the query rather than modifying it directly.</span></span>  <span data-ttu-id="059b4-111">Doğrudan sorgu düzenleme hakkında daha fazla bilgi için bkz: [sorgu dili başvurusu](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="059b4-111">For details on directly editing the query, see the [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="059b4-112">Günlük arama portalı yerine Advanced Analytics portalında aramaları oluşturmak için bkz [Analytics portalı ile çalışmaya başlama](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="059b4-112">To create searches in the Advanced Analytics portal instead of the Log Search portal, see [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="059b4-113">Her iki portalları aynı sorgu dili günlük analizi çalışma alanındaki aynı verilere erişmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="059b4-113">Both portals use the same query language to access the same data in the Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="059b4-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="059b4-114">Prerequisites</span></span>
<span data-ttu-id="059b4-115">Bu öğretici, bir günlük analizi çalışma alanı çözümlemek için sorgular için veri üretir en az bir bağlı kaynağıyla zaten sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="059b4-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for the queries to analyze.</span></span>  

- <span data-ttu-id="059b4-116">Bir çalışma alanı yoksa, en yordamı kullanarak boş bir tane oluşturabilirsiniz [günlük analizi çalışma alanı ile çalışmaya başlama](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="059b4-116">If you don't have a workspace, you can create a free one using the procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="059b4-117">En az bir bağlanma [Windows Aracısı](log-analytics-windows-agents.md) veya bir [Linux Aracısı](log-analytics-linux-agents.md) çalışma alanı.</span><span class="sxs-lookup"><span data-stu-id="059b4-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) to the workspace.</span></span>  

## <a name="open-the-log-search-portal"></a><span data-ttu-id="059b4-118">Günlük arama portalını açın</span><span class="sxs-lookup"><span data-stu-id="059b4-118">Open the Log Search portal</span></span>
<span data-ttu-id="059b4-119">Günlük arama Portalı'nı açarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="059b4-119">Start by opening the Log Search portal.</span></span>  <span data-ttu-id="059b4-120">Azure portal veya OMS portalı erişebilir.</span><span class="sxs-lookup"><span data-stu-id="059b4-120">You can access it in either the Azure portal or the OMS portal.</span></span>

1. <span data-ttu-id="059b4-121">Azure Portalı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="059b4-121">Open the Azure portal.</span></span>
2. <span data-ttu-id="059b4-122">Günlük analizi gidin ve çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="059b4-122">Navigate to Log Analytics and select your workspace.</span></span>
3. <span data-ttu-id="059b4-123">Her iki select **günlük arama** Azure portalında kalın veya seçerek OMS Portalı'nı başlatmak için **OMS portalı** ve günlük arama düğmesini tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="059b4-123">Either select **Log Search** to stay in the Azure portal or launch the OMS portal by selecting **OMS Portal** and then clicking the Log Search button.</span></span>

![Günlük Ara düğmesi](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="059b4-125">Basit Arama oluşturma</span><span class="sxs-lookup"><span data-stu-id="059b4-125">Create a simple search</span></span>
<span data-ttu-id="059b4-126">Tablodaki tüm kayıtları döndürür basit bir sorgu çalışmak için bazı veri almak için en hızlı yoludur.</span><span class="sxs-lookup"><span data-stu-id="059b4-126">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="059b4-127">Varsa tüm Windows veya Linux istemcileri, çalışma alanına bağlı sonra verileri olay (Windows) veya Syslog (Linux) tablosu sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="059b4-127">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="059b4-128">Aşağıdaki sorgularda arama kutusuna yazın ve arama düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="059b4-128">Type one the following queries in the search box and click the search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="059b4-129">Varsayılan liste görünümünde veriler döndürülür ve kaç tane toplam kaydı döndürülmedi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="059b4-129">Data is returned in the default list view, and you can see how many total records were returned.</span></span>

![Basit Sorgu](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="059b4-131">Her kayıt yalnızca ilk birkaç özellikleri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="059b4-131">Only the first few properties of each record are displayed.</span></span>  <span data-ttu-id="059b4-132">Tıklatın **daha fazla Göster** belirli bir kaydın tüm özelliklerini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="059b4-132">Click **show more** to display all properties for a particular record.</span></span>

![Kayıt ayrıntıları](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-the-time-scope"></a><span data-ttu-id="059b4-134">Zaman kapsamını Ayarla</span><span class="sxs-lookup"><span data-stu-id="059b4-134">Set the time scope</span></span>
<span data-ttu-id="059b4-135">Günlük analizi tarafından toplanan her kaydına sahip bir **TimeGenerated** kaydın oluşturulduğu saat ve tarihi içeren özelliği.</span><span class="sxs-lookup"><span data-stu-id="059b4-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains the date and time that the record was created.</span></span>  <span data-ttu-id="059b4-136">Günlük arama portal sorguda yalnızca kayıtlarıyla döndüren bir **TimeGenerated** zaman kapsamdaki ekranın sol tarafında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="059b4-136">A query in the Log Search portal only returns records with a **TimeGenerated** within the time scope that's displayed on the left side of the screen.</span></span>  

<span data-ttu-id="059b4-137">Zaman filtresi açılır seçerek veya kaydırıcıyı değiştirerek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="059b4-137">You can change the time filter either by selecting the dropdown or by modifying the slider.</span></span>  <span data-ttu-id="059b4-138">Kaydırıcı her zaman diliminin aralıkta kayıtlarını göreli sayısını gösteren bir çubuk grafiği görüntüler.</span><span class="sxs-lookup"><span data-stu-id="059b4-138">The slider displays a bar graph that shows the relative number of records for each time segment within the range.</span></span>  <span data-ttu-id="059b4-139">Bu kesimin aralığın bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="059b4-139">This segment will vary depending on the range.</span></span>

<span data-ttu-id="059b4-140">Varsayılan süre kapsamı **1 gün**.</span><span class="sxs-lookup"><span data-stu-id="059b4-140">The default time scope is **1 day**.</span></span>  <span data-ttu-id="059b4-141">Bu değeri değiştirmek **7 gün**, ve kayıtların toplam sayısını artırmalısınız.</span><span class="sxs-lookup"><span data-stu-id="059b4-141">Change this value to **7 days**, and the total number of records should increase.</span></span>

![Tarih saat kapsamı](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-the-query"></a><span data-ttu-id="059b4-143">Filtre sorgusunun sonuçları</span><span class="sxs-lookup"><span data-stu-id="059b4-143">Filter results of the query</span></span>
<span data-ttu-id="059b4-144">Ekranın sol tarafındaki filtreleme için sorgu doğrudan değiştirmeden eklemenize olanak sağlayan Filtre Bölmesi ' dir.</span><span class="sxs-lookup"><span data-stu-id="059b4-144">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span></span>  <span data-ttu-id="059b4-145">Döndürülen kayıtları birkaç özelliklerini ilk on değerleriyle kendi kayıt sayısı ile birlikte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="059b4-145">Several properties of the records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="059b4-146">İle çalışıyorsanız **olay**, yanındaki onay kutusunu işaretleyin **hata** altında **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="059b4-146">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="059b4-147">İle çalışıyorsanız **Syslog**, yanındaki onay kutusunu işaretleyin **hata** altında **önem düzeyi**.</span><span class="sxs-lookup"><span data-stu-id="059b4-147">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="059b4-148">Bu, sorgu sonuçları hata olayları sınırlandırmak için aşağıdakilerden birine değiştirir.</span><span class="sxs-lookup"><span data-stu-id="059b4-148">This changes the query to one of the following to limit the results to error events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtre](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="059b4-150">Özellikler Filtre bölmesini seçerek eklemek **için Filtre Ekle** menüsünden özelliği kayıtları biri.</span><span class="sxs-lookup"><span data-stu-id="059b4-150">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span></span>

![Filtre menü ekleme](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="059b4-152">Seçerek, aynı filtre ayarlayabilirsiniz **filtre** filtrelemek istediğiniz değer içeren bir kayıt özelliği menüsünden.</span><span class="sxs-lookup"><span data-stu-id="059b4-152">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span></span>  

<span data-ttu-id="059b4-153">Yalnızca **filtre** adlarının mavi olan özellikleri seçeneği.</span><span class="sxs-lookup"><span data-stu-id="059b4-153">You only have the **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="059b4-154">Bunlar *aranabilir* için dizin alanları arama koşulları.</span><span class="sxs-lookup"><span data-stu-id="059b4-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="059b4-155">Gri alanlar *serbest metin aranabilir* yalnızca olan alanları **Göster başvuruları** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="059b4-155">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span></span>  <span data-ttu-id="059b4-156">Bu seçenek, o değeri herhangi bir özellik olan kayıtları döndürür.</span><span class="sxs-lookup"><span data-stu-id="059b4-156">This option returns records that have that value in any property.</span></span>

![Filtre menüsü](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="059b4-158">Tek bir özellik sonuçlarına seçerek gruplandırabilirsiniz **Group by** kaydı menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="059b4-158">You can group the results on a single property by selecting the **Group by** option in the record menu.</span></span>  <span data-ttu-id="059b4-159">Bu ekler bir [özetlemek](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) sonuçları bir grafik görüntüler, sorgu işleci.</span><span class="sxs-lookup"><span data-stu-id="059b4-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span></span>  <span data-ttu-id="059b4-160">Birden fazla özellik gruplandırabilirsiniz, ancak sorgu doğrudan düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="059b4-160">You can group on more than one property, but you would need to edit the query directly.</span></span>  <span data-ttu-id="059b4-161">Kayıt sonraki menüsünü **bilgisayar** özelliği ve select **'Bilgisayar' grupla**.</span><span class="sxs-lookup"><span data-stu-id="059b4-161">Select the record menu next the the **Computer** property and select **Group by 'Computer'**.</span></span>  

![Bilgisayar grubu](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="059b4-163">Sonuçları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="059b4-163">Work with results</span></span>
<span data-ttu-id="059b4-164">Günlük arama portal çeşitli bir sorgunun sonuçlarını ile çalışmak için özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="059b4-164">The Log Search portal has a variety of features for working with the results of a query.</span></span>  <span data-ttu-id="059b4-165">Sıralayabilir, filtre ve gerçek sorgu değiştirilmeden verileri çözümlemek için Grup sonuçları.</span><span class="sxs-lookup"><span data-stu-id="059b4-165">You can sort, filter, and group results to analyze the data without modifying the actual query.</span></span>  <span data-ttu-id="059b4-166">Varsayılan olarak bir sorgunun sonuçlarını sıralı değil.</span><span class="sxs-lookup"><span data-stu-id="059b4-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="059b4-167">Verileri filtreleme ve sıralama için ek seçenekler sağlayan Tablo formunda görüntülemek için tıklatın **tablo**.</span><span class="sxs-lookup"><span data-stu-id="059b4-167">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Tablo görünümü](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="059b4-169">Bu kayıt ayrıntılarını görüntülemek için bir kayıt tarafından oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="059b4-169">Click the arrow by a record to view the details for that record.</span></span>

![Sıralama sonuçları](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="059b4-171">Herhangi bir alanı kendi sütun başlığına tıklayarak sıralayın.</span><span class="sxs-lookup"><span data-stu-id="059b4-171">Sort on any field by clicking on its column header.</span></span>

![Sıralama sonuçları](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="059b4-173">Belirli bir sütun değeri sonuçlarına filtre düğmesini tıklatarak ve bir filtre koşulu sağlayan filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="059b4-173">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span></span>

![Sonuçları filtresi](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="059b4-175">Bir sütun üzerinde sonuçları üstündeki sütun başlığını sürükleyerek grup.</span><span class="sxs-lookup"><span data-stu-id="059b4-175">Group on a column by dragging its column header to the top of the results.</span></span>  <span data-ttu-id="059b4-176">Birden çok sütun dön sürükleyerek üzerinde birden çok alan gruplandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="059b4-176">You can group on multiple fields by dragging multiple columns to the top.</span></span>

![Grup sonuçları](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="059b4-178">Performans verileri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="059b4-178">Work with performance data</span></span>
<span data-ttu-id="059b4-179">Windows ve Linux aracıları için performans verilerini günlük analizi çalışma alanında depolanan **Perf** tablo.</span><span class="sxs-lookup"><span data-stu-id="059b4-179">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span></span>  <span data-ttu-id="059b4-180">Diğer kaydı gibi performans kayıtları aramak ve biz tüm performans kayıtları olayları ile olduğu gibi veren basit bir sorgu yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="059b4-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Performans verileri](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="059b4-182">Tüm performans nesneleri ve sayaçları kayıtlarını milyonlarca ancak döndüren çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="059b4-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="059b4-183">Verileri filtreleyin veya yalnızca aşağıdaki sorguyu doğrudan günlük arama kutusuna yukarıda kullanılan aynı yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="059b4-183">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span></span>  <span data-ttu-id="059b4-184">Bu, Windows ve Linux bilgisayarlar için kullanım kayıtları yalnızca işlemci döndürür.</span><span class="sxs-lookup"><span data-stu-id="059b4-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![İşlemci kullanımı](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="059b4-186">Bu verileri belirli bir sayaç için sınırlar, ancak bunu hala bu özellikle yararlı bir formda put değil.</span><span class="sxs-lookup"><span data-stu-id="059b4-186">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="059b4-187">Veri bir çizgi grafiği görüntüler, ancak ilk bilgisayar ve TimeGenerated göre gruplandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="059b4-187">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="059b4-188">Birden çok alanları gruplandırmak için sorguyu doğrudan değiştirin, gerekir böylece şu sorguyu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="059b4-188">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span></span>  <span data-ttu-id="059b4-189">Bu kullanır [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) üzerinde işlev **CounterValue** her bir saat ortalama değerini hesaplamak için özellik.</span><span class="sxs-lookup"><span data-stu-id="059b4-189">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Performans veri grafiği](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="059b4-191">Veriler uygun gruplandırılır, onu visual grafik ekleyerek görüntüleyebileceğiniz [işleme](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) işleci.</span><span class="sxs-lookup"><span data-stu-id="059b4-191">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Çizgi grafiği](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="059b4-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="059b4-193">Next steps</span></span>

- <span data-ttu-id="059b4-194">Günlük analizi sorgu dili hakkında daha fazla bilgi [Analytics portalı ile çalışmaya başlama](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="059b4-194">Learn more about the Log Analytics query language at [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="059b4-195">Eğitmen kullanılarak üzerinden yol [Advanced Analytics portalı](https://go.microsoft.com/fwlink/?linkid=856587) olanak sağlayan aynı sorguları çalıştırmak ve günlük arama portalı aynı verilere erişmek.</span><span class="sxs-lookup"><span data-stu-id="059b4-195">Walk through a tutorial using the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you to run the same queries and access the same data as the Log Search portal.</span></span>

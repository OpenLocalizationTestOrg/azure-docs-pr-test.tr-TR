---
title: "aaaUsing hello günlük arama Azure günlük analizi portalında | Microsoft Docs"
description: "Bu makalede nasıl toocreate aramaları oturum ve hello günlük arama portal kullanarak günlük analizi çalışma alanınızda depolanan verileri çözümleyen açıklayan bir öğretici içerir.  Başlangıç Öğreticisi tooreturn farklı veri türlerini bazı basit sorguları çalıştırma ve sonuçları çözümleme içerir."
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
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a><span data-ttu-id="64874-104">Merhaba günlük arama portalı kullanarak Azure günlük analizi günlük aramalar oluşturun</span><span class="sxs-lookup"><span data-stu-id="64874-104">Create log searches in Azure Log Analytics using hello Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="64874-105">Bu makalede hello günlük arama hello yeni sorgu dili kullanarak Azure günlük analizi portalında açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="64874-105">This article describes hello Log Search portal in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="64874-106">Merhaba yeni dil hakkında daha fazla bilgi ve çalışma alanı hello yordamı tooupgrade almak [Azure günlük analizi çalışma alanı toonew günlük aramanızı yükseltme](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="64874-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="64874-107">Çalışma alanınızı yükseltilmiş toohello yeni sorgu dili bırakılmamışsa, çok başvurmalıdır[Bul günlük aramaları günlük analizi kullanarak verileri](log-analytics-log-searches.md) hello hello günlük arama Portalı'nın geçerli sürümü hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="64874-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="64874-108">Bu makalede nasıl toocreate aramaları oturum ve hello günlük arama portal kullanarak günlük analizi çalışma alanınızda depolanan verileri çözümleyen açıklayan bir öğretici içerir.</span><span class="sxs-lookup"><span data-stu-id="64874-108">This article includes a tutorial that describes how toocreate log searches and analyze data stored in your Log Analytics workspace using hello Log Search portal.</span></span>  <span data-ttu-id="64874-109">Başlangıç Öğreticisi tooreturn farklı veri türlerini bazı basit sorguları çalıştırma ve sonuçları çözümleme içerir.</span><span class="sxs-lookup"><span data-stu-id="64874-109">hello tutorial includes running some simple queries tooreturn different types of data and analyzing results.</span></span>  <span data-ttu-id="64874-110">Merhaba günlük arama portalında doğrudan değiştirmek yerine hello sorgu değiştirmek için özellikler odaklanır.</span><span class="sxs-lookup"><span data-stu-id="64874-110">It focuses on features in hello Log Search portal for modifying hello query rather than modifying it directly.</span></span>  <span data-ttu-id="64874-111">Merhaba doğrudan hello sorgu düzenleme hakkında daha fazla bilgi için bkz [sorgu dili başvurusu](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="64874-111">For details on directly editing hello query, see hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="64874-112">Merhaba günlük arama portalı yerine hello Advanced Analytics portalında toocreate aramaları Bkz [hello Analytics portalı ile çalışmaya başlama](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="64874-112">toocreate searches in hello Advanced Analytics portal instead of hello Log Search portal, see [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="64874-113">Her iki portalları hello kullanın dil tooaccess hello hello günlük analizi çalışma alanındaki aynı veri aynı sorgu.</span><span class="sxs-lookup"><span data-stu-id="64874-113">Both portals use hello same query language tooaccess hello same data in hello Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64874-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="64874-114">Prerequisites</span></span>
<span data-ttu-id="64874-115">Bu öğretici, bir günlük analizi çalışma alanı hello sorguları tooanalyze için veri üretir en az bir bağlı kaynağıyla zaten sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="64874-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for hello queries tooanalyze.</span></span>  

- <span data-ttu-id="64874-116">Bir çalışma alanı yoksa, ücretsiz bir tane oluşturabilirsiniz adresindeki hello yordamı kullanarak [günlük analizi çalışma alanı ile çalışmaya başlama](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="64874-116">If you don't have a workspace, you can create a free one using hello procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="64874-117">En az bir bağlanma [Windows Aracısı](log-analytics-windows-agents.md) veya bir [Linux Aracısı](log-analytics-linux-agents.md) toohello çalışma.</span><span class="sxs-lookup"><span data-stu-id="64874-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) toohello workspace.</span></span>  

## <a name="open-hello-log-search-portal"></a><span data-ttu-id="64874-118">Açık hello günlük arama portalı</span><span class="sxs-lookup"><span data-stu-id="64874-118">Open hello Log Search portal</span></span>
<span data-ttu-id="64874-119">Merhaba günlük arama portal açarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="64874-119">Start by opening hello Log Search portal.</span></span>  <span data-ttu-id="64874-120">Hello Azure portal veya hello OMS portalı erişebilir.</span><span class="sxs-lookup"><span data-stu-id="64874-120">You can access it in either hello Azure portal or hello OMS portal.</span></span>

1. <span data-ttu-id="64874-121">Açık hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="64874-121">Open hello Azure portal.</span></span>
2. <span data-ttu-id="64874-122">TooLog Analytics gidin ve çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="64874-122">Navigate tooLog Analytics and select your workspace.</span></span>
3. <span data-ttu-id="64874-123">Her iki select **günlük arama** hello seçerek Azure portal veya başlatma hello OMS portalında toostay **OMS portalı** ve ardından hello günlük arama düğmesini tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="64874-123">Either select **Log Search** toostay in hello Azure portal or launch hello OMS portal by selecting **OMS Portal** and then clicking hello Log Search button.</span></span>

![Günlük Ara düğmesi](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="64874-125">Basit Arama oluşturma</span><span class="sxs-lookup"><span data-stu-id="64874-125">Create a simple search</span></span>
<span data-ttu-id="64874-126">Merhaba hızlı şekilde tooretrieve bazı veri toowork ile tablodaki tüm kayıtları döndürür basit bir sorgudur.</span><span class="sxs-lookup"><span data-stu-id="64874-126">hello quickest way tooretrieve some data toowork with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="64874-127">Tüm Windows veya Linux istemcileri bağlı tooyour çalışma varsa ya da olay (Windows) veya Syslog (Linux) tablosu hello verilerde sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="64874-127">If you have any Windows or Linux clients connected tooyour workspace, then you'll have data in either hello Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="64874-128">Merhaba arama kutusu sorguları izleyen bir hello yazın ve hello arama düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="64874-128">Type one hello following queries in hello search box and click hello search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="64874-129">Veriler hello varsayılan liste görünümünde döndürülür ve kaç tane toplam kaydı döndürülmedi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64874-129">Data is returned in hello default list view, and you can see how many total records were returned.</span></span>

![Basit Sorgu](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="64874-131">Yalnızca hello ilk birkaç özellikleri her kaydın görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="64874-131">Only hello first few properties of each record are displayed.</span></span>  <span data-ttu-id="64874-132">Tıklatın **daha fazla Göster** toodisplay belirli bir kayıt için tüm özellikleri.</span><span class="sxs-lookup"><span data-stu-id="64874-132">Click **show more** toodisplay all properties for a particular record.</span></span>

![Kayıt ayrıntıları](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a><span data-ttu-id="64874-134">Başlangıç saati kapsamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="64874-134">Set hello time scope</span></span>
<span data-ttu-id="64874-135">Günlük analizi tarafından toplanan her kaydına sahip bir **TimeGenerated** bu hello kayıt başlangıç tarihi ve saati içeren özelliği oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="64874-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains hello date and time that hello record was created.</span></span>  <span data-ttu-id="64874-136">Merhaba günlük arama portal sorguda yalnızca kayıtlarıyla döndürür bir **TimeGenerated** yan hello ekranın sol hello üzerinde görüntülenen hello zaman kapsam içinde.</span><span class="sxs-lookup"><span data-stu-id="64874-136">A query in hello Log Search portal only returns records with a **TimeGenerated** within hello time scope that's displayed on hello left side of hello screen.</span></span>  

<span data-ttu-id="64874-137">Merhaba zaman filtresi hello açılır seçerek veya hello kaydırıcı değiştirerek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64874-137">You can change hello time filter either by selecting hello dropdown or by modifying hello slider.</span></span>  <span data-ttu-id="64874-138">Merhaba kaydırıcı hello göreli her zaman diliminin hello aralıkta için kayıt sayısını gösteren bir çubuk grafiği görüntüler.</span><span class="sxs-lookup"><span data-stu-id="64874-138">hello slider displays a bar graph that shows hello relative number of records for each time segment within hello range.</span></span>  <span data-ttu-id="64874-139">Bu kesimin hello aralığı bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="64874-139">This segment will vary depending on hello range.</span></span>

<span data-ttu-id="64874-140">Merhaba varsayılan saat kapsamı **1 gün**.</span><span class="sxs-lookup"><span data-stu-id="64874-140">hello default time scope is **1 day**.</span></span>  <span data-ttu-id="64874-141">Bu değeri çok değiştirmek**7 gün**, ve hello kayıtlarının toplam sayısını artırın.</span><span class="sxs-lookup"><span data-stu-id="64874-141">Change this value too**7 days**, and hello total number of records should increase.</span></span>

![Tarih saat kapsamı](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a><span data-ttu-id="64874-143">Merhaba sorgu sonuçlarını filtreleme</span><span class="sxs-lookup"><span data-stu-id="64874-143">Filter results of hello query</span></span>
<span data-ttu-id="64874-144">Merhaba üzerinde hello ekranın sol tarafındaki doğrudan değiştirmeden toohello Sorgu filtreleme tooadd sağlayan hello Filtre Bölmesi ' dir.</span><span class="sxs-lookup"><span data-stu-id="64874-144">On hello left side of hello screen is hello filter pane which allows you tooadd filtering toohello query without modifying it directly.</span></span>  <span data-ttu-id="64874-145">Çeşitli özellikleri döndürülen hello kayıtların üst on değerleriyle kendi kayıt sayısı ile birlikte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="64874-145">Several properties of hello records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="64874-146">İle çalışıyorsanız **olay**, select hello onay kutusu sonraki çok**hata** altında **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="64874-146">If you're working with **Event**, select hello checkbox next too**Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="64874-147">İle çalışıyorsanız **Syslog**, select hello onay kutusu sonraki çok**hata** altında **önem düzeyi**.</span><span class="sxs-lookup"><span data-stu-id="64874-147">If you're working with **Syslog**, select hello checkbox next too**err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="64874-148">Bu tooerror olayları toolimit hello aşağıdaki hello tooone sonuçları hello sorgu değiştirir.</span><span class="sxs-lookup"><span data-stu-id="64874-148">This changes hello query tooone of hello following toolimit hello results tooerror events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtre](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="64874-150">Seçerek Ekle özellikleri toohello filtre bölmesi **toofilters ekleme** hello özelliği menüsünden hello kayıtları biri.</span><span class="sxs-lookup"><span data-stu-id="64874-150">Add properties toohello filter pane by selecting **Add toofilters** from hello property menu on one of hello records.</span></span>

![Toofilter menü ekleme](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="64874-152">Aynı filtre seçerek hello ayarlayabilirsiniz **filtre** toofilter istediğiniz hello özelliği menüsünden hello içeren bir kaydı.</span><span class="sxs-lookup"><span data-stu-id="64874-152">You can set hello same filter by selecting **Filter** from hello property menu for a record with hello value you want toofilter.</span></span>  

<span data-ttu-id="64874-153">Merhaba yeterlidir **filtre** adlarının mavi olan özellikleri seçeneği.</span><span class="sxs-lookup"><span data-stu-id="64874-153">You only have hello **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="64874-154">Bunlar *aranabilir* için dizin alanları arama koşulları.</span><span class="sxs-lookup"><span data-stu-id="64874-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="64874-155">Gri alanlar *serbest metin aranabilir* hello yalnızca olan alanları **Göster başvuruları** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="64874-155">Fields in grey are *free text searchable* fields which only have hello **Show references** option.</span></span>  <span data-ttu-id="64874-156">Bu seçenek, o değeri herhangi bir özellik olan kayıtları döndürür.</span><span class="sxs-lookup"><span data-stu-id="64874-156">This option returns records that have that value in any property.</span></span>

![Filtre menüsü](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="64874-158">Merhaba seçerek tek bir özellik hello sonuçlarına gruplandırabilirsiniz **Group by** hello kayıt menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="64874-158">You can group hello results on a single property by selecting hello **Group by** option in hello record menu.</span></span>  <span data-ttu-id="64874-159">Bu ekler bir [özetlemek](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) hello sonuçları bir grafik görüntüler tooyour sorgu işleci.</span><span class="sxs-lookup"><span data-stu-id="64874-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query that displays hello results in a chart.</span></span>  <span data-ttu-id="64874-160">Birden fazla özellik gruplandırabilirsiniz, ancak tooedit hello sorgu doğrudan gerekir.</span><span class="sxs-lookup"><span data-stu-id="64874-160">You can group on more than one property, but you would need tooedit hello query directly.</span></span>  <span data-ttu-id="64874-161">Select hello kayıt menü sonraki hello hello **bilgisayar** özelliği ve select **'Bilgisayar' grupla**.</span><span class="sxs-lookup"><span data-stu-id="64874-161">Select hello record menu next hello hello **Computer** property and select **Group by 'Computer'**.</span></span>  

![Bilgisayar grubu](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="64874-163">Sonuçları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="64874-163">Work with results</span></span>
<span data-ttu-id="64874-164">Merhaba günlük arama portal çeşitli hello bir sorgunun sonuçlarını ile çalışmak için özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="64874-164">hello Log Search portal has a variety of features for working with hello results of a query.</span></span>  <span data-ttu-id="64874-165">Filtre ve Grup sonuçları tooanalyze hello veri hello gerçek sorgu değiştirilmeden sıralama yapabilirsiniz;</span><span class="sxs-lookup"><span data-stu-id="64874-165">You can sort, filter, and group results tooanalyze hello data without modifying hello actual query.</span></span>  <span data-ttu-id="64874-166">Varsayılan olarak bir sorgunun sonuçlarını sıralı değil.</span><span class="sxs-lookup"><span data-stu-id="64874-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="64874-167">tooview hello verileri filtreleme ve sıralama, için ek seçenekler sağlayan Tablo formunda tıklatın **tablo**.</span><span class="sxs-lookup"><span data-stu-id="64874-167">tooview hello data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Tablo görünümü](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="64874-169">Bu kayıt kayıt tooview hello ayrıntılarını tarafından Hello oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64874-169">Click hello arrow by a record tooview hello details for that record.</span></span>

![Sıralama sonuçları](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="64874-171">Herhangi bir alanı kendi sütun başlığına tıklayarak sıralayın.</span><span class="sxs-lookup"><span data-stu-id="64874-171">Sort on any field by clicking on its column header.</span></span>

![Sıralama sonuçları](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="64874-173">Merhaba filtre düğmesini tıklatarak ve bir filtre koşulu sağlayan hello sütununda belirli bir değer hello sonuçlarına filtre.</span><span class="sxs-lookup"><span data-stu-id="64874-173">Filter hello results on a specific value in hello column by clicking hello filter button and providing a filter condition.</span></span>

![Sonuçları filtresi](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="64874-175">Bir sütunda, sütun başlığı toohello üst hello sonuçlarının sürükleyerek gruplandırın.</span><span class="sxs-lookup"><span data-stu-id="64874-175">Group on a column by dragging its column header toohello top of hello results.</span></span>  <span data-ttu-id="64874-176">Birden çok sütun toohello üst sürükleyerek üzerinde birden çok alan gruplandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64874-176">You can group on multiple fields by dragging multiple columns toohello top.</span></span>

![Grup sonuçları](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="64874-178">Performans verileri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="64874-178">Work with performance data</span></span>
<span data-ttu-id="64874-179">Windows ve Linux aracıları için performans verilerini hello günlük analizi çalışma alanında hello depolandığı **Perf** tablo.</span><span class="sxs-lookup"><span data-stu-id="64874-179">Performance data for both Windows and Linux agents is stored in hello Log Analytics workspace in hello **Perf** table.</span></span>  <span data-ttu-id="64874-180">Diğer kaydı gibi performans kayıtları aramak ve biz tüm performans kayıtları olayları ile olduğu gibi veren basit bir sorgu yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64874-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Performans verileri](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="64874-182">Tüm performans nesneleri ve sayaçları kayıtlarını milyonlarca ancak döndüren çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="64874-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="64874-183">Doğrudan hello günlük arama kutusuna toofilter hello veri yukarıda kullanılan ya da yalnızca hello aşağıdakileri yazın aynı yöntemleri sorgu hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64874-183">You can use hello same methods you used above toofilter hello data or just type hello following query directly into hello log search box.</span></span>  <span data-ttu-id="64874-184">Bu, Windows ve Linux bilgisayarlar için kullanım kayıtları yalnızca işlemci döndürür.</span><span class="sxs-lookup"><span data-stu-id="64874-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![İşlemci kullanımı](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="64874-186">Bu hello veri tooa belirli sayaç sınırlar, ancak bunu hala bu özellikle yararlı bir formda put değil.</span><span class="sxs-lookup"><span data-stu-id="64874-186">This limits hello data tooa particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="64874-187">Bir çizgi grafiği hello verileri görüntülemek, ancak ilk toogroup gerekir, bilgisayar ve TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="64874-187">You can display hello data in a line chart, but first need toogroup it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="64874-188">toogroup birden çok alana ihtiyacınız toomodify hello sorgu doğrudan hello sorgu toohello aşağıdaki şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="64874-188">toogroup on multiple fields, you need toomodify hello query directly, so modify hello query toohello following.</span></span>  <span data-ttu-id="64874-189">Bu hello kullanır [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) hello işlevini **CounterValue** özelliği toocalculate hello her bir saat içinde ortalama değer.</span><span class="sxs-lookup"><span data-stu-id="64874-189">This uses hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on hello **CounterValue** property toocalculate hello average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Performans veri grafiği](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="64874-191">Hello veri uygun gruplandırılmış, onu visual grafik hello ekleyerek görüntüleyebileceğiniz [işleme](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) işleci.</span><span class="sxs-lookup"><span data-stu-id="64874-191">Now that hello data is suitably grouped, you can display it in a visual chart by adding hello [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Çizgi grafiği](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="64874-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64874-193">Next steps</span></span>

- <span data-ttu-id="64874-194">Hello günlük analizi sorgu dili hakkında daha fazla bilgi [hello Analytics portalı ile çalışmaya başlama](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="64874-194">Learn more about hello Log Analytics query language at [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="64874-195">Hello kullanarak bir öğreticide yol [Advanced Analytics portalı](https://go.microsoft.com/fwlink/?linkid=856587) olanak sağlayan toorun hello aynı sorgular ve erişim hello hello günlük arama portalı aynı verileri.</span><span class="sxs-lookup"><span data-stu-id="64874-195">Walk through a tutorial using hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you toorun hello same queries and access hello same data as hello Log Search portal.</span></span>

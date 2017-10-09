---
title: "Azure SQL veritabanı için aaaQuery performansı öngörüleri | Microsoft Docs"
description: "Sorgu performansı izleme çoğu CPU kullanan bir Azure SQL veritabanı için sorgular hello tanımlar."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="89954-103">Azure SQL veritabanı sorgu performansı öngörüleri</span><span class="sxs-lookup"><span data-stu-id="89954-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="89954-104">İlişkisel veritabanları hello performans ayarlama ve yönetme önemli uzmanlık ve zaman yatırımı gerektiren bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="89954-104">Managing and tuning hello performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="89954-105">Sorgu performansı öngörüleri toospend veritabanı performans sorunlarını giderme hello aşağıdakileri sağlayarak daha az zaman verir:</span><span class="sxs-lookup"><span data-stu-id="89954-105">Query Performance Insight allows you toospend less time troubleshooting database performance by providing hello following:</span></span>

* <span data-ttu-id="89954-106">Veritabanları (DTU) kaynak tüketimi daha derin bir anlayış.</span><span class="sxs-lookup"><span data-stu-id="89954-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="89954-107">Merhaba üst sorgular tarafından potansiyel olarak performansı için ayarlanan süre/CPU/yürütme sayısı.</span><span class="sxs-lookup"><span data-stu-id="89954-107">hello top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="89954-108">bir sorgu hello ayrıntılarını aşağı özelliği toodrill Merhaba, metin ve kaynak kullanımı geçmişini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="89954-108">hello ability toodrill down into hello details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="89954-109">Performans tarafından gerçekleştirilen eylemler Göster ek açıklamaları ayarlama [SQL Azure veritabanı Danışmanı](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="89954-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="89954-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="89954-110">Prerequisites</span></span>
* <span data-ttu-id="89954-111">Sorgu performansı öngörüleri gerektirir [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) veritabanınızda etkindir.</span><span class="sxs-lookup"><span data-stu-id="89954-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="89954-112">Merhaba portal Query Store çalışmıyorsa tooturn ister üzerinde.</span><span class="sxs-lookup"><span data-stu-id="89954-112">If Query Store is not running, hello portal prompts you tooturn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="89954-113">İzinler</span><span class="sxs-lookup"><span data-stu-id="89954-113">Permissions</span></span>
<span data-ttu-id="89954-114">Merhaba aşağıdaki [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md) izinler gerekli toouse sorgu performansı öngörüleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="89954-114">hello following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required toouse Query Performance Insight:</span></span> 

* <span data-ttu-id="89954-115">**Okuyucu**, **sahibi**, **katkıda bulunan**, **SQL DB Katılımcısı**, veya **SQL Server Katılımcısı** izinler tooview hello üst kaynak tüketen sorguları ve grafikler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="89954-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview hello top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="89954-116">**Sahibi**, **katkıda bulunan**, **SQL DB Katılımcısı**, veya **SQL Server Katılımcısı** gerekli tooview sorgu metni izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="89954-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="89954-117">Sorgu performansı öngörüleri kullanma</span><span class="sxs-lookup"><span data-stu-id="89954-117">Using Query Performance Insight</span></span>
<span data-ttu-id="89954-118">Sorgu performansı öngörüleri kolayca toouse şöyledir:</span><span class="sxs-lookup"><span data-stu-id="89954-118">Query Performance Insight is easy toouse:</span></span>

* <span data-ttu-id="89954-119">Açık [Azure portal](https://portal.azure.com/) ve Bul veritabanı tooexamine istiyor.</span><span class="sxs-lookup"><span data-stu-id="89954-119">Open [Azure portal](https://portal.azure.com/) and find database that you want tooexamine.</span></span> 
  * <span data-ttu-id="89954-120">Destek ve sorun giderme, sol taraftaki menüden "Sorgu performansı öngörüleri" seçin.</span><span class="sxs-lookup"><span data-stu-id="89954-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="89954-121">Merhaba ilk sekmesinde üst kaynak tüketen sorguları hello listesini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="89954-121">On hello first tab, review hello list of top resource-consuming queries.</span></span>
* <span data-ttu-id="89954-122">Bir sorguyu tooview ayrıntılarını seçin.</span><span class="sxs-lookup"><span data-stu-id="89954-122">Select an individual query tooview its details.</span></span>
* <span data-ttu-id="89954-123">Açık [SQL Azure veritabanı Danışmanı](sql-database-advisor.md) ve herhangi bir önerimiz kullanılabilir olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="89954-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="89954-124">Kaydırma çubuklarını kullanın veya aralık gözlenen simgeler toochange Yakınlaştır.</span><span class="sxs-lookup"><span data-stu-id="89954-124">Use sliders or zoom icons toochange observed interval.</span></span>
  
    ![Performans Panosu](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="89954-126">Birkaç saat veri SQL veritabanı tooprovide sorgu performansı öngörüleri için Query Store tarafından yakalanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="89954-126">A couple hours of data needs toobe captured by Query Store for SQL Database tooprovide query performance insights.</span></span> <span data-ttu-id="89954-127">Merhaba veritabanı sahip hiç etkinlik yok veya sorgu deposu belirli bir dönemdeki sırasında etkin değil, hello grafikleri döneme görüntülenirken boş olur.</span><span class="sxs-lookup"><span data-stu-id="89954-127">If hello database has no activity or Query Store was not active during a certain time period, hello charts will be empty when displaying that time period.</span></span> <span data-ttu-id="89954-128">Çalışır durumda değilse herhangi bir anda Query Store sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="89954-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="89954-129">Kaynak tüketen sorguları üst CPU gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="89954-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="89954-130">Merhaba, [portal](http://portal.azure.com) aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="89954-130">In hello [portal](http://portal.azure.com) do hello following:</span></span>

1. <span data-ttu-id="89954-131">Tooa SQL veritabanını bulun ve tıklatın **tüm ayarları** > **destek + sorun giderme** > **sorgu performansı öngörüleri**.</span><span class="sxs-lookup"><span data-stu-id="89954-131">Browse tooa SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Sorgu Performansı Öngörüleri][1]
   
    <span data-ttu-id="89954-133">Merhaba üst sorgular görünümünü açar ve hello üst CPU tüketim sorguları listelenir.</span><span class="sxs-lookup"><span data-stu-id="89954-133">hello top queries view opens and hello top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="89954-134">Ayrıntılar için hello grafiğin etrafında'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="89954-134">Click around hello chart for details.</span></span><br><span data-ttu-id="89954-135">Merhaba çubukları hello seçilen zaman aralığı boyunca seçili hello sorgular tarafından tüketilen CPU % gösterirken hello üst çizgi hello veritabanı için genel DTU % gösterir (örneğin, **geçen hafta** seçili her çubuk bir gününü temsil eder).</span><span class="sxs-lookup"><span data-stu-id="89954-135">hello top line shows overall DTU% for hello database, while hello bars show CPU% consumed by hello selected queries during hello selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![üst sorguları][2]
   
    <span data-ttu-id="89954-137">Merhaba alt kılavuz hello görünür sorgular için toplanan bilgileri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="89954-137">hello bottom grid represents aggregated information for hello visible queries.</span></span>
   
   * <span data-ttu-id="89954-138">Sorgu kimliği - sorgu veritabanı içinde benzersiz tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="89954-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="89954-139">CPU (toplama işlevini bağlıdır) sorgu observable aralığı sırasında başına.</span><span class="sxs-lookup"><span data-stu-id="89954-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="89954-140">Sorgu başına süre (toplama işlevini bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="89954-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="89954-141">Belirli bir sorgu için yürütmeleri toplam sayısı.</span><span class="sxs-lookup"><span data-stu-id="89954-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="89954-142">Seçin, tek tek sorguları tooinclude temizleyin veya onay kutularını kullanarak hello grafikten içermeyecek.</span><span class="sxs-lookup"><span data-stu-id="89954-142">Select or clear individual queries tooinclude or exclude them from hello chart using checkboxes.</span></span>
3. <span data-ttu-id="89954-143">Verilerinizi eski hale gelirse hello tıklatın **yenileme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89954-143">If your data becomes stale, click hello **Refresh** button.</span></span>
4. <span data-ttu-id="89954-144">Kaydırıcılar ve Yakınlaştırma düğmeleri toochange gözlem aralığı kullanın ve ani araştırın: ![ayarları](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="89954-144">You can use sliders and zoom buttons toochange observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="89954-145">İsteğe bağlı olarak, farklı bir görünüm istiyorsanız, seçebileceğiniz **özel** sekmesinde ve ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="89954-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="89954-146">Ölçüm (CPU süresi, yürütme sayısı)</span><span class="sxs-lookup"><span data-stu-id="89954-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="89954-147">Zaman aralığı (son 24 saat, geçen hafta geçen ay).</span><span class="sxs-lookup"><span data-stu-id="89954-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="89954-148">Sorgu sayısı.</span><span class="sxs-lookup"><span data-stu-id="89954-148">Number of queries.</span></span>
   * <span data-ttu-id="89954-149">Toplama işlevi.</span><span class="sxs-lookup"><span data-stu-id="89954-149">Aggregation function.</span></span>
     
     ![ayarlar](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="89954-151">Sorguyu ayrıntılarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="89954-151">Viewing individual query details</span></span>
<span data-ttu-id="89954-152">tooview sorgu ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="89954-152">tooview query details:</span></span>

1. <span data-ttu-id="89954-153">En sık kullanılan sorguların hello listesindeki herhangi bir sorgu tıklayın.</span><span class="sxs-lookup"><span data-stu-id="89954-153">Click any query in hello list of top queries.</span></span>
   
    ![Ayrıntıları](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="89954-155">Merhaba Ayrıntılar görünümünü açar ve hello sorguları CPU süresi/tüketim/yürütme sayısı zamanla ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="89954-155">hello details view opens and hello queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="89954-156">Ayrıntılar için hello grafiğin etrafında'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="89954-156">Click around hello chart for details.</span></span>
   
   * <span data-ttu-id="89954-157">Üst grafik genel veritabanı DTU % satırıyla, ve hello çubukları hello seçili sorgu tarafından tüketilen CPU % olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="89954-157">Top chart shows line with overall database DTU%, and hello bars are CPU% consumed by hello selected query.</span></span>
   * <span data-ttu-id="89954-158">İkinci grafik hello seçili sorgu tarafından toplam süresini gösterir.</span><span class="sxs-lookup"><span data-stu-id="89954-158">Second chart shows total duration by hello selected query.</span></span>
   * <span data-ttu-id="89954-159">Alt grafik hello seçili sorgu tarafından yürütmeleri toplam sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="89954-159">Bottom chart shows total number of executions by hello selected query.</span></span>
     
     ![Sorgu Ayrıntıları][3]
4. <span data-ttu-id="89954-161">İsteğe bağlı olarak, kaydırma çubuklarını kullanın, Yakınlaştırma düğmeleri veya tıklatın **ayarları** toocustomize sorgu verinin nasıl görüntüleneceğini veya toopick farklı bir zaman aralığı.</span><span class="sxs-lookup"><span data-stu-id="89954-161">Optionally, use sliders, zoom buttons or click **Settings** toocustomize how query data is displayed, or toopick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="89954-162">Üst sorguları süre her gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="89954-162">Review top queries per duration</span></span>
<span data-ttu-id="89954-163">Merhaba son güncelleştirmesinde sorgu performansı öngörüleri, olası performans sorunlarını belirlemenize yardımcı olabilecek iki yeni ölçümleri gösterdiğimizi: süresi ve yürütme sayısı.</span><span class="sxs-lookup"><span data-stu-id="89954-163">In hello recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="89954-164">Uzun süre çalışan sorgular uzun kaynakları kilitleme, diğer kullanıcıların engelleme ve ölçeklenebilirlik sınırlama hello büyük potansiyeline sahiptir.</span><span class="sxs-lookup"><span data-stu-id="89954-164">Long-running queries have hello greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="89954-165">Bunlar ayrıca hello en iyi duruma getirme adaylardır.</span><span class="sxs-lookup"><span data-stu-id="89954-165">They are also hello best candidates for optimization.</span></span><br>

<span data-ttu-id="89954-166">uzun süre çalışan sorgular tooidentify:</span><span class="sxs-lookup"><span data-stu-id="89954-166">tooidentify long running queries:</span></span>

1. <span data-ttu-id="89954-167">Açık **özel** sorgu performansı öngörüleri bir sekmede Seçilen veritabanı için</span><span class="sxs-lookup"><span data-stu-id="89954-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="89954-168">Değiştirme ölçümleri toobe **süresi**</span><span class="sxs-lookup"><span data-stu-id="89954-168">Change metrics toobe **duration**</span></span>
3. <span data-ttu-id="89954-169">Sorgular ve Gözlem aralığı sayısını seçin</span><span class="sxs-lookup"><span data-stu-id="89954-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="89954-170">Toplama işlevi seçin</span><span class="sxs-lookup"><span data-stu-id="89954-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="89954-171">**Sum** tüm gözlem aralığı sırasında tüm sorgu yürütme süresini ekler.</span><span class="sxs-lookup"><span data-stu-id="89954-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="89954-172">**Max** tüm gözlem aralığında hangi yürütme süresi en fazla sorguları bulur.</span><span class="sxs-lookup"><span data-stu-id="89954-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="89954-173">**Ortalama** ortalama yürütme süresi tüm sorgu yürütmeleri ve size göstermek bulur hello üst bu ortalamalar dışında.</span><span class="sxs-lookup"><span data-stu-id="89954-173">**Avg** finds average execution time of all query executions and show you hello top out of these averages.</span></span> 
     
     ![Sorgu süresi][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="89954-175">Üst sorguları yürütme sayısı her gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="89954-175">Review top queries per execution count</span></span>
<span data-ttu-id="89954-176">Çok sayıda yürütmeleri değil etkileyen veritabanının kendisi ve kaynak kullanımı düşük olabilir, ancak genel uygulama alabilirsiniz yavaş.</span><span class="sxs-lookup"><span data-stu-id="89954-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="89954-177">Bazı durumlarda, çok yüksek yürütme sayısı ağ tooincrease açabilir gidiş dönüş.</span><span class="sxs-lookup"><span data-stu-id="89954-177">In some cases, very high execution count may lead tooincrease of network round trips.</span></span> <span data-ttu-id="89954-178">Gidiş dönüş performansını önemli ölçüde etkiler.</span><span class="sxs-lookup"><span data-stu-id="89954-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="89954-179">Konu toonetwork gecikme süresi ve toodownstream sunucu gecikme süresi oldukları.</span><span class="sxs-lookup"><span data-stu-id="89954-179">They are subject toonetwork latency and toodownstream server latency.</span></span> 

<span data-ttu-id="89954-180">Örneğin, birçok veri tabanlı Web sitesi yoğun olarak her kullanıcı isteğine hello veritabanı erişin.</span><span class="sxs-lookup"><span data-stu-id="89954-180">For example, many data-driven Web sites heavily access hello database for every user request.</span></span> <span data-ttu-id="89954-181">Bağlantı havuzu yardımcı olur, hello artan sırada ağ trafiği ve hello veritabanı sunucusu üzerindeki işlem yükü performansını olumsuz etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="89954-181">While connection pooling helps, hello increased network traffic and processing load on hello database server can adversely affect performance.</span></span>  <span data-ttu-id="89954-182">Genel öneriler tookeep dönüşleri tooan minimuma round ' dir.</span><span class="sxs-lookup"><span data-stu-id="89954-182">General advice is tookeep round trips tooan absolute minimum.</span></span>

<span data-ttu-id="89954-183">tooidentify sık sorgular ("chatty") sorguları yürütülen:</span><span class="sxs-lookup"><span data-stu-id="89954-183">tooidentify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="89954-184">Açık **özel** sorgu performansı öngörüleri bir sekmede Seçilen veritabanı için</span><span class="sxs-lookup"><span data-stu-id="89954-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="89954-185">Değiştirme ölçümleri toobe **yürütme sayısı**</span><span class="sxs-lookup"><span data-stu-id="89954-185">Change metrics toobe **execution count**</span></span>
3. <span data-ttu-id="89954-186">Sorgular ve Gözlem aralığı sayısını seçin</span><span class="sxs-lookup"><span data-stu-id="89954-186">Select number of queries and observation interval</span></span>
   
    ![sorgu yürütme sayısı][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="89954-188">Performans ayarlama ek açıklamaları anlama</span><span class="sxs-lookup"><span data-stu-id="89954-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="89954-189">Sorgu performansı öngörüleri, iş yükü keşfetme sırasında hello grafik üstünde dikey çizgi simgelerle fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89954-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of hello chart.</span></span><br>

<span data-ttu-id="89954-190">Bu simgeleri ek açıklamaları; yine de uygun istiyor musunuz? tarafından gerçekleştirilen eylemler etkileyen performans temsil [SQL Azure veritabanı Danışmanı](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="89954-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="89954-191">Vurgulama ek açıklama tarafından hello eylem hakkında temel bilgileri alın:</span><span class="sxs-lookup"><span data-stu-id="89954-191">By hovering annotation, you get basic information about hello action:</span></span>

![Sorgu ek açıklaması][6]

<span data-ttu-id="89954-193">Daha fazla tooknow istediğiniz veya Danışmanı öneriyi hello simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="89954-193">If you want tooknow more or apply advisor recommendation, click hello icon.</span></span> <span data-ttu-id="89954-194">Eylem ayrıntılarını açar.</span><span class="sxs-lookup"><span data-stu-id="89954-194">It will open details of action.</span></span> <span data-ttu-id="89954-195">Etkin bir öneri ise hemen komutunu kullanarak uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89954-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![Sorgu ek açıklama Ayrıntıları][7]

### <a name="multiple-annotations"></a><span data-ttu-id="89954-197">Birden çok ek açıklama.</span><span class="sxs-lookup"><span data-stu-id="89954-197">Multiple annotations.</span></span>
<span data-ttu-id="89954-198">Yakınlaştırma düzeyi nedeniyle, diğer Kapat tooeach olan ek açıklamaları birine daraltılmış olduğunu, mümkündür.</span><span class="sxs-lookup"><span data-stu-id="89954-198">It’s possible, that because of zoom level, annotations that are close tooeach other will get collapsed into one.</span></span> <span data-ttu-id="89954-199">Bu özel simgesi ile temsil edilir, tıklatarak nerede ek açıklamaları listesi gruplandırılmış açık yeni dikey penceresi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="89954-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="89954-200">Sorgular ve performans Eylemler ayarlama bağıntı toobetter yükünüzü anlamanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="89954-200">Correlating queries and performance tuning actions can help toobetter understand your workload.</span></span> 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="89954-201">Sorgu performansı öngörüleri için en iyi duruma getirme hello sorgu deposu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="89954-201">Optimizing hello Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="89954-202">Query Store iletileri aşağıdaki hello kullanımınız sorgu performansı öngörüleri sırasında karşılaşabileceğiniz:</span><span class="sxs-lookup"><span data-stu-id="89954-202">During your use of Query Performance Insight, you might encounter hello following Query Store messages:</span></span>

* <span data-ttu-id="89954-203">"Query Store düzgün bu veritabanında yapılandırılmamış.</span><span class="sxs-lookup"><span data-stu-id="89954-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="89954-204">Daha fazla toolearn burayı."</span><span class="sxs-lookup"><span data-stu-id="89954-204">Click here toolearn more."</span></span>
* <span data-ttu-id="89954-205">"Query Store düzgün bu veritabanında yapılandırılmamış.</span><span class="sxs-lookup"><span data-stu-id="89954-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="89954-206">Burada toochange ayarlar'ı tıklatın."</span><span class="sxs-lookup"><span data-stu-id="89954-206">Click here toochange settings."</span></span> 

<span data-ttu-id="89954-207">Query Store mümkün toocollect yeni veri değilse bu iletiler genellikle görünür.</span><span class="sxs-lookup"><span data-stu-id="89954-207">These messages usually appear when Query Store is not able toocollect new data.</span></span> 

<span data-ttu-id="89954-208">Query Store salt okunur durumda ve en iyi şekilde parametrelerinin ilk durumda olur.</span><span class="sxs-lookup"><span data-stu-id="89954-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="89954-209">Bu sorgu deposunun boyutunu artırmayı veya sorgu deposunun temizlenmesi düzeltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89954-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![qds düğmesi][8]

<span data-ttu-id="89954-211">Query Store kapalı olduğu veya parametreler en iyi şekilde oluşturulmamış ikinci durumda olur.</span><span class="sxs-lookup"><span data-stu-id="89954-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="89954-212">Aşağıdaki komutları çalıştırarak veya doğrudan portalından hello bekletme ve yakalama İlkesi ve etkinleştir Query Store değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="89954-212">You can change hello Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![qds düğmesi][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="89954-214">Önerilen bekletme ve yakalama İlkesi</span><span class="sxs-lookup"><span data-stu-id="89954-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="89954-215">Bekletme ilkeleri iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="89954-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="89954-216">En büyük boyut olduğunda otomatik olarak yakın veri temizleyecek kümesi tooAUTO ulaşıldığında boyutu - tabanlı.</span><span class="sxs-lookup"><span data-stu-id="89954-216">Size based - if set tooAUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="89954-217">Temel - saat biz ayarlanmadıysa, varsayılan olarak 30 günden eski bilgileri too30 gün anlamına gelir, Query Store alanı dışında çalıştırırsanız, siler, sorgu</span><span class="sxs-lookup"><span data-stu-id="89954-217">Time based - by default we will set it too30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="89954-218">Yakalama ilke kümesine:</span><span class="sxs-lookup"><span data-stu-id="89954-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="89954-219">**Tüm** -tüm sorgular yakalar.</span><span class="sxs-lookup"><span data-stu-id="89954-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="89954-220">**Otomatik** -sık sorgular ve önemsiz derleme ve çalıştırma süresi sorgularıyla yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="89954-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="89954-221">Eşikleri yürütme sayısı, derleme ve çalışma zamanı süresi için dahili olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="89954-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="89954-222">Merhaba varsayılan seçenek budur.</span><span class="sxs-lookup"><span data-stu-id="89954-222">This is hello default option.</span></span>
* <span data-ttu-id="89954-223">**Hiçbiri** -Query Store yeni sorgular yakalamayı durdurur ancak, çalışma zamanı istatistikleri zaten yakalanan sorgular için hala toplanır.</span><span class="sxs-lookup"><span data-stu-id="89954-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="89954-224">Tüm ilkeler tooAUTO ve temiz İlkesi too30 gün ayarı öneririz:</span><span class="sxs-lookup"><span data-stu-id="89954-224">We recommend setting all policies tooAUTO and clean policy too30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="89954-225">Query Store boyutunu artırın.</span><span class="sxs-lookup"><span data-stu-id="89954-225">Increase size of Query Store.</span></span> <span data-ttu-id="89954-226">Bu bağlantı tooa veritabanı tarafından gerçekleştirilen veren sorgu şu olabilir:</span><span class="sxs-lookup"><span data-stu-id="89954-226">This could be performed by connecting tooa database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="89954-227">Toowait istemiyorsanız, Query Store temizleyebilirsiniz ancak bu ayarları uygulamak yeni sorgular toplama sorgu deposu sonunda hale getirir.</span><span class="sxs-lookup"><span data-stu-id="89954-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want toowait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="89954-228">Aşağıdaki sorgu yürütme hello Query Store tüm geçerli bilgileri silinmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="89954-228">Executing following query will delete all current information in hello Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="89954-229">Özet</span><span class="sxs-lookup"><span data-stu-id="89954-229">Summary</span></span>
<span data-ttu-id="89954-230">Sorgu performansı öngörüleri sorgu iş yükü hello etkisini ve toodatabase kaynak tüketimini ilişkilendirilme şekli anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="89954-230">Query Performance Insight helps you understand hello impact of your query workload and how it relates toodatabase resource consumption.</span></span> <span data-ttu-id="89954-231">Bu özellik, kaynak tüketen sorguları hello üst hakkında bilgi edinin ve bir sorun haline gelmeden önce hello olanları toofix kolayca tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="89954-231">With this feature, you will learn about hello top consuming queries, and easily identify hello ones toofix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89954-232">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="89954-232">Next steps</span></span>
<span data-ttu-id="89954-233">SQL veritabanınız hello performansını iyileştirme konusunda ek öneriler için tıklatın [önerileri](sql-database-advisor.md) hello üzerinde **sorgu performansı öngörüleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="89954-233">For additional recommendations about improving hello performance of your SQL database, click [Recommendations](sql-database-advisor.md) on hello **Query Performance Insight** blade.</span></span>

![Performans Danışmanı](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png


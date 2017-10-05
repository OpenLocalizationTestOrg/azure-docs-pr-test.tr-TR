---
title: "Azure Application Insights uygulama eşlemesinde | Microsoft Docs"
description: "Uygulama bileşenleri arasındaki bağımlılıkları görsel sunumu KPI'ları ve uyarılarla etiketli."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 207526b7a675f92134d045ebefb9a372749bce92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="3fd66-103">Application ınsights'ta uygulama eşlemesi</span><span class="sxs-lookup"><span data-stu-id="3fd66-103">Application Map in Application Insights</span></span>
<span data-ttu-id="3fd66-104">İçinde [Azure Application Insights](app-insights-overview.md), uygulama eşlemesi olan uygulama bileşenlerinizin bağımlılık ilişkilerini visual düzeni.</span><span class="sxs-lookup"><span data-stu-id="3fd66-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of the dependency relationships of your application components.</span></span> <span data-ttu-id="3fd66-105">Her bileşen yük, performans, hataları ve Uyarıları gibi bir performans sorunu veya hatası neden herhangi bir bileşeni keşfetmenize yardımcı olmak için KPI'ları gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-105">Each component shows KPIs such as load, performance, failures, and alerts, to help you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="3fd66-106">Aracılığıyla herhangi bir bileşeni Application Insights olaylarını gibi daha ayrıntılı tanılama tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd66-106">You can click through from any component to more detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="3fd66-107">Uygulamanızı Azure hizmetlerini kullanıyorsa, üzerinden SQL Database Advisor önerileri gibi Azure tanılama tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd66-107">If your app uses Azure services, you can also click through to Azure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="3fd66-108">Diğer grafikler gibi bir uygulama eşlemesi tam olarak işlevsel olduğu Azure panoya sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd66-108">Like other charts, you can pin an application map to the Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-the-application-map"></a><span data-ttu-id="3fd66-109">Uygulama eşlemesi açın</span><span class="sxs-lookup"><span data-stu-id="3fd66-109">Open the application map</span></span>
<span data-ttu-id="3fd66-110">Uygulamanız için genel bakış dikey penceresinden harita açın:</span><span class="sxs-lookup"><span data-stu-id="3fd66-110">Open the map from the overview blade for your application:</span></span>

![Uygulama Eşlem'i açın](./media/app-insights-app-map/01.png)

![Uygulama eşleme](./media/app-insights-app-map/02.png)

<span data-ttu-id="3fd66-113">Harita gösterir:</span><span class="sxs-lookup"><span data-stu-id="3fd66-113">The map shows:</span></span>

* <span data-ttu-id="3fd66-114">Kullanılabilirlik testleri</span><span class="sxs-lookup"><span data-stu-id="3fd66-114">Availability tests</span></span>
* <span data-ttu-id="3fd66-115">İstemci tarafı bileşen (JavaScript SDK'sı ile izlenen)</span><span class="sxs-lookup"><span data-stu-id="3fd66-115">Client-side component (monitored with the JavaScript SDK)</span></span>
* <span data-ttu-id="3fd66-116">Sunucu tarafı bileşeni</span><span class="sxs-lookup"><span data-stu-id="3fd66-116">Server-side component</span></span>
* <span data-ttu-id="3fd66-117">İstemci ve sunucu bileşenleri bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="3fd66-117">Dependencies of the client and server components</span></span>

<span data-ttu-id="3fd66-118">Genişletme ve bağımlılık bağlantı gruplarına daraltma:</span><span class="sxs-lookup"><span data-stu-id="3fd66-118">You can expand and collapse dependency link groups:</span></span>

![Daralt](./media/app-insights-app-map/03.png)

<span data-ttu-id="3fd66-120">Bir tür (SQL, HTTP vb.) pek çok bağımlılık varsa, bunlar gruplandırılmış görünebilir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![Gruplandırılmış bağımlılıkları](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="3fd66-122">Nokta sorunları</span><span class="sxs-lookup"><span data-stu-id="3fd66-122">Spot problems</span></span>
<span data-ttu-id="3fd66-123">Her düğüm bu bileşen için yükleme, performans ve hata hızlarını gibi ilgili performans göstergelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-123">Each node has relevant performance indicators, such as the load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="3fd66-124">Uyarı simgeleri olası sorunlar vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="3fd66-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="3fd66-125">Turuncu bir uyarı isteklerinde sayfa görünümleri veya bağımlılık çağrıları hataları olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="3fd66-126">Kırmızı bir hata oranı %5 yukarıda anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="3fd66-127">Bu eşikler ayarlamak istiyorsanız, Seçenekleri'ni açın.</span><span class="sxs-lookup"><span data-stu-id="3fd66-127">If you want to adjust these thresholds, open Options.</span></span>

![hata simgeleri](./media/app-insights-app-map/04.png)

<span data-ttu-id="3fd66-129">Etkin Göster yukarı da uyarır:</span><span class="sxs-lookup"><span data-stu-id="3fd66-129">Active alerts also show up:</span></span> 

![Etkin uyarılar](./media/app-insights-app-map/05.png)

<span data-ttu-id="3fd66-131">SQL Azure kullanırsanız, ne zaman gösteren bir simge yoktur nasıl performansını iyileştirebilir ilişkin öneriler vardır.</span><span class="sxs-lookup"><span data-stu-id="3fd66-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Azure önerisi](./media/app-insights-app-map/06.png)

<span data-ttu-id="3fd66-133">Daha fazla bilgi almak için herhangi bir simgesini tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3fd66-133">Click any icon to get more details:</span></span>

![Azure önerisi](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="3fd66-135">Tanılama geçişli tıklatma</span><span class="sxs-lookup"><span data-stu-id="3fd66-135">Diagnostic click through</span></span>
<span data-ttu-id="3fd66-136">Harita üzerinde düğümlerinin her biri için tanılama aracılığıyla hedeflenen tıklatın sunar.</span><span class="sxs-lookup"><span data-stu-id="3fd66-136">Each of the nodes on the map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="3fd66-137">Seçenekler düğüm türüne bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-137">The options vary depending on the type of the node.</span></span>

![Sunucu seçenekleri](./media/app-insights-app-map/09.png)

<span data-ttu-id="3fd66-139">Azure üzerinde barındırılan bileşenler için bunları doğrudan bağlantıların seçenekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-139">For components that are hosted in Azure, the options include direct links to them.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="3fd66-140">Filtreler ve zaman aralığı</span><span class="sxs-lookup"><span data-stu-id="3fd66-140">Filters and time range</span></span>
<span data-ttu-id="3fd66-141">Varsayılan olarak, seçilen zaman aralığı için kullanılabilir tüm verileri harita özetler.</span><span class="sxs-lookup"><span data-stu-id="3fd66-141">By default, the map summarizes all the data available for the chosen time range.</span></span> <span data-ttu-id="3fd66-142">Ancak, yalnızca belirli işlem adları veya bağımlılıkları içerecek şekilde filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd66-142">But you can filter it to include only specific operation names or dependencies.</span></span>

* <span data-ttu-id="3fd66-143">İşlem adı: Bu sayfa görünümleri ve sunucu tarafı istek türleri içerir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="3fd66-144">Bu seçenek, yalnızca seçili işlemler için istemci/sunucu-tarafı düğümde KPI eşlemesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-144">With this option, the map shows the KPI on the server/client-side node for the selected operations only.</span></span> <span data-ttu-id="3fd66-145">Bu belirli işlemler bağlamında adlı bağımlılıkları gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-145">It shows the dependencies called in the context of those specific operations.</span></span>
* <span data-ttu-id="3fd66-146">Bağımlılık temel name: Bu, sunucu tarafı bağımlılıkları ve AJAX tarayıcı bağımlılıklar içerir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-146">Dependency base name: This includes the AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="3fd66-147">Özel bağımlılık telemetrisi TrackDependency API ile rapor ise, bunlar ayrıca burada görünür.</span><span class="sxs-lookup"><span data-stu-id="3fd66-147">If you report custom dependency telemetry with the TrackDependency API, they also appear here.</span></span> <span data-ttu-id="3fd66-148">Haritada göstermek için bağımlılıklar seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd66-148">You can select the dependencies to show on the map.</span></span> <span data-ttu-id="3fd66-149">Şu anda bu seçimi sunucu tarafı istekleri ya da istemci-tarafı sayfa görünümleri filtre uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="3fd66-149">Currently this selection does not filter the server-side requests, or the client-side page views.</span></span>

![Filtrelerini ayarlama](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="3fd66-151">Filtreleri Kaydet</span><span class="sxs-lookup"><span data-stu-id="3fd66-151">Save filters</span></span>
<span data-ttu-id="3fd66-152">Filtre uygulanmış bir görünüm üzerine uyguladığınız filtreleri Kaydet sabitlemek bir [Pano](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="3fd66-152">To save the filters you have applied, pin the filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Panoya sabitle](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="3fd66-154">Hata bölmesi</span><span class="sxs-lookup"><span data-stu-id="3fd66-154">Error pane</span></span>
<span data-ttu-id="3fd66-155">Harita düğümünde tıkladığınızda bir hata bölmesi sağ taraftaki hataları bu düğüm için özetleme görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-155">When you click a node in the map, an error pane is displayed on the right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="3fd66-156">Hataları ilk işlem Kimliğine göre gruplandırılmış ve sorun kimliğine göre gruplandırılmış</span><span class="sxs-lookup"><span data-stu-id="3fd66-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Hata bölmesi](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="3fd66-158">Bir arıza tıklatarak bu hatanın en son örneğine alır.</span><span class="sxs-lookup"><span data-stu-id="3fd66-158">Clicking on a failure takes you to the most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="3fd66-159">Kaynak durumu</span><span class="sxs-lookup"><span data-stu-id="3fd66-159">Resource health</span></span>
<span data-ttu-id="3fd66-160">Bazı kaynak türleri için kaynak durumu hata bölmesinin üst kısmında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-160">For some resource types, resource health is displayed at the top of the error pane.</span></span> <span data-ttu-id="3fd66-161">Örneğin, bir SQL düğümü tıklatarak veritabanı sistem durumu ve puanlı herhangi bir uyarı gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-161">For example, clicking a SQL node will show the database health and any alerts that have fired.</span></span>

![Kaynak durumu](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="3fd66-163">Bu kaynak için standart genel bakış ölçümlerini görüntülemek için kaynak adı tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd66-163">You can click the resource name to view standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="3fd66-164">Uçtan uca sistem uygulama eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="3fd66-164">End-to-end system app maps</span></span>

<span data-ttu-id="3fd66-165">*SDK'sı sürüm 2.3 veya üstü gerektirir*</span><span class="sxs-lookup"><span data-stu-id="3fd66-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="3fd66-166">Uygulamanız çeşitli bileşenleri - Örneğin, bir arka uç hizmeti Ayrıca web uygulaması'na - sahip sonra bunları gösterebilir tüm bir tümleşik uygulama harita üzerinde.</span><span class="sxs-lookup"><span data-stu-id="3fd66-166">If your application has several components - for example, a back-end service in addition to the web app - then you can show them all on one integrated app map.</span></span>

![Filtrelerini ayarlama](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="3fd66-168">Uygulama harita yüklü Application Insights SDK'sı ile sunucu arasında yapılan tüm HTTP bağımlılık çağrıları izleyerek sunucu düğümleri bulur.</span><span class="sxs-lookup"><span data-stu-id="3fd66-168">The app map finds server nodes by following any HTTP dependency calls made between servers with the Application Insights SDK installed.</span></span> <span data-ttu-id="3fd66-169">Her bir Application Insights kaynağı, bir sunucu içeren varsayılır.</span><span class="sxs-lookup"><span data-stu-id="3fd66-169">Each Application Insights resource is assumed to contain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="3fd66-170">Birden çok rol uygulama eşleme (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="3fd66-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="3fd66-171">Önizleme birden çok rol uygulama eşleme özelliğini uygulama eşlemesi aynı Application Insights kaynağına veri gönderilirken birden fazla sunucuyla sayesinde / izleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="3fd66-171">The preview multi-role app map feature allows you to use the app map with multiple servers sending data to the same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="3fd66-172">Harita sunucuları, telemetri öğeler üzerinde cloud_RoleName özelliği tarafından ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="3fd66-172">Servers in the map are segmented by the cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="3fd66-173">Ayarlama *birden çok rol uygulama eşlemesi* için *üzerinde* bu yapılandırmayı etkinleştirmek için önizlemeleri dikey penceresinden.</span><span class="sxs-lookup"><span data-stu-id="3fd66-173">Set *Multi-role Application Map* to *On* from the Previews blade to enable this configuration.</span></span>

<span data-ttu-id="3fd66-174">Bu yaklaşım, bir mikro hizmetler uygulamasındaki ya da tek bir Application Insights kaynağı içinde birden çok sunucudaki olayları ilişkilendirmek istediğiniz diğer senaryolarda istenebilir.</span><span class="sxs-lookup"><span data-stu-id="3fd66-174">This approach may be desired in a micro-services application, or in other scenarios where you want to correlate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="3fd66-175">Video</span><span class="sxs-lookup"><span data-stu-id="3fd66-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="3fd66-176">Geri Bildirim</span><span class="sxs-lookup"><span data-stu-id="3fd66-176">Feedback</span></span>
<span data-ttu-id="3fd66-177">Portal geri bildirimi seçeneği aracılığıyla geri bildirim sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3fd66-177">Please provide feedback through the portal feedback option.</span></span>

![MapLink-1 görüntüsü](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="3fd66-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3fd66-179">Next steps</span></span>

* [<span data-ttu-id="3fd66-180">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3fd66-180">Azure portal</span></span>](https://portal.azure.com)

---
title: "Azure Application Insights eşlemesinde aaaApplication | Microsoft Docs"
description: "Uygulama bileşenleri arasında hello bağımlılıkları görsel sunumu KPI'ları ve uyarılarla etiketli."
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
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="008a8-103">Application ınsights'ta uygulama eşlemesi</span><span class="sxs-lookup"><span data-stu-id="008a8-103">Application Map in Application Insights</span></span>
<span data-ttu-id="008a8-104">İçinde [Azure Application Insights](app-insights-overview.md), uygulama eşlemesi olan uygulama bileşenlerinizin hello bağımlılık ilişkilerini visual düzeni.</span><span class="sxs-lookup"><span data-stu-id="008a8-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of hello dependency relationships of your application components.</span></span> <span data-ttu-id="008a8-105">Her bileşen KPI'ları bir performans sorunu veya hatası neden herhangi bir bileşeni Bul gibi yük, performans, hataları ve Uyarıları, toohelp gösterir.</span><span class="sxs-lookup"><span data-stu-id="008a8-105">Each component shows KPIs such as load, performance, failures, and alerts, toohelp you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="008a8-106">Hiçbir bileşen toomore aracılığıyla tıklatabilirsiniz ayrıntılı tanılama, Application Insights olaylarını gibi.</span><span class="sxs-lookup"><span data-stu-id="008a8-106">You can click through from any component toomore detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="008a8-107">Uygulamanızı Azure hizmetlerini kullanıyorsa, SQL veritabanı Danışmanı önerileri gibi tooAzure tanılama aracılığıyla tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="008a8-107">If your app uses Azure services, you can also click through tooAzure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="008a8-108">Diğer grafikler gibi bir uygulama eşlemesi toohello tam olarak işlevsel olduğu Azure Pano sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="008a8-108">Like other charts, you can pin an application map toohello Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-hello-application-map"></a><span data-ttu-id="008a8-109">Açık hello uygulama eşlemesi</span><span class="sxs-lookup"><span data-stu-id="008a8-109">Open hello application map</span></span>
<span data-ttu-id="008a8-110">Uygulamanız için hello genel bakış dikey penceresinden açık hello eşleyin:</span><span class="sxs-lookup"><span data-stu-id="008a8-110">Open hello map from hello overview blade for your application:</span></span>

![Uygulama Eşlem'i açın](./media/app-insights-app-map/01.png)

![Uygulama eşleme](./media/app-insights-app-map/02.png)

<span data-ttu-id="008a8-113">Merhaba eşlemesini gösterir:</span><span class="sxs-lookup"><span data-stu-id="008a8-113">hello map shows:</span></span>

* <span data-ttu-id="008a8-114">Kullanılabilirlik testleri</span><span class="sxs-lookup"><span data-stu-id="008a8-114">Availability tests</span></span>
* <span data-ttu-id="008a8-115">İstemci tarafı bileşen (Merhaba JavaScript SDK'sı ile izlenen)</span><span class="sxs-lookup"><span data-stu-id="008a8-115">Client-side component (monitored with hello JavaScript SDK)</span></span>
* <span data-ttu-id="008a8-116">Sunucu tarafı bileşeni</span><span class="sxs-lookup"><span data-stu-id="008a8-116">Server-side component</span></span>
* <span data-ttu-id="008a8-117">Merhaba istemci ve sunucu bileşenleri bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="008a8-117">Dependencies of hello client and server components</span></span>

<span data-ttu-id="008a8-118">Genişletme ve bağımlılık bağlantı gruplarına daraltma:</span><span class="sxs-lookup"><span data-stu-id="008a8-118">You can expand and collapse dependency link groups:</span></span>

![Daralt](./media/app-insights-app-map/03.png)

<span data-ttu-id="008a8-120">Bir tür (SQL, HTTP vb.) pek çok bağımlılık varsa, bunlar gruplandırılmış görünebilir.</span><span class="sxs-lookup"><span data-stu-id="008a8-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![Gruplandırılmış bağımlılıkları](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="008a8-122">Nokta sorunları</span><span class="sxs-lookup"><span data-stu-id="008a8-122">Spot problems</span></span>
<span data-ttu-id="008a8-123">Her düğüm bu bileşen için hello yük, performans ve hata hızlarını gibi ilgili performans göstergelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="008a8-123">Each node has relevant performance indicators, such as hello load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="008a8-124">Uyarı simgeleri olası sorunlar vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="008a8-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="008a8-125">Turuncu bir uyarı isteklerinde sayfa görünümleri veya bağımlılık çağrıları hataları olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="008a8-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="008a8-126">Kırmızı bir hata oranı %5 yukarıda anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="008a8-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="008a8-127">Bu eşikler tooadjust istiyorsanız Seçenekleri'ni açın.</span><span class="sxs-lookup"><span data-stu-id="008a8-127">If you want tooadjust these thresholds, open Options.</span></span>

![hata simgeleri](./media/app-insights-app-map/04.png)

<span data-ttu-id="008a8-129">Etkin Göster yukarı da uyarır:</span><span class="sxs-lookup"><span data-stu-id="008a8-129">Active alerts also show up:</span></span> 

![Etkin uyarılar](./media/app-insights-app-map/05.png)

<span data-ttu-id="008a8-131">SQL Azure kullanırsanız, ne zaman gösteren bir simge yoktur nasıl performansını iyileştirebilir ilişkin öneriler vardır.</span><span class="sxs-lookup"><span data-stu-id="008a8-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Azure önerisi](./media/app-insights-app-map/06.png)

<span data-ttu-id="008a8-133">Tüm simge tooget daha fazla ayrıntı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="008a8-133">Click any icon tooget more details:</span></span>

![Azure önerisi](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="008a8-135">Tanılama geçişli tıklatma</span><span class="sxs-lookup"><span data-stu-id="008a8-135">Diagnostic click through</span></span>
<span data-ttu-id="008a8-136">Merhaba haritaya hello düğümlerinin her biri için tanılama aracılığıyla hedeflenen tıklatın sunar.</span><span class="sxs-lookup"><span data-stu-id="008a8-136">Each of hello nodes on hello map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="008a8-137">Merhaba seçenekler hello düğümü hello türüne bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="008a8-137">hello options vary depending on hello type of hello node.</span></span>

![Sunucu seçenekleri](./media/app-insights-app-map/09.png)

<span data-ttu-id="008a8-139">Azure üzerinde barındırılan bileşenleri için doğrudan bağlantılar toothem hello seçenekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="008a8-139">For components that are hosted in Azure, hello options include direct links toothem.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="008a8-140">Filtreler ve zaman aralığı</span><span class="sxs-lookup"><span data-stu-id="008a8-140">Filters and time range</span></span>
<span data-ttu-id="008a8-141">Varsayılan olarak, zaman aralığı seçilen hello için kullanılabilir tüm hello veri hello harita özetler.</span><span class="sxs-lookup"><span data-stu-id="008a8-141">By default, hello map summarizes all hello data available for hello chosen time range.</span></span> <span data-ttu-id="008a8-142">Ancak tooinclude yalnızca belirli işlem adları veya bağımlılıkları filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="008a8-142">But you can filter it tooinclude only specific operation names or dependencies.</span></span>

* <span data-ttu-id="008a8-143">İşlem adı: Bu sayfa görünümleri ve sunucu tarafı istek türleri içerir.</span><span class="sxs-lookup"><span data-stu-id="008a8-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="008a8-144">Bu seçenek ile yalnızca seçili hello işlemleri için hello istemci/sunucu-tarafı düğümde KPI hello harita gösterir hello.</span><span class="sxs-lookup"><span data-stu-id="008a8-144">With this option, hello map shows hello KPI on hello server/client-side node for hello selected operations only.</span></span> <span data-ttu-id="008a8-145">Bu belirli işlemler hello bağlamında adlı hello bağımlılıkları gösterir.</span><span class="sxs-lookup"><span data-stu-id="008a8-145">It shows hello dependencies called in hello context of those specific operations.</span></span>
* <span data-ttu-id="008a8-146">Bağımlılık temel name: Bu hello AJAX tarayıcı ve sunucu tarafı iç bağımlılıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="008a8-146">Dependency base name: This includes hello AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="008a8-147">Özel bağımlılık telemetri hello TrackDependency API ile rapor ise, bunlar ayrıca burada görünür.</span><span class="sxs-lookup"><span data-stu-id="008a8-147">If you report custom dependency telemetry with hello TrackDependency API, they also appear here.</span></span> <span data-ttu-id="008a8-148">Merhaba bağımlılıkları tooshow hello haritaya seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="008a8-148">You can select hello dependencies tooshow on hello map.</span></span> <span data-ttu-id="008a8-149">Şu anda bu seçimi hello sunucu tarafı istekleri ya da hello istemci-tarafı sayfa görünümleri filtre uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="008a8-149">Currently this selection does not filter hello server-side requests, or hello client-side page views.</span></span>

![Filtrelerini ayarlama](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="008a8-151">Filtreleri Kaydet</span><span class="sxs-lookup"><span data-stu-id="008a8-151">Save filters</span></span>
<span data-ttu-id="008a8-152">uyguladığınız toosave hello filtreleri PIN hello filtrelenmiş görünüm üzerine bir [Pano](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="008a8-152">toosave hello filters you have applied, pin hello filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![PIN toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="008a8-154">Hata bölmesi</span><span class="sxs-lookup"><span data-stu-id="008a8-154">Error pane</span></span>
<span data-ttu-id="008a8-155">Merhaba eşlemesindeki bir düğümüne tıkladığınızda bir hata bölmesi hataları bu düğüm için özetleme hello sağ tarafında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="008a8-155">When you click a node in hello map, an error pane is displayed on hello right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="008a8-156">Hataları ilk işlem Kimliğine göre gruplandırılmış ve sorun kimliğine göre gruplandırılmış</span><span class="sxs-lookup"><span data-stu-id="008a8-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Hata bölmesi](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="008a8-158">Bir arıza tıklamak bu hatanın en son örnek toohello götürür.</span><span class="sxs-lookup"><span data-stu-id="008a8-158">Clicking on a failure takes you toohello most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="008a8-159">Kaynak durumu</span><span class="sxs-lookup"><span data-stu-id="008a8-159">Resource health</span></span>
<span data-ttu-id="008a8-160">Bazı kaynak türleri için kaynak durumu hello hello hata bölmesinin üst kısmında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="008a8-160">For some resource types, resource health is displayed at hello top of hello error pane.</span></span> <span data-ttu-id="008a8-161">Örneğin, bir SQL düğümü tıklatarak hello veritabanı sistem durumu ve puanlı herhangi bir uyarı gösterir.</span><span class="sxs-lookup"><span data-stu-id="008a8-161">For example, clicking a SQL node will show hello database health and any alerts that have fired.</span></span>

![Kaynak durumu](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="008a8-163">Bu kaynak için hello kaynak adı tooview standart genel bakış ölçümleri tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="008a8-163">You can click hello resource name tooview standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="008a8-164">Uçtan uca sistem uygulama eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="008a8-164">End-to-end system app maps</span></span>

<span data-ttu-id="008a8-165">*SDK'sı sürüm 2.3 veya üstü gerektirir*</span><span class="sxs-lookup"><span data-stu-id="008a8-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="008a8-166">Çeşitli bileşenleri - uygulamanız varsa, örneğin, bir arka uç Hizmeti ayrıca toohello web uygulaması - sonra gösterebilir bir tümleşik uygulama harita üzerinde tüm bunları.</span><span class="sxs-lookup"><span data-stu-id="008a8-166">If your application has several components - for example, a back-end service in addition toohello web app - then you can show them all on one integrated app map.</span></span>

![Filtrelerini ayarlama](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="008a8-168">Merhaba uygulama harita hello Application Insights SDK'sı yüklü olan sunucuları arasında yapılan tüm HTTP bağımlılık çağrıları izleyerek sunucu düğümleri bulur.</span><span class="sxs-lookup"><span data-stu-id="008a8-168">hello app map finds server nodes by following any HTTP dependency calls made between servers with hello Application Insights SDK installed.</span></span> <span data-ttu-id="008a8-169">Her bir Application Insights kaynağı toocontain bir sunucu olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="008a8-169">Each Application Insights resource is assumed toocontain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="008a8-170">Birden çok rol uygulama eşleme (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="008a8-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="008a8-171">Merhaba Önizleme birden çok rol uygulama eşleme özelliğini sağlar toouse hello uygulama harita veri toohello gönderme birden çok sunucu ile aynı Application Insights kaynağı / izleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="008a8-171">hello preview multi-role app map feature allows you toouse hello app map with multiple servers sending data toohello same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="008a8-172">Hello eşlemesindeki sunucuları, telemetri öğeler üzerinde hello cloud_RoleName özelliği tarafından ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="008a8-172">Servers in hello map are segmented by hello cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="008a8-173">Ayarlama *birden çok rol uygulama eşlemesi* çok*üzerinde* gelen önizlemeleri dikey tooenable bu yapılandırma hello.</span><span class="sxs-lookup"><span data-stu-id="008a8-173">Set *Multi-role Application Map* too*On* from hello Previews blade tooenable this configuration.</span></span>

<span data-ttu-id="008a8-174">Bu yaklaşım, bir mikro hizmetler uygulamasındaki ya da tek bir Application Insights kaynağı içinde birden çok sunucu boyunca toocorrelate olayları istediğiniz diğer senaryolarda istenebilir.</span><span class="sxs-lookup"><span data-stu-id="008a8-174">This approach may be desired in a micro-services application, or in other scenarios where you want toocorrelate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="008a8-175">Video</span><span class="sxs-lookup"><span data-stu-id="008a8-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="008a8-176">Geri Bildirim</span><span class="sxs-lookup"><span data-stu-id="008a8-176">Feedback</span></span>
<span data-ttu-id="008a8-177">Lütfen hello portal geri bildirimi seçeneği aracılığıyla geri bildirim sağlayın.</span><span class="sxs-lookup"><span data-stu-id="008a8-177">Please provide feedback through hello portal feedback option.</span></span>

![MapLink-1 görüntüsü](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="008a8-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="008a8-179">Next steps</span></span>

* [<span data-ttu-id="008a8-180">Azure portal</span><span class="sxs-lookup"><span data-stu-id="008a8-180">Azure portal</span></span>](https://portal.azure.com)

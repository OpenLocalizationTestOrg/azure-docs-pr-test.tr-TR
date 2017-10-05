---
title: "Power BI Embedded ile satır düzeyi güvenliği"
description: "Satır düzeyi güvenlik Power BI Embedded ile ilgili ayrıntıları"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 1cde5b9ee4c716af07d427d4d0eb3f0775d456ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="9ae48-103">Power BI Embedded ile satır düzeyinde güvenlik</span><span class="sxs-lookup"><span data-stu-id="9ae48-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="9ae48-104">Satır düzeyi güvenlik (RLS), rapor veya veri kümesi, birden çok farklı kullanıcıların aynı raporun tüm görme farklı veriler kullanmasına izin vermeyi içinde belirli veri kullanıcı erişimi sınırlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9ae48-104">Row level security (RLS) can be used to restrict user access to particular data within a report or dataset, allowing for multiple different users to use the same report while all seeing different data.</span></span> <span data-ttu-id="9ae48-105">Power BI Embedded artık RLS ile yapılandırılmış veri kümelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="9ae48-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="9ae48-106">RLS yararlanmak için üç ana kavramı anlamak önemlidir; Kullanıcıları, rolleri ve kuralları.</span><span class="sxs-lookup"><span data-stu-id="9ae48-106">In order to take advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="9ae48-107">Her daha yakın bir göz atalım:</span><span class="sxs-lookup"><span data-stu-id="9ae48-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="9ae48-108">**Kullanıcıların** – Bu gerçek son kullanıcılar görüntülemekte olduğunuz raporlar.</span><span class="sxs-lookup"><span data-stu-id="9ae48-108">**Users** –  These are the actual end-users viewing reports.</span></span> <span data-ttu-id="9ae48-109">Power BI Embedded içinde kullanıcıların bir uygulama belirteci username özelliği tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9ae48-109">In Power BI Embedded, users are identified by the username property in an App Token.</span></span>

<span data-ttu-id="9ae48-110">**Rolleri** – kullanıcıları rollere ait.</span><span class="sxs-lookup"><span data-stu-id="9ae48-110">**Roles** – Users belong to roles.</span></span> <span data-ttu-id="9ae48-111">Bir rolü kuralları için bir kapsayıcı ve bir şey "Satış Yöneticisi" veya "Satış Temsilcisi" gibi adlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="9ae48-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="9ae48-112">Power BI Embedded içinde kullanıcıların bir uygulama belirteci roller özelliği tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9ae48-112">In Power BI Embedded, users are identified by the roles property in an App Token.</span></span>

<span data-ttu-id="9ae48-113">**Kuralları** – rollerin kurallar vardır ve verilere uygulanacak giderek gerçek filtreler bu kurallardır.</span><span class="sxs-lookup"><span data-stu-id="9ae48-113">**Rules** – Roles have rules, and those rules are the actual filters that are going to be applied to the data.</span></span> <span data-ttu-id="9ae48-114">Bu kadar basit olabilir "Ülke = tr" veya daha fazla dinamik bir şey.</span><span class="sxs-lookup"><span data-stu-id="9ae48-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="9ae48-115">Örnek</span><span class="sxs-lookup"><span data-stu-id="9ae48-115">Example</span></span>

<span data-ttu-id="9ae48-116">Bu makalede kalanı için RLS yazma ve, katıştırılmış bir uygulama içinde kullanma örneği sağlarız.</span><span class="sxs-lookup"><span data-stu-id="9ae48-116">For the rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="9ae48-117">Bizim örneğimizde kullanan [Retail Analysis örnek](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX dosyası.</span><span class="sxs-lookup"><span data-stu-id="9ae48-117">Our example uses the [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="9ae48-118">Retail Analysis örneğimizde bir belirli perakende zincirindeki tüm depoları için satış gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ae48-118">Our Retail Analysis sample shows sales for all the stores in a particular retail chain.</span></span> <span data-ttu-id="9ae48-119">Hangi bölge olsun Yöneticisi oturum açtığında ve rapor görünümleri RLS, bunlar aynı verileri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9ae48-119">Without RLS, no matter which district manager signs in and views the report, they’ll see the same data.</span></span> <span data-ttu-id="9ae48-120">Üst düzey yönetim her bölge yöneticisi yalnızca satış yönettikleri depolarının görmeniz gerekir ve bunu yapmak için biz RLS kullanabilirsiniz belirledi.</span><span class="sxs-lookup"><span data-stu-id="9ae48-120">Senior management has determined each district manager should only see the sales for the stores they manage, and to do this, we can use RLS.</span></span>

<span data-ttu-id="9ae48-121">RLS, Power BI Desktop'ta yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="9ae48-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="9ae48-122">Rapor ve veri kümesi açıldığında, biz şema görmek için diyagram görünümüne geçiş yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae48-122">When the dataset and report are opened, we can switch to diagram view to see the schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="9ae48-123">Bu şema ile fark birkaç şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9ae48-123">Here are a few things to notice with this schema:</span></span>

* <span data-ttu-id="9ae48-124">Tüm ölçüleri, ister **toplam satış**, depolanmış **satış** Olgu Tablosu.</span><span class="sxs-lookup"><span data-stu-id="9ae48-124">All measures, like **Total Sales**, are stored in the **Sales** fact table.</span></span>
* <span data-ttu-id="9ae48-125">Dört ek ilgili boyut tabloları vardır: **öğesi**, **zaman**, **deposu**, ve **bölgesi**.</span><span class="sxs-lookup"><span data-stu-id="9ae48-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="9ae48-126">İlişki satırlarındaki okları filtreleri başka bir tablodan akış hangi yolu belirtin.</span><span class="sxs-lookup"><span data-stu-id="9ae48-126">The arrows on the relationship lines indicate which way filters can flow from one table to another.</span></span> <span data-ttu-id="9ae48-127">Örneğin, bir filtre yerleştirildiği **zaman [Date]**, geçerli şemada, yalnızca değerleri aşağı filtreler **satış** tablo.</span><span class="sxs-lookup"><span data-stu-id="9ae48-127">For example, if a filter is placed on **Time[Date]**, in the current schema it would only filter down values in the **Sales** table.</span></span> <span data-ttu-id="9ae48-128">Tüm okları ilişki satırlarındaki satış tabloya ve değil hemen noktası bu yana başka bir tablo bu filtrenin etkilenecek.</span><span class="sxs-lookup"><span data-stu-id="9ae48-128">No other tables would be affected by this filter since all of the arrows on the relationship lines point to the sales table and not away.</span></span>
* <span data-ttu-id="9ae48-129">**Bölge** tablo her bölge için yöneticisi olan gösterir:</span><span class="sxs-lookup"><span data-stu-id="9ae48-129">The **District** table indicates who the manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="9ae48-130">Biz bir filtre uygularsanız, bu şemaya göre **bölge yöneticisi** bölge tablodaki sütun ve bu filtre raporu görüntüleme kullanıcı eşleşiyorsa, bu filtre da aşağı süzer **deposu** ve  **Satış** yalnızca tablolara Yöneticisi bu belirli bölge verilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ae48-130">Based on this schema, if we apply a filter to the **District Manager** column in the District table, and if that filter matches the user viewing the report, that filter will also filter down the **Store** and **Sales** tables to only show data for that particular district manager.</span></span>

<span data-ttu-id="9ae48-131">İşte nasıl:</span><span class="sxs-lookup"><span data-stu-id="9ae48-131">Here’s how:</span></span>

1. <span data-ttu-id="9ae48-132">Modelleme sekmesinde, **Rolleri Yönet**.</span><span class="sxs-lookup"><span data-stu-id="9ae48-132">On the Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="9ae48-133">Adlı yeni bir rol oluşturmak **Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="9ae48-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="9ae48-134">İçinde **bölge** tablo aşağıdaki DAX ifadesi girin: **[Bölge Yöneticisi] USERNAME() =**</span><span class="sxs-lookup"><span data-stu-id="9ae48-134">In the **District** table enter the following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="9ae48-135">Kuralları çalıştığınız, üzerinde emin olmak için **modelleme** sekmesini tıklatın, **görünüm rolleri olarak**ve ardından aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="9ae48-135">To make sure the rules are working, on the **Modeling** tab, click **View as Roles**, and then enter the following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="9ae48-136">Sanki olarak imzalanmış raporlar artık verileri Göster **Barış Ma**.</span><span class="sxs-lookup"><span data-stu-id="9ae48-136">The reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="9ae48-137">Burada, yaptığımız şekilde filtre uygulama filtre uygulayarak tüm kayıtları aşağı **bölge**, **deposu**, ve **satış** tabloları.</span><span class="sxs-lookup"><span data-stu-id="9ae48-137">Applying the filter, the way we did here, will filter down all records in the **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="9ae48-138">Ancak, filtre yönünü arasındaki ilişkileri nedeniyle **satış** ve **zaman**, **satış** ve **öğesi**ve **Öğesi** ve **zaman** tabloları aşağı filtrelenmez.</span><span class="sxs-lookup"><span data-stu-id="9ae48-138">However, because of the filter direction on the relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="9ae48-139">Bu gereksinim için Tamam olabilir, ancak bunlar Satış yok öğeleri görmek için yöneticileri olmasını istemezseniz, biz çift yönlü çapraz filtreleme ilişkisi için açın ve her iki yönde güvenlik filtresi akış.</span><span class="sxs-lookup"><span data-stu-id="9ae48-139">That may be ok for this requirement, however, if we don’t want managers to see items for which they don’t have any sales, we could turn on bidirectional cross-filtering for the relationship and flow the security filter in both directions.</span></span> <span data-ttu-id="9ae48-140">Bu arasındaki ilişkiyi düzenleyerek yapılabilir **satış** ve **öğesi**, şöyle:</span><span class="sxs-lookup"><span data-stu-id="9ae48-140">This can be done by editing the relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="9ae48-141">Şimdi, filtreleri Ayrıca satış tablosundan akabilir **öğesi** tablosu:</span><span class="sxs-lookup"><span data-stu-id="9ae48-141">Now, filters can also flow from the Sales table to the **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="9ae48-142">Verileriniz için DirectQuery modu kullanıyorsanız, bu iki seçenek seçerek çift yönlü çapraz filtreleme etkinleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="9ae48-142">If you're using DirectQuery mode for your data, you will need to enable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="9ae48-143">**Dosya** -> **seçenekleri ve ayarları** -> **Önizleme özellikleri** -> **çapraz için her iki yönde filtreleme etkinleştir DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="9ae48-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="9ae48-144">**Dosya** -> **seçenekleri ve ayarları** -> **DirectQuery** -> **DirectQuerymodundaKısıtlanmamışölçüizinver**.</span><span class="sxs-lookup"><span data-stu-id="9ae48-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="9ae48-145">Çift yönlü çapraz filtreleme hakkında daha fazla bilgi için indirme [çift yönlü çapraz filtreleme SQL Server Analysis Services 2016 ve Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) teknik incelemesi.</span><span class="sxs-lookup"><span data-stu-id="9ae48-145">To learn more about bidirectional cross-filtering, download the [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="9ae48-146">Bu Power BI Desktop'ta yapılması gereken tüm iş yukarı sarmalar, ancak iş biz Power BI Embedded içinde tanımlanan bir daha fazla parça of RLS hale getirilmesi için gereken iş kuralları yok.</span><span class="sxs-lookup"><span data-stu-id="9ae48-146">This wraps up all the work that needs to be done in Power BI Desktop, but there’s one more piece of work that needs to be done to make the RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="9ae48-147">Kullanıcıların kimlik doğrulaması ve uygulamanız tarafından yetkili ve uygulama belirteçleri, belirli bir Power BI Embedded rapor kullanıcı erişimi vermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9ae48-147">Users are authenticated and authorized by your application and App tokens are used to grant that user access to a specific Power BI Embedded report.</span></span> <span data-ttu-id="9ae48-148">Power BI Embedded kullanıcı kim herhangi bir özel bilgi yok.</span><span class="sxs-lookup"><span data-stu-id="9ae48-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="9ae48-149">Çalışmak RLS için uygulama belirtecinin bir parçası bazı ek bağlam geçmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="9ae48-149">For RLS to work, you’ll need to pass some additional context as part of your app token:</span></span>

* <span data-ttu-id="9ae48-150">**Kullanıcı adı** (isteğe bağlı) – RLS ile kullanılan bu RLS kuralları uygularken kullanıcı tanımlamaya yardımcı olmak için kullanılan bir dize değeridir.</span><span class="sxs-lookup"><span data-stu-id="9ae48-150">**username** (optional) – Used with RLS this is a string that can be used to help identify the user when applying RLS rules.</span></span> <span data-ttu-id="9ae48-151">Bkz. satır düzeyi güvenlikte Power BI Embedded kullanma</span><span class="sxs-lookup"><span data-stu-id="9ae48-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="9ae48-152">**rolleri** – satır düzeyi güvenlik kuralları uygularken seçmek için rolleri içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="9ae48-152">**roles** – A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="9ae48-153">Birden fazla rol geçirilirse, bir dize dizisi olarak aktarılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ae48-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="9ae48-154">Kullanarak belirteci oluşturma [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9ae48-154">You create the token by using the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="9ae48-155">Username özelliği varsa, ayrıca en az bir değer rollerinde geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae48-155">If the username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="9ae48-156">Örneğin, EmbedSample değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae48-156">For example, you could change the EmbedSample.</span></span> <span data-ttu-id="9ae48-157">Gelen DashboardController satır 55 güncelleştirilemedi</span><span class="sxs-lookup"><span data-stu-id="9ae48-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="9ae48-158">-</span><span class="sxs-lookup"><span data-stu-id="9ae48-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="9ae48-159">Tam uygulama belirteci şunun gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="9ae48-159">The full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="9ae48-160">Birisi bu raporu görüntülemek için uygulamamıza açtığında artık, tüm parçaları ile birlikte, bunlar yalnızca bunlar görmek için bizim satır düzeyi güvenlik tarafından tanımlanan izin verilen verileri görmek kavrayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae48-160">Now, with all the pieces together, when someone logs into our application to view this report, they’ll only be able to see the data that they are allowed to see, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="9ae48-161">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="9ae48-161">See also</span></span>

[<span data-ttu-id="9ae48-162">Satır düzeyi güvenlik (RLS) güç</span><span class="sxs-lookup"><span data-stu-id="9ae48-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="9ae48-163">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="9ae48-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="9ae48-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="9ae48-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="9ae48-165">JavaScript Örnek Ekleme</span><span class="sxs-lookup"><span data-stu-id="9ae48-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="9ae48-166">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="9ae48-166">More questions?</span></span> [<span data-ttu-id="9ae48-167">Power BI Topluluğu'nu deneyin</span><span class="sxs-lookup"><span data-stu-id="9ae48-167">Try the Power BI Community</span></span>](http://community.powerbi.com/)


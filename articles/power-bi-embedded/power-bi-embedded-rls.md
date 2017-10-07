---
title: "Power BI Embedded ile aaaRow düzeyinde güvenlik"
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
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="9bde4-103">Power BI Embedded ile satır düzeyinde güvenlik</span><span class="sxs-lookup"><span data-stu-id="9bde4-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="9bde4-104">Satır düzeyi güvenlik (RLS), rapor veya birden çok farklı kullanıcılar toouse hello için tüm görme farklı veriler aynı rapor veren veri kümesi içinde kullanılan toorestrict kullanıcı erişimi tooparticular veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="9bde4-104">Row level security (RLS) can be used toorestrict user access tooparticular data within a report or dataset, allowing for multiple different users toouse hello same report while all seeing different data.</span></span> <span data-ttu-id="9bde4-105">Power BI Embedded artık RLS ile yapılandırılmış veri kümelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="9bde4-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="9bde4-106">Sipariş tootake avantajlarından RLS, üç ana kavramı anlamak önemlidir; Kullanıcıları, rolleri ve kuralları.</span><span class="sxs-lookup"><span data-stu-id="9bde4-106">In order tootake advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="9bde4-107">Her daha yakın bir göz atalım:</span><span class="sxs-lookup"><span data-stu-id="9bde4-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="9bde4-108">**Kullanıcıların** – bu hello gerçek son kullanıcılar görüntülemekte olduğunuz raporlar.</span><span class="sxs-lookup"><span data-stu-id="9bde4-108">**Users** –  These are hello actual end-users viewing reports.</span></span> <span data-ttu-id="9bde4-109">Power BI Embedded içinde kullanıcıların bir uygulama belirteci hello username özelliği tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9bde4-109">In Power BI Embedded, users are identified by hello username property in an App Token.</span></span>

<span data-ttu-id="9bde4-110">**Rolleri** – kullanıcılar tooroles aittir.</span><span class="sxs-lookup"><span data-stu-id="9bde4-110">**Roles** – Users belong tooroles.</span></span> <span data-ttu-id="9bde4-111">Bir rolü kuralları için bir kapsayıcı ve bir şey "Satış Yöneticisi" veya "Satış Temsilcisi" gibi adlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="9bde4-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="9bde4-112">Power BI Embedded içinde kullanıcıların bir uygulama belirteci hello roller özelliği tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9bde4-112">In Power BI Embedded, users are identified by hello roles property in an App Token.</span></span>

<span data-ttu-id="9bde4-113">**Kuralları** – rollerin kurallar vardır ve uygulanan toobe toohello veri giderek hello gerçek filtreler bu kurallardır.</span><span class="sxs-lookup"><span data-stu-id="9bde4-113">**Rules** – Roles have rules, and those rules are hello actual filters that are going toobe applied toohello data.</span></span> <span data-ttu-id="9bde4-114">Bu kadar basit olabilir "Ülke = tr" veya daha fazla dinamik bir şey.</span><span class="sxs-lookup"><span data-stu-id="9bde4-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="9bde4-115">Örnek</span><span class="sxs-lookup"><span data-stu-id="9bde4-115">Example</span></span>

<span data-ttu-id="9bde4-116">Bu makalede Hello kalanı için RLS yazma ve, katıştırılmış bir uygulama içinde kullanma örneği sağlarız.</span><span class="sxs-lookup"><span data-stu-id="9bde4-116">For hello rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="9bde4-117">Bizim örneğimizde hello kullanan [Retail Analysis örnek](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX dosyası.</span><span class="sxs-lookup"><span data-stu-id="9bde4-117">Our example uses hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="9bde4-118">Retail Analysis örneğimizde bir belirli perakende zincirindeki tüm hello depoları için satış gösterir.</span><span class="sxs-lookup"><span data-stu-id="9bde4-118">Our Retail Analysis sample shows sales for all hello stores in a particular retail chain.</span></span> <span data-ttu-id="9bde4-119">RLS, olmadan hangi bölge olsun Yöneticisi oturum açtığında ve görünümler rapor Merhaba, bunlar görürsünüz aynı veri hello.</span><span class="sxs-lookup"><span data-stu-id="9bde4-119">Without RLS, no matter which district manager signs in and views hello report, they’ll see hello same data.</span></span> <span data-ttu-id="9bde4-120">Üst düzey yönetim her bölge yöneticisi yalnızca hello satışlarının yönettikleri hello depoları ve toodo bu görmelisiniz belirledi, RLS kullanırız.</span><span class="sxs-lookup"><span data-stu-id="9bde4-120">Senior management has determined each district manager should only see hello sales for hello stores they manage, and toodo this, we can use RLS.</span></span>

<span data-ttu-id="9bde4-121">RLS, Power BI Desktop'ta yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="9bde4-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="9bde4-122">Merhaba veri kümesini ve raporu açıldığında, biz toodiagram görünüm toosee hello şema geçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9bde4-122">When hello dataset and report are opened, we can switch toodiagram view toosee hello schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="9bde4-123">Bu şema ile birkaç şey toonotice şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9bde4-123">Here are a few things toonotice with this schema:</span></span>

* <span data-ttu-id="9bde4-124">Tüm ölçüleri, ister **toplam satış**, hello depolanan **satış** Olgu Tablosu.</span><span class="sxs-lookup"><span data-stu-id="9bde4-124">All measures, like **Total Sales**, are stored in hello **Sales** fact table.</span></span>
* <span data-ttu-id="9bde4-125">Dört ek ilgili boyut tabloları vardır: **öğesi**, **zaman**, **deposu**, ve **bölgesi**.</span><span class="sxs-lookup"><span data-stu-id="9bde4-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="9bde4-126">Merhaba okları hello ilişki satırlarındaki filtreleri bir tablo tooanother akabilir hangi yolu belirtin.</span><span class="sxs-lookup"><span data-stu-id="9bde4-126">hello arrows on hello relationship lines indicate which way filters can flow from one table tooanother.</span></span> <span data-ttu-id="9bde4-127">Örneğin, bir filtre yerleştirildiği **zaman [Date]**, hello geçerli şemada, yalnızca hello değerlerde aşağı filtreler **satış** tablo.</span><span class="sxs-lookup"><span data-stu-id="9bde4-127">For example, if a filter is placed on **Time[Date]**, in hello current schema it would only filter down values in hello **Sales** table.</span></span> <span data-ttu-id="9bde4-128">Başka bir tablo tüm hello okları hello ilişki satırları noktası toohello satış tablosuna ve değil hemen bu filtrenin etkilenecek.</span><span class="sxs-lookup"><span data-stu-id="9bde4-128">No other tables would be affected by this filter since all of hello arrows on hello relationship lines point toohello sales table and not away.</span></span>
* <span data-ttu-id="9bde4-129">Merhaba **bölge** tablo her bölge için hello yöneticisi olan gösterir:</span><span class="sxs-lookup"><span data-stu-id="9bde4-129">hello **District** table indicates who hello manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="9bde4-130">Biz filtre toohello uygularsanız bu şemaya göre **bölge yöneticisi** sütununda bölge tablo hello ve bu filtre hello raporu görüntüleme hello kullanıcı eşleşiyorsa, bu filtre da hello filtre **deposu**ve **satış** tabloları tooonly Yöneticisi bu belirli bölge verilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9bde4-130">Based on this schema, if we apply a filter toohello **District Manager** column in hello District table, and if that filter matches hello user viewing hello report, that filter will also filter down hello **Store** and **Sales** tables tooonly show data for that particular district manager.</span></span>

<span data-ttu-id="9bde4-131">İşte nasıl:</span><span class="sxs-lookup"><span data-stu-id="9bde4-131">Here’s how:</span></span>

1. <span data-ttu-id="9bde4-132">Merhaba modelleme sekmesinde, **Rolleri Yönet**.</span><span class="sxs-lookup"><span data-stu-id="9bde4-132">On hello Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="9bde4-133">Adlı yeni bir rol oluşturmak **Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="9bde4-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="9bde4-134">Merhaba, **bölge** tablo DAX ifadesi aşağıdaki hello girin: **[Bölge Yöneticisi] USERNAME() =**</span><span class="sxs-lookup"><span data-stu-id="9bde4-134">In hello **District** table enter hello following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="9bde4-135">toomake emin hello kuralları çalıştığınız, üzerinde hello **modelleme** sekmesini tıklatın, **görünüm rolleri olarak**ve ardından hello aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="9bde4-135">toomake sure hello rules are working, on hello **Modeling** tab, click **View as Roles**, and then enter hello following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="9bde4-136">olarak oturum gibi varsa hello raporları şimdi veri gösterir **Barış Ma**.</span><span class="sxs-lookup"><span data-stu-id="9bde4-136">hello reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="9bde4-137">Merhaba filtre, burada yaptığımız hello şekilde uygulama filtre uygulayarak hello tüm kayıtları aşağı **bölge**, **deposu**, ve **satış** tabloları.</span><span class="sxs-lookup"><span data-stu-id="9bde4-137">Applying hello filter, hello way we did here, will filter down all records in hello **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="9bde4-138">Ancak, hello filtre yönünü arasındaki hello ilişkileri nedeniyle **satış** ve **zaman**, **satış** ve **öğesi**ve **Öğesi** ve **zaman** tabloları aşağı filtrelenmez.</span><span class="sxs-lookup"><span data-stu-id="9bde4-138">However, because of hello filter direction on hello relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="9bde4-139">Bu gereksinim için Tamam olabilir, bunlar Satış yok yöneticileri toosee öğeleri de istemiyorsanız, ancak biz her iki yönde hello ilişkisi ve akış hello güvenlik filtresi için çapraz filtreleme çift yönlü Aç.</span><span class="sxs-lookup"><span data-stu-id="9bde4-139">That may be ok for this requirement, however, if we don’t want managers toosee items for which they don’t have any sales, we could turn on bidirectional cross-filtering for hello relationship and flow hello security filter in both directions.</span></span> <span data-ttu-id="9bde4-140">Bu hello ilişkisi düzenleyerek yapılabilir **satış** ve **öğesi**, şöyle:</span><span class="sxs-lookup"><span data-stu-id="9bde4-140">This can be done by editing hello relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="9bde4-141">Şimdi, filtreleri hello satış tablo toohello ayrıca akabilir **öğesi** tablosu:</span><span class="sxs-lookup"><span data-stu-id="9bde4-141">Now, filters can also flow from hello Sales table toohello **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="9bde4-142">Verileriniz için DirectQuery modu kullanıyorsanız, tooenable çift yönlü-arası bu iki seçenek seçerek filtreleme gerekir:</span><span class="sxs-lookup"><span data-stu-id="9bde4-142">If you're using DirectQuery mode for your data, you will need tooenable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="9bde4-143">**Dosya** -> **seçenekleri ve ayarları** -> **Önizleme özellikleri** -> **çapraz için her iki yönde filtreleme etkinleştir DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="9bde4-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="9bde4-144">**Dosya** -> **seçenekleri ve ayarları** -> **DirectQuery** -> **DirectQuerymodundaKısıtlanmamışölçüizinver**.</span><span class="sxs-lookup"><span data-stu-id="9bde4-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="9bde4-145">çift yönlü çapraz filtreleme, indirme hello hakkında daha fazla toolearn [çift yönlü çapraz filtreleme SQL Server Analysis Services 2016 ve Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) teknik incelemesi.</span><span class="sxs-lookup"><span data-stu-id="9bde4-145">toolearn more about bidirectional cross-filtering, download hello [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="9bde4-146">Bu Power BI Desktop'ta bitti toobe gereken tüm hello iş yukarı sarmalar, ancak bir daha fazla parça bitti toobe toomake gereken çalışmanın yok hello RLS kuralları tanımladığımız iş Power BI Embedded içinde.</span><span class="sxs-lookup"><span data-stu-id="9bde4-146">This wraps up all hello work that needs toobe done in Power BI Desktop, but there’s one more piece of work that needs toobe done toomake hello RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="9bde4-147">Kullanıcıların kimlik doğrulaması ve uygulamanız tarafından yetkili ve uygulama belirteçleri kullanılan toogrant olduğundan, kullanıcı erişim tooa belirli Power BI Embedded rapor.</span><span class="sxs-lookup"><span data-stu-id="9bde4-147">Users are authenticated and authorized by your application and App tokens are used toogrant that user access tooa specific Power BI Embedded report.</span></span> <span data-ttu-id="9bde4-148">Power BI Embedded kullanıcı kim herhangi bir özel bilgi yok.</span><span class="sxs-lookup"><span data-stu-id="9bde4-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="9bde4-149">RLS toowork için uygulama belirtecinin bir parçası bazı ek bağlam toopass gerekir:</span><span class="sxs-lookup"><span data-stu-id="9bde4-149">For RLS toowork, you’ll need toopass some additional context as part of your app token:</span></span>

* <span data-ttu-id="9bde4-150">**Kullanıcı adı** (isteğe bağlı) – RLS ile kullanılan bu kullanılabilecek bir dizedir toohelp RLS kuralları uygularken hello kullanıcı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9bde4-150">**username** (optional) – Used with RLS this is a string that can be used toohelp identify hello user when applying RLS rules.</span></span> <span data-ttu-id="9bde4-151">Bkz. satır düzeyi güvenlikte Power BI Embedded kullanma</span><span class="sxs-lookup"><span data-stu-id="9bde4-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="9bde4-152">**rolleri** – satır düzeyi güvenlik kuralları uygularken hello rolleri tooselect içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="9bde4-152">**roles** – A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="9bde4-153">Birden fazla rol geçirilirse, bir dize dizisi olarak aktarılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9bde4-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="9bde4-154">Hello kullanarak hello belirteci oluşturma [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9bde4-154">You create hello token by using hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="9bde4-155">Merhaba username özelliği varsa, ayrıca en az bir değer rollerinde geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bde4-155">If hello username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="9bde4-156">Örneğin, hello EmbedSample değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9bde4-156">For example, you could change hello EmbedSample.</span></span> <span data-ttu-id="9bde4-157">Gelen DashboardController satır 55 güncelleştirilemedi</span><span class="sxs-lookup"><span data-stu-id="9bde4-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="9bde4-158">-</span><span class="sxs-lookup"><span data-stu-id="9bde4-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="9bde4-159">Merhaba tam uygulama belirteci şunun gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="9bde4-159">hello full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="9bde4-160">Birisi Bu rapor, uygulama tooview açtığında artık, tüm hello parça ile birlikte, yalnızca mümkün toosee hello veri toosee, izin verilen bizim satır düzeyi güvenlik tarafından tanımlandığı şekilde olmaları.</span><span class="sxs-lookup"><span data-stu-id="9bde4-160">Now, with all hello pieces together, when someone logs into our application tooview this report, they’ll only be able toosee hello data that they are allowed toosee, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="9bde4-161">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="9bde4-161">See also</span></span>

[<span data-ttu-id="9bde4-162">Satır düzeyi güvenlik (RLS) güç</span><span class="sxs-lookup"><span data-stu-id="9bde4-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="9bde4-163">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="9bde4-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="9bde4-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="9bde4-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="9bde4-165">JavaScript Örnek Ekleme</span><span class="sxs-lookup"><span data-stu-id="9bde4-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="9bde4-166">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="9bde4-166">More questions?</span></span> [<span data-ttu-id="9bde4-167">Merhaba Power BI topluluk deneyin</span><span class="sxs-lookup"><span data-stu-id="9bde4-167">Try hello Power BI Community</span></span>](http://community.powerbi.com/)


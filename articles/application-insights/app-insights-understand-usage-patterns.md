---
title: "aaaAzure uygulama Öngörüler Funnels"
description: "Funnels toodiscover nasıl kullanabileceğinizi öğrenin müşteriler uygulamanız ile nasıl etkileşim."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: cfreeman
ms.openlocfilehash: 3a90cfd11cb193e303136504df44008ffd04a290
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="discover-how-customers-are-using-your-application-with-hello-application-insights-funnels"></a><span data-ttu-id="aefe9-103">Müşteriler, uygulamanızın uygulama Öngörüler Funnels hello ile nasıl kullandığını keşfedin</span><span class="sxs-lookup"><span data-stu-id="aefe9-103">Discover how customers are using your application with hello Application Insights Funnels</span></span>

<span data-ttu-id="aefe9-104">Merhaba utmost önem tooyour iş kolu anlama müşteri deneyimidir.</span><span class="sxs-lookup"><span data-stu-id="aefe9-104">Understanding customer experience is of hello utmost importance tooyour business.</span></span> <span data-ttu-id="aefe9-105">Uygulamanız birden çok aşamaları içeriyorsa, müşterilerin çoğu hello tüm süreci devam veya belirli bir noktada hello işlem sona erecektir tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="aefe9-105">If your application involves multiple stages, you will need tooknow if most customers are progressing through hello entire process, or if they are ending hello process at some point.</span></span> <span data-ttu-id="aefe9-106">bir dizi adımı bir web uygulaması aracılığıyla Hello ilerlemeyi "Huni" bilinir.</span><span class="sxs-lookup"><span data-stu-id="aefe9-106">hello progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="aefe9-107">Kullanıcılarınızı ve izleme hakkında adım adım dönüştürme oranları hello uygulama Öngörüler Funnels toogain Öngörüler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aefe9-107">You can use hello Application Insights Funnels toogain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-hello-funnels-blade"></a><span data-ttu-id="aefe9-108">Merhaba Funnels dikey ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="aefe9-108">Get started with hello Funnels blade</span></span>
<span data-ttu-id="aefe9-109">Merhaba en kolay yolu toolearn Funnels hakkında toowalk bir örnek olur.</span><span class="sxs-lookup"><span data-stu-id="aefe9-109">hello easiest way toolearn about Funnels is toowalk though an example.</span></span> <span data-ttu-id="aefe9-110">Merhaba aşağıdaki çizimler bir e-ticaret iş hello adımları sahipleri müşterilerine kendi web uygulaması ile nasıl etkileşim toolearn götürecek göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="aefe9-110">hello following illustrations demonstrate hello steps owners of an e-commerce business would take toolearn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="aefe9-111">Huni oluşturma</span><span class="sxs-lookup"><span data-stu-id="aefe9-111">Create your funnel</span></span>
<span data-ttu-id="aefe9-112">Huni oluşturmadan önce toodecide gereken hello soru tooanswer istiyor.</span><span class="sxs-lookup"><span data-stu-id="aefe9-112">Before you create your funnel, you need toodecide on hello question you want tooanswer.</span></span> <span data-ttu-id="aefe9-113">Örneğin, bir tanıtım giriş sayfasını tıklatın görüntüleme kaç müşteriler tooknow isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aefe9-113">For example, you might want tooknow how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="aefe9-114">Bu örnekte, hello Fabrikam Fiber şirket hello sahipleri tooknow hello hello geçen ay sırasında alışveriş sepeti öğeleri tootheir ekledikten sonra satın almasını kolaylaştıran müşteriler yüzdesi istiyor.</span><span class="sxs-lookup"><span data-stu-id="aefe9-114">In this example, hello owners of hello Fabrikam Fiber company want tooknow hello percentage of customers who make a purchase after adding items tootheir shopping cart during hello last month.</span></span>

<span data-ttu-id="aefe9-115">Burada, bunlar toocreate kendi Huni hello adımlar bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="aefe9-115">Here are hello steps they take toocreate their funnel.</span></span>

1. <span data-ttu-id="aefe9-116">Merhaba Funnels dikey penceresinde Hello yeni düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="aefe9-116">Click hello New button on hello Funnels blade.</span></span>
1. <span data-ttu-id="aefe9-117">Hello "Geçen ay" Merhaba zaman aralığı seçin **zaman aralığı** açılır.</span><span class="sxs-lookup"><span data-stu-id="aefe9-117">Select hello time range of "Last month" from hello **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="aefe9-118">Select hello **ürün sayfası** hello olayından **1. adım** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="aefe9-118">Select hello **Product page** event from hello **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="aefe9-119">Select hello **Ekle tooshopping Sepeti** hello olayından **2. adım** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="aefe9-119">Select hello **Add tooshopping cart** event from hello **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="aefe9-120">Select hello **tıklatın satın alma** hello olayından **adım 3** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="aefe9-120">Select hello **Click purchase** event from hello **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="aefe9-121">Ad toohello Huni ekleyin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="aefe9-121">Add a name toohello funnel and click **Save**.</span></span>

<span data-ttu-id="aefe9-122">Merhaba aşağıdaki çizimde hello veri hello Funnels dikey oluşturur gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="aefe9-122">hello following illustration demonstrates hello data hello Funnels blade generates.</span></span> <span data-ttu-id="aefe9-123">Burada hello Fabrikam sahipleri hello geçen hafta sırasında tamamlanmış hello satın alma %22.7 bir öğe tootheir alışveriş eklenen müşterilerinin Sepeti görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aefe9-123">From here hello Fabrikam owners can see that during hello last week, 22.7% of their customers who added an item tootheir shopping cart completed hello purchase.</span></span> <span data-ttu-id="aefe9-124">Bunlar hello ürün sayfası ve % 20'müşterilerinin ziyaret kendi satın alma tamamladıktan sonra oturumu kapattınız önce %1 hello müşterilerin bir reklam tıklattınız de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aefe9-124">They can also see that 1% of hello customers clicked an advertisement before visiting hello product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Verilerle funnels dikey penceresi](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="aefe9-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aefe9-126">Next steps</span></span>
- <span data-ttu-id="aefe9-127">Daha fazla bilgi edinmek [kullanım analizi](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aefe9-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 

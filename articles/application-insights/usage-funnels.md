---
title: "Azure uygulama Öngörüler Funnels"
description: "Müşteriler uygulamanız ile nasıl etkileşim bulmak için Funnels nasıl kullanabileceğinizi öğrenin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 59c4dfafc102b26e3b9873f433065715f4aec9ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="discover-how-customers-are-using-your-application-with-the-application-insights-funnels"></a><span data-ttu-id="e5681-103">Müşteriler, uygulamanızın uygulama Öngörüler Funnels ile nasıl kullandığını keşfedin</span><span class="sxs-lookup"><span data-stu-id="e5681-103">Discover how customers are using your application with the Application Insights Funnels</span></span>

<span data-ttu-id="e5681-104">Anlama müşteri işinize utmost önem deneyimidir.</span><span class="sxs-lookup"><span data-stu-id="e5681-104">Understanding customer experience is of the utmost importance to your business.</span></span> <span data-ttu-id="e5681-105">Uygulamanız birden çok aşamaları içeriyorsa, müşterilerin çoğu tüm süreci devam veya belirli bir noktada işlem sona erecektir bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5681-105">If your application involves multiple stages, you will need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span></span> <span data-ttu-id="e5681-106">Bir dizi adımı bir web uygulaması aracılığıyla ilerlemeyi "Huni" bilinir.</span><span class="sxs-lookup"><span data-stu-id="e5681-106">The progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="e5681-107">Kullanıcılarınızı ve izleme hakkında adım adım dönüştürme oranları Öngörüler elde etmek için uygulama Öngörüler Funnels kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5681-107">You can use the Application Insights Funnels to gain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-the-funnels-blade"></a><span data-ttu-id="e5681-108">Funnels dikey ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e5681-108">Get started with the Funnels blade</span></span>
<span data-ttu-id="e5681-109">Funnels hakkında bilgi edinmek için kolay bir örnek ancak yürütmek için yoludur.</span><span class="sxs-lookup"><span data-stu-id="e5681-109">The easiest way to learn about Funnels is to walk though an example.</span></span> <span data-ttu-id="e5681-110">Aşağıdaki çizimler bir e-ticaret iş adımları sahipleri müşterilerine kendi web uygulaması ile nasıl etkileşim öğrenmek için harcanacak göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="e5681-110">The following illustrations demonstrate the steps owners of an e-commerce business would take to learn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="e5681-111">Huni oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5681-111">Create your funnel</span></span>
<span data-ttu-id="e5681-112">Huni oluşturmadan önce yanıt istediğiniz soru karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5681-112">Before you create your funnel, you need to decide on the question you want to answer.</span></span> <span data-ttu-id="e5681-113">Örneğin, bir tanıtım giriş sayfasını tıklatın görüntüleme kaç müşteriler bilmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5681-113">For example, you might want to know how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="e5681-114">Bu örnekte, Fabrikam Fiber şirket sahipleri öğeleri geçen ay sırasında kendi alışveriş sepetine ekledikten sonra satın almasını kolaylaştıran müşteriler yüzdesi bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e5681-114">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who make a purchase after adding items to their shopping cart during the last month.</span></span>

<span data-ttu-id="e5681-115">Burada, bunlar kendi Huni oluşturmak için adımlar bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e5681-115">Here are the steps they take to create their funnel.</span></span>

1. <span data-ttu-id="e5681-116">Funnels dikey yeni düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e5681-116">Click the New button on the Funnels blade.</span></span>
1. <span data-ttu-id="e5681-117">"Geçen ay" zaman aralığını seçin **zaman aralığı** açılır.</span><span class="sxs-lookup"><span data-stu-id="e5681-117">Select the time range of "Last month" from the **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="e5681-118">Seçin **ürün sayfası** olayından **1. adım** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="e5681-118">Select the **Product page** event from the **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="e5681-119">Seçin **eklemek alışveriş sepetine** olayından **2. adım** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="e5681-119">Select the **Add to shopping cart** event from the **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="e5681-120">Seçin **tıklatın satın alma** olayından **adım 3** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="e5681-120">Select the **Click purchase** event from the **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="e5681-121">Huni için bir ad eklemek ve tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e5681-121">Add a name to the funnel and click **Save**.</span></span>

<span data-ttu-id="e5681-122">Aşağıdaki çizimde Funnels dikey veriler üretir gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e5681-122">The following illustration demonstrates the data the Funnels blade generates.</span></span> <span data-ttu-id="e5681-123">Fabrikam buradan sahipleri, geçen hafta sırasında %22.7 kendi alışveriş sepetine eklenen bir öğe müşterilerinin satın alma tamamlandı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5681-123">From here the Fabrikam owners can see that during the last week, 22.7% of their customers who added an item to their shopping cart completed the purchase.</span></span> <span data-ttu-id="e5681-124">Bunlar %1 müşterilerin kendi satın alma tamamladıktan sonra ürün sayfası ve % 20'müşterilerinin ziyaret'ı oturumunuz önce bir reklam tıklattınız de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5681-124">They can also see that 1% of the customers clicked an advertisement before visiting the product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Verilerle funnels dikey penceresi](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="e5681-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e5681-126">Next steps</span></span>
  * [<span data-ttu-id="e5681-127">Kullanıma genel bakış</span><span class="sxs-lookup"><span data-stu-id="e5681-127">Usage overview</span></span>](app-insights-usage-overview.md)
  * [<span data-ttu-id="e5681-128">Kullanıcıları, oturumlar ve olaylar</span><span class="sxs-lookup"><span data-stu-id="e5681-128">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
  * [<span data-ttu-id="e5681-129">Bekletme</span><span class="sxs-lookup"><span data-stu-id="e5681-129">Retention</span></span>](app-insights-usage-retention.md)
  * [<span data-ttu-id="e5681-130">Çalışma kitapları</span><span class="sxs-lookup"><span data-stu-id="e5681-130">Workbooks</span></span>](app-insights-usage-workbooks.md)
  * [<span data-ttu-id="e5681-131">Kullanıcı bağlamı Ekle</span><span class="sxs-lookup"><span data-stu-id="e5681-131">Add user context</span></span>](app-insights-usage-send-user-context.md)

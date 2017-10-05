---
title: "Veri Hizmeti Market oluşturmaya Kılavuzu | Microsoft Docs"
description: "Oluşturma, sertifika ve bir veri hizmeti için dağıtma konusunda ayrıntılı yönergeler Azure Market satın alın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: c0c9362f1c2e15c947aaaf7187f3383ad243140f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="data-service-publishing-guide-for-the-azure-marketplace"></a><span data-ttu-id="eefb6-103">Veri Hizmeti Azure Market'e Kılavuzu yayımlama</span><span class="sxs-lookup"><span data-stu-id="eefb6-103">Data Service Publishing Guide for the Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="eefb6-104">**Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.**</span><span class="sxs-lookup"><span data-stu-id="eefb6-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="eefb6-105">Üzerinde AppSource yayımlamak istediğiniz bir SaaS iş uygulaması varsa daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="eefb6-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="eefb6-106">Bir Iaas uygulamalar varsa veya Azure marketi, yayımlamak istediğiniz Geliştirici hizmet, daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="eefb6-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="eefb6-107">Adım 1 ' tamamladıktan sonra [hesap oluşturma ve kayıt](marketplace-publishing-accounts-creation-registration.md), biz size kılavuzluk [genel teknik olmayan](marketplace-publishing-pre-requisites.md) ve [teknik gereksinimleri](marketplace-publishing-data-service-creation-prerequisites.md) veri hizmeti Azure Market sunar.</span><span class="sxs-lookup"><span data-stu-id="eefb6-107">After completing the step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through the [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="eefb6-108">Biz, üzerinde bir veri hizmeti teklifi oluşturmak için adımlarda size yol gösterecek artık [yayımlama portalında] [ link-pubportal] Azure Marketi için.</span><span class="sxs-lookup"><span data-stu-id="eefb6-108">Now we will walk you through the steps for creating a Data Service offer on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="1----login-to-the-publishing-portal"></a><span data-ttu-id="eefb6-109">1.    Yayımlama için oturum açma Portal.</span><span class="sxs-lookup"><span data-stu-id="eefb6-109">1.    Login to the Publishing Portal.</span></span>
<span data-ttu-id="eefb6-110">Git [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="eefb6-110">Go to [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="eefb6-111">**Yayımlama portalında ilk oturum açma için şirketinizin satıcı profili Geliştirici Merkezi'nde kayıtlı olduğu aynı hesabı kullanın.**</span><span class="sxs-lookup"><span data-stu-id="eefb6-111">**For first time login to Publishing Portal, use the same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="eefb6-112">(Daha sonra şirketinizin herhangi bir personel yayımlama portalında ortak yönetici olarak ekleyebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="eefb6-112">(Later you can add any employee of your company as a co-admin in the Publishing Portal).</span></span>

<span data-ttu-id="eefb6-113">Tıklayın **veri hizmetleri yayımlama** Bu yayımlama portalında ilk oturum ise döşeme.</span><span class="sxs-lookup"><span data-stu-id="eefb6-113">Click on the **Publish a Data Services** tile if this is the first login into the publishing portal.</span></span>

## <a name="2----choose-data-services-in-the-navigation-menu-on-the-left-side"></a><span data-ttu-id="eefb6-114">2.    Seçin **Veri Hizmetleri** sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="eefb6-114">2.    Choose **Data Services** in the navigation menu on the left side.</span></span>
  ![Çizim](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="eefb6-116">3.    Yeni bir veri hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="eefb6-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="eefb6-117">Başlık, yeni veri hizmeti sunmak için doldurun ve sağ taraftaki üzerinde "+"'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="eefb6-117">Fill in the title for your new Data Service Offer and click on “+” on the right.</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-the-sub-menu-under-the-newly-created-data-service-in-the-navigation-menu"></a><span data-ttu-id="eefb6-119">4.    Alt menü Gezinti menüsünde Yeni oluşturulan veri hizmeti altındaki gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="eefb6-119">4.    Review the sub-menu under the newly created Data Service in the navigation menu.</span></span>
<span data-ttu-id="eefb6-120">Tıklayın **izlenecek** sekmesinde ve Azure Market'te veri hizmeti düzgün şekilde yayımlamak için gerekli tüm gerekli adımları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="eefb6-120">Click on the **Walkthrough** tab and review all necessary steps needed to publish properly the Data Service on the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="eefb6-121">Her zaman "İzlenecek" sayfası bağlantıları tıklayın veya sol tarafındaki veri hizmeti teklif ait alt menüsünde sekmeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="eefb6-121">You always can click on the links in the “Walkthrough” page or use tabs on the Data Service offer’s sub-menu on the left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="eefb6-122">5.    Yeni bir Plan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eefb6-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="eefb6-123">, İşlemleri planları sunar.</span><span class="sxs-lookup"><span data-stu-id="eefb6-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="eefb6-124">Her teklif birden çok planına sahip olabilir, ancak en az birine (1) planı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eefb6-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="eefb6-125">Teklifiniz için son kullanıcıların abone olduğunuzda bunların teklif 's planı biri için abone olun.</span><span class="sxs-lookup"><span data-stu-id="eefb6-125">When end-users subscribe to your offer they subscribe for one of the offer’s Plan.</span></span> <span data-ttu-id="eefb6-126">Her plan nasıl son kullanıcılar hizmetinizi kullanabilmek için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="eefb6-126">Each plan defines how end-users will be able to use your service.</span></span>

<span data-ttu-id="eefb6-127">Şu anda Azure Marketi yalnızca aylık abonelik işlem tabanlı model verileri için Destek Hizmetleri, yani son kullanıcıların abone oldukları belirli plan fiyatı göre aylık ücret ödemeniz ve işlem her ay sayısı kullanamayabilir olacaktır plan tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="eefb6-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according to the price of the specific plan they subscribed to and will be able to consume each month number of transaction defined by the plan.</span></span>

<span data-ttu-id="eefb6-128">Genelde, veri hizmeti döndürülecek kayıt sayısı tanımlanan her bir işlem hizmete gönderilen bağlı.</span><span class="sxs-lookup"><span data-stu-id="eefb6-128">Each Transaction usually defined as number of records your Data Service will return based on the query sent to the Service.</span></span> <span data-ttu-id="eefb6-129">Varsayılan değer 100'dür.</span><span class="sxs-lookup"><span data-stu-id="eefb6-129">The default is 100.</span></span> <span data-ttu-id="eefb6-130">Her sorgu döndürülen işlem sayısı sayı olacaktır 100 ve kadar en yakın tamsayıya yuvarlanan bölü kayıtların.</span><span class="sxs-lookup"><span data-stu-id="eefb6-130">Number of transactions returned to each query will be number of records divided by 100 and rounded up to the closest integer.</span></span>

<span data-ttu-id="eefb6-131">Bu her sorgu tarafından tüketilen işlem sayısı (ölçüm) izlemek için Azure Market hizmet katmanı sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="eefb6-131">It’s Azure Marketplace Service layer responsibility to monitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eefb6-132">Ay sırasında işlem sınırına son kullanıcılar kendi aylık abonelik döngüsünün sonuna kadar hizmetini kullanmaya devam etmesini engellenir.</span><span class="sxs-lookup"><span data-stu-id="eefb6-132">End-Users which reached the transaction limit during the month will be blocked from continuing to use the service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="eefb6-133">Plan veya planları biri işlemleri sınırsız sayıda olabilir ama değil gerekir içerir.</span><span class="sxs-lookup"><span data-stu-id="eefb6-133">The plan or one of the plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="eefb6-134">Bir plan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eefb6-134">Create a plan.</span></span>
1. <span data-ttu-id="eefb6-135">Tıklayın **"+"** "Yeni bir plan Ekle" yanındaki.</span><span class="sxs-lookup"><span data-stu-id="eefb6-135">Click on **“+”** next to the “Add a new plan”.</span></span>
2. <span data-ttu-id="eefb6-136">Seçeneklerden birini seçin: **sınırsız** veya **sınırlı** Bu plan için kullanım.</span><span class="sxs-lookup"><span data-stu-id="eefb6-136">Choose one of the options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="eefb6-137">İşlem sayısı sınırlı sonra sağlarsanız, plan bir ay içinde kullanılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="eefb6-137">If Limited then provide the number of transaction the plan will allow to consume in a month.</span></span>
   
    ![Çizim](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="eefb6-139">Portal yayımlama "Planı son kullanıcılara kullanıcı arabiriminde planının adı iletişim kurmak için kullanılan ve ayrıca belirlemek için markette hizmeti tarafından kullanılan tanımlayıcı" önerir.</span><span class="sxs-lookup"><span data-stu-id="eefb6-139">Publishing Portal will also suggest “Plan Identifier”, which will be used to communicate to the end-users the name of the plan in the UI and also used by the Market Place Service to identify the Plan.</span></span> <span data-ttu-id="eefb6-140">İsterseniz, "Plan tanımlayıcısı" değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eefb6-140">You can change the “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="eefb6-141">"Plan tanımlayıcısı" her teklif kapsamında benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eefb6-141">The “Plan Identifier” must be unique within the scope of each offer.</span></span> <span data-ttu-id="eefb6-142">Diğer birçok tanımlayıcıları yayımlama Portal planlama tanımlayıcıda kullanılan ilk yayımlama üretim ve bu tanımlayıcı değiştirmesi mümkün olmayacaktır sonra kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="eefb6-142">As many other Identifiers used in the Publishing Portal Plan identifier will be locked after the first publishing to production and you will not be able to change this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="eefb6-143">Tercih ettiğiniz kabul etmek için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="eefb6-143">Click to accept your choice.</span></span>
4. <span data-ttu-id="eefb6-144">Ardından, birkaç ek soruları yeni oluşturulan planınız istenir.</span><span class="sxs-lookup"><span data-stu-id="eefb6-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![Çizim](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="eefb6-146">Soru</span><span class="sxs-lookup"><span data-stu-id="eefb6-146">Question</span></span> | <span data-ttu-id="eefb6-147">Anlamlı</span><span class="sxs-lookup"><span data-stu-id="eefb6-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="eefb6-148">**Bu Plan hazır ve kullanılabilir dünya çapında mi?**</span><span class="sxs-lookup"><span data-stu-id="eefb6-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="eefb6-149">Tamamen ücretsiz-in-ücret planı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eefb6-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="eefb6-150">Bu teklif – yalnızca planlama ise "Ücretsiz teklif" markette yayımladığınız olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="eefb6-150">If it’s the only plan for this offer – it means that you are publishing “Free Offer” in the Marketplace.</span></span> <span data-ttu-id="eefb6-151">Yalnızca biri (az) için ise planı, BT size hizmetiniz görece küçük bir aylık işlem sayısı ile ilgili daha fazla bilgi için son kullanıcılara sunmak için bir seçenek.</span><span class="sxs-lookup"><span data-stu-id="eefb6-151">If it’s only for one (of few) Plan, the it gives you an option to offer end-users to learn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="eefb6-152">Yanıt "Evet" ise, daha fazla soru istenir.</span><span class="sxs-lookup"><span data-stu-id="eefb6-152">If the answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="eefb6-153">Son kullanıcıların her zaman Ücretli planlarına yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eefb6-153">End users can always upgrade to the paid plans.</span></span>
> 
> 

| <span data-ttu-id="eefb6-154">Soru</span><span class="sxs-lookup"><span data-stu-id="eefb6-154">Question</span></span> | <span data-ttu-id="eefb6-155">Anlamlı</span><span class="sxs-lookup"><span data-stu-id="eefb6-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="eefb6-156">**Ücretsiz deneme sürümü var mı?**</span><span class="sxs-lookup"><span data-stu-id="eefb6-156">**Is free trial available?**</span></span> |<span data-ttu-id="eefb6-157">"Hayır deneme" arasında hiç seçin veya planınız "Bir ay" için kullanılacak bir seçenek sağlar.</span><span class="sxs-lookup"><span data-stu-id="eefb6-157">You can choose between “No Trial” at all or give an option to use your Plan for “One Month”.</span></span> <span data-ttu-id="eefb6-158">Son kullanıcılar için ücretsiz bir ay için önerinin avantajlarını öğrenmeniz olasılığını sağlamak için bu seçeneği kullanmak yayımcılar gibi.</span><span class="sxs-lookup"><span data-stu-id="eefb6-158">Publishers like to use this option to provide end-users the possibility to understand the benefits of the offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="eefb6-159">Son kullanıcılar yalnızca ödeme yöntemini kredi kartı ör, Kurumsal Anlaşma kurduysanız ücretsiz deneme satın açabilirler.</span><span class="sxs-lookup"><span data-stu-id="eefb6-159">End-users will only be able to purchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="eefb6-160">Müşteri aboneliği iptal başlatılan sürece ücretsiz deneme sürümü, bir ay sonra abonelik tarih itibariyle fiyat müşteriler şarj Azure Marketi başlar.</span><span class="sxs-lookup"><span data-stu-id="eefb6-160">After one month of the free trial, Azure Marketplace will start charging customers the price as of the date of the subscription, unless the customer initiated the subscription cancellation.</span></span> <span data-ttu-id="eefb6-161">Özel bildirim son kullanıcılara sağlanır.</span><span class="sxs-lookup"><span data-stu-id="eefb6-161">No special notification will be provided to the end-users.</span></span>
> 
> 

| <span data-ttu-id="eefb6-162">Soru</span><span class="sxs-lookup"><span data-stu-id="eefb6-162">Question</span></span> | <span data-ttu-id="eefb6-163">Anlamlı</span><span class="sxs-lookup"><span data-stu-id="eefb6-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="eefb6-164">**Bu planı satın almak için bir promosyon kodu gerektiriyor?**</span><span class="sxs-lookup"><span data-stu-id="eefb6-164">**This plan requires a promotion code to purchase?**</span></span> |<span data-ttu-id="eefb6-165">Yayımcılar belirli müşterilere "A Promocode" adlı bir özel kod sağlayarak kendi hizmet planları erişimi sınırlamak için bir seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="eefb6-165">Publishers have an option to limit access to their Service Plans by providing a special code, called “A Promocode” to specific customers.</span></span> <span data-ttu-id="eefb6-166">Bu Promocode sahip son kullanıcılar plana abone kuramaz.</span><span class="sxs-lookup"><span data-stu-id="eefb6-166">Only end-users which will have this Promocode will be able to subscribe to the Plan.</span></span> <span data-ttu-id="eefb6-167">"Hayır" ı seçin, sonra kabul durumunda herkes teklif olduğu kullanılabilir bölgesinden (bkz [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) daha fazla ayrıntı için) bu plana abone mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="eefb6-167">If you choose “No”, then you agree that everyone from the region where the offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able to subscribe to this plan.</span></span> <span data-ttu-id="eefb6-168">Daha fazla soru istenir.</span><span class="sxs-lookup"><span data-stu-id="eefb6-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="eefb6-169">**Ayrıca geçerli promosyon kodu yok herkes bu plandan Gizle?**</span><span class="sxs-lookup"><span data-stu-id="eefb6-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="eefb6-170">Önceki sorusunun yanıtını "Evet" ise yayımcının Market Arabiriminde görünen bu planı tamamen kaldırmak için bir seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="eefb6-170">If the answer to the previous question is “Yes” the Publisher has an option to completely remove this plan from appearing in the UI of the Marketplace.</span></span> <span data-ttu-id="eefb6-171">Bu anlamına gelir, müşteriler bu teklif'in ayrıntılar sayfası planında görmez.</span><span class="sxs-lookup"><span data-stu-id="eefb6-171">It means, customers will not see this plan in the Offer’s details page.</span></span> <span data-ttu-id="eefb6-172">Satın almak için bir promocode alacak son kullanıcılar erişebilir bu promocode kullanarak abone olun.</span><span class="sxs-lookup"><span data-stu-id="eefb6-172">End-users which will receive a promocode to purchase it, will be able to subscribe to it using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="eefb6-173">6.    İçerik pazarlama, Market oluşturma</span><span class="sxs-lookup"><span data-stu-id="eefb6-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="eefb6-174">Gerekli bilgileri sağlamak nasıl **pazarlama, fiyatlandırma, destek ve kategorileri** sekmeleri ziyaret edin [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) Azure yayımlanan tüm yapıları için ortak olan Market.</span><span class="sxs-lookup"><span data-stu-id="eefb6-174">For How to provide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common to all artifacts published in the Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-to-your-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="eefb6-175">7.    Teklifiniz hizmetinize (SQL tabanlı Azure veya Web tabanlı hizmet) bağlayın.</span><span class="sxs-lookup"><span data-stu-id="eefb6-175">7.    Connect your offer to your Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="eefb6-176">Tıklayın **Veri Hizmetleri** alt menüsünde.</span><span class="sxs-lookup"><span data-stu-id="eefb6-176">Click on the **Data Services** sub-menu.</span></span>

<span data-ttu-id="eefb6-177">Sayfanın üst kısmında teklif 's sağlamak için istenir, **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="eefb6-177">On the upper half of the page you’ll be asked to provide the offer’s **Namespace**.</span></span>  

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="eefb6-179">Soru yayımcı Azure Marketi'nde yeni oluşturulan sunmaya teklif ne olacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="eefb6-179">The below question will define how the Publisher is going to expose newly created offer to Azure Marketplace.</span></span> <span data-ttu-id="eefb6-180">(Daha fazla bilgi için bkz [Veri Hizmetleri Teknik önkoşul Kılavuzu](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="eefb6-180">(For more details see the [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="eefb6-182">**Temel veritabanı hizmeti yayımlama**</span><span class="sxs-lookup"><span data-stu-id="eefb6-182">**Publishing the Database based service**</span></span>

<span data-ttu-id="eefb6-183">Tıklayın **veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="eefb6-183">Click on **Database**.</span></span> <span data-ttu-id="eefb6-184">Aşağıdaki sayfası görünür:</span><span class="sxs-lookup"><span data-stu-id="eefb6-184">The following page will appear:</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="eefb6-186">SQL Azure DB'de tabanlı veri kümesi için bir CSDL eşlemesi oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="eefb6-186">To create a CSDL mapping for the Dataset based on the SQL Azure DB:</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="eefb6-188">Ve ardından her tablo için</span><span class="sxs-lookup"><span data-stu-id="eefb6-188">And then for each table</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="eefb6-191">Web hizmeti</span><span class="sxs-lookup"><span data-stu-id="eefb6-191">If Web Service</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="eefb6-193">Okuma [var olan eşleme web hizmeti CSDL aracılığıyla OData](marketplace-publishing-data-service-creation-odata-mapping.md) ayrıntılı yönergeler ve örnekler CSDL Web hizmeti oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="eefb6-193">Read [Mapping an existing web service to OData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="eefb6-194">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="eefb6-194">Next Steps</span></span>
<span data-ttu-id="eefb6-195">Veri Hizmeti teklifiniz oluşturduğunuza göre ' ndaki yönergeleri tamamlandığından emin olmak [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) İleri geçmeden önce [hazırlama,verihizmetisınama](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="eefb6-195">Now that you've created your Data Service offer, please ensure that you complete the instructions in the [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward to [Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="eefb6-196">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="eefb6-196">See Also</span></span>
* [<span data-ttu-id="eefb6-197">Başlarken: nasıl bir teklifi Azure Marketinde yayımlama</span><span class="sxs-lookup"><span data-stu-id="eefb6-197">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="eefb6-198">Genel OData eşleme işlemi ve amacı anlamak ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme](marketplace-publishing-data-service-creation-odata-mapping.md) tanımları, yapılar ve yönergeleri gözden geçirmek için.</span><span class="sxs-lookup"><span data-stu-id="eefb6-198">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="eefb6-199">Öğrenme ve belirli düğümler ve bunların parametrelerini anlama ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme düğümleri](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) tanımları ve açıklamalar, örnekler ve kullanım örneği bağlamı.</span><span class="sxs-lookup"><span data-stu-id="eefb6-199">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="eefb6-200">Örnekler gözden geçirme ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme örnekler](marketplace-publishing-data-service-creation-odata-mapping-examples.md) örnek kodu görmek ve kod sözdizimi ve bağlamı anlamak için.</span><span class="sxs-lookup"><span data-stu-id="eefb6-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com

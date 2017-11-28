---
title: "aaaGuide toocreating hello Market için veri hizmeti | Microsoft Docs"
description: "Nasıl toocreate, onaylamak ve dağıtmak için bir veri hizmeti ayrıntılı yönergeler hello üzerinde Azure Market satın alın."
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
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a><span data-ttu-id="38234-103">Veri Hizmeti Yayımlama Kılavuzu hello Azure Market</span><span class="sxs-lookup"><span data-stu-id="38234-103">Data Service Publishing Guide for hello Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="38234-104">**Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.**</span><span class="sxs-lookup"><span data-stu-id="38234-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="38234-105">Bir SaaS iş uygulaması varsa toopublish istediğiniz AppSource hakkında daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="38234-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="38234-106">Bir Iaas uygulamalar varsa veya Geliştirici hizmeti misiniz Azure Market'te toopublish gibi daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="38234-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="38234-107">Merhaba adım 1 ' tamamladıktan sonra [hesap oluşturma ve kayıt](marketplace-publishing-accounts-creation-registration.md), biz hello destekli [genel teknik olmayan](marketplace-publishing-pre-requisites.md) ve [teknik gereksinimleri](marketplace-publishing-data-service-creation-prerequisites.md) veri hizmeti Azure Market sunar.</span><span class="sxs-lookup"><span data-stu-id="38234-107">After completing hello step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through hello [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="38234-108">Biz, bir veri hizmeti teklif üzerinde hello oluşturmak için hello adımlarda size yol gösterecek artık [yayımlama portalında] [ link-pubportal] hello Azure Marketi için.</span><span class="sxs-lookup"><span data-stu-id="38234-108">Now we will walk you through hello steps for creating a Data Service offer on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="1----login-toohello-publishing-portal"></a><span data-ttu-id="38234-109">1.    Oturum açma toohello Yayımlama Portalı.</span><span class="sxs-lookup"><span data-stu-id="38234-109">1.    Login toohello Publishing Portal.</span></span>
<span data-ttu-id="38234-110">Çok Git[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="38234-110">Go too[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="38234-111">**İlk zaman oturum açma tooPublishing için portalı, aynı hesabı ile şirketinizin Seller profil Geliştirici Merkezi'nde kayıtlı hello kullanın.**</span><span class="sxs-lookup"><span data-stu-id="38234-111">**For first time login tooPublishing Portal, use hello same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="38234-112">(Daha sonra şirketinizin herhangi bir personel hello Yayımlama Portalı'nda bir ortak yönetici olarak ekleyebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="38234-112">(Later you can add any employee of your company as a co-admin in hello Publishing Portal).</span></span>

<span data-ttu-id="38234-113">Tıklatın hello üzerinde **veri hizmetleri yayımlama** Bu yayımlama hello portalında ilk oturum hello ise döşeme.</span><span class="sxs-lookup"><span data-stu-id="38234-113">Click on hello **Publish a Data Services** tile if this is hello first login into hello publishing portal.</span></span>

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a><span data-ttu-id="38234-114">2.    Seçin **Veri Hizmetleri** hello yan sol gezinti menüsünde hello.</span><span class="sxs-lookup"><span data-stu-id="38234-114">2.    Choose **Data Services** in hello navigation menu on hello left side.</span></span>
  ![Çizim](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="38234-116">3.    Yeni bir veri hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="38234-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="38234-117">Merhaba başlığında, yeni veri hizmeti sunmak için doldurun ve hello sağ üzerinde üzerinde "+"'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="38234-117">Fill in hello title for your new Data Service Offer and click on “+” on hello right.</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a><span data-ttu-id="38234-119">4.    Gözden geçirme hello alt menüsünde hello altında veri hizmeti hello Gezinti menüsünde Yeni oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="38234-119">4.    Review hello sub-menu under hello newly created Data Service in hello navigation menu.</span></span>
<span data-ttu-id="38234-120">Tıklatın hello üzerinde **izlenecek** sekmesinde ve toopublish düzgün şekilde hello veri hizmeti Azure Marketi hello tüm gerekli adımları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="38234-120">Click on hello **Walkthrough** tab and review all necessary steps needed toopublish properly hello Data Service on hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="38234-121">Her zaman hello "İzlenecek" sayfasında hello bağlantılarında tıklatın veya hello sol tarafında hello veri hizmeti teklif'ın alt menüsünde sekmeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="38234-121">You always can click on hello links in hello “Walkthrough” page or use tabs on hello Data Service offer’s sub-menu on hello left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="38234-122">5.    Yeni bir Plan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38234-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="38234-123">, İşlemleri planları sunar.</span><span class="sxs-lookup"><span data-stu-id="38234-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="38234-124">Her teklif birden çok planına sahip olabilir, ancak en az birine (1) planı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="38234-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="38234-125">Son kullanıcılar tooyour teklif abone olduğunuzda bunların hello teklif'ın planı biri için abone olun.</span><span class="sxs-lookup"><span data-stu-id="38234-125">When end-users subscribe tooyour offer they subscribe for one of hello offer’s Plan.</span></span> <span data-ttu-id="38234-126">Her plan nasıl son kullanıcılar tanımlar hizmetinizi mümkün toouse olabilir.</span><span class="sxs-lookup"><span data-stu-id="38234-126">Each plan defines how end-users will be able toouse your service.</span></span>

<span data-ttu-id="38234-127">Şu anda Azure Marketi yalnızca aylık abonelik işlem tabanlı model verileri için Destek Hizmetleri, yani son kullanıcılar toohello fiyat hello belirli planının, bunlar abone tooand göre aylık ücret ödemeniz mümkün tooconsume her ay sayısı olacaktır Merhaba planı tarafından tanımlanan işlem.</span><span class="sxs-lookup"><span data-stu-id="38234-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according toohello price of hello specific plan they subscribed tooand will be able tooconsume each month number of transaction defined by hello plan.</span></span>

<span data-ttu-id="38234-128">Genelde, veri hizmeti döndürülecek kayıt sayısı tanımlanan her bir işlem toohello hizmet gönderilen hello sorgusuna dayalı olarak.</span><span class="sxs-lookup"><span data-stu-id="38234-128">Each Transaction usually defined as number of records your Data Service will return based on hello query sent toohello Service.</span></span> <span data-ttu-id="38234-129">Merhaba, 100 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="38234-129">hello default is 100.</span></span> <span data-ttu-id="38234-130">İşlem sayısı döndürülen tooeach sorgu kayıt sayısı 100'e bölünmüş ve toohello en yakın tamsayı yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="38234-130">Number of transactions returned tooeach query will be number of records divided by 100 and rounded up toohello closest integer.</span></span>

<span data-ttu-id="38234-131">Azure Market hizmet katmanı sorumluluk toomonitor (ölçüm) sayısı her sorgu tarafından tüketilen işlemleri sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="38234-131">It’s Azure Marketplace Service layer responsibility toomonitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38234-132">Merhaba işlem sınırına hello ay sırasında son kullanıcılar kendi aylık abonelik döngüsünün sonuna kadar toouse hello hizmeti devam etmesini engellenir.</span><span class="sxs-lookup"><span data-stu-id="38234-132">End-Users which reached hello transaction limit during hello month will be blocked from continuing toouse hello service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="38234-133">Merhaba işlemleri sınırsız sayıda plan veya hello planlarından birini yapabilirsiniz ancak değil gerekir içerir.</span><span class="sxs-lookup"><span data-stu-id="38234-133">hello plan or one of hello plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="38234-134">Bir plan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38234-134">Create a plan.</span></span>
1. <span data-ttu-id="38234-135">Tıklayın **"+"** sonraki toohello "yeni bir plan Ekle".</span><span class="sxs-lookup"><span data-stu-id="38234-135">Click on **“+”** next toohello “Add a new plan”.</span></span>
2. <span data-ttu-id="38234-136">Merhaba seçeneklerden birini seçin: **sınırsız** veya **sınırlı** Bu plan için kullanım.</span><span class="sxs-lookup"><span data-stu-id="38234-136">Choose one of hello options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="38234-137">Tooconsume, sınırlı hareket hello planı hello sayısı ardından sağlarsanız, bir ay içinde izin verir.</span><span class="sxs-lookup"><span data-stu-id="38234-137">If Limited then provide hello number of transaction hello plan will allow tooconsume in a month.</span></span>
   
    ![Çizim](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="38234-139">Portal yayımlama son kullanıcılara hello UI hello planın adı hello ve ayrıca hello markette hizmet tooidentify hello planı tarafından kullanılan kullanılan toocommunicate toohello olacağı "Planı tanımlayıcısı" de önerir.</span><span class="sxs-lookup"><span data-stu-id="38234-139">Publishing Portal will also suggest “Plan Identifier”, which will be used toocommunicate toohello end-users hello name of hello plan in hello UI and also used by hello Market Place Service tooidentify hello Plan.</span></span> <span data-ttu-id="38234-140">İsterseniz, "Plan tanımlayıcısı" Merhaba değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38234-140">You can change hello “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="38234-141">Merhaba "Plan tanımlayıcısı" Merhaba her teklif kapsamında benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="38234-141">hello “Plan Identifier” must be unique within hello scope of each offer.</span></span> <span data-ttu-id="38234-142">Kullanılan sayıda tanımlayıcıları yayımlama Portal planlama hello ilk yayımlama tooproduction ve mümkün toochange olmaz sonra tanımlayıcısı kilitli bu tanımlayıcı hello.</span><span class="sxs-lookup"><span data-stu-id="38234-142">As many other Identifiers used in hello Publishing Portal Plan identifier will be locked after hello first publishing tooproduction and you will not be able toochange this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="38234-143">Tooaccept tercih ettiğiniz'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="38234-143">Click tooaccept your choice.</span></span>
4. <span data-ttu-id="38234-144">Ardından, birkaç ek soruları yeni oluşturulan planınız istenir.</span><span class="sxs-lookup"><span data-stu-id="38234-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![Çizim](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="38234-146">Soru</span><span class="sxs-lookup"><span data-stu-id="38234-146">Question</span></span> | <span data-ttu-id="38234-147">Anlamlı</span><span class="sxs-lookup"><span data-stu-id="38234-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="38234-148">**Bu Plan hazır ve kullanılabilir dünya çapında mi?**</span><span class="sxs-lookup"><span data-stu-id="38234-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="38234-149">Tamamen ücretsiz-in-ücret planı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38234-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="38234-150">Bu teklif için – yalnızca cihazın hello düşünüyorsanız, "Ücretsiz teklif" Merhaba Market yayımladığınız olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="38234-150">If it’s hello only plan for this offer – it means that you are publishing “Free Offer” in hello Marketplace.</span></span> <span data-ttu-id="38234-151">Yalnızca biri (az) için ise planı, Merhaba, size bir seçenek toooffer son kullanıcılar toolearn hizmetiniz görece küçük bir aylık işlem sayısı ile ilgili daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="38234-151">If it’s only for one (of few) Plan, hello it gives you an option toooffer end-users toolearn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="38234-152">Merhaba yanıt "Evet" ise, daha fazla soru istenir.</span><span class="sxs-lookup"><span data-stu-id="38234-152">If hello answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="38234-153">Son kullanıcıların her zaman planları Ücretli toohello yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38234-153">End users can always upgrade toohello paid plans.</span></span>
> 
> 

| <span data-ttu-id="38234-154">Soru</span><span class="sxs-lookup"><span data-stu-id="38234-154">Question</span></span> | <span data-ttu-id="38234-155">Anlamlı</span><span class="sxs-lookup"><span data-stu-id="38234-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="38234-156">**Ücretsiz deneme sürümü var mı?**</span><span class="sxs-lookup"><span data-stu-id="38234-156">**Is free trial available?**</span></span> |<span data-ttu-id="38234-157">"Hayır deneme" arasında hiç seçin veya planınız "Bir ay" için bir seçenek toouse verin.</span><span class="sxs-lookup"><span data-stu-id="38234-157">You can choose between “No Trial” at all or give an option toouse your Plan for “One Month”.</span></span> <span data-ttu-id="38234-158">Yayımcılar bu seçeneği tooprovide son kullanıcılar hello olasılığı toounderstand hello Merhaba, ücretsiz bir aylık yararlar toouse ister.</span><span class="sxs-lookup"><span data-stu-id="38234-158">Publishers like toouse this option tooprovide end-users hello possibility toounderstand hello benefits of hello offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="38234-159">Ödeme yöntemini kredi kartı ör, Kurumsal Anlaşma kurduysanız son kullanıcılar yalnızca mümkün toopurchase ücretsiz deneme sürümü.</span><span class="sxs-lookup"><span data-stu-id="38234-159">End-users will only be able toopurchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="38234-160">Merhaba müşteri hello aboneliği iptal başlatılan sürece hello ücretsiz deneme sürümü, bir ay sonra müşteriler hello fiyat hello aboneliğin hello tarih itibariyle şarj Azure Marketi başlar.</span><span class="sxs-lookup"><span data-stu-id="38234-160">After one month of hello free trial, Azure Marketplace will start charging customers hello price as of hello date of hello subscription, unless hello customer initiated hello subscription cancellation.</span></span> <span data-ttu-id="38234-161">Özel bildirim toohello son kullanıcılar sağlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="38234-161">No special notification will be provided toohello end-users.</span></span>
> 
> 

| <span data-ttu-id="38234-162">Soru</span><span class="sxs-lookup"><span data-stu-id="38234-162">Question</span></span> | <span data-ttu-id="38234-163">Anlamlı</span><span class="sxs-lookup"><span data-stu-id="38234-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="38234-164">**Bu plan bir promosyon kodu toopurchase gerektiriyor?**</span><span class="sxs-lookup"><span data-stu-id="38234-164">**This plan requires a promotion code toopurchase?**</span></span> |<span data-ttu-id="38234-165">Yayımcılar, "A Promocode" toospecific müşteriler adlı özel bir kod sağlayarak bir seçenek toolimit erişim tootheir hizmet planları vardır.</span><span class="sxs-lookup"><span data-stu-id="38234-165">Publishers have an option toolimit access tootheir Service Plans by providing a special code, called “A Promocode” toospecific customers.</span></span> <span data-ttu-id="38234-166">Bu Promocode olan son kullanıcıların mümkün toosubscribe toohello planı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="38234-166">Only end-users which will have this Promocode will be able toosubscribe toohello Plan.</span></span> <span data-ttu-id="38234-167">"Hayır" seçin, ardından herkes burada hello teklif hello bölgesinden kullanılabilir olduğunu kabul ediyorum, (bkz [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) daha fazla ayrıntı için) mümkün toosubscribe toothis planı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="38234-167">If you choose “No”, then you agree that everyone from hello region where hello offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able toosubscribe toothis plan.</span></span> <span data-ttu-id="38234-168">Daha fazla soru istenir.</span><span class="sxs-lookup"><span data-stu-id="38234-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="38234-169">**Ayrıca geçerli promosyon kodu yok herkes bu plandan Gizle?**</span><span class="sxs-lookup"><span data-stu-id="38234-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="38234-170">Merhaba yanıt toohello önceki sorunun "Evet" Merhaba yayımcı hello hello Market UI görünmesini bu planı kaldırma seçeneği toocompletely sahiptir.</span><span class="sxs-lookup"><span data-stu-id="38234-170">If hello answer toohello previous question is “Yes” hello Publisher has an option toocompletely remove this plan from appearing in hello UI of hello Marketplace.</span></span> <span data-ttu-id="38234-171">Bu anlamına gelir, müşteriler bu plana hello teklif'in ayrıntılar sayfası görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="38234-171">It means, customers will not see this plan in hello Offer’s details page.</span></span> <span data-ttu-id="38234-172">Promocode toopurchase alacak son kullanıcılar, olacaktır mümkün toosubscribe tooit bu promocode kullanarak.</span><span class="sxs-lookup"><span data-stu-id="38234-172">End-users which will receive a promocode toopurchase it, will be able toosubscribe tooit using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="38234-173">6.    İçerik pazarlama, Market oluşturma</span><span class="sxs-lookup"><span data-stu-id="38234-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="38234-174">Tooprovide bilgileri nasıl gerekli için **pazarlama, fiyatlandırma, destek ve kategorileri** sekmeleri ziyaret edin [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) hello yayımlanan ortak tooall yapıları olduğu Azure Market.</span><span class="sxs-lookup"><span data-stu-id="38234-174">For How tooprovide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common tooall artifacts published in hello Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="38234-175">7.    Teklif tooyour hizmet (SQL tabanlı Azure veya Web tabanlı hizmet) bağlayın.</span><span class="sxs-lookup"><span data-stu-id="38234-175">7.    Connect your offer tooyour Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="38234-176">Tıklatın hello üzerinde **Veri Hizmetleri** alt menüsünde.</span><span class="sxs-lookup"><span data-stu-id="38234-176">Click on hello **Data Services** sub-menu.</span></span>

<span data-ttu-id="38234-177">Merhaba üst kısmında hello sayfası üzerinde tooprovide hello teklif'ın istenir, **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="38234-177">On hello upper half of hello page you’ll be asked tooprovide hello offer’s **Namespace**.</span></span>  

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="38234-179">Soru aşağıda Hello hello yayımcı yeni oluşturulan tooexpose teklif tooAzure Market nasıl gittiğini tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="38234-179">hello below question will define how hello Publisher is going tooexpose newly created offer tooAzure Marketplace.</span></span> <span data-ttu-id="38234-180">(Merhaba daha fazla ayrıntı görmek için [Veri Hizmetleri Teknik önkoşul Kılavuzu](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="38234-180">(For more details see hello [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="38234-182">**Yayımlama Hello veritabanı hizmet tabanlı**</span><span class="sxs-lookup"><span data-stu-id="38234-182">**Publishing hello Database based service**</span></span>

<span data-ttu-id="38234-183">Tıklayın **veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="38234-183">Click on **Database**.</span></span> <span data-ttu-id="38234-184">Sayfa aşağıdaki hello görünür:</span><span class="sxs-lookup"><span data-stu-id="38234-184">hello following page will appear:</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="38234-186">toocreate CSDL eşleme hello veri kümesi için SQL Azure DB'de hello üzerinde temel:</span><span class="sxs-lookup"><span data-stu-id="38234-186">toocreate a CSDL mapping for hello Dataset based on hello SQL Azure DB:</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="38234-188">Ve ardından her tablo için</span><span class="sxs-lookup"><span data-stu-id="38234-188">And then for each table</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="38234-191">Web hizmeti</span><span class="sxs-lookup"><span data-stu-id="38234-191">If Web Service</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="38234-193">Okuma [var olan eşleme web hizmeti tooOData CSDL aracılığıyla](marketplace-publishing-data-service-creation-odata-mapping.md) ayrıntılı yönergeler ve örnekler CSDL Web hizmeti oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="38234-193">Read [Mapping an existing web service tooOData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="38234-194">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="38234-194">Next Steps</span></span>
<span data-ttu-id="38234-195">Veri Hizmeti teklifiniz oluşturduğunuza göre hello hello yönergeleri tamamlandığından emin olmak [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) İleri çok taşımadan önce[hazırlama,verihizmetitestetme](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="38234-195">Now that you've created your Data Service offer, please ensure that you complete hello instructions in hello [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward too[Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="38234-196">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="38234-196">See Also</span></span>
* [<span data-ttu-id="38234-197">Başlarken: Nasıl toopublish bir teklif toohello Azure Market</span><span class="sxs-lookup"><span data-stu-id="38234-197">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="38234-198">İçinde anlama ilgileniyorsanız hello genel OData eşleme işlemi ve amacı, bu makalede okuma [veri hizmeti OData eşleme](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview tanımları, yapılar ve yönergeler.</span><span class="sxs-lookup"><span data-stu-id="38234-198">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="38234-199">Öğrenme ve anlama hello belirli düğümler ve bunların parametrelerini ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme düğümleri](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) tanımları ve açıklamalar, örnekler ve kullanım örneği bağlamı.</span><span class="sxs-lookup"><span data-stu-id="38234-199">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="38234-200">Örnekler gözden geçirme ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme örnekler](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee örnek kod ve kod sözdizimi ve bağlam anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="38234-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com

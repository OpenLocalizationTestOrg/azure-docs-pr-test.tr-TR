---
title: Veri Hizmeti Merhaba Market teklifi aaaTesting | Microsoft Docs
description: "Nasıl tootest, veri hizmeti sunan hello Azure Marketi anlayın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="476b5-103">Veri Hizmeti teklifiniz hazırlamada test etme</span><span class="sxs-lookup"><span data-stu-id="476b5-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="476b5-104">**Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.**</span><span class="sxs-lookup"><span data-stu-id="476b5-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="476b5-105">Bir SaaS iş uygulaması varsa toopublish istediğiniz AppSource hakkında daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="476b5-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="476b5-106">Bir Iaas uygulamalar varsa veya Geliştirici hizmeti misiniz Azure Market'te toopublish gibi daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="476b5-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="476b5-107">Merhaba ilk iki adımları tamamladıktan sonra [, Microsoft Developer hesabı oluşturma](marketplace-publishing-accounts-creation-registration.md) ve [yayımlama portalında oluşturma, veri hizmeti sunan](marketplace-publishing-data-service-creation.md) teklifiniz hello kullanılabilir yapmak için hazır Azure Market.</span><span class="sxs-lookup"><span data-stu-id="476b5-107">After completing hello first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in hello Azure Marketplace.</span></span> <span data-ttu-id="476b5-108">Bu konuda hello ilk adım, Orta, çağrılan "Hazırlama" adım</span><span class="sxs-lookup"><span data-stu-id="476b5-108">This topic will walk you through hello first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="476b5-109">Hazırlama teklifiniz özel ", test ve tooproduction göndermeden önce işlevselliğini doğrulayın sandbox" dağıtma anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="476b5-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="476b5-110">Merhaba teklif hazırlama dağıtmış olan tooa müşteri gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="476b5-110">hello offer will appear in staging just as it would tooa customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-toostaging"></a><span data-ttu-id="476b5-111">1. Adım</span><span class="sxs-lookup"><span data-stu-id="476b5-111">Step 1.</span></span> <span data-ttu-id="476b5-112">Teklif toostaging iletme</span><span class="sxs-lookup"><span data-stu-id="476b5-112">Pushing your offer toostaging</span></span>
<span data-ttu-id="476b5-113">Teklif toostaging Ftp'den kullanılabilir toofuture aboneleri duruma gelmesi tootest hello teklif da sağlar.</span><span class="sxs-lookup"><span data-stu-id="476b5-113">Pushing your offer toostaging allows you tootest hello offer before it becomes available toofuture subscribers.</span></span>  <span data-ttu-id="476b5-114">Teklifiniz nasıl görüntülenir ve tooyour veri abone olanlar için işlev görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="476b5-114">You can see how your offer will appear and function for those subscribing tooyour data.</span></span>  

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="476b5-116">Merhaba oturum [Yayımlama Portalı](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="476b5-116">Login into hello [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="476b5-117">Seçin **Veri Hizmetleri** hello sol gezinti penceresinde</span><span class="sxs-lookup"><span data-stu-id="476b5-117">Select **Data Services** in hello left navigation window</span></span>
3. <span data-ttu-id="476b5-118">Teklifiniz toopush toostaging istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="476b5-118">Select your offer you want toopush toostaging.</span></span> <span data-ttu-id="476b5-119">Başlangıç ekranı üzerinde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="476b5-119">You will see hello above screen.</span></span>
4. <span data-ttu-id="476b5-120">Tıklatın **anında tooStaging** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="476b5-120">Click **Push tooStaging** button.</span></span>  
5. <span data-ttu-id="476b5-121">Bir sorun varsa ile Merhaba önceki toopushing toostaging toobe gerekli teklif tamamlandı, görüntülenen bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="476b5-121">If there are issues with hello offer that needed toobe completed prior toopushing toostaging, you will see a list displayed.</span></span>  <span data-ttu-id="476b5-122">Bu öğeler hello listedeki her öğeye tıklayarak düzeltin.</span><span class="sxs-lookup"><span data-stu-id="476b5-122">Correct these items by clicking on each item in hello list.</span></span> <span data-ttu-id="476b5-123">Yapılan, tüm düzeltmeler tıklattığınızda **anında tooStaging** yeniden düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="476b5-123">When all corrections made, click **Push tooStaging** button again.</span></span>

<span data-ttu-id="476b5-124">Teklifiniz hiçbir sorun varsa hello açılır pencere görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="476b5-124">If there are no issues with your offer you will see hello popup window below.</span></span>  

<span data-ttu-id="476b5-125">Siz değilseniz, planlama değil onaylanan toosurface teklifiniz Azure Portalı'nda (şu anda sınırlı kapasite), sonra yalnızca Kapat hello açılır penceresi.</span><span class="sxs-lookup"><span data-stu-id="476b5-125">If you’re not planning/not approved toosurface your offer in Azure Portal (currently has limited capacity), then just close hello pop-up window.</span></span>

<span data-ttu-id="476b5-126">tootest, verilerinizi Azure Portalı'nda (toplama toohello DataMarket Portalı'nda) hizmet ile bir Azure abonelik kimliği tootest gerekir.</span><span class="sxs-lookup"><span data-stu-id="476b5-126">tootest your Data Service in Azure Portal (in addition toohello DataMarket portal), you will need an Azure Subscription ID tootest with.</span></span>  <span data-ttu-id="476b5-127">Bu abonelik kimliği olacak hello hesabını tanımlayacak tootest teklifiniz izin verilir.</span><span class="sxs-lookup"><span data-stu-id="476b5-127">This Subscription ID will identify hello account that will be allowed tootest your offer.</span></span>  

<span data-ttu-id="476b5-128">Kesme ve abonelik Kimliğinizi yapıştırın ve hello onay işareti toocontinue'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="476b5-128">Cut and paste your Subscription ID and click hello checkmark toocontinue.</span></span>

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="476b5-130">Bu Azure abonelik kimlikleri yalnızca olan test etme ve hello hazırlama için gereken [Azure Yönetim Portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="476b5-130">These Azure subscriptions IDs are only required for testing and staging in hello [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="476b5-131">Bunlar Azure markette gerekli tootest değildir.</span><span class="sxs-lookup"><span data-stu-id="476b5-131">They are not required tootest in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="476b5-132">Merhaba görüntülenen sonraki ekranında yayımlama hello "Sürüyor" görüntüleyerek yer aldığını gösterir simgesi sarı aşağıdaki vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="476b5-132">hello next screen that appears shows that publishing is taking place by displaying hello “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="476b5-133">Toostaging Ftp'den arasında 10 too15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="476b5-133">Pushing toostaging takes between 10 too15 minutes.</span></span>  <span data-ttu-id="476b5-134">İlk uzun sürüyorsa, tarayıcınızı (IE içinde F5 tuşuna basın) yenileyin.</span><span class="sxs-lookup"><span data-stu-id="476b5-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="476b5-135">Burada teklifiniz hala toostaging bir saat sonra Ftp'den olduğu hello nadir durumlarda, bize bir sorun olduğunu bize toolet bağlantı hello kişiyi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="476b5-135">In hello rare cases where your offer is still pushing toostaging after an hour, click hello contact us link toolet us know that there is an issue.</span></span>

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="476b5-137">Merhaba itme tooStaging hello tamamlandığında "Sürüyor" taşıma simgesi durdurur ve çok "hazırlanmış" Merhaba durumu güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="476b5-137">When hello Push tooStaging completes hello “In progress” icon will stop moving and hello status will be updated too“Staged”.</span></span>  <span data-ttu-id="476b5-138">Artık hazır tootest teklifiniz şunlardır.</span><span class="sxs-lookup"><span data-stu-id="476b5-138">You are now ready tootest your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="476b5-139">2. Adım</span><span class="sxs-lookup"><span data-stu-id="476b5-139">Step 2.</span></span> <span data-ttu-id="476b5-140">DataMarket içinde hazırlanmış teklifiniz test</span><span class="sxs-lookup"><span data-stu-id="476b5-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="476b5-141">Merhaba metin aşağıdaki hello bağlantısına tıklayın **"adresindeki teklif hizmetinizi bkz..."**</span><span class="sxs-lookup"><span data-stu-id="476b5-141">Click hello link following hello text **“See Your service offer at…”**</span></span> <span data-ttu-id="476b5-142">Abone hello toodisplay Merhaba ekranında teklifiniz tooproduction gittiğinde görürsünüz ve DataMarket içinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="476b5-142">toodisplay hello screen that hello subscriber will see when your offer goes tooproduction and will appear in DataMarket.</span></span>

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="476b5-144">Test veya hello 12 öğelerin her birini tooensure olarak işaretlenmiş tüm logolar, Fiyatlar/işlemleri, metin, görüntüler, belgeleri ve bağlantıları düzgün doğru ve çalışıyor olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="476b5-144">Test or verify each of hello 12 items marked above tooensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="476b5-145">Teklifiniz oluştururken girdiğiniz tüm test değerleri gerçek değerlerle değiştirilmiştir iyi zaman tooensure budur.</span><span class="sxs-lookup"><span data-stu-id="476b5-145">This is a good time tooensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="476b5-146">Teklif logosu</span><span class="sxs-lookup"><span data-stu-id="476b5-146">Offer logo</span></span>
2. <span data-ttu-id="476b5-147">Teklif adı</span><span class="sxs-lookup"><span data-stu-id="476b5-147">Offer name</span></span>
3. <span data-ttu-id="476b5-148">Yayımcı adı/bağlantı tooyour şirketinizin Web sitesi</span><span class="sxs-lookup"><span data-stu-id="476b5-148">Publisher name/link tooyour company's website</span></span>
4. <span data-ttu-id="476b5-149">Teklifiniz için arama kategorileri</span><span class="sxs-lookup"><span data-stu-id="476b5-149">Search categories for your offer</span></span>
5. <span data-ttu-id="476b5-150">Teklifiniz 's destek bağlantı tooassist aboneleri</span><span class="sxs-lookup"><span data-stu-id="476b5-150">Your offer's support link tooassist subscribers</span></span>
6. <span data-ttu-id="476b5-151">Teklifiniz için bağlamsal açıklaması</span><span class="sxs-lookup"><span data-stu-id="476b5-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="476b5-152">Fatura Ayrıntıları gösteren teklif planı</span><span class="sxs-lookup"><span data-stu-id="476b5-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="476b5-153">Bağlantı tooimplementation kodu</span><span class="sxs-lookup"><span data-stu-id="476b5-153">Link tooimplementation code</span></span>
9. <span data-ttu-id="476b5-154">Teklif verilerini gösteren örnek görüntüleri kullanın</span><span class="sxs-lookup"><span data-stu-id="476b5-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="476b5-155">Merhaba teklif içinde her hizmet için giriş/çıkış meta verileri</span><span class="sxs-lookup"><span data-stu-id="476b5-155">Input/Output metadata for each service within hello offer</span></span>
11. <span data-ttu-id="476b5-156">Teklif'ın kullanım koşulları</span><span class="sxs-lookup"><span data-stu-id="476b5-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="476b5-157">Merhaba teklif'ın veri önizlemesi</span><span class="sxs-lookup"><span data-stu-id="476b5-157">Preview of hello offer's data</span></span>

<span data-ttu-id="476b5-158">Son olarak, onay hello hizmeti, "Keşfedin bu veri KÜMESİ" Merhaba bağlantıyı tıklatarak Datamarket hello çalışır.</span><span class="sxs-lookup"><span data-stu-id="476b5-158">Finally, check hello service will work through hello Datamarket by clicking hello link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="476b5-159">Yeni bir pencerede açılır hizmetinize karşı hello bir sorgunun sonuçlarını önizlemek için hello aracında "Hizmet Gezgini" diyoruz.</span><span class="sxs-lookup"><span data-stu-id="476b5-159">A new window will open in hello tool we call “Service Explorer” so you can preview hello results of a query against your service.</span></span>  <span data-ttu-id="476b5-160">Bu pencerede, parametreleri gerektiği ve hizmetinizi sorgusundan görüntülenen hello sonuçları görmek hello girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="476b5-160">In this window, you can enter hello parameters needed and see hello results displayed from a query against your service.</span></span>   <span data-ttu-id="476b5-161">Ayrıca, görüntülenen hello URL sorgunuz için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="476b5-161">Also, displayed is hello URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="476b5-162">Hello üstünde görüntülenen hello hizmetinin emin tooreview hello metinsel açıklaması olabilir.</span><span class="sxs-lookup"><span data-stu-id="476b5-162">Be sure tooreview hello textual description of hello service displayed at hello top.</span></span>  <span data-ttu-id="476b5-163">Teklifiniz birden fazla hizmeti oluşur, çağrı, hello alt tooswitch toohello sonraki hizmet tooreview hello sekmeleri tıklatın ve test.</span><span class="sxs-lookup"><span data-stu-id="476b5-163">And if your offer consists of more than one service call, click hello tabs at hello bottom tooswitch toohello next service tooreview and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="476b5-164">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="476b5-164">Next step</span></span>
<span data-ttu-id="476b5-165">Sorunu yaşıyor ve Yardım ihtiyacınız varsa bunları çözme Lütfen kişi [Azure yayımcı desteğine](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="476b5-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="476b5-166">Memnun ve hazır toopublish teklifiniz okuyun hello [isteği onayı tooPush tooProduction](marketplace-publishing-push-to-production.md) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="476b5-166">If you are satisfied and ready toopublish your offer please read hello [Request Approval tooPush tooProduction](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="476b5-167">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="476b5-167">See Also</span></span>
* [<span data-ttu-id="476b5-168">Başlarken: Nasıl toopublish bir teklif toohello Azure Market</span><span class="sxs-lookup"><span data-stu-id="476b5-168">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)


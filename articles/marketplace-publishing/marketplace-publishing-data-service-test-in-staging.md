---
title: "Veri Hizmeti teklifiniz Market için test etme | Microsoft Docs"
description: "Veri Hizmeti teklifiniz Azure Marketi için test etme anlayın."
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
ms.openlocfilehash: 56a8aad7484fed18b74200ffa7acf22363625a15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="daf65-103">Veri Hizmeti teklifiniz hazırlamada test etme</span><span class="sxs-lookup"><span data-stu-id="daf65-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="daf65-104">**Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.**</span><span class="sxs-lookup"><span data-stu-id="daf65-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="daf65-105">Üzerinde AppSource yayımlamak istediğiniz bir SaaS iş uygulaması varsa daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="daf65-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="daf65-106">Bir Iaas uygulamalar varsa veya Azure marketi, yayımlamak istediğiniz Geliştirici hizmet, daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="daf65-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="daf65-107">İlk iki adımları tamamladıktan sonra [, Microsoft Developer hesabı oluşturma](marketplace-publishing-accounts-creation-registration.md) ve [yayımlama portalında oluşturma, veri hizmeti sunan](marketplace-publishing-data-service-creation.md) teklifiniz Azure kullanılabilir yapmak için hazır Market.</span><span class="sxs-lookup"><span data-stu-id="daf65-107">After completing the first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in the Azure Marketplace.</span></span> <span data-ttu-id="daf65-108">Bu konuda ilk Ara "Hazırlama" adlı adım yol gösterir</span><span class="sxs-lookup"><span data-stu-id="daf65-108">This topic will walk you through the first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="daf65-109">Hazırlama teklifiniz özel ", test ve üretim göndermeden önce işlevselliğini doğrulayın sandbox" dağıtma anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="daf65-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="daf65-110">Teklif hazırlama dağıtmış olan bir müşteriye gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="daf65-110">The offer will appear in staging just as it would to a customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-to-staging"></a><span data-ttu-id="daf65-111">1. Adım</span><span class="sxs-lookup"><span data-stu-id="daf65-111">Step 1.</span></span> <span data-ttu-id="daf65-112">Teklifiniz hazırlama için iletme</span><span class="sxs-lookup"><span data-stu-id="daf65-112">Pushing your offer to staging</span></span>
<span data-ttu-id="daf65-113">Hazırlama teklif Ftp'den gelecekteki abonelere kullanılabilir olmadan önce teklif test etmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="daf65-113">Pushing your offer to staging allows you to test the offer before it becomes available to future subscribers.</span></span>  <span data-ttu-id="daf65-114">Teklifiniz nasıl görüntülenir ve bunlar verilerinizi abone için işlev görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daf65-114">You can see how your offer will appear and function for those subscribing to your data.</span></span>  

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="daf65-116">Oturum [portalını yayımlama](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="daf65-116">Login into the [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="daf65-117">Seçin **Veri Hizmetleri** sol gezinti penceresinde</span><span class="sxs-lookup"><span data-stu-id="daf65-117">Select **Data Services** in the left navigation window</span></span>
3. <span data-ttu-id="daf65-118">Hazırlama için anında istediğiniz teklifiniz seçin.</span><span class="sxs-lookup"><span data-stu-id="daf65-118">Select your offer you want to push to staging.</span></span> <span data-ttu-id="daf65-119">Yukarıdaki ekran görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="daf65-119">You will see the above screen.</span></span>
4. <span data-ttu-id="daf65-120">Tıklatın **hazırlama anında** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="daf65-120">Click **Push To Staging** button.</span></span>  
5. <span data-ttu-id="daf65-121">Hazırlama için itme önce tamamlanması gereken teklif ile ilgili sorunlar varsa, görüntülenen bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="daf65-121">If there are issues with the offer that needed to be completed prior to pushing to staging, you will see a list displayed.</span></span>  <span data-ttu-id="daf65-122">Bu öğeler, listedeki her öğeye tıklayarak düzeltin.</span><span class="sxs-lookup"><span data-stu-id="daf65-122">Correct these items by clicking on each item in the list.</span></span> <span data-ttu-id="daf65-123">Yapılan, tüm düzeltmeler tıklattığınızda **anında için hazırlama** yeniden düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="daf65-123">When all corrections made, click **Push to Staging** button again.</span></span>

<span data-ttu-id="daf65-124">Teklifiniz ile herhangi bir sorun varsa açılır pencere görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="daf65-124">If there are no issues with your offer you will see the popup window below.</span></span>  

<span data-ttu-id="daf65-125">Değil planlama/değil teklifiniz Azure Portalı'nda ortaya çıkarma onaylanırsa (şu anda sınırlı kapasite), yalnızca açılır penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="daf65-125">If you’re not planning/not approved to surface your offer in Azure Portal (currently has limited capacity), then just close the pop-up window.</span></span>

<span data-ttu-id="daf65-126">Veri Hizmeti (DataMarket portalı ek olarak) Azure Portalı'nda test test etmek için bir Azure abonelik kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="daf65-126">To test your Data Service in Azure Portal (in addition to the DataMarket portal), you will need an Azure Subscription ID to test with.</span></span>  <span data-ttu-id="daf65-127">Bu abonelik kimliği teklifiniz test etmek için izin verilecek hesap tanımlar.</span><span class="sxs-lookup"><span data-stu-id="daf65-127">This Subscription ID will identify the account that will be allowed to test your offer.</span></span>  

<span data-ttu-id="daf65-128">Kesme ve abonelik Kimliğinizi yapıştırın ve devam etmek için onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="daf65-128">Cut and paste your Subscription ID and click the checkmark to continue.</span></span>

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="daf65-130">Bu Azure abonelik kimlikleri yalnızca olduğundan, hazırlama ve test için gereken [Azure Yönetim Portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="daf65-130">These Azure subscriptions IDs are only required for testing and staging in the [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="daf65-131">Azure Marketi'nde test olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="daf65-131">They are not required to test in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="daf65-132">Yayımlama "Sürüyor" simge görüntüleyerek yer aldığını gösterir görüntülenen sonraki ekranında sarı aşağıdaki vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="daf65-132">The next screen that appears shows that publishing is taking place by displaying the “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="daf65-133">Hazırlama için itme arasında 10-15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="daf65-133">Pushing to staging takes between 10 to 15 minutes.</span></span>  <span data-ttu-id="daf65-134">İlk uzun sürüyorsa, tarayıcınızı (IE içinde F5 tuşuna basın) yenileyin.</span><span class="sxs-lookup"><span data-stu-id="daf65-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="daf65-135">Bizimle bağlantı kişiyi burada teklifiniz hala Ftp'den bir saat sonra hazırlama için nadir durumlarda tıklatın bir sorun olduğunu bize bildirin.</span><span class="sxs-lookup"><span data-stu-id="daf65-135">In the rare cases where your offer is still pushing to staging after an hour, click the contact us link to let us know that there is an issue.</span></span>

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="daf65-137">Hazırlama için anında iletme "Sürüyor" simgesini tamamlandığında Dur taşıma ve durumu "Aşamalı" güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="daf65-137">When the Push to Staging completes the “In progress” icon will stop moving and the status will be updated to “Staged”.</span></span>  <span data-ttu-id="daf65-138">Şimdi teklifiniz test etmek hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="daf65-138">You are now ready to test your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="daf65-139">2. Adım</span><span class="sxs-lookup"><span data-stu-id="daf65-139">Step 2.</span></span> <span data-ttu-id="daf65-140">DataMarket içinde hazırlanmış teklifiniz test</span><span class="sxs-lookup"><span data-stu-id="daf65-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="daf65-141">Metin aşağıdaki bağlantıyı tıklatın **"adresindeki teklif hizmetinizi bkz..."**</span><span class="sxs-lookup"><span data-stu-id="daf65-141">Click the link following the text **“See Your service offer at…”**</span></span> <span data-ttu-id="daf65-142">Abone teklifiniz üretime gittiğinde görür ve DataMarket içinde görünür ekranı görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="daf65-142">to display the screen that the subscriber will see when your offer goes to production and will appear in DataMarket.</span></span>

  ![Çizim](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="daf65-144">Test veya 12 öğelerin her birini tüm logolar, Fiyatlar/işlemleri, metin, görüntüler, belgeleri emin olmak için işaretlenmiş yukarıda ve bağlantıları düzgün doğru ve çalışıyor olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="daf65-144">Test or verify each of the 12 items marked above to ensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="daf65-145">Bu, gerçek değerlerle teklifiniz oluştururken girdiğiniz tüm test değerleri değiştirilmiştir emin olmak için iyi bir zamandır.</span><span class="sxs-lookup"><span data-stu-id="daf65-145">This is a good time to ensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="daf65-146">Teklif logosu</span><span class="sxs-lookup"><span data-stu-id="daf65-146">Offer logo</span></span>
2. <span data-ttu-id="daf65-147">Teklif adı</span><span class="sxs-lookup"><span data-stu-id="daf65-147">Offer name</span></span>
3. <span data-ttu-id="daf65-148">Yayımcı adı/bağlantı şirketinizin Web sitesi</span><span class="sxs-lookup"><span data-stu-id="daf65-148">Publisher name/link to your company's website</span></span>
4. <span data-ttu-id="daf65-149">Teklifiniz için arama kategorileri</span><span class="sxs-lookup"><span data-stu-id="daf65-149">Search categories for your offer</span></span>
5. <span data-ttu-id="daf65-150">Aboneler yardımcı olmak için teklifiniz 's destek bağlantısı</span><span class="sxs-lookup"><span data-stu-id="daf65-150">Your offer's support link to assist subscribers</span></span>
6. <span data-ttu-id="daf65-151">Teklifiniz için bağlamsal açıklaması</span><span class="sxs-lookup"><span data-stu-id="daf65-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="daf65-152">Fatura Ayrıntıları gösteren teklif planı</span><span class="sxs-lookup"><span data-stu-id="daf65-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="daf65-153">Uygulama kodu bağlantı</span><span class="sxs-lookup"><span data-stu-id="daf65-153">Link to implementation code</span></span>
9. <span data-ttu-id="daf65-154">Teklif verilerini gösteren örnek görüntüleri kullanın</span><span class="sxs-lookup"><span data-stu-id="daf65-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="daf65-155">Teklif içinde her hizmet için giriş/çıkış meta verileri</span><span class="sxs-lookup"><span data-stu-id="daf65-155">Input/Output metadata for each service within the offer</span></span>
11. <span data-ttu-id="daf65-156">Teklif'ın kullanım koşulları</span><span class="sxs-lookup"><span data-stu-id="daf65-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="daf65-157">Teklif ait veri önizlemesi</span><span class="sxs-lookup"><span data-stu-id="daf65-157">Preview of the offer's data</span></span>

<span data-ttu-id="daf65-158">Son olarak, hizmet Datamarket "Keşfedin bu veri KÜMESİ" bağlantısını tıklatarak çalışır denetleyin.</span><span class="sxs-lookup"><span data-stu-id="daf65-158">Finally, check the service will work through the Datamarket by clicking the link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="daf65-159">Yeni bir pencerede açılır hizmetinize karşı bir sorgunun sonuçlarını önizlemek için aracı "Hizmet Gezgini" diyoruz.</span><span class="sxs-lookup"><span data-stu-id="daf65-159">A new window will open in the tool we call “Service Explorer” so you can preview the results of a query against your service.</span></span>  <span data-ttu-id="daf65-160">Bu pencerede, gerekli parametreleri girin ve hizmetinizi sorgusundan görüntülenen sonuçlarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daf65-160">In this window, you can enter the parameters needed and see the results displayed from a query against your service.</span></span>   <span data-ttu-id="daf65-161">Ayrıca, görüntülenen URL'yi sorgunuz için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="daf65-161">Also, displayed is the URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="daf65-162">En üstte gösterilen hizmet metinsel açıklaması gözden geçirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="daf65-162">Be sure to review the textual description of the service displayed at the top.</span></span>  <span data-ttu-id="daf65-163">Ve teklifiniz birden fazla hizmeti oluşur, çağrı, gözden geçirin ve test etmek için İleri hizmetine geçiş yapmak için alttaki sekmeleri tıklatın.</span><span class="sxs-lookup"><span data-stu-id="daf65-163">And if your offer consists of more than one service call, click the tabs at the bottom to switch to the next service to review and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="daf65-164">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="daf65-164">Next step</span></span>
<span data-ttu-id="daf65-165">Sorunu yaşıyor ve Yardım ihtiyacınız varsa bunları çözme Lütfen kişi [Azure yayımcı desteğine](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="daf65-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="daf65-166">Memnun ve okuyun teklifiniz yayımlamak hazır olup olmadığını [isteği onayı üretime anında](marketplace-publishing-push-to-production.md) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="daf65-166">If you are satisfied and ready to publish your offer please read the [Request Approval to Push To Production](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="daf65-167">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="daf65-167">See Also</span></span>
* [<span data-ttu-id="daf65-168">Başlarken: nasıl bir teklifi Azure Marketinde yayımlama</span><span class="sxs-lookup"><span data-stu-id="daf65-168">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)


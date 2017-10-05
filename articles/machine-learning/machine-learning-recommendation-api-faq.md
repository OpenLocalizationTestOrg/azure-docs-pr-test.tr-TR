---
title: "Ayarlama ve Machine Learning önerileri API'si kullanma | Microsoft Docs"
description: "Microsoft önerileri Azure Machine Learning ile ilgili SSS ile yerleşik API"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 3851589818bb8f4309bf3c65f17b115e0dcd27fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="7d291-103">Machine Learning Öneri API’sini ayarlama ve kullanma hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="7d291-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="7d291-104">**ÖNERİLER nedir?**</span><span class="sxs-lookup"><span data-stu-id="7d291-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="7d291-105">Öneriler API Bilişsel hizmeti yerine bu sürümünü kullanarak başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d291-105">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="7d291-106">Öneriler Bilişsel hizmet bu hizmeti koyacağınız ve tüm yeni özellikler vardır geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7d291-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="7d291-107">Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="7d291-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="7d291-108">Daha fazla bilgi edinmek [yeni Bilişsel Service'e geçirme](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="7d291-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="7d291-109">Kuruluşlar ve çapraz satış için öneriler ve yukarı satış ürünleri ve Hizmetleri müşterilerine kullanan işletmeler için Azure Machine Learning önerileri bir Self Servis önerileri altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d291-109">For organizations and businesses that rely on recommendations to cross-sell and up-sell products and services to their customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="7d291-110">Bu matris factorization kendi çekirdek algoritması kullanan işbirliği filtrelemenin bir uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="7d291-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="7d291-111">Uygulama geliştiricilerinin önerileri REST API'lerini kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d291-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="7d291-112">**ÖNERİLERİ ne yapabilirim?**</span><span class="sxs-lookup"><span data-stu-id="7d291-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="7d291-113">ÖNERİLER bir öğe girişi veya öğeleri kümesi alır ve ilgili öneriler listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="7d291-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="7d291-114">Örneğin: bir çevrimiçi satıcısı müşterinin bir ürün tıklar.</span><span class="sxs-lookup"><span data-stu-id="7d291-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="7d291-115">Çevrimiçi satıcısında önerileri girdi olarak bu ürünü gönderir, ürünlerin listesini iade alır ve bu ürünlerin müşteriye gösterileceği karar verir.</span><span class="sxs-lookup"><span data-stu-id="7d291-115">The online retailer sends that product as input to RECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown to the customer.</span></span> <span data-ttu-id="7d291-116">Çevrimiçi mağazada en iyi duruma getirme veya bile, iç bildirmek için öneriler kullanmak isteyebilirsiniz satış departmanı veya Arama Merkezi.</span><span class="sxs-lookup"><span data-stu-id="7d291-116">You may want to use RECOMMENDATIONS to optimize your online store or even to inform your inside sales department or call center.</span></span>

<span data-ttu-id="7d291-117">**Kullanım sınırlamalar var mı?**</span><span class="sxs-lookup"><span data-stu-id="7d291-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="7d291-118">Önerileri şu kullanım sınırlamalara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="7d291-118">Recommendations has the following usage limitations:</span></span>

* <span data-ttu-id="7d291-119">Model abonelik başına en yüksek sayısı: 10</span><span class="sxs-lookup"><span data-stu-id="7d291-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="7d291-120">En fazla bir katalog tutabilir öğe sayısı: 100.000</span><span class="sxs-lookup"><span data-stu-id="7d291-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="7d291-121">En fazla tutulur kullanım noktaları ~ 5,000,000 sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="7d291-121">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="7d291-122">Yeni bir tane karşıya bildirilen veya gereken eski silinir.</span><span class="sxs-lookup"><span data-stu-id="7d291-122">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="7d291-123">200 MB (örneğin, veri içeri aktar katalog kullanım verileri İçeri Aktar) e-posta ile gönderilen verilerin en büyük boyut:</span><span class="sxs-lookup"><span data-stu-id="7d291-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="7d291-124">İşlemler (TP'ler) etkin değil önerileri modeli derlemesi için saniye başına ~ 2 TP'leri sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="7d291-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="7d291-125">Etkin bir önerileri modeli yapı en fazla 20 TP'leri basılı tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d291-125">A Recommendations model build that is active can hold up to 20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="7d291-126">Satın Alma ve Fatura</span><span class="sxs-lookup"><span data-stu-id="7d291-126">Purchase and Billing</span></span>
<span data-ttu-id="7d291-127">**Ne kadar önerileri maliyet başlatma süresi boyunca mu?**</span><span class="sxs-lookup"><span data-stu-id="7d291-127">**How much does Recommendations cost during the launch period?**</span></span>

<span data-ttu-id="7d291-128">Öneriler, bir abonelik tabanlı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="7d291-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="7d291-129">Şarj aylık işlem hacmi temel alır.</span><span class="sxs-lookup"><span data-stu-id="7d291-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="7d291-130">Kontrol edebilirsiniz [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations) fiyatlandırma bilgileri için Microsoft Azure Marketplace içinde.</span><span class="sxs-lookup"><span data-stu-id="7d291-130">You can check the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="7d291-131">**Öneriler sahip ile ilişkili maliyetlerin izlemek ve kullanıcı etkinliğini benim yerime depolamak var mı?**</span><span class="sxs-lookup"><span data-stu-id="7d291-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="7d291-132">Değil şu anda.</span><span class="sxs-lookup"><span data-stu-id="7d291-132">Not at the moment.</span></span>

<span data-ttu-id="7d291-133">**Öneriler ücretsiz deneme sürümü var mı?**</span><span class="sxs-lookup"><span data-stu-id="7d291-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="7d291-134">Aylık 10.000 işlemleri için kısıtlı olan ücretsiz bir izleme yoktur.</span><span class="sxs-lookup"><span data-stu-id="7d291-134">There is a free trail which is restricted to 10,000 transactions per month.</span></span>

<span data-ttu-id="7d291-135">**Ne zaman ı önerileri için Fatura edilecek?**</span><span class="sxs-lookup"><span data-stu-id="7d291-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="7d291-136">Ücretli bir abonelik var olduğu aylık bir ücret herhangi bir aboneliği ' dir.</span><span class="sxs-lookup"><span data-stu-id="7d291-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="7d291-137">Ücretli bir abonelik satın aldığınızda, ilk ayın kullanımı için hemen sizden ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="7d291-137">When you purchase a paid subscription, you are immediately charged for the first month's use.</span></span> <span data-ttu-id="7d291-138">Abonelik sayfası (artı geçerli vergileri) teklifini ilişkilendirilen tutar sizden ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="7d291-138">You are charged the amount that is associated with the offer on the subscription page (plus applicable taxes).</span></span> <span data-ttu-id="7d291-139">Aboneliğini iptal kadar her ay orijinal satın alma aynı takvim tarihte bu aylık ücret yapılır.</span><span class="sxs-lookup"><span data-stu-id="7d291-139">This monthly charge is made each month on the same calendar date as your original purchase until you cancel the subscription.</span></span> 

<span data-ttu-id="7d291-140">**Daha yüksek bir katman hizmet nasıl yükseltme?**</span><span class="sxs-lookup"><span data-stu-id="7d291-140">**How do I upgrade to a higher tier service?**</span></span>

<span data-ttu-id="7d291-141">Satın alma veya aboneliğinizden güncelleştirme [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations) Microsoft Azure Market sayfasında.</span><span class="sxs-lookup"><span data-stu-id="7d291-141">You can buy or update your subscription from the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="7d291-142">Bir abonelik yükseltme yaptığınızda:</span><span class="sxs-lookup"><span data-stu-id="7d291-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="7d291-143">Eski aboneliğinizi kalan işlemler yeni aboneliğinizi eklenmez.</span><span class="sxs-lookup"><span data-stu-id="7d291-143">Transactions that are remaining on your old subscription are not added to your new subscription.</span></span> 
* <span data-ttu-id="7d291-144">Olsa bile yeni abonelik için tam fiyat ödeme eski aboneliğinizi kullanılmayan hareketleri.</span><span class="sxs-lookup"><span data-stu-id="7d291-144">You pay full price for the new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="7d291-145">Bir abonelik yükseltme işlemi:</span><span class="sxs-lookup"><span data-stu-id="7d291-145">Process to upgrade a subscription:</span></span>

* <span data-ttu-id="7d291-146">İçin Nevigate [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="7d291-146">Nevigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="7d291-147">Oturum açmış değilseniz Market'te oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7d291-147">Sign in to the Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="7d291-148">Sağ bölmede, kullanılabilen tüm planlarla listelenir.</span><span class="sxs-lookup"><span data-stu-id="7d291-148">In the right pane, all the available plans are listed.</span></span> <span data-ttu-id="7d291-149">Yükseltmek istediğiniz planı için radyo düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d291-149">Click the radio button for the plan you want to upgrade to.</span></span>
* <span data-ttu-id="7d291-150">Yükseltmek istiyorsanız, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7d291-150">If you want to upgrade, click **OK**.</span></span> <span data-ttu-id="7d291-151">Yükseltmeye istemiyorsanız tıklayın **iptal**.</span><span class="sxs-lookup"><span data-stu-id="7d291-151">If you do not want to upgrade, click **Cancel**.</span></span>

<span data-ttu-id="7d291-152">**Önemli** iletişim kutusu faturalama ve kullanım uygulamalarını olduğundan yükseltme yapmadan önce dikkatle okuyun.</span><span class="sxs-lookup"><span data-stu-id="7d291-152">**Important** Carefully read the dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="7d291-153">**Ne zaman Aboneliğimi önerileri sona erecek mi?**</span><span class="sxs-lookup"><span data-stu-id="7d291-153">**When will my subscription to Recommendations end?**</span></span>

<span data-ttu-id="7d291-154">İptal ettiğinizde, aboneliğiniz sona erer.</span><span class="sxs-lookup"><span data-stu-id="7d291-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="7d291-155">Aboneliklerinizi iptal etmek istiyorsanız, aşağıdaki yönergelere bakın.</span><span class="sxs-lookup"><span data-stu-id="7d291-155">If you would like to cancel your subscriptions, see the following instructions.</span></span>

<span data-ttu-id="7d291-156">**Öneriler Aboneliğimi nasıl iptal edebilirim?**</span><span class="sxs-lookup"><span data-stu-id="7d291-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="7d291-157">Aboneliğinizi iptal etmek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d291-157">To cancel your subscription, use the following steps.</span></span> <span data-ttu-id="7d291-158">Geçerli aboneliğinizi Ücretli abonelik ise, aboneliğinizi yürürlükte geçerli fatura dönemi sonuna kadar devam eder.</span><span class="sxs-lookup"><span data-stu-id="7d291-158">If your current subscription is a paid subscription, your subscription continues in effect until the end of the current billing period.</span></span> <span data-ttu-id="7d291-159">İptal hemen etkin olması gerekiyorsa, adresinden bize başvurun [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="7d291-159">If you need the cancellation to be effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="7d291-160">**Not** bir fatura döneminde fatura döneminin veya kullanılmayan işlemler için bitmeden önce iptal ederseniz hiçbir para iadesi verilir.</span><span class="sxs-lookup"><span data-stu-id="7d291-160">**Note** No refund is given if you cancel before the end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="7d291-161">Gidin [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="7d291-161">Navigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="7d291-162">Oturum açmış değilseniz Market'te oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7d291-162">Sign in to the Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="7d291-163">Tıklatın **iptal** veri kümesi adı ve durum sağındaki.</span><span class="sxs-lookup"><span data-stu-id="7d291-163">Click **Cancel** to the right of the dataset name and status.</span></span> <span data-ttu-id="7d291-164">Bu abonelik geçerli fatura dönemi sonuna kadar kullanabilir veya (hangisi önce gerçekleşirse), işlem sınırına ulaştı.</span><span class="sxs-lookup"><span data-stu-id="7d291-164">You can use this subscription until the end of the current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="7d291-165">Bu nedenle yeni bir abonelik satın alabilirsiniz hemen aboneliğinizi iptal etmek istiyorsanız, bir bilet adresindeki dosya [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="7d291-165">If you would like to cancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="7d291-166">Öneriler ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7d291-166">Getting started with Recommendations</span></span>
<span data-ttu-id="7d291-167">**Öneriler benim için mi?**</span><span class="sxs-lookup"><span data-stu-id="7d291-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="7d291-168">Machine Learning önerileri organizasyonlar ve işletmeler arası satış önerileri ve yukarı satış ürünleri veya hizmetleri müşterilerine Bel içindir.</span><span class="sxs-lookup"><span data-stu-id="7d291-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations to cross-sell and up-sell products or services to their customers.</span></span> <span data-ttu-id="7d291-169">Varsa bir müşteri kullanıma yönelik Web sitesi, satış ekibi, bir iç satış ekibi ya da bir çağrı merkezi ve birkaç düzine ürünleri veya hizmetleri kataloğunu teklifi sunuyorsanız, alt çizgi önerileri kullanarak yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7d291-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="7d291-170">Önerileri denemeler oldukça basit olacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7d291-170">Experimenting with Recommendations is designed to be fairly simple.</span></span> <span data-ttu-id="7d291-171">Geçerli API tabanlı sürümünü temel programlama becerileri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7d291-171">The current API-based version requires basic programming skills.</span></span> <span data-ttu-id="7d291-172">Yardıma gereksinim duyarsanız, kimin Web sitenizi geliştirilen satıcısına başvurun.</span><span class="sxs-lookup"><span data-stu-id="7d291-172">If you need assistance, contact the vendor who developed your website.</span></span> <span data-ttu-id="7d291-173">Bir iç BT departmanına ya da şirket içi bir geliştirici varsa, bunlar işinize önerileri almak mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d291-173">If you have an internal IT department or an in-house developer, they should be able to get Recommendations to work for you.</span></span> 

<span data-ttu-id="7d291-174">**Önerileri ayarı önkoşulları nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="7d291-174">**What are the prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="7d291-175">Öneriler kataloğunuza ilgili olarak kullanıcı seçimlerini günlüğünü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d291-175">Recommendations requires that you have a log of user choices as it relates to your catalog.</span></span> <span data-ttu-id="7d291-176">Bu tür bir günlük yoksa ve bir müşteri kullanıma yönelik Web sitesi varsa, Öneriler size kullanıcı etkinliği toplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d291-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="7d291-177">Öneriler, ürünleri veya hizmetleri kataloğunu de gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7d291-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="7d291-178">Katalog yoksa, öneriler gerçek müşteri kullanım verilerini kullanır ve bir katalog biçimlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="7d291-178">If you don't have the catalog, Recommendations can use the actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="7d291-179">Kapsanan bir katalog kullanıcı işlemleri bir parçası raporlandı değil öğeleri dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="7d291-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="7d291-180">**İlk kez önerileri nasıl ayarlarım?**</span><span class="sxs-lookup"><span data-stu-id="7d291-180">**How do I set up Recommendations for the first time?**</span></span>

<span data-ttu-id="7d291-181">Sonra [abone](https://datamarket.azure.com/dataset/amla/recommendations) önerileri için API belgelerine kullanmalısınız [Azure Machine Learning önerileri - Hızlı Başlangıç Kılavuzu](machine-learning-recommendation-api-quick-start-guide.md) hizmeti kurmak için.</span><span class="sxs-lookup"><span data-stu-id="7d291-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) to Recommendations, you should use the API documentation in the [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) to set up the service.</span></span>

<span data-ttu-id="7d291-182">**API belgelerine nereden bulabilirim?**</span><span class="sxs-lookup"><span data-stu-id="7d291-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="7d291-183">API belgeleri [Azure Machine Learning önerileri-Hızlı Başlangıç Kılavuzu](machine-learning-recommendation-api-quick-start-guide.md).</span><span class="sxs-lookup"><span data-stu-id="7d291-183">The API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="7d291-184">**Öneriler için katalog ve kullanım verileri yüklemek hangi seçenekleri var mı?**</span><span class="sxs-lookup"><span data-stu-id="7d291-184">**What options do I have to upload catalog and usage data to Recommendations?**</span></span>

<span data-ttu-id="7d291-185">Katalog ve kullanım verileri yüklemek için iki seçeneğiniz vardır: verileri, CRM sisteminize veya diğer günlükler verin ve öneriler için yükleyin ya da kullanıcı etkinliklerini izler, Web sitenizin etiket ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d291-185">You have two options for uploading your catalog and usage data: You can export the data from your CRM system or other logs and upload it to Recommendations, or you can add tags to your website that will track user activities.</span></span> <span data-ttu-id="7d291-186">İkinci yöntemi kullanırsanız, verileri Azure içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="7d291-186">If you use the latter method, the data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="7d291-187">Bakım ve Destek</span><span class="sxs-lookup"><span data-stu-id="7d291-187">Maintenance and support</span></span>
<span data-ttu-id="7d291-188">**My veri kümesi ne kadar büyük olabilir?**</span><span class="sxs-lookup"><span data-stu-id="7d291-188">**How large can my data set be?**</span></span>

<span data-ttu-id="7d291-189">Her bir veri kümesi en fazla 100.000 katalog öğelerini içeren ve en çok kullanım verilerinin 2048 MB.</span><span class="sxs-lookup"><span data-stu-id="7d291-189">Each data set can contain up to 100,000 catalog items and up to 2048 MB of usage data.</span></span>
<span data-ttu-id="7d291-190">Ayrıca, bir abonelik en fazla 10 veri kümeleri (modellerin) içerebilir.</span><span class="sxs-lookup"><span data-stu-id="7d291-190">In addition, a subscription can contain up to 10 data sets (models).</span></span>

<span data-ttu-id="7d291-191">**Öneriler için teknik destek nereden alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="7d291-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="7d291-192">Teknik Destek edinilebilir [Microsoft Azure desteği](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span><span class="sxs-lookup"><span data-stu-id="7d291-192">Technical support is available on the [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="7d291-193">**Kullanım koşulları nereden bulabilirim?**</span><span class="sxs-lookup"><span data-stu-id="7d291-193">**Where can I find the terms of use?**</span></span>

<span data-ttu-id="7d291-194">[Microsoft Azure Machine Learning hizmet önerileri API koşullarını](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span><span class="sxs-lookup"><span data-stu-id="7d291-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>


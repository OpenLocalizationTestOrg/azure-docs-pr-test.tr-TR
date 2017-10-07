---
title: "aaaSet ayarlama ve kullanma hello Machine Learning önerileri API'si | Microsoft Docs"
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
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="e53f8-103">Machine Learning Öneri API’sini ayarlama ve kullanma hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="e53f8-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="e53f8-104">**ÖNERİLER nedir?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="e53f8-105">Merhaba önerileri API Bilişsel hizmeti yerine bu sürümünü kullanarak başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-105">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="e53f8-106">Merhaba önerileri Bilişsel hizmet bu hizmeti koyacağınız ve tüm hello yeni özellikler vardır geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="e53f8-107">Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="e53f8-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="e53f8-108">Daha fazla bilgi edinmek [geçiş toohello yeni Bilişsel hizmeti](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="e53f8-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="e53f8-109">Kuruluşlar ve öneriler toocross satış ve yukarı satış ürünleri ve Hizmetleri tootheir müşteriler kullanan işletmeler için Azure Machine Learning önerileri bir Self Servis önerileri altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e53f8-109">For organizations and businesses that rely on recommendations toocross-sell and up-sell products and services tootheir customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="e53f8-110">Bu matris factorization kendi çekirdek algoritması kullanan işbirliği filtrelemenin bir uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="e53f8-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="e53f8-111">Uygulama geliştiricilerinin önerileri REST API'lerini kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e53f8-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="e53f8-112">**ÖNERİLERİ ne yapabilirim?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="e53f8-113">ÖNERİLER bir öğe girişi veya öğeleri kümesi alır ve ilgili öneriler listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="e53f8-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="e53f8-114">Örneğin: bir çevrimiçi satıcısı müşterinin bir ürün tıklar.</span><span class="sxs-lookup"><span data-stu-id="e53f8-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="e53f8-115">Hello çevrimiçi satıcısında bu ürünü giriş tooRECOMMENDATIONS gönderir, iade ürünlerin listesini alır ve toohello müşteri bu ürünlerin gösterileceği karar verir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-115">hello online retailer sends that product as input tooRECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown toohello customer.</span></span> <span data-ttu-id="e53f8-116">Çevrimiçi mağazada toouse önerileri toooptimize istediğiniz veya tooinform, iç hatta satış departmanı veya Arama Merkezi.</span><span class="sxs-lookup"><span data-stu-id="e53f8-116">You may want toouse RECOMMENDATIONS toooptimize your online store or even tooinform your inside sales department or call center.</span></span>

<span data-ttu-id="e53f8-117">**Kullanım sınırlamalar var mı?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="e53f8-118">Öneriler kullanım kısıtlamaları aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="e53f8-118">Recommendations has hello following usage limitations:</span></span>

* <span data-ttu-id="e53f8-119">Model abonelik başına en yüksek sayısı: 10</span><span class="sxs-lookup"><span data-stu-id="e53f8-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="e53f8-120">En fazla bir katalog tutabilir öğe sayısı: 100.000</span><span class="sxs-lookup"><span data-stu-id="e53f8-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="e53f8-121">Merhaba maksimum tutulur kullanım noktaları ~ 5,000,000 sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="e53f8-121">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="e53f8-122">Yeni bir tane karşıya bildirilen veya gereken hello eski silinir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-122">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="e53f8-123">200 MB (örneğin, veri içeri aktar katalog kullanım verileri İçeri Aktar) e-posta ile gönderilen verilerin en büyük boyut:</span><span class="sxs-lookup"><span data-stu-id="e53f8-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="e53f8-124">İşlemler (TP'ler) etkin değil önerileri modeli derlemesi için saniye başına ~ 2 TP'leri sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="e53f8-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="e53f8-125">Etkin bir önerileri modeli yapı too20 TP'leri basılı tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e53f8-125">A Recommendations model build that is active can hold up too20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="e53f8-126">Satın Alma ve Fatura</span><span class="sxs-lookup"><span data-stu-id="e53f8-126">Purchase and Billing</span></span>
<span data-ttu-id="e53f8-127">**Nasıl önerileri hello başlatma süresi boyunca maliyeti nedir?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-127">**How much does Recommendations cost during hello launch period?**</span></span>

<span data-ttu-id="e53f8-128">Öneriler, bir abonelik tabanlı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="e53f8-129">Şarj aylık işlem hacmi temel alır.</span><span class="sxs-lookup"><span data-stu-id="e53f8-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="e53f8-130">Merhaba denetleyebilirsiniz [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations) fiyatlandırma bilgileri için Microsoft Azure Marketplace içinde.</span><span class="sxs-lookup"><span data-stu-id="e53f8-130">You can check hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="e53f8-131">**Öneriler sahip ile ilişkili maliyetlerin izlemek ve kullanıcı etkinliğini benim yerime depolamak var mı?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="e53f8-132">Merhaba şu anda değil.</span><span class="sxs-lookup"><span data-stu-id="e53f8-132">Not at hello moment.</span></span>

<span data-ttu-id="e53f8-133">**Öneriler ücretsiz deneme sürümü var mı?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="e53f8-134">Kısıtlı too10, her ay 000 hareketleri olan ücretsiz bir izleme yoktur.</span><span class="sxs-lookup"><span data-stu-id="e53f8-134">There is a free trail which is restricted too10,000 transactions per month.</span></span>

<span data-ttu-id="e53f8-135">**Ne zaman ı önerileri için Fatura edilecek?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="e53f8-136">Ücretli bir abonelik var olduğu aylık bir ücret herhangi bir aboneliği ' dir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="e53f8-137">Ücretli bir abonelik satın aldığınızda, hemen Merhaba ilk ücretlendirilen ayın kullanın.</span><span class="sxs-lookup"><span data-stu-id="e53f8-137">When you purchase a paid subscription, you are immediately charged for hello first month's use.</span></span> <span data-ttu-id="e53f8-138">Merhaba aboneliği sayfasına (artı geçerli vergileri) hello teklifini ilişkilendirilen hello tutar sizden ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-138">You are charged hello amount that is associated with hello offer on hello subscription page (plus applicable taxes).</span></span> <span data-ttu-id="e53f8-139">Bu aylık ücret her ay hello aboneliği iptal kadar aynı takvim tarih orijinal satın alma olarak hello üzerinde yapılır.</span><span class="sxs-lookup"><span data-stu-id="e53f8-139">This monthly charge is made each month on hello same calendar date as your original purchase until you cancel hello subscription.</span></span> 

<span data-ttu-id="e53f8-140">**Tooa daha yüksek katmanlı bir hizmet nasıl yükseltme?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-140">**How do I upgrade tooa higher tier service?**</span></span>

<span data-ttu-id="e53f8-141">Satın alma veya hello aboneliğinizden güncelleştirme [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations) Microsoft Azure Market sayfasında.</span><span class="sxs-lookup"><span data-stu-id="e53f8-141">You can buy or update your subscription from hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="e53f8-142">Bir abonelik yükseltme yaptığınızda:</span><span class="sxs-lookup"><span data-stu-id="e53f8-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="e53f8-143">Eski aboneliğinizi kalan işlemler tooyour yeni abonelik eklenmez.</span><span class="sxs-lookup"><span data-stu-id="e53f8-143">Transactions that are remaining on your old subscription are not added tooyour new subscription.</span></span> 
* <span data-ttu-id="e53f8-144">Olsa bile tam fiyat hello yeni abonelik için ödeme eski aboneliğinizi kullanılmayan hareketleri.</span><span class="sxs-lookup"><span data-stu-id="e53f8-144">You pay full price for hello new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="e53f8-145">İşlem tooupgrade bir abonelik:</span><span class="sxs-lookup"><span data-stu-id="e53f8-145">Process tooupgrade a subscription:</span></span>

* <span data-ttu-id="e53f8-146">Nevigate toohello [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="e53f8-146">Nevigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="e53f8-147">Oturum açmış değilseniz toohello Market oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e53f8-147">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="e53f8-148">Merhaba sağ bölmede, tüm hello taşınabileceği listelenir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-148">In hello right pane, all hello available plans are listed.</span></span> <span data-ttu-id="e53f8-149">İçin tooupgrade hello planı için Hello radyo düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e53f8-149">Click hello radio button for hello plan you want tooupgrade to.</span></span>
* <span data-ttu-id="e53f8-150">Tooupgrade istiyorsanız, **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e53f8-150">If you want tooupgrade, click **OK**.</span></span> <span data-ttu-id="e53f8-151">Tooupgrade istemiyorsanız tıklayın **iptal**.</span><span class="sxs-lookup"><span data-stu-id="e53f8-151">If you do not want tooupgrade, click **Cancel**.</span></span>

<span data-ttu-id="e53f8-152">**Önemli** faturalama ve kullanım uygulamalarını olduğundan yükseltme yapmadan önce dikkatle okuma hello iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="e53f8-152">**Important** Carefully read hello dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="e53f8-153">**My abonelik tooRecommendations ne zaman sona erecek mi?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-153">**When will my subscription tooRecommendations end?**</span></span>

<span data-ttu-id="e53f8-154">İptal ettiğinizde, aboneliğiniz sona erer.</span><span class="sxs-lookup"><span data-stu-id="e53f8-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="e53f8-155">Toocancel isterseniz aboneliklerinizi, yönergeleri izleyerek hello bakın.</span><span class="sxs-lookup"><span data-stu-id="e53f8-155">If you would like toocancel your subscriptions, see hello following instructions.</span></span>

<span data-ttu-id="e53f8-156">**Öneriler Aboneliğimi nasıl iptal edebilirim?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="e53f8-157">Aşağıdaki kullanım hello aboneliğinizi adımları toocancel.</span><span class="sxs-lookup"><span data-stu-id="e53f8-157">toocancel your subscription, use hello following steps.</span></span> <span data-ttu-id="e53f8-158">Geçerli aboneliğinizi Ücretli abonelik ise, aboneliğinizi yürürlükte hello faturalama dönemi geçerli hello sonuna kadar devam eder.</span><span class="sxs-lookup"><span data-stu-id="e53f8-158">If your current subscription is a paid subscription, your subscription continues in effect until hello end of hello current billing period.</span></span> <span data-ttu-id="e53f8-159">Etkili iptal toobe hemen hello varsa, adresinden bize başvurun [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="e53f8-159">If you need hello cancellation toobe effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="e53f8-160">**Not** bir fatura döneminde hello bitiş fatura döneminin veya kullanılmayan işlemler için önce iptal ederseniz hiçbir para iadesi verilir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-160">**Note** No refund is given if you cancel before hello end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="e53f8-161">Toohello gidin [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="e53f8-161">Navigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="e53f8-162">Oturum açmış değilseniz toohello Market oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e53f8-162">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="e53f8-163">Tıklatın **iptal** toohello sağında hello veri kümesi adı ve durum.</span><span class="sxs-lookup"><span data-stu-id="e53f8-163">Click **Cancel** toohello right of hello dataset name and status.</span></span> <span data-ttu-id="e53f8-164">Merhaba faturalama dönemi veya işlem sınırınızı geçerli Hello sonuna (hangisi önce gerçekleşirse) ulaşılana kadar bu aboneliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e53f8-164">You can use this subscription until hello end of hello current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="e53f8-165">Aboneliğiniz bu nedenle yeni bir abonelik satın alabilirsiniz hemen bir bilet adresindeki dosya toocancel isterseniz [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="e53f8-165">If you would like toocancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="e53f8-166">Öneriler ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e53f8-166">Getting started with Recommendations</span></span>
<span data-ttu-id="e53f8-167">**Öneriler benim için mi?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="e53f8-168">Machine Learning önerileri kuruluşlar ve öneriler toocross satış ve yukarı satış ürünleri veya hizmetleri tootheir müşteriler kullanan işletmeler içindir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations toocross-sell and up-sell products or services tootheir customers.</span></span> <span data-ttu-id="e53f8-169">Varsa bir müşteri kullanıma yönelik Web sitesi, satış ekibi, bir iç satış ekibi ya da bir çağrı merkezi ve birkaç düzine ürünleri veya hizmetleri kataloğunu teklifi sunuyorsanız, alt çizgi önerileri kullanarak yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="e53f8-170">Önerileri denemeler tasarlanmış toobe oldukça basit olduğunu.</span><span class="sxs-lookup"><span data-stu-id="e53f8-170">Experimenting with Recommendations is designed toobe fairly simple.</span></span> <span data-ttu-id="e53f8-171">temel programlama becerilerinizi Hello geçerli API tabanlı sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-171">hello current API-based version requires basic programming skills.</span></span> <span data-ttu-id="e53f8-172">Yardıma gereksinim duyarsanız, kimin Web sitenizi geliştirilen hello satıcısına başvurun.</span><span class="sxs-lookup"><span data-stu-id="e53f8-172">If you need assistance, contact hello vendor who developed your website.</span></span> <span data-ttu-id="e53f8-173">Bir iç BT departmanına ya da şirket içi bir geliştirici varsa, sizin için mümkün tooget önerileri toowork olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-173">If you have an internal IT department or an in-house developer, they should be able tooget Recommendations toowork for you.</span></span> 

<span data-ttu-id="e53f8-174">**Önerileri ayarı hello önkoşulları nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-174">**What are hello prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="e53f8-175">Öneriler tooyour katalog ilgili olarak kullanıcı seçimlerini günlüğünü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-175">Recommendations requires that you have a log of user choices as it relates tooyour catalog.</span></span> <span data-ttu-id="e53f8-176">Bu tür bir günlük yoksa ve bir müşteri kullanıma yönelik Web sitesi varsa, Öneriler size kullanıcı etkinliği toplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e53f8-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="e53f8-177">Öneriler, ürünleri veya hizmetleri kataloğunu de gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="e53f8-178">Merhaba katalog yoksa, öneriler hello gerçek müşteri kullanım verilerini kullanır ve bir katalog biçimlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-178">If you don't have hello catalog, Recommendations can use hello actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="e53f8-179">Kapsanan bir katalog kullanıcı işlemleri bir parçası raporlandı değil öğeleri dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="e53f8-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="e53f8-180">**Nasıl önerileri hello için ilk kez ayarlarım?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-180">**How do I set up Recommendations for hello first time?**</span></span>

<span data-ttu-id="e53f8-181">Sonra [abone](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, hello hello API belgelerine kullanması gereken [Azure Machine Learning önerileri - Hızlı Başlangıç Kılavuzu](machine-learning-recommendation-api-quick-start-guide.md) tooset up hello hizmeti.</span><span class="sxs-lookup"><span data-stu-id="e53f8-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, you should use hello API documentation in hello [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) tooset up hello service.</span></span>

<span data-ttu-id="e53f8-182">**API belgelerine nereden bulabilirim?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="e53f8-183">Merhaba API belgelerine olan [Azure Machine Learning önerileri-Hızlı Başlangıç Kılavuzu](machine-learning-recommendation-api-quick-start-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e53f8-183">hello API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="e53f8-184">**Seçenekler ne tooupload katalog ve kullanım verileri tooRecommendations sahip mi?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-184">**What options do I have tooupload catalog and usage data tooRecommendations?**</span></span>

<span data-ttu-id="e53f8-185">Katalog ve kullanım verileri yüklemek için iki seçeneğiniz vardır: CRM sisteminize veya diğer günlükler hello verilerini dışarı aktarın ve tooRecommendations yükleyin ya da kullanıcı etkinliklerini izler etiketleri tooyour Web sitesi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e53f8-185">You have two options for uploading your catalog and usage data: You can export hello data from your CRM system or other logs and upload it tooRecommendations, or you can add tags tooyour website that will track user activities.</span></span> <span data-ttu-id="e53f8-186">Merhaba ikinci yöntemi kullanırsanız, Azure'da hello veriler depolanır.</span><span class="sxs-lookup"><span data-stu-id="e53f8-186">If you use hello latter method, hello data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="e53f8-187">Bakım ve Destek</span><span class="sxs-lookup"><span data-stu-id="e53f8-187">Maintenance and support</span></span>
<span data-ttu-id="e53f8-188">**My veri kümesi ne kadar büyük olabilir?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-188">**How large can my data set be?**</span></span>

<span data-ttu-id="e53f8-189">Her bir veri kümesi too100, 000 katalog öğeleri yukarı ve Kullanım verilerinin too2048 MB yukarı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-189">Each data set can contain up too100,000 catalog items and up too2048 MB of usage data.</span></span>
<span data-ttu-id="e53f8-190">Ayrıca, bir abonelik too10 veri kümelerini (modellerin) içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e53f8-190">In addition, a subscription can contain up too10 data sets (models).</span></span>

<span data-ttu-id="e53f8-191">**Öneriler için teknik destek nereden alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="e53f8-192">Teknik Destek hello üzerinde kullanılabilir [Microsoft Azure desteği](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span><span class="sxs-lookup"><span data-stu-id="e53f8-192">Technical support is available on hello [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="e53f8-193">**Kullanım koşulları hello nereden bulabilirim?**</span><span class="sxs-lookup"><span data-stu-id="e53f8-193">**Where can I find hello terms of use?**</span></span>

<span data-ttu-id="e53f8-194">[Microsoft Azure Machine Learning hizmet önerileri API koşullarını](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span><span class="sxs-lookup"><span data-stu-id="e53f8-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>


---
title: "Mobile Services kullanıyorum, App Service bana nasıl yardımcı olur?"
description: "App Service’in mevcut Mobile Services projelerinize sağladığı avantajları öğrenin."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 26b68a11-8352-4f78-acd2-e4e0ec177781
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 22397b6b448b418d5b54a457c3bafaf5c68ecc7b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="76178-103"><a name="getting-started"> </a>Mobile Services kullanıyorum, App Service bana nasıl yardımcı olur?</span><span class="sxs-lookup"><span data-stu-id="76178-103"><a name="getting-started"> </a>I use Mobile Services, how does App Service help?</span></span>
## <a name="overview"></a><span data-ttu-id="76178-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="76178-104">Overview</span></span>
<span data-ttu-id="76178-105">Mevcut Mobil Hizmetiniz güvendedir ve desteklenmeye devam edecektir.</span><span class="sxs-lookup"><span data-stu-id="76178-105">Your existing Mobile Service is safe and will remain supported.</span></span> <span data-ttu-id="76178-106">Ancak *Azure App Service* platformunun sağladığı, mobil uygulamanız için bugün Mobile Services’de bulunmayan çok sayıda avantaj vardır:</span><span class="sxs-lookup"><span data-stu-id="76178-106">However there are number of advantages the *Azure App Service* platform provides for your mobile app that are not available today with Mobile Services:</span></span>

* <span data-ttu-id="76178-107">Web ve mobil istemciler içeren uygulamalar için daha basit, daha kolay ve daha düşük maliyetli teklifler.</span><span class="sxs-lookup"><span data-stu-id="76178-107">Simpler, easier and more cost effective offering for apps that include both web and mobile clients</span></span>
* <span data-ttu-id="76178-108">Web İşleri, özel CNames, daha iyi izleme dahil yeni ana bilgisayara özellikleri.</span><span class="sxs-lookup"><span data-stu-id="76178-108">New host features including Web Jobs, custom CNames, better monitoring</span></span>
* <span data-ttu-id="76178-109">Traffic Manager ile anahtar teslimi tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="76178-109">Turnkey integration with Traffic Manager</span></span>
* <span data-ttu-id="76178-110">Karma Bağlantılara ek olarak, VNet kullanarak şirket içi kaynaklarınıza ve VPN’lere bağlantı</span><span class="sxs-lookup"><span data-stu-id="76178-110">Connectivity to your on-premises resources and VPNs using VNet in addition to Hybrid Connections</span></span>
* <span data-ttu-id="76178-111">NewRelic veya AppInsights kullanarak uygulamanız için izleme, uyarma ve sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="76178-111">Monitoring, alerting and  troubleshooting for your app using NewRelic or AppInsights</span></span>
* <span data-ttu-id="76178-112">Temel hesaplama kaynakları ve fiyatlandırma için daha zengin yelpaze</span><span class="sxs-lookup"><span data-stu-id="76178-112">Richer spectrum of the underlying compute resources and pricing</span></span>
* <span data-ttu-id="76178-113">Yerleşik otomatik ölçeklendirme, yük dengeleme ve performans izleme</span><span class="sxs-lookup"><span data-stu-id="76178-113">Built-in auto scale, load balancing, and performance monitoring.</span></span>
* <span data-ttu-id="76178-114">Yerleşik hazırlık, yedekleme, geri alma ve üretim sırasında test etme özellikleri</span><span class="sxs-lookup"><span data-stu-id="76178-114">Built-in staging, backup, roll-back, and testing-in-production capabilities</span></span>

## <a name="new-hosting-features"></a><span data-ttu-id="76178-115">Yeni barındırma özellikleri</span><span class="sxs-lookup"><span data-stu-id="76178-115">New hosting features</span></span>
<span data-ttu-id="76178-116">*Azure App Service*’de *Mobil Uygulama* arka uç kodu; Web Uygulaması ve API Uygulaması ile aynı kapsayıcıda çalışır.</span><span class="sxs-lookup"><span data-stu-id="76178-116">In *Azure App Service* the *Mobile App* backend code runs in the same container as Web App and API App.</span></span> <span data-ttu-id="76178-117">Böylece, şu anda Mobile Services’de bulunmayan bazıları dahil, bu kapsayıcıdaki tüm özelliklerden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76178-117">As such you can take advantage of all the features in this container, including some of those that are not currently present in Mobile Services:</span></span>

* <span data-ttu-id="76178-118">Web İşleri aracılığıyla sürekli çalışan arka uç mantığı ekleyin</span><span class="sxs-lookup"><span data-stu-id="76178-118">Add continuously running backend logic via Web Jobs</span></span>
* <span data-ttu-id="76178-119">Arka uç kodunuzun her zaman çalıştığından emin olun</span><span class="sxs-lookup"><span data-stu-id="76178-119">Ensure your backend code is always running</span></span>
* <span data-ttu-id="76178-120">Mobil arka uç, uç noktalarınıza kolay ve kararlı adlar sağlamak için özel CNames kullanın</span><span class="sxs-lookup"><span data-stu-id="76178-120">Use custom CNames to provide friendly and stable names to your mobile backend endpoints</span></span>
* <span data-ttu-id="76178-121">Traffic Manager ile uygulamanızı coğrafi olarak ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="76178-121">Geo-scale your app with Traffic Manager</span></span>
* <span data-ttu-id="76178-122">İstediğiniz tüm kitaplıkları ve paketleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="76178-122">Include any libraries and packages you want.</span></span>
* <span data-ttu-id="76178-123">(.NET için) MVC dahil, ASP.NET’in her özelliğinden yararlanın</span><span class="sxs-lookup"><span data-stu-id="76178-123">(For .NET) Leverage any feature of ASP.NET, including MVC</span></span>
* <span data-ttu-id="76178-124">(Node.js için) Ortak MVC kitaplıkları dahil, Düğüm ekosisteminin tüm saf JavaScript kitaplığından yararlanın.</span><span class="sxs-lookup"><span data-stu-id="76178-124">(For Node.js) Leverage any pure JavaScript library of the Node ecosystem, including common MVC libraries.</span></span>

## <a name="access-on-premises-data-using-vnet"></a><span data-ttu-id="76178-125">VNet kullanarak şirket içi verilere erişin</span><span class="sxs-lookup"><span data-stu-id="76178-125">Access on-premises data using VNet</span></span>
<span data-ttu-id="76178-126">Günümüzde, Mobile Services ile şirket için kaynaklara erişim için Karma Bağlantıları halihazırda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76178-126">With Mobile Services today you can already use Hybrid Connections to access on-premises resources.</span></span> <span data-ttu-id="76178-127">Ancak bir VPN çözümünün tercih edildiği durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="76178-127">However there are situations where a VPN solution is preferred.</span></span> <span data-ttu-id="76178-128">*Azure App Service* ile Mobil Uygulama arka uç kodunuz için Azure VNet kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76178-128">With *Azure App Service* you can use Azure VNet for your Mobile App backend code.</span></span>

## <a name="use-your-favorite-backend-language"></a><span data-ttu-id="76178-129">Sık kullanılan arka uç dilinizi kullanın</span><span class="sxs-lookup"><span data-stu-id="76178-129">Use your favorite backend language</span></span>
<span data-ttu-id="76178-130">*Azure App Service* ASP.NET ve Node.js platformları için, en son çalışma zamanları dahil, daha geniş ve daha zengin bir destek sunar.</span><span class="sxs-lookup"><span data-stu-id="76178-130">*Azure App Service* offers broader and richer support for ASP.NET and Node.js platforms, including access to the latest runtimes.</span></span>

## <a name="set-up-automatic-scale"></a><span data-ttu-id="76178-131">Otomatik ölçeklendirme ayarlayın</span><span class="sxs-lookup"><span data-stu-id="76178-131">Set up automatic scale</span></span>
<span data-ttu-id="76178-132">Mobile Services ile arka uç kodunuzun tm örnekleri küçük VM’lerde çalışıyordu.</span><span class="sxs-lookup"><span data-stu-id="76178-132">With Mobile Services, all instances of your backend code were running on Small VMs.</span></span> <span data-ttu-id="76178-133">*Azure App Service*, VM boyutlarını çok daha zengin seçeneklerle seçmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="76178-133">*Azure App Service* enables you to select the size of the VMs from a much richer set of options.</span></span> <span data-ttu-id="76178-134">Ayrıca çeşitli performans ölçümleri temelinde, gelen müşteri yükünü işlemek için hızlı şekilde ölçeği artırabilir ya da genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76178-134">You can also  quickly scale up or out to handle any incoming customer load, based on various performance metrics.</span></span>

## <a name="be-in-the-know"></a><span data-ttu-id="76178-135">“Haberdar” olun</span><span class="sxs-lookup"><span data-stu-id="76178-135">Be in the “know”</span></span>
<span data-ttu-id="76178-136">Sizi ve ekibinizi otomatik bilgilendiren izleme ve uyarılarla gerçek zamanlı olarak sorulara yanıt verin.</span><span class="sxs-lookup"><span data-stu-id="76178-136">React to issues in real-time with monitoring and alerts to automatically notify you and your team.</span></span> <span data-ttu-id="76178-137">Mobil uygulamanızın nasıl çalıştığına ilişkin daha zengin bir öngörü sahibi olmak için New Relic ve AppInsights’dan gelen gelişmiş uygulama analizi ve izleme özelliğini tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="76178-137">Integrate advanced app analytics and monitoring functionality from New Relic and AppInsights to get even richer insight into how your Mobile app is performing.</span></span> <span data-ttu-id="76178-138">*Azure App Service* ile programlı şekilde ya da Azure Portal aracılığıyla, çeşitli performans ölçümleri temelinde uyarılar ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76178-138">With *Azure App Service* you can now setup alerts based on variety of performance metrics, either programatically and via the Azure Portal.</span></span>

## <a name="keep-your-assets-safe"></a><span data-ttu-id="76178-139">Varlıklarınızı güvende tutun</span><span class="sxs-lookup"><span data-stu-id="76178-139">Keep your assets safe</span></span>
<span data-ttu-id="76178-140">Arka ucunuzu ve veritabanınızı otomatik olarak yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="76178-140">Automatically back up your backend and database.</span></span> <span data-ttu-id="76178-141">Kodunuz ve verileriniz olağanüstü durumlara karşı güvendedir ve kolayca geri yüklenebilir, böylece işletmenizi güvenle çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76178-141">Your code and data is secure from disaster and easily restored, allowing you to run your business with confidence.</span></span>

## <a name="ready-stage-go"></a><span data-ttu-id="76178-142">Hazır Ol, Hazırla, Başla!</span><span class="sxs-lookup"><span data-stu-id="76178-142">Ready, Stage, Go!</span></span>
<span data-ttu-id="76178-143">*Azure App Service* ile artık mobil uygulamalarınız için birden fazla özel test ve hazırlık ortamı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76178-143">With *Azure App Service* you can now create multiple private testing and staging environments for your mobile apps.</span></span> <span data-ttu-id="76178-144">Dağıtmadan önce, bunları test gerçekleştirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="76178-144">Use them to perform testing before you deploy.</span></span> <span data-ttu-id="76178-145">Kesinti süresi olmaksızın üretime geçin.</span><span class="sxs-lookup"><span data-stu-id="76178-145">Swap to production with no downtime.</span></span> <span data-ttu-id="76178-146">Web uygulamaları, en iyi müşteri deneyimi sağlayacak şekilde önceden yüklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="76178-146">Web apps are pre-loaded, ensuring the best customer experience.</span></span>

<span data-ttu-id="76178-147">Bu [öğreticiyi](app-service-mobile-migrating-from-mobile-services.md) izleyerek mevcut Mobil Hizmetiniz için *App Service* avantajından yararlanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76178-147">You can get start taking advantage of *App Service* for your existing Mobile Service by following this [tutorial](app-service-mobile-migrating-from-mobile-services.md).</span></span>

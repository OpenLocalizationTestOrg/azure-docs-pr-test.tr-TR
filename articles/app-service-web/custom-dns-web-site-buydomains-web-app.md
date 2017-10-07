---
title: "aaaBuy Azure Web uygulamaları için özel etki alanı adı"
description: "Nasıl toobuy özel bir etki alanı adını Azure App Service'te bir web uygulaması ile bilgi edinin."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="edacf-103">Azure Web uygulamaları için özel etki alanı adı satın alma</span><span class="sxs-lookup"><span data-stu-id="edacf-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="edacf-104">Uygulama hizmeti etki alanları (Önizleme) doğrudan Azure içinde yönetilen en üst düzey etki alanlarıdır.</span><span class="sxs-lookup"><span data-stu-id="edacf-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="edacf-105">Bunlar, kolay toomanage özel etki alanları oluşturmak için [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="edacf-105">They make it easy toomanage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="edacf-106">Bu öğretici nasıl toobuy bir uygulama hizmeti etki alanı Ata DNS adları ve tooAzure Web uygulamaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="edacf-106">This tutorial shows you how toobuy an App Service domain and assign DNS names tooAzure Web Apps.</span></span>

<span data-ttu-id="edacf-107">Bu makalede Azure uygulama hizmeti (Web Apps, API Apps, Mobile Apps, Logic Apps) içindir.</span><span class="sxs-lookup"><span data-stu-id="edacf-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="edacf-108">Azure VM veya Azure Storage için bkz: [atamak uygulama hizmeti etki alanı tooAzure VM veya Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span><span class="sxs-lookup"><span data-stu-id="edacf-108">For Azure VM or Azure Storage, see [Assign App Service domain tooAzure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="edacf-109">Bulut Hizmetleri için bkz: [bir Azure bulut hizmeti için bir özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="edacf-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edacf-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="edacf-110">Prerequisites</span></span>

<span data-ttu-id="edacf-111">toocomplete Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="edacf-111">toocomplete this tutorial:</span></span>

* <span data-ttu-id="edacf-112">[Bir App Service uygulaması oluşturma](/azure/app-service/), veya başka bir öğretici için oluşturduğunuz bir uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="edacf-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-hello-app"></a><span data-ttu-id="edacf-113">Merhaba uygulamasını hazırlama</span><span class="sxs-lookup"><span data-stu-id="edacf-113">Prepare hello app</span></span>

<span data-ttu-id="edacf-114">Azure Web uygulamaları, web uygulaması'nın özel etki alanlarında toouse [uygulama hizmeti planı](https://azure.microsoft.com/pricing/details/app-service/) Ücretli katmanı olmalıdır (**paylaşılan**, **temel**, **standart**, veya **Premium**).</span><span class="sxs-lookup"><span data-stu-id="edacf-114">toouse custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="edacf-115">Bu adımda, bu hello web uygulaması fiyatlandırma katmanı hello desteklenir emin olun.</span><span class="sxs-lookup"><span data-stu-id="edacf-115">In this step, you make sure that hello web app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="edacf-116">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="edacf-116">Sign in tooAzure</span></span>

<span data-ttu-id="edacf-117">Açık hello [Azure portal](https://portal.azure.com) ve Azure hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="edacf-117">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="edacf-118">Toohello uygulamada hello Azure portalına gidin</span><span class="sxs-lookup"><span data-stu-id="edacf-118">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="edacf-119">Merhaba sol menüden seçin **uygulama hizmetleri**ve ardından hello uygulamasının hello adı seçin.</span><span class="sxs-lookup"><span data-stu-id="edacf-119">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="edacf-121">Merhaba App Service uygulaması hello Yönetimi sayfasında bakın.</span><span class="sxs-lookup"><span data-stu-id="edacf-121">You see hello management page of hello App Service app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="edacf-122">Fiyatlandırma katmanı hello denetleyin</span><span class="sxs-lookup"><span data-stu-id="edacf-122">Check hello pricing tier</span></span>

<span data-ttu-id="edacf-123">Sol gezinti hello uygulama sayfasının hello toohello kaydırma **ayarları** bölümünde ve seçin **(uygulama hizmeti planı) ölçeklendirme**.</span><span class="sxs-lookup"><span data-stu-id="edacf-123">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Büyütme menüsü](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="edacf-125">Merhaba uygulamanın geçerli katmanı mavi kenarlığı ile vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="edacf-125">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="edacf-126">Bu hello uygulama hello olmadığından emin toomake denetleyin **serbest** katmanı.</span><span class="sxs-lookup"><span data-stu-id="edacf-126">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="edacf-127">Özel DNS hello desteklenmiyor **serbest** katmanı.</span><span class="sxs-lookup"><span data-stu-id="edacf-127">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="edacf-129">Merhaba uygulama hizmeti planı değilse **serbest**, Kapat hello **fiyatlandırma katmanınızı seçin** sayfasında ve çok atla[satınalma hello etki alanı](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="edacf-129">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Buy hello domain](#buy-the-domain).</span></span>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="edacf-130">Uygulama hizmeti planı Hello ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="edacf-130">Scale up hello App Service plan</span></span>

<span data-ttu-id="edacf-131">Merhaba boş olmayan katmanları birini seçin (**paylaşılan**, **temel**, **standart**, veya **Premium**).</span><span class="sxs-lookup"><span data-stu-id="edacf-131">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="edacf-132">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="edacf-132">Click **Select**.</span></span>

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="edacf-134">Bildirim aşağıdaki hello gördüğünüzde, hello ölçeklendirme işlemi tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="edacf-134">When you see hello following notification, hello scale operation is complete.</span></span>

![Ölçek işlemi onayı](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a><span data-ttu-id="edacf-136">Merhaba etki alanı satın alma</span><span class="sxs-lookup"><span data-stu-id="edacf-136">Buy hello domain</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="edacf-137">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="edacf-137">Sign in tooAzure</span></span>
<span data-ttu-id="edacf-138">Açık hello [Azure portal](https://portal.azure.com/) ve Azure hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="edacf-138">Open hello [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="edacf-139">Satınalma etki alanları başlatma</span><span class="sxs-lookup"><span data-stu-id="edacf-139">Launch Buy domains</span></span>
<span data-ttu-id="edacf-140">Merhaba, **Web Apps** sekmesini seçin, web uygulamanızın hello adını tıklatın, **ayarları**ve ardından **özel etki alanları**</span><span class="sxs-lookup"><span data-stu-id="edacf-140">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="edacf-141">Merhaba, **özel etki alanları** sayfasında, **satın etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="edacf-141">In hello **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a><span data-ttu-id="edacf-142">Merhaba etki alanı satın alma yapılandırın</span><span class="sxs-lookup"><span data-stu-id="edacf-142">Configure hello domain purchase</span></span>

<span data-ttu-id="edacf-143">Merhaba, **uygulama hizmeti etki alanı** sayfasında hello **etki alanı Ara** kutusu, hello etki alanı adını yazın, istediğiniz toobuy ve türü `Enter`.</span><span class="sxs-lookup"><span data-stu-id="edacf-143">In hello **App Service Domain** page, in hello **Search for domain** box, type hello domain name you want toobuy and type `Enter`.</span></span> <span data-ttu-id="edacf-144">Merhaba önerilen kullanılabilir etki alanlarının hemen altındaki metin kutusuna hello gösterilir.</span><span class="sxs-lookup"><span data-stu-id="edacf-144">hello suggested available domains are shown just below hello text box.</span></span> <span data-ttu-id="edacf-145">Toobuy istediğiniz bir veya daha fazla etki alanı seçin.</span><span class="sxs-lookup"><span data-stu-id="edacf-145">Select one or more domains you want toobuy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="edacf-146">Merhaba tıklatın **iletişim bilgileri** ve hello etki alanının kişi bilgilerini formu doldurun.</span><span class="sxs-lookup"><span data-stu-id="edacf-146">Click hello **Contact Information** and fill out hello domain's contact information form.</span></span> <span data-ttu-id="edacf-147">Tamamlandığında tıklatarak **Tamam** tooreturn toohello uygulama hizmeti etki alanı sayfası.</span><span class="sxs-lookup"><span data-stu-id="edacf-147">When finished, click **OK** tooreturn toohello App Service Domain page.</span></span>
   
<span data-ttu-id="edacf-148">Mümkün olduğunca doğruluğu ile tüm gerekli alanları doldurun önemlidir.</span><span class="sxs-lookup"><span data-stu-id="edacf-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="edacf-149">İletişim bilgileri için yanlış veri hatası toopurchase alanlarında neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="edacf-149">Incorrect data for contact information can result in failure toopurchase domains.</span></span> 

<span data-ttu-id="edacf-150">Ardından, etki alanınız için istenen hello seçenekleri seçin.</span><span class="sxs-lookup"><span data-stu-id="edacf-150">Next, select hello desired options for your domain.</span></span> <span data-ttu-id="edacf-151">Aşağıdaki tablonun açıklamalarını hello bakın:</span><span class="sxs-lookup"><span data-stu-id="edacf-151">See hello following table for explanations:</span></span>

| <span data-ttu-id="edacf-152">Ayar</span><span class="sxs-lookup"><span data-stu-id="edacf-152">Setting</span></span> | <span data-ttu-id="edacf-153">Önerilen Değer</span><span class="sxs-lookup"><span data-stu-id="edacf-153">Suggested Value</span></span> | <span data-ttu-id="edacf-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="edacf-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="edacf-155">Otomatik yenileme</span><span class="sxs-lookup"><span data-stu-id="edacf-155">Auto renew</span></span> | <span data-ttu-id="edacf-156">**Etkinleştirme**</span><span class="sxs-lookup"><span data-stu-id="edacf-156">**Enable**</span></span> | <span data-ttu-id="edacf-157">Uygulama hizmeti etki alanınızın her yıl otomatik olarak yeniler.</span><span class="sxs-lookup"><span data-stu-id="edacf-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="edacf-158">Kredi kartınızdan ücret yenileme hello aynı anda aynı satın alma ücretinin hello.</span><span class="sxs-lookup"><span data-stu-id="edacf-158">Your credit card is charged hello same purchase price at hello time of renewal.</span></span> |
|<span data-ttu-id="edacf-159">Gizlilik Koruması</span><span class="sxs-lookup"><span data-stu-id="edacf-159">Privacy protection</span></span> | <span data-ttu-id="edacf-160">Etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="edacf-160">Enable</span></span> | <span data-ttu-id="edacf-161">Çok kabul "Merhaba satın alma fiyatına dahil gizlilik korumasını" _ücretsiz_ (kayıt defterine desteklemediği gizlilik korumasını gibi üst düzey etki alanları dışında _. co.in_, _. co.uk_, vb.).</span><span class="sxs-lookup"><span data-stu-id="edacf-161">Opt in too"Privacy protection", which is included in hello purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="edacf-162">Varsayılan ana bilgisayar adları atama</span><span class="sxs-lookup"><span data-stu-id="edacf-162">Assign default hostnames</span></span> | <span data-ttu-id="edacf-163">**www** ve**@**</span><span class="sxs-lookup"><span data-stu-id="edacf-163">**www** and **@**</span></span> | <span data-ttu-id="edacf-164">Select hello konak adı bağlamaları isterseniz istenen.</span><span class="sxs-lookup"><span data-stu-id="edacf-164">Select hello desired hostname bindings, if desired.</span></span> <span data-ttu-id="edacf-165">Merhaba etki alanı satın alma işlemi tamamlandığında, web uygulamanızı seçili hello ana bilgisayar adları erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="edacf-165">When hello domain purchase operation is complete, your web app can be accessed at hello selected hostnames.</span></span> <span data-ttu-id="edacf-166">Merhaba web uygulaması arkasında ise [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), hello seçeneği tooassign hello kök etki alanı görmüyorum (@), çünkü destek A kayıtlarını trafik Yöneticisi yapar.</span><span class="sxs-lookup"><span data-stu-id="edacf-166">If hello web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see hello option tooassign hello root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="edacf-167">Merhaba etki alanı satın alma işlemi tamamlandıktan sonra toohello hostname atamaları değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edacf-167">You can make changes toohello hostname assignments after hello domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="edacf-168">Koşulları kabul etmek ve satın alma</span><span class="sxs-lookup"><span data-stu-id="edacf-168">Accept terms and purchase</span></span>

<span data-ttu-id="edacf-169">Tıklatın **yasal koşulları** tooreview hello koşulları ve hello ücretleri, ardından **satın**.</span><span class="sxs-lookup"><span data-stu-id="edacf-169">Click **Legal Terms** tooreview hello terms and hello charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="edacf-170">Uygulama hizmeti etki alanlarının Azure DNS'ye toohost hello etki alanları kullanın.</span><span class="sxs-lookup"><span data-stu-id="edacf-170">App Service Domains use Azure DNS toohost hello domains.</span></span> <span data-ttu-id="edacf-171">Ayrıca toohello etki alanı kayıt ücreti, kullanım ücretleri Azure DNS için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="edacf-171">In addition toohello domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="edacf-172">Bilgi için bkz: [Azure DNS fiyatlandırma](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="edacf-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="edacf-173">Merhaba edilene **uygulama hizmeti etki alanı** sayfasında, **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="edacf-173">Back in hello **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="edacf-174">Merhaba işlemi sürerken bildirimleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="edacf-174">While hello operation is in progress, you see hello following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="edacf-175">Test hello ana bilgisayar adları</span><span class="sxs-lookup"><span data-stu-id="edacf-175">Test hello hostnames</span></span>

<span data-ttu-id="edacf-176">Varsayılan ana bilgisayar adları tooyour web uygulaması atanmışsa, seçilen her ana bilgisayar adı için bir başarı bildirimi de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edacf-176">If you have assigned default hostnames tooyour web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="edacf-177">Merhaba hello seçili konak adları Ayrıca bkz: **özel etki alanları** sayfasında hello **ana bilgisayar adları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="edacf-177">You also see hello selected hostnames in hello **Custom domains** page, in hello **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="edacf-178">tootest hello ana bilgisayar adı, listelenen toohello ana bilgisayar adları hello tarayıcıda gidin.</span><span class="sxs-lookup"><span data-stu-id="edacf-178">tootest hello hostnames, navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="edacf-179">Merhaba hello örnekte ekran, önceki deneyin too_kontoso.net_ gezinme ve _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="edacf-179">In hello example in hello preceding screenshot, try navigating too_kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-tooweb-app"></a><span data-ttu-id="edacf-180">Ana bilgisayar adları tooweb uygulama atama</span><span class="sxs-lookup"><span data-stu-id="edacf-180">Assign hostnames tooweb app</span></span>

<span data-ttu-id="edacf-181">Değil tooassign birini seçin veya daha fazla varsayılan ana bilgisayar adları tooyour web uygulaması hello sırasında satın alma işlemi ya da tooassign bir ana bilgisayar adı değil gerekiyorsa listelenen bir ana bilgisayar adı zaman atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edacf-181">If you choose not tooassign one or more default hostnames tooyour web app during hello purchase process, or if you need tooassign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="edacf-182">Ayrıca, diğer web uygulaması hello uygulama hizmeti etki alanı tooany konak adları atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edacf-182">You can also assign hostnames in hello App Service Domain tooany other web app.</span></span> <span data-ttu-id="edacf-183">Merhaba adımları olup olmadığını hello uygulama hizmeti etki alanı ve hello web uygulaması toohello ait üzerinde bağımlı aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="edacf-183">hello steps depend on whether hello App Service Domain and hello web app belong toohello same subscription.</span></span>

- <span data-ttu-id="edacf-184">Farklı bir abonelik: eşleme hello uygulama hizmeti etki alanı toohello web uygulamasından harici olarak satın alınan bir etki alanı gibi özel DNS kaydı.</span><span class="sxs-lookup"><span data-stu-id="edacf-184">Different subscription: Map custom DNS records from hello App Service Domain toohello web app like an externally purchased domain.</span></span> <span data-ttu-id="edacf-185">Ekleme özel DNS hakkında bilgi tooan uygulama hizmeti etki alanı adları için bkz: [özel DNS kayıtlarını yönetme](#custom).</span><span class="sxs-lookup"><span data-stu-id="edacf-185">For information on adding custom DNS names tooan App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="edacf-186">toomap bir dış satın alınan etki alanı tooa web uygulaması bkz [bir var olan özel DNS adı tooAzure Web Apps eşleme](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="edacf-186">toomap an external purchased domain tooa web app, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="edacf-187">Aynı abonelik: aşağıdaki adımları kullanın hello.</span><span class="sxs-lookup"><span data-stu-id="edacf-187">Same subscription: Use hello following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="edacf-188">Başlatma ana bilgisayar adı ekleyin</span><span class="sxs-lookup"><span data-stu-id="edacf-188">Launch add hostname</span></span>
<span data-ttu-id="edacf-189">Merhaba, **uygulama hizmetleri** sayfası, web uygulamanızın tooassign konak seçmek için istediğiniz select hello adı **ayarları**ve ardından **özel etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="edacf-189">In hello **App Services** page, select hello name of your web app that you want tooassign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="edacf-190">Satın alınan etki alanınızın hello listelendiğinden emin olun **uygulama hizmet alanları** bölümünde, ancak bunu seçmeyin.</span><span class="sxs-lookup"><span data-stu-id="edacf-190">Make sure that your purchased domain is listed in hello **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="edacf-191">Tüm uygulama hizmeti etki alanlarında aynı abonelik hello web uygulamanızın içinde gösterilen hello **özel etki alanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="edacf-191">All App Service Domains in hello same subscription are shown in hello web app's **Custom domains** page.</span></span> <span data-ttu-id="edacf-192">Merhaba web uygulamanızın abonelikte etki alanınızda olan ancak hello web uygulamanızın içinde göremiyorum **özel etki alanları** sayfasında, hello yeniden açmayı deneyin **özel etki alanları** sayfasında veya hello Web sayfasını yenileyin.</span><span class="sxs-lookup"><span data-stu-id="edacf-192">If your domain is in hello web app's subscription, but you cannot see it in hello web app's **Custom domains** page, try reopening hello **Custom domains** page or refresh hello webpage.</span></span> <span data-ttu-id="edacf-193">Ayrıca, ilerleme durumunu veya oluşturma hataları için hello Azure portal hello üstündeki hello bildirim zil kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="edacf-193">Also, check hello notification bell at hello top of hello Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="edacf-194">Seçin **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="edacf-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="edacf-195">Ana bilgisayar adı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="edacf-195">Configure hostname</span></span>
<span data-ttu-id="edacf-196">Merhaba, **ana bilgisayar adını eklemek** iletişim kutusunda, uygulama hizmeti etki alanı veya herhangi bir alt etki alanı hello tam olarak nitelenmiş etki alanı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="edacf-196">In hello **Add hostname** dialog, type hello fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="edacf-197">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="edacf-197">For example:</span></span>

- <span data-ttu-id="edacf-198">kontoso.NET</span><span class="sxs-lookup"><span data-stu-id="edacf-198">kontoso.net</span></span>
- <span data-ttu-id="edacf-199">www.kontoso.NET</span><span class="sxs-lookup"><span data-stu-id="edacf-199">www.kontoso.net</span></span>
- <span data-ttu-id="edacf-200">ABC.kontoso.NET</span><span class="sxs-lookup"><span data-stu-id="edacf-200">abc.kontoso.net</span></span>

<span data-ttu-id="edacf-201">Tamamlandığında, seçin **doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="edacf-201">When finished, select **Validate**.</span></span> <span data-ttu-id="edacf-202">Merhaba ana bilgisayar adı kayıt türü sizin için otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="edacf-202">hello hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="edacf-203">Seçin **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="edacf-203">Select **Add hostname**.</span></span>

<span data-ttu-id="edacf-204">Merhaba işlemi tamamlandığında, ana bilgisayar adı atanmış hello yönelik bir başarı bildirimi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="edacf-204">When hello operation is complete, you see a success notification for hello assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="edacf-205">Ana bilgisayar adı Kapat ekleme</span><span class="sxs-lookup"><span data-stu-id="edacf-205">Close add hostname</span></span>
<span data-ttu-id="edacf-206">Merhaba, **ana bilgisayar adını eklemek** sayfasında, tüm diğer ana bilgisayar adı tooyour web uygulaması, istenen olarak atayın.</span><span class="sxs-lookup"><span data-stu-id="edacf-206">In hello **Add hostname** page, assign any other hostname tooyour web app, as desired.</span></span> <span data-ttu-id="edacf-207">Tamamlandığında, hello kapatmak **ana bilgisayar adını eklemek** sayfası.</span><span class="sxs-lookup"><span data-stu-id="edacf-207">When finished, close hello **Add hostname** page.</span></span>

<span data-ttu-id="edacf-208">Yeni atanan hello hostname(s), uygulamanızın içinde görmelisiniz **özel etki alanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="edacf-208">You should now see hello newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="edacf-209">Test hello ana bilgisayar adları</span><span class="sxs-lookup"><span data-stu-id="edacf-209">Test hello hostnames</span></span>

<span data-ttu-id="edacf-210">Listelenen toohello ana bilgisayar adları hello tarayıcıda gidin.</span><span class="sxs-lookup"><span data-stu-id="edacf-210">Navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="edacf-211">Ekran görüntüsü önceki hello Hello örnekte, too_abc.kontoso.net_ gezinme deneyin.</span><span class="sxs-lookup"><span data-stu-id="edacf-211">In hello example in hello preceding screenshot, try navigating too_abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="edacf-212">Özel DNS kayıtlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="edacf-212">Manage custom DNS records</span></span>

<span data-ttu-id="edacf-213">Azure üzerinde bir uygulama hizmeti etki alanı için DNS kayıtlarını kullanılarak yönetilen [Azure DNS](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="edacf-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="edacf-214">Ekleyebilir, kaldırabilir, ve DNS kayıtlarını güncelleştirmek, harici olarak satın alınan bir etki alanı için olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="edacf-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="edacf-215">Açık uygulama hizmeti etki alanı</span><span class="sxs-lookup"><span data-stu-id="edacf-215">Open App Service Domain</span></span>

<span data-ttu-id="edacf-216">Merhaba hello sol menüden Azure portal seçin **daha Hizmetleri** > **uygulama hizmet alanları**.</span><span class="sxs-lookup"><span data-stu-id="edacf-216">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="edacf-217">Merhaba etki alanı toomanage seçin.</span><span class="sxs-lookup"><span data-stu-id="edacf-217">Select hello domain toomanage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="edacf-218">Erişim DNS bölgesi</span><span class="sxs-lookup"><span data-stu-id="edacf-218">Access DNS zone</span></span>

<span data-ttu-id="edacf-219">Merhaba etki alanının soldaki menüde seçin **DNS bölgesi**.</span><span class="sxs-lookup"><span data-stu-id="edacf-219">In hello domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="edacf-220">Bu eylemin hello açılır [DNS bölgesi](../dns/dns-zones-records.md) Azure DNS App Service etki alanınızda sayfası.</span><span class="sxs-lookup"><span data-stu-id="edacf-220">This action opens hello [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="edacf-221">Hakkında bilgi için bkz: tooedit DNS kayıtları, [nasıl toomanage DNS bölgelerini Azure portal hello](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="edacf-221">For information on how tooedit DNS records, see [How toomanage DNS Zones in hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="edacf-222">İptal satın alma (delete etki alanı)</span><span class="sxs-lookup"><span data-stu-id="edacf-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="edacf-223">Merhaba uygulama hizmeti etki alanı satın aldıktan sonra satın alma işleminiz tam iade için beş gün toocancel sahip.</span><span class="sxs-lookup"><span data-stu-id="edacf-223">After you purchase hello App Service Domain, you have five days toocancel your purchase for a full refund.</span></span> <span data-ttu-id="edacf-224">Beş gün sonra hello uygulama hizmeti etki alanı silebilir ancak para iadesi alamazsınız.</span><span class="sxs-lookup"><span data-stu-id="edacf-224">After five days, you can delete hello App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="edacf-225">Açık uygulama hizmeti etki alanı</span><span class="sxs-lookup"><span data-stu-id="edacf-225">Open App Service Domain</span></span>

<span data-ttu-id="edacf-226">Merhaba hello sol menüden Azure portal seçin **daha Hizmetleri** > **uygulama hizmet alanları**.</span><span class="sxs-lookup"><span data-stu-id="edacf-226">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="edacf-227">Merhaba etki alanı tooyou istediğiniz toocancel seçin veya silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edacf-227">Select hello domain tooyou want toocancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="edacf-228">Konak adı bağlamaları Sil</span><span class="sxs-lookup"><span data-stu-id="edacf-228">Delete hostname bindings</span></span>

<span data-ttu-id="edacf-229">Merhaba etki alanının soldaki menüde seçin **konak adı bağlamaları**.</span><span class="sxs-lookup"><span data-stu-id="edacf-229">In hello domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="edacf-230">Tüm Azure hizmetlerinden Hello konak adı bağlamaları burada listelenir.</span><span class="sxs-lookup"><span data-stu-id="edacf-230">hello hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="edacf-231">Tüm konak adı bağlamaları silinene kadar hello uygulama hizmeti etki alanı silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="edacf-231">You cannot delete hello App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="edacf-232">Her ana bilgisayar adı bağlama seçerek silme **...**   >  **Silmek**.</span><span class="sxs-lookup"><span data-stu-id="edacf-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="edacf-233">Tüm hello bağlamaları silindikten sonra Seç **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="edacf-233">After all hello bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="edacf-234">İptal veya silme</span><span class="sxs-lookup"><span data-stu-id="edacf-234">Cancel or delete</span></span>

<span data-ttu-id="edacf-235">Merhaba etki alanının soldaki menüde seçin **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="edacf-235">In hello domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="edacf-236">Merhaba iptal süresi satın hello etki alanında değil dolmuşsa, seçin **iptal satın alma**.</span><span class="sxs-lookup"><span data-stu-id="edacf-236">If hello cancellation period on hello purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="edacf-237">Aksi takdirde, gördüğünüz bir **silmek** yerine düğme.</span><span class="sxs-lookup"><span data-stu-id="edacf-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="edacf-238">para iadesi, select olmadan toodelete hello etki alanına **silmek**.</span><span class="sxs-lookup"><span data-stu-id="edacf-238">toodelete hello domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="edacf-239">Seçin **Tamam** tooconfirm hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="edacf-239">Select **OK** tooconfirm hello operation.</span></span> <span data-ttu-id="edacf-240">Tooproceed istemiyorsanız, hello onay iletişim dışında herhangi bir yere tıklayın.</span><span class="sxs-lookup"><span data-stu-id="edacf-240">If you don't want tooproceed, click anywhere outside of hello confirmation dialog.</span></span>

<span data-ttu-id="edacf-241">Merhaba işlemi tamamlandıktan sonra aboneliğiniz yayımlanan ve herkes için kullanılabilir hello etki alanıdır yeniden toopurchase.</span><span class="sxs-lookup"><span data-stu-id="edacf-241">After hello operation is complete, hello domain is released from your subscription and available for anyone toopurchase again.</span></span> 

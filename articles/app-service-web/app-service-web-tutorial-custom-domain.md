---
title: "aaaMap var olan bir özel DNS ad tooAzure Web Apps | Microsoft Docs"
description: "Nasıl tooadd var olan bir özel DNS etki alanı adı (gösterim etki alanında) tooa web uygulaması, mobil uygulama arka ucu veya Azure App Service'teki API uygulamasına öğrenin."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a><span data-ttu-id="cd9e7-103">Harita bir var olan özel DNS adı tooAzure Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="cd9e7-103">Map an existing custom DNS name tooAzure Web Apps</span></span>

<span data-ttu-id="cd9e7-104">[Azure Web Apps](app-service-web-overview.md) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="cd9e7-105">Bu öğretici nasıl toomap var olan bir özel DNS ad tooAzure Web uygulamaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-105">This tutorial shows you how toomap an existing custom DNS name tooAzure Web Apps.</span></span>

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="cd9e7-107">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="cd9e7-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cd9e7-108">Bir alt etki alanı eşleme (örneğin, `www.contoso.com`) bir CNAME kaydı kullanılarak</span><span class="sxs-lookup"><span data-stu-id="cd9e7-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="cd9e7-109">Kök etki alanını eşlemek (örneğin, `contoso.com`) kullanarak bir A kaydı</span><span class="sxs-lookup"><span data-stu-id="cd9e7-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="cd9e7-110">Joker karakter etki alanını eşlemek (örneğin, `*.contoso.com`) bir CNAME kaydı kullanılarak</span><span class="sxs-lookup"><span data-stu-id="cd9e7-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="cd9e7-111">Etki alanı eşlemesi komut dosyaları ile otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="cd9e7-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="cd9e7-112">Kullanabilirsiniz bir **CNAME kaydı** veya bir **kayıt** toomap özel DNS tooApp hizmet adı.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-112">You can use either a **CNAME record** or an **A record** toomap a custom DNS name tooApp Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="cd9e7-113">Bir kök etki alanı dışındaki tüm özel DNS adları için CNAME kullanmanızı öneririz (örneğin, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="cd9e7-114">Canlı site ve kendi DNS etki alanı adı tooApp hizmeti toomigrate bkz [etkin bir DNS adı tooAzure uygulama hizmeti geçirmek](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-114">toomigrate a live site and its DNS domain name tooApp Service, see [Migrate an active DNS name tooAzure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd9e7-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cd9e7-115">Prerequisites</span></span>

<span data-ttu-id="cd9e7-116">toocomplete Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="cd9e7-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="cd9e7-117">[Bir App Service uygulaması oluşturma](/azure/app-service/), veya başka bir öğretici için oluşturduğunuz bir uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="cd9e7-118">Bir etki alanı adı satın alın ve etki alanı sağlayıcınızın (örneğin, GoDaddy) erişim toohello DNS kayıt defteri sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-118">Purchase a domain name and make sure you have access toohello DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="cd9e7-119">Örneğin, için DNS girişleri tooadd `contoso.com` ve `www.contoso.com`, mümkün tooconfigure hello DNS ayarlarını hello olmalıdır `contoso.com` kök etki alanı.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-119">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must be able tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="cd9e7-120">Ad, göz önünde bulundurun var olan bir etki alanı yoksa [hello Azure portal kullanarak bir etki alanı satın alma](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-120">If you don't have an existing domain name, consider [purchasing a domain using hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-hello-app"></a><span data-ttu-id="cd9e7-121">Merhaba uygulamasını hazırlama</span><span class="sxs-lookup"><span data-stu-id="cd9e7-121">Prepare hello app</span></span>

<span data-ttu-id="cd9e7-122">bir özel DNS adı tooa web uygulamanızın, hello web uygulaması toomap [uygulama hizmeti planı](https://azure.microsoft.com/pricing/details/app-service/) Ücretli katmanı olmalıdır (**paylaşılan**, **temel**, **standart**, veya  **Premium**).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-122">toomap a custom DNS name tooa web app, hello web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="cd9e7-123">Bu adımda, fiyatlandırma katmanı bu hello uygulama hello uygulamadır hizmeti desteklenen emin olun.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-123">In this step, you make sure that hello App Service app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="cd9e7-124">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="cd9e7-124">Sign in tooAzure</span></span>

<span data-ttu-id="cd9e7-125">Açık hello [Azure portal](https://portal.azure.com) ve Azure hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-125">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="cd9e7-126">Toohello uygulamada hello Azure portalına gidin</span><span class="sxs-lookup"><span data-stu-id="cd9e7-126">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="cd9e7-127">Merhaba sol menüden seçin **uygulama hizmetleri**ve ardından hello uygulamasının hello adı seçin.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-127">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="cd9e7-129">Merhaba App Service uygulaması hello Yönetimi sayfasında bakın.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-129">You see hello management page of hello App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="cd9e7-130">Fiyatlandırma katmanı hello denetleyin</span><span class="sxs-lookup"><span data-stu-id="cd9e7-130">Check hello pricing tier</span></span>

<span data-ttu-id="cd9e7-131">Sol gezinti hello uygulama sayfasının hello toohello kaydırma **ayarları** bölümünde ve seçin **(uygulama hizmeti planı) ölçeklendirme**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-131">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Büyütme menüsü](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="cd9e7-133">Merhaba uygulamanın geçerli katmanı mavi kenarlığı ile vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-133">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="cd9e7-134">Bu hello uygulama hello olmadığından emin toomake denetleyin **serbest** katmanı.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-134">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="cd9e7-135">Özel DNS hello desteklenmiyor **serbest** katmanı.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-135">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="cd9e7-137">Merhaba uygulama hizmeti planı değilse **serbest**, Kapat hello **fiyatlandırma katmanınızı seçin** sayfasında ve çok atla[bir CNAME kaydı eşleme](#cname).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-137">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="cd9e7-138">Uygulama hizmeti planı Hello ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="cd9e7-138">Scale up hello App Service plan</span></span>

<span data-ttu-id="cd9e7-139">Merhaba boş olmayan katmanları birini seçin (**paylaşılan**, **temel**, **standart**, veya **Premium**).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-139">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="cd9e7-140">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-140">Click **Select**.</span></span>

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="cd9e7-142">Bildirim aşağıdaki hello gördüğünüzde, hello ölçeklendirme işlemi tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-142">When you see hello following notification, hello scale operation is complete.</span></span>

![Ölçek işlemi onayı](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="cd9e7-144">Harita bir CNAME kaydı</span><span class="sxs-lookup"><span data-stu-id="cd9e7-144">Map a CNAME record</span></span>

<span data-ttu-id="cd9e7-145">Başlangıç Öğreticisi örnekte hello için bir CNAME kaydı ekleyin `www` alt etki alanı (örneğin, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-145">In hello tutorial example, you add a CNAME record for hello `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="cd9e7-146">Merhaba CNAME kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-146">Create hello CNAME record</span></span>

<span data-ttu-id="cd9e7-147">Bir alt etki alanı toohello uygulamanın varsayılan ana bilgisayar adı bir CNAME kaydı toomap ekleyin (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-147">Add a CNAME record toomap a subdomain toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="cd9e7-148">Hello için `www.contoso.com` etki alanı örneği hello adı eşleyen bir CNAME kaydı ekleyin `www` çok`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-148">For hello `www.contoso.com` domain example, add a CNAME record that maps hello name `www` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="cd9e7-149">Merhaba CNAME ekledikten sonra aşağıdaki örneğine hello gibi hello DNS kayıtları sayfasında görünür:</span><span class="sxs-lookup"><span data-stu-id="cd9e7-149">After you add hello CNAME, hello DNS records page looks like hello following example:</span></span>

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a><span data-ttu-id="cd9e7-151">Azure'da Hello CNAME kaydı eşleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="cd9e7-151">Enable hello CNAME record mapping in Azure</span></span>

<span data-ttu-id="cd9e7-152">Hello Azure portalında sol gezinti hello uygulama sayfasının hello seçin **özel etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-152">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Özel etki alanı menüsü](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="cd9e7-154">Merhaba, **özel etki alanları** sayfa hello özel DNS adını tam hello uygulama Ekle (`www.contoso.com`) toohello listesi.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-154">In hello **Custom domains** page of hello app, add hello fully qualified custom DNS name (`www.contoso.com`) toohello list.</span></span>

<span data-ttu-id="cd9e7-155">Select hello  **+**  simgesi sonraki çok**ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-155">Select hello **+** icon next too**Add hostname**.</span></span>

![Ana bilgisayar adı ekleyin](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="cd9e7-157">Merhaba tam etki alanı adını yazın, için bir CNAME kaydı gibi eklenen `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-157">Type hello fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="cd9e7-158">Seçin **doğrulamak**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-158">Select **Validate**.</span></span>

<span data-ttu-id="cd9e7-159">Merhaba **ana bilgisayar adını eklemek** düğmesi etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-159">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="cd9e7-160">Olduğundan emin olun **ana bilgisayar adı kayıt türü** çok ayarlanır**CNAME (www.example.com veya herhangi bir alt etki alanı)**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-160">Make sure that **Hostname record type** is set too**CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="cd9e7-161">Seçin **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-161">Select **Add hostname**.</span></span>

![DNS adı toohello uygulama Ekle](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="cd9e7-163">Merhaba uygulamanın içinde yansıtılan hello yeni ana bilgisayar adı toobe için biraz zaman alabilir **özel etki alanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-163">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="cd9e7-164">Merhaba tarayıcı tooupdate hello verileri yenilemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-164">Try refreshing hello browser tooupdate hello data.</span></span>

![CNAME kaydı eklendi](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="cd9e7-166">Bir adımı eksik veya herhangi bir yerde yazmış hello sayfa hello altındaki bir doğrulama hatası daha önce bkz.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-166">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Doğrulama hatası](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="cd9e7-168">Bir A kaydı eşleme</span><span class="sxs-lookup"><span data-stu-id="cd9e7-168">Map an A record</span></span>

<span data-ttu-id="cd9e7-169">Başlangıç Öğreticisi örnekte hello kök etki alanı için bir A kaydı ekleyin (örneğin, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-169">In hello tutorial example, you add an A record for hello root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a><span data-ttu-id="cd9e7-170">Merhaba uygulamanın IP adresini kopyalayın</span><span class="sxs-lookup"><span data-stu-id="cd9e7-170">Copy hello app's IP address</span></span>

<span data-ttu-id="cd9e7-171">toomap bir A kaydı hello uygulamanın dış IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-171">toomap an A record, you need hello app's external IP address.</span></span> <span data-ttu-id="cd9e7-172">Bu IP adresi hello uygulamanın içinde bulabilirsiniz **özel etki alanları** hello Azure portal sayfasında.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-172">You can find this IP address in hello app's **Custom domains** page in hello Azure portal.</span></span>

<span data-ttu-id="cd9e7-173">Hello Azure portalında sol gezinti hello uygulama sayfasının hello seçin **özel etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-173">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Özel etki alanı menüsü](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="cd9e7-175">Merhaba, **özel etki alanları** sayfasında, hello uygulamanın IP adresini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-175">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a><span data-ttu-id="cd9e7-177">Merhaba A kaydını oluşturun</span><span class="sxs-lookup"><span data-stu-id="cd9e7-177">Create hello A record</span></span>

<span data-ttu-id="cd9e7-178">toomap bir A kaydı tooan uygulama, uygulama hizmeti gerekiyor. **iki** DNS kayıtları:</span><span class="sxs-lookup"><span data-stu-id="cd9e7-178">toomap an A record tooan app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="cd9e7-179">Bir **A** toomap toohello uygulamanın IP adresini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-179">An **A** record toomap toohello app's IP address.</span></span>
- <span data-ttu-id="cd9e7-180">A **TXT** toomap toohello uygulamanın varsayılan ana bilgisayar adı kayıt `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-180">A **TXT** record toomap toohello app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="cd9e7-181">Uygulama hizmeti bu kaydı yalnızca yapılandırması sırasında hello özel etki alanı kendi tooverify kullanır.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-181">App Service uses this record only at configuration time, tooverify that you own hello custom domain.</span></span> <span data-ttu-id="cd9e7-182">Özel etki alanınız doğrulandı ve App Service'te yapılandırdıktan sonra bu TXT kaydı silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="cd9e7-183">Hello için `contoso.com` etki alanı örneği, aşağıdaki tablonun toohello göre hello A ve TXT kayıtlarını oluşturun (`@` genellikle temsil kök etki alanı hello).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-183">For hello `contoso.com` domain example, create hello A and TXT records according toohello following table (`@` typically represents hello root domain).</span></span> 

| <span data-ttu-id="cd9e7-184">Kayıt türü</span><span class="sxs-lookup"><span data-stu-id="cd9e7-184">Record type</span></span> | <span data-ttu-id="cd9e7-185">Host</span><span class="sxs-lookup"><span data-stu-id="cd9e7-185">Host</span></span> | <span data-ttu-id="cd9e7-186">Değer</span><span class="sxs-lookup"><span data-stu-id="cd9e7-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="cd9e7-187">A</span><span class="sxs-lookup"><span data-stu-id="cd9e7-187">A</span></span> | `@` | <span data-ttu-id="cd9e7-188">IP adresinden [kopyalama hello uygulamanın IP adresi](#info)</span><span class="sxs-lookup"><span data-stu-id="cd9e7-188">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="cd9e7-189">TXT</span><span class="sxs-lookup"><span data-stu-id="cd9e7-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="cd9e7-190">Merhaba kayıtları eklendiğinde, hello DNS kayıtları sayfasında hello örnek aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="cd9e7-190">When hello records are added, hello DNS records page looks like hello following example:</span></span>

![DNS kayıtları sayfasında](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a><span data-ttu-id="cd9e7-192">Merhaba hello uygulama kaydı eşlemesindeki etkinleştir</span><span class="sxs-lookup"><span data-stu-id="cd9e7-192">Enable hello A record mapping in hello app</span></span>

<span data-ttu-id="cd9e7-193">Merhaba uygulamanın edilene **özel etki alanları** sayfasında hello Azure portal, hello özel DNS adını tam ekleyin (örneğin, `contoso.com`) toohello listesi.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-193">Back in hello app's **Custom domains** page in hello Azure portal, add hello fully qualified custom DNS name (for example, `contoso.com`) toohello list.</span></span>

<span data-ttu-id="cd9e7-194">Select hello  **+**  simgesi sonraki çok**ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-194">Select hello **+** icon next too**Add hostname**.</span></span>

![Ana bilgisayar adı ekleyin](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="cd9e7-196">Merhaba A kaydı, aşağıdaki gibi yapılandırılmış türü hello tam etki alanı adı `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-196">Type hello fully qualified domain name that you configured hello A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="cd9e7-197">Seçin **doğrulamak**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-197">Select **Validate**.</span></span>

<span data-ttu-id="cd9e7-198">Merhaba **ana bilgisayar adını eklemek** düğmesi etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-198">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="cd9e7-199">Olduğundan emin olun **ana bilgisayar adı kayıt türü** çok ayarlanır**bir kayıt (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-199">Make sure that **Hostname record type** is set too**A record (example.com)**.</span></span>

<span data-ttu-id="cd9e7-200">Seçin **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-200">Select **Add hostname**.</span></span>

![DNS adı toohello uygulama Ekle](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="cd9e7-202">Merhaba uygulamanın içinde yansıtılan hello yeni ana bilgisayar adı toobe için biraz zaman alabilir **özel etki alanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-202">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="cd9e7-203">Merhaba tarayıcı tooupdate hello verileri yenilemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-203">Try refreshing hello browser tooupdate hello data.</span></span>

![Bir kayıt eklendi](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="cd9e7-205">Bir adımı eksik veya herhangi bir yerde yazmış hello sayfa hello altındaki bir doğrulama hatası daha önce bkz.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-205">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Doğrulama hatası](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="cd9e7-207">Bir joker karakter etki alanına Eşle</span><span class="sxs-lookup"><span data-stu-id="cd9e7-207">Map a wildcard domain</span></span>

<span data-ttu-id="cd9e7-208">Hello öğretici örnekte, eşleme bir [joker DNS adına](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (örneğin, `*.contoso.com`) toohello bir CNAME kaydı ekleyerek App Service uygulaması.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-208">In hello tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) toohello App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="cd9e7-209">Merhaba CNAME kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-209">Create hello CNAME record</span></span>

<span data-ttu-id="cd9e7-210">Bir joker karakter adı toohello uygulamanın varsayılan ana bilgisayar adı bir CNAME kaydı toomap ekleyin (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-210">Add a CNAME record toomap a wildcard name toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="cd9e7-211">Hello için `*.contoso.com` etki alanı örneği hello CNAME kaydı hello adı eşleme `*` çok`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-211">For hello `*.contoso.com` domain example, hello CNAME record will map hello name `*` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="cd9e7-212">Merhaba CNAME eklendiğinde hello DNS kayıtları sayfasında hello örnek aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="cd9e7-212">When hello CNAME is added, hello DNS records page looks like hello following example:</span></span>

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a><span data-ttu-id="cd9e7-214">Merhaba uygulamasında Hello CNAME kaydı eşleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="cd9e7-214">Enable hello CNAME record mapping in hello app</span></span>

<span data-ttu-id="cd9e7-215">Merhaba joker adı toohello uygulama eşleşen alt etki alanı artık ekleyebilirsiniz (örneğin, `sub1.contoso.com` ve `sub2.contoso.com` eşleşen `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-215">You can now add any subdomain that matches hello wildcard name toohello app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="cd9e7-216">Hello Azure portalında sol gezinti hello uygulama sayfasının hello seçin **özel etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-216">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Özel etki alanı menüsü](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="cd9e7-218">Select hello  **+**  simgesi sonraki çok**ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-218">Select hello **+** icon next too**Add hostname**.</span></span>

![Ana bilgisayar adı ekleyin](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="cd9e7-220">Merhaba joker karakter etki alanıyla eşleşen bir tam etki alanı adı yazın (örneğin, `sub1.contoso.com`) ve ardından **doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-220">Type a fully qualified domain name that matches hello wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="cd9e7-221">Merhaba **ana bilgisayar adını eklemek** düğmesi etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-221">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="cd9e7-222">Olduğundan emin olun **ana bilgisayar adı kayıt türü** çok ayarlanır**CNAME kaydı (www.example.com veya herhangi bir alt etki alanı)**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-222">Make sure that **Hostname record type** is set too**CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="cd9e7-223">Seçin **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-223">Select **Add hostname**.</span></span>

![DNS adı toohello uygulama Ekle](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="cd9e7-225">Merhaba uygulamanın içinde yansıtılan hello yeni ana bilgisayar adı toobe için biraz zaman alabilir **özel etki alanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-225">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="cd9e7-226">Merhaba tarayıcı tooupdate hello verileri yenilemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-226">Try refreshing hello browser tooupdate hello data.</span></span>

<span data-ttu-id="cd9e7-227">Select hello  **+**  simge tekrar tooadd hello joker karakter etki alanıyla eşleşen başka bir ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-227">Select hello **+** icon again tooadd another hostname that matches hello wildcard domain.</span></span> <span data-ttu-id="cd9e7-228">Örneğin, ekleyin `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-228">For example, add `sub2.contoso.com`.</span></span>

![CNAME kaydı eklendi](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="cd9e7-230">Tarayıcıda test</span><span class="sxs-lookup"><span data-stu-id="cd9e7-230">Test in browser</span></span>

<span data-ttu-id="cd9e7-231">Daha önce yapılandırılmış toohello DNS adları göz atın (örneğin, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, ve `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-231">Browse toohello DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="cd9e7-233">Komut dosyalarıyla otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="cd9e7-233">Automate with scripts</span></span>

<span data-ttu-id="cd9e7-234">Hello kullanarak yönetim komut dosyaları ile özel etki alanlarının otomatik hale getirebilirsiniz [Azure CLI](/cli/azure/install-azure-cli) veya [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-234">You can automate management of custom domains with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="cd9e7-235">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cd9e7-235">Azure CLI</span></span> 

<span data-ttu-id="cd9e7-236">komutu aşağıdaki hello bir yapılandırılmış özel DNS adı tooan App Service uygulaması ekler.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-236">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="cd9e7-237">Daha fazla bilgi için bkz: [bir özel etki alanı tooa web uygulaması eşleme](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-237">For more information, see [Map a custom domain tooa web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="cd9e7-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd9e7-238">Azure PowerShell</span></span> 

<span data-ttu-id="cd9e7-239">komutu aşağıdaki hello bir yapılandırılmış özel DNS adı tooan App Service uygulaması ekler.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-239">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="cd9e7-240">Daha fazla bilgi için bkz: [bir özel etki alanı tooa web uygulaması atamak](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="cd9e7-240">For more information, see [Assign a custom domain tooa web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd9e7-241">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cd9e7-241">Next steps</span></span>

<span data-ttu-id="cd9e7-242">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="cd9e7-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cd9e7-243">Bir alt etki alanı CNAME kaydı kullanılarak eşleme</span><span class="sxs-lookup"><span data-stu-id="cd9e7-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="cd9e7-244">Bir A kaydı kullanarak bir kök etki alanına Eşle</span><span class="sxs-lookup"><span data-stu-id="cd9e7-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="cd9e7-245">Bir CNAME kaydı kullanılarak bir joker karakter etki alanına Eşle</span><span class="sxs-lookup"><span data-stu-id="cd9e7-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="cd9e7-246">Etki alanı eşlemesi komut dosyaları ile otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="cd9e7-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="cd9e7-247">İlerlemek toohello sonraki öğretici toolearn nasıl toobind özel bir SSL sertifikası tooa web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="cd9e7-247">Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cd9e7-248">Bir var olan özel SSL sertifika tooAzure Web Apps bağlama</span><span class="sxs-lookup"><span data-stu-id="cd9e7-248">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)

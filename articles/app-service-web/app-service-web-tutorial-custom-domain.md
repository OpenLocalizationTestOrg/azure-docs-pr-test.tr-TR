---
title: "Azure Web uygulamaları için var olan bir özel DNS ad eşleme | Microsoft Docs"
description: "Bir web uygulaması, mobil uygulama arka ucu veya Azure App Service'teki API uygulamasına varolan özel DNS etki alanı adı (gösterim etki alanında) eklemeyi öğrenin."
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
ms.openlocfilehash: 973cda462e8d258cc848e1036891c7f8af043102
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="map-an-existing-custom-dns-name-to-azure-web-apps"></a><span data-ttu-id="3efa1-103">Harita Azure Web uygulamaları için varolan bir özel DNS adı</span><span class="sxs-lookup"><span data-stu-id="3efa1-103">Map an existing custom DNS name to Azure Web Apps</span></span>

<span data-ttu-id="3efa1-104">[Azure Web Apps](app-service-web-overview.md) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="3efa1-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="3efa1-105">Bu öğretici, Azure Web uygulamaları için var olan bir özel DNS adını eşleştirmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="3efa1-105">This tutorial shows you how to map an existing custom DNS name to Azure Web Apps.</span></span>

![Azure App portalında gezinme](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="3efa1-107">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="3efa1-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3efa1-108">Bir alt etki alanı eşleme (örneğin, `www.contoso.com`) bir CNAME kaydı kullanılarak</span><span class="sxs-lookup"><span data-stu-id="3efa1-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="3efa1-109">Kök etki alanını eşlemek (örneğin, `contoso.com`) kullanarak bir A kaydı</span><span class="sxs-lookup"><span data-stu-id="3efa1-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="3efa1-110">Joker karakter etki alanını eşlemek (örneğin, `*.contoso.com`) bir CNAME kaydı kullanılarak</span><span class="sxs-lookup"><span data-stu-id="3efa1-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="3efa1-111">Etki alanı eşlemesi komut dosyaları ile otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="3efa1-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="3efa1-112">Ya da kullanabileceğiniz bir **CNAME kaydı** veya bir **bir kayıt** App Service'e bir özel DNS adını eşleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3efa1-112">You can use either a **CNAME record** or an **A record** to map a custom DNS name to App Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="3efa1-113">Bir kök etki alanı dışındaki tüm özel DNS adları için CNAME kullanmanızı öneririz (örneğin, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3efa1-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="3efa1-114">Canlı site ve DNS etki alanı adını App Service'e geçirmek için bkz [etkin bir DNS adı Azure App Service'e geçirme](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="3efa1-114">To migrate a live site and its DNS domain name to App Service, see [Migrate an active DNS name to Azure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3efa1-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3efa1-115">Prerequisites</span></span>

<span data-ttu-id="3efa1-116">Bu öğreticiyi tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="3efa1-116">To complete this tutorial:</span></span>

* <span data-ttu-id="3efa1-117">[Bir App Service uygulaması oluşturma](/azure/app-service/), veya başka bir öğretici için oluşturduğunuz bir uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="3efa1-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="3efa1-118">Bir etki alanı adı satın alın ve etki alanı sağlayıcınızın (örneğin, GoDaddy) DNS kayıt defterine erişim olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3efa1-118">Purchase a domain name and make sure you have access to the DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="3efa1-119">Örneğin, DNS girişlerini eklemek için `contoso.com` ve `www.contoso.com`, DNS ayarlarını yapılandırın olmalıdır `contoso.com` kök etki alanı.</span><span class="sxs-lookup"><span data-stu-id="3efa1-119">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must be able to configure the DNS settings for the `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3efa1-120">Ad, göz önünde bulundurun var olan bir etki alanı yoksa [Azure portalını kullanarak bir etki alanı satın alma](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="3efa1-120">If you don't have an existing domain name, consider [purchasing a domain using the Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-the-app"></a><span data-ttu-id="3efa1-121">Uygulamayı hazırlayın</span><span class="sxs-lookup"><span data-stu-id="3efa1-121">Prepare the app</span></span>

<span data-ttu-id="3efa1-122">Özel bir DNS adı bir web uygulamanızın için web uygulaması eşlemek için [uygulama hizmeti planı](https://azure.microsoft.com/pricing/details/app-service/) Ücretli katmanı olmalıdır (**paylaşılan**, **temel**, **standart**, veya  **Premium**).</span><span class="sxs-lookup"><span data-stu-id="3efa1-122">To map a custom DNS name to a web app, the web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="3efa1-123">Bu adımda, App Service uygulaması desteklenen fiyatlandırma katmanı olan olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3efa1-123">In this step, you make sure that the App Service app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="3efa1-124">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="3efa1-124">Sign in to Azure</span></span>

<span data-ttu-id="3efa1-125">Açık [Azure portal](https://portal.azure.com) ve Azure hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3efa1-125">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="3efa1-126">Azure portalında uygulama gidin</span><span class="sxs-lookup"><span data-stu-id="3efa1-126">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="3efa1-127">Sol menüden seçin **uygulama hizmetleri**ve ardından uygulama adını seçin.</span><span class="sxs-lookup"><span data-stu-id="3efa1-127">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Azure App portalında gezinme](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="3efa1-129">Uygulama Hizmeti uygulamasının yönetim sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="3efa1-129">You see the management page of the App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-the-pricing-tier"></a><span data-ttu-id="3efa1-130">Fiyatlandırma katmanı denetleyin</span><span class="sxs-lookup"><span data-stu-id="3efa1-130">Check the pricing tier</span></span>

<span data-ttu-id="3efa1-131">Uygulama sayfanın sol gezinti bölmesinde kaydırın **ayarları** bölümünde ve seçin **(uygulama hizmeti planı) ölçeklendirme**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-131">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Büyütme menüsü](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="3efa1-133">Uygulamanın geçerli katmanı mavi kenarlığı ile vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="3efa1-133">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="3efa1-134">Uygulama içinde olmadığından emin olmak için kontrol edin **serbest** katmanı.</span><span class="sxs-lookup"><span data-stu-id="3efa1-134">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="3efa1-135">İçinde özel DNS desteklenmiyor **serbest** katmanı.</span><span class="sxs-lookup"><span data-stu-id="3efa1-135">Custom DNS is not supported in the **Free** tier.</span></span> 

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="3efa1-137">Uygulama hizmeti planı değilse **serbest**, Kapat **fiyatlandırma katmanınızı seçin** sayfasında ve geçin [bir CNAME kaydı eşleme](#cname).</span><span class="sxs-lookup"><span data-stu-id="3efa1-137">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="3efa1-138">Uygulama hizmeti planı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="3efa1-138">Scale up the App Service plan</span></span>

<span data-ttu-id="3efa1-139">Boş olmayan katmanları birini seçin (**paylaşılan**, **temel**, **standart**, veya **Premium**).</span><span class="sxs-lookup"><span data-stu-id="3efa1-139">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="3efa1-140">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3efa1-140">Click **Select**.</span></span>

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="3efa1-142">Aşağıdaki bildirim görürseniz, bir ölçeklendirme işlemi tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="3efa1-142">When you see the following notification, the scale operation is complete.</span></span>

![Ölçek işlemi onayı](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="3efa1-144">Harita bir CNAME kaydı</span><span class="sxs-lookup"><span data-stu-id="3efa1-144">Map a CNAME record</span></span>

<span data-ttu-id="3efa1-145">Eğitmen örnekte için bir CNAME kaydı ekleyin `www` alt etki alanı (örneğin, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3efa1-145">In the tutorial example, you add a CNAME record for the `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="3efa1-146">CNAME kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3efa1-146">Create the CNAME record</span></span>

<span data-ttu-id="3efa1-147">Uygulamanın varsayılan ana bilgisayar adı için bir alt etki alanı eşlemek için bir CNAME kaydı ekleyin (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="3efa1-147">Add a CNAME record to map a subdomain to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="3efa1-148">İçin `www.contoso.com` etki alanı örneği adı eşleyen bir CNAME kaydı ekleyin `www` için `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="3efa1-148">For the `www.contoso.com` domain example, add a CNAME record that maps the name `www` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="3efa1-149">CNAME ekledikten sonra DNS kayıtları sayfasında aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="3efa1-149">After you add the CNAME, the DNS records page looks like the following example:</span></span>

![Azure App portalında gezinme](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-the-cname-record-mapping-in-azure"></a><span data-ttu-id="3efa1-151">CNAME kaydı eşleme Azure içinde etkinleştir</span><span class="sxs-lookup"><span data-stu-id="3efa1-151">Enable the CNAME record mapping in Azure</span></span>

<span data-ttu-id="3efa1-152">Azure Portalı'nda uygulama sayfası sol gezinti bölmesinde seçin **özel etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-152">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Özel etki alanı menüsü](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="3efa1-154">İçinde **özel etki alanları** sayfası uygulama, özel tam DNS adı Ekle (`www.contoso.com`) listesi.</span><span class="sxs-lookup"><span data-stu-id="3efa1-154">In the **Custom domains** page of the app, add the fully qualified custom DNS name (`www.contoso.com`) to the list.</span></span>

<span data-ttu-id="3efa1-155">Seçin  **+**  yanındaki simge **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-155">Select the **+** icon next to **Add hostname**.</span></span>

![Ana bilgisayar adı ekleyin](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="3efa1-157">İçin bir CNAME kaydı gibi eklenen tam etki alanı adı yazın `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="3efa1-157">Type the fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="3efa1-158">Seçin **doğrulamak**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-158">Select **Validate**.</span></span>

<span data-ttu-id="3efa1-159">**Ana bilgisayar adını eklemek** düğmesi etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3efa1-159">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="3efa1-160">Olduğundan emin olun **ana bilgisayar adı kayıt türü** ayarlanır **CNAME (www.example.com veya herhangi bir alt etki alanı)**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-160">Make sure that **Hostname record type** is set to **CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="3efa1-161">Seçin **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-161">Select **Add hostname**.</span></span>

![DNS adı için uygulama ekleme](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="3efa1-163">Uygulamanın içinde yansıtılması yeni ana bilgisayar adı için biraz zaman alabilir **özel etki alanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="3efa1-163">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="3efa1-164">Verileri güncelleştirmek için tarayıcıyı yenilemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="3efa1-164">Try refreshing the browser to update the data.</span></span>

![CNAME kaydı eklendi](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="3efa1-166">Bir adımı eksik veya herhangi bir yerde yazmış daha önce sayfanın sonundaki bir doğrulama hatası görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3efa1-166">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Doğrulama hatası](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="3efa1-168">Bir A kaydı eşleme</span><span class="sxs-lookup"><span data-stu-id="3efa1-168">Map an A record</span></span>

<span data-ttu-id="3efa1-169">Eğitmen örnekte kök etki alanı için bir A kaydı ekleyin (örneğin, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3efa1-169">In the tutorial example, you add an A record for the root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-the-apps-ip-address"></a><span data-ttu-id="3efa1-170">Uygulamanın IP adresini kopyalayın</span><span class="sxs-lookup"><span data-stu-id="3efa1-170">Copy the app's IP address</span></span>

<span data-ttu-id="3efa1-171">Bir A kaydı eşlemek için uygulamanın dış IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3efa1-171">To map an A record, you need the app's external IP address.</span></span> <span data-ttu-id="3efa1-172">Bu IP adresi uygulamanın içinde bulabilirsiniz **özel etki alanları** Azure portalında sayfası.</span><span class="sxs-lookup"><span data-stu-id="3efa1-172">You can find this IP address in the app's **Custom domains** page in the Azure portal.</span></span>

<span data-ttu-id="3efa1-173">Azure Portalı'nda uygulama sayfası sol gezinti bölmesinde seçin **özel etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-173">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Özel etki alanı menüsü](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="3efa1-175">İçinde **özel etki alanları** sayfasında, uygulamanın IP adresini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3efa1-175">In the **Custom domains** page, copy the app's IP address.</span></span>

![Azure App portalında gezinme](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-a-record"></a><span data-ttu-id="3efa1-177">A kaydını oluşturun</span><span class="sxs-lookup"><span data-stu-id="3efa1-177">Create the A record</span></span>

<span data-ttu-id="3efa1-178">Bir uygulama için bir A kaydı eşlemek için uygulama hizmeti gerektirir **iki** DNS kayıtları:</span><span class="sxs-lookup"><span data-stu-id="3efa1-178">To map an A record to an app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="3efa1-179">Bir **A** uygulamanın IP adresine eşlemek için kayıt.</span><span class="sxs-lookup"><span data-stu-id="3efa1-179">An **A** record to map to the app's IP address.</span></span>
- <span data-ttu-id="3efa1-180">A **TXT** uygulamanın varsayılan hostname eşlemek için kayıt `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="3efa1-180">A **TXT** record to map to the app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="3efa1-181">Uygulama hizmeti bu kaydı yalnızca yapılandırması sırasında özel etki alanı sahibi olduğunu doğrulamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="3efa1-181">App Service uses this record only at configuration time, to verify that you own the custom domain.</span></span> <span data-ttu-id="3efa1-182">Özel etki alanınız doğrulandı ve App Service'te yapılandırdıktan sonra bu TXT kaydı silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3efa1-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="3efa1-183">İçin `contoso.com` etki alanı örneği aşağıdaki tabloya göre A ve TXT kayıtlarını oluşturun (`@` genellikle kök etki alanını temsil eder).</span><span class="sxs-lookup"><span data-stu-id="3efa1-183">For the `contoso.com` domain example, create the A and TXT records according to the following table (`@` typically represents the root domain).</span></span> 

| <span data-ttu-id="3efa1-184">Kayıt türü</span><span class="sxs-lookup"><span data-stu-id="3efa1-184">Record type</span></span> | <span data-ttu-id="3efa1-185">Host</span><span class="sxs-lookup"><span data-stu-id="3efa1-185">Host</span></span> | <span data-ttu-id="3efa1-186">Değer</span><span class="sxs-lookup"><span data-stu-id="3efa1-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="3efa1-187">A</span><span class="sxs-lookup"><span data-stu-id="3efa1-187">A</span></span> | `@` | <span data-ttu-id="3efa1-188">IP adresinden [uygulamanın IP adresini kopyalayın](#info)</span><span class="sxs-lookup"><span data-stu-id="3efa1-188">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="3efa1-189">TXT</span><span class="sxs-lookup"><span data-stu-id="3efa1-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="3efa1-190">Kayıtları eklendiğinde, DNS kayıtları sayfasında aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="3efa1-190">When the records are added, the DNS records page looks like the following example:</span></span>

![DNS kayıtları sayfasında](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-the-a-record-mapping-in-the-app"></a><span data-ttu-id="3efa1-192">Uygulama A kaydı eşleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="3efa1-192">Enable the A record mapping in the app</span></span>

<span data-ttu-id="3efa1-193">Uygulamanın edilene **özel etki alanları** sayfasında Azure Portalı'nda, özel tam DNS adı ekleyin (örneğin, `contoso.com`) listesi.</span><span class="sxs-lookup"><span data-stu-id="3efa1-193">Back in the app's **Custom domains** page in the Azure portal, add the fully qualified custom DNS name (for example, `contoso.com`) to the list.</span></span>

<span data-ttu-id="3efa1-194">Seçin  **+**  yanındaki simge **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-194">Select the **+** icon next to **Add hostname**.</span></span>

![Ana bilgisayar adı ekleyin](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="3efa1-196">A kaydı için aşağıdaki gibi yapılandırılmış tam etki alanı adı yazın `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="3efa1-196">Type the fully qualified domain name that you configured the A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="3efa1-197">Seçin **doğrulamak**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-197">Select **Validate**.</span></span>

<span data-ttu-id="3efa1-198">**Ana bilgisayar adını eklemek** düğmesi etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3efa1-198">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="3efa1-199">Olduğundan emin olun **ana bilgisayar adı kayıt türü** ayarlanır **bir kayıt (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-199">Make sure that **Hostname record type** is set to **A record (example.com)**.</span></span>

<span data-ttu-id="3efa1-200">Seçin **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-200">Select **Add hostname**.</span></span>

![DNS adı için uygulama ekleme](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="3efa1-202">Uygulamanın içinde yansıtılması yeni ana bilgisayar adı için biraz zaman alabilir **özel etki alanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="3efa1-202">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="3efa1-203">Verileri güncelleştirmek için tarayıcıyı yenilemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="3efa1-203">Try refreshing the browser to update the data.</span></span>

![Bir kayıt eklendi](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="3efa1-205">Bir adımı eksik veya herhangi bir yerde yazmış daha önce sayfanın sonundaki bir doğrulama hatası görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3efa1-205">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Doğrulama hatası](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="3efa1-207">Bir joker karakter etki alanına Eşle</span><span class="sxs-lookup"><span data-stu-id="3efa1-207">Map a wildcard domain</span></span>

<span data-ttu-id="3efa1-208">Eğitmen örnekte, eşleme bir [joker DNS adına](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (örneğin, `*.contoso.com`) için bir CNAME kaydı ekleyerek App Service uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3efa1-208">In the tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) to the App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="3efa1-209">CNAME kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3efa1-209">Create the CNAME record</span></span>

<span data-ttu-id="3efa1-210">Uygulamanın varsayılan ana bilgisayar adı için bir joker karakter ad eşlemek için bir CNAME kaydı ekleyin (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="3efa1-210">Add a CNAME record to map a wildcard name to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="3efa1-211">İçin `*.contoso.com` etki alanı örneği CNAME kaydı adı eşler `*` için `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="3efa1-211">For the `*.contoso.com` domain example, the CNAME record will map the name `*` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="3efa1-212">CNAME eklendiğinde, DNS kayıtları sayfasında aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="3efa1-212">When the CNAME is added, the DNS records page looks like the following example:</span></span>

![Azure App portalında gezinme](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-the-cname-record-mapping-in-the-app"></a><span data-ttu-id="3efa1-214">Uygulamasında CNAME kaydı eşleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="3efa1-214">Enable the CNAME record mapping in the app</span></span>

<span data-ttu-id="3efa1-215">Uygulama için joker karakter adıyla eşleşen tüm alt etki alanı artık ekleyebilirsiniz (örneğin, `sub1.contoso.com` ve `sub2.contoso.com` eşleşen `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3efa1-215">You can now add any subdomain that matches the wildcard name to the app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="3efa1-216">Azure Portalı'nda uygulama sayfası sol gezinti bölmesinde seçin **özel etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-216">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Özel etki alanı menüsü](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="3efa1-218">Seçin  **+**  yanındaki simge **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-218">Select the **+** icon next to **Add hostname**.</span></span>

![Ana bilgisayar adı ekleyin](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="3efa1-220">Joker karakter etki alanıyla eşleşen bir tam etki alanı adı yazın (örneğin, `sub1.contoso.com`) ve ardından **doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-220">Type a fully qualified domain name that matches the wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="3efa1-221">**Ana bilgisayar adını eklemek** düğmesi etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3efa1-221">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="3efa1-222">Olduğundan emin olun **ana bilgisayar adı kayıt türü** ayarlanır **CNAME kaydı (www.example.com veya herhangi bir alt etki alanı)**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-222">Make sure that **Hostname record type** is set to **CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="3efa1-223">Seçin **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="3efa1-223">Select **Add hostname**.</span></span>

![DNS adı için uygulama ekleme](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="3efa1-225">Uygulamanın içinde yansıtılması yeni ana bilgisayar adı için biraz zaman alabilir **özel etki alanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="3efa1-225">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="3efa1-226">Verileri güncelleştirmek için tarayıcıyı yenilemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="3efa1-226">Try refreshing the browser to update the data.</span></span>

<span data-ttu-id="3efa1-227">Seçin  **+**  yeniden joker karakter etki alanıyla eşleşen başka bir ana bilgisayar adını eklemek için simge.</span><span class="sxs-lookup"><span data-stu-id="3efa1-227">Select the **+** icon again to add another hostname that matches the wildcard domain.</span></span> <span data-ttu-id="3efa1-228">Örneğin, ekleyin `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="3efa1-228">For example, add `sub2.contoso.com`.</span></span>

![CNAME kaydı eklendi](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="3efa1-230">Tarayıcıda test</span><span class="sxs-lookup"><span data-stu-id="3efa1-230">Test in browser</span></span>

<span data-ttu-id="3efa1-231">Daha önce yapılandırılmış DNS adları göz atın (örneğin, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, ve `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3efa1-231">Browse to the DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Azure App portalında gezinme](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="3efa1-233">Komut dosyalarıyla otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="3efa1-233">Automate with scripts</span></span>

<span data-ttu-id="3efa1-234">Komut dosyaları ile özel etki alanlarını yönetimini kullanarak otomatikleştirebilirsiniz [Azure CLI](/cli/azure/install-azure-cli) veya [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3efa1-234">You can automate management of custom domains with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="3efa1-235">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3efa1-235">Azure CLI</span></span> 

<span data-ttu-id="3efa1-236">Aşağıdaki komutu bir App Service uygulaması için yapılandırılmış bir özel DNS adı ekler.</span><span class="sxs-lookup"><span data-stu-id="3efa1-236">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="3efa1-237">Daha fazla bilgi için bkz: [bir web uygulaması için özel bir etki alanı eşleme](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="3efa1-237">For more information, see [Map a custom domain to a web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="3efa1-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3efa1-238">Azure PowerShell</span></span> 

<span data-ttu-id="3efa1-239">Aşağıdaki komutu bir App Service uygulaması için yapılandırılmış bir özel DNS adı ekler.</span><span class="sxs-lookup"><span data-stu-id="3efa1-239">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="3efa1-240">Daha fazla bilgi için bkz: [bir web uygulaması için özel bir etki alanı Ata](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="3efa1-240">For more information, see [Assign a custom domain to a web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3efa1-241">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3efa1-241">Next steps</span></span>

<span data-ttu-id="3efa1-242">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="3efa1-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3efa1-243">Bir alt etki alanı CNAME kaydı kullanılarak eşleme</span><span class="sxs-lookup"><span data-stu-id="3efa1-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="3efa1-244">Bir A kaydı kullanarak bir kök etki alanına Eşle</span><span class="sxs-lookup"><span data-stu-id="3efa1-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="3efa1-245">Bir CNAME kaydı kullanılarak bir joker karakter etki alanına Eşle</span><span class="sxs-lookup"><span data-stu-id="3efa1-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="3efa1-246">Etki alanı eşlemesi komut dosyaları ile otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="3efa1-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="3efa1-247">Bir web uygulaması için özel bir SSL sertifikası bağlama konusunda bilgi almak için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="3efa1-247">Advance to the next tutorial to learn how to bind a custom SSL certificate to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3efa1-248">Azure Web uygulamaları için var olan özel bir SSL sertifikası bağlama</span><span class="sxs-lookup"><span data-stu-id="3efa1-248">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)

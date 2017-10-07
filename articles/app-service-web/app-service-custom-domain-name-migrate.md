---
title: "aaaMigrate etkin bir DNS adı tooAzure App Service | Microsoft Docs"
description: "Nasıl toomigrate tooa zaten atanmış olan özel bir DNS etki alanı adı Canlı herhangi kesinti olmadan site tooAzure uygulama hizmeti hakkında bilgi edinin."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a><span data-ttu-id="a5c50-103">Etkin bir DNS adı tooAzure uygulama hizmeti geçirme</span><span class="sxs-lookup"><span data-stu-id="a5c50-103">Migrate an active DNS name tooAzure App Service</span></span>

<span data-ttu-id="a5c50-104">Bu makalede toomigrate etkin bir DNS adı çok nasıl gösterilmektedir[Azure App Service](../app-service/app-service-value-prop-what-is.md) herhangi kesinti olmadan.</span><span class="sxs-lookup"><span data-stu-id="a5c50-104">This article shows you how toomigrate an active DNS name too[Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="a5c50-105">Canlı site ve kendi DNS etki alanı adı tooApp hizmeti geçirdiğinizde, o DNS adını dinamik trafik zaten hizmet veriyor.</span><span class="sxs-lookup"><span data-stu-id="a5c50-105">When you migrate a live site and its DNS domain name tooApp Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="a5c50-106">Merhaba etkin DNS adı tooyour App Service uygulaması erken önlem bağlayarak hello geçiş sırasında kapalı kalma süresi DNS çözümlemesi ile önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5c50-106">You can avoid downtime in DNS resolution during hello migration by binding hello active DNS name tooyour App Service app preemptively.</span></span>

<span data-ttu-id="a5c50-107">Kapalı kalma süresi DNS çözümlemesi ile ilgili endişeleniyoruz değil, bkz: [bir var olan özel DNS adı tooAzure Web Apps eşleme](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="a5c50-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5c50-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a5c50-108">Prerequisites</span></span>

<span data-ttu-id="a5c50-109">toocomplete bu nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="a5c50-109">toocomplete this how-to:</span></span>

- <span data-ttu-id="a5c50-110">[Uygulama hizmeti uygulamanızı ücretsiz katmanında olmadığından emin olun](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="a5c50-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-hello-domain-name-preemptively"></a><span data-ttu-id="a5c50-111">Merhaba etki alanı adı erken önlem bağlama</span><span class="sxs-lookup"><span data-stu-id="a5c50-111">Bind hello domain name preemptively</span></span>

<span data-ttu-id="a5c50-112">Özel bir etki alanı erken önlem bağladığınızda, hem de DNS kayıtlarınızı herhangi bir değişiklik yapmadan önce hello aşağıdakileri gerçekleştirirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a5c50-112">When you bind a custom domain preemptively, you accomplish both of hello following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="a5c50-113">Etki alanı sahipliğini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a5c50-113">Verify domain ownership</span></span>
- <span data-ttu-id="a5c50-114">Merhaba etki alanı adını, uygulamanız için etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a5c50-114">Enable hello domain name for your app</span></span>

<span data-ttu-id="a5c50-115">Merhaba eski site toohello App Service uygulaması son olarak, özel DNS adı geçirdiğinizde, DNS çözümlemesi kapalı kalma süresi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a5c50-115">When you finally migrate your custom DNS name from hello old site toohello App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="a5c50-116">Etki alanı doğrulama kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a5c50-116">Create domain verification record</span></span>

<span data-ttu-id="a5c50-117">tooverify etki alanı sahipliğini Ekle bir TXT kaydı.</span><span class="sxs-lookup"><span data-stu-id="a5c50-117">tooverify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="a5c50-118">Merhaba TXT kaydı eşlemeleri _awverify.&lt; alt etki alanı >_ too_&lt;uygulamaadı >. azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="a5c50-118">hello TXT record maps from _awverify.&lt;subdomain>_ too_&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="a5c50-119">Merhaba ihtiyacınız TXT kaydı toomigrate istediğiniz DNS kaydı hello üzerinde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a5c50-119">hello TXT record you need depends on hello DNS record you want toomigrate.</span></span> <span data-ttu-id="a5c50-120">Örnekler için aşağıdaki tablonun hello bakın (`@` genellikle temsil kök etki alanı hello):</span><span class="sxs-lookup"><span data-stu-id="a5c50-120">For examples, see hello following table (`@` typically represents hello root domain):</span></span>  

| <span data-ttu-id="a5c50-121">DNS kaydı örneği</span><span class="sxs-lookup"><span data-stu-id="a5c50-121">DNS record example</span></span> | <span data-ttu-id="a5c50-122">TXT ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="a5c50-122">TXT Host</span></span> | <span data-ttu-id="a5c50-123">TXT değeri</span><span class="sxs-lookup"><span data-stu-id="a5c50-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="a5c50-124">@ (root)</span><span class="sxs-lookup"><span data-stu-id="a5c50-124">@ (root)</span></span> | <span data-ttu-id="a5c50-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="a5c50-125">_awverify_</span></span> | <span data-ttu-id="a5c50-126">_&lt;uygulamaadı >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="a5c50-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="a5c50-127">www (alt)</span><span class="sxs-lookup"><span data-stu-id="a5c50-127">www (sub)</span></span> | <span data-ttu-id="a5c50-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="a5c50-128">_awverify.www_</span></span> | <span data-ttu-id="a5c50-129">_&lt;uygulamaadı >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="a5c50-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="a5c50-130">\*(joker karakterler)</span><span class="sxs-lookup"><span data-stu-id="a5c50-130">\* (wildcard)</span></span> | <span data-ttu-id="a5c50-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="a5c50-131">_awverify.\*_</span></span> | <span data-ttu-id="a5c50-132">_&lt;uygulamaadı >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="a5c50-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="a5c50-133">DNS kayıtları sayfasında hello toomigrate istediğiniz DNS ad kayıt türü hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a5c50-133">In your DNS records page, note hello record type of hello DNS name you want toomigrate.</span></span> <span data-ttu-id="a5c50-134">Uygulama hizmeti CNAME ve A kayıtlarını eşlemelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="a5c50-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-hello-domain-for-your-app"></a><span data-ttu-id="a5c50-135">Uygulamanız için Hello etki alanı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a5c50-135">Enable hello domain for your app</span></span>

<span data-ttu-id="a5c50-136">Merhaba, [Azure portal](https://portal.azure.com), buna hello hello uygulama sayfasının sol gezinti bölmesinde, seçin **özel etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="a5c50-136">In hello [Azure portal](https://portal.azure.com), in hello left navigation of hello app page, select **Custom domains**.</span></span> 

![Özel etki alanı menüsü](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="a5c50-138">Merhaba, **özel etki alanları** sayfası, select hello  **+**  simgesi sonraki çok**ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="a5c50-138">In hello **Custom domains** page, select hello **+** icon next too**Add hostname**.</span></span>

![Ana bilgisayar adı ekleyin](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="a5c50-140">Hello tam etki alanı adını yazın, hello TXT kaydı gibi eklenen `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="a5c50-140">Type hello fully qualified domain name that you added hello TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="a5c50-141">Bir joker karakter etki alanı için (gibi \*. contoso.com), hello joker karakter etki alanıyla eşleşen herhangi bir DNS adı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5c50-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches hello wildcard domain.</span></span> 

<span data-ttu-id="a5c50-142">Seçin **doğrulamak**.</span><span class="sxs-lookup"><span data-stu-id="a5c50-142">Select **Validate**.</span></span>

<span data-ttu-id="a5c50-143">Merhaba **ana bilgisayar adını eklemek** düğmesi etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a5c50-143">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="a5c50-144">Olduğundan emin olun **ana bilgisayar adı kayıt türü** toomigrate istediğiniz toohello DNS kaydı türünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a5c50-144">Make sure that **Hostname record type** is set toohello DNS record type you want toomigrate.</span></span>

<span data-ttu-id="a5c50-145">Seçin **ana bilgisayar adını eklemek**.</span><span class="sxs-lookup"><span data-stu-id="a5c50-145">Select **Add hostname**.</span></span>

![DNS adı toohello uygulama Ekle](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="a5c50-147">Merhaba uygulamanın içinde yansıtılan hello yeni ana bilgisayar adı toobe için biraz zaman alabilir **özel etki alanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="a5c50-147">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="a5c50-148">Merhaba tarayıcı tooupdate hello verileri yenilemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="a5c50-148">Try refreshing hello browser tooupdate hello data.</span></span>

![CNAME kaydı eklendi](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="a5c50-150">Özel DNS adınızı Azure uygulamanızı şimdi etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="a5c50-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-hello-active-dns-name"></a><span data-ttu-id="a5c50-151">Merhaba active DNS adı yeniden eşleme</span><span class="sxs-lookup"><span data-stu-id="a5c50-151">Remap hello active DNS name</span></span>

<span data-ttu-id="a5c50-152">Merhaba yalnızca şey sol toodo, etkin DNS kaydı toopoint tooApp hizmeti yeniden eşleme.</span><span class="sxs-lookup"><span data-stu-id="a5c50-152">hello only thing left toodo is remapping your active DNS record toopoint tooApp Service.</span></span> <span data-ttu-id="a5c50-153">Sağ şimdi onu hala tooyour eski site işaret eder.</span><span class="sxs-lookup"><span data-stu-id="a5c50-153">Right now, it still points tooyour old site.</span></span>

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a><span data-ttu-id="a5c50-154">Merhaba uygulamanın IP adresini (yalnızca bir kayıt) kopyalayın</span><span class="sxs-lookup"><span data-stu-id="a5c50-154">Copy hello app's IP address (A record only)</span></span>

<span data-ttu-id="a5c50-155">Bir CNAME kaydı yeniden eşleme, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5c50-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="a5c50-156">tooremap bir A kaydı hello gösterilen hello uygulama hizmeti uygulamanın dış IP adresine gereksinim **özel etki alanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="a5c50-156">tooremap an A record, you need hello App Service app's external IP address, which is shown in hello **Custom domains** page.</span></span>

<span data-ttu-id="a5c50-157">Kapat hello **ana bilgisayar adını eklemek** seçerek sayfa **X** hello sağ üst köşedeki.</span><span class="sxs-lookup"><span data-stu-id="a5c50-157">Close hello **Add hostname** page by selecting **X** in hello upper-right corner.</span></span> 

<span data-ttu-id="a5c50-158">Merhaba, **özel etki alanları** sayfasında, hello uygulamanın IP adresini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a5c50-158">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a><span data-ttu-id="a5c50-160">Merhaba DNS kaydını güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="a5c50-160">Update hello DNS record</span></span>

<span data-ttu-id="a5c50-161">Geri hello DNS kayıtları sayfasında, etki alanı sağlayıcısının hello DNS kaydı tooremap seçin.</span><span class="sxs-lookup"><span data-stu-id="a5c50-161">Back in hello DNS records page of your domain provider, select hello DNS record tooremap.</span></span>

<span data-ttu-id="a5c50-162">Hello için `contoso.com` kök etki alanı örneği, aşağıdaki tablonun hello hello örneklerde gibi hello A veya CNAME kaydı yeniden eşleyin:</span><span class="sxs-lookup"><span data-stu-id="a5c50-162">For hello `contoso.com` root domain example, remap hello A or CNAME record like hello examples in hello following table:</span></span> 

| <span data-ttu-id="a5c50-163">FQDN örneği</span><span class="sxs-lookup"><span data-stu-id="a5c50-163">FQDN example</span></span> | <span data-ttu-id="a5c50-164">Kayıt türü</span><span class="sxs-lookup"><span data-stu-id="a5c50-164">Record type</span></span> | <span data-ttu-id="a5c50-165">Host</span><span class="sxs-lookup"><span data-stu-id="a5c50-165">Host</span></span> | <span data-ttu-id="a5c50-166">Değer</span><span class="sxs-lookup"><span data-stu-id="a5c50-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="a5c50-167">contoso.com (root)</span><span class="sxs-lookup"><span data-stu-id="a5c50-167">contoso.com (root)</span></span> | <span data-ttu-id="a5c50-168">A</span><span class="sxs-lookup"><span data-stu-id="a5c50-168">A</span></span> | `@` | <span data-ttu-id="a5c50-169">IP adresinden [kopyalama hello uygulamanın IP adresi](#info)</span><span class="sxs-lookup"><span data-stu-id="a5c50-169">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="a5c50-170">www.contoso.com (alt)</span><span class="sxs-lookup"><span data-stu-id="a5c50-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="a5c50-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="a5c50-171">CNAME</span></span> | `www` | <span data-ttu-id="a5c50-172">_&lt;uygulamaadı >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="a5c50-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="a5c50-173">\*. contoso.com (joker karakterler)</span><span class="sxs-lookup"><span data-stu-id="a5c50-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="a5c50-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="a5c50-174">CNAME</span></span> | _\*_ | <span data-ttu-id="a5c50-175">_&lt;uygulamaadı >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="a5c50-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="a5c50-176">Ayarlarınızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a5c50-176">Save your settings.</span></span>

<span data-ttu-id="a5c50-177">DNS sorguları hemen DNS'ye yayma işlemi gerçekleştikten sonra tooyour App Service uygulaması çözme başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5c50-177">DNS queries should start resolving tooyour App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5c50-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a5c50-178">Next steps</span></span>

<span data-ttu-id="a5c50-179">Nasıl toobind özel bir SSL sertifikası tooApp hizmeti hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="a5c50-179">Learn how toobind a custom SSL certificate tooApp Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a5c50-180">Bir var olan özel SSL sertifika tooAzure Web Apps bağlama</span><span class="sxs-lookup"><span data-stu-id="a5c50-180">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)

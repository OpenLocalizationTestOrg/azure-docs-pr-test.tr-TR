---
title: bir Azure bulut hizmeti Azure CDN ile aaaIntegrate | Microsoft Docs
description: "Nasıl bir tümleşik Azure CDN uç noktasından içerik sunan toodeploy bir bulut hizmeti öğrenin"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="1381f-103"><a name="intro"></a>Bir bulut hizmeti Azure CDN ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1381f-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="1381f-104">Bir bulut hizmeti, tüm içeriği hello bulut hizmetinin konumundan hizmet veren Azure CDN ile tümleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="1381f-104">A cloud service can be integrated with Azure CDN, serving any content from hello cloud service's location.</span></span> <span data-ttu-id="1381f-105">Bu yaklaşım, avantajları hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="1381f-105">This approach gives you hello following advantages:</span></span>

* <span data-ttu-id="1381f-106">Kolayca dağıtın ve görüntüleri, komut dosyalarını ve stil sayfalarını bulut hizmetinizin proje dizinlerde güncelleştir</span><span class="sxs-lookup"><span data-stu-id="1381f-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="1381f-107">Bulut hizmetinizde jQuery veya önyükleme sürümleri gibi hello NuGet paketlerini kolayca yükseltme</span><span class="sxs-lookup"><span data-stu-id="1381f-107">Easily upgrade hello NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="1381f-108">Web uygulamanızı yönetmek, CDN sunulan tüm hello aynı içerik ve Visual Studio arabirimi</span><span class="sxs-lookup"><span data-stu-id="1381f-108">Manage your Web application and your CDN-served content all from hello same Visual Studio interface</span></span>
* <span data-ttu-id="1381f-109">Web uygulamanız ve CDN sunulan içeriğiniz için birleşik dağıtım iş akışı</span><span class="sxs-lookup"><span data-stu-id="1381f-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="1381f-110">ASP.NET paketleme ve küçültme Azure CDN ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1381f-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1381f-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="1381f-111">What you will learn</span></span>
<span data-ttu-id="1381f-112">Bu öğreticide şunları öğreneceksiniz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="1381f-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="1381f-113">Azure CDN uç bulut hizmetiniz ile bütünleşir ve statik içerik Web sayfalarınıza Azure CDN hizmet</span><span class="sxs-lookup"><span data-stu-id="1381f-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="1381f-114">Bulut hizmetinizde statik içeriği için önbellek ayarlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1381f-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="1381f-115">Denetleyici eylemleri Azure CDN aracılığıyla içerikten hizmet</span><span class="sxs-lookup"><span data-stu-id="1381f-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="1381f-116">Hizmet vermemesini gruplanır ve Visual Studio deneyimi hello ayıklamasını korurken Azure CDN içeriğinden küçültülmüş</span><span class="sxs-lookup"><span data-stu-id="1381f-116">Serve bundled and minified content through Azure CDN while preserving hello script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="1381f-117">Azure CDN çevrimdışı olduğunda geri dönüş komut dosyaları ve CSS yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1381f-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="1381f-118">Yapı</span><span class="sxs-lookup"><span data-stu-id="1381f-118">What you will build</span></span>
<span data-ttu-id="1381f-119">Merhaba varsayılan ASP.NET MVC şablonu kullanarak bir bulut hizmeti Web rolü dağıtacağınızı, görüntü, denetleyici eylem sonuçlarını ve hello varsayılan JavaScript ve CSS dosyaları gibi tümleşik bir Azure CDN kod tooserve içerik ekleme ve ayrıca kod tooconfigure hello yazma Bu hello CDN hello olayda hizmet paketleri için geri dönüş mekanizması çevrimdışıdır.</span><span class="sxs-lookup"><span data-stu-id="1381f-119">You will deploy a cloud service Web role using hello default ASP.NET MVC template, add code tooserve content from an integrated Azure CDN, such as an image, controller action results, and hello default JavaScript and CSS files, and also write code tooconfigure hello fallback mechanism for bundles served in hello event that hello CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="1381f-120">İhtiyacınız olacak</span><span class="sxs-lookup"><span data-stu-id="1381f-120">What you will need</span></span>
<span data-ttu-id="1381f-121">Bu öğretici önkoşulları aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="1381f-121">This tutorial has hello following prerequisites:</span></span>

* <span data-ttu-id="1381f-122">Etkin bir [Microsoft Azure hesabı](/account/)</span><span class="sxs-lookup"><span data-stu-id="1381f-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="1381f-123">Visual Studio 2015 ile birlikte [Azure SDK'sı](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="1381f-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="1381f-124">Bu öğretici bir Azure hesabı toocomplete gerekir:</span><span class="sxs-lookup"><span data-stu-id="1381f-124">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="1381f-125">Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/) -krediler alırsınız tootry çıkışı Ücretli Azure hizmetlerini kullanabilirsiniz ve hatta kullanıldıktan sonra en fazla hello hesabı tutabilir ve ücretsiz Web siteleri gibi Azure hizmetlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1381f-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="1381f-126">Yapabilecekleriniz [MSDN abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -MSDN aboneliğiniz size kredi verir Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay.</span><span class="sxs-lookup"><span data-stu-id="1381f-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="1381f-127">Bir bulut hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="1381f-127">Deploy a cloud service</span></span>
<span data-ttu-id="1381f-128">Bu bölümde, hello varsayılan Visual Studio 2015 tooa bulut hizmeti Web rolünde ASP.NET MVC uygulama şablonu dağıtmak ve yeni bir CDN uç noktası ile tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="1381f-128">In this section, you will deploy hello default ASP.NET MVC application template in Visual Studio 2015 tooa cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="1381f-129">Aşağıdaki Hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="1381f-129">Follow hello instructions below:</span></span>

1. <span data-ttu-id="1381f-130">Visual Studio 2015'te, çok giderek hello menü çubuğundan yeni bir Azure bulut hizmeti oluşturma**Dosya > Yeni > Proje > bulut > Azure bulut hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="1381f-130">In Visual Studio 2015, create a new Azure cloud service from hello menu bar by going too**File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="1381f-131">Bir ad verin ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1381f-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="1381f-132">Seçin **ASP.NET Web rolü** hello tıklatıp  **>**  düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1381f-132">Select **ASP.NET Web Role** and click hello **>** button.</span></span> <span data-ttu-id="1381f-133">Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1381f-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="1381f-134">Seçin **MVC** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1381f-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="1381f-135">Şimdi, bu Web rolü tooan Azure bulut hizmeti yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="1381f-135">Now, publish this Web role tooan Azure cloud service.</span></span> <span data-ttu-id="1381f-136">Merhaba bulut hizmeti projesine sağ tıklatın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="1381f-136">Right-click hello cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="1381f-137">Henüz Microsoft Azure'da oturum değil, hello tıklatın **Hesap Ekle...**  tıklayın ve açılan hello **Hesap Ekle** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="1381f-137">If you have not yet signed into Microsoft Azure, click hello **Add an account...** dropdown and click hello **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="1381f-138">Merhaba oturum açma, hello Azure hesabınıza tooactivate kullanılan Microsoft hesabı ile oturum açma sayfası.</span><span class="sxs-lookup"><span data-stu-id="1381f-138">In hello sign-in page, sign in with hello Microsoft account you used tooactivate your Azure account.</span></span>
7. <span data-ttu-id="1381f-139">Oturum açtınız sonra tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="1381f-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="1381f-140">Bir bulut hizmeti veya depolama hesabı oluşturmadıysanız varsayılarak, Visual Studio hem de oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1381f-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="1381f-141">Merhaba, **bulut hizmeti oluşturun ve hesabı** iletişim kutusu, türü hello istenen hizmet adı ve istediğiniz bölgeyi seçin hello.</span><span class="sxs-lookup"><span data-stu-id="1381f-141">In hello **Create Cloud Service and Account** dialog, type hello desired service name and select hello desired region.</span></span> <span data-ttu-id="1381f-142">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1381f-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="1381f-143">Merhaba yayımlama Ayarları sayfası, hello yapılandırmasını doğrulayın ve tıklayın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="1381f-143">In hello publish settings page, verify hello configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="1381f-144">Bulut Hizmetleri için Hello yayımlama işlemi çok uzun sürüyor.</span><span class="sxs-lookup"><span data-stu-id="1381f-144">hello publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="1381f-145">Merhaba Web dağıtımını etkinleştirin tüm rolleri seçeneği için Web rolleri hızlı (ancak geçici) güncelleştirmeleri tooyour sağlayarak bulut hizmetiniz çok daha hızlı hata ayıklama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1381f-145">hello Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates tooyour Web roles.</span></span> <span data-ttu-id="1381f-146">Bu seçenek hakkında daha fazla bilgi için bkz: [yayımlama hello Azure araçlarını kullanarak bir bulut hizmeti](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="1381f-146">For more information on this option, see [Publishing a Cloud Service using hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="1381f-147">Ne zaman hello **Microsoft Azure etkinlik günlüğü** yayımlama durumu gösterir **tamamlandı**, bulut hizmeti ile tümleşik bir CDN uç noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1381f-147">When hello **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="1381f-148">Yayımladıktan sonra dağıtılan hello bulut hizmeti hata ekranı görüntüler, dağıttığınız hello bulut hizmeti tarafından kullanıldığından, büyük olasılıkla varsa, bir [konuk .NET 4.5.2 içermez OS](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="1381f-148">If, after publishing, hello deployed cloud service displays an error screen, it's likely because hello cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="1381f-149">Bu sorundan getirebilirler [.NET 4.5.2 bir başlangıç görevi olarak dağıtma](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1381f-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="1381f-150">Yeni bir CDN profili oluşturma</span><span class="sxs-lookup"><span data-stu-id="1381f-150">Create a new CDN profile</span></span>
<span data-ttu-id="1381f-151">CDN profili, CDN uç noktaları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="1381f-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="1381f-152">Her bir profil, bir veya daha fazla CDN uç noktası içerir.</span><span class="sxs-lookup"><span data-stu-id="1381f-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="1381f-153">Birden çok profilleri tooorganize toouse isteyebilir CDN uç noktalarınızı internet etki alanı, web uygulaması veya başka bir ölçüt.</span><span class="sxs-lookup"><span data-stu-id="1381f-153">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="1381f-154">Bu öğretici için toouse istediğiniz bir CDN profili varsa, çok devam[yeni bir CDN uç noktası oluşturma](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="1381f-154">If you already have a CDN profile that you want toouse for this tutorial, proceed too[Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="1381f-155">Yeni bir CDN uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="1381f-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="1381f-156">**toocreate depolama hesabınız için yeni bir CDN uç noktası**</span><span class="sxs-lookup"><span data-stu-id="1381f-156">**toocreate a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="1381f-157">Merhaba, [Azure Yönetim Portalı](https://portal.azure.com), tooyour CDN profili gidin.</span><span class="sxs-lookup"><span data-stu-id="1381f-157">In hello [Azure Management Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="1381f-158">Bu toohello Pano hello önceki adımda sabitlemiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1381f-158">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="1381f-159">Bunu tıklayarak bulabilirsiniz değil, varsa **Gözat**, ardından **CDN profili**, ve hello profili tıklatarak tooadd uç noktanızı planladığınız.</span><span class="sxs-lookup"><span data-stu-id="1381f-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="1381f-160">Merhaba CDN profili dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="1381f-160">hello CDN profile blade appears.</span></span>
   
    ![CDN profili][cdn-profile-settings]
2. <span data-ttu-id="1381f-162">Merhaba tıklatın **uç nokta Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1381f-162">Click hello **Add Endpoint** button.</span></span>
   
    ![Uç nokta ekle düğmesi][cdn-new-endpoint-button]
   
    <span data-ttu-id="1381f-164">Merhaba **bir uç nokta ekleyin** dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="1381f-164">hello **Add an endpoint** blade appears.</span></span>
   
    ![Uç nokta ekleme dikey penceresi][cdn-add-endpoint]
3. <span data-ttu-id="1381f-166">Bu CDN uç noktası için bir **Ad** girin.</span><span class="sxs-lookup"><span data-stu-id="1381f-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="1381f-167">Bu ad kullanılan tooaccess hello etki alanındaki önbelleğe alınmış kaynaklarınıza olacaktır `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="1381f-167">This name will be used tooaccess your cached resources at hello domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="1381f-168">Merhaba, **kaynak türü** açılan listesinde, select *bulut hizmeti*.</span><span class="sxs-lookup"><span data-stu-id="1381f-168">In hello **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="1381f-169">Merhaba, **kaynak ana bilgisayar adı** açılan listesinde, bulut hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="1381f-169">In hello **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="1381f-170">Merhaba Varsayılanları bırakabilir **kaynak yolu**, **kaynak ana bilgisayar üstbilgisi**, ve **Protokolü/kaynak bağlantı noktası**.</span><span class="sxs-lookup"><span data-stu-id="1381f-170">Leave hello defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="1381f-171">En az bir protokol (HTTP veya HTTPS) belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1381f-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="1381f-172">Merhaba tıklatın **Ekle** düğmesini toocreate hello yeni uç noktası.</span><span class="sxs-lookup"><span data-stu-id="1381f-172">Click hello **Add** button toocreate hello new endpoint.</span></span>
8. <span data-ttu-id="1381f-173">Merhaba uç nokta oluşturulduktan sonra hello profil için uç noktalar listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="1381f-173">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="1381f-174">Merhaba URL toouse tooaccess hello kaynak etki alanının yanı sıra, içeriği önbelleğe Hello liste görünümü gösterir.</span><span class="sxs-lookup"><span data-stu-id="1381f-174">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
   
    ![CDN uç noktası][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="1381f-176">Merhaba uç nokta hemen kullanılabilir olmaz.</span><span class="sxs-lookup"><span data-stu-id="1381f-176">hello endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="1381f-177">Merhaba kayıt toopropagate hello CDN ağ üzerinden too90 dakika yukarı alabilir.</span><span class="sxs-lookup"><span data-stu-id="1381f-177">It can take up too90 minutes for hello registration toopropagate through hello CDN network.</span></span> <span data-ttu-id="1381f-178">Merhaba içerik CDN hello kullanılabilir hale gelene kadar hemen toouse hello CDN etki alanı adı deneyen kullanıcılar durum kodu 404 alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1381f-178">Users who try toouse hello CDN domain name immediately may receive status code 404 until hello content is available via hello CDN.</span></span>
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="1381f-179">Test hello CDN uç noktası</span><span class="sxs-lookup"><span data-stu-id="1381f-179">Test hello CDN endpoint</span></span>
<span data-ttu-id="1381f-180">Durum yayımlama hello olduğunda **tamamlandı**, bir tarayıcı penceresi açın ve çok gidin**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="1381f-180">When hello publishing status is **Completed**, open a browser window and navigate too**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="1381f-181">My Kurulum, bu URL'yi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="1381f-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="1381f-182">Kaynak URL hello CDN uç noktada aşağıdaki toohello karşılık geldiği:</span><span class="sxs-lookup"><span data-stu-id="1381f-182">Which corresponds toohello following origin URL at hello CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="1381f-183">Ne zaman gezinmenizi çok**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, tarayıcınıza bağlı olarak, istendiğinde toodownload veya açık hello bootstrap.css olacaktır, yayımlanan Web uygulamanızdan geldi.</span><span class="sxs-lookup"><span data-stu-id="1381f-183">When you navigate too**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted toodownload or open hello bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="1381f-184">Genel olarak erişilebilir bir URL'de benzer şekilde erişebilirsiniz  **http://*&lt;serviceName >*doğrudan CDN uç noktanız gelen.cloudapp.net/**.</span><span class="sxs-lookup"><span data-stu-id="1381f-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="1381f-185">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1381f-185">For example:</span></span>

* <span data-ttu-id="1381f-186">Merhaba/Script yolundan .js dosya</span><span class="sxs-lookup"><span data-stu-id="1381f-186">A .js file from hello /Script path</span></span>
* <span data-ttu-id="1381f-187">Merhaba/Content içerik dosyanın yolu</span><span class="sxs-lookup"><span data-stu-id="1381f-187">Any content file from hello /Content path</span></span>
* <span data-ttu-id="1381f-188">Herhangi bir denetleyici/eylem</span><span class="sxs-lookup"><span data-stu-id="1381f-188">Any controller/action</span></span>
* <span data-ttu-id="1381f-189">CDN uç noktanız, sorgu dizeleri içeren herhangi bir URL'ye adresindeki Hello sorgu dizesi etkinleştirilirse</span><span class="sxs-lookup"><span data-stu-id="1381f-189">If hello query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="1381f-190">Aslında, yapılandırma yukarıda hello ile hello tüm bulut hizmetinden barındırabilir  **http://*&lt;cdnName >*.azureedge.net/**. Çok giderseniz,**http://camservice.azureedge.net/ ** alıyorum hello eylem sonucu giriş/dizinden.</span><span class="sxs-lookup"><span data-stu-id="1381f-190">In fact, with hello above configuration, you can host hello entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**. If I navigate too**http://camservice.azureedge.net/**, I get hello action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="1381f-191">Bu, ancak bu her zaman iyi bir fikir tooserve tüm bulut hizmeti Azure CDN aracılığıyla olduğunu anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="1381f-191">This does not mean, however, that it's always a good idea tooserve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="1381f-192">CDN statik teslim iyileştirme önbelleğe toobe amaçlanmamıştır veya hello CDN hello varlık yeni bir sürümü hello kaynak sunucudan çok sık çekme gerekir bu yana çok sık güncelleştirilen dinamik varlıklarını teslimat mutlaka hızlandırmak değil.</span><span class="sxs-lookup"><span data-stu-id="1381f-192">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant toobe cached, or are updated very frequently, since hello CDN must pull a new version of hello asset from hello Origin server very often.</span></span> <span data-ttu-id="1381f-193">Bu senaryo için etkinleştirmeniz [dinamik Site hızlandırma](cdn-dynamic-site-acceleration.md) çeşitli teknikleri toospeed alınabilir olmayan dinamik varlıklar teslimini kullanan CDN uç noktanız iyileştirmeyi (DSA).</span><span class="sxs-lookup"><span data-stu-id="1381f-193">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques toospeed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="1381f-194">Dinamik ve statik içeriği karışımını içeren bir siteniz varsa, tooserve CDN statik içerik (örneğin, genel web teslim) statik iyileştirme türüyle ve tooserve dinamik içerik hello kaynak sunucudan doğrudan ya da bir CDN aracılığıyla seçebilirsiniz bir olay temelinde açık DSA iyileştirme uç noktası.</span><span class="sxs-lookup"><span data-stu-id="1381f-194">If you have a site with a mix of static and dynamic content, you can choose tooserve your static content from CDN with a static optimization type (such as general web delivery), and tooserve dynamic content either directly from hello origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="1381f-195">toothat son nasıl hello CDN uç noktasından tooaccess ayrı içerik dosyaları zaten gördünüz.</span><span class="sxs-lookup"><span data-stu-id="1381f-195">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="1381f-196">I nasıl tooserve belirli denetleyici eylemi belirli bir CDN uç noktası aracılığıyla hizmet denetleyici eylemleri aracılığıyla Azure CDN içeriğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1381f-196">I will show you how tooserve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="1381f-197">Merhaba, Azure CDN gelen tooserve bulut hizmetinizde olay temelinde içerik toodetermine alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="1381f-197">hello alternative is toodetermine which content tooserve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="1381f-198">toothat son nasıl hello CDN uç noktasından tooaccess ayrı içerik dosyaları zaten gördünüz.</span><span class="sxs-lookup"><span data-stu-id="1381f-198">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="1381f-199">I size nasıl tooserve belirli denetleyici eylemi üzerinden hello CDN uç gösterir [hizmet denetleyici eylemleri Azure CDN aracılığıyla içerikten](#controller).</span><span class="sxs-lookup"><span data-stu-id="1381f-199">I will show you how tooserve a specific controller action through hello CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="1381f-200">Bulut hizmetinizde statik dosyalar için önbellek seçeneklerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1381f-200">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="1381f-201">Bulut hizmetinizde Azure CDN tümleştirme ile nasıl hello CDN uç önbelleğe statik içerik toobe istediğinizi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1381f-201">With Azure CDN integration in your cloud service, you can specify how you want static content toobe cached in hello CDN endpoint.</span></span> <span data-ttu-id="1381f-202">toodo Bu, açık *Web.config* (örneğin WebRole1), Web rolünden proje ve ekleme bir `<staticContent>` öğesi çok`<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="1381f-202">toodo this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element too`<system.webServer>`.</span></span> <span data-ttu-id="1381f-203">Merhaba XML aşağıdaki hello önbellek tooexpire 3 gün içinde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="1381f-203">hello XML below configures hello cache tooexpire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="1381f-204">Bunu yaptıktan sonra bulut hizmetindeki tüm statik dosyaları aynı CDN önbelleğiniz kural hello gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="1381f-204">Once you do this, all static files in your cloud service will observe hello same rule in your CDN cache.</span></span> <span data-ttu-id="1381f-205">Önbellek ayarları konusunda daha ayrıntılı denetim için ekleme bir *Web.config* bir klasöre dosya ve ayarlarınızı var. ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1381f-205">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="1381f-206">Örneğin, bir *Web.config* toohello dosya *\Content* klasörü ve Değiştir XML aşağıdaki hello ile içerik hello:</span><span class="sxs-lookup"><span data-stu-id="1381f-206">For example, add a *Web.config* file toohello *\Content* folder and replace hello content with hello following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="1381f-207">Bu ayarı tüm statik dosyaları hello neden *\Content* 15 gün boyunca önbelleğe alınan klasörü toobe.</span><span class="sxs-lookup"><span data-stu-id="1381f-207">This setting causes all static files from hello *\Content* folder toobe cached for 15 days.</span></span>

<span data-ttu-id="1381f-208">Hakkında daha fazla bilgi için tooconfigure hello `<clientCache>` öğesi, bkz: [istemci önbelleği &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="1381f-208">For more information on how tooconfigure hello `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="1381f-209">İçinde [hizmet denetleyici eylemleri Azure CDN aracılığıyla içerikten](#controller), ı de hello CDN önbellek denetleyici eylem sonuçlarını için önbellek ayarlarını nasıl yapılandıracağınızı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1381f-209">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in hello CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="1381f-210">Denetleyici eylemleri Azure CDN aracılığıyla içerikten hizmet</span><span class="sxs-lookup"><span data-stu-id="1381f-210">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="1381f-211">Bulut hizmeti Web rolü Azure CDN ile tümleştirmek denetleyici eylemleri hello Azure CDN aracılığıyla görece kolay tooserve içerikten olur.</span><span class="sxs-lookup"><span data-stu-id="1381f-211">When you integrate a cloud service Web role with Azure CDN, it is relatively easy tooserve content from controller actions through hello Azure CDN.</span></span> <span data-ttu-id="1381f-212">Bulut hizmet veren dışında doğrudan Azure (yukarıda gösterilen), CDN hizmet [Maarten Balliauw](https://twitter.com/maartenballiauw) nasıl gösterir toodo eğlenceli bir kendisiyle MemeGenerator denetleyicisi [hello Azure CDN ile Merhaba Web'de gecikmesini azaltır ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="1381f-212">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how toodo it with a fun MemeGenerator controller in [Reducing latency on hello web with hello Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="1381f-213">I yalnızca onu buraya yeniden.</span><span class="sxs-lookup"><span data-stu-id="1381f-213">I will simply reproduce it here.</span></span>

<span data-ttu-id="1381f-214">Bulut hizmetinizde Küçük yaştaki ALi Norris görüntüyü temel alarak toogenerate memes istediğinizi düşünelim (tarafından fotoğraf [Alan ışık](http://www.flickr.com/photos/alan-light/218493788/)) şöyle:</span><span class="sxs-lookup"><span data-stu-id="1381f-214">Suppose in your cloud service you want toogenerate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="1381f-215">Basit bir sahip `Index` hello müşterilerin toospecify hello derecelerinin hello görüntüde sağlayan eylem toohello eylem sonrası sonra hello meme sonra oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1381f-215">You have a simple `Index` action that allows hello customers toospecify hello superlatives in hello image, then generates hello meme once they post toohello action.</span></span> <span data-ttu-id="1381f-216">ALi Norris olduğundan, bu sayfa toobecome müthiş bir başarı popüler genel beklediğiniz.</span><span class="sxs-lookup"><span data-stu-id="1381f-216">Since it's Chuck Norris, you would expect this page toobecome wildly popular globally.</span></span> <span data-ttu-id="1381f-217">Bu, yarı dinamik içerik Azure CDN ile hizmet veren, iyi bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="1381f-217">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="1381f-218">Bu denetleyici eylemi toosetup yukarıdaki Hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="1381f-218">Follow hello steps above toosetup this controller action:</span></span>

1. <span data-ttu-id="1381f-219">Merhaba, *\Controllers* klasör adında yeni bir .cs dosyası oluşturmak *MemeGeneratorController.cs* ve Değiştir hello hello ile içerik aşağıdaki kodu.</span><span class="sxs-lookup"><span data-stu-id="1381f-219">In hello *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace hello content with hello following code.</span></span> <span data-ttu-id="1381f-220">CDN adıyla emin tooreplace hello vurgulanan bölümü olabilir.</span><span class="sxs-lookup"><span data-stu-id="1381f-220">Be sure tooreplace hello highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="1381f-221">Merhaba varsayılan olarak sağ `Index()` eylem ve select **Görünüm Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1381f-221">Right-click in hello default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="1381f-222">Aşağıdaki Hello ayarlarını kabul edin ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1381f-222">Accept hello settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="1381f-223">Açık hello yeni *Views\MemeGenerator\Index.cshtml* ve basit HTML hello derecelerinin göndermek için aşağıdaki hello hello içerik değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1381f-223">Open hello new *Views\MemeGenerator\Index.cshtml* and replace hello content with hello following simple HTML for submitting hello superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="1381f-224">Merhaba bulut hizmeti yeniden yayımlamanız ve çok gidin**http://*&lt;serviceName >*tarayıcınızda.cloudapp.net/MemeGenerator/Index**.</span><span class="sxs-lookup"><span data-stu-id="1381f-224">Publish hello cloud service again and navigate too**http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="1381f-225">Ne zaman gönderdiğiniz hello form değerleri çok`/MemeGenerator/Index`, hello `Index_Post` eylem yöntemine döndürür bağlantı toohello `Show` eylem yöntemi, hello ilgili giriş tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="1381f-225">When you submit hello form values too`/MemeGenerator/Index`, hello `Index_Post` action method returns a link toohello `Show` action method with hello respective input identifier.</span></span> <span data-ttu-id="1381f-226">Merhaba bağlantısını tıklattığınızda koddan hello ulaşmak:</span><span class="sxs-lookup"><span data-stu-id="1381f-226">When you click hello link, you reach hello following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="1381f-227">Ardından, yerel hata ayıklayıcısı ekli, yerel bir yeniden yönlendirme ile Merhaba normal hata ayıklama deneyimini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="1381f-227">If your local debugger is attached, then you will get hello regular debug experience with a local redirect.</span></span> <span data-ttu-id="1381f-228">Merhaba bulut Hizmeti çalışıyorsa, için yönlendirir:</span><span class="sxs-lookup"><span data-stu-id="1381f-228">If it's running in hello cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="1381f-229">CDN uç noktanız kaynak URL'de aşağıdaki toohello karşılık geldiği:</span><span class="sxs-lookup"><span data-stu-id="1381f-229">Which corresponds toohello following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="1381f-230">Merhaba sonra kullanabileceğiniz `OutputCacheAttribute` hello öznitelikte `Generate` nasıl hello eylem sonucu, önbelleğe, Azure CDN dokunmaz yöntemi toospecify.</span><span class="sxs-lookup"><span data-stu-id="1381f-230">You can then use hello `OutputCacheAttribute` attribute on hello `Generate` method toospecify how hello action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="1381f-231">Aşağıdaki Hello kodu Önbellek süre sonu 1 saatlik (3.600 saniye) belirtin.</span><span class="sxs-lookup"><span data-stu-id="1381f-231">hello code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="1381f-232">Benzer şekilde, size herhangi bir denetleyici eylem içerikten yukarı bulut hizmetiniz istenen hello önbelleğe alma seçeneği ile Azure CDN aracılığıyla hizmet verebilir.</span><span class="sxs-lookup"><span data-stu-id="1381f-232">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with hello desired caching option.</span></span>

<span data-ttu-id="1381f-233">Merhaba sonraki bölümde, ı size nasıl tooserve hello toplanmış ve komut dosyaları ve CSS Azure CDN aracılığıyla küçültülmüş gösterir.</span><span class="sxs-lookup"><span data-stu-id="1381f-233">In hello next section, I will show you how tooserve hello bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="1381f-234">ASP.NET paketleme ve küçültme Azure CDN ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1381f-234">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="1381f-235">Komut dosyaları ve CSS stil sayfaları, seyrek değiştirin ve hello Azure CDN önbellek prime adaylar.</span><span class="sxs-lookup"><span data-stu-id="1381f-235">Scripts and CSS stylesheets change infrequently and are prime candidates for hello Azure CDN cache.</span></span> <span data-ttu-id="1381f-236">Hizmet hello Azure CDN ile tüm Web rolü olan hello en kolay yolu toointegrate paketleme ve küçültme Azure CDN ile.</span><span class="sxs-lookup"><span data-stu-id="1381f-236">Serving hello entire Web role through your Azure CDN is hello easiest way toointegrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="1381f-237">Toodo bu isteyebilirsiniz, ancak, t, nasıl toodo hello korurken, ASP.NET paketleme ve küçültme, develper deneyimi gibi istenen gösterecektir:</span><span class="sxs-lookup"><span data-stu-id="1381f-237">However, as you may not want toodo this, I will show you how toodo it while preserving hello desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="1381f-238">Harika hata ayıklama modu deneyimi</span><span class="sxs-lookup"><span data-stu-id="1381f-238">Great debug mode experience</span></span>
* <span data-ttu-id="1381f-239">Basitleştirilmiş Dağıtım</span><span class="sxs-lookup"><span data-stu-id="1381f-239">Streamlined deployment</span></span>
* <span data-ttu-id="1381f-240">Komut dosyası/CSS sürüm yükseltme için hemen güncelleştirmeleri tooclients</span><span class="sxs-lookup"><span data-stu-id="1381f-240">Immediate updates tooclients for script/CSS version upgrades</span></span>
* <span data-ttu-id="1381f-241">CDN uç noktanız başarısız olduğunda bir geri dönüş mekanizması</span><span class="sxs-lookup"><span data-stu-id="1381f-241">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="1381f-242">Kod değişikliği simge durumuna küçült</span><span class="sxs-lookup"><span data-stu-id="1381f-242">Minimize code modification</span></span>

<span data-ttu-id="1381f-243">Merhaba, **WebRole1** oluşturduğunuz proje [Azure CDN uç Azure Web sitesi ile bütünleşir ve Azure CDN Web sayfalarınıza statik içerik sunmanızı](#deploy), açık *App_Start\ BundleConfig.cs* ve hello bakalım `bundles.Add()` yöntem çağrıları.</span><span class="sxs-lookup"><span data-stu-id="1381f-243">In hello **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at hello `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="1381f-244">ilk hello `bundles.Add()` deyimi hello sanal dizininde betik paket ekler `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="1381f-244">hello first `bundles.Add()` statement adds a script bundle at hello virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="1381f-245">Ardından, açın *görünümler/paylaşılan\_Layout.cshtml* toosee hello paket etiketi nasıl işlenir.</span><span class="sxs-lookup"><span data-stu-id="1381f-245">Then, open *Views\Shared\_Layout.cshtml* toosee how hello script bundle tag is rendered.</span></span> <span data-ttu-id="1381f-246">Razor kod satırı aşağıdaki mümkün toofind hello olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="1381f-246">You should be able toofind hello following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="1381f-247">Bu Razor kod hello Azure Web rolünde çalıştırdığınızda kılacak bir `<script>` etiketi hello için paket benzer toohello aşağıdaki komut dosyası:</span><span class="sxs-lookup"><span data-stu-id="1381f-247">When this Razor code is run in hello Azure Web role, it will render a `<script>` tag for hello script bundle similar toohello following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="1381f-248">Ancak, çalıştırıldığında Visual Studio'da yazarak `F5`, her komut dosyası hello paketteki tek tek kılacak (Merhaba yukarıdaki, yalnızca bir komut dosyası hello pakette bir durumdur):</span><span class="sxs-lookup"><span data-stu-id="1381f-248">However, when it is run in Visual Studio by typing `F5`, it will render each script file in hello bundle individually (in hello case above, only one script file is in hello bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="1381f-249">Eşzamanlı istemci bağlantıları (paketleme) azaltma ve dosya geliştirme performans (küçültme) üretimde karşıdan yüklerken bu, geliştirme ortamınızı toodebug hello JavaScript kodu sağlar.</span><span class="sxs-lookup"><span data-stu-id="1381f-249">This enables you toodebug hello JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="1381f-250">Azure CDN Tümleştirmesi ile bir önemli özellik toopreserve olur.</span><span class="sxs-lookup"><span data-stu-id="1381f-250">It's a great feature toopreserve with Azure CDN integration.</span></span> <span data-ttu-id="1381f-251">Ayrıca, işlenen hello paket zaten bir otomatik olarak oluşturulan sürüm dizesi içerdiğinden işlevselliği şekilde hello jQuery sürümünüz, NuGet aracılığıyla güncelleştirdiğinizde tooreplicate istediğiniz hello istemci tarafında güncelleştirilebilir hemen olası.</span><span class="sxs-lookup"><span data-stu-id="1381f-251">Furthermore, since hello rendered bundle already contains an automatically generated version string, you want tooreplicate that functionality so hello whenever you update your jQuery version through NuGet, it can be updated at hello client side as soon as possible.</span></span>

<span data-ttu-id="1381f-252">ASP.NET toointegration paketleme ve küçültme CDN uç noktanız ile Merhaba adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="1381f-252">Follow hello steps below toointegration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="1381f-253">Geri *App_Start\BundleConfig.cs*, hello değiştirme `bundles.Add()` yöntemleri toouse farklı bir [paket Oluşturucusu](http://msdn.microsoft.com/library/jj646464.aspx), bir CDN adresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1381f-253">Back in *App_Start\BundleConfig.cs*, modify hello `bundles.Add()` methods toouse a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="1381f-254">toodo Bu, Değiştir hello `RegisterBundles` koddan hello yöntemi tanımıyla:</span><span class="sxs-lookup"><span data-stu-id="1381f-254">toodo this, replace hello `RegisterBundles` method definition with hello following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="1381f-255">Emin tooreplace olması `<yourCDNName>` Azure CDN hello adı.</span><span class="sxs-lookup"><span data-stu-id="1381f-255">Be sure tooreplace `<yourCDNName>` with hello name of your Azure CDN.</span></span>
   
    <span data-ttu-id="1381f-256">Düz metin olarak ayarladığınız `bundles.UseCdn = true` ve dikkatli bir şekilde hazırlanmış bir CDN URL'sine tooeach paket eklenir.</span><span class="sxs-lookup"><span data-stu-id="1381f-256">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL tooeach bundle.</span></span> <span data-ttu-id="1381f-257">Örneğin, hello ilk oluşturucuda hello kod:</span><span class="sxs-lookup"><span data-stu-id="1381f-257">For example, hello first constructor in hello code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="1381f-258">olan hello aynıdır:</span><span class="sxs-lookup"><span data-stu-id="1381f-258">is hello same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="1381f-259">Bu oluşturucu ASP.NET paketleme ve küçültme hata ayıklaması sırasında toorender ayrı komut dosyaları yerel olarak bildirir ancak kullanım hello CDN adresi tooaccess hello betik söz konusu belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="1381f-259">This constructor tells ASP.NET bundling and minification toorender individual script files when debugged locally, but use hello specified CDN address tooaccess hello script in question.</span></span> <span data-ttu-id="1381f-260">Ancak, bu dikkatle hazırlanmış CDN URL ile iki önemli özelliklere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="1381f-260">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="1381f-261">Bu CDN URL'sine Hello kaynağı `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, aslında hello sanal dizin hello betik paketin bulut hizmetinizde olduğu.</span><span class="sxs-lookup"><span data-stu-id="1381f-261">hello origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually hello virtual directory of hello script bundle in your cloud service.</span></span>
   * <span data-ttu-id="1381f-262">CDN Oluşturucusu kullandığından hello hello paket için CDN komut dosyası etiketinin artık otomatik olarak oluşturulan hello sürüm dizesi URL çizilir hello içinde içerir.</span><span class="sxs-lookup"><span data-stu-id="1381f-262">Since you are using CDN constructor, hello CDN script tag for hello bundle no longer contains hello automatically generated version string in hello rendered URL.</span></span> <span data-ttu-id="1381f-263">Merhaba betik paket bir önbellek, Azure CDN kaçırılması değiştirilmiş tooforce her kullanılışında benzersiz sürüm dizesi el ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1381f-263">You must manually generate a unique version string every time hello script bundle is modified tooforce a cache miss at your Azure CDN.</span></span> <span data-ttu-id="1381f-264">AT hello aynı zaman, bu benzersiz sürüm dizesi devam etmelidir hello dağıtım toomaximize İsabetli Önbellek okuma sayısının Azure CDN adresindeki hello ömrü boyunca sabit hello paket dağıtıldıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="1381f-264">At hello same time, this unique version string must remain constant through hello life of hello deployment toomaximize cache hits at your Azure CDN after hello bundle is deployed.</span></span>
   * <span data-ttu-id="1381f-265">Sorgu dizesi v merhaba < W.X.Y.Z > çeken gelen = *Properties\AssemblyInfo.cs* Web rolü projenizdeki.</span><span class="sxs-lookup"><span data-stu-id="1381f-265">hello query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="1381f-266">TooAzure her yayımladığınızda hello derleme sürümü artırma içeren bir dağıtım iş akışı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1381f-266">You can have a deployment workflow that includes incrementing hello assembly version every time you publish tooAzure.</span></span> <span data-ttu-id="1381f-267">Veya yalnızca değiştirebileceğiniz *Properties\AssemblyInfo.cs* , oluşturduğunuz her zaman, proje tooautomatically artırma hello sürüm dizesi hello joker karakter kullanarak ' *'.</span><span class="sxs-lookup"><span data-stu-id="1381f-267">Or, you can just modify *Properties\AssemblyInfo.cs* in your project tooautomatically increment hello version string every time you build, using hello wildcard character '*'.</span></span> <span data-ttu-id="1381f-268">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1381f-268">For example:</span></span>
     
        <span data-ttu-id="1381f-269">[derleme: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="1381f-269">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="1381f-270">Merhaba ömrü dağıtımı için benzersiz bir dize oluşturma diğer strateji toostreamline burada çalışır.</span><span class="sxs-lookup"><span data-stu-id="1381f-270">Any other strategy toostreamline generating a unique string for hello life of a deployment will work here.</span></span>
2. <span data-ttu-id="1381f-271">Merhaba bulut hizmeti ve erişim hello giriş sayfasına yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="1381f-271">Republish hello cloud service and access hello home page.</span></span>
3. <span data-ttu-id="1381f-272">Görünüm hello hello sayfasının HTML kodunu.</span><span class="sxs-lookup"><span data-stu-id="1381f-272">View hello HTML code for hello page.</span></span> <span data-ttu-id="1381f-273">Mümkün toosee hello CDN, değişiklikleri tooyour bulut hizmeti yeniden yayımlamanız her zaman bir benzersiz sürüm dizesi ile işlenen URL olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1381f-273">You should be able toosee hello CDN URL rendered, with a unique version string every time you republish changes tooyour cloud service.</span></span> <span data-ttu-id="1381f-274">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1381f-274">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="1381f-275">Visual Studio'da yazarak hello bulut hizmeti Visual Studio'da hata ayıklama `F5`.,</span><span class="sxs-lookup"><span data-stu-id="1381f-275">In Visual Studio, debug hello cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="1381f-276">Görünüm hello hello sayfasının HTML kodunu.</span><span class="sxs-lookup"><span data-stu-id="1381f-276">View hello HTML code for hello page.</span></span> <span data-ttu-id="1381f-277">Böylece Visual Studio'da deneyimi tutarlı bir hata ayıklama sahip tek tek işlenen her komut dosyası hala görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1381f-277">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="1381f-278">CDN URL'ler için geri dönüş mekanizması</span><span class="sxs-lookup"><span data-stu-id="1381f-278">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="1381f-279">Azure CDN uç noktanız için herhangi bir nedenle başarısız olduğunda, Web sayfası toobe hello JavaScript veya önyükleme yüklenmesi için geri dönüş seçeneği olarak, kaynak Web sunucunuzun yeterli tooaccess akıllı istiyor.</span><span class="sxs-lookup"><span data-stu-id="1381f-279">When your Azure CDN endpoint fails for any reason, you want your Web page toobe smart enough tooaccess your origin Web server as hello fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="1381f-280">Web sitenizi tooCDN kullanılamazlık ancak komut dosyalarını ve stil sayfalarını tarafından sağlanan çok daha ağır toolose önemli sayfa işlevselliği nedeniyle yeterince önemli toolose görüntülerinde olur.</span><span class="sxs-lookup"><span data-stu-id="1381f-280">It's serious enough toolose images on your website due tooCDN unavailability, but much more severe toolose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="1381f-281">Merhaba [paket](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) sınıfı adlı bir özellik içerir [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) , CDN hatası tooconfigure hello geri dönüş mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="1381f-281">hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you tooconfigure hello fallback mechanism for CDN failure.</span></span> <span data-ttu-id="1381f-282">toouse bu özellik, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="1381f-282">toouse this property, follow hello steps below:</span></span>

1. <span data-ttu-id="1381f-283">Web rolü projesinde açmak *App_Start\BundleConfig.cs*, CDN URL'sine her eklediğiniz [paket Oluşturucusu](http://msdn.microsoft.com/library/jj646464.aspx)ve vurgulanmış hello aşağıdaki tooadd geri dönüş mekanizması toohello değiştirir Varsayılan paket:</span><span class="sxs-lookup"><span data-stu-id="1381f-283">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make hello following highlighted changes tooadd fallback mechanism toohello default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="1381f-284">Zaman `CdnFallbackExpression` olan hello paket başarıyla yüklendi olup olmadığını null, komut dosyası hello HTML tootest eklenmiş ve aksi durumda, doğrudan hello kaynak Web sunucusundan hello paket erişim.</span><span class="sxs-lookup"><span data-stu-id="1381f-284">When `CdnFallbackExpression` is not null, script is injected into hello HTML tootest whether hello bundle is loaded successfully and, if not, access hello bundle directly from hello origin Web server.</span></span> <span data-ttu-id="1381f-285">Bu özellik hello ilgili CDN paket düzgün şekilde yüklenmesini olup olmadığını sınar toobe kümesi tooa JavaScript ifadesi olması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="1381f-285">This property needs toobe set tooa JavaScript expression that tests whether hello respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="1381f-286">Merhaba ifade gerekli tootest according toohello içerik her paket farklıdır.</span><span class="sxs-lookup"><span data-stu-id="1381f-286">hello expression needed tootest each bundle differs according toohello content.</span></span> <span data-ttu-id="1381f-287">Merhaba varsayılan paketleri için yukarıdaki:</span><span class="sxs-lookup"><span data-stu-id="1381f-287">For hello default bundles above:</span></span>
   
   * <span data-ttu-id="1381f-288">`window.jquery`JQuery-{version} .js tanımlanır</span><span class="sxs-lookup"><span data-stu-id="1381f-288">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="1381f-289">`$.validator`JQuery.Validate.js tanımlanır</span><span class="sxs-lookup"><span data-stu-id="1381f-289">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="1381f-290">`window.Modernizr`modernizer gibi-{version} .js tanımlanır</span><span class="sxs-lookup"><span data-stu-id="1381f-290">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="1381f-291">`$.fn.modal`Bootstrap.js tanımlanır</span><span class="sxs-lookup"><span data-stu-id="1381f-291">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="1381f-292">I CdnFallbackExpression Merhaba ayarlamamış olduğunu fark etmiş olabilirsiniz `~/Cointent/css` paket.</span><span class="sxs-lookup"><span data-stu-id="1381f-292">You might have noticed that I did not set CdnFallbackExpression for hello `~/Cointent/css` bundle.</span></span> <span data-ttu-id="1381f-293">Şu anda bu olmadığından bir [System.Web.Optimization hatada](https://aspnetoptimization.codeplex.com/workitem/104) , yerleştirir bir `<script>` hello yerine geri dönüş CSS beklenen hello için etiket `<link>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="1381f-293">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for hello fallback CSS instead of hello expected `<link>` tag.</span></span>
     
     <span data-ttu-id="1381f-294">Yoktur, ancak iyi bir [stili paket geri dönüş](https://github.com/EmberConsultingGroup/StyleBundleFallback) tarafından sunulan [Ember danışmanlık grup](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="1381f-294">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="1381f-295">CSS için toouse hello geçici çözüm, Web rolü projenizin içinde yeni bir .cs dosyası oluşturma *App_Start* adlı bir klasör *StyleBundleExtensions.cs*ve ile Merhaba içeriğine Değiştir [gelen kod GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="1381f-295">toouse hello workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with hello [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="1381f-296">İçinde *App_Start\StyleFundleExtensions.cs*, başlangıç ad alanı tooyour Web rolün yeniden adlandırın (örneğin **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="1381f-296">In *App_Start\StyleFundleExtensions.cs*, rename hello namespace tooyour Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="1381f-297">Çok dön`App_Start\BundleConfig.cs` ve hello son değiştirme `bundles.Add` vurgulanmış kodu aşağıdaki hello deyimiyle:</span><span class="sxs-lookup"><span data-stu-id="1381f-297">Go back too`App_Start\BundleConfig.cs` and modify hello last `bundles.Add` statement with hello following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="1381f-298">Bu yeni genişletme yöntemi hello kullanan aynı fikir tooinject komut hello HTML toocheck hello DOM hello için içinde eşleşen sınıf adı, kural adı ve hello CSS paket ve toofind hello eşleşme başarısız olursa döner geri toohello kaynağı Web sunucusu tanımlanmış kural değer.</span><span class="sxs-lookup"><span data-stu-id="1381f-298">This new extension method uses hello same idea tooinject script in hello HTML toocheck hello DOM for hello a matching class name, rule name, and rule value defined in hello CSS bundle, and falls back toohello origin Web server if it fails toofind hello match.</span></span>
5. <span data-ttu-id="1381f-299">Yeniden Hello bulut hizmeti ve erişim hello giriş sayfası yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="1381f-299">Publish hello cloud service again and access hello home page.</span></span>
6. <span data-ttu-id="1381f-300">Görünüm hello hello sayfasının HTML kodunu.</span><span class="sxs-lookup"><span data-stu-id="1381f-300">View hello HTML code for hello page.</span></span> <span data-ttu-id="1381f-301">Eklenen komut dosyaları benzer toohello aşağıdaki bulmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1381f-301">You should find injected scripts similar toohello following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="1381f-302">Merhaba CSS paket için eklenen komut hello gelen hello yalıtılarak işlemi hala içerdiğine dikkat edin `CdnFallbackExpression` hello satır özelliğinde:</span><span class="sxs-lookup"><span data-stu-id="1381f-302">Note that injected script for hello CSS bundle still contains hello errant remnant from hello `CdnFallbackExpression` property in hello line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="1381f-303">Ancak hello ilk kısmı hello itibaren || ifade her zaman true (doğrudan yukarıdaki hello satırdaki) döndürür ve hello document.write() işlevi asla çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="1381f-303">But since hello first part of hello || expression will always return true (in hello line directly above that), hello document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="1381f-304">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="1381f-304">More Information</span></span>
* [<span data-ttu-id="1381f-305">Hello Azure içerik teslim ağı (CDN) genel bakış</span><span class="sxs-lookup"><span data-stu-id="1381f-305">Overview of hello Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="1381f-306">Azure CDN'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="1381f-306">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="1381f-307">ASP.NET paketleme ve küçültme</span><span class="sxs-lookup"><span data-stu-id="1381f-307">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png

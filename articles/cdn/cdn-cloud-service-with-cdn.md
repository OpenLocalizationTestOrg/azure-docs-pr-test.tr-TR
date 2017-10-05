---
title: "Bir Azure bulut hizmeti Azure CDN ile tümleştirmek | Microsoft Docs"
description: "Tümleşik bir Azure CDN uç noktasından içerik sunan bir bulut hizmeti dağıtmayı öğrenin"
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
ms.openlocfilehash: f2849fe25fd0d5b3dc26598ffba7591cb7433161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="bd2d9-103"><a name="intro"></a>Bir bulut hizmeti Azure CDN ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="bd2d9-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="bd2d9-104">Bir bulut hizmeti, bulut hizmetinin konumundan içerik sunan Azure CDN ile tümleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-104">A cloud service can be integrated with Azure CDN, serving any content from the cloud service's location.</span></span> <span data-ttu-id="bd2d9-105">Bu yaklaşım, aşağıdaki avantajları sunar:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-105">This approach gives you the following advantages:</span></span>

* <span data-ttu-id="bd2d9-106">Kolayca dağıtın ve görüntüleri, komut dosyalarını ve stil sayfalarını bulut hizmetinizin proje dizinlerde güncelleştir</span><span class="sxs-lookup"><span data-stu-id="bd2d9-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="bd2d9-107">JQuery veya önyükleme sürümleri gibi bulut hizmetinizde NuGet paketlerini kolayca yükseltme</span><span class="sxs-lookup"><span data-stu-id="bd2d9-107">Easily upgrade the NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="bd2d9-108">Web uygulamanız ve, CDN sunulan içerik tümü aynı Visual Studio arabiriminden yönetmek</span><span class="sxs-lookup"><span data-stu-id="bd2d9-108">Manage your Web application and your CDN-served content all from the same Visual Studio interface</span></span>
* <span data-ttu-id="bd2d9-109">Web uygulamanız ve CDN sunulan içeriğiniz için birleşik dağıtım iş akışı</span><span class="sxs-lookup"><span data-stu-id="bd2d9-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="bd2d9-110">ASP.NET paketleme ve küçültme Azure CDN ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="bd2d9-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bd2d9-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="bd2d9-111">What you will learn</span></span>
<span data-ttu-id="bd2d9-112">Bu öğreticide şunları öğreneceksiniz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="bd2d9-113">Azure CDN uç bulut hizmetiniz ile bütünleşir ve statik içerik Web sayfalarınıza Azure CDN hizmet</span><span class="sxs-lookup"><span data-stu-id="bd2d9-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="bd2d9-114">Bulut hizmetinizde statik içeriği için önbellek ayarlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bd2d9-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="bd2d9-115">Denetleyici eylemleri Azure CDN aracılığıyla içerikten hizmet</span><span class="sxs-lookup"><span data-stu-id="bd2d9-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="bd2d9-116">Hizmet vermemesini gruplanır ve Visual Studio deneyimi ayıklamasını korurken Azure CDN içeriğinden küçültülmüş</span><span class="sxs-lookup"><span data-stu-id="bd2d9-116">Serve bundled and minified content through Azure CDN while preserving the script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="bd2d9-117">Azure CDN çevrimdışı olduğunda geri dönüş komut dosyaları ve CSS yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="bd2d9-118">Yapı</span><span class="sxs-lookup"><span data-stu-id="bd2d9-118">What you will build</span></span>
<span data-ttu-id="bd2d9-119">Varsayılan ASP.NET MVC şablonu kullanarak bir bulut hizmeti Web rolü dağıtacağınızı, görüntü, denetleyici eylem sonuçlarını ve varsayılan JavaScript ve CSS dosyaları gibi tümleşik bir Azure CDN gelen içerik sunmak için kodu ekleyin ve ayrıca geri dönüş yapılandırmak için kod yazma CDN çevrimdışıysa gerektiğinde, paket için mekanizma sundu.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-119">You will deploy a cloud service Web role using the default ASP.NET MVC template, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="bd2d9-120">İhtiyacınız olacak</span><span class="sxs-lookup"><span data-stu-id="bd2d9-120">What you will need</span></span>
<span data-ttu-id="bd2d9-121">Bu öğretici aşağıdaki önkoşullar vardır:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-121">This tutorial has the following prerequisites:</span></span>

* <span data-ttu-id="bd2d9-122">Etkin bir [Microsoft Azure hesabı](/account/)</span><span class="sxs-lookup"><span data-stu-id="bd2d9-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="bd2d9-123">Visual Studio 2015 ile birlikte [Azure SDK'sı](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="bd2d9-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="bd2d9-124">Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-124">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="bd2d9-125">Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/) -krediler alırsınız, ücretli Azure hizmetlerini denemek için kullanabileceğiniz ve hatta kullanıldıktan sonra en fazla hesabı tutabilir ve ücretsiz Web siteleri gibi Azure hizmetlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="bd2d9-126">Yapabilecekleriniz [MSDN abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -MSDN aboneliğiniz size kredi verir Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="bd2d9-127">Bir bulut hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="bd2d9-127">Deploy a cloud service</span></span>
<span data-ttu-id="bd2d9-128">Bu bölümde, bir bulut hizmeti Web rolü için varsayılan ASP.NET MVC uygulama şablonu Visual Studio 2015'te dağıtın ve yeni bir CDN uç noktası ile tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-128">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to a cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="bd2d9-129">Aşağıdaki yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-129">Follow the instructions below:</span></span>

1. <span data-ttu-id="bd2d9-130">Visual Studio 2015'te, giderek menü çubuğundan yeni bir Azure bulut hizmeti oluşturma **Dosya > Yeni > Proje > bulut > Azure bulut hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-130">In Visual Studio 2015, create a new Azure cloud service from the menu bar by going to **File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="bd2d9-131">Bir ad verin ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="bd2d9-132">Seçin **ASP.NET Web rolü** tıklatıp  **>**  düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-132">Select **ASP.NET Web Role** and click the **>** button.</span></span> <span data-ttu-id="bd2d9-133">Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="bd2d9-134">Seçin **MVC** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="bd2d9-135">Şimdi, bu Web rolü için bir Azure bulut hizmeti yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-135">Now, publish this Web role to an Azure cloud service.</span></span> <span data-ttu-id="bd2d9-136">Bulut hizmeti projesine sağ tıklatın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-136">Right-click the cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="bd2d9-137">Henüz Microsoft Azure'da oturum değil,'ı tıklatın **Hesap Ekle...**  açılır tıklatıp **Hesap Ekle** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-137">If you have not yet signed into Microsoft Azure, click the **Add an account...** dropdown and click the **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="bd2d9-138">Oturum açma sayfası Azure hesabınızı etkinleştirmek için kullanılan Microsoft hesabıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-138">In the sign-in page, sign in with the Microsoft account you used to activate your Azure account.</span></span>
7. <span data-ttu-id="bd2d9-139">Oturum açtınız sonra tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="bd2d9-140">Bir bulut hizmeti veya depolama hesabı oluşturmadıysanız varsayılarak, Visual Studio hem de oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="bd2d9-141">İçinde **bulut hizmeti oluşturun ve hesabı** iletişim kutusunda, istenen hizmet adını yazın ve istediğiniz bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-141">In the **Create Cloud Service and Account** dialog, type the desired service name and select the desired region.</span></span> <span data-ttu-id="bd2d9-142">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="bd2d9-143">Yayımlama Ayarları sayfasında yapılandırmasını doğrulayın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-143">In the publish settings page, verify the configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="bd2d9-144">Bulut Hizmetleri için yayımlama işlemi çok uzun sürüyor.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-144">The publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="bd2d9-145">Web dağıtımını etkinleştirin tüm rolleri seçeneği için Web rolleri (ancak geçici) hızlı güncelleştirmeleri sağlayarak bulut hizmetiniz çok daha hızlı hata ayıklama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-145">The Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates to your Web roles.</span></span> <span data-ttu-id="bd2d9-146">Bu seçenek hakkında daha fazla bilgi için bkz: [yayımlama Azure araçlarını kullanarak bir bulut hizmeti](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd2d9-146">For more information on this option, see [Publishing a Cloud Service using the Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="bd2d9-147">Zaman **Microsoft Azure etkinlik günlüğü** yayımlama durumu gösterir **tamamlandı**, bulut hizmeti ile tümleşik bir CDN uç noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-147">When the **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="bd2d9-148">Yayımladıktan sonra dağıtılan bulut hizmeti hata ekranı görüntüler varsa, dağıttığınız bulut hizmeti tarafından kullanıldığından, büyük olasılıkla bir [konuk .NET 4.5.2 içermez OS](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="bd2d9-148">If, after publishing, the deployed cloud service displays an error screen, it's likely because the cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="bd2d9-149">Bu sorundan getirebilirler [.NET 4.5.2 bir başlangıç görevi olarak dağıtma](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="bd2d9-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="bd2d9-150">Yeni bir CDN profili oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd2d9-150">Create a new CDN profile</span></span>
<span data-ttu-id="bd2d9-151">CDN profili, CDN uç noktaları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="bd2d9-152">Her bir profil, bir veya daha fazla CDN uç noktası içerir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="bd2d9-153">CDN uç noktalarınızı İnternet etki alanı, web uygulaması veya başka ölçütlere göre düzenlemek için birden çok profil kullanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-153">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="bd2d9-154">Bu öğretici için kullanmak istediğiniz bir CDN profili varsa, devam [yeni bir CDN uç noktası oluşturma](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="bd2d9-154">If you already have a CDN profile that you want to use for this tutorial, proceed to [Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="bd2d9-155">Yeni bir CDN uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd2d9-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="bd2d9-156">**Depolama hesabınız için yeni bir CDN uç noktası oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="bd2d9-156">**To create a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="bd2d9-157">İçinde [Azure Yönetim Portalı](https://portal.azure.com), CDN profilinize gidin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-157">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="bd2d9-158">Önceki adımda bunu panoya sabitlemiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-158">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="bd2d9-159">Sabitlemediyseniz bunu bulmak için **Gözat**'a, ardından **CDN profilleri**'ne ve uç noktanızı eklemeyi planladığınız profile tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="bd2d9-160">CDN profili dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-160">The CDN profile blade appears.</span></span>
   
    ![CDN profili][cdn-profile-settings]
2. <span data-ttu-id="bd2d9-162">**Uç Nokta Ekle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-162">Click the **Add Endpoint** button.</span></span>
   
    ![Uç nokta ekle düğmesi][cdn-new-endpoint-button]
   
    <span data-ttu-id="bd2d9-164">**Uç nokta ekleme** dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-164">The **Add an endpoint** blade appears.</span></span>
   
    ![Uç nokta ekleme dikey penceresi][cdn-add-endpoint]
3. <span data-ttu-id="bd2d9-166">Bu CDN uç noktası için bir **Ad** girin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="bd2d9-167">Bu ad, `<EndpointName>.azureedge.net` etki alanındaki önbelleğe alınmış kaynaklarınıza erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-167">This name will be used to access your cached resources at the domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="bd2d9-168">İçinde **kaynak türü** açılan listesinde, select *bulut hizmeti*.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-168">In the **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="bd2d9-169">İçinde **kaynak ana bilgisayar adı** açılan listesinde, bulut hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-169">In the **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="bd2d9-170">Varsayılan değerleri bırakın **kaynak yolu**, **kaynak ana bilgisayar üstbilgisi**, ve **Protokolü/kaynak bağlantı noktası**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-170">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="bd2d9-171">En az bir protokol (HTTP veya HTTPS) belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="bd2d9-172">Yeni uç noktayı oluşturmak için **Ekle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-172">Click the **Add** button to create the new endpoint.</span></span>
8. <span data-ttu-id="bd2d9-173">Uç nokta oluşturulduktan sonra, profile yönelik uç noktalar listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-173">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="bd2d9-174">Liste görünümünde, kaynak etki alanının yanı sıra, önbelleğe alınan içeriğe erişmek için kullanılacak URL gösterilir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-174">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
   
    ![CDN uç noktası][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="bd2d9-176">Uç nokta hemen kullanılabilir olmaz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-176">The endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="bd2d9-177">CDN ağ üzerinden yaymak kayıt 90 dakika kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-177">It can take up to 90 minutes for the registration to propagate through the CDN network.</span></span> <span data-ttu-id="bd2d9-178">İçerik CDN kullanılabilir hale gelene kadar hemen CDN etki alanı adını kullanmayı deneyen kullanıcılar durum kodu 404 alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-178">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span></span>
   > 
   > 

## <a name="test-the-cdn-endpoint"></a><span data-ttu-id="bd2d9-179">CDN uç noktasını sınama</span><span class="sxs-lookup"><span data-stu-id="bd2d9-179">Test the CDN endpoint</span></span>
<span data-ttu-id="bd2d9-180">Yayımlama durumu olduğunda **tamamlandı**, bir tarayıcı penceresi açın ve gidin  **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-180">When the publishing status is **Completed**, open a browser window and navigate to **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="bd2d9-181">My Kurulum, bu URL'yi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="bd2d9-182">Hangi CDN uç noktası aşağıdaki kaynak URL'de karşılık gelir:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-182">Which corresponds to the following origin URL at the CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="bd2d9-183">Ne zaman gezinmek için  **http://*&lt;cdnName >*indirin veya gelen bootstrap.css açmak için bağlı olarak istenir, tarayıcınızdaki.azureedge.net/Content/bootstrap.css** yayımlanan Web uygulamanızdan.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-183">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted to download or open the bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="bd2d9-184">Genel olarak erişilebilir bir URL'de benzer şekilde erişebilirsiniz  **http://*&lt;serviceName >*doğrudan CDN uç noktanız gelen.cloudapp.net/**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="bd2d9-185">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-185">For example:</span></span>

* <span data-ttu-id="bd2d9-186">/ Script yolundan .js dosya</span><span class="sxs-lookup"><span data-stu-id="bd2d9-186">A .js file from the /Script path</span></span>
* <span data-ttu-id="bd2d9-187">/ Content içerik dosyanın yolu</span><span class="sxs-lookup"><span data-stu-id="bd2d9-187">Any content file from the /Content path</span></span>
* <span data-ttu-id="bd2d9-188">Herhangi bir denetleyici/eylem</span><span class="sxs-lookup"><span data-stu-id="bd2d9-188">Any controller/action</span></span>
* <span data-ttu-id="bd2d9-189">CDN uç noktanız, sorgu dizeleri içeren herhangi bir URL, sorgu dizesi etkinleştirilirse</span><span class="sxs-lookup"><span data-stu-id="bd2d9-189">If the query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="bd2d9-190">Aslında, yukarıdaki yapılandırma ile tüm bulut hizmetinden barındırabilir  **http://*&lt;cdnName >*.azureedge.net/**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-190">In fact, with the above configuration, you can host the entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**.</span></span> <span data-ttu-id="bd2d9-191">İçin giderseniz **http://camservice.azureedge.net/**, ev/dizinden eylem sonucu alıyorum.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-191">If I navigate to **http://camservice.azureedge.net/**, I get the action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="bd2d9-192">Bu, ancak bu her zaman bir tüm bulut hizmeti aracılığıyla Azure CDN sunmak için iyi bir fikir olduğu anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-192">This does not mean, however, that it's always a good idea to serve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="bd2d9-193">CDN statik teslim iyileştirme önbelleğe almak üzere düşünülmemiştir dinamik varlıklarını teslimat hızlandırmak değil veya CDN varlığı yeni bir sürümü kaynak sunucudan çok sık çekme gerekir bu yana çok sık güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-193">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant to be cached, or are updated very frequently, since the CDN must pull a new version of the asset from the Origin server very often.</span></span> <span data-ttu-id="bd2d9-194">Bu senaryo için etkinleştirmeniz [dinamik Site hızlandırma](cdn-dynamic-site-acceleration.md) alınabilir olmayan dinamik varlıklarını teslimat hızlandırmak için çeşitli teknikleri kullanan CDN uç noktanız iyileştirmeyi (DSA).</span><span class="sxs-lookup"><span data-stu-id="bd2d9-194">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques to speed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="bd2d9-195">Dinamik ve statik içeriği karışımını içeren bir siteniz varsa, statik en iyi duruma getirme türü (örneğin, genel web teslim) ile CDN, statik içerik sunmak ve dinamik içerik kaynak sunucudan doğrudan ya da bir CDN uç noktası w aracılığıyla hizmet seçebilir i DSA iyileştirme, bir olay temelinde açık.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-195">If you have a site with a mix of static and dynamic content, you can choose to serve your static content from CDN with a static optimization type (such as general web delivery), and to serve dynamic content either directly from the origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="bd2d9-196">Bu amaçla, ayrı ayrı içerik dosyaları CDN uç noktasından erişmek nasıl zaten gördünüz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-196">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="bd2d9-197">I denetleyici eylemleri Azure CDN aracılığıyla hizmet vermemesini içerikten bulunan belirli bir CDN uç noktası aracılığıyla belirli denetleyici eylemi hizmet nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-197">I will show you how to serve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="bd2d9-198">Bulut hizmetinizde olay temelinde Azure CDN sunmak için hangi içeriğini belirlemek için kullanılan alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-198">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="bd2d9-199">Bu amaçla, ayrı ayrı içerik dosyaları CDN uç noktasından erişmek nasıl zaten gördünüz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-199">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="bd2d9-200">T belirli denetleyici eylemi CDN uç aracılığıyla hizmet nasıl yapacağınızı gösterir [hizmet denetleyici eylemleri Azure CDN aracılığıyla içerikten](#controller).</span><span class="sxs-lookup"><span data-stu-id="bd2d9-200">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="bd2d9-201">Bulut hizmetinizde statik dosyalar için önbellek seçeneklerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bd2d9-201">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="bd2d9-202">Bulut hizmetinizde Azure CDN tümleştirme ile nasıl CDN uç önbelleğe alınacak statik içerik istediğinizi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-202">With Azure CDN integration in your cloud service, you can specify how you want static content to be cached in the CDN endpoint.</span></span> <span data-ttu-id="bd2d9-203">Bunu yapmak için açın *Web.config* (örneğin WebRole1), Web rolünden proje ve ekleme bir `<staticContent>` öğesine `<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-203">To do this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element to `<system.webServer>`.</span></span> <span data-ttu-id="bd2d9-204">XML süresi 3 gün içinde dolacak önbellek yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-204">The XML below configures the cache to expire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="bd2d9-205">Bunu yaptıktan sonra bulut hizmetindeki tüm statik dosyaları CDN önbelleğiniz aynı kuralında gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-205">Once you do this, all static files in your cloud service will observe the same rule in your CDN cache.</span></span> <span data-ttu-id="bd2d9-206">Önbellek ayarları konusunda daha ayrıntılı denetim için ekleme bir *Web.config* bir klasöre dosya ve ayarlarınızı var. ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-206">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="bd2d9-207">Örneğin, bir *Web.config* dosya *\Content* klasörü ve içeriği aşağıdaki XML ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-207">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="bd2d9-208">Bu ayarı tüm statik dosyaları neden *\Content* 15 gün boyunca önbelleğe alınacak klasörü.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-208">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span></span>

<span data-ttu-id="bd2d9-209">Nasıl yapılandırılacağı hakkında daha fazla bilgi için `<clientCache>` öğesi, bkz: [istemci önbelleği &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="bd2d9-209">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="bd2d9-210">İçinde [hizmet denetleyici eylemleri Azure CDN aracılığıyla içerikten](#controller), ı de CDN önbelleğinde önbellek ayarları denetleyici eylem sonuçlarına yönelik nasıl yapılandırabileceğiniz gösterilir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-210">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in the CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="bd2d9-211">Denetleyici eylemleri Azure CDN aracılığıyla içerikten hizmet</span><span class="sxs-lookup"><span data-stu-id="bd2d9-211">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="bd2d9-212">Bulut hizmeti Web rolü Azure CDN ile tümleştirdiğinizde, denetleyici eylemleri için Azure CDN aracılığıyla içerikten hizmet oldukça kolaydır.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-212">When you integrate a cloud service Web role with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span></span> <span data-ttu-id="bd2d9-213">Bulut hizmet veren dışında doğrudan Azure (yukarıda gösterilen), CDN hizmet [Maarten Balliauw](https://twitter.com/maartenballiauw) eğlenceli ile nasıl yapılacağını gösterir MemeGenerator denetleyicisi [Azure CDNwebüzerindegecikme](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="bd2d9-213">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="bd2d9-214">I yalnızca onu buraya yeniden.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-214">I will simply reproduce it here.</span></span>

<span data-ttu-id="bd2d9-215">Bulutunuzdaki Küçük yaştaki ALi Norris görüntüde memes oluşturmak istediğiniz hizmet tabanlı varsayalım (tarafından fotoğraf [Alan ışık](http://www.flickr.com/photos/alan-light/218493788/)) şöyle:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-215">Suppose in your cloud service you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="bd2d9-216">Basit bir sahip `Index` derecelerinin görüntüde belirtmek müşterilerin sağlayan eylem için eylem sonrası sonra meme sonra oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-216">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span></span> <span data-ttu-id="bd2d9-217">ALi Norris olduğuna göre genel müthiş bir başarı popüler hale için bu sayfayı beklenir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-217">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span></span> <span data-ttu-id="bd2d9-218">Bu, yarı dinamik içerik Azure CDN ile hizmet veren, iyi bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-218">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="bd2d9-219">Bu denetleyici eylemi kurulumu için yukarıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-219">Follow the steps above to setup this controller action:</span></span>

1. <span data-ttu-id="bd2d9-220">İçinde *\Controllers* klasör adında yeni bir .cs dosyası oluşturma *MemeGeneratorController.cs* ve içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-220">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span></span> <span data-ttu-id="bd2d9-221">Vurgulanan bölümü, CDN adınızla değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-221">Be sure to replace the highlighted portion with your CDN name.</span></span>  
   
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
   
                    if (Debugger.IsAttached) // Preserve the debug experience
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
2. <span data-ttu-id="bd2d9-222">Varsayılan olarak sağ `Index()` eylem ve select **Görünüm Ekle**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-222">Right-click in the default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="bd2d9-223">Aşağıdaki ayarları kabul edin ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-223">Accept the settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="bd2d9-224">Yeni *Views\MemeGenerator\Index.cshtml* ve içeriği derecelerinin göndermek için aşağıdaki basit HTML ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-224">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="bd2d9-225">Bulut hizmeti yeniden yayımlamanız ve gidin  **http://*&lt;serviceName >*tarayıcınızda.cloudapp.net/MemeGenerator/Index**.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-225">Publish the cloud service again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="bd2d9-226">Form değerleri gönderdiğiniz zaman `/MemeGenerator/Index`, `Index_Post` eylem yöntemine döndürür bağlantı `Show` eylem yöntemi ile ilgili giriş tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-226">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span></span> <span data-ttu-id="bd2d9-227">Bağlantıya tıkladığınızda, aşağıdaki kodu ulaşmak:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-227">When you click the link, you reach the following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve the debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="bd2d9-228">Ardından, yerel hata ayıklayıcısı ekli, yerel bir yeniden yönlendirme normal hata ayıklama deneyimini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-228">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span></span> <span data-ttu-id="bd2d9-229">Bulut Hizmeti çalışıyorsa, için yönlendirir:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-229">If it's running in the cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="bd2d9-230">Hangi CDN uç noktanız aşağıdaki kaynak URL'de karşılık gelir:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-230">Which corresponds to the following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="bd2d9-231">Daha sonra `OutputCacheAttribute` özniteliği `Generate` yöntemi nasıl eylem sonucu, hangi Azure CDN dokunmaz önbelleğe alınacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-231">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="bd2d9-232">Aşağıdaki kod bir önbellek süre sonu 1 saatlik (3.600 saniye) belirtin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-232">The code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="bd2d9-233">Benzer şekilde, size herhangi bir denetleyici eylem içerikten yukarı bulut hizmetiniz istenen önbelleğe alma seçeneği ile Azure CDN aracılığıyla hizmet verebilir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-233">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with the desired caching option.</span></span>

<span data-ttu-id="bd2d9-234">Sonraki bölümde, t, ile birlikte gelen ve küçültülmüş komut dosyaları ve CSS Azure CDN aracılığıyla sunmaya nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-234">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="bd2d9-235">ASP.NET paketleme ve küçültme Azure CDN ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="bd2d9-235">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="bd2d9-236">Komut dosyaları ve CSS stil sayfaları, seyrek değiştirin ve Azure CDN önbellek prime adaylar.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-236">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span></span> <span data-ttu-id="bd2d9-237">Tüm Web rolü, Azure CDN aracılığıyla hizmet veren, paketleme ve küçültme Azure CDN ile tümleştirmek için kolay bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-237">Serving the entire Web role through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="bd2d9-238">Ancak, ı bunu istemeyebilirsiniz gibi ASP.NET paketleme ve küçültme, istenen develper deneyimini gibi koruma sırasında nasıl yapılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-238">However, as you may not want to do this, I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="bd2d9-239">Harika hata ayıklama modu deneyimi</span><span class="sxs-lookup"><span data-stu-id="bd2d9-239">Great debug mode experience</span></span>
* <span data-ttu-id="bd2d9-240">Basitleştirilmiş Dağıtım</span><span class="sxs-lookup"><span data-stu-id="bd2d9-240">Streamlined deployment</span></span>
* <span data-ttu-id="bd2d9-241">Komut dosyası/CSS sürüm yükseltme için istemcilere hemen güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="bd2d9-241">Immediate updates to clients for script/CSS version upgrades</span></span>
* <span data-ttu-id="bd2d9-242">CDN uç noktanız başarısız olduğunda bir geri dönüş mekanizması</span><span class="sxs-lookup"><span data-stu-id="bd2d9-242">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="bd2d9-243">Kod değişikliği simge durumuna küçült</span><span class="sxs-lookup"><span data-stu-id="bd2d9-243">Minimize code modification</span></span>

<span data-ttu-id="bd2d9-244">İçinde **WebRole1** oluşturduğunuz proje [Azure CDN uç Azure Web sitesi ile bütünleşir ve Azure CDN Web sayfalarınıza statik içerik sunmanızı](#deploy), açık *App_Start\ BundleConfig.cs* ve bir göz atalım `bundles.Add()` yöntem çağrıları.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-244">In the **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="bd2d9-245">İlk `bundles.Add()` deyimi sanal dizininde betik paket ekler `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-245">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="bd2d9-246">Ardından, açın *görünümler/paylaşılan\_Layout.cshtml* paket etiketi nasıl işlendiğine görmek için.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-246">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span></span> <span data-ttu-id="bd2d9-247">Razor kodunun aşağıdaki satırı bulun yapabiliyor olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-247">You should be able to find the following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="bd2d9-248">Bu Razor kod Azure Web rolü çalıştırdığınızda kılacak bir `<script>` etiketi aşağıdakine benzer betik paket için:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-248">When this Razor code is run in the Azure Web role, it will render a `<script>` tag for the script bundle similar to the following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="bd2d9-249">Ancak, çalıştırıldığında Visual Studio'da yazarak `F5`, paketteki her komut dosyası ayrı ayrı kılacak (Yukarıdaki durumda yalnızca tek bir betik paketteki dosyasıdır):</span><span class="sxs-lookup"><span data-stu-id="bd2d9-249">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="bd2d9-250">Bu, eşzamanlı istemci bağlantıları (paketleme) azaltma ve dosya geliştirme performans (küçültme) üretimde karşıdan yüklenirken geliştirme ortamınızı JavaScript kodunda hata ayıklama olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-250">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="bd2d9-251">Azure CDN tümleştirme ile korumak için harika bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-251">It's a great feature to preserve with Azure CDN integration.</span></span> <span data-ttu-id="bd2d9-252">İşlenen paket otomatik olarak oluşturulan sürüm dizesi içerdiğinden, ayrıca, bu işlevselliği çoğaltmak istediğiniz şekilde jQuery sürümünüzü NuGet aracılığıyla güncelleştirdiğinizde, istemci tarafında mümkün olan en kısa sürede güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-252">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so the whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span></span>

<span data-ttu-id="bd2d9-253">ASP.NET tümleştirme paketleme ve küçültme ile CDN uç noktanız için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-253">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="bd2d9-254">Geri *App_Start\BundleConfig.cs*, değişiklik `bundles.Add()` farklı bir kullanılacak yöntemleri [paket Oluşturucusu](http://msdn.microsoft.com/library/jj646464.aspx), bir CDN adresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-254">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="bd2d9-255">Bunu yapmak için yerini `RegisterBundles` aşağıdaki kod ile yöntemi tanımı:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-255">To do this, replace the `RegisterBundles` method definition with the following code:</span></span>  
   
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
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you're
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="bd2d9-256">Değiştirdiğinizden emin olun `<yourCDNName>` Azure CDN adı.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-256">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span></span>
   
    <span data-ttu-id="bd2d9-257">Düz metin olarak ayarladığınız `bundles.UseCdn = true` ve her paket için dikkatli bir şekilde hazırlanmış bir CDN URL eklenir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-257">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span></span> <span data-ttu-id="bd2d9-258">Örneğin, ilk oluşturucuda kodu:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-258">For example, the first constructor in the code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="bd2d9-259">aynı sonucu verir:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-259">is the same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="bd2d9-260">Bu oluşturucu, ASP.NET paketleme ve küçültme yerel olarak hata ayıklaması sırasında ayrı komut dosyaları oluşturmak, ancak söz konusu betik erişmek için belirtilen CDN adresini kullanmak için söyler.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-260">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span></span> <span data-ttu-id="bd2d9-261">Ancak, bu dikkatle hazırlanmış CDN URL ile iki önemli özelliklere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-261">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="bd2d9-262">Bu CDN URL kaynağı `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, bulut hizmetinizin komut dosyası pakette gerçekte sanal dizinin olduğu.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-262">The origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your cloud service.</span></span>
   * <span data-ttu-id="bd2d9-263">CDN Oluşturucusu kullandığımızdan, paket için CDN komut dosyası etiketinin artık işlenmiş URL'de otomatik olarak oluşturulan sürüm dizesi içerir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-263">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span></span> <span data-ttu-id="bd2d9-264">Önbellek isabetsizliği Azure CDN adresindeki zorlamak için komut dosyası paket değiştiren her zaman bir benzersiz sürüm dizesi el ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-264">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span></span> <span data-ttu-id="bd2d9-265">Aynı anda bu benzersiz sürüm dizesi paket dağıtıldıktan sonra Azure CDN adresindeki İsabetli Önbellek okuma sayısı en üst düzeye çıkarmak için dağıtımı yaşam sabit kalması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-265">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span></span>
   * <span data-ttu-id="bd2d9-266">Sorgu dizesi v < W.X.Y.Z > çeken gelen = *Properties\AssemblyInfo.cs* Web rolü projenizdeki.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-266">The query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="bd2d9-267">Derleme sürümü için Azure yayımlama her zaman artırma içeren bir dağıtım iş akışı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-267">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span></span> <span data-ttu-id="bd2d9-268">Veya yalnızca değiştirebileceğiniz *Properties\AssemblyInfo.cs* projenize sürüm dizesi joker karakter kullanarak oluşturduğunuz her zaman otomatik olarak artırmak için ' *'.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-268">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '*'.</span></span> <span data-ttu-id="bd2d9-269">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-269">For example:</span></span>
     
        <span data-ttu-id="bd2d9-270">[derleme: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="bd2d9-270">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="bd2d9-271">Bir dağıtım ömrü için benzersiz bir dize oluşturma kolaylaştırmak için diğer bir strateji burada çalışır.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-271">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span></span>
2. <span data-ttu-id="bd2d9-272">Bulut hizmeti yeniden yayımlamanız ve giriş sayfasına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-272">Republish the cloud service and access the home page.</span></span>
3. <span data-ttu-id="bd2d9-273">Sayfanın HTML kodunu görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-273">View the HTML code for the page.</span></span> <span data-ttu-id="bd2d9-274">Bulut hizmetinizi değişiklikleri yeniden yayımlamanız her zaman bir benzersiz sürüm dizesi ile işlenen CDN URL'sine görebilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-274">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your cloud service.</span></span> <span data-ttu-id="bd2d9-275">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-275">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="bd2d9-276">Visual Studio'da yazarak, Visual Studio bulut hizmetinde hata ayıklama `F5`.,</span><span class="sxs-lookup"><span data-stu-id="bd2d9-276">In Visual Studio, debug the cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="bd2d9-277">Sayfanın HTML kodunu görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-277">View the HTML code for the page.</span></span> <span data-ttu-id="bd2d9-278">Böylece Visual Studio'da deneyimi tutarlı bir hata ayıklama sahip tek tek işlenen her komut dosyası hala görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-278">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
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

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="bd2d9-279">CDN URL'ler için geri dönüş mekanizması</span><span class="sxs-lookup"><span data-stu-id="bd2d9-279">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="bd2d9-280">Azure CDN uç noktanız için herhangi bir nedenle başarısız olduğunda, Web sayfanızın JavaScript veya önyükleme yüklenmesi için geri dönüş seçeneği olarak, kaynak Web sunucusuna erişmek akıllı olmasını istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-280">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="bd2d9-281">Sitenizdeki komut dosyalarını ve stil sayfalarını tarafından sağlanan önemli sayfa işlevleri için çok daha ağır ancak CDN kullanılamazlık nedeniyle görüntüleri kaybetmenize ciddi.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-281">It's serious enough to lose images on your website due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="bd2d9-282">[Paket](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) sınıfı adlı bir özellik içerir [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) CDN hatası için geri dönüş mekanizması yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-282">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span></span> <span data-ttu-id="bd2d9-283">Bu özelliği kullanmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-283">To use this property, follow the steps below:</span></span>

1. <span data-ttu-id="bd2d9-284">Web rolü projesinde açmak *App_Start\BundleConfig.cs*, CDN URL'sine her eklediğiniz [paket Oluşturucusu](http://msdn.microsoft.com/library/jj646464.aspx), varsayılan geri dönüş mekanizması eklemek için aşağıdaki vurgulanan değişiklikler Paketleri:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-284">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make the following highlighted changes to add fallback mechanism to the default bundles:</span></span>  
   
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
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
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
   
    <span data-ttu-id="bd2d9-285">Zaman `CdnFallbackExpression` olan null değil, betik paket başarıyla yüklendi olup olmadığını sınamak ve değilse, paket kaynak Web sunucusundan doğrudan erişmek için HTML'e eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-285">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span></span> <span data-ttu-id="bd2d9-286">Bu özellik, ilgili CDN paket düzgün şekilde yüklenmesini olup olmadığını, testleri bir JavaScript ifadesi ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-286">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="bd2d9-287">Her paket test etmek için gerekli ifade içeriği göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-287">The expression needed to test each bundle differs according to the content.</span></span> <span data-ttu-id="bd2d9-288">Varsayılan paketleri için yukarıdaki:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-288">For the default bundles above:</span></span>
   
   * <span data-ttu-id="bd2d9-289">`window.jquery`JQuery-{version} .js tanımlanır</span><span class="sxs-lookup"><span data-stu-id="bd2d9-289">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="bd2d9-290">`$.validator`JQuery.Validate.js tanımlanır</span><span class="sxs-lookup"><span data-stu-id="bd2d9-290">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="bd2d9-291">`window.Modernizr`modernizer gibi-{version} .js tanımlanır</span><span class="sxs-lookup"><span data-stu-id="bd2d9-291">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="bd2d9-292">`$.fn.modal`Bootstrap.js tanımlanır</span><span class="sxs-lookup"><span data-stu-id="bd2d9-292">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="bd2d9-293">I CdnFallbackExpression için ayarlamamış fark etmiş olabilirsiniz `~/Cointent/css` paket.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-293">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span></span> <span data-ttu-id="bd2d9-294">Şu anda bu olmadığından bir [System.Web.Optimization hatada](https://aspnetoptimization.codeplex.com/workitem/104) , yerleştirir bir `<script>` beklenen yerine geri dönüş CSS etiketini `<link>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-294">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span></span>
     
     <span data-ttu-id="bd2d9-295">Yoktur, ancak iyi bir [stili paket geri dönüş](https://github.com/EmberConsultingGroup/StyleBundleFallback) tarafından sunulan [Ember danışmanlık grup](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="bd2d9-295">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="bd2d9-296">Geçici çözüm için CSS kullanmak için Web rolü projenizin içinde yeni bir .cs dosyası oluşturun *App_Start* adlı bir klasör *StyleBundleExtensions.cs*ve içeriği ile Değiştir [github'dan kodu ](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="bd2d9-296">To use the workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="bd2d9-297">İçinde *App_Start\StyleFundleExtensions.cs*, ad alanı, Web rolün adıyla yeniden adlandırın (örneğin **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="bd2d9-297">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="bd2d9-298">Geri dönerek `App_Start\BundleConfig.cs` ve son değiştirme `bundles.Add` aşağıdaki vurgulanmış kodu deyimiyle:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-298">Go back to `App_Start\BundleConfig.cs` and modify the last `bundles.Add` statement with the following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="bd2d9-299">Komut dosyası için DOM denetlemek için HTML eklemesine aynı fikir bu yeni genişletme yöntemi kullanan bir eşleşen sınıf adı, kural adı ve CSS paket ve kaynağı Web sunucusu geri döner için eşleşme bulunamadı başarısız olursa tanımlanmış kural değer.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-299">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span></span>
5. <span data-ttu-id="bd2d9-300">Bulut hizmeti yeniden yayımlamanız ve giriş sayfasına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-300">Publish the cloud service again and access the home page.</span></span>
6. <span data-ttu-id="bd2d9-301">Sayfanın HTML kodunu görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-301">View the HTML code for the page.</span></span> <span data-ttu-id="bd2d9-302">Eklenen komut dosyaları aşağıdakine benzer bulmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-302">You should find injected scripts similar to the following:</span></span>    
   
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

    <span data-ttu-id="bd2d9-303">CSS paket için eklenen kod gelen yalıtılarak işlemi hala içerdiğine dikkat edin `CdnFallbackExpression` satır özelliğinde:</span><span class="sxs-lookup"><span data-stu-id="bd2d9-303">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="bd2d9-304">Ancak ilk kısmı bu yana || ifade her zaman true (satırda doğrudan yukarıdaki) döndürür ve document.write() işlevi asla çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="bd2d9-304">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="bd2d9-305">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="bd2d9-305">More Information</span></span>
* [<span data-ttu-id="bd2d9-306">Azure içerik teslim ağı (CDN) genel bakış</span><span class="sxs-lookup"><span data-stu-id="bd2d9-306">Overview of the Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="bd2d9-307">Azure CDN'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="bd2d9-307">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="bd2d9-308">ASP.NET paketleme ve küçültme</span><span class="sxs-lookup"><span data-stu-id="bd2d9-308">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png

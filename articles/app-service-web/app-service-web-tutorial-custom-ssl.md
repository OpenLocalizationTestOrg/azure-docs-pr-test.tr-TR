---
title: "Azure Web uygulamaları için var olan özel bir SSL sertifikası bağlama | Microsoft Docs"
description: "Web uygulaması, mobil uygulama arka ucu veya Azure App Service'teki API uygulamasına özel bir SSL sertifikası bağlanılacağını öğrenin."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 15c31ae5451a31dff2df08047ee43e75edacc127
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-to-azure-web-apps"></a><span data-ttu-id="99732-103">Azure Web uygulamaları için var olan özel bir SSL sertifikası bağlama</span><span class="sxs-lookup"><span data-stu-id="99732-103">Bind an existing custom SSL certificate to Azure Web Apps</span></span>

<span data-ttu-id="99732-104">Azure Web Apps düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="99732-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="99732-105">Bu öğretici için güvenilir bir sertifika yetkilisinden satın aldığınız özel bir SSL sertifikası bağlanacağı gösterilmektedir [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99732-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="99732-106">İşiniz bittiğinde, web uygulamanızı DNS etki alanınız HTTPS uç noktası erişmek mümkün olur.</span><span class="sxs-lookup"><span data-stu-id="99732-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span></span>

![Özel SSL sertifikası ile Web uygulaması](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="99732-108">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="99732-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="99732-109">Uygulamanızın fiyatlandırma katmanı yükseltme</span><span class="sxs-lookup"><span data-stu-id="99732-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="99732-110">Özel SSL sertifikanızı uygulama hizmetine bağlama</span><span class="sxs-lookup"><span data-stu-id="99732-110">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="99732-111">Uygulamanız için HTTPS zorla</span><span class="sxs-lookup"><span data-stu-id="99732-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="99732-112">SSL sertifikası bağlaması kodlarıyla otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="99732-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="99732-113">Özel bir SSL sertifikası almanız gerekiyorsa, Azure portalında doğrudan edinebileceğinizi ve web uygulamanıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="99732-113">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span></span> <span data-ttu-id="99732-114">İzleyin [uygulama hizmeti sertifikaları Öğreticisi](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="99732-114">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99732-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="99732-115">Prerequisites</span></span>

<span data-ttu-id="99732-116">Bu öğreticiyi tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="99732-116">To complete this tutorial:</span></span>

- [<span data-ttu-id="99732-117">Bir App Service uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="99732-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="99732-118">Harita web uygulamanız için özel bir DNS adı</span><span class="sxs-lookup"><span data-stu-id="99732-118">Map a custom DNS name to your web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="99732-119">Güvenilen sertifika yetkilisinden bir SSL sertifikası alın</span><span class="sxs-lookup"><span data-stu-id="99732-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="99732-120">SSL sertifika için gereksinimler</span><span class="sxs-lookup"><span data-stu-id="99732-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="99732-121">App Service'te bir sertifika kullanmak üzere sertifika aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="99732-121">To use a certificate in App Service, the certificate must meet all the following requirements:</span></span>

* <span data-ttu-id="99732-122">Bir güvenilir sertifika yetkilisi tarafından imzalanmış</span><span class="sxs-lookup"><span data-stu-id="99732-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="99732-123">Parola korumalı bir PFX dosyası olarak dışa</span><span class="sxs-lookup"><span data-stu-id="99732-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="99732-124">Özel anahtarı en az 2048 bit uzun içerir</span><span class="sxs-lookup"><span data-stu-id="99732-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="99732-125">Sertifika zincirindeki tüm ara sertifikaların içerir</span><span class="sxs-lookup"><span data-stu-id="99732-125">Contains all intermediate certificates in the certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="99732-126">**Eliptik Eğri Şifrelemesi (ECC) sertifikaları** App Service ile çalışabilir, ancak bu makalenin ele alınmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="99732-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="99732-127">Sertifika yetkilisi ile ECC sertifikaları oluşturmak için uygulanacak adımlar üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="99732-127">Work with your certificate authority on the exact steps to create ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="99732-128">Web uygulamanızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="99732-128">Prepare your web app</span></span>

<span data-ttu-id="99732-129">Özel bir SSL sertifikası, web uygulamanızın bağlamak için [uygulama hizmeti planı](https://azure.microsoft.com/pricing/details/app-service/) olmalıdır **temel**, **standart**, veya **Premium** katmanı.</span><span class="sxs-lookup"><span data-stu-id="99732-129">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="99732-130">Bu adımda, web uygulamanızı desteklenen fiyatlandırma katmanı olduğundan emin emin olun.</span><span class="sxs-lookup"><span data-stu-id="99732-130">In this step, you make sure that your web app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="99732-131">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="99732-131">Log in to Azure</span></span>

<span data-ttu-id="99732-132">[Azure portalı](https://portal.azure.com) açın.</span><span class="sxs-lookup"><span data-stu-id="99732-132">Open the [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-to-your-web-app"></a><span data-ttu-id="99732-133">Web uygulamanıza gidin</span><span class="sxs-lookup"><span data-stu-id="99732-133">Navigate to your web app</span></span>

<span data-ttu-id="99732-134">Sol menüden **uygulama hizmetleri**ve ardından, web uygulamanızın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99732-134">From the left menu, click **App Services**, and then click the name of your web app.</span></span>

![Web uygulaması seçin](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="99732-136">Web uygulaması Yönetimi sayfasındaki indiniz.</span><span class="sxs-lookup"><span data-stu-id="99732-136">You have landed in the management page of your web app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="99732-137">Fiyatlandırma katmanı denetleyin</span><span class="sxs-lookup"><span data-stu-id="99732-137">Check the pricing tier</span></span>

<span data-ttu-id="99732-138">Web uygulaması sayfanızı sol gezinti bölmesinde kaydırın **ayarları** bölümünde ve seçin **(uygulama hizmeti planı) ölçeklendirme**.</span><span class="sxs-lookup"><span data-stu-id="99732-138">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Büyütme menüsü](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="99732-140">Web uygulamanızı içinde olmadığından emin olmak için kontrol edin **serbest** veya **paylaşılan** katmanı.</span><span class="sxs-lookup"><span data-stu-id="99732-140">Check to make sure that your web app is not in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="99732-141">Web uygulamanızın geçerli katmanı Koyu mavi bir kutu vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="99732-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="99732-143">Özel SSL desteklenmez **serbest** veya **paylaşılan** katmanı.</span><span class="sxs-lookup"><span data-stu-id="99732-143">Custom SSL is not supported in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="99732-144">Ölçeği gerekiyorsa, sonraki bölümde yer alan adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="99732-144">If you need to scale up, follow the steps in the next section.</span></span> <span data-ttu-id="99732-145">Aksi takdirde, kapatmak **fiyatlandırma katmanınızı seçin** sayfasında ve geçin [karşıya yükleme ve SSL sertifikanız bağlama](#upload).</span><span class="sxs-lookup"><span data-stu-id="99732-145">Otherwise, close the **Choose your pricing tier** page and skip to [Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="99732-146">Uygulama hizmeti planınızı ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="99732-146">Scale up your App Service plan</span></span>

<span data-ttu-id="99732-147">Aşağıdakilerden birini seçin **temel**, **standart**, veya **Premium** katmanları.</span><span class="sxs-lookup"><span data-stu-id="99732-147">Select one of the **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="99732-148">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99732-148">Click **Select**.</span></span>

![Fiyatlandırma katmanı seçin](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="99732-150">Aşağıdaki bildirim görürseniz, bir ölçeklendirme işlemi tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="99732-150">When you see the following notification, the scale operation is complete.</span></span>

![Bildirimi ölçeklendirme](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="99732-152">SSL sertifikası bağlama</span><span class="sxs-lookup"><span data-stu-id="99732-152">Bind your SSL certificate</span></span>

<span data-ttu-id="99732-153">Web uygulamanız için SSL sertifikanızı karşıya yüklemeye hazırsınız demektir.</span><span class="sxs-lookup"><span data-stu-id="99732-153">You are ready to upload your SSL certificate to your web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="99732-154">Ara Sertifika birleştirme</span><span class="sxs-lookup"><span data-stu-id="99732-154">Merge intermediate certificates</span></span>

<span data-ttu-id="99732-155">Sertifika yetkilisi sertifika zincirinde birden çok sertifika veriyorsa, sipariş sertifikaları birleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="99732-155">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span></span> 

<span data-ttu-id="99732-156">Bunu yapmak için bir metin düzenleyicisinde alınan her sertifika açın.</span><span class="sxs-lookup"><span data-stu-id="99732-156">To do this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="99732-157">Adlı birleştirilmiş sertifikası için bir dosya oluşturmak _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="99732-157">Create a file for the merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="99732-158">Bir metin düzenleyicisinde içeriği her sertifika, bu dosyaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="99732-158">In a text editor, copy the content of each certificate into this file.</span></span> <span data-ttu-id="99732-159">Sertifikalarınızı sırasını aşağıdaki şablonu gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="99732-159">The order of your certificates should look like the following template:</span></span>

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-to-pfx"></a><span data-ttu-id="99732-160">PFX için sertifika verme</span><span class="sxs-lookup"><span data-stu-id="99732-160">Export certificate to PFX</span></span>

<span data-ttu-id="99732-161">Birleştirilmiş SSL sertifikanızı sertifika isteğinizi ile oluşturulan özel anahtarla dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="99732-161">Export your merged SSL certificate with the private key that your certificate request was generated with.</span></span>

<span data-ttu-id="99732-162">Ardından OpenSSL kullanarak sertifika isteğinizi oluşturursa, özel bir anahtar dosyası oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="99732-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="99732-163">PFX için sertifika vermek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="99732-163">To export your certificate to PFX, run the following command.</span></span> <span data-ttu-id="99732-164">Yer tutucuları değiştirmek  _&lt;özel anahtar dosyası >_ ve  _&lt;birleştirilmiş-sertifika-dosyası >_.</span><span class="sxs-lookup"><span data-stu-id="99732-164">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="99732-165">İstendiğinde, bir dışarı aktarma parolası tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="99732-165">When prompted, define an export password.</span></span> <span data-ttu-id="99732-166">Daha sonra App Service'e SSL sertifikanızı karşıya yüklenirken bu parolayı kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="99732-166">You'll use this password when uploading your SSL certificate to App Service later.</span></span>

<span data-ttu-id="99732-167">IIS kullandıysanız veya _Certreq.exe_ , sertifika isteği oluşturmak için sertifika yerel makinenize yükleyin ve ardından [PFX için sertifika verme](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="99732-167">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="99732-168">SSL sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="99732-168">Upload your SSL certificate</span></span>

<span data-ttu-id="99732-169">SSL sertifikanızı karşıya yüklemek için tıklayın **SSL sertifikalarını** , web uygulamanızın sol gezinti bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="99732-169">To upload your SSL certificate, click **SSL certificates** in the left navigation of your web app.</span></span>

<span data-ttu-id="99732-170">Tıklatın **karşıya sertifika**.</span><span class="sxs-lookup"><span data-stu-id="99732-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="99732-171">İçinde **PFX sertifika dosyanızı**, PFX dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="99732-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="99732-172">İçinde **sertifika parolası**, PFX dosyasını dışarı aktardığınızda, oluşturduğunuz parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="99732-172">In **Certificate password**, type the password that you created when you exported the PFX file.</span></span>

<span data-ttu-id="99732-173">**Karşıya Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99732-173">Click **Upload**.</span></span>

![Sertifikayı karşıya yükleme](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="99732-175">Uygulama hizmeti sertifikanızı karşıya yükleme tamamlandığında, görünür **SSL sertifikalarını** sayfası.</span><span class="sxs-lookup"><span data-stu-id="99732-175">When App Service finishes uploading your certificate, it appears in the **SSL certificates** page.</span></span>

![Karşıya sertifika](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="99732-177">SSL sertifikası bağlama</span><span class="sxs-lookup"><span data-stu-id="99732-177">Bind your SSL certificate</span></span>

<span data-ttu-id="99732-178">İçinde **SSL bağlamaları** 'yi tıklatın **eklemek bağlama**.</span><span class="sxs-lookup"><span data-stu-id="99732-178">In the **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="99732-179">İçinde **SSL bağlaması Ekle** sayfasında, bırakmalar güvenliğini sağlamak için etki alanı adı seçin ve kullanılacak sertifikayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="99732-179">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span></span>

> [!NOTE]
> <span data-ttu-id="99732-180">Sertifikanız karşıya yüklediğiniz halde etki alanı adları göremiyorsanız **ana bilgisayar adı** açılan listesinde, tarayıcı sayfayı yenilemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="99732-180">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span></span>
>
>

<span data-ttu-id="99732-181">İçinde **SSL türü**, kullanıp kullanmayacağınızı seçin  **[sunucu adı göstergesi (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  ya da IP tabanlı SSL.</span><span class="sxs-lookup"><span data-stu-id="99732-181">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="99732-182">**SNI tabanlı SSL** -birden çok SNI tabanlı SSL bağlamaları eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="99732-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="99732-183">Bu seçenek, aynı IP adresinde birden çok etki alanı güvenliğini sağlamak birden çok SSL sertifikası sağlar.</span><span class="sxs-lookup"><span data-stu-id="99732-183">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span></span> <span data-ttu-id="99732-184">(Internet Explorer, Chrome, Firefox ve Opera dahil) çoğu modern tarayıcılar SNI destekler (daha kapsamlı tarayıcı destek bilgilerini bulmak [sunucu adı göstergesi](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="99732-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="99732-185">**IP tabanlı SSL** -yalnızca bir IP temelli SSL bağlama eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="99732-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="99732-186">Bu seçenek, ayrılmış bir ortak IP adresi güvenli hale getirmek yalnızca bir SSL sertifikası sağlar.</span><span class="sxs-lookup"><span data-stu-id="99732-186">This option allows only one SSL certificate to secure a dedicated public IP address.</span></span> <span data-ttu-id="99732-187">Birden çok etki alanı güvenliğini sağlamak için bunların tümü aynı SSL sertifikası kullanarak güvenli hale getirmenize gerekir.</span><span class="sxs-lookup"><span data-stu-id="99732-187">To secure multiple domains, you must secure them all using the same SSL certificate.</span></span> <span data-ttu-id="99732-188">SSL bağlaması için geleneksel seçenek budur.</span><span class="sxs-lookup"><span data-stu-id="99732-188">This is the traditional option for SSL binding.</span></span>

<span data-ttu-id="99732-189">Tıklatın **bağlama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="99732-189">Click **Add Binding**.</span></span>

![SSL sertifikası bağlama](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="99732-191">Uygulama hizmeti sertifikanızı karşıya yükleme tamamlandığında, görünür **SSL bağlamaları** bölümler.</span><span class="sxs-lookup"><span data-stu-id="99732-191">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span></span>

![Web uygulaması'na bağlı sertifikası](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="99732-193">IP SSL için bir kayıt yeniden eşleme</span><span class="sxs-lookup"><span data-stu-id="99732-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="99732-194">Web uygulamanızda IP tabanlı SSL kullanmıyorsanız, geçin [Test HTTPS özel etki alanınız için](#test).</span><span class="sxs-lookup"><span data-stu-id="99732-194">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="99732-195">Varsayılan olarak, web uygulamanızı paylaşılan bir ortak IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="99732-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="99732-196">IP tabanlı SSL sertifikasıyla bağladığınızda, App Service web uygulamanız için yeni, ayrılmış bir IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99732-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="99732-197">Web uygulamanız için bir A kaydı eşledikten ise, etki alanı kayıt defteri bu yeni, özel IP adresi ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="99732-197">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="99732-198">Web uygulamanızın **özel etki alanı** sayfası, yeni, özel IP adresi ile güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="99732-198">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span></span> <span data-ttu-id="99732-199">[Bu IP adresi Kopyala](app-service-web-tutorial-custom-domain.md#info), ardından [A kaydını yeniden eşleme](app-service-web-tutorial-custom-domain.md#map-an-a-record) bu yeni bir IP adresi için.</span><span class="sxs-lookup"><span data-stu-id="99732-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="99732-200">Test HTTPS</span><span class="sxs-lookup"><span data-stu-id="99732-200">Test HTTPS</span></span>

<span data-ttu-id="99732-201">Tüm yapmak için sol sunulmuştur HTTPS için özel etki alanınızı çalıştığından emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="99732-201">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="99732-202">Çeşitli tarayıcılarda Gözat `https://<your.custom.domain>` web uygulamanıza hizmet etmediğini görmek için.</span><span class="sxs-lookup"><span data-stu-id="99732-202">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span></span>

![Azure App portalında gezinme](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="99732-204">Web uygulamanız varsa doğrulama hatalarını sertifika, büyük olasılıkla otomatik olarak imzalanan bir sertifika kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="99732-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="99732-205">Bu durumda değilse, PFX dosyası, sertifika verirken Ara sertifikalara sol.</span><span class="sxs-lookup"><span data-stu-id="99732-205">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="99732-206">HTTPS zorlama</span><span class="sxs-lookup"><span data-stu-id="99732-206">Enforce HTTPS</span></span>

<span data-ttu-id="99732-207">Uygulama hizmeti yapar *değil* herkes, HTTP kullanarak web uygulamanızı erişebilmesi için HTTPS zorla.</span><span class="sxs-lookup"><span data-stu-id="99732-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="99732-208">Web uygulamanız için HTTPS zorlamak için bir yeniden yazma kuralı tanımlamak _web.config_ web uygulamanız için dosya.</span><span class="sxs-lookup"><span data-stu-id="99732-208">To enforce HTTPS for your web app, define a rewrite rule in the _web.config_ file for your web app.</span></span> <span data-ttu-id="99732-209">Uygulama hizmeti, web uygulamanızın dili çerçevesini bağımsız olarak bu dosyayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="99732-209">App Service uses this file, regardless of the language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="99732-210">Dile özgü yeniden yönlendirme istekleri yoktur.</span><span class="sxs-lookup"><span data-stu-id="99732-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="99732-211">ASP.NET MVC kullanabileceğiniz [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) yeniden yazma kuralı yerine filtre _web.config_.</span><span class="sxs-lookup"><span data-stu-id="99732-211">ASP.NET MVC can use the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of the rewrite rule in _web.config_.</span></span>

<span data-ttu-id="99732-212">.NET Geliştirici değilseniz, bu dosya ile görece tanıyor olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="99732-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="99732-213">Çözümünüzü kök dizininde değil.</span><span class="sxs-lookup"><span data-stu-id="99732-213">It is in the root of your solution.</span></span>

<span data-ttu-id="99732-214">Alternatif olarak, PHP, Node.js, Python veya Java ile ortaya çıkarsa, size bu dosyayı sizin adınıza App Service içinde oluşturulan bir fırsat yok.</span><span class="sxs-lookup"><span data-stu-id="99732-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="99732-215">Kısmındaki yönergeleri izleyerek, web uygulamanızın FTP uç noktasını bağlamak [FTP/S kullanarak Azure App Service için uygulamanızı dağıtma](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="99732-215">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="99732-216">Bu dosyanın içinde bulunması _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="99732-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="99732-217">Değilse, oluşturmak bir _web.config_ aşağıdaki XML ile bu klasörde dosya:</span><span class="sxs-lookup"><span data-stu-id="99732-217">If not, create a _web.config_ file in this folder with the following XML:</span></span>

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="99732-218">Mevcut bir _web.config_ dosya, bütün kopyası `<rule>` öğesine, _web.config_'s `configuration/system.webServer/rewrite/rules` öğesi.</span><span class="sxs-lookup"><span data-stu-id="99732-218">For an existing _web.config_ file, copy the entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="99732-219">Varsa diğer `<rule>` öğelerinde, _web.config_, kopyalanan yerleştirin `<rule>` öğeden önce diğer `<rule>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="99732-219">If there are other `<rule>` elements in your _web.config_, place the copied `<rule>` element before the other `<rule>` elements.</span></span>

<span data-ttu-id="99732-220">Kullanıcı, web uygulamanızın HTTP isteği yaptığında bu kural HTTPS protokolü için bir HTTP 301 (kalıcı yeniden yönlendirme) döndürür.</span><span class="sxs-lookup"><span data-stu-id="99732-220">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="99732-221">Örneğin, gelen yönlendirir `http://contoso.com` için `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="99732-221">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

<span data-ttu-id="99732-222">IIS URL yeniden yazma modülü hakkında daha fazla bilgi için bkz: [URL yeniden yazma](http://www.iis.net/downloads/microsoft/url-rewrite) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="99732-222">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="99732-223">Linux üzerinde Web uygulamaları için HTTPS zorla</span><span class="sxs-lookup"><span data-stu-id="99732-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="99732-224">Uygulama hizmeti Linux'ta mu *değil* herkes, HTTP kullanarak web uygulamanızı erişebilmesi için HTTPS zorla.</span><span class="sxs-lookup"><span data-stu-id="99732-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="99732-225">Web uygulamanız için HTTPS zorlamak için bir yeniden yazma kuralı tanımlamak _.htaccess_ web uygulamanız için dosya.</span><span class="sxs-lookup"><span data-stu-id="99732-225">To enforce HTTPS for your web app, define a rewrite rule in the _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="99732-226">Kısmındaki yönergeleri izleyerek, web uygulamanızın FTP uç noktasını bağlamak [FTP/S kullanarak Azure App Service için uygulamanızı dağıtma](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="99732-226">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="99732-227">İçinde _/home/site/wwwroot_, oluşturma bir _.htaccess_ aşağıdaki kod ile dosya:</span><span class="sxs-lookup"><span data-stu-id="99732-227">In _/home/site/wwwroot_, create an _.htaccess_ file with the following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="99732-228">Kullanıcı, web uygulamanızın HTTP isteği yaptığında bu kural HTTPS protokolü için bir HTTP 301 (kalıcı yeniden yönlendirme) döndürür.</span><span class="sxs-lookup"><span data-stu-id="99732-228">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="99732-229">Örneğin, gelen yönlendirir `http://contoso.com` için `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="99732-229">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="99732-230">Komut dosyalarıyla otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="99732-230">Automate with scripts</span></span>

<span data-ttu-id="99732-231">Kullanarak, kodlarıyla web uygulamanız için SSL bağlamaları otomatikleştirebilirsiniz [Azure CLI](/cli/azure/install-azure-cli) veya [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="99732-231">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="99732-232">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="99732-232">Azure CLI</span></span>

<span data-ttu-id="99732-233">Aşağıdaki komutu bir dışarı aktarılan PFX dosyasını yükler ve parmak izi alır.</span><span class="sxs-lookup"><span data-stu-id="99732-233">The following command uploads an exported PFX file and gets the thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="99732-234">Aşağıdaki komut, parmak izini önceki komutu kullanarak bir SNI tabanlı SSL bağlama ekler.</span><span class="sxs-lookup"><span data-stu-id="99732-234">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="99732-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="99732-235">Azure PowerShell</span></span>

<span data-ttu-id="99732-236">Aşağıdaki komutu, dışa aktarılan bir PFX dosyası yükler ve SNI tabanlı SSL bağlaması ekler.</span><span class="sxs-lookup"><span data-stu-id="99732-236">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="99732-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99732-237">Next steps</span></span>

<span data-ttu-id="99732-238">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="99732-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="99732-239">Uygulamanızın fiyatlandırma katmanı yükseltme</span><span class="sxs-lookup"><span data-stu-id="99732-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="99732-240">Özel SSL sertifikanızı uygulama hizmetine bağlama</span><span class="sxs-lookup"><span data-stu-id="99732-240">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="99732-241">Uygulamanız için HTTPS zorla</span><span class="sxs-lookup"><span data-stu-id="99732-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="99732-242">SSL sertifikası bağlaması kodlarıyla otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="99732-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="99732-243">Azure içerik teslim ağı kullanmayı öğrenmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="99732-243">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="99732-244">İçerik teslim ağı (CDN) için bir Azure uygulama hizmeti Ekle</span><span class="sxs-lookup"><span data-stu-id="99732-244">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)

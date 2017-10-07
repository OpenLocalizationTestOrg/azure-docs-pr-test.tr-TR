---
title: "aaaAdd bir SSL sertifikası tooyour Azure App Service uygulaması | Microsoft Docs"
description: "Nasıl tooadd bir SSL sertifikası tooyour App Service uygulaması hakkında bilgi edinin."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="c54c8-103">Azure App Service için SSL Sertifikası Satın Alma ve Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c54c8-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="c54c8-104">Bu öğreticide, web uygulamanız için bir SSL sertifikası satın alarak güvenliğini,  **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, güvenli bir şekilde de depolamak [Azure anahtar kasası](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)ve bunu ilişkilendirme özel bir etki alanı ile.</span><span class="sxs-lookup"><span data-stu-id="c54c8-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-tooazure"></a><span data-ttu-id="c54c8-105">1. adım - tooAzure günlüğünde</span><span class="sxs-lookup"><span data-stu-id="c54c8-105">Step 1 - Log in tooAzure</span></span>

<span data-ttu-id="c54c8-106">İçinde toohello http://portal.azure.com Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="c54c8-106">Log in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="c54c8-107">2. adım - bir SSL sertifikası sipariş verin</span><span class="sxs-lookup"><span data-stu-id="c54c8-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="c54c8-108">Yeni bir oluşturarak bir SSL sertifikası sipariş yerleştirebilirsiniz [uygulama hizmet sertifikası](https://portal.azure.com/#create/Microsoft.SSL) hello içinde **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="c54c8-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In hello **Azure portal**.</span></span>

![Sertifika oluşturma](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="c54c8-110">Kolay bir girin **adı** hello girin ve için SSL sertifika **etki alanı adı**</span><span class="sxs-lookup"><span data-stu-id="c54c8-110">Enter a friendly **Name** for your SSL certificate and enter hello **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="c54c8-111">Bu, hello en kritik bölümleri hello satın alma işlemi biridir.</span><span class="sxs-lookup"><span data-stu-id="c54c8-111">This is one of hello most critical parts of hello purchase process.</span></span> <span data-ttu-id="c54c8-112">Bu sertifika ile tooprotect istediğiniz ana bilgisayar adı (özel etki alanı) düzeltmek emin tooenter olun.</span><span class="sxs-lookup"><span data-stu-id="c54c8-112">Make sure tooenter correct host name (custom domain) that you want tooprotect with this certificate.</span></span> <span data-ttu-id="c54c8-113">**SAĞLAMADIĞI** WWW ana bilgisayar adıyla hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c54c8-113">**DO NOT** append hello Host name with WWW.</span></span> 
>

<span data-ttu-id="c54c8-114">Seçin, **abonelik**, **kaynak grubu**, ve **sertifika SKU**</span><span class="sxs-lookup"><span data-stu-id="c54c8-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="c54c8-115">Uygulama Hizmeti sertifikaları yalnızca kullanılabilir hello içindeki diğer uygulama hizmetler tarafından aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="c54c8-115">App Service Certificates can only be used by other App Services within hello same subscription.</span></span>  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a><span data-ttu-id="c54c8-116">3. adım - Azure anahtar kasası hello sertifika deposu</span><span class="sxs-lookup"><span data-stu-id="c54c8-116">Step 3 - Store hello certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="c54c8-117">[Anahtar kasası](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) şifreleme anahtarları ve gizli anahtarları bulut uygulamalar ve hizmetler tarafından kullanılan korumaya yardımcı olan bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="c54c8-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="c54c8-118">Merhaba SSL sertifikası satın alma işlemi tamamlandıktan sonra tooopen gerekir [uygulama hizmeti sertifikaları](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) kaynak dikey.</span><span class="sxs-lookup"><span data-stu-id="c54c8-118">Once hello SSL Certificate purchase is complete, you need tooopen [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![içinde KV hazır toostore görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="c54c8-120">Sertifika durumu olduğunu fark edeceksiniz **"Bekleyen verme"** birkaç adım olduğundan bu sertifikayı kullanarak başlamadan önce toocomplete gerekir.</span><span class="sxs-lookup"><span data-stu-id="c54c8-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need toocomplete before you can start using this certificate.</span></span>

<span data-ttu-id="c54c8-121">' I tıklatın **sertifika Yapılandırması** sertifika özellikleri dikey penceresinde ve tıklayarak içinde **adım 1: depolama** toostore Azure anahtar Kasası'nda bu sertifika.</span><span class="sxs-lookup"><span data-stu-id="c54c8-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** toostore this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="c54c8-122">Gelen **anahtar kasası durumu** dikey penceresinde tıklatın **anahtar kasası deposu** toochoose var olan bir anahtar kasası toostore bu sertifikayı **veya oluşturma yeni anahtar kasası** toocreate yeni bir anahtar kasası aynı abonelik ve kaynak grubu içinde.</span><span class="sxs-lookup"><span data-stu-id="c54c8-122">From **Key Vault Status** Blade, click **Key Vault Repository** toochoose an existing Key Vault toostore this certificate **OR Create New Key Vault** toocreate new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="c54c8-123">Azure anahtar kasası bu sertifikayı depolamak için en düşük ücretler sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c54c8-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="c54c8-124">Daha fazla bilgi için bkz:  **[Azure anahtar kasası fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="c54c8-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="c54c8-125">Bu sertifikada hello anahtar kasası depo toostore seçtikten sonra hello **deposu** seçeneğini başarı göster.</span><span class="sxs-lookup"><span data-stu-id="c54c8-125">Once you have selected hello Key Vault Repository toostore this certificate in, hello **Store** option should show success.</span></span>

![KV deposu başarılı bir görüntüsünü Ekle](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a><span data-ttu-id="c54c8-127">Adım 4 - hello etki alanı sahipliğini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="c54c8-127">Step 4 - Verify hello Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="c54c8-128">Uygulama Hizmeti sertifikaları tarafından desteklenen etki alanı doğrulama üç tür vardır: etki alanı, posta, el ile doğrulama.</span><span class="sxs-lookup"><span data-stu-id="c54c8-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="c54c8-129">Bunlar daha ayrıntılı olarak hello açıklanacak [bölüm Gelişmiş](#advanced).</span><span class="sxs-lookup"><span data-stu-id="c54c8-129">These are explained in more details in hello [Advanced section](#advanced).</span></span>

<span data-ttu-id="c54c8-130">Gelen aynı hello **sertifika Yapılandırması** dikey adım 3'te kullanılan, tıklatın **2. adım: doğrulayın**.</span><span class="sxs-lookup"><span data-stu-id="c54c8-130">From hello same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="c54c8-131">**Etki alanı doğrulama** bu hello en kolay bir işlemdir **yalnızca IF** elinizde  **[özel etki alanınızı Azure App hizmetinden satın.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="c54c8-131">**Domain Verification** This is hello most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="c54c8-132">Tıklayın **doğrula** toocomplete bu adımı düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c54c8-132">Click on **Verify** button toocomplete this step.</span></span>

![etki alanı doğrulama görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="c54c8-134">' I tıklattıktan sonra **doğrulayın**, hello kullanın **yenileme** hello kadar düğme **doğrulayın** seçeneğini başarı göster.</span><span class="sxs-lookup"><span data-stu-id="c54c8-134">After clicking **Verify**, use hello **Refresh** button until hello **Verify** option should show success.</span></span>

![INSERT görüntüsü KV başarılı doğrulayın](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a><span data-ttu-id="c54c8-136">5. adım - sertifika tooApp Service uygulaması atayın</span><span class="sxs-lookup"><span data-stu-id="c54c8-136">Step 5 - Assign Certificate tooApp Service App</span></span>

> [!NOTE]
> <span data-ttu-id="c54c8-137">Bu bölümde Hello adımları gerçekleştirmeden önce bir özel etki alanı adı uygulamanızla ilişkili sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c54c8-137">Before performing hello steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="c54c8-138">Daha fazla bilgi için bkz:  **[bir web uygulaması için bir özel etki alanı adı yapılandırma.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="c54c8-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="c54c8-139">Merhaba,  **[Azure portal](https://portal.azure.com/)**, hello tıklatın **uygulama hizmeti** hello sayfasının hello soldaki seçeneği.</span><span class="sxs-lookup"><span data-stu-id="c54c8-139">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="c54c8-140">Merhaba adını tıklatın, uygulama toowhich bu sertifikayı tooassign istiyor.</span><span class="sxs-lookup"><span data-stu-id="c54c8-140">Click hello name of your app toowhich you want tooassign this certificate.</span></span>

<span data-ttu-id="c54c8-141">Merhaba, **ayarları**, tıklatın **SSL sertifikalarını**.</span><span class="sxs-lookup"><span data-stu-id="c54c8-141">In hello **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="c54c8-142">Tıklatın **alma uygulaması hizmet sertifikası** ve yalnızca satın select hello sertifikası.</span><span class="sxs-lookup"><span data-stu-id="c54c8-142">Click **Import App Service Certificate** and select hello certificate that you just purchased.</span></span>

![Sertifika İçeri Aktar görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="c54c8-144">Merhaba, **ssl bağlamaları** tıklatın bölümünde **bağlamaları Ekle**, SSL ile Merhaba bırakmalar tooselect hello etki alanı adı toosecure kullanın ve sertifika toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c54c8-144">In hello **ssl bindings** section Click on **Add bindings**, and use hello dropdowns tooselect hello domain name toosecure with SSL, and hello certificate toouse.</span></span> <span data-ttu-id="c54c8-145">Ayrıca seçebilirsiniz olup olmadığını toouse  **[sunucu adı göstergesi (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  veya IP tabanlı SSL.</span><span class="sxs-lookup"><span data-stu-id="c54c8-145">You may also select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![SSL bağlamaları görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="c54c8-147">Tıklatın **bağlaması Ekle** toosave hello değişiklikleri ve SSL'yi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c54c8-147">Click **Add Binding** toosave hello changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="c54c8-148">Seçtiyseniz **IP tabanlı SSL** ve özel etki alanınızı bir A kaydı kullanılarak yapılandırılır, hello aşağıdaki ek adımları gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c54c8-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps.</span></span> <span data-ttu-id="c54c8-149">Bunlar daha ayrıntılı olarak hello açıklanacak [bölüm Gelişmiş](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="c54c8-149">These are explained in more details in hello [Advanced section](#Advanced).</span></span>

<span data-ttu-id="c54c8-150">Bu noktada, mümkün toovisit uygulamasını kullanarak olmalıdır `HTTPS://` yerine `HTTP://` sertifika hello tooverify doğru şekilde yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="c54c8-150">At this point, you should be able toovisit your app using `HTTPS://` instead of `HTTP://` tooverify that hello certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="c54c8-151">Adım 6 - yönetim görevleri</span><span class="sxs-lookup"><span data-stu-id="c54c8-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="c54c8-152">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c54c8-152">Azure CLI</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a><span data-ttu-id="c54c8-153">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c54c8-153">PowerShell</span></span>

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a><span data-ttu-id="c54c8-154">Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="c54c8-154">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="c54c8-155">Etki alanı sahipliğini doğrulama</span><span class="sxs-lookup"><span data-stu-id="c54c8-155">Verifying Domain Ownership</span></span>

<span data-ttu-id="c54c8-156">Uygulama Hizmeti sertifikaları tarafından desteklenen etki alanı doğrulama daha fazla iki tür vardır: posta ve el ile doğrulama.</span><span class="sxs-lookup"><span data-stu-id="c54c8-156">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="c54c8-157">Posta doğrulama</span><span class="sxs-lookup"><span data-stu-id="c54c8-157">Mail Verification</span></span>

<span data-ttu-id="c54c8-158">E-posta adresleri bu özel etki alanı ile ilişkili toohello doğrulama e-posta zaten gönderildi.</span><span class="sxs-lookup"><span data-stu-id="c54c8-158">Verification email has already been sent toohello Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="c54c8-159">toocomplete hello e-posta doğrulama adımı, hello e-posta açın ve hello doğrulama bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c54c8-159">toocomplete hello Email verification step, open hello email and click hello verification link.</span></span>

![e-posta doğrulama görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="c54c8-161">Tooresend hello doğrulama e-posta gerekiyorsa, hello tıklatın **yeniden Gönder'e-posta** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c54c8-161">If you need tooresend hello verification email, click hello **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="c54c8-162">El ile doğrulama</span><span class="sxs-lookup"><span data-stu-id="c54c8-162">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c54c8-163">HTML Web sayfası Doğrulama (yalnızca standart sertifika SKU çalışır)</span><span class="sxs-lookup"><span data-stu-id="c54c8-163">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="c54c8-164">Adlı bir HTML dosyası oluşturmak **"starfield.html"**</span><span class="sxs-lookup"><span data-stu-id="c54c8-164">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="c54c8-165">Bu dosyanın hello tam etki alanı doğrulama belirteci hello adını içerik olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c54c8-165">Content of this file should be hello exact name of hello Domain Verification Token.</span></span> <span data-ttu-id="c54c8-166">(Etki alanı doğrulama durumu dikey penceresinde hello hello belirteci kopyalayabilirsiniz)</span><span class="sxs-lookup"><span data-stu-id="c54c8-166">(You can copy hello token from hello Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="c54c8-167">Merhaba kökündeki etki alanınızı barındırmaya hello web sunucusunun bu dosyayı karşıya yükleme`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="c54c8-167">Upload this file at hello root of hello web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="c54c8-168">Tıklatın **yenileme** doğrulama tamamlandıktan sonra tooupdate hello sertifika durumu.</span><span class="sxs-lookup"><span data-stu-id="c54c8-168">Click **Refresh** tooupdate hello certificate status after verification is completed.</span></span> <span data-ttu-id="c54c8-169">Doğrulama toocomplete için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c54c8-169">It might take few minutes for verification toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="c54c8-170">Terminal kullanarak bir doğrulama `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello yanıt hello içermelidir `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="c54c8-170">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello response should contain hello `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="c54c8-171">DNS TXT kaydını doğrulama</span><span class="sxs-lookup"><span data-stu-id="c54c8-171">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="c54c8-172">DNS Yöneticisi'ni kullanarak, hello üzerinde bir TXT kaydını oluşturmak `@` değer eşit toohello etki alanı doğrulama belirteci ile alt etki alanı.</span><span class="sxs-lookup"><span data-stu-id="c54c8-172">Using your DNS manager, Create a TXT record on hello `@` subdomain with value equal toohello Domain Verification Token.</span></span>
1. <span data-ttu-id="c54c8-173">Tıklatın **"Yenile"** tooupdate hello doğrulama tamamlandıktan sonra sertifika durumu.</span><span class="sxs-lookup"><span data-stu-id="c54c8-173">Click **“Refresh”** tooupdate hello Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="c54c8-174">Bilgisayarda toocreate TXT kaydı gerektiren `@.<domain>` değerle `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="c54c8-174">You need toocreate a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-tooapp-service-app"></a><span data-ttu-id="c54c8-175">Sertifika tooApp Service uygulaması atayın</span><span class="sxs-lookup"><span data-stu-id="c54c8-175">Assign Certificate tooApp Service App</span></span>

<span data-ttu-id="c54c8-176">Seçtiyseniz **IP tabanlı SSL** ve özel etki alanınızı bir A kaydı kullanılarak yapılandırılır, hello aşağıdaki ek adımları gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="c54c8-176">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps:</span></span>

<span data-ttu-id="c54c8-177">Yapılandırdıktan sonra bir IP temelli SSL bağlaması, ayrılmış bir IP adresi tooyour uygulama atanır.</span><span class="sxs-lookup"><span data-stu-id="c54c8-177">After you have configured an IP based SSL binding, a dedicated IP address is assigned tooyour app.</span></span> <span data-ttu-id="c54c8-178">Bu IP adresi üzerinde hello bulabilirsiniz **özel etki alanı** hello üzerinde doğru uygulamanızın ayarlar altında sayfa **ana bilgisayar adları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c54c8-178">You can find this IP address on hello **Custom domain** page under settings of your app, right above hello **Hostnames** section.</span></span> <span data-ttu-id="c54c8-179">Olarak listelenen **dış IP adresi**</span><span class="sxs-lookup"><span data-stu-id="c54c8-179">It is listed as **External IP Address**</span></span>

![IP SSL görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="c54c8-181">Bu IP adresi hello sanal IP adresi tooconfigure hello A kaydı etki alanınız için daha önce kullanılan farklı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c54c8-181">Note that this IP address is different than hello virtual IP address used previously tooconfigure hello A record for your domain.</span></span> <span data-ttu-id="c54c8-182">Yapılandırdıysanız SNI tabanlı SSL veya olmayan toouse toouse SSL yapılandırılmış, bu giriş için bir adresinin.</span><span class="sxs-lookup"><span data-stu-id="c54c8-182">If you are configured toouse SNI based SSL, or are not configured toouse SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="c54c8-183">Etki alanı adı kayıt şirketiniz tarafından sağlanan hello Araçları'nı kullanarak hello hello önceki adımdaki, özel etki alanı adı toopoint toohello IP adresi için bir kayıt değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c54c8-183">Using hello tools provided by your domain name registrar, modify hello A record for your custom domain name toopoint toohello IP address from hello previous step.</span></span>

## <a name="rekey-and-sync-hello-certificate"></a><span data-ttu-id="c54c8-184">Yeniden anahtarlama ve eşitleme hello sertifika</span><span class="sxs-lookup"><span data-stu-id="c54c8-184">Rekey and Sync hello Certificate</span></span>

<span data-ttu-id="c54c8-185">Sertifikanızı erişiminizi tooRekey gerekirse seçin **anahtar yenileme ve eşitleme** gelen seçeneği **sertifika özellikleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="c54c8-185">If you ever need tooRekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="c54c8-186">Tıklatın **anahtar yenileme** düğmesini tooinitiate hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="c54c8-186">Click **Rekey** Button tooinitiate hello process.</span></span> <span data-ttu-id="c54c8-187">Bu işlem, 1-10 dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="c54c8-187">This process can take 1-10 minutes toocomplete.</span></span>

![anahtar yenileme SSL görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="c54c8-189">Sertifikanızı yeniden anahtarlama hello sertifika hello sertifika yetkilisi tarafından verilen yeni bir sertifika ile yapar.</span><span class="sxs-lookup"><span data-stu-id="c54c8-189">Rekeying your certificate rolls hello certificate with a new certificate issued from hello certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c54c8-190">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c54c8-190">Next Steps</span></span>

* [<span data-ttu-id="c54c8-191">Bir içerik teslim ağı Ekle</span><span class="sxs-lookup"><span data-stu-id="c54c8-191">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)
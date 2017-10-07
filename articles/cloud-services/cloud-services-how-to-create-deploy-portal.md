---
title: "aaaHow toocreate ve bir bulut hizmeti dağıtma | Microsoft Docs"
description: "Bilgi nasıl toocreate ve hello Azure portal kullanarak bir bulut hizmeti dağıtın."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a><span data-ttu-id="eca15-103">Nasıl toocreate ve bir bulut hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="eca15-103">How toocreate and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eca15-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="eca15-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="eca15-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="eca15-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="eca15-106">Hello Azure portal toocreate sizin için iki yöntem sağlar ve bir bulut hizmeti dağıtma: *hızlı Oluştur* ve *özel Oluştur*.</span><span class="sxs-lookup"><span data-stu-id="eca15-106">hello Azure portal provides two ways for you toocreate and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="eca15-107">Bu makalede nasıl toouse hızlı oluşturma yöntemini toocreate yeni bir bulut hizmeti hello ve ardından açıklanmaktadır **karşıya** tooupload ve Azure bulut hizmet paketinde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="eca15-107">This article explains how toouse hello Quick Create method toocreate a new cloud service and then use **Upload** tooupload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="eca15-108">Bu yöntemi kullandığınızda, hello Azure portal, Git gibi tüm gereksinimleri tamamlamak için kullanılabilir uygun bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="eca15-108">When you use this method, hello Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="eca15-109">Bulut hizmet oluşturduğunuzda hazır toodeploy değilseniz, hem hello yapabilirsiniz aynı anda özel Oluştur kullanma.</span><span class="sxs-lookup"><span data-stu-id="eca15-109">If you're ready toodeploy your cloud service when you create it, you can do both at hello same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="eca15-110">Bulut hizmeti Visual Studio Team Services (VSTS) gelen toopublish planlıyorsanız, hızlı Oluştur'u kullanın ve ardından VSTS yayımlama hello Azure hızlı başlangıç veya hello panosundan ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="eca15-110">If you plan toopublish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from hello Azure Quickstart or hello dashboard.</span></span> <span data-ttu-id="eca15-111">Daha fazla bilgi için bkz: [kesintisiz teslim tooAzure kullanarak Visual Studio Team Services tarafından][TFSTutorialForCloudService], veya Merhaba yardımcı **Hızlı Başlangıç** sayfası.</span><span class="sxs-lookup"><span data-stu-id="eca15-111">For more information, see [Continuous Delivery tooAzure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for hello **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="eca15-112">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="eca15-112">Concepts</span></span>
<span data-ttu-id="eca15-113">Gerekli toodeploy bir uygulamayı Azure bulut hizmeti olarak üç bileşeni vardır:</span><span class="sxs-lookup"><span data-stu-id="eca15-113">Three components are required toodeploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="eca15-114">**Hizmet tanımı**</span><span class="sxs-lookup"><span data-stu-id="eca15-114">**Service Definition**</span></span>  
  <span data-ttu-id="eca15-115">Merhaba bulut Hizmet tanım dosyası (.csdef) rollerini hello sayısı dahil olmak üzere hello hizmet modeli tanımlar.</span><span class="sxs-lookup"><span data-stu-id="eca15-115">hello cloud service definition file (.csdef) defines hello service model, including hello number of roles.</span></span>
* <span data-ttu-id="eca15-116">**Hizmet yapılandırması**</span><span class="sxs-lookup"><span data-stu-id="eca15-116">**Service Configuration**</span></span>  
  <span data-ttu-id="eca15-117">Merhaba bulut hizmet yapılandırma dosyasının (.cscfg) hello bulut hizmeti ve bireysel rolleri rol örnekleri hello sayısı dahil olmak üzere, yapılandırma ayarlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="eca15-117">hello cloud service configuration file (.cscfg) provides configuration settings for hello cloud service and individual roles, including hello number of role instances.</span></span>
* <span data-ttu-id="eca15-118">**Hizmet paketi**</span><span class="sxs-lookup"><span data-stu-id="eca15-118">**Service Package**</span></span>  
  <span data-ttu-id="eca15-119">Merhaba hizmet paketi (.cspkg) hello uygulama kodu ve yapılandırmaları ve hello hizmet tanımı dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="eca15-119">hello service package (.cspkg) contains hello application code and configurations and hello service definition file.</span></span>

<span data-ttu-id="eca15-120">Bunlar hakkında daha fazla bilgi edinmek ve nasıl toocreate bir paket [burada](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="eca15-120">You can learn more about these and how toocreate a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="eca15-121">Uygulamanızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="eca15-121">Prepare your app</span></span>
<span data-ttu-id="eca15-122">Bir bulut hizmeti dağıtmadan önce uygulama kodunuz ve bir bulut hizmet yapılandırma dosyasının (.cscfg) hello bulut hizmet paketi (.cspkg) oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eca15-122">Before you can deploy a cloud service, you must create hello cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="eca15-123">Hello Azure SDK'sı, bu gerekli dağıtım dosyaları hazırlamak için araçlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="eca15-123">hello Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="eca15-124">Merhaba SDK hello yükleyebilirsiniz [Azure indirmeleri](https://azure.microsoft.com/downloads/) sayfa olan uygulama kodunuz toodevelop tercih hello dilde.</span><span class="sxs-lookup"><span data-stu-id="eca15-124">You can install hello SDK from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page, in hello language in which you prefer toodevelop your application code.</span></span>

<span data-ttu-id="eca15-125">Bir hizmet paketi vermeden önce üç bulut hizmeti özellikleri özel yapılandırmalar gerektirir:</span><span class="sxs-lookup"><span data-stu-id="eca15-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="eca15-126">Veri şifreleme için Güvenli Yuva Katmanı (SSL) kullanan bir bulut hizmeti toodeploy istiyorsanız [uygulamanızı yapılandırma](cloud-services-configure-ssl-certificate-portal.md#modify) SSL için.</span><span class="sxs-lookup"><span data-stu-id="eca15-126">If you want toodeploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="eca15-127">Tooconfigure Uzak Masaüstü bağlantıları toorole örnekleri, isterseniz [hello rollerini yapılandırma](cloud-services-role-enable-remote-desktop-new-portal.md) Uzak Masaüstü için.</span><span class="sxs-lookup"><span data-stu-id="eca15-127">If you want tooconfigure Remote Desktop connections toorole instances, [configure hello roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="eca15-128">Tooconfigure ayrıntılı bulut hizmetiniz için izleme istiyorsanız Azure tanılama hello bulut hizmeti için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="eca15-128">If you want tooconfigure verbose monitoring for your cloud service, enable Azure Diagnostics for hello cloud service.</span></span> <span data-ttu-id="eca15-129">*Minimum izleme* (Merhaba varsayılan düzeyi izleme) hello ana bilgisayar işletim sistemlerinden rol örnekleri (sanal makineler) için toplanan performans sayaçlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="eca15-129">*Minimal monitoring* (hello default monitoring level) uses performance counters gathered from hello host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="eca15-130">*Ayrıntılı izleme* hello rol örnekleri tooenable yakın analizini uygulama işlemi sırasında oluşabilecek sorunları içinde performans verilerine göre ek ölçümleri toplar.</span><span class="sxs-lookup"><span data-stu-id="eca15-130">*Verbose monitoring* gathers additional metrics based on performance data within hello role instances tooenable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="eca15-131">toofind nasıl tooenable Azure tanılama Bkz [Azure tanılama etkinleştirme](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="eca15-131">toofind out how tooenable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="eca15-132">toocreate web rolleri veya çalışan rolleri dağıtımlarına sahip bulut hizmeti, şunları yapmalısınız [hello hizmet paketi oluşturma](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="eca15-132">toocreate a cloud service with deployments of web roles or worker roles, you must [create hello service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eca15-133">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="eca15-133">Before you begin</span></span>
* <span data-ttu-id="eca15-134">Hello Azure SDK'sı yüklemediyseniz tıklatın **Azure SDK Yükle** tooopen hello [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/)ve hello SDK, tercih ettiğiniz toodevelop kodunuzu hello dil için karşıdan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="eca15-134">If you haven't installed hello Azure SDK, click **Install Azure SDK** tooopen hello [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download hello SDK for hello language in which you prefer toodevelop your code.</span></span> <span data-ttu-id="eca15-135">(Bu bir fırsat toodo sahip olacaksınız daha sonra.)</span><span class="sxs-lookup"><span data-stu-id="eca15-135">(You'll have an opportunity toodo this later.)</span></span>
* <span data-ttu-id="eca15-136">Tüm rol örneklerinin bir sertifika gerektiriyorsa, hello sertifikaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eca15-136">If any role instances require a certificate, create hello certificates.</span></span> <span data-ttu-id="eca15-137">Bulut Hizmetleri bir .pfx dosyası özel bir anahtarla gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eca15-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="eca15-138">Merhaba bulut hizmeti oluşturup gibi hello sertifikaları tooAzure karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eca15-138">You can upload hello certificates tooAzure as you create and deploy hello cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="eca15-139">Oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="eca15-139">Create and deploy</span></span>
1. <span data-ttu-id="eca15-140">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="eca15-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="eca15-141">Tıklatın **yeni > işlem**, tooand tıklatın kaydırarak **bulut hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="eca15-141">Click **New > Compute**, and then scroll down tooand click **Cloud Service**.</span></span>

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="eca15-143">Merhaba yeni içinde **bulut hizmeti** dikey penceresinde hello için bir değer girin **DNS adı**.</span><span class="sxs-lookup"><span data-stu-id="eca15-143">In hello new **Cloud Service** blade, enter a value for hello **DNS name**.</span></span>
4. <span data-ttu-id="eca15-144">Yeni bir **kaynak grubu** veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="eca15-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="eca15-145">Bir **Konum** seçin.</span><span class="sxs-lookup"><span data-stu-id="eca15-145">Select a **Location**.</span></span>
6. <span data-ttu-id="eca15-146">Tıklatın **paket**.</span><span class="sxs-lookup"><span data-stu-id="eca15-146">Click **Package**.</span></span> <span data-ttu-id="eca15-147">Bu hello açar **bir paketi yükleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="eca15-147">This will open hello **Upload a package** blade.</span></span> <span data-ttu-id="eca15-148">Merhaba gerekli alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="eca15-148">Fill in hello required fields.</span></span> <span data-ttu-id="eca15-149">Rollerinizi hiçbirini tek bir örnek içeriyorsa, olun **bir veya daha fazla rol tek bir örnek içeriyorsa bile Dağıt** seçilir.</span><span class="sxs-lookup"><span data-stu-id="eca15-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="eca15-150">Olduğundan emin olun **Başlat dağıtım** seçilir.</span><span class="sxs-lookup"><span data-stu-id="eca15-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="eca15-151">Tıklatın **Tamam** hello kapatılacak **bir paketi yükleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="eca15-151">Click **OK** which will close hello **Upload a package** blade.</span></span>
9. <span data-ttu-id="eca15-152">Tüm sertifikaları tooadd yoksa tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="eca15-152">If you do not have any certificates tooadd, click **Create**.</span></span>

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="eca15-154">Bir sertifikayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="eca15-154">Upload a certificate</span></span>
<span data-ttu-id="eca15-155">Dağıtım paketi varsa [toouse sertifikaları yapılandırılmış](cloud-services-configure-ssl-certificate-portal.md#modify), hello sertifika şimdi karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eca15-155">If your deployment package was [configured toouse certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload hello certificate now.</span></span>

1. <span data-ttu-id="eca15-156">Seçin **sertifikaları**ve hello **eklemek sertifikaları** dikey penceresinde hello SSL sertifika .pfx dosyasını seçin ve ardından hello sağlayın **parola** hello sertifika için</span><span class="sxs-lookup"><span data-stu-id="eca15-156">Select **Certificates**, and on hello **Add certificates** blade, select hello SSL certificate .pfx file, and then provide hello **Password** for hello certificate,</span></span>
2. <span data-ttu-id="eca15-157">Tıklatın **Attach sertifika**ve ardından **Tamam** hello üzerinde **eklemek sertifikaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="eca15-157">Click **Attach certificate**, and then click **OK** on hello **Add certificates** blade.</span></span>
3. <span data-ttu-id="eca15-158">Tıklatın **oluşturma** hello üzerinde **bulut hizmeti** dikey.</span><span class="sxs-lookup"><span data-stu-id="eca15-158">Click **Create** on hello **Cloud Service** blade.</span></span> <span data-ttu-id="eca15-159">Merhaba dağıtım ulaşıldığında hello **hazır** durumu toohello sonraki adımlara geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eca15-159">When hello deployment has reached hello **Ready** status, you can proceed toohello next steps.</span></span>

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="eca15-161">Başarıyla tamamlandı, dağıtımı doğrulama</span><span class="sxs-lookup"><span data-stu-id="eca15-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="eca15-162">Merhaba bulut hizmet örneği'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="eca15-162">Click hello cloud service instance.</span></span>

    <span data-ttu-id="eca15-163">Merhaba durum hello hizmet olduğunu göstermelidir **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="eca15-163">hello status should show that hello service is **Running**.</span></span>
2. <span data-ttu-id="eca15-164">Altında **Essentials**, hello tıklatın **Site URL'si** bulut hizmeti bir web tarayıcısında tooopen.</span><span class="sxs-lookup"><span data-stu-id="eca15-164">Under **Essentials**, click hello **Site URL** tooopen your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="eca15-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eca15-166">Next steps</span></span>
* <span data-ttu-id="eca15-167">[Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eca15-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="eca15-168">Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eca15-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="eca15-169">[Bulut hizmetinizi yönetme](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eca15-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="eca15-170">Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eca15-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

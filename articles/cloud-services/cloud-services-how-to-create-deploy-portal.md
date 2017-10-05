---
title: "Oluşturma ve bir bulut hizmeti dağıtma | Microsoft Docs"
description: "Oluşturma ve Azure portalını kullanarak bir bulut hizmeti dağıtma hakkında bilgi edinin."
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
ms.openlocfilehash: e5ce666f1d826c7901c9fd5e7fafe6171139c3ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="5045d-103">Oluşturma ve bir bulut hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="5045d-103">How to create and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5045d-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="5045d-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="5045d-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="5045d-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="5045d-106">Azure Portalı'nı oluşturmak ve bir bulut hizmeti dağıtmak iki yol sunar: *hızlı Oluştur* ve *özel Oluştur*.</span><span class="sxs-lookup"><span data-stu-id="5045d-106">The Azure portal provides two ways for you to create and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="5045d-107">Bu makalede Hızlı oluşturma yönteminin yeni bir bulut hizmeti oluşturabilir ve daha sonra kullanmak için nasıl kullanılacağı açıklanmaktadır **karşıya** karşıya yükleyin ve Azure bulut hizmet paketinde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="5045d-107">This article explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="5045d-108">Bu yöntemi kullandığınızda, Azure portalında gittiğiniz gibi tüm gereksinimleri tamamlamak için kullanılabilir uygun bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="5045d-108">When you use this method, the Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="5045d-109">Oluşturduğunuzda, bulut hizmeti dağıtmak hazırsanız özel Oluştur kullanarak aynı anda hem de yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5045d-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="5045d-110">Bulut hizmeti Visual Studio Team Services (VSTS) gelen yayımlamayı düşünüyorsanız, hızlı Oluştur'u kullanın ve ardından Azure hızlı başlangıç veya panoyu VSTS yayımlama Ayarla.</span><span class="sxs-lookup"><span data-stu-id="5045d-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from the Azure Quickstart or the dashboard.</span></span> <span data-ttu-id="5045d-111">Daha fazla bilgi için bkz: [Azure kullanarak Visual Studio Team Services tarafından sürekli teslim][TFSTutorialForCloudService], veya Yardım için bkz: **Hızlı Başlangıç** sayfası.</span><span class="sxs-lookup"><span data-stu-id="5045d-111">For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for the **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="5045d-112">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="5045d-112">Concepts</span></span>
<span data-ttu-id="5045d-113">Üç bileşeni, Azure'daki bir bulut hizmeti olarak bir uygulamayı dağıtmak için gereklidir:</span><span class="sxs-lookup"><span data-stu-id="5045d-113">Three components are required to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="5045d-114">**Hizmet tanımı**</span><span class="sxs-lookup"><span data-stu-id="5045d-114">**Service Definition**</span></span>  
  <span data-ttu-id="5045d-115">Bulut Hizmet tanım dosyası (.csdef) rol sayısı dahil olmak üzere hizmet modeli tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5045d-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="5045d-116">**Hizmet yapılandırması**</span><span class="sxs-lookup"><span data-stu-id="5045d-116">**Service Configuration**</span></span>  
  <span data-ttu-id="5045d-117">Bulut hizmet yapılandırma dosyasının (.cscfg) rol örneği sayısı dahil olmak üzere, hizmet ve bireysel rolleri bulut için yapılandırma ayarlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5045d-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="5045d-118">**Hizmet paketi**</span><span class="sxs-lookup"><span data-stu-id="5045d-118">**Service Package**</span></span>  
  <span data-ttu-id="5045d-119">Hizmet Paketi (.cspkg) uygulama kodu ve yapılandırmaları ve hizmet tanımı dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="5045d-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="5045d-120">Bunlar ve bir paketinin nasıl oluşturulacağı hakkında daha fazla bilgiyi [burada](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="5045d-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="5045d-121">Uygulamanızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="5045d-121">Prepare your app</span></span>
<span data-ttu-id="5045d-122">Bir bulut hizmeti dağıtmadan önce bulut hizmet paketi (.cspkg) uygulama kodunuz ve bir bulut hizmet yapılandırma dosyasının (.cscfg) oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5045d-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="5045d-123">Azure SDK'sı, bu gerekli dağıtım dosyaları hazırlamak için araçlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="5045d-123">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="5045d-124">SDK'dan gelen yükleyebilirsiniz [Azure indirmeleri](https://azure.microsoft.com/downloads/) sayfasında, tercih ettiğiniz uygulama kodunuz geliştirmek dili.</span><span class="sxs-lookup"><span data-stu-id="5045d-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="5045d-125">Bir hizmet paketi vermeden önce üç bulut hizmeti özellikleri özel yapılandırmalar gerektirir:</span><span class="sxs-lookup"><span data-stu-id="5045d-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="5045d-126">Veri şifreleme için Güvenli Yuva Katmanı (SSL) kullanan bir bulut hizmet dağıtmak istiyorsanız [uygulamanızı yapılandırma](cloud-services-configure-ssl-certificate-portal.md#modify) SSL için.</span><span class="sxs-lookup"><span data-stu-id="5045d-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="5045d-127">Rol örneği Uzak Masaüstü bağlantılarını yapılandırmak istiyorsanız, [rollerini yapılandırma](cloud-services-role-enable-remote-desktop-new-portal.md) Uzak Masaüstü için.</span><span class="sxs-lookup"><span data-stu-id="5045d-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="5045d-128">Ayrıntılı bulut hizmetiniz için izleme yapılandırmak istiyorsanız, Azure tanılama bulut hizmeti için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5045d-128">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="5045d-129">*Minimum izleme* rol örnekleri (sanal makineler) için ana bilgisayar işletim sistemlerden topladığı performans sayaçlarını (varsayılan düzeyi izleme) kullanır.</span><span class="sxs-lookup"><span data-stu-id="5045d-129">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="5045d-130">*Ayrıntılı izleme* uygulama işlem sırasında oluşan sorunları daha yakından Analizine olanak sağlamak için rol örnekleri içinde performans verilerine göre ek ölçümleri toplar.</span><span class="sxs-lookup"><span data-stu-id="5045d-130">*Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="5045d-131">Azure Tanılama'yı etkinleştirme konusunda bilgi edinmek için bkz: [Azure tanılama etkinleştirme](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5045d-131">To find out how to enable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="5045d-132">Web rolleri veya çalışan rolleri dağıtımlarında bir bulut hizmeti oluşturmak için şunları yapmanız gerekir [hizmet paketi oluşturma](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="5045d-132">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5045d-133">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5045d-133">Before you begin</span></span>
* <span data-ttu-id="5045d-134">Azure SDK'sını yüklemediyseniz tıklatın **Azure SDK Yükle** açmak için [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/)ve ardından, tercih ettiğiniz kodunuzu geliştirmek dil için SDK'sını indirin.</span><span class="sxs-lookup"><span data-stu-id="5045d-134">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="5045d-135">(Daha sonra bunu fırsatına sahip olacaksınız.)</span><span class="sxs-lookup"><span data-stu-id="5045d-135">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="5045d-136">Tüm rol örneklerinin bir sertifika gerektiriyorsa, sertifikaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5045d-136">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="5045d-137">Bulut Hizmetleri bir .pfx dosyası özel bir anahtarla gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5045d-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="5045d-138">Oluşturur ve bulut hizmeti dağıtmak için Azure sertifikaları karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5045d-138">You can upload the certificates to Azure as you create and deploy the cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="5045d-139">Oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="5045d-139">Create and deploy</span></span>
1. <span data-ttu-id="5045d-140">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5045d-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5045d-141">Tıklatın **yeni > işlem**, tıklatın ve sonra aşağı kaydırarak **bulut hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="5045d-141">Click **New > Compute**, and then scroll down to and click **Cloud Service**.</span></span>

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="5045d-143">Yeni **bulut hizmeti** dikey penceresinde için bir değer girin **DNS adı**.</span><span class="sxs-lookup"><span data-stu-id="5045d-143">In the new **Cloud Service** blade, enter a value for the **DNS name**.</span></span>
4. <span data-ttu-id="5045d-144">Yeni bir **kaynak grubu** veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5045d-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="5045d-145">Bir **Konum** seçin.</span><span class="sxs-lookup"><span data-stu-id="5045d-145">Select a **Location**.</span></span>
6. <span data-ttu-id="5045d-146">Tıklatın **paket**.</span><span class="sxs-lookup"><span data-stu-id="5045d-146">Click **Package**.</span></span> <span data-ttu-id="5045d-147">Bu açılır **bir paketi yükleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="5045d-147">This will open the **Upload a package** blade.</span></span> <span data-ttu-id="5045d-148">Gerekli alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="5045d-148">Fill in the required fields.</span></span> <span data-ttu-id="5045d-149">Rollerinizi hiçbirini tek bir örnek içeriyorsa, olun **bir veya daha fazla rol tek bir örnek içeriyorsa bile Dağıt** seçilir.</span><span class="sxs-lookup"><span data-stu-id="5045d-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="5045d-150">Olduğundan emin olun **Başlat dağıtım** seçilir.</span><span class="sxs-lookup"><span data-stu-id="5045d-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="5045d-151">Tıklatın **Tamam** hangi kapatılacak **bir paketi yükleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="5045d-151">Click **OK** which will close the **Upload a package** blade.</span></span>
9. <span data-ttu-id="5045d-152">Eklemek için herhangi bir sertifika yoksa tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="5045d-152">If you do not have any certificates to add, click **Create**.</span></span>

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="5045d-154">Bir sertifikayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="5045d-154">Upload a certificate</span></span>
<span data-ttu-id="5045d-155">Dağıtım paketi varsa [sertifikalar kullanmak üzere yapılandırılmış](cloud-services-configure-ssl-certificate-portal.md#modify), sertifika artık karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5045d-155">If your deployment package was [configured to use certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload the certificate now.</span></span>

1. <span data-ttu-id="5045d-156">Seçin **sertifikaları**ve **eklemek sertifikaları** dikey penceresinde, SSL sertifika .pfx dosyasını seçin ve ardından sağlayın **parola** sertifika için</span><span class="sxs-lookup"><span data-stu-id="5045d-156">Select **Certificates**, and on the **Add certificates** blade, select the SSL certificate .pfx file, and then provide the **Password** for the certificate,</span></span>
2. <span data-ttu-id="5045d-157">Tıklatın **Attach sertifika**ve ardından **Tamam** üzerinde **eklemek sertifikaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="5045d-157">Click **Attach certificate**, and then click **OK** on the **Add certificates** blade.</span></span>
3. <span data-ttu-id="5045d-158">Tıklatın **oluşturma** üzerinde **bulut hizmeti** dikey.</span><span class="sxs-lookup"><span data-stu-id="5045d-158">Click **Create** on the **Cloud Service** blade.</span></span> <span data-ttu-id="5045d-159">Dağıtım ulaşıldığında **hazır** durumu, sonraki adımlara devam.</span><span class="sxs-lookup"><span data-stu-id="5045d-159">When the deployment has reached the **Ready** status, you can proceed to the next steps.</span></span>

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="5045d-161">Başarıyla tamamlandı, dağıtımı doğrulama</span><span class="sxs-lookup"><span data-stu-id="5045d-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="5045d-162">Bulut hizmet örneği'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5045d-162">Click the cloud service instance.</span></span>

    <span data-ttu-id="5045d-163">Hizmetin durumunu göstermesi gerekir **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="5045d-163">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="5045d-164">Altında **Essentials**, tıklatın **Site URL'si** bulut hizmetiniz bir web tarayıcısında açın.</span><span class="sxs-lookup"><span data-stu-id="5045d-164">Under **Essentials**, click the **Site URL** to open your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="5045d-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5045d-166">Next steps</span></span>
* <span data-ttu-id="5045d-167">[Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5045d-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="5045d-168">Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5045d-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="5045d-169">[Bulut hizmetinizi yönetme](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5045d-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="5045d-170">Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5045d-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

---
title: "Oluşturma ve bir bulut hizmeti dağıtma | Microsoft Docs"
description: "Oluşturmak ve Azure'da hızlı oluşturma yöntemini kullanarak bir bulut hizmeti dağıtma hakkında bilgi edinin."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 2a2172a78bfd3ac923edbc9de366b035629dd27b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="6b299-103">Oluşturma ve bir bulut hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="6b299-103">How to Create and Deploy a Cloud Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b299-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6b299-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="6b299-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="6b299-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
> 
> 

<span data-ttu-id="6b299-106">Klasik Azure portalı oluşturmak ve bir bulut hizmeti dağıtmak iki yol sunar: **hızlı Oluştur** ve **özel Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="6b299-106">The Azure classic portal provides two ways for you to create and deploy a cloud service: **Quick Create** and **Custom Create**.</span></span>

<span data-ttu-id="6b299-107">Bu konuda, yeni bir bulut hizmeti oluşturun ve ardından Hızlı oluşturma yönteminin kullanılacağını açıklanmaktadır **karşıya** karşıya yükleyin ve Azure bulut hizmet paketinde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6b299-107">This topic explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="6b299-108">Bu yöntemi kullandığınızda, Klasik Azure portalı gittiğiniz gibi tüm gereksinimleri tamamlamak için kullanılabilir uygun bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b299-108">When you use this method, the Azure classic portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="6b299-109">Oluşturduğunuzda, bulut hizmeti dağıtmak hazırsanız kullanarak aynı anda hem yapabilirsiniz **özel Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="6b299-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using **Custom Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="6b299-110">Bulut hizmeti Visual Studio Team Services (VSTS) gelen yayımlamayı düşünüyorsanız kullanmak **hızlı Oluştur**ve ardından VSTS yayımlama ayarlama **Hızlı Başlangıç** veya panoyu.</span><span class="sxs-lookup"><span data-stu-id="6b299-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use **Quick Create**, and then set up VSTS publishing from **Quick Start** or the dashboard.</span></span>
> 
> 

## <a name="concepts"></a><span data-ttu-id="6b299-111">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="6b299-111">Concepts</span></span>
<span data-ttu-id="6b299-112">Bir uygulamayı Azure bulut hizmeti olarak dağıtmak için üç bileşenler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="6b299-112">Three components are required in order to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="6b299-113">**Hizmet tanımı**</span><span class="sxs-lookup"><span data-stu-id="6b299-113">**Service Definition**</span></span>  
  <span data-ttu-id="6b299-114">Bulut Hizmet tanım dosyası (.csdef) rol sayısı dahil olmak üzere hizmet modeli tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6b299-114">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="6b299-115">**Hizmet yapılandırması**</span><span class="sxs-lookup"><span data-stu-id="6b299-115">**Service Configuration**</span></span>  
  <span data-ttu-id="6b299-116">Bulut hizmet yapılandırma dosyasının (.cscfg) rol örneği sayısı dahil olmak üzere, hizmet ve bireysel rolleri bulut için yapılandırma ayarlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b299-116">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="6b299-117">**Hizmet paketi**</span><span class="sxs-lookup"><span data-stu-id="6b299-117">**Service Package**</span></span>  
  <span data-ttu-id="6b299-118">Hizmet Paketi (.cspkg) uygulama kodu ve yapılandırmaları ve hizmet tanımı dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="6b299-118">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="6b299-119">Bunlar ve bir paketinin nasıl oluşturulacağı hakkında daha fazla bilgiyi [burada](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="6b299-119">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="6b299-120">Uygulamanızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="6b299-120">Prepare your app</span></span>
<span data-ttu-id="6b299-121">Bir bulut hizmeti dağıtmadan önce bulut hizmet paketi (.cspkg) uygulama kodunuz ve bir bulut hizmet yapılandırma dosyasının (.cscfg) oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b299-121">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="6b299-122">Azure SDK'sı, bu gerekli dağıtım dosyaları hazırlamak için araçlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b299-122">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="6b299-123">SDK'dan gelen yükleyebilirsiniz [Azure indirmeleri](https://azure.microsoft.com/downloads/) sayfasında, tercih ettiğiniz uygulama kodunuz geliştirmek dili.</span><span class="sxs-lookup"><span data-stu-id="6b299-123">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="6b299-124">Bir hizmet paketi vermeden önce üç bulut hizmeti özellikleri özel yapılandırmalar gerektirir:</span><span class="sxs-lookup"><span data-stu-id="6b299-124">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="6b299-125">Veri şifreleme için Güvenli Yuva Katmanı (SSL) kullanan bir bulut hizmet dağıtmak istiyorsanız [uygulamanızı yapılandırma](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) SSL için.</span><span class="sxs-lookup"><span data-stu-id="6b299-125">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) for SSL.</span></span>
* <span data-ttu-id="6b299-126">Rol örneği Uzak Masaüstü bağlantılarını yapılandırmak istiyorsanız, [rollerini yapılandırma](cloud-services-role-enable-remote-desktop.md) Uzak Masaüstü için.</span><span class="sxs-lookup"><span data-stu-id="6b299-126">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop.md) for Remote Desktop.</span></span>
* <span data-ttu-id="6b299-127">Ayrıntılı bulut hizmetiniz için izleme yapılandırmak istiyorsanız, Azure tanılama bulut hizmeti için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6b299-127">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="6b299-128">*Minimum izleme* rol örnekleri (sanal makineler) için ana bilgisayar işletim sistemlerden topladığı performans sayaçlarını (varsayılan düzeyi izleme) kullanır.</span><span class="sxs-lookup"><span data-stu-id="6b299-128">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="6b299-129">"Ayrıntılı izleme * uygulama işlem sırasında oluşan sorunları daha yakından Analizine olanak sağlamak için rol örnekleri içinde performans verilerine göre ek ölçümleri toplar.</span><span class="sxs-lookup"><span data-stu-id="6b299-129">"Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="6b299-130">Azure Tanılama'yı etkinleştirme konusunda bilgi edinmek için bkz: [Azure etkinleştirme tanılamada](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6b299-130">To find out how to enable Azure Diagnostics, see [Enabling Diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="6b299-131">Web rolleri veya çalışan rolleri dağıtımlarında bir bulut hizmeti oluşturmak için şunları yapmanız gerekir [hizmet paketi oluşturma](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="6b299-131">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6b299-132">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="6b299-132">Before you begin</span></span>
* <span data-ttu-id="6b299-133">Azure SDK'sını yüklemediyseniz tıklatın **Azure SDK Yükle** açmak için [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/)ve ardından, tercih ettiğiniz kodunuzu geliştirmek dil için SDK'sını indirin.</span><span class="sxs-lookup"><span data-stu-id="6b299-133">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="6b299-134">(Daha sonra bunu fırsatına sahip olacaksınız.)</span><span class="sxs-lookup"><span data-stu-id="6b299-134">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="6b299-135">Tüm rol örneklerinin bir sertifika gerektiriyorsa, sertifikaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b299-135">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="6b299-136">Bulut Hizmetleri bir .pfx dosyası özel bir anahtarla gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6b299-136">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="6b299-137">Yapabilecekleriniz [sertifikaları Azure'a yükleyin](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) oluşturur ve bulut hizmeti dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6b299-137">You can [upload the certificates to Azure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) as you create and deploy the cloud service.</span></span>
* <span data-ttu-id="6b299-138">Bulut hizmeti bir benzeşim grubuna dağıtmayı planlıyorsanız, benzeşim grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b299-138">If you plan to deploy the cloud service to an affinity group, create the affinity group.</span></span> <span data-ttu-id="6b299-139">Bir benzeşim grubu bir bölgede aynı konuma bulut hizmetiniz ve diğer Azure hizmetleriyle dağıtmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b299-139">You can use an affinity group to deploy your cloud service and other Azure services to the same location in a region.</span></span> <span data-ttu-id="6b299-140">Benzeşim grubu oluşturabilirsiniz **ağlar** alanı Azure Klasik portalı üzerinde **benzeşim grupları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="6b299-140">You can create the affinity group in the **Networks** area of the Azure classic portal, on the **Affinity Groups** page.</span></span>

## <a name="how-to-create-a-cloud-service-using-quick-create"></a><span data-ttu-id="6b299-141">Nasıl yapılır: Hızlı oluşturma yöntemini kullanarak bir bulut hizmeti oluştur</span><span class="sxs-lookup"><span data-stu-id="6b299-141">How to: Create a cloud service using Quick Create</span></span>
1. <span data-ttu-id="6b299-142">İçinde [Klasik Azure portalı](http://manage.windowsazure.com/), tıklatın **yeni**>**işlem**>**bulut hizmeti** > **Hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="6b299-142">In the [Azure classic portal](http://manage.windowsazure.com/), click **New**>**Compute**>**Cloud Service**>**Quick Create**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. <span data-ttu-id="6b299-144">İçinde **URL**, üretim dağıtımlarında bulut hizmetinize erişmek için genel URL'de kullanılacak bir alt etki alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="6b299-144">In **URL**, enter a subdomain name to use in the public URL for accessing your cloud service in production deployments.</span></span> <span data-ttu-id="6b299-145">Üretim dağıtımları için URL biçimi: http://*myURL*. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="6b299-145">The URL format for production deployments is: http://*myURL*.cloudapp.net.</span></span>
3. <span data-ttu-id="6b299-146">İçinde **bölge veya benzeşim grubunda**, coğrafi bölge veya benzeşim grubu bulut hizmeti dağıtmak için seçin.</span><span class="sxs-lookup"><span data-stu-id="6b299-146">In **Region or Affinity Group**, select the geographic region or affinity group to deploy the cloud service to.</span></span> <span data-ttu-id="6b299-147">Bulut hizmetiniz bir bölge içindeki diğer Azure hizmetleriyle aynı konuma dağıtmak istiyorsanız, bir benzeşim grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="6b299-147">Select an affinity group if you want to deploy your cloud service to the same location as other Azure services within a region.</span></span>
4. <span data-ttu-id="6b299-148">**Bulut Hizmeti Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b299-148">Click **Create Cloud Service**.</span></span>
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    <span data-ttu-id="6b299-150">İşlemin durumunu pencerenin altındaki ileti alanında izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b299-150">You can monitor the status of the process in the message area at the bottom of the window.</span></span>
   
    <span data-ttu-id="6b299-151">**Bulut Hizmetleri** alanı açılır ve yeni bulut hizmeti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6b299-151">The **Cloud Services** area opens, with the new cloud service displayed.</span></span> <span data-ttu-id="6b299-152">Durumu Oluşturuldu olarak değiştiğinde, bulut hizmeti oluşturma başarıyla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="6b299-152">When the status changes to Created, cloud service creation has completed successfully.</span></span>
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a><span data-ttu-id="6b299-154">Nasıl yapılır: bir bulut hizmeti için bir sertifika karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="6b299-154">How to: Upload a certificate for a cloud service</span></span>
1. <span data-ttu-id="6b299-155">İçinde [Klasik Azure portalı](http://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**, bulut hizmeti adına tıklayın ve ardından **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="6b299-155">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Certificates**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. <span data-ttu-id="6b299-157">Ya da tıklatın **bir sertifika karşıya** veya **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="6b299-157">Click either **Upload a certificate** or **Upload**.</span></span>
3. <span data-ttu-id="6b299-158">İçinde **dosya**, kullanın **Gözat** sertifikayı (.pfx dosyası) seçin.</span><span class="sxs-lookup"><span data-stu-id="6b299-158">In **File**, use **Browse** to select the certificate (.pfx file).</span></span>
4. <span data-ttu-id="6b299-159">İçinde **parola**, sertifikanın özel anahtarı girin.</span><span class="sxs-lookup"><span data-stu-id="6b299-159">In **Password**, enter the private key for the certificate.</span></span>
5. <span data-ttu-id="6b299-160">Tıklatın **Tamam** (onay işareti).</span><span class="sxs-lookup"><span data-stu-id="6b299-160">Click **OK** (checkmark).</span></span>
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    <span data-ttu-id="6b299-162">Aşağıda gösterilen karşıya yükleme iletisi alanında ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b299-162">You can watch the progress of the upload in the message area, shown below.</span></span> <span data-ttu-id="6b299-163">Karşıya yükleme tamamlandığında, sertifika tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="6b299-163">When the upload completes, the certificate is added to the table.</span></span> <span data-ttu-id="6b299-164">İleti alanına iletiyi kapatmak için Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6b299-164">In the message area, click OK to close the message.</span></span>
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a><span data-ttu-id="6b299-166">Nasıl yapılır: bir bulut hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="6b299-166">How to: Deploy a cloud service</span></span>
1. <span data-ttu-id="6b299-167">İçinde [Klasik Azure portalı](http://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**, bulut hizmeti adına tıklayın ve ardından **Pano**.</span><span class="sxs-lookup"><span data-stu-id="6b299-167">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Dashboard**.</span></span>
2. <span data-ttu-id="6b299-168">Ya da tıklatın **yeni bir üretim dağıtımı karşıya** veya **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="6b299-168">Click either **Upload a new production deployment** or **Upload**.</span></span>
3. <span data-ttu-id="6b299-169">İçinde **dağıtım etiketi**, yeni dağıtım - Örneğin, MyCloudServicev4 için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="6b299-169">In **Deployment label**, enter a name for the new deployment - for example, MyCloudServicev4.</span></span>
4. <span data-ttu-id="6b299-170">İçinde **paket**, kullanın **Gözat** kullanmak için hizmet paketi dosyasının (.cspkg) seçin.</span><span class="sxs-lookup"><span data-stu-id="6b299-170">In **Package**, use **Browse** to select the service package file (.cspkg) to use.</span></span>
5. <span data-ttu-id="6b299-171">İçinde **yapılandırma**, kullanın **Gözat** kullanmak için hizmet yapılandırma dosyasının (.cscfg) seçin.</span><span class="sxs-lookup"><span data-stu-id="6b299-171">In **Configuration**, use **Browse** to select the service configure file (.cscfg) to use.</span></span>
6. <span data-ttu-id="6b299-172">Bulut hizmeti herhangi bir rol ile yalnızca bir örnek içeriyorsa, seçin **bir veya daha fazla rol tek bir örnek içeriyorsa bile Dağıt** ilerlemek için dağıtımını etkinleştirmek için onay kutusunu.</span><span class="sxs-lookup"><span data-stu-id="6b299-172">If the cloud service will include any roles with only one instance, select the **Deploy even if one or more roles contain a single instance** check box to enable the deployment to proceed.</span></span>
   
    <span data-ttu-id="6b299-173">Her role en az iki örnek varsa azure yalnızca bulut hizmetine 99,95 yüzde erişimi Bakım ve hizmet güncelleştirmeleri sırasında garanti edebilir.</span><span class="sxs-lookup"><span data-stu-id="6b299-173">Azure can only guarantee 99.95 percent access to the cloud service during maintenance and service updates if every role has at least two instances.</span></span> <span data-ttu-id="6b299-174">Gerekirse, ek rol örnekleri üzerinde ekleyebileceğiniz **ölçek** bulut hizmeti dağıttıktan sonra sayfa.</span><span class="sxs-lookup"><span data-stu-id="6b299-174">If needed, you can add additional role instances on the **Scale** page after you deploy the cloud service.</span></span> <span data-ttu-id="6b299-175">Daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="6b299-175">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
7. <span data-ttu-id="6b299-176">Tıklatın **Tamam** (bulut hizmeti dağıtımı başlatmak için onay işaretine).</span><span class="sxs-lookup"><span data-stu-id="6b299-176">Click **OK** (checkmark) to begin the cloud service deployment.</span></span>
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    <span data-ttu-id="6b299-178">İleti alanında dağıtım durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b299-178">You can monitor the status of the deployment in the message area.</span></span> <span data-ttu-id="6b299-179">İleti gizlemek için Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6b299-179">Click OK to hide the message.</span></span>
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="6b299-181">Başarıyla tamamlandı, dağıtımı doğrulama</span><span class="sxs-lookup"><span data-stu-id="6b299-181">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="6b299-182">Tıklatın **Pano**.</span><span class="sxs-lookup"><span data-stu-id="6b299-182">Click **Dashboard**.</span></span>
   
    <span data-ttu-id="6b299-183">Hizmetin durumunu göstermesi gerekir **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="6b299-183">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="6b299-184">Altında **Hızlı Bakış**, bulut hizmetiniz bir web tarayıcısında açmak için site URL'sini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6b299-184">Under **quick glance**, click the site URL to open your cloud service in a web browser.</span></span>
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a><span data-ttu-id="6b299-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b299-186">Next steps</span></span>
* <span data-ttu-id="6b299-187">[Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6b299-187">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="6b299-188">Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="6b299-188">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="6b299-189">[Bulut hizmetinizi yönetme](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="6b299-189">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* <span data-ttu-id="6b299-190">Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="6b299-190">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>


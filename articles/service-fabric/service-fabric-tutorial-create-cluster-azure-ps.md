---
title: "Service Fabric kümesi oluşturma | Microsoft Docs"
description: "PowerShell kullanarak Azure'da bir Windows veya Linux Service Fabric kümesi oluşturmayı öğrenin."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: f62249417552b9cf840bfac3b94c27f63bd7064e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="8c5c1-103">PowerShell kullanarak Azure'da güvenli küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c5c1-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="8c5c1-104">Bu öğretici bir Service Fabric kümesi (Windows veya Linux) oluşturmak gösterilmiştir Azure'da çalışan.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-104">This tutorial shows you how to create a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="8c5c1-105">İşlemi tamamladığınızda, uygulamaları dağıtabileceğiniz bulutta çalıştıran bir kümeye sahip.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-105">When you're finished, you have a cluster running in the cloud that you can deploy applications to.</span></span>

<span data-ttu-id="8c5c1-106">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="8c5c1-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8c5c1-107">PowerShell kullanarak Azure'da güvenli bir Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="8c5c1-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="8c5c1-108">Küme bir X.509 sertifikası ile güvenli</span><span class="sxs-lookup"><span data-stu-id="8c5c1-108">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="8c5c1-109">PowerShell kullanarak kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="8c5c1-109">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="8c5c1-110">Bir küme Kaldır</span><span class="sxs-lookup"><span data-stu-id="8c5c1-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c5c1-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8c5c1-111">Prerequisites</span></span>
<span data-ttu-id="8c5c1-112">Bu öğreticiye başlamadan önce:</span><span class="sxs-lookup"><span data-stu-id="8c5c1-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="8c5c1-113">Bir Azure aboneliğiniz yoksa, oluşturma bir [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="8c5c1-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="8c5c1-114">Yükleme [Service Fabric SDK ve PowerShell Modülü](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="8c5c1-114">Install the [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="8c5c1-115">Yükleme [Azure Powershell modülü sürümü 4.1 veya üzeri](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="8c5c1-115">Install the [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="8c5c1-116">Aşağıdaki yordam (tek sanal makine) tek bir düğüm Önizleme Service Fabric kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-116">The following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="8c5c1-117">Küme yanı sıra küme oluşturulan ve bir anahtar kasası yerleştirilen otomatik olarak imzalanan bir sertifika tarafından korunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-117">The cluster is secured by a self-signed certificate that gets created along with the cluster and then placed in a key vault.</span></span> <span data-ttu-id="8c5c1-118">Tek düğümlü küme bir sanal makine genişletilemez ve önizleme kümeleri için daha yeni sürümleri yükseltilemez.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded to newer versions.</span></span>

<span data-ttu-id="8c5c1-119">Service Fabric kümesi Azure kullanımda çalıştırarak ücrete maliyeti hesaplamak için [Azure fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="8c5c1-119">To calculate cost incurred by running a Service Fabric cluster in Azure use the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="8c5c1-120">Service Fabric kümeleri oluşturma hakkında daha fazla bilgi için bkz: [Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8c5c1-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-the-cluster-using-azure-powershell"></a><span data-ttu-id="8c5c1-121">Azure PowerShell kullanarak küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c5c1-121">Create the cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="8c5c1-122">Azure Resource Manager şablonu ve parametre dosyanın yerel bir kopyasını indirin [Service Fabric için Azure Resource Manager şablonu](https://aka.ms/securepreviewonelineclustertemplate) GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-122">Download a local copy of the Azure Resource Manager template and the parameter file from the [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="8c5c1-123">*azuredeploy.JSON* Service Fabric kümesi tanımlayan Azure Resource Manager şablonudur.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-123">*azuredeploy.json* is the Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="8c5c1-124">*azuredeploy.Parameters.JSON* , Küme dağıtımı özelleştirmek bir parametre dosyası.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-124">*azuredeploy.parameters.json* is a parameters file for you to customize the cluster deployment.</span></span>

2. <span data-ttu-id="8c5c1-125">Aşağıdaki parametreleri özelleştirmek *azuredeploy.parameters.json* parametreler dosyası:</span><span class="sxs-lookup"><span data-stu-id="8c5c1-125">Customize the following parameters in the *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="8c5c1-126">Parametre</span><span class="sxs-lookup"><span data-stu-id="8c5c1-126">Parameter</span></span>       | <span data-ttu-id="8c5c1-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8c5c1-127">Description</span></span> | <span data-ttu-id="8c5c1-128">Önerilen Değer</span><span class="sxs-lookup"><span data-stu-id="8c5c1-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="8c5c1-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="8c5c1-129">clusterLocation</span></span> | <span data-ttu-id="8c5c1-130">Küme dağıtılacağı Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-130">The Azure region to which to deploy the cluster.</span></span> | <span data-ttu-id="8c5c1-131">*Örneğin, westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="8c5c1-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="8c5c1-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="8c5c1-132">clusterName</span></span>     | <span data-ttu-id="8c5c1-133">Oluşturmak istediğiniz küme adıdır.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-133">Name of the cluster you want to create.</span></span> | <span data-ttu-id="8c5c1-134">*Örneğin, bobs sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="8c5c1-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="8c5c1-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="8c5c1-135">adminUserName</span></span>   | <span data-ttu-id="8c5c1-136">Küme sanal makinelerde yerel yönetici hesabı.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-136">The local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="8c5c1-137">*Herhangi bir geçerli Windows Server kullanıcı adı*</span><span class="sxs-lookup"><span data-stu-id="8c5c1-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="8c5c1-138">Admınpassword</span><span class="sxs-lookup"><span data-stu-id="8c5c1-138">adminPassword</span></span>   | <span data-ttu-id="8c5c1-139">Küme sanal makinelerde yerel yönetici hesabının parolası.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-139">Password of the local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="8c5c1-140">*Geçerli bir Windows Server parola*</span><span class="sxs-lookup"><span data-stu-id="8c5c1-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="8c5c1-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="8c5c1-141">clusterCodeVersion</span></span> | <span data-ttu-id="8c5c1-142">Çalıştırmak üzere Service Fabric sürümü.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-142">The Service Fabric version to run.</span></span> <span data-ttu-id="8c5c1-143">(255.255.X.255 Önizleme sürümleri).</span><span class="sxs-lookup"><span data-stu-id="8c5c1-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="8c5c1-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="8c5c1-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="8c5c1-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="8c5c1-145">vmInstanceCount</span></span> | <span data-ttu-id="8c5c1-146">(1 ya da 3-99 olabilir), kümedeki sanal makine sayısı.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-146">The number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="8c5c1-147">**1**</span><span class="sxs-lookup"><span data-stu-id="8c5c1-147">**1**</span></span> | <span data-ttu-id="8c5c1-148">*Önizleme küme için yalnızca bir sanal makine belirtin*</span><span class="sxs-lookup"><span data-stu-id="8c5c1-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="8c5c1-149">Azure, oturum açma bir PowerShell konsolu açın ve kümede dağıtmak istediğiniz aboneliği seçin:</span><span class="sxs-lookup"><span data-stu-id="8c5c1-149">Open a PowerShell console, login to Azure, and select the subscription you want to deploy the cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="8c5c1-150">Oluşturma ve Service Fabric tarafından kullanılmak üzere sertifika için bir parola şifreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-150">Create and encrypt a password for the certificate to be used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="8c5c1-151">Küme ve sertifikasını aşağıdaki komutu çalıştırarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="8c5c1-151">Create the cluster and its certificate by running the following command:</span></span>

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   ><span data-ttu-id="8c5c1-152">`-CertificateSubjectName` Parametre Hizala gibi seçtiğiniz bir Azure bölgesine bağlı etki alanının yanı sıra Parametreler dosyasında belirtilen clusterName parametresi: `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-152">The `-CertificateSubjectName` parameter should align with the clusterName parameter specified in the parameters file, as well as the domain tied to the Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="8c5c1-153">Yapılandırma tamamlandıktan sonra Azure içinde oluşturulan küme bilgilerini çıkarır.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-153">Once the configuration finishes, it outputs information about the cluster created in Azure.</span></span> <span data-ttu-id="8c5c1-154">Ayrıca bu parametre için belirtilen yol - CertificateOutputFolder dizinine küme sertifika kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-154">It also copies the cluster certificate to the -CertificateOutputFolder directory on the path you specified for this parameter.</span></span> <span data-ttu-id="8c5c1-155">Service Fabric Explorer erişmek ve kümenizi durumunu görüntülemek için bu sertifika gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-155">You need this certificate to access Service Fabric Explorer and view the health of your cluster.</span></span>

<span data-ttu-id="8c5c1-156">Aşağıdaki URL'ye benzer kümenizi URL'sini not edin: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="8c5c1-156">Take note of the URL for your cluster, which may be similar to the following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-the-certificate--access-service-fabric-explorer"></a><span data-ttu-id="8c5c1-157">Service Fabric Explorer erişim & sertifika Değiştir</span><span class="sxs-lookup"><span data-stu-id="8c5c1-157">Modify the certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="8c5c1-158">Sertifika Alma Sihirbazı'nı açmak için sertifikayı çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-158">Double-click the certificate to open the Certificate Import Wizard.</span></span>

2. <span data-ttu-id="8c5c1-159">Varsayılan ayarları kullanır, ancak denetlediğinizden emin olun **bu anahtarı verilebilir olarak işaretle.**</span><span class="sxs-lookup"><span data-stu-id="8c5c1-159">Use default settings, but make sure to check the **Mark this key as exportable.**</span></span> <span data-ttu-id="8c5c1-160">onay kutusunu içinde **özel anahtar korumasını** adım.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-160">check box, in the **private key protection** step.</span></span> <span data-ttu-id="8c5c1-161">Azure kapsayıcı kayıt defteri için daha sonra Bu öğreticide Service Fabric kümesi kimlik doğrulamasını yapılandırırken sertifika vermek Visual Studio gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-161">Visual Studio needs to export the certificate when configuring Azure Container Registry to Service Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="8c5c1-162">Bu gibi durumlarda, Service Fabric Explorer şimdi bir tarayıcıda açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="8c5c1-163">Bunu yapmak için gidin **ManagementEndpoint** bir web tarayıcısı kullanarak kümenizi URL'sini ve makinenizde kaydedilen sertifikayı seçin.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-163">To do so, navigate to the **ManagementEndpoint** URL for your cluster using a web browser, and select the certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="8c5c1-164">Kendinden imzalı bir sertifika kullanıyor gibi Service Fabric Explorer açarken bir sertifika hatası bakın.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="8c5c1-165">Kenar içinde tıklattığınızdan sahip *ayrıntıları* ve ardından *Web sayfasına gidin* bağlantı.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-165">In Edge, you have to click *Details* and then the *Go on to the webpage* link.</span></span> <span data-ttu-id="8c5c1-166">Chrome'tıklatmak zorunda *Gelişmiş* ve ardından *devam* bağlantı.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-166">In Chrome, you have to click *Advanced* and then the *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="8c5c1-167">Küme oluşturma başarısız olursa, her zaman zaten dağıtılmış kaynaklar güncelleştirmeleri komutu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-167">If the cluster creation fails, you can always rerun the command, which updates the resources already deployed.</span></span> <span data-ttu-id="8c5c1-168">Bir sertifika başarısız dağıtımının bir parçası oluşturulmuş olsa bile, yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-168">If a certificate was created as part of the failed deployment, a new one is generated.</span></span> <span data-ttu-id="8c5c1-169">Küme oluşturma sorunlarını gidermek için bkz: [Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8c5c1-169">To troubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-to-the-secure-cluster"></a><span data-ttu-id="8c5c1-170">Güvenli kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="8c5c1-170">Connect to the secure cluster</span></span>
<span data-ttu-id="8c5c1-171">Service Fabric SDK ile birlikte yüklenen Service Fabric PowerShell modülünü kullanarak kümeye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-171">Connect to the cluster using the Service Fabric PowerShell module installed with the Service Fabric SDK.</span></span>  <span data-ttu-id="8c5c1-172">İlk olarak, geçerli kullanıcının, bilgisayarınızdaki kişisel (My) deposuna sertifikası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-172">First, install the certificate into the Personal (My) store of the current user on your computer.</span></span>  <span data-ttu-id="8c5c1-173">Aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8c5c1-173">Run the following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="8c5c1-174">Şimdi güvenli kümenize bağlanmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-174">You are now ready to connect to your secure cluster.</span></span>

<span data-ttu-id="8c5c1-175">**Service Fabric** PowerShell Modülü Service Fabric kümeleri, uygulamaları ve hizmetleri yönetmek için birçok cmdlet'leri sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-175">The **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="8c5c1-176">Kullanım [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet'ini güvenli kümeye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-176">Use the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet to connect to the secure cluster.</span></span> <span data-ttu-id="8c5c1-177">Sertifika parmak izi ve bağlantı uç nokta ayrıntılarını önceki adımdaki çıktı bulunur.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-177">The certificate thumbprint and connection endpoint details are found in the output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="8c5c1-178">Bağlı ve küme sağlıklı olduğundan emin olun kullanarak [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-178">Check that you are connected and the cluster is healthy using the [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="8c5c1-179">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="8c5c1-179">Clean up resources</span></span>

<span data-ttu-id="8c5c1-180">Küme, küme kaynağının yanı sıra diğer Azure kaynaklarından oluşur.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-180">A cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="8c5c1-181">Kümeyi ve kullandığı tüm kaynakları silmenin en basit yolu, kaynak grubunun silinmesidir.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-181">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span>

<span data-ttu-id="8c5c1-182">Azure'da oturum açma ve küme kaldırmak istediğiniz abonelik kimliği seçin.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-182">Log in to Azure and select the subscription ID with which you want to remove the cluster.</span></span>  <span data-ttu-id="8c5c1-183">Abonelik Kimliğiniz için oturum açarak bulabileceğiniz [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c5c1-183">You can find your subscription ID by logging in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="8c5c1-184">Kaynak grubu ve kullanarak tüm küme kaynakları silmek [Remove-AzureRMResourceGroup cmdlet'i](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="8c5c1-184">Delete the resource group and all the cluster resources using the [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="8c5c1-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8c5c1-185">Next steps</span></span>
<span data-ttu-id="8c5c1-186">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="8c5c1-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8c5c1-187">Service Fabric kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c5c1-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="8c5c1-188">Küme bir X.509 sertifikası ile güvenli</span><span class="sxs-lookup"><span data-stu-id="8c5c1-188">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="8c5c1-189">PowerShell kullanarak kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="8c5c1-189">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="8c5c1-190">Bir küme Kaldır</span><span class="sxs-lookup"><span data-stu-id="8c5c1-190">Remove a cluster</span></span>

<span data-ttu-id="8c5c1-191">Ardından, var olan bir uygulama dağıtma hakkında bilgi edinmek için aşağıdaki öğreticiyi ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="8c5c1-191">Next, advance to the following tutorial to learn how to deploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8c5c1-192">Varolan bir .NET uygulama Docker Compose ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="8c5c1-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)

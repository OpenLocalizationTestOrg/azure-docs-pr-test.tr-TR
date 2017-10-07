---
title: "aaaCreate Service Fabric küme Azure'da | Microsoft Docs"
description: "Nasıl toocreate bir Windows veya Linux Service Fabric kümesi Azure PowerShell'i kullanma hakkında bilgi edinin."
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
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="609f0-103">PowerShell kullanarak Azure'da güvenli küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="609f0-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="609f0-104">Bu öğretici nasıl toocreate Service Fabric kümesi (Windows veya Linux) çalıştığından gösterir azure'da.</span><span class="sxs-lookup"><span data-stu-id="609f0-104">This tutorial shows you how toocreate a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="609f0-105">İşlemi tamamladığınızda, uygulamaları dağıtabileceğiniz hello bulutta çalıştıran bir kümeye sahip.</span><span class="sxs-lookup"><span data-stu-id="609f0-105">When you're finished, you have a cluster running in hello cloud that you can deploy applications to.</span></span>

<span data-ttu-id="609f0-106">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="609f0-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="609f0-107">PowerShell kullanarak Azure'da güvenli bir Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="609f0-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="609f0-108">Bir X.509 sertifikası ile güvenli hello kümesi</span><span class="sxs-lookup"><span data-stu-id="609f0-108">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="609f0-109">PowerShell kullanarak toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="609f0-109">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="609f0-110">Bir küme Kaldır</span><span class="sxs-lookup"><span data-stu-id="609f0-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="609f0-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="609f0-111">Prerequisites</span></span>
<span data-ttu-id="609f0-112">Bu öğreticiye başlamadan önce:</span><span class="sxs-lookup"><span data-stu-id="609f0-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="609f0-113">Bir Azure aboneliğiniz yoksa, oluşturma bir [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="609f0-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="609f0-114">Merhaba yüklemek [Service Fabric SDK ve PowerShell Modülü](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="609f0-114">Install hello [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="609f0-115">Merhaba yüklemek [Azure Powershell modülü sürümü 4.1 veya üzeri](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="609f0-115">Install hello [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="609f0-116">Aşağıdaki yordamı hello (tek sanal makine) tek bir düğüm Önizleme Service Fabric kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="609f0-116">hello following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="609f0-117">Merhaba küme hello küme yanı sıra oluşturulan ve bir anahtar kasası yerleştirilen otomatik olarak imzalanan bir sertifika tarafından korunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="609f0-117">hello cluster is secured by a self-signed certificate that gets created along with hello cluster and then placed in a key vault.</span></span> <span data-ttu-id="609f0-118">Tek düğümlü küme bir sanal makine genişletilemez ve önizleme kümeleri yükseltilmiş toonewer sürümleri kaldırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="609f0-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded toonewer versions.</span></span>

<span data-ttu-id="609f0-119">Azure kullanım hello Service Fabric kümesi çalıştırarak ücrete toocalculate maliyet [Azure fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="609f0-119">toocalculate cost incurred by running a Service Fabric cluster in Azure use hello [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="609f0-120">Service Fabric kümeleri oluşturma hakkında daha fazla bilgi için bkz: [Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="609f0-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-hello-cluster-using-azure-powershell"></a><span data-ttu-id="609f0-121">Azure PowerShell kullanarak hello kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="609f0-121">Create hello cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="609f0-122">Hello hello Azure Resource Manager şablonu ve hello parametre dosyası yerel bir kopyasını indirin [Service Fabric için Azure Resource Manager şablonu](https://aka.ms/securepreviewonelineclustertemplate) GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="609f0-122">Download a local copy of hello Azure Resource Manager template and hello parameter file from hello [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="609f0-123">*azuredeploy.JSON* tanımlayan bir Service Fabric kümesi hello Azure Resource Manager şablonudur.</span><span class="sxs-lookup"><span data-stu-id="609f0-123">*azuredeploy.json* is hello Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="609f0-124">*azuredeploy.Parameters.JSON* toocustomize hello Küme dağıtımı sizin için bir parametre dosyası olduğunu.</span><span class="sxs-lookup"><span data-stu-id="609f0-124">*azuredeploy.parameters.json* is a parameters file for you toocustomize hello cluster deployment.</span></span>

2. <span data-ttu-id="609f0-125">Merhaba parametrelerinde aşağıdaki hello özelleştirme *azuredeploy.parameters.json* parametreler dosyası:</span><span class="sxs-lookup"><span data-stu-id="609f0-125">Customize hello following parameters in hello *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="609f0-126">Parametre</span><span class="sxs-lookup"><span data-stu-id="609f0-126">Parameter</span></span>       | <span data-ttu-id="609f0-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="609f0-127">Description</span></span> | <span data-ttu-id="609f0-128">Önerilen Değer</span><span class="sxs-lookup"><span data-stu-id="609f0-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="609f0-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="609f0-129">clusterLocation</span></span> | <span data-ttu-id="609f0-130">Hello Azure bölgesi toowhich toodeploy hello küme.</span><span class="sxs-lookup"><span data-stu-id="609f0-130">hello Azure region toowhich toodeploy hello cluster.</span></span> | <span data-ttu-id="609f0-131">*Örneğin, westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="609f0-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="609f0-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="609f0-132">clusterName</span></span>     | <span data-ttu-id="609f0-133">Ad hello kümesinin toocreate istiyor.</span><span class="sxs-lookup"><span data-stu-id="609f0-133">Name of hello cluster you want toocreate.</span></span> | <span data-ttu-id="609f0-134">*Örneğin, bobs sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="609f0-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="609f0-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="609f0-135">adminUserName</span></span>   | <span data-ttu-id="609f0-136">Merhaba küme sanal makinelerde Hello yerel yönetici hesabı.</span><span class="sxs-lookup"><span data-stu-id="609f0-136">hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="609f0-137">*Herhangi bir geçerli Windows Server kullanıcı adı*</span><span class="sxs-lookup"><span data-stu-id="609f0-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="609f0-138">Admınpassword</span><span class="sxs-lookup"><span data-stu-id="609f0-138">adminPassword</span></span>   | <span data-ttu-id="609f0-139">Hello hello küme sanal makinelerde yerel yönetici hesabının parolası.</span><span class="sxs-lookup"><span data-stu-id="609f0-139">Password of hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="609f0-140">*Geçerli bir Windows Server parola*</span><span class="sxs-lookup"><span data-stu-id="609f0-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="609f0-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="609f0-141">clusterCodeVersion</span></span> | <span data-ttu-id="609f0-142">Merhaba Service Fabric sürümü toorun.</span><span class="sxs-lookup"><span data-stu-id="609f0-142">hello Service Fabric version toorun.</span></span> <span data-ttu-id="609f0-143">(255.255.X.255 Önizleme sürümleri).</span><span class="sxs-lookup"><span data-stu-id="609f0-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="609f0-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="609f0-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="609f0-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="609f0-145">vmInstanceCount</span></span> | <span data-ttu-id="609f0-146">sanal makineler (1 ya da 3-99 olabilir) kümenizdeki Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="609f0-146">hello number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="609f0-147">**1**</span><span class="sxs-lookup"><span data-stu-id="609f0-147">**1**</span></span> | <span data-ttu-id="609f0-148">*Önizleme küme için yalnızca bir sanal makine belirtin*</span><span class="sxs-lookup"><span data-stu-id="609f0-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="609f0-149">Bir PowerShell konsol, oturum açma tooAzure açın ve toodeploy hello küme istediğiniz hello aboneliği seçin:</span><span class="sxs-lookup"><span data-stu-id="609f0-149">Open a PowerShell console, login tooAzure, and select hello subscription you want toodeploy hello cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="609f0-150">Oluşturma ve Service Fabric tarafından kullanılan hello sertifika toobe için bir parola şifreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="609f0-150">Create and encrypt a password for hello certificate toobe used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="609f0-151">Merhaba küme ve sertifikasını hello aşağıdaki komutu çalıştırarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="609f0-151">Create hello cluster and its certificate by running hello following command:</span></span>

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
   ><span data-ttu-id="609f0-152">Merhaba `-CertificateSubjectName` parametre Hizala hello Parametreler dosyasında belirtilen hello clusterName parametresiyle, de etki alanına bağlı toohello Azure bölgesi hello gibi gibi seçtiğiniz: `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="609f0-152">hello `-CertificateSubjectName` parameter should align with hello clusterName parameter specified in hello parameters file, as well as hello domain tied toohello Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="609f0-153">Merhaba Yapılandırma tamamlandıktan sonra Azure içinde oluşturulan hello küme bilgilerini çıkarır.</span><span class="sxs-lookup"><span data-stu-id="609f0-153">Once hello configuration finishes, it outputs information about hello cluster created in Azure.</span></span> <span data-ttu-id="609f0-154">Ayrıca, bu parametre için belirtilen hello yolunda hello küme sertifika toohello - CertificateOutputFolder dizin kopyalar.</span><span class="sxs-lookup"><span data-stu-id="609f0-154">It also copies hello cluster certificate toohello -CertificateOutputFolder directory on hello path you specified for this parameter.</span></span> <span data-ttu-id="609f0-155">Bu sertifika tooaccess kümenizi Service Fabric Explorer ve görünüm hello durumunu gerekir.</span><span class="sxs-lookup"><span data-stu-id="609f0-155">You need this certificate tooaccess Service Fabric Explorer and view hello health of your cluster.</span></span>

<span data-ttu-id="609f0-156">Benzer toohello olabilir, kümeniz hello URL'sini not edin URL aşağıdaki: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="609f0-156">Take note of hello URL for your cluster, which may be similar toohello following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a><span data-ttu-id="609f0-157">Service Fabric Explorer erişim & Hello sertifika Değiştir</span><span class="sxs-lookup"><span data-stu-id="609f0-157">Modify hello certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="609f0-158">Merhaba sertifika tooopen hello Sertifika Alma Sihirbazı'nı çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="609f0-158">Double-click hello certificate tooopen hello Certificate Import Wizard.</span></span>

2. <span data-ttu-id="609f0-159">Varsayılan ayarları kullanır, ancak emin toocheck hello olun **bu anahtarı verilebilir olarak işaretle.**</span><span class="sxs-lookup"><span data-stu-id="609f0-159">Use default settings, but make sure toocheck hello **Mark this key as exportable.**</span></span> <span data-ttu-id="609f0-160">onay kutusuna hello **özel anahtar korumasını** adım.</span><span class="sxs-lookup"><span data-stu-id="609f0-160">check box, in hello **private key protection** step.</span></span> <span data-ttu-id="609f0-161">Visual Studio, Azure kapsayıcı kayıt defteri tooService doku küme kimlik doğrulaması daha sonra Bu öğreticide yapılandırırken tooexport hello sertifika gerekir.</span><span class="sxs-lookup"><span data-stu-id="609f0-161">Visual Studio needs tooexport hello certificate when configuring Azure Container Registry tooService Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="609f0-162">Bu gibi durumlarda, Service Fabric Explorer şimdi bir tarayıcıda açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="609f0-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="609f0-163">toodo, bu nedenle, toohello gidin **ManagementEndpoint** bir web tarayıcısı ve makinenizde kaydedilmiş select hello sertifika kullanarak, kümeniz için URL.</span><span class="sxs-lookup"><span data-stu-id="609f0-163">toodo so, navigate toohello **ManagementEndpoint** URL for your cluster using a web browser, and select hello certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="609f0-164">Kendinden imzalı bir sertifika kullanıyor gibi Service Fabric Explorer açarken bir sertifika hatası bakın.</span><span class="sxs-lookup"><span data-stu-id="609f0-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="609f0-165">Edge'de, tooclick sahip *ayrıntıları* ve ardından hello *toohello Web sayfasındaki Git* bağlantı.</span><span class="sxs-lookup"><span data-stu-id="609f0-165">In Edge, you have tooclick *Details* and then hello *Go on toohello webpage* link.</span></span> <span data-ttu-id="609f0-166">Chrome'tooclick sahip *Gelişmiş* ve ardından hello *devam* bağlantı.</span><span class="sxs-lookup"><span data-stu-id="609f0-166">In Chrome, you have tooclick *Advanced* and then hello *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="609f0-167">Merhaba küme oluşturma işlemi başarısız olursa, her zaman önceden dağıtılan hello kaynak güncelleştirmeleri hello komutu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="609f0-167">If hello cluster creation fails, you can always rerun hello command, which updates hello resources already deployed.</span></span> <span data-ttu-id="609f0-168">Bir sertifika başarısız hello dağıtımının bir parçası oluşturulmuş olsa bile, yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="609f0-168">If a certificate was created as part of hello failed deployment, a new one is generated.</span></span> <span data-ttu-id="609f0-169">tootroubleshoot küme oluşturma, bkz: [Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="609f0-169">tootroubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-toohello-secure-cluster"></a><span data-ttu-id="609f0-170">Toohello güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="609f0-170">Connect toohello secure cluster</span></span>
<span data-ttu-id="609f0-171">Service Fabric SDK Hello ile yüklü hello Service Fabric PowerShell modülünü kullanarak toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="609f0-171">Connect toohello cluster using hello Service Fabric PowerShell module installed with hello Service Fabric SDK.</span></span>  <span data-ttu-id="609f0-172">Önce bilgisayarınızdaki geçerli kullanıcının hello hello (My) kişisel deposuna hello sertifikası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="609f0-172">First, install hello certificate into hello Personal (My) store of hello current user on your computer.</span></span>  <span data-ttu-id="609f0-173">Merhaba aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="609f0-173">Run hello following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="609f0-174">Hazır tooconnect tooyour güvenli küme sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="609f0-174">You are now ready tooconnect tooyour secure cluster.</span></span>

<span data-ttu-id="609f0-175">Merhaba **Service Fabric** PowerShell Modülü Service Fabric kümeleri, uygulamaları ve hizmetleri yönetmek için birçok cmdlet'leri sağlar.</span><span class="sxs-lookup"><span data-stu-id="609f0-175">hello **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="609f0-176">Kullanım hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello güvenli küme.</span><span class="sxs-lookup"><span data-stu-id="609f0-176">Use hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello secure cluster.</span></span> <span data-ttu-id="609f0-177">Sertifika parmak izi hello ve bağlantı uç nokta ayrıntılarını bir önceki adımda hello çıktısı bulunur.</span><span class="sxs-lookup"><span data-stu-id="609f0-177">hello certificate thumbprint and connection endpoint details are found in hello output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="609f0-178">Bağlı ve hello küme hello kullanarak sağlıklı olduğundan emin olun [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="609f0-178">Check that you are connected and hello cluster is healthy using hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="609f0-179">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="609f0-179">Clean up resources</span></span>

<span data-ttu-id="609f0-180">Bir küme diğer Azure kaynaklarını toohello küme kaynağı kendisi ayrıca oluşur.</span><span class="sxs-lookup"><span data-stu-id="609f0-180">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="609f0-181">Merhaba en basit yolu toodelete hello küme içereceği tükettiği tüm hello kaynakları ise toodelete hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="609f0-181">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span>

<span data-ttu-id="609f0-182">İçinde tooAzure oturum ve hello abonelik kimliği tooremove hello kümenin istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="609f0-182">Log in tooAzure and select hello subscription ID with which you want tooremove hello cluster.</span></span>  <span data-ttu-id="609f0-183">Abonelik Kimliğinizi toohello içinde oturum açarak bulabilirsiniz [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="609f0-183">You can find your subscription ID by logging in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="609f0-184">Merhaba kaynak grubu ve hello kullanarak tüm hello küme kaynakları silmek [Remove-AzureRMResourceGroup cmdlet'i](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="609f0-184">Delete hello resource group and all hello cluster resources using hello [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="609f0-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="609f0-185">Next steps</span></span>
<span data-ttu-id="609f0-186">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="609f0-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="609f0-187">Service Fabric kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="609f0-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="609f0-188">Bir X.509 sertifikası ile güvenli hello kümesi</span><span class="sxs-lookup"><span data-stu-id="609f0-188">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="609f0-189">PowerShell kullanarak toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="609f0-189">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="609f0-190">Bir küme Kaldır</span><span class="sxs-lookup"><span data-stu-id="609f0-190">Remove a cluster</span></span>

<span data-ttu-id="609f0-191">Ardından, öğretici toolearn nasıl aşağıdaki toohello ilerletmek toodeploy varolan bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="609f0-191">Next, advance toohello following tutorial toolearn how toodeploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="609f0-192">Varolan bir .NET uygulama Docker Compose ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="609f0-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)

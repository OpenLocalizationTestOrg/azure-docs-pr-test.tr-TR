---
title: "API Management Hızlı Başlangıç ile Azure Service Fabric | Microsoft Docs"
description: "Bu kılavuz hızlı bir şekilde Azure API Management ve Service Fabric nasıl başlayacağınızı gösterir."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: e9f44d8a43d274768f43261fea68f0da9c681ae1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="3cc4a-103">Service Fabric ile Azure API Management hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="3cc4a-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="3cc4a-104">Bu kılavuz size Azure API Management Service Fabric ile ayarlama ve arka uç hizmetlerine Service Fabric trafiği göndermek için ilk API işlemi yapılandırma gösterir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-104">This guide shows you how to set up Azure API Management with Service Fabric and configure your first API operation to send traffic to back-end services in Service Fabric.</span></span> <span data-ttu-id="3cc4a-105">Service Fabric ile Azure API Management senaryoları hakkında daha fazla bilgi için bkz: [genel bakış](service-fabric-api-management-overview.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-105">To learn more about Azure API Management scenarios with Service Fabric, see the [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-to-azure"></a><span data-ttu-id="3cc4a-106">API Management ve Service Fabric Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="3cc4a-106">Deploy API Management and Service Fabric to Azure</span></span>

<span data-ttu-id="3cc4a-107">Paylaşılan bir sanal ağ ile Azure API Management ve Service Fabric kümesi dağıtmak için ilk adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-107">The first step is to deploy API Management and a Service Fabric cluster to Azure in a shared Virtual Network.</span></span> <span data-ttu-id="3cc4a-108">Bu API, hizmet bulma, hizmet bölümü çözümleme ve iletme trafiği doğrudan herhangi bir arka uç hizmeti için Service Fabric gerçekleştirebilmek için Service Fabric ile doğrudan iletişim kurmak yönetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-108">This allows API Management to communicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly to any backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="3cc4a-109">Topoloji</span><span class="sxs-lookup"><span data-stu-id="3cc4a-109">Topology</span></span>

<span data-ttu-id="3cc4a-110">Bu kılavuz aşağıdaki topoloji Azure API Management ve Service Fabric aynı sanal ağ alt ağlarında olduğu dağıtır:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-110">This guide deploys the following topology to Azure in which API Management and Service Fabric are in subnets of the same Virtual Network:</span></span>

 ![Resim yazısı][sf-apim-topology-overview]

<span data-ttu-id="3cc4a-112">Hızlıca başlamak için Resource Manager şablonları her dağıtım adımı için sağlanır:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-112">To get started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="3cc4a-113">Ağ topolojisi:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-113">Network topology:</span></span>
    - <span data-ttu-id="3cc4a-114">[Network.JSON][network-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="3cc4a-115">[Network.Parameters.JSON][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="3cc4a-116">Service Fabric kümesi:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="3cc4a-117">[Cluster.JSON][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="3cc4a-118">[Cluster.Parameters.JSON][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="3cc4a-119">API Management:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-119">API Management:</span></span>
    - <span data-ttu-id="3cc4a-120">[apim.JSON][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="3cc4a-121">[apim.Parameters.JSON][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-to-azure-and-select-your-subscription"></a><span data-ttu-id="3cc4a-122">Azure'da oturum açın ve aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="3cc4a-122">Sign in to Azure and select your subscription</span></span>

<span data-ttu-id="3cc4a-123">Bu kılavuzu kullanır [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="3cc4a-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="3cc4a-124">Yeni bir PowerShell oturumu başlattığınızda, Azure hesabınızda oturum açın ve Azure komutları çalıştırmadan önce aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-124">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="3cc4a-125">Azure hesabınızda oturum açın:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-125">Sign in to your Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="3cc4a-126">Aboneliğinizi seçin:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="3cc4a-127">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cc4a-127">Create a resource group</span></span>

<span data-ttu-id="3cc4a-128">Dağıtımınız için yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="3cc4a-129">Bir ad ve bir konum girin.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-the-network-topology"></a><span data-ttu-id="3cc4a-130">Ağ topolojisi dağıtmak</span><span class="sxs-lookup"><span data-stu-id="3cc4a-130">Deploy the network topology</span></span>

<span data-ttu-id="3cc4a-131">İlk adım, API Management ve Service Fabric kümesi dağıtılacak ağ topolojisini ayarlamaktır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-131">The first step is to set up the network topology to which API Management and the Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="3cc4a-132">[Network.json] [ network-arm] Resource Manager şablonu iki alt ağ ve iki ağ güvenlik grupları (NSG) ile sanal ağ (VNET) oluşturmak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-132">The [network.json][network-arm] Resource Manager template is configured to create a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="3cc4a-133">[Network.parameters.json] [ network-parameters-arm] parametreler dosyası alt ağları ve API Management ve Service Fabric dağıtılacağı Nsg'ler adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-133">The [network.parameters.json][network-parameters-arm] parameters file contains the names of the subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="3cc4a-134">Bu kılavuz, parametre değerlerini değiştirilmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-134">For this guide, the parameter values do not need to be changed.</span></span> <span data-ttu-id="3cc4a-135">Bu değerleri, bunlar burada değiştirilirse, onları diğer Resource Manager şablonları uygun şekilde değiştirmeniz gerekir, böylece API Management ve Service Fabric Resource Manager şablonları kullanın.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-135">The API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in the other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="3cc4a-136">Aşağıdaki Resource Manager şablonu ve parametre dosyasını karşıdan yükleyin:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-136">Download the following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="3cc4a-137">[Network.JSON][network-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="3cc4a-138">[Network.Parameters.JSON][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="3cc4a-139">Ağ Kurulumu Resource Manager şablonu ve parametre dosyalarını dağıtmak için aşağıdaki PowerShell komutunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-139">Use the following PowerShell command to deploy the Resource Manager template and parameter files for the network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-the-service-fabric-cluster"></a><span data-ttu-id="3cc4a-140">Service Fabric kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="3cc4a-140">Deploy the Service Fabric cluster</span></span>

<span data-ttu-id="3cc4a-141">Ağ kaynaklarını dağıtma tamamladıktan sonra sonraki adım bir Service Fabric kümesi sanal ağ alt ağındaki ve Service Fabric kümesi için belirlenmiş NSG dağıtmaktır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-141">Once the network resources have finished deploying, the next step is to deploy a Service Fabric cluster to the VNET in the subnet and NSG designated for the Service Fabric cluster.</span></span> <span data-ttu-id="3cc4a-142">Bu öğreticide, Service Fabric Resource Manager şablonu VNET, alt ağ ve önceki adımda ayarladığınız NSG adları kullanmak üzere önceden yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-142">For this tutorial, the Service Fabric Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

<span data-ttu-id="3cc4a-143">Service Fabric kümesi Resource Manager şablonu, sertifika güvenliği ile güvenli bir küme oluşturmak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-143">The Service Fabric cluster Resource Manager template is configured to create a secure cluster with certificate security.</span></span> <span data-ttu-id="3cc4a-144">Sertifika, küme düğümü, düğümü iletişimin güvenliğini sağlamak için ve Service Fabric kümesi kullanıcı erişimini yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-144">The certificate is used to secure node-to-node communication for your cluster and to manage user access to your Service Fabric cluster.</span></span> <span data-ttu-id="3cc4a-145">API Management hizmet bulma için Service Fabric adlandırma hizmetine erişim için bu sertifikayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-145">API Management uses this certificate to access  the Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="3cc4a-146">Bu adım, bir sertifikanın anahtar kasası için küme güvenlik sonucunda gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="3cc4a-147">Anahtar kasası ile güvenli bir küme ayarlama hakkında daha fazla bilgi için bkz: [bu kılavuz Azure Kaynak Yöneticisi'ni kullanarak bir küme oluşturma](service-fabric-cluster-creation-via-arm.md)</span><span class="sxs-lookup"><span data-stu-id="3cc4a-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="3cc4a-148">Azure Active Directory kimlik doğrulaması küme erişimi için kullanılan sertifikaya ek olarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-148">You may add Azure Active Directory authentication in addition to the certificate used for cluster access.</span></span> <span data-ttu-id="3cc4a-149">Azure Active Directory Service Fabric kümesi kullanıcı erişimini yönetmek için önerilen yöntem, ancak bu öğreticiyi tamamlamak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-149">Azure Active Directory is the recommended way to manage user access to your Service Fabric cluster, but is not necessary to complete this tutorial.</span></span> <span data-ttu-id="3cc4a-150">Bir sertifika her iki durumda da Azure Active Directory ile bir Service Fabric arka ucu için kimlik doğrulaması şu anda desteklemiyor Azure API Management kimlik doğrulama ve küme düğümü, düğümü güvenlik için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="3cc4a-151">Aşağıdaki Resource Manager şablonu ve parametre dosyasını karşıdan yükleyin:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-151">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="3cc4a-152">[Cluster.JSON][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="3cc4a-153">[Cluster.Parameters.JSON][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="3cc4a-154">Boş parametre doldurun `cluster.parameters.json` dosya, dağıtımınız için de dahil olmak üzere [anahtar kasası bilgileri](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) küme sertifikanızın.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-154">Fill in the empty parameters in the `cluster.parameters.json` file for your deployment, including the [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="3cc4a-155">Service Fabric kümesi oluşturmak için Resource Manager şablonu ve parametre dosyalarını dağıtmak için aşağıdaki PowerShell komutunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-155">Use the following PowerShell command to deploy the Resource Manager template and parameter files to create the Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="3cc4a-156">API Management dağıtma</span><span class="sxs-lookup"><span data-stu-id="3cc4a-156">Deploy API Management</span></span>

<span data-ttu-id="3cc4a-157">Son olarak, alt ağdaki sanal ağa API Management dağıtın ve API yönetimi için NSG atanmış.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-157">Finally, deploy API Management to the VNET in the subnet and NSG designated for API Management.</span></span> <span data-ttu-id="3cc4a-158">API Management dağıtmadan önce tamamlanması Service Fabric Küme dağıtımı için beklemesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-158">You do not need to wait for the Service Fabric cluster deployment to finish before deploying API Management.</span></span> 

<span data-ttu-id="3cc4a-159">Bu öğreticide, API Management Resource Manager şablonu VNET, alt ağ ve önceki adımda ayarladığınız NSG adları kullanmak üzere önceden yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-159">For this tutorial, the API Management Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

 1. <span data-ttu-id="3cc4a-160">Aşağıdaki Resource Manager şablonu ve parametre dosyasını karşıdan yükleyin:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-160">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="3cc4a-161">[apim.JSON][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="3cc4a-162">[apim.Parameters.JSON][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="3cc4a-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="3cc4a-163">Boş parametre doldurun `apim.parameters.json` dağıtımınız için.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-163">Fill in the empty parameters in the `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="3cc4a-164">API yönetimi için Resource Manager şablonu ve parametre dosyalarını dağıtmak için aşağıdaki PowerShell komutunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-164">Use the following PowerShell command to deploy the Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="3cc4a-165">API Management yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3cc4a-165">Configure API Management</span></span>

<span data-ttu-id="3cc4a-166">API Management ve Service Fabric kümesi dağıtıldığı sonra Service Fabric arka uç API Management'te yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="3cc4a-167">Bu, Service Fabric kümesi trafiği gönderen bir arka uç hizmet ilkesi oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-167">This allows you to create a backend service policy that sends traffic to your Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="3cc4a-168">API yönetim güvenliği</span><span class="sxs-lookup"><span data-stu-id="3cc4a-168">API Management Security</span></span>

<span data-ttu-id="3cc4a-169">Service Fabric arka uç yapılandırmak için ilk API Management güvenlik ayarlarını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-169">To configure the Service Fabric backend, you first need to configure API Management security settings.</span></span> <span data-ttu-id="3cc4a-170">Güvenlik ayarlarını yapılandırmak üzere API Management hizmetiniz Azure portalında gidin.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-170">To configure security settings, go to your API Management service in the Azure portal.</span></span>

#### <a name="enable-the-api-management-rest-api"></a><span data-ttu-id="3cc4a-171">API Management REST API etkinleştir</span><span class="sxs-lookup"><span data-stu-id="3cc4a-171">Enable the API Management REST API</span></span>

<span data-ttu-id="3cc4a-172">API Management REST API şu anda bir arka uç hizmeti yapılandırmak için tek yoludur.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-172">The API Management REST API is currently the only way to configure a backend service.</span></span> <span data-ttu-id="3cc4a-173">API Management REST API etkinleştirmek ve onu güvenliğini sağlamak için ilk adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-173">The first step is to enable the API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="3cc4a-174">API Management hizmeti seçin **Yönetimi API - Önizleme** altında **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-174">In the API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="3cc4a-175">Denetleme **API Management REST API etkinleştir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-175">Check the **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="3cc4a-176">Yönetim API'si URL Not - Bu daha sonra Service Fabric arka ucu ayarlamak için kullanacağız URL'si</span><span class="sxs-lookup"><span data-stu-id="3cc4a-176">Note the Management API URL - this is the URL we'll use later to set up the Service Fabric backend</span></span>
 4. <span data-ttu-id="3cc4a-177">Generate bir **belirtecine erişmesini** bir sona erme tarihi ve bir anahtar seçerek, ardından **Generate** sayfasının en altına doğru düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-177">Generate an **access Token** by selecting an expiry date and a key, then click the **Generate** button toward the bottom of the page.</span></span>
 5. <span data-ttu-id="3cc4a-178">Kopya **erişim belirteci** ve onu Kaydet - Bu aşağıdaki adımlarda kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-178">Copy the **access token** and save it - we'll use this in the following steps.</span></span> <span data-ttu-id="3cc4a-179">Bu birincil anahtar ve ikincil anahtar farklı olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-179">Note this is different from the primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="3cc4a-180">Service Fabric istemci sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="3cc4a-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="3cc4a-181">API Management Service Fabric kümeniz kümenizi erişimi olan bir istemci sertifikası kullanılarak hizmet bulma için kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access to your cluster.</span></span> <span data-ttu-id="3cc4a-182">Kolaylık olması için Bu öğretici, kümenizi erişmek için kullanılan varsayılan Service Fabric kümesi oluşturulurken belirtilen aynı sertifikayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-182">For simplicity, this tutorial uses the same certificate specified when creating the Service Fabric cluster, which by default can be used to access your cluster.</span></span>

 1. <span data-ttu-id="3cc4a-183">API Management hizmeti seçin **istemci sertifikalarını - Önizleme** altında **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-183">In the API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="3cc4a-184">Tıklatın **+ Ekle** düğmesi</span><span class="sxs-lookup"><span data-stu-id="3cc4a-184">Click the **+ Add** button</span></span>
 2. <span data-ttu-id="3cc4a-185">Service Fabric kümesi oluştururken, belirtilen küme sertifikanın özel anahtar dosyası (.pfx) seçin, bir ad verin ve özel anahtar parolası sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-185">Select the private key file (.pfx) of the cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide the private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="3cc4a-186">Bu öğretici, istemci kimlik doğrulaması ve küme düğümü, düğümü güvenlik için aynı sertifikayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-186">This tutorial uses the same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="3cc4a-187">Bir Service Fabric kümesi erişmek için yapılandırılan yoksa ayrı bir istemci sertifikası kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-187">You may use a separate client certificate if you have one configured to access your Service Fabric cluster.</span></span>

### <a name="configure-the-backend"></a><span data-ttu-id="3cc4a-188">Arka uç yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3cc4a-188">Configure the backend</span></span>

<span data-ttu-id="3cc4a-189">API Management güvenlik yapılandırıldığında, Service Fabric arka uç yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-189">Now that API Management security is configured, you can configure the Service Fabric backend.</span></span> <span data-ttu-id="3cc4a-190">Service Fabric arka uçlarını için Service Fabric kümesi, belirli bir Service Fabric hizmeti yerine arka uç grubudur.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-190">For Service Fabric backends, the Service Fabric cluster is the backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="3cc4a-191">Bu, kümedeki birden fazla hizmeti yönlendirmek tek bir ilke sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-191">This allows a single policy to route to more than one service in the cluster.</span></span>

<span data-ttu-id="3cc4a-192">Bu adım, önceki adımda API Management karşıya küme sertifikanızın daha önce oluşturulan erişim belirteci ve parmak izi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-192">This step requires the access token you generated earlier and the thumbprint for your cluster certificate you uploaded to API Management in the previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="3cc4a-193">API yönetimi için önceki adımda ayrı istemci sertifikası kullandıysanız, bu adımda küme sertifika parmak izi yanı sıra istemci sertifikasının parmak izi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-193">If you used a separate client certificate in the previous step for API Management, you need the thumbprint for the client certificate in addition to the cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="3cc4a-194">Aşağıdaki HTTP PUT, Service Fabric arka uç hizmetini yapılandırmak API Management REST API etkinleştirirken daha önce Not API Management API URL'sine isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-194">Send the following HTTP PUT request to the API Management API URL you noted earlier when enabling the API Management REST API to configure the Service Fabric backend service.</span></span> <span data-ttu-id="3cc4a-195">Görmeniz gerekir bir `HTTP 201 Created` komutu başarılı olduğunda yanıt.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-195">You should see an `HTTP 201 Created` response when the command succeeds.</span></span> <span data-ttu-id="3cc4a-196">Her bir alan hakkında daha fazla bilgi için bkz: API Yönetimi [arka uç API başvuru belgeleri](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="3cc4a-196">For more information on each field, see the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="3cc4a-197">HTTP komutu ve URL:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="3cc4a-198">İstek üstbilgilerini:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="3cc4a-199">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-199">Request body:</span></span>
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

<span data-ttu-id="3cc4a-200">**Url** burada parametredir bir hizmet tam adı bir hizmetin kümenizdeki bir arka uç ilkesinde hiçbir hizmet adı belirtilmezse, tüm istekleri varsayılan olarak yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-200">The **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed to by default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="3cc4a-201">Sahte hizmet adı gibi kullanabilir "fabric: / sahte/service" bir geri dönüş hizmetine sahip düşünmüyorsanız.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend to have a fallback service.</span></span>

<span data-ttu-id="3cc4a-202">API Management başvuran [arka uç API başvuru belgeleri](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) her bir alan hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-202">Refer to the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="3cc4a-203">Örnek</span><span class="sxs-lookup"><span data-stu-id="3cc4a-203">Example</span></span>

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="3cc4a-204">Service Fabric arka uç hizmet dağıtma</span><span class="sxs-lookup"><span data-stu-id="3cc4a-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="3cc4a-205">API Management için bir arka uç olarak yapılandırılan Service Fabric sahip olduğunuza göre Apı'lerinizi Service Fabric hizmetleriniz için trafiği göndermek için arka uç ilkeleri yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-205">Now that you have the Service Fabric configured as a backend to API Management, you can author backend policies for your APIs that send traffic to your Service Fabric services.</span></span> <span data-ttu-id="3cc4a-206">Ancak önce isteklerini kabul etmek için Service Fabric içinde çalışan bir hizmete gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-206">But first you need a service running in Service Fabric to accept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="3cc4a-207">Bir HTTP uç noktası ile bir Service Fabric hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cc4a-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="3cc4a-208">Bu öğreticide, temel bir durum bilgisiz ASP.NET Core güvenilir varsayılan Web API projesi şablonunu kullanarak hizmet oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using the default Web API project template.</span></span> <span data-ttu-id="3cc4a-209">Azure API Management kullanıma hizmetiniz için bir HTTP uç noktası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="3cc4a-210">Tarafından Başlat [ASP.NET Core geliştirme için geliştirme ortamınızı kurma](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="3cc4a-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="3cc4a-211">Geliştirme ortamınızı ayarladıktan sonra Visual Studio'yu yönetici olarak başlatın ve ASP.NET Core hizmet oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="3cc4a-212">Visual Studio'da yeni proje dosyası seçin ->.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="3cc4a-213">Bulut altında Service Fabric uygulaması şablonu seçin ve adlandırın **"ApiApplication"**.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-213">Select the Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="3cc4a-214">ASP.NET Core hizmet şablonu seçin ve projeyi adlandırın **"WebApiService"**.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-214">Select the ASP.NET Core service template and name the project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="3cc4a-215">Web API ASP.NET Core 1.1 proje şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-215">Select the Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="3cc4a-216">Proje oluşturulduktan sonra açmak `PackageRoot\ServiceManifest.xml` kaldırıp `Port` uç nokta kaynak yapılandırması özniteliğinden:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-216">Once the project is created, open `PackageRoot\ServiceManifest.xml` and remove the `Port` attribute from the endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="3cc4a-217">Bu, bir bağlantı noktasından, biz ağ güvenlik grubu için API Management trafiğe izin verme küme Resource Manager şablonunda aracılığıyla açılan dinamik olarak uygulama bağlantı noktası aralığını belirtmek Service Fabric sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-217">This allows Service Fabric to specify a port dynamically from the application port range, which we opened through the Network Security Group in the cluster Resource Manager template, allowing traffic to flow to it from API Management.</span></span>
 
 6. <span data-ttu-id="3cc4a-218">Web API doğrulamak için Visual Studio'da F5 tuşuna basarak yerel olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-218">Press F5 in Visual Studio to verify the web API is available locally.</span></span> 

    <span data-ttu-id="3cc4a-219">Açık Service Fabric Explorer ve ASP.NET Core hizmeti belirli bir örneği inceleyin taban adresi görmek için hizmet üzerinde dinliyor.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-219">Open Service Fabric Explorer and drill down to a specific instance of the ASP.NET Core service to see the base address the service is listening on.</span></span> <span data-ttu-id="3cc4a-220">Ekleme `/api/values` bankasına adresi ve bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-220">Add `/api/values` to the base address and open it in a browser.</span></span> <span data-ttu-id="3cc4a-221">Bu Web API şablonunda ValuesController Get yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-221">This invokes the Get method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="3cc4a-222">Bu şablon tarafından sağlanan varsayılan yanıt, iki dizeyi içeren bir JSON dizisi döndürür:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-222">It returns the default response that is provided by the template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="3cc4a-223">Bu, Azure API Management'te aracılığıyla kullanıma uç noktadır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-223">This is the endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="3cc4a-224">Son olarak, Azure kümenizdeki uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-224">Finally, deploy the application to your cluster in Azure.</span></span> <span data-ttu-id="3cc4a-225">[Visual Studio kullanarak](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), uygulama projesine sağ tıklatın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click the Application project and select **Publish**.</span></span> <span data-ttu-id="3cc4a-226">Küme uç noktası sağlayın (örneğin, `mycluster.westus.cloudapp.azure.com:19000`) Azure Service Fabric kümenizdeki uygulamayı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) to deploy the application to your Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="3cc4a-227">Adlı bir ASP.NET Core durum bilgisiz hizmeti `fabric:/ApiApplication/WebApiService` artık Azure Service Fabric kümenizdeki çalıştırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="3cc4a-228">Bir API işlem oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cc4a-228">Create an API operation</span></span>

<span data-ttu-id="3cc4a-229">Şimdi biz, dış istemcilere Service Fabric kümede çalışan ASP.NET Core durum bilgisiz hizmeti ile iletişim kurmak için API Management bir işlem oluşturmak için hazır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-229">Now we're ready to create an operation in API Management that external clients use to communicate with the ASP.NET Core stateless service running in the Service Fabric cluster.</span></span>

 1. <span data-ttu-id="3cc4a-230">Azure portalında oturum açın ve API Management hizmeti dağıtımınızı gidin.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-230">Log in to the Azure portal and navigate to your API Management service deployment.</span></span>
 2. <span data-ttu-id="3cc4a-231">API Management hizmeti dikey penceresinde, seçin **API'leri - Önizleme**</span><span class="sxs-lookup"><span data-stu-id="3cc4a-231">In the API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="3cc4a-232">Tıklayarak yeni bir API eklemek **boş API** kutusu ve iletişim kutusunu doldurma:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-232">Add a new API by clicking the **Blank API** box and filling out the dialog box:</span></span>

     - <span data-ttu-id="3cc4a-233">**Web hizmeti URL'si**: Service Fabric arka uçlarını için değil Bu URL değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="3cc4a-234">Herhangi bir değer buraya koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-234">You can put any value here.</span></span> <span data-ttu-id="3cc4a-235">Bu öğretici için kullanın: `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="3cc4a-236">**Ad**: API'nizi için herhangi bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="3cc4a-237">Bu öğretici için kullanmak `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="3cc4a-238">**URL şeması**: HTTP, HTTPS ya da her ikisini de seçin.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="3cc4a-239">Bu öğretici için kullanmak `both`.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="3cc4a-240">**API'si URL soneki**: bir sonek için bizim API sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="3cc4a-241">Bu öğretici için kullanmak `myapp`.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="3cc4a-242">API oluşturulduktan sonra tıklatın **+ ekleme işlemi** bir ön uç API işlemi eklemek için.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-242">Once the API is created, click **+ Add operation** to add a front-end API operation.</span></span> <span data-ttu-id="3cc4a-243">Değerlerin doldurun:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-243">Fill out the values:</span></span>
    
     - <span data-ttu-id="3cc4a-244">**URL**: seçin `GET` ve bir URL yolu için API sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-244">**URL**: Select `GET` and provide a URL path for the API.</span></span> <span data-ttu-id="3cc4a-245">Bu öğretici için kullanmak `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="3cc4a-246">Varsayılan olarak, Service Fabric hizmeti arka ucuna gönderilen URL yolunu URL yolu burada belirtilen.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-246">By default, the URL path specified here is the URL path sent to the backend Service Fabric service.</span></span> <span data-ttu-id="3cc4a-247">Hizmetinizi kullanır, bu durumda aynı URL yolunu buraya kullanırsanız `/api/values`, sonra işlemi daha fazla değişiklik yapılmadan çalışır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-247">If you use the same URL path here that your service uses, in this case `/api/values`, then the operation works without further modification.</span></span> <span data-ttu-id="3cc4a-248">Ayrıca, arka uç Service Fabric hizmeti tarafından kullanılan URL yolu farklı bir URL yolu buraya belirtebilir, bu durumda, aynı zamanda bir yolu yeniden yazma işlemi ilkenizde daha sonra belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-248">You may also specify a URL path here that is different from the URL path used by your backend Service Fabric service, in which case you will also need to specify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="3cc4a-249">**Görünen ad**: API için herhangi bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-249">**Display name**: Provide any name for the API.</span></span> <span data-ttu-id="3cc4a-250">Bu öğretici için kullanmak `Values`.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="3cc4a-251">Arka uç ilkesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3cc4a-251">Configure a backend policy</span></span>

<span data-ttu-id="3cc4a-252">Arka uç ilke her şeyi birbirine bağlar.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-252">The backend policy ties everything together.</span></span> <span data-ttu-id="3cc4a-253">İstekleri yönlendirilen arka uç Service Fabric hizmeti yapılandırdığınız budur.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-253">This is where you configure the backend Service Fabric service to which requests are routed.</span></span> <span data-ttu-id="3cc4a-254">Bu ilke için herhangi bir API işlemi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-254">You can apply this policy to any API operation.</span></span> <span data-ttu-id="3cc4a-255">[Service Fabric için arka uç yapılandırması](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) aşağıdaki isteği yönlendirme denetimleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-255">The [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides the following request routing controls:</span></span> 
 - <span data-ttu-id="3cc4a-256">Hizmet örneği seçimi ya da sabit kodlanmış bir Service Fabric hizmeti örnek adı belirterek (örneğin, `"fabric:/myapp/myservice"`) veya HTTP isteğinden oluşturulan (örneğin, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="3cc4a-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from the HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="3cc4a-257">Tüm Service Fabric bölümleme düzenini kullanarak bir bölüm anahtarı oluşturma tarafından bölüm çözünürlüğü.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="3cc4a-258">Durum bilgisi olan hizmetler için çoğaltma seçimi.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="3cc4a-259">Bir hizmet konumu yeniden çözümlemeyi ve isteği yeniden göndermeyi koşullarını belirtmenize olanak veren çözümleme yeniden deneme koşulları.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-259">Resolution retry conditions that allow you to specify the conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="3cc4a-260">Bu öğretici için daha önce dağıttığınız ASP.NET Core durum bilgisiz hizmete isteklerini doğrudan yönlendiren bir arka uç ilkesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-260">For this tutorial, create a backend policy that routes requests directly to the ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="3cc4a-261">Seçme ve düzenleme **gelen ilkeleri** için `Values` Düzenle simgesine tıklayarak ve ardından seçerek işlemi **kod görünümü**.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-261">Select and edit the **inbound policies** for the `Values` operation by clicking the edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="3cc4a-262">İlke Kod düzenleyicisinde ekleyin bir `set-backend-service` ilkesi altında aşağıda gösterildiği gibi ilkeleri gelen ve tıklatın **kaydetmek** düğmesi:</span><span class="sxs-lookup"><span data-stu-id="3cc4a-262">In the policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click the **Save** button:</span></span>
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

<span data-ttu-id="3cc4a-263">Service Fabric arka uç İlkesi özniteliklerini tam kümesi için başvurmak [API Management arka uç belgeleri](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="3cc4a-263">For a full set of Service Fabric back-end policy attributes, refer to the [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-the-api-to-a-product"></a><span data-ttu-id="3cc4a-264">Bir ürüne API ekleme.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-264">Add the API to a product.</span></span> 

<span data-ttu-id="3cc4a-265">API aramadan önce burada kullanıcılara erişim izni verebilirsiniz ürün eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-265">Before you can call the API, it must be added to a product where you can grant access to users.</span></span> 

 1. <span data-ttu-id="3cc4a-266">API Management hizmeti seçin **ürünler - Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-266">In the API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="3cc4a-267">Varsayılan olarak, API Management sağlayıcıları iki ürünler: Starter ve sınırsız.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="3cc4a-268">Sınırsız ürün seçin.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-268">Select the Unlimited product.</span></span>
 3. <span data-ttu-id="3cc4a-269">API seçin.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-269">Select APIs.</span></span>
 4. <span data-ttu-id="3cc4a-270">Tıklatın **+ Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-270">Click the **+ Add** button.</span></span>
 5. <span data-ttu-id="3cc4a-271">Seçin `Service Fabric App` tıklayın ve önceki adımları içinde oluşturduğunuz API **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-271">Select the `Service Fabric App` API you created in the previous steps and click the **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="3cc4a-272">test</span><span class="sxs-lookup"><span data-stu-id="3cc4a-272">Test it</span></span>

<span data-ttu-id="3cc4a-273">Şimdi doğrudan Azure Portalı'ndan API Management üzerinden Service Fabric, arka uç hizmetinde bir istek göndermesini deneyin.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-273">You can now try sending a request to your back-end service in Service Fabric through API Management directly from the Azure portal.</span></span>

 1. <span data-ttu-id="3cc4a-274">API Management hizmeti seçin **API - Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-274">In the API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="3cc4a-275">İçinde `Service Fabric App` önceki adımlarda, select oluşturduğunuz API **Test** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-275">In the `Service Fabric App` API you created in the previous steps, select the **Test** tab.</span></span>
 3. <span data-ttu-id="3cc4a-276">Tıklatın **Gönder** düğmesi bir test isteği arka uç hizmetine göndermek için.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-276">Click the **Send** button to send a test request to the backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cc4a-277">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3cc4a-277">Next steps</span></span>

<span data-ttu-id="3cc4a-278">Bu noktada, Service Fabric ve API Management temel bir kurulumu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="3cc4a-279">Bu öğretici temel kullanıcı sertifika tabanlı kimlik doğrulaması, Service Fabric kümesi için hızlı bir şekilde ayarlanan almak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster to get you set up quickly.</span></span> <span data-ttu-id="3cc4a-280">Service Fabric kümesi için daha gelişmiş kullanıcı kimlik doğrulaması ile tercih [Azure Active Directory kimlik doğrulaması](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="3cc4a-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="3cc4a-281">Ardından, [oluşturma ve Gelişmiş Ürün ayarları Azure API Management'te yapılandırma](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) uygulamanızı gerçek dünya trafiği için hazırlamak için.</span><span class="sxs-lookup"><span data-stu-id="3cc4a-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) to prepare your application for real world traffic.</span></span>

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png

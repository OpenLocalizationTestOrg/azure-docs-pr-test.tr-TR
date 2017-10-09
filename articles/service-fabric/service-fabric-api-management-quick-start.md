---
title: "API Management Hızlı Başlangıç ile Service Fabric aaaAzure | Microsoft Docs"
description: "Bu kılavuz size nasıl tooquickly Başlarken Azure API Management ve Service Fabric gösterir."
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
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="da990-103">Service Fabric ile Azure API Management hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="da990-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="da990-104">Bu kılavuz size gösterir nasıl tooset yukarı Azure API Management Service Fabric ile ve ilk API işlemi toosend trafiği tooback uç hizmetlerinizi Service Fabric yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="da990-104">This guide shows you how tooset up Azure API Management with Service Fabric and configure your first API operation toosend traffic tooback-end services in Service Fabric.</span></span> <span data-ttu-id="da990-105">Service Fabric ile Azure API Management senaryoları hakkında daha fazla toolearn bkz hello [genel bakış](service-fabric-api-management-overview.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="da990-105">toolearn more about Azure API Management scenarios with Service Fabric, see hello [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a><span data-ttu-id="da990-106">API Management ve Service Fabric tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="da990-106">Deploy API Management and Service Fabric tooAzure</span></span>

<span data-ttu-id="da990-107">Merhaba ilk toodeploy API Management ve paylaşılan bir sanal ağ içinde bir Service Fabric kümesi tooAzure adımdır.</span><span class="sxs-lookup"><span data-stu-id="da990-107">hello first step is toodeploy API Management and a Service Fabric cluster tooAzure in a shared Virtual Network.</span></span> <span data-ttu-id="da990-108">Bu, tooany arka uç hizmeti doğrudan Service Fabric hizmet bulma, hizmet bölümü çözümleme ve iletme trafiği gerçekleştirebilmek için Service Fabric ile doğrudan API Management toocommunicate sağlar.</span><span class="sxs-lookup"><span data-stu-id="da990-108">This allows API Management toocommunicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly tooany backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="da990-109">Topoloji</span><span class="sxs-lookup"><span data-stu-id="da990-109">Topology</span></span>

<span data-ttu-id="da990-110">Bu kılavuz hello aşağıdaki dağıtır API Management ve Service Fabric olduğu alt ağların topoloji tooAzure hello aynı sanal ağ:</span><span class="sxs-lookup"><span data-stu-id="da990-110">This guide deploys hello following topology tooAzure in which API Management and Service Fabric are in subnets of hello same Virtual Network:</span></span>

 ![Resim yazısı][sf-apim-topology-overview]

<span data-ttu-id="da990-112">Resource Manager şablonları tooget hızlı bir şekilde başlatıldı, her dağıtım adımı için sağlanır:</span><span class="sxs-lookup"><span data-stu-id="da990-112">tooget started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="da990-113">Ağ topolojisi:</span><span class="sxs-lookup"><span data-stu-id="da990-113">Network topology:</span></span>
    - <span data-ttu-id="da990-114">[Network.JSON][network-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="da990-115">[Network.Parameters.JSON][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="da990-116">Service Fabric kümesi:</span><span class="sxs-lookup"><span data-stu-id="da990-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="da990-117">[Cluster.JSON][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="da990-118">[Cluster.Parameters.JSON][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="da990-119">API Management:</span><span class="sxs-lookup"><span data-stu-id="da990-119">API Management:</span></span>
    - <span data-ttu-id="da990-120">[apim.JSON][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="da990-121">[apim.Parameters.JSON][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-tooazure-and-select-your-subscription"></a><span data-ttu-id="da990-122">İçinde tooAzure oturum ve aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="da990-122">Sign in tooAzure and select your subscription</span></span>

<span data-ttu-id="da990-123">Bu kılavuzu kullanır [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="da990-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="da990-124">Yeni bir PowerShell oturumu başlattığınızda tooyour Azure hesabı oturum ve Azure komutları çalıştırmadan önce aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="da990-124">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="da990-125">Azure hesabı tooyour oturum:</span><span class="sxs-lookup"><span data-stu-id="da990-125">Sign in tooyour Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="da990-126">Aboneliğinizi seçin:</span><span class="sxs-lookup"><span data-stu-id="da990-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="da990-127">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="da990-127">Create a resource group</span></span>

<span data-ttu-id="da990-128">Dağıtımınız için yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="da990-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="da990-129">Bir ad ve bir konum girin.</span><span class="sxs-lookup"><span data-stu-id="da990-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a><span data-ttu-id="da990-130">Merhaba ağ topolojisi dağıtmak</span><span class="sxs-lookup"><span data-stu-id="da990-130">Deploy hello network topology</span></span>

<span data-ttu-id="da990-131">Merhaba ilk tooset hello ağ topolojisi toowhich API Management yukarı adımdır ve hello Service Fabric kümesi dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="da990-131">hello first step is tooset up hello network topology toowhich API Management and hello Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="da990-132">Merhaba [network.json] [ network-arm] Resource Manager şablonu olan bir sanal ağ (VNET) iki alt ağı ve iki ağ güvenlik grupları (NSG) yapılandırılmış toocreate.</span><span class="sxs-lookup"><span data-stu-id="da990-132">hello [network.json][network-arm] Resource Manager template is configured toocreate a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="da990-133">Merhaba [network.parameters.json] [ network-parameters-arm] parametreler dosyası hello alt ağları ve API Management ve Service Fabric dağıtılacağı Nsg'ler hello adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="da990-133">hello [network.parameters.json][network-parameters-arm] parameters file contains hello names of hello subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="da990-134">Bu kılavuz, değiştirilen toobe hello parametre değerlerini gerekmez.</span><span class="sxs-lookup"><span data-stu-id="da990-134">For this guide, hello parameter values do not need toobe changed.</span></span> <span data-ttu-id="da990-135">bunlar burada değiştirilirse değiştirmeniz gerekir böylece bunları diğer Resource Manager şablonları aşağıdaki buna göre Merhaba, bu değerleri Hello API Management ve Service Fabric Resource Manager şablonları kullanın.</span><span class="sxs-lookup"><span data-stu-id="da990-135">hello API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in hello other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="da990-136">Aşağıdaki Resource Manager şablonu ve parametre dosyasına hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="da990-136">Download hello following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="da990-137">[Network.JSON][network-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="da990-138">[Network.Parameters.JSON][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="da990-139">PowerShell komut toodeploy hello Resource Manager şablonu ve parametre hello ağ kurulumu için aşağıdaki dosyaları hello kullan:</span><span class="sxs-lookup"><span data-stu-id="da990-139">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for hello network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a><span data-ttu-id="da990-140">Merhaba Service Fabric kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="da990-140">Deploy hello Service Fabric cluster</span></span>

<span data-ttu-id="da990-141">Hello ağ kaynaklarını dağıtma tamamladıktan sonra hello sonraki toodeploy hello alt ağda bir Service Fabric kümesi toohello VNET adımdır ve NSG hello Service Fabric kümesi için belirlenmiş.</span><span class="sxs-lookup"><span data-stu-id="da990-141">Once hello network resources have finished deploying, hello next step is toodeploy a Service Fabric cluster toohello VNET in hello subnet and NSG designated for hello Service Fabric cluster.</span></span> <span data-ttu-id="da990-142">Bu öğretici için hello Service Fabric Resource Manager şablonu hello VNET, alt ağ ve hello önceki adımda ayarladığınız NSG önceden yapılandırılmış toouse hello adlarını ' dir.</span><span class="sxs-lookup"><span data-stu-id="da990-142">For this tutorial, hello Service Fabric Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

<span data-ttu-id="da990-143">Merhaba Service Fabric kümesi Resource Manager şablonu yapılandırılmış toocreate sertifika güvenliği ile güvenli bir kümede ' dir.</span><span class="sxs-lookup"><span data-stu-id="da990-143">hello Service Fabric cluster Resource Manager template is configured toocreate a secure cluster with certificate security.</span></span> <span data-ttu-id="da990-144">Merhaba, küme ve toomanage kullanıcı erişimi tooyour Service Fabric kümesi için kullanılan toosecure düğümü düğümü iletişim sertifikasıdır.</span><span class="sxs-lookup"><span data-stu-id="da990-144">hello certificate is used toosecure node-to-node communication for your cluster and toomanage user access tooyour Service Fabric cluster.</span></span> <span data-ttu-id="da990-145">API Management hizmet bulma için bu sertifika tooaccess hello Service Fabric adlandırma hizmeti kullanır.</span><span class="sxs-lookup"><span data-stu-id="da990-145">API Management uses this certificate tooaccess  hello Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="da990-146">Bu adım, bir sertifikanın anahtar kasası için küme güvenlik sonucunda gerektirir.</span><span class="sxs-lookup"><span data-stu-id="da990-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="da990-147">Anahtar kasası ile güvenli bir küme ayarlama hakkında daha fazla bilgi için bkz: [bu kılavuz Azure Kaynak Yöneticisi'ni kullanarak bir küme oluşturma](service-fabric-cluster-creation-via-arm.md)</span><span class="sxs-lookup"><span data-stu-id="da990-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="da990-148">Toplama toohello sertifikasında küme erişimi için kullanılan Azure Active Directory kimlik doğrulaması ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="da990-148">You may add Azure Active Directory authentication in addition toohello certificate used for cluster access.</span></span> <span data-ttu-id="da990-149">Azure Active Directory şekilde toomanage kullanıcı erişimi tooyour Service Fabric kümesi önerilen Merhaba, ancak bu öğreticide gerekli olmayan toocomplete gelir.</span><span class="sxs-lookup"><span data-stu-id="da990-149">Azure Active Directory is hello recommended way toomanage user access tooyour Service Fabric cluster, but is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="da990-150">Bir sertifika her iki durumda da Azure Active Directory ile bir Service Fabric arka ucu için kimlik doğrulaması şu anda desteklemiyor Azure API Management kimlik doğrulama ve küme düğümü, düğümü güvenlik için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="da990-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="da990-151">Aşağıdaki Resource Manager şablonu ve parametre dosyasına hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="da990-151">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="da990-152">[Cluster.JSON][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="da990-153">[Cluster.Parameters.JSON][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="da990-154">Merhaba boş hello parametrelerinde doldurun `cluster.parameters.json` hello dahil olmak üzere, dağıtımınız için dosya [anahtar kasası bilgileri](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) küme sertifikanızın.</span><span class="sxs-lookup"><span data-stu-id="da990-154">Fill in hello empty parameters in hello `cluster.parameters.json` file for your deployment, including hello [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="da990-155">PowerShell komut toodeploy hello Resource Manager şablonu ve parametre dosyalarını toocreate hello Service Fabric kümesi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="da990-155">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files toocreate hello Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="da990-156">API Management dağıtma</span><span class="sxs-lookup"><span data-stu-id="da990-156">Deploy API Management</span></span>

<span data-ttu-id="da990-157">Son olarak, API Management toohello VNET hello alt ağ ve API yönetimi için tasarlanmış NSG dağıtın.</span><span class="sxs-lookup"><span data-stu-id="da990-157">Finally, deploy API Management toohello VNET in hello subnet and NSG designated for API Management.</span></span> <span data-ttu-id="da990-158">Toowait hello Service Fabric küme dağıtım toofinish için API Management dağıtmadan önce gerekmez.</span><span class="sxs-lookup"><span data-stu-id="da990-158">You do not need toowait for hello Service Fabric cluster deployment toofinish before deploying API Management.</span></span> 

<span data-ttu-id="da990-159">Bu öğretici için hello API Management Resource Manager şablonu hello VNET, alt ağ ve hello önceki adımda ayarladığınız NSG önceden yapılandırılmış toouse hello adlarını ' dir.</span><span class="sxs-lookup"><span data-stu-id="da990-159">For this tutorial, hello API Management Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

 1. <span data-ttu-id="da990-160">Aşağıdaki Resource Manager şablonu ve parametre dosyasına hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="da990-160">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="da990-161">[apim.JSON][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="da990-162">[apim.Parameters.JSON][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="da990-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="da990-163">Merhaba boş hello parametrelerinde doldurun `apim.parameters.json` dağıtımınız için.</span><span class="sxs-lookup"><span data-stu-id="da990-163">Fill in hello empty parameters in hello `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="da990-164">PowerShell toodeploy hello Resource Manager şablonu ve parametre betikleri için API Management aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="da990-164">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="da990-165">API Management yapılandırın</span><span class="sxs-lookup"><span data-stu-id="da990-165">Configure API Management</span></span>

<span data-ttu-id="da990-166">API Management ve Service Fabric kümesi dağıtıldığı sonra Service Fabric arka uç API Management'te yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da990-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="da990-167">Bu, toocreate trafiği tooyour Service Fabric kümesi gönderir bir arka uç hizmeti ilke sağlar.</span><span class="sxs-lookup"><span data-stu-id="da990-167">This allows you toocreate a backend service policy that sends traffic tooyour Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="da990-168">API yönetim güvenliği</span><span class="sxs-lookup"><span data-stu-id="da990-168">API Management Security</span></span>

<span data-ttu-id="da990-169">tooconfigure hello Service Fabric arka uç, ilk tooconfigure API Management güvenlik ayarları gerekir.</span><span class="sxs-lookup"><span data-stu-id="da990-169">tooconfigure hello Service Fabric backend, you first need tooconfigure API Management security settings.</span></span> <span data-ttu-id="da990-170">tooconfigure güvenlik ayarları, hello Azure portal tooyour API Management hizmetine gidin.</span><span class="sxs-lookup"><span data-stu-id="da990-170">tooconfigure security settings, go tooyour API Management service in hello Azure portal.</span></span>

#### <a name="enable-hello-api-management-rest-api"></a><span data-ttu-id="da990-171">Merhaba API Management REST API etkinleştir</span><span class="sxs-lookup"><span data-stu-id="da990-171">Enable hello API Management REST API</span></span>

<span data-ttu-id="da990-172">Merhaba API Management REST API hello tek yolu tooconfigure bir arka uç hizmeti şu anda değil.</span><span class="sxs-lookup"><span data-stu-id="da990-172">hello API Management REST API is currently hello only way tooconfigure a backend service.</span></span> <span data-ttu-id="da990-173">Merhaba ilk adımı tooenable hello API Management REST API ve onu güvenli.</span><span class="sxs-lookup"><span data-stu-id="da990-173">hello first step is tooenable hello API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="da990-174">Hello API Management hizmeti, seçin **Yönetimi API - Önizleme** altında **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="da990-174">In hello API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="da990-175">Merhaba denetleyin **API Management REST API etkinleştir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="da990-175">Check hello **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="da990-176">Merhaba yönetim API'si URL Not - Bu hello URL hello Service Fabric arka uç yukarı sonraki tooset kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="da990-176">Note hello Management API URL - this is hello URL we'll use later tooset up hello Service Fabric backend</span></span>
 4. <span data-ttu-id="da990-177">Generate bir **belirtecine erişmesini** bir sona erme tarihi ve bir anahtar seçerek hello ardından **Oluştur** düğmesi hello sayfanın hello bulunun.</span><span class="sxs-lookup"><span data-stu-id="da990-177">Generate an **access Token** by selecting an expiry date and a key, then click hello **Generate** button toward hello bottom of hello page.</span></span>
 5. <span data-ttu-id="da990-178">Kopya hello **erişim belirteci** ve onu Kaydet - Bu adımları izleyerek hello kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="da990-178">Copy hello **access token** and save it - we'll use this in hello following steps.</span></span> <span data-ttu-id="da990-179">Bu hello birincil anahtar ve ikincil anahtar farklı olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="da990-179">Note this is different from hello primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="da990-180">Service Fabric istemci sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="da990-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="da990-181">API Management Service Fabric kümeniz erişim tooyour küme sahip bir istemci sertifikası kullanılarak hizmet bulma için kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="da990-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access tooyour cluster.</span></span> <span data-ttu-id="da990-182">Kolaylık olması için Bu öğretici kullanır, varsayılan olarak kullanılan tooaccess olabilecek hello Service Fabric kümesi oluştururken, belirtilen aynı sertifika kümenizi hello.</span><span class="sxs-lookup"><span data-stu-id="da990-182">For simplicity, this tutorial uses hello same certificate specified when creating hello Service Fabric cluster, which by default can be used tooaccess your cluster.</span></span>

 1. <span data-ttu-id="da990-183">Hello API Management hizmeti, seçin **istemci sertifikalarını - Önizleme** altında **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="da990-183">In hello API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="da990-184">Merhaba tıklatın **+ Ekle** düğmesi</span><span class="sxs-lookup"><span data-stu-id="da990-184">Click hello **+ Add** button</span></span>
 2. <span data-ttu-id="da990-185">Merhaba özel anahtar dosyası (.pfx), Service Fabric kümesi oluştururken, belirtilen hello küme sertifika seçin, bir ad verin ve hello özel anahtar parolası sağlayın.</span><span class="sxs-lookup"><span data-stu-id="da990-185">Select hello private key file (.pfx) of hello cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide hello private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="da990-186">Bu öğretici, istemci kimlik doğrulaması ve küme düğümü, düğümü güvenliği için aynı sertifika hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="da990-186">This tutorial uses hello same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="da990-187">Service Fabric kümesi bir yapılandırılmış tooaccess varsa, ayrı bir istemci sertifikası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da990-187">You may use a separate client certificate if you have one configured tooaccess your Service Fabric cluster.</span></span>

### <a name="configure-hello-backend"></a><span data-ttu-id="da990-188">Merhaba arka uç yapılandırın</span><span class="sxs-lookup"><span data-stu-id="da990-188">Configure hello backend</span></span>

<span data-ttu-id="da990-189">API Management güvenlik yapılandırıldığında, hello Service Fabric arka uç yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da990-189">Now that API Management security is configured, you can configure hello Service Fabric backend.</span></span> <span data-ttu-id="da990-190">Service Fabric arka uçlarını için belirli bir Service Fabric hizmeti yerine hello arka uç hello Service Fabric kümesi değil.</span><span class="sxs-lookup"><span data-stu-id="da990-190">For Service Fabric backends, hello Service Fabric cluster is hello backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="da990-191">Bu tek bir ilke tooroute toomore bir hizmet daha hello kümede sağlar.</span><span class="sxs-lookup"><span data-stu-id="da990-191">This allows a single policy tooroute toomore than one service in hello cluster.</span></span>

<span data-ttu-id="da990-192">Bu adım, daha önce oluşturulan hello erişim belirteci gerektirir ve tooAPI yönetim hello önceki adımda karşıya küme sertifikanızın parmak izi hello.</span><span class="sxs-lookup"><span data-stu-id="da990-192">This step requires hello access token you generated earlier and hello thumbprint for your cluster certificate you uploaded tooAPI Management in hello previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="da990-193">API Management hello önceki adımda ayrı istemci sertifikası kullandıysanız, bu adımda toplama toohello küme sertifika parmak izi hello istemci sertifikasını için hello parmak izi gerekir.</span><span class="sxs-lookup"><span data-stu-id="da990-193">If you used a separate client certificate in hello previous step for API Management, you need hello thumbprint for hello client certificate in addition toohello cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="da990-194">HTTP PUT İsteği toohello API yönetim API'si, daha önce hello API Management REST API tooconfigure hello Service Fabric arka uç hizmeti etkinleştirirken Not URL aşağıdaki hello gönderin.</span><span class="sxs-lookup"><span data-stu-id="da990-194">Send hello following HTTP PUT request toohello API Management API URL you noted earlier when enabling hello API Management REST API tooconfigure hello Service Fabric backend service.</span></span> <span data-ttu-id="da990-195">Görmeniz gerekir bir `HTTP 201 Created` hello komut başarılı olduğunda yanıt.</span><span class="sxs-lookup"><span data-stu-id="da990-195">You should see an `HTTP 201 Created` response when hello command succeeds.</span></span> <span data-ttu-id="da990-196">Her bir alan hakkında daha fazla bilgi için bkz: hello API Management [arka uç API başvuru belgeleri](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="da990-196">For more information on each field, see hello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="da990-197">HTTP komutu ve URL:</span><span class="sxs-lookup"><span data-stu-id="da990-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="da990-198">İstek üstbilgilerini:</span><span class="sxs-lookup"><span data-stu-id="da990-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="da990-199">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="da990-199">Request body:</span></span>
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

<span data-ttu-id="da990-200">Merhaba **url** burada parametredir hizmet kümenizdeki tüm istekleri tam hizmet adını yönlendirilen tooby varsayılan bir arka uç ilkesinde hiçbir hizmet adı belirtilirse.</span><span class="sxs-lookup"><span data-stu-id="da990-200">hello **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed tooby default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="da990-201">Sahte hizmet adı gibi kullanabilir "fabric: / sahte/service" toohave bir geri dönüş hizmet düşünmüyorsanız.</span><span class="sxs-lookup"><span data-stu-id="da990-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend toohave a fallback service.</span></span>

<span data-ttu-id="da990-202">API Management toohello başvuran [arka uç API başvuru belgeleri](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) her bir alan hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="da990-202">Refer toohello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="da990-203">Örnek</span><span class="sxs-lookup"><span data-stu-id="da990-203">Example</span></span>

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

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="da990-204">Service Fabric arka uç hizmet dağıtma</span><span class="sxs-lookup"><span data-stu-id="da990-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="da990-205">Service Fabric arka uç tooAPI yönetim yapılandırılmış hello sahip olduğunuza göre arka uç ilkeleri tooyour Service Fabric hizmetleri trafiği göndermek için API'leri yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da990-205">Now that you have hello Service Fabric configured as a backend tooAPI Management, you can author backend policies for your APIs that send traffic tooyour Service Fabric services.</span></span> <span data-ttu-id="da990-206">Ancak önce Service Fabric tooaccept isteklerinde çalışan bir hizmete gerekir.</span><span class="sxs-lookup"><span data-stu-id="da990-206">But first you need a service running in Service Fabric tooaccept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="da990-207">Bir HTTP uç noktası ile bir Service Fabric hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="da990-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="da990-208">Bu öğreticide, temel bir durum bilgisiz ASP.NET Core güvenilir hello varsayılan Web API projesi şablonunu kullanarak hizmet oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="da990-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using hello default Web API project template.</span></span> <span data-ttu-id="da990-209">Azure API Management kullanıma hizmetiniz için bir HTTP uç noktası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="da990-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="da990-210">Tarafından Başlat [ASP.NET Core geliştirme için geliştirme ortamınızı kurma](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="da990-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="da990-211">Geliştirme ortamınızı ayarladıktan sonra Visual Studio'yu yönetici olarak başlatın ve ASP.NET Core hizmet oluşturun:</span><span class="sxs-lookup"><span data-stu-id="da990-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="da990-212">Visual Studio'da yeni proje dosyası seçin ->.</span><span class="sxs-lookup"><span data-stu-id="da990-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="da990-213">Bulut altında Hello Service Fabric uygulaması şablonu seçin ve adlandırın **"ApiApplication"**.</span><span class="sxs-lookup"><span data-stu-id="da990-213">Select hello Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="da990-214">Merhaba ASP.NET çekirdek hizmet şablonu seçip adı hello proje **"WebApiService"**.</span><span class="sxs-lookup"><span data-stu-id="da990-214">Select hello ASP.NET Core service template and name hello project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="da990-215">Merhaba Web API ASP.NET Core 1.1 proje şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="da990-215">Select hello Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="da990-216">Merhaba Proje oluşturulduktan sonra açmak `PackageRoot\ServiceManifest.xml` hello kaldırıp `Port` hello uç nokta kaynak yapılandırması özniteliğinden:</span><span class="sxs-lookup"><span data-stu-id="da990-216">Once hello project is created, open `PackageRoot\ServiceManifest.xml` and remove hello `Port` attribute from hello endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="da990-217">Bu, bir bağlantı noktasından biz hello küme Resource Manager şablonu hello ağ güvenlik grubu üzerinden trafik tooflow tooit API Yönetimi'nden izin vererek açılan dinamik olarak hello uygulama bağlantı noktası aralığı, Service Fabric toospecify sağlar.</span><span class="sxs-lookup"><span data-stu-id="da990-217">This allows Service Fabric toospecify a port dynamically from hello application port range, which we opened through hello Network Security Group in hello cluster Resource Manager template, allowing traffic tooflow tooit from API Management.</span></span>
 
 6. <span data-ttu-id="da990-218">F5 tuşuna basarak Visual Studio tooverify hello Web API'de yerel olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="da990-218">Press F5 in Visual Studio tooverify hello web API is available locally.</span></span> 

    <span data-ttu-id="da990-219">Service Fabric Explorer'ı açın ve ASP.NET Core toosee hello taban adresi hello hizmeti dinlediği hello belirli örneği tooa detaya.</span><span class="sxs-lookup"><span data-stu-id="da990-219">Open Service Fabric Explorer and drill down tooa specific instance of hello ASP.NET Core service toosee hello base address hello service is listening on.</span></span> <span data-ttu-id="da990-220">Ekleme `/api/values` toohello temel adresi ve bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="da990-220">Add `/api/values` toohello base address and open it in a browser.</span></span> <span data-ttu-id="da990-221">Merhaba hello ValuesController hello Web API şablonunda Get yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="da990-221">This invokes hello Get method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="da990-222">İki dizeyi içeren bir JSON dizisi hello şablon tarafından sağlanan hello varsayılan yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="da990-222">It returns hello default response that is provided by hello template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="da990-223">Bu, Azure API Management'te aracılığıyla kullanıma hello uç noktadır.</span><span class="sxs-lookup"><span data-stu-id="da990-223">This is hello endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="da990-224">Son olarak, azure'da hello uygulama tooyour küme dağıtın.</span><span class="sxs-lookup"><span data-stu-id="da990-224">Finally, deploy hello application tooyour cluster in Azure.</span></span> <span data-ttu-id="da990-225">[Visual Studio kullanarak](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), hello uygulama projesine sağ tıklatın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="da990-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click hello Application project and select **Publish**.</span></span> <span data-ttu-id="da990-226">Küme uç noktası sağlayın (örneğin, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello uygulama tooyour Service Fabric kümesi Azure'da.</span><span class="sxs-lookup"><span data-stu-id="da990-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="da990-227">Adlı bir ASP.NET Core durum bilgisiz hizmeti `fabric:/ApiApplication/WebApiService` artık Azure Service Fabric kümenizdeki çalıştırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="da990-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="da990-228">Bir API işlem oluşturma</span><span class="sxs-lookup"><span data-stu-id="da990-228">Create an API operation</span></span>

<span data-ttu-id="da990-229">Hazır toocreate API Management bir işlem ki artık, dış istemcilere kullanım toocommunicate ile Merhaba Service Fabric kümede çalışan ASP.NET Core durum bilgisiz hizmeti hello.</span><span class="sxs-lookup"><span data-stu-id="da990-229">Now we're ready toocreate an operation in API Management that external clients use toocommunicate with hello ASP.NET Core stateless service running in hello Service Fabric cluster.</span></span>

 1. <span data-ttu-id="da990-230">Toohello Azure portalında oturum açın ve tooyour API Management hizmet dağıtımı gidin.</span><span class="sxs-lookup"><span data-stu-id="da990-230">Log in toohello Azure portal and navigate tooyour API Management service deployment.</span></span>
 2. <span data-ttu-id="da990-231">Merhaba API Management hizmeti dikey penceresinde, seçin **API'leri - Önizleme**</span><span class="sxs-lookup"><span data-stu-id="da990-231">In hello API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="da990-232">Merhaba tıklatarak yeni bir API eklemek **boş API** kutusu ve hello iletişim kutusunu doldurma:</span><span class="sxs-lookup"><span data-stu-id="da990-232">Add a new API by clicking hello **Blank API** box and filling out hello dialog box:</span></span>

     - <span data-ttu-id="da990-233">**Web hizmeti URL'si**: Service Fabric arka uçlarını için değil Bu URL değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="da990-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="da990-234">Herhangi bir değer buraya koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da990-234">You can put any value here.</span></span> <span data-ttu-id="da990-235">Bu öğretici için kullanın: `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="da990-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="da990-236">**Ad**: API'nizi için herhangi bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="da990-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="da990-237">Bu öğretici için kullanmak `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="da990-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="da990-238">**URL şeması**: HTTP, HTTPS ya da her ikisini de seçin.</span><span class="sxs-lookup"><span data-stu-id="da990-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="da990-239">Bu öğretici için kullanmak `both`.</span><span class="sxs-lookup"><span data-stu-id="da990-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="da990-240">**API'si URL soneki**: bir sonek için bizim API sağlar.</span><span class="sxs-lookup"><span data-stu-id="da990-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="da990-241">Bu öğretici için kullanmak `myapp`.</span><span class="sxs-lookup"><span data-stu-id="da990-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="da990-242">Merhaba API oluşturulduktan sonra tıklatın **+ ekleme işlemi** tooadd bir ön uç API işlemi.</span><span class="sxs-lookup"><span data-stu-id="da990-242">Once hello API is created, click **+ Add operation** tooadd a front-end API operation.</span></span> <span data-ttu-id="da990-243">Merhaba değerlere doldurun:</span><span class="sxs-lookup"><span data-stu-id="da990-243">Fill out hello values:</span></span>
    
     - <span data-ttu-id="da990-244">**URL**: seçin `GET` ve API hello için bir URL yolu sağlayın.</span><span class="sxs-lookup"><span data-stu-id="da990-244">**URL**: Select `GET` and provide a URL path for hello API.</span></span> <span data-ttu-id="da990-245">Bu öğretici için kullanmak `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="da990-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="da990-246">Varsayılan olarak, hello URL yolu toohello arka uç Service Fabric hizmeti gönderilen hello URL yolu burada belirtilen.</span><span class="sxs-lookup"><span data-stu-id="da990-246">By default, hello URL path specified here is hello URL path sent toohello backend Service Fabric service.</span></span> <span data-ttu-id="da990-247">Merhaba kullanırsanız, hizmetiniz kullanır, bu durumda aynı URL yolunu Buraya `/api/values`, sonra hello işlemi daha fazla değişiklik yapılmadan çalışır.</span><span class="sxs-lookup"><span data-stu-id="da990-247">If you use hello same URL path here that your service uses, in this case `/api/values`, then hello operation works without further modification.</span></span> <span data-ttu-id="da990-248">Bu durumda, gerek toospecify bir yolu yeniden yazma işlemi ilkenizde daha sonra kazandırır hello URL yolu, arka uç Service Fabric hizmeti tarafından kullanılan farklı bir URL yolu buraya de belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="da990-248">You may also specify a URL path here that is different from hello URL path used by your backend Service Fabric service, in which case you will also need toospecify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="da990-249">**Görünen ad**: hello API için herhangi bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="da990-249">**Display name**: Provide any name for hello API.</span></span> <span data-ttu-id="da990-250">Bu öğretici için kullanmak `Values`.</span><span class="sxs-lookup"><span data-stu-id="da990-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="da990-251">Arka uç ilkesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="da990-251">Configure a backend policy</span></span>

<span data-ttu-id="da990-252">Merhaba arka uç ilke her şeyi birbirine bağlar.</span><span class="sxs-lookup"><span data-stu-id="da990-252">hello backend policy ties everything together.</span></span> <span data-ttu-id="da990-253">Merhaba arka uç hizmeti toowhich istekleri yönlendirilir Service Fabric yapılandırdığınız budur.</span><span class="sxs-lookup"><span data-stu-id="da990-253">This is where you configure hello backend Service Fabric service toowhich requests are routed.</span></span> <span data-ttu-id="da990-254">Bu ilke tooany API işlemi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da990-254">You can apply this policy tooany API operation.</span></span> <span data-ttu-id="da990-255">Merhaba [Service Fabric için arka uç yapılandırması](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) hello aşağıdaki isteği yönlendirme denetimleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="da990-255">hello [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides hello following request routing controls:</span></span> 
 - <span data-ttu-id="da990-256">Hizmet örneği seçimi ya da sabit kodlanmış bir Service Fabric hizmeti örnek adı belirterek (örneğin, `"fabric:/myapp/myservice"`) veya hello HTTP isteğinden oluşturulan (örneğin, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="da990-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from hello HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="da990-257">Tüm Service Fabric bölümleme düzenini kullanarak bir bölüm anahtarı oluşturma tarafından bölüm çözünürlüğü.</span><span class="sxs-lookup"><span data-stu-id="da990-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="da990-258">Durum bilgisi olan hizmetler için çoğaltma seçimi.</span><span class="sxs-lookup"><span data-stu-id="da990-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="da990-259">Çözümleme için bir hizmet konumu yeniden çözümlemeyi ve isteği yeniden göndermeyi toospecify hello koşulları izin koşulları yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="da990-259">Resolution retry conditions that allow you toospecify hello conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="da990-260">Bu öğretici için yollar isteklerinin doğrudan toohello daha önce dağıtılan durum bilgisiz hizmet ASP.NET Core bir arka uç ilkesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="da990-260">For this tutorial, create a backend policy that routes requests directly toohello ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="da990-261">Seçme ve düzenleme hello **gelen ilkeleri** hello için `Values` hello Düzenle simgesine tıklayarak ve ardından seçerek işlemi **kod görünümü**.</span><span class="sxs-lookup"><span data-stu-id="da990-261">Select and edit hello **inbound policies** for hello `Values` operation by clicking hello edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="da990-262">Hello İlkesi Kod düzenleyicisinde ekleyin bir `set-backend-service` ilkesi altında aşağıda gösterildiği gibi ilkeleri gelen ve hello tıklatın **kaydetmek** düğmesi:</span><span class="sxs-lookup"><span data-stu-id="da990-262">In hello policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click hello **Save** button:</span></span>
    
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

<span data-ttu-id="da990-263">Service Fabric arka uç İlkesi özniteliklerini tam kümesi için toohello başvuran [API Management arka uç belgeleri](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="da990-263">For a full set of Service Fabric back-end policy attributes, refer toohello [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-hello-api-tooa-product"></a><span data-ttu-id="da990-264">Merhaba API tooa ürün ekleyin.</span><span class="sxs-lookup"><span data-stu-id="da990-264">Add hello API tooa product.</span></span> 

<span data-ttu-id="da990-265">Merhaba API aramadan önce burada erişim toousers verebilirsiniz tooa ürün eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="da990-265">Before you can call hello API, it must be added tooa product where you can grant access toousers.</span></span> 

 1. <span data-ttu-id="da990-266">Hello API Management hizmeti, seçin **ürünler - Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="da990-266">In hello API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="da990-267">Varsayılan olarak, API Management sağlayıcıları iki ürünler: Starter ve sınırsız.</span><span class="sxs-lookup"><span data-stu-id="da990-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="da990-268">Merhaba sınırsız ürün seçin.</span><span class="sxs-lookup"><span data-stu-id="da990-268">Select hello Unlimited product.</span></span>
 3. <span data-ttu-id="da990-269">API seçin.</span><span class="sxs-lookup"><span data-stu-id="da990-269">Select APIs.</span></span>
 4. <span data-ttu-id="da990-270">Merhaba tıklatın **+ Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="da990-270">Click hello **+ Add** button.</span></span>
 5. <span data-ttu-id="da990-271">Select hello `Service Fabric App` hello önceki adımlarda oluşturduğunuz ve hello tıklatın API **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="da990-271">Select hello `Service Fabric App` API you created in hello previous steps and click hello **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="da990-272">test</span><span class="sxs-lookup"><span data-stu-id="da990-272">Test it</span></span>

<span data-ttu-id="da990-273">Şimdi doğrudan hello Azure Portalı ' Service Fabric API Management ile bir istek tooyour arka uç hizmeti gönderme deneyin.</span><span class="sxs-lookup"><span data-stu-id="da990-273">You can now try sending a request tooyour back-end service in Service Fabric through API Management directly from hello Azure portal.</span></span>

 1. <span data-ttu-id="da990-274">Hello API Management hizmeti, seçin **API - Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="da990-274">In hello API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="da990-275">Merhaba, `Service Fabric App` hello önceki adımlarda oluşturduğunuz API seçin hello **Test** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="da990-275">In hello `Service Fabric App` API you created in hello previous steps, select hello **Test** tab.</span></span>
 3. <span data-ttu-id="da990-276">Merhaba tıklatın **Gönder** düğmesini toosend bir test isteği toohello arka uç hizmeti.</span><span class="sxs-lookup"><span data-stu-id="da990-276">Click hello **Send** button toosend a test request toohello backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da990-277">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="da990-277">Next steps</span></span>

<span data-ttu-id="da990-278">Bu noktada, Service Fabric ve API Management temel bir kurulumu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="da990-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="da990-279">Bu öğretici, hızlı bir şekilde ayarlamak, Service Fabric kümesi tooget için temel kullanıcı sertifika tabanlı kimlik doğrulaması kullanır.</span><span class="sxs-lookup"><span data-stu-id="da990-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster tooget you set up quickly.</span></span> <span data-ttu-id="da990-280">Service Fabric kümesi için daha gelişmiş kullanıcı kimlik doğrulaması ile tercih [Azure Active Directory kimlik doğrulaması](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="da990-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="da990-281">Ardından, [oluşturma ve Gelişmiş Ürün ayarları Azure API Management'te yapılandırma](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare uygulamanızı gerçek dünya trafiği için.</span><span class="sxs-lookup"><span data-stu-id="da990-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare your application for real world traffic.</span></span>

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

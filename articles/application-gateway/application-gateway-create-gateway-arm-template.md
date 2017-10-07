---
title: "Azure uygulama ağ geçidi - şablonları aaaCreate | Microsoft Docs"
description: "Bu sayfa, hello Azure Resource Manager şablonu kullanarak bir Azure uygulama ağ geçidi yönergeleri toocreate sağlar"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a><span data-ttu-id="a667c-103">Hello Azure Resource Manager şablonu kullanarak bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a667c-103">Create an application gateway by using hello Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a667c-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="a667c-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="a667c-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="a667c-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="a667c-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="a667c-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="a667c-107">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="a667c-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="a667c-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a667c-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="a667c-109">Azure Application Gateway, bir katman 7 yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="a667c-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="a667c-110">Merhaba Bulut veya şirket içi olup, yük devretme ve performans yönlendirme HTTP isteklerini, farklı sunucular arasında sağlar.</span><span class="sxs-lookup"><span data-stu-id="a667c-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="a667c-111">Application Gateway; HTTP yük dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) boşaltma, özel sistem durumu araştırmaları, çoklu site desteği gibi birçok uygulama teslim denetleyicisi (ADC) özelliği sunar.</span><span class="sxs-lookup"><span data-stu-id="a667c-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="a667c-112">toofind desteklenen özelliklerin tam bir listesi ziyaret [uygulama ağ geçidi'ne genel bakış](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="a667c-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="a667c-113">Bu makalede, indirme ve var olan bir Azure Resource Manager şablonunu github'dan değiştirme ve hello şablonu GitHub, PowerShell ve Azure CLI hello dağıtma anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a667c-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="a667c-114">Yalnızca hello Azure Resource Manager şablonu herhangi bir değişiklik yapmadan doğrudan github'dan dağıtıyorsanız, Github'dan şablon toodeploy atlayın.</span><span class="sxs-lookup"><span data-stu-id="a667c-114">If you are simply deploying hello Azure Resource Manager template directly from GitHub without any changes, skip toodeploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="a667c-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="a667c-115">Scenario</span></span>

<span data-ttu-id="a667c-116">Bu senaryoda:</span><span class="sxs-lookup"><span data-stu-id="a667c-116">In this scenario you will:</span></span>

* <span data-ttu-id="a667c-117">Bir uygulama ağ geçidi ile web uygulaması güvenlik duvarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a667c-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="a667c-118">Ayrılmış 10.0.0.0/16 CIDR bloğu olan, VirtualNetwork1 adlı bir sanal ağ oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a667c-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="a667c-119">Appgatewaysubnet adlı, CIDR bloğu olarak 10.0.0.0/28 kullanan bir alt ağ oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a667c-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="a667c-120">Merhaba web sunucuları için önceden yapılandırılmış iki arka uç IP'leri ayarlamak tooload hello trafiği dengelemek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="a667c-120">Set up two previously configured back-end IPs for hello web servers you want tooload balance hello traffic.</span></span> <span data-ttu-id="a667c-121">Bu şablon örneğinde hello arka uç IP de 10.0.1.10 ve 10.0.1.11.olacak.</span><span class="sxs-lookup"><span data-stu-id="a667c-121">In this template example, hello back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="a667c-122">Bu ayarlar, bu şablonu hello parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="a667c-122">Those settings are hello parameters for this template.</span></span> <span data-ttu-id="a667c-123">toocustomize hello şablonu, kurallar, hello dinleyicisi, SSL ve diğer seçenekleri hello azuredeploy.json dosyasını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a667c-123">toocustomize hello template, you can change rules, hello listener, SSL, and other options in hello azuredeploy.json file.</span></span>

![Senaryo](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="a667c-125">İndirme ve hello Azure Resource Manager şablonu anlama</span><span class="sxs-lookup"><span data-stu-id="a667c-125">Download and understand hello Azure Resource Manager template</span></span>

<span data-ttu-id="a667c-126">Merhaba mevcut Azure Resource Manager şablonu toocreate bir sanal ağ ve iki alt Github'dan indirdiğinizde, istediğiniz ve yeniden tüm değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="a667c-126">You can download hello existing Azure Resource Manager template toocreate a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="a667c-127">toodo, bu nedenle, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="a667c-127">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="a667c-128">Çok gidin[etkin web uygulaması güvenlik duvarı ile uygulama ağ geçidi oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="a667c-128">Navigate too[Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="a667c-129">**azuredeploy.json** ve **RAW** öğelerine sırayla tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a667c-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="a667c-130">Merhaba dosya tooa yerel klasör bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a667c-130">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="a667c-131">Azure Resource Manager şablonları hakkında bilginiz varsa 7 toostep atlayın.</span><span class="sxs-lookup"><span data-stu-id="a667c-131">If you are familiar with Azure Resource Manager templates, skip toostep 7.</span></span>
1. <span data-ttu-id="a667c-132">Kaydettiğiniz hello dosyasını açın ve altındaki hello içeriğe bakın **parametreleri** satırında</span><span class="sxs-lookup"><span data-stu-id="a667c-132">Open hello file that you saved and look at hello contents under **parameters** in line</span></span>
1. <span data-ttu-id="a667c-133">Azure Resource Manager şablonu parametreleri, dağıtım sırasında doldurulabilecek değerler için yer tutucu sağlar.</span><span class="sxs-lookup"><span data-stu-id="a667c-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="a667c-134">Parametre</span><span class="sxs-lookup"><span data-stu-id="a667c-134">Parameter</span></span> | <span data-ttu-id="a667c-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a667c-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="a667c-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="a667c-136">**subnetPrefix**</span></span> |<span data-ttu-id="a667c-137">Merhaba uygulama ağ geçidi alt ağının CIDR bloğu.</span><span class="sxs-lookup"><span data-stu-id="a667c-137">CIDR block for hello application gateway subnet.</span></span> |
  | <span data-ttu-id="a667c-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="a667c-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="a667c-139">Merhaba uygulama ağ geçidi boyutu.</span><span class="sxs-lookup"><span data-stu-id="a667c-139">Size of hello application gateway.</span></span>  <span data-ttu-id="a667c-140">WAF yalnızca orta ve büyük ölçekli izin verir.</span><span class="sxs-lookup"><span data-stu-id="a667c-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="a667c-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="a667c-141">**backendIpaddress1**</span></span> |<span data-ttu-id="a667c-142">Merhaba ilk web sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="a667c-142">IP address of hello first web server.</span></span> |
  | <span data-ttu-id="a667c-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="a667c-143">**backendIpaddress2**</span></span> |<span data-ttu-id="a667c-144">Merhaba ikinci web sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="a667c-144">IP address of hello second web server.</span></span> |
  | <span data-ttu-id="a667c-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="a667c-145">**wafEnabled**</span></span> | <span data-ttu-id="a667c-146">WAF etkinleştirilirse toodetermine ayarlama.</span><span class="sxs-lookup"><span data-stu-id="a667c-146">Setting toodetermine if WAF is enabled.</span></span>|
  | <span data-ttu-id="a667c-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="a667c-147">**wafMode**</span></span> | <span data-ttu-id="a667c-148">Merhaba web uygulaması güvenlik duvarı modu.</span><span class="sxs-lookup"><span data-stu-id="a667c-148">Mode of hello web application firewall.</span></span>  <span data-ttu-id="a667c-149">Kullanılabilir seçenekler **önleme** veya **algılama**.</span><span class="sxs-lookup"><span data-stu-id="a667c-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="a667c-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="a667c-150">**wafRuleSetType**</span></span> | <span data-ttu-id="a667c-151">WAF RuleSet türü.</span><span class="sxs-lookup"><span data-stu-id="a667c-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="a667c-152">Şu anda OWASP hello seçeneği yalnızca desteklenen değil.</span><span class="sxs-lookup"><span data-stu-id="a667c-152">Currently OWASP is hello only supported option.</span></span> |
  | <span data-ttu-id="a667c-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="a667c-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="a667c-154">RuleSet sürümü.</span><span class="sxs-lookup"><span data-stu-id="a667c-154">Ruleset version.</span></span> <span data-ttu-id="a667c-155">Şu anda desteklenen hello seçenekler OWASP CRS 2.2.9 ve 3.0 belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a667c-155">OWASP CRS 2.2.9 and 3.0 are currently hello supported options.</span></span> |

1. <span data-ttu-id="a667c-156">Merhaba içeriği altında denetleyin **kaynakları** ve bildirimi hello aşağıdaki özellikleri:</span><span class="sxs-lookup"><span data-stu-id="a667c-156">Check hello content under **resources** and notice hello following properties:</span></span>

   * <span data-ttu-id="a667c-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="a667c-157">**type**.</span></span> <span data-ttu-id="a667c-158">Merhaba şablon tarafından oluşturulan kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="a667c-158">Type of resource being created by hello template.</span></span> <span data-ttu-id="a667c-159">Bu durumda, hello türüdür `Microsoft.Network/applicationGateways`, bir uygulama ağ geçidini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a667c-159">In this case, hello type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="a667c-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="a667c-160">**name**.</span></span> <span data-ttu-id="a667c-161">Merhaba kaynak adı.</span><span class="sxs-lookup"><span data-stu-id="a667c-161">Name for hello resource.</span></span> <span data-ttu-id="a667c-162">Bildirim hello kullanımını `[parameters('applicationGatewayName')]`, bu hello adı başka bir deyişle, girdi olarak sizin tarafınızdan veya bir parametre dosyası dağıtımı sırasında sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a667c-162">Notice hello use of `[parameters('applicationGatewayName')]`, which means that hello name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="a667c-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="a667c-163">**properties**.</span></span> <span data-ttu-id="a667c-164">Merhaba kaynak özelliklerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="a667c-164">List of properties for hello resource.</span></span> <span data-ttu-id="a667c-165">Bu şablon, uygulama ağ geçidi oluşturma sırasında hello sanal ağ ve genel IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="a667c-165">This template uses hello virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a667c-166">Şablonlar hakkında daha fazla bilgi için ziyaret edin: [Resource Manager şablonları başvurusu](/templates/)</span><span class="sxs-lookup"><span data-stu-id="a667c-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="a667c-167">Geri çok gidin[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="a667c-167">Navigate back too[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="a667c-168">Tıklatın **azuredeploy-parameters.json**ve ardından **RAW**.</span><span class="sxs-lookup"><span data-stu-id="a667c-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="a667c-169">Merhaba dosya tooa yerel klasör bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a667c-169">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="a667c-170">Kaydettiğiniz hello dosyasını açın ve hello parametreleri hello değerlerini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="a667c-170">Open hello file that you saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="a667c-171">Senaryomuzda açıklanan değerleri toodeploy hello uygulama ağ geçidi aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="a667c-171">Use hello following values toodeploy hello application gateway described in our scenario.</span></span>

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. <span data-ttu-id="a667c-172">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a667c-172">Save hello file.</span></span> <span data-ttu-id="a667c-173">Merhaba JSON şablonunu ve parametre şablonunu gibi çevrimiçi JSON doğrulama araçlarını kullanarak test edebilirsiniz [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="a667c-173">You can test hello JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="a667c-174">PowerShell kullanarak Hello Azure Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="a667c-174">Deploy hello Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="a667c-175">Azure PowerShell'i hiç kullanmadıysanız, ziyaret edin: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) Azure'da hello yönergeleri toosign izleyin ve aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="a667c-175">If you have never used Azure PowerShell, visit: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions toosign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="a667c-176">Oturum açma tooPowerShell</span><span class="sxs-lookup"><span data-stu-id="a667c-176">Login tooPowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="a667c-177">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="a667c-177">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="a667c-178">Kimlik bilgilerinizle istendiğinde tooauthenticate var.</span><span class="sxs-lookup"><span data-stu-id="a667c-178">You are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="a667c-179">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="a667c-179">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="a667c-180">Gerekirse, hello kullanarak bir kaynak grubu oluşturma **New-AzureResourceGroup** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a667c-180">If needed, create a resource group by using hello **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="a667c-181">Aşağıdaki örnek hello, Doğu ABD konumunda AppgatewayRG adlı bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a667c-181">In hello following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="a667c-182">Merhaba çalıştırmak **New-AzureRmResourceGroupDeployment** indirdiğiniz ve değiştirdiğiniz şablonu ve parametre dosyalarını önceki hello kullanarak cmdlet toodeploy hello yeni sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="a667c-182">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toodeploy hello new virtual network by using hello preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a><span data-ttu-id="a667c-183">Hello Azure CLI kullanarak Hello Azure Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="a667c-183">Deploy hello Azure Resource Manager template by using hello Azure CLI</span></span>

<span data-ttu-id="a667c-184">Azure CLI kullanarak indirdiğiniz toodeploy hello Azure Resource Manager şablonu hello aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a667c-184">toodeploy hello Azure Resource Manager template you downloaded by using Azure CLI, follow hello following steps:</span></span>

1. <span data-ttu-id="a667c-185">Azure CLI hiç kullanmadıysanız bkz [yükleyin ve hello Azure CLI yapılandırma](/cli/azure/install-azure-cli) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="a667c-185">If you have never used Azure CLI, see [Install and configure hello Azure CLI](/cli/azure/install-azure-cli) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="a667c-186">Gerekli olduğunda, çalışma hello `az group create` komutu toocreate hello aşağıdaki kod parçacığında gösterildiği gibi bir kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="a667c-186">If necessary, run hello `az group create` command toocreate a resource group, as shown in hello following code snippet.</span></span> <span data-ttu-id="a667c-187">Merhaba hello komutunun çıkışını dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a667c-187">Notice hello output of hello command.</span></span> <span data-ttu-id="a667c-188">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a667c-188">hello list shown after hello output explains hello parameters used.</span></span> <span data-ttu-id="a667c-189">Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md) sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="a667c-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="a667c-190">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="a667c-190">**-n (or --name)**.</span></span> <span data-ttu-id="a667c-191">Merhaba yeni kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="a667c-191">Name for hello new resource group.</span></span> <span data-ttu-id="a667c-192">Senaryomuz için bu ad, *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="a667c-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="a667c-193">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="a667c-193">**-l (or --location)**.</span></span> <span data-ttu-id="a667c-194">Merhaba yeni kaynak grubunun oluşturulduğu azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="a667c-194">Azure region where hello new resource group is created.</span></span> <span data-ttu-id="a667c-195">Bizim senaryomuz için sahip *westus*.</span><span class="sxs-lookup"><span data-stu-id="a667c-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="a667c-196">Merhaba çalıştırmak `az group deployment create` hello şablonu ve parametre kullanarak cmdlet toodeploy hello yeni sanal ağ indirdiğiniz ve değiştirdiğiniz adım önceki hello dosyaları.</span><span class="sxs-lookup"><span data-stu-id="a667c-196">Run hello `az group deployment create` cmdlet toodeploy hello new virtual network by using hello template and parameter files you downloaded and modified in hello preceding step.</span></span> <span data-ttu-id="a667c-197">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a667c-197">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="a667c-198">Dağıtmak için kullanarak Hello Azure Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="a667c-198">Deploy hello Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="a667c-199">Dağıtmak için başka bir şekilde toouse Azure Resource Manager şablonları olur.</span><span class="sxs-lookup"><span data-stu-id="a667c-199">Click-to-deploy is another way toouse Azure Resource Manager templates.</span></span> <span data-ttu-id="a667c-200">Hello Azure portalında kolay bir yolu toouse şablonlarıyla olur.</span><span class="sxs-lookup"><span data-stu-id="a667c-200">It's an easy way toouse templates with hello Azure portal.</span></span>

1. <span data-ttu-id="a667c-201">Çok Git[web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="a667c-201">Go too[Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="a667c-202">Tıklatın **tooAzure dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="a667c-202">Click **Deploy tooAzure**.</span></span>

    ![TooAzure dağıtma](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="a667c-204">Hello dağıtım şablonu hello portalındaki hello parametrelerini doldurun ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a667c-204">Fill out hello parameters for hello deployment template on hello portal and click **OK**.</span></span>

    ![Parametreler](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="a667c-206">Seçin **toohello hüküm ve koşullar yukarıda belirtildiği kabul** tıklatıp **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="a667c-206">Select **I agree toohello terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="a667c-207">Merhaba özel dağıtım dikey penceresinde **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="a667c-207">On hello Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-tooresource-manager-templates"></a><span data-ttu-id="a667c-208">Sertifika verileri tooResource Manager şablonları sağlama</span><span class="sxs-lookup"><span data-stu-id="a667c-208">Providing certificate data tooResource Manager templates</span></span>

<span data-ttu-id="a667c-209">SSL sahip bir şablon kullanırken hello sertifikanın karşıya yüklenen yerine bir base64 dizesi sağlanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a667c-209">When using SSL with a template, hello certificate needs toobe provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="a667c-210">tooconvert bir .pfx veya .cer tooa base64 dizesi komutları aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a667c-210">tooconvert a .pfx or .cer tooa base64 string use one of hello following commands.</span></span> <span data-ttu-id="a667c-211">Merhaba aşağıdaki komutları toohello şablonu sağlanan hello sertifika tooa base64 dizesi, dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="a667c-211">hello following commands convert hello certificate tooa base64 string, which can be provided toohello template.</span></span> <span data-ttu-id="a667c-212">Merhaba çıktı bir değişkende depolanan ve hello şablonunda yapıştırılan bir dize bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="a667c-212">hello expected output is a string that can be stored in a variable and pasted in hello template.</span></span>

### <a name="macos"></a><span data-ttu-id="a667c-213">macOS</span><span class="sxs-lookup"><span data-stu-id="a667c-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="a667c-214">Windows</span><span class="sxs-lookup"><span data-stu-id="a667c-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="a667c-215">Tüm kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="a667c-215">Delete all resources</span></span>

<span data-ttu-id="a667c-216">Bu makalede, aşağıdaki adımları hello tam bir oluşturulan tüm kaynakları toodelete:</span><span class="sxs-lookup"><span data-stu-id="a667c-216">toodelete all resources created in this article, complete one of hello following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="a667c-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a667c-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="a667c-218">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a667c-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="a667c-219">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a667c-219">Next steps</span></span>

<span data-ttu-id="a667c-220">SSL boşaltma tooconfigure istiyorsanız, ziyaret edin: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="a667c-220">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="a667c-221">Bir iç yük dengeleyici ile bir uygulama ağ geçidi toouse tooconfigure istiyorsanız, ziyaret edin: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="a667c-221">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="a667c-222">Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.:</span><span class="sxs-lookup"><span data-stu-id="a667c-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="a667c-223">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="a667c-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="a667c-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="a667c-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)


---
title: "Azure uygulama ağ geçidi - şablonları oluşturma | Microsoft Docs"
description: "Bu sayfa, Azure Resource Manager şablonunu kullanarak, Azure uygulama ağ geçidi oluşturma yönergelerini verir."
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
ms.openlocfilehash: 46cca89ccb5bd77d57fabc3e9027fcebd38da8e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="e0596-103">Azure Resource Manager şablonunu kullanarak uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0596-103">Create an application gateway by using the Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0596-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e0596-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="e0596-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0596-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="e0596-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0596-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="e0596-107">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="e0596-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="e0596-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e0596-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="e0596-109">Azure Application Gateway, bir katman 7 yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="e0596-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="e0596-110">Bulutta veya şirket içinde olmalarından bağımsız olarak, farklı sunucular arasında yük devretme ve performans yönlendirmeli HTTP istekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0596-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="e0596-111">Application Gateway; HTTP yük dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) boşaltma, özel sistem durumu araştırmaları, çoklu site desteği gibi birçok uygulama teslim denetleyicisi (ADC) özelliği sunar.</span><span class="sxs-lookup"><span data-stu-id="e0596-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="e0596-112">Desteklenen özelliklerin tam listesi için ziyaret edin [uygulama ağ geçidi'ne genel bakış](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="e0596-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="e0596-113">Bu makalede, indirme ve var olan bir Azure Resource Manager şablonunu github'dan değiştirme ve şablonu GitHub, PowerShell ve Azure CLI dağıtımı aracılığıyla anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e0596-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="e0596-114">Azure Resource Manager şablonunu hiçbir değişiklik yapmadan doğrudan GitHub'dan dağıtıyorsanız, GitHub'dan şablon dağıtma bölümüne atlayın.</span><span class="sxs-lookup"><span data-stu-id="e0596-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="e0596-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="e0596-115">Scenario</span></span>

<span data-ttu-id="e0596-116">Bu senaryoda:</span><span class="sxs-lookup"><span data-stu-id="e0596-116">In this scenario you will:</span></span>

* <span data-ttu-id="e0596-117">Bir uygulama ağ geçidi ile web uygulaması güvenlik duvarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e0596-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="e0596-118">Ayrılmış 10.0.0.0/16 CIDR bloğu olan, VirtualNetwork1 adlı bir sanal ağ oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e0596-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="e0596-119">Appgatewaysubnet adlı, CIDR bloğu olarak 10.0.0.0/28 kullanan bir alt ağ oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e0596-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="e0596-120">Trafik yük dengelemesi yapmak istediğiniz web sunucuları için, önceden yapılandırılmış iki arka uç IP’si ayarlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e0596-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="e0596-121">Bu şablon örneğinde arka uç IP’leri 10.0.1.10 ve 10.0.1.11’dir.</span><span class="sxs-lookup"><span data-stu-id="e0596-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="e0596-122">Bu ayarlar, bu şablonun parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="e0596-122">Those settings are the parameters for this template.</span></span> <span data-ttu-id="e0596-123">Şablonu özelleştirmek için kuralları, dinleyiciyi, SSL ve diğer seçenekleri azuredeploy.json dosyasını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0596-123">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span></span>

![Senaryo](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="e0596-125">Azure Resource Manager şablonu indirme ve anlama</span><span class="sxs-lookup"><span data-stu-id="e0596-125">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="e0596-126">GitHub’dan sanal ağ ve iki adet alt ağ oluşturmak için, mevcut Azure Resource Manager şablonunu indirebilir, istediğiniz değişikliği yapabilir ve yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0596-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="e0596-127">Bunu yapmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="e0596-127">To do so, use the following steps:</span></span>

1. <span data-ttu-id="e0596-128">Gidin [etkin web uygulaması güvenlik duvarı ile uygulama ağ geçidi oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="e0596-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="e0596-129">**azuredeploy.json** ve **RAW** öğelerine sırayla tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0596-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="e0596-130">Dosyayı bilgisayarınızdaki yerel bir klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e0596-130">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="e0596-131">Eğer Azure Resource Manager şablonları hakkında bilginiz varsa, 7. adıma atlayın.</span><span class="sxs-lookup"><span data-stu-id="e0596-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="e0596-132">Kaydettiğiniz dosyayı açın ve altındaki içeriğe bakın **parametreleri** satırında</span><span class="sxs-lookup"><span data-stu-id="e0596-132">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="e0596-133">Azure Resource Manager şablonu parametreleri, dağıtım sırasında doldurulabilecek değerler için yer tutucu sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0596-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="e0596-134">Parametre</span><span class="sxs-lookup"><span data-stu-id="e0596-134">Parameter</span></span> | <span data-ttu-id="e0596-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e0596-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="e0596-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="e0596-136">**subnetPrefix**</span></span> |<span data-ttu-id="e0596-137">Uygulama ağ geçidi alt ağının CIDR bloğu.</span><span class="sxs-lookup"><span data-stu-id="e0596-137">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="e0596-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="e0596-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="e0596-139">Uygulama ağ geçidi boyutu.</span><span class="sxs-lookup"><span data-stu-id="e0596-139">Size of the application gateway.</span></span>  <span data-ttu-id="e0596-140">WAF yalnızca orta ve büyük ölçekli izin verir.</span><span class="sxs-lookup"><span data-stu-id="e0596-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="e0596-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="e0596-141">**backendIpaddress1**</span></span> |<span data-ttu-id="e0596-142">İlk web sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="e0596-142">IP address of the first web server.</span></span> |
  | <span data-ttu-id="e0596-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="e0596-143">**backendIpaddress2**</span></span> |<span data-ttu-id="e0596-144">İkinci web sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="e0596-144">IP address of the second web server.</span></span> |
  | <span data-ttu-id="e0596-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="e0596-145">**wafEnabled**</span></span> | <span data-ttu-id="e0596-146">WAF etkin olup olmadığını belirlemek için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="e0596-146">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="e0596-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="e0596-147">**wafMode**</span></span> | <span data-ttu-id="e0596-148">Web uygulaması güvenlik duvarı modu.</span><span class="sxs-lookup"><span data-stu-id="e0596-148">Mode of the web application firewall.</span></span>  <span data-ttu-id="e0596-149">Kullanılabilir seçenekler **önleme** veya **algılama**.</span><span class="sxs-lookup"><span data-stu-id="e0596-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="e0596-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="e0596-150">**wafRuleSetType**</span></span> | <span data-ttu-id="e0596-151">WAF RuleSet türü.</span><span class="sxs-lookup"><span data-stu-id="e0596-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="e0596-152">Şu anda OWASP yalnızca desteklenen bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="e0596-152">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="e0596-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="e0596-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="e0596-154">RuleSet sürümü.</span><span class="sxs-lookup"><span data-stu-id="e0596-154">Ruleset version.</span></span> <span data-ttu-id="e0596-155">Şu anda desteklenen seçenekler OWASP CRS 2.2.9 ve 3.0 belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e0596-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |

1. <span data-ttu-id="e0596-156">Altındaki içeriği denetleyin **kaynakları** ve aşağıdaki özelliklere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="e0596-156">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="e0596-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="e0596-157">**type**.</span></span> <span data-ttu-id="e0596-158">Şablon tarafından oluşturulan kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="e0596-158">Type of resource being created by the template.</span></span> <span data-ttu-id="e0596-159">Bu durumda, türüdür `Microsoft.Network/applicationGateways`, bir uygulama ağ geçidini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e0596-159">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="e0596-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="e0596-160">**name**.</span></span> <span data-ttu-id="e0596-161">Kaynağın adı.</span><span class="sxs-lookup"><span data-stu-id="e0596-161">Name for the resource.</span></span> <span data-ttu-id="e0596-162">Kullanımına dikkat edin `[parameters('applicationGatewayName')]`, adı giriş olarak sizin tarafınızdan veya bir parametre dosyası dağıtımı sırasında sağlanan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e0596-162">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="e0596-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="e0596-163">**properties**.</span></span> <span data-ttu-id="e0596-164">Kaynak özelliklerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="e0596-164">List of properties for the resource.</span></span> <span data-ttu-id="e0596-165">Bu şablon, uygulama ağ geçidi oluştururken sanal ağı ve genel IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e0596-165">This template uses the virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e0596-166">Şablonlar hakkında daha fazla bilgi için ziyaret edin: [Resource Manager şablonları başvurusu](/templates/)</span><span class="sxs-lookup"><span data-stu-id="e0596-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="e0596-167">Geri gidin [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="e0596-167">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="e0596-168">Tıklatın **azuredeploy-parameters.json**ve ardından **RAW**.</span><span class="sxs-lookup"><span data-stu-id="e0596-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="e0596-169">Dosyayı bilgisayarınızdaki yerel bir klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e0596-169">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="e0596-170">Kaydettiğiniz dosyayı açın ve parametre değerlerini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="e0596-170">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="e0596-171">Senaryomuzda açıklanan uygulama ağ geçidini dağıtmak için aşağıdaki değerleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e0596-171">Use the following values to deploy the application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="e0596-172">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e0596-172">Save the file.</span></span> <span data-ttu-id="e0596-173">JSON şablonunu ve parametre şablonunu, [JSlint.com](http://www.jslint.com/) gibi çevrimiçi JSON doğrulama araçlarını kullanarak test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0596-173">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="e0596-174">PowerShell kullanarak Azure Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="e0596-174">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="e0596-175">Azure PowerShell'i hiç kullanmadıysanız, ziyaret edin: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) ve Azure'da oturum açıp aboneliğinizi seçmek için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="e0596-175">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="e0596-176">PowerShell oturum açın</span><span class="sxs-lookup"><span data-stu-id="e0596-176">Login to PowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="e0596-177">Hesapla ilişkili abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="e0596-177">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="e0596-178">Kimlik bilgilerinizle kimliğinizi doğrulamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="e0596-178">You are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="e0596-179">Hangi Azure aboneliğinizin kullanılacağını seçin.</span><span class="sxs-lookup"><span data-stu-id="e0596-179">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="e0596-180">Gerekirse, **New-AzureResourceGroup** cmdlet’ini kullanarak bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e0596-180">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="e0596-181">Aşağıdaki örnekte Doğu ABD konumunda AppgatewayRG adlı yeni bir kaynak grubu oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e0596-181">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="e0596-182">Önceden indirdiğiniz ve değiştirdiğiniz şablonu ve parametre dosyalarını kullanarak yeni sanal ağı dağıtmak için, **New-AzureRmResourceGroupDeployment** cmdlet’ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e0596-182">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="e0596-183">Azure CLI kullanarak Azure Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="e0596-183">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="e0596-184">Azure CLI kullanarak indirdiğiniz Azure Resource Manager şablonu dağıtmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e0596-184">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

1. <span data-ttu-id="e0596-185">Daha önce Azure CLI kullanmadıysanız, [Azure CLI yükleme ve yapılandırma](/cli/azure/install-azure-cli) sayfasına gidin ve Azure hesabınızı ve aboneliğinizi seçene kadar talimatları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="e0596-185">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="e0596-186">Gerekirse, çalıştırmak `az group create` aşağıdaki kod parçacığında gösterildiği gibi bir kaynak grubu oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="e0596-186">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="e0596-187">Komutun çıktısına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e0596-187">Notice the output of the command.</span></span> <span data-ttu-id="e0596-188">Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e0596-188">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="e0596-189">Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md) sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="e0596-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="e0596-190">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="e0596-190">**-n (or --name)**.</span></span> <span data-ttu-id="e0596-191">Yeni kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="e0596-191">Name for the new resource group.</span></span> <span data-ttu-id="e0596-192">Senaryomuz için bu ad, *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="e0596-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="e0596-193">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="e0596-193">**-l (or --location)**.</span></span> <span data-ttu-id="e0596-194">Yeni kaynak grubunun oluşturulduğu Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="e0596-194">Azure region where the new resource group is created.</span></span> <span data-ttu-id="e0596-195">Bizim senaryomuz için sahip *westus*.</span><span class="sxs-lookup"><span data-stu-id="e0596-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="e0596-196">Çalıştırma `az group deployment create` şablonu ve parametre kullanarak yeni sanal ağı dağıtmak için cmdlet indirdiğiniz ve değiştirdiğiniz önceki adımda dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e0596-196">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="e0596-197">Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e0596-197">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="e0596-198">Dağıtmak için tıkla özelliğini kullanarak Azure Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="e0596-198">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="e0596-199">Dağıtmak için tıkla, Azure Resource Manager şablonlarını kullanmanın başka bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="e0596-199">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="e0596-200">Kolay bir Azure portalıyla şablonları kullanma yoludur.</span><span class="sxs-lookup"><span data-stu-id="e0596-200">It's an easy way to use templates with the Azure portal.</span></span>

1. <span data-ttu-id="e0596-201">Git [web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="e0596-201">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="e0596-202">**Azure’a dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0596-202">Click **Deploy to Azure**.</span></span>

    ![Azure’a Dağıt](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="e0596-204">Portalda, dağıtım şablonu parametrelerini doldurun ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0596-204">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

    ![Parametreler](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="e0596-206">Seçin **hüküm ve koşulları yukarıda belirtildiği ediyorum** tıklatıp **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="e0596-206">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="e0596-207">Özel dağıtım dikey penceresinde **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0596-207">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="e0596-208">Resource Manager şablonları için sertifika verileri sağlayan</span><span class="sxs-lookup"><span data-stu-id="e0596-208">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="e0596-209">SSL sahip bir şablon kullanıldığında, sertifikanın karşıya yüklenen yerine bir base64 dizesi sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0596-209">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="e0596-210">Dönüştürmek için bir .pfx veya base64 dizesi .cer kullanmak aşağıdaki komutlardan birini.</span><span class="sxs-lookup"><span data-stu-id="e0596-210">To convert a .pfx or .cer to a base64 string use one of the following commands.</span></span> <span data-ttu-id="e0596-211">Aşağıdaki komutları sertifika şablonu için sağlanan bir base64 dizesi dönüştürülemiyor.</span><span class="sxs-lookup"><span data-stu-id="e0596-211">The following commands convert the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="e0596-212">Beklenen çıktı bir değişkende depolanan ve şablonda yapıştırılan bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="e0596-212">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

### <a name="macos"></a><span data-ttu-id="e0596-213">macOS</span><span class="sxs-lookup"><span data-stu-id="e0596-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="e0596-214">Windows</span><span class="sxs-lookup"><span data-stu-id="e0596-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="e0596-215">Tüm kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="e0596-215">Delete all resources</span></span>

<span data-ttu-id="e0596-216">Bu makalede oluşturulan tüm kaynakları silmek için aşağıdaki adımlardan birini tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="e0596-216">To delete all resources created in this article, complete one of the following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="e0596-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0596-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="e0596-218">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e0596-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="e0596-219">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e0596-219">Next steps</span></span>

<span data-ttu-id="e0596-220">SSL yükü boşaltmayı yapılandırmak istiyorsanız [SSL yükü boşaltma için uygulama ağ geçidi yapılandırma](application-gateway-ssl.md) sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="e0596-220">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="e0596-221">İç yük dengeleyiciyle kullanacağınız uygulama ağ geçidi yapılandırmak istiyorsanız [İç yük dengeleyici (ILB) ile uygulama ağ geçidi oluşturma](application-gateway-ilb.md) sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="e0596-221">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="e0596-222">Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.:</span><span class="sxs-lookup"><span data-stu-id="e0596-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="e0596-223">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="e0596-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="e0596-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="e0596-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)


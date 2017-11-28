---
title: "İnternet’e yönelik yük dengeleyicisi oluşturma - Azure şablonu | Microsoft Docs"
description: "Şablon kullanarak Resource Manager’da İnternet’e yönelik yük dengeleyici oluşturmayı öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d829000e63515814b192f3f8256e3b8637bb3a34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="bde5e-103">Şablon kullanarak İnternet’e yönelik yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="bde5e-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bde5e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="bde5e-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="bde5e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bde5e-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="bde5e-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bde5e-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="bde5e-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="bde5e-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="bde5e-108">Bu makalede Resource Manager dağıtım modeli anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bde5e-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="bde5e-109">[Klasik dağıtım modeli kullanarak İnternet’e yönelik yük dengeleyici oluşturma](load-balancer-get-started-internet-classic-portal.md) sayfasını da inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bde5e-109">You can also [Learn how to create an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="bde5e-110">Tıklayarak dağıtma kullanarak şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="bde5e-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="bde5e-111">Genel depoda yer alan örnek şablonda, yukarıdaki senaryoyu oluşturmak için kullanılan varsayılan değerleri içeren parametre dosyası kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bde5e-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="bde5e-112">Tıklayarak dağıtma kullanarak bu şablonu dağıtmak için [bu bağlantıya](http://go.microsoft.com/fwlink/?LinkId=544801) gidin, **Azure’a dağıt**’a tıklayın, gerekirse varsayılan parametreleri değiştirin ve portaldaki talimatları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="bde5e-112">To deploy this template using click to deploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="bde5e-113">PowerShell kullanarak şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="bde5e-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="bde5e-114">PowerShell kullanarak yüklediğiniz şablonu dağıtmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="bde5e-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="bde5e-115">Daha önce Azure PowerShell kullanmadıysanız, [Azure PowerShell’i Yükleme ve Yapılandırma](/powershell/azure/overview) sayfasına gidin ve Azure’da oturum açıp aboneliğinizi seçmek için talimatları sonuna kadar uygulayın.</span><span class="sxs-lookup"><span data-stu-id="bde5e-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="bde5e-116">Şablonu kullanarak kaynak grubu oluşturmak için **New-AzureRmResourceGroupDeployment** cmdlet’ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bde5e-116">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="bde5e-117">Azure CLI kullanarak şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="bde5e-117">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="bde5e-118">Azure CLI’yi kullanarak şablonu dağıtmak için aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="bde5e-118">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="bde5e-119">Hiç Azure CLI kullanmadıysanız bkz. [Azure CLI’yi Yükleme ve Yapılandırma](../cli-install-nodejs.md); sonra da, Azure hesabınızı ve aboneliğinizi seçtiğiniz noktaya kadar yönergeleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="bde5e-119">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="bde5e-120">Resource Manager moduna geçmek için **azure config mode** komutunu aşağıda gösterildiği gibi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bde5e-120">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="bde5e-121">Yukarıdaki komut için beklenen çıktı şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="bde5e-121">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="bde5e-122">Tarayıcınızdan [Hızlı Başlangıç Şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules)’na gidin, json dosyasının içeriğini kopyalayın ve bilgisayarınızda yeni bir dosyaya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="bde5e-122">From your browser, navigate to [the Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy the contents of the json file and paste into a new file in your computer.</span></span> <span data-ttu-id="bde5e-123">Bu senaryo için değerleri **c:\lb\azuredeploy.parameters.json** adlı bir dosyaya kopyalayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bde5e-123">For this scenario, you would be copying the values below to a file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="bde5e-124">Yukarıda indirdiğiniz ve değiştirdiğiniz şablonu ve parametre dosyalarını kullanarak yeni yük dengeleyiciyi dağıtmak için, **azure group deployment create** cmdlet’ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bde5e-124">Run the **azure group deployment create** cmdlet to deploy the new load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="bde5e-125">Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bde5e-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="bde5e-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bde5e-126">Next steps</span></span>

[<span data-ttu-id="bde5e-127">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="bde5e-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="bde5e-128">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bde5e-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="bde5e-129">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bde5e-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

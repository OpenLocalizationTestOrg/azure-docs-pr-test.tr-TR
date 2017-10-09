---
title: "aaaCreate bir Internet'e yönelik Yük Dengeleyici - Azure şablonu | Microsoft Docs"
description: "Nasıl toocreate Internet'e yönelik Yük Dengeleyici kaynak bir şablon kullanarak Yöneticisi'nde öğrenin"
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
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="b26ed-103">Şablon kullanarak İnternet’e yönelik yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="b26ed-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b26ed-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b26ed-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="b26ed-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b26ed-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="b26ed-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b26ed-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="b26ed-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="b26ed-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="b26ed-108">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="b26ed-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="b26ed-109">Ayrıca [nasıl toocreate Internet'e yönelik Yük Dengeleyici Klasik dağıtım modeli kullanarak bilgi edinin](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b26ed-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="b26ed-110">Kullanarak Hello şablonu dağıtma toodeploy tıklatın</span><span class="sxs-lookup"><span data-stu-id="b26ed-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="b26ed-111">Merhaba örnek şablonunda kullanılabilir hello genel depo yukarıda açıklanan hello varsayılan kullanılan değerler toogenerate hello senaryosu içeren bir parametre dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="b26ed-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="b26ed-112">toodeploy tıklatın toodeploy, bu şablonu kullanarak izleyin [bu bağlantıyı](http://go.microsoft.com/fwlink/?LinkId=544801), tıklatın **tooAzure dağıtmak**hello varsayılan parametre değerlerini gerekiyorsa değiştirin ve hello hello Portalı'ndaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="b26ed-112">toodeploy this template using click toodeploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="b26ed-113">PowerShell kullanarak Hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="b26ed-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="b26ed-114">PowerShell kullanarak yüklediğiniz toodeploy hello şablonunu hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b26ed-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="b26ed-115">Azure PowerShell'i hiç kullanmadıysanız bkz [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) ve tüm hello yolu toohello toosign Azure'da sonlandırmak ve aboneliğinizi seçin hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="b26ed-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="b26ed-116">Merhaba çalıştırmak **New-AzureRmResourceGroupDeployment** kullanarak bir kaynak grubu cmdlet toocreate hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="b26ed-116">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="b26ed-117">Hello Azure CLI kullanarak Hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="b26ed-117">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="b26ed-118">hello Azure CLI kullanarak toodeploy hello şablon hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b26ed-118">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="b26ed-119">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="b26ed-119">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="b26ed-120">Merhaba çalıştırmak **azure config modu** aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.</span><span class="sxs-lookup"><span data-stu-id="b26ed-120">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="b26ed-121">Yukarıdaki hello komut için beklenen hello çıktı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b26ed-121">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="b26ed-122">Tarayıcınızdan çok gidin[hızlı başlatma şablonunu hello](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules)hello hello json dosyasının içeriğini kopyalayın ve bilgisayarınızı yeni bir dosyaya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b26ed-122">From your browser, navigate too[hello Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy hello contents of hello json file and paste into a new file in your computer.</span></span> <span data-ttu-id="b26ed-123">Bu senaryo için adlı tooa dosya altındaki hello değerler kopyaladığınız **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="b26ed-123">For this scenario, you would be copying hello values below tooa file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="b26ed-124">Merhaba çalıştırmak **azure Grup dağıtımı oluşturmak** hello şablonu ve parametre kullanarak cmdlet toodeploy hello Yeni Yük Dengeleyici, yukarıda indirdiğiniz ve değiştirdiğiniz dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b26ed-124">Run hello **azure group deployment create** cmdlet toodeploy hello new load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="b26ed-125">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b26ed-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="b26ed-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b26ed-126">Next steps</span></span>

[<span data-ttu-id="b26ed-127">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="b26ed-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="b26ed-128">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b26ed-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b26ed-129">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b26ed-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

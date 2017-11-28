---
title: "bir iç yük dengeleyici - Azure şablonu aaaCreate | Microsoft Docs"
description: "Nasıl toocreate bir iç yük dengeleyici Kaynak Yöneticisi'nde bir şablon kullanarak bilgi edinin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="65c6b-103">Şablon kullanarak iç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="65c6b-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="65c6b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="65c6b-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="65c6b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65c6b-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="65c6b-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="65c6b-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="65c6b-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="65c6b-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="65c6b-108">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="65c6b-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="65c6b-109">Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="65c6b-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="65c6b-110">Kullanarak Hello şablonu dağıtma toodeploy tıklatın</span><span class="sxs-lookup"><span data-stu-id="65c6b-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="65c6b-111">Merhaba örnek şablonunda kullanılabilir hello genel depo yukarıda açıklanan hello varsayılan kullanılan değerler toogenerate hello senaryosu içeren bir parametre dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="65c6b-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="65c6b-112">toodeploy tıklatın toodeploy, bu şablonu kullanarak izleyin [bu bağlantıyı](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), tıklatın **tooAzure dağıtmak**hello varsayılan parametre değerlerini gerekiyorsa değiştirin ve hello hello Portalı'ndaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="65c6b-112">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="65c6b-113">PowerShell kullanarak Hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="65c6b-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="65c6b-114">PowerShell kullanarak yüklediğiniz toodeploy hello şablonunu hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="65c6b-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="65c6b-115">Azure PowerShell'i hiç kullanmadıysanız bkz [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) ve tüm hello yolu toohello toosign Azure'da sonlandırmak ve aboneliğinizi seçin hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="65c6b-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="65c6b-116">Merhaba parametreleri dosya tooyour yerel disk indirin.</span><span class="sxs-lookup"><span data-stu-id="65c6b-116">Download hello parameters file tooyour local disk.</span></span>
3. <span data-ttu-id="65c6b-117">Merhaba dosyasını düzenleyin ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="65c6b-117">Edit hello file and save it.</span></span>
4. <span data-ttu-id="65c6b-118">Merhaba çalıştırmak **New-AzureRmResourceGroupDeployment** kullanarak bir kaynak grubu cmdlet toocreate hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="65c6b-118">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="65c6b-119">Hello Azure CLI kullanarak Hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="65c6b-119">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="65c6b-120">hello Azure CLI kullanarak toodeploy hello şablon hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="65c6b-120">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="65c6b-121">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="65c6b-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="65c6b-122">Merhaba çalıştırmak **azure config modu** aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.</span><span class="sxs-lookup"><span data-stu-id="65c6b-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="65c6b-123">Yukarıdaki hello komut için beklenen hello çıktı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="65c6b-123">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="65c6b-124">Merhaba parametre dosyasını açın, içeriğini seçin ve tooa dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="65c6b-124">Open hello parameter file, select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="65c6b-125">Bu örnekte, hello parametreler dosyası çok kaydettik*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="65c6b-125">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="65c6b-126">Merhaba çalıştırmak **azure Grup dağıtımı oluşturmak** toodeploy hello şablonu ve parametre kullanarak yeni iç yük dengeleyici hello komut dosyaları, yukarıda indirdiğiniz ve değiştirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="65c6b-126">Run hello **azure group deployment create** command toodeploy hello new internal load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="65c6b-127">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="65c6b-127">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="65c6b-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65c6b-128">Next steps</span></span>

[<span data-ttu-id="65c6b-129">Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="65c6b-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="65c6b-130">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="65c6b-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)


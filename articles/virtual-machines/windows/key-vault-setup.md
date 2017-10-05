---
title: "Anahtar kasası için Windows sanal makineleri Azure Kaynak Yöneticisi'nde ayarlama | Microsoft Docs"
description: "Anahtar kasası bir Azure Resource Manager sanal makinesi ile kullanmak için nasıl kurulur."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: a5083a5216efbfd76fd912ec48c2f0ec3b30c4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="90a45-103">Sanal makineler Azure Kaynak Yöneticisi'nde için anahtar kasasını oluşturup</span><span class="sxs-lookup"><span data-stu-id="90a45-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="90a45-104">Gizli/sertifikalar, anahtar kasası kaynak sağlayıcısı tarafından sağlanan kaynaklar olarak Azure Kaynak Yöneticisi yığınında modellenir.</span><span class="sxs-lookup"><span data-stu-id="90a45-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="90a45-105">Anahtar kasası hakkında daha fazla bilgi için bkz: [Azure anahtar kasası nedir?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="90a45-105">To learn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="90a45-106">Azure Resource Manager sanal makinelerle kullanılacak anahtar kasası için sırayla **EnabledForDeployment** anahtar kasası özelliğinin ayarlanması true.</span><span class="sxs-lookup"><span data-stu-id="90a45-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the **EnabledForDeployment** property on Key Vault must be set to true.</span></span> <span data-ttu-id="90a45-107">Çeşitli istemciler bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90a45-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="90a45-108">Anahtar kasası aynı abonelikte ve konumda sanal makine olarak oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90a45-108">The Key Vault needs to be created in the same subscription and location as the Virtual Machine.</span></span>
>
>

## <a name="use-powershell-to-set-up-key-vault"></a><span data-ttu-id="90a45-109">Anahtar kasası ayarlamak için PowerShell kullanın</span><span class="sxs-lookup"><span data-stu-id="90a45-109">Use PowerShell to set up Key Vault</span></span>
<span data-ttu-id="90a45-110">PowerShell kullanarak bir anahtar kasası oluşturmak için bkz: [Azure anahtar kasası ile çalışmaya başlama](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="90a45-110">To create a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="90a45-111">Yeni anahtar kasalarını için bu PowerShell cmdlet'ini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90a45-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="90a45-112">Varolan anahtar kasalarını için bu PowerShell cmdlet'ini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90a45-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-to-set-up-key-vault"></a><span data-ttu-id="90a45-113">Bize CLI anahtar kasası ayarlamak için</span><span class="sxs-lookup"><span data-stu-id="90a45-113">Us CLI to set up Key Vault</span></span>
<span data-ttu-id="90a45-114">Komut satırı arabirimi (CLI) kullanarak bir anahtar kasası oluşturmak için bkz: [anahtar kasası CLI kullanarak yönetme](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="90a45-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="90a45-115">CLI için dağıtım ilkesi atamadan önce anahtar kasası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90a45-115">For CLI, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="90a45-116">Aşağıdaki komutu kullanarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90a45-116">You can do this by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="90a45-117">Anahtar kasası ayarlamak için şablonlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="90a45-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="90a45-118">Bir şablon kullanırken ayarlamanız gerekir `enabledForDeployment` özelliğine `true` anahtar kasası kaynak için.</span><span class="sxs-lookup"><span data-stu-id="90a45-118">While you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

    {
      "type": "Microsoft.KeyVault/vaults",
      "name": "ContosoKeyVault",
      "apiVersion": "2015-06-01",
      "location": "<location-of-key-vault>",
      "properties": {
        "enabledForDeployment": "true",
        ....
        ....
      }
    }

<span data-ttu-id="90a45-119">Şablonları kullanarak bir anahtar kasası oluşturduğunuzda, sizin yapılandırabileceğiniz diğer seçenekleri için bkz: [bir anahtar kasası oluşturma](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="90a45-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

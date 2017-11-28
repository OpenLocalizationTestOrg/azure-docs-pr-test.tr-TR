---
title: "Anahtar kasası için Windows Vm'leri Azure Kaynak Yöneticisi'nde yedekleme aaaSet | Microsoft Docs"
description: "Nasıl bir Azure Resource Manager sanal makinesi ile kullanmak için anahtar kasası yukarı tooset."
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
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="46d1d-103">Sanal makineler Azure Kaynak Yöneticisi'nde için anahtar kasasını oluşturup</span><span class="sxs-lookup"><span data-stu-id="46d1d-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="46d1d-104">Gizli/sertifikalar, anahtar kasasının hello kaynak sağlayıcısı tarafından sağlanan kaynaklar olarak Azure Kaynak Yöneticisi yığınında modellenir.</span><span class="sxs-lookup"><span data-stu-id="46d1d-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="46d1d-105">Anahtar kasası hakkında daha fazla toolearn bakın [Azure anahtar kasası nedir?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="46d1d-105">toolearn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="46d1d-106">Azure Resource Manager sanal makinelerle kullanılan anahtar kasası toobe için sırayla hello **EnabledForDeployment** tootrue anahtar kasası özelliği ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="46d1d-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello **EnabledForDeployment** property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="46d1d-107">Çeşitli istemciler bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46d1d-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="46d1d-108">Merhaba anahtar kasası gereksinimlerini toobe oluşturulan aynı abonelikte ve konumda sanal makine hello gibi hello.</span><span class="sxs-lookup"><span data-stu-id="46d1d-108">hello Key Vault needs toobe created in hello same subscription and location as hello Virtual Machine.</span></span>
>
>

## <a name="use-powershell-tooset-up-key-vault"></a><span data-ttu-id="46d1d-109">Anahtar kasası yukarı PowerShell tooset kullanın</span><span class="sxs-lookup"><span data-stu-id="46d1d-109">Use PowerShell tooset up Key Vault</span></span>
<span data-ttu-id="46d1d-110">toocreate PowerShell kullanarak bir anahtar kasası bkz [Azure anahtar kasası ile çalışmaya başlama](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="46d1d-110">toocreate a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="46d1d-111">Yeni anahtar kasalarını için bu PowerShell cmdlet'ini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46d1d-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="46d1d-112">Varolan anahtar kasalarını için bu PowerShell cmdlet'ini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46d1d-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a><span data-ttu-id="46d1d-113">Bize CLI tooset anahtar kasası ayarlama</span><span class="sxs-lookup"><span data-stu-id="46d1d-113">Us CLI tooset up Key Vault</span></span>
<span data-ttu-id="46d1d-114">toocreate hello komut satırı arabirimi (CLI) kullanarak bir anahtar kasası bkz [anahtar kasası CLI kullanarak yönetme](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="46d1d-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="46d1d-115">CLI için hello dağıtım ilkesi atamadan önce toocreate hello anahtar kasası sahip.</span><span class="sxs-lookup"><span data-stu-id="46d1d-115">For CLI, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="46d1d-116">Bu komutu aşağıdaki hello kullanarak yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46d1d-116">You can do this by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="46d1d-117">Anahtar kasası yukarı şablonları tooset kullanın</span><span class="sxs-lookup"><span data-stu-id="46d1d-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="46d1d-118">Bir şablon kullanırken tooset hello gereksinim `enabledForDeployment` özelliği çok`true` hello anahtar kasası kaynak için.</span><span class="sxs-lookup"><span data-stu-id="46d1d-118">While you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="46d1d-119">Şablonları kullanarak bir anahtar kasası oluşturduğunuzda, sizin yapılandırabileceğiniz diğer seçenekleri için bkz: [bir anahtar kasası oluşturma](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="46d1d-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

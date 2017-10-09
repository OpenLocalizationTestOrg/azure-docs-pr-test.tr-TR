---
title: "Anahtar kasası Linux VM'ler için yukarı aaaSet hello Azure CLI 1.0 ile | Microsoft Docs"
description: "Nasıl anahtar kasası yukarı tooset ile bir Azure Resource Manager sanal makine ile kullanmak için Azure CLI 1.0 hello."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a><span data-ttu-id="8a7d7-103">Sanal makine Azure Kaynak Yöneticisi'nde hello Azure CLI 1.0 için anahtar kasasını oluşturup</span><span class="sxs-lookup"><span data-stu-id="8a7d7-103">Set up Key Vault for virtual machines in Azure Resource Manager with hello Azure CLI 1.0</span></span>
<span data-ttu-id="8a7d7-104">Gizli/sertifikalar, anahtar kasasının hello kaynak sağlayıcısı tarafından sağlanan kaynaklar olarak Hello Azure Kaynak Yöneticisi yığınında modellenir.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="8a7d7-105">Azure anahtar kasası hakkında daha fazla toolearn bakın [Azure anahtar kasası nedir?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="8a7d7-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="8a7d7-106">Azure Resource Manager sanal makinelerle kullanılan anahtar kasası toobe için sırayla hello *EnabledForDeployment* tootrue anahtar kasası özelliği ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="8a7d7-107">Çeşitli istemciler bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-107">You can do this in various clients.</span></span> <span data-ttu-id="8a7d7-108">Bu makale size nasıl gösterir anahtar kasası yukarı tooset Azure sanal makineler ile kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-108">This article shows you how tooset up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="8a7d7-109">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="8a7d7-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="8a7d7-110">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlayın</span><span class="sxs-lookup"><span data-stu-id="8a7d7-110">You can complete hello task using one of hello following CLI versions</span></span>

- <span data-ttu-id="8a7d7-111">[Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="8a7d7-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8a7d7-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="8a7d7-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="use-cli-10-tooset-up-key-vault"></a><span data-ttu-id="8a7d7-113">Anahtar kasası yukarı CLI 1.0 tooset kullanın</span><span class="sxs-lookup"><span data-stu-id="8a7d7-113">Use CLI 1.0 tooset up Key Vault</span></span>
<span data-ttu-id="8a7d7-114">toocreate hello komut satırı arabirimi (CLI) kullanarak bir anahtar kasası bkz [anahtar kasası CLI kullanarak yönetme](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="8a7d7-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="8a7d7-115">CLI 1.0 için hello dağıtım ilkesi atamadan önce toocreate hello anahtar kasası sahip.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-115">For CLI 1.0, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="8a7d7-116">Ardından, komutu aşağıdaki hello kullanarak hello İlkesi atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8a7d7-116">You can then assign hello policy by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="8a7d7-117">Anahtar kasası yukarı şablonları tooset kullanın</span><span class="sxs-lookup"><span data-stu-id="8a7d7-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="8a7d7-118">Bir şablonu kullandığınızda tooset hello gereksinim `enabledForDeployment` özelliği çok`true` hello anahtar kasası kaynak için.</span><span class="sxs-lookup"><span data-stu-id="8a7d7-118">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="8a7d7-119">Şablonları kullanarak bir anahtar kasası oluşturduğunuzda, sizin yapılandırabileceğiniz diğer seçenekleri için bkz: [bir anahtar kasası oluşturma](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="8a7d7-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

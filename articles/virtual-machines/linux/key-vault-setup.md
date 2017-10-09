---
title: "Azure anahtar kasası Linux VM'ler için yukarı aaaSet | Microsoft Docs"
description: "Nasıl anahtar kasası yukarı tooset ile bir Azure Resource Manager sanal makine ile kullanmak için CLI 2.0 hello."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a><span data-ttu-id="b80af-103">Anahtar kasası yukarı tooset ile sanal makineler için Azure CLI 2.0 nasıl hello</span><span class="sxs-lookup"><span data-stu-id="b80af-103">How tooset up Key Vault for virtual machines with hello Azure CLI 2.0</span></span>

<span data-ttu-id="b80af-104">Gizli/sertifikalar, anahtar kasası tarafından sağlanan kaynaklar olarak Hello Azure Kaynak Yöneticisi yığınında modellenir.</span><span class="sxs-lookup"><span data-stu-id="b80af-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="b80af-105">Azure anahtar kasası hakkında daha fazla toolearn bakın [Azure anahtar kasası nedir?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="b80af-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="b80af-106">Azure Kaynak Yöneticisi Vm'leri ile kullanılan anahtar kasası toobe için sırayla hello *EnabledForDeployment* tootrue anahtar kasası özelliği ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b80af-106">In order for Key Vault toobe used with Azure Resource Manager VMs, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="b80af-107">Bu makale size gösterir nasıl Azure kullanarak sanal makineleri (VM'ler) ile kullanmak için anahtar kasası yukarı tooset hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="b80af-107">This article shows you how tooset up Key Vault for use with Azure virtual machines (VMs) using hello Azure CLI 2.0.</span></span> <span data-ttu-id="b80af-108">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b80af-108">You can also perform these steps with hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b80af-109">Aşağıdaki adımları tooperform ihtiyacınız hello son [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b80af-109">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="b80af-110">Anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="b80af-110">Create a Key Vault</span></span>
<span data-ttu-id="b80af-111">Bir anahtar kasası oluşturun ve hello dağıtım ilkesiyle atayın [az keyvault oluşturma](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="b80af-111">Create a key vault and assign hello deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="b80af-112">Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar kasası `myKeyVault` hello içinde `myResourceGroup` kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="b80af-112">hello following example creates a key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="b80af-113">Sanal makineler ile kullanmak için bir anahtar kasası güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b80af-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="b80af-114">Merhaba dağıtım ilkesi olan bir anahtar kasası ile ayarlandığında [az keyvault güncelleştirme](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="b80af-114">Set hello deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="b80af-115">Merhaba aşağıdaki güncelleştirmeleri hello adlı anahtar kasası `myKeyVault` hello içinde `myResourceGroup` kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="b80af-115">hello following updates hello key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="b80af-116">Anahtar kasası yukarı şablonları tooset kullanın</span><span class="sxs-lookup"><span data-stu-id="b80af-116">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="b80af-117">Bir şablonu kullandığınızda tooset hello gereksinim `enabledForDeployment` özelliği çok`true` şekilde hello anahtar kasası kaynak için:</span><span class="sxs-lookup"><span data-stu-id="b80af-117">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource as follows:</span></span>

```json
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
```

## <a name="next-steps"></a><span data-ttu-id="b80af-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b80af-118">Next steps</span></span>
<span data-ttu-id="b80af-119">Şablonları kullanarak bir anahtar kasası oluşturduğunuzda, sizin yapılandırabileceğiniz diğer seçenekleri için bkz: [bir anahtar kasası oluşturma](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="b80af-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

---
title: "Azure CLI betik örnek - Batch hesabı oluşturun. | Microsoft Docs"
description: "Azure CLI betik örnek - Batch hesabı oluşturma"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a><span data-ttu-id="010ee-103">Azure CLI ile bir toplu işlem hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="010ee-103">Create a Batch account with the Azure CLI</span></span>

<span data-ttu-id="010ee-104">Bu komut dosyasını bir Azure Batch hesabı oluşturur ve hesabın nasıl çeşitli özellikleri sorgulanan ve güncelleştirilmiş gösterir.</span><span class="sxs-lookup"><span data-stu-id="010ee-104">This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="010ee-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="010ee-105">Prerequisites</span></span>

<span data-ttu-id="010ee-106">Sağlanan yönergeleri kullanarak Azure CLI yükleme [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.</span><span class="sxs-lookup"><span data-stu-id="010ee-106">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="010ee-107">Toplu işlem hesabı örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="010ee-107">Batch account sample script</span></span>

<span data-ttu-id="010ee-108">Varsayılan olarak, bir toplu işlem hesabı oluşturduğunuzda, işlem düğümlerini Batch hizmeti tarafından dahili olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="010ee-108">When you create a Batch account, by default its compute nodes are assigned internally by the Batch service.</span></span> <span data-ttu-id="010ee-109">Hesap ya da paylaşılan anahtar kimlik bilgileri veya bir Azure Active Dirctory belirteci aracılığıyla doğrulanabilir ve ayrılmış işlem düğümleri ayrı çekirdek kotası tabi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="010ee-109">Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

<span data-ttu-id="010ee-110">[!code-azurecli[Ana](../../../cli_scripts/batch/create-account/create-account.sh "hesabı oluştur")]</span><span class="sxs-lookup"><span data-stu-id="010ee-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]</span></span>

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="010ee-111">Toplu işlem hesabı kullanıcı abonelik örnek komut dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="010ee-111">Batch account using user subscription sample script</span></span>

<span data-ttu-id="010ee-112">Toplu işlem düğümlerinden kendi Azure aboneliği oluşturmak için tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="010ee-112">You can also opt to have Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="010ee-113">Allocate hesapları işlem düğümlerin aboneliğinizi içine bir Azure Active Directory token kimlik doğrulaması gerekir ve ayrılan işlem düğümleri abonelik kotanızı sayılacaktır.</span><span class="sxs-lookup"><span data-stu-id="010ee-113">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="010ee-114">Bu modda bir hesap oluşturmak için bir anahtar kasası başvuru hesabı oluştururken belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="010ee-114">To create an account in this mode, one must specify a Key Vault reference when creating the account.</span></span>

<span data-ttu-id="010ee-115">[!code-azurecli[Ana](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "kullanıcı aboneliği kullanarak hesabı oluştur")]</span><span class="sxs-lookup"><span data-stu-id="010ee-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="010ee-116">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="010ee-116">Clean up deployment</span></span>

<span data-ttu-id="010ee-117">Yukarıdaki örnek betikler birini çalıştırdıktan sonra kaynak grubunu kaldırmak için aşağıdaki komutu çalıştırın ve ilişkili tüm kaynaklar (toplu işlem hesabı, Azure depolama hesapları ve Azure anahtar kasalarını dahil).</span><span class="sxs-lookup"><span data-stu-id="010ee-117">After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="010ee-118">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="010ee-118">Script explanation</span></span>

<span data-ttu-id="010ee-119">Bu komut, bir kaynak grubu, toplu işlem hesabı ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="010ee-119">This script uses the following commands to create a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="010ee-120">Komut özgü belgelere Tablo bağlantıları her komut.</span><span class="sxs-lookup"><span data-stu-id="010ee-120">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="010ee-121">Komut</span><span class="sxs-lookup"><span data-stu-id="010ee-121">Command</span></span> | <span data-ttu-id="010ee-122">Notlar</span><span class="sxs-lookup"><span data-stu-id="010ee-122">Notes</span></span> |
|---|---|
| [<span data-ttu-id="010ee-123">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="010ee-123">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="010ee-124">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="010ee-124">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="010ee-125">az toplu işlem hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="010ee-125">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="010ee-126">Toplu işlem hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="010ee-126">Creates the Batch account.</span></span>  |
| [<span data-ttu-id="010ee-127">az toplu işlem hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="010ee-127">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="010ee-128">Batch hesabı özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="010ee-128">Updates properties of the Batch account.</span></span>  |
| [<span data-ttu-id="010ee-129">az toplu işlem hesabı Göster</span><span class="sxs-lookup"><span data-stu-id="010ee-129">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="010ee-130">Belirtilen toplu işlem hesabı ayrıntılarını alır.</span><span class="sxs-lookup"><span data-stu-id="010ee-130">Retrieves details of the specified Batch account.</span></span>  |
| [<span data-ttu-id="010ee-131">az batch hesabı anahtarları listesi</span><span class="sxs-lookup"><span data-stu-id="010ee-131">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="010ee-132">Belirtilen toplu işlem hesabı erişim anahtarları alır.</span><span class="sxs-lookup"><span data-stu-id="010ee-132">Retrieves the access keys of the specified Batch account.</span></span>  |
| [<span data-ttu-id="010ee-133">az toplu işlem hesabı oturum açma</span><span class="sxs-lookup"><span data-stu-id="010ee-133">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="010ee-134">Daha fazla CLI etkileşim için belirtilen toplu işlem hesabı karşı doğrular.</span><span class="sxs-lookup"><span data-stu-id="010ee-134">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="010ee-135">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="010ee-135">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="010ee-136">Bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="010ee-136">Creates a storage account.</span></span> |
| [<span data-ttu-id="010ee-137">az keyvault oluşturma</span><span class="sxs-lookup"><span data-stu-id="010ee-137">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="010ee-138">Bir anahtar kasası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="010ee-138">Creates a key vault.</span></span> |
| [<span data-ttu-id="010ee-139">az keyvault-ilkesini ayarlama</span><span class="sxs-lookup"><span data-stu-id="010ee-139">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="010ee-140">Belirtilen anahtar kasası güvenlik ilkesini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="010ee-140">Update the security policy of the specified key vault.</span></span> |
| [<span data-ttu-id="010ee-141">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="010ee-141">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="010ee-142">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="010ee-142">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="010ee-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="010ee-143">Next steps</span></span>

<span data-ttu-id="010ee-144">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="010ee-144">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="010ee-145">Ek toplu CLI kod örnekleri bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="010ee-145">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

---
title: "aaaAzure CLI komut dosyası örneği - Batch hesabı oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a><span data-ttu-id="85140-103">Hello Azure CLI ile bir toplu işlem hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="85140-103">Create a Batch account with hello Azure CLI</span></span>

<span data-ttu-id="85140-104">Bu komut dosyasını bir Azure Batch hesabı oluşturur ve hello hesabının nasıl çeşitli özelliklerini sorgulanan ve güncelleştirilmiş gösterir.</span><span class="sxs-lookup"><span data-stu-id="85140-104">This script creates an Azure Batch account and shows how various properties of hello account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85140-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="85140-105">Prerequisites</span></span>

<span data-ttu-id="85140-106">Yükleme hello hello sağlanan hello yönergeleri kullanarak Azure CLI [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.</span><span class="sxs-lookup"><span data-stu-id="85140-106">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="85140-107">Toplu işlem hesabı örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="85140-107">Batch account sample script</span></span>

<span data-ttu-id="85140-108">Varsayılan olarak, bir toplu işlem hesabı oluşturduğunuzda, işlem düğümlerini hello Batch hizmeti tarafından dahili olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="85140-108">When you create a Batch account, by default its compute nodes are assigned internally by hello Batch service.</span></span> <span data-ttu-id="85140-109">Ayrılmış işlem düğümleri konu tooa ayrı çekirdek kotası olacaktır ve hello hesabı ya da paylaşılan anahtar kimlik bilgileri veya bir Azure Active Dirctory belirteci aracılığıyla doğrulanabilir.</span><span class="sxs-lookup"><span data-stu-id="85140-109">Allocated compute nodes will be subject tooa separate core quota and hello account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="85140-110">Toplu işlem hesabı kullanıcı abonelik örnek komut dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="85140-110">Batch account using user subscription sample script</span></span>

<span data-ttu-id="85140-111">Ayrıca seçebilirsiniz toohave toplu işlem düğümlerinden kendi Azure aboneliği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85140-111">You can also opt toohave Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="85140-112">Allocate hesapları işlem düğümlerin aboneliğinizi içine bir Azure Active Directory token kimlik doğrulaması gerekir ve ayrılan hello işlem düğümleri abonelik kotanızı sayılacaktır.</span><span class="sxs-lookup"><span data-stu-id="85140-112">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and hello compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="85140-113">toocreate hesabınız bu modda, bir anahtar kasası başvuru hello hesabını oluştururken belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="85140-113">toocreate an account in this mode, one must specify a Key Vault reference when creating hello account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="85140-114">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="85140-114">Clean up deployment</span></span>

<span data-ttu-id="85140-115">Yukarıdaki örnek betikler hello birini çalıştırdıktan sonra komutu tooremove aşağıdaki hello kaynak grubu ve tüm ilgili kaynaklar (toplu işlem hesabı, Azure depolama hesapları ve Azure anahtar kasalarını dahil) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="85140-115">After you run either of hello above sample scripts, run hello following command tooremove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="85140-116">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="85140-116">Script explanation</span></span>

<span data-ttu-id="85140-117">Bu komut dosyası komutları toocreate bir kaynak grubu, toplu işlem hesabı ve tüm ilişkili kaynakları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="85140-117">This script uses hello following commands toocreate a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="85140-118">Her komut hello tablosundaki toocommand özgü belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="85140-118">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="85140-119">Komut</span><span class="sxs-lookup"><span data-stu-id="85140-119">Command</span></span> | <span data-ttu-id="85140-120">Notlar</span><span class="sxs-lookup"><span data-stu-id="85140-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="85140-121">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="85140-121">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="85140-122">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="85140-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="85140-123">az toplu işlem hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="85140-123">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="85140-124">Merhaba toplu işlem hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="85140-124">Creates hello Batch account.</span></span>  |
| [<span data-ttu-id="85140-125">az toplu işlem hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="85140-125">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="85140-126">Merhaba Batch hesabı özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="85140-126">Updates properties of hello Batch account.</span></span>  |
| [<span data-ttu-id="85140-127">az toplu işlem hesabı Göster</span><span class="sxs-lookup"><span data-stu-id="85140-127">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="85140-128">Belirtilen toplu hesaba hello ayrıntılarını alır.</span><span class="sxs-lookup"><span data-stu-id="85140-128">Retrieves details of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="85140-129">az batch hesabı anahtarları listesi</span><span class="sxs-lookup"><span data-stu-id="85140-129">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="85140-130">Merhaba alır hello erişim anahtarlarını toplu işlem hesabı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="85140-130">Retrieves hello access keys of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="85140-131">az toplu işlem hesabı oturum açma</span><span class="sxs-lookup"><span data-stu-id="85140-131">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="85140-132">Belirtilen hello karşı doğrular Batch hesabı başka CLI etkileşim için.</span><span class="sxs-lookup"><span data-stu-id="85140-132">Authenticates against hello specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="85140-133">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="85140-133">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="85140-134">Bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="85140-134">Creates a storage account.</span></span> |
| [<span data-ttu-id="85140-135">az keyvault oluşturma</span><span class="sxs-lookup"><span data-stu-id="85140-135">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="85140-136">Bir anahtar kasası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="85140-136">Creates a key vault.</span></span> |
| [<span data-ttu-id="85140-137">az keyvault-ilkesini ayarlama</span><span class="sxs-lookup"><span data-stu-id="85140-137">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="85140-138">Belirtilen anahtar kasası hello Hello güvenlik ilkesini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="85140-138">Update hello security policy of hello specified key vault.</span></span> |
| [<span data-ttu-id="85140-139">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="85140-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="85140-140">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="85140-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="85140-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="85140-141">Next steps</span></span>

<span data-ttu-id="85140-142">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="85140-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="85140-143">Ek toplu CLI kod örnekleri hello bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="85140-143">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

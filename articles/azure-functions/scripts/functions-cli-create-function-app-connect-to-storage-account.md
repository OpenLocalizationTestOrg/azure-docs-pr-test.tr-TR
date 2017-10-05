---
title: "Bir Azure depolama alanına bağlanan bir Azure işlevi oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - bir Azure depolama alanına bağlanan bir Azure işlevi oluşturma"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 36dbc2c181c9991a27163e3194800f63c6c0e01e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="b2dba-103">Azure Storage hesabınıza işlev uygulaması tümleştirme</span><span class="sxs-lookup"><span data-stu-id="b2dba-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="b2dba-104">Bu örnek betik, bir işlev uygulaması ve depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2dba-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b2dba-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2dba-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b2dba-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b2dba-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="b2dba-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b2dba-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b2dba-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="b2dba-108">Sample script</span></span>

<span data-ttu-id="b2dba-109">Bu örnek bir Azure işlevi uygulamasını oluşturur ve bir uygulama ayarı için depolama bağlantı dizesi ekler.</span><span class="sxs-lookup"><span data-stu-id="b2dba-109">This sample creates an Azure Function app and adds the storage connection string to an app setting.</span></span>

<span data-ttu-id="b2dba-110">[!code-azurecli-interactive[Ana](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "işlevi uygulamaya tümleştirmek Azure depolama hesabı")]</span><span class="sxs-lookup"><span data-stu-id="b2dba-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="b2dba-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="b2dba-111">Clean up deployment</span></span>

<span data-ttu-id="b2dba-112">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, App Service uygulaması kaldırmak için aşağıdaki komut kullanılabilir ve tüm kaynakları ilgili:</span><span class="sxs-lookup"><span data-stu-id="b2dba-112">After the script sample has been run, the following command can be used to remove the resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b2dba-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="b2dba-113">Script explanation</span></span>

<span data-ttu-id="b2dba-114">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2dba-114">This script uses the following commands.</span></span> <span data-ttu-id="b2dba-115">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="b2dba-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b2dba-116">Komut</span><span class="sxs-lookup"><span data-stu-id="b2dba-116">Command</span></span> | <span data-ttu-id="b2dba-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="b2dba-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b2dba-118">az oturum açma</span><span class="sxs-lookup"><span data-stu-id="b2dba-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="b2dba-119">Azure oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b2dba-119">Login to Azure.</span></span> |
| [<span data-ttu-id="b2dba-120">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2dba-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b2dba-121">Konumu ile kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="b2dba-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="b2dba-122">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2dba-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="b2dba-123">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2dba-123">Create a storage account</span></span> |
| [<span data-ttu-id="b2dba-124">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2dba-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="b2dba-125">Yeni bir işlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2dba-125">Create a new function app</span></span> |
| [<span data-ttu-id="b2dba-126">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="b2dba-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="b2dba-127">Temizleme</span><span class="sxs-lookup"><span data-stu-id="b2dba-127">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b2dba-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2dba-128">Next steps</span></span>

<span data-ttu-id="b2dba-129">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b2dba-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b2dba-130">Ek Azure işlevleri CLI kod örnekleri bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b2dba-130">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>

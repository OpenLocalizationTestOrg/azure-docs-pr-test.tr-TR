---
title: "Azure CLI toplu işleminde bir uygulama eklemek örnek - komut dosyası | Microsoft Docs"
description: "Azure CLI toplu işleminde bir uygulama eklemek örnek - komut dosyası"
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
ms.openlocfilehash: 5d057eaf32867aedc95d58c5185e2be1f9385ec0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a><span data-ttu-id="5d6a3-103">Azure CLI ile Azure Batch uygulamalarına ekleme</span><span class="sxs-lookup"><span data-stu-id="5d6a3-103">Adding applications to Azure Batch with Azure CLI</span></span>

<span data-ttu-id="5d6a3-104">Bu komut, bir uygulama için bir Azure Batch havuzu ya da görev ile kullanmak üzere ayarlamak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="5d6a3-105">Bir uygulamayı kurmak için bir .zip dosyasına tüm bağımlılıkları ile birlikte, yürütülebilir paketi.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="5d6a3-106">Bu örnekte yürütülebilir zip dosyası olarak adlandırılır ' my-uygulama-exe.zip'.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-106">In this example the executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d6a3-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5d6a3-107">Prerequisites</span></span>

- <span data-ttu-id="5d6a3-108">Sağlanan yönergeleri kullanarak Azure CLI yükleme [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="5d6a3-109">Zaten yoksa, bir toplu işlem hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="5d6a3-110">Bkz: [Azure CLI ile bir toplu işlem hesabı oluşturun](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) bir hesap oluşturan bir örnek komut dosyası için.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="5d6a3-111">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="5d6a3-111">Sample script</span></span>

<span data-ttu-id="5d6a3-112">[!code-azurecli[Ana](../../../cli_scripts/batch/add-application/add-application.sh "uygulama Ekle")]</span><span class="sxs-lookup"><span data-stu-id="5d6a3-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]</span></span>

## <a name="clean-up-application"></a><span data-ttu-id="5d6a3-113">Uygulamayı oluşturan Temizle</span><span class="sxs-lookup"><span data-stu-id="5d6a3-113">Clean up application</span></span>

<span data-ttu-id="5d6a3-114">Yukarıdaki örnek komut dosyasını çalıştırdıktan sonra uygulama ve onun karşıya yüklenen uygulama paketleri kaldırmak için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-114">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="5d6a3-115">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="5d6a3-115">Script explanation</span></span>

<span data-ttu-id="5d6a3-116">Bu komut, bir uygulama oluşturmak ve bir uygulama paketini karşıya yüklemek için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-116">This script uses the following commands to create an application and upload an application package.</span></span>
<span data-ttu-id="5d6a3-117">Komut özgü belgelere Tablo bağlantıları her komut.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-117">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="5d6a3-118">Komut</span><span class="sxs-lookup"><span data-stu-id="5d6a3-118">Command</span></span> | <span data-ttu-id="5d6a3-119">Notlar</span><span class="sxs-lookup"><span data-stu-id="5d6a3-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5d6a3-120">az batch uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d6a3-120">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="5d6a3-121">Bir uygulama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-121">Creates an application.</span></span>  |
| [<span data-ttu-id="5d6a3-122">az toplu uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="5d6a3-122">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="5d6a3-123">Bir uygulamanın özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-123">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="5d6a3-124">az toplu uygulama paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d6a3-124">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="5d6a3-125">Belirtilen uygulama için bir uygulama paketi ekler.</span><span class="sxs-lookup"><span data-stu-id="5d6a3-125">Adds an application package to the specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="5d6a3-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5d6a3-126">Next steps</span></span>

<span data-ttu-id="5d6a3-127">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5d6a3-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5d6a3-128">Ek toplu CLI kod örnekleri bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5d6a3-128">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

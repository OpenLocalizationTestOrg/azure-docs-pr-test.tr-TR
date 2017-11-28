---
title: "Azure bulut Kabuğu (Önizleme) hızlı başlangıç | Microsoft Docs"
description: "Azure bulut kabuğu için hızlı başlangıç"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 75676eb0ab784e2adbfd27b170c1dee5599b74ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-for-using-the-azure-cloud-shell"></a><span data-ttu-id="2b3ef-103">Azure bulut Kabuğu'nu kullanarak için hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="2b3ef-103">Quickstart for using the Azure Cloud Shell</span></span>

<span data-ttu-id="2b3ef-104">Bu belgede Azure bulut Kabuğu'nda kullanmak üzere nasıl ayrıntıları [Azure portal](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2b3ef-104">This document details how to use the Azure Cloud Shell in the [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="2b3ef-105">Bulut Kabuğu'nu başlatın</span><span class="sxs-lookup"><span data-stu-id="2b3ef-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="2b3ef-106">Başlatma **bulut Kabuk** Azure portal'ın üst gezinti gelen</span><span class="sxs-lookup"><span data-stu-id="2b3ef-106">Launch **Cloud Shell** from the top navigation of the Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="2b3ef-107">Bir depolama hesabı ve Azure dosya paylaşımı oluşturmak için bir abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="2b3ef-107">Select a subscription to create a storage account and Azure file share</span></span>
3. <span data-ttu-id="2b3ef-108">"Depolama oluştur" seçeneğini belirleyin</span><span class="sxs-lookup"><span data-stu-id="2b3ef-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="2b3ef-109">Azure CLI 2.0 için her oturumu otomatik olarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="2b3ef-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="2b3ef-110">Aboneliğinizi</span><span class="sxs-lookup"><span data-stu-id="2b3ef-110">Set your subscription</span></span>
1. <span data-ttu-id="2b3ef-111">Liste abonelikler erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2b3ef-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="2b3ef-112">Tercih edilen aboneliğinizi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="2b3ef-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="2b3ef-113">Aboneliğinizi kullanarak sonraki oturumlar için hatırlanır `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="2b3ef-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="2b3ef-114">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b3ef-114">Create a resource group</span></span>
<span data-ttu-id="2b3ef-115">İçinde WestUS "MyRG" adlı yeni bir kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2b3ef-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="2b3ef-116">Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b3ef-116">Create a Linux VM</span></span>
<span data-ttu-id="2b3ef-117">Bir Ubuntu VM, yeni kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2b3ef-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="2b3ef-118">Azure CLI 2.0 SSH anahtarları oluşturma ve bunlarla VM ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2b3ef-118">The Azure CLI 2.0 will create SSH keys and setup the VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="2b3ef-119">VM kimliğini doğrulamak için kullanılan ortak ve özel anahtarlar yerleştirilir `/User/.ssh/id_rsa` ve `/User/.ssh/id_rsa.pub` varsayılan olarak Azure CLI 2.0 tarafından.</span><span class="sxs-lookup"><span data-stu-id="2b3ef-119">The public and private keys used to authenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="2b3ef-120">.Ssh klasörü, bağlı Azure dosya paylaşımının 5 GB görüntüde kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="2b3ef-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="2b3ef-121">Bulut Kabuğu'nda kullanılan kullanıcı adı, kullanıcı adı bu VM'de olacaktır ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="2b3ef-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="2b3ef-122">SSH, Linux VM'NİZDE içine</span><span class="sxs-lookup"><span data-stu-id="2b3ef-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="2b3ef-123">Azure portal arama çubuğunda, VM adı arayın</span><span class="sxs-lookup"><span data-stu-id="2b3ef-123">Search for your VM name in the Azure portal search bar</span></span>
2. <span data-ttu-id="2b3ef-124">"Bağlan"'ı tıklatın ve çalıştırın:`ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="2b3ef-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="2b3ef-125">SSH bağlantı kurulduktan sonra Ubuntu Hoş Geldiniz istemi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b3ef-125">Upon establishing the SSH connection, you should see the Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="2b3ef-126">Temizleme</span><span class="sxs-lookup"><span data-stu-id="2b3ef-126">Cleaning up</span></span> 
<span data-ttu-id="2b3ef-127">Kaynak grubu ve içerdiği tüm kaynaklar Sil:</span><span class="sxs-lookup"><span data-stu-id="2b3ef-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="2b3ef-128">`az group delete -n MyRG` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2b3ef-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b3ef-129">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="2b3ef-129">Next Steps</span></span>
[<span data-ttu-id="2b3ef-130">Bulut Kabuk üzerinde kalıcı depolama hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="2b3ef-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="2b3ef-131">
[Azure CLI 2.0 hakkında bilgi edinin](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="2b3ef-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="2b3ef-132">
[Azure File storage hakkında bilgi edinin](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2b3ef-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>
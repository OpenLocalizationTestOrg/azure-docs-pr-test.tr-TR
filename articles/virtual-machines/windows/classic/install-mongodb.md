---
title: "aaaInstall Azure Windows VM üzerinde MongoDB | Microsoft Docs"
description: "Windows Server çalıştıran hello Klasik dağıtım modeliyle tooinstall Azure VM'de MongoDB nasıl oluşturulacağını öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="00a59-103">Windows Azure VM MongoDB yükleyin.</span><span class="sxs-lookup"><span data-stu-id="00a59-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="00a59-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="00a59-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="00a59-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="00a59-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="00a59-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="00a59-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="00a59-107">tooinstall ve hello Resource Manager dağıtım modelini kullanarak MongoDB yapılandırmak için bkz: [bu makalede](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="00a59-107">tooinstall and configure MongoDB using hello Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="00a59-108">[MongoDB] [ MongoDB] bir popüler açık kaynak, yüksek performanslı NoSQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="00a59-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="00a59-109">Bu makalede, bir Windows Server hello kullanarak sanal makine (VM) oluşturmada size yol gösterir [Azure portal][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="00a59-109">This article guides you through creating a Windows Server virtual machine (VM) using hello [Azure portal][AzurePortal].</span></span> <span data-ttu-id="00a59-110">Ardından oluşturun ve bir veri diski toohello yükleyip MongoDB yapılandırmadan önce VM ekleyin.</span><span class="sxs-lookup"><span data-stu-id="00a59-110">You then create and attach a data disk toohello VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="00a59-111">Mevcut bir VM'yi toouse istediğiniz Azure'da varsa, doğrudan çok atlayabilirsiniz[yükleme ve yapılandırma MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="00a59-111">If you have an existing VM in Azure that you would like toouse, you can jump straight too[installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="00a59-112">Windows Server çalıştıran bir sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="00a59-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="00a59-113">Bu yönergeler toocreate bir sanal makine izleyin.</span><span class="sxs-lookup"><span data-stu-id="00a59-113">Follow these instructions toocreate a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="00a59-114">Merhaba sanal makine oluşturulurken MongoDB için bir uç nokta ekleyin ve aşağıdaki gibi yapılandırın: olarak adlandırın **Mongo**, kullanın **TCP** hello Protokolü hem de kümesi ortak ve özel bağlantı noktalarını çok hello gibi**27017**.</span><span class="sxs-lookup"><span data-stu-id="00a59-114">You can add an endpoint for MongoDB while creating hello virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as hello protocol, and set both hello public and private ports too**27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="00a59-115">Veri diski ekleme</span><span class="sxs-lookup"><span data-stu-id="00a59-115">Attach a data disk</span></span>
<span data-ttu-id="00a59-116">tooprovide depolama hello sanal makine için bir veri diskini ve Windows kullanabilmesi başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="00a59-116">tooprovide storage for hello virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="00a59-117">Bir veri diski varsa, bu varolan bir diski ekleyebilirsiniz ya da boş bir disk ekleyin.</span><span class="sxs-lookup"><span data-stu-id="00a59-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="00a59-118">Merhaba disk başlatma ile ilgili yönergeler için bkz: "nasıl yapılır: Windows Server'da yeni bir veri diski başlatın" içinde [nasıl tooattach bir veri diski tooa Windows sanal makine](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="00a59-118">For instructions on initializing hello disk, see "How to: Initialize a new data disk in Windows Server" in [How tooattach a data disk tooa Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a><span data-ttu-id="00a59-119">Yükleyin ve MongoDB hello sanal makinede çalıştırın</span><span class="sxs-lookup"><span data-stu-id="00a59-119">Install and run MongoDB on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="00a59-120">Özet</span><span class="sxs-lookup"><span data-stu-id="00a59-120">Summary</span></span>
<span data-ttu-id="00a59-121">Bu öğreticide, nasıl toocreate Windows Server çalıştıran bir sanal makine uzaktan tooit bağlanın ve bir veri diskini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="00a59-121">In this tutorial, you learned how toocreate a virtual machine running Windows Server, remotely connect tooit, and attach a data disk.</span></span>  <span data-ttu-id="00a59-122">Ayrıca nasıl öğrenilen tooinstall ve MongoDB hello Windows tabanlı sanal makinede yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="00a59-122">You also learned how tooinstall and configure MongoDB on hello Windows-based virtual machine.</span></span> <span data-ttu-id="00a59-123">Artık MongoDB hello Windows tabanlı sanal makineye göre hello konularında Gelişmiş hello aşağıdaki erişebilirsiniz [MongoDB belgelerine][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="00a59-123">You can now access MongoDB on hello Windows-based virtual machine, by following hello advanced topics in hello [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/


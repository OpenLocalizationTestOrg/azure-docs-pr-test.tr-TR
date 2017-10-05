---
title: "Azure RemoteApp ile kullanmak için Azure VNET doğrulama | Microsoft Docs"
description: "Azure sanal Azure RemoteApp ile kullanıma hazır olduğundan emin olun öğrenin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 05c8a0ff04293947cec391b6467cc4adddb6a7b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="validate-the-azure-vnet-to-use-with-azure-remoteapp"></a><span data-ttu-id="53d5b-103">Azure RemoteApp ile kullanmak için Azure VNET doğrula</span><span class="sxs-lookup"><span data-stu-id="53d5b-103">Validate the Azure VNET to use with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="53d5b-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="53d5b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="53d5b-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="53d5b-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="53d5b-106">Azure RemoteApp ile bir Azure sanal kullanmadan önce sanal ağ doğrulamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53d5b-106">Before you use an Azure VNET with Azure RemoteApp, you might want to validate the VNET.</span></span> <span data-ttu-id="53d5b-107">Bu bağlantı sorunları önlemeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="53d5b-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="53d5b-108">Azure sanal doğrulamak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="53d5b-108">To validate your Azure VNET, do the following:</span></span>

1. <span data-ttu-id="53d5b-109">Azure RemoteApp ile kullanmak istediğiniz Azure sanal alt ağ içindeki bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53d5b-109">Create an Azure virtual machine inside the subnet of the Azure VNET you want to use with Azure RemoteApp.</span></span>
2. <span data-ttu-id="53d5b-110">Bağlan'kullanarak bu VM'ye **Bağlan** Yönetim Portalı'nda seçeneği.</span><span class="sxs-lookup"><span data-stu-id="53d5b-110">Connect to that VM by using the **Connect** option in the management portal.</span></span>
3. <span data-ttu-id="53d5b-111">Sanal makineyi Azure RemoteApp ile kullanmak istediğiniz aynı etki alanına katılın.</span><span class="sxs-lookup"><span data-stu-id="53d5b-111">Join the virtual machine to the same domain that you want to use with Azure RemoteApp.</span></span> <span data-ttu-id="53d5b-112">Şirket içi ağınıza bağlanan bir karma koleksiyon oluşturuyorsanız, sanal makinenin yerel etki alanınıza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="53d5b-112">If you are creating a hybrid collection that connects to your on-premises network, join the virtual machine to your local domain.</span></span>

<span data-ttu-id="53d5b-113">Bu başarılı olursa, Azure VNET RemoteApp ile kullanmak hazırdır.</span><span class="sxs-lookup"><span data-stu-id="53d5b-113">If this is successful, the Azure VNET is ready to use with RemoteApp.</span></span>

<span data-ttu-id="53d5b-114">Uçtan uca karma koleksiyonu iş akışı hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="53d5b-114">For more information about the end-to-end hybrid collection workflow, see the following articles:</span></span>

* [<span data-ttu-id="53d5b-115">Azure RemoteApp için sanal ağınızı planlama hakkında</span><span class="sxs-lookup"><span data-stu-id="53d5b-115">How to plan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="53d5b-116">Karma koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="53d5b-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="53d5b-117">Azure sanal ağınıza (desteğiyle ExpressRoute) Azure RemoteApp koleksiyonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="53d5b-117">Deploy Azure RemoteApp collection to your Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)


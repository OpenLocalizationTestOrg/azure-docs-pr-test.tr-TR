---
title: Azure RemoteApp ile aaaValidate hello Azure VNET toouse | Microsoft Docs
description: "Nasıl toomake emin Azure sanal hazır olduğunu öğrenin toouse Azure RemoteApp ile"
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
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a><span data-ttu-id="a54d3-103">Azure RemoteApp ile Hello Azure VNET toouse doğrula</span><span class="sxs-lookup"><span data-stu-id="a54d3-103">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a54d3-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="a54d3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a54d3-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="a54d3-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a54d3-106">Azure RemoteApp ile bir Azure sanal kullanmadan önce toovalidate hello VNET isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a54d3-106">Before you use an Azure VNET with Azure RemoteApp, you might want toovalidate hello VNET.</span></span> <span data-ttu-id="a54d3-107">Bu bağlantı sorunları önlemeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a54d3-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="a54d3-108">toovalidate Azure sanal ağınızın, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="a54d3-108">toovalidate your Azure VNET, do hello following:</span></span>

1. <span data-ttu-id="a54d3-109">Bir Azure sanal makinesi hello Azure toouse Azure RemoteApp ile istediğiniz sanal alt ağdan hello içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a54d3-109">Create an Azure virtual machine inside hello subnet of hello Azure VNET you want toouse with Azure RemoteApp.</span></span>
2. <span data-ttu-id="a54d3-110">Toothat VM hello kullanarak bağlanmak **Bağlan** hello Yönetim Portalı'nda seçeneği.</span><span class="sxs-lookup"><span data-stu-id="a54d3-110">Connect toothat VM by using hello **Connect** option in hello management portal.</span></span>
3. <span data-ttu-id="a54d3-111">Merhaba sanal makine toohello katılma toouse Azure RemoteApp ile istediğiniz aynı etki alanı.</span><span class="sxs-lookup"><span data-stu-id="a54d3-111">Join hello virtual machine toohello same domain that you want toouse with Azure RemoteApp.</span></span> <span data-ttu-id="a54d3-112">Tooyour şirket içi ağınızı bağlayan karma koleksiyon oluşturuyorsanız hello sanal makine tooyour yerel etki alanına katılın.</span><span class="sxs-lookup"><span data-stu-id="a54d3-112">If you are creating a hybrid collection that connects tooyour on-premises network, join hello virtual machine tooyour local domain.</span></span>

<span data-ttu-id="a54d3-113">Bu başarılı olursa, hello Azure VNET RemoteApp ile hazır toouse ' dir.</span><span class="sxs-lookup"><span data-stu-id="a54d3-113">If this is successful, hello Azure VNET is ready toouse with RemoteApp.</span></span>

<span data-ttu-id="a54d3-114">Merhaba uçtan uca karma koleksiyonu iş akışı hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="a54d3-114">For more information about hello end-to-end hybrid collection workflow, see hello following articles:</span></span>

* [<span data-ttu-id="a54d3-115">Nasıl tooplan Azure RemoteApp için sanal ağınıza</span><span class="sxs-lookup"><span data-stu-id="a54d3-115">How tooplan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="a54d3-116">Karma koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="a54d3-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="a54d3-117">Azure RemoteApp koleksiyonu tooyour Azure Virtual Network (desteğiyle ExpressRoute) dağıtma</span><span class="sxs-lookup"><span data-stu-id="a54d3-117">Deploy Azure RemoteApp collection tooyour Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)


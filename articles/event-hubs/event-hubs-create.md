---
title: bir Azure event hub aaaCreate | Microsoft Docs
description: "Azure Event Hubs ad alanı ve bir event hub'hello Azure portal kullanarak oluşturma"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a><span data-ttu-id="5361e-103">Bir olay hub'ları ad alanı ve bir event hub'hello Azure portal kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="5361e-103">Create an Event Hubs namespace and an event hub using hello Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="5361e-104">Bir olay hub'ları ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5361e-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="5361e-105">Toohello üzerinde oturum [Azure portal][Azure portal], tıklatıp **yeni** hello adresindeki hello ekranın sol üst.</span><span class="sxs-lookup"><span data-stu-id="5361e-105">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
1. <span data-ttu-id="5361e-106">Tıklatın **nesnelerin interneti**ve ardından **olay hub'ları**.</span><span class="sxs-lookup"><span data-stu-id="5361e-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="5361e-107">Merhaba, **ad alanı oluşturma** dikey penceresinde, bir ad alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="5361e-107">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="5361e-108">Merhaba adı olup olmadığını hello sistem hemen toosee denetler.</span><span class="sxs-lookup"><span data-stu-id="5361e-108">hello system immediately checks toosee if hello name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="5361e-109">Emin hello ad alanı adı yapmadan kullanılabilir olduktan sonra hello fiyatlandırma Katmanı (temel veya standart) seçin.</span><span class="sxs-lookup"><span data-stu-id="5361e-109">After making sure hello namespace name is available, choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="5361e-110">Ayrıca, hangi toocreate hello kaynak bir Azure aboneliği, kaynak grubunu ve konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="5361e-110">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> 
1. <span data-ttu-id="5361e-111">Tıklatın **oluşturma** toocreate hello ad alanı.</span><span class="sxs-lookup"><span data-stu-id="5361e-111">Click **Create** toocreate hello namespace.</span></span> <span data-ttu-id="5361e-112">Merhaba sistem toofully sağlama hello kaynakları için bir kaç dakika toowait olabilir.</span><span class="sxs-lookup"><span data-stu-id="5361e-112">You may have toowait a few minutes for hello system toofully provision hello resources.</span></span>
2. <span data-ttu-id="5361e-113">Merhaba portal listesinde ad alanları, yeni ad alanı oluşturulan hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5361e-113">In hello portal list of namespaces, click hello newly created namespace.</span></span>
2. <span data-ttu-id="5361e-114">Tıklatın **paylaşılan erişim ilkeleri**ve ardından **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="5361e-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="5361e-115">Merhaba Kopyala düğmesine toocopy hello tıklatın **RootManageSharedAccessKey** bağlantı dizesi toohello Pano.</span><span class="sxs-lookup"><span data-stu-id="5361e-115">Click hello copy button toocopy hello **RootManageSharedAccessKey** connection string toohello clipboard.</span></span> <span data-ttu-id="5361e-116">Bu bağlantı dizesini Not Defteri, daha sonra toouse gibi geçici bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5361e-116">Save this connection string in a temporary location, such as Notepad, toouse later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="5361e-117">Olay hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5361e-117">Create an event hub</span></span>

1. <span data-ttu-id="5361e-118">Merhaba olay hub'ları ad listesinde yeni oluşturulan hello ad alanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5361e-118">In hello Event Hubs namespace list, click hello newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="5361e-119">Merhaba ad alanı dikey penceresinde tıklayın **olay hub'ları**.</span><span class="sxs-lookup"><span data-stu-id="5361e-119">In hello namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="5361e-120">Merhaba dikey penceresinde Hello üstünde tıklatın **Event Hub'ı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="5361e-120">At hello top of hello blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="5361e-121">Olay hub'ınız için bir ad yazın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="5361e-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="5361e-122">Olay hub'ınız şimdi oluşturulur ve toosend gerekir ve olayları alma hello bağlantı dizelerine sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="5361e-122">Your event hub is now created, and you have hello connection strings you need toosend and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5361e-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5361e-123">Next steps</span></span>
<span data-ttu-id="5361e-124">Event Hubs hakkında daha fazla toolearn bu bağlantıları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="5361e-124">toolearn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="5361e-125">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="5361e-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="5361e-126">Event Hubs API’sine genel bakış</span><span class="sxs-lookup"><span data-stu-id="5361e-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/
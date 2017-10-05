---
title: "Bir Azure olay hub'ı oluşturma | Microsoft Docs"
description: "Azure Event Hubs ad alanı ve Azure portalını kullanarak bir event hub oluşturma"
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
ms.openlocfilehash: 816bf1426704d3391550e80c0700f1b011683a94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-the-azure-portal"></a><span data-ttu-id="61613-103">Bir olay hub'ları ad alanı ve Azure portalını kullanarak bir event hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="61613-103">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="61613-104">Bir olay hub'ları ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="61613-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="61613-105">[Azure portalında][Azure portal] oturum açın ve ekranın sol üst köşesindeki **Yeni**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61613-105">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
1. <span data-ttu-id="61613-106">Tıklatın **nesnelerin interneti**ve ardından **olay hub'ları**.</span><span class="sxs-lookup"><span data-stu-id="61613-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="61613-107">**Ad alanı oluştur** dikey penceresine bir ad alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="61613-107">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="61613-108">Adın kullanılabilirliği sistem tarafından hemen denetlenir.</span><span class="sxs-lookup"><span data-stu-id="61613-108">The system immediately checks to see if the name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="61613-109">Ad alanı adının kullanılabilir durumda olduğundan emin olduktan sonra fiyatlandırma katmanını (Temel veya Standart) seçin.</span><span class="sxs-lookup"><span data-stu-id="61613-109">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="61613-110">Ayrıca, bir Azure aboneliği, kaynak grubu ve kaynağın oluşturulacağı konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="61613-110">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> 
1. <span data-ttu-id="61613-111">Ad alanını oluşturmak için **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61613-111">Click **Create** to create the namespace.</span></span> <span data-ttu-id="61613-112">Tam olarak kaynakları sağlamak üzere sistem için bir kaç dakika beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="61613-112">You may have to wait a few minutes for the system to fully provision the resources.</span></span>
2. <span data-ttu-id="61613-113">Ad alanları portal listesinde yeni oluşturulan ad alanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61613-113">In the portal list of namespaces, click the newly created namespace.</span></span>
2. <span data-ttu-id="61613-114">Tıklatın **paylaşılan erişim ilkeleri**ve ardından **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="61613-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="61613-115">**RootManageSharedAccessKey** bağlantı dizesini panoya kopyalamak için kopyala düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61613-115">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span></span> <span data-ttu-id="61613-116">Bu bağlantı dizesi daha sonra kullanmak üzere not defteri gibi geçici bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="61613-116">Save this connection string in a temporary location, such as Notepad, to use later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="61613-117">Olay hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="61613-117">Create an event hub</span></span>

1. <span data-ttu-id="61613-118">Olay hub'ları ad listesinde yeni oluşturulan ad alanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61613-118">In the Event Hubs namespace list, click the newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="61613-119">Ad alanı dikey penceresinde **Event Hubs**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61613-119">In the namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="61613-120">Dikey pencerenin en üstündeki **Olay Hub’ı Ekle** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61613-120">At the top of the blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="61613-121">Olay hub'ınız için bir ad yazın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="61613-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="61613-122">Olay hub'ınız şimdi oluşturulur ve olayları alıp göndermek için gereken bağlantı dizelerine sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="61613-122">Your event hub is now created, and you have the connection strings you need to send and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61613-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="61613-123">Next steps</span></span>
<span data-ttu-id="61613-124">Event Hubs hakkında daha fazla bilgi için aşağıdaki bağlantıları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="61613-124">To learn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="61613-125">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="61613-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="61613-126">Event Hubs API’sine genel bakış</span><span class="sxs-lookup"><span data-stu-id="61613-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/
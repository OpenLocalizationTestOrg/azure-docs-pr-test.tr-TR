---
title: "Logic apps içinde Office 365 Video Bağlayıcısı'nı kullanın | Microsoft Docs"
description: "Office 365 Video Bağlayıcısı'nı Microsoft Azure App service Logic apps içinde kullanmaya başlama"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 738e5aa7-2523-4116-8b65-211b9063852d
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: f0e3613d4a3fd5478787c0365eb7a0bcde886c81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office365-video-connector"></a><span data-ttu-id="d2571-103">Office365 Video Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d2571-103">Get started with the Office365 Video connector</span></span>
<span data-ttu-id="d2571-104">Office 365 bir Office 365 hakkında bilgi video almak için videolar ve daha fazlası listesini almak için Video bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d2571-104">Connect to Office 365 Video to get information about an Office 365 video, get a list of videos, and more.</span></span> <span data-ttu-id="d2571-105">Office 365 Video ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d2571-105">With Office 365 Video, you can:</span></span>

* <span data-ttu-id="d2571-106">Office 365 Video alma verileri temel alan, iş akışınızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2571-106">Build your business flow based on the data you get from Office 365 Video.</span></span> 
* <span data-ttu-id="d2571-107">Video portal durumunu kontrol edin ve bir kanal tüm video listesini al eylemleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="d2571-107">Use actions that check the video portal status, get a list of all video in a channel, and more.</span></span> <span data-ttu-id="d2571-108">Bu eylemler bir yanıt ve çıkış diğer eylemler için kullanılabilir yapın.</span><span class="sxs-lookup"><span data-stu-id="d2571-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="d2571-109">Örneğin, Office 365 videolar için arama yapmak için Bing arama Bağlayıcısı'nı kullanın ve sonra bu video hakkında bilgi almak için Office 365 video Bağlayıcısı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d2571-109">For example, you can use the Bing Search connector to search for Office 365 videos, and then use the Office 365 video connector to get information about that video.</span></span> <span data-ttu-id="d2571-110">Video gereksinimlerinizi karşılıyorsa, bu videoyu FaceBook'ta nakledebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2571-110">If the video meets your requirements, you can post this video on Facebook.</span></span> 

<span data-ttu-id="d2571-111">Bir mantıksal uygulama'yi şimdi oluşturmaya başlamak, bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d2571-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office365-video-connector"></a><span data-ttu-id="d2571-112">Office365 Video Bağlayıcısı bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2571-112">Create a connection to Office365 Video connector</span></span>
<span data-ttu-id="d2571-113">Bu bağlayıcı mantıksal uygulamalarınızı eklediğinizde, Office 365 Video hesabınızda oturum açın ve gerekir mantıksal uygulamaları hesabınıza bağlanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d2571-113">When you add this connector to your logic apps, you must sign-in to your Office 365 Video account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Video](../../includes/connectors-create-api-office365video.md)]
> 
> 

<span data-ttu-id="d2571-114">Bağlantı oluşturduktan sonra Kiracı adı gibi Office 365 video özelliklerini girin veya kimliği kanal</span><span class="sxs-lookup"><span data-stu-id="d2571-114">After you create the connection, you enter the Office 365 video properties, like the tenant name or channel ID.</span></span> 


## <a name="connector-specific-details"></a><span data-ttu-id="d2571-115">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="d2571-115">Connector-specific details</span></span>

<span data-ttu-id="d2571-116">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/office365videoconnector/).</span><span class="sxs-lookup"><span data-stu-id="d2571-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365videoconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d2571-117">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="d2571-117">More connectors</span></span>
<span data-ttu-id="d2571-118">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d2571-118">Go back to the [APIs list](apis-list.md).</span></span>
---
title: "Logic apps içinde Google sürücü bağlayıcısını ekleyin | Microsoft Docs"
description: "REST API parametreleri Google sürücü bağlayıcısıyla genel bakış"
services: 
suite: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2bcebc5-02d2-435b-b0da-ef53bc51c4b6
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c066a10b33e172eb5f16eede43ec407794000c90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-google-drive-connector"></a><span data-ttu-id="11aa4-103">Google sürücü Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="11aa4-103">Get started with the Google Drive connector</span></span>
<span data-ttu-id="11aa4-104">Dosyaları, get satırları ve daha fazlasını oluşturmak için Google sürücüye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="11aa4-104">Connect to Google Drive to create files, get rows, and more.</span></span> <span data-ttu-id="11aa4-105">Google sürücüyle şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="11aa4-105">With Google Drive, you can:</span></span> 

* <span data-ttu-id="11aa4-106">İş akışınız aramanıza alma verileri temel alan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="11aa4-106">Build your business flow based on the data you get from your search.</span></span> 
* <span data-ttu-id="11aa4-107">Eylemler görüntüleri arama, Haberler ve daha fazla bilgi aramak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="11aa4-107">Use actions to search images, search the news, and more.</span></span> <span data-ttu-id="11aa4-108">Bu eylemler bir yanıt ve çıkış diğer eylemler için kullanılabilir yapın.</span><span class="sxs-lookup"><span data-stu-id="11aa4-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="11aa4-109">Örneğin, bir video arayın ve akış bir Twitter video göndermek için Twitter kullanın.</span><span class="sxs-lookup"><span data-stu-id="11aa4-109">For example, you can search for a video, and then use Twitter to post that video to a Twitter feed.</span></span>

<span data-ttu-id="11aa4-110">Bir mantıksal uygulama'yi şimdi oluşturmaya başlamak, bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="11aa4-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-the-connection-to-google-drive"></a><span data-ttu-id="11aa4-111">Google sürücü bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="11aa4-111">Create the connection to Google Drive</span></span>
<span data-ttu-id="11aa4-112">Bu bağlayıcı mantıksal uygulamalarınızı eklediğinizde, Google sürücüsüne bağlanacak şekilde mantıksal uygulamalar yetkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="11aa4-112">When you add this connector to your logic apps, you must authorize logic apps to connect to your Google Drive.</span></span>

> [!INCLUDE [Steps to create a connection to googledrive](../../includes/connectors-create-api-googledrive.md)]
> 
> 

<span data-ttu-id="11aa4-113">Bağlantı oluşturduktan sonra klasör yolu veya dosya adı gibi Google sürücü özelliklerini girin.</span><span class="sxs-lookup"><span data-stu-id="11aa4-113">After you create the connection, you enter the Google Drive properties, like the folder path or file name.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="11aa4-114">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="11aa4-114">Connector-specific details</span></span>

<span data-ttu-id="11aa4-115">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/googledrive/).</span><span class="sxs-lookup"><span data-stu-id="11aa4-115">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/googledrive/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="11aa4-116">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="11aa4-116">More connectors</span></span>
<span data-ttu-id="11aa4-117">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="11aa4-117">Go back to the [APIs list](apis-list.md).</span></span>

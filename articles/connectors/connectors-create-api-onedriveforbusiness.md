---
title: "OneDrive iş | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. OneDrive dosyalarınızı yönetmek iş bağlayın. Çeşitli eylemler gerçekleştir güncelleştirmenin yüklenmesi gibi almak ve dosyaları silin."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cf9484e9-7a20-4de0-93c8-0fa132221f2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 783d6a640d9626508bcabc5f991dc5b6fc22eaf4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-for-business-connector"></a><span data-ttu-id="ef7b8-105">İş bağlayıcı OneDrive kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ef7b8-105">Get started with the OneDrive for Business connector</span></span>
<span data-ttu-id="ef7b8-106">OneDrive dosyalarınızı yönetmek iş bağlayın.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-106">Connect to OneDrive for Business to manage your files.</span></span> <span data-ttu-id="ef7b8-107">Çeşitli eylemler gerçekleştir güncelleştirmenin yüklenmesi gibi almak ve dosyaları silin.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-107">You can perform various actions such as upload, update, get, and delete on files.</span></span>

<span data-ttu-id="ef7b8-108">Bir mantıksal uygulama'yi şimdi oluşturmaya başlamak, bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ef7b8-108">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-onedrive-for-business"></a><span data-ttu-id="ef7b8-109">OneDrive iş bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-109">Create a connection to OneDrive for Business</span></span>
<span data-ttu-id="ef7b8-110">OneDrive iş ile Logic apps oluşturmak için önce oluşturmanız gerekir bir **bağlantı** ardından ayrıntılar için aşağıdaki özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="ef7b8-110">To create Logic apps with OneDrive for Business, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="ef7b8-111">Özellik</span><span class="sxs-lookup"><span data-stu-id="ef7b8-111">Property</span></span> | <span data-ttu-id="ef7b8-112">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ef7b8-112">Required</span></span> | <span data-ttu-id="ef7b8-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ef7b8-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ef7b8-114">Belirteç</span><span class="sxs-lookup"><span data-stu-id="ef7b8-114">Token</span></span> |<span data-ttu-id="ef7b8-115">Evet</span><span class="sxs-lookup"><span data-stu-id="ef7b8-115">Yes</span></span> |<span data-ttu-id="ef7b8-116">OneDrive İş Kimlik Bilgilerini Girin</span><span class="sxs-lookup"><span data-stu-id="ef7b8-116">Provide OneDrive for Business Credentials</span></span> |

<span data-ttu-id="ef7b8-117">Bağlantı oluşturduktan sonra Eylemler yürütür ve bu makalede açıklanan Tetikleyicileri dinlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef7b8-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to OneDrive for Business](../../includes/connectors-create-api-onedriveforbusiness.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="ef7b8-118">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="ef7b8-118">Connector-specific details</span></span>

<span data-ttu-id="ef7b8-119">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/onedriveforbusinessconnector/).</span><span class="sxs-lookup"><span data-stu-id="ef7b8-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveforbusinessconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="ef7b8-120">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ef7b8-120">More connectors</span></span>
<span data-ttu-id="ef7b8-121">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ef7b8-121">Go back to the [APIs list](apis-list.md).</span></span>
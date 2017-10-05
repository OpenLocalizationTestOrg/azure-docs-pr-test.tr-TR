---
title: "Office 365 kullanıcıları bağlayıcı Logic Apps içinde ekleme | Microsoft Docs"
description: "Office 365 kullanıcıları bağlayıcı REST API parametrelerle genel bakış"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 330f733440932a769eb0fe6031cd0d947a820080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-users-connector"></a><span data-ttu-id="a494a-103">Office 365 kullanıcıları Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a494a-103">Get started with the Office 365 Users connector</span></span>
<span data-ttu-id="a494a-104">Profilleri, arama kullanıcıları ve daha fazla bilgi almak için Office 365 kullanıcıları için bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a494a-104">Connect to Office 365 Users to get profiles, search users, and more.</span></span> <span data-ttu-id="a494a-105">Office 365 kullanıcıları ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a494a-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="a494a-106">Office 365 kullanıcılardan alma verileri temel alan, iş akışınızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a494a-106">Build your business flow based on the data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="a494a-107">Doğrudan raporları Al kullanım Eylemler, bir yöneticinin kullanıcı profili ve daha fazla bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="a494a-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="a494a-108">Bu eylemler bir yanıt ve çıkış diğer eylemler için kullanılabilir yapın.</span><span class="sxs-lookup"><span data-stu-id="a494a-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="a494a-109">Örneğin, bir kişinin doğrudan rapor alın ve sonra bu bilgileri almak ve bir SQL Azure veritabanı güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="a494a-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="a494a-110">Bir mantıksal uygulama'yi şimdi oluşturmaya başlamak, bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a494a-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office-365-users"></a><span data-ttu-id="a494a-111">Office 365 kullanıcıları bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a494a-111">Create a connection to Office 365 Users</span></span>
<span data-ttu-id="a494a-112">Bu bağlayıcı mantıksal uygulamalarınızı eklediğinizde, Office 365 kullanıcıları hesabınızda oturum açın ve gerekir mantıksal uygulamaları hesabınıza bağlanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a494a-112">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="a494a-113">Bağlantı oluşturduktan sonra kullanıcı kimliği gibi Office 365 kullanıcıları özelliklerini girin</span><span class="sxs-lookup"><span data-stu-id="a494a-113">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span></span> <span data-ttu-id="a494a-114">**REST API Başvurusu** bu konuda bu özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="a494a-114">The **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="a494a-115">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="a494a-115">Connector-specific details</span></span>

<span data-ttu-id="a494a-116">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/officeusers/).</span><span class="sxs-lookup"><span data-stu-id="a494a-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="a494a-117">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="a494a-117">More connectors</span></span>
<span data-ttu-id="a494a-118">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a494a-118">Go back to the [APIs list](apis-list.md).</span></span>
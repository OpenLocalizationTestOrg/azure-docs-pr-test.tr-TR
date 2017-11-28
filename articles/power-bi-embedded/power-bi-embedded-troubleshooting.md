---
title: "Microsoft Power BI Embedded Önizleme sorunlarını giderme"
description: "Microsoft Power BI Embedded Önizleme sorunlarını giderme"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: f406d23e578acc825514aa5bd9eabcbf160bf9ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="75f0d-103">Microsoft Power BI Embedded Önizleme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="75f0d-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="75f0d-104">Bu makalede nasıl giderilir için yanıtlar sağlayan **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="75f0d-104">This article provides answers for how  to troubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="75f0d-105">SQL Server bağlantı dizelerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="75f0d-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="75f0d-106">Dize bağlanan bir SQL Server için belirli bir biçimi izleyen gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f0d-106">To set a SQL Server connecting string, you need to follow a specific format.</span></span> <span data-ttu-id="75f0d-107">SQL Server için bir örnek bağlantı dizesi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="75f0d-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="75f0d-108">SQL Server bağlantı dizeleri hakkında daha fazla bilgi edinmek için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="75f0d-108">To learn more about SQL Server connection strings, see the following articles:</span></span>

* [<span data-ttu-id="75f0d-109">SQL Server bağlantı dizeleri</span><span class="sxs-lookup"><span data-stu-id="75f0d-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="75f0d-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="75f0d-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="75f0d-111">Kimlik bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="75f0d-111">Setting credentials</span></span>
<span data-ttu-id="75f0d-112">Bir geliştirme veya kullanıcı adı ve parola gibi hazırlık ortamı için kimlik bilgilerini sahip olduğu durumda bir üretim çözüm eşleşen kimlik bilgilerini güncelleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="75f0d-112">In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="75f0d-113">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="75f0d-113">See Also</span></span>
* [<span data-ttu-id="75f0d-114">Bir örnek ile kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="75f0d-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="75f0d-115">Power BI Embedded nedir</span><span class="sxs-lookup"><span data-stu-id="75f0d-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)


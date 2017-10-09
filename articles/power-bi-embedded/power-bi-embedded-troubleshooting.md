---
title: "Power BI Embedded Önizleme aaaMicrosoft sorun giderme"
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
ms.openlocfilehash: a0a25cd73977c0ea0bd6b7c82e215412245771bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="c8fa9-103">Microsoft Power BI Embedded Önizleme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="c8fa9-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="c8fa9-104">Bu makalede yanıtlar hakkında bilgi sağlar. tootroubleshoot **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="c8fa9-104">This article provides answers for how  tootroubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="c8fa9-105">SQL Server bağlantı dizelerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="c8fa9-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="c8fa9-106">tooset bir SQL Server bağlantı dizesi, belirli bir biçimi toofollow gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8fa9-106">tooset a SQL Server connecting string, you need toofollow a specific format.</span></span> <span data-ttu-id="c8fa9-107">SQL Server için bir örnek bağlantı dizesi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="c8fa9-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="c8fa9-108">SQL Server bağlantı dizeleri hakkında daha fazla toolearn makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="c8fa9-108">toolearn more about SQL Server connection strings, see hello following articles:</span></span>

* [<span data-ttu-id="c8fa9-109">SQL Server bağlantı dizeleri</span><span class="sxs-lookup"><span data-stu-id="c8fa9-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="c8fa9-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="c8fa9-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="c8fa9-111">Kimlik bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="c8fa9-111">Setting credentials</span></span>
<span data-ttu-id="c8fa9-112">Bir geliştirme veya kullanıcı adı ve parola gibi hazırlık ortamı için kimlik bilgilerini sahip olduğu hello durumda üretim çözüm eşleşen tooupdate kimlik bilgileri gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c8fa9-112">In hello case where you have credentials for a development or staging environment, such as user name and password, you might need tooupdate credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="c8fa9-113">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="c8fa9-113">See Also</span></span>
* [<span data-ttu-id="c8fa9-114">Bir örnek ile kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c8fa9-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="c8fa9-115">Power BI Embedded nedir</span><span class="sxs-lookup"><span data-stu-id="c8fa9-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)


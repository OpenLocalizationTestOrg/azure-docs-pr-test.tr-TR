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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Microsoft Power BI Embedded Önizleme sorunlarını giderme
Bu makalede nasıl giderilir için yanıtlar sağlayan **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>SQL Server bağlantı dizelerini ayarlama
Dize bağlanan bir SQL Server için belirli bir biçimi izleyen gerekir. SQL Server için bir örnek bağlantı dizesi aşağıdadır.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

SQL Server bağlantı dizeleri hakkında daha fazla bilgi edinmek için aşağıdaki makalelere bakın:

* [SQL Server bağlantı dizeleri](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Kimlik bilgilerini ayarlama
Bir geliştirme veya kullanıcı adı ve parola gibi hazırlık ortamı için kimlik bilgilerini sahip olduğu durumda bir üretim çözüm eşleşen kimlik bilgilerini güncelleştirmeniz gerekebilir.

## <a name="see-also"></a>Ayrıca Bkz.
* [Bir örnek ile kullanmaya başlama](power-bi-embedded-get-started-sample.md)
* [Power BI Embedded nedir](power-bi-embedded-what-is-power-bi-embedded.md)


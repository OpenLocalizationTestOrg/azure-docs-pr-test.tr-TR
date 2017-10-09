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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Microsoft Power BI Embedded Önizleme sorunlarını giderme
Bu makalede yanıtlar hakkında bilgi sağlar. tootroubleshoot **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>SQL Server bağlantı dizelerini ayarlama
tooset bir SQL Server bağlantı dizesi, belirli bir biçimi toofollow gerekir. SQL Server için bir örnek bağlantı dizesi aşağıdadır.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

SQL Server bağlantı dizeleri hakkında daha fazla toolearn makaleler hello bakın:

* [SQL Server bağlantı dizeleri](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Kimlik bilgilerini ayarlama
Bir geliştirme veya kullanıcı adı ve parola gibi hazırlık ortamı için kimlik bilgilerini sahip olduğu hello durumda üretim çözüm eşleşen tooupdate kimlik bilgileri gerekebilir.

## <a name="see-also"></a>Ayrıca Bkz.
* [Bir örnek ile kullanmaya başlama](power-bi-embedded-get-started-sample.md)
* [Power BI Embedded nedir](power-bi-embedded-what-is-power-bi-embedded.md)


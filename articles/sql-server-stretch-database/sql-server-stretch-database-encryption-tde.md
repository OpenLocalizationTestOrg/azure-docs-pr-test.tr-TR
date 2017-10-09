---
title: "Saydam veri şifreleme için Esnetme veritabanı - Azure aaaEnable | Microsoft Docs"
description: "Saydam veri şifreleme (TDE) Azure üzerinde SQL Server Esnetme veritabanı için etkinleştirin"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Azure üzerinde Esnetme veritabanı için saydam veri şifreleme (TDE) etkinleştir
> [!div class="op_single_selector"]
> * [Azure portal](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Saydam veri şifreleme (TDE) gerçek zamanlı şifreleme ve şifre çözme hello veritabanının, ilişkili yedeklemelerinizi ve geri kalan işlem günlüğü dosyalarını değişiklikleri toohello gerek kalmadan gerçekleştirerek kötü amaçlı etkinliği hello tehdide karşı korunmasına yardımcı olur. uygulama.

TDE, bir simetrik anahtar adlı hello veritabanı şifreleme anahtarı kullanarak veritabanının tamamını hello depolanmasını şifreler. Merhaba veritabanı şifreleme anahtarı, bir yerleşik bir sunucu sertifikası tarafından korunur. Merhaba yerleşik bir sunucu sertifikası Azure her sunucu için benzersizdir. Microsoft, bu sertifikalar otomatik olarak en az 90 günde döndürür. TDE genel bir açıklaması için bkz [saydam veri şifreleme (TDE)].

## <a name="enabling-encryption"></a>Şifrelemeyi etkinleştirme
bir SQL Server Esnetme etkinleştirilmiş veritabanından veri geçişi hello depolama Azure bir veritabanı için tooenable TDE hello şeyler aşağıdaki:

1. Merhaba açık hello veritabanında [Azure portalı](https://portal.azure.com)
2. Merhaba veritabanı dikey penceresinde hello tıklayın **ayarları** düğmesi
3. Select hello **saydam veri şifreleme** seçeneği![][1]
4. Select hello **üzerinde** ayarlama ve ardından **Kaydet**
   ![][2]

## <a name="disabling-encryption"></a>Şifreleme devre dışı bırakma
bir SQL Server Esnetme etkinleştirilmiş veritabanından veri geçişi hello depolama Azure bir veritabanı için toodisable TDE hello şeyler aşağıdaki:

1. Merhaba açık hello veritabanında [Azure portalı](https://portal.azure.com)
2. Merhaba veritabanı dikey penceresinde hello tıklayın **ayarları** düğmesi
3. Select hello **saydam veri şifreleme** seçeneği
4. Select hello **kapalı** ayarlama ve ardından **Kaydet**

<!--Anchors-->
[saydam veri şifreleme (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->

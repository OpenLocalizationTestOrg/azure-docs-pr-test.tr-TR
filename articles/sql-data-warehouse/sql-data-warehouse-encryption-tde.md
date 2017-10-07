---
title: "aaaTransparent veri şifrelemesi SQL Data warehouse'da (Portal) | Microsoft Docs"
description: "SQL Data warehouse'da saydam veri şifreleme (TDE)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a>İle saydam veri şifreleme (TDE) SQL veri ambarı kullanmaya başlama
> [!div class="op_single_selector"]
> * [Güvenlik genel bakış](sql-data-warehouse-overview-manage-security.md)
> * [Kimlik doğrulaması](sql-data-warehouse-authentication.md)
> * [Şifreleme (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Şifreleme (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Gerekli izinleri
tooenable saydam veri şifreleme (TDE), bir yönetici veya hello dbmanager rolünün bir üyesi olmanız gerekir.

## <a name="enabling-encryption"></a>Şifrelemeyi etkinleştirme
tooenable TDE bir SQL Data Warehouse için hello adımları izleyin:

1. Merhaba açık hello veritabanında [Azure portalı](https://portal.azure.com)
2. Merhaba veritabanı dikey penceresinde hello tıklayın **ayarları** düğmesi
3. Select hello **saydam veri şifreleme** seçeneği![][1]
4. Select hello **üzerinde** ayarı![][2]
5. Seçin **Kaydet**
   ![][3]  

## <a name="disabling-encryption"></a>Şifreleme devre dışı bırakma
toodisable TDE bir SQL Data Warehouse için hello adımları izleyin:

1. Merhaba açık hello veritabanında [Azure portalı](https://portal.azure.com)
2. Merhaba veritabanı dikey penceresinde hello tıklayın **ayarları** düğmesi
3. Select hello **saydam veri şifreleme** seçeneği![][1]
4. Select hello **kapalı** ayarı![][4]
5. Seçin **Kaydet**
   ![][5]  

## <a name="encryption-dmvs"></a>Şifreleme Dmv'leri
Şifreleme ile Dmv'leri aşağıdaki hello onaylanabilir:

* [sys.Databases]
* [sys.dm_pdw_nodes_database_encryption_keys]

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.Databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->

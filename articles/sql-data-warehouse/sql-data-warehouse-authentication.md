---
title: aaaAuthentication tooAzure SQL Data Warehouse | Microsoft Docs
description: "Azure Active Directory (AAD) ve SQL Server kimlik doğrulama tooAzure SQL veri ambarı."
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a>Kimlik doğrulama tooAzure SQL veri ambarı
> [!div class="op_single_selector"]
> * [Güvenlik genel bakış](sql-data-warehouse-overview-manage-security.md)
> * [Kimlik doğrulaması](sql-data-warehouse-authentication.md)
> * [Şifreleme (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Şifreleme (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

tooconnect tooSQL veri ambarı, kimlik doğrulama amacıyla güvenlik kimlik bilgilerini geçmesi gerekir. Bağlantı kurulduktan sonra belirli bağlantı ayarları, sorgu oturumu bir parçası olarak yapılandırılır.  

Güvenlik hakkında daha fazla bilgi ve nasıl tooenable bağlantıları tooyour veri ambarı, bkz: [SQL veri ambarı veritabanında güvenli][Secure a database in SQL Data Warehouse].

## <a name="sql-authentication"></a>SQL kimlik doğrulaması
tooconnect tooSQL veri ambarı, aşağıdaki bilgilerle hello sağlamanız gerekir:

* Tam servername
* SQL kimlik doğrulaması belirtin
* Kullanıcı adı
* Parola
* Varsayılan veritabanı (isteğe bağlı)

Varsayılan olarak, bağlantı toohello bağlar *ana* veritabanı ve, kullanıcı veritabanını değil. tooconnect tooyour kullanıcı veritabanı toodo ikisinden birini seçebilirsiniz:

* Merhaba varsayılan veritabanı sunucunuz hello SQL Server Nesne Gezgini SSDT, SSMS, veya uygulama bağlantı dizenizi kaydedilirken belirtin. Örneğin, bir ODBC bağlantı için hello InitialCatalog parametresini ekleyin.
* Bir oturum SSDT oluşturmadan önce Hello kullanıcı veritabanı vurgulayın.

> [!NOTE]
> Transact-SQL deyimini hello **kullanım Veritabanım;** hello veritabanı bağlantı değiştirilmesi desteklenmiyor. SSDT ile tooSQL veri ambarına bağlanma rehberlik için toohello başvuran [sorgu Visual Studio ile] [ Query with Visual Studio] makale.
> 
> 

## <a name="azure-active-directory-aad-authentication"></a>Azure Active Directory (AAD) kimlik doğrulaması
[Azure Active Directory] [ What is Azure Active Directory] kimlik doğrulama mekanizmasıdır Azure Active Directory (Azure AD) kullanarak kimlikleri tooMicrosoft Azure SQL Data Warehouse bağlayan bir. Azure Active Directory kimlik doğrulaması ile veritabanı kullanıcıları hello kimlikleri ve diğer Microsoft Hizmetleri tek bir merkezi konumda merkezi olarak yönetebilir. Merkezi kimlik yönetimi toomanage SQL Data Warehouse kullanıcılar tek bir yer sağlar ve izin yönetimini basitleştirir. 

### <a name="benefits"></a>Avantajlar
Azure Active Directory yararlar şunlardır:

* Bir alternatif tooSQL sunucu kimlik doğrulaması sağlar.
* Yardımcı veritabanı sunucuları arasında kullanıcı kimlikleri hello artışı durdurun.
* Tek bir yerde parola döndürme sağlar
* Dış (AAD) gruplarını kullanarak veritabanı izinleri yönetin.
* Depolama parolalar, tümleşik Windows kimlik doğrulaması ve Azure Active Directory tarafından desteklenen kimlik doğrulama başka biçimlerde etkinleştirerek ortadan kaldırır.
* Kullanır, veritabanı kullanıcıları tooauthenticate kimlikleri hello veritabanı düzeyinde içeriyor.
* Belirteç tabanlı kimlik doğrulaması için tooSQL veri ambarına bağlanan uygulamaları destekler.
* Active Directory Evrensel kimlik doğrulaması aracılığıyla çok faktörlü kimlik doğrulaması için SQL Server Management Studio destekler. Çok faktörlü kimlik doğrulaması açıklaması için bkz: [SSMS desteklemek için SQL Database ve SQL Data Warehouse ile Azure AD MFA](../sql-database/sql-database-ssms-mfa-authentication.md).

> [!NOTE]
> Azure Active Directory hala yeni ve bazı sınırlamalar vardır. Azure Active Directory ortamınız için uygun olmanın olduğunu tooensure bkz [Azure AD özelliklerini ve sınırlamalarını][Azure AD features and limitations], özellikle dikkat edilecek diğer noktalar hello.
> 
> 

### <a name="configuration-steps"></a>Yapılandırma adımları
Bu adımları tooconfigure Azure Active Directory kimlik doğrulaması izleyin.

1. Oluşturma ve Azure Active Directory doldurma
2. İsteğe bağlı: İlişkilendir ya da şu anda Azure aboneliğinizle ilişkili hello active directory değiştirme
3. Azure SQL Data Warehouse için Azure Active Directory yönetici oluşturun.
4. İstemci bilgisayarları yapılandırın
5. Kapsanan veritabanı kullanıcıları, eşlenen veritabanı tooAzure AD kimlikleri oluşturma
6. Azure AD kimlikleri kullanarak tooyour veri ambarına bağlanma

Şu anda Azure Active Directory Kullanıcıları SSDT nesne Gezgini'nde gösterilmez. Geçici bir çözüm olarak hello kullanıcılar görüntülemek [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).

### <a name="find-hello-details"></a>Merhaba ayrıntılarını bulun
* Merhaba adımları tooconfigure ve kullanım Azure Active Directory kimlik doğrulaması Azure SQL Database ve Azure SQL Data Warehouse için neredeyse aynı. İzleyin hello ayrıntılı hello konudaki adımları [bağlanıyor tooSQL veritabanı veya SQL veri ambarı tarafından kullanarak Azure Active Directory kimlik doğrulaması](../sql-database/sql-database-aad-authentication.md).
* Özel veritabanı rolleri oluşturun ve kullanıcıların toohello roller ekleyin. Ardından toohello rolleri ayrıntılı izinleri verin. Daha fazla bilgi için bkz: [veritabanı altyapısı izinleri ile çalışmaya başlama](https://msdn.microsoft.com/library/mt667986.aspx).

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio ve diğer uygulamalar, veri Ambarınızı sorgulama toostart bkz [sorgu Visual Studio ile][Query with Visual Studio].

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations

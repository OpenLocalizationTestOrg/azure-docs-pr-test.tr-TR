---
title: "aaaConditional erişim - Azure SQL veritabanı ve veri ambarı | Microsoft belge"
description: "Bilgi tooconfigure koşullu erişim nasıl Azure SQL veritabanı ve veri ambarı için."
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>Azure SQL veritabanı ve veri ambarı ile koşullu erişim (MFA)  

SQL Database ve SQL Data Warehouse Microsoft koşullu erişimi destekler. adımları Göster nasıl aşağıdaki hello tooconfigure SQL veritabanı tooenforce bir koşullu erişim ilkesi.  

## <a name="prerequisites"></a>Ön koşullar  
- SQL Database veya SQL Data Warehouse toosupport Azure Active Directory kimlik doğrulaması yapılandırmanız gerekir. Belirli adımlar için bkz: [yapılandırma ve SQL Database veya SQL Data Warehouse ile Azure Active Directory kimlik doğrulamasını yönetmek](sql-database-aad-authentication-configure.md).  
- Çok faktörlü kimlik doğrulaması etkinleştirildiğinde ile desteklenen aracı en son SSMS hello gibi bağlamanız gerekir. Daha fazla bilgi için bkz: [SQL Server Management Studio Azure SQL veritabanını yapılandırma çok faktörlü kimlik doğrulamasını](sql-database-ssms-mfa-authentication-configure.md).  

## <a name="configure-ca-for-azure-sql-dbdw"></a>Azure SQL DB/DW için CA'yı yapılandırma  
1.  Oturum açma toohello Portal seçin **Azure Active Directory**ve ardından **koşullu erişim**. Daha fazla bilgi için bkz: [Azure Active Directory koşullu erişim teknik başvuru](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).  
  ![koşullu erişim dikey penceresi](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  Merhaba, **koşullu erişim ilkeleri** dikey penceresinde tıklatın **yeni ilke**, bir ad sağlayın ve ardından **kurallar**.  
3.  Altında **atamaları**seçin **kullanıcılar ve gruplar**, denetleme **kullanıcıları ve grupları seçin**, koşullu erişim için hello kullanıcısı veya grubu seçin. Tıklatın **seçin**ve ardından **Bitti** tooaccept seçiminizi.  
  ![Kullanıcıları ve grupları seçin](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  Seçin **bulut uygulamaları**, tıklatın **uygulamaları**. Tüm uygulamalar için koşullu erişim kullanılabilir bakın. Seçin **Azure SQL veritabanı**, hello altındaki tıklatın **seçin**ve ardından **Bitti**.  
  ![SQL veritabanı seçin](./media/sql-database-conditional-access/select-sql-database.png)  
  Bilgisayarınızda bulamazsanız **Azure SQL veritabanı** hello üçüncü ekran görüntüsü aşağıdaki listede, hello aşağıdaki adımları tamamlayın:   
  - Tooyour Azure SQL DB/DW örneğinde SSMS ile bir AAD yönetici hesabı kullanarak oturum açın.  
  - Yürütme `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.  
  - İçinde tooAAD oturum ve Azure SQL veritabanı ve veri ambarı, AAD hello uygulamalarda listelendiğini doğrulayın.  

5.  Seçin **erişim denetimleri**seçin **Grant**ve ardından tooapply istediğiniz hello İlkesi denetleyin. Bu örnekte, biz seçin **çok faktörlü kimlik doğrulaması gerektiren**.  
  ![erişim izni ver seçin](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>Özet  
Seçili Merhaba uygulaması tooconnect tooAzure SQL DB/DW Azure AD Premium kullanarak izin verme (Azure SQL veritabanı) seçili hello koşullu erişim ilkesi, şimdi zorlar **gerekli çok faktörlü kimlik doğrulaması.**  
Çok faktörlü kimlik doğrulaması ile ilgili Azure SQL veritabanı ve veri ambarı hakkında sorular için başvurun MFAforSQLDB@microsoft.com.  

## <a name="next-steps"></a>Sonraki adımlar  

Bir öğretici için bkz: [Azure SQL veritabanınıza güvenli](sql-database-security-tutorial.md).

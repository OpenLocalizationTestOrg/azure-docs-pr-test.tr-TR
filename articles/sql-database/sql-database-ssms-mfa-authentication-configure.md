---
title: "aaaConfigure çok faktörlü kimlik doğrulama - Azure SQL | Microsoft Docs"
description: "Kimlik doğrulaması çoklu oluşturmak SSMS ile SQL veritabanı ve SQL Data Warehouse için kullanın."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/17/2017
ms.author: rickbyh
ms.openlocfilehash: acb275965f4199f7d5e1378d5077824a9bbc80e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a>SQL Server Management Studio ve Azure AD için çok faktörlü kimlik doğrulamasını yapılandırma

Bu konu, nasıl gösterir SQL Server Management Studio ile toouse Azure Active Directory'ye multi factor authentication (MFA). Azure AD MFA SSMS veya SqlPackage.exe tooAzure SQL Database ve Azure SQL Data Warehouse bağlanırken kullanılabilir.

Azure SQL veritabanı çok faktörlü kimlik doğrulamasına genel bakış için bkz: [Evrensel kimlik doğrulaması SQL Database ve SQL Data Warehouse (MFA desteği SSMS) ile](sql-database-ssms-mfa-authentication.md).

## <a name="configuration-steps"></a>Yapılandırma adımları

1. **Bir Azure Active Directory yapılandırma** - daha fazla bilgi için bkz: [Azure AD dizininizi yönetme](https://msdn.microsoft.com/library/azure/hh967611.aspx), [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](../active-directory/active-directory-aadconnect.md), [Kendi etki alanı adı tooAzure AD eklemek](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure artık Windows Server Active Directory ile Federasyon destekler](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), ve [Windows PowerShell kullanarak Azure AD'yi yönetme ](https://msdn.microsoft.com/library/azure/jj151815.aspx).
2. **MFA yapılandırma** - adım adım yönergeler için bkz: [Azure multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md), [koşullu erişim (MFA) ile Azure SQL veritabanı ve veri ambarı](sql-database-conditional-access.md). (Bir Premium Azure Active Directory (Azure AD) tam koşullu erişim gerektirir. Sınırlı MFA standart bir Azure AD ile kullanılabilir.)
3. **SQL Database veya SQL Data Warehouse Azure AD kimlik doğrulaması için yapılandırma** - adım adım yönergeler için bkz: [bağlanıyor tooSQL veritabanı veya SQL veri ambarı tarafından kullanarak Azure Active Directory kimlik doğrulaması](sql-database-aad-authentication.md).
4. **SSMS karşıdan** - hello istemci bilgisayarda, indirme gelen son SSMS hello [karşıdan SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Merhaba, tüm özellikler için bu konudaki en az Temmuz 2017, sürüm 17,2 kullanın.  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a>SSMS ile Evrensel kimlik doğrulaması kullanarak bağlanma

Aşağıdaki adımları hello nasıl tooconnect tooSQL veritabanı veya kullanarak SQL Data Warehouse hello son SSMS gösterir.

1. Merhaba üzerinde Evrensel kimlik doğrulamasını kullanarak tooconnect **tooServer bağlanmak** iletişim kutusunda **Active Directory - Evrensel MFA desteğiyle**. (Görürseniz **Active Directory Evrensel kimlik doğrulaması** hello en son sürümünde SSMS değildir.)  
   ![1mfa Evrensel Bağlan][1]  
2. Tam hello **kullanıcı adı** hello biçiminde hello Azure Active Directory kimlik kutusuyla `user_name@domain.com`.  
   ![1mfa-universal-connect-kullanıcı](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)   
3. Konuk kullanıcı olarak bağlanıyorsanız tıklatmalısınız **seçenekleri**ve hello **bağlantı özelliği** iletişim kutusu, tam hello **AD etki alanı adı veya Kiracı kimliği** kutusu. Daha fazla bilgi için bkz: [Evrensel kimlik doğrulaması SQL Database ve SQL Data Warehouse (MFA desteği SSMS) ile](sql-database-ssms-mfa-authentication.md).
   ![mfa Kiracı ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   
4. SQL Database ve SQL Data Warehouse için her zamanki gibi tıklatmalısınız **seçenekleri** ve hello veritabanı üzerinde hello belirtin **seçenekleri** iletişim kutusu. (Merhaba bağlıysa Konuk kullanıcı olduğu (yani joe@outlook.com), hello kutuyu işaretleyin ve hello geçerli AD etki alanı adı veya Kiracı kimliği seçenekleri bir parçası olarak eklemeniz gerekir. Bkz: [Evrensel kimlik doğrulaması SQL Database ve SQL Data Warehouse (MFA desteği SSMS) ile]()(sql-veritabanı-ssms-mfa-authentication.md. Ardından **Bağlan**.  
5. Ne zaman hello **tooyour hesabında oturum** iletişim kutusu görüntülenirse, hello hesabı ve parolası, Azure Active Directory kimlik bilgilerinizi sağlayın. Parolasız bir kullanıcı Azure AD ile federe bir etki alanının parçası ise gereklidir.  
   ![2mfa oturum aç][2]  

   > [!NOTE]
   > MFA gerektirmeyen bir hesapla Evrensel kimlik doğrulaması için bu noktada bağlayın. MFA gerektirme kullanıcılar için aşağıdaki adımları hello ile devam edin:
   >  
   
6. İki MFA Kurulum iletişim kutusu görünebilir. Bu bir kez işlem ayarı hello MFA yönetici bağlıdır ve bu nedenle isteğe bağlı olabilir. MFA etkinse etki alanı için bu adımı bazen önceden tanımlanmış (örneğin, hello etki alanı kullanıcıları toouse akıllı kart ve PIN gerektirir).  
   ![3mfa Kurulumu][3]  
7. Merhaba ikinci olası bir kez iletişim kutusu, kimlik doğrulama yöntemini tooselect hello ayrıntılarını verir. Merhaba olası seçenekleri, yöneticiniz tarafından yapılandırılır.  
   ![4mfa doğrula 1][4]  
8. Hello Azure Active Directory bilgileri tooyou onaylayan hello gönderir. Merhaba doğrulama kodunu aldığınızda, hello girin **doğrulama kodunu girin** ve'ı tıklatın **oturum**.  
   ![5mfa doğrula 2][5]  

Doğrulama tamamlandıktan sonra normal olarak geçerli kimlik bilgileri ve güvenlik duvarı erişim pek fazla SSMS bağlanır.

## <a name="next-steps"></a>Sonraki adımlar

* Evrensel kimlik doğrulaması ile Azure SQL veritabanı çok faktörlü kimlik doğrulamasına genel bakış için bkz: [SQL Database ve SQL Data Warehouse (MFA desteği SSMS)](sql-database-ssms-mfa-authentication.md).
* Başkalarının tooyour veritabanına erişim izni: [SQL veritabanı kimlik doğrulaması ve yetkilendirme: erişim verme](sql-database-manage-logins.md)  
Başkalarının hello güvenlik duvarı üzerinden bağlanabilir emin olun: [yapılandırma bir Azure SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı kullanarak hello Azure portalı](sql-database-configure-firewall-settings.md)


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png


---
title: "aaaSecuring Azure PaaS veritabanlarında | Microsoft Docs"
description: " Azure SQL Database ve SQL veri ambarı güvenliği hakkında bilgi edinme PaaS web ve mobil uygulamaların güvenliğini sağlamaya yönelik en iyi uygulamalar. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: a7f9a2846b59dcb05e82f2ad88b41c5213295603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-databases-in-azure"></a>Azure PaaS veritabanlarında güvenliğini sağlama

Bu makalede, bir koleksiyonu aşağıdakiler ele [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/) ve [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/) PaaS web ve mobil uygulamaların güvenliğini sağlamaya yönelik en iyi güvenlik uygulamaları. Bu en iyi uygulamaları Azure ile deneyimi bizim türetilmiş ve müşterilerin hello deneyimleri bulunun.

## <a name="azure-sql-database-and-sql-data-warehouse"></a>Azure SQL Database ve SQL veri ambarı
[Azure SQL veritabanı](../sql-database/sql-database-technical-overview.md) ve [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) , Internet tabanlı uygulamalar için bir ilişkisel veritabanı hizmeti sağlar. Azure SQL Database ve SQL Data Warehouse dağıtımı bir PaaS kullanırken, uygulamaları ve verileri korumaya yardımcı olmak Hizmetleri bakalım:

- Azure Active Directory kimlik doğrulaması (yerine SQL Server kimlik doğrulaması)
- Azure SQL güvenlik duvarı
- Saydam veri şifreleme (TDE)

## <a name="best-practices"></a>En iyi uygulamalar

### <a name="use-a-centralized-identity-repository-for-authentication-and-authorization"></a>Kimlik doğrulama ve yetkilendirme için merkezi kimlik deposu kullanın

Azure SQL veritabanları, yapılandırılmış toouse iki tür kimlik doğrulaması biri olabilir:

- **SQL kimlik doğrulaması** bir kullanıcı adı ve parola kullanır. Veritabanınız için hello mantıksal sunucu oluşturduğunuzda, bir kullanıcı adı ve parola bir "sunucusuna yönetici" oturum açma belirttiniz. Bu kimlik bilgilerini kullanarak, bu sunucu üzerinde tooany veritabanı hello veritabanı sahibi olarak doğrulayabilir.

- **Azure Active Directory kimlik doğrulaması** Azure Active Directory tarafından yönetilen kimlikleri kullanır ve yönetilen ve tümleşik etki alanları için desteklenir. Azure Active Directory kimlik doğrulaması toouse hello "tooadminister Azure AD kullanıcıları ve grupları izin Azure AD yönetim," adlı başka bir sunucu yöneticisinin oluşturmanız gerekir. Bu yönetici normal bir sunucu yöneticisinin gerçekleştirebileceği tüm işlemleri yapabilir.

[Azure Active Directory kimlik doğrulaması](../active-directory/develop/active-directory-authentication-scenarios.md) tooAzure SQL Database ve SQL Data Warehouse Azure Active Directory (AD,) kullanarak kimlikleri bağlayan bir mekanizmadır. Azure AD kullanıcı kimlikleri hello artışı veritabanı sunucuları arasında durdurmak için bir alternatif tooSQL sunucu kimlik doğrulaması sağlar. Azure AD kimlik doğrulama sağlar, toocentrally veritabanı kullanıcıları ve diğer Microsoft Hizmetleri tek bir merkezi konumda hello Kimlikleri Yönet. Merkezi kimlik yönetimi toomanage veritabanı kullanıcıları tek bir yer sağlar ve izin yönetimini basitleştirir.  

SQL kimlik doğrulaması yerine Azure AD kimlik doğrulaması kullanmanın avantajları şunlardır:

- Tek bir yerde parola döndürme sağlar.
- Dış Azure kullanarak veritabanı izinlerini yönetir AD grupları.
- Depolama parolalar, tümleşik Windows kimlik doğrulaması ve Azure AD tarafından desteklenen kimlik doğrulama başka biçimlerde etkinleştirerek ortadan kaldırır.
- Kullanır, veritabanı kullanıcıları tooauthenticate kimlikleri hello veritabanı düzeyinde içeriyor.
- Belirteç tabanlı kimlik doğrulaması için tooSQL veritabanına bağlanan uygulamaları destekler.
- Etki alanı eşitleme olmadan yerel bir Azure AD için ADFS (etki alanı Federasyonu) veya yerel kullanıcı/parola kimlik doğrulamasını destekler.
- Active Directory Evrensel içeren kimlik doğrulaması kullanan SQL Server Management Studio bağlantılarını destekler [çok faktörlü kimlik doğrulama (MFA)](../multi-factor-authentication/multi-factor-authentication.md). MFA kolay doğrulama seçeneklerini aralıklı güçlü kimlik doğrulaması içerir — telefon araması, SMS mesajı, akıllı kartlar ve PIN ya da mobil uygulama bildirimi. Daha fazla bilgi için bkz: [SSMS desteklemek için SQL Database ve SQL Data Warehouse ile Azure AD MFA](../sql-database/sql-database-ssms-mfa-authentication.md).

Azure AD kimlik doğrulama hakkında daha fazla toolearn bakın:

- [TooSQL veritabanı veya SQL veri ambarı tarafından kullanarak Azure Active Directory kimlik doğrulaması bağlanma](../sql-database/sql-database-aad-authentication.md)
- [Kimlik doğrulama tooAzure SQL veri ambarı](../sql-data-warehouse/sql-data-warehouse-authentication.md)
- [Azure AD kimlik doğrulaması kullanarak Azure SQL DB belirteç tabanlı kimlik doğrulama desteği](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)

> [!NOTE]
> Azure Active Directory ortamınız için uygun olmanın olduğunu tooensure bkz [Azure AD özelliklerini ve sınırlamalarını](../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations), özellikle hello ek hususlar.
>
>

### <a name="restrict-access-based-on-ip-address"></a>IP adresine göre erişimi kısıtlama
Kabul edilebilir IP adreslerinin aralıklarını belirtmek güvenlik duvarı kuralları oluşturabilirsiniz. Bu kurallar, hem hello sunucu ve veritabanı düzeyinde hedeflenebilir. Veritabanı düzeyinde güvenlik duvarı kuralları kullanmanızı öneririz her olası tooenhance güvenlik ve toomake veritabanınızı daha taşınabilir. Sunucu düzeyinde güvenlik duvarı kuralları en iyi Yöneticiler için kullanılır ve hello sahip birçok veritabanı varsa aynı erişim gereksinimleri, ancak her veritabanı ayrı ayrı yapılandırma toospend zaman istemiyorum.

SQL veritabanı'nın varsayılan kaynak IP adresi sınırlamaları (diğer abonelikler ve kiracılar dahil) tüm Azure adresinden erişime izin ver. Bu tooonly kısıtlayabilirsiniz IP adreslerini tooaccess hello örneğinizi izin. Hatta, SQL güvenlik duvarı ve IP adresi sınırlamaları ile güçlü kimlik doğrulaması hala gereklidir. Bu makalenin önceki bölümlerinde hello önerilerin bakın.

Azure SQL güvenlik duvarı ve IP kısıtlamaları hakkında daha fazla toolearn bakın:

- [Azure SQL veritabanına erişim denetimi](../sql-database/sql-database-control-access.md)
- [Azure SQL veritabanı güvenlik duvarı kurallarını - yapılandırma genel bakış](../sql-database/sql-database-firewall-configure.md)
- [Hello Azure portal kullanarak bir Azure SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı yapılandırma](../sql-database/sql-database-configure-firewall-settings.md)

### <a name="encryption-of-data-at-rest"></a>Bekleyen verilerin şifrelenmesi
[Saydam veri şifreleme (TDE)](https://msdn.microsoft.com/library/azure/bb934049) varsayılan olarak etkindir. TDE, SQL Server, Azure SQL Database ve Azure SQL Data Warehouse veri ve günlük dosyalarını saydam şifreler. TDE doğrudan erişim toohello dosyaları veya kendi yedekleme güvenliğinin karşı korur. Bu işlem, mevcut uygulamaları değiştirmeden rest tooencrypt verileri sağlar. TDE, her zaman etkin kalmalı; Ancak, bu hello normal erişim yolu kullanarak bir saldırganın durdurmaz. TDE hello özelliği toocomply pek çok yasalar, düzenlemeler ve çeşitli sektörün oluşturduğu yönergeleri sağlar.

Azure SQL TDE'nin için anahtar ilgili sorunlar yönetir. Tooensure kurtarılabilirliği TDE ile şirket içi özellikle dikkatli olunmalıdır gibi ve veritabanlarını taşıma. Daha karmaşık senaryolarda hello anahtarları açıkça Azure anahtar kasası Genişletilebilir anahtar yönetimi yönetilebilir (bkz [etkinleştirmek TDE SQL Server kullanarak EKM üzerinde](/security/encryption/enable-tde-on-sql-server-using-ekm)). Bu ayrıca Getir bilgisayarınızı kendi anahtarını (BYOK için) Azure anahtar kasası BYOK yeteneği sağlar.

Azure SQL sütunlar için şifreleme sağlar [her zaman şifreli](/sql/relational-databases/security/encryption/always-encrypted-database-engine). Bu, toosensitive sütunları yalnızca yetkili uygulamalar erişim sağlar. Bu tür bir şifreleme kullanarak SQL sorgularını şifrelenmiş sütunlar tooequality dayalı değerler için sınırlar.

Uygulama düzeyinde şifreleme için seçmeli verileri de kullanılması gerekir. Veri egemenliği sorunları bazen hello doğru ülkede tutulur bir anahtarla verileri şifreleyerek azaltılabilir. Bu, hatta yanlışlıkla veri aktarımı (AES 256 gibi) kullanılan veri hello anahtarı, güçlü bir algoritma varsayılarak olmadan imkansız toodecrypt hello olduğundan bir soruna neden önler.

Ek güvenlik önlemleri toohelp güvenli hello veritabanını güvenli bir sistemde tasarlama, gizli varlıklar şifreleme ve bir Güvenlik Duvarı'nı hello veritabanı sunucuları geçici oluşturma gibi kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede SQL veritabanı ve PaaS web ve mobil uygulamaların güvenliğini sağlamaya yönelik SQL veri ambarı en iyi güvenlik uygulamalarını, tooa koleksiyonu sunmuştur. PaaS dağıtımlarınızın güvenliğini sağlama hakkında daha fazla toolearn bakın:

- [PaaS dağıtımlarının güvenliğini sağlama](security-paas-deployments.md)
- [PaaS web ve mobil uygulamaları Azure App Services kullanarak güvenli hale getirme](security-paas-applications-using-app-services.md)

---
title: "Azure Analysis Services aaaAuthentication ve kullanıcı izinleri | Microsoft Docs"
description: "Azure Analysis Services kimlik doğrulama ve kullanıcı izinleri hakkında bilgi edinin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: dd49fd59eec1f68dfe8a0fe373fa612ac46de4e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-user-permissions"></a>Kimlik doğrulaması ve kullanıcı izinleri
Azure Analysis Services Kimlik Yönetimi ve kullanıcı kimlik doğrulaması için Azure Active Directory (Azure AD) kullanır. Herhangi bir kullanıcı oluşturma, yönetme veya tooan Azure Analysis Services bağlanma sunucu geçerli kullanıcı kimliği olmalıdır bir [Azure AD kiracısı](../active-directory/active-directory-administer.md) hello içinde aynı abonelik.

Azure Analysis Services destekleyen [Azure AD B2B işbirliği](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md). B2B ile bir Azure AD dizinine Konuk kullanıcılar olarak kuruluşun dışındaki kullanıcıları davet edilebilirsiniz. Konuklar, başka bir Azure AD Kiracı dizini veya herhangi bir geçerli e-posta adresi olabilir. Bir kez davet ve hello davet e-posta ile Azure kaynağından hello kullanıcı kimliği toohello Kiracı dizin eklenir gönderilen hello kullanıcı kabul eder. Bu kimlikleri sonra toosecurity grupları eklenebilir veya sunucu yöneticisi veya veritabanı rolü üyeleri olarak.

![Azure Analysis Services kimlik doğrulama mimarisi](./media/analysis-services-manage-users/aas-manage-users-arch.png)

## <a name="authentication"></a>Kimlik Doğrulaması
Bir veya daha fazla hello Analysis Services tüm istemci uygulamaları ve araçları kullanmak [istemci kitaplıkları](analysis-services-data-providers.md) (AMO, MSOLAP, ADOMD) tooconnect tooa sunucu. 

Tüm üç istemci kitaplıkları, hem Azure AD etkileşimli akış ve etkileşimli olmayan kimlik doğrulama yöntemlerini destekler. Etkileşimli olmayan yöntemlerden Merhaba, Active Directory parolası ve Active Directory tümleşik kimlik doğrulaması yöntemleri AMOMD ve MSOLAP kullanan uygulamalarda kullanılabilir. Bu iki yöntem hiçbir zaman açılır iletişim kutularında neden.

SSMS ve SSDT gibi araçlar hello en son güncelleştirildiği hello kitaplıklarının sürümlerini yükleyin ve istemci uygulamaları gibi Excel ve Power BI Desktop toohello en son sürüm. Power BI Desktop, SSMS ve SSDT aylık güncelleştirilir. Excel [Office 365 ile güncelleştirilmiş](https://support.office.com/en-us/article/When-do-I-get-the-newest-features-in-Office-2016-for-Office-365-da36192c-58b9-4bc9-8d51-bb6eed468516). Office 365 güncelleştirmelerini daha az sıklıkta ve anlamı güncelleştirmeleri toothree ay ertelenmiş, bazı kuruluşlar hello ertelenmiş kanal kullanın.

 Merhaba istemci uygulaması veya kullandığınız aracı bağlı olarak, kimlik doğrulama ve oturum nasıl hello türü farklı olabilir. Her uygulama, Azure Analysis Services gibi toocloud hizmetlerine bağlanmak için farklı özellikleri destekleyebilir.


### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Azure Analysis Services sunucuları desteği bağlantılarından [SSMS V17.1](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) ve Windows kimlik doğrulaması, Active Directory parola kimlik doğrulaması ve Active Directory Evrensel kimlik doğrulaması kullanarak daha yüksek. Genel olarak, çünkü Active Directory Evrensel kimlik doğrulaması kullanmanız önerilir:

*  Etkileşimli ve etkileşimli olmayan kimlik doğrulama yöntemini destekler.

*  Azure B2B Konuk kullanıcılar Hello Azure AS Kiracı davet destekler. Tooa sunucusu bağlanırken Konuk kullanıcılar Active Directory Evrensel kimlik doğrulaması toohello sunucusu bağlanırken seçmeniz gerekir.

*  Çok faktörlü kimlik doğrulamasını (MFA) destekler. Azure MFA koruma erişim toodata ve doğrulama seçeneklerini çeşitli uygulamalarla yardımcı olur: telefon araması, SMS mesajı, akıllı kartlar ve PIN ya da mobil uygulama bildirimi. Azure AD ile etkileşimli MFA doğrulama için bir açılır iletişim kutusu neden olabilir.

### <a name="sql-server-data-tools-ssdt"></a>SQL Server Veri Araçları (SSDT)
SSDT tooAzure Analysis Services MFA desteği ile Active Directory Evrensel kimlik doğrulaması kullanarak bağlanır. İstendiğinde toosign tooAzure hello ilk dağıtımda, kendi kuruluş kimliği (e-posta) kullanarak kullanıcılardır. Kullanıcıların tooAzure için dağıtma hello sunucuda Sunucu Yöneticisi izinlerine sahip bir hesapla oturum açmanız gerekir. TooAzure hello ilk kez açarken bir belirteç atanır. SSDT hello belirteci bellek içi gelecekteki yeniden bağlantılar için önbelleğe alır.

### <a name="power-bi-desktop"></a>Power BI Desktop
Power BI Desktop tooAzure Analysis Services MFA desteği ile Active Directory Evrensel kimlik doğrulaması kullanarak bağlanır. İstendiğinde toosign tooAzure hello ilk bağlantıda, bunların Kuruluş Kimliği (e-posta) kullanarak kullanıcılardır. Kullanıcıların tooAzure bir sunucu yöneticisi veya veritabanı rolü dahil bir hesapla oturum açmanız gerekir.

### <a name="excel"></a>Excel
Excel kullanıcılar, bir Windows hesabı, bir kuruluş kimliği (e-posta adresi) veya bir dış e-posta adresi kullanarak tooa sunucusuna bağlanabilir. Dış e-posta kimlikleri hello Azure AD Konuk kullanıcı olarak mevcut olmalıdır.

## <a name="user-permissions"></a>Kullanıcı izinleri

**Sunucu yöneticileri** belirli tooan Azure Analysis Services sunucu örneği olan. Azure portalı, SSMS ve SSDT gibi araçlarla veritabanları ekleme ve kullanıcı rollerini yönetme gibi görevleri tooperform bağlandıklarında. Varsayılan olarak, hello sunucusu oluşturur hello kullanıcı Analysis Services sunucu yönetici olarak otomatik olarak eklenir. Diğer yöneticiler, Azure portal veya SSMS kullanarak eklenebilir. Sunucu yöneticileri hello hello Azure AD kiracısında içinde bir hesap olmalıdır aynı abonelik. toolearn daha, fazla [sunucu yöneticileri yönetmek](analysis-services-server-admins.md). 


**Veritabanı kullanıcıları** toomodel veritabanları Excel veya Power BI gibi istemci uygulamalarını kullanarak bağlanır. Kullanıcıların toodatabase rolleri eklenmesi gerekir. Veritabanı rolleri, yönetici, işlem ya da bir veritabanı için Okuma izinleri tanımlar. Yönetici izinlerine sahip bir roldeki toounderstand veritabanı kullanıcılar sunucu yöneticileri farklı önemlidir. Ancak, varsayılan olarak, sunucu yöneticilerinin Veritabanı yöneticileri aynı zamanda değildir. toolearn daha, fazla [veritabanı rolleri ve kullanıcıları yönetme](analysis-services-database-users.md).

**Azure kaynak sahiplerine**. Kaynak sahiplerine bir Azure aboneliğine yönelik kaynakları yönetin. Kaynak sahiplerine ekleyebilirsiniz Azure AD kullanıcı kimlikleri tooOwner veya katkıda bulunan rolü bir abonelik kullanarak **erişim denetimi** Azure portalında veya Azure Resource Manager şablonları ile. 

![Azure portalında erişim denetimi](./media/analysis-services-manage-users/aas-manage-users-rbac.png)

Bu düzeyde rolleri toousers veya hello portalında veya Azure Resource Manager şablonları kullanarak tamamlanabilir tooperform görevleri gereken hesapları uygulayın. toolearn daha, fazla [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md). 


## <a name="database-roles"></a>Veritabanı rolleri

 Tablo modeli için tanımlanan veritabanı rolleri rolleridir. Diğer bir deyişle, Azure AD kullanıcılarının oluşan üyeleri hello rolleri içerir ve bu üyeler hello eylemi tanımlamak özel izinleri olan güvenlik grupları bir model veritabanı üzerinde alabilir. Bir veritabanı rolü hello veritabanında ayrı bir nesne olarak oluşturulur ve bu rol oluşturulduğu yalnızca toohello veritabanı uygular.   
  
 Yeni bir tablo modeli projesi oluşturduğunuzda varsayılan olarak, herhangi bir rol hello modeli projesi yok. SSDT hello Rol Yöneticisi iletişim kutusunu kullanarak rolleri tanımlanabilir. Rolleri modeli proje tasarım sırasında tanımlandığında, uygulanan yalnızca toohello model çalışma alanı veritabanı oldukları. Merhaba modeli dağıtıldığında hello aynı dağıtılan uygulanan toohello modeli rolleridir. Bir model dağıtıldıktan sonra rolleri ve üyeleri, sunucu ve Veritabanı yöneticileri SSMS kullanarak yönetebilirsiniz. toolearn daha, fazla [veritabanı rolleri ve kullanıcıları yönetme](analysis-services-database-users.md).
  


## <a name="next-steps"></a>Sonraki adımlar

[Azure Active Directory grupları ile erişim tooresources yönetme](../active-directory/active-directory-manage-groups.md)   
[Veritabanı rolleri ve kullanıcıları yönetme](analysis-services-database-users.md)  
[Sunucu yöneticilerini yönetme](analysis-services-server-admins.md)  
[Rol Tabanlı Access Control](../active-directory/role-based-access-control-what-is.md)  
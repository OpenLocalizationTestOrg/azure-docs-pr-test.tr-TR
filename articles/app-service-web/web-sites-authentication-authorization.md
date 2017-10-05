---
title: "Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması | Microsoft Docs"
description: "Şirket içi Active Directory ile kimlik doğrulaması için Azure App Service'te satır iş kolu uygulamaları için farklı seçenekler hakkında bilgi edinin"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: dde6b7e6-bf6a-4fa5-8390-3a18155d21bd
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: a68bcd7040498515a6e35a87ee6e6940a84506d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması
Bu makalede, şirket içi Active Directory (AD) içinde kimlik doğrulaması yapmayı gösterir [Azure App Service](../app-service/app-service-value-prop-what-is.md). Azure uygulama bulutta barındırılan, ancak kimlik doğrulaması yöntemlerini AD kullanıcıları güvenli bir şekilde şirket içi vardır. 

## <a name="authenticate-through-azure-active-directory"></a>Azure Active Directory aracılığıyla kimlik doğrulaması
Azure Active Directory kiracısı directory ile eşitlenen bir şirket içi AD. Bu yaklaşım, uygulamanızın internet'ten erişmek ve şirket içi kimlik bilgilerini kullanarak kimlik doğrulaması AD kullanıcıları sağlar. Ayrıca, Azure uygulama hizmeti sağlayan bir [bu yöntem için anahtar teslim çözümü](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Bir düğme birkaç tıklatmayla Azure uygulamanız için bir dizin eşitlenen Kiracı kimlik doğrulamasını etkinleştirebilirsiniz. Bu yaklaşım, aşağıdaki avantajlara sahiptir:

* Tüm kimlik doğrulama kodu, uygulamanızda gerektirmez. Uygulama kimlik doğrulaması yapmak ve uygulamanızda işlevselliği sağlayan zamanınızı hizmeti sağlar.
* [Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) erişimi etkinleştirir dizin verilerini Azure uygulamanızdan.
* SSO için sağlar [Azure Active Directory tarafından desteklenen tüm uygulamalar](/marketplace/active-directory/)Office 365, Dynamics CRM Online, Microsoft Intune ve Microsoft olmayan bulut uygulamaları binlerce dahil olmak üzere. 
* Azure Active Directory, rol tabanlı erişim denetimini destekler. [Authorize(Roles="X")] düzeni en az değişikliklerle kodunuzu kullanabilirsiniz.

Azure Active Directory ile kimlik doğrulaması iş Azure uygulaması yazma hakkında bilgi için bkz: [Azure Active Directory kimlik doğrulaması ile bir iş Azure uygulaması oluşturma](web-sites-dotnet-lob-application-azure-ad.md).

## <a name="authenticate-through-an-on-premises-sts"></a>Bir şirket içi STS ile kimlik doğrulaması
Bir şirket içi güvenli belirteç hizmeti (STS) gibi Active Directory Federasyon Hizmetleri (AD FS) varsa, Azure uygulamanız için kimlik doğrulamasını birleştirmeyi için kullanabilirsiniz. Azure'da depolanan şirket ilkesi AD veri yasaklar olduğunda bu en iyi bir yaklaşımdır. Ancak, aşağıdakilere dikkat edin:

* STS topoloji dağıtılan ile şirket içi, maliyet ve yönetim yükünü olması gerekir.
* Yalnızca AD FS Yöneticiler yapılandırabilir [bağlı olan taraf güvenlerini ve talep kuralları](http://technet.microsoft.com/library/dd807108.aspx), geliştirici seçenekleri sınırlayabilir. Diğer taraftan, yönetmek ve özelleştirmek olası [talep](http://technet.microsoft.com/library/ee913571.aspx) uygulama başına temelinde.
* Erişim şirket içi AD veri Kurumsal güvenlik duvarı üzerinden ayrı bir çözüm gerektirir.

Bir şirket içi STS ile kimlik doğrulaması iş Azure uygulaması yazma hakkında bilgi için bkz: [AD FS kimlik doğrulaması ile bir iş Azure uygulaması oluşturma](web-sites-dotnet-lob-application-adfs.md).


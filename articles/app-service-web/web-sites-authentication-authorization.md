---
title: "Azure uygulamanızı şirket içi Active Directory ile aaaAuthenticate | Microsoft Docs"
description: "Şirket içi Active Directory ile Azure App Service tooauthenticate satır iş kolu uygulamaları için hello farklı seçenekler hakkında bilgi edinin"
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
ms.openlocfilehash: 65bf25aaa0447fbbea7c754db55842d57e70757e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması
Bu makale size nasıl tooauthenticate ile Active Directory (AD) şirket içi gösterir [Azure App Service](../app-service/app-service-value-prop-what-is.md). Azure uygulama hello bulutta barındırılan ancak yolları tooauthenticate AD kullanıcıları güvenli bir şekilde şirket içi vardır. 

## <a name="authenticate-through-azure-active-directory"></a>Azure Active Directory aracılığıyla kimlik doğrulaması
Azure Active Directory kiracısı directory ile eşitlenen bir şirket içi AD. Bu yaklaşım, uygulamanızdan AD erişmelerini Internet hello ve şirket içi kimlik bilgilerini kullanarak kimlik doğrulaması. Ayrıca, Azure uygulama hizmeti sağlayan bir [bu yöntem için anahtar teslim çözümü](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Bir düğme birkaç tıklatmayla Azure uygulamanız için bir dizin eşitlenen Kiracı kimlik doğrulamasını etkinleştirebilirsiniz. Bu yaklaşımın avantajları aşağıdaki hello vardır:

* Tüm kimlik doğrulama kodu, uygulamanızda gerektirmez. Kimlik doğrulaması hello ve uygulamanızda işlevselliği sağlayan zamanınızı uygulama hizmeti olanak tanır.
* [Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) etkinleştirir Azure uygulamanızdan toodirectory verilere erişebilir.
* SSO çok sağlar[Azure Active Directory tarafından desteklenen tüm uygulamalar](/marketplace/active-directory/)Office 365, Dynamics CRM Online, Microsoft Intune ve Microsoft olmayan bulut uygulamaları binlerce dahil olmak üzere. 
* Azure Active Directory, rol tabanlı erişim denetimini destekler. Küçük değişiklikler tooyour koduyla hello [Authorize(Roles="X")] desen kullanabilirsiniz.

toowrite Azure Active Directory ile kimlik doğrulaması iş Azure uygulaması nasıl görürüm toosee [Azure Active Directory kimlik doğrulaması ile bir iş Azure uygulaması oluşturma](web-sites-dotnet-lob-application-azure-ad.md).

## <a name="authenticate-through-an-on-premises-sts"></a>Bir şirket içi STS ile kimlik doğrulaması
Bir şirket içi güvenli belirteç hizmeti (STS) gibi Active Directory Federasyon Hizmetleri (AD FS) varsa, o toofederate kimlik doğrulaması Azure uygulamanız için kullanabilirsiniz. Azure'da depolanan şirket ilkesi AD veri yasaklar olduğunda bu en iyi bir yaklaşımdır. Ancak, hello aşağıdakilere dikkat edin:

* STS topoloji dağıtılan ile şirket içi, maliyet ve yönetim yükünü olması gerekir.
* Yalnızca AD FS Yöneticiler yapılandırabilir [bağlı olan taraf güvenlerini ve talep kuralları](http://technet.microsoft.com/library/dd807108.aspx), hello Geliştirici seçenekleri sınırlayabilir. Merhaba üzerindeki diğer yandan, bu olası toomanage ve özelleştirme [talep](http://technet.microsoft.com/library/ee913571.aspx) uygulama başına temelinde.
* Erişim tooon içi AD veri hello Kurumsal güvenlik duvarı üzerinden ayrı bir çözüm gerektirir.

toowrite bir şirket içi STS ile kimlik doğrulaması iş Azure uygulaması nasıl görürüm toosee [AD FS kimlik doğrulaması ile bir iş Azure uygulaması oluşturma](web-sites-dotnet-lob-application-adfs.md).


---
title: "aaaSecuring PaaS web ve mobil uygulamaları Azure App Services kullanarak | Microsoft Docs"
description: " PaaS web ve mobil uygulamaların güvenliğini sağlamaya yönelik en iyi güvenlik uygulamaları Azure uygulama hizmetleri hakkında bilgi edinin. "
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
ms.openlocfilehash: 68a741c668efe2157cff114b649e0e287ef196f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-services"></a>PaaS web ve mobil uygulamaları Azure App Services kullanarak güvenli hale getirme

Bu makalede, bir koleksiyonu aşağıdakiler ele [Azure App Services](https://azure.microsoft.com/services/app-service/) PaaS web ve mobil uygulamaların güvenliğini sağlamaya yönelik en iyi güvenlik uygulamaları. Bu en iyi uygulamaları Azure ile deneyimi bizim türetilmiş ve müşterilerin hello deneyimleri bulunun.

## <a name="azure-app-services"></a>Azure Uygulama Hizmetleri
[Azure App Services](../app-service/app-service-value-prop-what-is.md) olduğu web ve tüm platform veya cihazlar için mobil uygulamalar oluşturmanızı ve herhangi bir yere, toodata hello Bulut veya şirket içi bağlantı sağlar bir PaaS teklifi. Uygulama Hizmetleri hello web ve daha önce ayrı olarak Azure Web siteleri ve Azure Mobile Services teslim mobil özelliklerini içerir. Ayrıca iş süreçlerini otomatikleştirmek ve bulut API'leri barındırmak için yeni özellikler içerir. Tek bir tümleşik hizmet olarak uygulama hizmetleri tooweb, mobil ve tümleştirme senaryoları zengin bir özellikler kümesi getirir.

toolearn daha gördüğünüz genel bakışlar [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) ve [Web Apps](../app-service-web/app-service-web-overview.md).

## <a name="best-practices"></a>En iyi uygulamalar

Uygulama hizmetleri kullanırken, bu en iyi uygulamaları izleyin:

- [Azure Active Directory (AD) aracılığıyla kimlik doğrulaması](../app-service-web/web-sites-authentication-authorization.md#authenticate-through-azure-active-directory). Uygulama Hizmetleri, kimlik sağlayıcısı için OAuth 2.0 hizmeti sağlar. OAuth 2.0 istemci Geliştirici Basitlik, Web uygulamaları, Masaüstü uygulamaları ve cep telefonları için özel yetkilendirme akışları sağlarken odaklanır. Azure AD OAuth 2.0 tooenable kullanır, tooauthorize toomobile ve web uygulamalarına erişim.
- Merhaba gerek tooknow ve en az ayrıcalık güvenlik ilkelerine göre erişimi kısıtlayın. Erişimi kısıtlamak, veri erişimi için tooenforce güvenlik ilkeleri istediğiniz kuruluşlar için zorunludur. Rol tabanlı erişim denetimi (RBAC) kullanılan tooassign izinleri toousers, gruplar ve uygulamalar belirli bir kapsamda olabilir. kullanıcıların erişim tooapplications, verme hakkında daha fazla toolearn bkz [access management ile çalışmaya başlama](../active-directory/role-based-access-control-what-is.md).
- Anahtarlarınızı koruyun. Güvenlik ne kadar iyi olduğu önemli değildir, abonelik anahtarlarınızı kaybetmeniz durumunda. Azure Anahtar Kasası, bulut uygulamaları ve hizmetleri tarafından kullanılan şifreleme anahtarlarının ve gizli anahtarların korunmasına yardımcı olur. Anahtar Kasası'nı kullanarak anahtarları ve gizli anahtarları (kimlik doğrulaması anahtarları, depolama hesabı anahtarları, veri şifreleme anahtarları, .PFX dosyaları ve parolalar gibi), donanım güvenlik modülleri tarafından korunan anahtarları kullanarak şifreleyebilirsiniz. Ek güvenlik için HSM'lerde anahtarları içeri aktarabilir veya oluşturabilirsiniz. Bkz: [Azure anahtar kasası](../key-vault/key-vault-whatis.md) toolearn daha fazla. Anahtar kasası toomanage TLS sertifikalarınızı otomatik yenileme ile de kullanabilirsiniz.
- Gelen kaynak IP adreslerini kısıtlayın. [Uygulama Hizmetleri ortamı](../app-service-web/app-service-app-service-environment-intro.md) ağ güvenlik grupları (Nsg'ler) üzerinden gelen kaynak IP adresleri kısıtlamanıza yardımcı olan bir sanal ağ tümleştirme özelliği vardır. Azure sanal ağlar (Vnet'ler) ile bilginiz yoksa, tooplace birçok Azure kaynaklarınızı denetim Internet olmayan, yönlendirilebilir bir ağ erişimi sağlayan bir özellik budur. toolearn daha, fazla [uygulamanız bir Azure sanal ağı ile tümleştirmek](../app-service-web/web-sites-integrate-with-vnet.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede PaaS web ve mobil uygulamaların güvenliğini sağlamaya yönelik uygulama hizmetleri en iyi güvenlik uygulamaları tooa koleksiyonu kullanıma sunuldu. PaaS dağıtımlarınızın güvenliğini sağlama hakkında daha fazla toolearn bakın:

- [PaaS dağıtımlarının güvenliğini sağlama](security-paas-deployments.md)
- [PaaS web ve mobil uygulamaları Azure SQL Database ve SQL Data Warehouse kullanarak güvenli hale getirme](security-paas-applications-using-sql.md)

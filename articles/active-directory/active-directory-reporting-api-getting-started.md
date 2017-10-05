---
title: "Azure AD Azure AD Klasik portalında raporlama API'si ile çalışmaya başlama | Microsoft Docs"
description: "Azure Active raporlama API'si ile dizinde nereden başlayacaksınız"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a>Azure Active Directory'ı Azure AD Klasik portalında raporlama API'si ile çalışmaya başlama
*Bu konuda yer [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).*

Azure Active Directory ile çok çeşitli raporlar sağlar. Bu raporların verileri SIEM sistemleri, denetim ve iş zekası araçları gibi uygulamalarınız için çok yararlı olabilir. Azure AD raporlama API'leri, bir dizi REST tabanlı API aracılığıyla verilere programlı erişim sağlar. Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.

Bu makalede, Azure AD ile çalışmaya başlamak gereken bilgilerle API'leri raporlama sağlar.
Sonraki bölümde, Denetim kullanma hakkında daha fazla ayrıntı ve API oturum açın. Diğer tüm API'leri için bkz: [Azure AD raporları ve events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) makalesi.

Sorularınız, sorunları veya Geri bildiriminiz için lütfen başvurun [raporlama AAD Yardım](mailto:aadreportinghelp@microsoft.com).

## <a name="learning-map"></a>Öğrenme haritası
1. **Hazırlama** -API örneklerinizi test etmeden önce tamamlamanız gereken [Azure AD raporlama API'si erişmek için Önkoşullar](active-directory-reporting-api-prerequisites.md).
2. **Araştır** -raporlama API'leri bir ilk izlenim alın:
   
   * [Denetim API'si örnekleri kullanma](active-directory-reporting-api-audit-samples.md) 
   * [Oturum açma etkinliği raporu API örnekleri kullanma](active-directory-reporting-api-sign-in-activity-samples.md)
3. **Özelleştirme** -kendi çözümü oluşturun: 
   
   * [API Başvurusu denetim kullanma](active-directory-reporting-api-audit-reference.md) 
   * [Oturum açma etkinliği raporu API başvurusunu kullanma](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a>Sonraki Adımlar
Tüm mevcut Azure AD Graph API uç noktaları giderek görmek merak ediyorsanız [https://graph.windows.net/tenant-name/reports/$ metadata? api-version beta =](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).


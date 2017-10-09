---
title: "hello Azure AD Klasik portalında hello Azure AD raporlama API'si ile çalışmaya aaaGetting | Microsoft Docs"
description: "Nasıl kullanmaya tooget hello Azure Active Directory raporlama API'si"
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
ms.openlocfilehash: 52e22d442650731fc6ed28991fc65f9182af0540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api-on-hello-azure-ad-classic-portal"></a>Hello Azure Active Directory hello Azure AD Klasik portalında raporlama API'si ile çalışmaya başlama
*Bu konu hello parçasıdır [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).*

Azure Active Directory ile çok çeşitli raporlar sağlar. Bu raporların Hello veriler SIEM sistemleri, Denetim ve iş zekası araçları gibi çok kullanışlı tooyour uygulamalar olabilir. bir dizi REST tabanlı API'ler aracılığıyla programlı erişim toohello veri API'leri sağlamak Hello Azure AD raporlama. Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.

Bu makale hello Azure AD Raporlama ile çalışmaya tooget ihtiyacınız hello bilgilerle sağlar API'leri.
Merhaba sonraki bölümde hello kullanma hakkında daha fazla ayrıntı denetim ve oturum API bileşenini bulun. Diğer tüm API'leri için hello bkz [Azure AD raporları ve events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) makalesi.

Sorularınız, sorunları veya Geri bildiriminiz için lütfen başvurun [raporlama AAD Yardım](mailto:aadreportinghelp@microsoft.com).

## <a name="learning-map"></a>Öğrenme haritası
1. **Hazırlama** -API örneklerinizi test etmeden önce toocomplete hello gereksinim [Önkoşullar tooaccess hello Azure AD raporlama API'si](active-directory-reporting-api-prerequisites.md).
2. **Araştır** -API'leri raporlama hello bir ilk izlenim alın:
   
   * [Merhaba örnekleri hello denetim API kullanma](active-directory-reporting-api-audit-samples.md) 
   * [Hello örnekleri için hello oturum açma etkinliği raporu API kullanma](active-directory-reporting-api-sign-in-activity-samples.md)
3. **Özelleştirme** -kendi çözümü oluşturun: 
   
   * [Merhaba denetim API başvurusunu kullanma](active-directory-reporting-api-audit-reference.md) 
   * [Merhaba oturum açma etkinliği raporu kullanarak API Başvurusu](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a>Sonraki Adımlar
Merak toosee varsa tüm mevcut Azure AD Graph API uç noktaları çok giderek hello[https://graph.windows.net/tenant-name/reports/$ metadata? api-version beta =](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).


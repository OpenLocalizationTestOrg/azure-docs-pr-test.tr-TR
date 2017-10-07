---
title: "aaaPrivileged Kimlik Yönetimi abonelikleri - Azure | Microsoft Docs"
description: "Merhaba abonelik ve lisans yönetimi ve Azure AD Privileged Identity Management kiracınızda kullanma gereksinimleri açıklanır"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 2639d13c250a582fdcf0b277c9bab37fdfcabcb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a>Azure Active Directory Privileged Identity Management abonelik gereksinimleri

Azure AD Privileged Identity Management kullanılabilir Azure AD Premium P2 hello sürümünün bir parçası olarak. Merhaba hakkında daha fazla bilgi için bkz: diğer özellikleri P2 ve nasıl tooPremium P1, karşılaştırır [Azure Active Directory sürümleri](../active-directory-editions.md).

>[!NOTE]
Azure Active Directory (Azure AD) Privileged Identity Management önizlemede olduğunda, bir kiracı tootry hello service için herhangi bir lisans denetim vardı.  Azure AD Privileged Identity Management genel kullanılabilirlik ulaştı, bir deneme aboneliği veya Ücretli abonelik aralık 2016 sonrasında ayrıcalıklı Kimlik Yönetimi'ni kullanarak hello Kiracı toocontinue için mevcut olması gerekir.
  

## <a name="confirm-your-trial-or-paid-subscription"></a>Deneme aboneliği veya Ücretli aboneliğinizi onaylayın

Abonelik satın veya kuruluşunuzun bir deneme sürümü olup emin değilseniz, olup olmadığını kiracınızda bir abonelik Azure Active Directory modülü için Windows PowerShell V1 dahil hello komutlarını kullanarak kontrol edebilirsiniz. 
1. Bir PowerShell penceresi açın.
2. Girin `Connect-MsolService` tooauthenticate kiracınızda bir kullanıcı olarak.
3. Girin `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.

Bu komut kiracınızda hello Aboneliklerin listesini alır. Varsa bir Azure AD Premium P2 tooobtain deneme gerekir hiçbir satır döndürdü, bir Azure AD Premium P2 abonelik ya da EMS E5 abonelik toouse Azure AD Privileged Identity Management satın alın.  tooget bir deneme ve Azure AD Privileged Identity Management kullanarak başlangıç okuma [Azure AD Privileged Identity Management ile çalışmaya başlama](../active-directory-privileged-identity-management-getting-started.md).

Bu komut bir satır döndürürse hangi SkuPartNumber "AAD_PREMIUM_P2" veya "EMSPREMIUM" ve IsTrial "True" ise, bu Azure AD Premium P2 deneme hello Kiracı içinde mevcut olduğunu gösterir.  Ardından Hello abonelik durumunu etkin değil ve bir Azure AD Premium P2 ya da EMS E5 abonelik satın alma sahip değil, bir Azure AD Premium P2 aboneliği veya Azure AD Privileged Identity Management kullanarak EMS E5 abonelik toocontinue satın almalısınız.

Azure AD Premium P2 aracılığıyla kullanılabilen bir [Microsoft Enterprise sözleşmesi](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), hello [açık toplu lisans programı](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx)ve hello [bulut çözüm sağlayıcıları program](https://partner.microsoft.com/en-US/cloud-solution-provider). Azure ve Office 365 aboneleri de Azure AD Premium P2 çevrimiçi satın alabilirsiniz.  Azure AD Premium fiyatlandırma ve çevrimiçi tooorder nasıl bulunabilir hakkında daha fazla bilgi [Azure Active Directory fiyatlandırma](https://azure.microsoft.com/en-us/pricing/details/active-directory/).

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a>Azure AD Privileged Identity Management kiracısında kullanılamıyor

Azure AD Privileged Identity Management artık kullanılabilir kiracınızda varsa:
- Önizlemede olan ve Azure AD Premium P2 abonelik ya da EMS E5 abonelik satın değil, kuruluşunuz Azure AD Privileged Identity Management kullanıyordu.
- Kuruluşunuz Azure AD Premium P2 ya da EMS süresi dolan E5 deneme vardı.
- Kuruluşunuz süresi satın alınan bir abonelik vardı.

Bir Azure AD Premium P2 abonelik ya da EMS E5 abonelik süresi dolduğunda veya bir Azure AD Privileged Identity Management önizlemede kullanarak kuruluş Azure AD Premium P2 ya da EMS E5 aboneliği edinmek değil:

- Kalıcı rol atamalarını tooAzure AD roller etkilenmeyecek.
- Merhaba hello Azure portal, Azure AD Privileged Identity Management uzantısında yanı sıra hello grafik API'si cmdlet'leri ve Azure AD Privileged Identity Management PowerShell arabirimleri artık tooactivate ayrıcalıklı rolleri kullanıcılar için kullanılabilir, yönetme ayrıcalıklı erişim ya da ayrıcalıklı rolleri erişim incelenmesi gerçekleştirin.
- Kullanıcılar artık mümkün tooactivate ayrıcalıklı rolleri olarak Azure AD rollerin uygun rol atamaları kaldırılır.
- Tüm Azure AD rolleri devam eden erişim incelenmesi sona erer ve Azure AD Privileged Identity Management yapılandırma ayarları kaldırılır.
- Azure AD Privileged Identity Management, artık rol atama değişiklikleri e-posta gönderir.

## <a name="next-steps"></a>Sonraki adımlar

- [Azure AD Privileged Identity Management ile çalışmaya başlama](../active-directory-privileged-identity-management-getting-started.md)
- [Azure AD Privileged Identity Management rollerinde](../active-directory-privileged-identity-management-roles.md)

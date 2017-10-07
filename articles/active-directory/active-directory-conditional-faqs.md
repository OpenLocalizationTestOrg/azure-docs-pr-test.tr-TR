---
title: "aaaAzure Active Directory koşullu erişim ile ilgili SSS | Microsoft Docs"
description: "Azure Active Directory'de koşullu erişim hakkında sorular yanıtlar toofrequently alın."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a>Azure Active Directory koşullu erişim ile ilgili SSS

## <a name="which-applications-work-with-conditional-access-policies"></a>Hangi uygulamaların koşullu erişim ilkeleriyle birlikte çalışır?

Koşullu erişim ilkeleriyle birlikte çalışan uygulamalar hakkında daha fazla bilgi için bkz: [uygulamalar ve Azure Active Directory'de koşullu erişim kuralları kullanma tarayıcılar](active-directory-conditional-access-supported-apps.md).

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a>Koşullu erişim ilkeleri, B2B işbirliğinin ve Konuk kullanıcılar için uygulanır?

İlkeleri işletmeden işletmeye (B2B) işbirliği kullanıcılar için uygulanır. Ancak, bazı durumlarda, bir kullanıcı mümkün toosatisfy hello ilkesi gereksinimlerini olmayabilir. Örneğin, bir Konuk kullanıcı kuruluşunun çok faktörlü kimlik doğrulamasını desteklemiyor olabilir. 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a>SharePoint Online İlkesi de tooOneDrive iş için uygulanacak?

Evet. SharePoint Online İlkesi tooOneDrive işletmeler için de geçerlidir.


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a>Neden t istemci uygulamaları, Word veya Outlook gibi bir ilke ayarlanamaz?

Bir koşullu erişim ilkesi, bir hizmete erişim gereksinimleri ayarlar. Kimlik doğrulama toothat hizmeti oluştuğunda zorlanır. Hello İlkesi doğrudan bir istemci uygulaması ayarlanmadı. Bunun yerine, bir istemci bir hizmet çağırdığında uygulanır. Örneğin, SharePoint üzerinde ayarlanmış bir ilkeyle SharePoint çağırma tooclients geçerlidir. Bir ilke Exchange'de kümesi tooOutlook geçerlidir.

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a>Bir koşullu erişim ilkesi tooservice hesapları uygulanacak?

Koşullu erişim ilkeleri, tooall kullanıcı hesapları uygulanır. Bu, hizmet hesapları olarak kullanılan kullanıcı hesaplarını içerir. Genellikle, katılımsız çalışan bir hizmet hesabı hello gereksinimleri koşullu erişim ilkesinin gerçekleştiremiyor. Örneğin, çok faktörlü kimlik doğrulaması gerekli olabilir. Hizmet hesapları, koşullu erişim ilkesi yönetimi ayarları kullanarak bir ilkeden tutulabilir. 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a>Graph API koşullu erişim ilkelerini yapılandırma için kullanılabilir mi?

Şu anda yok. 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a>Desteklenmeyen cihaz platformları için hello varsayılan dışlama İlkesi nedir?

Şu anda, koşullu erişim ilkeleri seçmeli olarak iOS ve Android cihazlarının kullanıcıları uygulanır. Uygulamalar diğer cihaz platformları üzerinde varsayılan olarak, iOS ve Android cihazlar için hello koşullu erişim ilkesi tarafından etkilenmez. Bir kiracı Yöneticisi toooverride hello genel ilke toodisallow erişim toousers desteklenmeyen platformlarda seçebilirsiniz.


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a>Koşullu erişim ilkeleri Microsoft Teams nasıl çalışır?  

Microsoft Teams yoğun olarak Exchange Online ve SharePoint Online toplantılar, takvimler ve dosya paylaşımı gibi temel üretkenlik senaryolar için dayanır. Bir kullanıcı oturum açtığında bu bulut uygulamaları için ayarlanan koşullu erişim ilkeleri tooMicrosoft takımlar uygulayın.

Microsoft Teams de Azure Active Directory koşullu erişim ilkeleri, bir bulut uygulamasında olarak ayrı olarak desteklenir. Bir kullanıcı oturum açtığında bir bulut uygulaması için ayarlanan sertifika yetkilisi ilkeleri tooMicrosoft takımlar uygulayın.

Windows ve Mac için Microsoft Teams Masaüstü istemcileri modern kimlik doğrulamasını destekler. Modern kimlik doğrulaması oturum platformlarında hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office istemci uygulamalarını temel açma getirir. 

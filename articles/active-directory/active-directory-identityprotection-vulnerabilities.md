---
title: "Azure Active Directory kimlik koruması tarafından algılanan aaaVulnerabilities | Microsoft Docs"
description: "Azure Active Directory kimlik koruması tarafından algılanan hello güvenlik açıkları genel bakış."
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Azure Active Directory kimlik koruması tarafından algılanan güvenlik açığı
Güvenlik açıkları zayıf bir saldırgan tarafından yararlanılabilir ortamınızda giderilmiştir. Bu güvenlik açıkları tooimprove hello güvenlik yaklaşımı, kuruluşunuzun adres ve bunları yararlanmasını saldırganların önlemeye öneririz.


![Güvenlik Açıkları](./media/active-directory-identityprotection-vulnerabilities/101.png "güvenlik açıkları")



Merhaba aşağıdaki bölümlerde kimlik koruması tarafından bildirilen hello güvenlik açıkları genel bir bakış sağlar.

## <a name="multi-factor-authentication-registration-not-configured"></a>Çok faktörlü kimlik doğrulaması kayıt yapılandırılmadı
Bu güvenlik açığından yardımcı olacak denetim kuruluşunuzda Azure çok faktörlü kimlik doğrulamasının hello dağıtımı. 

Azure çok faktörlü kimlik doğrulaması güvenlik toouser kimlik doğrulamasının ikinci bir katmanı sağlar. Bu koruma erişim toodata ve uygulamaları basit bir oturum açma işlemi için kullanıcı talebine buluştururken yardımcı olur. Kolay doğrulama seçeneklerini çeşitli aracılığıyla güçlü kimlik doğrulaması sunar — telefon araması, SMS mesajı veya mobil uygulama bildirimi veya doğrulama kodu ve 3. taraf OATH belirteçleri.

Azure multi-Factor Authentication kullanıcı oturum açma işlemleri için gerekli öneririz. Çok faktörlü kimlik doğrulaması risk bağlı olarak koşullu erişim ilkelerindeki kimlik koruması kullanılabilir önemli bir rol oynar.

Daha fazla ayrıntı için bkz: [Azure multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="unmanaged-cloud-apps"></a>Yönetilmeyen bulut uygulamaları
Bu güvenlik açığından kuruluşunuzdaki yönetilmeyen bulut uygulamaları tanımlamasına yardımcı olur.

Modern kuruluşlarda, BT departmanları genellikle kullanıcılar kuruluşlarındaki işlerine toodo kullanmakta olduğunuz tüm hello bulut uygulamaları farkında değildir. Yöneticiler yetkisiz erişim toocorporate verileri, olası veri sıkıntılarına ve diğer güvenlik risklerine endişeniz neden olurdu kolay toosee olur. 

Kuruluşunuz Azure Active Directory'yi kullanarak bu uygulamaları Cloud App Discovery toodiscover yönetilmeyen bulut uygulamaları ve toomanage dağıtmanızı öneririz.

Daha fazla ayrıntı için bkz: [Cloud App Discovery ile yönetilmeyen bulut uygulamaları bulma](active-directory-cloudappdiscovery-whatis.md).

## <a name="security-alerts-from-privileged-identity-management"></a>Privileged Identity Management güvenlik uyarıları
Bu güvenlik açığından bulmak ve uyarılar, kuruluşunuzda ayrıcalıklı kimlikleri hakkında çözümlemenize yardımcı olur.  

tooenable kullanıcılar toocarry genişletme ayrıcalıklı işlemleri kuruluşların gerekir geçici veya kalıcı ayrıcalıklı erişim Azure AD'de toogrant kullanıcılar Azure veya Office 365 kaynakları veya diğer SaaS uygulamaları. Bunların her biri, kullanıcıların artar hello saldırı yüzeyini, kuruluşunuzun ayrıcalıklı. Bu güvenlik açığından gereksiz ayrıcalıklı erişimi kullanıcıları tanımlamak ve tooreduce uygun eylemi gerçekleştirin ve bunlar teşkil hello riski ortadan kaldırmanıza yardımcı olur. 

Kuruluşunuzun Azure AD Privileged Identity Management toomanage, Denetim ve ayrıcalıklı izleme kimlikleri ve bunların erişim tooresources Azure AD'de yanı sıra Office 365 veya Microsoft Intune gibi diğer Microsoft online services kullandığı öneririz.

Daha fazla ayrıntı için bkz: [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Active Directory kimlik koruması](active-directory-identityprotection.md)


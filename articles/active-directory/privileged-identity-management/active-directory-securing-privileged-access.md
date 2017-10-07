---
title: "Azure AD'de ayrıcalıklı erişim aaaSecuring | Microsoft Docs"
description: "Azure, Azure Active Directory ve Microsoft Online Services ayrıcalıklı erişim güvenliğini sağlamak için hello açıklayan bir konu yaklaşıyor."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a>Azure AD'de ayrıcalıklı erişimi güvenli hale getirme
Ayrıcalıklı güvenliğini sağlama erişim önemli bir ilk adım, toohelp korumak modern bir kuruluştaki iş varlıklar. Ayrıcalıklı hesapları yönetmek ve BT sistemleri yöneten hesaplarıdır. Bu hesapları toogain erişim tooan kuruluşunuzun veri ve sistemler siber saldırganların hedefleyin. toosecure ayrıcalıklı erişimi, hello hesapları yalıtarak ve tooa kötü amaçlı kullanıcı olma hello risk sistemlerden gösteriliyor.

Daha fazla kullanıcı tooget ayrıcalıklı erişim bulut Hizmetleri ile başlıyor. Bu, Office365, genel Yöneticiler, Azure aboneliği yöneticileri ve VM'ler veya SaaS uygulamalarını yönetimsel erişime sahip kullanıcılar içerebilir.

Microsoft önerir bu yol haritası izlediğiniz [ayrıcalıklı erişimi güvenli hale getirme](https://technet.microsoft.com/library/mt631194.aspx).

Kullanıcı hesapları yönetilir ve Azure Active Directory veya Active Directory tarafından kimliği doğrulanmış olup olmadığını Azure Active Directory, Office 365 veya diğer Microsoft Hizmetleri ve uygulamaları kullanan müşteriler için bu kurallar uygulanır. Merhaba aşağıdaki bölümlerde daha fazla bilgi üzerinde Azure AD özellikleri toosupport ayrıcalıklı erişim güvenliğini sağlayın.

## <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication
tooincrease hello güvenlik yönetici kimlik doğrulama ayrıcalıklarını verme önce iki aşamalı doğrulama istemeniz gerekir. İki aşamalı doğrulama, olan doğrulama için bir yöntem hello kullanımını daha fazlasını bir kullanıcı adı ve parola gerektirmesidir. Güvenlik toouser oturum açmalarına ve işlemlerine ikinci bir katmanı sağlar.

Azure multi-Factor Authentication (MFA) Microsoft'un iki aşamalı doğrulama çözüm, hangi erişim toodata ve uygulamaları basit bir oturum açma işlemi için kullanıcı talebine buluştururken korunmasına yardımcı olur. Kolay doğrulama seçenekleri de dahil olmak üzere çeşitli aracılığıyla güçlü kimlik doğrulaması sunar:

- telefon aramaları
- Metin iletileri
- Mobil uygulama bildirimleri
- Mobil uygulama doğrulama kodları
- Üçüncü taraf OATH belirteçleri

Azure multi-Factor Authentication nasıl çalıştığını genel bir bakış için aşağıdaki videoyu hello bakın:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

Daha fazla bilgi için bkz: [MFA Office 365 ve Azure MFA için](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).

## <a name="time-bound-privileges"></a>Zaman sınırlı ayrıcalıkları
Bazı kuruluşlar, çok sayıda kullanıcı yüksek ayrıcalıklı rolleri olması fark edebilirsiniz. Bir kullanıcı bir hizmet için toosign gibi belirli bir etkinliği için toohello rolü eklenmiş olabilir ancak bu ayrıcalıkları sık daha sonra kullanmadı.

toolower hello Etkilenme zaman ayrıcalık ve bunların kullanılması ayrıcalıklarını üzerinde "tam zamanında" alma sınırı kullanıcılar tooonly, görünürlük artırma (JIT), bir görev tooperform gerektiğinde. Azure Active Directory ve Microsoft Online Services için kullanabileceğiniz [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).

![PIM Panosu][2]

## <a name="attack-detection"></a>Saldırı algılama
[Azure Active Directory kimlik koruması](../active-directory-identityprotection.md) risk olaylarına ve olası güvenlik açıklarını kuruluşunuzdaki kimlikleri etkileyen birleştirilmiş bir görünüm sağlar. Risk olaylarına bağlı olarak, her kullanıcı için bir kullanıcı risk düzeyi kimlik koruması hesaplar, sağlayarak tooautomatically korumak tooconfigure risk tabanlı ilkeleri, kuruluşunuzun kimlikleri hello. Azure Active Directory ve EMS tarafından sağlanan diğer koşullu erişim denetimlerle birlikte bu ilkeler, otomatik olarak hello kullanıcı engelleme veya parola sıfırlama ve çok faktörlü kimlik doğrulaması zorlama dahil öneriler sunar.

![Azure AD Kimlik Koruması][3]

## <a name="conditional-access"></a>Koşullu erişim
Koşullu erişim denetimi ile Azure Active Directory erişimi tooan uygulama izin vermeden önce bir kullanıcının kimliğini doğrularken seçtiğiniz hello belirli koşullar denetler. Bu koşullar sağlandığında hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin verilir.

![MFA ile koşullu erişim kurallarının ayarlanması][4]

## <a name="related-articles"></a>İlgili makaleler
* Etkinleştirme [Azure çok faktörlü kimlik doğrulaması](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Etkinleştirme [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)
* Etkinleştirme [Azure AD kimlik koruması](../active-directory-identityprotection.md)
* Etkinleştirme [koşullu erişim denetimleri](../active-directory-conditional-access.md)

Tüm güvenlik yol haritası oluşturma ile ilgili daha fazla bilgi için hello hello "Müşteri sorumlulukları ve yol haritası" bölümüne bakın [Microsoft Cloud Security Kurumsal Mimarlar için](http://aka.ms/securecustomer) belge. Bu konularda biriyle Microsoft Hizmetleri tooassist çekici daha fazla bilgi için Microsoft temsilcinize başvurun veya ziyaret bizim [siber güvenlik çözümleri sayfa](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png

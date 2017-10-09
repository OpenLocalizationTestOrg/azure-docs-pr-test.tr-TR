---
title: "aaaAzure Active Directory cihaz kayıt genel bakış | Microsoft Docs"
description: "Azure Active Directory cihaz kaydı, cihaz temelli koşullu erişim senaryoları için hello temelidir. Bir cihaz kaydedildiğinde Azure Active Directory cihaz kaydı hükümleri hello kullanıcı oturum açtığında kullanılan tooauthenticate hello cihaz olan bir kimliğe sahip cihazı hello."
services: active-directory
keywords: "cihaz kaydı, cihaz kaydını etkinleştirme, cihaz kaydı ve MDM"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 1e92c1a2-01b8-4225-950b-373cd601b035
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: b9846e34fe873d271ebe71cbf8e70c6b4768885b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Azure Active Directory cihaz kaydına başlarken
Azure Active Directory cihaz kaydı, cihaz temelli koşullu erişim senaryoları için hello temelidir. Bir cihaz kaydedildiğinde Azure Active Directory cihaz kaydı hello hello kullanıcı oturum açtığında kullanılan tooauthenticate hello cihaz olan bir kimliğe sahip cihazı sağlar. Kimliği doğrulanmış hello cihaz ve hello cihazın hello öznitelikleri hello bulutta ve şirket içi barındırılan uygulamalar için kullanılan tooenforce koşullu erişim ilkeleri olabilir.

Microsoft Intune gibi bir mobil cihaz birleştirildiğinde çözümü ile birleştirildiğinde Azure Active Directory'de hello cihaz öznitelikleri hello cihaz hakkındaki ek bilgilerle güncelleştirilir. Bu, cihazları toomeet erişimden zorunlu toocreate koşullu erişim kuralları, güvenlik ve uyumluluğa yönelik standartlarınızı sağlar. Microsoft Intune’da cihazları kaydetme hakkında daha fazla bilgi için bkz. [Intune’da yönetim için cihazları kaydetme](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a>Azure Active Directory cihaz kaydı tarafından etkinleştirilen senaryolar
Azure Active Directory cihaz kaydı iOS, Android ve Windows cihazları için destek içerir. hello Azure AD cihaz kaydı'nı kullanan bireysel senaryolar daha fazla özel gereksinime ve platform desteğine sahip olabilir. Bu senaryolar aşağıdaki gibidir:

* **Olan koşullu erişim tooapplications şirket içinde barındırılan**: uygulamalar toouse AD FS Windows Server 2012 R2 ile yapılandırılmış için kayıtlı cihazlara erişim ilkeleri ile kullanabilirsiniz. Şirket içi uygulamalara koşullu erişimi ayarlama hakkında daha fazla bilgi edinmek için bkz. [Azure Active Directory cihaz kaydı hizmetini kullanarak Şirket İçi Uygulamalara Koşullu Erişim](active-directory-device-registration-on-premises-setup.md).
* **Microsoft Intune ile Office 365 uygulamaları için koşullu erişim** : BT yöneticileri, koşullu erişim cihaz ilkeleri toosecure şirket kaynaklarına, hazırlayabilirsiniz, hello aynı zaman uyumlu cihazlara izin verme bilgi çalışanları sırada tooaccess hello Hizmetleri. Daha fazla bilgi edinmek için bkz. [Office 365 hizmetleri için Koşullu Erişim Cihaz İlkeleri](active-directory-conditional-access-device-policies.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Azure Active Directory cihaz kaydını ayarlama
Böylece mobil cihazlar için iyi bilinen DNS kayıtlarına bakarak hello hizmet bulabilir tooenable Azure AD cihaz kaydı'hello Azure Portal gerekir. Windows 10, Windows 8.1, Windows 7, Android ve iOS aygıtları bulmak ve hello Hizmeti'yle böylece şirket DNS'nizi yapılandırmanız gerekir.
Görüntüleyebilir ve Azure Active Directory'de Yönetici portalı hello kullanarak kayıtlı cihazları etkinleştir/devre dışı bırak.

> [!NOTE]
> En son yönergeler nasıl tooset otomatik cihaz kaydını ayarlama bakın, [toosetup otomatik kayıt Windows etki alanına katılmış cihazlarda Azure Active Directory ile nasıl](active-directory-conditional-access-automatic-device-registration-setup.md).
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a>Azure Active Directory cihaz kaydı hizmetini etkinleştirme
1. İçinde toohello Microsoft Azure portalında yönetici olarak oturum açın.
2. Merhaba soldaki bölmede bulunan seçin **Active Directory**.
3. Merhaba üzerinde **Directory** sekmesinde, dizininizi seçin.
4. Select hello **yapılandırma** sekmesi.
5. Kaydırma adlı toohello bölüm **aygıtları**.
6. **USERS MAY WORKPLACE JOIN DEVICES (KULLANICILAR ÇALIŞMA ALANINA CİHAZ KATABİLİR)** için **ALL (TÜMÜ)** seçeneğini belirleyin.
7. Merhaba en büyük sayı seçin aygıtların kullanıcı başına tooauthorize istiyor.

> [!NOTE]
> Office 365 için Microsoft Intune veya Mobil Cihaz Yönetimi ile kayıt için Çalışma Alanına Katılım gereklidir. Bu hizmetlerden herhangi birini yapılandırdıysanız tümü seçilir ve hello hiçbiri düğmesi devre dışıdır.
> 
> 

Varsayılan olarak, iki öğeli kimlik doğrulama hello hizmeti için etkin değil. Yine de bir cihaz kaydedilirken iki öğeli kimlik doğrulama önerilir.

* Bu hizmet için iki öğeli kimlik doğrulama istemeden önce Azure Active Directory'de iki öğeli kimlik doğrulama sağlayıcısını yapılandırmanız ve kullanıcı hesaplarınızı çok faktörlü kimlik doğrulaması için yapılandırmanız gerekir, bkz: [multi-Factor ekleme Active Directory kimlik doğrulama tooAzure](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Windows Server 2012 R2 ile AD FS kullanıyorsanız AD FS'de iki öğeli kimlik doğrulama modülünü yapılandırmanız gerekir, bkz. [Active Directory Federasyon Hizmetleri ile Multi-Factor Authentication kullanma](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="configure-azure-active-directory-device-registration-discovery"></a>Azure Active Directory cihaz kaydı keşfini yapılandırma
Windows 7 ve Windows 8.1 cihazları, hello kullanıcı hesabı adı ile iyi bilinen cihaz kaydı sunucu adını birleştirerek hello cihaz kayıt hizmeti keşfeder.

Azure Active Directory cihaz kaydı hizmetiniz ile ilişkili toohello A kaydı işaret eden bir DNS CNAME kaydı oluşturmanız gerekir. Hello CNAME kaydı, kuruluşunuzdaki hello kullanıcı hesapları tarafından kullanılan hello UPN soneki arkasından hello iyi bilinen enterpriseregistration önekini kullanmalıdır. Kuruluşunuz birden fazla UPN soneki kullanırsa DNS'de birden çok CNAME kaydının oluşturulması gerekir.

Örneğin, kuruluşunuzda adlı iki UPN soneki kullanırsanız @contoso.com ve @region.contoso.com, aşağıdaki DNS kayıtları hello oluşturur.

| Girdi | Tür | Adres |
| --- | --- | --- |
| enterpriseregistration.contoso.com |CNAME |enterpriseregistration.windows.net |
| enterpriseregistration.region.contoso.com |CNAME |enterpriseregistration.windows.net |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Azure Active Directory'de cihaz nesnelerini görüntüleme ve yönetme
1. Hello Azure yönetici portalından görüntülemek, engelleme ve aygıtların engellemesini kaldırmak. Engellenen bir cihaz artık yapılandırılmış tooallow yalnızca kayıtlı aygıtların erişim tooapplications sahip olur.
2. Microsoft Azure portalı toohello üzerinde yönetici olarak oturum açın.
3. Merhaba soldaki bölmede bulunan seçin **Active Directory**.
4. Dizininizi seçin.
5. Select hello **kullanıcılar** sekmesi. Bir kullanıcı tooview cihazlarını seçip
6. Select hello **aygıtları** sekmesi.
7. Seçin **kayıtlı cihazlar** hello açılan menüsünde.
8. Burada görüntüleyebilir, engelleyebilir veya hello kullanıcılar kayıtlı aygıtların engellemesini kaldırmak.

## <a name="additional-topics"></a>Ek konu başlıkları
Azure AD cihaz kaydı ile Windows 7 ve Windows 8.1 Etki Alanına Katılmış cihazlarınızı kaydedebilirsiniz. Aşağıdaki konularda hello Windows 7 ve Windows 8.1 cihazlarda hello önkoşulları ve hello adımları gerekli tooconfigure aygıt kaydı hakkında daha fazla bilgi sağlar.

* [Windows Etki Alanına Katılmış Cihazlar için Azure Active Directory ile Otomatik cihaz kaydı](active-directory-conditional-access-automatic-device-registration.md)
* [Windows 10 etki alanına katılmış cihazlar için Azure Active Directory ile otomatik cihaz kaydı](active-directory-azureadjoin-devices-group-policy.md)


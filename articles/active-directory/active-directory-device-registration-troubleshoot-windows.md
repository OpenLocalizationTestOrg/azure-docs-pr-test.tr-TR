---
title: "Azure AD etki alanının otomatik kayıt sorunlarını giderme alanına katılmış bilgisayarları Windows 10 ve Windows Server 2016 için | Microsoft Docs"
description: "Azure AD etki alanının otomatik kayıt sorunlarını giderme bilgisayarları Windows 10 ve Windows Server 2016 için katıldı."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a>Azure AD ile – Windows 10 ve Windows Server 2016 alanına katılmamış bilgisayarlar etki alanının otomatik kayıt sorunlarını giderme

Bu konu, aşağıdaki istemciler için geçerlidir:

-   Windows 10
-   Windows Server 2016

Diğer Windows istemcileri için bkz: [etki alanının otomatik kaydı sorun giderme bilgisayarları Windows alt düzey istemciler için Azure AD alanına](active-directory-device-registration-troubleshoot-windows-legacy.md).

Bu konu, etki alanına katılmış aygıtlar otomatik kaydı nda olarak açıklanan yapılandırmış olduğunuz varsayılır, [Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma](active-directory-device-registration-get-started.md) aşağıdaki senaryoları desteklemek için:

- [Cihaz temelli koşullu erişim](active-directory-conditional-access-automatic-device-registration-setup.md)

- [Kurumsal Dolaşım ayarları](active-directory-windows-enterprise-state-roaming-overview.md)

- [İş İçin Windows Hello](active-directory-azureadjoin-passport-deployment.md)


Bu belge hakkında olası sorunları gidermek sorun giderme kılavuzu sağlar. 

Windows kayıt desteklenen 10 Kasım 2015 güncelleştirmesi ve üstü.  
Yukarıdaki senaryoları etkinleştirmek için Yıldönümü güncelleştirme kullanmanızı öneririz.

## <a name="step-1-retrieve-the-registration-status"></a>1. adım: kayıt durumunu alma 

**Kayıt durumunu almak için:**

1. Komut istemini yönetici olarak açın.

2. Tür **dsregcmd/Status**



    +----------------------------------------------------------------------+
   | Cihaz durumu |+----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: Cihaz kimliği yok: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 parmak izi: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platformu Crypto sağlayıcısı TpmProtected: Evet KeySignTest:: test etmek için yükseltilmiş çalıştırmanız gerekir.
                  IDP: login.windows.net Tenantıd: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ JoinSrvVersion ==: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: Evet DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
   | Kullanıcı durumunu |+----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority: kuruluşların WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (Azuread'i) AzureAdPrt: Evet



## <a name="step-2-evaluate-the-registration-status"></a>2. adım: kayıt durumunu değerlendirme 

Aşağıdaki alanları gözden geçirin ve beklenen değerleri sahip olduğunuzdan emin olun:

### <a name="azureadjoined--yes"></a>AzureAdJoined: Evet  

Bu alan, Azure AD ile cihazın kayıtlı olup olmadığını gösterir. Değer 'Hayır' gösteriliyorsa, kayıt tamamlanmadı. 

**Olası nedenler:**

- Kayıt bilgisayarın kimlik doğrulaması başarısız oldu.

- Bilgisayar tarafından bulunan kuruluştaki bir HTTP proxy yok

- Bilgisayar kimlik doğrulaması için Azure AD veya Azure DRS kaydı için ulaşamıyor

- Bilgisayar VPN veya kuruluşunuzun iç ağ üzerinde doğrudan görüş bir şirket içi ile olmayabilir AD etki alanı denetleyicisi.

- Bilgisayar bir TPM varsa, hatalı durumda olabilir.

- Olabilir yetersizliğini Hizmetleri'ndeki not ettiğiniz belgede daha önce yeniden doğrulamanız gerekir. Ortak örnekler şunlardır:

    - Federasyon sunucunuz etkin WS-Trust uç nokta yok

    - Federasyon sunucunuz bilgisayarlardan gelen kimlik doğrulama tümleşik Windows kimlik doğrulaması kullanarak ağınızda izin vermeyebilir.

    - Bilgisayar için ait olduğu AD ormanında Azure AD'de doğrulanmış etki alanı adınızı işaret hizmet bağlantı noktası nesnesi yok

---

### <a name="domainjoined--yes"></a>DomainJoined: Evet  

Bu alan, cihaz bir şirket içi Active Directory veya alanına katılıp katılmadığını gösterir. Değer olarak gösteriliyorsa **Hayır**, aygıt otomatik-Azure AD ile kayıt olamaz. İlk olarak Azure AD ile kaydedebilmek için şirket içi Active Directory cihaz birleştirir denetleyin. Lütfen doğrudan Azure AD ile bilgisayarın katılmasını istiyorsanız, Azure Active Directory katılım yeteneklerini hakkında edinin gidin.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: Hayır  

Bu alan, aygıt Azure AD ile ancak ('Çalışma alanına katılmış ' işaretli) bir kişisel cihaz olarak kayıtlı olup olmadığını gösterir. Bu değer, Azure AD ile kayıtlı bir etki alanına katılmış bilgisayar için 'Hayır' göstermesi gerekir, Evet olarak görünüyorsa ancak bu bir iş veya Okul hesabı kayıt Tamamlanıyor bilgisayar önce eklendiğini anlamına gelir. Bu durumda hesaba Windows 10 (zaman WinVer çalışan komut 'Çalışma' veya bir komut istemi penceresinde 1607) Yıldönümü güncelleştirme sürümünü kullanıyorsanız yoksayılacak.

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: Evet ve AzureADPrt: Evet
  
Bu alanlar cihaza oturum açtıktan sonra Azure ad kullanıcı başarıyla kimliğini doğrulamasından gösterir. Olası nedenler şunlardır gösterdikleri 'Hayır' ise:

- Hatalı depolama anahtar aygıt kaydı (denetimi yükseltilmiş çalışırken KeySignTest) ile ilişkili TPM (STK).

- Alternatif oturum açma kimliği

- HTTP Proxy bulunamadı

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için bkz: [otomatik cihaz kaydı SSS](active-directory-device-registration-faq.md) 
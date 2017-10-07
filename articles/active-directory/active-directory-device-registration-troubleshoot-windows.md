---
title: "aaaTroubleshooting hello otomatik kaydı Azure AD etki alanına katılmış bilgisayarları Windows 10 ve Windows Server 2016 için | Microsoft Docs"
description: "Sorun giderme Hello otomatik kaydı Azure AD etki alanı bilgisayarları Windows 10 ve Windows Server 2016 için katıldı."
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
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a>Birleştirilmiş bilgisayarlar tooAzure AD – Windows 10 ve Windows Server 2016 etki alanının otomatik kayıt sorunlarını giderme

Bu konuda geçerli toohello istemcileri aşağıdaki gibidir:

-   Windows 10
-   Windows Server 2016

Diğer Windows istemcileri için bkz: [Windows alt düzey istemciler için birleştirilmiş bilgisayarlar tooAzure AD otomatik kaydı etki alanının sorun giderme](active-directory-device-registration-troubleshoot-windows-legacy.md).

Bu konu, etki alanına katılmış aygıtlar otomatik kaydı nda olarak açıklanan yapılandırmış olduğunuz varsayılır, [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-device-registration-get-started.md) Aşağıdaki senaryolar toosupport hello:

- [Cihaz temelli koşullu erişim](active-directory-conditional-access-automatic-device-registration-setup.md)

- [Kurumsal Dolaşım ayarları](active-directory-windows-enterprise-state-roaming-overview.md)

- [İş İçin Windows Hello](active-directory-azureadjoin-passport-deployment.md)


Bu belge, nasıl tooresolve olası sorunları hakkında sorun giderme kılavuzu sağlar. 

Merhaba kayıt hello Windows'da desteklenen 10 Kasım 2015 güncelleştirmesi ve üstü.  
Yukarıdaki hello senaryoları etkinleştirmek için hello Yıldönümü güncelleştirme kullanmanızı öneririz.

## <a name="step-1-retrieve-hello-registration-status"></a>1. adım: hello kayıt durumunu alma 

**tooretrieve hello kayıt durumu:**

1. Merhaba komut istemini yönetici olarak açın.

2. Tür **dsregcmd/Status**



    +----------------------------------------------------------------------+
   | Cihaz durumu |+----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: Cihaz kimliği yok: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 parmak izi: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform şifreleme sağlayıcısı TpmProtected: Evet KeySignTest:: Çalıştır yükseltilmiş tootest gerekir.
                  IDP: login.windows.net Tenantıd: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ JoinSrvVersion ==: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: Evet DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
   | Kullanıcı durumunu |+----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority: kuruluşların WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (Azuread'i) AzureAdPrt: Evet



## <a name="step-2-evaluate-hello-registration-status"></a>2. adım: hello kayıt durumunu değerlendirme 

Alanları aşağıdaki hello gözden geçirin ve hello beklenen değerler sahip olduğunuzdan emin olun:

### <a name="azureadjoined--yes"></a>AzureAdJoined: Evet  

Bu alan, Azure AD ile Merhaba cihazın kayıtlı olup olmadığını gösterir. Merhaba değeri 'Hayır' gösteriliyorsa, kayıt tamamlanmadı. 

**Olası nedenler:**

- Merhaba bilgisayarın kayıt için kimlik doğrulaması başarısız oldu.

- Merhaba bilgisayar tarafından bulunan hello kuruluşta bir HTTP proxy yok

- Merhaba bilgisayar kimlik doğrulaması için Azure AD veya Azure DRS kaydı için ulaşamıyor

- Merhaba bilgisayar hello kuruluşunuzun iç ağ veya VPN ile doğrudan görüş tooan olmayabilir şirket içi AD etki alanı denetleyicisi.

- Merhaba bilgisayarda TPM varsa, hatalı durumda olabilir.

- Olabilir yetersizliğini Hizmetleri'ndeki not ettiğiniz hello belgede daha önce tooverify yeniden gerekir. Ortak örnekler şunlardır:

    - Federasyon sunucunuz etkin WS-Trust uç nokta yok

    - Federasyon sunucunuz bilgisayarlardan gelen kimlik doğrulama tümleşik Windows kimlik doğrulaması kullanarak ağınızda izin vermeyebilir.

    - Merhaba bilgisayar için ait olduğu hello AD ormanındaki Azure AD'de tooyour doğrulanmış etki alanı adına işaret hizmet bağlantı noktası nesnesi yok

---

### <a name="domainjoined--yes"></a>DomainJoined: Evet  

Bu alan hello aygıt birleştirilmiş tooan şirket içi Active Directory olup olmadığını gösterir. Merhaba değeri olarak gösteriliyorsa **Hayır**, hello aygıt olamaz otomatik kaydını Azure AD ile. İlk olarak bu hello aygıt birleştirmeler toohello Active Directory, Azure AD ile kaydedebilmek için şirket içi denetleyin. Lütfen hello bilgisayar tooAzure AD doğrudan katılmak için arıyorsanız, Azure Active Directory katılım yetenekleriyle ilgili tooLearn gidin.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: Hayır  

Bu alan hello aygıt Azure AD ile ancak ('Çalışma alanına katılmış ' işaretli) bir kişisel cihaz olarak kayıtlı olup olmadığını gösterir. Ancak bu değer, Azure AD ile kayıtlı bir etki alanına katılmış bilgisayar için 'Hayır' göstermesi gerekir, bu anlamına gelir Evet olarak gösteriliyorsa eklenen önceki toohello bilgisayar Tamamlanıyor kaydı bir iş veya Okul hesabı idi. Bu durumda hello hesap hello Yıldönümü güncelleştirme Windows 10 (zaman içinde hello WinVer komutu çalıştıran hello 'Run' veya bir komut istemi penceresinde 1607) sürümünü kullanıyorsanız yoksayılacak.

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: Evet ve AzureADPrt: Evet
  
Bu alanlar hello kullanıcı toohello aygıtı imzalama sırasında tooAzure AD başarıyla doğrulaması gösterir. Bunlar gösterirse 'Hayır' hello olası nedenleri şunlardır:

- Hatalı depolama anahtar hello aygıt kaydı (KeySignTest yükseltilmiş çalışırken onay hello) ile ilişkili TPM (STK).

- Alternatif oturum açma kimliği

- HTTP Proxy bulunamadı

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için bkz: Merhaba [otomatik cihaz kaydı SSS](active-directory-device-registration-faq.md) 

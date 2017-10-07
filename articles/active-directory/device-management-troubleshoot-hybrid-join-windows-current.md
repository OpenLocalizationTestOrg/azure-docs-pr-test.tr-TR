---
title: "aaaTroubleshooting karma Azure Active Directory'ye katılmış Windows 10 ve Windows Server 2016 cihazları | Microsoft Docs"
description: "Karma Azure Active Directory sorun giderme Windows 10 ve Windows Server 2016 cihazları katıldı."
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a>Katılmış Windows 10 ve Windows Server 2016 cihazlarda karma Azure Active Directory sorun giderme 

Bu konuda geçerli toohello istemcileri aşağıdaki gibidir:

-   Windows 10
-   Windows Server 2016

Diğer Windows istemcileri için bkz: [sorun giderme karma Azure Active Directory birleştirilmiş alt düzey aygıtları](device-management-troubleshoot-hybrid-join-windows-legacy.md).

Bu konu, sahibi olduğunuzu varsayar [yapılandırılmış karma Azure Active Directory'ye katılmış cihazları](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello senaryolar:

- Cihaz temelli koşullu erişim

- [Kurumsal Dolaşım ayarları](active-directory-windows-enterprise-state-roaming-overview.md)

- [İş İçin Windows Hello](active-directory-azureadjoin-passport-deployment.md)


Bu belge, nasıl tooresolve olası sorunları hakkında sorun giderme kılavuzu sağlar. 


Windows 10 ve Windows Server 2016 için karma Azure Active Directory katılım destekler hello Windows 10 Kasım 2015 güncelleştirmesi ve üstü. Merhaba Yıldönümü güncelleştirme kullanmanızı öneririz.

## <a name="step-1-retrieve-hello-join-status"></a>1. adım: hello birleşim durumu alma 

**tooretrieve hello birleşim durumu:**

1. Bir yönetici olarak açın hello komut istemi

2. Tür **dsregcmd/Status**



    +----------------------------------------------------------------------+
   | Cihaz durumu |+----------------------------------------------------------------------+
    
        AzureAdJoined: YES
     EnterpriseJoined: Cihaz kimliği yok: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 parmak izi: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform şifreleme sağlayıcısı TpmProtected: Evet KeySignTest:: Çalıştır yükseltilmiş tootest gerekir.
                  IDP: login.windows.net Tenantıd: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/ msitsupp.microsoft.com/oauth2/Token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https:// Portal.Manage-Beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ JoinSrvVersion ==: 1.0 JoinSrvUrl: https:// enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs: enterpriseregistration.Windows.NET DomainJoined: Evet DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
   | Kullanıcı durumunu |+----------------------------------------------------------------------+
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    WamDefaultAuthority: kuruluşların WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (Azuread'i) AzureAdPrt: Evet



## <a name="step-2-evaluate-hello-join-status"></a>2. adım: hello birleşim durumu değerlendirin 

Alanları aşağıdaki hello gözden geçirin ve hello beklenen değerler sahip olduğunuzdan emin olun:

### <a name="azureadjoined--yes"></a>AzureAdJoined: Evet  

Bu alan hello aygıt ile Azure AD alanına katılıp katılmadığını gösterir. Merhaba değer ise **Hayır**, hello birleştirme tooAzure AD henüz tamamlanmadı. 

**Olası nedenler:**

- Bir birleştirme hello bilgisayarın kimlik doğrulaması başarısız oldu.

- Merhaba bilgisayar tarafından bulunan hello kuruluşta bir HTTP proxy yok

- Merhaba bilgisayar kaydı için Azure AD tooauthenticate veya Azure DRS ulaşamıyor

- Merhaba bilgisayar hello kuruluşunuzun iç ağ veya VPN ile doğrudan görüş tooan olmayabilir şirket içi AD etki alanı denetleyicisi.

- Merhaba bilgisayarda TPM varsa, hatalı durumda olabilir.

- Olabilir yetersizliğini hello Hizmetleri'ndeki not ettiğiniz hello belgede daha önce tooverify yeniden gerekir. Ortak örnekler şunlardır:

    - Federasyon sunucunuz etkin WS-Trust uç nokta yok

    - Federasyon sunucunuz bilgisayarlardan gelen kimlik doğrulama tümleşik Windows kimlik doğrulaması kullanarak ağınızda izin vermiyor.

    - Merhaba bilgisayar için ait olduğu hello AD ormanındaki Azure AD'de tooyour doğrulanmış etki alanı adına işaret hizmet bağlantı noktası nesnesi yok

---

### <a name="domainjoined--yes"></a>DomainJoined: Evet  

Bu alan hello aygıt alanına katılmış olup olmadığını tooan Active Directory veya şirket içi gösterir. Merhaba değer ise **Hayır**, hello aygıt, bir karma Azure AD birleştirme gerçekleştiremez.  

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: Hayır  

Bu alan bir kişisel cihaz olarak Azure AD ile Merhaba cihazın kayıtlı olup olmadığını belirtir (olarak işaretlenmiş *çalışma alanına katılmış*). Bu değer olmalıdır **Hayır** de etki alanına katılmış bir bilgisayar için karma Azure AD alanına. Merhaba değer ise **Evet**, bir iş veya Okul hesabı önceki toohello tamamlama hello karma Azure AD birleştirme eklendi. Bu durumda, hello hesap hello Yıldönümü güncelleştirme Windows 10 (1607) sürümünü kullanırken göz ardı edilir.

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: Evet ve AzureADPrt: Evet
  
Bu alanların hello kullanıcı başarıyla tooAzure AD doğrulaması olup olmadığını belirtmek toohello aygıtı imzalarken. Merhaba değerler ise **Hayır**, son olabilir:

- Hatalı depolama anahtar hello aygıt kaydı (KeySignTest yükseltilmiş çalışırken onay hello) ile ilişkili TPM (STK).

- Alternatif oturum açma kimliği

- HTTP Proxy bulunamadı

## <a name="next-steps"></a>Sonraki adımlar

Merhaba soruları için bkz [aygıt yönetimi hakkında SSS](device-management-faq.md) 

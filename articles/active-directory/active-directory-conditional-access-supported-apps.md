---
title: "aaaApplications ve Azure Active Directory'de koşullu erişim kuralları kullanma tarayıcıları | Microsoft Docs"
description: "Merhaba kullanıcı ve tooallow uygulama erişimini doğruladığında koşullu erişim denetimi ile Azure Active Directory belirli koşullarını denetler."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca20853bb9f4b22d0b88ddd2f051d658e0d88cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a>Uygulamalar ve Azure Active Directory'de koşullu erişim kuralları kullanma tarayıcılar

Koşullu erişim kuralları, Azure Active Directory (Azure AD) desteklenir-bağlı uygulamalar, Federasyon yazılım hizmet (SaaS) uygulaması olarak, parola çoklu oturum açma (SSO) kullanan uygulamaları satır iş kolu uygulamaları, önceden tümleştirilmiştir ve Azure AD uygulama proxy'si kullanan uygulamalar. Uygulamaları koşullu erişim için kullanabileceğiniz ayrıntılı bir listesi için bkz [Hizmetleri ile koşullu erişim etkin](active-directory-conditional-access-technical-reference.md). Koşullu erişim modern kimlik doğrulaması kullanan mobil ve Masaüstü uygulamaları ile hem de çalışır. Bu makalede, koşullu erişimin nasıl çalıştığı mobil ve masaüstü uygulamalarında kapsar.

Modern kimlik doğrulaması kullanan uygulamalarda Azure AD oturum açma sayfalarını kullanabilirsiniz. Bir oturum açma sayfası ile çok faktörlü kimlik doğrulaması için bir kullanıcıya sorulur. Merhaba kullanıcının erişimi engellendi bir ileti gösterilir. Böylece cihaz temelli koşullu erişim ilkelerinin değerlendirildiği Modern kimlik doğrulaması Azure AD ile Merhaba aygıt tooauthenticate gereklidir.

Hangi uygulamaların koşullu erişim kuralları kullanmak ve diğer uygulama giriş noktaları tootake toosecure gerekebilecek adımları hello önemli tooknow olur.

## <a name="applications-that-use-modern-authentication"></a>Modern kimlik doğrulamasını kullanan uygulamalar
> [!NOTE]
> Office 365'te bir eşdeğer olan Azure AD koşullu erişim ilkesi varsa, her iki koşullu erişim ilkelerini yapılandırın. Bu, örneğin, Exchange Online veya SharePoint Online için tooconditional erişim ilkeleri uygular.
>
>

Merhaba aşağıdaki uygulamalar koşullu erişim Office 365 ve diğer Azure AD bağlı hizmet uygulamaları için destek:


| Hedef hizmet| Platform| Uygulama |
| --- | --- | --- |
| Herhangi bir My uygulamaları uygulama hizmeti| Android ve iOS| MFA ve konum İlkesi uygulamalar için. Cihaz tabanlı ilkeleri desteklenmez.|
| Azure uzak uygulama hizmeti| Windows 10, Windows 8.1, Windows 7, iOS, Android ve Mac OS X| Azure RemoteApp|
| Dynamics CRM| Windows 10, Windows 8.1, Windows 7, iOS ve Android| Dynamics CRM uygulaması|
| Microsoft Teams| Windows 10, Windows 8.1, Windows 7, iOS/Android ve MAC OSX| Windows masaüstünde, MAC OS X, iOS, Android, WP ve web istemcisi Microsoft Teams destekleyen tüm hizmetleri ve onun tüm istemci uygulamaları - Microsoft ekipleri Hizmetleri - bu denetler|
| Office 365 Exchange Online| Windows 10| Takvim/posta/kişiler uygulama, Outlook 2016, Outlook 2013 (modern kimlik doğrulaması ile) Skype Kurumsal (ile modern kimlik doğrulaması)|
| Office 365 Exchange Online| Windows 8.1, Windows 7| Outlook 2016, Outlook 2013 (modern kimlik doğrulaması ile) Skype Kurumsal (modern kimlik doğrulaması)|
| Office 365 Exchange Online| iOS| Outlook mobil uygulama|
| Office 365 Exchange Online| Mac OS X| Outlook 2016 (Office macOS için)|
| Office 365 SharePoint Online| Windows 10| Office 2016 uygulamalar, Evrensel Office uygulamaları, Office 2013 (modern kimlik doğrulaması ile), OneDrive eşitleme istemcisi (bkz [notları](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), Office grupları desteği, hello gelecek için planlanan SharePoint uygulama desteği planlanan hello gelecekteki|
| Office 365 SharePoint Online| Windows 8.1, Windows 7| Office 2016 uygulamaları, Office 2013 (modern kimlik doğrulaması ile) OneDrive eşitleme istemci (bkz [notları](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))|
| Office 365 SharePoint Online| iOS, Android| Office mobil uygulamaları|
| Office 365 SharePoint Online| Mac OS X| MacOS (Word, Excel, PowerPoint, yalnızca OneNote) için Office 2016. OneDrive iş desteğine hello gelecek için planlanan|
| Office 365 Yammer| Windows 10, iOS, Android| Office Yammer uygulaması|
| Powerbı hizmeti| Windows 10, Windows 8.1, Windows 7 ve iOS| Power BI uygulaması. Android için Hello Power BI uygulaması cihaz temelli koşullu erişim şu anda desteklemiyor.|
| Visual Studio Team Services| Windows 10, Windows 8.1, Windows 7, iOS ve Android| Visual Studio Team Services uygulama|








## <a name="applications-that-do-not-use-modern-authentication"></a>Modern kimlik doğrulamasını kullanmayın uygulamaları
Şu anda, modern kimlik doğrulamasını kullanmayın diğer yöntemleri tooblock erişim tooapps kullanmanız gerekir. Modern kimlik doğrulaması kullanmayan uygulamalar için erişim kuralları tarafından koşullu erişim uygulanmaz. Bu öncelikle için bir Exchange ve SharePoint erişimini konusudur. Uygulamaların çoğu önceki sürümleri eski erişim denetimi protokolleri kullanır.

### <a name="control-access-in-office-365-sharepoint-online"></a>Office 365 SharePoint Online'daki erişimi denetleme
Merhaba kümesi SPOTenant cmdlet'ini kullanarak SharePoint erişimi için eski protokolleri devre dışı bırakabilirsiniz. SharePoint Online kaynaklarına erişmesini modern olmayan kimlik doğrulama protokollerini kullanan Bu cmdlet'i tooprevent Office istemcileri kullanın.

**Örnek komut**:`Set-SPOTenant -LegacyAuthProtocolsEnabled $false`

### <a name="control-access-in-office-365-exchange-online"></a>Office 365 Exchange Online'da erişimi denetleme
Exchange kurallarının iki ana kategoriye sunar. Seçenekler aşağıdaki hello gözden geçirin ve ardından kuruluşunuz için uygun olduğunu hello ilkesi seçin.

* **Exchange ActiveSync**. Varsayılan olarak, Exchange ActiveSync için çok faktörlü kimlik doğrulaması ve konumu için koşullu erişim ilkeleri uygulanmaz. Exchange ActiveSync İlkesi doğrudan yapılandırarak veya Active Directory Federasyon Hizmetleri (AD FS) kurallarını kullanarak Exchange ActiveSync engelleme tooprotect erişim toothese Hizmetleri gerekir.
* **Eski protokolleri**. AD FS ile eski protokolleri engelleyebilirsiniz. Bu, Office 2013 modern kimlik doğrulaması etkinleştirilmiş ve Office'in önceki sürümlerinde olmadan gibi erişim tooolder Office istemcileri engeller.

### <a name="use-ad-fs-tooblock-legacy-protocol"></a>AD FS tooblock eski protokolünü kullan
Aşağıdaki örnek verme yetkilendirme kuralları tooblock eski Protokolü erişimi hello AD FS düzeyinde hello kullanabilirsiniz. İki ortak yapılandırmalardan seçin.

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-hello-intranet"></a>Seçenek 1: Exchange ActiveSync izin verme ve eski uygulamalar, ancak yalnızca hello intranet üzerinde izin ver
Aşağıdaki üç kuralları toohello hello uygulayarak Microsoft Office 365 kimlik platformu için Exchange ActiveSync trafiği, AD FS bağlı olan taraf güven ve tarayıcı ve modern kimlik doğrulama trafiğini erişimi vardır. Eski uygulamalar hello extranet engellenir.

##### <a name="rule-1"></a>Kural 1
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a>Kural 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a>Kuralı 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a>Seçenek 2: Exchange ActiveSync izin verme ve eski uygulamaları engelleme
Aşağıdaki üç kuralları toohello hello uygulayarak Microsoft Office 365 kimlik platformu için Exchange ActiveSync trafiği, AD FS bağlı olan taraf güven ve tarayıcı ve modern kimlik doğrulama trafiğini erişimi vardır. Eski uygulamaları herhangi bir konumdan engellenir.

##### <a name="rule-1"></a>Kural 1
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a>Kural 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a>Kuralı 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a>Cihaz tabanlı ilkeleri için desteklenen tarayıcılar 

Azure AD tanımlamak ve hello cihaz kimlik doğrulaması gerektiğinde erişimi denetleme tabanlı cihaz ilkeleri için cihaz uyumluluğu ve etki alanına katılma için yalnızca elde edebilirsiniz. Konum ve MFA iş çoğu cihazlar ve tarayıcılar gibi çoğu denetimleri sırasında hello işletim sistemi sürümü ve tarayıcılar aşağıda listelenen cihaz ilkeleri gerektirir. Bir cihaz İlkesi devredeyken desteklenmeyen tarayıcılarda veya hello işletim sistemlerinde kullanıcılar için erişim engellenir. 

| İşletim Sistemi                     | Tarayıcılar                 | Destek     |
| :--                    | :--                      | :-:         |
| Win 10                 | IE, sınır                 | ![İşaretli][1] |
| Win 10                 | Chrome                   | Önizleme     |
| Win 8 / 8.1            | IE, Chrome               | ![İşaretli][1] |
| Win 7                  | IE, Chrome               | ![İşaretli][1] |
| iOS                    | Safari                   | ![İşaretli][1] |
| Android                | Chrome                   | ![İşaretli][1] |
| Windows Phone          | IE, sınır                 | ![İşaretli][1] |
| Windows Server 2016    | IE, sınır                 | ![İşaretli][1] |
| Windows Server 2016    | Chrome                   | Çok yakında |
| Windows Server 2012 R2 | IE, Chrome               | ![İşaretli][1] |
| Windows Server 2008 R2 | IE, Chrome               | ![İşaretli][1] |
| Mac OS                 | Safari                   | ![İşaretli][1] |
| Mac OS                 | Chrome                   | Çok yakında |

> [!NOTE]
> Chrome desteği, Windows 10 oluşturucuları güncelleştirme ve bulunan yükleme hello uzantısı kullanıyor olmanız gerekir [burada](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).
>
>

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla ayrıntı için bkz: [Azure Active Directory'de koşullu erişim](active-directory-conditional-access.md)




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png



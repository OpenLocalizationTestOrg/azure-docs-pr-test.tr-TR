---
title: "Azure AD Connect: Doğrudan kimlik doğrulama sorunlarını giderme | Microsoft Docs"
description: "Bu makalede nasıl tootroubleshoot Azure Active Directory (Azure AD) doğrudan kimlik doğrulaması."
services: active-directory
keywords: "Azure AD Connect doğrudan kimlik doğrulama sorunlarını giderme, Active Directory, Azure AD, SSO için gerekli bileşenleri yüklemek çoklu oturum açma"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a>Azure Active Directory doğrudan kimlik doğrulama sorunlarını giderme

Bu makale size yardımcı olacak bilgileri Azure AD geçişli kimlik doğrulaması ile ilgili genel sorunları hakkında sorun giderme bulma.

>[!IMPORTANT]
>Kullanıcı oturum açma sorunları geçişli kimlik doğrulaması ile karşılıklı yok hello özelliğini devre dışı bırakmak veya bir yalnızca bulut genel yönetici hesabı toofall kalmadan geri doğrudan kimlik doğrulama aracıları kaldırın. Hakkında bilgi edinin [bir yalnızca bulut genel yönetici hesabı ekleme](../active-directory-users-create-azure-portal.md). Bu adımı uygulamadan önemlidir ve, kiracınızın dışında erişebilmenizin sağlar.

## <a name="general-issues"></a>Genel sorunlar

### <a name="check-status-of-hello-feature-and-authentication-agents"></a>Merhaba özellik ve kimlik doğrulama aracısı durumunu denetleme

Bu hello doğrudan kimlik doğrulama özelliği olduğundan hala emin **etkin** , Kiracı ve hello kimlik doğrulaması aracılar üzerinde durumunu gösterir **etkin**ve **devre dışı**. Giden toohello tarafından durumunu denetleyebilirsiniz **Azure AD Connect** hello dikey penceresinde [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com/).

![Azure Active Directory Yönetim Merkezi - Azure AD Connect dikey penceresi](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory Yönetim Merkezi - doğrudan kimlik doğrulama dikey penceresi](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a>Oturum açma kullanıcı dönük hata iletileri

Merhaba kullanıcı doğrudan kimlik doğrulama kullanarak oluşturulamıyor toosign ise, bunlar aşağıdaki hello Azure AD oturum açma ekranında kullanıcı dönük hatalar hello birini görebilirsiniz: 

|Hata|Açıklama|Çözüm
| --- | --- | ---
|AADSTS80001|Dizin oluşturulamıyor tooconnect tooActive|Aracı sunucularının hello aynı AD orman üyeleri olarak hello kullanıcıların parolaları toobe doğrulanması gerekir ve bunlar mümkün tooconnect tooActive dizin olduğundan emin olun.  
|AADSTS8002|Bağlantı tooActive dizin zaman aşımı oluştu|Active Directory kullanılabilir ve toorequests hello aracılardan yanıt tooensure denetleyin.
|AADSTS80004|toohello aracı geçirilen hello kullanıcı adı geçerli değil.|Merhaba kullanıcı toosign hello doğru kullanıcı adı ile çalışıyor olun.
|AADSTS80005|Doğrulama öngörülemeyen WebException karşılaştı|Geçici bir hata oluştu. Merhaba isteği yeniden deneyin. Toofail devam ederse, Microsoft Destek'e başvurun.
|AADSTS80007|Active Directory ile iletişim kuran bir hata oluştu|Daha fazla bilgi için Hello Aracısı günlüklerine bakın ve Active Directory beklendiği gibi çalıştığını doğrulayın.

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Oturum açma hatası nedeniyle'hello Azure Active Directory Yönetim Merkezi'nde

Kullanıcı oturum açma sırasında hello bakarak sorunlarını Başlat [oturum açma etkinliği raporu](../active-directory-reporting-activity-sign-ins.md) hello üzerinde [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com/).

![Azure Active Directory Yönetim Merkezi - oturum açma işlemleri raporu](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

Çok gidin**Azure Active Directory** -> **oturum açma işlemleri** hello üzerinde [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com/) ve belirli bir kullanıcının oturum açma etkinliği tıklatın. Merhaba Ara **oturum açmayı hata kodu** alan. Bu alan tooa hata nedeni ve çözümü aşağıdaki tablonun hello kullanarak Hello değeri eşleyin:

|Oturum açma hata kodu|Oturum açma hatası nedeni|Çözüm
| --- | --- | ---
| 50144 | Kullanıcının Active Directory parolasının süresi doldu. | Şirket içi Active Directory'de Hello kullanıcının parolasını sıfırlayın.
| 80001 | Kullanılabilir Kimlik Doğrulama Aracısı yok. | Yükleyin ve bir kimlik doğrulama Aracısı kaydedin.
| 80002 | Kimlik Doğrulama Aracısı'nın parola doğrulama isteği zaman aşımına uğradı. | Active Directory kimlik doğrulama Aracısı hello erişilebilir olup olmadığını denetleyin.
| 80003 | Kimlik Doğrulama Aracısı tarafından geçersiz yanıt alındı. | Merhaba sorun birden çok kullanıcı arasında tutarlı bir şekilde yineleniyorsa, Active Directory yapılandırmanızı denetleyin.
| 80004 | Oturum açma isteğinde yanlış Kullanıcı Asıl Adı (UPN) kullanıldı. | Merhaba kullanıcı toosign hello doğru kullanıcı adını oturum isteyin.
| 80005 | Kimlik Doğrulama Aracısı: Hata oluştu. | Geçici hata oluştu. Daha sonra yeniden deneyin.
| 80007 | Kimlik Doğrulama Aracısı yüklenemiyor tooconnect tooActive dizini. | Active Directory kimlik doğrulama Aracısı hello erişilebilir olup olmadığını denetleyin.
| 80010 | Kimlik Doğrulama Aracısı yüklenemiyor toodecrypt parolası. | Merhaba sorun tutarlı bir şekilde yineleniyorsa yükleyin ve yeni bir kimlik doğrulama Aracısı kaydedin. Ve geçerli bir hello kaldırın. 
| 80011 | Kimlik Doğrulama Aracısı yüklenemiyor tooretrieve şifre çözme anahtarı. | Merhaba sorun tutarlı bir şekilde yineleniyorsa yükleyin ve yeni bir kimlik doğrulama Aracısı kaydedin. Ve geçerli bir hello kaldırın.

## <a name="authentication-agent-installation-issues"></a>Kimlik Doğrulama Aracısı yükleme sorunları

### <a name="an-unexpected-error-occurred"></a>Beklenmeyen bir hata oluştu

[Aracı günlükleri toplamak](#collecting-pass-through-authentication-agent-logs) hello sunucusuna gelen ve sorunu ile Microsoft Support başvurun.

## <a name="authentication-agent-registration-issues"></a>Kimlik Doğrulama Aracısı kayıt sorunları

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a>Merhaba kimlik doğrulama Aracısı kaydı tooblocked bağlantı noktaları başarısız oldu

Hangi hello üzerinde kimlik doğrulama aracısı yüklü hello sunucu URL'lerin ve bağlantı noktalarının listelenen bizim hizmetiyle iletişim olun [burada](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a>Merhaba kimlik doğrulama Aracısı kaydı tootoken veya hesap yetkilendirme hataları başarısız oldu

Tüm Azure AD Connect veya tek başına kimlik doğrulama Aracısı yükleme ve kayıt işlemleri için bir yalnızca bulut genel yönetici hesabı kullandığınızdan emin olun. MFA etkin genel yönetici hesapları ile ilgili bilinen bir sorun yoktur; MFA devre dışı geçici olarak (yalnızca toocomplete hello işlemleri) geçici bir çözüm olarak etkinleştirin.

### <a name="an-unexpected-error-occurred"></a>Beklenmeyen bir hata oluştu

[Aracı günlükleri toplamak](#collecting-pass-through-authentication-agent-logs) hello sunucusuna gelen ve sorunu ile Microsoft Support başvurun.

## <a name="authentication-agent-uninstallation-issues"></a>Kimlik Doğrulama Aracısı kaldırma konuları

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a>Azure AD Connect kaldırırken uyarı iletisi

Doğrudan kimlik doğrulama, Kiracı'etkin olması ve toouninstall Azure AD Connect çalışırsanız, uyarı iletisi hello gösterir: "kullanıcılar olmayacak mümkün toosign bileşenini tooAzure AD diğer doğrudan kimlik doğrulama Aracısı yoksa diğer sunucularda yüklü."

Kurulumunuzu olduğundan emin olun [yüksek kullanılabilir](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) kullanıcı oturum açma yeni Azure AD Connect tooavoid kaldırmadan önce.

## <a name="issues-with-enabling-hello-feature"></a>Merhaba özelliğini etkinleştirme sorunlar

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a>Kullanılabilir herhangi bir kimlik doğrulama aracı olduğundan hello özelliğini etkinleştirme başarısız oldu

Toohave gereken en az bir etkin kimlik doğrulama Aracısı tooenable doğrudan kimlik doğrulama kiracınız üzerinde. Azure AD Connect yükleme ya da tek başına bir kimlik doğrulama aracısı tarafından bir kimlik doğrulama Aracısı yükleyebilirsiniz.

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a>Merhaba özelliğini etkinleştirme tooblocked bağlantı noktaları başarısız oldu

Azure AD Connect yüklü hello sunucu URL'lerin ve bağlantı noktalarının listelenen bizim hizmetiyle iletişim olun [burada](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a>Merhaba özelliğini etkinleştirme tootoken veya hesap yetkilendirme hataları başarısız oldu

Merhaba Özellik etkinleştirilirken bir yalnızca bulut genel yönetici hesabı kullandığınızdan emin olun. Çok faktörlü kimlik doğrulaması (MFA) ile ilgili bilinen bir sorun yoktur-genel yönetici hesapları; etkin MFA devre dışı geçici olarak (yalnızca toocomplete hello işlemi) geçici bir çözüm olarak etkinleştirin.

## <a name="exchange-activesync-configuration-issues"></a>Exchange ActiveSync yapılandırma sorunları

Doğrudan kimlik doğrulama için Exchange ActiveSync desteği yapılandırdığınızda bu hello yaygın sorunlardır.

### <a name="exchange-powershell-issue"></a>Exchange PowerShell sorunu

Merhaba görürseniz "**parametre adı 'PerTenantSwitchToESTSEnabled' ile eşleşen bir parametre bulunamıyor\.**" Merhaba'nı çalıştırdığınızda hata `Set-OrganizationConfig` Exchange PowerShell komutu, Microsoft Support başvurun.

### <a name="exchange-activesync-not-working"></a>Exchange ActiveSync çalışmıyor

Merhaba yapılandırma bazı zaman tootake etkinleşir - hello süre ortamınıza bağlıdır. Uzun bir süredir Hello durum devam ederse, Microsoft Support başvurun.

## <a name="collecting-pass-through-authentication-agent-logs"></a>Toplama doğrudan kimlik doğrulama Aracısı günlükleri

Sorunu olabilirsiniz Hello türüne bağlı olarak farklı yerlerde toolook için doğrudan kimlik doğrulama Aracısı günlüklerini gerekir.

### <a name="authentication-agent-event-logs"></a>Kimlik Doğrulama Aracısı olay günlükleri

Kimlik Doğrulama Aracısı toohello ilgili hatalarla ilgili için hello hello sunucusundaki Uygulama Olay Görüntüleyicisi'ni açın ve altında denetleyin **uygulama ve hizmet Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.

Ayrıntılı analizler için hello "Oturum" günlüğünü etkinleştirin. Merhaba kimlik doğrulama Aracısı, bu günlüğü normal işlemler sırasında etkin ile çalıştırma; yalnızca sorun giderme için kullanın. Merhaba günlük yeniden devre dışı bırakıldıktan sonra hello günlük içeriği yalnızca görünür.

### <a name="detailed-trace-logs"></a>Ayrıntılı izleme günlükleri

İzleme günlüklerini arayın tootroubleshoot kullanıcı oturum açma hatalarının **%programdata%\Microsoft\Azure AD Connect kimlik doğrulama Agent\Trace\\**. Bu günlükler neden bir belirli bir kullanıcı oturum açma hello doğrudan kimlik doğrulama özelliğini kullanarak başarısız nedenleri. Bu hatalar da hello önceki gösterilen eşlenen toohello oturum açma hatası nedenleri [tablo](#sign-in-failure-reasons-on-the-Azure-portal). Günlük girişi örneğidir aşağıdadır:

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

Merhaba komut istemi ve çalışan hello komutu aşağıdaki açarak hello hatanın (örnek önceki hello içinde ' 1328') açıklayıcı ayrıntılarını alabilirsiniz (Not: günlüklerinizi içinde gördüğünüz hello gerçek hata numarası '1328' yerine):

`Net helpmsg 1328`

![Doğrudan Kimlik Doğrulama](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a>Etki alanı denetleyicisi

Denetim günlüğü etkinleştirilirse, etki alanı denetleyicileriniz güvenlik günlükleri hello ek bilgiler bulunabilir. Doğrudan kimlik doğrulama aracı tarafından gönderilen bir basit yol tooquery oturum açma istekleri aşağıdaki gibidir:

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a>Performans İzleyicisi sayaçları

Başka bir şekilde toomonitor kimlik doğrulama Aracısı tootrack belirli Performans İzleyicisi sayaçları hello kimlik doğrulama Aracısı yüklendiği her sunucuda ' dir. Genel sayaçlar aşağıdaki kullanım hello (**# PTA kimlik doğrulamaları**, **#PTA kimlik doğrulamaları başarısız** ve **#PTA başarılı kimlik doğrulamalarını**) ve hata sayaçları (**# PTA kimlik doğrulama hataları**):

![Doğrudan kimlik doğrulama Performans İzleyicisi sayaçları](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
>Doğrudan kimlik doğrulama birden çok kimlik doğrulama aracı kullanarak yüksek kullanılabilirlik sağlar ve _değil_ Yük Dengeleme. Yapılandırmanıza bağlı olarak _değil_ tüm kimlik doğrulama Aracısı kabaca alma _eşit_ isteklerinin sayısı. Belirli bir kimlik doğrulama Aracısı hiçbir trafik hiç alır mümkündür.

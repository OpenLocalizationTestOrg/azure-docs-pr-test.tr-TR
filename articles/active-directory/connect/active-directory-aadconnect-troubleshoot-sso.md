---
title: "Azure AD Connect: Sorunsuz çoklu oturum açma sorunlarını giderme | Microsoft Docs"
description: "Bu konuda açıklanmaktadır nasıl tootroubleshoot Azure Active Directory sorunsuz çoklu oturum açma (Azure AD sorunsuz SSO)."
services: active-directory
keywords: "Azure AD, SSO, gerekli bileşenleri yükleme Active Directory, Azure AD Connect nedir çoklu oturum açma"
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
ms.openlocfilehash: f1c1c11522f22d5bc742c126fff483c5b06e1f06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a>Azure Active Directory sorunsuz çoklu oturum açma sorunlarını giderme

Bu makale size yardımcı olacak sorun giderme ilişkin Azure AD sorunsuz çoklu oturum açma ortak sorunlar hakkında bilgileri bulabilirsiniz.

## <a name="known-issues"></a>Bilinen sorunlar

- 30 veya daha fazla AD ormanına eşitleme, Azure AD Connect'i kullanarak sorunsuz SSO etkinleştiremezsiniz. Geçici bir çözüm olarak, şunları yapabilirsiniz [el ile etkinleştirmeniz](#manual-reset-of-azure-ad-seamless-sso) Kiracı hello özelliği.
- Ekleme Azure AD hizmeti URL'leri (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) toohello "Güvenilen siteler" bölgesine hello "yerel" Intranet yerine **kullanıcıların açmasını engelleyen**.
- Sorunsuz SSO Firefox ve Kenar çubuğunda özel gözatma modunda çalışmıyor. Ve ayrıca üzerinde Internet geliştirilmiş koruma modu etkinken Explorer.

>[!IMPORTANT]
>Biz son kenar tooinvestigate desteği müşteri bildirilen sorunlar geri.

## <a name="check-status-of-hello-feature"></a>Merhaba özelliği durumunu denetleme

Bu hello sorunsuz SSO özelliği olduğundan hala emin **etkin** kiracınız üzerinde. Giden toohello tarafından durumunu denetleyebilirsiniz **Azure AD Connect** hello dikey penceresinde [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com/).

![Azure Active Directory Yönetim Merkezi - Azure AD Connect dikey penceresi](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Oturum açma hatası nedeniyle'hello Azure Active Directory Yönetim Merkezi'nde

Toolook hello en sorunsuz SSO oturum açma kullanıcı sorunlarını giderme iyi toostart olan [oturum açma etkinliği raporu](../active-directory-reporting-activity-sign-ins.md) hello üzerinde [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com/).

![Azure Active Directory Yönetim Merkezi - oturum açma işlemleri raporu](./media/active-directory-aadconnect-sso/sso9.png)

Çok gidin**Azure Active Directory** -> **oturum açma işlemleri** hello üzerinde [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com/) ve belirli bir kullanıcının oturum açma etkinliği tıklatın. Merhaba Ara **oturum açmayı hata kodu** alan. Bu alan tooa hata nedeni ve çözümü aşağıdaki tablonun hello kullanarak Hello değeri eşleyin:

|Oturum açma hata kodu|Oturum açma hatası nedeni|Çözüm
| --- | --- | ---
| 81001 | Kullanıcının Kerberos anahtarı fazla büyük. | Kullanıcı Grup üyeliklerini azaltın ve yeniden deneyin.
| 81002 | %S toovalidate kullanıcının Kerberos bileti. | Bkz: [denetim listesi sorun giderme](#troubleshooting-checklist).
| 81003 | %S toovalidate kullanıcının Kerberos bileti. | Bkz: [denetim listesi sorun giderme](#troubleshooting-checklist).
| 81004 | Kerberos kimlik doğrulaması girişimi başarısız oldu. | Bkz: [denetim listesi sorun giderme](#troubleshooting-checklist).
| 81008 | %S toovalidate kullanıcının Kerberos bileti. | Bkz: [denetim listesi sorun giderme](#troubleshooting-checklist).
| 81009 | "Oluşturulamıyor toovalidate kullanıcının Kerberos bileti. | Bkz: [denetim listesi sorun giderme](#troubleshooting-checklist).
| 81010 | Merhaba kullanıcının Kerberos anahtarının süresi doldu veya geçersiz olduğu için sorunsuz SSO başarısız oldu. | Kullanıcı etki alanına katılmış bir CİHAZDAN Kurumsal ağınızdaki içinde toosign gerekir.
| 81011 | Merhaba kullanıcının Kerberos bileti içindeki bilgileri temel oluşturulamıyor toofind kullanıcı nesnesi. | Azure AD Connect toosynchronize kullanıcı bilgileri Azure AD'ye kullanın.
| 81012 | toosign tooAzure AD içinde çalışan hello kullanıcının hello cihazda imzalı hello kullanıcı farklıdır. | Farklı bir CİHAZDAN oturum açın.
| 81013 | Merhaba kullanıcının Kerberos bileti içindeki bilgileri temel oluşturulamıyor toofind kullanıcı nesnesi. |Azure AD Connect toosynchronize kullanıcı bilgileri Azure AD'ye kullanın. 

## <a name="troubleshooting-checklist"></a>Sorun giderme denetim listesi

Denetim listesi tootroubleshoot sorunsuz SSO sorunları aşağıdaki hello kullan:

- Merhaba sorunsuz SSO Özelliği Azure AD Connect etkin olup olmadığını denetleyin. Merhaba özelliği (örneğin, nedeniyle engellenen tooa bağlantı noktası) etkinleştiremezsiniz tüm hello sahip olun [ön koşullar](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) yerinde.
- Her iki bu Azure AD URL'leri (https://autologon.microsoftazuread-sso.com ve https://aadg.windows.net.nsatc.net) hello kullanıcının Intranet bölgesi ayarlarının bir parçası olup olmadığını denetleyin.
- Merhaba Kurumsal cihaz etki alanına katılmış toohello AD alanı olduğundan emin olun.
- Merhaba kullanıcı toohello aygıtta bir AD etki alanı hesabı kullanarak oturum emin olun.
- Merhaba kullanıcı hesabının sorunsuz SSO burada bırakıldı bir AD ormandan kurulduğundan emin olun.
- Hello aygıtın hello şirket ağında bağlandığından emin olun.
- Merhaba cihazın zaman hello Active Directory'nin ve hello etki alanı denetleyicileri zamanı ile eşitlenir ve beş dakikalık olduğundan emin olun.
- Hello kullanarak hello cihazda mevcut Kerberos anahtarları listesinde **klist** bir komut isteminden komutu. Bilet Merhaba verilen varsa denetleyin `AZUREADSSOACCT` bilgisayar hesabı. Kullanıcıların Kerberos biletleri için 12 saat genellikle geçerlidir. Active Directory'de farklı ayarlara sahip olabilir.
- Mevcut Kerberos anahtarları hello kullanarak hello aygıttan Temizleme **klist Temizleme** komut ve yeniden deneyin.
- toodetermine JavaScript ile ilgili bir sorun varsa ("Geliştirici Araçları" altında) hello tarayıcının hello konsol günlüklerini inceleyin.
- Gözden geçirme hello [etki alanı denetleyicisi](#domain-controller-logs) de.

### <a name="domain-controller-logs"></a>Etki alanı denetleyicisi

Ardından etki alanı denetleyicinizde Başarı Denetimi etkinse, sorunsuz SSO kullanarak kullanıcının oturum açtığı her zaman bir güvenlik girişi hello olay günlüğüne kaydedilir. Sorgu aşağıdaki hello kullanarak bu güvenlik olaylarını Bul (olayını arayın **4769** hello bilgisayar hesabıyla ilişkilendirilmiş **AzureADSSOAcc$**):

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-hello-feature"></a>Merhaba özelliğinin elle sıfırlama

Sorun giderme işe yaramazsa, Kiracı'hello özelliğini el ile sıfırlayabilirsiniz. Azure AD Connect çalıştırdığınız hello şirket içi sunucusunda aşağıdaki adımları izleyin:

### <a name="step-1-import-hello-seamless-sso-powershell-module"></a>1. adım: hello sorunsuz SSO PowerShell modülünü içeri aktarın

1. İlk olarak, indirme ve yükleme hello [Microsoft Online Services oturum açma Yardımcısı](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Ardından yükleyip hello [64-bit Windows PowerShell için Azure Active Directory Modülü](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Toohello gidin `%programfiles%\Microsoft Azure Active Directory Connect` klasör.
4. Bu komutu kullanarak içeri aktarma hello sorunsuz SSO PowerShell Modülü: `Import-Module .\AzureADSSO.psd1`.

### <a name="step-2-get-hello-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a>2. adım: AD ormanına sorunsuz SSO etkinleştirildiği hello listesini al

1. PowerShell'i yönetici olarak çalıştırın. PowerShell'de, çağrı `New-AzureADSSOAuthenticationContext`. İstendiğinde, kiracının genel Yöneticisi kimlik bilgilerini girin.
2. Çağrı `Get-AzureADSSOStatus`. Bu komut, bu özellik etkinleştirildiği üzerinde AD ormanına (Merhaba "etki alanları" listesi bakın) listesi hello sağlar.

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a>3. adım: Bunu üzerinde oluşturulduğuna her AD ormanı için sorunsuz SSO devre dışı bırak

1. Çağrı `$creds = Get-Credential`. İstendiğinde, AD ormanındaki Hello hedeflenen hello etki alanı yönetici kimlik bilgilerini girin.
2. Çağrı `Disable-AzureADSSOForest -OnPremCredentials $creds`. Bu komut hello kaldırır `AZUREADSSOACCT` hello bilgisayar hesabından şirket içi etki alanı denetleyicisi için bu belirli AD orman.
3. Merhaba özelliği ayarladığınız her bir AD orman için adımları önceki hello yineleyin.

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a>4. adım: Her bir AD orman için sorunsuz SSO etkinleştir

1. Çağrı `Enable-AzureADSSOForest`. İstendiğinde, AD ormanındaki Hello hedeflenen hello etki alanı yönetici kimlik bilgilerini girin.
2. Adımları tooset hello özelliği yedeklemek istediğiniz her bir AD orman için önceki hello yineleyin.

### <a name="step-5-enable-hello-feature-on-your-tenant"></a>5. Adım. Kiracı Hello özelliğini etkinleştir

Çağrı `Enable-AzureADSSO` hello adresindeki "true" yazın `Enable: ` komut istemi tooturn kiracınızda hello özelliği.

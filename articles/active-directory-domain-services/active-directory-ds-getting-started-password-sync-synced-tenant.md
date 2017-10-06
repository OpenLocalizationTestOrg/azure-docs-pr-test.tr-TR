---
title: "Azure AD Domain Services: Parola eşitlemeyi etkinleştirme | Microsoft Docs"
description: "Azure Active Directory Etki Alanı Hizmetleri ile çalışmaya başlama"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Parola Eşitleme tooAzure Active Directory etki alanı Hizmetleri'ni etkinleştirme
Önceki görevlerde Azure Active Directory (Azure AD) kiracınız için Azure Active Directory Domain Services hizmetini etkinleştirdiniz. Merhaba sonraki kimlik bilgisi karmalarını tooenable eşitlenmesi için NT LAN Yöneticisi (NTLM) ve Kerberos kimlik doğrulaması tooAzure AD etki alanı Hizmetleri gerekli bir görevdir. Kimlik bilgisi eşitlemesini ayarladıktan sonra kullanıcılar toohello yönetilen etki alanında Kurumsal kimlik ile oturum açabilir.

Merhaba adımlar, Azure AD Connect kullanarak şirket içi dizininizden eşitlenen yalnızca bulut kullanıcı hesapları vs kullanıcı hesapları için farklıdır. Azure AD kiracınıza bileşimini varsa ve yalnızca kullanıcılar, şirket içi bulut AD, her iki adımın tooperform gerekir.

<br>

> [!div class="op_single_selector"]
> * **Yalnızca bulut kullanıcı hesapları**: [yalnızca bulut kullanıcı tooyour yönetilen etki alanı hesapları için parola eşitleme](active-directory-ds-getting-started-password-sync.md)
> * **Şirket içi kullanıcı hesaplarını**: [, şirket içi eşitlenen kullanıcı hesapları için parola eşitleme AD tooyour yönetilen etki alanı](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a>Görev 5: şirket içi ile eşitlenen kullanıcı hesapları için parola eşitleme tooyour etki alanı yönetilen etkinleştirmek AD
A eşitlenmiş Azure AD kiracısı Azure AD Connect'i kullanarak, kuruluşunuzun şirket içi dizin toosynchronize ayarlanır. Varsayılan olarak, Azure AD Connect NTLM ve Kerberos kimlik bilgisi karmaları tooAzure AD eşitlenmez. toouse Azure AD etki alanı Hizmetleri, NTLM ve Kerberos kimlik doğrulaması için gerekli tooconfigure Azure AD Connect toosynchronize kimlik bilgisi karmalarını gerekir. Aşağıdaki adımları hello gerekli hello kimlik bilgisi karmalarını şirket içi dizin tooyour Azure AD kiracınıza gelen eşitleme etkinleştirin.

> [!NOTE]
> Kuruluşunuzun şirket içi dizininizden, sizin gerekir eşitlendikten kullanıcı hesapları varsa NTLM ve Kerberos sağlamalarının sipariş toouse hello yönetilen etki alanındaki eşitlemeyi etkinleştir. Tooyour Azure AD kiracısı Azure AD Connect kullanarak şirket içi dizininizde oluşturulduysa ve bir hesap eşitlenen bir eşitlenmiş kullanıcı hesabıdır.
>
>

### <a name="install-or-update-azure-ad-connect"></a>Azure AD Connect'i yükleme veya güncelleştirme 
En son önerilen hello yüklemek yayın Azure AD Connect bir etki alanına katılmış bilgisayar. Azure AD Connect kurulumunun var olan bir örneği varsa, tooupdate gerekir, Azure AD Connect toouse hello en son sürümü. Düzeltilmiş, sorunları/hatalar bilinen tooavoid olun her zaman hello Azure AD Connect'in en son sürümünü kullanın.

**[Azure AD Connect'i indirme](http://www.microsoft.com/download/details.aspx?id=47594)**

Önerilen sürüm: **1.1.553.0** - 27 Haziran 2017'da yayımlanmıştır.

> [!WARNING]
> Merhaba yüklemelisiniz en son Azure AD Connect tooenable hello eski parola kimlik bilgilerini (NTLM ve Kerberos kimlik doğrulaması için gerekli) toosynchronize tooyour Azure AD Kiracı sürümü önerilir. Bu işlev Azure AD Connect veya hello eski DirSync aracında ile önceki sürümlerde kullanılabilir değil.
>
>

Azure AD Connect'i yükleme yönergeleri hello aşağıdaki makalede - [Azure AD Connect ile çalışmaya başlama](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a>NTLM ve Kerberos kimlik bilgisi karmaları tooAzure AD eşitlemeyi etkinleştir
PowerShell Betiği tooforce tam parola eşitlemesini, her AD ağacında aşağıdaki hello yürütün ve tüm şirket içi kullanıcıların kimlik bilgisi karmaları toosync tooyour Azure AD Kiracı etkinleştirin. Bu komut dosyası için NTLM/Kerberos kimlik doğrulaması toobe eşitlenmiş tooyour Azure AD Kiracı gerekli hello kimlik bilgisi karmalarını sağlar.

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

Hello dizininizin boyutuna bağlı olarak (sayısı, kullanıcıların, grupların vb.), kimlik bilgisi eşitlemesine karmaları tooAzure AD zaman alır. Merhaba kimlik bilgisi karmalarını tooAzure AD kısa süre içinde eşitledikten sonra hello parolaları hello Azure AD etki alanı Hizmetleri tarafından yönetilen etki alanında kullanılabilir olur.

<br>

## <a name="related-content"></a>İlgili İçerik
* [Parola Eşitleme tooAAD bir yalnızca bulut Azure için etki alanı Hizmetleri'ni etkinleştirme AD dizini](active-directory-ds-getting-started-password-sync.md)
* [Azure AD Domain Services tarafından yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-domain.md)
* [Windows sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md)
* [Red Hat Enterprise Linux sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-rhel-linux-vm.md)

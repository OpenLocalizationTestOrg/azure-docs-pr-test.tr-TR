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
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="8617e-103">Parola Eşitleme tooAzure Active Directory etki alanı Hizmetleri'ni etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="8617e-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="8617e-104">Önceki görevlerde Azure Active Directory (Azure AD) kiracınız için Azure Active Directory Domain Services hizmetini etkinleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="8617e-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="8617e-105">Merhaba sonraki kimlik bilgisi karmalarını tooenable eşitlenmesi için NT LAN Yöneticisi (NTLM) ve Kerberos kimlik doğrulaması tooAzure AD etki alanı Hizmetleri gerekli bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="8617e-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="8617e-106">Kimlik bilgisi eşitlemesini ayarladıktan sonra kullanıcılar toohello yönetilen etki alanında Kurumsal kimlik ile oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="8617e-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="8617e-107">Merhaba adımlar, Azure AD Connect kullanarak şirket içi dizininizden eşitlenen yalnızca bulut kullanıcı hesapları vs kullanıcı hesapları için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="8617e-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="8617e-108">Azure AD kiracınıza bileşimini varsa ve yalnızca kullanıcılar, şirket içi bulut AD, her iki adımın tooperform gerekir.</span><span class="sxs-lookup"><span data-stu-id="8617e-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="8617e-109">**Yalnızca bulut kullanıcı hesapları**: [yalnızca bulut kullanıcı tooyour yönetilen etki alanı hesapları için parola eşitleme](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="8617e-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="8617e-110">**Şirket içi kullanıcı hesaplarını**: [, şirket içi eşitlenen kullanıcı hesapları için parola eşitleme AD tooyour yönetilen etki alanı](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="8617e-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="8617e-111">Görev 5: şirket içi ile eşitlenen kullanıcı hesapları için parola eşitleme tooyour etki alanı yönetilen etkinleştirmek AD</span><span class="sxs-lookup"><span data-stu-id="8617e-111">Task 5: enable password synchronization tooyour managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="8617e-112">A eşitlenmiş Azure AD kiracısı Azure AD Connect'i kullanarak, kuruluşunuzun şirket içi dizin toosynchronize ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8617e-112">A synced Azure AD tenant is set toosynchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="8617e-113">Varsayılan olarak, Azure AD Connect NTLM ve Kerberos kimlik bilgisi karmaları tooAzure AD eşitlenmez.</span><span class="sxs-lookup"><span data-stu-id="8617e-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes tooAzure AD.</span></span> <span data-ttu-id="8617e-114">toouse Azure AD etki alanı Hizmetleri, NTLM ve Kerberos kimlik doğrulaması için gerekli tooconfigure Azure AD Connect toosynchronize kimlik bilgisi karmalarını gerekir.</span><span class="sxs-lookup"><span data-stu-id="8617e-114">toouse Azure AD Domain Services, you need tooconfigure Azure AD Connect toosynchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="8617e-115">Aşağıdaki adımları hello gerekli hello kimlik bilgisi karmalarını şirket içi dizin tooyour Azure AD kiracınıza gelen eşitleme etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8617e-115">hello following steps enable synchronization of hello required credential hashes from your on-premises directory tooyour Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="8617e-116">Kuruluşunuzun şirket içi dizininizden, sizin gerekir eşitlendikten kullanıcı hesapları varsa NTLM ve Kerberos sağlamalarının sipariş toouse hello yönetilen etki alanındaki eşitlemeyi etkinleştir.</span><span class="sxs-lookup"><span data-stu-id="8617e-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order toouse hello managed domain.</span></span> <span data-ttu-id="8617e-117">Tooyour Azure AD kiracısı Azure AD Connect kullanarak şirket içi dizininizde oluşturulduysa ve bir hesap eşitlenen bir eşitlenmiş kullanıcı hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="8617e-117">A synced user account is an account that was created in your on-premises directory and is synchronized tooyour Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="8617e-118">Azure AD Connect'i yükleme veya güncelleştirme </span><span class="sxs-lookup"><span data-stu-id="8617e-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="8617e-119">En son önerilen hello yüklemek yayın Azure AD Connect bir etki alanına katılmış bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="8617e-119">Install hello latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="8617e-120">Azure AD Connect kurulumunun var olan bir örneği varsa, tooupdate gerekir, Azure AD Connect toouse hello en son sürümü.</span><span class="sxs-lookup"><span data-stu-id="8617e-120">If you have an existing instance of Azure AD Connect setup, you need tooupdate it toouse hello latest version of Azure AD Connect.</span></span> <span data-ttu-id="8617e-121">Düzeltilmiş, sorunları/hatalar bilinen tooavoid olun her zaman hello Azure AD Connect'in en son sürümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="8617e-121">tooavoid known issues/bugs that may have already been fixed, ensure you always use hello latest version of Azure AD Connect.</span></span>

<span data-ttu-id="8617e-122">**[Azure AD Connect'i indirme](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="8617e-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="8617e-123">Önerilen sürüm: **1.1.553.0** - 27 Haziran 2017'da yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8617e-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="8617e-124">Merhaba yüklemelisiniz en son Azure AD Connect tooenable hello eski parola kimlik bilgilerini (NTLM ve Kerberos kimlik doğrulaması için gerekli) toosynchronize tooyour Azure AD Kiracı sürümü önerilir.</span><span class="sxs-lookup"><span data-stu-id="8617e-124">You MUST install hello latest recommended release of Azure AD Connect tooenable hello legacy password credentials (required for NTLM and Kerberos authentication) toosynchronize tooyour Azure AD tenant.</span></span> <span data-ttu-id="8617e-125">Bu işlev Azure AD Connect veya hello eski DirSync aracında ile önceki sürümlerde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="8617e-125">This functionality is not available in prior releases of Azure AD Connect or with hello legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="8617e-126">Azure AD Connect'i yükleme yönergeleri hello aşağıdaki makalede - [Azure AD Connect ile çalışmaya başlama](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="8617e-126">Installation instructions for Azure AD Connect are available in hello following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a><span data-ttu-id="8617e-127">NTLM ve Kerberos kimlik bilgisi karmaları tooAzure AD eşitlemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="8617e-127">Enable synchronization of NTLM and Kerberos credential hashes tooAzure AD</span></span>
<span data-ttu-id="8617e-128">PowerShell Betiği tooforce tam parola eşitlemesini, her AD ağacında aşağıdaki hello yürütün ve tüm şirket içi kullanıcıların kimlik bilgisi karmaları toosync tooyour Azure AD Kiracı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8617e-128">Execute hello following PowerShell script on each AD forest, tooforce full password synchronization, and enable all on-premises users’ credential hashes toosync tooyour Azure AD tenant.</span></span> <span data-ttu-id="8617e-129">Bu komut dosyası için NTLM/Kerberos kimlik doğrulaması toobe eşitlenmiş tooyour Azure AD Kiracı gerekli hello kimlik bilgisi karmalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8617e-129">This script enables hello credential hashes required for NTLM/Kerberos authentication toobe synchronized tooyour Azure AD tenant.</span></span>

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

<span data-ttu-id="8617e-130">Hello dizininizin boyutuna bağlı olarak (sayısı, kullanıcıların, grupların vb.), kimlik bilgisi eşitlemesine karmaları tooAzure AD zaman alır.</span><span class="sxs-lookup"><span data-stu-id="8617e-130">Depending on hello size of your directory (number of users, groups etc.), synchronization of credential hashes tooAzure AD takes time.</span></span> <span data-ttu-id="8617e-131">Merhaba kimlik bilgisi karmalarını tooAzure AD kısa süre içinde eşitledikten sonra hello parolaları hello Azure AD etki alanı Hizmetleri tarafından yönetilen etki alanında kullanılabilir olur.</span><span class="sxs-lookup"><span data-stu-id="8617e-131">hello passwords will be usable on hello Azure AD Domain Services managed domain shortly after hello credential hashes have synchronized tooAzure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="8617e-132">İlgili İçerik</span><span class="sxs-lookup"><span data-stu-id="8617e-132">Related Content</span></span>
* [<span data-ttu-id="8617e-133">Parola Eşitleme tooAAD bir yalnızca bulut Azure için etki alanı Hizmetleri'ni etkinleştirme AD dizini</span><span class="sxs-lookup"><span data-stu-id="8617e-133">Enable password synchronization tooAAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="8617e-134">Azure AD Domain Services tarafından yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="8617e-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="8617e-135">Windows sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl</span><span class="sxs-lookup"><span data-stu-id="8617e-135">Join a Windows virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="8617e-136">Red Hat Enterprise Linux sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl</span><span class="sxs-lookup"><span data-stu-id="8617e-136">Join a Red Hat Enterprise Linux virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)

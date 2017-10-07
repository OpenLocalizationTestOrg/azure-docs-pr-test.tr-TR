---
title: "Office 365 bağlı olan taraf güveni için aaaChange imza karma algoritmasını | Microsoft Docs"
description: "Bu sayfa, Office 365 ile bir federasyon güveni için SHA algoritma değiştirmek için yönergeler sağlar"
keywords: "SHA1, SHA256, O365, Federasyon, aadconnect, adfs, ad fs, değişiklik sha, bağlı olan taraf güveni bir federasyon güveni"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a>Office 365 bağlı olan taraf güveni için imza karma algoritması değiştirme
## <a name="overview"></a>Genel Bakış
Active Directory Federasyon Hizmetleri (AD FS) ile değiştirilmemesi kendi belirteçleri tooMicrosoft Azure Active Directory tooensure imzalar. Bu imza SHA1 veya SHA256 dayalı olabilir. Azure Active Directory şimdi SHA256 algoritmasını ile imzalanmış belirteçleri destekler ve hello belirteç imzalama algoritması tooSHA256 hello yüksek düzeyde güvenlik için ayarlanması önerilir. Bu makalede, tooset hello belirteç imzalama algoritması toohello SHA256 düzeyi daha güvenli hello adımları açıklanmaktadır.

>[!NOTE]
>Microsoft, SHA1'den daha güvenlidir, ancak desteklenen bir seçenek SHA1 kalıyor gibi Belirteçleri imzalamak için hello algoritması olarak SHA256 kullanımını önerir.

## <a name="change-hello-token-signing-algorithm"></a>Değişiklik hello belirteç imzalama algoritması
Merhaba imza algoritması hello iki işlem aşağıdaki biriyle ayarladıktan sonra AD FS bağlı olan taraf güveni SHA256 ile Office 365 için hello belirteçlerini imzalar. Ek yapılandırma değişiklikleri toomake gerekmez ve bu değişiklik, özelliği tooaccess Office 365 veya diğer Azure AD uygulamaları herhangi bir etkisi yoktur.

### <a name="ad-fs-management-console"></a>AD FS Yönetim Konsolu
1. Merhaba birincil AD FS sunucusunda Hello AD FS Yönetim Konsolu'nu açın.
2. Merhaba AD FS düğümünü genişletin ve tıklatın **bağlı olan taraf güvenleri**.
3. Office 365/Azure bağlı olan taraf güveniniz sağ tıklatıp **özellikleri**.
4. Select hello **Gelişmiş** sekmesi ve select hello güvenli karma algoritması SHA256.
5. **Tamam** düğmesine tıklayın.

![SHA256 imzalama algoritmasını--MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a>AD FS PowerShell cmdlet'leri
1. Herhangi bir AD FS sunucusu üzerinde PowerShell'i yönetici ayrıcalıklarıyla açın.
2. Set hello güvenli karma algoritması'hello kullanarak **Set-AdfsRelyingPartyTrust** cmdlet'i.
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a>Ayrıca okuyun
* [Azure AD Connect ile Office 365 güven onarın](connect/active-directory-aadconnect-federation-management.md#repairthetrust)


---
title: "Azure Active Directory etki alanı Hizmetleri: Kısıtlı kerberos temsilcisi etkinleştirme | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri yönetilen etki alanlarında kerberos Kısıtlı temsilci etkinleştir"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2017
ms.author: maheshu
ms.openlocfilehash: b09c725609fe866b0c9ba2f5b5789e00f808b1ab
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a>Yönetilen bir etki alanında Kerberos Kısıtlı temsilci (KCD) yapılandırma
Birçok uygulama, kullanıcının bağlamında kaynaklara erişim izni gerekir. Active Directory bu kullanım örneği sağlayan Kerberos temsilcisi olarak adlandırılan bir mekanizma destekler. Ayrıca, böylece yalnızca belirli kaynaklara kullanıcı bağlamında erişilebilir temsilci kısıtlayabilirsiniz. Bunlar daha güvenli bir şekilde kilitlendiğini beri azure AD etki alanı Hizmetleri yönetilen etki alanları geleneksel Active Directory etki alanından farklı.

Bu makale bir Azure AD etki alanı Hizmetleri yönetilen etki alanında kısıtlı Kerberos temsilcisi yapılandırma gösterilmektedir.

## <a name="kerberos-constrained-delegation-kcd"></a>Kerberos Kısıtlı temsilci (KCD)
Kerberos temsilcisi başka bir güvenlik sorumlusu (örneğin, bir kullanıcı) kaynaklara erişmek için kimliğine bürünmek için bir hesap sağlar. Bir kullanıcı bağlamında bir arka uç web API'si erişen bir web uygulaması göz önünde bulundurun. Bu örnekte, (bir hizmet hesabı veya bilgisayar/makine hesabının bağlamında çalışır) web uygulaması (arka uç web API'si) kaynağa erişilirken kullanıcı temsil eder. Kerberos temsilcisi güvenli olduğu özellikleri alınırken hesabı kullanıcı bağlamında erişebildiği kaynakları kısıtlamaz.

Kerberos Kısıtlı temsilci (KCD), belirtilen sunucunun kullanıcı adına işlem yapabileceği Hizmetleri/kaynakları kısıtlar. Geleneksel KCD bir hizmet için bir etki alanı hesabı yapılandırmak için etki alanı yöneticisi ayrıcalıkları gerektirir ve hesabı tek bir etki alanına kısıtlar.

Geleneksel KCD de ilişkili bazı sorunlar vardır. Etki alanı yöneticisi hesabı tabanlı KCD hizmet için yapılandırılmışsa önceki işletim sistemlerinde hizmet yöneticisinin, sahibi kaynak Hizmetleri temsilci hangi ön uç hizmetlerin bilmesinin yolu yoktu. Ve bir kaynak hizmeti temsilci seçebilecek tüm ön uç Hizmetleri olası bir saldırı noktası gösterilir. Bir ön uç hizmeti barındırılan bir sunucunun güvenliği aşılırsa ve kaynak Hizmetleri temsilci seçmek üzere yapılandırılmışsa, kaynak hizmetlerin de güvenliği aşılabilirdi.

> [!NOTE]
> Bir Azure AD etki alanı Hizmetleri tarafından yönetilen etki alanında, etki alanı yönetici ayrıcalıklarına sahip değil. Bu nedenle, **geleneksel KCD yönetilen bir etki alanında yapılandırılamaz**. Kaynak tabanlı KCD, bu makalede anlatıldığı gibi kullanın. Bu düzenek ayrıca daha güvenlidir.
>
>

## <a name="resource-based-kcd"></a>KDC kaynak tabanlı
Windows Server 2012'den başlayarak, hizmet yöneticileri, kendi hizmet için kısıtlı temsilci yapılandırma yeteneğini elde edilir. Bu modelde, arka uç Hizmeti Yöneticisi izin verebilir veya KCD kullanarak özel ön uç Hizmetleri reddet. Bu model olarak bilinen **kaynak tabanlı KCD**.

Kaynak tabanlı KCD, PowerShell kullanılarak yapılandırılır. Kullandığınız `Set-ADComputer` veya `Set-ADUser` özellikleri alınırken hesap bir bilgisayar hesabı veya bir kullanıcı hesabı/hizmet hesabı olup olmamasına bağlı olarak cmdlet'leri.

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a>Yönetilen bir etki alanında bilgisayar hesabı için kaynak tabanlı KCD yapılandırın
Bilgisayarda çalışan bir web uygulaması olduğunu varsayın ' contoso100-webapp.contoso100.com'. Kaynağa erişim gereken (üzerinde çalışan bir web API ' contoso100-api.contoso100.com') etki alanı kullanıcıları bağlamında. İşte nasıl kaynak tabanlı KCD bu senaryo için ayarlamanız.

```powershell
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a>Yönetilen bir etki alanında kaynak tabanlı KCD bir kullanıcı hesabı yapılandırın
Hizmet hesabı 'appsvc' olarak çalışan bir web uygulaması olduğu varsayılır ve etki alanı kullanıcıları bağlamında (bir hizmet hesabı - 'backendsvc' olarak çalışan bir web API) kaynağa erişmek gerekiyor. İşte nasıl kaynak tabanlı KCD bu senaryo için ayarlamanız.

```powershell
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a>İlgili İçerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Kerberos kısıtlanmış Temsile genel bakış](https://technet.microsoft.com/library/jj553400.aspx)

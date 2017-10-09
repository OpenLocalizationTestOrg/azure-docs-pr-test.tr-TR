---
title: "Azure Active Directory etki alanı Hizmetleri: Kısıtlı kerberos temsilcisi etkinleştirme | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri yönetilen etki alanlarında kerberos Kısıtlı temsilci etkinleştir"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a>Yönetilen bir etki alanında kerberos Kısıtlı temsilci (KCD) yapılandırma
Birçok uygulama tooaccess kaynakları hello kullanıcının hello bağlamında gerekir. Active Directory bu kullanım örneği sağlayan Kerberos temsilcisi olarak adlandırılan bir mekanizma destekler. Ayrıca, böylece yalnızca belirli kaynaklara hello hello kullanıcının bağlamında erişilebilir temsilci kısıtlayabilirsiniz. Bunlar daha güvenli bir şekilde kilitlendiğini beri azure AD etki alanı Hizmetleri yönetilen etki alanları geleneksel Active Directory etki alanından farklı.

Bu makalede nasıl tooconfigure kerberos kısıtlı temsilcisi Azure AD etki alanı Hizmetleri yönetilen etki alanı gösterilmektedir.

## <a name="kerberos-constrained-delegation-kcd"></a>Kerberos Kısıtlı temsilci (KCD)
Kerberos temsilcisi bir hesap tooimpersonate başka bir güvenlik sorumlusu (örneğin, bir kullanıcı) tooaccess kaynakları sağlar. Bir kullanıcının hello bağlamında arka uç web API'si erişen bir web uygulaması göz önünde bulundurun. Bu örnekte, hello web uygulaması (bir hizmet hesabı veya bilgisayar/makine hesabının hello bağlamında çalışır) hello kullanıcı hello kaynak (arka uç web API'si) erişirken temsil eder. Kerberos temsilcisi güvenli olduğu hesabı kimliğine bürünme kaynakları hello hello hello kullanıcının bağlamında erişebilirsiniz hello kısıtlamaz.

Kerberos Kısıtlı temsilci (KCD) Hizmetleri/kaynakları toowhich hello belirtilen sunucu hello bir kullanıcı adına işlem yapabileceği hello kısıtlar. Geleneksel KCD, bir hizmet için etki alanı yönetici ayrıcalıkları tooconfigure bir etki alanı hesabı gerektirir ve hello hesabı tooa tek etki alanı kısıtlar.

Geleneksel KCD de ilişkili bazı sorunlar vardır. Önceki işletim hello etki alanı yöneticisi hello hizmet yapılandırdığınız yerde sistemlerinde, hello hizmet yöneticisinin, sahibi toohello kaynak Hizmetleri hangi ön uç hizmetlerin temsilci hiçbir kullanışlı bir yol tooknow vardı. Ve tooa kaynak hizmeti temsilci seçebilecek tüm ön uç Hizmetleri olası bir saldırı noktası gösterilir. Bir ön uç hizmeti barındırılan bir sunucunun güvenliği aşılırsa ve yapılandırılmış toodelegate tooresource Hizmetleri başarısız olursa hello kaynak hizmetlerin de güvenliği aşılabilirdi.

> [!NOTE]
> Bir Azure AD etki alanı Hizmetleri tarafından yönetilen etki alanında, etki alanı yönetici ayrıcalıklarına sahip değil. Bu nedenle, **geleneksel KCD yönetilen bir etki alanında yapılandırılamaz**. Kaynak tabanlı KCD, bu makalede anlatıldığı gibi kullanın. Bu düzenek ayrıca daha güvenlidir.
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a>Kaynak tabanlı kerberos Kısıtlanmış temsilci seçme
Windows Server 2012 R2 ve Windows Server 2012, hello özelliği tooconfigure Kısıtlı temsilci hello hizmeti için hello etki alanı yönetici toohello Hizmet Yöneticisi'nden aktarıldı. Bu şekilde, hello arka uç Hizmeti Yöneticisi izin verebilir veya ön uç Hizmetleri reddet. Bu model olarak bilinen **kaynak tabanlı kerberos Kısıtlanmış temsilci seçimini**.

Kaynak tabanlı KCD, PowerShell kullanılarak yapılandırılır. Merhaba Set-ADComputer ya da hesabı kimliğine bürünme hello bilgisayar hesabı veya bir kullanıcı hesabı/hizmet hesabı olup olmamasına bağlı olarak, Set-ADUser cmdlet'leri kullanın.

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a>Yönetilen bir etki alanında bilgisayar hesabı için kaynak tabanlı KCD yapılandırın
Merhaba bilgisayarda çalışan bir web uygulaması olduğunu varsayın ' contoso100-webapp.contoso100.com'. Tooaccess hello kaynak gerekir (üzerinde çalışan bir web API ' contoso100-api.contoso100.com') etki alanı kullanıcıları hello bağlamında. İşte nasıl kaynak tabanlı KCD bu senaryo için ayarlamanız.

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a>Yönetilen bir etki alanında kaynak tabanlı KCD bir kullanıcı hesabı yapılandırın
Hizmet hesabı 'appsvc' olarak çalışan bir web uygulamanız ve tooaccess hello kaynak etki alanı kullanıcıları hello bağlamında (bir hizmet hesabı - 'backendsvc' olarak çalışan bir web API) gerekir varsayalım. İşte nasıl kaynak tabanlı KCD bu senaryo için ayarlamanız.

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a>İlgili İçerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Kerberos kısıtlanmış Temsile genel bakış](https://technet.microsoft.com/library/jj553400.aspx)

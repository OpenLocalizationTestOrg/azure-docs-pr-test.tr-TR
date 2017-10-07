---
title: "aaaAzure AD Connect eşitleme hizmet özellikleri ve yapılandırma | Microsoft Docs"
description: "Azure AD Connect eşitleme hizmeti için hizmet tarafı özelliklerini açıklar."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a>Azure AD Connect eşitleme hizmeti özellikleri
Azure AD Connect eşitleme özelliği Hello iki bileşenden oluşur:

* adlı hello şirket içi bileşeni **Azure AD Connect eşitleme**, olarak da bilinir **eşitleme altyapısı**.
* Azure AD'de olarak da bilinen bulunan hello hizmet **Azure AD Connect eşitleme hizmeti**

Bu konuda aşağıdaki hello nasıl özellikleri açıklanmaktadır Merhaba, **Azure AD Connect eşitleme hizmeti** çalışma ve bunları Windows PowerShell kullanarak nasıl yapılandırabilirsiniz.

Bu ayarları hello tarafından yapılandırılan [Azure Active Directory için Windows PowerShell Modülü](http://aka.ms/aadposh). İndirin ve Azure AD Connect'ten ayrı olarak yükleyin. Bu konudaki belgelenen hello cmdlet'leri hello sunuldu [2016 Mart sürümünden (yapı 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1). Bu konudaki belgelenen hello cmdlet'leri varsa değil veya aynı sonucu sonra emin olun hello oluşturmaya hello en son sürümünü çalıştırın.

toosee hello çalıştırmak Azure AD dizininizi yapılandırmasında `Get-MsolDirSyncFeatures`.  
![Get-MsolDirSyncFeatures sonucu](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)

Bu ayarların çoğu, yalnızca Azure AD Connect tarafından değiştirilebilir.

Merhaba aşağıdaki ayarları tarafından yapılandırılabilir `Set-MsolDirSyncFeature`:

| DirSyncFeature | Açıklama |
| --- | --- |
| [EnableSoftMatchOnUpn](#userprincipalname-soft-match) |Nesneleri toojoin toplama tooprimary SMTP adresi userPrincipalName olanak tanır. |
| [SynchronizeUpnForManagedUsers](#synchronize-userprincipalname-updates) |Merhaba eşitleme altyapısı tooupdate hello userPrincipalName özniteliği, yönetilen ve lisanslı (Federasyon olmayan) kullanıcılar için sağlar. |

Bir özellik etkinleştirdikten sonra onu yeniden devre dışı bırakılamaz.

> [!NOTE]
> Özellik 24 Ağustos 2016'dan hello *yinelenen öznitelik dayanıklılık* yeni Azure için varsayılan olarak etkin AD dizinleri. Bu özellik ayrıca alındı ve olması bu tarihten önce oluşturulan dizinleri etkin. Dizininizi hakkında tooget bu özelliği etkin olduğunda, bir e-posta bildirimi alırsınız.
> 
> 

Merhaba aşağıdaki ayarları Azure AD Connect tarafından yapılandırılır ve tarafından değiştirilemez `Set-MsolDirSyncFeature`:

| DirSyncFeature | Açıklama |
| --- | --- |
| DeviceWriteback |[Azure AD Connect: cihaz geri yazma özelliğini etkinleştirme](active-directory-aadconnect-feature-device-writeback.md) |
| DirectoryExtensions |[Azure AD Connect eşitleme: dizin uzantıları](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency](#duplicate-attribute-resiliency) |Dışa aktarma sırasında hello nesnenin tamamı başarısız yerine başka bir nesnenin yinelemesi karantinaya bir öznitelik toobe sağlar. |
| PasswordSync |[Parola Eşitleme ile Azure AD Connect eşitleme uygulama](active-directory-aadconnectsync-implement-password-synchronization.md) |
| UnifiedGroupWriteback |[Önizleme: Grup geri yazma](active-directory-aadconnect-feature-preview.md#group-writeback) |
| UserWriteback |Şu anda desteklenmiyor. |

## <a name="duplicate-attribute-resiliency"></a>Yinelenen öznitelik dayanıklılık
Yinelenen UPN ile tooprovision başarısız yerine nesneleri / proxyAddresses, hello yinelenen öznitelik "karantinaya" ve geçici bir değeri atanır. Merhaba çakışma giderildikten sonra UPN hello geçici olan toohello doğru değer otomatik olarak değiştirildi. Daha fazla ayrıntı için bkz: [kimlik eşitleme ve yinelenen öznitelik dayanıklılık](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="userprincipalname-soft-match"></a>UserPrincipalName yumuşak eşleşmiyor
Bu özellik etkinleştirildiğinde, soft-match toplama toohello için UPN etkin [birincil SMTP adresi](https://support.microsoft.com/kb/2641663), her zaman etkin. Soft-kullanılan toomatch mevcut bulut kullanıcıları şirket içi kullanıcıları Azure AD'de eşleşmedir.

Gerekirse toomatch AD hesaplarıyla hello bulutta oluşturulan mevcut şirket içi ve Exchange Online kullanmıyorsanız, sonra bu özellik yararlı olur. Bu senaryoda, genellikle hello bulutta bir nedenle tooset hello SMTP özniteliği yok.

Bu özellik için varsayılan olarak yeni Azure AD dizinlerinden oluşturulur. Bu özellik, çalıştırarak etkin olup olmadığını görebilirsiniz:  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

Bu özellik, Azure AD dizini için etkin değilse, ardından onu çalıştırarak etkinleştirebilirsiniz:  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a>UserPrincipalName güncelleştirmelerini eşitleme
Bu koşulların her ikisi de doğruysa sürece tarihsel olarak, şirket içi hello eşitleme hizmeti kullanarak güncelleştirmeleri toohello UserPrincipalName özniteliği, engellendi:

* Merhaba kullanıcı (Federasyon olmayan) yönetilir.
* Merhaba kullanıcı bir lisans atanmadı.

Daha fazla ayrıntı için bkz: [kullanıcı Office 365, Azure veya Intune adları eşleşmiyor hello şirket içi UPN veya alternatif oturum açma kimliği](https://support.microsoft.com/kb/2523192).

Bu özelliği etkinleştirmek, değiştirilen şirket içi olduğunda ve Parola Eşitleme'yi kullanmaya hello eşitleme altyapısı tooupdate hello userPrincipalName sağlar. Federasyon kullanırsanız, bu özellik desteklenmiyor.

Bu özellik için varsayılan olarak yeni Azure AD dizinlerinden oluşturulur. Bu özellik, çalıştırarak etkin olup olmadığını görebilirsiniz:  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

Bu özellik, Azure AD dizini için etkin değilse, ardından onu çalıştırarak etkinleştirebilirsiniz:  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

Bu özellik etkinleştirildikten sonra varolan userPrincipalName değerleri olarak kalır-değil. Merhaba userPrincipalName özniteliği şirket içi sonraki değişiminde hello normal delta eşitleme kullanıcıları hello UPN güncelleştirir.  

## <a name="see-also"></a>Ayrıca bkz.
* [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).


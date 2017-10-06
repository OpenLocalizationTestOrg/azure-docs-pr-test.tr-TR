---
title: "Azure AD Connect: Otomatik yükseltme | Microsoft Docs"
description: "Bu konuda hello yerleşik Otomatik yükseltme Özelliği Azure AD Connect eşitleme açıklanmaktadır."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b395e8f-fa3c-4e55-be54-392dd303c472
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 70d15eb3adf7758d8a43d278157daa504e059a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-automatic-upgrade"></a>Azure AD Connect: Otomatik yükseltme
Bu özellik, (Şubat 2016 yayımlandı) yapı ile 1.1.105.0 sunulmuştur.

## <a name="overview"></a>Genel Bakış
Azure AD Connect yüklemenize her zaman toodate olmasını sağlama hiçbir zaman hello ile daha kolay **otomatik yükseltme** özelliği. Bu özellik express yüklemeleri için varsayılan olarak etkindir ve DirSync yükseltir. Yeni bir sürümü yayımlandığında, yükleme otomatik olarak yükseltilir.

Otomatik yükseltmeyi hello aşağıdaki için varsayılan olarak etkindir:

* Hızlı ayarlar yüklemesi ve DirSync yükseltmeleri.
* SQL Express LocalDB kullanımıyla, ne zaman hızlı ayarları kullanın olduğu. SQL Express ile DirSync de LocalDB kullanın.
* Merhaba AD hesabının hızlı ayarları ve DirSync tarafından oluşturulan hello varsayılan MSOL_ hesabıdır.
* 100. 000'den az nesneleri hello meta veri deposunda sahiptir.

Otomatik yükseltmeyi geçerli durumunu Hello hello PowerShell cmdlet'iyle görüntülenebilir `Get-ADSyncAutoUpgrade`. Aşağıdaki durumlar hello sahiptir:

| Durum | Açıklama |
| --- | --- |
| Etkin |Otomatik yükseltmeyi etkinleştirilir. |
| askıya alındı |Yalnızca Hello sistem tarafından ayarlayın. Merhaba artık uygun tooreceive otomatik yükseltme sistemidir. |
| Devre dışı |Otomatik yükseltmeyi devre dışı bırakılır. |

Arasında değiştirebileceğiniz **etkin** ve **devre dışı** ile `Set-ADSyncAutoUpgrade`. Merhaba sistem hello durumu ayarlamalısınız yalnızca **askıya**.

Otomatik yükseltmeyi hello Yükseltme Altyapısı için Azure AD Connect Health kullanıyor. Otomatik yükseltme toowork için proxy sunucunuzun içinde hello URL'leri açtıklarını emin olun **Azure AD Connect Health** açıklandığı gibi [Office 365 URL'leri ve IP adresi aralıkları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Merhaba, **Eşitleme Hizmeti Yöneticisi'ni** UI hello sunucu üzerinde çalışan sonra hello UI kapatılana kadar hello yükseltme askıya alınır.

## <a name="troubleshooting"></a>Sorun giderme
Connect yüklemenizi kendisini beklendiği gibi değil yükseltirseniz, bu adımları toofind nerede olabilir çıkışı izleyin.

İlk olarak, size hello çalıştı otomatik yükseltme toobe hello yeni bir sürüm yayımlanan ilk günü beklememeniz gerekir. Bir yükseltme yüklemenizi hemen yükselttiyseniz değil uyarıda olmayan şekilde denenmeden önce kasıtlı rastgele yoktur.

Bir şey değil sağ düşünüyorsanız, önce Çalıştır `Get-ADSyncAutoUpgrade` tooensure otomatik yükseltme etkindir.

Ardından, gerekli hello URL'lerin proxy ya da güvenlik duvarı açtığınızdan emin olun. Otomatik güncelleştirme hello açıklandığı gibi Azure AD Connect Health kullanarak [genel bakış](#overview). Bir proxy kullanıyorsanız, sistem durumu, yapılandırılmış toouse açıldı emin olun bir [proxy sunucusu](../connect-health/active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy). Ayrıca hello test [sistem durumu bağlantı](../connect-health/active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) tooAzure AD.

Merhaba bağlantı tooAzure doğrulandı AD ile Merhaba eventlogs içine zaman toolook olur. Merhaba Olay Görüntüleyicisi'ni başlatın ve hello arayın **uygulama** eventlog. Merhaba kaynağı için bir olay günlüğü filtresi ekleme **Azure AD Connect Yükseltmesi** ve hello olay kimliği aralığını **300 399**.  
![Otomatik yükseltme için olay günlüğü filtresi](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogfilter.png)  

Otomatik yükseltmeyi hello durumuyla ilişkili hello eventlogs şimdi görebilirsiniz.  
![Otomatik yükseltme için olay günlüğü filtresi](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogresult.png)  

Merhaba Sonuç kodu hello durumu genel bir bakış önekiyle sahiptir.

| Sonuç kodu öneki | Açıklama |
| --- | --- |
| Başarılı |Merhaba yükleme başarıyla yükseltildi. |
| UpgradeAborted |Geçici bir durum hello yükseltme durduruldu. Yeniden denenecek ve daha sonra başarılı hello beklenir. |
| UpgradeNotSupported |Merhaba sistem otomatik olarak yükseltilecek hello sistemin engelleme bir yapılandırmaya sahip. Merhaba durumunu değiştirme, ancak hello sistem el ile yükseltilmesi gereken hello beklenir, denenen toosee olacaktır. |

Burada, bulduğunuz hello en yaygın iletilerinin bir listesi verilmiştir. Tüm listelenmez, ancak hello sonucu iletisi temizleyin hangi hello sorun olması gerekir.

| Sonuç iletisi | Açıklama |
| --- | --- |
| **UpgradeAborted** | |
| UpgradeAbortedCouldNotSetUpgradeMarker |Toohello kayıt defteri yazılamadı. |
| UpgradeAbortedInsufficientDatabasePermissions |Merhaba yerleşik Yöneticiler grubunun izinleri toohello veritabanı yok. El ile bu sorunu Azure AD Connect tooaddress toohello en son sürümünü yükseltin. |
| UpgradeAbortedInsufficientDiskSpace |Bir yükseltme yeterli disk alanı toosupport yoktur. |
| UpgradeAbortedSecurityGroupsNotPresent |Sağlanamadı bulmak ve hello eşitleme altyapısı tarafından kullanılan tüm güvenlik gruplarını çözün. |
| UpgradeAbortedServiceCanNotBeStarted |Merhaba NT hizmeti **Microsoft Azure AD eşitleme** toostart başarısız oldu. |
| UpgradeAbortedServiceCanNotBeStopped |Merhaba NT hizmeti **Microsoft Azure AD eşitleme** toostop başarısız oldu. |
| UpgradeAbortedServiceIsNotRunning |Merhaba NT hizmeti **Microsoft Azure AD eşitleme** çalışmıyor. |
| UpgradeAbortedSyncCycleDisabled |Merhaba SyncCycle seçeneğinde hello [Zamanlayıcı](active-directory-aadconnectsync-feature-scheduler.md) devre dışı bırakıldı. |
| UpgradeAbortedSyncExeInUse |Merhaba [Eşitleme Hizmeti Yöneticisi kullanıcı Arabirimi](active-directory-aadconnectsync-service-manager-ui.md) hello sunucuda açılır. |
| UpgradeAbortedSyncOrConfigurationInProgress |Merhaba yükleme sihirbazını çalıştırma veya bir eşitleme hello Zamanlayıcı dışında zamanlanabilir. |
| **UpgradeNotSupported** | |
| UpgradeNotSupportedCustomizedSyncRules |Kendi özel kurallar toohello yapılandırma eklediniz. |
| UpgradeNotSupportedDeviceWritebackEnabled |Merhaba etkinleştirdiğiniz [cihaz geri yazma](active-directory-aadconnect-feature-device-writeback.md) özelliği. |
| UpgradeNotSupportedGroupWritebackEnabled |Merhaba etkinleştirdiğiniz [grup geri yazma](active-directory-aadconnect-feature-preview.md#group-writeback) özelliği. |
| UpgradeNotSupportedInvalidPersistedState |Merhaba yüklemesi hızlı ayarları veya DirSync yükseltme değil. |
| UpgradeNotSupportedMetaverseSizeExceeeded |100. 000'den fazla nesneleri hello meta veri deposunda sahiptir. |
| UpgradeNotSupportedMultiForestSetup |Bir ormandaki daha toomore bağlanırsınız. Hızlı Kurulum yalnızca tooone orman bağlanır. |
| UpgradeNotSupportedNonLocalDbInstall |Bir SQL Server Express LocalDB veritabanına kullanmıyorsunuz. |
| UpgradeNotSupportedNonMsolAccount |Merhaba [AD Bağlayıcısı hesabı](active-directory-aadconnect-accounts-permissions.md#active-directory-account) hello varsayılan MSOL_ hesabı artık değil. |
| UpgradeNotSupportedStagingModeEnabled |Merhaba server olarak ayarlanmış toobe [hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode). |
| UpgradeNotSupportedUserWritebackEnabled |Merhaba etkinleştirdiğiniz [kullanıcı geri yazma](active-directory-aadconnect-feature-preview.md#user-writeback) özelliği. |

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.

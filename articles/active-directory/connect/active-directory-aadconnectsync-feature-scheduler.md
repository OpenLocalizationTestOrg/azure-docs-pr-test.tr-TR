---
title: "Azure AD Connect eşitleme: Zamanlayıcı | Microsoft Docs"
description: "Bu konuda, Azure AD Connect eşitleme hello yerleşik Zamanlayıcı özelliği açıklanmaktadır."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a>Azure AD Connect eşitleme: Zamanlayıcı
Bu konu, Azure AD Connect eşitleme yerleşik zamanlayıcıda hello (paketini açıklar Eşitleme altyapısı).

Bu özellik, (Şubat 2016 yayımlandı) yapı ile 1.1.105.0 sunulmuştur.

## <a name="overview"></a>Genel Bakış
Azure AD Connect eşitleme bir Zamanlayıcı'yı kullanarak şirket içi dizininizde değişikliğinizin eşitleyin. İki Zamanlayıcı işlemleri, parola eşitleme için bir ve nesne/özniteliği eşitleme ve bakım görevleri için başka bir vardır. Bu konu hello ikinci kapsar.

Önceki sürümlerde hello Zamanlayıcı nesneleri ve öznitelikleri için dış toohello eşitleme altyapısı oluştu. Windows Görev Zamanlayıcısı'nı veya ayrı bir Windows hizmeti tootrigger hello eşitleme işlemi kullanılır. 1.1 sürümleri yerleşik toohello eşitleme altyapısı hello ve bazı özelleştirmeye izin Hello Zamanlayıcı iş. Merhaba yeni varsayılan eşitleme sıklığı 30 dakikadır.

Merhaba Zamanlayıcı iki görevlerden sorumlu şöyledir:

* **Eşitleme döngüsü**. Merhaba işlem tooimport, eşitleme ve dışarı aktarma değişiklikleri.
* **Bakım görevleri**. Anahtarları ve parola sıfırlama ve cihaz kaydı hizmeti (DRS) için sertifikaları yenileyin. Merhaba işlem günlüğünde eski girişleri temizlemek.

Hello Zamanlayıcı kendisi her zaman çalışıyor, ancak bir veya hiçbiri bu görevleri çalıştırmak yapılandırılmış tooonly olabilir. Toohave kendi eşitleme döngüsü işlemi gerekiyorsa, örneğin, size bu görevde hello Zamanlayıcı ancak hala çalışma hello bakım görevini devre dışı bırakabilirsiniz.

## <a name="scheduler-configuration"></a>Zamanlayıcı'yı yapılandırma
toosee geçerli yapılandırma ayarlarınızı tooPowerShell gidin ve Çalıştır `Get-ADSyncScheduler`. Size bu resimdeki şöyle gösterir:

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

Görürseniz **hello eşitleme komutu veya cmdlet kullanılabilir değil** bu cmdlet'ini çalıştırdığınızda, ardından hello PowerShell modülünün yüklenmedi. Azure AD Connect ile birlikte bir etki alanı denetleyicisinde veya hello varsayılan ayarlar daha yüksek PowerShell kısıtlama düzeylerine sahip bir sunucuda çalıştırırsanız bu sorun oluşabilir. Bu hatayı görürseniz, ardından çalıştırın `Import-Module ADSync` toomake hello cmdlet'i kullanılabilir.

* **AllowedSyncCycleInterval**. Azure AD tarafından izin verilen eşitleme döngüleri arasındaki zaman aralığını kısa Hello. Bu ayar daha sık eşitleyemez ve hala desteklenmiyor.
* **CurrentlyEffectiveSyncCycleInterval**. Merhaba zamanlamada şu anda etkin. Aynı değeri CustomizedSyncInterval hello sahiptir (varsa ayarlayın) AllowedSyncInterval daha sık değilse. 1.1.281 önce bir derleme kullanma CustomizedSyncCycleInterval değiştirirseniz, bu değişiklik bir sonraki eşitleme döngüsünden sonra etkinleşir. Derleme 1.1.281 hello değişikliği hemen etkinleşir.
* **CustomizedSyncCycleInterval**. Ardından, herhangi bir hello varsayılan sıklığından adresindeki hello Zamanlayıcı toorun 30 dakika istiyorsanız, bu ayarı yapılandırın. Yukarıdaki Hello resim içinde hello Zamanlayıcı toorun saatte yerine ayarlandı. Bu ayar tooa değeri AllowedSyncInterval değerinden daha düşük ayarlarsanız, ikinci hello kullanılır.
* **NextSyncCyclePolicyType**. Delta veya ilk. Sonraki çalıştırma hello yalnızca işlem delta değişiklikleri gerekir ya da Merhaba, sonraki çalıştırma tam yapması gerektiğini tanımlar içeri aktarma ve eşitleme. Merhaba ikinci de yeni veya değiştirilmiş kuralları yeniden işleyin.
* **NextSyncCycleStartTimeInUTC**. Sonraki hello Zamanlayıcı hello sonraki eşitleme döngüsü başlatır.
* **PurgeRunHistoryInterval**. Merhaba zaman işlem günlükleri tutulmalıdır. Bu günlükler hello Eşitleme Hizmeti Yöneticisi'nde incelenebilir. Merhaba varsayılan tookeep Bu günlükler 7 için gündür.
* **SyncCycleEnabled**. Merhaba Zamanlayıcı hello alma, eşitleme ve dışarı aktarma işlemlerini kendi işleminin bir parçası çalışıp çalışmadığını gösterir.
* **MaintenanceEnabled**. Merhaba bakım işlemi etkin olup olmadığını gösterir. Merhaba sertifikaları/anahtarları güncelleştirir ve işlem günlüğü temizler hello.
* **StagingModeEnabled**. Gösterir, [hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode) etkinleştirilir. Bu ayar etkinleştirilirse, çalışan hello dışarı bastırır ancak hala içeri aktarma ve eşitleme çalıştırın.
* **SchedulerSuspended**. Connect tarafından bir yükseltme tootemporarily blok hello Zamanlayıcı sırasında çalışmasını ayarlayın.

Bu ayarlarla bazılarını değiştirebilirsiniz `Set-ADSyncScheduler`. şu parametreler hello değiştirilebilir:

* CustomizedSyncCycleInterval
* NextSyncCyclePolicyType
* PurgeRunHistoryInterval
* SyncCycleEnabled
* MaintenanceEnabled

Azure AD Connect, önceki derlemelerde **isStagingModeEnabled** Set-ADSyncScheduler ortaya çıkmıştır. Bu **desteklenmeyen** tooset bu özellik. Merhaba özelliği **SchedulerSuspended** yalnızca Connect tarafından değiştirilmemelidir. Bu **desteklenmeyen** tooset bu doğrudan PowerShell ile.

Merhaba Zamanlayıcı yapılandırması Azure AD içinde depolanır. Hazırlama sunucunuz varsa, herhangi bir değişiklik hello birincil sunucuda (dışında IsStagingModeEnabled) sunucuyu hazırlama hello de etkiler.

### <a name="customizedsynccycleinterval"></a>CustomizedSyncCycleInterval
Sözdizimi:`Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`  
d - gün ss - saat, dd dakika, ss - saniye

Örnek:`Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`  
Değişiklikleri Zamanlayıcı toorun 3 saatte hello.

Örnek:`Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`  
Merhaba Zamanlayıcı toorun günlük değişiklik.

### <a name="disable-hello-scheduler"></a>Merhaba Zamanlayıcısı'nı devre dışı bırak  
Sonra toomake yapılandırma değişiklikleri gerekiyorsa, toodisable hello Zamanlayıcı istiyorsunuz. Örneğin, ne zaman, [filtrelemeyi yapılandırma](active-directory-aadconnectsync-configure-filtering.md) veya [toosynchronization kuralları değişiklik](active-directory-aadconnectsync-change-the-configuration.md).

çalıştırma toodisable hello Zamanlayıcı `Set-ADSyncScheduler -SyncCycleEnabled $false`.

![Merhaba Zamanlayıcısı'nı devre dışı bırak](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

Yaptığınız değişiklikler yaptığınızda, tooenable hello Zamanlayıcı'yla yeniden unutmadığınızdan `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="start-hello-scheduler"></a>Merhaba Zamanlayıcı'yı başlatma
Merhaba Zamanlayıcı 30 dakikada çalıştırın varsayılan olarak açıktır. Bazı durumlarda, bir eşitleme döngüsü Between hello toorun döngüleri zamanlanmış veya farklı bir tür toorun ihtiyacınız isteyebilirsiniz.

**Delta eşitleme döngüsü**  
Bir delta eşitleme döngüsü hello aşağıdaki adımları içerir:

* Tüm bağlayıcılar üzerinde delta içeri aktarma
* Tüm bağlayıcılar delta eşitleme
* Tüm bağlayıcıların dışarı aktarma

Bir Acil sahip olabilir toomanually ihtiyacınız neden olan hemen eşitlenmesi gereken değişikliği bir döngü çalıştırın. Toomanually gerekiyorsa bir döngü ardından Çalıştır Powershell'den çalıştırın `Start-ADSyncSyncCycle -PolicyType Delta`.

**Tam eşitleme döngüsü**  
Yapılandırma değişiklikleri izleyen hello birini yaptıysanız, bir tam eşitleme döngüsü toorun (paketini gerekir İlk):

* Bir kaynak dizinden alınan daha fazla nesne veya öznitelik toobe eklendi
* Toohello eşitleme kuralları yapılan değişiklikler
* Değiştirilen [filtreleme](active-directory-aadconnectsync-configure-filtering.md) nesneleri farklı sayıda dahil edilecek şekilde

Daha sonra bu değişikliklerden birini yaptıysanız, tam bir eşitleme döngüsü hello eşitleme altyapısı hello fırsat tooreconsolidate hello bağlayıcı alanları nedenle toorun gerekir. Bir tam eşitleme döngüsü hello aşağıdaki adımları içerir:

* Tüm bağlayıcılar üzerinde tam içeri aktarma
* Tüm bağlayıcılar üzerinde tam eşitleme
* Tüm bağlayıcıların dışarı aktarma

Tam eşitleme döngüsü, bir tooinitiate Çalıştır `Start-ADSyncSyncCycle -PolicyType Initial` PowerShell isteminde. Bu komut, bir tam eşitleme döngüsü başlatır.

## <a name="stop-hello-scheduler"></a>Merhaba Zamanlayıcı Durdur
Bir eşitleme döngüsü Hello Zamanlayıcı çalışıyorsa toostop gerekebilir. Merhaba Yükleme Sihirbazı'nı başlatın ve bu hatayı alırsınız, örneğin:

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

Bir eşitleme döngüsü çalıştırıldığında, yapılandırma değişiklikleri yapamazsınız. Merhaba Zamanlayıcı hello işlemi tamamlandığında, ancak hemen değişikliklerinizi olabilmeniz de durdurabilirsiniz kadar bekleyin. Geçerli döngüsü Hello durdurma zararlı değil ve bekleyen değişiklikler ile sonraki çalıştırma işlenir.

1. Mevcut hello Zamanlayıcı toostop söyleyen tarafından başlangıç hello PowerShell cmdlet'ini döngüsüyle `Stop-ADSyncSyncCycle`.
2. 1.1.281 önce bir derleme kullanma sonra hello Zamanlayıcısı durduruluyor değil Durdur hello geçerli geçerli görevini bir bağlayıcı. tooforce bağlayıcı toostop Merhaba, hello aşağıdaki eylemleri gerçekleştirin: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)
   * Başlat **eşitleme hizmeti** hello Başlat menüsünden. Çok Git**Bağlayıcılar**, hello bağlayıcı hello durumuyla vurgulayın **çalıştıran**seçip **durdurmak** hello Eylemler gelen.

Merhaba Zamanlayıcı hala etkin ve bir sonraki fırsatta yeniden başlatır.

## <a name="custom-scheduler"></a>Özel Zamanlayıcı
Merhaba bu bölümünde belgelenen cmdlet'leri yalnızca yapı içinde kullanılabilir [1.1.130.0](active-directory-aadconnect-version-history.md#111300) ve daha sonra.

Ardından Hello yerleşik Zamanlayıcı gereksinimlerinizi karşılamadığı, PowerShell kullanarak hello bağlayıcılar zamanlayabilirsiniz.

### <a name="invoke-adsyncrunprofile"></a>Çağırma ADSyncRunProfile
Bu şekilde bir bağlayıcı için bir profil başlatabilirsiniz:

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

Merhaba adları toouse [bağlayıcı adlarıyla](active-directory-aadconnectsync-service-manager-ui-connectors.md) ve [çalıştırma profili adları](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) hello bulunabilir [Eşitleme Hizmeti Yöneticisi kullanıcı Arabirimi](active-directory-aadconnectsync-service-manager-ui.md).

![Çalıştırma profili çağırma](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

Merhaba `Invoke-ADSyncRunProfile` cmdlet zaman uyumlu, hello Bağlayıcısı başarıyla veya bir hata ile Merhaba işlemi tamamlanana kadar başka bir deyişle, bu denetim döndürmüyor.

Bağlayıcılar zamanladığınızda hello tooschedule önerilir sırasının hello bunları:

1. (Tam/Delta) Active Directory gibi şirket içi dizinlere alın
2. (Tam/Delta) Azure AD'den alma
3. (Tam/Delta) Active Directory gibi şirket içi dizin eşitlemesi
4. (Tam/Delta) Azure AD'den eşitleme
5. TooAzure AD dışarı aktarma
6. Active Directory gibi tooon içi dizinleri dışarı aktarma

Bu sırada, hello yerleşik Zamanlayıcı hello bağlayıcıları nasıl çalıştığı yerdir.

### <a name="get-adsyncconnectorrunstatus"></a>Get-ADSyncConnectorRunStatus
Meşgul veya boş ise hello eşitleme altyapısı toosee da izleyebilirsiniz. Bu cmdlet Hello eşitleme altyapısı boşta ise ve bir bağlayıcı çalışmıyor boş bir sonuç döndürür. Bir bağlayıcı çalışıyorsa, hello bağlayıcı hello adını döndürür.

```
Get-ADSyncConnectorRunStatus
```

![Bağlayıcı durumu çalıştırın](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
Merhaba yukarıdaki, hello ilk satırı hello eşitleme altyapısı boşta olduğu bir durumdan resimdir. hello Azure AD Bağlayıcısı ne zaman çalışmasını ikinci satır hello.

## <a name="scheduler-and-installation-wizard"></a>Zamanlayıcı ve Yükleme Sihirbazı
Merhaba Yükleme Sihirbazı'nı başlatın, ardından hello Zamanlayıcı geçici olarak askıya alındı. Yapılandırma değişiklikleri yapın ve hello eşitleme altyapısı etkin olarak çalışıyorsa, bu ayarları uygulanamaz varsayıldığından bu davranıştır. Bu nedenle, hello Yükleme Sihirbazı'nı, hello eşitleme altyapısının eşitleme eylemleri gerçekleştirmeyi durdurduğu beri açık bırakmayın.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.

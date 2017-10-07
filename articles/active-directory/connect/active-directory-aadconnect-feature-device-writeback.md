---
title: "Azure AD Connect: cihaz geri yazma özelliğini etkinleştirme | Microsoft Docs"
description: "Bu belge ayrıntıları nasıl Azure AD Connect'i kullanarak tooenable cihaz geri yazma"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a>Azure AD Connect: cihaz geri yazma özelliğini etkinleştirme
> [!NOTE]
> Cihaz geri yazma için bir abonelik tooAzure AD Premium gereklidir.
> 
> 

Belge aşağıdaki hello nasıl tooenable hello cihaz geri yazma özelliğini Azure AD Connect içinde hakkında bilgiler sağlar. Cihaz geri yazma senaryoları aşağıdaki hello kullanılır:

* Aygıtları tooADFS üzerinde göre koşullu erişimi etkinleştir (2012 R2 veya üstü) korumalı uygulamaları (bağlı olan taraf güvenleri).

Bu ek güvenlik sağlar ve tooapplications erişim güvence yalnızca tootrusted cihazları verilir. Koşullu erişim hakkında daha fazla bilgi için bkz: [koşullu erişim ile Risk yönetme](../active-directory-conditional-access.md) ve [şirket içi koşullu Azure Active Directory cihaz kaydı kullanarak erişimi ayarlama](../active-directory-conditional-access-automatic-device-registration-setup.md).

> [!IMPORTANT]
> <li>Aygıtları aynı hello kullanıcılar olarak orman hello yer almalıdır. Aygıtları geri tooa tek orman yazılmalıdır olduğundan, bu özellik birden çok kullanıcı ormanı olan bir dağıtım şu anda desteklemiyor.</li>
> <li>Yalnızca bir cihaz kaydı yapılandırma nesnesi toohello şirket içi Active Directory ormanı eklenebilir. Bu özellik burada hello eşitlenmiş toomultiple Azure AD dizinleri Active Directory olduğu şirket içi bir topolojisi ile uyumlu değil.</li>> 

## <a name="part-1-install-azure-ad-connect"></a>1. Kısım: Yükleme Azure AD Connect
1. Özel kullanarak Azure AD Connect'i yüklemek veya hızlı ayarlar. Microsoft, tüm kullanıcılar ve gruplarla cihaz geri yazma etkinleştirmeden önce başarıyla eşitlendi toostart önerir.

## <a name="part-2-prepare-active-directory"></a>2. Kısım: Active Directory hazırlama
Cihaz geri yazma kullanma adımları tooprepare aşağıdaki hello kullanın.

1. Azure AD Connect yüklendiği hello makineden yükseltilmiş modda PowerShell'i başlatın.
2. Merhaba Active Directory PowerShell Modülü yüklü değilse, komutu aşağıdaki hello kullanarak yükleyin:
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. Hello Azure Active Directory PowerShell Modülü yüklü değilse, ardından yükleyip buradan [Azure Active Directory için Windows PowerShell Modülü (64-bit sürümü)](http://go.microsoft.com/fwlink/p/?linkid=236297). Bu bileşen, Azure AD Connect ile yüklenen hello oturum açma Yardımcısı üzerinde bir bağımlılığa sahiptir.
4. Kuruluş yönetici kimlik bilgileriyle hello aşağıdaki komutları çalıştırın ve ardından PowerShell çıkın.
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

Değişiklikleri toohello yapılandırma ad gerekiyor bu yana Kurumsal yönetici kimlik bilgileri gereklidir. Bir etki alanı yönetici yeterli izne sahip değil.

![Cihaz geri yazma özelliğini etkinleştirmek için Powershell](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

Açıklama:

* Bunlar zaten var olmadığından, oluşturur ve yeni kapsayıcılar ve nesneler CN altında yapılandırır Device Registration Configuration, CN = Services, CN = Configuration, = [orman-dn].
* Bunlar zaten var olmadığından, oluşturur ve yeni kapsayıcılar ve nesneler CN altında yapılandırır RegisteredDevices, = [etki alanı-dn]. Cihaz nesneleri, bu kapsayıcıda oluşturulur.
* Gerekli izinleri hello üzerinde Azure AD Bağlayıcısı hesabı, Active Directory toomanage cihazlarda ayarlar.
* Azure AD Connect üzerinde birden çok orman yüklü olsa bile, yalnızca tek bir ormanda toorun gerekir.

Parametreler:

* DomainName: Active Directory cihaz nesnelerinin oluşturulacağı etki alanı. Not: Belirli bir Active Directory ormanı için tüm cihazları tek bir etki alanında oluşturulur.
* AdConnectorAccount: Azure AD Connect toomanage nesneleri hello dizininde tarafından kullanılan Active Directory hesabı. Bu Azure AD Connect eşitleme tooconnect tooAD tarafından kullanılan hello hesabıdır. Hızlı ayarları kullanarak yüklediyseniz, bu MSOL_ ile önek hello hesabıdır.

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a>3. Kısım: Etkinleştir cihaz geri yazma özelliğini Azure AD Connect
Aşağıdaki yordam tooenable cihaz geri yazma özelliğini Azure AD Connect hello kullanın.

1. Merhaba Yükleme Sihirbazı'nı yeniden çalıştırın. Seçin **eşitleme seçeneklerini özelleştirme** hello ek görevleri sayfasında ve tıklayın **sonraki**.
   ![Özel yükleme eşitleme seçeneklerini özelleştirme](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)
2. Merhaba isteğe bağlı özellikler sayfasında, cihaz geri yazma artık gri olacaktır. Lütfen hello varsa Azure AD Connect hazırlık adımları tamamlanmamış olduğunu unutmayın. cihaz geri yazma gri out hello isteğe bağlı özellikler sayfasında. Cihaz geri yazma için Hello kutuyu işaretleyin ve tıklatın **sonraki**. Merhaba onay kutusu hala devre dışıysa, hello bkz [sorun giderme bölümüne](#the-writeback-checkbox-is-still-disabled).
   ![Özel cihaz geri yazma isteğe bağlı özellikler yükleme](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)
3. Merhaba geri yazma sayfasında hello varsayılan cihaz geri yazma orman olarak sağlanan hello etki alanı görürsünüz.
   ![Özel yükleme cihaz geri yazma hedef orman](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)
4. Hello Sihirbazı hiçbir ek yapılandırma değişiklikleri ile Merhaba yüklemesini tamamlayın. Gerekli olursa, çok başvuran[Azure AD Connect özel yüklemesi.](active-directory-aadconnect-get-started-custom.md)

## <a name="enable-conditional-access"></a>Koşullu erişimi etkinleştirme
Bu senaryo içinde kullanılabilir ayrıntılı yönergeler tooenable [şirket içi koşullu Azure Active Directory cihaz kaydı kullanarak erişimi ayarlama](../active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-devices-are-synchronized-tooactive-directory"></a>Aygıtları eşitlenmiş tooActive dizin doğrulayın
Cihaz geri yazma düzgün çalışıyor. Cihaz nesneleri toobe yazılmış geri tooAD için too3 saatlerini alabilir, dikkat edin.  aygıtlarınızı eşitlenen düzgün tooverify hello hello eşitleme kuralları tamamladıktan sonra aşağıdaki:

1. Active Directory Yönetim Merkezi'ni başlatın.
2. RegisteredDevices, hello federe etki alanı içinde genişletin.
   ![Active Directory Yönetim Merkezi'ni cihazların kayıtlı](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)
3. Geçerli kayıtlı cihazlar var. listelenir.
   ![Active Directory Yönetim Merkezi'ni kayıtlı cihazlar listesi](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)

## <a name="troubleshooting"></a>Sorun giderme
### <a name="hello-writeback-checkbox-is-still-disabled"></a>Merhaba geri yazma onay kutusu hala devre dışı
Yukarıdaki hello adımları izlediğinizi olsa bile cihaz geri yazma etkinleştirilmemiş Hello onay kutusunu Merhaba, aşağıdaki adımları size yol gösterecektir hello kutusunu etkinleştirilmeden önce hangi hello Yükleme Sihirbazı'nı doğruluyor.

İlk şey ilk:

* Windows Server 2012R2 en az bir ormanda olduğundan emin olun. Merhaba aygıt nesne türü mevcut olması gerekir.
* Merhaba Yükleme Sihirbazı zaten çalışıyorsa, herhangi bir değişiklik algılanmaz. Bu durumda, hello yükleme sihirbazını tamamlayın ve yeniden çalıştırın.
* Active Directory Bağlayıcısı hello tarafından kullanılan gerçekte hello doğru kullanıcı hello başlatma komut dosyasında sağladığınız hello hesabı olduğundan emin olun. tooverify Bu, şu adımları izleyin:
  * Merhaba Başlat menüsünden açmak **eşitleme hizmeti**.
  * Açık hello **Bağlayıcılar** sekmesi.
  * Active Directory etki alanı Hizmetleri türüyle Hello bağlayıcısını bulun ve seçin.
  * Altında **Eylemler**seçin **özellikleri**.
  * Çok Git**tooActive Directory ormanına Bağlan**. Bu ekran eşleşme hello sağlanan hesap toohello komut belirtilen o hello etki alanı ve kullanıcı adını doğrulayın.
    ![Eşitleme Hizmeti Yöneticisi'nde Bağlayıcısı hesabı](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)

Active Directory yapılandırmasını doğrulayın:

* Cihaz kayıt hizmeti aşağıdaki hello konumu bulunuyorsa bu hello doğrulayın (CN DeviceRegistrationService, CN = cihaz kayıt Services, CN = Device Registration Configuration, CN = Services, CN = Configuration =) yapılandırma adlandırma bağlamında altında.

![Sorun giderme, yapılandırma ad alanındaki DeviceRegistrationService](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* Merhaba yapılandırma ad arayarak yalnızca bir yapılandırma nesnesi olduğunu doğrulayın. Varsa birden fazla, hello yinelenen silin.

![Sorun giderme, hello yinelenen nesneleri Ara](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* Merhaba cihaz kayıt hizmeti nesnesinde hello özniteliği msDS-DeviceLocation var ve bir değere sahip emin olun. Arama bu konumu ve emin olun hello objectType msDS-DeviceContainer ile mevcut.

![Sorun giderme, msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![Sorun giderme, RegisteredDevices nesne sınıfı](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* Active Directory Bağlayıcısı hello önceki adımı tarafından bulunan hello kayıtlı cihazlar kapsayıcısı üzerinde gerekli izinlere sahip hello tarafından kullanılan hello hesap doğrulayın. Bu kapsayıcı beklenen hello izinlerini şudur:

![Sorun giderme, kapsayıcısı üzerindeki izinleri doğrulayın](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* Merhaba Active Directory hesabına sahip izinleri CN hello üzerinde doğrulayın Device Registration Configuration, CN = Services, CN = = Yapılandırma nesnesi.

![Sorun giderme, cihaz kaydı yapılandırma üzerindeki izinleri doğrulayın](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a>Ek bilgi
* [Koşullu erişim ile risk yönetme](../active-directory-conditional-access.md)
* [Azure Active Directory cihaz kaydı ile şirket içi koşullu erişim ayarlama](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.


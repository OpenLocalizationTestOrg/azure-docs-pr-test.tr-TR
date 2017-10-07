---
title: "Azure Active Directory'de Kurumsal durumda Dolaşım ayarları sorunlarını giderme | Microsoft Docs"
description: "Yanıtlar toosome BT yöneticileri ayarları ve uygulama veri eşitleme hakkında sorularınız olabilir sağlar."
services: active-directory
keywords: "Kurumsal durum Dolaşım ayarları, windows bulut Kurumsal durumda Dolaşım hakkında sık sorulan sorular"
documentationcenter: 
author: tanning
manager: swadhwa
editor: 
ms.assetid: f45d0515-99f7-42ad-94d8-307bc0d07be5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4636d016983426e30d696459f54167b8ad2babcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a>Sorun giderme Azure Active Directory'de Kurumsal durumda Dolaşım ayarları

Bu konu hakkında bilgi sağlar tootroubleshoot Kurumsal durumda Dolaşım ile ilgili sorunları tanılamak ve bilinen sorunların bir listesini sağlar.

## <a name="preliminary-steps-for-troubleshooting"></a>Sorun giderme için başlangıç adımları 
Sorun giderme başlamadan önce hello kullanıcı ve aygıt düzgün yapılandırıldığını ve tüm başlangıç gereksinimlerini Kurumsal durumda Dolaşım hello cihaz ve hello kullanıcı tarafından karşılandığından doğrulayın. 

1. Merhaba en son güncelleştirmeleri içeren Windows 10 ve en düşük sürüm 1511 (işletim sistemi yapı 10586 veya sonrası) hello cihazda yüklü. 
2. Merhaba, Azure AD alanına katılmış veya etki alanına katılmış ve Azure AD ile kayıtlı aygıttır.
3. Hello Azure Active Directory portalında **Kurumsal durumda Dolaşım** altındaki hello dizinin etkin **yapılandırma** > **aygıtları**  >  **Kullanıcılar eşitleme ayarları ve kurumsal uygulama verileri**. Seçili tüm kullanıcıları veya hello kullanıcı seçili hello seçeneği üzerinden eşitleme için etkinleştirilmiş ve hello güvenlik grubuna dahil.
4. Merhaba kullanıcının toothem atanmış bir Azure Active Directory Premium aboneliğiniz var.  
5. Merhaba aygıt yeniden ve kurumsal durumda Dolaşım etkinleştirildikten sonra hello kullanıcının oturum açtığı.

## <a name="information-tooinclude-when-you-need-help"></a>Yardıma ihtiyacınız olduğunda bilgi tooinclude
Aşağıdaki hello yönergeleri ile sorunu çözemiyorsanız, bizim destek mühendisleri başvurabilirsiniz. Bunları başvurduğunuzda, aşağıdaki bilgilerle tooinclude hello önerilir:

- **Genel hello hatanın açıklaması** – hello kullanıcı tarafından görülen hata iletileri vardır? Hata iletisi varsa, açıklamak fark, ayrıntılı olarak beklenmeyen davranışları hello. Hangi özellikler eşitleme için etkindir ve ne toosync bekleniyor hello kullanıcı nedir? Birden çok özelliği olmayan eşitleniyor yoksa yalıtılmış BT tooone mı?
- **Etkilenen kullanıcılar** – çalışma/başarısız olan bir kullanıcı veya birden çok kullanıcı için eşitleme olduğu? Her kullanıcı kaç cihaz oynayan? Bunları değil eşitleniyor tümü veya bunlardan bazıları eşitleniyor ve bazı eşitleniyor değil misiniz?
- **Merhaba kullanıcı hakkındaki bilgileri** – hangi kimliktir toolog toohello aygıtı kullanarak hello kullanıcı? Merhaba kullanıcı toohello aygıtı nasıl oturum? Bunlar toosync izin Seçili güvenlik grubunun parçası misiniz? 
- **Merhaba aygıt hakkındaki bilgileri** – bu cihaz Azure AD alanına katılmış veya etki alanına katılmış? Hangi derleme hello cihaz üzerinde mi? Merhaba en son güncelleştirmeler nelerdir?
- **Tarih / saat / saat dilimi** – hello kesin tarih ve saat hello hata gördüğünüz neydi (Merhaba saat dilimi dahil)?
- Bu bilgiler dahil olmak üzere mümkün olan en kısa sürede sorunu çözmenize yardımcı olur.

## <a name="troubleshooting-and-diagnosing-issues"></a>Sorunlarını tanılama ve sorun giderme
Bu bölümde öneriler hakkında yönergeler verir tootroubleshoot ve sorunları ilgili tooEnterprise durumda Dolaşım tanılayın.

## <a name="verify-sync-and-hello-sync-your-settings-settings-page"></a>Eşitleme doğrulayın ve Ayarlar sayfasında "ayarlarınızı eşitleyin" Merhaba 

1. Windows 10 bilgisayarı tooa katıldıktan sonra etki alanı tooallow Kurumsal durumda dolaşım, iş hesabınız ile oturum açma yapılandırılmış. Çok Git**ayarları** > **hesapları** > **eşitleme ayarlarınızı** ve eşitleme ve hello ayrı ayrı ayarlar, olduğunu onaylayın ve o hello üst İş hesabınız ile eşitleniyor Hello Ayarları sayfası gösterir. Aynı hesap, oturum açma hesabı olarak da kullanılır hello onaylayın **ayarları** > **hesapları** > **bilgisayarınızı bilgisi**. 
2. Merhaba görev toohello sağa ya da üst tarafındaki Merhaba ekranında taşıma gibi hello özgün makine üzerinde bazı değişiklikler yaparak eşitleme birden fazla makine arasında çalıştığını doğrulayın. Beş dakika içinde toohello ikinci makine yayılması hello değişiklik izleyin. 
 - Kilitlenmesini ve kilidinin açılmasını Merhaba ekranında (Win + L), bir eşitleme tetikleme yardımcı olabilir.
 - Kullanıyor olmanız gerekir Kurumsal durumda Dolaşım bağlı toohello kullanıcı hesabı ve hello makine hesabı olarak eşitleme toowork için– her iki bilgisayar aynı oturum açma hesabı hello.

**Olası sorun**: hello ayarları sayfasına sahip gri hello değiştirir ve bir hesap görme yerine hello metin "bazı Windows özellikleri yalnızca bir Microsoft hesabı veya iş hesabı kullanıyorsanız, kullanılabilir" görürsünüz. Bu sorun, toobe ayarlamak cihazlar etki alanına katılmış ve tooAzure AD kayıtlı ancak hello aygıt başarıyla tooAzure AD doğrulaması ortaya çıkabilir. Olası bir neden hello cihaz İlkesi uygulanmış olması gerekir, ancak bu uygulama zaman uyumsuz olarak olur ve tarafından birkaç saat Gecikmeli ' dir. Bu sorun, içinde hello adımları doğrulayın tooverify bu hello durumda aygıt kayıt durumu toocheck hello.

### <a name="verify-hello-device-registration-status"></a>Merhaba cihaz kayıt durumunu doğrulayın
Kurumsal durumda Dolaşım Azure AD ile kayıtlı hello aygıt toobe gerektirir. Özel olmayan tooEnterprise hello yönergeleri izleyerek durumda dolaşım, Windows 10 istemci kayıtlı bu hello onaylayın ve parmak izi, Azure AD ayarları URL'si NGC'ye durumunu yardımcı olmakla birlikte ve diğer bilgileri.

1.  Açık hello komut istemi yetkisiz. Windows, toodo açık çalışma Başlatıcısı (Win + R) hello ve "cmd" tooopen yazın.
2.  Merhaba komut istemi açıldıktan sonra türü "*dsregcmd.exe/status*".
3.  Beklenen çıktı için hello **AzureAdJoined** alan değeri, "Evet" olmalıdır **WamDefaultSet** alan değeri "Evet" olabilir ve gerekir hello **WamDefaultGUID** alan değeri olmalıdır bir Merhaba sonunda GUID ile "(Azuread'i)".

**Olası sorun**: **WamDefaultSet** ve **AzureAdJoined** hem "Hayır" Merhaba alan değeri olması, hello cihaz etki alanına katılmış ve Azure AD ile kayıtlı ve hello cihazı eşitleyebilir değil. Bu gösteriyor, hello aygıt toowait uygulanan ilkeyi toobe için gereken veya tooAzure AD bağlanırken başarısız hello cihaz için kimlik doğrulaması hello. Merhaba kullanıcı toowait uygulanan hello İlkesi toobe için birkaç saat olabilir. Diğer sorun giderme adımları Görev Zamanlayıcı'dan oturumunuzu kapatıp yeniden imzalama veya başlatan hello görevi tarafından otomatik kaydı yeniden deneniyor içerebilir. Bazı durumlarda, çalışan "*dsregcmd.exe /leave*" ile bu sorunu yeniden başlatılıyor ve kayıt yeniden deneme bir yükseltilmiş komut istemi penceresinde yardımcı olabilir.


**Olası sorun**: hello alanı için **AzureAdSettingsUrl** boşsa ve hello aygıt Eşitleme. yapar hello kullanıcı son oturum açan toohello aygıtı Kurumsal durumda Dolaşım hello Azure Active etkinleştirilmeden önce Dizin portalı. Merhaba aygıt yeniden başlatma ve hello kullanıcı oturum açma vardır. İsteğe bağlı olarak, BT yöneticisi devre dışı bırakın ve kullanıcıların olabilir eşitleme ayarları ve kurumsal uygulama verileri yeniden etkinleştirmek hello sahip hello Portalı'nda deneyin. Sonra tekrar etkinleştirilirse, yeniden başlatma hello cihaz ve hello kullanıcı oturum açma sahip. Merhaba sorunu çözmezse **AzureAdSettingsUrl** hatalı aygıt sertifika hello durumda boş olabilir. Bu durumda, çalışan "*dsregcmd.exe /leave*" ile bu sorunu yeniden başlatılıyor ve kayıt yeniden deneme bir yükseltilmiş komut istemi penceresinde yardımcı olabilir.

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a>Kurumsal durumda Dolaşım ve çok faktörlü kimlik doğrulaması 
Azure çok faktörlü kimlik doğrulaması yapılandırılmışsa, belirli koşullar altında Kurumsal durumda Dolaşım toosync veri başarısız olabilir. Bu belirtiler hakkında daha fazla ayrıntı için hello Destek belgesine bakın [KB3193683](https://support.microsoft.com/kb/3193683). 

**Olası sorun**: Cihazınızı hello Azure Active Directory portalında toorequire çok faktörlü kimlik doğrulaması yapılandırılmış ise, bir parola kullanarak tooa Windows 10 cihazı imzalarken toosync ayarları başarısız olabilir. Bu, çok faktörlü kimlik doğrulama yapılandırması hedeflenen tooprotect Azure yönetici hesabı türüdür. Yönetici kullanıcılar kendi Microsoft Passport ile tootheir Windows 10 cihazlarında iş PIN kodu için imzalama veya Office 365 gibi diğer Azure hizmetleriyle erişirken çok faktörlü kimlik doğrulamasını tamamlayan mümkün toosync olabilir.

**Olası sorun**: hello Yöneticisi hello Active Directory Federasyon Hizmetleri çok faktörlü kimlik doğrulaması koşullu erişim ilkesini yapılandırır ve hello aygıtta hello erişim belirtecinin süresi eşitleme başarısız olabilir. Oturum açmak ve hello Microsoft Passport for Work PIN kullanarak oturum emin olun veya Office 365 gibi diğer Azure hizmetleriyle erişirken çok faktörlü kimlik doğrulaması gerçekleştirmez.

###<a name="event-viewer"></a>Olay Görüntüleyicisi
Gelişmiş sorun giderme için Olay Görüntüleyicisi'ni kullanılan toofind belirli hataları olabilir. Bunlar hello aşağıdaki tabloda belirtilmiştir. Merhaba olayları Olay Görüntüleyicisi'ni altında bulunabilir > Uygulama ve hizmet günlükleri > **Microsoft** > **Windows** > **SettingSync** ve Eşitleme kimlikle ilgili sorunlar için **Microsoft** > **Windows** > **Azure AD**.


## <a name="known-issues"></a>Bilinen sorunlar

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a>Eşitleme MDM yazılım kullanarak dışarıdan yüklenen uygulamaların bulunduğu cihazlara çalışmıyor

Çalıştıran etkiler cihazlar Windows 10 Anniversary güncelleştirme (sürüm 1607) hello. Merhaba SettingSync Azure günlükleri altında Olay Görüntüleyicisi'nde hello olay kimliği 6013 80070259 hatasıyla sık görülür.

**Önerilen eylem**  
Merhaba Windows 10 v1607 istemci 23 Ağustos 2016 hello sahip olduğundan emin olun toplu güncelleştirme ([KB3176934](https://support.microsoft.com/kb/3176934) OS yapı 14393.82). 

---

### <a name="internet-explorer-favorites-do-not-sync"></a>Internet Explorer Sık Kullanılanlar eşitleme değil

Çalıştıran etkiler cihazlar Windows 10 Kasım güncelleştirme (sürüm 1511) hello.

**Önerilen eylem**  
Merhaba Windows 10 v1511 istemci Temmuz 2016 hello sahip olduğundan emin olun toplu güncelleştirme ([KB3172985](https://support.microsoft.com/kb/3172985) OS yapı 10586.494).

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a>Tema, Windows Information Protection ile korunan verileri yanı sıra eşitlemiyor 

tooprevent veri sızıntısı, ile korunan verileri [Windows bilgi koruması](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) Windows 10 Anniversary Update kullanarak cihazları hello için Kurumsal durumda Dolaşım eşitlenmez.



**Önerilen eylem**  
yok. Gelecekteki güncelleştirmeleri tooWindows Bu sorun çözülebilir.

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a>Tarih, saat ve bölge ayarları etki alanına katılmış aygıtta eşitliyor musunuz 
  
Etki alanına katılmış aygıtlar değil eşitleme tarih, saat ve bölge ayarı hello için deneyimi: otomatik saat. Otomatik saat kullanarak geçersiz kılma diğer tarih, saat ve bölge ayarları hello ve bu ayarları değil toosync neden olabilir. 

**Önerilen eylem**  
yok. 

---

### <a name="uac-prompts-when-syncing-passwords"></a>UAC parolaları eşitlerken ister

Merhaba çalıştıran etkiler cihazlar Windows 10 Kasım Güncelleştirmesi (sürüm 1511) olan bir kablosuz NIC ile toosync parolaları yapılandırılmış.

**Önerilen eylem**  
Merhaba Windows 10 v1511 istemci hello toplu güncelleştirme olduğundan emin olun ([KB3140743](https://support.microsoft.com/kb/3140743) OS yapı 10586.494).

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a>Akıllı kart oturum açma kullanan cihazları eşitleme çalışmıyor
Bir akıllı kart veya sanal akıllı kart kullanarak tooyour Windows aygıtında toosign çalışırsanız, ayarları eşitleme çalışmayı durdurur.     

**Önerilen eylem**  
yok. Gelecekteki güncelleştirmeleri tooWindows Bu sorun çözülebilir.

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a>Etki alanına katıldı cihazın şirket ağına bırakarak sonra eşitlemiyor     
Etki alanına katılmış cihazların Merhaba aygıt uzun süre için şirket dışı ise ve etki alanı kimlik doğrulaması tamamlayamıyor AD eşitleme hatası karşılaşabilirsiniz tooAzure kayıtlı.

**Önerilen eylem**  
Eşitleme devam edebilmeniz için hello aygıt tooa şirket ağına bağlayın.

---

 ### <a name="azure-ad-joined-device-is-not-syncing-and-hello-user-has-a-mixed-case-user-principal-name"></a>Azure AD katılmış aygıt değil eşitleniyor ve karışık bir servis talebi kullanıcı asıl adı hello kullanıcı vardır.
 Karma durum UPN (örn. kullanıcı adı yerine UserName) Hello kullanıcı varsa ve Windows 10 derleme 10586 too14393 yükseltti bir Azure AD katılmış aygıtında hello kullanıcıdır hello kullanıcının cihaz toosync başarısız olabilir. 

**Önerilen eylem**  
Merhaba kullanıcı toounjoin gerekir ve hello cihaz toohello bulut katılabilir. toodo hello yerel yönetici kullanıcı olarak bu, oturum açma ve çok giderek hello aygıt ayrılma**ayarları** > **sistem** > **hakkında** ve seçin " Yönetmenize veya iş veya Okul kesin". Aşağıdaki hello dosyaları ve Azure AD katılım hello aygıtı yeniden Temizleme **ayarları** > **sistem** > **hakkında** ve "Bağlan seçme tooWork veya Okul". Toojoin hello aygıt tooAzure Active Directory ve tam hello akış devam eder.

Merhaba temizleme adımda, aşağıdaki dosyaları temizleme hello:
- İçinde Settings.dat`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\`
- Başlangıç klasörü altındaki tüm hello dosyaları`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a>Olay Kimliği 6065:80070533 bu hesap şu anda devre dışı bırakıldığı için bu kullanıcı oturum açamaz  
Merhaba SettingSync/hata ayıklama günlükleri altında Olay Görüntüleyicisi'nde hello kullanıcının kimlik bilgilerinin süresi dolmuş ne zaman bu hata görülebilir. Ayrıca, Hello Kiracı sağlanan AzureRMS otomatik olarak sahip olduğunda oluşabilir. 

**Önerilen eylem**  
Merhaba ilk durumda, kendi kimlik bilgilerini ve oturum açma toohello aygıt hello yeni kimlik bilgileriyle güncelleyin hello kullanıcı sahip. toosolve hello AzureRMS sorunu devam listelenen hello adımlara [KB3193791](https://support.microsoft.com/kb/3193791). 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a>Olay Kimliği 1098: Hata: 0xCAA5001C belirteci Aracısı işlemi başarısız oldu  
Olay Görüntüleyicisi'nde hello AAD/Operational günlükleri altında bu hata ile olay 1104 görülebilir: AAD bulut AP eklentisi çağrı Get belirteci hata döndürdü: 0xC000005F. İzinleri veya sahipliği öznitelikler var. eksik ise bu sorun oluşur.    

**Önerilen eylem**  
Listelenen hello adımlarla devam [KB3196528](https://support.microsoft.com/kb/3196528).  



## <a name="next-steps"></a>Sonraki adımlar

- Kullanım hello [kullanıcı sesi Forumu](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming) nasıl tooimprove Kurumsal durum gezici üzerinde tooprovide geri bildirim ve marka öneriler.

- Daha fazla bilgi için bkz: Merhaba [Kurumsal durumda Dolaşım genel bakış](active-directory-windows-enterprise-state-roaming-overview.md). 

## <a name="related-topics"></a>İlgili konular
* [Kurumsal durum gezici genel bakış](active-directory-windows-enterprise-state-roaming-overview.md)
* [Azure Active Directory'de gezici Kurumsal durumunu etkinleştir](active-directory-windows-enterprise-state-roaming-enable.md)
* [Ayarlar ve veri dolaşımı SSS](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Grup İlkesi ve ayarları eşitleme için MDM ayarları](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 Dolaşım ayarları başvurusu](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)

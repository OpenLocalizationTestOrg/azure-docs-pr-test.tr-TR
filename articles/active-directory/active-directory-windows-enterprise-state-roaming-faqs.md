---
title: "aaaSettings ve veri dolaşımı SSS | Microsoft Docs"
description: "Yanıtlar toosome BT yöneticileri ayarları ve uygulama veri eşitleme hakkında sorularınız olabilir sağlar."
services: active-directory
keywords: "Kurumsal durum Dolaşım ayarları, windows bulut Kurumsal durumda Dolaşım hakkında sık sorulan sorular"
documentationcenter: 
author: tanning
manager: swadhwa
editor: curtand
ms.assetid: c0824f5c-129b-4240-969f-921f6a64eae7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4d6d6619b3a5fbd1d274603808d89b73ed942cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="settings-and-data-roaming-faq"></a>Ayarlar ve veri dolaşımı hakkında SSS
Bu konuda, BT yöneticileri, ayarları ve uygulama veri eşitleme hakkında olabilir bazı sorular yanıtlanmaktadır.

## <a name="what-data-roams"></a>Hangi verilerin Dolaşım yapar?
**Windows ayarlarını**: hello Windows işletim sisteminde yerleşik PC Ayarları hello. Genellikle, bunlar Bilgisayarınızı kişiselleştirme ayarlarını ve geniş kategorisi aşağıdaki hello içerir:

* *Tema*, masaüstü teması ve görev çubuğunda ayarlar gibi özellikleri içerir.
* *Internet Explorer ayarlarını*son açılan sekmeler ve Sık Kullanılanlar dahil olmak üzere.
* *Kenar tarayıcı ayarlarını*, Sık Kullanılanlar ve okuma listesi gibi.
* *Parolalar*Internet parolaları, Wi-Fi profilleri ve diğerleri dahil olmak üzere.
* *Dil Tercihleri*, klavye düzenleri, Sistem dili, tarih ve saat ve daha fazlası için ayarları içerir.
* *Özelliklere erişim kolaylığı*, yüksek karşıtlık teması, okuyucu ve Büyüteç gibi.
* *Diğer Windows ayarları*komut istemi ayarlarını ve uygulama listesi gibi.

**Uygulama verileri**: Evrensel Windows uygulamaları klasörü Dolaşım ayarları veri tooa yazma ve toothis klasörü yazılan tüm veriler otomatik olarak senkronize edilir. Toohello tek tek uygulama Geliştirici toodesign bu özellik bir uygulama tootake avantajı olur. Dolaşım kullanan bir evrensel Windows uygulaması toodevelop nasıl görürüm hakkında daha fazla ayrıntı için hello [appdata depolama API](https://msdn.microsoft.com/library/windows/apps/mt299098.aspx) ve hello [Geliştirici blog gezici Windows 8 appdata](http://blogs.msdn.com/b/windowsappdev/archive/2012/07/17/roaming-your-app-data.aspx).

## <a name="what-account-is-used-for-settings-sync"></a>Hangi hesabı ayarları eşitleme için kullanılır?
Windows 8 ve Windows 8.1 ayarları eşitleme tüketici Microsoft hesapları her zaman kullanılır. Kurumsal kullanıcılar bir Microsoft hesabı tootheir Active Directory etki alanı hesabı toogain erişim toosettings eşitleme hello özelliği tooconnect vardı. Windows 10'da bu işlevselliği birincil/ikincil hesap çerçevesiyle değiştirilmekte olan Microsoft hesabı bağlı.

Merhaba hesabı toosign tooWindows içinde kullanılan gibi hello birincil hesap tanımlanır. Bu, bir Microsoft hesabı, bir Azure Active Directory (Azure AD) hesabı, bir şirket içi Active Directory hesabı veya yerel bir hesap olabilir. Toplama toohello birincil hesabı, bir veya daha fazla ikincil bulut hesapları tootheir cihaz Windows 10 kullanıcıları ekleyebilirsiniz. Bir ikincil genellikle bir Microsoft hesabı, bir Azure AD hesabının veya başka bir hesap Gmail veya Facebook gibi hesabıdır. Bu ikincil hesapları erişim çoklu oturum açma ve hello Windows mağazası gibi tooadditional Hizmetleri sağlasa da, bunlar ayarları eşitleme destekleyen yeteneğine sahip değil.

Windows 10'da yalnızca hello birincil hesabı hello cihaz için ayarları eşitleme için kullanılabilir (bkz [nasıl yükseltebilirim Microsoft hesabı ayarları eşitleme Windows 8 tooAzure AD ayarları eşitleme Windows 10?](active-directory-windows-enterprise-state-roaming-faqs.md#how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-to-azure-ad-settings-sync-in-windows-10)).

Veri hello aygıtta hello farklı kullanıcı hesapları arasında hiçbir zaman karma. Ayarları eşitleme için iki kural vardır:

* Windows ayarlarını her zaman hello birincil hesabıyla dolaşan.
* Uygulama verileri hello kullanılan hesap tooacquire hello uygulamayla etiketlenecektir. Merhaba birincil hesabıyla etiketli yalnızca uygulamaları eşitler. Bir uygulama hello Windows mağazası veya mobil cihaz Yönetimi (MDM) dışarıdan yüklenen olduğunda uygulama sahipliği etiketleme belirlenir.

Bir uygulamanın sahibi tanımlanamıyorsa hello birincil hesabıyla dolaşan. Bir cihaz Windows 8 veya Windows 8.1 tooWindows 10 yükselttiyseniz, tüm hello uygulamalar hello Microsoft hesabı tarafından alınan olarak etiketlenecektir. Bu kullanıcıların çoğunun hello Windows mağazası uygulamaları edinmeli ve Azure AD hesapları önceki tooWindows 10 için Windows mağazası desteği vardı kaynaklanır. Bir uygulama çevrimdışı bir lisans yüklüyse hello uygulama hello aygıtta hello birincil hesabı kullanarak etiketlenecektir.

> [!NOTE]
> Bağlı tooAzure AD kuruluşa ait olan ve Windows 10 cihazlarına artık Microsoft hesapları tooa etki alanı hesabını bağlanabilir. özelliği tooconnect bir Microsoft hesabı tooa etki alanı hesabı hello ve tüm hello kullanıcının veri eşitleme sahip toohello Microsoft hesabı (gezici bağlı hello Microsoft hesabı ve Active Directory işlevselliği başka bir deyişle, hello Microsoft hesabı) kaldırılır Birleştirilmiş tooa Windows 10 cihazları, Active Directory veya Azure AD ortamında bağlı.
>
>

## <a name="how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-tooazure-ad-settings-sync-in-windows-10"></a>Windows 8 tooAzure AD ayarları eşitleme Windows 10'daki Microsoft hesabı ayarları eşitleme nasıl yükseltme?
Bağlı bir Microsoft hesabı ile Windows 8 veya Windows 8.1 çalıştıran birleştirilmiş toohello Active Directory etki alanı varsa, Microsoft hesabınız üzerinden ayarları eşitleme yapar. TooWindows 10 yükselttikten sonra Microsoft hesabı aracılığıyla toosync kullanıcı ayarlarını etki alanına katılmış bir kullanıcı olduğunuz ve Azure AD ile Merhaba Active Directory etki alanına bağlanmaz sürece devam eder.

Merhaba içi bağlı Active Directory etki alanı ile Azure AD connect, Cihazınızı toosync ayarlarını bağlı hello Azure AD hesabı kullanarak çalışacaktır. Merhaba Azure AD yönetici Kurumsal durumda dolaşım, sizin bağlı etkinleştirmez, Azure AD hesabının ayarları eşitleniyor durdurur. Bir Windows 10 kullanıcı olduğunuz ve Azure AD kimlik bilgilerinizle oturum açın, Azure AD üzerinden ayarları eşitleme yöneticinize etkinleştirir hemen sonra windows ayarları eşitleme başlar.

Kişisel verileri şirket aygıtınızda depolanırsa, Windows işletim sistemi ve uygulama verilerini tooAzure AD eşitleniyor başlayacağını farkında olmalıdır. Bu uygulamaları aşağıdaki hello sahiptir:

* Kişisel Microsoft hesap ayarlarınızı hello ayarları dışında üzerindeki çalışmanızı kayma veya Okul Azure AD hesapları. Merhaba Microsoft hesabını ve Azure AD ayarları eşitleme olmasıdır artık ayrı hesaplar kullanma.
* Wi-Fi parolalar, web kimlik bilgilerini ve bağlı bir Microsoft hesabı ile önceden eşitlenmiş olan Internet Explorer Sık Kullanılanlar gibi kişisel verileri Azure AD ile eşitlenir.

## <a name="how-do-microsoft-account-and-azure-ad-enterprise-state-roaming-interoperability-work"></a>Microsoft hesabınız ve Azure AD kuruluş durumu gezici birlikte çalışabilirlik iş nasıl musunuz?
Merhaba Kasım 2015 veya sonraki sürümlerinde Windows 10 Kurumsal durumda Dolaşım yalnızca tek bir hesap için aynı anda desteklenir. TooWindows içinde bir iş veya Okul Azure AD hesabı kullanarak imzalarsanız, tüm verileri Azure AD eşitleme yapar. İçinde tooWindows kişisel bir Microsoft hesabı kullanarak imzalarsanız, tüm verileri hello Microsoft hesabı ile eşitler. Evrensel appdata yalnızca hello birincil oturum açma hesabı hello aygıtta kullanarak dolaşan ve yalnızca hello uygulamanın lisans hello birincil hesabıyla aitse dolaşan. Tüm İkincil hesapları tarafından sahip olunan hello uygulamalar için evrensel appdata eşitlenmeyecek.

## <a name="do-settings-sync-for-azure-ad-accounts-from-multiple-tenants"></a>Ayarları birden çok kiracıdan Azure AD hesapları için eşitliyor musunuz?
Azure AD kiracılarıyla birden çok Azure AD farklı hesapları üzerinde hello alındığında aynı aygıt, Azure Rights Management (Azure RMS) hello cihazın kayıt defteri toocommunicate her bir Azure AD Kiracı için güncelleştirmeniz gerekir.  

1. Hello GUID her Azure AD kiracısı bulur. Merhaba Klasik Azure portalını açın ve Azure AD kiracısı seçin. Merhaba URL'sini tarayıcınızın adres çubuğuna hello Hello GUID hello Kiracı için kullanılıyor. Örneğin, `https://manage.windowsazure.com/YourAccount.onmicrosoft.com#Workspaces/ActiveDirectoryExtension/Directory/Tenant GUID/directoryQuickStart`
2. Merhaba GUID aldıktan sonra tooadd hello kayıt defteri anahtarına ihtiyaç duyarsınız **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\SettingSync\WinMSIPC\<kimliği GUID Kiracı >**.
   Merhaba gelen **kimliği GUID Kiracı** anahtar, adlı yeni bir çok dizeli değer (REG-MULTI-SZ) oluşturma **AllowedRMSServerUrls**. Verileri için dağıtım noktası hello URL'lerini aygıt erişimleri hello Azure diğer kiracılar lisans hello belirtin.
3. Dağıtım noktası URL'leri hello çalıştırarak lisans hello bulabilirsiniz **Get-AadrmConfiguration** cmdlet'i. Merhaba Hello değerleri, **Licensingıntranetdistributionpointurl** ve **LicensingExtranetDistributionPointUrl** farklıysa, her iki değeri belirtin. Değerler hello aynı Merhaba, yalnızca bir kez hello değeri belirtin.

## <a name="what-are-hello-roaming-settings-options-for-existing-windows-desktop-applications"></a>Var olan Windows Masaüstü uygulamaları için hello Dolaşım ayarları seçenekleri nelerdir?
Dolaşım, yalnızca evrensel Windows uygulamaları için çalışır. Varolan bir Windows Masaüstü uygulama gezici etkinleştirmek için kullanılabilen iki seçenek vardır:

* Merhaba [Masaüstü köprüsü](http://aka.ms/desktopbridge) , var olan Windows Masaüstü uygulamaları toohello Evrensel Windows platformu getirmenize yardımcı olur. Buradan, Azure AD uygulama verileri dolaşımı tootake avantajı değişikliklerin çok az kod gereklidir. Merhaba Masaüstü köprüsü sağlar uygulamalarınızı bir uygulama kimliği ile varolan Masaüstü uygulamaları için gezici tooenable uygulama verilerini gerekli olduğu.
* [Kullanıcı deneyimi sanallaştırma (UE-V)](https://technet.microsoft.com/library/dn458947.aspx) , var olan Windows Masaüstü uygulamaları için özel ayarlar şablonu oluşturmak ve Win32 uygulamaları için dolaşımını etkinleştir yardımcı olur. Bu seçenek hello Uygulama geliştirici toochange kodu hello uygulamasının gerektirmez. UE-V hello Microsoft Masaüstü iyileştirme paketi satın alan müşteriler için gezici sınırlı tooon içi Active Directory ' dir.

Yöneticiler, Windows işletim sistemi ayarları ve evrensel uygulama verilerine gezici değiştirerek UE-V tooroam Windows Masaüstü uygulama verilerini yapılandırabilirsiniz [UE-V grup ilkeleri](https://technet.microsoft.com/itpro/mdop/uev-v2/configuring-ue-v-2x-with-group-policy-objects-both-uevv2)dahil:

* Windows ayarlarını Grup İlkesi dolaşan
* Windows uygulamaları Grup İlkesi eşitlemeyin
* Internet Explorer hello uygulamaları bölümünde Dolaşım

Hello gelecekteki, Microsoft UE-V derine Windows'da tümleşik şekilde toomake araştırın ve UE-V tooroam ayarları hello Azure AD bulut aracılığıyla genişletme.

## <a name="can-i-store-synced-settings-and-data-on-premises"></a>Şirket içinde eşitlenmiş ayarları ve verileri depolayabilir?
Kurumsal durumda Dolaşım tüm eşitlenmiş veriler hello Azure bulut depolar. UE-V sunan bir şirket içi çözüm gezici.

## <a name="who-owns-hello-data-thats-being-roamed"></a>Çıkan hello veri sahibi kim?
Merhaba kuruluşlar kendi veri Kurumsal durumda Dolaşım çıkan hello. Veriler bir Azure veri merkezinde depolanır. Tüm kullanıcı verileri aktarım sırasında hem Azure RMS kullanarak hello bulutta REST şifrelenir. Merhaba aygıt terk etmeden önce yalnızca kullanıcı kimlik bilgileri gibi hassas belirli verileri şifreler bir karşılaştırma geliştirme tooMicrosoft hesabı tabanlı ayarları eşitleme, budur.

Microsoft, kaydedilmiş toosafeguarding müşteri verilerdir. Başka bir kullanıcı bu verileri okuyabilmesi için bir Windows 10 cihaz terk etmeden önce bir kurumsal kullanıcının ayarlarını verileri Azure RMS tarafından otomatik olarak şifrelenir. Kuruluşunuz Azure RMS için ücretli bir abonelik varsa, izleme gibi diğer Azure RMS özellikleri kullanmak ve belgeleri iptal edebilir, otomatik olarak hassas bilgiler içeren bir e-postaları korumak ve kendi anahtarları Yönet (Merhaba "kendi anahtarını getir" Çözüm Ayrıca bilinen BYOK olarak). Bu özellikler ve Azure RMS'nin nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Azure Rights Management nedir](https://technet.microsoft.com/jj585026.aspx).

## <a name="can-i-manage-sync-for-a-specific-app-or-setting"></a>Eşitleme için belirli uygulama veya ayarını yönetebilir miyim?
Windows 10'da tek bir uygulama için gezici hiçbir MDM veya Grup İlkesi ayarı toodisable yoktur. Kiracı Yöneticiler appdata eşitleme yönetilen bir cihazda tüm uygulamalar için devre dışı bırakabilir, ancak uygulama başına veya uygulama içinde düzeyinde daha hassas bir denetim yok yok.

## <a name="how-can-i-enable-or-disable-roaming"></a>Nasıl etkinleştirebilirim veya gezici devre dışı?
Merhaba, **ayarları** uygulama, çok Git**hesapları** > **ayarlarınızı eşitleyin**. Bu sayfadan hangi hesabı kullanılan tooroam ayarlar yapılıyor görebilirsiniz ve etkinleştirmek veya ayarları toobe çıkan tek tek grupları devre dışı bırakabilirsiniz.

## <a name="what-is-microsofts-recommendation-for-enabling-roaming-in-windows-10"></a>Windows 10 Dolaşım etkinleştirmek için Microsoft'un öneri nedir?
Microsoft solutions gezici kullanıcı profilleri, UE-V ve kurumsal durumu Dolaşım gibi kullanılabilir gezici birkaç farklı ayarları vardır.  Microsoft kaydedilmiş toomaking yatırımın gelecekteki Windows sürümlerinde gezici Kurumsal durumda olduğunu. Ardından, kuruluşunuzun taşıma veri toohello bulutla hazır veya rahat değilse, birincil gezici teknolojiyi UE-V kullanma öneririz. Kuruluşunuz var olan Windows Masaüstü uygulamaları için destek gezici gerektiriyor, ancak istekli toomove toohello bulut, kuruluş durumu gezici hem UE-V kullanmanızı öneririz. UE-V ve kurumsal durumda Dolaşım çok benzer teknolojiler olsa da, bunlar birbirini dışlayan değildir. Bunlar, birbirleri toohelp emin olun, kuruluşunuz, kullanıcılarınıza gereken Hizmetleri gezici hello sağlar tamamlar.  

Kurumsal durumda Dolaşım ve UE-V kullanırken kuralları aşağıdaki hello geçerlidir:

* Kurumsal durumda Dolaşım hello birincil gezici hello aygıtta aracısıdır. UE-V kullanılan toosupplement hello "Win32 boşluk" yapılıyor
* İlkeleri Hello UE-V Grup kullanarak olduğunda UE-V Windows ayarları ve modern UWP uygulama verileri için gezici devre dışı bırakılması gerekir. Bunlar zaten Kurumsal durumda Dolaşım tarafından ele alınmıştır.

## <a name="how-does-enterprise-state-roaming-support-virtual-desktop-infrastructure-vdi"></a>Sanal Masaüstü Altyapısı (VDI) Kurumsal durumda Dolaşım nasıl destekler?
Kurumsal durumda dolaşım, Windows 10 İstemci SKU'ları, ancak sunucu SKU'ları desteklenir. Bir istemci VM hiper yönetici makinesinde barındırılır ve Uzaktan toohello sanal makinede oturum verilerinizi dolaşıma. Birden çok kullanıcı aynı işletim sistemi ve kullanıcıların uzaktan tooa sunucusu tam masaüstü deneyimi için oturum açma hello paylaşıyorsanız, gezici çalışmayabilir. Merhaba ikinci oturum tabanlı senaryo resmi olarak desteklenmez.

## <a name="what-happens-when-my-organization-purchases-azure-rms-after-using-roaming"></a>Dolaşım kullandıktan sonra Azure RMS Kuruluşum satın ne olur?
Kuruluşunuz zaten kullanıyorsanız, Windows 10 Dolaşım hello Azure RMS sınırlı kullanım ücretsiz abonelik, ücretli bir Azure RMS aboneliği satın hello gezici özelliği hello işlevselliğini hiçbir etkisi olmaz ve hiçbir yapılandırma değişikliği olacaktır BT yöneticiniz tarafından gerekli.

## <a name="known-issues"></a>Bilinen sorunlar
Lütfen hello hello belgelerine bakın [sorun giderme](active-directory-windows-enterprise-state-roaming-troubleshooting.md) bilinen sorunların bir listesi için bölüm. 

## <a name="related-topics"></a>İlgili konular
* [Kurumsal durum gezici genel bakış](active-directory-windows-enterprise-state-roaming-overview.md)
* [Azure Active Directory'de gezici Kurumsal durumunu etkinleştir](active-directory-windows-enterprise-state-roaming-enable.md)
* [Grup İlkesi ve ayarları eşitleme için MDM ayarları](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 Dolaşım ayarları başvurusu](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Sorun giderme](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

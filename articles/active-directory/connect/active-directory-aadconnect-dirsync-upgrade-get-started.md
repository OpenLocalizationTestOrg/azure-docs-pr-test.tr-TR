---
title: "Azure AD Connect: DirSync'ten yükseltme | Microsoft Belgeleri"
description: "Bilgi nasıl tooupgrade DirSync tooAzure AD alanından Bağlan. Bu makaleler DirSync tooAzure AD Connect yükseltme hello adımları açıklar."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: baf52da7-76a8-44c9-8e72-33245790001c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 05572af410698deaa1392c8837bfcb749efc69e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a>Azure AD Connect: DirSync'ten yükseltme
Azure AD Connect hello ardıl tooDirSync ' dir. Bu konu başlığı altında Dirsync'ten yükseltme hello yollarını bulun. Bu adımlar, Azure AD Connect'in başka bir sürümünden veya Azure AD Eşitleme'den yapılacak yükseltmeler için geçerli değildir.

Azure AD Connect'i yüklemeye başlamadan önce emin olun çok[Azure AD Connect indirin](http://go.microsoft.com/fwlink/?LinkId=615771) ve tam hello önkoşul adımlarını [Azure AD Connect: donanım ve Önkoşullar](active-directory-aadconnect-prerequisites.md). Özellikle, bu alanlar Dirsync'ten farklı olduğundan hello aşağıdaki hakkında tooread istiyor:

* Merhaba, PowerShell ve .net sürümü gereklidir. DirSync gerekenleri daha hello sunucuda gerekli toobe daha yeni sürümleri.
* Merhaba proxy sunucu yapılandırması. Bir proxy sunucu tooreach kullanıyorsanız, Internet Merhaba, yükseltmeden önce bu ayarın yapılandırılması gerekir. DirSync hello proxy sunucusu yükleme hello kullanıcı için yapılandırılan her zaman kullanılır, ancak Azure AD Connect kullanan makine ayarlarını yerine.
* Merhaba URL'leri gerekli toobe hello proxy sunucu açın. Temel senaryoları, aynı zamanda DirSync tarafından desteklenen bu senaryoları için aynı hello hello gereksinimleri verilmiştir. Azure AD Connect ile sunulan yeni özelliklerle hello hiçbirini toouse istiyorsanız, bazı yeni URL'ler açılması gerekir.

> [!NOTE]
> Yeni Azure AD Connect sunucusu toostart eşitleme değişiklikleri tooAzure AD etkinleştirdikten sonra toousing DirSync veya Azure AD eşitleme geri gerekir. Azure AD Connect toolegacy istemcilerden DirSync ve Azure AD eşitleme gibi eski sürüme düşürmeyi desteklenmez ve Azure AD içinde veri kaybı gibi tooissues yol açabilir.

DirSync'ten yükseltmiyorsanız diğer senaryolar için [ilgili belgelere](#related-documentation) göz atın.

## <a name="upgrade-from-dirsync"></a>DirSync'ten yükseltme
Geçerli DirSync dağıtımınıza bağlı olarak, hello yükseltme için farklı seçenekler vardır. Merhaba yükseltme süresi üç saatten az olması beklenen sonra hello toodo yerinde yükseltme önerilir. Merhaba yükseltme süresi üç saatten fazla bekleniyordu, ardından hello toodo başka bir sunucu üzerinde paralel dağıtım önerilir. 50. 000'den fazla nesneniz varsa, birden çok üç saat toodo hello yükseltme süreceğini tahmin.

| Senaryo |
| --- | --- |
| [Yerinde yükseltme](#in-place-upgrade) |
| [Paralel dağıtım](#parallel-deployment) |

> [!NOTE]
> DirSync tooAzure AD alanından tooupgrade planlarken Connect, DirSync kendiniz hello yükseltmeden önce kaldırmayın. Azure AD Connect okuyun ve Dirsync'ten hello yapılandırmasını geçirmek ve hello sunucuyu denetledikten sonra kaldırma.

**Yerinde yükseltme**  
Merhaba, zaman toocomplete hello yükseltme hello Sihirbazı tarafından görüntülenen bekleniyordu. Bu tahmin, üç saat toocomplete 50.000 nesne (kullanıcılar, kişiler ve gruplar) içeren bir veritabanı için yükseltme gereken hello varsayımına dayanır. Merhaba, veritabanınızdaki nesne sayısı 50. 000'den az ise, Azure AD Connect yerinde yükseltme önerir. Toocontinue karar verirseniz, geçerli ayarlarınız otomatik olarak yükseltme sırasında uygulanır ve sunucunuz etkin eşitlemeyi otomatik olarak sürdürür.

Ardından, toodo yapılandırma geçişi ve paralel dağıtım yapmak istiyorsanız hello yerinde yükseltme önerisini geçersiz kılabilirsiniz. Örneğin, hello fırsat toorefresh hello donanım ve işletim sistemi alabilir. Daha fazla bilgi için bkz: Merhaba [paralel dağıtım](#parallel-deployment) bölümü.

**Paralel dağıtım**  
50.000'den fazla nesneniz varsa paralel dağıtım seçeneğini kullanmanız önerilir. Bu dağıtım, kullanıcılarınızın işletimsel gecikme yaşamasını önler. Merhaba yükseltme için tooestimate hello kapalı kalma süresi Hello Azure AD Connect yükleme çalışır ancak hello geçmiş DirSync yükselttiyseniz kendi deneyiminizin büyük olasılıkla toobe hello en iyi kılavuzdur.

### <a name="supported-dirsync-configurations-toobe-upgraded"></a>Desteklenen DirSync yapılandırmaları toobe yükseltme
yapılandırma değişiklikleri izleyen hello yükseltilmiş DirSync ile desteklenir:

* Etki alanı ve OU filtreleme
* Alternatif kimlik (UPN)
* Parola eşitleme ve Exchange karma ayarları
* Ormanınız/etki alanınız ve Azure AD ayarlarınız
* Kullanıcı özniteliği tabanlı filtreleme

Merhaba değişikliğinden sonra yükseltilemez. Bu yapılandırma varsa, hello yükseltme engellenir:

* Kaldırılan öznitelikler ve özel uzantı DLL'si kullanmak gibi desteklenmeyen DirSync değişiklikleri

![Yükseltme engellendi](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

Bu gibi durumlarda hello tooinstall yeni bir Azure AD Connect sunucusunun önerilir [hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode) ve doğrulama eski DirSync ile yeni Azure AD Connect yapılandırması hello. [Azure AD Connect Eşitleme özel yapılandırmasında](active-directory-aadconnectsync-whatis.md) tanımlanan şekilde, özel yapılandırmayı kullanarak yapılan tüm değişiklikleri yeniden uygulayın.

hello hizmet hesapları için DirSync tarafından kullanılan hello parolalar alınamaz ve değil geçirilir. Bu parolalar hello yükseltme sırasında sıfırlanır.

### <a name="high-level-steps-for-upgrading-from-dirsync-tooazure-ad-connect"></a>DirSync tooAzure AD Connect yükseltme için üst düzey adımlar
1. Hoş Geldiniz tooAzure AD Connect
2. Geçerli DirSync yapılandırmasının analizi
3. Azure AD genel yönetici parolası toplama
4. (Azure AD Connect hello yükleme sırasında kullanılan yalnızca) bir kuruluş yöneticisi hesabı için kimlik bilgileri toplama
5. Azure AD Connect yüklemesi
   * DirSync’i kaldırma (veya geçici olarak devre dışı bırakma)
   * Azure AD Connect'i yükleme
   * Eşitlemeyi isteğe bağlı olarak başlatma

Ek adımların gerekli olduğu durumlar:

* Tam SQL Server (yerel veya uzak) kullanıyor olmanız
* Eşitleme kapsamında 50.000'den fazla nesnenizin olması

## <a name="in-place-upgrade"></a>Yerinde yükseltme
1. Hello Azure AD Connect yükleyicisini (MSI) başlatın.
2. Gözden geçirin ve toolicense koşulları ve gizlilik bildirimini kabul etmektesiniz.  
   ![TooAzure AD Hoş Geldiniz](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. Mevcut DirSync yüklemenizin sonraki toobegin çözümleme'yi tıklatın.  
   ![Mevcut Directory Sync yüklemesini analiz etme](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. Merhaba analiz tamamlandığında nasıl hello önerilerini görmek tooproceed.  
   * SQL Server Express kullanıyorsanız ve 50. 000'den az nesneniz varsa, aşağıdaki ekran hello gösterilir:  
     ![Analiz tamamlandı, dirsync'ten hazır tooupgrade](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * DirSync için tam SQL Sunucusu kullanıyorsanız bu paketi görürsünüz:  
     ![Analiz tamamlandı, dirsync'ten hazır tooupgrade](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)  
     DirSync tarafından kullanılan hello var olan SQL Server veritabanı sunucusunun ilgili Hello bilgileri görüntülenir. Gerekirse uygun ayarlamaları yapın. Tıklatın **sonraki** toocontinue hello yükleme.
   * 50.000’den fazla nesneniz varsa şu ekranı görürsünüz:  
     ![Analiz tamamlandı, dirsync'ten hazır tooupgrade](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)  
     yerinde yükseltme ile tooproceed hello onay kutusu sonraki toothis iletiye tıklayın: **bu bilgisayarda Dirsync'i yükseltmeye devam edin.**
     toodo bir [paralel dağıtım](#parallel-deployment) bunun yerine, hello DirSync yapılandırma ayarlarını dışarı aktarın ve hello yapılandırma toohello yeni sunucusuna taşıyın.
5. Şu anda tooconnect tooAzure AD kullandığınız hello hesabı için Hello parola sağlayın. Bu, şu anda DirSync tarafından kullanılan hello hesabı olması gerekir.  
   ![Azure AD kimlik bilgilerinizi girin](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)  
   Bir hatayla karşılaştıysanız ve bağlantı sorunlarınız varsa bkz. [Bağlantı sorunlarını giderme](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Active Directory için bir kuruluş yöneticisi hesabı sağlayın.  
   ![ADDS kimlik bilgilerinizi girin](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. Şimdi hazır tooconfigure olduğunuz. **Yükselt**'e tıkladığınızda DirSync kaldırılır, Azure AD Connect yapılandırılır ve eşitleme başlar.  
   ![Hazır tooconfigure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)
8. Merhaba yükleme tamamlandıktan sonra oturumu kapatın ve Eşitleme Hizmeti Yöneticisi, eşitleme kuralı düzenleyicisi kullanın ya da herhangi bir yapılandırma değişikliği toomake deneyin önce tooWindows içinde yeniden oturum açın.

## <a name="parallel-deployment"></a>Paralel dağıtım
### <a name="export-hello-dirsync-configuration"></a>Merhaba DirSync yapılandırmasını dışarı aktarma
**50.000'den fazla nesneyle paralel dağıtım**

50. 000'den fazla nesneniz sahip sonra hello Azure AD Connect yükleme paralel dağıtım önerir.

Ekran benzer toohello aşağıdaki görüntülenir:  
![Analiz tamamlandı](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

Paralel dağıtım ile tooproceed istiyorsanız, aşağıdaki adımları tooperform hello gerekir:

* Merhaba tıklatın **ayarlarını dışa aktarma** düğmesi. Azure AD Connect'i ayrı bir sunucuya yüklediğinizde, bu ayarlar, geçerli DirSync tooyour yeni Azure AD Connect'i yüklemeye geçirilir.

Ayarlarınız başarıyla dışarı aktarıldıktan sonra hello Azure AD Connect Sihirbazı hello DirSync sunucusundaki çıkabilirsiniz. Çok Hello sonraki adıma devam[Azure AD Connect'i ayrı bir sunucuya yükleme](#installation-of-azure-ad-connect-on-separate-server)

**50.000'den az nesneyle paralel dağıtım**

Ardından 50. 000'den az nesneniz varsa, ancak yine de paralel dağıtım toodo mi yoksa aşağıdaki hello:

1. Hello Azure AD Connect yükleyicisini (MSI) çalıştırın.
2. Merhaba gördüğünüzde **Hoş Geldiniz tooAzure AD Connect** ekran, çıkış hello Yükleme Sihirbazı'hello "X" Merhaba sağ üst köşedeki hello penceresinin tıklatarak.
3. Bir komut istemi açın.
4. Merhaba yükleme konumu Azure AD Connect (varsayılan: C:\Program Files\Microsoft Azure Active Directory Connect) hello aşağıdaki komutu yürütün: `AzureADConnect.exe /ForceExport`.
5. Merhaba tıklatın **ayarlarını dışa aktarma** düğmesi. Azure AD Connect'i ayrı bir sunucuya yüklediğinizde, bu ayarlar, geçerli DirSync tooyour yeni Azure AD Connect'i yüklemeye geçirilir.

![Analiz tamamlandı](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

Ayarlarınız başarıyla dışarı aktarıldıktan sonra hello Azure AD Connect Sihirbazı hello DirSync sunucusundaki çıkabilirsiniz. Çok Hello sonraki adıma devam[Azure AD Connect'i ayrı bir sunucuya yüklemek](#installation-of-azure-ad-connect-on-separate-server).

### <a name="install-azure-ad-connect-on-separate-server"></a>Azure AD Connect'i ayrı bir sunucuya yükleme
Azure AD Connect'i yeni bir sunucuya yüklediğinizde, hello tooperform Azure AD Connect temiz bir yüklemesini istediğiniz varsayılır. Toouse hello DirSync yapılandırması istediğinden, bazı ek adımlar tootake vardır:

1. Hello Azure AD Connect yükleyicisini (MSI) çalıştırın.
2. Merhaba gördüğünüzde **Hoş Geldiniz tooAzure AD Connect** ekran, çıkış hello Yükleme Sihirbazı'hello "X" Merhaba sağ üst köşedeki hello penceresinin tıklatarak.
3. Bir komut istemi açın.
4. Merhaba yükleme konumu Azure AD Connect (varsayılan: C:\Program Files\Microsoft Azure Active Directory Connect) hello aşağıdaki komutu yürütün: `AzureADConnect.exe /migrate`.
   Hello Azure AD Connect Yükleme Sihirbazı'nı başlatır ve ekran aşağıdaki hello ile sunar:  
   ![Azure AD kimlik bilgilerinizi girin](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)
5. DirSync yüklemesinden dışarı aktarılan hello ayarları dosyasını seçin.
6. Şunlar dahil olmak üzere tüm gelişmiş seçenekleri yapılandırın:
   * Azure AD Connect için özel bir yükleme konumu.
   * Mevcut bir SQL Server örneği (Varsayılan: Azure AD Connect, SQL Server 2012 Express'i yükler). Merhaba kullanmayın DirSync sunucunuzla aynı veritabanı örneği.
   * (Bu hesap bir etki alanı hizmeti hesabı olması gerekir SQL Server veritabanınız uzak ise) bir hizmet hesabı tooconnect tooSQL sunucu kullanılır.
     Bu seçenekler şu ekranda görülebilir:  
     ![Azure AD kimlik bilgilerinizi girin](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)
7. **İleri**’ye tıklayın.
8. Merhaba üzerinde **hazır tooconfigure** sayfasında, hello bırakın **hello Yapılandırma tamamlandıktan hemen sonra hello eşitleme işlemini başlatmak** işaretli. Hello server şu an içinde [hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode) nedenle değişiklikleri dışarı aktarılan tooAzure AD değildir.
9. **Yükle**'ye tıklayın.
10. Merhaba yükleme tamamlandıktan sonra oturumu kapatın ve Eşitleme Hizmeti Yöneticisi, eşitleme kuralı düzenleyicisi kullanın ya da herhangi bir yapılandırma değişikliği toomake deneyin önce tooWindows içinde yeniden oturum açın.

> [!NOTE]
> Windows Server Active Directory ve Azure Active Directory arasında eşitleme başlar ancak dışarı aktarılan tooAzure AD hiçbir değişir. Aynı anda yalnızca bir eşitleme aracı değişiklikleri etkin olarak dışarı aktarabilir. Bu durum, [hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode) olarak adlandırılır.

### <a name="verify-that-azure-ad-connect-is-ready-toobegin-synchronization"></a>Azure AD Connect hazır toobegin eşitleme olduğunu doğrulayın
Azure AD Connect, dirsync'ten üzerinden hazır tootake tooverify, gereksinim duyduğunuz tooopen **Eşitleme Hizmeti Yöneticisi'ni** hello grubundaki **Azure AD Connect** hello Başlat menüsünden.

Merhaba uygulamada toohello Git **Operations** sekmesi. Bu sekmede, işlemleri aşağıdaki o hello tamamladığınızdan onaylayın:

* Merhaba AD Bağlayıcısı üzerinde içeri aktarma
* Hello Azure AD Bağlayıcısı üzerinde içeri aktarma
* Merhaba AD Bağlayıcısı üzerinde tam eşitleme
* Hello Azure AD Bağlayıcısı üzerinde tam eşitleme

![İçeri aktarma ve Eşitleme tamamlandı](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

Bu işlemlerin Hello sonucunu gözden geçirin ve hiç hata olmadığından emin olun.

Toosee istediğiniz ve AD dışarı toobe tooAzure hakkında hello değişikliklerini inceleyin, ardından nasıl tooverify hello yapılandırmada okuma [hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode). Beklenmeyen bir durumla karşılaşmadığınız sürece gerekli yapılandırma değişikliklerini yapın.

DirSync tooAzure zaman bu adımları tamamladıktan ve hello sonuçla Mutluluk duyuyoruz AD alanından hazır tooswitch var.

### <a name="uninstall-dirsync-old-server"></a>DirSync'i (eski sunucuyu) kaldırma
* **Programlar ve özellikler**’de **Microsoft Azure Active Directory eşitleme aracını** bulun
* **Microsoft Azure Active Directory eşitleme aracını** kaldırma
* Merhaba kaldırma too15 dakika toocomplete alabilir.

Daha sonra DirSync toouninstall tercih ederseniz, geçici olarak hello sunucusunu kapatın veya hello hizmetini devre dışı bırakın. Bu yöntem bir sorun yaşanırsa toore etkinleştir tanır. Ancak, bu gerekli böylece bu hello sonraki adımı başarısız olur beklenmiyor.

Kaldırılması veya devre dışı DirSync ile tooAzure AD dışarı aktarma etkin sunucusu yok. Merhaba sonraki adım tooenable Azure AD Connect değişiklikleri şirket içi Active Directory'de eşitlenen toobe tooAzure AD devam etmeden önce tamamlanması gerekir.

### <a name="enable-azure-ad-connect-new-server"></a>Azure AD Connect'i (yeni sunucu) etkinleştirme
Yükleme sonrasında, Azure AD açmayı Connect'i toomake ek yapılandırma değişiklikleri izin verin. Başlat **Azure AD Connect** hello Başlat menüsünden veya hello masaüstünde hello kısayol. Toorun hello MSI yüklemesini tekrar denemek emin olun.

Merhaba şunları görmeniz gerekir:  
![Ek görevler](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* **Hazırlama modunu yapılandır** seçeneğini belirleyin.
* İn işaretini kaldırarak hello tarafından hazırlamayı devre dışı bırakma **hazırlama modunu** onay kutusu.

![Azure AD kimlik bilgilerinizi girin](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* Merhaba tıklatın **sonraki** düğmesi
* Merhaba Hello onay sayfasında, tıklatın **yükleme** düğmesi.

Azure AD Connect artık etkin sunucunuzdur ve geri toousing mevcut DirSync sunucunuzu geçiş gerekir değil.

## <a name="next-steps"></a>Sonraki adımlar
Azure AD Connect'i sahip olduğunuza göre şunları yapabilirsiniz [hello yüklemeyi doğrulayın ve lisansları atama](active-directory-aadconnect-whats-next.md).

Merhaba yüklemeyle etkinleştirilen şu yeni özellikler hakkında daha fazla bilgi edinin: [otomatik yükseltme](active-directory-aadconnect-feature-automatic-upgrade.md), [yanlışlıkla silmeleri engelleme](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), ve [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Bu genel konular hakkında daha fazla bilgi edinin: [Zamanlayıcı ve nasıl tootrigger eşitleme](active-directory-aadconnectsync-feature-scheduler.md).

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.

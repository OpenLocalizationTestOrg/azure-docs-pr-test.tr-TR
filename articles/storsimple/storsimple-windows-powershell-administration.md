---
title: "StorSimple cihaz yönetimi için aaaPowerShell | Microsoft Docs"
description: "Bilgi nasıl StorSimple toomanage için Windows PowerShell toouse StorSimple Cihazınızı."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0ff3bb0d-897a-4676-bdcb-402c2628dac5
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: alkohli@microsoft.com
ms.openlocfilehash: 1adcbb8bb89e3e3b4f328aac198690476c2a78cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-for-storsimple-tooadminister-your-device"></a>Cihazınızı StorSimple tooadminister için Windows PowerShell'i kullanma
## <a name="overview"></a>Genel Bakış
StorSimple için Windows PowerShell komut satırı arabirimi sağlayan Microsoft Azure StorSimple Cihazınızı toomanage kullanabilirsiniz. Merhaba adı da anlaşılacağı gibi bir Windows PowerShell tabanlı komut satırı kısıtlı bir çalışma alanında yerleşik arabirimidir. Merhaba kullanıcı hello komut satırında Hello perspektifinden, kısıtlı bir çalışma alanı kısıtlı bir Windows PowerShell sürümü olarak görünür. Bazı Windows PowerShell temel özelliklerini hello korurken, bu arabirim Microsoft Azure StorSimple Cihazınızı yönetmek doğrultusunda sağlamıştır ek adanmış cmdlet'lere sahiptir. 

Bu makalede toothis arabirimi nasıl bağlanacağını dahil olmak üzere StorSimple özellikleri için Windows PowerShell hello ve bağlantıları toostep adım yordamları ya da bu arabirimi kullanarak gerçekleştirebilirsiniz iş akışları içerir. Hello iş akışlarının nasıl tooregister Cihazınızı hello ağ arabirimi aygıtınızda hello aygıt toobe bakım modunda gerektirir, hello cihaz durumunu değiştir güncelleştirmeleri yapılandırmak ve karşılaşabileceğiniz sorunları gidermek içerir.

Bu makaleyi okuduktan sonra aşağıdakileri gerçekleştirebilirsiniz:

* Tooyour StorSimple cihaz StorSimple için Windows PowerShell kullanarak bağlanın.
* StorSimple Cihazınızı StorSimple için Windows PowerShell kullanarak yönetebilirsiniz.
* Yardım StorSimple için Windows PowerShell'de alın.

> [!NOTE]
> * StorSimple cmdlet'leri için Windows PowerShell toomanage izin StorSimple Cihazınızı bir seri konsoldan veya uzaktan Windows PowerShell uzaktan iletişimini aracılığıyla. Her bir bu arabirimi kullanılabilir hello tek tek cmdlet'ler hakkında daha fazla bilgi için çok Git[StorSimple için Windows PowerShell için cmdlet başvurusu](https://technet.microsoft.com/library/dn688168.aspx).
> * Hello Azure PowerShell StorSimple cmdlet'leri, StorSimple hizmet düzeyi tooautomate ve geçiş görevleri hello komut satırından izin cmdlet'lerinin farklı bir koleksiyonudur. StorSimple için hello Azure PowerShell cmdlet'leri hakkında daha fazla bilgi için toohello Git [Azure StorSimple cmdlet başvurusu](/powershell/module/azure/?view=azuresmps-3.7.0).
> 
> 

Yöntemler aşağıdaki hello birini kullanarak StorSimple için Windows PowerShell hello erişebilirsiniz:

* [TooStorSimple cihaz seri konsoluna bağlanmak](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [Uzaktan Windows PowerShell kullanarak tooStorSimple Bağlan](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-toowindows-powershell-for-storsimple-via-hello-device-serial-console"></a>TooWindows PowerShell StorSimple için hello cihaz seri Konsolu bağlanma
Yapabilecekleriniz [PuTTY karşıdan](http://www.putty.org/) veya benzer terminal öykünme yazılımı tooconnect tooWindows StorSimple için PowerShell. Tooconfigure PuTTY ihtiyacınız özellikle tooaccess hello Microsoft Azure StorSimple cihazı. Merhaba aşağıdaki konular içerir ilgili ayrıntılı adımlar tooconfigure PuTTy ve toohello aygıtı bağlayın. Merhaba seri konsol içinde çeşitli menü seçeneklerini de açıklanmıştır.

### <a name="putty-settings"></a>PuTTY ayarları
PuTTY ayarları tooconnect toohello Windows PowerShell arabirimi hello seri konsoldan aşağıdaki hello kullandığınızdan emin olun.

#### <a name="tooconfigure-putty"></a>tooconfigure PuTTY
1. Merhaba PuTTY içinde **yeniden yapılandırma** iletişim kutusunda hello **kategori** bölmesinde, **klavye**.
2. Seçenekler aşağıdaki o hello seçili olduğundan emin olun (yeni bir oturum başlattığınızda hello varsayılan ayarları bunlar). 
   
   | Klavye öğesi | Şunu seçin: |
   | --- | --- |
   | Geri tuşu |Denetim-? (127) |
   | Giriş ve bitiş anahtarları |Standart |
   | İşlev tuşları ve tuş |ESC [n ~ |
   | İmleç anahtarların ilk durumu |Normal |
   | Sayısal tuş takımında başlangıç durumu |Normal |
   | Ek klavye özellikleri etkinleştirme |Denetim Alt AltGr farklı. |
   
    ![Desteklenen Putty ayarları](./media/storsimple-windows-powershell-administration/IC740877.png)
3. **Uygula**'ya tıklayın.
4. Merhaba, **kategori** bölmesinde, **çeviri**.
5. Merhaba, **uzak karakter kümesi** liste kutusunda **UTF-8**.
6. Altında **çizim karakterlerinden işleme**seçin **kullanım Unicode çizim kod noktaları**. Merhaba aşağıdaki şekilde hello doğru PuTTY seçimleri gösterilmektedir.
   
    ![UTF Putty ayarları](./media/storsimple-windows-powershell-administration/IC740878.png)
7. **Uygula**'ya tıklayın.

PuTTY tooconnect toohello cihaz seri konsoluna artık hello aşağıdaki adımları uygulayarak da kullanabilirsiniz.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-hello-serial-console"></a>Merhaba seri Konsolu hakkında
StorSimple Cihazınızı hello Windows PowerShell arabirimini hello seri konsol üzerinden eriştiğinizde, menü seçenekleri tarafından izlenen bir başlık iletisi görüntülenir. 

Merhaba başlık iletisi hello modeli, ad, yüklü yazılım sürümü ve eriştiğiniz hello denetleyicisi durumunu gibi temel StorSimple cihaz bilgileri içerir. Görüntü aşağıdaki hello bir başlık iletisi örneği gösterilmektedir.

![Seri tanıtıcı iletisi](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> Merhaba denetleyici olup olmadığına hello başlık iletisi tooidentify kullanabilirsiniz bağlı toois etkin veya Pasif.
> 
> 

Görüntü gösterir aşağıdaki hello hello seri konsol menüsünde kullanılabilir çeşitli çalışma alanı seçenekleri hello.

![2 Cihazınızı kaydedin](./media/storsimple-windows-powershell-administration/IC740906.png)

Ayarları aşağıdaki hello seçebilirsiniz:

1. **Oturum oturum tam erişim** bu seçenek, tooconnect (ile Merhaba doğru kimlik bilgileri) toohello tanır **SSAdminConsole** hello yerel denetleyicisinde çalışma. (Merhaba yerel denetleyici şu anda hello seri konsol StorSimple cihazınızın üzerinden eriştiğiniz hello denetleyicisi değil.) Bu seçenek de kullanılabilir tooallow Microsoft Support tooaccess Kısıtlanmamış çalışma (Destek oturumu) tootroubleshoot olası cihaz sorunları. Üzerinde seçeneği 1 toolog kullandıktan sonra belirli bir cmdlet çalıştırarak hello Microsoft Support mühendisi Kısıtlanmamış tooaccess çalışma izin verebilirsiniz. Ayrıntılar için çok başvurun[destek oturum başlatma](storsimple-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple).
2. **Tam erişimi olan toopeer denetleyicisinde oturum** (Merhaba doğru kimlik bilgileriyle) bağlanabilir bu seçeneği aynı seçeneği 1 olarak hello olmasıdır toohello **SSAdminConsole** hello eş denetleyicisinde çalışma. Merhaba StorSimple cihazı bir Aktif-Pasif yapılandırmasında iki denetleyicisi yüksek oranda kullanılabilirlik aygıtla olduğundan, eş toohello diğer denetleyicisi hello seri konsol üzerinden eriştiğiniz hello aygıtı ifade eder).
   Benzer toooption 1, bu seçenek ayrıca kullanılan tooallow Microsoft Support Kısıtlanmamış tooaccess çalışma eş denetleyicisinde olabilir.
3. **Sınırlı erişimi bağlantı** bu seçeneği kullanılan tooaccess Windows PowerShell arabirimi sınırlı moddur. Erişim kimlik bilgileri istenmez. Bu seçenek kısıtlanmış tooa karşılaştırıldığında çalışma toooptions 1 ve 2 bağlanır.  Seçenek 1 kullanılabilir hello görevlerden bazıları, **olamaz* bu çalışma alanında gerçekleştirilebilir şunlardır:
   
   * Toohello fabrika ayarlarına sıfırlama
   * Merhaba Parolayı Değiştir
   * Etkinleştirmek veya destek erişimini devre dışı bırakma
   * Güncelleştirme uygulama
   * Düzeltmeleri yükleme 

    > [!NOTE]
    > Merhaba cihaz Yöneticisi parolası unutmuş ve 1 veya 2 seçeneği üzerinden bağlanamıyorsa hello tercih edilen seçenek budur.

4. **Dili Değiştir** bu seçenek, toochange hello görüntüleme dilini hello Windows PowerShell arabiriminde sağlar. desteklenen hello dili, İngilizce, Japonca, Rusça, Fransızca, Güney Kore dili, İspanyolca, İtalyanca, Almanca, Çince ve Portekizce (Brezilya) gösterilebilir.

## <a name="connect-remotely-toostorsimple-using-windows-powershell-for-storsimple"></a>TooStorSimple StorSimple için Windows PowerShell kullanarak uzaktan bağlanma
Windows PowerShell uzaktan iletişim tooconnect tooyour StorSimple cihazı kullanabilirsiniz. Bu şekilde bağlandığınızda, menü görmezsiniz. (Yalnızca hello seri konsol hello aygıt tooconnect üzerinde kullanıyorsanız, bir menü görürsünüz. Uzaktan bağlanma, alır, doğrudan toohello denk "seçeneği 1 – tam erişim" Merhaba seri konsol.) Windows PowerShell uzaktan iletişimini ile tooa belirli çalışma bağlayın. Merhaba görüntüleme dili de belirtebilirsiniz. 

Merhaba görüntüleme dilini hello kullanarak ayarlamak hello dil bağımsızdır **Dili Değiştir** hello seri konsol menüsünde seçeneği. Uzak PowerShell belirtilmemişse içinden bağlanan hello yerel hello aygıt otomatik olarak seçer.

> [!NOTE]
> Microsoft Azure sanal konaklar ve StorSimple sanal cihazlar ile çalışıyorsanız, Windows PowerShell uzaktan iletişim ve hello sanal ana bilgisayar tooconnect toohello sanal cihazı kullanabilirsiniz. Bir paylaşımı konumu hello Windows PowerShell oturumunda hangi toosave bilgilerini hello konaktaki ayarladıysanız, yalnızca kimliği doğrulanmış kullanıcılar asıl herkes içerir, hello farkında olmalıdır. Bu nedenle, herkes tarafından hello paylaşım tooallow erişimi ayarladıysanız ve kimlik bilgilerini belirtmeden bağlanmak, hello kimliği doğrulanmamış anonim asıl kullanılacak ve bir hata görürsünüz. Bu sorunu, hello paylaşmak hello Konuk hesabını etkinleştirme ve hello Konuk hesabı tam erişim toohello paylaşımı veya verin konak toofix hello Windows PowerShell cmdlet'i ile birlikte geçerli kimlik bilgilerini belirtmeniz gerekir.
> 
> 

Windows PowerShell uzaktan iletişimini aracılığıyla HTTP veya HTTPS tooconnect kullanabilirsiniz. Eğitim aşağıdaki hello Hello yönergeleri kullanın:

* [HTTP kullanarak uzaktan bağlanma](storsimple-remote-connect.md#connect-through-http)
* [HTTPS kullanarak uzaktan bağlanma](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a>Bağlantı güvenlik konuları
Ne zaman karar tooconnect tooWindows StorSimple, PowerShell hello aşağıdaki nasıl dikkate alın:

* Doğrudan toohello bağlanma cihaz seri konsoluna güvenlidir, ancak ağ anahtarları üzerinden bağlanan toohello seri konsol değil. Toodevice seri ağ anahtarları bağlanırken hello güvenlik riskini dikkatli olun.
* Bir HTTP oturumu aracılığıyla bağlanan ağ üzerinden hello seri konsol üzerinden bağlanma daha fazla güvenlik sunar. Bu en güvenli yöntemi hello olmamasına karşın, güvenilen ağlarda kabul edilebilir.
* HTTPS oturumu aracılığıyla bağlanma hello en güvenli ve önerilen seçenek hello olur.

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a>StorSimple Cihazınızı StorSimple için Windows PowerShell kullanarak yönetme
Merhaba aşağıdaki tabloda tüm hello genel yönetim görevleri ve gerçekleştirilebilir karmaşık iş akışları özetini içinde StorSimple Cihazınızı hello Windows PowerShell arabirimini gösterir. Her bir iş akışı hakkında daha fazla bilgi için hello uygun hello tablo girişi'ı tıklatın.

#### <a name="windows-powershell-for-storsimple-workflows"></a>StorSimple iş akışları için Windows PowerShell
| Bu toodo isterseniz... | Bu yordamı kullanın. |
| --- | --- |
| Cihazınızı kaydedin |[StorSimple için Windows PowerShell kullanarak hello cihazı yapılandırma ve kaydetme](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| Web proxy yapılandırma</br>Görünümü web proxy ayarları |[StorSimple cihazınız için Web Proxy'yi Yapılandır](storsimple-configure-web-proxy.md) |
| Cihazınızda veri 0 ağ arabirimi ayarlarını değiştirme |[DATA 0 ağ arabirimindeki StorSimple cihazınız için değiştirme](storsimple-modify-data-0.md) |
| Bir denetleyici Durdur </br> Yeniden başlatma veya kapatma denetleyicisi </br> Bir cihazı kapatmak</br>Merhaba aygıt toofactory varsayılan ayarlarına sıfırlama |[Cihaz Denetleyicilerini Yönet](storsimple-manage-device-controller.md) |
| Bakım modu güncelleştirmeleri ve düzeltmeleri yüklemeniz |[Cihazınızı güncelleştirme](storsimple-update-device.md) |
| Bakım modu girin </br>Bakım modundan çık |[StorSimple cihaz modları](storsimple-device-modes.md) |
| Bir destek paketi oluştur</br>Şifresini çözmek ve Destek paketini Düzenle |[Oluşturma ve Destek Paketi yönetme](storsimple-create-manage-support-package.md) |
| Bir destek oturumu Başlat</br> |[StorSimple için Windows PowerShell içinde bir destek oturumu Başlat](storsimple-create-manage-support-package.md#manually-create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a>StorSimple için Windows PowerShell'de yardım alın
StorSimple için Windows PowerShell içinde cmdlet Yardım kullanılabilir. Bu Yardım çevrimiçi, güncel bir sürümünü de kullanabilirsiniz, kullanılabildiği sisteminizdeki tooupdate hello Yardım.

Windows PowerShell'de benzer toothat olduğundan bu arabirimde Yardım alma ve hello Yardım ile ilgili cmdlet'leri çoğunu çalışır. Yardım için Windows PowerShell çevrimiçi hello TechNet kitaplığında bulabilirsiniz: [ile Windows PowerShell komut dosyası](http://go.microsoft.com/fwlink/?LinkID=108518).

Merhaba, Yardım hello türleri nasıl tooupdate hello Yardım dahil olmak üzere bu Windows PowerShell arabirimi için kısa bir açıklaması verilmiştir.

#### <a name="tooget-help-for-a-cmdlet"></a>bir cmdlet için Yardım tooget
* Yardım tooget herhangi bir cmdlet veya işlev, komut aşağıdaki kullanım hello için:`Get-Help <cmdlet-name>`
* tooget herhangi bir cmdlet'i için çevrimiçi Yardım ile Merhaba hello önceki cmdlet'ini kullanın `-Online` parametre:`Get-Help <cmdlet-name> -Online`
* Tam Yardım almak için hello kullanabilirsiniz `–Full` parametresi ve örnekler için hello `–Examples` parametresi.

#### <a name="tooupdate-help"></a>tooupdate Yardım
Merhaba Yardım hello Windows PowerShell arabiriminde kolayca güncelleştirebilirsiniz. Sisteminizde adımları tooupdate hello Yardım aşağıdaki hello gerçekleştirin.

#### <a name="tooupdate-cmdlet-help"></a>tooupdate cmdlet Yardım
1. Windows PowerShell ile Merhaba Başlat **yönetici olarak çalıştır** seçeneği.
2. Merhaba komut satırına aşağıdakini yazın:`Update-Help`
3. Merhaba Yardım dosyalarının yüklü güncelleştirildi.
4. Merhaba Yardım dosyalarını yüklendikten sonra yazın: `Get-Help Get-Command`. Bu Yardım kullanılabilir cmdlet'lerin bir listesi görüntülenir.

> [!NOTE]
> bir çalışma tüm hello kullanılabilen cmdlet'leri listesi tooget toohello karşılık gelen menü seçeneğini oturum açın ve hello çalıştırın `Get-Command` cmdlet'i.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
İş akışları yukarıda hello birini gerçekleştirirken StorSimple cihazınızla herhangi bir sorunla karşılaşırsanız, çok başvuran[StorSimple dağıtım sorunlarını giderme araçları](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments).


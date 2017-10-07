---
title: Azure yedekleme sunucusu aaaTroubleshoot | Microsoft Docs
description: "Yükleme, kayıt Azure yedekleme sunucusu ve yedekleme ve geri yükleme uygulama iş yüklerinin sorunlarını giderme"
services: backup
documentationcenter: 
author: pvrk
manager: shreeshd
editor: 
ms.assetid: 2d73c349-0fc8-4ca8-afd8-8c9029cb8524
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pullabhk;markgal;
ms.openlocfilehash: 2386cfcfbf7cc686b5c051d2e1a3a884481ccdc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-server"></a>Azure Backup Sunucusu sorunlarını giderme

Azure yedekleme sunucusu bilgileri kullanarak, aşağıdaki tablonun hello listelenen sırasında oluşan hatalar giderebilirsiniz.


## <a name="installation-issues"></a>Yükleme sorunları

| İşlem | Hata ayrıntıları | Geçici çözüm |
|-----------|---------------|------------|
|Yükleme | Kurulum, kayıt defteri meta veriler güncelleştirilemedi. Bu güncelleştirme hatası depolama tüketimini tooover kullanımını yol açabilir. tooavoid bu Lütfen güncelleştirme hello ReFS kırpma kayıt defteri girişi. | Merhaba kayıt defteri anahtarı, SYSTEM\CurrentControlSet\Control\FileSystem\RefsEnableInlineTrim ayarlayın. Dword too1 Hello değerini ayarlayın. |
|Yükleme | Kurulum, kayıt defteri meta veriler güncelleştirilemedi. Bu güncelleştirme hatası depolama tüketimini tooover kullanımını yol açabilir. tooavoid bu Lütfen güncelleştirme hello birim SnapOptimization kayıt defteri girişi. | Merhaba kayıt defteri anahtarı, SOFTWARE\Microsoft veri koruma Manager\Configuration\VolSnapOptimization\WriteIds boş dize değeri ile oluşturun. |

## <a name="registration-and-agent-related-issues"></a>Kayıt ve aracı ilgili sorunlar
| İşlem | Hata ayrıntıları | Geçici çözüm |
| --- | --- | --- |
| Tooa kasası kaydediliyor | Geçersiz kasa kimlik bilgileri sağlandı. Merhaba dosya bozuk veya değil sahip hello kurtarma hizmeti ile ilişkilendirilmiş en yeni kimlik | toofix bu hata: <ol><li> Merhaba kasadan Hello son kimlik bilgileri dosyasını indirin ve tekrar deneyin <br>(VEYA)</li> <li> Eylem yukarıda Hello işe yaramadı, hello kimlik bilgilerini tooa farklı yerel dizin karşıdan yüklemeyi deneyin veya yeni bir kasa oluşturun <br>(VEYA)</li> <li> Başlangıç tarihi güncelleştirmeyi deneyin ve zaman içinde belirtildiği gibi ayarları [bu Web günlüğü](https://azure.microsoft.com/blog/troubleshooting-common-configuration-issues-with-azure-backup/) <br>(VEYA)</li> <li> C:\windows\temp birden fazla 65000 dosyaları olup olmadığını denetleyin. Eski dosyaların tooanother konumu veya hello Temp klasörü hello öğeleri silme <br>(VEYA)</li> <li> Sertifikaların Hello durumunu denetleyin <br> a. "Bilgisayar sertifikaları yönetme" (hello Denetim Masası) açın <br> b. Merhaba "Kişisel" ve onun alt düğümlerini "Sertifikalar" açın <br> c.  "Windows Azure Araçları" Merhaba sertifikayı Kaldır <br> d. Hello Azure Backup İstemcisi'nde Hello kayıt işlemini yeniden deneyin <br> (VEYA) </li> <li> Her Grup İlkesi yerinde olup olmadığını denetleyin </li></ol> |
| Aracıların tooprotected sunucularına iletme | Merhaba aracı işlemi başarısız oldu hello DPM aracı Düzenleyicisi hizmetindeki bir iletişim hatası nedeniyle üzerinde \<sunucuadı > | **Önerilen eylem Hello üründe gösterilen hello işe yaramazsa**, <ol><li> Bir bilgisayar güvenilmeyen bir etki alanından bağlıyorsanız izleyin [bu](https://technet.microsoft.com/library/hh757801(v=sc.12).aspx) adımları <br> (VEYA) </li><li> Bir bilgisayar güvenilen bir etki alanından bağlıyorsanız özetlenen hello adımları kullanarak sorun giderme [bu Web günlüğü](https://blogs.technet.microsoft.com/dpm/2012/02/06/data-protection-manager-agent-network-troubleshooting/) <br>(VEYA)</li><li> Sorun giderme adımı olarak virüsten koruma devre dışı bırakmayı deneyin. Merhaba sorunu çözümlenirse, önerilen [Bu makalede] hello virüsten koruma ayarlarını değiştirme (https://technet.microsoft.com/library/hh757911.aspx)</li></ol> |
| Aracıların tooprotected sunucularına iletme | sunucusu için belirtilen hello kimlik bilgileri geçersiz | **Önerilen eylem Hello üründe gösterilen hello işe yaramazsa**, <br> tooinstall hello koruma aracısını el ile belirtildiği gibi hello üretim sunucusu üzerinde deneyin [bu makalede](https://technet.microsoft.com/library/hh758186(v=sc.12).aspx#BKMK_Manual)|
| Azure Backup Aracısı yüklenemiyor tooconnect toohello Azure Backup hizmeti oluştu (kimlik: 100050) | Hello Azure Yedekleme aracısı yüklenemiyor tooconnect toohello Azure Backup hizmeti oluştu. | **Önerilen eylem Hello üründe gösterilen hello işe yaramazsa**, <br>1. Psexec yükseltilmiş gelen komut isteminde, komutu çalıştırın -i - Internet explorer penceresi açılır s "c:\Program Files\Internet Explorer\iexplore.exe". <br/> 2. Git tooTools Internet Seçenekleri -> -> bağlantıları LAN Ayarları ->. <br/> 3. Sistem hesabı için proxy ayarlarını doğrulayın. Proxy IP ve bağlantı noktası ayarlayın. <br/> 4. Internet Explorer'ı kapatın.|
| Azure Backup Aracısı yüklemesi başarısız oldu | Merhaba Microsoft Azure kurtarma Hizmetleri yüklemesi başarısız oldu. Microsoft Azure kurtarma Hizmetleri Yükleme toohello sistem Hello tarafından yapılan tüm değişiklikler geri alındı. (KİMLİK: 4024) | El ile Azure aracısını yükleyin


## <a name="configuring-protection-group"></a>Koruma grubu yapılandırma
| İşlem | Hata ayrıntıları | Geçici çözüm |
| --- | --- | --- |
| Koruma gruplarını yapılandırma | DPM, korunan bilgisayarda (korunan bilgisayar adı) uygulama bileşeni numaralandıramadı | '' Hello üzerinde Yenile hello ilgili veri kaynağı/bileşen düzeyinde koruma grubu UI ekran yapılandırın |
| Koruma gruplarını yapılandırma | %S tooconfigure koruma | Merhaba korumalı sunucu bir SQL sunucusu ise, sysadmin rolü izinleri (ntauthority\system adlı) toohello sistem hesabını hello korumalı bilgisayarda de belirtildiği gibi sağlanmış olan olup olmadığını denetleyin [bu makalede](https://technet.microsoft.com/library/hh757977(v=sc.12).aspx)
| Koruma gruplarını yapılandırma | Bu koruma grubu için hello depolama havuzunda yeterli boş alan yok | Merhaba toohello depolama havuzuna eklenen diskler [bir bölüm içermemelidir](https://technet.microsoft.com/library/hh758075(v=sc.12).aspx). Merhaba disklerdeki mevcut birimler silin ve toohello depolama havuzuna ekleyin|
| İlke değişikliği |Merhaba yedekleme İlkesi değiştirilemedi. Hata: tooan iç hizmet hatası [0x29834] hello geçerli işlem başarısız oldu. Lütfen hello işlemi bir süre sonra yeniden deneyin. Merhaba sorun devam ederse, lütfen Microsoft Destek'e başvurun. |**Neden:**<br/>Bu hata, güvenlik ayarlarını etkinleştirdiğinizde, yukarıda belirtilen minimum değerler hello aşağıda tooreduce bekletme aralığı deneyin ve (aşağıda MAB sürüm 2.0.9052 ve Azure yedekleme sunucusu güncelleştirme 1) desteklenmeyen bir sürümü bulunuyor, gelir. <br/>**Önerilen eylem:**<br/> Bu durumda, yukarıda belirtilen dönem hello minimum bekletme (günlük, haftalık, üç hafta aylık veya yıllık yedekleme için bir yıl için dört hafta için yedi gün) saklama dönemi ayarlamalısınız tooproceed ilkesiyle ilgili güncelleştirdi. İsteğe bağlı olarak, tercih edilen yaklaşım tooupdate yedekleme aracısını ve Azure yedekleme sunucusu tooleverage olacak tüm güvenlik güncelleştirmeleri hello. |

## <a name="backup"></a>Backup
| İşlem | Hata ayrıntıları | Geçici çözüm |
| --- | --- | --- |
| Backup | Çoğaltma tutarsız | Merhaba nedenlerini çoğaltma tutarsızlık ve ilgili öneriler hakkında daha fazla ayrıntı bulabilirsiniz [burada](https://technet.microsoft.com/library/cc161593.aspx) <br> <ol><li> Windows Server Yedekleme yüklü olup olmadığını veya korumalı sunucuda değil, sistem durumu/BMR yedekleme durumunda lütfen denetleyin </li><li> Denetlemek için alanı ilgili sorunlar DPM depolama havuzu hello DPM/MABS sunucusunda ve gerektikçe depolama alanı Ayır </li><li> Merhaba birim gölge kopyası hizmeti hello korumalı sunucuda Hello durumunu denetleyin. İçinde ise devre dışı durumunu toostart el ile ayarlayın ve hello sunucuda hello hizmetini başlatın. Ardından toohello DPM/MABS konsol geri dönün ve tutarlılık denetimiyle birlikte hello eşitleme başlatın.</li></ol>|
| Backup | Merhaba iş çalışırken beklenmeyen bir hata oluştu, hello cihaz hazır değil | **Önerilen eylem Hello üründe gösterilen hello işe yaramazsa**, <br> <ol><li>Merhaba koruma grubundaki hello öğelerde Hello gölge kopya depolama alanı toounlimited ayarlayın ve hello tutarlılık denetimini Çalıştır <br></li> (VEYA) <li>– Tek tek her öğesinde biriyle birden çok yeni kampanya oluşturmak ve Hello mevcut koruma grubunu silme deneyin</li></ol> |
| Backup | Yalnızca sistem durumu yedeklemesi yedekliyorsanız hello korunan bilgisayar toostore hello sistem durumu yedeklemesi üzerinde yeterli boş alan olup olmadığını doğrulayın | <ol><li>Bu ' % s'hello WSB korumalı hello makinede yüklü olduğundan emin olun</li><li>Yeterli alan hello sistem durumunu hello korumalı bilgisayar üzerinde var olduğunu doğrulayın: en kolay yolu toodo hello bu toogo toohello korunan bilgisayar, WSB açın ve hello seçimlerinizi ' ı tıklatın ve BMR seçin. Merhaba UI sonra ne kadar bu gerekli bir alandır söyler. Açık WSB -> yerel yedekleme -> Yedekleme zamanlaması seçin yedekleme yapılandırması -> tam sunucu -> (boyutu görüntülenir). Bu boyut doğrulama için kullanın.</li></ol>
| Backup | Çevrimiçi kurtarma noktası oluşturma başarısız oldu | Merhaba hata iletisi diyorsa "Windows Azure Yedekleme aracısı yüklenemiyor toocreate seçili hello görüntüsünü olan birim", Lütfen çoğaltma ve kurtarma noktası birimi artan hello alanı deneyin.
| Backup | Çevrimiçi kurtarma noktası oluşturma başarısız oldu | Merhaba hata iletisi diyorsa "Windows hello Azure Yedekleme aracısı toohello OBEngine hizmetine bağlanamıyor", hizmetleri hello bilgisayarda çalışan hello listesi bulunmaktadır OBEngine bu hello doğrulayın. Merhaba OBEngine hizmetinin kullanımı hello "net start OBEngine" komutu toostart hello OBEngine hizmet çalışmıyorsa.
| Backup | Çevrimiçi kurtarma noktası oluşturma başarısız oldu | Merhaba hata iletisi diyorsa "Merhaba bu sunucunun şifreleme parolası ayarlanmamış. Lütfen bir şifreleme parolası yapılandırın"bir şifreleme parolası yapılandırmayı deneyin. Başarısız olursa, <br> <ol><li>Merhaba karalama konumu veya mevcut olup olmadığını denetleyin. Kayıt defterinde hello HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config "ScratchLocation" adıyla belirtilen hello konumu var olmalıdır.</li><li> Merhaba karalama konum mevcutsa, hello eski parolayı kullanarak yeniden deneyin. **Lütfen bir şifreleme parolası yapılandırdığınız zaman, güvenli bir konuma kaydedin**</li><ol>
| Backup | BMR için yedekleme hatası | BMR boyutu çok büyük, ise bazı uygulama dosyaları tooOS sürücüsü taşıdıktan sonra yeniden deneyin |
| Backup | Dosyaları ve paylaşılan klasörlerin erişilirken hata oluştu | Önerilen Hello virüsten koruma ayarlarını değiştirmeyi deneyin [burada](https://technet.microsoft.com/library/hh757911.aspx)|
| Backup | VMware VM için çevrimiçi kurtarma noktası oluşturma işleri başarısız olur. DPM, tooget ChangeTracking bilgi çalışırken VMware hatayla karşılaştı. ErrorCode - FileFaultFault (ID 33621) |  1. Merhaba VM'ler etkilenen VMWare üzerinde hello ctk Sıfırla <br/> Bağımsız disk VMWare yerinde değil onay <br/> Etkilenen hello VM'ler için korumayı durdurun ve yeniden Yenile düğmesini ile koruyun <br/> Bir bilgi etkilenen hello VM'ler için Çalıştır|


## <a name="change-passphrase"></a>Parola değiştirme
| İşlem | Hata ayrıntıları | Geçici çözüm |
| --- | --- | --- |
| Parola değiştirme |Güvenlik girdiğiniz PIN yanlış. Bu işlem Hello doğru güvenlik PIN toocomplete sağlar. |**Neden:**<br/> (Parola değiştirme gibi) kritik işlemi gerçekleştirirken geçersiz veya süresi dolmuş güvenlik PIN girdiğinizde, bu hata verilir. <br/>**Önerilen eylem:**<br/> toocomplete hello işlemi, geçerli güvenlik PIN girmeniz gerekir. tooget PIN Merhaba, tooAzure Portalı'nda oturum açın ve tooRecovery Hizmetleri kasasına gidin > Ayarlar > Özellikler > Güvenlik PIN oluşturun. Bu PIN toochange parolayı kullanın. |
| Parola değiştirme |İşlem başarısız oldu. KİMLİĞİ: 120002 |**Neden:**<br/>Bu hata, güvenlik ayarları etkin, toochange parolayı deneyin ve desteklenmeyen sürümü gelir.<br/>**Önerilen eylem:**<br/> toochange parola ilk güncelleştirme yedekleme aracısını toominimum sürümü en düşük 2.0.9052 ve Azure yedekleme sunucusu toominimum güncelleştirme 1 gerekir, geçerli güvenlik PIN girin. tooget PIN Merhaba, tooAzure Portalı'nda oturum açın ve tooRecovery Hizmetleri kasasına gidin > Ayarlar > Özellikler > Güvenlik PIN oluşturun. Bu PIN toochange parolayı kullanın. |


## <a name="configure-email-notifications"></a>E-posta bildirimleri yapılandırma
| İşlem | Hata ayrıntıları | Geçici çözüm |
| --- | --- | --- |
| E-posta bildirimleri Office365 hesabı kullanarak yukarı tooset çalışıyor. | Hata kimliği alma: 2013| **Neden:**<br/> Toouse Office 365 hesabı çalışıyor <br/> **Önerilen eylem:**<br/> Merhaba ilk şey tooensure "İzin anonim geçiş üzerinde bir alma bağlayıcısında" DPM sunucunuz için Exchange'deki Kurulum olmasıdır. Şöyle bir bağlantı tooconfigure bu: http://technet.microsoft.com/en-us/library/bb232021.aspx <br/> İç SMTP geçişine kullanın ve Office 365 sunucunuz kullanarak yukarı tooset ihtiyacınız varsa, IIS toobe geçiş bunu için ayarlayabilirsiniz. <br/> IIS https://technet.microsoft.com/en-us/library/aa995718(v=exchg.65).aspx toosetup IIS toorelay tooO365 kullanarak tooconfigure hello DPM sunucusu toobe mümkün toorelay hello SMTP tooO365 gerekir <br/> Önemli Not: adım 3 -> g emin toouse olması, II -> user@domain.com biçimi ve olmayan etki alanı\kullanıcı <br/> Noktası DPM toouse 587 numaralı bağlantı noktalarını SMTP sunucusu olarak yerel servername hello ve hello e-postaları alınması gereken kullanıcı e-posta hello. <br/> Merhaba kullanıcı adı ve parola hello DPM SMTP Kurulum sayfasında DPM açıktır hello etki alanındaki bir etki alanı hesabı olmalıdır. <br/> Not: hello SMTP sunucu adresi değiştirirken hello toonew ayarlarını değiştirmek, hello ayarları kutusunu kapatıp toobe hello yeni değer gösterdiğinden emin olun.  Her zaman bu şekilde test en iyi uygulamadır şekilde yalnızca değiştirme ve sınama hello yeni ayarları olmayacaktır. <br/> Bu işlem sırasında herhangi bir zamanda bu ayarları DPM Konsolu kapatmak ve kayıt defteri anahtarlarını aşağıdaki hello düzenleme temizleyebilir:<br/> HKLM\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Notification\ <br/> SMTPPassword ve SMTPUserName anahtarlarını silin. <br/> Yeniden başlattığınızda geri hello UI ekleyebilirsiniz.

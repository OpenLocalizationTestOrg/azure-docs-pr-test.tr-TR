---
title: Azure sanal makine yedekleme hatalarla aaaTroubleshoot | Microsoft Docs
description: "Yedekleme ve geri yükleme Azure sanal makinelerin sorun giderme"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 73214212-57a4-4b57-a2e2-eaf9d7fde67f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: trinadhk;markgal;jpallavi;
ms.openlocfilehash: 9224c47e02b52688adcba5876c674c88502557c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Azure sanal makine yedekleme sorunlarını giderme
> [!div class="op_single_selector"]
> * [Kurtarma Hizmetleri kasası](backup-azure-vms-troubleshoot.md)
> * [Yedekleme kasası](backup-azure-vms-troubleshoot-classic.md)
>
>

Azure Backup ile bilgileri kullanarak hello aşağıdaki tabloda listelenen karşılaştı hataları giderebilirsiniz.

## <a name="backup"></a>Backup
| Hata ayrıntıları | Geçici çözüm |
| --- | --- |
| VM artık gibi hello işlem gerçekleştirilemedi. -Sanal makine yedekleme verileri silmeden korumayı durdurun. Http://go.microsoft.com/fwlink/?LinkId=808124 daha fazla bilgi |Bu hello birincil VM silinmez, ancak hello yedekleme ilkesi için bir VM tooback bakan devam olur. toofix bu hata: <ol><li> Merhaba ile Merhaba sanal makine yeniden aynı ada ve aynı kaynak grubu adı [bulut hizmet adı]<br>(VEYA)</li><li> Sanal makine ile veya olmadan hello yedekleme verileri silme korumayı durdurun. [Daha fazla ayrıntı](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| Anlık görüntü işlemi hello sanal makinedeki - toono ağ bağlantısı nedeniyle başarısız oldu, VM ağ erişimi bulunduğundan emin olun. Anlık görüntü toosucceed da beyaz liste Azure veri merkezi IP aralıkları veya ağ erişimi için bir proxy sunucusu ayarlayın. Daha fazla ayrıntı için çok başvurun http://go.microsoft.com/fwlink/?LinkId=800034. Proxy sunucu kullanıyorsanız, proxy sunucusu ayarlarının doğru şekilde yapılandırıldığından emin olun | Merhaba giden internet bağlantısı hello sanal makine üzerinde reddetme olduğunda bu hata atılır. VM anlık görüntü uzantısı tootake temel disk hello sanal makinenin bir anlık görüntü için Internet bağlantısı gereklidir. [Daha fazla bilgi edinin](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#snapshot-operation-failed-due-to-no-network-connectivity-on-the-virtual-machine) toofix hataları nedeniyle tooblocked ağ erişimi nasıl anlık görüntü üzerinde. |
| VM Aracısı'hello Azure Backup hizmeti ile oluşturulamıyor toocommunicate ' dir. -Hello VM ağ bağlantısı olduğunu ve hello VM Aracısı en son ve çalıştığından emin olun. Daha fazla bilgi için lütfen çok başvurun http://go.microsoft.com/fwlink/?LinkId=800034 |Bu hata, hello VM Aracısı ile ilgili bir sorun veya ağ erişim toohello Azure altyapı herhangi bir yolla engellendi atılır. [Daha fazla bilgi edinin](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vm-agent-unable-to-communicate-with-azure-backup) sorunları VM'yi hata ayıklama hakkında anlık görüntüsünü alın.<br> Merhaba VM Aracısı sorunları neden, hello VM yeniden başlatın. Bazen, yanlış bir VM durum sorunlara neden olabilir ve bu "bozuk durum" Merhaba VM yeniden başlatma sıfırlar. |
| Başarısız sağlama durumda VM - Lütfen hello VM yeniden başlatın ve bu hello VM çalışıyor veya kapatma için yedekleme durumda olduğundan emin olun | Bu durum, hello uzantı hataları birini VM durumu toobe sağlama durumu başarısız olarak müşteri adayları oluşur. Tooextensions listesine gidin ve başarısız bir uzantısı olup olmadığını, kaldırmak ve hello sanal makineyi yeniden başlatmayı deneyin. Tüm uzantıları çalışır durumda olduğundan, VM aracısı hizmetinin çalışıp çalışmadığını denetleyin. Aksi durumda, hello VM Aracısı hizmetini yeniden başlatın. | 
| VMSnapshot uzantısı işlemi için yönetilen diskleri - Lütfen yeniden deneme hello yedekleme işlemi başarısız oldu. Merhaba sorun devam ederse, 'http://go.microsoft.com/fwlink/?LinkId=800034' hello yönergeleri izleyin. Daha fazla başarısız olursa, lütfen Microsoft Destek'e başvurun | Azure Backup hizmeti tootrigger bir anlık görüntü başarısız olduğunda bu hata oluştu. [Daha fazla bilgi edinin](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vmsnapshot-extension-operation-failed) sorunları VM hata ayıklama hakkında anlık görüntüsünü alın. |
| Merhaba premium depolama disklerde mevcut toohello verileri toohello sanal makineye bağlı olmayan kopyalama hello hello sanal makinenin anlık görüntüsünü, hello depolama hesabı - tooinsufficient boş alanı nedeniyle depolama hesabı eşdeğer boş alan olduğundan emin | Premium VM'ler durumunda hello anlık görüntü toostorage hesabı kopyalayın. Bu toomake anlık görüntü üzerinde çalışır, yedekleme yönetim trafiği premium diskleri kullanarak IOPS kullanılabilir toohello uygulama hello sayısı sınırı değil emin olur. Microsoft, hello Azure Backup hizmeti depolama hesabı toohello kasasında kopyalanan bu konumdan Merhaba, anlık görüntü toostorage hesabı ve aktarım verilerini kopyalayabilmesi için yalnızca %50 hello toplam depolama hesabı alanının tahsis önerir. | 
| Yüklenemiyor tooperform hello işlemi hello VM aracısı yanıt vermiyor |Bu hata, hello VM Aracısı ile ilgili bir sorun veya ağ erişim toohello Azure altyapı herhangi bir yolla engellendi atılır. Windows VM'ler için hizmetleri ve hello Aracısı Denetim Masası'ndaki Programlar görüntülenip hello VM aracısı hizmet durumunu denetleyin. Try kaldırma hello programdan belirtildiği gibi Denetim Masası ve yeniden yüklenmeden hello Aracısı [aşağıda](#vm-agent). Merhaba aracıyı yeniden yükledikten sonra bir geçici yedekleme tooverify tetikler. |
| Kurtarma Hizmetleri Uzantısı işlemi başarısız oldu. -Lütfen hello sanal makinede en son sanal makine Aracısı'nın ve aracı hizmetinin çalıştığından emin olun. Lütfen yedekleme işlemini yeniden deneyin ve başarısız olursa, Microsoft Destek'e başvurun. |VM Aracısı güncel olduğunda bu hata oluşturulur. Tooupdate hello VM aracısı aşağıdaki "Güncelleştirme hello VM Aracısı" bölümüne bakın. |
| Sanal makine yok. -Lütfen sanal makinenin var olduğundan emin olun veya farklı bir sanal makine seçin. |Bu, hello birincil VM silindiği, ancak bir VM tooperform yedekleme toolook hello yedekleme İlkesi devam durumlarda gerçekleşir. toofix bu hata: <ol><li> Merhaba ile Merhaba sanal makine yeniden aynı ada ve aynı kaynak grubu adı [bulut hizmet adı]<br>(VEYA)<br></li><li>Merhaba yedekleme verileri silmeden Hello sanal makine korumasını durdurun. [Daha fazla ayrıntı](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| Komut yürütme başarısız oldu. -Başka bir işlem şu anda bu öğeyi sürüyor. Merhaba önceki işlem tamamlanana kadar bekleyin ve sonra yeniden deneyin |Var olan bir yedeğini hello VM üzerinde çalıştığından ve hello mevcut iş çalışırken yeni bir işi başlatılamıyor. |
| VHD'ler hello yedekleme Kasası'nı kopyalama zaman aşımına uğradı - Lütfen hello işlemi birkaç dakika içinde yeniden deneyin. Merhaba sorun devam ederse, Microsoft Support başvurun. | Bu depolama tarafında geçici bir hata varsa veya yedekleme hizmeti yeterli IOPS hello VM sipariş tootransfer verilerini zaman aşımı dönemi toovault içinde barındırma depolama hesabından almaktır değil gerçekleşir. Uyguladığınız emin olun [en iyi uygulamalar](backup-azure-vms-introduction.md#best-practices) yedekleme ayarı oluştu. Yüklü değilse VM tooa farklı depolama hesabı taşımayı deneyin ve yedeklemeyi yeniden deneyin.|
| Yedekleme bir iç hatayla başarısız oldu - Lütfen hello işlemi birkaç dakika içinde yeniden deneyin. Merhaba sorun devam ederse, Microsoft Support başvurun |2 nedenlerden dolayı bu hatayı alabilirsiniz: <ol><li> Merhaba VM depolama erişirken geçici bir sorun yoktur. Lütfen denetleyin [Azure durum](https://azure.microsoft.com/en-us/status/) devam eden herhangi bir sorun varsa toosee ilgili toocompute, depolama veya ağ hello bölgede. Merhaba sorun çözüldüğünde hello yedekleme işini yeniden deneyin. <li>Merhaba özgün VM silindi ve bu nedenle, hello kurtarma noktası alınamaz. tookeep silinmiş bir VM için yedekleme verileri Merhaba, ancak hello yedekleme hataları kaldırın: hello VM korumasını kaldırın ve hello seçeneği tookeep hello verileri seçin. Bu eylemin hello zamanlanmış yedekleme işi ve hello yinelenen hata iletileri durdurur. |
| Tooinstall hello Azure kurtarma Hizmetleri Uzantısı hello seçili öğe üzerinde başarısız oldu - hello VM Aracısı'hello Azure kurtarma Hizmetleri uzantısı için ön koşuldur. Hello Azure VM aracısı yükleyin ve hello kayıt işlemini yeniden başlatın |<ol> <li>Merhaba VM Aracısı doğru şekilde yüklenip yüklenmediğini denetleyin. <li>Merhaba VM config Hello bayrağı doğru ayarlandığından emin olun.</ol> [Daha fazla bilgi](#validating-vm-agent-installation) hello VM aracısı ve nasıl toovalidate hello VM Aracısı yükleme yükleme hakkında. |
| Uzantı yüklemesi "COM + oluşturulamıyor tootalk toohello Microsoft Distributed Transaction Coordinator edildi hello hatasıyla başarısız oldu |Bu, genellikle hello COM + hizmeti çalışmadığı anlamına gelir. Bu sorunu düzeltme konusunda yardım için Microsoft Destek'e başvurun. |
| VSS işlemi hatası ile Merhaba "Bu sürücünün BitLocker Sürücü Şifrelemesi tarafından kilitlenmiş. anlık görüntü işlemi başarısız Merhaba Denetim Masası'ndan bu sürücünün kilidini açmanız gerekir. |Hello VM üzerindeki tüm sürücüleri için BitLocker'ı açın ve hello VSS sorunun giderilip giderilmediğini inceleyin |
| VM yedeklemeleri izin veren bir durumda değil. |<ul><li>VM aşağı çalışan ve bilgisayarı arasında geçici bir durumda olup olmadığını denetleyin. İse, hello VM durumu toobe için bunlardan birini bekleyin ve tetiklemek yeniden yedekleme. <li> Merhaba VM bir Linux VM kullanır [güvenlik Gelişmiş Linux] çekirdek modülü ise, tooexclude hello Linux Aracısı yolu gerekir (_/var/lib/waagent_) güvenlik ilkesi toomake emin yedekleme uzantısı yüklü.  |
| Azure sanal makine bulunamadı. |Bu, hello birincil VM silindiği, ancak yedekleme için bir VM tooperform toolook hello yedekleme İlkesi devam durumlarda gerçekleşir. toofix bu hata: <ol><li>Merhaba ile Merhaba sanal makine yeniden aynı ada ve aynı kaynak grubu adı [bulut hizmet adı] <br>(VEYA) <li> Merhaba yedekleme işleri oluşturulmayacak şekilde bu VM için korumayı devre dışı bırakın. </ol> |
| Sanal makine aracısını hello sanal makinede mevcut değil - Lütfen herhangi bir önkoşulu ve hello VM aracısı yükleyin ve hello işlemi yeniden deneyin. |[Daha fazla bilgi](#vm-agent) VM Aracısı yükleme ve nasıl toovalidate hello VM Aracısı yükleme hakkında. |
| Anlık görüntü işlemi hatalı durumda tooVSS yazıcılarının nedeniyle başarısız oldu |Hatalı durumda toorestart (birim gölge kopyası hizmeti) VSS yazıcılarının gerekir. tooachieve Bu, yükseltilmiş bir komut isteminden çalıştırın _vssadmin listesi yazıcılarının_. Çıktı tüm VSS yazıcılarının ve durumlarını içerir. Değil "[1] kararlı" durumu olan her VSS yazıcısı için VSS Yazıcı komutları yükseltilmiş komut isteminden aşağıdaki çalıştırarak yeniden başlatın:<br> _net stop serviceName_ <br> _net start serviceName_|
| Anlık görüntü işlemi tooa ayrıştırma hatası hello yapılandırması başarısız oldu |Bu hello MachineKeys dizini toochanged izinleri nedeniyle gerçekleşir: _%systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br>Lütfen aşağıdaki komutunu çalıştırın ve varsayılan olanları MachineKeys dizin üzerindeki izinleri doğrulayın:<br>_icacls %systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br><br> Varsayılan izinler şunlardır:<br>Everyone:(R,W) <br>BUILTIN\Administrators:(F)<br><br>MachineKeys dizinindeki varsayılandan farklı izinleri görürseniz, lütfen adımları toocorrect izinleri uygulayın, hello sertifika silin ve hello yedeklemeyi başlatın.<ol><li>İzinleri MachineKeys dizinde düzeltin.<br>Explorer güvenlik özellikleri ve Gelişmiş güvenlik ayarları hello dizinde kullanarak, sıfırlama izinleri geri toohello varsayılan değerleri, herhangi bir ek (varsayılan) daha kullanıcı nesnesi hello dizininden kaldırın ve bu hello 'Everyone' sağlamak izinleri özel vardı erişim için:<br>-Liste klasörü / veri okuma <br>-Öznitelikleri okuması <br>-Genişletilmiş öznitelikleri okuması <br>-Dosya Oluştur / Veri Yaz <br>-Klasör Oluştur / Veri Ekle<br>-Öznitelikleri yazma<br>-Yazma genişletilmiş öznitelikleri<br>-Okuma izinleri<br><br><li>Tüm sertifikaları 'Issued To' alanıyla silmek = "Windows Azure hizmet yönetimi için uzantıları" veya "Windows Azure CRP sertifika Oluşturucu".<ul><li>[Sertifikalar (yerel bilgisayar) konsolunu açın](https://msdn.microsoft.com/library/ms788967(v=vs.110).aspx)<li>Tüm sertifikaları sil (Sertifikalar -> kişisel altında) 'İçin verilen' alanıyla = "Windows Azure hizmet yönetimi için uzantıları" veya "Windows Azure CRP sertifika Oluşturucu".</ul><li>Tetikleyici VM yedekleme. </ol>|
| Sanal makine BEK ile tek başına şifrelenmiş olarak doğrulaması başarısız oldu. Yalnızca şifrelenmiş BEK ve KEK ile sanal makineleri için yedeklemeleri etkinleştirilebilir. |Sanal makine, BitLocker şifreleme anahtarını ve anahtar şifreleme anahtarı kullanarak şifrelenmelidir. Bundan sonra yedekleme etkinleştirilmelidir. |
| Azure Backup hizmeti, yedekleme, şifrelenmiş sanal makineler için yeterli izinleri tooKey Kasa yok. |Yedekleme hizmeti sağlanmalıdır PowerShell'de bu izinleri belirtilen adımları kullanarak **yedeklemeyi etkinleştir** bölümünü [PowerShell belgelerine](backup-azure-vms-automation.md). |
|Yüklemesini anlık görüntü uzantı hatasıyla başarısız oldu - COM + oluşturulamıyor tootalk toohello Microsoft Dağıtılmış İşlem Düzenleyicisi | Lütfen deneyin toostart windows hizmeti "COM + Sistem uygulaması" (yükseltilmiş komut isteminden - _net Başlat COMSysApp_). <br>Başlatma sırasında başarısız olursa, lütfen aşağıdaki adımları izleyin:<ol><li> Oturum açma hesabını hizmeti "Dağıtılmış İşlem Düzenleyicisi" Hello "Network Service" olduğunu doğrulayın. Değilse, lütfen değiştirmek çok "Network Service" Bu hizmetini yeniden başlatın ve sonra toostart hizmeti "COM + Sistem uygulaması" deneyin.'<li>Toostart yine başarısız olursa, kaldırma/hizmet "Dağıtılmış İşlem Düzenleyicisi" aşağıdaki adımları izleyerek yükle:<br> -Hello MSDTC hizmetini durdurun<br> -Bir komut istemi (cmd) açın <br> -Komutu çalıştır "msdtc-kaldırma" <br> -Komutu çalıştır "msdtc-yükleyin" <br> -Hello MSDTC hizmetini Başlat<li>Windows hizmeti "COM + Sistem uygulaması" başlatın ve başlatıldıktan sonra portalından yedeklemeyi başlatın.</ol> |
|  Anlık görüntü işlemi tooCOM + hatası başarısız oldu | Merhaba önerilen eylem toorestart windows hizmeti "COM + Sistem uygulaması" (yükseltilmiş komut isteminden - _net Başlat COMSysApp_). Merhaba sorun devam ederse hello VM yeniden başlatın. VM değil Yardım hello yeniden başlatmayı deneyin [kaldırma hello VMSnapshot uzantısı](https://docs.microsoft.com/en-us/azure/backup/backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout#cause-3-the-backup-extension-fails-to-update-or-load) ve hello yedeklemeyi el ile başlatın. |
| Toofreeze biri başarısız oldu veya daha fazla bağlama noktaları, VM tootake dosya sistemi ile tutarlı bir anlık görüntü hello | Merhaba aşağıdaki adımları kullanın: <ol><li>Merhaba dosya sistemi kullanan tüm bağlı aygıtları durumunu denetlemek _'tune2fs'_ komutu.<br> Örn: tune2fs -m/dev/sdb1 \| GREP "Dosya sistemi durumu" <li>Merhaba aygıtlar için hangi dosya sistemi durumu değil temiz kullanarak çıkarın _'umount'_ komutu <li> Kullanarak bu cihazları üzerinde FileSystemConsistency denetimi Çalıştır _'fsck'_ komutu <li> Merhaba aygıtları yeniden bağlayın ve yedekleme deneyin.</ol> |
| Anlık görüntü işlemi nedeniyle başarısız oldu toofailure iletişim kanalını güvenli ağ oluşturma | <ol><Li> Yükseltilmiş modda regedit.exe çalıştırarak kayıt defteri Düzenleyicisi'ni açın. <li> Tüm sürümleri tanımlayın. NetFramework sistemde mevcut. Kayıt defteri anahtarı "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft" Merhaba hiyerarşisi altında mevcut <li> Her biri için. Kayıt defteri anahtarında mevcut NetFramework anahtarı ekleyin: <br> "SchUseStrongCrypto" = dword: 00000001 </ol>|
| Anlık görüntü işlemi nedeniyle başarısız oldu toofailure Visual C++ yeniden dağıtılabilir yüklemesinde Visual Studio 2012 için | TooC:\Packages\Plugins\Microsoft.Azure.RecoveryServices.VMSnapshot\agentVersion gidin ve vcredist2012_x64 yükleyin. Bu hizmeti yüklemesi izin vermek için kayıt defteri anahtarı değerini toocorrect değeri yani kayıt defteri anahtarının değeri ayarlandığından emin olun _HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSIServer_ too3 ve değil 4 ayarlayın. Yükleme sorunları devam bakacak, çalıştırarak Yükleme hizmeti yeniden başlatın _MSIEXEC /UNREGISTER_ arkasından _MSIEXEC /REGISTER_ yükseltilmiş bir komut isteminden.  |


## <a name="jobs"></a>İşler
| Hata ayrıntıları | Geçici çözüm |
| --- | --- |
| İptal bu iş türü için desteklenmeyen - hello iş tamamlanana kadar bekleyin. |None |
| Merhaba işi iptal edilebilen bir durumda değil - hello iş tamamlanana kadar bekleyin. <br>OR<br> Merhaba seçili işi iptal edilebilen bir durumda değil - hello iş toocomplete için bekleyin. |Tüm olasılığını içinde hello iş neredeyse tamamlandı. Merhaba iş tamamlanana kadar bekleyin.|
| Merhaba işi devam eden değil - iptal yalnızca sürmekte olan işleri için desteklenen olduğundan iptal edemezsiniz. Lütfen girişimi iptal bir sürüyor işi. |Tooa geçici durumu meydana gelir. Bir dakika bekleyin ve hello İptal işlemi yeniden deneyin. |
| Başarısız toocancel hello iş - işi tamamlanana kadar bekleyin. |None |

## <a name="restore"></a>Geri Yükleme
| Hata ayrıntıları | Geçici çözüm |
| --- | --- |
| Geri yükleme bulut iç hata vererek başarısız oldu |<ol><li>Bulut hizmeti toowhich toorestore çalıştığınız DNS ayarlarla yapılandırılır. Kontrol edebilirsiniz <br>$deployment get-AzureDeployment - ServiceName "ServiceName" =-yuvası "Üretim" Get-AzureDns - DnsSettings $deployment. DnsSettings<br>Yapılandırılmış adresi varsa, bu DNS ayarlarının yapılandırıldığını anlamına gelir.<br> <li>Bulut hizmeti toowhich tooyou çalıştığınız toorestore ReservedIP ile yapılandırıldığından ve bulut hizmetindeki VM'ler durdurulmuş durumda.<br>Bir bulut hizmeti powershell cmdlet'lerini kullanarak IP ayrılmış denetleyebilirsiniz:<br>$deployment get-AzureDeployment - ServiceName "servicename" =-yuvası "Üretim" $DEP Reservedıpname <br><li>Toorestore toosame bulut hizmeti aşağıdaki özel ağ yapılandırmaları ile bir sanal makine çalışıyorsunuz. <br>-Sanal makineler yük dengeleyici yapılandırması (dahili ve harici)<br>-Sanal makinelerle birden çok ayrılmış IP<br>-Birden çok NIC içeren sanal makinelere<br>Lütfen yeni bir bulut hizmeti hello UI seçin ya da çok başvurun[konuları geri](backup-azure-arm-restore-vms.md#restoring-vms-with-special-network-configurations) özel ağ yapılandırmaları olan VM'ler için.</ol> |
| Seçili hello DNS adı zaten alınmış - Lütfen farklı bir DNS adı belirtin ve yeniden deneyin. |Merhaba DNS adını buraya başvurduğu toohello bulut hizmeti adı (genellikle ile biten. cloudapp.net). Bu toobe benzersiz gerekir. Bu hatayla karşılaşırsanız, geri yükleme sırasında toochoose farklı bir VM adı gerekir. <br><br> Bu hata yalnızca toousers hello Azure portal, gösterilir. yalnızca hello diskleri geri yükler ve hello VM oluşturmaz çünkü hello PowerShell aracılığıyla geri yükleme işlemi başarılı olur. Merhaba VM açıkça sizin tarafınızdan hello disk geri yükleme işleminden sonra oluşturulduğunda hello hata karşılaştığı. |
| Merhaba belirtilen sanal ağ yapılandırması doğru değil - Lütfen farklı bir sanal ağ yapılandırması belirtin ve yeniden deneyin. |None |
| Merhaba, bulut hizmeti değil hello geri yüklenen hello sanal makine yapılandırmasıyla eşleşen - Lütfen ayrılmış IP kullanarak değil, farklı bir bulut hizmeti belirtin veya başka bir kurtarma noktası toorestore gelen seçin bir ayrılmış IP kullanılarak belirtilir. |None |
| Bulut hizmeti, giriş uç noktaları - sayısı yeniden deneme hello işlemi farklı bir bulut hizmeti belirterek veya mevcut bir uç noktası kullanarak sınırına ulaştı. |None |
| Yedekleme kasası ve hedef depolama hesabı iki farklı bölgelerde - geri yükleme işleminde belirtilen hello depolama hesabı hello olduğundan emin olun hello yedekleme kasasıyla aynı Azure bölgesi. |None |
| Depolama hesabı için Hello geri yükleme işlemi belirtilen desteklenen - yalnızca temel/standart depolama hesapları ile yerel olarak yedekli veya coğrafi olarak yedekli çoğaltma ayarları desteklenir. Lütfen desteklenen depolama hesabı seçin |None |
| Geri yükleme işlemi için belirtilen depolama hesabı türü çevrimiçi değil - geri yükleme işleminde belirtilen hello depolama hesabına çevrimiçi olduğundan emin olun |Azure Storage veya tooan kesilmesi nedeniyle geçici bir hata nedeniyle gerçekleşebilir. Lütfen başka bir depolama hesabı seçin. |
| Kaynak grubu kotasına ulaşıldı - Lütfen Azure Portalı'ndan bazı kaynak gruplarını silin veya Azure destek tooincrease hello sınırları başvurun. |None |
| Seçilen alt ağ yok - Lütfen var olan bir alt ağ seçin |None |
| Yedekleme hizmeti yetkilendirme tooaccess kaynakları aboneliğinizde sahip değil. |tooresolve Bu, ilk geri yükleme bölümünde belirtilen adımları kullanarak diskleri **yedeklenmiş diskleri geri yükleme** içinde [VM seçerek geri yükleme yapılandırmasını](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Bundan sonra belirtilen PowerShell adımları kullanın [geri yüklenen disklerden bir VM oluşturmak](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate geri yüklenen disklerden VM tam. |

## <a name="backup-or-restore-taking-time"></a>Yedekleme veya geri yükleme sürüyor
Görürseniz, backup(>12 hours) veya geri alma time(>6 hours):
* Anlamak [toobackup zaman katkıda bulunan Etkenler](backup-azure-vms-introduction.md#total-vm-backup-time) ve [toorestore zaman katkıda bulunan Etkenler](backup-azure-vms-introduction.md#total-restore-time).
* Takip ettiğinizden emin olun [yedekleme en iyi yöntemler](backup-azure-vms-introduction.md#best-practices). 

## <a name="vm-agent"></a>VM Aracısı
### <a name="setting-up-hello-vm-agent"></a>Merhaba VM Aracısı ayarlama
Genellikle, hello VM Aracısı zaten hello Azure galerisinde ' oluşturulan VM'ler bulunur. Ancak, şirket içi veri merkezlerinden Geçişi sanal makineleri hello VM aracısının yüklü sahip olmaz. Bu tür VM'ler için açıkça yüklü toobe hello VM Aracısı gerekiyor.

Windows VM'ler için:

* Merhaba yükleyip [aracı MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir.
* Klasik sanal makineler için [güncelleştirme hello VM özelliği](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) Aracısı hello tooindicate yüklenir. Bu adım, Resource Manager sanal makineler için gerekli değildir.

Linux VM'ler için:

* Son dağıtım depodan yükleyin. Biz **tavsiye** yalnızca dağıtım deposu üzerinden yükleme Aracısı. Paket adı hakkında daha fazla bilgi için lütfen çok başvurun[Linux Aracısı deposu](https://github.com/Azure/WALinuxAgent) 
* Klasik VM'ler için [güncelleştirme hello VM özelliği](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) Aracısı hello tooindicate yüklenir. Bu adım, Resource Manager sanal makineler için gerekli değildir.

### <a name="updating-hello-vm-agent"></a>Merhaba VM Aracısı güncelleştiriliyor
Windows VM'ler için:

* Güncelleştirme hello VM aracısı yeniden yüklemeyi hello kadar basit [VM Aracısı ikili dosyalarının](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Ancak, herhangi bir yedekleme işleminin VM Aracısı güncelleştirilmiş hello sırasında çalışan tooensure gerekir.

Linux VM'ler için:

* Merhaba yönergelerini izleyin [güncelleştirme Linux VM Aracısı](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Biz **tavsiye** yalnızca dağıtım deposu aracılığıyla güncelleştirme Aracısı. Doğrudan github'dan hello aracısı kodu indiriliyor ve güncelleştirmeden önermiyoruz. En son aracı, dağıtım için kullanılabilir durumda değilse, lütfen yönergeler toodistribution desteği çıkışı ulaşmak tooinstall en son aracı. Son kontrol edebilirsiniz [Windows Azure Linux Aracısı](https://github.com/Azure/WALinuxAgent/releases) github deposunu bilgileri.

### <a name="validating-vm-agent-installation"></a>VM Aracısı yüklemesini doğrulama
Nasıl toocheck için Windows vm'lerde VM Aracısı sürümü hello:

1. Azure sanal makinesi toohello üzerinde oturum ve toohello klasörüne gidin *C:\WindowsAzure\Packages*. Mevcut hello WaAppAgent.exe dosyasını bulmanız gerekir.
2. Merhaba dosyaya sağ tıklayın, çok Git**özellikleri**seçip hello **ayrıntıları** sekmesini hello ürün sürümü alanı 2.6.1198.718 olmalıdır ya da daha yüksek

## <a name="troubleshoot-vm-snapshot-issues"></a>VM anlık görüntü sorunlarını giderme
VM yedekleme anlık görüntü komutları toounderlying depolama veren kullanır. Erişim toostorage veya gecikmeleri bir anlık görüntü görev yürütme olmamasından hello yedekleme işi toofail neden olabilir. Merhaba aşağıdaki anlık görüntü görev başarısız olmasına neden olabilir.

1. Ağ erişim tooStorage NSG kullanarak engellendi<br>
    Çok konusunda daha fazla bilgi edinin[ağ erişimini etkinleştir](backup-azure-vms-prepare.md#network-connectivity) ya da uygulamaları güvenilir listeye almayı IP'leri veya proxy sunucu üzerinden kullanarak tooStorage.
2. Yapılandırılan Sql Server Yedekleme ile VM anlık görüntü görev gecikmeye neden olabilir <br>
   Varsayılan VM yedekleme sorunları VSS tam yedekleme ile Windows sanal makineleri üzerinde. Sql sunucuları ve Sql Server Yedekleme yapılandırılıp yapılandırılmadığını çalıştırmakta olan VM'ler üzerinde bu anlık görüntü yürütme gecikmesi neden olabilir. Lütfen yedekleme hataları nedeniyle anlık görüntü sorunları yaşıyorsanız, aşağıdaki kayıt defteri anahtarını ayarlayın.

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
   "USEVSSCOPYBACKUP"="TRUE"
   ```
3. RDP VM'yi kapatın olduğundan VM durumu yanlış bildirdi.  <br>
   RDP hello sanal makinede aşağı kapattığınızdan Lütfen hello Portalı'nda VM durumu düzgün yansıtılmasını kontrol edin. Aksi halde, lütfen hello VM VM panosunda 'Kapatma' seçeneğini kullanarak portalında kapatın.
4. Dörtten fazla VMs paylaşımı aynı Merhaba, bulut hizmeti, bu nedenle hiçbir dörtten fazla VM yedekleme sırasında hello başlatılan yedekleme zamanları birden çok yedekleme ilkeleri toostage hello yapılandırın aynı anda. Toospread hello yedekleme başlangıç arasında ilkeler birbirinden saatte bir kez deneyin.
5. VM yüksek CPU/bellek çalışıyor.<br>
   Yüksek CPU Hello sanal makine çalışıyorsa usage(>90%) veya bellek, anlık görüntü görev sıraya, Gecikmeli ve sonunda zaman aşımına uğradı alır. Böyle durumlarda talep üzerine yedekleme deneyin.

<br>

## <a name="networking"></a>Ağ
Tüm uzantıları gibi yedekleme uzantısını toohello ortak Internet toowork erişim. Erişim toohello olmamasından genel internet kendisini çeşitli şekillerde bildirilebilir:

* Merhaba uzantı yükleme başarısız olabilir
* (disk snapshot gibi) Hello yedekleme işlemleri başarısız olabilir
* Merhaba yedekleme işlemi Hello durumunu görüntüleme başarısız olabilir

Ortak internet adresleri çözülüyor hello gereksinimini geliştirilmiştir [burada](http://blogs.msdn.com/b/mast/archive/2014/06/18/azure-vm-provisioning-stuck-on-quot-installing-extensions-on-virtual-machine-quot.aspx). Azure URI'ler çözülebilir bu hello emin olun ve Merhaba VNET toocheck hello DNS yapılandırmaları gerekir.

Merhaba ad çözümlemesi doğru yaptıktan sonra erişim toohello Azure IP'leri sağlanan toobe da gerekir. toounblock erişim toohello Azure altyapı, aşağıdaki adımlardan birini izleyin:

1. Beyaz liste hello Azure veri merkezi IP aralıkları.
   * Merhaba listesini almak [Azure veri merkezi IP](https://www.microsoft.com/download/details.aspx?id=41653) toobe Güvenilenler listesine.
   * Engellemesini hello kullanarak IP hello [yeni NetRoute](https://technet.microsoft.com/library/hh826148.aspx) cmdlet'i. (Yönetici olarak çalıştır) yükseltilmiş bir PowerShell penceresinde hello Azure VM içinde bu cmdlet'i çalıştırın.
   * NSG kuralları toohello (bir yerinde yoksa) eklemek tooallow erişim toohello IP'leri.
2. HTTP trafiği tooflow için bir yol oluşturma
   * Varsa bazı ağ kısıtlaması yerde (bir ağ güvenlik grubu, örneğin) bir HTTP proxy sunucusu tooroute hello trafiği dağıtın. Bir HTTP Proxy sunucusu bulunan adımları toodeploy [burada](backup-azure-vms-prepare.md#network-connectivity).
   * NSG kuralları toohello (bir yerinde yoksa) eklemek hello HTTP Proxy gelen tooallow erişim toohello Internet.

> [!NOTE]
> DHCP Iaas VM yedekleme toowork hello Konuk içinde etkinleştirilmesi gerekir.  Statik bir özel IP gerekiyorsa, hello platformu ile yapılandırmanız gerekir. Merhaba VM bırakılmalıdır hello etkin içinde DHCP seçeneği.
> Hakkında daha fazla bilgi görüntülemek [statik iç özel IP ayarı](../virtual-network/virtual-networks-reserved-private-ip.md).
>
>

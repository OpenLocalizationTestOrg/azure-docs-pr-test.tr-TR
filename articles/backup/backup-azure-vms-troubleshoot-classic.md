---
title: "aaaTroubleshoot Azure Klasik Portalı'nda hataları yedekleme | Microsoft Docs"
description: "Azure yedekleme ve geri yükleme hello Klasik portalındaki Azure sanal makinelerin sorunlarını giderin."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 117201fb-c0cd-4be4-b47f-abd88fe914cf
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: trinadhk;markgal;
ms.openlocfilehash: b9907f6fa57c631f5446c4d00f946a57c4efd72b
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

## <a name="discovery"></a>Bulma
| Yedekleme işlemi | Hata ayrıntıları | Geçici çözüm |
| --- | --- | --- |
| Bulma |Toodiscover yeni öğe - Microsoft Azure yedekleme ile karşılaştı ve iç hatayla başarısız oldu. Birkaç dakika bekleyin ve ardından hello işlemi yeniden deneyin. |Merhaba bulma işlemi, 15 dakika sonra yeniden deneyin. |
| Bulma |Toodiscover yeni öğeler – başka bir işlemi zaten devam ediyor bulma başarısız oldu. Merhaba geçerli bulma işlemi tamamlanana kadar bekleyin. |None |

## <a name="register"></a>Kaydolma
| Yedekleme işlemi | Hata ayrıntıları | Geçici çözüm |
| --- | --- | --- |
| Kaydolma |Veri diski sayısı toohello sanal makine aşıldı hello desteklenen sınırı bağlı - Lütfen bu sanal makine ve Yeniden Dene'yi hello işlem bazı veri disklerde ayırın. Azure yedekleme destekler too16 veri diskleri yukarı tooan Azure sanal makine yedekleme için bağlı |None |
| Kaydolma |Microsoft Azure yedekleme bir iç hata - birkaç dakika bekleyin karşılaştı ve hello işlemi yeniden deneyin. Merhaba sorun devam ederse, Microsoft Support başvurun. |Premium LRS üzerinde VM aşağıdaki Merhaba, desteklenmeyen tooone yapılandırması nedeniyle bu hatayı alabilirsiniz. <br> Premium depolama Vm'leri kurtarma Hizmetleri kasası kullanılarak yedeklenebilir. [Daha Fazla Bilgi](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup) |
| Kaydolma |Kayıt Aracısı yükleme işlemi zaman aşımı ile başarısız oldu |Merhaba işletim sistemi sürümü hello sanal makinenin desteklenip desteklenmediğini denetleyin. |
| Kaydolma |Komut yürütme başarısız oldu - başka bir işlem bu öğeyi devam ediyor. Merhaba önceki işlem tamamlanana kadar bekleyin |None |
| Kaydolma |Premium depolama alanında depolanan sanal sabit diskler sahip sanal makineler için yedekleme desteklenmez. |None |
| Kaydolma |Sanal makine aracısını hello sanal makinede mevcut değil - Lütfen hello gerekli önkoşul, VM agent'ı yükleyin ve hello işlemi yeniden deneyin. |[Daha fazla bilgi](#vm-agent) VM Aracısı yükleme ve nasıl toovalidate hello VM Aracısı yükleme hakkında. |

## <a name="backup"></a>Backup
| Yedekleme işlemi | Hata ayrıntıları | Geçici çözüm |
| --- | --- | --- |
| Backup |Anlık görüntü durum için hello VM Aracısı ile iletişim kuramadı. Anlık görüntü VM alt görevi zaman aşımına uğradı. -Lütfen hello sorunlarını giderme konusunda Yardım bakın tooresolve bu. |Bu hata, hello VM Aracısı ile ilgili bir sorun veya ağ erişim toohello Azure altyapı herhangi bir yolla engellendi atılır. Daha fazla bilgi edinmek [anlık görüntü sorunlarını VM'yi hata ayıklama](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md). <br> Merhaba VM Aracısı sorunları neden, hello VM yeniden başlatın. Bazen, yanlış bir VM durum sorunlara neden olabilir ve bu "bozuk durum" Merhaba VM yeniden başlatma sıfırlar |
| Backup |Yedekleme bir iç hatayla başarısız oldu - Lütfen hello işlemi birkaç dakika içinde yeniden deneyin. Merhaba sorun devam ederse, Microsoft Support başvurun |Lütfen olup geçici bir sorun VM depolama erişirken denetleyin. Lütfen denetleyin [Azure durum](https://azure.microsoft.com/en-us/status/) tüm ilgili toocompute/depolama/ağ hello bölgede sorunu devam eden ise toosee. Lütfen yeniden deneme hello yedekleme sonrası sorunu azalır. |
| Backup |VM artık gibi hello işlem gerçekleştirilemedi. |Merhaba yedekleme için yapılandırılmış VM silindiğinden, yedekleme gerçekleştirilemiyor. Lütfen tooProtected öğeleri gruplama giderek daha fazla yedekleme durdurmak, korumalı öğe seçin ve korumayı Durdur'ı tıklatın. Yedekleme korumak veri seçeneğini belirleyerek verileri koruyabilirsiniz. Tıklayarak bu sanal makine üzerinde yapılandırmak için kayıtlı öğeler görünümü korumadan koruma daha sonra devam edebilirsiniz |
| Backup |Azure kurtarma Hizmetleri uzantısı için önkoşul başarısız tooinstall hello Azure kurtarma Hizmetleri Uzantısı hello seçili öğe - VM Aracısı ' dir. Lütfen hello Azure VM aracısı yükleyin ve hello kayıt işlemi yeniden başlatın |<ol> <li>Merhaba VM Aracısı doğru şekilde yüklenip yüklenmediğini denetleyin. <li>Bu hello olun hello VM config bayrağı doğru şekilde ayarlayın.</ol> [Daha fazla bilgi](#validating-vm-agent-installation) VM Aracısı yükleme ve nasıl toovalidate hello VM Aracısı yükleme hakkında. |
| Backup |Komut yürütme başarısız oldu - başka bir işlem şu anda bu öğeyi devam ediyor. Merhaba önceki işlem tamamlanana kadar bekleyin ve sonra yeniden deneyin |Merhaba VM için mevcut bir yedekleme veya geri yükleme işi çalıştığından ve hello mevcut iş çalışırken yeni bir işi başlatılamıyor. |
| Backup |Uzantı yüklemesi "COM + oluşturulamıyor tootalk toohello Microsoft Distributed Transaction Coordinator edildi hello hatasıyla başarısız oldu |Bu, genellikle hello COM + hizmeti çalışmadığı anlamına gelir. Bu sorunu düzeltme konusunda yardım için Microsoft Destek'e başvurun. |
| Backup |VSS işlemi hatası ile Merhaba "Bu sürücünün BitLocker Sürücü Şifrelemesi tarafından kilitlenmiş. anlık görüntü işlemi başarısız Denetim Masası'ndan bu sürücünün kilidini açmanız gerekir. |Hello VM üzerindeki tüm sürücüleri için BitLocker'ı açın ve hello VSS sorunun giderilip giderilmediğini inceleyin |
| Backup |Premium depolama alanında depolanan sanal sabit diskler sahip sanal makineler için yedekleme desteklenmez. |None |
| Backup |Azure sanal makine bulunamadı. |Bu, hello birincil VM silindiği, ancak bir VM tooperform yedekleme toolook hello yedekleme İlkesi devam durumlarda gerçekleşir. toofix bu hata: <ol><li>Merhaba ile Merhaba sanal makine yeniden aynı ada ve aynı kaynak grubu adı [bulut hizmet adı] <br>(VEYA) <li> Sonraki yedeklemeleri değil tetiklenen için bu sanal makine için koruma devre dışı bırakın. </ol> |
| Backup |Sanal makine aracısını hello sanal makinede mevcut değil - Lütfen hello gerekli önkoşul, VM agent'ı yükleyin ve hello işlemi yeniden deneyin. |[Daha fazla bilgi](#vm-agent) VM Aracısı yükleme ve nasıl toovalidate hello VM Aracısı yükleme hakkında. |

## <a name="jobs"></a>İşler
| İşlem | Hata ayrıntıları | Geçici çözüm |
| --- | --- | --- |
| İşi iptal et |İptal bu iş türü için desteklenmeyen - hello iş tamamlanana kadar bekleyin. |None |
| İşi iptal et |Merhaba işi iptal edilebilen bir durumda değil - hello iş tamamlanana kadar bekleyin. <br>OR<br> Merhaba seçili işi iptal edilebilen bir durumda değil - hello iş toocomplete için bekleyin. |Tüm olasılığını içinde hello iş neredeyse tamamlandı; Merhaba iş tamamlanana kadar bekleyin |
| İşi iptal et |Merhaba işi devam eden değil - iptal yalnızca sürmekte olan işleri için desteklenen olduğundan iptal edemezsiniz. Lütfen girişimi iptal bir sürüyor işi. |Tooa geçici durumu meydana gelir. Bir dakika bekleyin ve hello İptal işlemi yeniden deneyin |
| İşi iptal et |Başarısız toocancel hello iş - işi tamamlanana kadar bekleyin. |None |

## <a name="restore"></a>Geri Yükleme
| İşlem | Hata ayrıntıları | Geçici çözüm |
| --- | --- | --- |
| Geri Yükleme |Geri yükleme bulut iç hata vererek başarısız oldu |<ol><li>Bulut hizmeti toowhich toorestore çalıştığınız DNS ayarlarla yapılandırılır. Kontrol edebilirsiniz <br>$deployment get-AzureDeployment - ServiceName "ServiceName" =-yuvası "Üretim" Get-AzureDns - DnsSettings $deployment. DnsSettings<br>Yapılandırılmış adresi varsa, bu DNS ayarlarının yapılandırıldığını anlamına gelir.<br> <li>Bulut hizmeti toowhich tooyou çalıştığınız toorestore ReservedIP ile yapılandırıldığından ve bulut hizmetindeki VM'ler durdurulmuş durumda.<br>Bir bulut hizmeti powershell cmdlet'lerini kullanarak IP ayrılmış denetleyebilirsiniz:<br>$deployment get-AzureDeployment - ServiceName "servicename" =-yuvası "Üretim" $DEP Reservedıpname <br><li>Toorestore toosame bulut hizmeti aşağıdaki özel ağ yapılandırmaları ile bir sanal makine çalışıyorsunuz. <br>-Sanal makineler yük dengeleyici yapılandırması (dahili ve harici)<br>-Sanal makinelerle birden çok ayrılmış IP<br>-Birden çok NIC içeren sanal makinelere<br>Lütfen yeni bir bulut hizmeti hello UI seçin ya da çok başvurun[konuları geri](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations) özel ağ yapılandırmaları olan VM'ler için</ol> |
| Geri Yükleme |Seçili hello DNS adı zaten alınmış - Lütfen farklı bir DNS adı belirtin ve yeniden deneyin. |Merhaba DNS adını buraya başvurduğu toohello bulut hizmeti adı (genellikle ile biten. cloudapp.net). Bu toobe benzersiz gerekir. Bu hatayla karşılaşırsanız, geri yükleme sırasında toochoose farklı bir VM adı gerekir. <br><br> Bu hata yalnızca toousers hello Azure portal, gösterilir. yalnızca hello diskleri geri yükler ve hello VM oluşturmaz çünkü hello PowerShell aracılığıyla geri yükleme işlemi başarılı olur. Merhaba VM açıkça sizin tarafınızdan hello disk geri yükleme işleminden sonra oluşturulduğunda hello hata karşılaştığı. |
| Geri Yükleme |Merhaba belirtilen sanal ağ yapılandırması doğru değil - Lütfen farklı bir sanal ağ yapılandırması belirtin ve yeniden deneyin. |None |
| Geri Yükleme |Merhaba, bulut hizmeti değil hello geri yüklenen hello sanal makine yapılandırmasıyla eşleşen - Lütfen farklı bir bulut hizmeti, bir ayrılmış IP kullanmayan belirtin veya başka bir kurtarma noktası toorestore gelen seçin bir ayrılmış IP kullanılarak belirtilir. |None |
| Geri Yükleme |Bulut hizmeti, giriş uç noktaları - sayısı yeniden deneme hello işlemi farklı bir bulut hizmeti belirterek veya mevcut bir uç noktası kullanarak sınırına ulaştı. |None |
| Geri Yükleme |Yedekleme kasası ve hedef depolama hesabı iki farklı bölgelerde - geri yükleme işleminde belirtilen hello depolama hesabı hello olduğundan emin olun hello yedekleme kasasıyla aynı Azure bölgesi. |None |
| Geri Yükleme |Depolama hesabı için Hello geri yükleme işlemi belirtilen desteklenen - yalnızca temel/standart depolama hesapları ile yerel olarak yedekli veya coğrafi olarak yedekli çoğaltma ayarları desteklenir. Lütfen desteklenen depolama hesabı seçin |None |
| Geri Yükleme |Geri yükleme işlemi için belirtilen depolama hesabı türü çevrimiçi değil - geri yükleme işleminde belirtilen hello depolama hesabına çevrimiçi olduğundan emin olun |Azure Storage veya tooan kesilmesi nedeniyle geçici bir hata nedeniyle gerçekleşebilir. Lütfen başka bir depolama hesabı seçin. |
| Geri Yükleme |Kaynak grubu kotasına ulaşıldı - Lütfen Azure Portalı'ndan bazı kaynak gruplarını silin veya Azure destek tooincrease hello sınırları başvurun. |None |
| Geri Yükleme |Seçilen alt ağ yok - Lütfen var olan bir alt ağ seçin |None |

## <a name="policy"></a>İlke
| İşlem | Hata ayrıntıları | Geçici çözüm |
| --- | --- | --- |
| İlke Oluştur |Toocreate hello İlkesi - başarısız oldu Lütfen hello bekletme seçenekleri toocontinue ilkesi yapılandırması ile azaltın. |None |

## <a name="vm-agent"></a>VM Aracısı
### <a name="setting-up-hello-vm-agent"></a>Merhaba VM Aracısı ayarlama
Genellikle, hello VM Aracısı zaten hello Azure galerisinde ' oluşturulan VM'ler bulunur. Ancak, şirket içi veri merkezlerinden Geçişi sanal makineleri hello VM aracısının yüklü sahip olmaz. Bu tür VM'ler için açıkça yüklü toobe hello VM Aracısı gerekiyor. Daha fazla bilgi edinin [yükleme hello VM Aracısı'nı mevcut bir VM'yi](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

Windows VM'ler için:

* Merhaba yükleyip [aracı MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir.
* [Merhaba VM özelliğini güncelleştirin](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) Aracısı hello tooindicate yüklenir.

Linux VM'ler için:

* Son yükleme [Linux Aracısı](https://github.com/Azure/WALinuxAgent) github'dan.
* [Merhaba VM özelliğini güncelleştirin](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) Aracısı hello tooindicate yüklenir.

### <a name="updating-hello-vm-agent"></a>Merhaba VM Aracısı güncelleştiriliyor
Windows VM'ler için:

* Güncelleştirme hello VM aracısı yeniden yüklemeyi hello kadar basit [VM Aracısı ikili dosyalarının](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Ancak, herhangi bir yedekleme işleminin VM Aracısı güncelleştirilmiş hello sırasında çalışan tooensure gerekir.

Linux VM'ler için:

* Merhaba yönergelerini izleyin [güncelleştirme Linux VM Aracısı](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="validating-vm-agent-installation"></a>VM Aracısı yüklemesini doğrulama
Nasıl toocheck için Windows vm'lerde VM Aracısı sürümü hello:

1. Azure sanal makinesi toohello üzerinde oturum ve toohello klasörüne gidin *C:\WindowsAzure\Packages*. Mevcut hello WaAppAgent.exe dosyasını bulmanız gerekir.
2. Merhaba dosyaya sağ tıklayın, çok Git**özellikleri**seçip hello **ayrıntıları** sekmesini hello ürün sürümü alanı 2.6.1198.718 olmalıdır ya da daha yüksek

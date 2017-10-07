---
title: "iş yükleri tooAzure Klasik portal yukarı aaaUse Azure yedekleme sunucusu tooback | Microsoft Docs"
description: "Ortamınıza iş yüklerini Azure yedekleme sunucusu kullanarak tooback doğru şekilde hazırlandığından emin olun"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: "Azure backup sunucusu; Yedekleme kasası"
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: 7b574824c448096e0c0ba74a872ab8f2a434f6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Azure yedekleme sunucusu kullanarak iş yüklerini tooback hazırlama
> [!div class="op_single_selector"]
> * [Azure Backup Sunucusu](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup sunucusu (Klasik)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (Klasik)](backup-azure-dpm-introduction-classic.md)
>
>

Bu makalede, Azure yedekleme sunucusu kullanarak iş yüklerini, ortam tooback hazırlama hakkında ' dir. Azure yedekleme Sunucusu'nu kullanarak, Hyper-V sanal makineleri, Microsoft SQL Server, SharePoint Server, Microsoft Exchange ve Windows istemcileri gibi uygulama iş yükleri tek bir konsoldan koruyabilirsiniz.

> [!WARNING]
> Azure Backup sunucusu hello işlevselliği Data Protection Manager (DPM) iş yükü yedeklemesi için devralır. Bu özelliklerden bazıları tooDPM belgelerine işaretçileri bulacaksınız. Ancak Azure yedekleme sunucusu bant üzerindeki koruma sağlamaz veya System Center ile tümleştirme.
>
>

## <a name="1-windows-server-machine"></a>1. Windows Server makine
![step1](./media/backup-azure-microsoft-azure-backup/step1.png)

hello Azure yedekleme sunucusu Başlarken hazırlarken ve çalışırken doğrultusunda hello ilk toohave bir Windows Server makine adımdır.

| Konum | En düşük gereksinimler | Ek yönergeler |
| --- | --- | --- |
| Azure |Azure Iaas sanal makinesi<br><br>A2 Standart: 2 Çekirdek, 3.5GB RAM |Windows Server 2012 R2 Datacenter basit galeri görüntüsü ile başlayabilirsiniz. [Azure yedekleme Server'ı (DPM) kullanılarak Iaas iş yüklerini koruyorsanız](https://technet.microsoft.com/library/jj852163.aspx) pek çok küçük farklar vardır. Hello makale tamamen hello makineyi dağıtmadan önce okuduğunuzdan emin olun. |
| Şirket içi |Hyper-V VM<br> VMWare VM<br> ya da fiziksel bir ana bilgisayar<br><br>2 Çekirdek ve 4GB RAM |Windows Server yinelenen kaldırma kullanarak hello DPM depolama alanında yinelenenleri kaldırma. Hakkında daha fazla bilgi [DPM ve yinelenenleri kaldırma](https://technet.microsoft.com/library/dn891438.aspx) Hyper-V VM dağıtıldığında birlikte çalışır. |

> [!NOTE]
> Azure yedekleme sunucusu Windows Server 2012 R2 Datacenter olan bir makinede yüklü önerilir. Çok sayıda hello Önkoşullar otomatik olarak hello son hello Windows işletim sistemi sürümüyle ele alınmıştır.
>
>

Toojoin Azure yedekleme sunucusu tooa etki alanı planlıyorsanız, hello Azure yedekleme sunucusu yazılım yüklemeden önce hello fiziksel sunucu veya sanal makine toohello etki alanına katılma önerilir. Dağıtımdan sonra bir Azure yedekleme sunucusu tooa yeni etki alanına taşıma *desteklenmiyor*.

## <a name="2-backup-vault"></a>2. Yedekleme kasası
![step2](./media/backup-azure-microsoft-azure-backup/step2.png)

Yedekleme verilerini tooAzure göndermek ya da yerel olarak tutmak isteyip hello Azure yedekleme sunucusu kayıtlı tooa kasası olması gerekir. Yeni bir Azure yedekleme kullanıcısıysanız ve toouse Azure yedekleme sunucusu istiyorsanız, hello Azure bkz bu makalenin - portal sürümü [tooback Azure yedekleme sunucusu kullanarak iş yüklerini hazırlama](backup-azure-microsoft-azure-backup.md).

> [!IMPORTANT]
> Mart 2017'dan başlayarak, hello Klasik portal toocreate yedekleme kasaları artık kullanabilirsiniz.
> Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> 15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız. **1 Kasım 2017’ye kadar**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
>



## <a name="3-software-package"></a>3. Yazılım paketi
![Adım 3](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-hello-software-package"></a>Merhaba yazılım paketini indirme
Benzer toovault kimlik bilgileri, indirebilirsiniz Microsoft Azure yedekleme hello uygulama iş yüklerini için **hızlı başlangıç sayfasında** hello yedekleme kasasının.

1. Tıklatın **için uygulama iş yüklerini (Disk tooDisk tooCloud)**. Bu toohello İndirme Merkezi sayfasından, hello yazılım paketi indirdiğiniz sürecek.

    ![Microsoft Azure yedekleme Hoş Geldiniz ekranı](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. **İndir**’e tıklayın.

    ![İndirme Merkezinden 1](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. Tüm hello dosyaları seçin ve tıklatın **sonraki**. Tüm dosyaları hello Microsoft Azure yedekleme indirme sayfasından gelen hello indirme ve tüm dosyalarda hello Yerleştir aynı klasöre hello.
   ![İndirme Merkezinden 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    Too60 sürebilir 10 MB/sn indirme bağlantıyı Hello indirme boyutu tüm hello dosyaların birlikte > 3 G olduğundan, toocomplete hello dakika indirin.

### <a name="extracting-hello-software-package"></a>Merhaba yazılım paketi ayıklanıyor
Tüm hello dosyaları indirdikten sonra tıklayın **MicrosoftAzureBackupInstaller.exe**. Bu hello başlatır **Microsoft Azure yedekleme Kurulum Sihirbazı'nı** tooextract hello Kurulum dosyaları belirttiğiniz tarafından tooa konumu. Merhaba sihirbaza devam edin ve üzerinde hello tıklatın **ayıklamak** düğmesini toobegin hello ayıklama işlemi.

> [!WARNING]
> En az 4GB boş disk alanı gerekli tooextract hello Kurulum dosyaları'dır.
>
>

![Microsoft Azure yedekleme Kurulum Sihirbazı](./media/backup-azure-microsoft-azure-backup/extract/03.png)

Bir kez hello ayıklama işlemi tamamlandı, onay hello kutusunu toolaunch hello istemcinin ayıklanan *setup.exe* toobegin Microsoft Azure yedekleme sunucusu yükleme üzerinde hello tıklatıp **son** düğmesi.

### <a name="installing-hello-software-package"></a>Merhaba yazılım paketi yükleniyor
1. Tıklatın **Microsoft Azure yedekleme** toolaunch hello Kurulum Sihirbazı'nı.

    ![Microsoft Azure yedekleme Kurulum Sihirbazı](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. Merhaba Hoş Geldiniz ekranında hello tıklatın **sonraki** düğmesi. Bu toohello sürer *önkoşul denetler* bölümü. Bu ekranda hello üzerinde tıklatın **denetleyin** Azure yedekleme sunucusu hello donanım ve yazılım önkoşulları karşılanıyorsa toodetermine düğmesi. Tüm Önkoşullar olan hello başarıyla karşılanıyorsa, o hello makine hello gereksinimleri karşılayan belirten bir ileti görürsünüz. Tıklatın hello üzerinde **sonraki** düğmesi.

    ![Azure yedekleme sunucusu - Hoş Geldiniz ve önkoşulları denetleyin](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Microsoft Azure yedekleme sunucusu SQL Server Standard gerektirir ve gerekli hello uygun SQL Server ikili dosyalarıyla hello Azure yedekleme sunucusu yükleme paketi ile birlikte gelen sunar. Yeni bir Azure yedekleme sunucusu yüklemesine başlatırken hello seçeneği seçmeniz gerekir **yeni SQL Server örneği bu kurulum ile yükleme** hello tıklatıp **denetle ve Yükle** düğmesi. Merhaba Önkoşullar başarıyla yüklendikten sonra tıklayın **sonraki**.

    ![Azure yedekleme sunucusu - SQL denetimi](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    Bir öneri toorestart hello makineyle bir arıza durumunda bunu ve tıklayın **yeniden denetle**.

   > [!NOTE]
   > Azure yedekleme sunucusu uzak bir SQL Server örneği ile çalışmaz. Azure yedekleme sunucusu tarafından kullanılan hello örneği toobe yerel gerekir.
   >
   >

4. Microsoft Azure yedekleme sunucusu dosyaları hello yüklenmesi için bir konum belirtin ve tıklatın **sonraki**.

    ![Microsoft Azure yedekleme PreReq2](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    Merhaba karalama konumu tooAzure yedeklemek için gerekli değildir. En az %5 hello veri toohello bulut yedeklenen toobe planlanmış Hello karalama konumu olduğundan emin olun. Disk koruması için ayrı diskin hello yükleme işlemi tamamlandıktan sonra yapılandırılmış toobe gerekir. Depolama havuzları hakkında daha fazla bilgi için bkz: [depolama havuzlarını yapılandırın ve disk depolama](https://technet.microsoft.com/library/hh758075.aspx).
5. Kısıtlı yerel kullanıcı hesapları için güçlü bir parola sağlayın ve tıklatın **sonraki**.

    ![Microsoft Azure yedekleme PreReq2](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Toouse istediğinizi seçin *Microsoft Update* güncelleştirmeleri ve tıklatın toocheck **sonraki**.

   > [!NOTE]
   > Windows Update tooMicrosoft Windows ve Microsoft Azure yedekleme sunucusu gibi diğer ürünleri için güvenlik ve önemli güncelleştirmeler sunar güncelleştirme yönlendirmek olması önerilir.
   >
   >

    ![Microsoft Azure yedekleme PreReq2](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. Gözden geçirme hello *ayarların özeti* tıklatıp **yükleme**.

    ![Microsoft Azure yedekleme PreReq2](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. Merhaba yükleme aşamada gerçekleşir. Merhaba ilk aşaması hello Microsoft Azure kurtarma Hizmetleri Aracısı hello sunucusuna yüklenir. Başlangıç Sihirbazı'nı, ayrıca Internet bağlantısını denetler. Internet bağlantısı olup olmadığını yüklemeye devam edebilirsiniz, aksi durumda, tooprovide proxy ayrıntıları tooconnect toohello Internet gerekir.

    Merhaba sonraki tooconfigure hello Microsoft Azure kurtarma Hizmetleri Aracısı adımdır. Merhaba yapılandırmasının parçası olarak, hello kasa kimlik bilgileri tooregister hello makine toohello yedekleme kasası tooprovide sahip olur. Ayrıca, şirket içi ve Azure arasında gönderilen bir parola tooencrypt/şifre çözme hello verileri sağlar. Otomatik olarak bir parola oluşturmak veya kendi en az 16 karakter parola girin. Merhaba Aracısı yapılandırılana kadar hello sihirbazına devam edin.

    ![Azure yedekleme Serer PreReq2](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. Merhaba Microsoft Azure yedekleme sunucusu kayıt başarıyla tamamlandıktan sonra hello Genel Kurulum Sihirbazı'nı toohello yüklenmesi ve yapılandırılması SQL Server ve hello Azure yedekleme sunucusu bileşenleri ile devam eder. Merhaba SQL Server bileşen yüklemesi tamamlandıktan sonra hello Azure yedekleme sunucusu bileşenleri yüklenir.

    ![Azure Backup Sunucusu](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Merhaba yükleme adım tamamlandığında, hello ürünün masaüstü simgelerini de oluşturulmuş. Yalnızca hello simgesi toolaunch hello ürün çift tıklayın.

### <a name="add-backup-storage"></a>Yedekleme depolama ekleme
Merhaba ilk yedek kopyayı Azure yedekleme sunucusu makine bağlı depolama toohello üzerinde tutulur. Diskleri ekleme hakkında daha fazla bilgi için bkz: [depolama havuzlarını yapılandırın ve disk depolama](https://technet.microsoft.com/library/hh758075.aspx).

> [!NOTE]
> Toosend veri tooAzure bile planlıyorsanız tooadd yedekleme depolama gerekir. Merhaba geçerli mimarisinde Azure yedekleme sunucusu hello Azure yedekleme kasası hello tutan *ikinci* kopyasını hello verileri hello yerel depolama hello ilk (ve zorunlu) yedek kopyasını tutar.  
>
>

## <a name="4-network-connectivity"></a>4. Ağ bağlantısı
![step4](./media/backup-azure-microsoft-azure-backup/step4.png)

Azure yedekleme sunucusu hello ürün toowork için bağlantı toohello Azure Backup hizmeti başarıyla gerektirir. toovalidate hello makine hello bağlantı tooAzure olup olmadığını hello kullan ```Get-DPMCloudConnection``` komutunu hello Azure yedekleme sunucusu PowerShell konsolunda. Hello bağlantısı varsa hello komutunu çıktısını TRUE ise, başka bağlantısı yok.

Merhaba sağlıklı bir durumda toobe aynı zamanda, hello Azure aboneliği gerekir. Aboneliğiniz ve toomanage hello durumu çıkışı toofind, toohello günlüğünde [abonelik portal](https://account.windowsazure.com/Subscriptions).

Merhaba durumu hello Azure bağlantısı ve hello Azure aboneliği öğrendikten sonra sunulan hello yedekleme/geri yükleme işlevselliği üzerinde toofind hello etkisi çıkışı aşağıdaki hello tabloyu kullanabilirsiniz.

| Bağlantı durumu | Azure Aboneliği | Yedekleme tooAzure | Yedekleme toodisk | Azure'dan geri yükleme | Disk, geri yükleme |
| --- | --- | --- | --- | --- | --- |
| bağlı |Etkin |İzin verilen |İzin verilen |İzin verilen |İzin verilen |
| bağlı |Süresi dolmuş |Durduruldu |Durduruldu |İzin verilen |İzin verilen |
| bağlı |Sağlaması kaldırılıyor. sağlaması |Durduruldu |Durduruldu |Silinen durduruldu ve Azure kurtarma noktaları |Durduruldu |
| Kayıp bağlantısı > 15 gün |Etkin |Durduruldu |Durduruldu |İzin verilen |İzin verilen |
| Kayıp bağlantısı > 15 gün |Süresi dolmuş |Durduruldu |Durduruldu |İzin verilen |İzin verilen |
| Kayıp bağlantısı > 15 gün |Sağlaması kaldırılıyor. sağlaması |Durduruldu |Durduruldu |Silinen durduruldu ve Azure kurtarma noktaları |Durduruldu |

### <a name="recovering-from-loss-of-connectivity"></a>Bağlantı kaybına karşı kurtarma
Bir güvenlik duvarı ya da erişim tooAzure engelleyen bir proxy varsa, etki alanı adresleri hello güvenlik duvarı/proxy profilinde aşağıdaki toowhitelist hello gerekir:

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

Bağlantı tooAzure geri yüklenen toohello Azure yedekleme sunucusu makine silindikten sonra gerçekleştirilebilir hello işlemleri hello Azure abonelik durumu tarafından belirlenir. Yukarıdaki tabloda Hello hello makineye bağlı"sonra" izin verilen hello işlemleri hakkında ayrıntılar bulunur.

### <a name="handling-subscription-states"></a>Abonelik durumları işleme
Azure aboneliğinden olası tootake olan bir *süresi doldu* veya *Deprovisioned* durumu toohello *etkin* durumu. Merhaba durumu olmamasına karşın ancak bu bazı hello ürün davranışı şifrelemelerini *etkin*:

* A *Deprovisioned* abonelik bu sağlaması kaldırılıyor. sağlaması hello dönem için işlevselliğini kaybeder. Dönüş üzerinde *etkin*, yedekleme/geri yükleme hello ürün işlevselliğini geri. yeterli büyüklükte bekletme süresi ile bıraktıysanız hello hello yerel disk üzerindeki yedekleme verileri de alınabilir. Merhaba abonelik hello girdikten sonra ancak yedekleme verilerini azure'da hello irretrievably kaybolur *Deprovisioned* durumu.
* Bir *süresi doldu* abonelik hale getirdiği kadar işlevselliği için yalnızca kaybederse *etkin* yeniden. Abonelik hello hello dönem için zamanlanan yedeklemeleri edildi *süresi doldu* çalışmaz.

## <a name="troubleshooting"></a>Sorun giderme
Microsoft Azure yedekleme sunucusu hello Kurulum aşaması (veya yedekleme veya geri yükleme sırasında) hataları ile başarısız olursa, toothis başvuran [hata kodları belge](https://support.microsoft.com/kb/3041338) daha fazla bilgi için.
Ayrıca çok başvurabilir[Azure Backup ile ilgili sık sorulan sorular](backup-azure-backup-faq.md)

## <a name="next-steps"></a>Sonraki adımlar
Ayrıntılı bilgi almak [DPM için ortamınızı hazırlama](https://technet.microsoft.com/library/hh758176.aspx) hello Microsoft TechNet sitesindeki. Ayrıca, üzerinde Azure yedekleme sunucusu dağıtılan ve kullanılabilecek desteklenen yapılandırmalar hakkında bilgi içerir.

Bu makaleler toogain Microsoft Azure yedekleme sunucusu kullanarak iş yükü koruması daha derin bir anlayış kullanabilirsiniz.

* [SQL Server Yedekleme](backup-azure-backup-sql.md)
* [SharePoint server yedekleme](backup-azure-backup-sharepoint.md)
* [Diğer sunucu yedekleme](backup-azure-alternate-dpm-server.md)

---
title: "iş yükleri tooAzure yukarı aaaUse Azure yedekleme sunucusu tooback | Microsoft Docs"
description: "Azure yedekleme sunucusu tooprotect kullanın veya iş yükleri toohello Azure portal yedekleyin."
services: backup
documentationcenter: 
author: PVRK
manager: shivamg
editor: 
keywords: "Azure backup sunucusu; iş yüklerini korumak; iş yüklerini yedeklemeye"
ms.assetid: e7fb1907-9dc1-4ca1-8c61-50423d86540c
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: a99b2919ffd44c6133960e3a935038a2bb1281c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Azure yedekleme sunucusu kullanarak iş yüklerini tooback hazırlama
> [!div class="op_single_selector"]
> * [Azure Backup Sunucusu](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
>
>

Bu makalede açıklanır nasıl tooprepare, ortam tooback iş yüklerini Azure yedekleme sunucusu kullanarak. Azure yedekleme Sunucusu'nu kullanarak, Hyper-V sanal makineleri, Microsoft SQL Server, SharePoint Server, Microsoft Exchange ve Windows istemcileri gibi uygulama iş yükleri tek bir konsoldan koruyabilirsiniz.

> [!NOTE]
> Azure yedekleme sunucusu artık VMware Vm'leri koruyabilir ve Gelişmiş güvenlik özellikleri sağlar. Merhaba ürün bölümlerde hello aşağıda açıklandığı gibi yükleyin; en son Azure Backup Aracısı hello ve güncelleştirme 1 uygulanır. Azure yedekleme sunucusu VMware sunucularıyla yedekleme hakkında daha fazla toolearn hello makaleye bakın [bir VMware sunucusu kullanım Azure yedekleme sunucusu tooback](backup-azure-backup-server-vmware.md). güvenlik özellikleri hakkında toolearn başvurmak çok[Azure yedekleme güvenlik özellikleri belgelerine](backup-azure-security-feature.md).
>
>

Azure'da VM gibi bir hizmet (Iaas) iş yükleri olarak altyapısı da koruyabilir.

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki dağıtım modeline sahiptir: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Resource Manager modelini kullanarak dağıtılan VM'ler geri yüklemek için hello bilgi ve yordamlar sağlar.
>
>

Azure Backup sunucusu hello iş yükü yedekleme işlevlerinin çoğunu Data Protection Manager (DPM) devralır. Bu makalede tooDPM belgelerine tooexplain bağlantılar hello bazıları paylaşılan işlevselliği. Azure yedekleme sunucusu hello çoğunu paylaşır ancak DPM ile aynı işlevselliği. Azure yedekleme sunucusu başlamıyor tootape geri ya da System Center ile tümleşik çalışıyor.

## <a name="1-choose-an-installation-platform"></a>1. Bir yükleme platformu seçin
hello Azure yedekleme sunucusu Başlarken hazırlarken ve çalışırken doğrultusunda hello ilk tooset bir Windows sunucusu adımdır. Sunucunuz, Azure veya şirket içi olabilir.

### <a name="using-a-server-in-azure"></a>Azure üzerinde bir sunucu kullanarak
Azure yedekleme sunucusu çalıştıran bir sunucu seçerken, bir Windows Server 2012 R2 Datacenter galeri görüntüsüyle Başlat önerilir. Merhaba makale [hello Azure portalında, ilk Windows sanal makine oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), hello ile çalışmaya başlama önerilen, azure'da sanal makine için hiç Azure önce kullanmış olduğunuz olsa bile bir öğretici sağlar. Merhaba önerilen en düşük gereksinimler hello sunucu sanal makine (VM) olmalıdır: A2 standart iki çekirdek ve 3.5 GB RAM ile.

Azure yedekleme sunucusu ile iş yüklerini koruma pek çok küçük farklar vardır. Merhaba makale [bir Azure sanal makinesi olarak DPM yükleme](https://technet.microsoft.com/library/jj852163.aspx), yardımcı olur, bu küçük farklar açıklanmaktadır. Merhaba makine dağıtmadan önce bu makalenin tümüyle okuyun.

### <a name="using-an-on-premises-server"></a>Bir şirket içi sunucu kullanma
Azure'da hello temel sunucu toorun istemiyorsanız, Hyper-V VM, bir VMware sanal veya fiziksel bir ana bilgisayar üzerinde hello sunucu çalıştırabilirsiniz. Merhaba hello sunucu donanımı için en düşük gereksinimler iki çekirdek ve 4 GB RAM önerilir. Merhaba desteklenen işletim sistemleri, aşağıdaki tablonun hello listelenmiştir:

| İşletim Sistemi | Platform | SKU |
|:--- | --- |:--- |
| Windows Server 2012 R2 ve en son SP'ler |64 bit |Standard, Datacenter, Foundation |
| Windows Server 2012 ve en son SP'ler |64 bit |Datacenter, Foundation, Standard |
| Windows Storage Server 2012 R2 ve en son SP'ler |64 bit |Standard, Workgroup |
| Windows Storage Server 2012 ve en son SP'ler |64 bit |Standard, Workgroup |

Windows Server yinelenen kaldırma kullanarak hello DPM depolama alanında yinelenenleri kaldırma. Hakkında daha fazla bilgi [DPM ve yinelenenleri kaldırma](https://technet.microsoft.com/library/dn891438.aspx) Hyper-V VM dağıtıldığında birlikte çalışır.

> [!NOTE]
> Azure yedekleme ayrılmış, tek amaçlı bir sunucuda tasarlanmış toorun sunucusudur. Azure yedekleme sunucusu üzerinde yüklenemiyor:
> - Bir etki alanı denetleyicisi olarak çalıştıran bir bilgisayar
> - Hangi hello uygulama sunucusu rolünün yüklü olduğu bir bilgisayar
> - System Center Operations Manager yönetim sunucusu olan bir bilgisayar
> - Exchange Server çalıştıran bir bilgisayar
> - Kümenin bir düğümü olan bir bilgisayar

Her zaman Azure yedekleme sunucusu tooa etki alanına katılın. Toomove hello server tooa farklı etki alanı düşünüyorsanız, Azure yedekleme sunucusu yüklemeden önce hello server toohello yeni etki alanına katılma önerilir. Var olan bir Azure yedekleme sunucusu taşıma makine tooa yeni etki alanı dağıtım tamamlandıktan sonra *desteklenmiyor*.

## <a name="2-recovery-services-vault"></a>2. Kurtarma Hizmetleri kasası
Yedekleme verilerini tooAzure göndermek ya da yerel olarak tutmak isteyip hello yazılım bağlı toobe tooAzure gerekir. daha belirgin toobe, bir kurtarma Hizmetleri kasasına kayıtlı toobe hello Azure yedekleme sunucusu makinenin gerekiyor.

Kasa toocreate bir kurtarma Hizmetleri:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba Hub menüsünde **Gözat** ve kaynakları hello listesinde yazın **kurtarma Hizmetleri**. Yazmaya başladığınızda liste filtreleri, girişinize göre hello. **Kurtarma Hizmetleri kasası** seçeneğine tıklayın.

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png) <br/>

    Merhaba kurtarma Hizmetleri kasalarının listesi görüntülenir.
3. Merhaba üzerinde **kurtarma Hizmetleri kasaları** menüsünde tıklatın **Ekle**.

    ![Kurtarma Hizmetleri Kasası oluşturma 2. adım](./media/backup-azure-microsoft-azure-backup/rs-vault-menu.png)

    Merhaba kurtarma Hizmetleri kasası dikey penceresi açılır tooprovide isteyen bir **adı**, **abonelik**, **kaynak grubu**, ve **konumu**.

    ![Kurtarma Hizmetleri kasası oluşturma 5. adım](./media/backup-azure-microsoft-azure-backup/rs-vault-attributes.png)
4. İçin **adı**, bir kolay ad tooidentify hello kasası girin. Merhaba adı toobe hello Azure aboneliği için benzersiz olmalıdır. 2 ila 50 karakterden oluşan bir ad yazın. Ad bir harf ile başlamalıdır ve yalnızca harf, rakam ve kısa çizgi içerebilir.
5. Tıklatın **abonelik** toosee hello kullanılabilir abonelik listesini. Hangi abonelik toouse emin değilseniz, hello varsayılan kullanın (veya önerilen) aboneliği. Yalnızca kuruluş hesabınızın birden çok Azure aboneliği ile ilişkili olması durumunda birden çok seçenek olur.
6. Tıklatın **kaynak grubu** toosee hello kullanılabilir kaynak gruplarının listesini ya da tıklatın **yeni** toocreate yeni bir kaynak grubu. Kaynak grupları hakkında eksiksiz bilgiler için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md)
7. Tıklatın **konumu** tooselect hello hello kasa için coğrafi bölgeyi.
8. **Oluştur**'a tıklayın. Oluşturulan toobe kurtarma Hizmetleri kasası hello için biraz zaman alabilir. Merhaba üst sağ alanında hello portal Hello durum bildirimlerini izleyin.
   Kasanız oluşturulduktan sonra hello Portalı'nda açılır.

### <a name="set-storage-replication"></a>Depolama Çoğaltmayı Ayarlama
Merhaba depolama çoğaltma seçeneği, coğrafi olarak yedekli depolama ve yerel olarak yedekli depolama arasında toochoose sağlar. Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir. Bu kasaya birincil kasanızı hello depolama seçeneği kümesi toogeo yedekli depolama bırakın. Daha düşük dayanıklılık düzeyinde olan daha uygun maliyetli bir seçenek istiyorsanız yerel olarak yedekli depolamayı seçin. Daha fazla bilgi edinin [coğrafi olarak yedekli](../storage/common/storage-redundancy.md#geo-redundant-storage) ve [yerel olarak yedekli](../storage/common/storage-redundancy.md#locally-redundant-storage) hello Depolama Seçenekleri [Azure Storage Çoğaltmaya genel bakış](../storage/common/storage-redundancy.md).

tooedit hello depolama çoğaltma ayarı:

1. Kasa tooopen hello kasa panosu ve hello ayarları dikey seçin. Merhaba, **ayarları** dikey penceresi açılmazsa, tıklatın **tüm ayarları** hello kasa panosunda.
2. Merhaba üzerinde **ayarları** dikey penceresinde tıklatın **Yedekleme Altyapısı** > **yedekleme yapılandırması** tooopen hello **yedekleme yapılandırması** dikey. Merhaba üzerinde **yedekleme yapılandırması** dikey penceresinde kasanızı hello depolama çoğaltma seçeneğini seçin.

    ![Yedekleme kasalarının listesi](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Merhaba kasanız için depolama seçeneğini belirledikten sonra hazır tooassociate hello VM hello kasası ile demektir. toobegin hello ilişkilendirme bulmak ve gerekir kaydetmek Azure sanal makineleri hello.

## <a name="3-software-package"></a>3. Yazılım paketi
### <a name="downloading-hello-software-package"></a>Merhaba yazılım paketini indirme
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Açık bir kurtarma Hizmetleri kasası zaten varsa toostep 3 devam edin. Açık kurtarma Hizmetleri kasanız yoksa ancak hello hello Hub menüsünde, Azure portalında bulunan tıklatmak **Gözat**.

   * Kaynakları Hello listesinde yazın **kurtarma Hizmetleri**.
   * Yazmaya başladığınızda, hello filtreleyecek girişinize bağlı. **Kurtarma Hizmetleri kasaları** seçeneğini gördüğünüzde buna tıklayın.

     ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png)

     Merhaba kurtarma Hizmetleri kasalarının listesi görüntülenir.
   * Kurtarma Hizmetleri kasalarının Hello listesinden bir kasa seçin.

     Merhaba seçilen kasa panosu açılır.

     ![Kasa dikey penceresini açma](./media/backup-azure-microsoft-azure-backup/vault-dashboard.png)
3. Merhaba **ayarları** dikey varsayılan olarak açılır. Kapalıysa, tıklayın **ayarları** tooopen hello ayarlar dikey penceresi.

    ![Kasa dikey penceresini açma](./media/backup-azure-microsoft-azure-backup/vault-setting.png)
4. Tıklatın **yedekleme** tooopen hello Başlangıç Sihirbazı.

    ![Başlarken yedekleme](./media/backup-azure-microsoft-azure-backup/getting-started-backup.png)

    Merhaba, **yedekleme ile çalışmaya başlama** açar, dikey **yedekleme hedefleri** otomatik olarak seçilir.

    ![Yedekleme hedefleri-varsayılan-açılan](./media/backup-azure-microsoft-azure-backup/getting-started.png)

5. Merhaba, **yedekleme hedefi** dikey penceresinde, hello **, iş yükünü çalıştırdığı** menüsünde, select **şirket içi**.

    ![Şirket içi ve hedefleri olarak iş yükleri](./media/backup-azure-microsoft-azure-backup/backup-goals-azure-backup-server.png)

    Merhaba gelen **neler toobackup istediğiniz?** açılır menü, Azure yedekleme sunucusu kullanarak tooprotect istediğiniz ve ardından select hello iş yükleri **Tamam**.

    Merhaba **yedekleme ile çalışmaya başlama** Sihirbazı anahtarları hello **altyapıyı hazırlama** seçeneği tooback iş yükleri tooAzure ayarlama.

   > [!NOTE]
   > Hello Azure Backup aracısını kullanan ve hello makale hello kılavuzunda aşağıdaki yalnızca tooback dosya ve klasörleri yedeklemek istiyorsanız, öneririz [ilk bakış: dosyaları ve klasörleri yedekleyin](backup-try-azure-backup-in-10-mins.md). Tooprotect kullanacaksanız dosyaları ve klasörleri veya tooexpand hello koruma planladığınıza fazlasını gerekir hello gelecekte select bu iş yükleri.
   >
   >

    ![Başlarken Sihirbazı'nı değişiklik alma](./media/backup-azure-microsoft-azure-backup/getting-started-prep-infra.png)

6. Merhaba, **altyapıyı hazırlama** dikey penceresini açar, hello tıklatın **karşıdan** bağlantılarını Azure yedekleme sunucusu yükleme ve indirme kasa kimlik bilgileri. Azure yedekleme sunucusu toohello kurtarma Hizmetleri kasası kayıt sırasında hello kasa kimlik bilgileri kullanın. Merhaba bağlantılar toohello indirme burada hello yazılım paketi indirilebilir merkezi götürür.

    ![Azure yedekleme sunucusu için altyapıyı hazırlama](./media/backup-azure-microsoft-azure-backup/azure-backup-server-prep-infra.png)

7. Tüm hello dosyaları seçin ve tıklatın **sonraki**. Tüm dosyaları hello Microsoft Azure yedekleme indirme sayfasından gelen hello indirme ve tüm dosyalarda hello Yerleştir aynı klasöre hello.

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
2. Merhaba Hoş Geldiniz ekranında hello tıklatın **sonraki** düğmesi. Bu toohello sürer *önkoşul denetler* bölümü. Bu ekranda tıklatın **denetleyin** Azure yedekleme sunucusu hello donanım ve yazılım önkoşulları karşılanıyorsa toodetermine. Tüm Önkoşullar başarıyla sağlanıyorsa bu hello makine hello gereksinimleri karşılayan belirten bir ileti görürsünüz. Tıklatın hello üzerinde **sonraki** düğmesi.

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

    Merhaba sonraki tooconfigure hello Microsoft Azure kurtarma Hizmetleri Aracısı adımdır. Merhaba yapılandırmasının parçası olarak, kasa kimlik bilgileri tooregister hello makine toohello kurtarma Hizmetleri tooprovide olacaktır kasası. Ayrıca, şirket içi ve Azure arasında gönderilen bir parola tooencrypt/şifre çözme hello verileri sağlar. Otomatik olarak bir parola oluşturmak veya kendi en az 16 karakter parola girin. Merhaba Aracısı yapılandırılana kadar hello sihirbazına devam edin.

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
Azure yedekleme sunucusu hello ürün toowork için bağlantı toohello Azure Backup hizmeti başarıyla gerektirir. toovalidate hello makine hello bağlantı tooAzure olup olmadığını hello kullan ```Get-DPMCloudConnection``` hello Azure yedekleme sunucusu PowerShell konsolunda cmdlet'i. Merhaba, bağlantı varsa hello cmdlet'in çıktısı, doğru ise, başka bağlantısı yok.

Merhaba sağlıklı bir durumda toobe aynı zamanda, hello Azure aboneliği gerekir. Aboneliğiniz ve toomanage hello durumu çıkışı toofind, toohello günlüğünde [abonelik portal](https://account.windowsazure.com/Subscriptions).

Merhaba durumu hello Azure bağlantısı ve hello Azure aboneliği öğrendikten sonra sunulan hello yedekleme/geri yükleme işlevselliği üzerinde toofind hello etkisi çıkışı aşağıdaki hello tabloyu kullanabilirsiniz.

| Bağlantı durumu | Azure Aboneliği | TooAzure yedekleyin | Toodisk yedekleyin | Azure'dan geri yükleme | Disk, geri yükleme |
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

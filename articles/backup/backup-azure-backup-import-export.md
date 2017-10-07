---
title: "aaaAzure yedekleme - Çevrimdışı Yedekleme ya da ilk dengeli dağıtım kullanarak Azure içeri/dışarı aktarma hizmeti hello | Microsoft Docs"
description: "Nasıl hello Azure içeri/dışarı aktarma hizmetini kullanarak hello ağ toosend verileri sağlar Azure yedekleme hakkında bilgi edinin. Bu makalede hello çevrimdışı hello ilk yedek verileri hello Azure içe aktarma dışarı aktarma hizmetini kullanarak dengeli açıklanmaktadır."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: ada19c12-3e60-457b-8a6e-cf21b9553b97
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/20/2017
ms.author: saurse;nkolli;trinadhk
ms.openlocfilehash: f1696957c3e9684b800c8d030131255905459f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="offline-backup-workflow-in-azure-backup"></a>Azure Backup’ta çevrimdışı yedekleme iş akışı
Azure yedekleme, ağ ve depolama maliyetlerini veri tooAzure ilk tam yedeklemesi sırasında hello Kaydet birkaç yerleşik verimliliği sahiptir. İlk tam yedeklemeler genellikle büyük miktarlarda veri aktarmak ve karşılaştırıldığında daha fazla ağ bant genişliği gerektiren hello farkları/incrementals yalnızca Aktarım toosubsequent yedekler. Azure yedekleme hello ilk yedekleme sıkıştırır. Çevrimdışı dengeli hello sürecinde, diskleri tooupload sıkıştırılmış hello ilk yedek verileri çevrimdışı tooAzure Azure Yedekleme'yi kullanabilirsiniz.  

Hello Azure yedekleme işlemini çevrimdışı dengeli hello ile tümleşiktir [Azure içeri/dışarı aktarma hizmeti](../storage/common/storage-import-export-service.md) sağlayan tootransfer veri tooAzure diskleri kullanarak. Yüksek gecikmeli ve düşük bant genişlikli ağ üzerinden aktarılan toobe gereken ilk yedek verileri terabayt (TBs) varsa, bir veya daha fazla sabit disk sürücüler tooan'üzerinde Azure veri merkezi hello dengeli çevrimdışı iş akışı tooship hello ilk yedek kopyayı kullanabilirsiniz. Bu makalede, bu iş akışını tamamlamak hello adımlara genel bir bakış sağlar.

## <a name="overview"></a>Genel Bakış
Merhaba dengeli çevrimdışı Azure Backup ve Azure içeri/dışarı aktarma ile basit tooupload hello veri çevrimdışı tooAzure diskleri kullanarak bir yetenektir. Merhaba ilk tam kopya hello ağ üzerinden aktarılması yerine hello yedekleme verilerini tooa yazılır *hazırlama konumuna*. Hello kopyalama toohello hazırlama konumu hello Azure içeri/dışarı aktarma aracını kullanarak tamamlandıktan sonra bu veriler, hello veri miktarına bağlı olarak tooone ya da daha fazla SATA sürücülerini yazılır. Bu sürücüleri Azure veri merkezinde en yakın sonunda sevk edilen toohello sağlar.

Merhaba [Azure Yedekleme'nin (ve daha sonra) güncelleştirme Ağustos 2016](http://go.microsoft.com/fwlink/?LinkID=229525) hello içeren *Azure Disk Hazırlama aracı*, AzureOfflineBackupDiskPrep, adlı:

* Sürücülerinizin hello Azure içeri/dışarı aktarma aracını kullanarak Azure alma için hazırlanmanıza yardımcı olur.
* Otomatik olarak üzerinde hello hello Azure içeri/dışarı aktarma hizmeti için bir Azure içe aktarma işi oluşturur [Klasik Azure portalı](https://manage.windowsazure.com) karşılıklı toocreating aynı el ile eski sürümleri Azure yedekleme ile Merhaba.

Merhaba yedekleme verilerini tooAzure Hello karşıya yükleme tamamlandıktan sonra Azure Backup hello yedekleme verilerini toohello yedekleme kasası kopyalar ve hello artımlı yedeklemeler zamanlanır.

> [!NOTE]
> toouse hello Azure Disk hazırlığı aracı, hello Ağustos 2016 güncelleştirmenin Azure Yedekleme'nin (veya üstü) yüklü olduğu ve hello akışıyla tüm hello adımları gerçekleştirmek emin olun. Azure Backup eski bir sürümünü kullanıyorsanız, hello Azure içeri/dışarı aktarma aracı ayrıntılı, bu makalenin sonraki bölümlerinde kullanarak hello SATA sürücü hazırlayabilirsiniz.
>
>

## <a name="prerequisites"></a>Ön koşullar
* [Hello Azure içeri/dışarı aktarma iş akışı ile öğrenmeniz](../storage/common/storage-import-export-service.md).
* Merhaba iş akışı başlatmadan önce hello aşağıdakilerden emin olun:
  * Bir Azure yedekleme kasası oluşturuldu.
  * İndirilen kasa kimlik bilgileri.
  * Hello Azure Yedekleme aracısı Windows Server/Windows istemci veya System Center Data Protection Manager sunucu üzerinde yüklü ve hello bilgisayar hello Azure yedekleme kasasına kayıtlı.
* [Karşıdan yükleme dosyası ayarları Azure yayımlama Hello](https://manage.windowsazure.com/publishsettings) hello bilgisayarda içinden planladığınız tooback verilerinizi yedekleyin.
* Bir ağ paylaşımına veya hello bilgisayarda ek sürücü olabilir bir hazırlama konumu hazırlayın. Hazırlama konumuna hello geçici depolama ve geçici olarak bu iş akışı sırasında kullanılır. Bu hello hazırlama konumuna ilk kopyanızı yeterli disk alanı toohold olduğundan emin olun. Örneğin, 500 GB dosya sunucusu tooback çalışıyorsanız, en az 500 GB bu hello hazırlama alanı olduğundan emin olun. (Daha küçük miktarda son kullanılan toocompression.)
* Desteklenen bir sürücü kullandığınızdan emin olun. Yalnızca 2,5 inç, SSD veya 2.5 veya 3,5 inç SATA II/III dahili sabit sürücüler, hello içeri/dışarı aktarma hizmeti ile kullanım için desteklenir. Too10 TB sabit sürücüleri kullanabilirsiniz. Merhaba denetleyin [Azure içeri/dışarı aktarma hizmeti belgeleri](../storage/common/storage-import-export-service.md#hard-disk-drives) hello en son hizmet destekler hello sürücüleri kümesi için.
* BitLocker'ı etkinleştirmek hello bilgisayar toowhich üzerinde hello SATA sürücü yazan bağlandı.
* [Hello Azure içeri/dışarı aktarma Aracı'nı indirme](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409) toohello bilgisayar toowhich hello SATA sürücü yazıcısı bağlı. İndirilen ve hello Ağustos 2016 güncelleştirme Azure Yedekleme'nin (veya üstü) yüklü, bu adım gerekli değildir.

## <a name="workflow"></a>İş akışı
Merhaba bu bölümdeki bilgiler, böylece verilerinizi tooan Azure veri merkezi teslim edilebilir hello Çevrimdışı Yedekleme iş akışı tamamlamanıza yardımcı olur ve tooAzure depolama yüklenir. Merhaba hello içeri aktarma hizmeti veya herhangi bir yönü hello işleminin hakkında sorularınız varsa bkz [alma hizmetine genel bakış](../storage/common/storage-import-export-service.md) daha önce başvurulan belgeleri.

### <a name="initiate-offline-backup"></a>Çevrimdışı Yedekleme başlatmak
1. Bir yedekleme işini zamanlamak için Merhaba ekranında (Windows Server, Windows istemci veya System Center Data Protection Manager) aşağıdaki görürsünüz.

    ![İçeri aktarma ekran](./media/backup-azure-backup-import-export/offlineBackupscreenInputs.png)

    System Center Data Protection Manager hello karşılık gelen ekran şöyledir: <br/>
    ![DPM içeri aktarma ekran](./media/backup-azure-backup-import-export/dpmoffline.png)

    Merhaba girişleri Hello açıklaması aşağıdaki gibidir:

    * **Hazırlama konumu**: hello geçici depolama konumu toowhich hello ilk yedek kopyayı yazılır. Bu, bir ağ paylaşımına veya yerel bilgisayarda olabilir. Merhaba kopya bilgisayar ve kaynak bilgisayar farklıysa, hazırlama konumuna hello hello tam ağ yolunu belirtin önerilir.
    * **Azure içeri aktarma iş adı**: hangi Azure alma tarafından hizmet ve Azure Backup izleyen hello gönderilen veri aktarımını diskleri tooAzure üzerinde hello benzersiz adı.
    * **Azure yayımlama ayarları**: Abonelik profilinizi hakkında bilgi içeren bir XML dosyası. Ayrıca, aboneliğinizle ilişkili güvenli kimlik bilgileri içerir. Yapabilecekleriniz [hello dosya indirme](https://manage.windowsazure.com/publishsettings). Sağlamak hello yerel yol toohello yayımlama ayarları dosyası.
    * **Azure abonelik kimliği**: hello abonelik planı nerede tooinitiate hello Azure içe aktarma işi için Azure abonelik kimliği hello. Birden çok Azure aboneliğiniz varsa, hello tooassociate hello içeri aktarma işi ile istediğiniz hello abonelik Kimliğini kullanın.
    * **Azure depolama hesabı**: hello hello Klasik tür depolama hesabında sağlanan hello Azure içe aktarma işi ile ilişkilendirilecek Azure aboneliği.
    * **Azure depolama kapsayıcısının**: hello adını hello hedef depolama blob hello Azure depolama hesabı bu işin verileri nerede alınır.

    > [!NOTE]
    > Sunucu tooan kaydolduysanız hello Azure kurtarma Hizmetleri kasası [Azure portal](https://portal.azure.com) değil ve yedeklemeler için bir bulut çözümü sağlayıcısı (CSP) abonelik depolama hesabı Klasik türü hello oluşturabilirsiniz Azure portal ve hello Çevrimdışı Yedekleme iş akışı için kullanın.
    >
    >

     Tooenter gerektiğinden bu bilgileri kaydetmek, aşağıdaki adımları yeniden içinde. Yalnızca hello *hazırlama konumuna* hello Azure Disk Hazırlık Aracı tooprepare hello diskleri kullandıysanız gereklidir.    
2. Merhaba iş akışı tamamlayın ve ardından **Şimdi Yedekle** hello Azure yedekleme Yönetim Konsolu tooinitiate hello Çevrimdışı Yedekleme kopyasında. Merhaba ilk yedekleme toohello hazırlama alanı bu adım bir parçası olarak yazılır.

    ![Şimdi Yedekle](./media/backup-azure-backup-import-export/backupnow.png)

    toocomplete hello karşılık gelen iş akışı içinde System Center Data Protection Manager, sağ tıklatın, hello **koruma grubu**ve ardından hello **kurtarma noktası oluşturma** seçeneği. Ardından hello Seçtiğiniz **çevrimiçi koruma** seçeneği.

    ![Şimdi DPM yedekleme](./media/backup-azure-backup-import-export/dpmbackupnow.png)

    Merhaba işlemi tamamlandıktan sonra hazırlama konumuna hello disk hazırlığı için kullanılan hazır toobe ' dir.

    ![Yedekleme ilerleme durumu](./media/backup-azure-backup-import-export/opbackupnow.png)

### <a name="prepare-a-sata-drive-and-create-an-azure-import-job-by-using-hello-azure-disk-preparation-tool"></a>SATA sürücü hazırlamak ve hello Azure Disk hazırlığı aracını kullanarak bir Azure alma işi oluşturma
Hello Azure Disk Hazırlama aracı hello kurtarma Hizmetleri aracısını yükleme dizininde kullanılabilir (Ağustos 2016 güncelleştirin ve daha sonra) yolu izleyerek hello içinde.

   *\Microsoft* *azure* *kurtarma* *Hizmetleri* * Agent\Utils\*

1. Kopya hello gidip toohello directory **AzureOfflineBackupDiskPrep** directory tooa kopya bilgisayar şu hangi hello üzerinde hazırlanmış sürücüleri toobe bağlandı. Hesaba toohello kopyalama bilgisayarla Hello aşağıdakilerden emin olun:

    * Merhaba kopya bilgisayar hello dengeli çevrimdışı iş akışı için aynı ağ hello sağlanan yolu hello kullanarak hazırlama hello erişebilir **başlatmak Çevrimdışı Yedekleme** iş akışı.
    * BitLocker hello bilgisayarda etkin.
    * Merhaba bilgisayar hello Azure portalına erişebilir.

    Gerekirse, hello kopya bilgisayar olması hello hello kaynak bilgisayar ile aynı.
2. Hello Azure Disk Hazırlık Aracı dizini hello geçerli dizini olarak hello kopyalama bilgisayarda yükseltilmiş bir komut istemi açın ve hello aşağıdaki komutu çalıştırın:

    `*.\AzureOfflineBackupDiskPrep.exe*   s:<*Staging Location Path*>   [p:<*Path tooPublishSettingsFile*>]`

    | Parametre | Açıklama |
    | --- | --- |
    | s:&lt;*hazırlama konumu yolu*&gt; |Hazırlama hello girdiğiniz konumuna tooprovide hello yolu toohello kullandı Zorunlu giriş **başlatmak Çevrimdışı Yedekleme** iş akışı. |
    | p:&lt;*yolu tooPublishSettingsFile*&gt; |Tooprovide hello yolu toohello kullanılan isteğe bağlı giriş **Azure yayımlama ayarları** hello girdiğiniz dosya **başlatmak Çevrimdışı Yedekleme** iş akışı. |

    > [!NOTE]
    > Merhaba &lt;yolu tooPublishSettingFile&gt; hello kopya bilgisayar ve kaynak bilgisayar farklı olduğunda değer zorunludur.
    >
    >

    Merhaba komutu çalıştırdığınızda, hello aracı hello seçimi hazırlanmış toobe gerek toohello sürücüleri karşılık gelen hello Azure Alma işinin ister. Yalnızca bir tek içe aktarma işi hazırlama konumu sağlanan hello ile ilişkilidir, izleyen bir hello gibi bir ekran görürsünüz.

    ![Azure Disk Hazırlık Aracı giriş](./media/backup-azure-backup-import-export/azureDiskPreparationToolDriveInput.png) <br/>
3. Merhaba sürücü harfini izleyen iki nokta üst üste hello bağlı disk için Aktarım tooAzure tooprepare istediğiniz hello olmadan girin. Merhaba istendiğinde hello sürücüsünü biçimlendirmek için onay sağlayın.

    Merhaba aracı sonra tooprepare hello disk hello yedekleme verileri ile başlar. Disk hello yedekleme verileri için yeterli alanı yok hello sağlanan durumda hello aracı tarafından istendiğinde tooattach ek diskleri gerekebilir. <br/>

    Merhaba aracı aktarılmadığı Hello sonunda, sağladığınız bir veya daha fazla disk sevkiyat tooAzure için hazırlanır. Ayrıca, hello ada sahip bir içeri aktarma iş hello sırasında sağladığınız **başlatmak Çevrimdışı Yedekleme** iş akışı, Klasik Azure portalı hello üzerinde oluşturulur. Son olarak, hello aracı görüntüler sevkiyat adresi toohello hello diskleri sevk toobe gereken yeri Azure veri merkezi hello ve bağlantı toolocate hello alma işi hello Klasik Azure portalı üzerinde hello.

    ![Azure disk hazırlığı tamamlandı](./media/backup-azure-backup-import-export/azureDiskPreparationToolSuccess.png)<br/>

4. Sevk hello diskleri toohello sağlanan bu hello aracı adres ve izleme numarası ileride kullanılmak üzere hello tutun.<br/>

5. Toohello gittiğinizde görüntülenen hello aracı bağlantı, hello belirtilen hello Azure depolama hesabı gördüğünüz **başlatmak Çevrimdışı Yedekleme** iş akışı. Burada hello üzerinde yeni oluşturulan hello alma işi görebilirsiniz **İÇERİ/dışarı aktarma** hello depolama hesabı sekmesinde.

    ![Oluşturulan alma işi](./media/backup-azure-backup-import-export/ImportJobCreated.png)<br/>

6. Tıklatın **Sevkiyat bilgisi** hello hello sayfa tooupdate sonunda kişiniz hello ekran aşağıdaki gösterildiği gibi ayrıntıları. Microsoft bu bilgileri tooship hello içeri aktardıktan sonra iş, diskleri geri tooyou tamamlandı kullanır.

    ![İletişim bilgileri](./media/backup-azure-backup-import-export/contactInfoAddition.PNG)<br/>

7. Hello hello sonraki ekranda sevkiyat ayrıntılarını girin. Merhaba sağlamak **teslim taşıyıcı** ve **izleme numarası** toohello Azure veri merkezi sevk toohello diskleri karşılık ayrıntıları.

    ![Sevkiyat bilgileri](./media/backup-azure-backup-import-export/shippingInfoAddition.PNG)<br/>

### <a name="complete-hello-workflow"></a>Tam hello iş akışı
Merhaba alma işi tamamlandıktan sonra ilk yedek verileri depolama hesabınızdaki kullanılabilir. Merhaba kurtarma Hizmetleri aracısını ardından kopya hello içeriğini hello verileri bu hesabı toohello yedekleme kasası veya kurtarma Hizmetleri kasası, bunlardan hangisi söz konusuysa. Sonraki zamanlanmış hello yedekleme zamanında hello Azure Yedekleme aracısı hello ilk yedek kopyayı hello artımlı yedekleme gerçekleştirir.

> [!NOTE]
> Merhaba aşağıdaki bölümlerde toousers erişim toohello Azure Disk Hazırlık Aracı yüklü olmayan önceki sürümlerinin Azure Backup uygulayın.
>
>

### <a name="prepare-a-sata-drive"></a>SATA sürücüyü hazırlama
1. Merhaba karşıdan [Microsoft Azure içeri/dışarı aktarma aracı](http://go.microsoft.com/fwlink/?linkid=301900&clcid=0x409) toohello kopya bilgisayar. Hazırlama konumuna bu hello toorun hello sonraki komut kümesini planlama hello bilgisayardan erişilebilir olduğundan emin olun. Gerekirse, hello kopya bilgisayar olması hello hello kaynak bilgisayar ile aynı.

2. Merhaba WAImportExport.zip dosyanın sıkıştırmasını açın. Merhaba SATA sürücü biçimleri, hello yedekleme verilerini toohello SATA sürücü yazar ve bunu şifreler hello WAImportExport aracını çalıştırın. Komutu aşağıdaki hello çalıştırmadan önce BitLocker hello bilgisayarda etkinleştirildiğinden emin olun. <br/>

    `*.\WAImportExport.exe PrepImport /j:<*JournalFile*>.jrn /id: <*SessionId*> /sk:<*StorageAccountKey*> /BlobType:**PageBlob** /t:<*TargetDriveLetter*> /format /encrypt /srcdir:<*staging location*> /dstdir: <*DestinationBlobVirtualDirectory*>/*`

    > [!NOTE]
    > Merhaba Ağustos 2016 güncelleştirme Azure Yedekleme'nin (veya üstü) yüklü değilse, girdiğiniz hazırlama bu hello hello birinde hello aynı hello olduğundan emin olun **Şimdi Yedekle** ekranında ve AIB ve temel Blob dosyalarını içerir.
    >
    >

| Parametre | Açıklama |
| --- | --- |
| /j: <*JournalFile*> |Merhaba yol toohello günlük dosyası. Her bir sürücü tam olarak bir günlük dosyası olmalıdır. Merhaba günlük dosyası hello hedef sürücüde olmaması gerekir. Merhaba günlük dosya uzantısının .jrn ve bu komutu çalıştıran bir parçası olarak oluşturulur. |
| /ID: <*SessionID*> |Merhaba oturum kimliği kopyalama oturumu tanımlar. Bu, kullanılan tooensure doğru kurtarma kesintiye uğramış kopyalama oturumu olur. Bir kopyalama oturumda kopyalanır dosyaları hello oturum kimliği hello hedef sürücüde sonra adlı bir dizinde depolanır. |
| /SK: <*StorageAccountKey*> |Merhaba hesap anahtarı hello depolama hesabı toowhich hello veriler için alınır. Merhaba anahtar gereksinimlerini toobe hello aynı şekilde yedekleme İlkesi/koruma grubu oluşturma sırasında girildi. |
| / BlobType |blob Hello türü. Yalnızca bu iş akışı başarılı **PageBlob** belirtilir. Bu hello varsayılan seçeneği değil ve bu komutta belirtilen. |
| / t: <*TargetDriveLetter*> |Merhaba sürücü harfi hello geçerli kopyalama oturumu için iki nokta üst üste hello hedef sabit sürücüde sondaki hello olmadan. |
| Format |Merhaba seçeneği tooformat hello sürücü. Sürücü Merhaba biçimlendirilmiş toobe gerektiğinde bu parametreyi belirtin; Aksi takdirde yok sayın. Merhaba aracı hello sürücü biçimleri önce hello konsolundan onay ister. toosuppress hello onay hello /silentmode parametresini belirtin. |
| / şifrele |Merhaba seçeneği tooencrypt hello sürücü. Merhaba sürücü henüz hello aracı tarafından şifrelenmiş BitLocker ve gereksinimlerini toobe ile şifrelenmiş değil, bu parametreyi belirtin. Merhaba sürücüsü BitLocker ile şifrelenmiş, bu parametreyi, hello /bk parametresini belirtin ve hello varolan BitLocker anahtarı sağlayın. Merhaba Format parametresini belirtirseniz, ayrıca hello belirtin / parametre şifreleme gerekir. |
| /srcdir: <*SourceDirectory*> |dosyaları toobe içeren hello kaynak dizin toohello hedef sürücü kopyalanır. Bu hello belirtilen dizin adı bir tam yerine göreli yol olduğundan emin olun. |
| /dstdir: <*DestinationBlobVirtualDirectory*> |Merhaba yolu toohello hedef sanal dizin Azure depolama hesabınızdaki. Merhaba hedef sanal dizinleri ve blobları belirttiğinizde emin toouse geçerli kapsayıcı adları olabilir. Kapsayıcı adları küçük harfli olması gerektiğini unutmayın.  Bu kapsayıcı adı hello bir yedekleme İlkesi/koruma grubu oluşturma sırasında girilen olmalıdır. |

> [!NOTE]
> Bir günlük dosyası hello tüm bilgileri hello iş akışının yakalar hello WAImportExport klasöründe oluşturulur. Hello Azure portal içeri aktarma işi oluşturduğunuzda bu dosya gerekir.
>
>

  ![PowerShell çıkışı](./media/backup-azure-backup-import-export/psoutput.png)

### <a name="create-an-import-job-in-hello-azure-portal"></a>Hello Azure portalında bir içeri aktarma işi oluşturma
1. Merhaba tooyour depolama hesabında Git [Klasik Azure portalı](https://manage.windowsazure.com/), tıklatın **içeri/dışarı aktarma**ve ardından **alma işi oluştur** hello görev bölmesinde.

    ![İçeri/dışarı aktarma sekmesinde hello Azure portalı](./media/backup-azure-backup-import-export/azureportal.png)

2. 1. adımda hello Sihirbazı'nın sürücünüze hazırladıktan ve hello sürücü günlük dosyasının kullanılabilir olduğunu gösterir.

3. 2. adımda hello Sihirbazı'nın bu içeri aktarma işi için sorumlu olan hello kişi için kişi bilgilerini sağlayın.

4. 3. adımda hello önceki bölümde edindiğiniz hello sürücü günlük dosyalarını karşıya yükleyin.

5. 4. adımda, yedekleme İlkesi/koruma grubu oluşturma sırasında girilen hello içe aktarma işi için açıklayıcı bir ad girin. Girdiğiniz hello adı içerebilir yalnızca küçük harfler, sayılar, tire ve alt çizgi, bir harf ile başlamalı ve boşluk içermemelidir. devam eden ve tamamlandıktan sonra sağlarken kullanılan tootrack işleriniz olduğu seçtiğiniz hello adı.

6. Ardından, veri merkezi bölgenizi hello listeden seçin. Merhaba datacenter bölge paketinizi hazırlamalısınız hello datacenter ve adres toowhich gösterir.

    ![Veri Merkezi bölgeyi seçin](./media/backup-azure-backup-import-export/dc.png)

7. 5. adım, dönüş taşıyıcı hello listeden seçin ve taşıyıcı hesap numaranızı girin. Microsoft, bu hesabı kullanır tooship sürücülerinizin geri tooyou alma işi tamamlandıktan sonra.

8. Merhaba disk sevk ve hello Sevkiyat Numara tootrack hello durumunu izleme hello girin. Merhaba disk hello veri merkezinde ulaşan sonra toohello depolama hesabına kopyalanır ve hello durumu güncelleştirilir.

    ![Tamamlanma durumu](./media/backup-azure-backup-import-export/complete.png)

### <a name="complete-hello-workflow"></a>Tam hello iş akışı
Merhaba ilk yedek verileri hello Microsoft Azure kurtarma Hizmetleri aracısını hello veri Merhaba içeriğine, bu hesabı toohello yedekleme kasası veya kurtarma Hizmetleri kasası kopyalar. depolama hesabınızdaki kullanılabilir olduktan sonra bunlardan hangisi söz konusuysa. Merhaba sonraki zamanlamada yedekleme saati, hello Azure Yedekleme aracısı hello ilk yedek kopyayı hello artımlı yedekleme gerçekleştirir.

## <a name="next-steps"></a>Sonraki adımlar
* Hello Azure içeri/dışarı aktarma iş akışı üzerinde herhangi bir sorunuz için çok başvuran[hello Microsoft Azure içeri/dışarı aktarma hizmeti tootransfer veri tooBlob depolama kullanan](../storage/common/storage-import-export-service.md).
* Azure Backup hello toohello Çevrimdışı Yedekleme bölümüne bakın [SSS](backup-azure-backup-faq.md) hello iş akışıyla ilgili herhangi bir sorunuz için.

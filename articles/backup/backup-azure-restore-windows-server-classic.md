---
title: "Azure kullanarak aaaRestore veri tooa Windows Server veya Windows İstemcisi hello Klasik dağıtım modeli | Microsoft Docs"
description: "Bilgi nasıl toorestore bir Windows Server veya Windows İstemcisi."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a>Dosyaları tooa Windows server veya Windows istemci makinesi hello Klasik dağıtım modeli kullanılarak geri yükleme
> [!div class="op_single_selector"]
> * [Klasik portal](backup-azure-restore-windows-server-classic.md)
> * [Azure portal](backup-azure-restore-windows-server.md)
>
>

Bu makalede, bir yedekten toorecover verinin nasıl kasa ve tooa sunucu veya bilgisayar geri açıklanmaktadır. Mart 2017'dan başlayarak, hello Klasik portalda yedekleme kasaları artık oluşturabilirsiniz.

> [!IMPORTANT]
> Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> **15 Ekim 2017**, artık mümkün toouse PowerShell toocreate yedekleme kasaları olacaktır. <br/> **1 Kasım 2017'den itibaren**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
>

toorestore veri hello Microsoft Azure kurtarma Hizmetleri (MARS) aracısı hello Veri Kurtarma Sihirbazı'nı kullanın. Verileri geri yüklediğinizde, mümkün olur:

* Aynı makine hangi hello yedeklerden geri yükleme veri toohello gerçekleştirilecek.
* Veri tooan alternatif makine geri yükleyin.

Ocak 2017 ' Microsoft, Önizleme update toohello MARS Aracısı yayımladı. Hata düzeltmeleri yanı sıra, bu güncelleştirme anlık toomount sağlayan geri yükleme, yazılabilir kurtarma noktası anlık görüntü kurtarma birimi olarak sağlar. Ardından, böylece seçerek dosyaları geri yükleme hello kurtarma birimi ve kopyalama dosyaları tooa yerel bilgisayara keşfedebilirsiniz.

> [!NOTE]
> Merhaba [Ocak 2017 Azure Backup güncelleştirmesini](https://support.microsoft.com/en-us/help/3216528?preview) toouse toorestore verilerin anlık geri yüklemek istiyorsanız gereklidir. Ayrıca hello destek makalesinde listelenen yerel ayarlar kasalarında hello yedekleme verilerini korunmalıdır. Merhaba başvurun [Ocak 2017 Azure Backup güncelleştirmesini](https://support.microsoft.com/en-us/help/3216528?preview) hello son anlık geri yükleme desteği yerel ayarların listesi için. Anlık geri yükleme **değil** tüm bölgelerde kullanılabilir.
>

Anlık geri yükleme hello Klasik Portalı'nda, Kurtarma Hizmetleri kasalarının hello Azure portal'ın kullanımda ve yedekleme kasaları için kullanılabilir. Toouse anlık geri yüklemek istiyorsanız, hello MARS güncelleştirmeyi indirin ve anlık geri Bahsediyor hello yordamları izleyin.


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a>Anlık geri toorecover veri toohello kullanmak aynı makine

Dosya ve istek toorestore yanlışlıkla sildiyseniz, (hangi hello yedekleme alınır) aynı makine hello aşağıdaki adımları toohello hello verileri kurtarmanıza yardımcı olur.

1. Açık hello **Microsoft Azure yedekleme** içinde Vurgu. Merhaba ek bileşeninde yüklendiği bilmiyorsanız, hello bilgisayar veya sunucu için arama **Microsoft Azure yedekleme**.

    Merhaba masaüstü uygulaması hello arama sonuçlarında görüntülenmesi gerekir.

2. Tıklatın **verileri kurtarabilirsiniz** toostart hello Sihirbazı.

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server/recover.png)

3. Merhaba üzerinde **Başlarken** bölmesi, toorestore hello veri toohello aynı sunucu bilgisayar seçin veya **bu sunucu (`<server name>`)** tıklatıp **sonraki**.

    ![Bu sunucu seçeneği toorestore hello veri toohello seçin aynı makine](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. Merhaba üzerinde **seçin kurtarma moduna** bölmesinde seçin **dosyalara ve klasörlere** ve ardından **sonraki**.

    ![Gözatma dosyaları](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. Merhaba üzerinde **birim seçin ve tarih** bölmesi, hello dosyaları ve/veya toorestore istediğiniz klasörleri içeren bir select hello birimi.

    Merhaba takvimde bir kurtarma noktası seçin. Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz. İçinde tarihleri **kalın** hello en az bir kurtarma noktası kullanılabilirliğini gösterir. Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra hello hello belirli bir kurtarma noktası seçin **zaman** açılır menü.

    ![Birimi ve tarih](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. Merhaba kurtarma noktası toorestore seçtikten sonra tıklatın **bağlama**.

    Azure yedekleme hello yerel kurtarma noktası bağlar ve kurtarma birimi olarak kullanır.

7. Hello üzerinde **Gözat ve kurtarma dosyaları** bölmesinde tıklatın **Gözat** tooopen Windows Gezgini, Bul hello dosya ve klasörleri istediğiniz.

    ![Kurtarma Seçenekleri](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. Windows Gezgini, kopyalama hello dosyaları ve/veya klasörleri de toorestore istediğiniz ve tooany konumu yerel toohello sunucusu veya bilgisayar yapıştırın. Açın veya hello dosyaları doğrudan hello kurtarma birimi akış ve hello sürümleri kurtarılan doğru doğrulayın.

    ![Dosyaları ve klasörleri takılı birim toolocal konumdan kopyalama ve yapıştırma](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. İşiniz bittiğinde geri yükleme hello dosyaları ve/veya klasörlerde hello **göz atın ve kurtarma dosyaları** bölmesinde tıklatın **çıkarma**. Ardından **Evet** tooconfirm toounmount hello birim istiyor.

    ![Merhaba birim çıkarın ve onaylayın](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > Çıkarma değil tıklatırsanız, hello kurtarma birimi zaman takıldı hello zamandan altı saat bağlı kalır. Merhaba birim bağlıyken hiçbir yedekleme işlemleri çalıştırın. Merhaba kurtarma birimi kaldırılan tamamlandıktan sonra tüm zamanlanmış yedekleme işlemi toorun hello birimin zaman bağlı, hello süre boyunca çalışır.
    >


## <a name="recover-data-toohello-same-machine"></a>Veri toohello kurtarmak aynı makine
Dosya ve istek toorestore yanlışlıkla sildiyseniz, (hangi hello yedekleme alınır) aynı makine hello aşağıdaki adımları toohello hello verileri kurtarmanıza yardımcı olur.

1. Açık hello **Microsoft Azure yedekleme** içinde Vurgu.
2. Tıklatın **verileri kurtarabilirsiniz** tooinitiate hello iş akışı.

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server-classic/recover.png)
3. Select hello  **bu sunucu (*yourmachinename*) ** seçeneğinin toorestore hello yedeklenen hello dosyada aynı makine.

    ![Aynı makine](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. Çok seçin**gözatma için dosyaları** veya **dosya aramak için**.

    Toorestore düşünüyorsanız, yolu bilinen bir veya daha fazla hello varsayılan seçeneği bırakın. Merhaba klasör yapısı hakkında emin değilseniz, ancak bir dosya için toosearch istersiniz, hello çekme **dosya aramak için** seçeneği. Bu bölümde Hello amaçla biz hello varsayılan seçeneği ile devam eder.

    ![Gözatma dosyaları](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. Toorestore hello dosya istediğiniz hello birimi seçin.

    Zaman içinde herhangi bir noktadan geri yükleyebilirsiniz. Görüntülenen tarihler **kalın** hello Takvim denetiminde bir geri yükleme noktası hello kullanılabilirliğini gösterir. Bir tarih seçildikten sonra yedekleme zamanlaması (ve yedekleme işlemini hello başarısını), temel bir noktası hello zamandan seçebileceğiniz **zaman** açılır.

    ![Birimi ve tarih](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. Merhaba öğeleri toorecover seçin. Çoklu seçim klasörleri/dosyaları toorestore istediğiniz kullanabilirsiniz.

    ![Dosya seçme](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. Merhaba kurtarma parametreleri belirtin.

    ![Kurtarma Seçenekleri](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * Bir seçeneğiniz toohello özgün konumuna (hangi hello dosya/klasör üzerine yazılacağını) veya hello tooanother konuma geri yüklenmesi, aynı makine.
   * Merhaba dosya/klasör, istediğiniz toorestore hello hedef konumda mevcut kopyaları oluşturabileceğiniz varsa (Merhaba iki sürümü aynı dosya) hello hedef konumda hello dosyaları üzerine veya, hello hedef mevcut hello dosyaların hello kurtarma işlemini atla.
   * Kurtarılmakta hello dosyaları hello ACL'ler geri yüklenmesi hello varsayılan seçeneği bırakın önerilir.
8. Bu girişleri sağlanan sonra tıklayın **sonraki**. Merhaba dosyaları toothis makineyi yükler, hello kurtarma akışı başlar.

## <a name="recover-tooan-alternate-machine"></a>Tooan alternatif makine Kurtar
Tüm sunucunuzu kaybolursa, verileri Azure yedekleme tooa farklı makineden kurtarmaya devam edebilirsiniz. Aşağıdaki adımları hello hello iş akışı gösterilmektedir.  

Bu adımlarda kullanılan hello terminolojisi içerir:

* *Kaynak makine* – hello özgün makine hangi hello yedekten alındığı ve hangi şu anda kullanılamıyor.
* *Hedef makine* – hello makine toowhich hello verilerin kurtarıldığı.
* *Örnek kasa* – hello yedekleme kasası toowhich hello *kaynak makine* ve *hedef makine* kaydedilir. <br/>

> [!NOTE]
> Bir makineden alınan yedeklemeler hello işletim sisteminin önceki bir sürümünü çalıştıran bir makineye geri yüklenemez. Yedeklemeler Windows 7 makineden alınır, örneğin, bir Windows 8 veya üstü makine geri yüklenebilir. Ancak, hello tam tersini true tutmaz.
>
>

1. Açık hello **Microsoft Azure yedekleme** hello üzerinde içinde Vurgu *hedef makine*.
2. Bu hello olun *hedef makine* ve hello *kaynak makine* kayıtlı toohello olan aynı yedekleme kasası.
3. Tıklatın **verileri kurtarabilirsiniz** tooinitiate hello iş akışı.

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server-classic/recover.png)
4. Seçin **başka bir sunucu**

    ![Başka bir sunucu](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. Toohello karşılık gelen hello kasa kimlik bilgilerini sağlayın *örnek kasa*. Merhaba kasa kimlik bilgilerini geçersiz (veya süresi dolmuş) ise yeni bir kasa kimlik bilgilerini hello indirin *örnek kasa* hello Klasik Azure Portalı'nda. Merhaba kasa kimlik bilgilerini sağlanan sonra hello yedekleme kasası hello kasa kimlik bilgilerini karşı görüntülenir.
6. Select hello *kaynak makine* görüntülenmesini makineler hello listesinden.

    ![Makineler listesi](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. Her iki hello seçin **dosya aramak için** veya **gözatma için dosyaları** seçeneği. Bu bölümde Hello amaçla hello kullanacağız **dosya aramak için** seçeneği.

    ![Arama](./media/backup-azure-restore-windows-server-classic/search.png)
8. Merhaba birimi ve tarih hello sonraki ekranında seçin. Arama toorestore istediğiniz için hello klasör/dosya adı.

    ![Arama öğeleri](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. Merhaba dosyaları geri toobe gereken yeri hello konumu seçin.

    ![Geri yükleme konumu](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. Sırasında sağlanan hello şifreleme parolası sağlamak *kaynak makinenin* kayıt çok*örnek kasa*.

    ![Şifreleme](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. Merhaba giriş sağlanan sonra tıklayın **kurtarmak**, hangi Tetikleyicileri hello sağlanan dosyaları toohello hedef yedeklenen hello geri yükleme.

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a>Toorestore veri tooan alternatif makine anında geri kullanın
Tüm sunucunuzu kaybolursa, verileri Azure yedekleme tooa farklı makineden kurtarmaya devam edebilirsiniz. Aşağıdaki adımları hello hello iş akışı gösterilmektedir.

Bu adımlarda kullanılan hello terminolojisi içerir:

* *Kaynak makine* – hello özgün makine hangi hello yedekten alındığı ve hangi şu anda kullanılamıyor.
* *Hedef makine* – hello makine toowhich hello verilerin kurtarıldığı.
* *Örnek kasa* – hello kurtarma Hizmetleri kasası toowhich hello *kaynak makine* ve *hedef makine* kaydedilir. <br/>

> [!NOTE]
> Yedeklemeler, geri yüklenen tooa hedef makine hello işletim sisteminin önceki bir sürümünü çalıştıran olamaz. Örneğin, bir Windows bilgisayarı olabilir 7'den alınan bir yedeklemeyi bilgisayar bir Windows 8 veya daha sonra geri. Bir Windows 8 bilgisayardan alınan bir yedeklemeyi geri yüklenen tooa Windows 7 bilgisayar olamaz.
>
>

1. Açık hello **Microsoft Azure yedekleme** hello üzerinde içinde Vurgu *hedef makine*.

2. Merhaba olun *hedef makine* ve hello *kaynak makine* aynı kurtarma Hizmetleri kasası kayıtlı toohello şunlardır.

3. Tıklatın **verileri kurtarabilirsiniz** tooopen hello **Veri Kurtarma Sihirbazı'nı**.

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server/recover.png)

4. Merhaba üzerinde **Başlarken** bölmesinde, **başka bir sunucu**

    ![Başka bir sunucu](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. Toohello karşılık gelen hello kasa kimlik bilgilerini sağlayın *örnek kasa*, tıklatıp **sonraki**.

    Merhaba kasa kimlik bilgilerini geçersiz (veya süresi dolmuş) varsa, yeni bir kasa kimlik bilgilerini hello indirin *örnek kasa* hello Azure Portalı'nda. Geçerli kasa kimlik bilgileri sağladığınızda, yedekleme kasası karşılık gelen hello hello adı görüntülenir.

6. Merhaba üzerinde **yedekleme sunucusu seçin** bölmesinde, select hello *kaynak makine* görüntülenmesini makineler hello listesinden ve hello parola girin. Ardından **İleri**'ye tıklayın.

    ![Makineler listesi](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. Merhaba üzerinde **seçin kurtarma moduna** bölmesinde seçin **dosyalara ve klasörlere** tıklatıp **sonraki**.

    ![Arama](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. Merhaba üzerinde **birim seçin ve tarih** bölmesi, hello dosyaları ve/veya toorestore istediğiniz klasörleri içeren bir select hello birimi.

    Merhaba takvimde bir kurtarma noktası seçin. Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz. İçinde tarihleri **kalın** hello en az bir kurtarma noktası kullanılabilirliğini gösterir. Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra hello hello belirli bir kurtarma noktası seçin **zaman** açılır menü.

    ![Arama öğeleri](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. Tıklatın **bağlama** toolocally bağlama hello kurtarma noktası olarak bir kurtarma birimde, *hedef makine*.

10. Hello üzerinde **Gözat ve kurtarma dosyaları** bölmesinde tıklatın **Gözat** tooopen Windows Gezgini, Bul hello dosya ve klasörleri istediğiniz.

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. Windows Gezgini'nde, hello dosyaları ve/veya klasörleri hello kurtarma birimden kopyalayıp bunları tooyour *hedef makine* konumu. Açın veya hello dosyaları doğrudan hello kurtarma birimi akış ve hello sürümleri kurtarılan doğru doğrulayın.

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. İşiniz bittiğinde geri yükleme hello dosyaları ve/veya klasörlerde hello **göz atın ve kurtarma dosyaları** bölmesinde tıklatın **çıkarma**. Ardından **Evet** tooconfirm toounmount hello birim istiyor.

    ![Şifreleme](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > Çıkarma değil tıklatırsanız, hello kurtarma birimi zaman takıldı hello zamandan altı saat bağlı kalır. Merhaba birim bağlıyken hiçbir yedekleme işlemleri çalıştırın. Merhaba kurtarma birimi kaldırılan tamamlandıktan sonra tüm zamanlanmış yedekleme işlemi toorun hello birimin zaman bağlı, hello süre boyunca çalışır.
    >


## <a name="next-steps"></a>Sonraki adımlar
* [Azure Backup ile ilgili SSS](backup-azure-backup-faq.md)
* Merhaba ziyaret [Azure yedekleme Forumu](http://go.microsoft.com/fwlink/p/?LinkId=290933).

## <a name="learn-more"></a>Daha fazla bilgi edinin
* [Azure yedekleme genel bakış](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [Yedekleme Azure sanal makineler](backup-azure-vms-introduction.md)
* [Microsoft iş yüklerini yedekleme](backup-azure-dpm-introduction.md)

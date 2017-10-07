---
title: "Azure tooa Windows Server veya Windows bilgisayarı aaaRestore verileri | Microsoft Docs"
description: "Azure tooa Windows Server veya Windows bilgisayarı toorestore verilerin depolanma öğrenin."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a>Dosyaları tooa Windows server veya Windows istemci makinesi Resource Manager dağıtım modelini kullanarak geri yükleme
> [!div class="op_single_selector"]
> * [Azure portal](backup-azure-restore-windows-server.md)
> * [Klasik portal](backup-azure-restore-windows-server-classic.md)
>
>

Bu makalede açıklanır nasıl bir yedekleme kasası toorestore verileri. toorestore veri hello Microsoft Azure kurtarma Hizmetleri (MARS) aracısı hello Veri Kurtarma Sihirbazı'nı kullanın. Verileri geri yüklediğinizde, mümkün olur:

* Aynı makine hangi hello yedeklerden geri yükleme veri toohello gerçekleştirilecek.
* Veri tooan alternatif makine geri yükleyin.

Ocak 2017 ' Microsoft, Önizleme update toohello MARS Aracısı yayımladı. Hata düzeltmeleri yanı sıra, bu güncelleştirme anlık toomount sağlayan geri yükleme, yazılabilir kurtarma noktası anlık görüntü kurtarma birimi olarak sağlar. Ardından, böylece seçerek dosyaları geri yükleme hello kurtarma birimi ve kopyalama dosyaları tooa yerel bilgisayara keşfedebilirsiniz.

> [!NOTE]
> Merhaba [Ocak 2017 Azure Backup güncelleştirmesini](https://support.microsoft.com/en-us/help/3216528?preview) toouse toorestore verilerin anlık geri yüklemek istiyorsanız gereklidir. Ayrıca hello destek makalesinde listelenen yerel ayarlar kasalarında hello yedekleme verilerini korunmalıdır. Merhaba başvurun [Ocak 2017 Azure Backup güncelleştirmesini](https://support.microsoft.com/en-us/help/3216528?preview) hello son anlık geri yükleme desteği yerel ayarların listesi için. Anlık geri yükleme **değil** tüm bölgelerde kullanılabilir.
>

Anlık geri yükleme hello Klasik Portalı'nda, Kurtarma Hizmetleri kasalarının hello Azure portal'ın kullanımda ve yedekleme kasaları için kullanılabilir. Toouse anlık geri yüklemek istiyorsanız, hello MARS güncelleştirmeyi indirin ve anlık geri Bahsediyor hello yordamları izleyin.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

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
    > Çıkarma değil tıklatırsanız, hello kurtarma birimi zaman takıldı hello zamandan 6 saat boyunca bağlı kalır. Ancak, genişletilmiş değerine kadar devam eden bir dosya kopyalama durumunda 24 saat maksimum hello bağlama zamanı geldi. Merhaba birim bağlıyken hiçbir yedekleme işlemleri çalıştırın. Merhaba kurtarma birimi kaldırılan tamamlandıktan sonra tüm zamanlanmış yedekleme işlemi toorun hello birimin zaman bağlı, hello süre boyunca çalışır.
    >


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
    > Çıkarma değil tıklatırsanız, hello kurtarma birimi zaman takıldı hello zamandan 6 saat boyunca bağlı kalır. Ancak, genişletilmiş değerine kadar devam eden bir dosya kopyalama durumunda 24 saat maksimum hello bağlama zamanı geldi. Merhaba birim bağlıyken hiçbir yedekleme işlemleri çalıştırın. Merhaba kurtarma birimi kaldırılan tamamlandıktan sonra tüm zamanlanmış yedekleme işlemi toorun hello birimin zaman bağlı, hello süre boyunca çalışır.
    >

## <a name="troubleshooting"></a>Sorun giderme
Azure Backup hello kurtarma birimi başarıyla tıklama bile birkaç dakika sonra bağlamaz varsa **bağlama** veya başarısız toomount hello kurtarma birimi bir veya daha fazla hata ile normalde kurtarma toobegin hello adımları izleyin.

1.  Birkaç dakika çalışıyor durumda hello devam eden bağlama işlemi iptal edin.

2.  Merhaba üzerinde hello Azure yedekleme Aracısı'nın en son sürüm olduğundan emin olun. Merhaba sürüm bilgilerini Azure yedekleme Aracısı'nın çıkışı toofind tıklayın **hakkında Microsoft Azure kurtarma Hizmetleri Aracısı** hello üzerinde **Eylemler** Microsoft Azure yedekleme bölmesinde konsol ve o hello eminolun **Sürüm** eşit tooor belirtilen hello sürümden daha yüksek sayıdır [bu makalede](https://go.microsoft.com/fwlink/?linkid=229525). Merhaba en son sürümü karşıdan [burada](https://go.microsoft.com/fwLink/?LinkID=288905)

3.  Çok Git**Aygıt Yöneticisi'ni** -> **depolama alanı denetleyicileri** ve, bulabilmesini sağlama **Microsoft iSCSI başlatıcısı**. Bulabiliyorsa, doğrudan toostep 7 aşağıdaki gidin. 

4.  Adım 3'te belirtildiği gibi Microsoft iSCSI başlatıcısı hizmetinin bulamazsanız, bir giriş altında bulabilirsiniz toosee denetleyin **Aygıt Yöneticisi'ni** -> **depolama alanı denetleyicileri** adlı  **Bilinmeyen aygıt** donanım kimliği ile **ROOT\ISCSIPRT**.

5.  Sağ tıklayın **bilinmeyen aygıt** seçip **sürücü yazılımı güncelleştirme**.

6.  Merhaba seçeneği çok seçerek güncelleştirme hello sürücü **otomatik olarak güncelleştirilen sürücü yazılım Ara**. Hello güncelleştirmesinin tamamlanması değiştirmek **bilinmeyen aygıt** çok**Microsoft iSCSI başlatıcısı** aşağıda gösterildiği gibi. 

    ![Şifreleme](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  Çok Git**Görev Yöneticisi'ni** -> **hizmetler (yerel)** -> **Microsoft iSCSI başlatıcısı hizmetini**. 

    ![Şifreleme](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  Tıklayarak, hello hizmetini sağ tıklayarak Hello Microsoft iSCSI başlatıcısı hizmetinin yeniden **durdurmak** ve sağ yeniden tıklatıp tıklayarak daha fazla **Başlat**.

9.  Anlık geri yükleme özelliğini kullanarak kurtarma yeniden deneyin. 

Merhaba kurtarma yine başarısız olursa, sunucu/istemci yeniden başlatın. Yeniden başlatma arzu değil veya hello kurtarma başarısız hello sunucu bile makine yeniden başlatıldıktan sonra başka bir makineden kurtarmayı deneyin ve çok giderek Azure desteği ile iletişim kurun[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ve bir destek isteği gönderiliyor.

## <a name="next-steps"></a>Sonraki adımlar
* Dosya ve klasörleri kurtarma yaptıktan, yapabilecekleriniz [Yedeklemelerinizin yönetmek](backup-azure-manage-windows-server.md).

---
title: Yedekleme Azure Linux VM'ler | Microsoft Docs
description: "Linux Vm'lerinizi Azure Yedekleme kullanılarak yedekleyerek koruyun."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a>Azure'daki Linux sanal makineleri yedekleyin

Düzenli aralıklarla yedekleme yaparak verilerinizi koruyabilirsiniz. Azure yedekleme coğrafi olarak yedekli kurtarma kasalarında depolanan kurtarma noktaları oluşturur. Bir kurtarma noktasından geri yüklediğinizde, geri yükleyebilirsiniz tüm VM ya da yalnızca belirli dosyaları hello. Bu makalede nasıl toorestore tek bir dosya tooa Linux VM çalışan nginx açıklanmaktadır. VM toouse zaten sahip değilseniz, birini oluşturabilirsiniz hello kullanarak [Linux quickstart](quick-create-cli.md). Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * VM bir yedeğini oluşturun
> * Günlük yedekleme zamanlaması
> * Bir dosyayı bir yedekten geri yükleyin



## <a name="backup-overview"></a>Backup’a genel bakış

Hello Azure Backup hizmeti yedekleme başlattığında hello yedekleme uzantısını tootake zaman içinde nokta anlık görüntü tetikler. Hello Azure Backup hizmeti kullanan hello _VMSnapshotLinux_ Linux uzantı. Merhaba VM çalışıyorsa hello uzantısı hello ilk VM yedekleme sırasında yüklenir. Merhaba VM çalışır durumda değilse, hello Backup hizmeti bir anlık görüntüsünü hello bu yana (hiçbir uygulama yazma VM durduruldu hello sırasında gerçekleşir) depolama temel alır.

Varsayılan olarak, Azure Backup dosya sisteminin tutarlı bir yedeklemenin Linux VM için alır ancak yapılandırılmış tootake olabilir [uygulama tutarlı yedekleme öncesi betik ve sonrası betik framework kullanarak](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). Hello Azure Backup hizmeti hello anlık görüntüsünü alır sonra hello aktarılan toohello kasası verilerdir. toomaximize verimliliği hello hizmeti tanımlar ve yalnızca hello hello önceki yedeklemeden bu yana değişmiş olan veri bloklarını aktarır.

Merhaba veri aktarımı tamamlandığında hello anlık görüntü kaldırılır ve bir kurtarma noktası oluşturulur.


## <a name="create-a-backup"></a>Bir yedekleme oluşturun
Bir basit zamanlanmış günlük yedekleme tooa kurtarma Hizmetleri kasası oluşturun. 

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba soldaki Hello menüde seçin **sanal makineleri**. 
3. Merhaba listeden VM tooback seçin.
4. Merhaba, hello VM dikey **ayarları** 'yi tıklatın **yedekleme**. Merhaba **yedeklemeyi etkinleştir** dikey pencere açılır.
5. İçinde **kurtarma Hizmetleri kasası**, tıklatın **Yeni Oluştur** hello ad hello yeni kasa belirtin. Yeni bir kasa aynı hello oluşturulan kaynak grubunu ve konumu hello sanal makine olarak.
6. Tıklatın **yedekleme İlkesi**. Bu örneğin hello Varsayılanları tutun ve **Tamam**.
7. Merhaba üzerinde **yedeklemeyi etkinleştir** dikey penceresinde tıklatın **yedeklemeyi etkinleştir**. Merhaba varsayılan zamanlamaya göre günlük yedekleme oluşturur.
10. toocreate bir ilk kurtarma noktasında hello **yedekleme** dikey penceresinde **Şimdi Yedekle**.
11. Merhaba üzerinde **Şimdi Yedekle** dikey penceresinde hello takvim simgesini tıklatın, hello Takvim denetimi tooselect hello bu kurtarma noktası korunur ve tıklatın son günü kullanmak **yedekleme**.
12. Merhaba, **yedekleme** dikey penceresinde, VM için tam kurtarma noktalarının sayısı hello görürsünüz.

    ![Kurtarma noktaları](./media/tutorial-backup-vms/backup-complete.png)

Merhaba ilk yedek yaklaşık 20 dakika sürer. Yedekleme tamamlandıktan sonra bu öğreticinin sonraki bölümü toohello devam edin.

## <a name="restore-a-file"></a>Bir dosya geri yükleme

Yanlışlıkla silme veya değişiklikleri tooa dosyasını, dosya kurtarma toorecover hello dosyasını yedekleme Kasası'nı kullanabilirsiniz. Dosya Kurtarma kullanan VM hello üzerinde çalışan bir komut yerel sürücü olarak toomount hello kurtarma noktası. Merhaba kurtarma noktasından dosya kopyalayabilir ve toohello VM geri için bu sürücüler için 12 saat bağlı kalır.  

Bu örnekte, nasıl toorecover hello varsayılan nginx web sayfası /var/www/html/index.nginx-debian.html gösterir. Merhaba ortak IP adresi bu örnekte bizim VM *13.69.75.209*. Başlangıç IP adresi vm kullanmanın bulabilirsiniz:

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. Yerel bilgisayarınızda, bir tarayıcı ve türü hello genel IP adresi VM toosee hello varsayılan nginx web sayfanızın açın.

    ![Varsayılan nginx web sayfası](./media/tutorial-backup-vms/nginx-working.png)

1. VM içine SSH.

    ```bash
    ssh 13.69.75.209
    ```
2. /Var/www/HTML/index.nginx-debian.HTML silin.

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. Yerel bilgisayarınızda CTRL tuşuna tarafından hello tarayıcıyı yenilemek + varsayılan nginx sayfa F5 toosee kaldırılmıştır.

    ![Varsayılan nginx web sayfası](./media/tutorial-backup-vms/nginx-broken.png)
    
1. Yerel bilgisayarınızda toohello içinde oturum [Azure portal](https://portal.azure.com/).
6. Merhaba soldaki Hello menüde seçin **sanal makineleri**. 
7. Merhaba listeden hello VM seçin.
8. Merhaba, hello VM dikey **ayarları** 'yi tıklatın **yedekleme**. Merhaba **yedekleme** dikey pencere açılır. 
9. Merhaba dikey penceresinde hello üstündeki Hello menüde seçin **dosya kurtarma**. Merhaba **dosya kurtarma** dikey pencere açılır.
10. İçinde **1. adım: kurtarma noktası seçin**, hello açılan listeden bir kurtarma noktası seçin.
11. İçinde **2. adım: betik toobrowse indirin ve dosyaları kurtarmak**, hello tıklatın **karşıdan yürütülebilir** düğmesi. Merhaba indirilen dosya tooyour yerel bilgisayara kaydedin.
7. Tıklatın **karşıdan yükleme komut dosyası** toodownload hello komut dosyası yerel olarak.
8. Aşağıdaki, değiştirerek bir Bash istemi hello açmak *Linux_myVM_05 05 2017.sh* yol ve dosya adı, indirdiğiniz hello komut ile Merhaba düzeltmek *azureuser* hello username hello VM için ve *13.69.75.209* hello ortak IP adresiyle VM.
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. Yerel bilgisayarınızda, bir SSH bağlantısı toohello VM açın.

    ```bash
    ssh 13.69.75.209
    ```
    
10. VM'nizi üzerinde eklemek izinleri toohello betiği yürütün.

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. VM'nizi üzerinde hello betik toomount hello kurtarma noktası bir dosya sistemi çalıştırın.

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. Hello hello bağlama noktası yolunu hello hello betik verir çıktı. Merhaba çıkış benzer toothis görünür:

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. Merhaba nginx varsayılan web sayfası, VM, kopyalama hello bağlama noktası geri toowhere hello dosyası silindi.

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. Yerel bilgisayarınızda bağlandığı hello tarayıcısı sekmesi açın hello VM hello nginx varsayılan sayfasını gösteren toohello IP adresidir. CTRL + F5'e basın. toorefresh hello tarayıcı sayfası. Bu hello görmelisiniz varsayılan sayfa yeniden çalışma.

    ![Varsayılan nginx web sayfası](./media/tutorial-backup-vms/nginx-working.png)

18. Yerel bilgisayarınızda toohello tarayıcı sekmesinde hello Azure portal için ve geri dönün **adım 3: hello diskleri kurtarma işleminden sonra çıkarın** hello tıklatın **çıkarın diskleri** düğmesi. Bu adım toodo unutursanız, hello bağlantı toohello mountpoint 12 saat sonra otomatik olarak kapat. Bu 12 saat sonra yeni bir komut dosyası toocreate yeni mountpoint toodownload gerekir.


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * VM bir yedeğini oluşturun
> * Günlük yedekleme zamanlaması
> * Bir dosyayı bir yedekten geri yükleyin

Sanal makineler izleme hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [Sanal makineleri izleme](tutorial-monitoring.md)


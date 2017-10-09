---
title: aaaBackup Azure Windows VM | Microsoft Docs
description: "Windows Vm'lerinizi Azure Yedekleme kullanılarak yedekleyerek koruyun."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a>Azure'da Windows sanal makineleri yedekleyin

Düzenli aralıklarla yedekleme yaparak verilerinizi koruyabilirsiniz. Azure yedekleme coğrafi olarak yedekli kurtarma kasalarında depolanan kurtarma noktaları oluşturur. Bir kurtarma noktasından geri yüklediğinizde, geri yükleyebilirsiniz tüm VM ya da yalnızca belirli dosyaları hello. Bu makalede, nasıl toorestore tek bir dosya tooa VM açıklanmaktadır Windows Server ve IIS çalıştırıyor. VM toouse zaten sahip değilseniz, birini oluşturabilirsiniz hello kullanarak [Windows Hızlı Başlangıç](quick-create-portal.md). Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * VM bir yedeğini oluşturun
> * Günlük yedekleme zamanlaması
> * Bir dosyayı bir yedekten geri yükleyin




## <a name="backup-overview"></a>Backup’a genel bakış

Hello Azure Backup hizmeti yedekleme işini başlattığında hello yedekleme uzantısını tootake zaman içinde nokta anlık görüntü tetikler. Hello Azure Backup hizmeti kullanan hello _VMSnapshot_ uzantısı. Merhaba VM çalışıyorsa hello uzantısı hello ilk VM yedekleme sırasında yüklenir. Merhaba VM çalışır durumda değilse, hello Backup hizmeti bir anlık görüntüsünü hello bu yana (hiçbir uygulama yazma VM durduruldu hello sırasında gerçekleşir) depolama temel alır.

Windows VM görüntüsünü alırken, hello Backup hizmeti ile Merhaba Birim Gölge Kopyası Hizmeti (VSS) tooget tutarlı bir anlık görüntü hello sanal makinenin disklerinin düzenler. Hello Azure Backup hizmeti hello anlık görüntüsünü alır sonra hello aktarılan toohello kasası verilerdir. toomaximize verimliliği hello hizmeti tanımlar ve yalnızca hello hello önceki yedeklemeden bu yana değişmiş olan veri bloklarını aktarır.

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

## <a name="recover-a-file"></a>Bir dosya kurtarma

Yanlışlıkla silme veya değişiklikleri tooa dosyasını, dosya kurtarma toorecover hello dosyasını yedekleme Kasası'nı kullanabilirsiniz. Dosya Kurtarma kullanan VM hello üzerinde çalışan bir komut yerel sürücü olarak toomount hello kurtarma noktası. Merhaba kurtarma noktasından dosya kopyalayabilir ve toohello VM geri için bu sürücüler için 12 saat bağlı kalır.  

Bu örnekte, nasıl toorecover hello hello varsayılan web sayfasında IIS için kullanılan görüntü dosyası gösterir. 

1. Bir tarayıcı açın ve hello VM tooshow hello varsayılan IIS sayfası toohello IP adresine bağlanın.

    ![Varsayılan IIS web sayfası](./media/tutorial-backup-vms/iis-working.png)

2. Toohello VM bağlayın.
3. Hello VM, açık **dosya Gezgini** too\inetpub\wwwroot gidin ve hello dosya silme **iisstart.png**.
4. Yerel bilgisayarınızda hello varsayılan IIS sayfasında görüntü hello yenileme hello tarayıcı toosee kaldırılmıştır.

    ![Varsayılan IIS web sayfası](./media/tutorial-backup-vms/iis-broken.png)

5. Yerel bilgisayarınızda bir yeni sekmesine gidin hello hello açın ve [Azure portal](https://portal.azure.com).
6. Merhaba soldaki Hello menüde seçin **sanal makineleri** ve select hello VM form hello listesi.
8. Merhaba, hello VM dikey **ayarları** 'yi tıklatın **yedekleme**. Merhaba **yedekleme** dikey pencere açılır. 
9. Merhaba dikey penceresinde hello üstündeki Hello menüde seçin **dosya kurtarma**. Merhaba **dosya kurtarma** dikey pencere açılır.
10. İçinde **1. adım: kurtarma noktası seçin**, hello açılan listeden bir kurtarma noktası seçin.
11. İçinde **2. adım: betik toobrowse indirin ve dosyaları kurtarmak**, hello tıklatın **karşıdan yürütülebilir** düğmesi. Merhaba dosya tooyour kaydetmek **indirmeleri** klasör.
12. Yerel bilgisayarınızda açın **dosya Gezgini** tooyour giderek **indirmeleri** klasörü ve kopyalama hello indirilen .exe dosyası. Merhaba filename VM adıyla önek alacaktır. 
13. VM'nizi (üzerinden RDP bağlantısı hello) üzerinde hello .exe dosyası toohello VM masaüstünün yapıştırın. 
14. Vm'nizin toohello Masaüstü gidin ve üzerinde hello .exe dosyasını çift tıklatın. Bu, bir komut istemi başlatın ve sonra erişebileceğiniz bir dosya paylaşımı bağlama hello kurtarma noktası. Bu tamamlandığında hello paylaşımı oluşturma, yazın **q** tooclose hello komut istemi.
15. VM'nizi üzerinde açık **dosya Gezgini** ve hello dosya paylaşımı için kullanılan toohello sürücü harfi gidin.
16. Too\inetpub\wwwroot ve kopyalama gidin **iisstart.png** hello dosyasından paylaşmak ve \inetpub\wwwroot yapıştırabilirsiniz. Örneğin, F:\inetpub\wwwroot\iisstart.png kopyalayın ve c:\inetpub\wwwroot toorecover hello dosyaya yapıştırın.
17. Yerel bilgisayarınızda bağlandığı hello tarayıcısı sekmesi açın hello VM hello IIS varsayılan sayfasını gösteren toohello IP adresidir. CTRL + F5'e basın. toorefresh hello tarayıcı sayfası. Bu hello görmelisiniz görüntüsü geri yüklendi.
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










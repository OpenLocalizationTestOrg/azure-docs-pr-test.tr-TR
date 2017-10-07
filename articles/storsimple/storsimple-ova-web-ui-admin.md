---
title: "aaaStorSimple sanal dizinin web kullanıcı Arabirimi Yönetim | Microsoft Docs"
description: "Merhaba StorSimple sanal dizinin web kullanıcı Arabirimi nasıl tooperform temel aygıt yönetim görevleri açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a>StorSimple sanal dizinizi Hello Web kullanıcı arabirimini tooadminister kullanın
![Kurulum işlem akışı](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a>Genel Bakış
Bu makalede Hello öğreticileri toohello Microsoft Azure StorSimple sanal dizinin (olarak da bilinen hello StorSimple şirket içi sanal cihaz) çalışan Mart 2016 genel kullanılabilirlik (GA) sürümü geçerli. Bu makalede hello karmaşık iş akışları ve StorSimple sanal dizinin hello üzerinde gerçekleştirilen yönetim görevlerini bazıları açıklanmaktadır. Yönetebileceğiniz StorSimple sanal hello StorSimple Yöneticisi hizmeti kullanıcı Arabirimi (başvurulan tooas hello portal UI) kullanarak dizi hello ve hello cihaz için yerel web kullanıcı Arabirimi hello. Bu makalede, hello web kullanıcı arabirimini kullanarak gerçekleştirebilirsiniz hello görevlerde odaklanır.

Bu makalede öğreticileri aşağıdaki hello içerir:

* Merhaba hizmet verileri şifreleme anahtarı alma
* Web kullanıcı Arabirimi Kurulum hatalarında sorun giderme
* Bir günlük paketi oluştur
* Kapatıldı veya aygıtınızı yeniden başlatın

## <a name="get-hello-service-data-encryption-key"></a>Merhaba hizmet verileri şifreleme anahtarı alma
StorSimple Yöneticisi hizmeti hello ile ilk Cihazınızı kaydederken bir hizmet verileri şifreleme anahtarı oluşturulur. Bu anahtarı ise hello hizmet kayıt anahtarı tooregister ek aygıtlarla hello StorSimple Yöneticisi hizmeti ile gereklidir.

Hizmet verileri şifreleme anahtarı yanlış ve tooretrieve gerekir, hello aşağıdakileri gerçekleştirmek hello yerel web kullanıcı Arabirimi hello cihazın adımlarda hizmetiniz ile kayıtlı.

#### <a name="tooget-hello-service-data-encryption-key"></a>tooget hello hizmet verileri şifreleme anahtarı
1. Toohello yerel web kullanıcı Arabirimi bağlayın. Çok Git**yapılandırma** > **bulut ayarları**.
2. Merhaba sayfasının Hello altında tıklatın **Get hizmet verileri şifreleme anahtarı**. Bir anahtarı görüntülenir. Kopyalayın ve bu anahtar kaydedin.
   
    ![Hizmet verileri şifreleme anahtarı 1 alma](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a>Web kullanıcı Arabirimi Kurulum hatalarında sorun giderme
Bazı durumlarda hello aygıtı hello yerel web kullanıcı Arabirimi aracılığıyla yapılandırdığınızda hatalarla karşılaşırsanız çalıştırabilirsiniz. toodiagnose ve bu tür hatalarında sorun giderme, hello tanılama testleri çalıştırabilirsiniz.

#### <a name="toorun-hello-diagnostic-tests"></a>toorun hello tanılama testleri
1. Merhaba yerel web kullanıcı Arabirimi, çok Git**sorun giderme** > **tanılama testleri**.
   
    ![Tanılama'yı 1 çalıştırın](./media/storsimple-ova-web-ui-admin/image29.png)
2. Merhaba sayfasının Hello altında tıklatın **tanılama Testleri Çalıştır**. Bu ağ, aygıt, web proxy, saati veya Bulut ayarları ile ilgili tüm olası sorunları testleri toodiagnose başlatır. Merhaba aygıt testleri çalıştırma bildirilir.
3. Merhaba testleri tamamladıktan sonra hello sonuçları görüntülenir. Merhaba aşağıdaki örnek tanılama testleri hello sonuçlarını gösterir. Bu aygıtta Hello web proxy ayarları yapılandırılmadı ve bu nedenle, hello web proxy testi değil çalıştırıldığı unutmayın. Tüm ağ ayarlarını, DNS sunucusu için diğer testleri hello ve saat ayarları başarılı oldu.
   
    ![Tanılama 2 çalıştırma](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a>Bir günlük paketi oluştur
Bir günlük paketi Microsoft Support cihaz sorunları gidermenize yardımcı olabilecek tüm hello ilgili günlüklerini oluşur. Bu sürümde, bir günlük paket hello yerel web kullanıcı Arabirimi oluşturulabilir.

#### <a name="toogenerate-hello-log-package"></a>toogenerate hello günlük paketi
1. Merhaba yerel web kullanıcı Arabirimi, çok Git**sorun giderme** > **sistem günlüklerini**.
   
    ![Günlük Paketi 1 oluştur](./media/storsimple-ova-web-ui-admin/image31.png)
2. Merhaba sayfasının Hello altında tıklatın **günlük Paket Oluştur**. Merhaba sistem günlüklerini paketi oluşturulacak. Bu işlem birkaç dakika sürebilir.
   
    ![2 günlük paketi oluştur](./media/storsimple-ova-web-ui-admin/image32.png)
   
    Hello paketi başarıyla oluşturulduktan sonra hello sayfa tooindicate hello saat ve tarih hello paketinin oluşturulduğu güncelleştirilecektir bildirilir.
   
    ![3 günlük paketi oluştur](./media/storsimple-ova-web-ui-admin/image33.png)
3. Tıklatın **yükleme günlük paketini**. Sıkıştırılmış paketi sisteminizde indirilir.
   
    ![Günlük Paketi 4 oluştur](./media/storsimple-ova-web-ui-admin/image34.png)
4. Merhaba indirilen günlük paketin sıkıştırmasını açın ve hello sistem günlük dosyalarını görüntüleyin.

## <a name="shut-down-and-restart-your-device"></a>Kapatılır ve aygıtınızı yeniden başlatın
Kapatıldı veya hello yerel web kullanıcı arabirimini kullanarak sanal Cihazınızı yeniden başlatın. Yeniden başlatma, hello birimler veya paylaşımlar çevrimdışı hello konakta alın ve cihaz hello önce öneririz. Bu veri bozulması olasılığını en aza indirgenecektir. 

#### <a name="tooshut-down-your-virtual-device"></a>Sanal cihazınız aşağı tooshut
1. Merhaba yerel web kullanıcı Arabirimi, çok Git**Bakım** > **güç ayarları**.
2. Merhaba sayfasının Hello altında tıklatın **kapatma**.
   
    ![cihaz kapatma 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. Bir kapanma hello cihazın kapalı kalma süresi ile elde edilen etmekte olan tüm g/ç kesintiye uğrar belirten bir uyarı görüntülenir. Merhaba onay simgesine tıklayın ![onay simgesi](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![cihaz kapatma uyarı](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Bu hello kapatma başlatılan bildirilir.
   
    ![cihaz kapatma başlatıldı](./media/storsimple-ova-web-ui-admin/image38.png)
   
    Merhaba cihaz şimdi kapanacak. Cihazınızı toostart istiyorsanız, Hyper-V Yöneticisi'ni hello aracılığıyla toodo gerekir.

#### <a name="toorestart-your-virtual-device"></a>toorestart sanal Cihazınızı
1. Merhaba yerel web kullanıcı Arabirimi, çok Git**Bakım** > **güç ayarları**.
2. Merhaba sayfasının Hello altında tıklatın **yeniden**.
   
    ![Aygıt yeniden başlatma](./media/storsimple-ova-web-ui-admin/image36.png)
3. Bu yeniden başlatmayı hello aygıt kapalı kalma süresi ile elde edilen etmekte olan tüm IOs kesintiye uğrar bildiren bir uyarı görüntülenir. Merhaba onay simgesine tıklayın ![onay simgesi](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![Uyarı yeniden başlatın](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Bu hello yeniden başlatma bildirilir.
   
    ![başlatılan yeniden başlatma](./media/storsimple-ova-web-ui-admin/image39.png)
   
    Merhaba yeniden başlatma işlemi devam ederken, hello bağlantı toohello UI kaybedersiniz. Merhaba kullanıcı arabirimini düzenli aralıklarla yenileyerek hello yeniden izleyebilirsiniz. Alternatif olarak, Hyper-V Yöneticisi'ni hello aracılığıyla hello aygıt yeniden başlatma durumunu izleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Nasıl çok öğrenin[kullanım Cihazınızı StorSimple Yöneticisi hizmet toomanage hello](storsimple-virtual-array-manager-service-administration.md).


---
title: "aaaManage aygıtlar ile StorSimple Snapshot Manager | Microsoft Docs"
description: "Toouse StorSimple Snapshot Manager MMC ek bileşenini tooconnect hello ve StorSimple cihazları yönetmenize nasıl açıklanmaktadır."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a>StorSimple Snapshot Manager tooconnect kullanma ve StorSimple cihazları yönetme
## <a name="overview"></a>Genel Bakış
Merhaba StorSimple Snapshot Manager düğümlerini kullanabilirsiniz **kapsam** bölmesinde tooverify StorSimple cihaz verileri içe ve bağlı depolama cihazları yenileyin. Ayrıca, hello tıklattığınızda **aygıtları** düğümü, bağlı cihazlarınız ve ilgili durum bilgileri hello listesini görebilir **sonuçları** bölmesi.

![Bağlı aygıtlar](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

**Şekil 1: Cihaz StorSimple Snapshot Manager bağlı** 

Bağlı olarak, **Görünüm** seçimleri, hello **sonuçları** bölmesinde, her cihazı hakkında bilgileri aşağıdaki hello gösterilir. (Bir görünüm yapılandırma hakkında daha fazla bilgi için çok Git[Görünüm menüsünde](storsimple-use-snapshot-manager.md#view-menu).

| Sonuçları sütun | Açıklama |
|:--- |:--- |
| Ad |Merhaba Klasik Azure portalı yapılandırıldığı şekilde hello aygıtın Hello adı |
| modeli |Merhaba modeli hello aygıt sayısı |
| Sürüm |Merhaba cihazda yüklü hello yazılımın Hello sürümü |
| Durum |Merhaba cihaz hazır olup |
| Son eşitlendi |Tarih ve saat hello aygıt en son ne zaman eşitlendiği |
| Seri No |Merhaba aygıtın Hello seri numarası |

Merhaba sağ tıklattığınızda, **aygıtları** hello düğümünde **kapsam** bölmesinde, aşağıdaki eylemler hello seçebilirsiniz:

* Ekleme veya bir aygıt değiştirme
* Bir aygıtı bağlayın ve içeri aktarmalar doğrulayın
* Bağlı aygıtlar Yenile

Merhaba tıklatırsanız **aygıtları** düğümünü ve ardından sağ tıklayarak bir aygıt adı hello **sonuçları** bölmesinde, aşağıdaki eylemler hello seçebilirsiniz:

* Bir cihaz kimlik doğrulaması
* Cihaz ayrıntıları görüntüle
* Bir cihaz yenileme
* Cihaz yapılandırmasını Sil
* Aygıt parola değiştirme

> [!NOTE]
> Tüm bu eylemleri de hello kullanılabilir **Eylemler** bölmesi.


Bu öğretici açıklar nasıl toouse StorSimple Snapshot Manager tooconnect ve cihazları yönetmek ve hello aşağıdaki görevleri gerçekleştirin:

* Ekleme veya bir aygıt değiştirme
* Bir aygıtı bağlayın ve içeri aktarmalar doğrulayın
* Bağlı aygıtlar Yenile
* Bir cihaz kimlik doğrulaması
* Cihaz ayrıntıları görüntüle
* Tek bir cihaza Yenile
* Cihaz yapılandırmasını Sil
* Süresi dolan cihaz parolasını değiştirme
* Başarısız aygıt değiştirin

> [!NOTE]
> Merhaba StorSimple Snapshot Manager arabirimini kullanma hakkında genel bilgi için çok Git[StorSimple Snapshot Manager kullanıcı arabirimini](storsimple-use-snapshot-manager.md).


## <a name="add-or-replace-a-device"></a>Ekleme veya bir aygıt değiştirme
Aşağıdaki yordam tooadd hello kullanın veya bir StorSimple cihazı değiştirin.

#### <a name="tooadd-or-replace-a-device"></a>tooadd veya bir aygıt Değiştir
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesi, sağ hello **aygıtları** düğümünü ve ardından **bir aygıt yapılandırma**. Merhaba **bir aygıt yapılandırma** iletişim kutusu görüntülenir.
   
    ![Bir StorSimple cihazını Yapılandır](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. Merhaba, **aygıt** açılan kutusu, select hello IP adresini hello aygıt veya sanal aygıt. 
4. Merhaba, **parola** metin kutusu, Klasik Azure portalı hello hello aygıt için oluşturulan türü hello StorSimple Snapshot Manager parolası. **Tamam** düğmesine tıklayın. StorSimple Snapshot Manager tanımladığınız hello aygıt için arar. 
   
   * Merhaba aygıt varsa, StorSimple Snapshot Manager bağlantı ekler.
   * Merhaba aygıt herhangi bir nedenle kullanılamıyorsa, StorSimple Snapshot Manager bir hata iletisi döndürür. Tıklatın **Tamam** tooclose hello hata iletisi ve ardından **iptal** tooclose hello **bir aygıt yapılandırma** iletişim kutusu.

## <a name="connect-a-device-and-verify-imports"></a>Bir aygıtı bağlayın ve içeri aktarmalar doğrulayın
Yordam tooconnect StorSimple cihazını izleyen hello kullanın ve yedeklemeleri ilişkilendirdiğiniz varolan birim gruplarda alınır doğrulayın.

#### <a name="tooconnect-a-device-and-verify-imports"></a>bir aygıt tooconnect ve içeri aktarmalar doğrulayın
1. tooconnect aygıt tooStorSimple anlık görüntü Yöneticisi'ni Ekle hello yönergeleri izleyin veya bir aygıt değiştirin. Tooa Aygıt bağlandığında, StorSimple Snapshot Manager şu şekilde yanıt verir:
   
   * Merhaba aygıt herhangi bir nedenle kullanılamıyorsa, StorSimple Snapshot Manager bir hata iletisi döndürür. 
   
   * Merhaba aygıt varsa, StorSimple Snapshot Manager bağlantı ekler. Merhaba cihaz seçtiğinizde, hello göründüğü **sonuçları** bölmesinde ve hello durumu alanı gösterir, hello aygıt **kullanılabilir**. StorSimple Snapshot Manager Hello birim grupları yedeklemeleri ilişkili sahip olması koşuluyla hello aygıt için yapılandırılmış herhangi bir birim grubu içeri aktarır. Yedekleme ilkeleri içeri aktarılmadı. İlişkili yedeklemelerinizi olmayan birim grupları içeri aktarılmadı.
2. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
3. Sağ hello üst düğümü hello **kapsam** bölmesi ve ardından **içeri aktarmalar ekranını Değiştir**.
   
    ![İçeri aktarmalar ekranını Değiştir'i seçin](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. Merhaba **içeri aktarmalar ekranını Değiştir** iletişim kutusu görüntülenirse, hello hello durumunu gösteren içe birim grupları ve yedekler. **Tamam** düğmesine tıklayın.

Merhaba birim grupları ve yedeklemeleri başarıyla içeri aktarıldı sonra bunları, yalnızca StorSimple Snapshot Manager toomanage kullanabilirsiniz birim grupları ve oluşturulan ve StorSimple Snapshot Manager ile yapılandırılmış yedeklemeleri yönetebilir gibi. 

## <a name="refresh-connected-devices"></a>Bağlı aygıtlar Yenile
Aşağıdaki yordam toosynchronize bağlı hello StorSimple cihazlar ile StorSimple Snapshot Manager hello kullanın.

#### <a name="toorefresh-connected-devices"></a>toorefresh bağlı aygıtları
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde, sağ tıklatın **aygıtları**ve ardından **yenileme aygıtları**. Merhaba birim grupları ve tüm sınıflarla da içeren yedeklemeler görüntüleyebilmek bu hello bağlı aygıtları StorSimple Snapshot Manager ile eşitler. 
   
    ![Merhaba StorSimple cihazlarını Yenile](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

Merhaba **yenileme aygıtları** eylem bağlı aygıtlardan yeni birim grupları ve tüm ilişkili yedeklemelerinin alır. Merhaba aksine **birimleri yeniden tara** eylemin hello için kullanılabilir **birimleri** düğümü, **yenileme aygıtları** hello yedek kayıt defteri geri yüklemeyin.

## <a name="authenticate-a-device"></a>Bir cihaz kimlik doğrulaması
Aşağıdaki yordam tooauthenticate StorSimple cihazı ile StorSimple Snapshot Manager hello kullanın.

#### <a name="tooauthenticate-a-device"></a>tooauthenticate bir aygıtı
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde tıklatın **aygıtları**.
3. Merhaba, **sonuçları** bölmesinde hello aygıt hello adına sağ tıklayın ve ardından **kimlik doğrulama**.
4. Merhaba **kimlik doğrulama** iletişim kutusu görüntülenir. Merhaba cihaz parolasını yazın ve ardından **Tamam**.
   
    ![Kimlik doğrulaması iletişim kutusu](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a>Cihaz ayrıntıları görüntüle
Aşağıdaki yordam tooview hello ayrıntılara StorSimple cihazı hello kullanın ve gerekirse, hello cihazı ile StorSimple Snapshot Manager yeniden eşitleyin.

#### <a name="tooview-and-resynchronize-device-details"></a>tooview ve yeniden eşzamanlılaştırabilir cihaz ayrıntıları
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde tıklatın **aygıtları**.
3. Merhaba, **sonuçları** bölmesinde hello aygıt hello adına sağ tıklayın ve ardından **ayrıntıları**.

4 hello **cihaz ayrıntıları** iletişim kutusu görüntülenir. Bu kutu gösterir hello adı, model, sürüm, seri numarası, durum, hedef iSCSI tam adını (IQN) ve son eşitleme tarihi ve saati.

* Tıklatın **yeniden eşitleme** toosynchronize hello aygıt.
* Tıklatın **Tamam** veya **iptal** tooclose hello iletişim kutusu.
  
  ![Cihaz ayrıntıları](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a>Tek bir cihaza Yenile
Aşağıdaki yordam tooresynchronize tek tek bir StorSimple cihazı ile StorSimple Snapshot Manager hello kullanın.

#### <a name="toorefresh-a-device"></a>toorefresh bir aygıtı
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın. 
2. Merhaba, **kapsam** bölmesinde tıklatın **aygıtları**. 
3. Merhaba, **sonuçları** bölmesinde hello aygıt hello adına sağ tıklayın ve ardından **yenileme aygıt**. Bu hello cihaz StorSimple Snapshot Manager ile eşitler.

## <a name="delete-a-device-configuration"></a>Cihaz yapılandırmasını Sil
StorSimple anlık görüntü Yöneticisi'nden yordamı toodelete tek tek bir StorSimple cihaz yapılandırma aşağıdaki hello kullanın.

#### <a name="toodelete-a-device-configuration"></a>toodelete aygıt yapılandırması
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde tıklatın **aygıtları**. 
3. Merhaba, **sonuçları** bölmesinde hello aygıt hello adına sağ tıklayın ve ardından **silmek**. 
4. iletiden hello görüntülenir. Tıklatın **Evet** toodelete hello yapılandırma veya tıklatın **Hayır** toocancel hello silme.
   
    ![Cihaz yapılandırmasını Sil](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a>Süresi dolan cihaz parolasını değiştirme
Parola tooauthenticate StorSimple cihazı ile StorSimple Snapshot Manager girmeniz gerekir. Merhaba Windows PowerShell arabirimi tooset hello aygıt yukarı kullandığınızda bu parola yapılandırın. Ancak, hello parola süresinin dolmasını sağlayabilir. Bu durumda, hello Azure Klasik portalı toochange hello parola kullanabilirsiniz. Ardından, Hello parola süresi dolmadan önce StorSimple anlık görüntü Yöneticisi'nde hello aygıt yapılandırıldığı StorSimple anlık görüntü Yöneticisi'nde hello aygıt yeniden doğrulaması gerekir.

#### <a name="toochange-hello-expired-password"></a>toochange hello parolasının süresi dolmuş
1. Hello Klasik Azure portalı, hello StorSimple Yöneticisi hizmetini başlatın.
2. Tıklatın **aygıtları** > **yapılandırma** hello cihaz için.
3. Toohello StorSimple Snapshot Manager bölümüne kaydırın. 14-15 karakter olan bir parola girin. Merhaba parola büyük harf, küçük harfler, sayısal ve özel karakterlerin bir karışımı içerdiğinden emin olun.
4. Merhaba parola tooconfirm yeniden girin.
5. Tıklatın **kaydetmek** hello sayfanın hello sonundaki.

#### <a name="toore-authenticate-hello-device"></a>toore-hello cihaz kimlik doğrulaması
1. StorSimple anlık görüntü Yöneticisi'ni başlatın.
2. Merhaba, **kapsam** bölmesinde tıklatın **aygıtları**. Yapılandırılmış aygıtların listesini hello görünür **sonuçları** bölmesi.
3. Merhaba aygıt, sağ tıklatın ve ardından seçin **kimlik doğrulama**.
4. Merhaba, **kimlik doğrulama** penceresinde hello yeni bir parola girin.
5. Merhaba aygıt, sağ tıklatın ve seçin seçin **yenileme aygıt**. Bu hello cihaz StorSimple Snapshot Manager ile eşitler.

## <a name="replace-a-failed-device"></a>Başarısız aygıt değiştirin
StorSimple cihazı başarısız olur ve bekleme (yük devretme) aygıtıyla adımları tooconnect aşağıdaki kullanım hello yerine toohello yeni cihaz ve görünüm ilişkili yedeklemelerinizi hello.

#### <a name="tooconnect-tooa-new-device-after-failover"></a>Yük devretme sonrasında tooconnect tooa yeni cihaz
1. Merhaba iSCSI bağlantı toohello yeni cihaz yeniden yapılandırın. Yönergeler için çok gidin "Adım 7: bağlama, başlatma ve format bir birim" olarak [şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md).

> [!NOTE]
> Eski bir hello aynı IP adresine sahip Hello yeni StorSimple cihazı hello olursa, mümkün tooconnect hello eski yapılandırma olabilir.


1. Merhaba Microsoft StorSimple Yöneticisi Hizmeti Durdur:
   
   1. Sunucu Yöneticisi'ni başlatın.
   2. Merhaba üzerinde Sunucu Yöneticisi Panosu hello üzerinde **Araçları** menüsünde, select **Hizmetleri**.
   3. Merhaba üzerinde **Hizmetleri** penceresinde, select hello **Microsoft StorSimple Yöneticisi hizmeti**.
   4. Hello bölmesini altında sağ **Microsoft StorSimple Yöneticisi hizmeti**, tıklatın **hello hizmetini durdurun**.
2. Merhaba yapılandırma bilgilerini ilgili toohello eski aygıt kaldırın:
   
   1. Dosya Gezgini'nde tooC:\ProgramData\Microsoft\StorSimple\BACatalog göz atın.
   2. Merhaba BACatalog klasöründeki Hello dosyaları silin.
3. Merhaba Microsoft StorSimple Yöneticisi hizmeti yeniden başlatın:
   
   1. Merhaba üzerinde Sunucu Yöneticisi Panosu hello üzerinde **Araçları** menüsünde, select **Hizmetleri**.
   2. Merhaba üzerinde **Hizmetleri** penceresinde, select hello **Microsoft StorSimple Yöneticisi hizmeti**.
   3. Hello bölmesini altında sağ **Microsoft StorSimple Yöneticisi hizmeti**, tıklatın **hello hizmetini yeniden başlatın**.
4. StorSimple anlık görüntü Yöneticisi'ni başlatın.
5. tooconfigure hello yeni StorSimple cihazı, tam hello adımları 2. adım: bir StorSimple cihazı bağlanmak [dağıtmak StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).
6. Sağ hello en üst düzey düğümünde hello **kapsam** bölmesinde (Merhaba örnekte StorSimple Snapshot Manager) ve ardından **içeri aktarmalar ekranını Değiştir**. 
7. Birim grupları hello aktarılması ve yedeklemeleri StorSimple anlık görüntü Yöneticisi'nde göründüğünden bir ileti görüntülenir. **Tamam** düğmesine tıklayın.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[StorSimple Snapshot Manager tooadminister StorSimple çözümünüzün kullanmak](storsimple-snapshot-manager-admin.md).
* Nasıl çok öğrenin[StorSimple Snapshot Manager tooview kullanın ve birimleri yönetme](storsimple-snapshot-manager-manage-volumes.md).


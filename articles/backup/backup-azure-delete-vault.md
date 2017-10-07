---
title: " Azure kurtarma Hizmetleri kasasını Sil | Microsoft Docs "
description: "Nasıl toodelete bir Azure yedekleme ve kurtarma Hizmetleri kasası. Bir yedekleme kasası, bir Azure bulut kasası ya da Azure recovery kasası çağrılabilir. Merhaba Klasik portalında veya Azure portalında bir yedekleme kasası silinemiyor zaman sorunlarını giderme."
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: 9047f50f4b2c991fbf2454ddcad08073ec7cd975
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasasını silme
Hello Azure Backup hizmeti kasalarını - hello yedekleme kasası ve hello kurtarma Hizmetleri kasası iki tür vardır. Merhaba yedekleme kasası ilk geldi. Ardından Kurtarma Hizmetleri kasası hello toosupport genişletilmiş hello Resource Manager dağıtımları geldi. Genişletilmiş özellikler ve bir yedekleme veya kurtarma Hizmetleri kasası silme hello kasasında depolanan gerekir hello bilgi bağımlılıkları nedeniyle Hello kafa karıştırıcı olabilir. Bu makalede nasıl toodelete hello hello Klasik portal ve hello Azure portal kasaları açıklanmaktadır.  

| **Dağıtım türü** | **Portal** | **Kasa adı** |
| --- | --- | --- |
| Klasik |Klasik |Yedekleme kasası |
| Resource Manager |Azure |Kurtarma Hizmetleri kasası |

> [!NOTE]
> Yedekleme kasaları, Resource Manager ile dağıtılan çözümleri koruyamaz. Ancak, bir kurtarma Hizmetleri kasası kullanabilirsiniz tooprotect classically dağıtılan sunucularını ve Vm'leri.  
>

> [!IMPORTANT]
> Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> **15 Ekim 2017**, artık mümkün toouse PowerShell toocreate yedekleme kasaları olacaktır. <br/> **1 Kasım 2017'den itibaren**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
>

Bu makalede, kullanırız hello terimi, kasa, toorefer toohello genel form hello yedekleme kasası ya da kurtarma Hizmetleri kasası. Merhaba kasalarını arasında gerekli toodistinguish olduğunda hello resmi adı, yedekleme kasası ya da kurtarma Hizmetleri kasası kullanın.

## <a name="deleting-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası silme
Kurtarma Hizmetleri kasası silinmesi olduğundan, bir tek adımlı işlem - *hello kasası herhangi bir kaynağa içermiyor sağlanan*. Kurtarma Hizmetleri kasası silmeden önce kaldırın veya tüm kaynakları hello kasasında silmeniz gerekir. Toodelete kaynakları içeren bir kasa çalışırsanız, görüntü aşağıdaki hello gibi bir hata alıyorsunuz:

![Kasa silme hatası](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

Merhaba kasası hello kaynaklardan temizlediniz kadar tıklatarak **yeniden deneme** üretir hello aynı hata. Bu hata iletisini takılmış tıklatmak **iptal** ve kullanım hello aşağıdaki adımları hello kasadaki toodelete hello kaynakları.

### <a name="removing-hello-items-from-a-vault-protecting-a-vm"></a>Bir VM koruma kasadan Hello öğeleri kaldırma
Merhaba kurtarma Hizmetleri kasası açmak zaten varsa, toohello ikinci adımı atlayın.

1. Hello Azure portalını açın ve Pano hello toodelete istediğiniz hello kasası açın.

   Ürününe sahip değilseniz, Kurtarma Hizmetleri kasası hello toohello panoyu hello Hub menüsünde sabitlenmiş, tıklatın **daha Hizmetleri** ve kaynakları hello listesinde yazın **kurtarma Hizmetleri**. Yazmaya başladığınızda liste filtreleri, girişinize göre hello. Tıklatın **kurtarma Hizmetleri kasaları**.

   ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   Merhaba kurtarma Hizmetleri kasalarının listesi görüntülenir. Merhaba listeden toodelete istediğiniz hello kasayı seçin.

   ![Kasa listesinden seçin](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. Hello görünümü, arama sırasında hello kasa **Essentials** bölmesi. toodelete bir kasa korumalı öğeler olamaz. Bir sayı ya da altında sıfır dışındaki görürseniz **yedekleme öğeleri** veya **yönetim sunucularını yedekleme**, hello kasası silmeden önce bu öğeleri kaldırmanız gerekir.

    ![Korumalı öğeler için Essentials bölmesi bakın](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    VM'ler ve dosyaların/klasörlerin yedekleme öğeleri olarak kabul edilir ve hello listelenen **yedekleme öğeleri** hello Essentials bölmesinin alanını. Bir DPM sunucusu hello listelenen **Yedekleme Yönetimi Sunucusu** hello Essentials bölmesinin alanını. **Öğeleri çoğaltılan** toohello Azure Site Recovery hizmeti ilgilidir.
3. Merhaba kaldırma toobegin hello kasasından hello kasasında hello öğelerini bulmak korunan öğeleri. Merhaba kasa panosunda tıklatın **ayarları**ve ardından **yedekleme öğeleri** tooopen o dikey.

    ![Kasa listesinden seçin](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    Merhaba **yedekleme öğeleri** dikey penceresinde hello öğesi türü üzerinde temelinde ayrı listeler sahiptir: Azure sanal makine ya da dosya klasörleri (görüntü bakın). gösterilen hello varsayılan öğesi türü Azure sanal makineleri listesidir. tooview hello dosya klasörleri öğeleri hello kasasında, select listesi **dosya klasörleri** hello açılan menüsünden.
4. Bir VM koruma hello kasadan bir öğesini silmeden önce hello öğesi'nin yedekleme işini durdurmak ve hello kurtarma noktası verilerini silmeniz gerekir. Merhaba kasadaki her öğe için şu adımları izleyin:

    a. Merhaba üzerinde **yedekleme öğeleri** dikey penceresinde sağ hello öğesi, hello bağlam menüsünden seçip **Dur yedekleme**.

    ![Merhaba yedekleme işini durdurma](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    Merhaba Durdur yedekleme dikey pencere açılır.

    b. Hello üzerinde **durdurmak yedekleme** dikey penceresinde, hello **bir seçenek belirleyin** menüsünde, select **yedekleme verilerini Sil** > hello öğesinin tür hello adı > tıklatıp **Durdur Yedekleme**.

    Merhaba öğesinin toodelete istediğiniz tooverify tür hello adı. Merhaba **durdurmak yedekleme** hello öğesi doğrulayın sonra düğmesini etkinleştirir. Merhaba iletişim kutusu tootype hello hello yedekleme öğesinin adını görmüyorsanız hello Seçtiğiniz **yedekleme verileri koru** seçeneği.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    İsteğe bağlı olarak, bir nedeni neden, hello verileri siliniyor ve açıklamaları ekleme sağlayabilir. Tıklattıktan sonra **durdurmak yedekleme**, toodelete hello kasası denemeden önce hello silme işi toocomplete izin verin. İş hello tooverify tamamlandı, hello Azure iletilerini denetleyin ![yedekleme verilerini silmek](./media/backup-azure-delete-vault/messages.png). <br/>
    Merhaba işi tamamlandıktan sonra hello yedekleme işlemi durduruldu ve bu öğe için hello yedekleme verileri silindi bildiren bir ileti alırsınız.

    c. Öğeyi hello listesinde, hello sildikten sonra **yedekleme öğeleri** menüsünde tıklatın **yenileme** öğeleri hello kasasında kalan toosee hello.

      ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/empty-items-list.png)

      Merhaba listede öğe yok olduğunda toohello kaydırma **Essentials** hello yedekleme kasası dikey bölmesinde. Döndürmemelidir olması herhangi **yedekleme öğeleri**, **yönetim sunucularını yedekleme**, veya **öğeleri çoğaltılan** listelenir. Öğeleri hello kasasına görüntülenmeye devam ederse, toostep üç dönün ve farklı öğe türü listesini seçin.  
5. Merhaba kasası araç çubuğunda başka öğe yok olduğunda tıklatın **silmek**.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/delete-vault.png)
6. toodelete hello kasası, istediğiniz tooverify tıklatın **Evet**.

    Merhaba kasası silinir ve hello portal döndürür toohello **yeni** servis menüsü.

## <a name="what-if-i-stopped-hello-backup-process-but-retained-hello-data"></a>Ne hello yedekleme işlemi durduruldu ancak hello veri tutulur?
Merhaba yedekleme işlemi ancak yanlışlıkla durdurduysanız *korunur* hello veri silmelisiniz hello yedekleme verilerini hello kasası silmeden önce. toodelete hello yedekleme verileri:

1. Merhaba üzerinde **yedekleme öğeleri** dikey penceresinde sağ hello tıklayın öğesi ve hello bağlam menüsü **yedekleme verileri Sil**.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    Merhaba **yedekleme verilerini Sil** dikey pencere açılır.
2. Merhaba üzerinde **yedekleme verilerini Sil** dikey penceresinde, tür hello adı hello öğesini tıklatın ve **silmek**.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/delete-retained-vault.png)

    Merhaba veri sildikten sonra toostep 4 c dönün ve hello işlemine devam edin.

## <a name="delete-a-vault-used-tooprotect-a-dpm-server"></a>Kullanılan kasa tooprotect bir DPM sunucusu Sil
Kullanılan kasa tooprotect bir DPM sunucusu silmeden önce oluşturulmuş bir kurtarma noktası temizleyin ve hello kasası hello sunucunun kaydını silmek gerekir.

bir koruma grubuyla ilişkili toodelete hello veriler:

1. Hello DPM Yönetici Konsolu, tıklatın **koruma** > bir koruma grubu seçin > merhaba koruma grubu üyesini seçin > merhaba araç şeridinde tıklatıp **kaldırmak**.

  Select hello koruma grubu üyesi tooactivate hello **kaldırmak** düğmesini hello aracı. Merhaba örnekte hello üyesidir **dummyvm9**. tooselect hello koruma grubunda birden çok üye tutun hello Ctrl tuşunu basılı hello üyelerinde a tıklayarak.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    Merhaba **korumayı Durdur** iletişim kutusunu açar.
2. Merhaba, **korumayı Durdur** iletişim kutusunda **korumalı verileri Sil**, tıklatıp **korumayı Durdur**.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    toodelete bir kasa, temizler, silmek veya gerekir, hello kasası, korumalı verileri. Hello sayısına kurtarma noktaları ve hello koruma grubundaki verileri bağlı olarak, bunu herhangi bir yere birkaç saniye tooseveral dakika toodelete hello verileri alabilir. Merhaba **korumayı Durdur** iletişim hello iş tamamlandığında hello durumunu gösterir.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. Bu işlem, tüm koruma gruplarındaki tüm üyeleri için devam edin.

    Tüm korumalı veriler ve koruma grupları kaldırın.
4. Tüm üyeler hello koruma grubundan sildikten sonra toohello Azure portalına geçin. Merhaba kasa Panosu açın ve olmadığından emin olun hiçbir **yedekleme öğeleri**, **yönetim sunucularını yedekleme**, veya **öğeleri çoğaltılan**. Merhaba kasası araç çubuğundan, **silmek**.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/delete-vault.png)

    Yedekleme Yönetimi Sunucusu kaydedildi toohello kasası varsa, hello kasada hiç veri olsa hello kasası silinemiyor. Merhaba kasayla ilişkili hello yedekleme yönetim sunucuları silindi ancak hello listelenen sunucuları **Essentials** bölmesinde bkz [Bul hello yedekleme yönetim sunucuları kayıtlı toohello kasası](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault) .
5. toodelete hello kasası, istediğiniz tooverify tıklatın **Evet**.

    Merhaba kasası silinir ve hello portal döndürür toohello **yeni** servis menüsü.

## <a name="delete-a-vault-used-tooprotect-a-production-server"></a>Kullanılan kasa tooprotect bir üretim sunucusu Sil
Kullanılan kasa tooprotect bir üretim sunucusu silmeden önce silmek veya hello kasası hello sunucudan kaydı silinemedi.

Merhaba kasayla ilişkili toodelete hello üretim sunucusu:

1. Hello Azure portal, hello kasa Panosu açın ve'ı tıklatın **ayarları** > **Yedekleme Altyapısı** > **üretim sunucuları**.

    ![Üretim sunucularında dikey penceresini açın](./media/backup-azure-delete-vault/delete-production-server.png)

    Merhaba **üretim sunucuları** dikey penceresi açılır ve hello kasasında tüm üretim sunucuları listeler.

    ![Üretim sunucuları listesi](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. Merhaba üzerinde **üretim sunucuları** dikey penceresinde hello sunucuda sağ tıklayın ve **silmek**.

    ![Üretim sunucusunu Sil ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    Merhaba **silmek** dikey pencere açılır.

    ![Üretim sunucusunu Sil ](./media/backup-azure-delete-vault/delete-blade.png)
3. Merhaba üzerinde **silmek** dikey penceresinde hello sunucu adını doğrulayın ve tıklatın **silmek**. Doğru ad hello sunucusu, tooactivate hello gerekir **silmek** düğmesi.

    Merhaba kasası silindikten sonra hello kasası silinmiş bildiren bir ileti alırsınız. Tüm sunucuları hello kasasında sildikten sonra geri toohello Essentials hello kasa Panosu bölmesinde gidin.
4. Merhaba kasa panosunda olmadığından emin olun hiçbir **yedekleme öğeleri**, **yönetim sunucularını yedekleme**, veya **öğeleri çoğaltılan**. Merhaba kasası araç çubuğundan, **silmek**.
5. toodelete hello kasası, istediğiniz tooverify tıklatın **Evet**.

    Merhaba kasası silinir ve hello portal döndürür toohello **yeni** servis menüsü.

## <a name="delete-a-backup-vault-in-classic-portal"></a>Klasik Portalı'ndaki yedekleme kasalarının Sil
Merhaba aşağıdaki hello Klasik Portalı'nda bir yedekleme kasası silmek için yönergelerdir. Merhaba yedekleme kasası silmeden önce maddelerini yedeklenen hello kurtarma noktalarını silmeniz gerekir veya hello kayıtlı sunucuları kaldırın. Merhaba kayıtlı hello Windows Server, iş istasyonu veya kayıtlı toohello kasası olan sanal makinelere sunucularıdır.

1. Açık hello [Klasik portal](https://manage.windowsazure.com).

2. Yedekleme kasalarını Hello listeden toodelete istediğiniz hello kasayı seçin.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    Merhaba kasa panosu açılır. Windows sunucuları ve/veya Azure sanal makinelerin hello kasayla ilişkili hello numarası bakın. Ayrıca, Azure'da tüketilen hello toplam depolama alanı bakın. Tüm yedekleme işleri durdurur ve hello kasası silmeden önce tüm veri.

3. Merhaba tıklatın **korunan öğeler** sekmesini ve ardından **korumayı Durdur**

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    Merhaba **'kasanızı' korumasını Durdur** iletişim kutusu görüntülenir.
4. Merhaba, **'kasanızı' korumasını Durdur** iletişim kutusunda, onay **Delete ilişkilendirilmiş yedekleme verileri** tıklatıp ![onay işaretine](./media/backup-azure-delete-vault/checkmark.png). <br/>
    İsteğe bağlı olarak, korumayı durdurma nedeni seçin ve bir açıklama sağlayın.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    Merhaba kasasında Hello öğeleri sildikten sonra hello kasası boş olur.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. Sekmeleri Hello listesinde tıklayın **kayıtlı öğeler**. Merhaba **türü** açılır menüsünde, toochoose hello yazın kayıtlı sunucu toohello kasası etkinleştirir. Merhaba türü, Windows Server ya da Azure sanal makine olabilir. Aşağıdaki örneğine hello, hello sanal makine kayıtlı toohello kasa seçin ve tıklatın **Unregister**.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  Bir Windows Server'dan hello için toodelete hello kayıt istiyorsanız **türü** açılır menüsünde, select **Windows Server**, tıklatın ![onay işareti](./media/backup-azure-delete-vault/checkmark.png) toorefresh Merhaba ekranında, ve ardından **silmek**. <br/>

  ![Windows Server'ı seçin](./media/backup-azure-delete-vault/select-windows-server.png)

6. Sekmeleri Hello listesinde tıklayın **Pano** sekmesinde tooopen. Kayıtlı sunucu ya da Azure sanal makineleri hello bulutta korumalı olmadığını doğrulayın. Ayrıca, depolama alanına veri olduğunu doğrulayın. Tıklatın **silmek** toodelete hello kasası.

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    Merhaba silme yedekleme kasası onay ekranı açılır. Neden hello kasası silmekte olduğunuz bir seçenek belirleyin ve'ı tıklatın ![onay işareti](./media/backup-azure-delete-vault/checkmark.png). <br/>

    ![Yedekleme verilerini sil](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    Merhaba kasası silinir ve toohello Klasik portal panoya dönün.

### <a name="find-hello-backup-management-servers-registered-toohello-vault"></a>Merhaba yedekleme yönetim sunucuları kayıtlı toohello kasası Bul
Birden çok kayıtlı sunucuları tooa kasası varsa zor tooremember olabilir bunları. toosee hello sunucuları toohello kasaya kayıtlı ve bunları silin:

1. Açık hello kasa Panosu.
2. Merhaba, **Essentials** bölmesinde tıklatın **ayarları** tooopen o dikey.

    ![ayarları dikey penceresini açın](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. Merhaba üzerinde **ayarlar dikey**, tıklatın **Yedekleme Altyapısı**.
4. Merhaba üzerinde **Yedekleme Altyapısı** dikey penceresinde tıklatın **yedekleme yönetim sunucuları**. Merhaba yedekleme yönetim sunucuları dikey pencere açılır.

    ![Yedekleme yönetim sunucuları listesi](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. toodelete hello listesinde, bir sunucudan hello sunucunun hello adına sağ tıklayın ve ardından **silmek**.
    Merhaba **silmek** dikey pencere açılır.
6. Merhaba üzerinde **silmek** dikey penceresinde hello hello sunucunun adını belirtin. Uzun bir adı olması durumunda kopyalayın ve yedekleme yönetim sunucularının hello listeden yapıştırın. Ardından **silmek**.  

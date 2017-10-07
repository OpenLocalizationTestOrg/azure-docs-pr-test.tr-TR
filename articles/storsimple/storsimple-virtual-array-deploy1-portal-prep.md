---
title: "StorSimple sanal dizini aaaPortal hazırlığı | Microsoft Docs"
description: "İlk öğretici toodeploy StorSimple sanal dizinin hello Azure portal hazırlanmasını içerir"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a>StorSimple sanal dizinin dağıtma - hello Azure portal hazırlama

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a>Genel Bakış

Gerekli dağıtım öğreticileri hello serideki makalesine ilk hello budur toocompletely sanal dizinizi bir dosya sunucusu veya hello Resource Manager modelini kullanarak bir iSCSI sunucu olarak dağıtın. Bu makalede hello gerekli hazırlık toocreate ve, StorSimple cihaz Yöneticisi hizmeti önceki tooprovisioning sanal bir dizi yapılandırın. Bu makalede ayrıca tooa dağıtım yapılandırma denetim listesi ve yapılandırma önkoşulları bağlar.

Kurulum ve yapılandırma yönetici ayrıcalıkları toocomplete hello işlemi gerekir. Başlamadan önce hello dağıtım yapılandırma denetim listesini gözden geçirmenizi öneririz. Merhaba portal hazırlık 10 dakikadan daha kısa sürer.

Bu makalede yayımlanmış hello bilgiler, StorSimple sanal hello Azure portal dizilerde ve Microsoft Azure kamu bulut toohello dağıtımını geçerlidir.

### <a name="get-started"></a>başlarken
Merhaba dağıtımı iş akışı hello portal hazırlama, sanallaştırılmış ortamınızdaki sanal bir dizi sağlama ve hello Kurulumu Tamamlanıyor oluşur. Merhaba StorSimple sanal dizinin dağıtım bir dosya sunucusu veya bir iSCSI sunucusu olarak kullanmaya tooget, aşağıdaki tabloda kaynakları toorefer toohello gerekir.

#### <a name="deployment-articles"></a>Dağıtım makaleleri

toodeploy, StorSimple sanal dizinin dizisi belirlenen hello makalelerinde aşağıdaki toohello bakın.

| **#** | **Bu adımda** | **Bunu...** | **Ve bu belgeleri kullanın.** |
| --- | --- | --- | --- |
| 1. |**Azure portal Hello ayarlayın** |Oluşturun ve, StorSimple cihaz Yöneticisi hizmeti önceki tooprovisioning StorSimple sanal dizinin yapılandırın. |[Merhaba portal hazırlama](storsimple-virtual-array-deploy1-portal-prep.md) |
| 2. |**Merhaba sanal dizinin sağlama** |Hyper-v, sağlama ve Windows Server 2012 R2, Windows Server 2012 veya Windows Server 2008 R2 üzerinde Hyper-V çalıştıran bir konak sisteminde tooa StorSimple sanal dizinin bağlanın. <br></br> <br></br> VMware, sağlamak ve tooa StorSimple sanal dizinin VMware ESXi 5.5 çalıştıran bir konak sistemi ve üstü bağlanın.<br></br> |[Hyper-V sanal bir dizide sağlama](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [VMware sanal bir dizide sağlama](storsimple-virtual-array-deploy2-provision-vmware.md) |
| 3. |**Sanal dizinin Hello ayarlayın** |Dosya sunucunuz için ilk kurulum gerçekleştirmek, StorSimple dosya sunucunuzu kaydetmek ve hello cihaz kurulumunu tamamlayın. Ardından, SMB paylaşımları sağlayabilirsiniz. <br></br> <br></br> İSCSI sunucunuz için ilk kurulum gerçekleştirmek, StorSimple iSCSI sunucuyu kaydetmek ve hello cihaz kurulumunu tamamlayın. Ardından, iSCSI birimleri sağlayabilirsiniz. |[Sanal dizinin Kurulumu dosya sunucusu olarak ayarlayın](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[Sanal dizinin Kurulumu iSCSI sunucusu olarak ayarla](storsimple-virtual-array-deploy3-iscsi-setup.md) |

Hello Azure portal yukarı tooset şimdi başlayabilirsiniz.

## <a name="configuration-checklist"></a>Yapılandırma denetim listesi

Merhaba yapılandırma denetim listesi, StorSimple sanal dizisinde hello yazılım yapılandırmadan önce toocollect gereksinim hello bilgileri açıklar. Zaman yardımcı öncesinde bu bilgiler, ortamınızdaki hello StorSimple cihazı dağıtma daha verimli hale hello işlemi hazırlanıyor. StorSimple sanal dizinizi bir dosya sunucusu veya bir iSCSI sunucu olarak dağıtılan bağlı bağlı olarak, denetim listeleri aşağıdaki hello biri gerekir.

* Merhaba karşıdan [StorSimple sanal dizinin dosya sunucusu yapılandırma denetim listesi](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).
* Merhaba karşıdan [StorSimple sanal dizinin iSCSI sunucu yapılandırma denetim listesi](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).

## <a name="prerequisites"></a>Ön koşullar

Burada, StorSimple cihaz Yöneticisi hizmetiniz, StorSimple sanal dizinin ve hello veri merkezi ağ için hello yapılandırma önkoşulları öğrenin.

### <a name="for-hello-storsimple-device-manager-service"></a>Merhaba StorSimple cihaz Yöneticisi hizmeti

Başlamadan önce aşağıdakilerden emin olun:

* Erişim kimlik bilgilerine sahip bir Microsoft hesabınız var.
* Erişim kimlik bilgilerine sahip bir Microsoft Azure Storage hesabınız var.
* Microsoft Azure aboneliğiniz StorSimple cihaz Yöneticisi hizmeti için etkinleştirilmiş olmalıdır.

### <a name="for-hello-storsimple-virtual-array"></a>StorSimple sanal dizinin Hello için

Sanal bir dizi dağıtmadan önce emin olun:

* Hyper-V Windows Server 2008 R2 veya sonraki sürümlerde çalışan erişim tooa ana bilgisayar sistemi sahip veya kullanılan tooa olabilir (ESXi 5.5 veya sonraki) VMware bir aygıtı sağlamak.
* Merhaba ana bilgisayar sistemidir mümkün toodedicate kaynakları tooprovision sanal dizinizi hello:
  
  * 4 çekirdek en az.
  * En az 8 GB RAM. Dosya sunucusu olarak tooconfigure hello sanal dizinin planlıyorsanız, 8 GB 2 milyon dosyalarını destekler. 16 GB RAM toosupport 2-4 milyon dosyaları gerekir.
  * Bir ağ arabirimi.
  * Sistem verileri için 500 GB sanal disk.

### <a name="for-hello-datacenter-network"></a>Merhaba veri merkezi ağ için

Başlamadan önce aşağıdakilerden emin olun:

* Merhaba ağ, veri merkezinizdeki hello StorSimple cihazınız için ağ gereksinimlerine uygun yapılandırılır. Daha fazla bilgi için bkz: Merhaba [StorSimple sanal dizinin sistem gereksinimleri](storsimple-ova-system-requirements.md).
* StorSimple sanal dizinizi ayrılmış 5 MB/sn Internet bant genişliği (veya daha fazla) olduğundan her zaman kullanılabilir. Bu bant genişliği herhangi bir uygulama ile Paylaşılmaması gerekiyor.

## <a name="step-by-step-preparation"></a>Adım adım hazırlama

Adım adım yönergeler tooprepare aşağıdaki hello portalınızı hello StorSimple cihaz Yöneticisi hizmeti için kullanın.

## <a name="step-1-create-a-new-service"></a>1. Adım: Yeni bir hizmet oluşturun

Merhaba StorSimple cihaz Yöneticisi hizmeti tek bir örneği birden çok StorSimple sanal diziler yönetebilirsiniz. Adımları toocreate hello StorSimple cihaz Yöneticisi hizmetinin bir örneği aşağıdaki hello gerçekleştirin. Mevcut bir StorSimple cihaz Yöneticisi hizmeti toomanage sanal dizileriniz varsa, bu adımı atlayın ve çok gidin[2. adım: hello hizmet kayıt anahtarını Al](#step-2-get-the-service-registration-key).

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> Hizmetiniz ile Merhaba otomatik bir depolama hesabının oluşturulmasını etkinleştirmediyseniz toocreate ihtiyacınız olacak bir hizmeti başarıyla oluşturduktan sonra en az bir depolama hesabı.
> 
> * Otomatik olarak bir depolama hesabı oluşturmadıysanız, çok Git[hello hizmet için yeni bir depolama hesabı yapılandırma](#optional-step-configure-a-new-storage-account-for-the-service) ayrıntılı yönergeler için.
> * Depolama hesabı hello otomatik oluşturma etkinleştirilirse, çok Git[2. adım: hello hizmet kayıt anahtarını Al](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>2. adım: hello hizmet kayıt anahtarını alın

Merhaba StorSimple cihaz Yöneticisi hizmeti çalışır durumda sonra tooget hello hizmet kayıt anahtarı gerekir. Bu anahtar kullanılan tooregister ve StorSimple Cihazınızı hello hizmetiyle bağlama.

Merhaba adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://portal.azure.com/).

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> Merhaba hizmet kayıt anahtarı olan kullanılan tooregister tüm StorSimple Aygıt Yöneticisi'ni hizmetinizle tooregister gereken StorSimple Aygıt Yöneticisi'ni cihazların Merhaba.
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a>Adım 3: hello sanal dizinin görüntü indirin

Merhaba hizmet kayıt anahtarını oluşturduktan sonra ana bilgisayar sisteminde toodownload hello uygun sanal dizinin görüntü tooprovision sanal bir dizi gerekir. Merhaba sanal dizinin görüntüleri, işletim sisteminin belirli ve hello Azure Portalı'nda hello hızlı başlangıç sayfasından indirilebilir.

> [!IMPORTANT]
> StorSimple sanal dizinin Hello üzerinde çalışan hello yazılımı yalnızca StorSimple cihaz Yöneticisi hizmeti hello ile kullanılabilir.
> 
> 

Merhaba adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://portal.azure.com/).

#### <a name="tooget-hello-virtual-array-image"></a>tooget hello sanal dizinin görüntüsü

1. Merhaba içine oturum [Azure portal](https://portal.azure.com/). 
2. Hello Azure portal'ı tıklatın **Gözat > StorSimple cihaz yöneticileri**.
3. Var olan bir StorSimple cihaz Yöneticisi hizmetini seçin. Merhaba, **StorSimple Aygıt Yöneticisi'ni** dikey penceresinde tıklatın **Hızlı Başlangıç**. 
4. Merhaba Microsoft Download Center gelen toodownload istediğiniz hello bağlantı karşılık gelen toohello görüntüsünü tıklatın. yaklaşık 4.8 GB Hello görüntü dosyalarıdır.
   
   * Hyper-V Windows Server 2012 ve sonraki sürümler için VHDX
   * VHD için Hyper-V Windows Server 2008 R2 ve sonraki sürümler
   * VMDK VMWare ESXi 5.5 ve sonraki sürümleri
5. Karşıdan yükle ve hello sıkıştırması açılmış dosyasının bulunduğu bir not yapmadan hello dosya tooa yerel sürücü, sıkıştırmasını açın.

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a>İsteğe bağlı adım: yeni bir depolama hesabı hello hizmeti için yapılandırma

Bu adım isteğe bağlıdır ve yalnızca, bir depolama hesabının otomatik oluşturulmasını hello hizmetiniz ile etkinleştirmediyseniz gerçekleştirilmelidir.

Azure storage hesabı farklı bir bölgede toocreate gerekirse bkz [nasıl toocreate bir depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account) adım adım yönergeler için.

Merhaba adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://ms.portal.azure.com/) hello StorSimple cihaz Yöneticisi hizmet sayfası tooadd var olan bir Microsoft Azure depolama hesabı üzerinde.

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>tooadd sahip bir depolama hesabı kimlik bilgilerini hello hello Aygıt Yöneticisi hizmeti aynı Azure abonelik

1. Aygıt Yöneticisi hizmeti, select tooyour gidin ve çift tıklatın. Merhaba açılır **genel bakış** dikey.
2. Seçin **depolama hesabının kimlik bilgilerini** hello içinde **yapılandırma** bölümü.
3. **Ekle**'ye tıklayın.
4. Merhaba, **depolama hesabı ekleme** dikey penceresinde, aşağıdaki hello:
   
    1. İçin **abonelik**seçin **geçerli**.
   
    2. Hello Azure depolama hesabınızın adını sağlayın.
   
    3. Seçin **etkinleştirmek** toocreate StorSimple cihaz ve hello bulut arasındaki ağ iletişimi için güvenli bir kanal. Seçin **devre dışı** yalnızca özel bir bulutta işlem yapıyorsanız.
   
    4. **Ekle**'ye tıklayın. Merhaba depolama hesabı başarıyla oluşturulduktan sonra size bildirilir.<br></br>
   
     ![Varolan bir depolama hesabı kimlik bilgileri Ekle](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a>Sonraki adım

Merhaba sonraki tooprovision, StorSimple sanal dizi için bir sanal makine adımdır. Ana bilgisayar işletim sistemine bağlı olarak bkz hello ayrıntılı yönergeleri:

* [Hyper-V StorSimple sanal dizisinde sağlama](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [VMware StorSimple sanal dizisinde sağlama](storsimple-virtual-array-deploy2-provision-vmware.md)


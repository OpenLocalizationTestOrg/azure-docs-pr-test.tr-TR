---
title: "aaaStorSimple bulut Gereci güncelleştirme 3'ü | Microsoft Docs"
description: "Nasıl toocreate, dağıtmak ve Microsoft Azure sanal ağında StorSimple bulut uygulaması yönetmek öğrenin. (TooStorSimple güncelleştirme 3 ve sonrasında geçerlidir)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: ba60a629f1f4b8f0d4566eeb45bae8696f50d0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-cloud-appliance-in-azure-update-3-and-later"></a>Azure’da StorSimple Cloud Appliance dağıtma ve yönetme (StorSimple Güncelleştirme 3 ve üstü)

## <a name="overview"></a>Genel Bakış

Merhaba StorSimple 8000 serisi bulut uygulaması, Microsoft Azure StorSimple çözümünüzle birlikte gelen ek bir yetenektir. Microsoft Azure sanal ağındaki bir sanal makinede Hello StorSimple bulut uygulaması çalışır ve bunu tooback yukarı ve kopya veri ana bilgisayarlarını kullanabilirsiniz.

Bu makalede hello adım adım işlemi toodeploy ve azure'da bir StorSimple bulut uygulaması yönetin. Bu makaleyi okuduktan sonra şunları yapabilir olacaksınız:

* Nasıl hello bulut uygulaması hello fiziksel CİHAZDAN farkı anlayın.
* Mümkün toocreate olması ve hello bulut uygulaması yapılandırın.
* Toohello bulut uygulaması bağlayın.
* Nasıl toowork hello ile bulut Gereci öğrenin.

Bu öğretici tooall hello StorSimple bulut güncelleştirme 3'ü çalıştıran cihazları uygular ve daha sonra.

#### <a name="cloud-appliance-model-comparison"></a>Bulut gereci modeli karşılaştırması

Merhaba StorSimple bulut uygulaması kullanılabilir iki modellerinde standart 8010 (önceden hello 1100 biliniyordu) ve premium 8020 (güncelleştirme 2'de sunulmuştur). Aşağıdaki tablonun hello hello iki modellerin karşılaştırması gösterir.

| Cihaz modeli | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Maksimum kapasite** |30 TB |64 TB |
| **Azure VM** |Standard_A3 (4 çekirdek, 7 GB bellek)| Standard_DS3 (4 çekirdek, 14 GB bellek)|
| **Bölge kullanılabilirliği** |Tüm Azure bölgeleri |Premium Depolama ve DS3 Azure VM’lerini destekleyen Azure bölgeleri<br></br>Kullanım [bu listeyi](https://azure.microsoft.com/regions/services/) toosee her iki **sanal makineleri > DS serisi** ve **depolama > Disk Depolama** Bölgenizde kullanılabilir. |
| **Depolama türü** |Yerel diskler için Azure Standard Storage kullanır.<br></br> Nasıl çok öğrenin[standart depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md) |Yerel diskler için Azure Premium Depolama kullanır<sup>2</sup> <br></br>Nasıl çok öğrenin[Premium depolama hesabı oluşturma](../storage/common/storage-premium-storage.md) |
| **İş yükü kılavuzu** |Yedeklerden dosya alma öğe düzeyi |Bulut geliştirme ve test senaryoları <br></br>Düşük gecikme süreli ve daha yüksek performanslı iş yükleri<br></br>Olağanüstü durum kurtarma için ikincil cihaz |

<sup>1</sup> *önceden hello 1100 biliniyordu*.

<sup>2</sup> *hem 8010 hello ve 8020 hello bulut katmanı. hello fark hello aygıt yerel katmandadır hello yalnızca bulunmaktadır için Azure Standard Storage kullanır*.

## <a name="how-hello-cloud-appliance-differs-from-hello-physical-device"></a>Nasıl hello bulut uygulaması hello fiziksel CİHAZDAN farkı

Merhaba StorSimple bulut uygulaması, bir Microsoft Azure sanal makinesi'nın tek bir düğümde çalışan StorSimple, yalnızca yazılım tabanlı bir sürümüdür. Merhaba bulut uygulaması fiziksel cihazınız kullanılabilir değil olağanüstü durum kurtarma senaryolarını destekler. yedeklemeler, şirket içi olağanüstü durum kurtarma ve bulut geliştirme ve test senaryolarından öğe düzeyinde alma Hello bulut uygulaması uygundur.

#### <a name="differences-from-hello-physical-device"></a>Merhaba fiziksel CİHAZDAN farklar

Merhaba aşağıdaki tabloda hello StorSimple bulut uygulaması ve hello StorSimple fiziksel cihazı arasındaki bazı temel farklar gösterilmektedir.

|  | Fiziksel cihaz | Bulut gereci |
| --- | --- | --- |
| **Konum** |Merhaba veri merkezinde yer alır. |Azure üzerinde çalışır. |
| **Ağ arabirimleri** |Altı ağ arabirimi bulunur: VERİ 0’dan VERİ 5’e. |Yalnızca bir ağ arabirimi bulunur: VERİ 0 |
| **Kayıt** |Merhaba ilk yapılandırma adımı sırasında kaydedilir. |Kayıt ayrı bir görevdir. |
| **Hizmeti verileri şifreleme anahtarı** |Merhaba fiziksel cihazda yeniden oluşturun ve ardından hello bulut uygulaması hello yeni anahtarla güncelleştirin. |Merhaba bulut Gereci yeniden oluşturamıyor. |
| **Desteklenen birim türleri** |Hem yerel olarak sabitlenmiş hem de katmanlı birimleri destekler. |Yalnızca katmanlı birimleri destekler. |

## <a name="prerequisites-for-hello-cloud-appliance"></a>Merhaba bulut uygulaması için Önkoşullar

Aşağıdaki bölümlerde hello StorSimple bulut uygulaması için hello yapılandırma önkoşulları açıklanmaktadır. Bulut uygulaması dağıtmadan önce bulut uygulaması kullanarak hello güvenlik konuları gözden geçirin.

[!INCLUDE [StorSimple Cloud Appliance security](../../includes/storsimple-8000-cloud-appliance-security.md)]

#### <a name="azure-requirements"></a>Azure gereksinimleri

Merhaba bulut uygulaması sağlamadan önce Azure ortamınızda hazırlıklar aşağıdaki toomake hello gerekir:

* Veri merkezinizde bir StorSimple 8000 serisi fiziksel cihazının (model 8100 veya 8600) dağıtıldığından ve çalıştırıldığından emin olun. Bu aygıtla hello düşündüğünüz aynı StorSimple cihaz Yöneticisi hizmeti kayıt StorSimple bulut uygulaması için bir toocreate.
* Merhaba bulut uygulaması için [Azure üzerinde bir sanal ağ yapılandırma](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Premium Storage kullanıyorsanız, Premium Storage’ı destekleyen bir Azure bölgesinde sanal ağ oluşturmanız gerekir. Merhaba Premium Storage bölgeleri olan toohello satır hello Disk depolama için karşılık gelen bölgeler [bölgeye göre Azure Hizmetleri listesini](https://azure.microsoft.com/regions/services/).
* Kendi DNS sunucu adınızı belirtmek yerine Azure tarafından sağlanan hello varsayılan DNS sunucusu kullanmanızı öneririz. DNS sunucusu adınız geçerli değilse veya hello DNS sunucusu mümkün tooresolve IP adreslerini doğru değilse, hello bulut uygulaması hello oluşturma başarısız olur.
* Noktadan siteye ve siteden siteye isteğe bağlıdır, ancak gerekli değildir. İsterseniz, daha gelişmiş senaryolar için bu seçenekleri yapılandırabilirsiniz.
* Oluşturabileceğiniz [Azure sanal makineleri](../virtual-machines/virtual-machines-windows-quick-create-portal.md) (barındırma sunucuları) hello bulut uygulaması tarafından sunulan hello birimleri kullanabileceğiniz sanal ağda hello. Bu sunucular hello aşağıdaki gereksinimleri karşılamalıdır:

  * iSCSI Initiator yazılımı yüklü Windows veya Linux sanal makineleri olmalıdır.
  * Hello çalıştırması hello bulut uygulaması aynı sanal ağ.
  * Merhaba bulut uygulaması hello iç IP adresi üzerinden hello bulut uygulaması mümkün tooconnect toohello iSCSI hedefi olabilir.
  * Yapılandırdığınız destek iSCSI ve bulut üzerinde hello aynı trafiği için emin olun sanal ağ.

#### <a name="storsimple-requirements"></a>StorSimple gereksinimleri

Bulut uygulaması oluşturmadan önce aşağıdaki güncelleştirmeleri tooyour StorSimple cihaz Yöneticisi hizmeti hello olun:

* Ekleme [erişim denetimi kayıtları](storsimple-8000-manage-acrs.md) giderek toobe hello konak sunucuları, bulut uygulaması için hello VM'ler için.
* Kullanım bir [depolama hesabı](storsimple-8000-manage-storage-accounts.md#add-a-storage-account) hello içinde hello bulut uygulaması ile aynı bölgeye. Farklı bölgelerdeki Depolama hesapları performansın düşmesine neden olabilir. Merhaba bulut uygulaması ile standart veya Premium depolama hesabı kullanabilirsiniz. Hakkında daha fazla bilgi toocreate bir [standart depolama hesabı](../storage/common/storage-create-storage-account.md) veya [Premium depolama hesabı](../storage/common/storage-premium-storage.md)
* Merhaba, verileriniz için kullanılan bulut Gereci oluşturulması için farklı bir depolama hesabı kullanın. Aynı depolama hesabındaki performansın düşmesine neden hello kullanma.

Başlamadan önce bilgilerini aşağıdaki hello sahip olduğunuzdan emin olun:

* Azure portalı hesabınıza erişim kimlik bilgileri.
* Hello hizmet verileri şifreleme anahtarı fiziksel cihazınızdan bir kopyasını toohello StorSimple cihaz Yöneticisi hizmetine kayıtlı.

## <a name="create-and-configure-hello-cloud-appliance"></a>Oluşturma ve hello bulut uygulaması yapılandırma

Bu yordamları gerçekleştirmeden önce hello karşıladığınızdan emin olun [hello bulut uygulaması için Önkoşullar](#prerequisites-for-the-cloud-appliance).

Aşağıdaki adımları toocreate StorSimple bulut uygulaması hello gerçekleştirin.

### <a name="step-1-create-a-cloud-appliance"></a>1. Adım: Bulut gereci oluşturma

Aşağıdaki adımları toocreate hello StorSimple bulut uygulaması hello gerçekleştirin.

[!INCLUDE [Create a cloud appliance](../../includes/storsimple-8000-create-cloud-appliance-u2.md)]

Bu adımda hello bulut uygulaması Hello oluşturulmasını başarısız olursa, bağlantı toohello Internet olmayabilir. Daha fazla bilgi için çok Git[Internet bağlantı hatalarını giderme](#troubleshoot-internet-connectivity-errors) bulut uygulaması oluştururken.

### <a name="step-2-configure-and-register-hello-cloud-appliance"></a>2. adım: Yapılandırma ve hello bulut uygulaması kaydetme

Bu yordama başlamadan önce hello hizmet verileri şifreleme anahtarının bir kopyasına sahip olduğunuzdan emin olun. StorSimple cihaz Yöneticisi hizmeti hello ile ilk StorSimple fiziksel cihazınız kayıtlı hello hizmet verileri şifreleme anahtarı oluşturulur. Toosave belirtildiği gibi güvenli bir konumda. Hello hizmeti veri şifreleme anahtarının bir kopyası yoksa, Yardım için Microsoft Support başvurmanız gerekir.

Aşağıdaki adımları tooconfigure hello gerçekleştirmek ve StorSimple bulut uygulaması kaydedin.

[!INCLUDE [Configure and register a cloud appliance](../../includes/storsimple-8000-configure-register-cloud-appliance.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>3. adım: (İsteğe bağlı) Değiştir hello cihaz yapılandırma ayarları

Merhaba aşağıdaki bölümde, toouse CHAP, StorSimple Snapshot Manager veya hello cihaz Yöneticisi parolasını değiştirmek istiyorsanız hello StorSimple bulut uygulaması için gereken hello cihaz yapılandırma ayarları açıklanmaktadır.

#### <a name="configure-hello-chap-initiator"></a>Merhaba CHAP başlatıcısını yapılandırma

Bu parametre, bulut uygulaması (hedef) tooaccess hello birimleri çalıştığınız hello başlatıcılardan (sunucu) beklediği hello kimlik bilgilerini içerir. Hello başlatıcıları CHAP kullanıcı adı ve CHAP parolası tooidentify kendilerini tooyour cihaz bu kimlik doğrulaması sırasında sağlar. Ayrıntılı adımlar için çok Git[cihazınız için CHAP yapılandırma](storsimple-8000-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Merhaba CHAP hedefini yapılandırma

Bu parametre CHAP etkin Başlatıcı karşılıklı veya çift yönlü kimlik doğrulaması istediğinde, bulut uygulaması kullandığı hello kimlik bilgileri içerir. Bulut uygulaması bir ters CHAP kullanıcı adı ve ters CHAP parolası tooidentify kendisini bu kimlik doğrulama işlemi sırasında toohello başlatıcısını kullanır.

> [!NOTE]
> CHAP hedefi ayarları genel ayarlardır. Bu ayarlar uygulandığında, tüm hello birimleri toohello bulut Gereci CHAP kimlik doğrulamasını kullan bağlı.

Ayrıntılı adımlar için çok Git[cihazınız için CHAP yapılandırma](storsimple-8000-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Merhaba StorSimple Snapshot Manager parolasını yapılandırma

StorSimple Snapshot Manager yazılımı Windows ana bilgisayarınıza bulunur ve StorSimple Cihazınızı hello form yerel ve bulut anlık görüntüleri toomanage yedeklerini yöneticilerinin sağlar.

> [!NOTE]
> Merhaba bulut uygulaması için Windows ana bilgisayarınız bir Azure sanal makinesidir.

Bir aygıt hello StorSimple Snapshot Manager yapılandırırken istenir tooprovide depolama Cihazınızı StorSimple cihazı IP adresi ve parola tooauthenticate hello. Ayrıntılı adımlar için çok Git[yapılandırma StorSimple Snapshot Manager parolası](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Değişiklik hello cihaz Yöneticisi parolası

Kullandığınızda bulut uygulaması hello Windows PowerShell arabirimi tooaccess Merhaba, gerekli tooenter bir cihaz Yöneticisi parolası olur. Verilerinizin güvenliğini hello için Hello bulut uygulaması kullanılabilmesi için önce bu parolayı değiştirmeniz gerekir. Ayrıntılı adımlar için çok Git[cihaz Yöneticisi parolasını yapılandırma](../storsimple/storsimple-8000-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-cloud-appliance"></a>Toohello bulut uygulaması uzaktan bağlanma

Uzaktan erişim tooyour bulut uygulaması hello Windows PowerShell arabirimi üzerinden varsayılan olarak etkin değildir. İlk hello bulut uygulaması uzaktan yönetimini etkinleştirmeniz gerekir ve istemci hello tooaccess hello bulut uygulaması kullanılır.

Aşağıdaki iki aşamalı yordamı hello açıklar nasıl tooconnect tooyour uzaktan bulut uygulaması.

### <a name="step-1-configure-remote-management"></a>1. Adım: Uzaktan yönetimi yapılandırma

Adımları tooconfigure uzaktan yönetimi, StorSimple bulut uygulaması için aşağıdaki hello gerçekleştirin.

[!INCLUDE [Configure remote management via HTTP for cloud appliance](../../includes/storsimple-8000-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-cloud-appliance"></a>2. adım: Uzaktan erişim hello bulut uygulaması

Merhaba bulut uygulaması uzaktan yönetimi etkinleştirdikten sonra Windows PowerShell uzaktan iletişim tooconnect toohello Gereci hello içinde başka bir sanal makineden kullanmak aynı sanal ağ. Örneğin, yapılandırılmış ve tooconnect iSCSI kullanılan VM hello ana bilgisayardan bağlanabilir. Çoğu dağıtımda ana bilgisayarınız hello bulut uygulaması erişmek için kullanabileceğiniz VM ortak uç nokta tooaccess açılır.

> [!WARNING]
> **Gelişmiş güvenlik için HTTPS toohello uç noktaları bağlanırken kullanmak ve PowerShell uzak oturumunuz tamamladıktan sonra hello uç noktaları silin öneririz.**

Merhaba yordamları izlemelisiniz [tooyour StorSimple cihazı uzaktan bağlanma](storsimple-8000-remote-connect.md) tooset uzaktan iletişim, bulut uygulaması için ayarlama.

## <a name="connect-directly-toohello-cloud-appliance"></a>Toohello bulut uygulaması doğrudan bağlanın

Toohello bulut uygulaması da doğrudan bağlanabilirsiniz. tooconnect toohello bulut doğrudan dışındaki başka bir bilgisayardan Gereci Merhaba sanal ağ veya dış hello Microsoft Azure ortamı, ek uç noktalar oluşturmanız gerekir.

Aşağıdaki adımları toocreate genel bir uç nokta hello bulut aygıtınızdaki hello gerçekleştirin.

[!INCLUDE [Create public endpoints on a cloud appliance](../../includes/storsimple-8000-create-public-endpoints-cloud-appliance.md)]

Hello içinde başka bir sanal makineden sanal aynı bağlanmasını öneririz bu yöntem hello sanal ağınızdaki ortak uç noktaların sayısını en aza ağ. Bu durumda, Uzak Masaüstü oturumu aracılığıyla toohello sanal makineye bağlanmak ve yerel ağdaki başka bir Windows istemcisinde olduğu gibi sanal makine kullanımı için yapılandırın. Başlangıç bağlantı noktası zaten bilindiği için tooappend hello genel bağlantı noktası numarası gerekmez.

## <a name="work-with-hello-storsimple-cloud-appliance"></a>Merhaba StorSimple bulut uygulaması ile çalışma

Oluşturulan ve hello StorSimple bulut uygulaması yapılandırılmış göre Bununla çalışmaya hazır toostart demektir. Bulut gereçlerinde, tıpkı fiziksel bir StorSimple cihazında olduğu gibi birim kapsayıcıları, birimler ve yedekleme ilkeleriyle çalışabilirsiniz. Merhaba tek fark, toomake cihaz listenizden hello bulut uygulaması seçtiğinizden emin olmanızdır. Çok başvuran[hello StorSimple cihaz Yöneticisi hizmeti toomanage bulut uygulaması kullanmak](storsimple-8000-manager-service-administration.md) çeşitli yönetim görevlerini hello bulut uygulaması için hello hakkında adım adım yordamlar.

Merhaba aşağıdaki bölümlerde bazı hello bulut uygulaması ile çalışırken karşınıza hello farklar açıklanmaktadır.

### <a name="maintain-a-storsimple-cloud-appliance"></a>StorSimple Cloud Appliance’ın bakımını yapma

Yalnızca yazılım tabanlı bir cihaz olduğundan, bakım hello bulut uygulaması için en az olduğunda hello fiziksel aygıt için toomaintenance karşılaştırılan.

Bulut gerecini güncelleştiremezsiniz. Yazılım toocreate yeni bir bulut Gereci Hello en son sürümünü kullanın.


### <a name="storage-accounts-for-a-cloud-appliance"></a>Bulut gereci için depolama hesapları

Depolama hesapları hello StorSimple cihaz Yöneticisi hizmeti, hello bulut uygulaması ve hello fiziksel cihaz tarafından kullanılmak üzere oluşturulur. Depolama hesaplarınızı oluşturduğunuzda, hello kolay ad, bölge tanımlayıcısı kullanmanızı öneririz. Bu, o hello bölgenin tüm hello sistem bileşenleri tutarlı olduğundan emin olun yardımcı olur. Bulut uygulaması için tüm hello bileşenleri hello olduğunu önemli aynı bölge tooprevent performans sorunları.

Adım adım bir yordam için çok Git[depolama hesabı ekleme](storsimple-8000-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-cloud-appliance"></a>StorSimple Cloud Appliance’ı devre dışı bırakma

Bulut uygulaması devre dışı bıraktığınızda, hello eylemin hello VM ve hazırlandığında oluşturulan hello kaynakları siler. Merhaba bulut uygulaması devre dışı bırakıldıktan sonra olamaz tooits önceki durumuna geri. Merhaba bulut uygulaması devre dışı bırakmadan önce toostop emin olun veya istemciler ve bağımlı konakları silin.

Bulut uygulaması devre dışı bırakma hello eylemleri aşağıdaki sonuçları:

* Merhaba bulut uygulaması kaldırılır.
* Merhaba işletim sistemi disk ve hello bulut uygulaması için oluşturulan veri diskleri kaldırılır.
* Merhaba barındırılan hizmet ve sağlama işlemi sırasında oluşturulan sanal ağ korunur. Bunları kullanmıyorsanız, bunları el ile silmeniz gerekir.
* Merhaba bulut uygulaması için oluşturulan bulut anlık görüntüleri korunur.

Adım adım bir yordam için çok Git[devre dışı bırakın ve StorSimple Cihazınızı silme](storsimple-8000-deactivate-and-delete-device.md).

Hello bulut uygulaması dikey penceresinde hello StorSimple cihaz Yöneticisi hizmeti devre dışı olarak gösterilen hemen sonra aygıt listesinden hello hello bulut uygulaması silebilirsiniz **aygıtları** dikey.

### <a name="start-stop-and-restart-a-cloud-appliance"></a>Bulut gerecini başlatma, durdurma ve yeniden başlatma
Merhaba StorSimple fiziksel cihazının aksine, yoktur güç açık veya güç kapalı düğmesi toopush StorSimple bulut uygulaması üzerinde. Ancak, burada toostop gerekir ve hello bulut uygulaması yeniden durumlar olabilir.

Merhaba en kolay yolu, toostart, durdurma ve yeniden başlatma bulut uygulaması hello sanal makineler hizmeti dikey ' dir. Merhaba sanal makine hizmeti gidin. Hello listesinden VM'lerin hello VM karşılık gelen tooyour bulut uygulaması (aynı adı) tanımlamak ve hello VM adını tıklatın. Sanal makine dikey penceresine baktığınızda hello bulut Gereci durumudur **çalıştıran** çünkü oluşturulduktan sonra varsayılan olarak başlatılır. Bir sanal makineyi istediğiniz zaman başlatabilir, durdurabilir veya yeniden başlatabilirsiniz.

[!INCLUDE [Stop and restart cloud appliance](../../includes/storsimple-8000-stop-restart-cloud-appliance.md)]

### <a name="reset-toofactory-defaults"></a>Toofactory Varsayılanları sıfırla
Toostart üzerinden, bulut uygulaması ile istediğiniz karar verirseniz, devre dışı bırakın ve silin ve yeni bir tane oluşturun.

## <a name="fail-over-toohello-cloud-appliance"></a>Toohello bulut uygulaması başarısız
Olağanüstü Durum Kurtarma (DR) biridir Merhaba StorSimple bulut uygulaması hello senaryoları için tasarlanmıştır. Bu senaryoda, fiziksel StorSimple cihazı hello veya veri merkezinin tamamı kullanılamayabilir. Neyse ki, farklı bir konuma bulut Gereci toorestore işlemleri kullanabilirsiniz. DR sırasında hello kaynak aygıttan hello birim kapsayıcıları sahipliği değiştirir ve aktarılan toohello bulut uygulaması olan.

DR için Hello Önkoşullar şunlardır:

* Merhaba bulut uygulaması oluşturulur ve yapılandırılır.
* Merhaba birim kapsayıcı içindeki tüm hello birimleri çevrimdışı.
* Yük devretme hello birim kapsayıcısı sahip ilişkili bir bulut anlık görüntüsü.

> [!NOTE]
> * Bir bulut uygulaması için DR hello ikincil cihaz olarak kullanırken, hello 8010 30 TB Standard Storage ve 8020 64 TB Premium Storage sahip olduğunu göz önünde bulundurun. Merhaba daha yüksek kapasite 8020 bulut uygulaması bir DR senaryosuna daha uygun olabilir.

Adım adım bir yordam için çok Git[tooa bulut uygulaması başarısız](storsimple-8000-device-failover-cloud-appliance.md).

## <a name="delete-hello-cloud-appliance"></a>Merhaba bulut uygulaması Sil
Önceden yapılandırılmış ve kullanılan bir StorSimple bulut uygulaması ancak şimdi toostop kullanımı için Ücret tahakkuk etmesini istiyorsanız, hello bulut uygulaması durdurmanız gerekir. Durdurma hello bulut uygulaması hello VM kaldırır. Bu eylem, aboneliğinizde ücret tahakkuk etmesini engeller. Merhaba hello işletim sistemi için depolama ücretleri ve veri diskleri ancak devam eder.

Tüm hello toostop ücretlendirilen hello bulut uygulaması silmeniz gerekir. Merhaba bulut uygulaması tarafından oluşturulan toodelete hello yedeklemeleri devre dışı bırakma veya silme hello aygıt. Daha fazla bilgi için bkz. [StorSimple cihazını devre dışı bırakma ve silme](storsimple-8000-deactivate-and-delete-device.md).

[!INCLUDE [Delete a cloud appliance](../../includes/storsimple-8000-delete-cloud-appliance.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>İnternet bağlantısı sorunlarını giderme
Hiçbir bağlantı toohello Internet ise bir bulut uygulaması hello oluşturulurken hello Oluşturma adımı başarısız olur. tootroubleshoot Internet bağlantısı hataları hello Azure Portalı'ndaki adımları izleyerek hello gerçekleştirin:

1. [Azure’da bir Windows Server 2012 sanal makinesi oluşturun](/articles/virtual-machines/windows/quick-create-portal.md). Bu sanal makinenin kullanması gereken aynı depolama hesabı, VNet ve alt ağ, bulut uygulaması tarafından kullanılan hello. Varsa mevcut bir Azure kullanarak Windows Server ana Merhaba aynı depolama hesabı, VNet ve alt ağ, siz de tootroubleshoot hello Internet bağlantısı kullanabilirsiniz.
2. Önceki adım hello oluşturulan hello sanal makinenin uzak günlüğüne.
3. Merhaba sanal makine içinde bir komut penceresi açın (Win + R ve ardından türü `cmd`).
4. Başlangıç cmd hello komut isteminde aşağıdaki çalıştırın.

    `nslookup windows.net`
5. Varsa `nslookup` Internet bağlantısı hatası toohello StorSimple cihaz Yöneticisi hizmeti kaydetme gelen hello bulut uygulaması engelliyor sonra başarısız olur.
6. Bulut uygulaması hello tooyour sanal ağ tooensure olan gerekli hello mümkün tooaccess Azure siteleri gibi değişiklik _windows.net_.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[hello StorSimple cihaz Yöneticisi hizmeti toomanage bulut uygulaması kullanmak](storsimple-8000-manager-service-administration.md).
* Nasıl çok anlamak[bir yedeklemek kümesinden StorSimple birimini geri](storsimple-8000-restore-from-backup-set-u2.md).

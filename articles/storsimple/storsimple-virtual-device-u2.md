---
title: "aaaStorSimple sanal cihazını güncelleştirme 2 | Microsoft Docs"
description: "Nasıl toocreate, dağıtmak ve Microsoft Azure sanal ağında StorSimple sanal cihazı yönetmek öğrenin. (Güncelleştirme 2 tooStorSimple geçerlidir)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: f37752a5-cd0c-479b-bef2-ac2c724bcc37
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.openlocfilehash: 8d2a0520f1ed30ebec929c2bdabb4838691b8ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-virtual-device-in-azure"></a>Azure’da StorSimple sanal cihazını dağıtma ve yönetme
## <a name="overview"></a>Genel Bakış
Merhaba StorSimple 8000 serisi sanal cihaz, Microsoft Azure StorSimple çözümünüzle birlikte gelen ek bir yetenektir. Microsoft Azure sanal ağındaki bir sanal makinede Hello StorSimple sanal cihazı çalışır ve bunu tooback yukarı ve kopya veri ana bilgisayarlarını kullanabilirsiniz. Bu öğretici açıklar nasıl toodeploy ve azure'da sanal cihazı yönetmek ve geçerli tooall yazılım sürümü güncelleştirme 2 ve daha düşük çalıştıran hello sanal cihazlar.

#### <a name="virtual-device-model-comparison"></a>Sanal cihaz modeli karşılaştırması
Merhaba StorSimple sanal cihazı kullanılabilir iki modellerinde standart 8010 (önceden hello 1100 biliniyordu) ve premium 8020 (güncelleştirme 2'de sunulmuştur). Merhaba iki modellerin karşılaştırması aşağıdaki tabloda verilmiştir.

| Cihaz modeli | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Maksimum kapasite** |30 TB |64 TB |
| **Azure VM** |Standard_A3 (4 çekirdek, 7 GB bellek) |Standard_DS3 (4 çekirdek, 14 GB bellek) |
| **Sürüm uyumluluğu** |Güncelleştirme 2 ya da üst sürümü öncesini çalıştıran sürümler |Güncelleştirme 2 ya da üst sürümünü çalıştıran sürümler |
| **Bölge kullanılabilirliği** |Tüm Azure bölgeleri |Premium Depolama ve DS3 Azure VM’lerini destekleyen tüm Azure bölgeleri<br></br> Kullanım [bu listeyi](https://azure.microsoft.com/en-us/regions/services) toosee her iki *sanal makineleri > DS serisi* ve *depolama > Disk Depolama* Bölgenizde kullanılabilir. |
| **Depolama türü** |Yerel diskler için Azure Standard Storage kullanır.<br></br> Nasıl çok öğrenin[standart depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md) |Yerel diskler için Azure Premium Depolama kullanır<sup>2</sup> <br></br>Nasıl çok öğrenin[Premium depolama hesabı oluşturma](../storage/common/storage-premium-storage.md) |
| **İş yükü kılavuzu** |Yedeklerden dosya alma öğe düzeyi |Bulut geliştirme ve test senaryoları, düşük gecikme, daha yüksek performans iş yükleri <br></br>Olağanüstü durum kurtarma için ikincil cihaz |

<sup>1</sup> *önceden hello 1100 biliniyordu*.

<sup>2</sup> *hem 8010 hello ve 8020 hello bulut katmanı. hello fark hello aygıt yerel katmandadır hello yalnızca bulunmaktadır için Azure Standard Storage kullanır*.

Bu makalede, azure'da StorSimple sanal cihazı dağıtma hello adım adım işlemi açıklanmaktadır. Bu makaleyi okuduktan sonra şunları yapabilir olacaksınız:

* Nasıl hello sanal aygıt hello fiziksel CİHAZDAN farkı anlayın.
* Mümkün toocreate olması ve hello sanal aygıt yapılandırın.
* Toohello sanal cihazı bağlayın.
* Bilgi nasıl hello sanal aygıtla toowork.

Bu öğretici, güncelleştirme 2 ve üzeri çalıştıran tooall hello StorSimple sanal cihazlar geçerlidir.

## <a name="how-hello-virtual-device-differs-from-hello-physical-device"></a>Nasıl hello sanal aygıt hello fiziksel CİHAZDAN farkı
Merhaba StorSimple sanal cihazı, içinde bir Microsoft Azure sanal makine tek bir düğümde çalışan StorSimple, yalnızca yazılım tabanlı bir sürümüdür. hangi fiziksel cihazınız kullanılabilir değil ve yedeklemeler, öğe düzeyinde alma için uygundur hello sanal aygıt olağanüstü durum kurtarma senaryoları destekler olağanüstü durum kurtarma, şirket içi ve bulut geliştirme ve test senaryoları.

#### <a name="differences-from-hello-physical-device"></a>Merhaba fiziksel CİHAZDAN farklar
Merhaba aşağıdaki tabloda hello StorSimple sanal cihazı ve hello StorSimple fiziksel cihazı arasındaki bazı temel farklar gösterilmektedir.

|  | Fiziksel cihaz | Sanal cihaz |
| --- | --- | --- |
| **Konum** |Merhaba veri merkezinde yer alır. |Azure üzerinde çalışır. |
| **Ağ arabirimleri** |Altı ağ arabirimi bulunur: VERİ 0’dan VERİ 5’e. |Yalnızca bir ağ arabirimi bulunur: VERİ 0 |
| **Kayıt** |Merhaba yapılandırma adımı sırasında kaydedilir. |Kayıt ayrı bir görevdir. |
| **Hizmeti verileri şifreleme anahtarı** |Merhaba fiziksel cihazda yeniden oluşturun ve ardından hello yeni anahtarla hello sanal cihazı güncelleştirin. |Merhaba sanal CİHAZDAN yeniden oluşturamazsınız. |

## <a name="prerequisites-for-hello-virtual-device"></a>Merhaba sanal cihaz için Önkoşullar
Merhaba aşağıdaki bölümlerde, StorSimple sanal cihazınız için hello yapılandırma önkoşulları açıklanmaktadır. Önceki toodeploying sanal aygıt gözden hello [sanal cihaz kullanımıyla ilgili güvenlik konuları](storsimple-security.md#storsimple-virtual-device-security).

#### <a name="azure-requirements"></a>Azure gereksinimleri
Merhaba sanal cihaz sağlamadan önce Azure ortamınızda hazırlıklar aşağıdaki toomake hello gerekir:

* Merhaba sanal cihaz için [Azure üzerinde bir sanal ağ yapılandırma](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Premium Storage kullanıyorsanız, Premium Storage’ı destekleyen bir Azure bölgesinde sanal ağ oluşturmanız gerekir. Merhaba Premium depolama bölgeleri olan toohello satır için karşılık gelen bölgeler *Disk Depolama* hello listesinde [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/en-us/regions/services).
* Bunu kendi DNS sunucu adınızı belirtmek yerine Azure tarafından sağlanan önerilir toouse hello varsayılan DNS sunucusudur. DNS sunucusu adınız geçerli değilse veya hello DNS sunucusu mümkün tooresolve IP adreslerini doğru değilse, sanal cihazın hello hello oluşturma başarısız olur.
* Noktadan siteye ve siteden siteye isteğe bağlıdır, ancak gerekli değildir. İsterseniz, daha gelişmiş senaryolar için bu seçenekleri yapılandırabilirsiniz.
* Oluşturabileceğiniz [Azure sanal makineleri](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (barındırma sunucuları) hello sanal cihaz tarafından sunulan hello birimleri kullanabileceğiniz sanal ağda hello. Bu sunucular hello aşağıdaki gereksinimleri karşılamalıdır:                             

  * iSCSI Initiator yazılımı yüklü Windows veya Linux sanal makineleri olmalıdır.
  * Hello çalıştırması hello sanal aygıt aynı sanal ağ.
  * Merhaba hello sanal cihazın iç IP adresi üzerinden sanal cihazın hello mümkün tooconnect toohello iSCSI hedefi olabilir.
* Yapılandırdığınız destek iSCSI ve bulut üzerinde hello aynı trafiği için emin olun sanal ağ.

#### <a name="storsimple-requirements"></a>StorSimple gereksinimleri
Sanal cihaz oluşturmadan önce aşağıdaki güncelleştirmeleri tooyour Azure StorSimple hizmeti hello olun:

* Ekleme [erişim denetimi kayıtları](storsimple-manage-acrs.md) hello toobe ana bilgisayar sunucuları sanal cihazınız için uygulayacağınız VM'ler için.
* Kullanım bir [depolama hesabı](storsimple-manage-storage-accounts.md#add-a-storage-account) hello içinde hello sanal aygıt aynı bölgede. Farklı bölgelerdeki Depolama hesapları performansın düşmesine neden olabilir. Merhaba sanal cihazla standart veya Premium depolama hesabı kullanabilirsiniz. Hakkında daha fazla bilgi toocreate bir [standart depolama hesabı](../storage/common/storage-create-storage-account.md) veya [Premium depolama hesabı](../storage/common/storage-premium-storage.md)
* Merhaba, verileriniz için kullanılan sanal cihazın oluşturulması için farklı bir depolama hesabı kullanın. Aynı depolama hesabındaki performansın düşmesine neden hello kullanma.

Başlamadan önce bilgilerini aşağıdaki hello sahip olduğunuzdan emin olun:

* Klasik Azure portalı hesabınıza erişim kimlik bilgileri.
* Merhaba hizmet verileri şifreleme anahtarı fiziksel cihazınızdan kopyası.

## <a name="create-and-configure-hello-virtual-device"></a>Oluşturma ve hello sanal aygıt yapılandırma
Bu yordamları gerçekleştirmeden önce hello karşıladığınızdan emin olun [hello sanal cihaz için Önkoşullar](#prerequisites-for-the-virtual-device).

Sanal ağ oluşturduktan, StorSimple Yöneticisi hizmeti yapılandırdıktan ve fiziksel StorSimple Cihazınızı hello hizmetine kayıtlı sonra aşağıdaki adımları toocreate hello kullanın ve StorSimple sanal cihazı yapılandırın.

### <a name="step-1-create-a-virtual-device"></a>1. Adım: Sanal cihaz oluşturma
Aşağıdaki adımları toocreate hello StorSimple sanal cihazı hello gerçekleştirin.

[!INCLUDE [Create a virtual device](../../includes/storsimple-create-virtual-device-u2.md)]

Bu adımda hello sanal aygıt Hello oluşturulmasını başarısız olursa, bağlantı toohello Internet olmayabilir. Daha fazla bilgi için çok Git[Internet bağlantı hatalarını giderme](#troubleshoot-internet-connectivity-errors) sanal cihazı oluştururken.

### <a name="step-2-configure-and-register-hello-virtual-device"></a>Adım 2: Yapılandırma ve hello sanal cihaz kaydetme
Bu yordamı başlatmadan önce hello hizmet verileri şifreleme anahtarının bir kopyasına sahip olduğunuzdan emin olun. Merhaba hizmet verileri şifreleme anahtarı, ilk StorSimple Cihazınızı yapılandırdığınız belirtildiği toosave olduğunuz seçtiğinizde oluşturulmuştur, güvenli bir konumda. Hello hizmeti veri şifreleme anahtarının bir kopyası yoksa, Yardım için Microsoft Support başvurmanız gerekir.

Aşağıdaki adımları tooconfigure hello gerçekleştirmek ve StorSimple sanal Cihazınızı kaydedin.

[!INCLUDE [Configure and register a virtual device](../../includes/storsimple-configure-register-virtual-device.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>3. adım: (İsteğe bağlı) Değiştir hello cihaz yapılandırma ayarları
Merhaba aşağıdaki bölümde, toouse CHAP, StorSimple Snapshot Manager veya hello cihaz Yöneticisi parolasını değiştirmek istiyorsanız hello StorSimple sanal cihaz için gerekli hello cihaz yapılandırma ayarları açıklanmaktadır.

#### <a name="configure-hello-chap-initiator"></a>Merhaba CHAP başlatıcısını yapılandırma
Bu parametre sanal cihazınızın (hedef) tooaccess hello birimleri çalıştığınız hello başlatıcılardan (sunucu) beklediği hello kimlik bilgilerini içerir. Hello başlatıcıları CHAP kullanıcı adı ve CHAP parolası tooidentify kendilerini tooyour cihaz bu kimlik doğrulaması sırasında sağlar. Ayrıntılı adımlar için çok Git[cihazınız için CHAP yapılandırma](storsimple-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Merhaba CHAP hedefini yapılandırma
Bu parametre CHAP etkin Başlatıcı karşılıklı veya çift yönlü kimlik doğrulama istediğinde sanal cihazınızın kullandığı hello kimlik bilgilerini içerir. Sanal cihazınız bir ters CHAP kullanıcı adı ve ters CHAP parolası tooidentify kendisini toohello Başlatıcı bu kimlik doğrulama işlemi sırasında kullanır. CHAP hedefi ayarlarının genel ayarlar olduğunu unutmayın. Bunlar uygulandığında tüm hello birimleri bağlı toohello depolama sanal aygıt CHAP kimlik doğrulamasını kullanır. Ayrıntılı adımlar için çok Git[cihazınız için CHAP yapılandırma](storsimple-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Merhaba StorSimple Snapshot Manager parolasını yapılandırma
StorSimple Snapshot Manager yazılımı Windows ana bilgisayarınıza bulunur ve StorSimple Cihazınızı hello form yerel ve bulut anlık görüntüleri toomanage yedeklerini yöneticilerinin sağlar.

> [!NOTE]
> Merhaba sanal cihaz için Windows ana bilgisayarınız bir Azure sanal makinesidir.
>
>

Bir aygıt hello StorSimple Snapshot Manager yapılandırırken istenir tooprovide depolama Cihazınızı StorSimple cihazı IP adresi ve parola tooauthenticate hello. Ayrıntılı adımlar için çok Git[yapılandırma StorSimple Snapshot Manager parolası](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Değişiklik hello cihaz Yöneticisi parolası
Kullandığınızda hello Windows PowerShell arabirimi tooaccess sanal aygıt Merhaba, gerekli tooenter bir cihaz Yöneticisi parolası olacaktır. Verilerinizin Hello güvenlik için önce bu parola gerekli toochange olan hello sanal aygıt kullanılabilir. Ayrıntılı adımlar için çok Git[cihaz Yöneticisi parolasını yapılandırma](storsimple-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-virtual-device"></a>Toohello sanal cihaza uzaktan bağlanma
Uzaktan erişim tooyour hello Windows PowerShell arabirimi üzerinden sanal bir aygıtı varsayılan olarak etkin değildir. Merhaba sanal cihazda uzaktan yönetimi tooenable önce gerekir ve ardından sanal Cihazınızı kullanılan tooaccess olacak hello istemcisinde etkinleştirin.

Merhaba iki adımlı işlem tooconnect uzaktan aşağıda ayrıntılı olarak verilmiştir.

### <a name="step-1-configure-remote-management"></a>1. Adım: Uzaktan yönetimi yapılandırma
Aşağıdaki adımları tooconfigure uzaktan yönetimi, StorSimple sanal cihazınız için başlangıç gerçekleştirin.

[!INCLUDE [Configure remote management via HTTP for virtual device](../../includes/storsimple-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-virtual-device"></a>2. adım: Hello sanal cihaza uzaktan erişim
Merhaba StorSimple cihaz yapılandırma sayfasında uzaktan yönetimi etkinleştirdikten sonra Windows PowerShell uzaktan iletişim tooconnect toohello sanal aygıt hello içinde başka bir sanal makineden kullanabilirsiniz aynı sanal ağı; Örneğin, yapılandırılmış ve tooconnect iSCSI kullanılan VM hello ana bilgisayardan bağlanabilir. Çoğu dağıtımda zaten bir ortak uç nokta tooaccess ana bilgisayarınız hello sanal cihaza erişmek için kullanabileceğiniz VM açtığınız.

> [!WARNING]
> **Gelişmiş güvenlik için HTTPS toohello uç noktaları bağlanırken kullanmak ve PowerShell uzak oturumunuz tamamladıktan sonra hello uç noktaları silin öneririz.**
>
>

Merhaba yordamlarını izlemelisiniz [tooyour StorSimple cihazı uzaktan bağlanma](storsimple-remote-connect.md) tooset sanal cihazınız için uzaktan iletişim kurma.

## <a name="connect-directly-toohello-virtual-device"></a>Toohello sanal cihaza doğrudan bağlanma
Toohello sanal cihazı da doğrudan bağlanabilirsiniz. Toocreate aşağıdaki yordamı hello açıklandığı gibi ek uç noktaları ihtiyacınız toohello sanal aygıt hello sanal ağ veya dış hello Microsoft Azure ortamı dışındaki başka bir bilgisayardan doğrudan tooconnect istiyorsanız.

Merhaba sanal cihazda adımları toocreate genel bir uç nokta aşağıdaki hello gerçekleştirin.

[!INCLUDE [Create public endpoints on a virtual device](../../includes/storsimple-create-public-endpoints-virtual-device.md)]

Hello içinde başka bir sanal makineden sanal aynı bağlanmasını öneririz bu yöntem hello sanal ağınızdaki ortak uç noktaların sayısını en aza ağ. Bu yöntemi kullandığınızda, yalnızca Uzak Masaüstü oturumu aracılığıyla toohello sanal makineye bağlanmak ve yerel ağdaki başka bir Windows istemcisinde olduğu gibi sanal makine kullanımı için yapılandırın. Başlangıç bağlantı noktası zaten biliniyor olacağından tooappend hello genel bağlantı noktası numarası gerekmez.

## <a name="work-with-hello-storsimple-virtual-device"></a>Merhaba StorSimple sanal cihazı ile çalışma
Oluşturulan ve hello StorSimple sanal cihazı yapılandırılmış göre Bununla çalışmaya hazır toostart demektir. Bir fiziksel StorSimple cihazında gibi bir sanal cihazdaki birim kapsayıcıları, birimler ve yedekleme ilkeleri ile çalışabilirsiniz; Merhaba tek fark, toomake cihaz listenizden hello sanal cihazı seçtiğinizden emin olmanızdır. Çok başvuran[hello StorSimple Yöneticisi hizmet toomanage sanal cihazı kullanmak](storsimple-manager-service-administration.md) çeşitli yönetim görevlerini hello sanal cihaz için hello hakkında adım adım yordamlar.

Merhaba aşağıdaki bölümlerde bazı hello sanal cihazla çalışırken karşınıza çıkacak hello farklar açıklanmaktadır.

### <a name="maintain-a-storsimple-virtual-device"></a>StorSimple sanal cihazına bakım yapma
Yalnızca yazılım tabanlı bir cihaz olduğundan, bakım hello sanal cihaz için en az olduğunda hello fiziksel aygıt için toomaintenance karşılaştırılan. Seçenekler aşağıdaki hello vardır:

* **Yazılım güncelleştirmelerini** – hello yazılımın, herhangi bir güncelleştirme durum iletisi birlikte güncelleştirildiği son hello tarihi görüntüleyebilirsiniz. Merhaba kullanabilirsiniz **Güncelleştirmeleri tara** yeni güncelleştirmeleri toocheck istiyorsanız hello sayfa tooperform hello altındaki el ile tarama düğmesi. Güncelleştirmeler varsa, tıklatın **Güncelleştirmeleri Yükle** tooinstall. Merhaba sanal cihazda tek bir arabirim olduğundan, bu olacağını ufak hizmet kesintisi güncelleştirmeler uygulandığında anlamına gelir. Merhaba sanal aygıt kapatılır ve (gerekirse) yeniden tooapply çıkarılan herhangi bir güncelleştirme. Adım adım bir yordam için çok Git[Cihazınızı güncelleştirmek](storsimple-update-device.md#install-regular-updates-via-the-azure-classic-portal).
* **Destek Paketi** – oluşturabilir ve karşıya yükleme destek paketi toohelp Microsoft Support sanal cihazınızla ilgili sorunları sorun giderme. Adım adım bir yordam için çok Git[oluşturmak ve bir destek paketi yönetmek](storsimple-create-manage-support-package.md).

### <a name="storage-accounts-for-a-virtual-device"></a>Sanal cihaz için depolama hesapları
Depolama hesapları kullanılmak üzere hello StorSimple Yöneticisi hizmeti, hello sanal cihaz ve hello fiziksel aygıt tarafından oluşturulur. Depolama hesaplarınızı oluşturduğunuzda, bir bölge kullanmanızı öneririz hello kolay ad toohelp tanımlayıcıda o hello bölgenin tüm hello sistem bileşenleri tutarlı olduğundan emin olun. Sanal cihaz için tüm bileşenler hello aynı bölge tooprevent performans sorunlarını hello önemlidir.

Adım adım bir yordam için çok Git[depolama hesabı ekleme](storsimple-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-virtual-device"></a>StorSimple sanal cihazını devre dışı bırakma
Sanal cihazı devre dışı bırakma hello VM ve hazırlandığında oluşturulan hello kaynakları siler. Merhaba sanal cihazı devre dışı bırakıldıktan sonra olamaz tooits önceki durumuna geri. Merhaba sanal cihazı devre dışı bırakmadan önce toostop emin olun veya istemciler ve bağımlı konakları silin.

Sanal cihazı devre dışı bırakma hello eylemleri aşağıdaki sonuçları:

* Merhaba sanal cihaz kaldırılır.
* Merhaba işletim sistemi disk ve hello sanal cihaz için oluşturulan veri diskleri kaldırılır.
* Merhaba barındırılan hizmet ve sağlama işlemi sırasında oluşturulan sanal ağ korunur. Bunları kullanmıyorsanız, bunları el ile silmeniz gerekir.
* Merhaba sanal cihaz için oluşturulan bulut anlık görüntüleri korunur.

Adım adım bir yordam için çok Git[devre dışı bırakın ve StorSimple Cihazınızı silme](storsimple-deactivate-and-delete-device.md).

Hello sanal aygıt hello StorSimple Yöneticisi hizmet sayfasında devre dışı olarak gösterilen hemen sonra aygıt listesinden hello hello sanal aygıt silebilirsiniz **aygıtları** sayfası.

### <a name="start-stop-and-restart-a-virtual-device"></a>Sanal cihazı başlatma, durdurma ve yeniden başlatma
Merhaba StorSimple fiziksel cihazının aksine, yoktur güç açık veya güç kapalı düğmesi toopush StorSimple sanal cihazı üzerinde. Ancak, burada toostop gerekir ve hello sanal aygıt yeniden başlatma durumlar olabilir. Örneğin, bazı güncelleştirmeler VM'nin bu hello toofinish hello güncelleştirme işlemini yeniden gerektirebilir. Merhaba en kolay yolu, toostart, durdurma ve yeniden başlatma sanal cihazı toouse hello sanal makineleri yönetme Konsolu'nu ' dir.

Yönetim Konsolu hello baktığınızda hello sanal aygıt durumudur **çalıştıran** çünkü oluşturulduktan sonra varsayılan olarak başlatılır. Bir sanal makineyi istediğiniz zaman başlatabilir, durdurabilir veya yeniden başlatabilirsiniz.

[!INCLUDE [Stop and restart virtual device](../../includes/storsimple-stop-restart-virtual-device.md)]

### <a name="reset-toofactory-defaults"></a>Toofactory Varsayılanları sıfırla
Yalnızca toostart üzerinden sanal cihazınızla istediğiniz karar verirseniz, yalnızca devre dışı bırakın ve silin ve yeni bir tane oluşturun. Yalnızca fiziksel cihazınız sıfırlandığında gibi, yeni sanal Cihazınızda yüklü güncelleştirme sahip olmaz; Bu nedenle, kullanmadan önce güncelleştirmeleri emin toocheck olun.

## <a name="fail-over-toohello-virtual-device"></a>Toohello sanal aygıt başarısız
Olağanüstü Durum Kurtarma (DR), StorSimple sanal cihazın tasarlanma hello hello senaryoları biridir. Bu senaryoda, fiziksel StorSimple cihazı hello veya veri merkezinin tamamı kullanılamayabilir. Neyse ki, farklı bir konuma sanal aygıt toorestore işlemlerini kullanabilirsiniz. DR sırasında hello kaynak aygıttan hello birim kapsayıcıları sahipliği değiştirme ve aktarılan toohello sanal aygıt olan. Merhaba DR için Önkoşullar hello sanal aygıt oluşturduktan ve yapılandırdıktan, hello birim kapsayıcı içindeki tüm hello birimlerin çevrimdışına alınması ve hello birim kapsayıcısının ilişkili bir sahip olduğunu olduğundan bulut anlık görüntüsü.

> [!NOTE]
> * Sanal cihazı DR için hello ikincil cihaz olarak kullanırken, hello 8010 30 TB Standard Storage ve 8020 64 TB Premium Storage sahip olduğunu göz önünde bulundurun. Merhaba daha yüksek kapasite 8020 sanal cihazı bir DR senaryosuna daha uygun olabilir.
> * Yük devretme olamaz veya kopya çalıştıran bir CİHAZDAN güncelleştirme 1 yazılımı öncesini çalıştıran 2 tooa cihaz güncelleştirin. Ancak güncelleştirme 1 (1.1 veya 1.2) çalıştıran güncelleştirme 2 tooa cihazda çalışan bir aygıt başarısız olabilir
>
>

Adım adım bir yordam için çok Git[yük devretme tooa sanal aygıt](storsimple-device-failover-disaster-recovery.md#fail-over-to-a-storsimple-virtual-device).

## <a name="shut-down-or-delete-hello-virtual-device"></a>Kapatıldı veya hello sanal cihazı Sil
Önceden yapılandırılmış ve sanal bir StorSimple kullanılan aygıt ancak şimdi toostop kullanımı için Ücret tahakkuk etmesini istiyorsanız, hello sanal cihazı kapatmanız yeterlidir. Merhaba sanal cihazı kapatmak, işletim sistemi veya veri disklerinin depolama silmez. Aboneliğinize tahakkuk eden ücretleri durdurur, ancak hello işletim sistemi için depolama ücretleri ve veri diskleri devam eder.

Silme veya hello sanal cihazı kapatmak, olarak görünür **çevrimdışı** hello cihazlar sayfasında hello StorSimple Yöneticisi hizmeti. Toodeactivate seçin veya toodelete hello sanal cihaz tarafından oluşturulan hello yedekler de istiyorsanız hello aygıt silin. Daha fazla bilgi için bkz. [StorSimple cihazını devre dışı bırakma ve silme](storsimple-deactivate-and-delete-device.md).

[!INCLUDE [Shut down a virtual device](../../includes/storsimple-shutdown-virtual-device.md)]

[!INCLUDE [Delete a virtual device](../../includes/storsimple-delete-virtual-device.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>İnternet bağlantısı sorunlarını giderme
Hiçbir bağlantı toohello Internet ise sanal cihazı hello oluşturulurken hello Oluşturma adımı başarısız olur. tootroubleshoot hello hatası Internet bağlantısı nedeniyle ise hello Klasik Azure Portalı'ndaki adımları izleyerek hello gerçekleştirin:

1. Azure’da bir Windows server 2012 sanal makinesi oluşturun. Bu sanal makinenin kullanması gereken aynı depolama hesabı, sanal ağ ve sanal cihazınız tarafından kullanılan alt ağ hello. Var olan zaten varsa Azure kullanarak Windows Server ana Merhaba aynı depolama hesabı, Vnet ve alt ağ, siz de tootroubleshoot hello Internet bağlantısı kullanabilirsiniz.
2. Önceki adım hello oluşturulan hello sanal makinenin uzak günlüğüne.
3. Merhaba sanal makine içinde bir komut penceresi açın (Win + R ve ardından türü `cmd`).
4. Başlangıç cmd hello komut isteminde aşağıdaki çalıştırın.

    `nslookup windows.net`
5. Varsa `nslookup` Internet bağlantısı hatası toohello StorSimple Yöneticisi hizmeti kaydetme hello sanal aygıt engelliyor sonra başarısız olur.
6. Mümkün tooaccess "windows.net" gibi Azure siteleri sanal aygıt hello tooyour sanal ağ tooensure olan hello gerekli değişiklikleri yapın.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[hello StorSimple Yöneticisi hizmet toomanage sanal cihazı kullanmak](storsimple-manager-service-administration.md).
* Nasıl çok anlamak[bir yedeklemek kümesinden StorSimple birimini geri](storsimple-restore-from-backup-set.md).

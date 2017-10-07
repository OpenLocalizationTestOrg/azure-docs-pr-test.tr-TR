---
title: "aaaStorSimple Yöneticisi Hizmeti Yönetimi | Microsoft Docs"
description: "Klasik Azure portalı kullanarak StorSimple Cihazınızı StorSimple Yöneticisi hizmeti hello toomanage hello nasıl öğrenin."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2586582e-d85c-42e1-afb3-be734c1c0461
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 695ebbb785590a0e3d6de4c73125f65b16dcb776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooadminister-your-storsimple-device"></a>StorSimple Cihazınızı Hello StorSimple Yöneticisi hizmet tooadminister kullanın
## <a name="overview"></a>Genel Bakış
Bu makalede hello StorSimple Yöneticisi hizmet arabirimden nasıl tooconnect tooit çeşitli seçenekleri hello ve bu kullanıcı Arabirimi gerçekleştirilebilecek toohello belirli iş akışları giden bağlantılar dahil olmak üzere, açıklanmaktadır. Bu kılavuz, geçerli tooboth olur; Merhaba StorSimple fiziksel ve sanal cihaz hello.

Bu makaleyi okuduktan sonra öğreneceksiniz:

* TooStorSimple Yöneticisi hizmetine bağlanın
* Merhaba StorSimple Yöneticisi kullanıcı Arabirimi gidin
* StorSimple Cihazınızı hello StorSimple Yöneticisi hizmeti aracılığıyla yönetmek

## <a name="connect-toostorsimple-manager-service"></a>TooStorSimple Yöneticisi hizmetine bağlanın
Merhaba StorSimple Yöneticisi hizmeti Microsoft Azure üzerinde çalışır ve toomultiple StorSimple cihazları bağlanır. Bu aygıtlar bir tarayıcı toomanage çalıştıran merkezi bir Microsoft Azure Klasik portalı kullanın. tooconnect toohello StorSimple Yöneticisi hizmet hello aşağıdaki.

#### <a name="tooconnect-toohello-service"></a>tooconnect toohello hizmeti
1. Çok gidin[https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. Toohello Microsoft Azure Klasik portalında (Merhaba sağ üst tarafında hello bölmesinin bulunur), Microsoft hesabı kimlik bilgilerinizi kullanarak oturum açın.
3. Sol gezinti bölmesinde tooaccess hello StorSimple Yöneticisi hizmeti hello kaydırın.

## <a name="navigate-storsimple-manager-service-ui"></a>StorSimple Yöneticisi hizmeti kullanıcı Arabirimi gidin
Aşağıdaki tablonun hello UI gösterilen hello StorSimple Yöneticisi hizmeti için gezinme hiyerarşisi hello.

* **StorSimple Yöneticisi** giriş sayfası toohello UI hizmet düzeyi sayfaları geçerli tooall aygıtları bir hizmet kapsamındaki alır.
* **Aygıtları** sayfa toohello aygıt – düzeyi kullanıcı Arabirimi sayfalarını geçerli tooa belirli cihaz alır.
* **Birim kapsayıcıları** sayfa bir cihaz ile ilişkili tüm hello birimleri gösterir toohello birimi sayfası alır.

#### <a name="storsimple-manager-service-navigational-hierarchy"></a>StorSimple Yöneticisi hizmeti gezinme hiyerarşisi
| Giriş sayfası | Hizmet düzeyi sayfaları | Cihaz düzeyinde sayfaları | Cihaz düzeyinde sayfaları |
| --- | --- | --- | --- |
| StorSimple Yöneticisi hizmeti |Hizmet panosu |Cihaz Pano | |
| Aygıtları → |İzleme | | |
| Yedekleme kataloğu |Birim containers→ |Birimleri | |
| (Hizmeti) yapılandırma |Yedekleme ilkeleri | | |
| İşler |(Cihaz) yapılandırma | | |
| Uyarılar |Bakım | | |

![Video var](./media/storsimple-manager-service-administration/Video_icon.png) **Video var**

toowatch hello StorSimple Yöneticisi hizmeti kullanıcı arabirimi anlatan bir videoyu tıklatın [burada](https://azure.microsoft.com/documentation/videos/storsimple-manager-service-overview/).

## <a name="administer-storsimple-device-using-storsimple-manager-service"></a>StorSimple Yöneticisi hizmetini kullanarak StorSimple cihazı yönetme
Merhaba aşağıdaki tabloda tüm hello genel yönetim görevleri ve StorSimple Yöneticisi hizmeti kullanıcı Arabirimi hello içinde gerçekleştirilebilir karmaşık iş akışları bir özetini gösterir. Bu görevler üzerinde bunlar başlatılan hello kullanıcı Arabirimi sayfalarını göre düzenlenir.

Her bir iş akışı hakkında daha fazla bilgi için hello tablosundaki hello uygun yordamı tıklatın.

#### <a name="storsimple-manager-workflows"></a>StorSimple Yöneticisi iş akışları
| Bu toodo isterseniz... | Toothis UI sayfa Git... | Bu yordamı kullanın. |
| --- | --- | --- |
| Hizmet oluşturma</br>Bir hizmeti silin</br>Hizmet kayıt anahtarını alın</br>Hizmet kayıt anahtarını yeniden oluşturma |StorSimple Yöneticisi hizmeti |[StorSimple Yöneticisi hizmet dağıtma](storsimple-manage-service.md) |
| Değişiklik hello hizmet verileri şifreleme anahtarı</br>Merhaba işlem günlüklerini görüntüle |StorSimple Yöneticisi hizmet → Panosu |[Merhaba StorSimple Yöneticisi hizmet panosunu kullanma](storsimple-service-dashboard.md) |
| Bir cihazı devre dışı</br>Bir aygıtı silme |StorSimple Yöneticisi hizmeti → cihazları |[Bir cihazı silmek veya devre dışı bırakma](storsimple-deactivate-and-delete-device.md) |
| Olağanüstü durum kurtarma ve aygıt yük devretme hakkında bilgi edinin</br>Yük devretme tooa fiziksel cihaz</br>Yük devretme tooa sanal cihaz</br>İş sürekliliği olağanüstü durum kurtarma (BCDR) |StorSimple Yöneticisi hizmeti → cihazları |[StorSimple cihazınız için yük devretme ve olağanüstü durum kurtarma](storsimple-device-failover-disaster-recovery.md) |
| Bir birim için liste yedeklemeleri</br>Bir yedekleme kümesi seçin</br>Bir yedekleme kümesi Sil |StorSimple Yöneticisi hizmet → yedekleme kataloğu |[Yedeklemeleri yönetme](storsimple-manage-backup-catalog.md) |
| Bir birimi kopyalama |StorSimple Yöneticisi hizmet → yedekleme kataloğu |[Bir birimi kopyalama](storsimple-clone-volume.md) |
| Bir yedekleme kümesi geri yükleme |StorSimple Yöneticisi hizmet → yedekleme kataloğu |[Bir yedekleme kümesi geri yükleme](storsimple-restore-from-backup-set.md) |
| Depolama hesapları hakkında</br>Depolama hesabı ekleme</br>Bir depolama hesabı Düzenle</br>Bir depolama hesabını silme</br>Depolama hesaplarının anahtar döndürme |StorSimple Yöneticisi hizmet → yapılandırın |[Depolama hesaplarını yönetme](storsimple-manage-storage-accounts.md) |
| Bant genişliği şablonları hakkında</br>Bant genişliği şablonu ekleyin</br>Bant genişliği Şablonu Düzenle</br>Bant genişliği Şablonu Sil</br>Varsayılan bant genişliği şablonu kullanın</br>Belirli bir zamanda başlatır süren bir bant genişliği şablonu oluştur |StorSimple Yöneticisi hizmet → yapılandırın |[Bant genişliği şablonlarını yönetme](storsimple-manage-bandwidth-templates.md) |
| Erişim denetimi kayıtları hakkında</br>Bir erişim denetimi kaydı oluşturun</br>Bir erişim denetimi kaydı Düzenle</br>Bir erişim denetimi kaydını sil |StorSimple Yöneticisi hizmet → yapılandırın |[Erişim denetimi kayıtlarını yönetme](storsimple-manage-acrs.md) |
| İş ayrıntılarını görüntüleme</br>Bir işi iptal etme |StorSimple Yöneticisi hizmet → işleri |[İşleri yönetme](storsimple-manage-jobs.md) |
| Uyarı bildirimleri alma</br>Uyarıları yönetme</br>Uyarıları gözden geçirin |StorSimple Yöneticisi hizmet → uyarıları |[StorSimple uyarıları görüntüleyin ve yönetin](storsimple-manage-alerts.md) |
| Bağlı başlatıcıları görüntüleyin</br>Merhaba cihaz seri numarasını Bul</br>Merhaba hedef IQN Bul |StorSimple Yöneticisi hizmet → cihazların → Panosu |[Merhaba StorSimple cihaz Pano kullanın](storsimple-device-dashboard.md) |
| İzleme grafikleri oluşturma |StorSimple Yöneticisi hizmet → cihazların → izleme |[StorSimple Cihazınızı izleme](storsimple-monitor-device.md) |
| Birim kapsayıcısı Ekle</br>Birim kapsayıcısı değiştirme</br>Birim kapsayıcısı Sil |StorSimple Yöneticisi hizmet → cihazların → birim kapsayıcıları |[Birim kapsayıcıları yönetme](storsimple-manage-volume-containers.md) |
| Birim Ekle</br>Bir birim değiştirme</br>Bir birim çevrimdışı duruma getirin</br>Bir birim Sil</br>Bir birimi izleyin |StorSimple Yöneticisi hizmet → cihazların → birim kapsayıcıları → birimleri |[Birimleri yönetme](storsimple-manage-volumes.md) |
| Cihaz ayarlarını değiştirme</br>Saat ayarlarını değiştirme</br>DNS.md ayarlarını değiştirme</br>Ağ arabirimleri yapılandırın |StorSimple Yöneticisi hizmet → cihazların → yapılandırın |[StorSimple cihazınız için aygıt yapılandırmasını Değiştir](storsimple-modify-device-config.md) |
| Görünümü web proxy ayarları |StorSimple Yöneticisi hizmet → cihazların → yapılandırın |[Cihazınız için Web Proxy'yi Yapılandır](storsimple-configure-web-proxy.md) |
| Cihaz Yöneticisi parolasını değiştirme</br>StorSimple Snapshot Manager parolasını değiştirme |StorSimple Yöneticisi hizmet → cihazların → yapılandırın |[StorSimple parolalarını değiştirme](storsimple-change-passwords.md) |
| Uzaktan Yönetimi yapılandırma |StorSimple Yöneticisi hizmet → cihazların → yapılandırın |[Tooyour StorSimple cihazı uzaktan bağlanma](storsimple-remote-connect.md) |
| Uyarı ayarlarını yapılandırma |StorSimple Yöneticisi hizmet → cihazların → yapılandırın |[StorSimple uyarıları görüntüleyin ve yönetin](storsimple-manage-alerts.md) |
| StorSimple cihazınız için CHAP yapılandırma |StorSimple Yöneticisi hizmet → cihazların → yapılandırın |[StorSimple cihazınız için CHAP yapılandırma](storsimple-configure-chap.md) |
| Yedekleme ilkesi ekleme</br>Ekleyin veya bir zamanlama değiştirin</br>Bir yedekleme ilkesi silme</br>El ile yedekleyin</br>Birden çok birimleri ve zamanlamaları özel bir yedekleme ilkesi oluşturma |StorSimple Yöneticisi hizmeti → cihazların → yedekleme ilkeleri |[Yedekleme ilkelerini yönetme](storsimple-manage-backup-policies.md) |
| Aygıt denetleyicileri Durdur</br>Cihaz denetleyicilerini yeniden başlatın</br>Aygıt denetleyicileri Kapat</br>Aygıt toofactory Varsayılanları sıfırla</br>(Yalnızca şirket içi cihaz için yukarıdaki dışında) |StorSimple Yöneticisi hizmet → cihazların → bakım |[StorSimple cihaz denetleyicisi yönetme](storsimple-manage-device-controller.md) |
| StorSimple donanım bileşenleri hakkında bilgi edinin</br>Donanım durumunu izleyin</br>(Yalnızca şirket içi cihaz için yukarıdaki dışında) |StorSimple Yöneticisi hizmet → cihazların → bakım |[İzleyici donanım bileşenleri](storsimple-monitor-hardware-status.md) |
| Bir destek paketi oluştur |StorSimple Yöneticisi hizmet → cihazların → bakım |[Oluşturma ve Destek Paketi yönetme](storsimple-create-manage-support-package.md) |
| Yazılım güncelleştirmelerini yükle |StorSimple Yöneticisi hizmet → cihazların → bakım |[Cihazınızı güncelleştirme](storsimple-update-device.md) |

## <a name="next-steps"></a>Sonraki adımlar
StorSimple Cihazınızı günlük işlemleri hello veya herhangi bir donanım bileşenlerinden biri ile herhangi bir sorunla karşılaşırsanız, bakın:

* [İşletimsel bir aygıtı sorun giderme](storsimple-troubleshoot-operational-device.md)
* [Gösterge LED'lerinin İzleme StorSimple kullanın](storsimple-monitoring-indicators.md)

Merhaba sorunları çözümlenemiyor ve toocreate bir hizmet isteği ihtiyacınız varsa çok başvuran[Microsoft Destek birimine başvurun](storsimple-contact-microsoft-support.md).


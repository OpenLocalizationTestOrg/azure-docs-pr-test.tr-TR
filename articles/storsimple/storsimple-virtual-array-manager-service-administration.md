---
title: "Azure StorSimple Yöneticisi Sanal dizinin yönetim aaaMicrosoft | Microsoft Docs"
description: "Azure portal, StorSimple sanal dizinin hello StorSimple Aygıt Yöneticisi'ni hizmetinde kullanarak şirket içi toomanage hello nasıl öğrenin."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 958244a5-f9f5-455e-b7ef-71a65558872e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 1fabf9ca524b461266346a6cabf49aef772032ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooadminister-your-storsimple-virtual-array"></a>StorSimple sanal dizinizi Hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanın
![Kurulum işlem akışı](./media/storsimple-virtual-array-manager-service-administration/manage4.png)

## <a name="overview"></a>Genel Bakış
Bu makalede tooconnect tooit ve çeşitli kullanılabilir seçenekleri ve bağlantıları toohello belirli iş akışları sağlayan hello bu kullanıcı Arabirimi nasıl gerçekleştirilebilir dahil olmak üzere, hello StorSimple cihaz Yöneticisi hizmeti arabirimi açıklanmaktadır.

Bu makaleyi okuduktan sonra şunları öğrenmiş olacaksınız nasıl yapılır:

* Toohello StorSimple cihaz Yöneticisi hizmetine bağlanın
* Merhaba StorSimple cihaz Yöneticisi kullanıcı Arabirimi gidin
* StorSimple sanal dizinizi hello StorSimple cihaz Yöneticisi hizmeti aracılığıyla yönetmek

> [!NOTE]
> tooview hello yönetim seçenekleri hello StorSimple 8000 serisi aygıt için Git çok[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).
> 
> 

## <a name="connect-toohello-storsimple-device-manager-service"></a>Toohello StorSimple cihaz Yöneticisi hizmetine bağlanın
Merhaba StorSimple cihaz Yöneticisi hizmeti Microsoft Azure üzerinde çalışır ve toomultiple StorSimple sanal diziler bağlanır. Bu aygıtlar bir tarayıcı toomanage çalıştıran merkezi bir Microsoft Azure portalını kullanın. tooconnect toohello StorSimple cihaz Yöneticisi hizmeti hello aşağıdaki.

#### <a name="tooconnect-toohello-service"></a>tooconnect toohello hizmeti
1. Çok Git[https://ms.portal.azure.com](https://ms.portal.azure.com).
2. Toohello Microsoft Azure Portal'da (Merhaba sağ üst tarafında hello bölmesinin bulunur), Microsoft hesabı kimlik bilgilerinizi kullanarak oturum açın.
3. Gezinme tooBrowse--> 'Filter' StorSimple cihaz yöneticileri tooview üzerinde belirli bir aboneliğe tüm cihaz yöneticileri.

## <a name="use-hello-storsimple-device-manager-service-tooperform-management-tasks"></a>Merhaba StorSimple cihaz Yöneticisi hizmeti tooperform yönetimi görevlerini kullanma
Merhaba aşağıdaki tabloda tüm hello genel yönetim görevleri ve içinde hello StorSimple cihaz Yöneticisi hizmeti dikey penceresinde Özet gerçekleştirilebilir karmaşık iş akışları bir özetini gösterir. Bu görevler üzerinde bunlar başlatılan hello Kanatlar göre düzenlenir.

Her bir iş akışı hakkında daha fazla bilgi için hello tablosundaki hello uygun yordamı tıklatın.

#### <a name="storsimple-device-manager-workflows"></a>StorSimple cihaz Manager iş akışları
| Bu toodo isterseniz... | Bu yordamı kullanın |
| --- | --- | --- |
| Hizmet oluşturma</br>Bir hizmeti silin</br>Merhaba hizmet kayıt anahtarını alın</br>Merhaba hizmet kayıt anahtarını yeniden oluşturma |[Merhaba StorSimple cihaz Yöneticisi hizmetini dağıtma](storsimple-virtual-array-manage-service.md) |
| Merhaba etkinlik günlüklerini görüntüle |[Merhaba StorSimple hizmeti Özet kullanın](storsimple-virtual-array-service-summary.md) |
| Sanal bir dizi devre dışı bırakma</br>Sanal bir dizi Sil |[Sanal bir dizi silmek veya devre dışı bırakma](storsimple-virtual-array-deactivate-and-delete-device.md) |
| Olağanüstü durum kurtarma ve aygıt yük devretme</br>Yük devretme önkoşulları</br>İş sürekliliği olağanüstü durum kurtarma (BCDR)</br>Olağanüstü durum kurtarma sırasında hatalar |[Olağanüstü durum kurtarma ve aygıt yük devretme, StorSimple sanal dizini](storsimple-virtual-array-failover-dr.md) |
| Paylaşımları ve birimler yedekleme</br>El ile yedekleyin</br>Merhaba yedekleme zamanlamasını değiştirme</br>Var olan yedekleri görüntüleyin |[StorSimple sanal dizinizi yedekleyin](storsimple-virtual-array-backup.md) |
| Bir yedekleme kümesinden kopya paylaşımları</br>Bir yedekleme kümesi birimlerden kopyalama</br>Öğe düzeyinde Kurtarma (yalnızca dosya sunucusu) |[StorSimple sanal dizinizi yedekten kopyalama](storsimple-virtual-array-clone.md) |
| Depolama hesapları hakkında</br>Depolama hesabı ekleme</br>Bir depolama hesabı Düzenle</br>Bir depolama hesabını silme |[Merhaba StorSimple sanal dizi depolama hesaplarını yönetme](storsimple-virtual-array-manage-storage-accounts.md) |
| Erişim denetimi kayıtları hakkında</br>Ekleyin veya bir erişim denetimi kaydı değiştirin </br>Bir erişim denetimi kaydını sil |[Merhaba StorSimple sanal dizi için erişim denetim kayıtlarını yönetme](storsimple-virtual-array-manage-acrs.md) |
| İş ayrıntılarını görüntüleme |[StorSimple sanal dizinin işlerini yönetme](storsimple-virtual-array-manage-jobs.md) |
| Uyarı ayarlarını yapılandırma</br>Uyarı bildirimleri alma</br>Uyarıları yönetme</br>Uyarıları gözden geçirin |[Merhaba StorSimple sanal dizinin için uyarıları görüntüleyin ve yönetin](storsimple-virtual-array-manage-alerts.md) |
| Merhaba cihaz Yöneticisi parolasını değiştirme |[Merhaba StorSimple sanal dizinin cihaz Yöneticisi parolasını değiştirme](storsimple-virtual-array-change-device-admin-password.md) |
| Yazılım güncelleştirmelerini yükle |[Sanal dizinizi güncelleştir](storsimple-virtual-array-install-update.md) |

> [!NOTE]
> Merhaba kullanmalısınız [yerel web kullanıcı Arabirimi](storsimple-ova-web-ui-admin.md) görevleri aşağıdaki hello için:
> 
> * [Merhaba hizmet verileri şifreleme anahtarı alma](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)
> * [Bir destek paketi oluştur](storsimple-ova-web-ui-admin.md#generate-a-log-package)
> * [Durdurun ve sanal dizinin yeniden başlatın](storsimple-ova-web-ui-admin.md#shut-down-and-restart-your-device)
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Web kullanıcı Arabirimi hello hakkında bilgi için ve nasıl toouse, çok Git[kullanın, StorSimple sanal dizinizi StorSimple web kullanıcı Arabirimi tooadminister hello](storsimple-ova-web-ui-admin.md).


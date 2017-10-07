---
title: "Azure IOT Hub ile aaaDevice Yönetimi | Microsoft Docs"
description: "Azure IoT Hub'daki cihaz yönetimine genel bakış: kurumsal cihaz yaşam döngüsü ve yeniden başlatma, fabrika sıfırlaması, üretici yazılımı güncelleştirmesi, yapılandırma, cihaz çiftleri, sorgular, işler gibi cihaz yönetim düzenleri."
services: iot-hub
documentationcenter: 
author: bzurcher
manager: timlt
editor: 
ms.assetid: a367e715-55f6-4593-bd68-7863cbf0eb81
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: briz
ms.openlocfilehash: 7e22fb6eb3c541a513b16a047c7c3ef557255532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-device-management-with-iot-hub"></a>IoT Hub ile cihaz yönetimine genel bakış
## <a name="introduction"></a>Giriş
Azure IOT Hub hello özellikleri ve cihaz ve arka uç geliştiriciler toobuild sağlam cihaz yönetim çözümlerini etkinleştiren genişletilebilirlik modeli sağlar. Kısıtlanmış algılayıcılar ve tek amaçlı mikrodenetleyici, cihaz gruplarını iletişimlerde rota toopowerful ağ geçitleri aralığından aygıtlar.  Ayrıca, hello kullanım durumları ve IOT işleçleri gereksinimlerini önemli ölçüde endüstriler arasında farklılık gösterir.  Bu değişim rağmen hello özellikleri, desenleri ve kod kitaplıkları toocater tooa farklı aygıt kümesini ve son kullanıcıların IOT hub'ı ile cihaz yönetimi sağlar.

Kendi cihaz koleksiyonu devam eden Yönetimi hello işleçleri nasıl işleneceğini yönelik bir strateji tooprovide başarılı Kurumsal IOT çözümü oluşturma önemli bir parçasıdır. IOT işleçleri basit ve güvenilir araçları ve bunları toofocus hello hakkında daha fazla stratejik yönlerini işlerini etkinleştirmek uygulamaları gerektirir. Bu makalede aşağıdakiler sunulmaktadır:

* Azure IOT Hub yaklaşım toodevice yönetimi, kısa bir özeti.
* Genel cihaz yönetimi ilkelerinin açıklaması.
* Merhaba cihaz yaşam döngüsü açıklaması.
* Genel cihaz yönetimi desenlerine genel bakış.

## <a name="device-management-principles"></a>Cihaz yönetimi ilkeleri
IOT ile cihaz Yönetimi zorluklar benzersiz bir dizi özelliği sunar ve her kurumsal sınıf çözüm ilkeler aşağıdaki hello adres gerekir:

![Cihaz yönetimi ilkeleri grafiği][img-dm_principles]

* **Ölçek ve Otomasyon**: IOT çözümleri gerektirir rutin görevleri otomatik hale getirmek ve görece küçük işlemleri etkinleştirmek basit araçları personel toomanage milyonlarca cihaz. Günlük, işleçler toohandle aygıt işlemleri uzaktan toplu olarak beklediğiniz ve tooonly doğrudan dikkatini gerektiren sorunlar çıkması olduğunda uyarılmak.
* **Açıklık ve Uyumluluk**: hello aygıt ekosistemi alıyoruz farklı. Yönetim Araçları uyarlanmış tooaccommodate aygıt sınıfları, platformlar ve protokolleri çok sayıda olmalıdır. İşleçler sağlayabilmelidir çeşitli aygıtlardan hello en kısıtlı toosupport katıştırılmış tek işlem yongaları, toopowerful ve tam olarak işlevsel bilgisayarlar.
* **Bağlam tanıma**: IoT ortamları dinamik ve sürekli değişen yapıdadır. Hizmet güvenilirliği üst düzey öneme sahiptir. Aygıt yönetimi işlemleri bu bakım Etkenler tooensure aşağıdaki hesap hello gerçekleştirmeniz gereken kapalı kalma süresi değil veya önemli iş işlemlerini etkileyen tehlikeli koşullar oluşturun:
    * SLA bakım pencereleri
    * Ağ ve güç durumları
    * Kullanım koşulları
    * Cihaz coğrafi konumu
* **Birçok rol hizmeti**: hello benzersiz iş akışları ve IOT işlem rolü işlemleri için destek önemlidir. Merhaba personelinin harmoniously iç BT departmanları kısıtlamalara hello ile çalışması gerekir.  Sürdürülebilir yolları toosurface gerçek zamanlı cihaz operations bilgi toosupervisors ve diğer iş yönetim rolleri bulmak de gerekir.

## <a name="device-lifecycle"></a>Cihaz yaşam döngüsü
Bir dizi ortak tooall Kurumsal IOT projeler genel aygıt yönetimi aşamaları yoktur. Azure IOT hello cihaz yaşam döngüsü içinde beş aşama vardır:

![beş Azure IOT cihaz yaşam döngüsü aşamaları hello: planlama, sağlama, yapılandırmak, izlemek, devre dışı bırakma][img-device_lifecycle]

Her beş Bu aşamalar içinde karşılanan tooprovide eksiksiz bir çözüm olması gereken birkaç aygıt işleci gereksinimleri vardır:

* **Plan**: etkinleştirme işleçleri toocreate tooeasily ve doğru bir şekilde sorgu için sağlayan cihaz meta veri şeması ve cihazların toplu yönetim işlemleri için bir grubu hedeflemek. Bu cihaz meta verilerini etiketleri ve özellikleri hello biçiminde hello cihaz çifti toostore kullanabilirsiniz.
  
    *Daha fazla okuma*: [cihaz çiftlerini ile çalışmaya başlama][lnk-twins-getstarted], [cihaz çiftlerini anlamak][lnk-twins-devguide], [nasıl toouse cihaz çifti özellikleri][lnk-twin-properties].
* **Sağlama**: güvenli bir şekilde yeni aygıtları tooIoT Hub ve etkinleştir işleçleri tooimmediately Bul cihaz özellikleri sağlama.  Merhaba IOT Hub kimlik kayıt defteri toocreate esnek cihaz kimliklerini ve kimlik bilgilerini kullanın ve bir işi kullanarak toplu olarak bu işlem gerçekleştirin. Aygıtları tooreport kendi yetenekleri ve cihaz özellikleri hello cihaz çiftine aracılığıyla koşullar oluşturun.
  
    *Daha fazla okuma*: [aygıt kimlikleri yönetmek][lnk-identity-registry], [toplu yönetim cihaz kimlikleri][lnk-bulk-identity], [Nasıl toouse cihaz çifti özellikleri][lnk-twin-properties].
* **Yapılandırma**: Toplu kolaylaştırmak yapılandırma değişiklikleri ve bellenim güncelleştirmeleri toodevices sistem durumu ve güvenlik korurken. İstediğiniz özellikleri kullanarak ve doğrudan yöntemler ve yayın işleri ile bu cihaz yönetimi işlemlerini toplu olarak gerçekleştirin.
  
    *Daha fazla okuma*: [doğrudan yöntemleri kullanın][lnk-c2d-methods], [bir cihazda doğrudan bir yöntem çağırma][lnk-methods-devguide], [nasıl toouse cihaz çifti özellikleri][lnk-twin-properties], [zamanlama ve yayın işleri][lnk-jobs], [zamanlama işlerini birden çok aygıta] [lnk-jobs-devguide].
* **İzleyici**: Genel cihaz toplama sistem durumu, devam eden işlemler ve dikkatini gerektirebilir uyarı işleçleri tooissues hello durumunu izleyin.  Hello cihaz çifti tooallow aygıtları tooreport gerçek zamanlı kullanım koşullarına ve güncelleştirme işlemlerinin durumunu uygulanır. Cihaz çifti sorguları kullanarak yapı bu yüzey hello en yakın sorunlar güçlü panoyu raporlar.
  
    *Daha fazla okuma*: [nasıl toouse cihaz çifti özellikleri][lnk-twin-properties], [IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query-language].
* **Devre dışı bırakma**: değiştirin veya cihazları bir hatadan sonra yetkisini, döngü, yükseltme veya hello hizmet ömrü hello sonunda.  Merhaba fiziksel aygıt yaşanıyorsa hello cihaz çifti toomaintain aygıt bilgileri kullanmak yerine ya da devre dışı bırakıldığını, arşivlenen. Merhaba IOT Hub kimlik kayıt defteri cihaz kimliklerini ve kimlik bilgilerini güvenli bir şekilde iptal kullanın.
  
    *Daha fazla okuma*: [nasıl toouse cihaz çifti özellikleri][lnk-twin-properties], [aygıt kimlikleri yönetmek][lnk-identity-registry].

## <a name="device-management-patterns"></a>Cihaz yönetimi modelleri
IOT Hub cihaz Yönetimi desenleri aşağıdaki hello sağlar.  Merhaba [aygıt yönetimi öğreticileri] [ lnk-get-started] daha ayrıntılı olarak nasıl yapacağınızı tooextend bu desenleri toofit şablonları çekirdek, tam senaryo ve nasıl toodesign yeni desenler bunlar üzerinde temel.

* **Yeniden başlatma** -hello arka uç uygulama bildirir hello cihaz doğrudan bir yöntem yeniden başlattı.  Merhaba aygıt kullanır hello hello cihaz özellikleri tooupdate hello yeniden başlatma durumu bildirdi.
  
    ![Cihaz yönetimi yeniden başlatma deseninin grafiği][img-reboot_pattern]
* **Fabrika sıfırlaması** -hello arka uç uygulama bildirir hello cihaz doğrudan bir yöntem bir Fabrika sıfırlaması başlattı.  Merhaba aygıt kullanır hello özellikleri tooupdate hello Fabrika hello cihaz durumunu sıfırlamak bildirdi.
  
    ![Cihaz yönetimi fabrika sıfırlama deseninin grafiği][img-facreset_pattern]
* **Yapılandırma** -hello arka uç uygulama hello cihazda çalışan istenen hello özellikleri tooconfigure yazılım kullanır.  Merhaba aygıt kullanır hello hello cihaz özellikleri tooupdate yapılandırma durumu bildirdi.
  
    ![Cihaz yönetimi yapılandırma deseninin grafiği][img-config_pattern]
* **Bellenim güncelleştirme** -hello arka uç uygulama bildirir hello cihaz doğrudan bir yöntem bir ürün yazılımı güncelleştirmesi başlattı.  çok adımlı bir işlemi toodownload hello bellenim görüntü Hello aygıt başlatır, hello bellenim görüntüsünü uygulamak ve son toohello IOT Hub hizmetine yeniden bağlanın.  Hello çok adımlı işlemi boyunca hello aygıt kullanır hello özellikleri tooupdate hello ilerleme ve hello cihazın durumu bildirdi.
  
    ![Cihaz yönetimi üretici yazılımı güncelleştirme deseninin grafiği][img-fwupdate_pattern]
* **İlerleme durumu ve durumu raporlama** -hello çözüm arka ucu cihazları, tooreport hello durumu ile ilgili bir dizi ve ilerleme hello cihazlarda çalışan işlemlerin arasında cihaz çifti sorguları çalıştırır.
  
    ![Cihaz yönetimi raporlama ilerleme ve durum deseninin grafiği][img-report_progress_pattern]

## <a name="next-steps"></a>Sonraki Adımlar
Merhaba özellikleri, desenleri ve IOT Hub cihaz yönetimi için sağlar kodu kitaplıkları Kurumsal IOT işleci her cihaz yaşam döngüsü aşaması içinde gerekliliklerini toocreate IOT uygulamaları etkinleştirir.

Merhaba cihaz yönetimi özellikleri IOT hub'ı öğrenmeye toocontinue bkz hello [aygıt Management'i kullanmaya başlama] [ lnk-get-started] Öğreticisi.

<!-- Images and links -->
[img-dm_principles]: media/iot-hub-device-management-overview/image4.png
[img-device_lifecycle]: media/iot-hub-device-management-overview/image5.png
[img-config_pattern]: media/iot-hub-device-management-overview/configuration-pattern.png
[img-facreset_pattern]: media/iot-hub-device-management-overview/facreset-pattern.png
[img-fwupdate_pattern]: media/iot-hub-device-management-overview/fwupdate-pattern.png
[img-reboot_pattern]: media/iot-hub-device-management-overview/reboot-pattern.png
[img-report_progress_pattern]: media/iot-hub-device-management-overview/report-progress-pattern.png

[lnk-twins-devguide]: iot-hub-devguide-device-twins.md
[lnk-get-started]: iot-hub-node-node-device-management-get-started.md
[lnk-twins-getstarted]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-hub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-query-language]: iot-hub-devguide-query-language.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-methods-devguide]: iot-hub-devguide-direct-methods.md
[lnk-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-jobs-devguide]: iot-hub-devguide-jobs.md

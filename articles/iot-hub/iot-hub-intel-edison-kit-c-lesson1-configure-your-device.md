---
title: "Connect Intel Edison (C) tooAzure IOT - Ders 1: cihaz yapılandırma | Microsoft Docs"
description: "Intel Edison'u ilk kez kullanmak için yapılandırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "ayarlama, arduino bağlanmak arduino toopc, Kurulum arduino, arduino Panosu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5e06e06f1fcea02086e95742804f82cfcb8e265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a>Intel Edison'u yapılandırın
## <a name="what-you-will-do"></a>Ne yapacağını
Intel Edison'u hello Panosu, Yukarı başlatırken birleştirerek ilk kez kullanmak için yapılandırın ve yapılandırma aracı tooyour masaüstü işletim sistemi tooflash yükleme Edison'u'nın bellenim parolasını ayarlayın ve tooWi-Fi bağlanın. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Nasıl tooassemble Edison'u tahtası ve yukarı güç.
* Nasıl tooflash Edison'u'nın üretici yazılımı, parola ayarlama ve Wi-Fi bağlanın.

## <a name="what-you-need"></a>Ne gerekiyor
toocomplete bu işlem, Intel Edison'u Starter Kit bölümleri aşağıdaki hello gerekir:

* Intel® Edison'u Modülü
* Arduino genişletme kartı
* Bir ayırıcı çubukları veya iki Vida toofasten hello modülü toohello genişletme kartı ve vida ve plastik boşluk ekleyiciler dört kümeleri dahil olmak üzere hello paketleme de dahil Vida.
* Mikro B tooType bir USB kablosu
* Bir doğrudan geçerli (DC) güç kaynağı. Güç kaynağı gibi derecelendirilmiş:
  - 7 15V DC
  - En az 1500mA
  - Merhaba merkezi/iç PIN hello pozitif kutbu'na hello güç kaynağı, olmalıdır

  ![Starter Kit şeyler](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

Şunları da yapmanız gerekir:

* Windows, Mac veya Linux çalıştıran bir bilgisayar.
* Kablosuz bağlantı Edison'u tooconnect için.
* Bir Internet bağlantısı toodownload yapılandırma aracı.

## <a name="assemble-your-board"></a>Panonuzu birleştirin

Bu bölümdeki adımları tooattach Intel® Edison'u modülü tooyour genişletme panonuzu içerir.

1. Merhaba Intel® Edison'u modülü hello beyaz anahat içinde hello genişletme panosunda hello Vida ile Merhaba delik hello modül hizalama genişletme panonuzu yerleştirin.

2. Merhaba modül hello sözcükleri hemen altındaki aşağı basın `What will you make?` bir ek düşündüğünüz kadar.

   ![Pano 2 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. Merhaba iki (Merhaba paketine dahil) onaltılık nasıl toosecure hello modülü toohello genişletme kartı kullanın.

   ![Pano 3 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Merhaba dört köşe delik hello genişletme panosunda birinde bir Vidayı ekleyin. Bük ve hello Beyaz Plastik boşluk ekleyiciler hello Vidayı üzerine birini sıkılaştırabilirsiniz.

   ![Pano 4 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Diğer üç köşe boşluk ekleyiciler hello için yineleyin.

   ![Pano 5 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

Panonuz artık derlenip.

   ![Birleştirilmiş Panosu](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Güç Edison'u ayarlama

1. Merhaba güç takın.

   ![Güç kaynağı bağlama](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. (DS1 hello Arduino * genişletme Panosu üzerinde etiketli) yeşil bir LED açık ve aydınlatılmış olmak gerekir.

3. Başlangıç Panosu toofinish yukarı önyükleme için bir dakika bekleyin.

   > [!NOTE]
   > DC güç kaynağı yoksa, hala bir USB bağlantı noktası üzerinden Güç hello Panosu kullanabilirsiniz. Bkz: `Connect Edison tooyour computer` ayrıntıları bölümü. Özellikle Wi-Fi kullanarak veya yürüten motors zaman Panonuzu bu şekilde destekleyen, karttan beklenmeyen davranışlara neden olabilir.

## <a name="connect-edison-tooyour-computer"></a>Edison'u tooyour bilgisayara bağlanma

1. Böylece Edison'u aygıt modunda hello mikro düğme hello iki mikro USB bağlantı noktası doğru aşağı Değiştir. Cihaz mod ve ana mod arasındaki farklar için lütfen başvuru [burada](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Merhaba mikro düğme Değiştir](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Merhaba mikro USB kablosu hello üst mikro USB bağlantı noktasına takın.

   ![Üst mikro USB bağlantı noktası](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Tak bilgisayarınıza USB kablosu diğer ucundaki hello.

   ![Bilgisayar USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. Bilgisayarınızın yeni bir sürücüye (çok SD kart bilgisayarınıza ekleme gibi) bağladığında panonuzu tam olarak başlatılmadan bilirsiniz.

## <a name="download-and-run-hello-configuration-tool"></a>Karşıdan yükle ve hello yapılandırma aracını çalıştırın.
Merhaba en son yapılandırma aracından alma [bu bağlantıyı](https://software.intel.com/en-us/iot/hardware/edison/downloads) hello altında listelenen `Installers` başlığı. Hello aracını Yürüt ve izleyin, ekrandaki yönergeleri, gerektiğinde İleri tıklatıldığında

### <a name="flash-firmware"></a>Bellenim flash
1. Merhaba üzerinde `Set up options` sayfasında, `Flash Firmware`.
2. Merhaba görüntü tooflash panonuzu üzerine hello aşağıdakilerden birini yaparak seçin:
   - toodownload flash panonuzu görüntüsüyle hello en son bellenim Intel'in, kullanılabilir seçip `Download hello latest image version xxxx`.
   - panonuzu, önceden kaydettiğiniz bilgisayarınızdan bir görüntüyle tooflash seçin `Select hello local image`. Tooflash tooyour Panosu tooand select hello görüntü göz atın.
3. Merhaba Kurulum aracı tooflash panonuzu deneyecek. Merhaba tüm yanıp sönen işlem too10 dakika sürebilir.

### <a name="set-password"></a>Parola ayarlama
1. Merhaba üzerinde `Set up options` sayfasında, `Enable Security`.
2. Intel® Edison'u panonuz için bir özel ad ayarlayabilirsiniz. Bu isteğe bağlıdır.
3. Panonuz için bir parola yazın ve ardından `Set password`.
4. Daha sonra kullanılan hello parola işaretleyin.

### <a name="connect-wi-fi"></a>Wi-Fi Bağlan
1. Merhaba üzerinde `Set up options` sayfasında, `Connect Wi-Fi`. Kullanılabilir kablosuz ağlar için bilgisayar taramaları olarak tooone dakika yukarı bekleyin.
2. Merhaba gelen `Detected Networks` aşağı açılan listesinde, ağınızı seçin.
3. Merhaba gelen `Security` aşağı açılan listesinden, select hello ağın güvenlik türü.
4. Oturum açma ve parola bilgilerinizi sağlayın ve ardından `Configure Wi-Fi`.
5. Hello daha sonra kullanılan IP adresi işaretleyin.

> [!NOTE]
> Edison'u bağlı toohello aynı bilgisayarınızda olarak ağ olduğundan emin olun. Bilgisayarınızı tooyour Edison'u hello IP adresini kullanarak bağlanır.

Tebrikler! Edison'u başarıyla yapılandırdıktan.

## <a name="summary"></a>Özet
Bu makalede, nasıl tooassemble Edison'u Panosu Merhaba, flash, üretici yazılımı, Kurulum parola ve tooWi-Fi Yapılandırması aracını kullanarak bağlamak öğrendiniz. LED henüz açık değil yukarı bu hello unutmayın. Merhaba sonraki tooinstall hello gerekli araçları ve yazılım üzerinde Edison'u örnek bir uygulamayı çalıştırmak için hazırlanırken bir görevdir.

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba araçları edinin][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
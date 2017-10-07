---
title: "Azure IOT kenarıyla fiziksel bir aygıtı aaaUse | Microsoft Docs"
description: "Nasıl toouse bir Texas Instruments SensorTag aygıt toosend veri tooan IOT hub Raspberry Pi 3 cihazda çalışan IOT sınır ağ geçidi üzerinden. Merhaba ağ geçidi, Azure IOT kenar kullanılarak oluşturulur."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a>Azure IOT kenar Raspberry Pi'yi tooforward cihaz bulut iletilerini tooIoT Hub kullanın

Bu kılavuz hello [Bluetooth düşük enerji örnek] [ lnk-ble-samplecode] nasıl gösterir toouse [Azure IOT kenar] [ lnk-sdk] için:

* Cihaz bulut telemetri tooIoT Hub fiziksel CİHAZDAN iletin.
* IOT hub'ı tooa fiziksel CİHAZDAN rota komutları.

Bu kılavuzda aşağıdaki konular ele alınmaktadır:

* **Mimari**: hello Bluetooth düşük enerji örnek hakkında önemli mimari bilgiler.
* **Derleme ve çalıştırma**: hello adımları gerekli toobuild ve çalışma hello örnek.

## <a name="architecture"></a>Mimari

Merhaba anlatım nasıl toobuild ve Raspberry Pi 3 IOT sınır ağ geçidi çalıştırılmasında Raspbian Linux çalıştıran gösterir. Merhaba ağ geçidi IOT kenar kullanılarak oluşturulur. Merhaba örnek bir Texas Instruments SensorTag Bluetooth düşük enerji (bırak) cihaz toocollect sıcaklık verileri kullanır.

Merhaba IOT sınır ağ geçidi çalıştırdığınızda bu:

* Tooa SensorTag aygıt Hello Bluetooth düşük enerji (bırak) protokolünü kullanarak bağlanır.
* TooIoT Hub bağlayan hello HTTP protokolünü kullanarak.
* Telemetri hello SensorTag aygıt tooIoT Hub iletir.
* IOT hub'ı toohello SensorTag aygıttan komutları yönlendirir.

Merhaba ağ geçidi IOT kenar modülleri aşağıdaki hello içerir:

* A *bırak Modülü* verilerle bir bırak aygıt tooreceive sıcaklık hello aygıt ve gönderme komutları toohello aygıt arabirimleri.
* A *bırak bulut toodevice Modülü* bırak yönergeler hello için içine IOT Hub'ından gönderilen JSON iletileri çevirir *bırak Modülü*.
* A *Günlükçü Modülü* tüm ağ geçidi iletileri tooa yerel dosya kaydeder.
* Bir *kimlik eşleme Modülü* bırak aygıt MAC adresi ile Azure IOT Hub cihaz kimlikleri arasında çevirir.
* Bir *IOT hub'ı Modülü* telemetri verileri tooan IOT hub'ı yükler ve IOT hub'ından cihaz komutlarını alır.
* A *bırak yazıcı Modülü* hello bırak cihaz telemetrisinden yorumlar ve biçimlendirilmiş veriler toohello konsol tooenable sorun giderme ve hata ayıklama yazdırır.

### <a name="how-data-flows-through-hello-gateway"></a>Merhaba ağ geçidi üzerinden nasıl veri akışları

Blok Diyagramı aşağıdaki hello hello telemetri karşıya yükleme veri akışı ardışık gösterilmektedir:

![Telemetri karşıya yükleme ağ geçidi ardışık düzen](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

öğeyi telemetri bırak aygıt tooIoT seyahat alan hello Hub adımlardır:

1. Merhaba bırak aygıt sıcaklık örnek oluşturur ve Bluetooth toohello bırak hello ağ geçidi modülünde üzerinden gönderir.
1. Merhaba bırak modülü hello örnek alır ve toohello Aracısı hello aygıtın hello MAC adresi birlikte yayımlar.
1. Hello kimlik eşleme modülü bu iletiyi alır ve bir iç tablo tootranslate hello hello aygıt MAC adresi bir IOT Hub cihaz kimliğini kullanır. Bir IOT Hub cihaz kimliği, bir cihaz kimliği ve aygıt anahtarı oluşur.
1. Merhaba kimlik eşleme modülü hello sıcaklık örnek verileri, hello MAC adresi hello aygıt, hello cihaz kimliği ve hello aygıt anahtarı içeren yeni bir ileti yayımlar.
1. Merhaba IOT hub'ı Modülü (Merhaba kimlik eşleme modülü tarafından oluşturulan) bu yeni bir ileti alır ve tooIoT Hub yayımlar.
1. Merhaba Günlükçü modülü hello Aracısı tooa yerel dosyadan tüm iletileri günlüğe kaydeder.

Blok Diyagramı aşağıdaki hello hello aygıt komutu veri akışı ardışık gösterilmektedir:

![Cihaz komut ağ geçidi ardışık düzeni](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. Yeni komut iletileri için IOT hub hello Hello IOT Hub'ın modül düzenli aralıklarla yoklar.
1. Merhaba IOT hub'ı modülü yeni bir komut iletisi aldığında, onu toohello Aracısı yayımlar.
1. Merhaba kimlik eşleme modülü hello komutu iletiyi alır ve bir iç tablo tootranslate hello IOT Hub cihaz kimliği tooa aygıt MAC adresi kullanır. Ardından, hello özellikleri eşlemesinde hello iletisinin hello hedef aygıt hello MAC adresini içeren yeni bir ileti yayımlar.
1. Merhaba bırak bulut-cihaz modülü bu iletiyi alır ve hello uygun bırak yönerge hello bırak modülü için çevirir. Ardından, yeni bir ileti yayımlar.
1. Merhaba bırak modülü bu iletiyi alır ve hello bırak aygıtla iletişim kurarak hello g/ç yönerge çalıştırır.
1. Merhaba Günlükçü modülü hello Aracısı tooa disk dosyasından tüm iletileri günlüğe kaydeder.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğreticide, bir etkin Azure aboneliği gerekir.

> [!NOTE]
> Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].

Tooremotely erişim hello komut satırı Raspberry Pi'yi hello üzerinde Masaüstü makine tooenable üzerinde SSH istemcisi gerekir.

- Windows, bir SSH istemcisi içermez. Kullanmanızı öneririz [PuTTY](http://www.putty.org/).
- Çoğu Linux dağıtımları ve Mac OS komut satırı SSH yardımcı programını hello içerir. Daha fazla bilgi için bkz: [SSH kullanarak Linux veya Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).

## <a name="prepare-your-hardware"></a>Donanımınızın hazırlama

Bu öğreticide kullandığınız varsayılır bir [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) aygıt bağlı tooa Raspberry Pi 3 Raspbian çalışıyor.

### <a name="install-raspbian"></a>Raspbian yükleyin

Seçenekler tooinstall Raspbian Raspberry Pi 3 aygıtınızda aşağıdaki hello birini kullanabilirsiniz.

* tooinstall hello en son sürümünü Raspbian, kullanım hello [NOOBS] [ lnk-noobs] grafik kullanıcı arabirimi.
* El ile [karşıdan] [ lnk-raspbian] ve hello son hello Raspbian işletim sistemi tooan SD kart görüntüsü yazma.

### <a name="sign-in-and-access-hello-terminal"></a>Oturum açma ve hello terminal erişim

İki seçenek tooaccess, Raspberry Pi'yi bir terminal ortamına sahip:

* Klavye varsa ve bağlı tooyour Raspberry Pi'yi izlemek, hello Raspbian GUI tooaccess bir terminal penceresi kullanabilirsiniz.

* Erişim hello komut satırında Masaüstü makinenizden SSH kullanarak, Raspberry Pi'yi.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Merhaba GUI içinde bir terminal penceresi kullanın

Merhaba varsayılan kimlik bilgilerini Raspbian olan kullanıcı adı **PI** ve parola **raspberry**. Merhaba Görev Çubuğu'nda hello GUI, hello başlatabilirsiniz **Terminal** gibi bir izleyici arar hello simgesini kullanarak yardımcı programı.

#### <a name="sign-in-with-ssh"></a>Oturum SSH oturum

Komut satırı erişimi tooyour Raspberry Pi'yi için SSH kullanabilirsiniz. Merhaba makale [SSH (Secure Shell)] [ lnk-pi-ssh] açıklar nasıl tooconfigure, Raspberry Pi'yi üzerinde SSH ve nasıl tooconnect gelen [Windows] [ lnk-ssh-windows] veya [Linux ve Mac OS][lnk-ssh-linux].

Kullanıcı adıyla oturum **PI** ve parola **raspberry**.

### <a name="install-bluez-537"></a>BlueZ 5.37 yükleyin

Merhaba bırak modülleri toohello Bluetooth donanım hello BlueZ yığını ile görüşün. BlueZ 5.37 sürümü hello modülleri toowork için doğru ihtiyacınız var. Bu yönergeleri hello BlueZ doğru sürümünün yüklü olduğundan emin olun.

1. Merhaba geçerli bluetooth arka plan programı durdurun:

    ```sh
    sudo systemctl stop bluetooth
    ```

1. Merhaba BlueZ bağımlılıkları yükler:

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. Merhaba BlueZ kaynak kodu bluez.org yükleyin:

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. Merhaba kaynak kodu sıkıştırmasını açın:

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. Dizinleri toohello yeni oluşturulan klasör değiştirin:

    ```sh
    cd bluez-5.37
    ```

1. Yerleşik hello BlueZ kod toobe yapılandırın:

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. BlueZ oluşturun:

    ```sh
    make
    ```

1. Bunu yaptıktan sonra BlueZ yükleme oluşturma:

    ```sh
    sudo make install
    ```

1. Değişiklik systemd hizmet yapılandırması toohello yeni bluetooth arka plan programı hello dosyasında işaret şekilde bluetooth `/lib/systemd/system/bluetooth.service`. Merhaba 'ExecStart' satır metnini izleyen hello ile değiştirin:

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a>Bağlantı toohello SensorTag aygıtı Raspberry Pi 3 cihazınızdan etkinleştir

Çalışan hello örnek önce Raspberry Pi 3 toohello SensorTag aygıt bağlanabilir tooverify gerekir.

1. Merhaba olun `rfkill` yardımcı programı yüklenir:

    ```sh
    sudo apt-get install rfkill
    ```

1. Bluetooth hello Raspberry Pi 3 üzerinde engelini kaldırmak ve hello sürüm numarası olup olmadığını denetleyin **5.37**:

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. tooenter hello etkileşimli bluetooth Kabuk hello bluetooth hizmetini başlatın ve hello yürütme **bluetoothctl** komutu:

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Merhaba komutu girin **güç açma** toopower hello bluetooth denetleyici ayarlama. Merhaba komut çıktısı benzer toohello aşağıdaki döndürür:

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. Merhaba etkileşimli bluetooth Kabuğu'nda hello komutu girin **taraması** tooscan bluetooth cihazları için. Merhaba komut çıktısı benzer toohello aşağıdaki döndürür:

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. Merhaba SensorTag aygıt bulunabilirlik hello küçük (yeşil LED flash hello) düğmesini tıklatarak olun. Merhaba Raspberry Pi 3 hello SensorTag aygıtı keşfet:

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    Bu örnekte, bu hello hello SensorTag aygıt MAC adresi görebilirsiniz **A0:E6:F8:B5:F6:00**.

1. Merhaba girerek taramayı kapatabilirsiniz **kapalı tarama** komutu:

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. MAC adresini girerek kullanarak tooyour SensorTag aygıtı bağlayın **bağlanmak \<MAC adresi\>**. örnek çıktı aşağıdaki hello daha anlaşılır olması için kısaltılır:

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > Merhaba GATT hello kullanarak yeniden hello aygıtın özelliklerini listeleyebilirsiniz **liste öznitelikleri** komutu.

1. Artık hello kullanarak hello aygıttan bağlantısını **bağlantısını** komut ve hello kullanarak hello bluetooth Kabuğu'ndan çıkmak **çıkın** komutu:

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

Şimdi Raspberry Pi 3'te hazır toorun hello bırak IOT kenar örnek demektir.

## <a name="run-hello-iot-edge-ble-sample"></a>Merhaba IOT kenar Bırak örneğini çalıştırın

toorun hello IOT kenar bırak örnek toocomplete üç görevler gerekir:

* İki örnek cihazlar IOT Hub'ınıza yapılandırın.
* IOT kenar Raspberry Pi 3 aygıtınızda oluşturun.
* Yapılandırın ve Raspberry Pi 3 aygıtınızda hello bırak örnek çalıştırın.

Yazma Hello anda IOT kenar yalnızca bırak modülleri Linux üzerinde çalışan ağ geçitleri de destekler.

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>İki örnek cihazlar IOT hub'ınızı yapılandırma

* [IOT hub oluşturma] [ lnk-create-hub] Azure aboneliğinizde bu kılavuzda, hub toocomplete hello adı gerekir. Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.
* Adlı bir aygıt Ekle **SensorTag_01** tooyour IOT hub ve kendi kimliği ve cihaz anahtarını not edin. Merhaba kullanabilirsiniz [aygıt explorer veya iothub-explorer] [ lnk-explorer-tools] tooadd oluşturduğunuz hello önceki adımı ve tooretrieve anahtarıyla bu cihaz toohello IOT hub araçları. Merhaba ağ geçidi yapılandırdığınızda bu cihaz toohello SensorTag aygıt eşleyin.

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>Azure IOT kenar, Böğürtlenli Pi 3 derleme

Bağımlılıklar için Azure IOT kenar yükleyin:

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

Kullanım hello aşağıdaki tooclone IOT kenar ve tüm alt submodules tooyour giriş dizini komutlar:

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

Merhaba IOT kenar havuzu tam bir kopyasını Raspberry Pi 3'te olduğunda komut hello SDK içeren hello klasöründen aşağıdaki hello kullanarak oluşturabilirsiniz:

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a>Yapılandırma ve hello bırak örnek Raspberry Pi 3'te çalıştırma

toobootstrap ve çalışma hello örnek, hello ağ geçidi katılan her IOT kenar modülü yapılandırmanız gerekir. Bu yapılandırma bir JSON dosyası sağlanır ve tüm beş katılımcı IOT kenar modülleri yapılandırmanız gerekir. Merhaba depoya adlı örnek bir JSON dosyası olduğu **ağ geçidi\_sample.json** başlangıç noktası kendi yapılandırma dosyası oluşturmak için hello olarak kullanabilirsiniz. Bu bir dosyadır hello **ble_gateway/samples/src** hello IOT kenar havuzu yerel kopyasını klasöründe.

Hello aşağıdaki bölümlerde bu yapılandırma hello bırak örnek için dosya ve o hello IOT kenar havuzu varsayın tooedit hello nasıl olduğunu açıklamak **/home/pi/iot-edge /** klasörü Raspberry Pi 3. Merhaba deposu başka bir yerde ise, hello yollar uygun şekilde ayarlayın.

#### <a name="logger-configuration"></a>Günlükçü yapılandırma

Merhaba ağ geçidi deposu hello bulunan varsayılarak **/home/pi/iot-edge /** klasörünü hello Günlükçü Modülü aşağıdaki gibi yapılandırın:

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a>BIRAK modül yapılandırması

Merhaba bırak cihaz için Hello örnek yapılandırma Texas Instruments SensorTag aygıt varsayar. Çevre bir GATT çalışması gerekir, ancak tooupdate hello GATT karakteristiğini kimlikleri ve veri gerekebilir gibi çalışabilir standart herhangi bırak aygıt. SensorTag Cihazınızı Hello MAC adresini ekleyin:

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

SensorTag aygıt kullanmıyorsanız tooupdate hello GATT karakteristiğini kimlikleri ve veri değerlerini gerekip gerekmediğini bırak aygıt toodetermine için hello belgelerini gözden geçirin.

#### <a name="iot-hub-module"></a>IOT hub'ı Modülü

IOT Hub'ınızı Hello adını ekleyin. Merhaba sonek değeri genellikle **azure devices.net**:

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a>Kimlik eşleme modülü yapılandırması

Merhaba MAC adresini SensorTag cihaz ve hello cihaz kimliği ve başlangıç anahtarı eklemek **SensorTag_01** tooyour IOT hub'ı eklediğiniz aygıt:

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a>BIRAK yazıcı modülü yapılandırması

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a>BLEC2D modülü yapılandırması

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a>Yönlendirme yapılandırması

Merhaba aşağıdaki yapılandırmayı sağlar hello aşağıdaki IOT kenar modülleri arasında yönlendirme:

* Merhaba **Günlükçü** modülü alır ve tüm iletileri günlüğe kaydeder.
* Merhaba **SensorTag** modül gönderir iletileri tooboth hello **eşleme** ve **bırak yazıcı** modüller.
* Merhaba **eşleme** modül gönderir iletileri toohello **Iothub** tooyour IOT hub'ı gönderilen modülü toobe.
* Merhaba **Iothub** modül gönderir iletileri geri toohello **eşleme** modülü.
* Merhaba **eşleme** modül gönderir iletileri toohello **BLEC2D** modülü.
* Merhaba **BLEC2D** modül gönderir iletileri geri toohello **algılayıcı etiketi** modülü.

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

toorun hello örnek, geçişi hello yol toohello JSON yapılandırma dosyası bir parametre toohello olarak **bırak\_ağ geçidi** ikili. Merhaba aşağıdaki komut hello kullandığınız varsayar **gateway_sample.json** yapılandırma dosyası. Hello bu komutu yürütmek **IOT kenar** hello Raspberry Pi'yi klasörü:

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

Toopress gerekebilir hello küçük düğmesini hello SensorTag aygıt toomake üzerinde bulunabilir, hello örneği çalıştırmadan önce.

Merhaba örneği çalıştırdığınızda, hello kullanabilirsiniz [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) veya hello [iothub-explorer](https://github.com/Azure/iothub-explorer) aracı toomonitor hello iletileri hello IOT sınır ağ geçidi hello SensorTag aygıttan iletir. Örneğin, ıothub explorer kullanarak cihaz bulut iletilerini komutu aşağıdaki hello kullanarak izleyebilirsiniz:

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>Buluttan cihaza iletileri gönderme

Merhaba bırak modülü IOT hub'ı toohello aygıttan gönderen komutları da destekler. Merhaba kullanabilirsiniz [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) veya hello [iothub-explorer](https://github.com/Azure/iothub-explorer) aracı toosend JSON iletileri bu hello bırak ağ geçidi modülü toohello bırak aygıtta iletir.

Merhaba Texas Instruments SensorTag cihaz kullanıyorsanız, IOT Hub'ından komutlar göndererek hello kırmızı LED, yeşil LED veya sesli uyaran kapatabilirsiniz. IOT Hub'ından komutları göndermeden önce ilk iki JSON iletileri sırayla aşağıdaki hello gönderin. Ardından herhangi bir hello komutları tooturn hello ışık veya sesli uyaran gönderebilirsiniz.

1. Tüm LED'leri ve (devre dışı bırakma) hello sesli uyaran sıfırlama:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. G/ç 'uzaktan' yapılandırın:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

Şimdi komutları tooturn hello ışık veya sesli uyaran hello SensorTag cihazdaki aşağıdaki hello hiçbirini gönderebilirsiniz:

* Merhaba kırmızı LED üzerinde açın:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* Merhaba yeşil LED üzerinde açın:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* Merhaba sesli uyaran üzerinde açın:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>Sonraki Adımlar

Toogain IOT kenar daha gelişmiş bir anlayış istiyorsanız ve bazı kod örnekleri ile denemeler hello aşağıdaki ziyaret Geliştirici öğreticiler ve kaynaklar:

* [Azure IOT kenar][lnk-sdk]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md

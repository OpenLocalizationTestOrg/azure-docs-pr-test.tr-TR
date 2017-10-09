## <a name="view-hello-telemetry"></a>Görünüm hello telemetri

Merhaba Raspberry Pi'yi artık telemetri toohello Uzaktan izleme çözümü gönderiyor. Merhaba telemetri hello çözüm panosunda görüntüleyebilirsiniz. Merhaba çözüm panodan iletileri tooyour Raspberry Pi'yi de gönderebilirsiniz.

- Toohello çözüm Panosu gidin.
- Cihazınızı hello seçin **aygıt tooView** açılır.
- Merhaba Hello telemetrisinden Raspberry Pi'yi hello Panoda görüntüler.

![Merhaba Raspberry Pi'yi telemetrisini görüntüleme][img-telemetry-display]

## <a name="act-on-hello-device"></a>Merhaba aygıtta hareket

Merhaba çözüm panodan, Raspberry Pi'yi yöntemleri çağırabilirsiniz. Merhaba Raspberry Pi'yi toohello Uzaktan izleme çözümü bağlandığında, desteklediği hello yöntemleri hakkında bilgi gönderir.

- Merhaba çözüm panosunda tıklatın **aygıtları** toovisit hello **aygıtları** sayfası. Hello Raspberry Pi'yi seçin **cihaz listesi**. Ardından **yöntemleri**:

    ![Panoda aygıtları listele][img-list-devices]

- Merhaba üzerinde **yöntemi çağırma** sayfasında, **LightBlink** hello içinde **yöntemi** açılır.

- Seçin **InvokeMethod**. Merhaba LED Raspberry Pi'yi birkaç kez yanıp sönen toohello bağlı. Merhaba Raspberry Pi'yi Hello uygulamasına bir bildirim geri toohello çözüm Panosu gönderir:

    ![Yöntem geçmişini göster][img-method-history]

- Hello kullanarak açma ve kapatma hello LED geçebilirsiniz **ChangeLightStatus** yöntemi ile bir **LightStatusValue** çok ayarlamak**1** için üzerinde veya **0** için devre dışı.

> [!WARNING]
> Merhaba Uzaktan izleme çözümü Azure hesabınızda çalışan bırakırsanız hello çalıştırıldığında için faturalandırılır. Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config]. Bunu kullanmayı bitirdikten sonra hello önceden yapılandırılmış çözümü Azure hesabınızdan silin.


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
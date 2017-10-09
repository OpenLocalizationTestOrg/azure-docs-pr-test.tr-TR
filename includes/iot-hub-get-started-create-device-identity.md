## <a name="create-a-device-identity"></a>Cihaz kimliği oluşturma

Bu bölümde, kullandığınız adı verilen bir Node.js aracı [iothub-explorer] [ iot-hub-explorer] toocreate Bu öğretici için bir cihaz kimliği. Cihaz Kimlikleri büyük/küçük harfe duyarlıdır.

1. Merhaba aşağıdaki komut satırı ortamınızda çalıştırın:

    `npm install -g iothub-explorer@latest`

1. Ardından, komut toologin tooyour hub aşağıdaki hello çalıştırın. Yedek `{iot hub connection string}` hello daha önce kopyaladığınız IOT Hub bağlantı dizesine sahip:

    `iothub-explorer login "{iot hub connection string}"`

1. Son olarak, adlı yeni bir cihaz kimliği oluşturma `myDeviceId` hello komutuyla:

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

Merhaba sonuç hello cihaz bağlantı dizesini not edin. Bu cihaz bağlantı dizesi hello cihaz uygulama tooconnect tooyour IOT Hub cihaz olarak kullanılır.

![][img-identity]

Çok başvuran[IOT Hub ile çalışmaya başlama] [ lnk-getstarted] tooprogrammatically cihaz kimliklerini oluşturun.

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md

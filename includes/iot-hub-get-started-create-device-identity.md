## <a name="create-a-device-identity"></a><span data-ttu-id="cb53d-101">Cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="cb53d-101">Create a device identity</span></span>

<span data-ttu-id="cb53d-102">Bu bölümde, kullandığınız adı verilen bir Node.js aracı [iothub-explorer] [ iot-hub-explorer] toocreate Bu öğretici için bir cihaz kimliği.</span><span class="sxs-lookup"><span data-stu-id="cb53d-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] toocreate a device identity for this tutorial.</span></span> <span data-ttu-id="cb53d-103">Cihaz Kimlikleri büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="cb53d-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="cb53d-104">Merhaba aşağıdaki komut satırı ortamınızda çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cb53d-104">Run hello following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="cb53d-105">Ardından, komut toologin tooyour hub aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cb53d-105">Then, run hello following command toologin tooyour hub.</span></span> <span data-ttu-id="cb53d-106">Yedek `{iot hub connection string}` hello daha önce kopyaladığınız IOT Hub bağlantı dizesine sahip:</span><span class="sxs-lookup"><span data-stu-id="cb53d-106">Substitute `{iot hub connection string}` with hello IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="cb53d-107">Son olarak, adlı yeni bir cihaz kimliği oluşturma `myDeviceId` hello komutuyla:</span><span class="sxs-lookup"><span data-stu-id="cb53d-107">Finally, create a new device identity called `myDeviceId` with hello command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="cb53d-108">Merhaba sonuç hello cihaz bağlantı dizesini not edin.</span><span class="sxs-lookup"><span data-stu-id="cb53d-108">Make a note of hello device connection string from hello result.</span></span> <span data-ttu-id="cb53d-109">Bu cihaz bağlantı dizesi hello cihaz uygulama tooconnect tooyour IOT Hub cihaz olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cb53d-109">This device connection string is used by hello device app tooconnect tooyour IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="cb53d-110">Çok başvuran[IOT Hub ile çalışmaya başlama] [ lnk-getstarted] tooprogrammatically cihaz kimliklerini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cb53d-110">Refer too[Getting started with IoT Hub][lnk-getstarted] tooprogrammatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md

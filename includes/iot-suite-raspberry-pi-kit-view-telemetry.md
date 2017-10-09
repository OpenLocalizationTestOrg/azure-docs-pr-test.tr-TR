## <a name="view-hello-telemetry"></a><span data-ttu-id="dc34e-101">Görünüm hello telemetri</span><span class="sxs-lookup"><span data-stu-id="dc34e-101">View hello telemetry</span></span>

<span data-ttu-id="dc34e-102">Merhaba Raspberry Pi'yi artık telemetri toohello Uzaktan izleme çözümü gönderiyor.</span><span class="sxs-lookup"><span data-stu-id="dc34e-102">hello Raspberry Pi is now sending telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="dc34e-103">Merhaba telemetri hello çözüm panosunda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc34e-103">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="dc34e-104">Merhaba çözüm panodan iletileri tooyour Raspberry Pi'yi de gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc34e-104">You can also send messages tooyour Raspberry Pi from hello solution dashboard.</span></span>

- <span data-ttu-id="dc34e-105">Toohello çözüm Panosu gidin.</span><span class="sxs-lookup"><span data-stu-id="dc34e-105">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="dc34e-106">Cihazınızı hello seçin **aygıt tooView** açılır.</span><span class="sxs-lookup"><span data-stu-id="dc34e-106">Select your device in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="dc34e-107">Merhaba Hello telemetrisinden Raspberry Pi'yi hello Panoda görüntüler.</span><span class="sxs-lookup"><span data-stu-id="dc34e-107">hello telemetry from hello Raspberry Pi displays on hello dashboard.</span></span>

![Merhaba Raspberry Pi'yi telemetrisini görüntüleme][img-telemetry-display]

## <a name="act-on-hello-device"></a><span data-ttu-id="dc34e-109">Merhaba aygıtta hareket</span><span class="sxs-lookup"><span data-stu-id="dc34e-109">Act on hello device</span></span>

<span data-ttu-id="dc34e-110">Merhaba çözüm panodan, Raspberry Pi'yi yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc34e-110">From hello solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="dc34e-111">Merhaba Raspberry Pi'yi toohello Uzaktan izleme çözümü bağlandığında, desteklediği hello yöntemleri hakkında bilgi gönderir.</span><span class="sxs-lookup"><span data-stu-id="dc34e-111">When hello Raspberry Pi connects toohello remote monitoring solution, it sends information about hello methods it supports.</span></span>

- <span data-ttu-id="dc34e-112">Merhaba çözüm panosunda tıklatın **aygıtları** toovisit hello **aygıtları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="dc34e-112">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="dc34e-113">Hello Raspberry Pi'yi seçin **cihaz listesi**.</span><span class="sxs-lookup"><span data-stu-id="dc34e-113">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="dc34e-114">Ardından **yöntemleri**:</span><span class="sxs-lookup"><span data-stu-id="dc34e-114">Then choose **Methods**:</span></span>

    ![Panoda aygıtları listele][img-list-devices]

- <span data-ttu-id="dc34e-116">Merhaba üzerinde **yöntemi çağırma** sayfasında, **LightBlink** hello içinde **yöntemi** açılır.</span><span class="sxs-lookup"><span data-stu-id="dc34e-116">On hello **Invoke Method** page, choose **LightBlink** in hello **Method** dropdown.</span></span>

- <span data-ttu-id="dc34e-117">Seçin **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="dc34e-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="dc34e-118">Merhaba LED Raspberry Pi'yi birkaç kez yanıp sönen toohello bağlı.</span><span class="sxs-lookup"><span data-stu-id="dc34e-118">hello LED connected toohello Raspberry Pi flashes several times.</span></span> <span data-ttu-id="dc34e-119">Merhaba Raspberry Pi'yi Hello uygulamasına bir bildirim geri toohello çözüm Panosu gönderir:</span><span class="sxs-lookup"><span data-stu-id="dc34e-119">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard:</span></span>

    ![Yöntem geçmişini göster][img-method-history]

- <span data-ttu-id="dc34e-121">Hello kullanarak açma ve kapatma hello LED geçebilirsiniz **ChangeLightStatus** yöntemi ile bir **LightStatusValue** çok ayarlamak**1** için üzerinde veya **0** için devre dışı.</span><span class="sxs-lookup"><span data-stu-id="dc34e-121">You can switch hello LED on and off using hello **ChangeLightStatus** method with a **LightStatusValue** set too**1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="dc34e-122">Merhaba Uzaktan izleme çözümü Azure hesabınızda çalışan bırakırsanız hello çalıştırıldığında için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="dc34e-122">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="dc34e-123">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="dc34e-123">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="dc34e-124">Bunu kullanmayı bitirdikten sonra hello önceden yapılandırılmış çözümü Azure hesabınızdan silin.</span><span class="sxs-lookup"><span data-stu-id="dc34e-124">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
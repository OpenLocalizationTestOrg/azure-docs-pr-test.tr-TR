## <a name="view-hello-telemetry"></a><span data-ttu-id="3aec3-101">Görünüm hello telemetri</span><span class="sxs-lookup"><span data-stu-id="3aec3-101">View hello telemetry</span></span>

<span data-ttu-id="3aec3-102">Merhaba Raspberry Pi'yi artık telemetri toohello Uzaktan izleme çözümü gönderiyor.</span><span class="sxs-lookup"><span data-stu-id="3aec3-102">hello Raspberry Pi is now sending telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="3aec3-103">Merhaba telemetri hello çözüm panosunda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aec3-103">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="3aec3-104">Merhaba çözüm panodan iletileri tooyour Raspberry Pi'yi de gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aec3-104">You can also send messages tooyour Raspberry Pi from hello solution dashboard.</span></span>

- <span data-ttu-id="3aec3-105">Toohello çözüm Panosu gidin.</span><span class="sxs-lookup"><span data-stu-id="3aec3-105">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="3aec3-106">Cihazınızı hello seçin **aygıt tooView** açılır.</span><span class="sxs-lookup"><span data-stu-id="3aec3-106">Select your device in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="3aec3-107">Merhaba Hello telemetrisinden Raspberry Pi'yi hello Panoda görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3aec3-107">hello telemetry from hello Raspberry Pi displays on hello dashboard.</span></span>

![Merhaba Raspberry Pi'yi telemetrisini görüntüleme][img-telemetry-display]

## <a name="act-on-hello-device"></a><span data-ttu-id="3aec3-109">Merhaba aygıtta hareket</span><span class="sxs-lookup"><span data-stu-id="3aec3-109">Act on hello device</span></span>

<span data-ttu-id="3aec3-110">Merhaba çözüm panodan, Raspberry Pi'yi yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aec3-110">From hello solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="3aec3-111">Merhaba Raspberry Pi'yi toohello Uzaktan izleme çözümü bağlandığında, desteklediği hello yöntemleri hakkında bilgi gönderir.</span><span class="sxs-lookup"><span data-stu-id="3aec3-111">When hello Raspberry Pi connects toohello remote monitoring solution, it sends information about hello methods it supports.</span></span>

- <span data-ttu-id="3aec3-112">Merhaba çözüm panosunda tıklatın **aygıtları** toovisit hello **aygıtları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="3aec3-112">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="3aec3-113">Hello Raspberry Pi'yi seçin **cihaz listesi**.</span><span class="sxs-lookup"><span data-stu-id="3aec3-113">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="3aec3-114">Ardından **yöntemleri**:</span><span class="sxs-lookup"><span data-stu-id="3aec3-114">Then choose **Methods**:</span></span>

    ![Panoda aygıtları listele][img-list-devices]

- <span data-ttu-id="3aec3-116">Merhaba üzerinde **yöntemi çağırma** sayfasında, **LightBlink** hello içinde **yöntemi** açılır.</span><span class="sxs-lookup"><span data-stu-id="3aec3-116">On hello **Invoke Method** page, choose **LightBlink** in hello **Method** dropdown.</span></span>

- <span data-ttu-id="3aec3-117">Seçin **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="3aec3-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="3aec3-118">Merhaba simulator Raspberry Pi'yi hello üzerinde bir ileti hello konsolunda yazdırır.</span><span class="sxs-lookup"><span data-stu-id="3aec3-118">hello simulator prints a message in hello console on hello Raspberry Pi.</span></span> <span data-ttu-id="3aec3-119">Merhaba Raspberry Pi'yi Hello uygulamasına bir bildirim geri toohello çözüm Panosu gönderir:</span><span class="sxs-lookup"><span data-stu-id="3aec3-119">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard:</span></span>

    ![Yöntem geçmişini göster][img-method-history]

- <span data-ttu-id="3aec3-121">Hello kullanarak açma ve kapatma hello LED geçebilirsiniz **ChangeLightStatus** yöntemi ile bir **LightStatusValue** çok ayarlamak**1** için üzerinde veya **0** için devre dışı.</span><span class="sxs-lookup"><span data-stu-id="3aec3-121">You can switch hello LED on and off using hello **ChangeLightStatus** method with a **LightStatusValue** set too**1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="3aec3-122">Merhaba Uzaktan izleme çözümü Azure hesabınızda çalışan bırakırsanız hello çalıştırıldığında için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="3aec3-122">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="3aec3-123">Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="3aec3-123">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="3aec3-124">Bunu kullanmayı bitirdikten sonra hello önceden yapılandırılmış çözümü Azure hesabınızdan silin.</span><span class="sxs-lookup"><span data-stu-id="3aec3-124">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
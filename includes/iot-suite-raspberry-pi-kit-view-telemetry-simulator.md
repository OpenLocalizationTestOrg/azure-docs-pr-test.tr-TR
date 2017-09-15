## <a name="view-the-telemetry"></a><span data-ttu-id="c0a0e-101">Telemetriyi görüntüleyebilir</span><span class="sxs-lookup"><span data-stu-id="c0a0e-101">View the telemetry</span></span>

<span data-ttu-id="c0a0e-102">Raspberry Pi'yi, artık uzaktan izleme çözümüne telemetri gönderiyor.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-102">The Raspberry Pi is now sending telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="c0a0e-103">Çözüm panosunda telemetri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-103">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="c0a0e-104">Ayrıca, Raspberry Pi'yi çözüm panodan iletisi gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-104">You can also send messages to your Raspberry Pi from the solution dashboard.</span></span>

- <span data-ttu-id="c0a0e-105">Çözüm panosuna gidin.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-105">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="c0a0e-106">Cihazınızı seçmek **cihaz görünümüne** açılır.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-106">Select your device in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="c0a0e-107">Raspberry Pi'yi telemetrisinden Panoda görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-107">The telemetry from the Raspberry Pi displays on the dashboard.</span></span>

![Raspberry Pi'yi telemetrisini görüntüleme][img-telemetry-display]

## <a name="act-on-the-device"></a><span data-ttu-id="c0a0e-109">Cihazda hareket</span><span class="sxs-lookup"><span data-stu-id="c0a0e-109">Act on the device</span></span>

<span data-ttu-id="c0a0e-110">Çözüm panodan, Raspberry Pi'yi yöntemleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-110">From the solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="c0a0e-111">Uzaktan izleme çözümüne Raspberry Pi'yi bağlandığında, desteklediği yöntemleri hakkında bilgi gönderir.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-111">When the Raspberry Pi connects to the remote monitoring solution, it sends information about the methods it supports.</span></span>

- <span data-ttu-id="c0a0e-112">Çözüm panosunda tıklatın **aygıtları** ziyaret etmek için **aygıtları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-112">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="c0a0e-113">Böğürtlenli Pi seçin **cihaz listesi**.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-113">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="c0a0e-114">Ardından **yöntemleri**:</span><span class="sxs-lookup"><span data-stu-id="c0a0e-114">Then choose **Methods**:</span></span>

    ![Panoda aygıtları listele][img-list-devices]

- <span data-ttu-id="c0a0e-116">Üzerinde **yöntemi çağırma** sayfasında, **LightBlink** içinde **yöntemi** açılır.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-116">On the **Invoke Method** page, choose **LightBlink** in the **Method** dropdown.</span></span>

- <span data-ttu-id="c0a0e-117">Seçin **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="c0a0e-118">Simulator konsolunda bir ileti üzerinde Raspberry Pi'yi yazdırır.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-118">The simulator prints a message in the console on the Raspberry Pi.</span></span> <span data-ttu-id="c0a0e-119">Uygulamasını Raspberry Pi'yi çözüm panosuna geri bildirim gönderir:</span><span class="sxs-lookup"><span data-stu-id="c0a0e-119">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard:</span></span>

    ![Yöntem geçmişini göster][img-method-history]

- <span data-ttu-id="c0a0e-121">Kullanarak açma ve kapatma LED geçebilirsiniz **ChangeLightStatus** yöntemi ile bir **LightStatusValue** kümesine **1** için üzerinde veya **0** için devre dışı.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-121">You can switch the LED on and off using the **ChangeLightStatus** method with a **LightStatusValue** set to **1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="c0a0e-122">Azure hesabınızda çalıştıran uzaktan izleme çözümü bırakırsanız çalıştırıldığında için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-122">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="c0a0e-123">Uzaktan izleme çözümü çalışırken tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="c0a0e-123">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="c0a0e-124">Bunu kullanmayı bitirdikten sonra önceden yapılandırılmış çözümü Azure hesabınızdan silin.</span><span class="sxs-lookup"><span data-stu-id="c0a0e-124">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
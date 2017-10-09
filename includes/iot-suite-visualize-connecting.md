## <a name="view-device-telemetry-in-hello-dashboard"></a><span data-ttu-id="b212c-101">Görünüm cihaz telemetrisi hello panosunda</span><span class="sxs-lookup"><span data-stu-id="b212c-101">View device telemetry in hello dashboard</span></span>
<span data-ttu-id="b212c-102">Uzaktan izleme çözümü sağlar, tooview hello telemetri aygıtlarınızı tooIoT Hub Gönder hello panosunda Hello.</span><span class="sxs-lookup"><span data-stu-id="b212c-102">hello dashboard in hello remote monitoring solution enables you tooview hello telemetry your devices send tooIoT Hub.</span></span>

1. <span data-ttu-id="b212c-103">Tarayıcınızda dönüş toohello Uzaktan izleme çözüm panosunu, tıklatın **aygıtları** hello Sol paneli toonavigate toohello içinde **cihazlar listesi**.</span><span class="sxs-lookup"><span data-stu-id="b212c-103">In your browser, return toohello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="b212c-104">Merhaba, **cihazlar listesi**, Cihazınızı hello durumunu olduğunu görmeniz gerekir **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="b212c-104">In hello **Devices list**, you should see that hello status of your device is **Running**.</span></span> <span data-ttu-id="b212c-105">Aksi durumda, tıklatın **aygıtı etkinleştir** hello içinde **cihaz ayrıntıları** paneli.</span><span class="sxs-lookup"><span data-stu-id="b212c-105">If not, click **Enable Device** in hello **Device Details** panel.</span></span>
   
    ![Cihaz durumunu görüntüle][18]
3. <span data-ttu-id="b212c-107">Tıklatın **Pano** tooreturn toohello Pano hello Cihazınızı seçin **aygıt tooView** açılan tooview kendi telemetri.</span><span class="sxs-lookup"><span data-stu-id="b212c-107">Click **Dashboard** tooreturn toohello dashboard, select your device in hello **Device tooView** drop-down tooview its telemetry.</span></span> <span data-ttu-id="b212c-108">Merhaba telemetri hello örnek uygulamadan iç sıcaklık için 50 birime, 55 birimleri için dış sıcaklık ve nem için 50 birime ' dir.</span><span class="sxs-lookup"><span data-stu-id="b212c-108">hello telemetry from hello sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Cihaz telemetrisini görüntüleme][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="b212c-110">Cihazınızda bir yöntem çağırma</span><span class="sxs-lookup"><span data-stu-id="b212c-110">Invoke a method on your device</span></span>
<span data-ttu-id="b212c-111">Hello Pano hello Uzaktan izleme çözümünde IOT hub'ı aracılığıyla aygıtlarınızdaki tooinvoke yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b212c-111">hello dashboard in hello remote monitoring solution enables you tooinvoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="b212c-112">Örneğin, hello Uzaktan izleme çözümü, bir aygıt yeniden başlatma yöntemini toosimulate çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b212c-112">For example, in hello remote monitoring solution you can invoke a method toosimulate rebooting a device.</span></span>

1. <span data-ttu-id="b212c-113">Merhaba Uzaktan izleme çözüm panosunda, tıklatın **aygıtları** hello Sol paneli toonavigate toohello içinde **cihazlar listesi**.</span><span class="sxs-lookup"><span data-stu-id="b212c-113">In hello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="b212c-114">Tıklatın **cihaz kimliği** aygıtınızın hello **cihazlar listesi**.</span><span class="sxs-lookup"><span data-stu-id="b212c-114">Click **Device ID** for your device in hello **Devices list**.</span></span>
3. <span data-ttu-id="b212c-115">Merhaba, **cihaz ayrıntıları** öğesine tıklayın **yöntemleri**.</span><span class="sxs-lookup"><span data-stu-id="b212c-115">In hello **Device details** panel, click **Methods**.</span></span>
   
    ![Cihaz yöntemleri][13]
4. <span data-ttu-id="b212c-117">Merhaba, **yöntemi** açılan listesinde, select **InitiateFirmwareUpdate**ve ardından **FWPACKAGEURI** sahte bir URL girin.</span><span class="sxs-lookup"><span data-stu-id="b212c-117">In hello **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="b212c-118">Tıklatın **yöntemi çağırma** hello aygıtta toocall hello yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b212c-118">Click **Invoke Method** toocall hello method on hello device.</span></span>
   
    ![Cihaz yöntemi çağırma][14]
   

5. <span data-ttu-id="b212c-120">Merhaba aygıt hello yöntemi işlediğinde aygıt kodunuzu çalıştırmaya hello konsolunda bir ileti görür.</span><span class="sxs-lookup"><span data-stu-id="b212c-120">You see a message in hello console running your device code when hello device handles hello method.</span></span> <span data-ttu-id="b212c-121">Merhaba yöntemi Hello sonuçlarını toohello geçmişi hello çözüm portalında eklendi:</span><span class="sxs-lookup"><span data-stu-id="b212c-121">hello results of hello method are added toohello history in hello solution portal:</span></span>

    ![Yöntem geçmişini görüntüleme][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="b212c-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b212c-123">Next steps</span></span>
<span data-ttu-id="b212c-124">Merhaba makale [özelleştirme önceden yapılandırılmış çözümleri] [ lnk-customize] Bu örnek genişletebilir bazı yolları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b212c-124">hello article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="b212c-125">Gerçek sensörler kullanma ve ek komutlar uygulama gibi eklemeler yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b212c-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="b212c-126">Merhaba hakkında daha fazla bilgiyi [hello azureiotsuite.com sitesindeki izinler][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="b212c-126">You can learn more about hello [permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md

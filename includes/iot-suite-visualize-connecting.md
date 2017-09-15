## <a name="view-device-telemetry-in-the-dashboard"></a><span data-ttu-id="1aca9-101">Cihaz telemetrisini panoda görüntüleme</span><span class="sxs-lookup"><span data-stu-id="1aca9-101">View device telemetry in the dashboard</span></span>
<span data-ttu-id="1aca9-102">Uzaktan izleme çözümündeki pano, cihazlarınızın IoT Hub'a gönderdiği telemetriyi görüntülemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1aca9-102">The dashboard in the remote monitoring solution enables you to view the telemetry your devices send to IoT Hub.</span></span>

1. <span data-ttu-id="1aca9-103">Tarayıcınızda uzaktan izleme çözümü panosuna dönün, sol taraftaki **Cihazlar** paneline tıklayın ve **Cihaz listesi** sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="1aca9-103">In your browser, return to the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="1aca9-104">**Cihaz listesinde** cihazınızın durumu **Çalışıyor** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1aca9-104">In the **Devices list**, you should see that the status of your device is **Running**.</span></span> <span data-ttu-id="1aca9-105">Değilse **Cihaz Ayrıntıları** panelinden **Cihazı Etkinleştir**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1aca9-105">If not, click **Enable Device** in the **Device Details** panel.</span></span>
   
    ![Cihaz durumunu görüntüle][18]
3. <span data-ttu-id="1aca9-107">**Pano**'ya tıklayarak panoya dönün ve telemetrisini görüntülemek için **Görüntülenecek Cihaz** açılır menüsünden cihazınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="1aca9-107">Click **Dashboard** to return to the dashboard, select your device in the **Device to View** drop-down to view its telemetry.</span></span> <span data-ttu-id="1aca9-108">Örnek uygulamadan gelen telemetri iç ortam sıcaklığı için 50 birim, dış ortam sıcaklığı için 55 birim ve nem için 50 birim şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1aca9-108">The telemetry from the sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Cihaz telemetrisini görüntüleme][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="1aca9-110">Cihazınızda bir yöntem çağırma</span><span class="sxs-lookup"><span data-stu-id="1aca9-110">Invoke a method on your device</span></span>
<span data-ttu-id="1aca9-111">Uzaktan izleme çözümündeki pano, IoT Hub aracılığıyla cihazlarınızda yöntem çağırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="1aca9-111">The dashboard in the remote monitoring solution enables you to invoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="1aca9-112">Örneğin uzaktan izleme çözümünde cihazın yeniden başlatılması benzetimini yapmak için bir yöntem çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1aca9-112">For example, in the remote monitoring solution you can invoke a method to simulate rebooting a device.</span></span>

1. <span data-ttu-id="1aca9-113">Uzaktan izleme çözümü panosunda, sol taraftaki **Cihazlar** paneline tıklayın ve **Cihaz listesi** sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="1aca9-113">In the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="1aca9-114">**Cihaz listesi** bölümünde cihazınızın **Cihaz kimliğine** tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1aca9-114">Click **Device ID** for your device in the **Devices list**.</span></span>
3. <span data-ttu-id="1aca9-115">**Cihaz ayrıntıları** panelinde **Yöntemler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1aca9-115">In the **Device details** panel, click **Methods**.</span></span>
   
    ![Cihaz yöntemleri][13]
4. <span data-ttu-id="1aca9-117">**Yöntem** açılır menüsünde **InitiateFirmwareUpdate** seçin ve **FWPACKAGEURI** alanına işlevsiz bir URL girin.</span><span class="sxs-lookup"><span data-stu-id="1aca9-117">In the **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="1aca9-118">Yöntemi cihazda çağırmak için **Yöntemi Çağır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1aca9-118">Click **Invoke Method** to call the method on the device.</span></span>
   
    ![Cihaz yöntemi çağırma][14]
   

5. <span data-ttu-id="1aca9-120">Cihaz yöntemi işlediğinde cihazınızın kodunu çalıştıran konsolda bir ileti göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1aca9-120">You see a message in the console running your device code when the device handles the method.</span></span> <span data-ttu-id="1aca9-121">Yöntemin sonuçları, çözüm portalındaki geçmişe eklenir:</span><span class="sxs-lookup"><span data-stu-id="1aca9-121">The results of the method are added to the history in the solution portal:</span></span>

    ![Yöntem geçmişini görüntüleme][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="1aca9-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1aca9-123">Next steps</span></span>
<span data-ttu-id="1aca9-124">[Önceden yapılandırılmış çözümleri özelleştirme][lnk-customize] makalesinde bu örneği bir adım ileri taşımak için kullanabileceğiniz adımlar anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1aca9-124">The article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="1aca9-125">Gerçek sensörler kullanma ve ek komutlar uygulama gibi eklemeler yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1aca9-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="1aca9-126">İzinler hakkında daha fazla bilgi için [azureiotsuite.com sitesini][lnk-permissions] inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1aca9-126">You can learn more about the [permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md

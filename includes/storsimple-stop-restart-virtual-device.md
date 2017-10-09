#### <a name="toostop-and-start-a-virtual-device"></a><span data-ttu-id="7a5a9-101">toostop ve başlangıç sanal cihazı</span><span class="sxs-lookup"><span data-stu-id="7a5a9-101">toostop and start a virtual device</span></span>
<span data-ttu-id="7a5a9-102">toostop sanal cihaz adına tıklayın ve ardından **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="7a5a9-102">toostop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="7a5a9-103">Merhaba sanal cihaz kapatıldığı sırada durumundadır **durdurma**.</span><span class="sxs-lookup"><span data-stu-id="7a5a9-103">While hello virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="7a5a9-104">Merhaba sanal cihaz kapatıldıktan sonra durumundadır **durduruldu**.</span><span class="sxs-lookup"><span data-stu-id="7a5a9-104">After hello virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="7a5a9-105">Cmdlet'leri toostop aşağıdaki hello kullanın ve sanal cihazı başlatın.</span><span class="sxs-lookup"><span data-stu-id="7a5a9-105">Use hello following cmdlets toostop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a><span data-ttu-id="7a5a9-106">toorestart sanal cihazı</span><span class="sxs-lookup"><span data-stu-id="7a5a9-106">toorestart a virtual device</span></span>
<span data-ttu-id="7a5a9-107">Sanal cihaz çalışırken ve toorestart istediğinizde, adına tıklayın ve ardından **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="7a5a9-107">When a virtual device is running and you want toorestart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="7a5a9-108">Merhaba sanal cihaz yeniden başlatıldığı sırada durumundadır **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="7a5a9-108">While hello virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="7a5a9-109">Merhaba sanal aygıt, toouse hazır olduğunda durumundadır **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="7a5a9-109">When hello virtual device is ready for you toouse, its status is **Running**.</span></span>

<span data-ttu-id="7a5a9-110">Aşağıdaki cmdlet'i toorestart sanal cihazı hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a5a9-110">Use hello following cmdlet toorestart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`


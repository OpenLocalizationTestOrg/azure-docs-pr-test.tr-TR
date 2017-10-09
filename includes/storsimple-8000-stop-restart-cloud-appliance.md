#### <a name="toostop-and-start-a-cloud-appliance"></a><span data-ttu-id="c1d05-101">toostop ve başlangıç bulut uygulaması</span><span class="sxs-lookup"><span data-stu-id="c1d05-101">toostop and start a cloud appliance</span></span>

1. <span data-ttu-id="c1d05-102">toostop bulut uygulaması toohello VM bulut uygulaması için gidin.</span><span class="sxs-lookup"><span data-stu-id="c1d05-102">toostop a cloud appliance, go toohello VM for your cloud appliance.</span></span>
    <span data-ttu-id="c1d05-103">![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="c1d05-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="c1d05-104">Merhaba Komut çubuğundaki **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="c1d05-104">From hello command bar, click **Stop**.</span></span>

    ![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="c1d05-106">Onayınız istendiğinde **Evet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c1d05-106">When prompted for confirmation, click **Yes**.</span></span>

    ![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="c1d05-108">Bir VM durdurulduğunda serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="c1d05-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="c1d05-109">Merhaba bulut uygulaması durdurma olsa da, durumundadır **Deallocating**.</span><span class="sxs-lookup"><span data-stu-id="c1d05-109">While hello cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="c1d05-110">Merhaba bulut uygulaması durdurulduktan sonra durumundadır **durduruldu (serbest bırakıldı)**.</span><span class="sxs-lookup"><span data-stu-id="c1d05-110">After hello cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="c1d05-112">Bir VM durdurulduğunda tıklatın **Başlat** (düğmesi kullanılabilir olur) toostart hello VM.</span><span class="sxs-lookup"><span data-stu-id="c1d05-112">Once a VM is stopped, click **Start** (button becomes available) toostart hello VM.</span></span> <span data-ttu-id="c1d05-113">Merhaba bulut uygulaması başladıktan sonra durumundadır **başlatıldı**.</span><span class="sxs-lookup"><span data-stu-id="c1d05-113">After hello cloud appliance has started up, its status is **Started**.</span></span>

    ![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="c1d05-115">Cmdlet'leri toostop aşağıdaki hello kullanın ve bulut uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="c1d05-115">Use hello following cmdlets toostop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a><span data-ttu-id="c1d05-116">toorestart bulut uygulaması</span><span class="sxs-lookup"><span data-stu-id="c1d05-116">toorestart a cloud appliance</span></span>

<span data-ttu-id="c1d05-117">toorestart bulut uygulaması toohello VM bulut uygulaması için gidin.</span><span class="sxs-lookup"><span data-stu-id="c1d05-117">toorestart a cloud appliance, go toohello VM for your cloud appliance.</span></span> <span data-ttu-id="c1d05-118">Merhaba Komut çubuğundaki **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="c1d05-118">From hello command bar, click **Restart**.</span></span> <span data-ttu-id="c1d05-119">İstendiğinde, hello yeniden onaylayın.</span><span class="sxs-lookup"><span data-stu-id="c1d05-119">When prompted, confirm hello restart.</span></span> <span data-ttu-id="c1d05-120">Merhaba bulut uygulaması, toouse hazır olduğunda, durumundadır **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="c1d05-120">When hello cloud appliance is ready for you toouse, its status is **Running**.</span></span>

![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="c1d05-122">Cmdlet toorestart bulut uygulaması aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="c1d05-122">Use hello following cmdlet toorestart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`


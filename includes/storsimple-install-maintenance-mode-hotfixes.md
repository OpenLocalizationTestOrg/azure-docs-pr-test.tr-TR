<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="c9a62-101">StorSimple için Windows PowerShell aracılığıyla Bakım modu düzeltmeler yüklemek için</span><span class="sxs-lookup"><span data-stu-id="c9a62-101">To install Maintenance mode hotfixes via Windows PowerShell for StorSimple</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c9a62-102">Bakım modunda bir denetleyici ve ardından diğer denetleyicisi ilk düzeltmeyi uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9a62-102">In Maintenance mode, you need to apply the hotfix first on one controller and then on the other controller.</span></span>
> 
> 

1. <span data-ttu-id="c9a62-103">Cihazın bakım moduna yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="c9a62-103">Place the device into Maintenance mode.</span></span> <span data-ttu-id="c9a62-104">Bkz: [2. adım: girin Bakım modu](../articles/storsimple/storsimple-update-device.md#step2) bakım moduna hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="c9a62-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how to enter Maintenance mode.</span></span>
2. <span data-ttu-id="c9a62-105">Düzeltmeyi uygulamak için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="c9a62-105">To apply the hotfix, type:</span></span>
   
     `Start-HcsHotfix` 
3. <span data-ttu-id="c9a62-106">İstendiğinde, düzeltme dosyalarını içeren ağ paylaşılan klasörün yolunu sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c9a62-106">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
4. <span data-ttu-id="c9a62-107">Onayınız istenir.</span><span class="sxs-lookup"><span data-stu-id="c9a62-107">You will be prompted for confirmation.</span></span> <span data-ttu-id="c9a62-108">Tür **Y** düzeltme yüklemeye devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="c9a62-108">Type **Y** to proceed with the hotfix installation.</span></span>
5. <span data-ttu-id="c9a62-109">Bir denetleyicisinde düzeltmeyi uyguladıktan sonra diğer denetleyiciye oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c9a62-109">After you have applied the hotfix on one controller, log on to the other controller.</span></span> <span data-ttu-id="c9a62-110">Önceki denetleyici için yaptığınız gibi düzeltmeyi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c9a62-110">Apply the hotfix as you did for the previous controller.</span></span>
6. <span data-ttu-id="c9a62-111">Düzeltmeleri uyguladıktan sonra bakım modundan çıkın.</span><span class="sxs-lookup"><span data-stu-id="c9a62-111">After the hotfixes are applied, exit Maintenance mode.</span></span> <span data-ttu-id="c9a62-112">Bkz: [4. adım: çıkış Bakım modu](../articles/storsimple/storsimple-update-device.md#step4) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="c9a62-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span></span>


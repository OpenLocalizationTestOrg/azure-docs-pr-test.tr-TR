<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="1ad08-101">tooinstall StorSimple için Windows PowerShell aracılığıyla Bakım modu düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="1ad08-101">tooinstall Maintenance mode hotfixes via Windows PowerShell for StorSimple</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1ad08-102">Bakım modunda tooapply hello düzeltme önce bir denetleyicisinde gerekir ve ardından üzerindeki diğer denetleyicisi hello.</span><span class="sxs-lookup"><span data-stu-id="1ad08-102">In Maintenance mode, you need tooapply hello hotfix first on one controller and then on hello other controller.</span></span>
> 
> 

1. <span data-ttu-id="1ad08-103">Merhaba aygıt bakım moduna yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="1ad08-103">Place hello device into Maintenance mode.</span></span> <span data-ttu-id="1ad08-104">Bkz: [2. adım: girin Bakım modu](../articles/storsimple/storsimple-update-device.md#step2) yönelik yönergeler tooenter Bakım modu.</span><span class="sxs-lookup"><span data-stu-id="1ad08-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how tooenter Maintenance mode.</span></span>
2. <span data-ttu-id="1ad08-105">tooapply hello düzeltme, türü:</span><span class="sxs-lookup"><span data-stu-id="1ad08-105">tooapply hello hotfix, type:</span></span>
   
     `Start-HcsHotfix` 
3. <span data-ttu-id="1ad08-106">İstendiğinde, hello düzeltme dosyalarını içeren hello yolu toohello ağ paylaşılan klasöründe sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ad08-106">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
4. <span data-ttu-id="1ad08-107">Onayınız istenir.</span><span class="sxs-lookup"><span data-stu-id="1ad08-107">You will be prompted for confirmation.</span></span> <span data-ttu-id="1ad08-108">Tür **Y** tooproceed hello düzeltme yüklemesi ile.</span><span class="sxs-lookup"><span data-stu-id="1ad08-108">Type **Y** tooproceed with hello hotfix installation.</span></span>
5. <span data-ttu-id="1ad08-109">Sonra hello düzeltme bir denetleyicisinde oturum açma toohello diğer denetleyicisi uyguladınız.</span><span class="sxs-lookup"><span data-stu-id="1ad08-109">After you have applied hello hotfix on one controller, log on toohello other controller.</span></span> <span data-ttu-id="1ad08-110">Merhaba önceki denetleyici için yaptığınız gibi hello düzeltmeyi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="1ad08-110">Apply hello hotfix as you did for hello previous controller.</span></span>
6. <span data-ttu-id="1ad08-111">Merhaba düzeltmeleri uyguladıktan sonra bakım modundan çıkın.</span><span class="sxs-lookup"><span data-stu-id="1ad08-111">After hello hotfixes are applied, exit Maintenance mode.</span></span> <span data-ttu-id="1ad08-112">Bkz: [4. adım: çıkış Bakım modu](../articles/storsimple/storsimple-update-device.md#step4) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="1ad08-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span></span>


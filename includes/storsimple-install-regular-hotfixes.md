<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="0861f-101">StorSimple için Windows PowerShell aracılığıyla normal düzeltmeler yüklemek için</span><span class="sxs-lookup"><span data-stu-id="0861f-101">To install regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="0861f-102">Cihaz seri konsoluna bağlanmak.</span><span class="sxs-lookup"><span data-stu-id="0861f-102">Connect to the device serial console.</span></span> <span data-ttu-id="0861f-103">Daha fazla bilgi için bkz: [1. adım: seri konsoluna bağlanmak](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="0861f-103">For more information, see [Step 1: Connect to the serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="0861f-104">Seri konsol menüsünde seçeneğini 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="0861f-104">In the serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="0861f-105">Parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="0861f-105">Type the password.</span></span> <span data-ttu-id="0861f-106">Varsayılan parola **Parola1**.</span><span class="sxs-lookup"><span data-stu-id="0861f-106">The default password is **Password1**.</span></span>
3. <span data-ttu-id="0861f-107">Komut istemine yazın:</span><span class="sxs-lookup"><span data-stu-id="0861f-107">At the command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="0861f-108">Bu komut, yalnızca normal düzeltmeleri uygular.</span><span class="sxs-lookup"><span data-stu-id="0861f-108">This command applies only to regular hotfixes.</span></span> <span data-ttu-id="0861f-109">Bu komut yalnızca bir denetleyicisinde çalıştırın, ancak her iki denetleyicileri güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="0861f-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="0861f-110">Denetleyici yük devretmesi güncelleştirme işlemi sırasında fark edebilirsiniz; Ancak, yük devretme sistem kullanılabilirliğini veya işlem etkilemez.</span><span class="sxs-lookup"><span data-stu-id="0861f-110">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="0861f-111">İstendiğinde, düzeltme dosyalarını içeren ağ paylaşılan klasörün yolunu sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0861f-111">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
5. <span data-ttu-id="0861f-112">Onayınız istenir.</span><span class="sxs-lookup"><span data-stu-id="0861f-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="0861f-113">Tür **Y** düzeltme yüklemeye devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="0861f-113">Type **Y** to proceed with the hotfix installation.</span></span>


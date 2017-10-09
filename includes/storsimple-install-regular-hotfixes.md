<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="df325-101">StorSimple için Windows PowerShell aracılığıyla tooinstall normal düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="df325-101">tooinstall regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="df325-102">Toohello cihaz seri konsoluna bağlayın.</span><span class="sxs-lookup"><span data-stu-id="df325-102">Connect toohello device serial console.</span></span> <span data-ttu-id="df325-103">Daha fazla bilgi için bkz: [1. adım: toohello seri konsol bağlantısı](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="df325-103">For more information, see [Step 1: Connect toohello serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="df325-104">Merhaba seri konsol menüsünde seçeneğini 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="df325-104">In hello serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="df325-105">Merhaba parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="df325-105">Type hello password.</span></span> <span data-ttu-id="df325-106">Merhaba varsayılan parola **Parola1**.</span><span class="sxs-lookup"><span data-stu-id="df325-106">hello default password is **Password1**.</span></span>
3. <span data-ttu-id="df325-107">Merhaba komut satırına aşağıdakini yazın:</span><span class="sxs-lookup"><span data-stu-id="df325-107">At hello command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="df325-108">Bu komut yalnızca tooregular düzeltmeleri uygular.</span><span class="sxs-lookup"><span data-stu-id="df325-108">This command applies only tooregular hotfixes.</span></span> <span data-ttu-id="df325-109">Bu komut yalnızca bir denetleyicisinde çalıştırın, ancak her iki denetleyicileri güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="df325-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="df325-110">Denetleyici yük devretmesi hello güncelleştirme işlemi sırasında fark edebilirsiniz; Ancak, hello yük devretme sistem kullanılabilirliğini veya işlem etkilemez.</span><span class="sxs-lookup"><span data-stu-id="df325-110">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="df325-111">İstendiğinde, hello düzeltme dosyalarını içeren hello yolu toohello ağ paylaşılan klasöründe sağlayın.</span><span class="sxs-lookup"><span data-stu-id="df325-111">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
5. <span data-ttu-id="df325-112">Onayınız istenir.</span><span class="sxs-lookup"><span data-stu-id="df325-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="df325-113">Tür **Y** tooproceed hello düzeltme yüklemesi ile.</span><span class="sxs-lookup"><span data-stu-id="df325-113">Type **Y** tooproceed with hello hotfix installation.</span></span>


<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="a1456-101">StorSimple için Windows PowerShell aracılığıyla tooinstall düzenli güncelleştirmeler</span><span class="sxs-lookup"><span data-stu-id="a1456-101">tooinstall regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="a1456-102">Açık hello cihaz seri konsoluna ve seçenek 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="a1456-102">Open hello device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="a1456-103">Merhaba parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="a1456-103">Type hello password.</span></span> <span data-ttu-id="a1456-104">Merhaba varsayılan parola *Parola1*.</span><span class="sxs-lookup"><span data-stu-id="a1456-104">hello default password is *Password1*.</span></span> 
2. <span data-ttu-id="a1456-105">Merhaba komut satırına aşağıdakini yazın:</span><span class="sxs-lookup"><span data-stu-id="a1456-105">At hello command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="a1456-106">Güncelleştirmeler varsa ve kesintiye uğratan veya benzer hello güncelleştirmelerin olup olmadığını size bildirilecek.</span><span class="sxs-lookup"><span data-stu-id="a1456-106">You will be notified if updates are available and whether hello updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="a1456-107">Merhaba komut satırına aşağıdakini yazın:</span><span class="sxs-lookup"><span data-stu-id="a1456-107">At hello command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="a1456-108">Merhaba güncelleştirme işlemi başlar.</span><span class="sxs-lookup"><span data-stu-id="a1456-108">hello update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="a1456-109">Bu komut yalnızca tooregular güncelleştirmeleri uygular.</span><span class="sxs-lookup"><span data-stu-id="a1456-109">This command applies only tooregular updates.</span></span> <span data-ttu-id="a1456-110">Bu komut yalnızca bir denetleyicisinde çalıştırın, ancak her iki denetleyicileri güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a1456-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="a1456-111">Denetleyici yük devretmesi hello güncelleştirme işlemi sırasında fark edebilirsiniz; Ancak, hello yük devretme sistem kullanılabilirliğini veya işlem etkilemez.</span><span class="sxs-lookup"><span data-stu-id="a1456-111">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>
> 
> 


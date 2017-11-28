<!--author=SharS last changed: 11/18/16-->

#### <a name="to-install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="36a19-101">StorSimple için Windows PowerShell aracılığıyla düzenli olarak güncelleştirmeleri yüklemek için</span><span class="sxs-lookup"><span data-stu-id="36a19-101">To install regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="36a19-102">Cihaz seri konsoluna açıp seçenek 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="36a19-102">Open the device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="36a19-103">Parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="36a19-103">Type the password.</span></span> <span data-ttu-id="36a19-104">Varsayılan parola *Parola1*.</span><span class="sxs-lookup"><span data-stu-id="36a19-104">The default password is *Password1*.</span></span> 
2. <span data-ttu-id="36a19-105">Komut istemine yazın:</span><span class="sxs-lookup"><span data-stu-id="36a19-105">At the command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="36a19-106">Güncelleştirmeler varsa ve güncelleştirmeleri kesintiye uğratan veya benzer olup bildirilir.</span><span class="sxs-lookup"><span data-stu-id="36a19-106">You will be notified if updates are available and whether the updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="36a19-107">Komut istemine yazın:</span><span class="sxs-lookup"><span data-stu-id="36a19-107">At the command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="36a19-108">Güncelleştirme işlemi başlar.</span><span class="sxs-lookup"><span data-stu-id="36a19-108">The update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="36a19-109">Bu komut, yalnızca normal güncelleştirmeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="36a19-109">This command applies only to regular updates.</span></span> <span data-ttu-id="36a19-110">Bu komut yalnızca bir denetleyicisinde çalıştırın, ancak her iki denetleyicileri güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="36a19-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="36a19-111">Denetleyici yük devretmesi güncelleştirme işlemi sırasında fark edebilirsiniz; Ancak, yük devretme sistem kullanılabilirliğini veya işlem etkilemez.</span><span class="sxs-lookup"><span data-stu-id="36a19-111">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>
> 
> 


<!--author=SharS last changed: 12/01/15-->

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="60348-101">Bakım modu girmek için</span><span class="sxs-lookup"><span data-stu-id="60348-101">To enter Maintenance mode</span></span>
1. <span data-ttu-id="60348-102">Seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="60348-102">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
2. <span data-ttu-id="60348-103">Parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="60348-103">Type the password.</span></span> <span data-ttu-id="60348-104">Varsayılan parola **Parola1**.</span><span class="sxs-lookup"><span data-stu-id="60348-104">The default password is **Password1**.</span></span>
3. <span data-ttu-id="60348-105">Komut istemine yazın</span><span class="sxs-lookup"><span data-stu-id="60348-105">At the command prompt, type</span></span>
   
     `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="60348-106">Bakım modu tüm g/ç istekleri kesintiye ve klasik Azure portalı bağlantısı sever ve onaylamanız istenir bildiren bir uyarı iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="60348-106">You will see a warning message telling you that Maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="60348-107">Tür **Y** bakım moduna girmek için.</span><span class="sxs-lookup"><span data-stu-id="60348-107">Type **Y** to enter Maintenance mode.</span></span>
   
    <span data-ttu-id="60348-108">Hem denetleyicileri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="60348-108">Both controllers will restart.</span></span> <span data-ttu-id="60348-109">Yeniden başlatma tamamlandıktan sonra aygıtın bakım modunda olduğunu gösteren başka bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="60348-109">When the restart is complete, another message will appear indicating that the device is in Maintenance mode.</span></span>


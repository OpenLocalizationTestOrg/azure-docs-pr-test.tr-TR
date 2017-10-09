<span data-ttu-id="c538b-101">Merhaba adımları toounregister bir işlem sunucusu hello yapılandırma sunucusu ile bağlantı durumunu bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="c538b-101">hello steps toounregister a process server differs depending on its connection status with hello Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="c538b-102">Bağlı durumdaki işlem sunucusunun kaydını kaldırma</span><span class="sxs-lookup"><span data-stu-id="c538b-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="c538b-103">Uzaktan hello işlem sunucusuna yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="c538b-103">Remote into hello process server as an Administrator.</span></span>
2. <span data-ttu-id="c538b-104">Merhaba başlatma **Denetim Masası** açarak **Programlar > program Kaldır**</span><span class="sxs-lookup"><span data-stu-id="c538b-104">Launch hello **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="c538b-105">Merhaba adıyla program Kaldır **Microsoft Azure Site kurtarma yapılandırması/işlem sunucusu**</span><span class="sxs-lookup"><span data-stu-id="c538b-105">Uninstall a program by hello name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="c538b-106">Adım 3 tamamlandıktan sonra **Microsoft Azure Site Recovery Yapılandırması/İşlem Sunucusu Bağımlılıkları**’nı kaldırabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c538b-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="c538b-107">Bağlantısı kesik durumdaki işlem sunucusunun kaydını kaldırma</span><span class="sxs-lookup"><span data-stu-id="c538b-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="c538b-108">Hiçbir şekilde toorevive hello sanal makine üzerinde hangi hello işlem sunucusu yüklü ise, aşağıdaki adımları kullanın hello kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c538b-108">Use hello below steps should be used if there is no way toorevive hello virtual machine on which hello Process Server was installed.</span></span>

1. <span data-ttu-id="c538b-109">Tooyour yapılandırma sunucusunda yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c538b-109">Log on tooyour configuration server as an Administrator.</span></span>
2. <span data-ttu-id="c538b-110">Bir yönetici komut istemi açın ve toohello dizin taraması `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="c538b-110">Open an Administrative command prompt and browse toohello directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="c538b-111">Şimdi hello komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c538b-111">Now run hello command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="c538b-112">Bu hello işlem sunucusu hello ayrıntılarını hello sistemden temizlenir.</span><span class="sxs-lookup"><span data-stu-id="c538b-112">This will purge hello details of hello process server from hello system.</span></span>

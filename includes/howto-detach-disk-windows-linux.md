<span data-ttu-id="85410-101">Ekli tooa sanal makine veri diski artık ihtiyacınız olduğunda, kolayca ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85410-101">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="85410-102">Bir disk ayırma hello disk hello sanal makineden kaldırır, ancak hello disk hello Azure depolama hesabı ' silmez.</span><span class="sxs-lookup"><span data-stu-id="85410-102">Detaching a disk removes hello disk from hello virtual machine, but doesn't delete hello disk from hello Azure storage account.</span></span>

<span data-ttu-id="85410-103">Merhaba disk üzerindeki toouse hello mevcut verileri yeniden istiyorsanız, toohello iliştirebilirsiniz aynı sanal makine ya da başka bir.</span><span class="sxs-lookup"><span data-stu-id="85410-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="85410-104">bir işletim sistemi diski toodetach, ilk toodelete hello sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="85410-104">toodetach an operating system disk, you first need toodelete hello virtual machine.</span></span>
>

## <a name="find-hello-disk"></a><span data-ttu-id="85410-105">Başlangıç diski bulun</span><span class="sxs-lookup"><span data-stu-id="85410-105">Find hello disk</span></span>
<span data-ttu-id="85410-106">Disk hello veya tooverify istediğiniz hello adını bilmiyorsanız, önce onu detach, şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="85410-106">If you don't know hello name of hello disk or want tooverify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="85410-107">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85410-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="85410-108">Tıklatın **sanal makineleri**, ve ardından uygun VM seçin hello.</span><span class="sxs-lookup"><span data-stu-id="85410-108">Click **Virtual Machines**, and then select hello appropriate VM.</span></span>

3. <span data-ttu-id="85410-109">Tıklatın **diskleri** hello hello sanal makine Panosu kenarına altında sol **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="85410-109">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="85410-110">Merhaba sanal makine Pano hello adını ve eklenen tüm diskler türünü listeler.</span><span class="sxs-lookup"><span data-stu-id="85410-110">hello virtual machine dashboard lists hello name and type of all attached disks.</span></span> <span data-ttu-id="85410-111">Örneğin, bu ekran bir işletim sistemi (OS) diskine ve bir veri diskine sahip bir sanal makineyi göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="85410-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Veri diskini bulma](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a><span data-ttu-id="85410-113">Merhaba disk ayırma</span><span class="sxs-lookup"><span data-stu-id="85410-113">Detach hello disk</span></span>
1. <span data-ttu-id="85410-114">Hello ifadesini Azure portal'ı tıklatın **sanal makineleri**ve ardından toodetach istediğiniz hello veri diski hello sanal makine hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85410-114">From hello Azure portal, click **Virtual Machines**, and then click hello name of hello virtual machine that has hello data disk you want toodetach.</span></span>

2. <span data-ttu-id="85410-115">Tıklatın **diskleri** hello hello sanal makine Panosu kenarına altında sol **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="85410-115">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="85410-116">Toodetach hello diske tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85410-116">Click hello disk you want toodetach.</span></span>

  ![Merhaba disk toodetach tanımlayın](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="85410-118">Merhaba Komut çubuğundaki **ayırma**.</span><span class="sxs-lookup"><span data-stu-id="85410-118">From hello command bar, click **Detach**.</span></span>

  ![Merhaba bulun komutu ayırma](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="85410-120">Merhaba onay penceresinde **Evet** toodetach hello disk.</span><span class="sxs-lookup"><span data-stu-id="85410-120">In hello confirmation window, click **Yes** toodetach hello disk.</span></span>

  ![Ayrılıyor hello disk onaylayın](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="85410-122">Merhaba disk depolama alanında kalır, ancak artık ekli tooa sanal makine değil.</span><span class="sxs-lookup"><span data-stu-id="85410-122">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>

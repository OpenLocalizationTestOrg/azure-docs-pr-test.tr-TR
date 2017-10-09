
<span data-ttu-id="560ff-101">Diskler hakkında daha fazla bilgi için bkz. [Sanal Makineler için Diskler ve VHD’ler hakkında](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="560ff-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a><span data-ttu-id="560ff-102">Boş disk ekleme</span><span class="sxs-lookup"><span data-stu-id="560ff-102">Attach an empty disk</span></span>
1. <span data-ttu-id="560ff-103">Azure CLI 1.0 açın ve [tooyour Azure aboneliğine bağlanma](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="560ff-103">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="560ff-104">Azure Hizmet Yönetimi modunda olduğunuzdan emin olun (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="560ff-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="560ff-105">Girin `azure vm disk attach-new` toocreate ve hello aşağıdaki örnekte gösterildiği gibi yeni bir disk ekleyin.</span><span class="sxs-lookup"><span data-stu-id="560ff-105">Enter `azure vm disk attach-new` toocreate and attach a new disk as shown in hello following example.</span></span> <span data-ttu-id="560ff-106">Değiştir *myVM* , Linux sanal makineniz hello adla ve hello hello diskin boyutunu olan GB cinsinden belirtin *100GB* Bu örnekte:</span><span class="sxs-lookup"><span data-stu-id="560ff-106">Replace *myVM* with hello name of your Linux Virtual Machine and specify hello size of hello disk in GB, which is *100GB* in this example:</span></span>

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. <span data-ttu-id="560ff-107">Merhaba veri diski oluşturduktan ve bağlı sonra hello çıkışında da listelenir `azure vm disk list <virtual-machine-name>` hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="560ff-107">After hello data disk is created and attached, it's listed in hello output of `azure vm disk list <virtual-machine-name>` as shown in hello following example:</span></span>
   
    ```azurecli
    azure vm disk list TestVM
    ```

    <span data-ttu-id="560ff-108">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="560ff-108">hello output is similar toohello following example:</span></span>

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a><span data-ttu-id="560ff-109">Var olan bir diski ekleme</span><span class="sxs-lookup"><span data-stu-id="560ff-109">Attach an existing disk</span></span>
<span data-ttu-id="560ff-110">Var olan bir diskin eklenmesi için depolama hesabında bir .vhd olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="560ff-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span>

1. <span data-ttu-id="560ff-111">Azure CLI 1.0 açın ve [tooyour Azure aboneliğine bağlanma](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="560ff-111">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="560ff-112">Azure Hizmet Yönetimi modunda olduğunuzdan emin olun (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="560ff-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="560ff-113">Merhaba tooattach zaten istediğiniz VHD tooyour Azure aboneliği karşıya olmadığını kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="560ff-113">Check if hello VHD you want tooattach is already uploaded tooyour Azure subscription:</span></span>
   
    ```azurecli
    azure vm disk list
    ```

    <span data-ttu-id="560ff-114">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="560ff-114">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. <span data-ttu-id="560ff-115">Merhaba disk bulamazsanız toouse istediğiniz, kullanarak bir yerel VHD tooyour abonelik karşıya `azure vm disk create` veya `azure vm disk upload`.</span><span class="sxs-lookup"><span data-stu-id="560ff-115">If you don't find hello disk that you want toouse, you may upload a local VHD tooyour subscription by using `azure vm disk create` or `azure vm disk upload`.</span></span> <span data-ttu-id="560ff-116">Bir örneği `disk create` aşağıdaki örneğine hello olduğu gibi olacaktır:</span><span class="sxs-lookup"><span data-stu-id="560ff-116">An example of `disk create` would be as in hello following example:</span></span>
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    <span data-ttu-id="560ff-117">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="560ff-117">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   <span data-ttu-id="560ff-118">De kullanabilirsiniz `azure vm disk upload` tooupload bir VHD tooa belirli bir depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="560ff-118">You may also use `azure vm disk upload` tooupload a VHD tooa specific storage account.</span></span> <span data-ttu-id="560ff-119">Azure sanal makine veri diski hello hakkında daha fazla komutları toomanage okuma [burada üzerinden](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="560ff-119">Read more about hello commands toomanage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

4. <span data-ttu-id="560ff-120">Eklediğiniz artık hello VHD tooyour sanal makine istenen:</span><span class="sxs-lookup"><span data-stu-id="560ff-120">Now you attach hello desired VHD tooyour virtual machine:</span></span>
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   <span data-ttu-id="560ff-121">Emin tooreplace olun *myVM* sanal makinenizin hello adla ve *myVHD* istenen VHD ile.</span><span class="sxs-lookup"><span data-stu-id="560ff-121">Make sure tooreplace *myVM* with hello name of your virtual machine, and *myVHD* with your desired VHD.</span></span>

5. <span data-ttu-id="560ff-122">Merhaba disktir ekli toohello sanal makineyle doğrulayabilirsiniz `azure vm disk list <virtual-machine-name>`:</span><span class="sxs-lookup"><span data-stu-id="560ff-122">You can verify hello disk is attached toohello virtual machine with `azure vm disk list <virtual-machine-name>`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="560ff-123">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="560ff-123">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> <span data-ttu-id="560ff-124">Bir veri diski ekledikten sonra toohello sanal makineye toolog gerekir ve hello sanal makine hello disk depolama için kullanabileceğiniz şekilde hello diskini başlatmak (aşağıdaki hello nasıl toodo başlatma üzerinde hello disk daha fazla bilgi için adımlarına bakın).</span><span class="sxs-lookup"><span data-stu-id="560ff-124">After you add a data disk, you'll need toolog on toohello virtual machine and initialize hello disk so hello virtual machine can use hello disk for storage (see hello following steps for more information on how toodo initialize hello disk).</span></span>
> 
> 


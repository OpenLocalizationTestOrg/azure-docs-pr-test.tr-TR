<span data-ttu-id="27448-101">Ekli tooa sanal makine (VM) bir veri diski artık ihtiyacınız olduğunda, kolayca ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27448-101">When you no longer need a data disk that's attached tooa virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="27448-102">Merhaba VM diskten ayırdığınızda hello disk değil depolama biriminden kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="27448-102">When you detach a disk from hello VM, hello disk is not removed it from storage.</span></span> <span data-ttu-id="27448-103">Merhaba disk üzerindeki toouse hello mevcut verileri yeniden istiyorsanız, toohello iliştirebilirsiniz aynı VM veya başka bir tane.</span><span class="sxs-lookup"><span data-stu-id="27448-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="27448-104">Azure'da VM’ler işletim sistemi diski, yerel geçici disk ve isteğe bağlı veri diskleri gibi farklı tür diskler kullanır.</span><span class="sxs-lookup"><span data-stu-id="27448-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="27448-105">Ayrıntılar için bkz. [Sanal Makinelerde Diskler ve VHD’ler Hakkında](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27448-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="27448-106">Ayrıca hello VM silmediğiniz sürece bir işletim sistemi diski ayıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="27448-106">You cannot detach an operating system disk unless you also delete hello VM.</span></span>

## <a name="find-hello-disk"></a><span data-ttu-id="27448-107">Başlangıç diski bulun</span><span class="sxs-lookup"><span data-stu-id="27448-107">Find hello disk</span></span>
<span data-ttu-id="27448-108">Bir diskten VM ayırmadan önce hello hello disk toobe ayrılmış bir tanıtıcısıdır LUN numarası çıkışı toofind gerekir.</span><span class="sxs-lookup"><span data-stu-id="27448-108">Before you can detach a disk from a VM you need toofind out hello LUN number, which is an identifier for hello disk toobe detached.</span></span> <span data-ttu-id="27448-109">Bu adımları, toodo:</span><span class="sxs-lookup"><span data-stu-id="27448-109">toodo that, follow these steps:</span></span>

1. <span data-ttu-id="27448-110">Azure CLI'ni açın ve [tooyour Azure aboneliğine bağlanma](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="27448-110">Open Azure CLI and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="27448-111">Azure Hizmet Yönetimi modunda olduğunuzdan emin olun (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="27448-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="27448-112">Hangi disklerin ekli tooyour VM olduğunu bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27448-112">Find out which disks are attached tooyour VM.</span></span> <span data-ttu-id="27448-113">Merhaba aşağıdaki örnek listeler hello adlı VM için diskleri `myVM`:</span><span class="sxs-lookup"><span data-stu-id="27448-113">hello following example lists disks for hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="27448-114">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="27448-114">hello output is similar toohello following example:</span></span>

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. <span data-ttu-id="27448-115">Not hello LUN veya hello **mantıksal birim numarası** toodetach istediğiniz hello diski için.</span><span class="sxs-lookup"><span data-stu-id="27448-115">Note hello LUN or hello **logical unit number** for hello disk that you want toodetach.</span></span>

## <a name="remove-operating-system-references-toohello-disk"></a><span data-ttu-id="27448-116">İşletim sistemi başvuruları toohello diski Kaldır</span><span class="sxs-lookup"><span data-stu-id="27448-116">Remove operating system references toohello disk</span></span>
<span data-ttu-id="27448-117">Merhaba Linux Konuk Hello diskten kullanımdan çıkarmadan önce hello diskteki tüm bölümlerin kullanımda olmadığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="27448-117">Before detaching hello disk from hello Linux guest, you should make sure that all partitions on hello disk are not in use.</span></span> <span data-ttu-id="27448-118">Merhaba işletim sistemi tooremount denemez olun bir yeniden başlatma işleminden sonra onları.</span><span class="sxs-lookup"><span data-stu-id="27448-118">Ensure that hello operating system does not attempt tooremount them after a reboot.</span></span> <span data-ttu-id="27448-119">Büyük olasılıkla oluşturmuşsunuz ne zaman hello yapılandırma adımları geri [ekleme](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span><span class="sxs-lookup"><span data-stu-id="27448-119">These steps undo hello configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span></span>

1. <span data-ttu-id="27448-120">Kullanım hello `lsscsi` komut toodiscover hello disk tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="27448-120">Use hello `lsscsi` command toodiscover hello disk identifier.</span></span> <span data-ttu-id="27448-121">`lsscsi`, `yum install lsscsi` (Red Hat üzerinde dağıtımlarda) veya `apt-get install lsscsi` (Debian üzerinde dağıtımlarda) aracılığıyla yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="27448-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="27448-122">Merhaba LUN numarası kullanarak aradığınız hello disk tanımlayıcısı bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27448-122">You can find hello disk identifier you are looking for by using hello LUN number.</span></span> <span data-ttu-id="27448-123">Merhaba son hello tuple her satırda hello LUN sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="27448-123">hello last number in hello tuple in each row is hello LUN.</span></span> <span data-ttu-id="27448-124">Örnekten aşağıdaki hello içinde `lsscsi`, LUN 0 eşlemeleri çok  */dev/sdc*</span><span class="sxs-lookup"><span data-stu-id="27448-124">In hello following example from `lsscsi`, LUN 0 maps too*/dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="27448-125">Kullanım `fdisk -l <disk>` toodiscover hello bölümleri ayrılmış hello disk toobe ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="27448-125">Use `fdisk -l <disk>` toodiscover hello partitions associated with hello disk toobe detached.</span></span> <span data-ttu-id="27448-126">Merhaba aşağıdaki örnekte hello çıktısı için gösterilmektedir `/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="27448-126">hello following example shows hello output for `/dev/sdc`:</span></span>

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. <span data-ttu-id="27448-127">Merhaba disk için listelenen her bir bölümü çıkarın.</span><span class="sxs-lookup"><span data-stu-id="27448-127">Unmount each partition listed for hello disk.</span></span> <span data-ttu-id="27448-128">Merhaba aşağıdaki örnek çıkarır `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="27448-128">hello following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="27448-129">Kullanım hello `blkid` tüm bölümler için komut toodiscovery hello UUID.</span><span class="sxs-lookup"><span data-stu-id="27448-129">Use hello `blkid` command toodiscovery hello UUIDs for all partitions.</span></span> <span data-ttu-id="27448-130">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="27448-130">hello output is similar toohello following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="27448-131">Hello silmemelisiniz **/etc/fstab** ayrılmış hello disk toobe için tüm bölümler için hello aygıt yolları veya UUID'ler ile ilişkili dosya.</span><span class="sxs-lookup"><span data-stu-id="27448-131">Remove entries in hello **/etc/fstab** file associated with either hello device paths or UUIDs for all partitions for hello disk toobe detached.</span></span>  <span data-ttu-id="27448-132">Bu örneğin girişleri şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="27448-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="27448-133">or</span><span class="sxs-lookup"><span data-stu-id="27448-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a><span data-ttu-id="27448-134">Merhaba disk ayırma</span><span class="sxs-lookup"><span data-stu-id="27448-134">Detach hello disk</span></span>
<span data-ttu-id="27448-135">Merhaba LUN sayısını hello disk ve kaldırılan hello işletim sistemi başvuruları bulduktan sonra hazır toodetach olduğunuz bu:</span><span class="sxs-lookup"><span data-stu-id="27448-135">After you find hello LUN number of hello disk and removed hello operating system references, you're ready toodetach it:</span></span>

1. <span data-ttu-id="27448-136">Merhaba komutu çalıştırarak hello sanal makineden Hello seçili disk ayırma `azure vm disk detach
   <virtual-machine-name> <LUN>`.</span><span class="sxs-lookup"><span data-stu-id="27448-136">Detach hello selected disk from hello virtual machine by running hello command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="27448-137">Merhaba aşağıdaki örnek ayırır LUN `0` hello adlı VM gelen `myVM`:</span><span class="sxs-lookup"><span data-stu-id="27448-137">hello following example detaches LUN `0` from hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="27448-138">Merhaba disk çalıştırarak ayrıldı olmadığını denetleyebilirsiniz `azure vm disk list` yeniden.</span><span class="sxs-lookup"><span data-stu-id="27448-138">You can check if hello disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="27448-139">Aşağıdaki örnek denetimleri hello hello adlı VM `myVM`:</span><span class="sxs-lookup"><span data-stu-id="27448-139">hello following example checks hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="27448-140">Merhaba, benzer toohello hello veri diski artık takılı gösteren örnek aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="27448-140">hello output is similar toohello following example, which shows hello data disk is no longer attached:</span></span>

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

<span data-ttu-id="27448-141">Merhaba ayrılmış disk depolama alanında kalır, ancak artık ekli tooa sanal makine değil.</span><span class="sxs-lookup"><span data-stu-id="27448-141">hello detached disk remains in storage but is no longer attached tooa virtual machine.</span></span>


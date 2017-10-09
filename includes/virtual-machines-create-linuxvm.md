
1. <span data-ttu-id="f89a9-101">Listelenen hello adımları kullanarak Azure aboneliği tooyour oturum [tooAzure hello Azure CLI 1.0 ' bağlanma](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f89a9-101">Sign in tooyour Azure subscription using hello steps listed in [Connect tooAzure from hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="f89a9-102">Aşağıdaki gibi hello Klasik dağıtım modunda olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="f89a9-102">Make sure you are in hello Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="f89a9-103">Merhaba Linux görüntüyü hello kullanılabilir görüntülerden tooload gibi istediğiniz bulun:</span><span class="sxs-lookup"><span data-stu-id="f89a9-103">Find out hello Linux image that you want tooload from hello available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="f89a9-104">Bir Windows komut istemi penceresinde grep yerine **find** komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="f89a9-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="f89a9-105">Kullanım `azure vm create` toocreate hello önceki listeden hello Linux görüntüsü olan bir VM.</span><span class="sxs-lookup"><span data-stu-id="f89a9-105">Use `azure vm create` toocreate a VM with hello Linux image from hello previous list.</span></span> <span data-ttu-id="f89a9-106">Bu adımda bir bulut hizmeti ve depolama hesabı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f89a9-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="f89a9-107">VM tooan mevcut bulut hizmeti ile bağlantı kurulamadı bir `-c` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f89a9-107">You could also connect this VM tooan existing cloud service with a `-c` option.</span></span> <span data-ttu-id="f89a9-108">Bir SSH uç noktası toolog hello ile toohello Linux sanal makine oluşturma `-e` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f89a9-108">Create an SSH endpoint toolog in toohello Linux virtual machine with hello `-e` option.</span></span> <span data-ttu-id="f89a9-109">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` hello kullanarak `Ubuntu-14_04_4-LTS` hello görüntüde `West US` konumu ve bir kullanıcı adı ekler `ops`:</span><span class="sxs-lookup"><span data-stu-id="f89a9-109">hello following example creates a VM named `myVM` using hello `Ubuntu-14_04_4-LTS` image in hello `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="f89a9-110">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="f89a9-110">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > <span data-ttu-id="f89a9-111">Bir Linux sanal makine için hello sağlamalısınız `-e` seçeneğini `vm create`.</span><span class="sxs-lookup"><span data-stu-id="f89a9-111">For a Linux virtual machine, you must provide hello `-e` option in `vm create`.</span></span> <span data-ttu-id="f89a9-112">Merhaba sanal makine oluşturulduktan sonra olası tooenable SSH değil.</span><span class="sxs-lookup"><span data-stu-id="f89a9-112">It is not possible tooenable SSH after hello virtual machine has been created.</span></span> <span data-ttu-id="f89a9-113">SSH hakkında daha fazla bilgi için okuma [nasıl tooUse Linux Azure üzerinde SSH](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f89a9-113">For more details on SSH, read [How tooUse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="f89a9-114">Merhaba VM hello özniteliklerini hello kullanarak doğrulayabilirsiniz `azure vm show` komutu.</span><span class="sxs-lookup"><span data-stu-id="f89a9-114">You can verify hello attributes of hello VM by using hello `azure vm show` command.</span></span> <span data-ttu-id="f89a9-115">Merhaba aşağıdaki örnek listeler bilgi hello adlı VM için `myVM`:</span><span class="sxs-lookup"><span data-stu-id="f89a9-115">hello following example lists information for hello VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="f89a9-116">VM ile Merhaba Başlat `azure vm start` gibi komut:</span><span class="sxs-lookup"><span data-stu-id="f89a9-116">Start your VM with hello `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="f89a9-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f89a9-117">Next steps</span></span>
<span data-ttu-id="f89a9-118">Bu Azure CLI 1.0 sanal makine komutlar hakkında daha fazla bilgi için hello okuma [hello Klasik dağıtım API'si ile kullanma hello Azure CLI 1.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f89a9-118">For details on all these Azure CLI 1.0 virtual machine commands, read hello [Using hello Azure CLI 1.0 with hello Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>


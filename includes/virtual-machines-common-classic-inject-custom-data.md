


<span data-ttu-id="3fe7d-101">Bu konuda açıklanmaktadır nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="3fe7d-101">This topic describes how to:</span></span>

* <span data-ttu-id="3fe7d-102">Bunu sağlanan zaman veri bir Azure sanal makine (VM) yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="3fe7d-103">Windows ve Linux için alın.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="3fe7d-104">Bazı sistemler toodetect özel araçlar kullanılabilir kullanın ve özel verileri otomatik olarak işler.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-104">Use special tools available on some systems toodetect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="3fe7d-105">Bu makalede nasıl özel veri hello Azure Hizmet Yönetimi API'si ile oluşturulan bir VM'yi kullanarak yerleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-105">This article describes how custom data can be injected by using a VM created with hello Azure Service Management API.</span></span> <span data-ttu-id="3fe7d-106">toouse hello Azure kaynak yönetimi API'sini nasıl görürüm toosee [hello örnek şablon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="3fe7d-106">toosee how toouse hello Azure Resource Management API, see [hello example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="3fe7d-107">Azure sanal makineniz özel veri injecting</span><span class="sxs-lookup"><span data-stu-id="3fe7d-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="3fe7d-108">Bu özellik şu anda yalnızca hello desteklenir [Azure komut satırı arabirimi](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="3fe7d-108">This feature is currently supported only in hello [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="3fe7d-109">Burada oluşturuyoruz bir `custom-data.txt` bizim veri içeren dosyayı ardından Ekle, toohello VM sağlama sırasında.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-109">Here we create a `custom-data.txt` file that contains our data, then inject that in toohello VM during provisioning.</span></span> <span data-ttu-id="3fe7d-110">Merhaba hello seçeneklerinden herhangi birini kullanabilirsiniz ancak `azure vm create` komutunu hello aşağıdaki çok basit bir yaklaşım gösterir:</span><span class="sxs-lookup"><span data-stu-id="3fe7d-110">Although you may use any of hello options for hello `azure vm create` command, hello following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a><span data-ttu-id="3fe7d-111">Özel veri hello sanal makinede kullanma</span><span class="sxs-lookup"><span data-stu-id="3fe7d-111">Using custom data in hello virtual machine</span></span>
* <span data-ttu-id="3fe7d-112">Windows tabanlı bir VM, Azure VM, sonra hello özel veri dosyası çok kaydedilmiş`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-112">If your Azure VM is a Windows-based VM, then hello custom data file is saved too`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="3fe7d-113">Base64 ile kodlanmış tootransfer hello yerel bilgisayar toohello gelen olmasına rağmen yeni VM olduğu otomatik olarak kodunu çözdü ve açılabilen veya hemen kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-113">Although it was base64-encoded tootransfer from hello local computer toohello new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3fe7d-114">Merhaba dosya varsa üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-114">If hello file exists, it is overwritten.</span></span> <span data-ttu-id="3fe7d-115">Merhaba güvenlik hello dizinindeki çok ayarlama**sistem: Tam Denetim** ve **Administrators: Tam Denetim**.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-115">hello security on hello directory is set too**System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="3fe7d-116">Merhaba özel veri dosyası bulunan Azure VM Linux tabanlı bir VM ise hello aşağıdakilerden birini bağlı olarak, distro yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-116">If your Azure VM is a Linux-based VM, then hello custom data file will be located in one of hello following places depending on your distro.</span></span> <span data-ttu-id="3fe7d-117">toodecode hello veri ilk gerekebilir şekilde hello veriler Base64 ile kodlanmış olabilir:</span><span class="sxs-lookup"><span data-stu-id="3fe7d-117">hello data may be base64-encoded, so you may need toodecode hello data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="3fe7d-118">Azure üzerinde bulut başlatma</span><span class="sxs-lookup"><span data-stu-id="3fe7d-118">Cloud-init on Azure</span></span>
<span data-ttu-id="3fe7d-119">Daha sonra Azure VM Ubuntu veya CoreOS görüntüden ise, bir bulut-config toocloud init CustomData toosend kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="3fe7d-120">Veya özel veri dosyanızın bir komut dosyası ise, sonra bulut init yalnızca onu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="3fe7d-121">Ubuntu bulut görüntüleri</span><span class="sxs-lookup"><span data-stu-id="3fe7d-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="3fe7d-122">Çoğu Azure Linux görüntülerinde düzenlemek istiyorum "/ etc/waagent.conf" tooconfigure, hello geçici kaynak disk ve takas dosyası.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-122">In most Azure Linux images, you would edit "/etc/waagent.conf" tooconfigure hello temporary resource disk and swap file.</span></span> <span data-ttu-id="3fe7d-123">Bkz: [Azure Linux Aracısı Kullanıcı Kılavuzu](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="3fe7d-124">Ancak, hello Ubuntu bulut görüntülerinde bulut init tooconfigure hello kaynak disk (diğer bir deyişle, hello "kısa ömürlü" disk) ve takas kullanmalısınız bölüm.</span><span class="sxs-lookup"><span data-stu-id="3fe7d-124">However, on hello Ubuntu Cloud Images, you must use cloud-init tooconfigure hello resource disk (that is, hello "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="3fe7d-125">Daha fazla ayrıntı için hello Ubuntu Wiki Sayfa aşağıdaki hello bkz: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="3fe7d-125">See hello following page on hello Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="3fe7d-126">Sonraki adımlar: Bulut init kullanma</span><span class="sxs-lookup"><span data-stu-id="3fe7d-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="3fe7d-127">Daha fazla bilgi için bkz: Merhaba [Ubuntu bulut init belgelerine](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="3fe7d-127">For further information, see hello [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="3fe7d-128">Rolü Hizmet Yönetimi REST API Başvurusu Ekle</span><span class="sxs-lookup"><span data-stu-id="3fe7d-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="3fe7d-129">Azure komut satırı arabirimi</span><span class="sxs-lookup"><span data-stu-id="3fe7d-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)


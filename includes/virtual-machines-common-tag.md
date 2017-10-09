


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="26bc8-101">Bir sanal makine şablonlarıyla etiketleme</span><span class="sxs-lookup"><span data-stu-id="26bc8-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="26bc8-102">İlk olarak, şablonları üzerinden etiketleme konumundaki bakalım.</span><span class="sxs-lookup"><span data-stu-id="26bc8-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="26bc8-103">[Bu şablon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) kaynakları aşağıdaki hello üzerinde etiketleri yerleştirir: işlem (sanal makine), depolama (depolama hesabı) ve ağ (genel IP adresi, sanal ağ ve ağ arabirimi).</span><span class="sxs-lookup"><span data-stu-id="26bc8-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on hello following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="26bc8-104">Bu şablon için bir Windows VM olmakla birlikte Linux VM'ler için uyarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="26bc8-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="26bc8-105">Merhaba tıklatın **tooAzure dağıtmak** hello düğmesinden [şablon bağlantısı](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="26bc8-105">Click hello **Deploy tooAzure** button from hello [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="26bc8-106">Bu toohello gideceği [Azure portal](https://portal.azure.com/) bu şablonu dağıtabileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="26bc8-106">This will navigate toohello [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Etiketler basit dağıtımı](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="26bc8-108">Bu şablon etiketleri aşağıdaki hello içerir: *departmanı*, *uygulama*, ve *oluşturan*.</span><span class="sxs-lookup"><span data-stu-id="26bc8-108">This template includes hello following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="26bc8-109">Ekle/hello şablonunda doğrudan bu etiketler farklı etiket adları isterseniz Düzenle.</span><span class="sxs-lookup"><span data-stu-id="26bc8-109">You can add/edit these tags directly in hello template if you would like different tag names.</span></span>

![Bir şablonu Azure etiketleri](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="26bc8-111">Gördüğünüz gibi hello etiketleri iki nokta (:) ayırarak anahtar/değer çiftleri olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="26bc8-111">As you can see, hello tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="26bc8-112">Başlangıç etiketleri bu biçimde tanımlanmış olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="26bc8-112">hello tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="26bc8-113">Tercih ettiğiniz hello etiketleriyle düzenlemeyi tamamladıktan sonra hello şablon dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="26bc8-113">Save hello template file after you finish editing it with hello tags of your choice.</span></span>

<span data-ttu-id="26bc8-114">Merhaba sonraki **parametreleri Düzenle** bölümünde etiketlerinizi için hello değerlere doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26bc8-114">Next, in hello **Edit Parameters** section, you can fill out hello values for your tags.</span></span>

![Azure portalında etiket düzenleme](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="26bc8-116">Tıklatın **oluşturma** toodeploy bu şablonla, etiket değeri.</span><span class="sxs-lookup"><span data-stu-id="26bc8-116">Click **Create** toodeploy this template with your tag values.</span></span>

## <a name="tagging-through-hello-portal"></a><span data-ttu-id="26bc8-117">Merhaba Portal etiketleme</span><span class="sxs-lookup"><span data-stu-id="26bc8-117">Tagging through hello Portal</span></span>
<span data-ttu-id="26bc8-118">Kaynaklarınızın etiketleriyle oluşturduktan sonra görüntülemek, ekleyin ve hello portal etiketleri silin.</span><span class="sxs-lookup"><span data-stu-id="26bc8-118">After creating your resources with tags, you can view, add, and delete tags in hello portal.</span></span>

<span data-ttu-id="26bc8-119">Select hello simgesi tooview etiketlerinizi etiketler:</span><span class="sxs-lookup"><span data-stu-id="26bc8-119">Select hello tags icon tooview your tags:</span></span>

![Azure portalında etiketleri simgesi](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="26bc8-121">Kendi anahtar/değer çifti tanımlayarak hello Portalı aracılığıyla yeni bir etiket eklemek ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="26bc8-121">Add a new tag through hello portal by defining your own Key/Value pair, and save it.</span></span>

![Azure portalında Yeni Etiket Ekle](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="26bc8-123">Yeni etiket şimdi kaynağınız için etiketler hello listesinde gösterilmelidir.</span><span class="sxs-lookup"><span data-stu-id="26bc8-123">Your new tag should now appear in hello list of tags for your resource.</span></span>

![Azure portalında kaydedilen yeni etiket](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)


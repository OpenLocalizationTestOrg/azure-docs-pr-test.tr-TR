

<span data-ttu-id="d4b9c-101">*Özel* bir sanal makine, **Mağaza**’daki **öne çıkan uygulamaları** kullanarak oluşturabileceğiniz bir sanal makinedir ve işin çoğunu sizin yerinize yapar.</span><span class="sxs-lookup"><span data-stu-id="d4b9c-101">A *custom* virtual machine simply means a virtual machine that you create using a **Featured app** from the **Marketplace** because it does much of the work for you.</span></span> <span data-ttu-id="d4b9c-102">Ancak siz de aşağıdakiler dahil olmak üzere belirli yapılandırma seçeneklerini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d4b9c-102">Yet, you can still make configuration choices that include the following items:</span></span>

* <span data-ttu-id="d4b9c-103">Sanal makineyi bir sanal ağa bağlama.</span><span class="sxs-lookup"><span data-stu-id="d4b9c-103">Connecting the virtual machine to a virtual network.</span></span>
* <span data-ttu-id="d4b9c-104">Kötü amaçlı yazılımdan korunma gibi nedenlerle Azure Sanal Makinesi Aracısı ve Azure Sanal Makine Uzantılarını yükleme.</span><span class="sxs-lookup"><span data-stu-id="d4b9c-104">Installing the Azure Virtual Machine Agent and Azure Virtual Machine Extensions, such as for antimalware.</span></span>
* <span data-ttu-id="d4b9c-105">Var olan bulut hizmetlerine sanal makine ekleme.</span><span class="sxs-lookup"><span data-stu-id="d4b9c-105">Adding the virtual machine to existing cloud services.</span></span>
* <span data-ttu-id="d4b9c-106">Sanal makineyi var olan Depolama hesabına ekleme.</span><span class="sxs-lookup"><span data-stu-id="d4b9c-106">Adding the virtual machine to an existing Storage account.</span></span>
* <span data-ttu-id="d4b9c-107">Sanal makineyi bir kullanılabilirlik kümesine ekleme.</span><span class="sxs-lookup"><span data-stu-id="d4b9c-107">Adding the virtual machine to an availability set.</span></span>

<!--
> [!IMPORTANT]
> If you want your virtual machine to use a virtual network so you can connect to it directly by host name or set up cross-premises connections, make sure that you specify the virtual network when you create the virtual machine. A virtual machine can be configured to join a virtual network only when you create the virtual machine. For details on virtual networks, see [Azure Virtual Network overview](../articles/virtual-network/virtual-networks-overview.md).
>
>
 -->

> [!IMPORTANT]
> <span data-ttu-id="d4b9c-108">Sanal makinenizin bir sanal ağı kullanmasını istiyorsanız, sanal makineyi oluştururken sanal ağı da belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4b9c-108">If you want your virtual machine to use a virtual network, make sure that you specify the virtual network when you create the virtual machine.</span></span>

> * <span data-ttu-id="d4b9c-109">Sanal ağ kullanmanın iki avantajı, sanal makineye doğrudan bağlanmak ve şirket içi bağlantıları kurmaktır.</span><span class="sxs-lookup"><span data-stu-id="d4b9c-109">Two benefits of using a virtual network are connecting directly to the virtual machine and to set up cross-premises connections.</span></span>

> * <span data-ttu-id="d4b9c-110">Bir sanal makine, yalnızca sanal makineyi oluşturduğunuzda sanal ağa katılmak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d4b9c-110">A virtual machine can be configured to join a virtual network only when you create the virtual machine.</span></span> <span data-ttu-id="d4b9c-111">Sanal ağlar hakkında daha fazla bilgi için bkz. [Azure Sanal Ağına Genel Bakış](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4b9c-111">For details on virtual networks, see [Azure Virtual Network overview](../articles/virtual-network/virtual-networks-overview.md).</span></span>
>
>

## <a name="to-create-the-virtual-machine"></a><span data-ttu-id="d4b9c-112">Sanal makineyi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="d4b9c-112">To create the virtual machine</span></span>

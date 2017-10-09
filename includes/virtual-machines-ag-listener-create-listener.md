<span data-ttu-id="078ca-101">Bu adımda, yük devretme kümesi Yöneticisi'ni ve SQL Server Management Studio hello kullanılabilirlik grubu dinleyicisi el ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="078ca-101">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="078ca-102">Hello birincil çoğaltmayı barındıran hello düğümden diğerine yük devretme kümesi Yöneticisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="078ca-102">Open Failover Cluster Manager from hello node that hosts hello primary replica.</span></span>

2. <span data-ttu-id="078ca-103">Select hello **ağlar** düğümü ve Not hello küme ağ adı.</span><span class="sxs-lookup"><span data-stu-id="078ca-103">Select hello **Networks** node, and then note hello cluster network name.</span></span> <span data-ttu-id="078ca-104">Bu ad hello PowerShell Betiği hello $ClusterNetworkName değişkeni kullanılır.</span><span class="sxs-lookup"><span data-stu-id="078ca-104">This name is used in hello $ClusterNetworkName variable in hello PowerShell script.</span></span>

3. <span data-ttu-id="078ca-105">Merhaba küme adını genişletin ve ardından **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="078ca-105">Expand hello cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="078ca-106">Merhaba, **rolleri** bölmesi, sağ hello kullanılabilirlik grubu adını ve ardından **kaynak ekleme** > **istemci erişim noktası**.</span><span class="sxs-lookup"><span data-stu-id="078ca-106">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Kullanılabilirlik grubu için istemci erişim noktası Ekle](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="078ca-108">Merhaba, **adı** kutusunda, bu yeni dinleyici için bir ad oluşturun, **sonraki** iki kez tıkladıktan sonra **son**.</span><span class="sxs-lookup"><span data-stu-id="078ca-108">In hello **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="078ca-109">Merhaba dinleyicisi veya kaynağı çevrimiçi bu noktada Getir değil.</span><span class="sxs-lookup"><span data-stu-id="078ca-109">Do not bring hello listener or resource online at this point.</span></span>

6. <span data-ttu-id="078ca-110">Merhaba tıklatın **kaynakları** sekmesini tıklatın ve ardından yeni oluşturduğunuz hello istemci erişim noktası genişletin.</span><span class="sxs-lookup"><span data-stu-id="078ca-110">Click hello **Resources** tab, and then expand hello client access point you just created.</span></span> 
    <span data-ttu-id="078ca-111">Başlangıç IP adresi kaynağı, kümedeki her bir küme ağı için görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="078ca-111">hello IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="078ca-112">Bu yalnızca Azure çözümünü ise, yalnızca bir IP adresi kaynak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="078ca-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="078ca-113">Merhaba aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="078ca-113">Do either of hello following:</span></span>
   
   * <span data-ttu-id="078ca-114">karma bir çözüm tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="078ca-114">tooconfigure a hybrid solution:</span></span>
     
        <span data-ttu-id="078ca-115">a.</span><span class="sxs-lookup"><span data-stu-id="078ca-115">a.</span></span> <span data-ttu-id="078ca-116">Tooyour şirket içi alt karşılık gelen başlangıç IP adresi kaynağı sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="078ca-116">Right-click hello IP address resource that corresponds tooyour on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="078ca-117">Başlangıç IP adresi adı ve ağ adını not edin.</span><span class="sxs-lookup"><span data-stu-id="078ca-117">Note hello IP address name and network name.</span></span>
   
        <span data-ttu-id="078ca-118">b.</span><span class="sxs-lookup"><span data-stu-id="078ca-118">b.</span></span> <span data-ttu-id="078ca-119">Seçin **statik IP adresi**, kullanılmayan bir IP adresi atayın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="078ca-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="078ca-120">yalnızca Azure çözümünü tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="078ca-120">tooconfigure an Azure-only solution:</span></span>

        <span data-ttu-id="078ca-121">a.</span><span class="sxs-lookup"><span data-stu-id="078ca-121">a.</span></span> <span data-ttu-id="078ca-122">Tooyour Azure alt ağa karşılık gelen başlangıç IP adresi kaynağı sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="078ca-122">Right-click hello IP address resource that corresponds tooyour Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="078ca-123">Merhaba dinleyicisi DHCP tarafından seçilen bir IP adresi nedeniyle çevrimiçi toocome daha sonra başarısız olursa, bu Özellikler penceresinde geçerli bir statik IP adresi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="078ca-123">If hello listener later fails toocome online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="078ca-124">b.</span><span class="sxs-lookup"><span data-stu-id="078ca-124">b.</span></span> <span data-ttu-id="078ca-125">İçinde aynı hello **IP adresi** Özellikleri penceresinde, değişiklik hello **IP adresi adı**.</span><span class="sxs-lookup"><span data-stu-id="078ca-125">In hello same **IP Address** properties window, change hello **IP Address Name**.</span></span>  
        <span data-ttu-id="078ca-126">Bu ad hello PowerShell Betiği hello $IPResourceName değişkeninde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="078ca-126">This name is used in hello $IPResourceName variable of hello PowerShell script.</span></span> <span data-ttu-id="078ca-127">Çözümünüzün birden fazla Azure sanal ağı yayılırsa, her IP kaynağı için bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="078ca-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>


<span data-ttu-id="fde07-101">Bu adımda, yük devretme kümesi Yöneticisi'ni ve SQL Server Management Studio kullanılabilirlik grubu dinleyicisi el ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fde07-101">In this step, you manually create the availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="fde07-102">Birincil çoğaltmayı barındıran düğümden diğerine yük devretme kümesi Yöneticisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="fde07-102">Open Failover Cluster Manager from the node that hosts the primary replica.</span></span>

2. <span data-ttu-id="fde07-103">Seçin **ağlar** düğüm ve Not küme ağ adı.</span><span class="sxs-lookup"><span data-stu-id="fde07-103">Select the **Networks** node, and then note the cluster network name.</span></span> <span data-ttu-id="fde07-104">Bu ad, PowerShell Betiği $ClusterNetworkName değişkeninde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fde07-104">This name is used in the $ClusterNetworkName variable in the PowerShell script.</span></span>

3. <span data-ttu-id="fde07-105">Küme adını genişletin ve ardından **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="fde07-105">Expand the cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="fde07-106">İçinde **rolleri** bölmesinde, kullanılabilirlik grubu adını sağ tıklatın ve ardından **kaynak ekleme** > **istemci erişim noktası**.</span><span class="sxs-lookup"><span data-stu-id="fde07-106">In the **Roles** pane, right-click the availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Kullanılabilirlik grubu için istemci erişim noktası Ekle](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="fde07-108">İçinde **adı** kutusunda, bu yeni dinleyici için bir ad oluşturun, **sonraki** iki kez tıkladıktan sonra **son**.</span><span class="sxs-lookup"><span data-stu-id="fde07-108">In the **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="fde07-109">Dinleyici veya kaynağı çevrimiçi bu noktada çıkarır değil.</span><span class="sxs-lookup"><span data-stu-id="fde07-109">Do not bring the listener or resource online at this point.</span></span>

6. <span data-ttu-id="fde07-110">Tıklatın **kaynakları** sekmesini tıklatın ve ardından yeni oluşturduğunuz istemci erişim noktası'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="fde07-110">Click the **Resources** tab, and then expand the client access point you just created.</span></span> 
    <span data-ttu-id="fde07-111">Kümenizdeki her bir küme ağı için IP adresi kaynağı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fde07-111">The IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="fde07-112">Bu yalnızca Azure çözümünü ise, yalnızca bir IP adresi kaynak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fde07-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="fde07-113">Aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="fde07-113">Do either of the following:</span></span>
   
   * <span data-ttu-id="fde07-114">Karma bir çözüm yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="fde07-114">To configure a hybrid solution:</span></span>
     
        <span data-ttu-id="fde07-115">a.</span><span class="sxs-lookup"><span data-stu-id="fde07-115">a.</span></span> <span data-ttu-id="fde07-116">Şirket içi alt ağa karşılık gelen IP adresi kaynağı sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="fde07-116">Right-click the IP address resource that corresponds to your on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="fde07-117">Ağ adı ve IP adresi adını not edin.</span><span class="sxs-lookup"><span data-stu-id="fde07-117">Note the IP address name and network name.</span></span>
   
        <span data-ttu-id="fde07-118">b.</span><span class="sxs-lookup"><span data-stu-id="fde07-118">b.</span></span> <span data-ttu-id="fde07-119">Seçin **statik IP adresi**, kullanılmayan bir IP adresi atayın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fde07-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="fde07-120">Yalnızca Azure çözümünü yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="fde07-120">To configure an Azure-only solution:</span></span>

        <span data-ttu-id="fde07-121">a.</span><span class="sxs-lookup"><span data-stu-id="fde07-121">a.</span></span> <span data-ttu-id="fde07-122">Azure alt ağa karşılık gelen IP adresi kaynağı sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="fde07-122">Right-click the IP address resource that corresponds to your Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="fde07-123">Dinleyici çakışan bir IP adresi DHCP tarafından seçilen nedeniyle çevrimiçine alınamıyor. daha sonra başarısız olursa, bu Özellikler penceresinde geçerli bir statik IP adresi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fde07-123">If the listener later fails to come online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="fde07-124">b.</span><span class="sxs-lookup"><span data-stu-id="fde07-124">b.</span></span> <span data-ttu-id="fde07-125">Aynı **IP adresi** Özellikler penceresi, değişiklik **IP adresi adı**.</span><span class="sxs-lookup"><span data-stu-id="fde07-125">In the same **IP Address** properties window, change the **IP Address Name**.</span></span>  
        <span data-ttu-id="fde07-126">Bu ad PowerShell Betiği $IPResourceName değişkeninde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fde07-126">This name is used in the $IPResourceName variable of the PowerShell script.</span></span> <span data-ttu-id="fde07-127">Çözümünüzün birden fazla Azure sanal ağı yayılırsa, her IP kaynağı için bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="fde07-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>


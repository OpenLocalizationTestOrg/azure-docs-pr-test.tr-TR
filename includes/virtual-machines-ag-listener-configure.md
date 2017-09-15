<span data-ttu-id="5671c-101">Kullanılabilirlik grubu dinleyicisi SQL Server kullanılabilirlik grubu dinlediği bir IP adresi ve ağ adı değil.</span><span class="sxs-lookup"><span data-stu-id="5671c-101">The availability group listener is an IP address and network name that the SQL Server availability group listens on.</span></span> <span data-ttu-id="5671c-102">Kullanılabilirlik grubu dinleyicisi oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="5671c-102">To create the availability group listener, do the following:</span></span>

1. <span data-ttu-id="5671c-103"><a name="getnet"></a>Küme ağ kaynağı adını alın.</span><span class="sxs-lookup"><span data-stu-id="5671c-103"><a name="getnet"></a>Get the name of the cluster network resource.</span></span>

    <span data-ttu-id="5671c-104">a.</span><span class="sxs-lookup"><span data-stu-id="5671c-104">a.</span></span> <span data-ttu-id="5671c-105">Birincil çoğaltmayı barındıran Azure sanal makine için bağlanmak için RDP kullanın.</span><span class="sxs-lookup"><span data-stu-id="5671c-105">Use RDP to connect to the Azure virtual machine that hosts the primary replica.</span></span> 

    <span data-ttu-id="5671c-106">b.</span><span class="sxs-lookup"><span data-stu-id="5671c-106">b.</span></span> <span data-ttu-id="5671c-107">Yük Devretme Kümesi Yöneticisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="5671c-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="5671c-108">c.</span><span class="sxs-lookup"><span data-stu-id="5671c-108">c.</span></span> <span data-ttu-id="5671c-109">Seçin **ağlar** düğümü ve Not küme ağ adı.</span><span class="sxs-lookup"><span data-stu-id="5671c-109">Select the **Networks** node, and note the cluster network name.</span></span> <span data-ttu-id="5671c-110">Bu adı kullanmak `$ClusterNetworkName` PowerShell Betiği değişkeni.</span><span class="sxs-lookup"><span data-stu-id="5671c-110">Use this name in the `$ClusterNetworkName` variable in the PowerShell script.</span></span> <span data-ttu-id="5671c-111">Aşağıdaki görüntüde küme ağ adı olan **küme ağ 1**:</span><span class="sxs-lookup"><span data-stu-id="5671c-111">In the following image the cluster network name is **Cluster Network 1**:</span></span>

   ![Küme ağ adı](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="5671c-113"><a name="addcap"></a>İstemci erişim noktası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5671c-113"><a name="addcap"></a>Add the client access point.</span></span>  
    <span data-ttu-id="5671c-114">İstemci erişim noktası bir kullanılabilirlik grubuna veritabanlarına bağlanmak için uygulamaları kullanan ağ adıdır.</span><span class="sxs-lookup"><span data-stu-id="5671c-114">The client access point is the network name that applications use to connect to the databases in an availability group.</span></span> <span data-ttu-id="5671c-115">İstemci erişim noktası, yük devretme kümesi Yöneticisi'nde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5671c-115">Create the client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="5671c-116">a.</span><span class="sxs-lookup"><span data-stu-id="5671c-116">a.</span></span> <span data-ttu-id="5671c-117">Küme adını genişletin ve ardından **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="5671c-117">Expand the cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="5671c-118">b.</span><span class="sxs-lookup"><span data-stu-id="5671c-118">b.</span></span> <span data-ttu-id="5671c-119">İçinde **rolleri** bölmesinde, kullanılabilirlik grubu adını sağ tıklatın ve ardından **kaynak ekleme** > **istemci erişim noktası**.</span><span class="sxs-lookup"><span data-stu-id="5671c-119">In the **Roles** pane, right-click the availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![İstemci erişim noktası](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="5671c-121">c.</span><span class="sxs-lookup"><span data-stu-id="5671c-121">c.</span></span> <span data-ttu-id="5671c-122">İçinde **adı** kutusunda, bu yeni dinleyici için bir ad oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5671c-122">In the **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="5671c-123">Yeni dinleyici uygulamaları SQL Server kullanılabilirlik grubundaki veritabanlarına bağlanmak için kullandığınız ağ adı adıdır.</span><span class="sxs-lookup"><span data-stu-id="5671c-123">The name for the new listener is the network name that applications use to connect to databases in the SQL Server availability group.</span></span>
   
    <span data-ttu-id="5671c-124">d.</span><span class="sxs-lookup"><span data-stu-id="5671c-124">d.</span></span> <span data-ttu-id="5671c-125">Dinleyiciyi oluşturmayı tamamlamak için tıklatın **sonraki** iki kez tıkladıktan sonra **son**.</span><span class="sxs-lookup"><span data-stu-id="5671c-125">To finish creating the listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="5671c-126">Dinleyici veya kaynağı çevrimiçi bu noktada çıkarır değil.</span><span class="sxs-lookup"><span data-stu-id="5671c-126">Do not bring the listener or resource online at this point.</span></span>

3. <span data-ttu-id="5671c-127"><a name="congroup"></a>IP kaynağı kullanılabilirlik grubu için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5671c-127"><a name="congroup"></a>Configure the IP resource for the availability group.</span></span>

    <span data-ttu-id="5671c-128">a.</span><span class="sxs-lookup"><span data-stu-id="5671c-128">a.</span></span> <span data-ttu-id="5671c-129">Tıklatın **kaynakları** sekmesini tıklatın ve ardından oluşturduğunuz istemci erişim noktası'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="5671c-129">Click the **Resources** tab, and then expand the client access point you created.</span></span>  
    <span data-ttu-id="5671c-130">İstemci erişim noktası çevrimdışıdır.</span><span class="sxs-lookup"><span data-stu-id="5671c-130">The client access point is offline.</span></span>

   ![İstemci erişim noktası](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="5671c-132">b.</span><span class="sxs-lookup"><span data-stu-id="5671c-132">b.</span></span> <span data-ttu-id="5671c-133">IP kaynağı sağ tıklayın ve ardından Özellikler'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5671c-133">Right-click the IP resource, and then click properties.</span></span> <span data-ttu-id="5671c-134">IP adresini not alın ve bunu kullanmak `$IPResourceName` PowerShell Betiği değişkeni.</span><span class="sxs-lookup"><span data-stu-id="5671c-134">Note the name of the IP address, and use it in the `$IPResourceName` variable in the PowerShell script.</span></span>

    <span data-ttu-id="5671c-135">c.</span><span class="sxs-lookup"><span data-stu-id="5671c-135">c.</span></span> <span data-ttu-id="5671c-136">Altında **IP adresi**, tıklatın **statik IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="5671c-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="5671c-137">IP adresi Azure portalında yük dengeleyici adresi ayarlarken kullandığınız aynı adresi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5671c-137">Set the IP address as the same address that you used when you set the load balancer address on the Azure portal.</span></span>

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="5671c-139"><a name = "dependencyGroup"></a>SQL Server kullanılabilirlik grubu kaynağı istemci erişim noktasında bağımlı hale getirin.</span><span class="sxs-lookup"><span data-stu-id="5671c-139"><a name = "dependencyGroup"></a>Make the SQL Server availability group resource dependent on the client access point.</span></span>

    <span data-ttu-id="5671c-140">a.</span><span class="sxs-lookup"><span data-stu-id="5671c-140">a.</span></span> <span data-ttu-id="5671c-141">Yük Devretme Kümesi Yöneticisi'nde **rolleri**, kullanılabilirlik grubunuzun'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5671c-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="5671c-142">b.</span><span class="sxs-lookup"><span data-stu-id="5671c-142">b.</span></span> <span data-ttu-id="5671c-143">Üzerinde **kaynakları** sekmesinde, altında **diğer kaynakları**kullanılabilirlik kaynak grubuna sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="5671c-143">On the **Resources** tab, under **Other Resources**, right-click the availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="5671c-144">c.</span><span class="sxs-lookup"><span data-stu-id="5671c-144">c.</span></span> <span data-ttu-id="5671c-145">Bağımlılıklar sekmesinde istemci erişim noktası (dinleyici) kaynağın adını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5671c-145">On the dependencies tab, add the name of the client access point (the listener) resource.</span></span>

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="5671c-147">d.</span><span class="sxs-lookup"><span data-stu-id="5671c-147">d.</span></span> <span data-ttu-id="5671c-148">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5671c-148">Click **OK**.</span></span>

5. <span data-ttu-id="5671c-149"><a name="listname"></a>İstemci erişim noktası kaynak IP adresine bağımlı olun.</span><span class="sxs-lookup"><span data-stu-id="5671c-149"><a name="listname"></a>Make the client access point resource dependent on the IP address.</span></span>

    <span data-ttu-id="5671c-150">a.</span><span class="sxs-lookup"><span data-stu-id="5671c-150">a.</span></span> <span data-ttu-id="5671c-151">Yük Devretme Kümesi Yöneticisi'nde **rolleri**, kullanılabilirlik grubunuzun'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5671c-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="5671c-152">b.</span><span class="sxs-lookup"><span data-stu-id="5671c-152">b.</span></span> <span data-ttu-id="5671c-153">Üzerinde **kaynakları** sekmesinde, istemci erişim noktası kaynağa altında sağ **sunucu adı**ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="5671c-153">On the **Resources** tab, right-click the client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="5671c-155">c.</span><span class="sxs-lookup"><span data-stu-id="5671c-155">c.</span></span> <span data-ttu-id="5671c-156">Tıklatın **bağımlılıkları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5671c-156">Click the **Dependencies** tab.</span></span> <span data-ttu-id="5671c-157">IP adresi bir bağımlılığı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5671c-157">Verify that the IP address is a dependency.</span></span> <span data-ttu-id="5671c-158">Değilse, bir bağımlılık IP adresi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5671c-158">If it is not, set a dependency on the IP address.</span></span> <span data-ttu-id="5671c-159">Listelenen birden fazla kaynak varsa, IP adreslerini veya değil olduğunu doğrulayın ve, bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="5671c-159">If there are multiple resources listed, verify that the IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="5671c-160">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5671c-160">Click **OK**.</span></span> 

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="5671c-162">d.</span><span class="sxs-lookup"><span data-stu-id="5671c-162">d.</span></span> <span data-ttu-id="5671c-163">Dinleyici adına sağ tıklayın ve ardından **çevrimiçine**.</span><span class="sxs-lookup"><span data-stu-id="5671c-163">Right-click the listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="5671c-164">Bağımlılıkların doğru bir şekilde yapılandırıldığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5671c-164">You can validate that the dependencies are correctly configured.</span></span> <span data-ttu-id="5671c-165">Yük Devretme Kümesi Yöneticisi'nde, kullanılabilirlik grubu, rollere sağ tıklayın, Git **diğer eylemler**ve ardından **bağımlılık raporunu göster**.</span><span class="sxs-lookup"><span data-stu-id="5671c-165">In Failover Cluster Manager, go to Roles, right-click the availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="5671c-166">Bağımlılıklar doğru şekilde yapılandırıldığında, ağ adı üzerinde kullanılabilirlik grubu bağlıdır ve ağ adı IP adresine bağımlı.</span><span class="sxs-lookup"><span data-stu-id="5671c-166">When the dependencies are correctly configured, the availability group is dependent on the network name, and the network name is dependent on the IP address.</span></span> 


6. <span data-ttu-id="5671c-167"><a name="setparam"></a>Küme parametreleri PowerShell'de ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5671c-167"><a name="setparam"></a>Set the cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="5671c-168">a.</span><span class="sxs-lookup"><span data-stu-id="5671c-168">a.</span></span> <span data-ttu-id="5671c-169">Aşağıdaki PowerShell komut dosyası, SQL Server örnekleri birine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5671c-169">Copy the following PowerShell script to one of your SQL Server instances.</span></span> <span data-ttu-id="5671c-170">Değişkenleri ortamınız için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5671c-170">Update the variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
    $IPResourceName = "<IPResourceName>" # the IP Address resource name
    $ILBIP = “<n.n.n.n>” # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="5671c-171">b.</span><span class="sxs-lookup"><span data-stu-id="5671c-171">b.</span></span> <span data-ttu-id="5671c-172">Küme düğümlerinden birinin PowerShell betiğini çalıştırarak küme parametreleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5671c-172">Set the cluster parameters by running the PowerShell script on one of the cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="5671c-173">SQL Server örnekleri farklı bölgelerde bulunuyorsa, PowerShell Betiği iki kez çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5671c-173">If your SQL Server instances are in separate regions, you need to run the PowerShell script twice.</span></span> <span data-ttu-id="5671c-174">İlk kez kullanmak `$ILBIP` ve `$ProbePort` ilk bölgesinden.</span><span class="sxs-lookup"><span data-stu-id="5671c-174">The first time, use the `$ILBIP` and `$ProbePort` from the first region.</span></span> <span data-ttu-id="5671c-175">İkinci kez kullanmak `$ILBIP` ve `$ProbePort` ikinci bölgesinden.</span><span class="sxs-lookup"><span data-stu-id="5671c-175">The second time, use the `$ILBIP` and `$ProbePort` from the second region.</span></span> <span data-ttu-id="5671c-176">Küme ağ adı ve küme IP kaynak adı aynıdır.</span><span class="sxs-lookup"><span data-stu-id="5671c-176">The cluster network name and the cluster IP resource name are the same.</span></span> 

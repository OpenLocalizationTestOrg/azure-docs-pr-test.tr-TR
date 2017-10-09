<span data-ttu-id="f5d5f-101">Merhaba kullanılabilirlik grubu dinleyicisi SQL Server kullanılabilirlik grubu dinlediği hello bir IP adresi ve ağ adı değil.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-101">hello availability group listener is an IP address and network name that hello SQL Server availability group listens on.</span></span> <span data-ttu-id="f5d5f-102">toocreate hello kullanılabilirlik grubu dinleyicisi, hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="f5d5f-102">toocreate hello availability group listener, do hello following:</span></span>

1. <span data-ttu-id="f5d5f-103"><a name="getnet"></a>Merhaba küme ağ kaynağı Hello adını alın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-103"><a name="getnet"></a>Get hello name of hello cluster network resource.</span></span>

    <span data-ttu-id="f5d5f-104">a.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-104">a.</span></span> <span data-ttu-id="f5d5f-105">RDP tooconnect toohello hello birincil çoğaltmayı barındıran Azure sanal makine kullanın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-105">Use RDP tooconnect toohello Azure virtual machine that hosts hello primary replica.</span></span> 

    <span data-ttu-id="f5d5f-106">b.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-106">b.</span></span> <span data-ttu-id="f5d5f-107">Yük Devretme Kümesi Yöneticisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="f5d5f-108">c.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-108">c.</span></span> <span data-ttu-id="f5d5f-109">Select hello **ağlar** düğümü ve Not hello küme ağ adı.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-109">Select hello **Networks** node, and note hello cluster network name.</span></span> <span data-ttu-id="f5d5f-110">Hello bu adı kullanmak `$ClusterNetworkName` hello PowerShell Betiği değişkeni.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-110">Use this name in hello `$ClusterNetworkName` variable in hello PowerShell script.</span></span> <span data-ttu-id="f5d5f-111">Görüntü hello küme ağ adı aşağıdaki Hello olan **küme ağ 1**:</span><span class="sxs-lookup"><span data-stu-id="f5d5f-111">In hello following image hello cluster network name is **Cluster Network 1**:</span></span>

   ![Küme ağ adı](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="f5d5f-113"><a name="addcap"></a>Merhaba istemci erişim noktası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-113"><a name="addcap"></a>Add hello client access point.</span></span>  
    <span data-ttu-id="f5d5f-114">Merhaba istemci erişim noktası uygulamaları bir kullanılabilirlik grubunda tooconnect toohello veritabanlarını kullanmanızı hello ağ adıdır.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-114">hello client access point is hello network name that applications use tooconnect toohello databases in an availability group.</span></span> <span data-ttu-id="f5d5f-115">Yük Devretme Kümesi Yöneticisi'nde Hello istemci erişim noktası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-115">Create hello client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="f5d5f-116">a.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-116">a.</span></span> <span data-ttu-id="f5d5f-117">Merhaba küme adını genişletin ve ardından **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-117">Expand hello cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="f5d5f-118">b.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-118">b.</span></span> <span data-ttu-id="f5d5f-119">Merhaba, **rolleri** bölmesi, sağ hello kullanılabilirlik grubu adını ve ardından **kaynak ekleme** > **istemci erişim noktası**.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-119">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![İstemci erişim noktası](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="f5d5f-121">c.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-121">c.</span></span> <span data-ttu-id="f5d5f-122">Merhaba, **adı** kutusunda, bu yeni dinleyici için bir ad oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-122">In hello **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="f5d5f-123">Merhaba hello yeni dinleyici uygulamaları hello SQL Server kullanılabilirlik grubundaki tooconnect toodatabases kullanmak hello ağ adı adıdır.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-123">hello name for hello new listener is hello network name that applications use tooconnect toodatabases in hello SQL Server availability group.</span></span>
   
    <span data-ttu-id="f5d5f-124">d.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-124">d.</span></span> <span data-ttu-id="f5d5f-125">toofinish oluşturma hello dinleyicisi tıklatın **sonraki** iki kez tıkladıktan sonra **son**.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-125">toofinish creating hello listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="f5d5f-126">Merhaba dinleyicisi veya kaynağı çevrimiçi bu noktada Getir değil.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-126">Do not bring hello listener or resource online at this point.</span></span>

3. <span data-ttu-id="f5d5f-127"><a name="congroup"></a>Merhaba IP kaynağı hello kullanılabilirlik grubu için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-127"><a name="congroup"></a>Configure hello IP resource for hello availability group.</span></span>

    <span data-ttu-id="f5d5f-128">a.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-128">a.</span></span> <span data-ttu-id="f5d5f-129">Merhaba tıklatın **kaynakları** sekmesini tıklatın ve ardından oluşturduğunuz hello istemci erişim noktası'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-129">Click hello **Resources** tab, and then expand hello client access point you created.</span></span>  
    <span data-ttu-id="f5d5f-130">Merhaba istemci erişim noktası çevrimdışıdır.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-130">hello client access point is offline.</span></span>

   ![İstemci erişim noktası](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="f5d5f-132">b.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-132">b.</span></span> <span data-ttu-id="f5d5f-133">Merhaba IP kaynağı sağ tıklayın ve ardından Özellikler'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-133">Right-click hello IP resource, and then click properties.</span></span> <span data-ttu-id="f5d5f-134">Başlangıç IP adresi hello adını not edin ve hello kullan `$IPResourceName` hello PowerShell Betiği değişkeni.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-134">Note hello name of hello IP address, and use it in hello `$IPResourceName` variable in hello PowerShell script.</span></span>

    <span data-ttu-id="f5d5f-135">c.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-135">c.</span></span> <span data-ttu-id="f5d5f-136">Altında **IP adresi**, tıklatın **statik IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="f5d5f-137">Merhaba aynı hello Azure portalı üzerinde hello yük dengeleyici adresi ayarlarken kullanılan adres gibi hello IP adresi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-137">Set hello IP address as hello same address that you used when you set hello load balancer address on hello Azure portal.</span></span>

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="f5d5f-139"><a name = "dependencyGroup"></a>Merhaba SQL Server kullanılabilirlik grubu kaynağının hello istemci erişim noktasında bağımlı hale getirin.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-139"><a name = "dependencyGroup"></a>Make hello SQL Server availability group resource dependent on hello client access point.</span></span>

    <span data-ttu-id="f5d5f-140">a.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-140">a.</span></span> <span data-ttu-id="f5d5f-141">Yük Devretme Kümesi Yöneticisi'nde **rolleri**, kullanılabilirlik grubunuzun'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="f5d5f-142">b.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-142">b.</span></span> <span data-ttu-id="f5d5f-143">Merhaba üzerinde **kaynakları** sekmesinde, altında **diğer kaynakları**hello kullanılabilirlik kaynak grubuna sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-143">On hello **Resources** tab, under **Other Resources**, right-click hello availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="f5d5f-144">c.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-144">c.</span></span> <span data-ttu-id="f5d5f-145">Merhaba Bağımlılıklar sekmesinde hello hello istemci erişim noktası (Merhaba dinleyicisi) kaynağın adını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-145">On hello dependencies tab, add hello name of hello client access point (hello listener) resource.</span></span>

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="f5d5f-147">d.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-147">d.</span></span> <span data-ttu-id="f5d5f-148">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-148">Click **OK**.</span></span>

5. <span data-ttu-id="f5d5f-149"><a name="listname"></a>Merhaba istemci erişimi olun noktası kaynak hello IP adresine bağımlı.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-149"><a name="listname"></a>Make hello client access point resource dependent on hello IP address.</span></span>

    <span data-ttu-id="f5d5f-150">a.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-150">a.</span></span> <span data-ttu-id="f5d5f-151">Yük Devretme Kümesi Yöneticisi'nde **rolleri**, kullanılabilirlik grubunuzun'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="f5d5f-152">b.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-152">b.</span></span> <span data-ttu-id="f5d5f-153">Merhaba üzerinde **kaynakları** sekmesinde, hello istemci erişim noktası kaynağa altında sağ **sunucu adı**ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-153">On hello **Resources** tab, right-click hello client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="f5d5f-155">c.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-155">c.</span></span> <span data-ttu-id="f5d5f-156">Merhaba tıklatın **bağımlılıkları** sekmesi. Başlangıç IP adresi bir bağımlılığı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-156">Click hello **Dependencies** tab. Verify that hello IP address is a dependency.</span></span> <span data-ttu-id="f5d5f-157">Değilse, bir bağımlılık hello IP adresine göre ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-157">If it is not, set a dependency on hello IP address.</span></span> <span data-ttu-id="f5d5f-158">Listelenen birden çok kaynak varsa hello IP adreslerini veya değil olduğunu doğrulayın ve, bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-158">If there are multiple resources listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="f5d5f-159">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-159">Click **OK**.</span></span> 

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="f5d5f-161">d.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-161">d.</span></span> <span data-ttu-id="f5d5f-162">Merhaba dinleyici adına sağ tıklayın ve ardından **çevrimiçine**.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-162">Right-click hello listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="f5d5f-163">Bağımlılıklar doğru şekilde yapılandırıldığından bu hello doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-163">You can validate that hello dependencies are correctly configured.</span></span> <span data-ttu-id="f5d5f-164">Yük Devretme Kümesi Yöneticisi'nde tooRoles gidin, hello kullanılabilirlik grubuna sağ tıklayın, **diğer eylemler**ve ardından **bağımlılık raporunu göster**.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-164">In Failover Cluster Manager, go tooRoles, right-click hello availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="f5d5f-165">Merhaba bağımlılıklar doğru şekilde yapılandırıldığında, hello kullanılabilirlik grubu hello ağ adı üzerinde bağımlıdır ve hello ağ hello IP adresine bağımlı adıdır.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-165">When hello dependencies are correctly configured, hello availability group is dependent on hello network name, and hello network name is dependent on hello IP address.</span></span> 


6. <span data-ttu-id="f5d5f-166"><a name="setparam"></a>Merhaba küme parametreleri PowerShell'de ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-166"><a name="setparam"></a>Set hello cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="f5d5f-167">a.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-167">a.</span></span> <span data-ttu-id="f5d5f-168">PowerShell komut dosyası tooone, SQL Server örnekleri aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-168">Copy hello following PowerShell script tooone of your SQL Server instances.</span></span> <span data-ttu-id="f5d5f-169">Merhaba değişkenleri ortamınız için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-169">Update hello variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="f5d5f-170">b.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-170">b.</span></span> <span data-ttu-id="f5d5f-171">Merhaba küme düğümlerinden birinin hello PowerShell betiğini çalıştırarak Hello küme parametreleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-171">Set hello cluster parameters by running hello PowerShell script on one of hello cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="f5d5f-172">SQL Server örnekleri farklı bölgelerde bulunuyorsa, toorun hello PowerShell Betiği iki kez gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-172">If your SQL Server instances are in separate regions, you need toorun hello PowerShell script twice.</span></span> <span data-ttu-id="f5d5f-173">Merhaba ilk kez, hello kullan `$ILBIP` ve `$ProbePort` hello ilk bölgesinden.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-173">hello first time, use hello `$ILBIP` and `$ProbePort` from hello first region.</span></span> <span data-ttu-id="f5d5f-174">Merhaba ikinci kez, hello kullan `$ILBIP` ve `$ProbePort` hello ikinci bölgesinden.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-174">hello second time, use hello `$ILBIP` and `$ProbePort` from hello second region.</span></span> <span data-ttu-id="f5d5f-175">Merhaba küme ağ adı ve hello küme IP kaynak adı olan hello aynı.</span><span class="sxs-lookup"><span data-stu-id="f5d5f-175">hello cluster network name and hello cluster IP resource name are hello same.</span></span> 

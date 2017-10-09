Merhaba kullanılabilirlik grubu dinleyicisi SQL Server kullanılabilirlik grubu dinlediği hello bir IP adresi ve ağ adı değil. toocreate hello kullanılabilirlik grubu dinleyicisi, hello aşağıdaki:

1. <a name="getnet"></a>Merhaba küme ağ kaynağı Hello adını alın.

    a. RDP tooconnect toohello hello birincil çoğaltmayı barındıran Azure sanal makine kullanın. 

    b. Yük Devretme Kümesi Yöneticisi'ni açın.

    c. Select hello **ağlar** düğümü ve Not hello küme ağ adı. Hello bu adı kullanmak `$ClusterNetworkName` hello PowerShell Betiği değişkeni. Görüntü hello küme ağ adı aşağıdaki Hello olan **küme ağ 1**:

   ![Küme ağ adı](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <a name="addcap"></a>Merhaba istemci erişim noktası ekleyin.  
    Merhaba istemci erişim noktası uygulamaları bir kullanılabilirlik grubunda tooconnect toohello veritabanlarını kullanmanızı hello ağ adıdır. Yük Devretme Kümesi Yöneticisi'nde Hello istemci erişim noktası oluşturun.

    a. Merhaba küme adını genişletin ve ardından **rolleri**.

    b. Merhaba, **rolleri** bölmesi, sağ hello kullanılabilirlik grubu adını ve ardından **kaynak ekleme** > **istemci erişim noktası**.

   ![İstemci erişim noktası](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    c. Merhaba, **adı** kutusunda, bu yeni dinleyici için bir ad oluşturun. 
   Merhaba hello yeni dinleyici uygulamaları hello SQL Server kullanılabilirlik grubundaki tooconnect toodatabases kullanmak hello ağ adı adıdır.
   
    d. toofinish oluşturma hello dinleyicisi tıklatın **sonraki** iki kez tıkladıktan sonra **son**. Merhaba dinleyicisi veya kaynağı çevrimiçi bu noktada Getir değil.

3. <a name="congroup"></a>Merhaba IP kaynağı hello kullanılabilirlik grubu için yapılandırın.

    a. Merhaba tıklatın **kaynakları** sekmesini tıklatın ve ardından oluşturduğunuz hello istemci erişim noktası'nı genişletin.  
    Merhaba istemci erişim noktası çevrimdışıdır.

   ![İstemci erişim noktası](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    b. Merhaba IP kaynağı sağ tıklayın ve ardından Özellikler'i tıklatın. Başlangıç IP adresi hello adını not edin ve hello kullan `$IPResourceName` hello PowerShell Betiği değişkeni.

    c. Altında **IP adresi**, tıklatın **statik IP adresi**. Merhaba aynı hello Azure portalı üzerinde hello yük dengeleyici adresi ayarlarken kullanılan adres gibi hello IP adresi ayarlayın.

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <a name = "dependencyGroup"></a>Merhaba SQL Server kullanılabilirlik grubu kaynağının hello istemci erişim noktasında bağımlı hale getirin.

    a. Yük Devretme Kümesi Yöneticisi'nde **rolleri**, kullanılabilirlik grubunuzun'a tıklayın.

    b. Merhaba üzerinde **kaynakları** sekmesinde, altında **diğer kaynakları**hello kullanılabilirlik kaynak grubuna sağ tıklayın ve ardından **özellikleri**. 

    c. Merhaba Bağımlılıklar sekmesinde hello hello istemci erişim noktası (Merhaba dinleyicisi) kaynağın adını ekleyin.

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    d. **Tamam** düğmesine tıklayın.

5. <a name="listname"></a>Merhaba istemci erişimi olun noktası kaynak hello IP adresine bağımlı.

    a. Yük Devretme Kümesi Yöneticisi'nde **rolleri**, kullanılabilirlik grubunuzun'a tıklayın. 

    b. Merhaba üzerinde **kaynakları** sekmesinde, hello istemci erişim noktası kaynağa altında sağ **sunucu adı**ve ardından **özellikleri**. 

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    c. Merhaba tıklatın **bağımlılıkları** sekmesi. Başlangıç IP adresi bir bağımlılığı olduğundan emin olun. Değilse, bir bağımlılık hello IP adresine göre ayarlayın. Listelenen birden çok kaynak varsa hello IP adreslerini veya değil olduğunu doğrulayın ve, bağımlılıkları. **Tamam** düğmesine tıklayın. 

   ![IP kaynağı](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    d. Merhaba dinleyici adına sağ tıklayın ve ardından **çevrimiçine**. 

    >[!TIP]
    >Bağımlılıklar doğru şekilde yapılandırıldığından bu hello doğrulayabilirsiniz. Yük Devretme Kümesi Yöneticisi'nde tooRoles gidin, hello kullanılabilirlik grubuna sağ tıklayın, **diğer eylemler**ve ardından **bağımlılık raporunu göster**. Merhaba bağımlılıklar doğru şekilde yapılandırıldığında, hello kullanılabilirlik grubu hello ağ adı üzerinde bağımlıdır ve hello ağ hello IP adresine bağımlı adıdır. 


6. <a name="setparam"></a>Merhaba küme parametreleri PowerShell'de ayarlayın.
    
    a. PowerShell komut dosyası tooone, SQL Server örnekleri aşağıdaki hello kopyalayın. Merhaba değişkenleri ortamınız için güncelleştirin.     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    b. Merhaba küme düğümlerinden birinin hello PowerShell betiğini çalıştırarak Hello küme parametreleri ayarlayın.  

    > [!NOTE]
    > SQL Server örnekleri farklı bölgelerde bulunuyorsa, toorun hello PowerShell Betiği iki kez gerekir. Merhaba ilk kez, hello kullan `$ILBIP` ve `$ProbePort` hello ilk bölgesinden. Merhaba ikinci kez, hello kullan `$ILBIP` ve `$ProbePort` hello ikinci bölgesinden. Merhaba küme ağ adı ve hello küme IP kaynak adı olan hello aynı. 

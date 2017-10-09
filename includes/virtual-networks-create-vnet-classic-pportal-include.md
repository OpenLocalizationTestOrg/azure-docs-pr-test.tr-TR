## <a name="how-toocreate-a-classic-vnet-in-hello-azure-portal"></a>Nasıl toocreate hello Azure portalı, klasik bir VNet
Yukarıdaki hello senaryoyu temel klasik bir VNet toocreate hello adımları izleyin.

1. Tarayıcıdan toohttp://portal.azure.com gidin ve gerekiyorsa Azure hesabınıza.
2. Tıklatın **yeni** > **ağ** > **sanal ağ**, o hello fark **dağıtım modeli seçin** Liste zaten gösterir **Klasik**ve ardından **oluşturma**hello aşağıdaki çizimde görüldüğü gibi.
   
    ![Azure portalında VNet oluşturma](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)
3. Merhaba üzerinde **sanal ağ** dikey penceresinde, türü hello **adı** hello VNet ve ardından **adres alanı**. Merhaba VNet ve kendi ilk alt ağ, adres alanı ayarlarını yapılandırmak ve ardından **Tamam**. Aşağıdaki Hello şekilde hello CIDR bloğu ayarlarını senaryomuz için gösterilmektedir.
   
    ![Adres alanı dikey penceresini](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)
4. Tıklatın **kaynak grubu** seçip bir kaynak grubu tooadd Vnet'e hello veya tıklatın **yeni kaynak grubu oluştur** tooadd hello VNet tooa yeni kaynak grubu. Merhaba aşağıdaki şekilde hello kaynak olarak adlandırılan yeni bir kaynak grubu için Grup ayarları gösterilmektedir **TestRG**. Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a Genel Bakış](../articles/azure-resource-manager/resource-group-overview.md#resource-groups)’ı ziyaret edin.
   
    ![Kaynak grubu dikey penceresi oluşturma](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)
5. Gerekirse, hello değiştirmek **abonelik** ve **konumu** ayarlarını. 
6. Toosee hello VNet hello parçasında olarak istemiyorsanız **Sabitle**, devre dışı **PIN tooStartboard**. 
7. Tıklatın **oluşturma** ve bildirimi hello döşeme adlı **sanal ağ oluşturuluyor** hello aşağıdaki çizimde gösterildiği gibi.
   
    ![Portalında VNet oluşturma](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)
8. Oluşturulan VNet toobe Hello için bekleyin ve aşağıda döşeme, tooadd tıklatın hello gördüğünüzde daha fazla alt ağ.
   
    ![Portalında VNet oluşturma](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)
9. Merhaba görmelisiniz **yapılandırma** aşağıda gösterildiği gibi VNet için. 
   
    ![Portalında VNet oluşturma](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)
10. Tıklatın **alt ağlar** > **Ekle**, yazın bir **adı** ve belirtin bir **adres aralığı (CIDR bloğu)** , alt ağ için ve ardından tıklatın **Tamam**. Aşağıdaki Hello şekilde geçerli senaryomuz için hello ayarları gösterilmektedir.
    
    ![Azure portalında VNet oluşturma](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)


Azure portalını kullanarak Resource Manager dağıtımında bir VNet oluşturmak için aşağıdaki adımları izleyin. Ekran görüntüleri örnek olarak verilmiştir. Değerlerin kendinizinkilerle değiştirildiğinden emin olun. Sanal ağlarla çalışma hakkında daha fazla bilgi için bkz. [Virtual Network’e Genel Bakış](../articles/virtual-network/virtual-networks-overview.md).

>[!NOTE]
>Bu VNet’in bir şirket içi konuma bağlanması için şirket içi ağ yöneticinizle bu ağ için özellikle kullanabileceğiniz bir IP adresi aralığı ayırma işlemini koordine etmeniz gerekir. VPN bağlantısının her iki tarafında bir yinelenen adres aralığı varsa, trafik beklediğiniz şekilde yönlendirilmez. Ayrıca, bu sanal ağı başka bir sanal ağa bağlamak isterseniz adres alanı diğer sanal ağ ile örtüşemez. Ağ yapılandırmanızı uygun şekilde planlamaya dikkat edin.
>
>

1. Tarayıcıdan [Azure portalına](http://portal.azure.com) gidin ve gerekiyorsa Azure hesabınızda oturum açın.
2. **+** öğesine tıklayın. **Market’te ara** alanına "Sanal Ağ" yazın. Döndürülen listeden **Sanal Ağ**’ı bulun ve tıklayarak **Sanal Ağ** sayfasını açın.

  ![Sanal Ağ kaynağı sayfasını bulma](./media/vpn-gateway-basic-vnet-rm-portal-include/newvnetportal700.png "Sanal Ağ kaynağı sayfasını bulma")
3. Sanal Ağ sayfasının en altına doğru, **Bir dağıtım modeli seçin** listesinden **Resource Manager**’ı seçip **Oluştur**’a tıklayın.

  ![Resource Manager’ı seçin](./media/vpn-gateway-basic-vnet-rm-portal-include/resourcemanager250.png "Resource Manager’ı seçin")
4. **Sanal ağ oluştur** sayfasında sanal ağ ayarlarını yapılandırın. Alanları doldururken, alana girilen karakterler geçerliyse kırmızı ünlem işareti yeşil onay işaretine dönüşür. Otomatik olarak doldurulmuş değerler olabilir. Böyle değerler varsa, değerleri kendi değerlerinizle değiştirin. **Sanal ağ oluştur** sayfası aşağıdaki örneğe benzer şekilde görünür.

  ![Sanal ağ oluşturma sayfası](./media/vpn-gateway-basic-vnet-rm-portal-include/vnet.png "Sanal ağ oluşturma sayfası")
5. **Ad**: Sanal ağınızın adını girin.
6. **Adres alanı**: Adres alanını girin. Eklenecek birden fazla adres alanınız varsa birinci adres alanınızı ekleyin. Sanal ağı oluşturduktan sonra başka adres alanları ekleyebilirsiniz.
7. **Abonelik**: Listelenen aboneliğin doğru olduğunu onaylayın. Açılan listeyi kullanarak abonelikleri değiştirebilirsiniz.
8. **Kaynak grubu**: Var olan bir kaynak grubunu seçin ya da yeni kaynak grubunuz için bir ad yazarak yeni bir tane oluşturun. Yeni bir grup oluşturuyorsanız, planlanan yapılandırma değerlerinize göre kaynak grubunu adlandırın. Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a Genel Bakış](../articles/azure-resource-manager/resource-group-overview.md#resource-groups) sayfasını ziyaret edin.
9. **Konum**: Sanal ağınızın konumunu seçin. Konum bu sanal ağa dağıttığınız kaynakların nerede olacağını belirler.
10. **Alt ağ**: Alt ağ adını ve alt ağ adres aralığını ekleyin. Sanal ağı oluşturduktan sonra başka alt ağlar ekleyebilirsiniz.
11. VNet’inizi panoda kolay bulmak istiyorsanız **Panoya sabitle**’yi seçin ve ardından **Oluştur**’a tıklayın.

  ![Panoya sabitleme](./media/vpn-gateway-basic-vnet-rm-portal-include/pintodashboard150.png "Panoya sabitleme")
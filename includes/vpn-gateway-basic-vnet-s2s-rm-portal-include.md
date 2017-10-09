toocreate hello Resource Manager dağıtım modelinde'hello Azure portalını kullanarak VNet hello adımları izleyin. Kullanım hello [örnek değerler](#values) bir öğretici bu adımları kullanıyorsanız. Bu adımları bir öğretici yaptığınızı değil, emin tooreplace hello değerleri kendi değerlerinizle olması. Sanal ağlarla çalışma hakkında daha fazla bilgi için bkz: Merhaba [Virtual Network'e genel bakış](../articles/virtual-network/virtual-networks-overview.md).

1. Tarayıcıdan toohello gidin [Azure portal](http://portal.azure.com) ve Azure hesabınızla oturum açın.
2. **Yeni**’ye tıklayın. Merhaba, **arama hello Market** alanında, 'Sanal ağ' yazın. Bulun **sanal ağ** döndürülen hello listelemek ve tooopen hello'ı tıklatın **sanal ağ** dikey.
3. Merhaba alt kısmındaki hello sanal ağ dikey hello penceresinden **dağıtım modeli seçin** listesinde, seçin **Resource Manager**ve ardından **oluşturma**. Bu hello 'Sanal ağ oluştur' dikey pencere açılır.

    ![Sanal ağ oluşturma dikey penceresi](./media/vpn-gateway-basic-vnet-s2s-rm-portal-include/createvnet.png "Create virtual network blade")
4. Merhaba üzerinde **sanal ağ oluştur** dikey penceresinde hello VNet ayarlarını yapılandırın. Merhaba alanları doldurun, hello alanına girilen hello karakterler geçerli olduğunda hello kırmızı bir ünlem işareti yeşil bir onay işareti haline gelir.

  - **Ad**: hello sanal ağınız için bir ad girin. Bu örnekte TestVNet1 kullandık.
  - **Adres alanı**: hello adres alanı girin. Birden çok adres alanları tooadd varsa, ilk adres alanınızı ekleyin. Merhaba VNet oluşturduktan sonra ek adres alanları daha sonra ekleyebilirsiniz. Şirket içi konumunuz hello adres alanı çakışmadığından belirtin, hello adres alanı emin olun.
  - **Alt ağ adı**: hello ilk alt ağ adı ve alt ağ adres aralığı Ekle. Bu VNet oluşturduktan sonra ek alt ağlar ve hello ağ geçidi alt ağı daha sonra ekleyebilirsiniz. 
  - **Abonelik**: hello abonelik listelenen doğru olanı hello olduğunu doğrulayın. Merhaba açılan kullanarak abonelikleri değiştirebilirsiniz.
  - **Kaynak grubu**: Var olan bir kaynak grubunu seçin ya da yeni kaynak grubunuz için bir ad yazarak yeni bir tane oluşturun. Yeni bir grup oluşturuyorsanız, tooyour göre adı hello kaynak grubu yapılandırma değerlerini planlanan. Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a Genel Bakış](../articles/azure-resource-manager/resource-group-overview.md#resource-groups)’ı ziyaret edin.
  - **Konum**: sanal ağınızı hello konumu seçin. Merhaba kaynakları toothis VNet dağıtmadan bulunacağı Hello konumunu belirler.

5. Seçin **PIN toodashboard** toobe mümkün toofind ağınızı hello Panoda kolayca isterseniz ve ardından **oluşturma**. ' I tıklattıktan sonra **oluşturma**, Panonuzda hello Vnet'inizin ilerleme durumunu yansıtacak bir kutucuk görürsünüz. VNet Hello döşeme değişiklikleri hello olarak oluşturuldu.

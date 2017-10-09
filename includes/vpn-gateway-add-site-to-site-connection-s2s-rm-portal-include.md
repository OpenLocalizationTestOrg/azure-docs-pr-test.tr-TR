1. Sanal ağ geçidiniz için tooand açık hello dikey penceresine gidin. Birden çok yol toonavigate vardır. Bizim örneğimizde, biz toohello ağ geçidi 'VNet1GW' çok giderek gittiğinizde**TestVNet1 -> genel bakış bağlı -> cihazları -> VNet1GW**.
2. VNet1GW için Hello dikey penceresinde **bağlantıları**. Merhaba bağlantıları dikey penceresinde Hello üstünde tıklatın **+ Ekle** tooopen hello **Bağlantı Ekle** dikey.

    ![Siteden Siteye bağlantısı oluşturma](./media/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include/connection1.png)

3. Merhaba üzerinde **Bağlantı Ekle** dikey penceresinde hello doldurun bağlantınızı toocreate değerleri.

  - **Ad:** Bağlantınızı adlandırın. Örneğimizde **VNet1toSite2** kullandık.
  - **Bağlantı türü:** **Siteden siteye (IPSec)** seçeneğini belirleyin.
  - **Sanal ağ geçidi:** hello değeri, bu ağ geçidinden bağlandığınızdan sabittir.
  - **Yerel ağ geçidi:** tıklatın **bir yerel ağ geçidi seçin** ve select hello yerel ağ geçidi toouse istiyor. Örneğimizde **Site2** kullandık.
  - **Paylaşılan anahtar:** buraya hello değer, yerel şirket içi VPN cihazınız için kullandığınız hello değeri aynı olmalıdır. Merhaba örnekte 'abc123' kullandık, ancak daha karmaşık bir şey olabilir ve kullanmanız gerekir. Burada belirttiğiniz başlangıç değeri şeydir önemli Hello hello aynı VPN Cihazınızı yapılandırırken belirtilen değeri olmalıdır.
  - değerlerini kalan hello **abonelik**, **kaynak grubu**, ve **konumu** düzeltilmiştir.

4. Tıklatın **Tamam** toocreate bağlantınızı. Göreceğiniz *bağlantısı oluşturuluyor* Merhaba ekranında flash.
5. Hello hello bağlantı görüntüleyebilirsiniz **bağlantıları** hello sanal ağ geçidi dikey. Merhaba durumu gelen gidecek *bilinmeyen* çok*bağlanıyor*ve ardından çok*başarılı*.

1. Portal sayfasının sol tarafına **+** simgesine tıklayın ve arama alanına ‘Sanal Ağ Geçidi’ yazın. **Sonuçlar** alanında **Sanal Ağ Geçidi**’ni bulup tıklayın.
2. ‘Sanal ağ geçidi’ sayfasının alt tarafındaki **Oluştur**'a tıklayın. Bu işlem **Sanal ağ geçidi oluşturma** sayfasını açar.

    ![Sanal ağ geçidi oluştur sayfasının alanları](./media/vpn-gateway-add-gw-s2s-rm-portal-include/newgw.png "Yeni ağ geçidi")
3. **Sanal ağ geçidi oluştur** sayfasında sanal ağ geçidinize ait değerleri belirtin.

  - **Ad**: Ağ geçidinizi adlandırın. Bir ağ geçidi alt ağını adlandırmayla aynı değildir. Bu ad, oluşturduğunuz ağ geçidi nesnesinin adıdır.
  - **Ağ geçidi türü**: **VPN**’i seçin. VPN ağ geçitleri, **VPN** sanal ağ geçidi türünü kullanır. 
  - **VPN türü**: Yapılandırmanızla ilgili belirtilen VPN türünü seçin. Çoğu yapılandırma, Yol Tabanlı bir VPN türü gerektirir.
  - **SKU**: Açılır listeden ağ geçidi SKU’sunu seçin. Açılır listede sıralanan SKU’lar seçtiğiniz VPN türüne bağlıdır. Ağ geçidi SKU’ları hakkında bilgi için bkz. [Ağ geçidi SKU’ları](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).
  - **Konum**: Konumu görmek için kaydırmanız gerekebilir. **Konum** alanını, sanal ağınızın bulunduğu konumu işaret edecek şekilde ayarlayın. Konum, sanal ağınızın bulunduğu bölgeye işaret etmiyorsa, sonraki adımda bir sanal ağ seçtiğinizde bu seçim açılır listede görünmez.
  - **Sanal ağ**: Bu ağ geçidini eklemek istediğiniz sanal ağı seçin. **Sanal ağ**'a tıklayarak ‘Sanal ağ seçin’ sayfasını açın. VNet'i seçin. VNet'inizi görmüyorsanız Konum alanının, sanal ağınızın bulunduğu bölgeyi işaret ettiğinden emin olun.
  - **Geçit alt ağı adres aralığı**: Bu ayarı yalnızca daha önce sanal ağınız için bir ağ geçidi alt ağı oluşturmadıysanız görürsünüz. Daha önce geçerli bir ağ geçidi alt ağı oluşturduysanız, bu ayar görünmez.
  - **İlk IP yapılandırması**: 'Genel IP adresi seçin' sayfası, VPN ağ geçidi ile ilişkilendirilen genel bir IP adresi nesnesi oluşturur. VPN ağ geçidi oluşturulduğunda genel IP adresi bu nesneye dinamik olarak atanır. VPN Gateway hizmeti şu anda yalnızca *Dinamik* Genel IP adresi ayırmayı desteklemektedir. Ancak, bu durum IP adresinin VPN ağ geçidinize atandıktan sonra değiştiği anlamına gelmez. Genel IP adresi, yalnızca ağ geçidi silinip yeniden oluşturulduğunda değişir. VPN ağ geçidiniz üzerinde gerçekleştirilen yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında değişmez.

    - Önce **Ağ geçidi IP yapılandırması oluştur**'a tıklayarak ‘Genel IP adresi seç’ sayfasını, sonra da **+Yeni Oluştur**'a tıklayarak ‘Genel IP adresi oluştur" sayfasını açın.
    - Ardından, genel IP adresiniz için bir **Ad** girin. Başka bir değere değiştirmeniz için özel bir neden yoksa SKU’yu **Temel** olarak bırakın, sonra bu sayfanın altındaki **Tamam**’a tıklayarak değişikliklerinizi kaydedin.

      ![Genel IP oluşturma](./media/vpn-gateway-add-gw-s2s-rm-portal-include/gwip.png "PIP oluşturma")

4. Ayarları doğrulayın. Ağ geçidinizin panoda görünmesini istiyorsanız sayfanın en altında yer alan **Panoya sabitle** seçeneğini belirleyebilirsiniz. 
5. VPN ağ geçidi oluşturmaya başlamak için **Oluştur**'a tıklayın. Ayarlar doğrulandıktan sonra, panoda "Sanal ağ geçidi dağıtma" kutucuğunu görürsünüz. Bir ağ geçidi oluşturma 45 dakika kadar sürebilir. Tamamlanma durumunu görmek için portal sayfanızı yenilemeniz gerekebilir.

Ağ geçidi oluşturulduktan sonra, portalda sanal ağa bakarak bu ağ geçidine atanmış IP adresini görüntüleyin. Ağ geçidi bağlı bir cihaz gibi görüntülenir. Daha fazla bilgi görüntülemek için bağlı cihaza (sanal ağ geçidiniz) tıklayabilirsiniz.
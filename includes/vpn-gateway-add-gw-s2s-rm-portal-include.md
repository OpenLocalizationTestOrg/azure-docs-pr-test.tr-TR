1. Yan hello portal sayfasının sol hello üzerinde tıklatın  **+**  ve Ara 'Sanal ağ geçidi' yazın. **Sonuçlar** alanında **Sanal Ağ Geçidi**’ni bulup tıklayın.
2. Merhaba 'Sanal ağ geçidi' dikey penceresinde Hello altındaki tıklatın **oluşturma**. Merhaba açılır **sanal ağ geçidi Oluştur** dikey.

    ![Sanal ağ geçidi oluştur dikey penceresinin alanları](./media/vpn-gateway-add-gw-s2s-rm-portal-include/vnet_gw.png "Yeni ağ geçidi")

3. Merhaba üzerinde **sanal ağ geçidi Oluştur** dikey penceresinde, sanal ağ geçidinizi hello değerlerini belirtin.

  - **Ad**: Ağ geçidinizi adlandırın. Bu olduğu değil hello bir ağ geçidi alt ağını adlandırmayla aynı. Oluşturmakta olduğunuz hello ağ geçidi nesnesinin hello adı kullanıcının.
  - **Ağ geçidi türü**: **VPN**’i seçin. VPN ağ geçitleri kullanmaları hello sanal ağ geçidi türü **VPN**. 
  - **VPN türü**: yapılandırmanızla ilgili belirtilen hello VPN türünü seçin. Çoğu yapılandırma, Yol Tabanlı bir VPN türü gerektirir.
  - **SKU**: Select hello ağ geçidinden SKU hello açılır. Merhaba açılır listede hello SKU'ları hello Seçtiğiniz VPN türü üzerinde bağlıdır. Ağ geçidi SKU’ları hakkında bilgi için bkz. [Ağ geçidi SKU’ları](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).
  - **Konum**: tooscroll toosee konumu gerekebilir. Merhaba ayarlamak **konumu** alan sanal ağınızı bulunduğu toopoint toohello konumu. Başlangıç konumu, sanal ağınızda bulunduğu toohello bölge işaret etmiyor, hello sanal ağ açılır 'sanal ağ seçin' hello sonraki adımda görünmez.
  - **Sanal ağ**: hello sanal ağ toowhich seçin bu ağ geçidi tooadd istiyor. Tıklatın **sanal ağ** tooopen hello 'sanal ağ seçin' dikey. Merhaba VNet seçin. Sanal ağınızı görmüyorsanız, sanal ağınızı bulunduğu toohello bölge hello konum alanı işaret ettiğinden emin olun.
  - **Genel IP adresi**: hello 'ortak IP adresi oluştur' dikey bir ortak IP adresi nesnesi oluşturur. Merhaba VPN ağ geçidi oluşturulduğunda hello genel IP adresi dinamik olarak atanır. VPN Gateway hizmeti şu anda yalnızca *Dinamik* Genel IP adresi ayırmayı desteklemektedir. Ancak, bu tooyour VPN ağ geçidi atandıktan sonra hello IP adresini değiştirse anlamına gelmez. ağ geçidi Hello genel IP adresi değişiklikleri hello zaman hello yalnızca zaman silinmiş ve yeniden oluşturulmalıdır. VPN ağ geçidiniz üzerinde gerçekleştirilen yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında değişmez.

    - Önce tıklatın **genel IP adresi** tooopen dikey 'genel IP adresi seçin' hello ve ardından **+ Yeni Oluştur** tooopen hello 'ortak IP adresi oluştur' dikey.
    - Ardından, Giriş bir **adı** için genel IP adresi, ardından **Tamam** sırasında değişikliklerinizi bu dikey toosave alt hello.

      ![Genel IP oluşturma](./media/vpn-gateway-add-gw-s2s-rm-portal-include/pip.png "PIP oluşturma")

4. Hello ayarlarını doğrulayın. Seçebileceğiniz **PIN toodashboard** , ağ geçidi tooappear hello Panoda istiyorsanız hello dikey penceresinde hello sonundaki. 
5. Tıklatın **oluşturma** toobegin hello VPN ağ geçidi oluşturma. Merhaba görürsünüz ve Hello ayarları doğrulandı "Dağıtma sanal ağ geçidi" Merhaba Panoda döşeme. Bir ağ geçidi oluşturma too45 dakika sürebilir. Portal sayfasının toosee tamamlandı hello durumunuzu toorefresh gerekebilir.

Merhaba ağ geçidi oluşturulduktan sonra tooit hello portaldaki sanal ağın hello bakarak atandı hello IP adresini görüntüleyin. Merhaba ağ geçidi bağlı bir aygıt görüntülenir. Daha fazla bilgi bağlı hello aygıt (sanal ağ geçidiniz) tooview tıklayabilirsiniz.

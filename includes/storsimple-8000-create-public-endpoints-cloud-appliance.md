#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a>toocreate genel Uç noktalara hello bulut uygulaması

1. Toohello Azure portalında oturum açın.
2. Çok Git**sanal makineleri**, seçin ve bulut uygulaması olarak kullanılan hello sanal makineye tıklayın.
    
3. Sanal makineniz ve bu moddan toocreate bir ağ güvenlik grubu (NSG) kural toocontrol hello trafik akışını gerekir. Aşağıdaki adımları toocreate bir NSG kuralı hello gerçekleştirin.
    1. **Ağ güvenlik grubu**’nu seçin.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. Sunulan hello varsayılan ağ güvenlik grubunu tıklatın.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. **Gelen güvenlik kuralları**’nı seçin.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. Tıklatın **+ Ekle** toocreate bir gelen güvenlik kuralı.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        Merhaba Ekle gelen güvenlik kuralı dikey penceresinde:

        1. Hello için **adı**, türü hello aşağıdaki hello uç noktası için ad: WinRMHttps.
        
        2. Hello için **öncelik**seçin (Merhaba varsayılan kural hello önceliği olan) bir sayı 1000'den küçük. Daha yüksek hello değeri, düşük hello önceliği.

        3. Set hello **kaynak** çok**herhangi**.

        4. Hello için **hizmet**seçin **WinRM**. Merhaba **Protokolü** otomatik olarak çok ayarlanır**TCP** ve hello **bağlantı noktası aralığı** çok ayarlanır**5986**.

        5. Tıklatın **Tamam** toocreate hello kuralı.

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. Ağınızda güvenlik grubunun bir alt ağ veya belirli bir ağ arabiriminde tooassociate, son adımdır. Aşağıdaki adımları tooassociate hello bir alt ağ, ağ güvenlik grubuyla gerçekleştirin.
    1. Çok Git**alt ağlar**.
    2. **+ İlişkilendir**’e tıklayın.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. Sanal ağınızı seçin ve ardından hello uygun alt ağ seçin.
    4. Tıklatın **Tamam** toocreate hello kuralı.

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

Merhaba kural oluşturulduktan sonra ayrıntıları toodetermine hello ortak sanal IP (VIP) adresini görüntüleyebilirsiniz. Bu adresini kaydedin.



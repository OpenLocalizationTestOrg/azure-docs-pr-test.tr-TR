<!--author=alkohli last changed: 01/12/17-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello en düşük StorSimple cihaz Kurulumu

   > [!NOTE]
   > Merhaba minimum cihaz kurulumu tamamlandıktan sonra hello aygıt adı değiştirilemiyor.
   
1. Merhaba tablo hello cihazların listesi gelen **aygıtları** dikey penceresinde, seçin ve aygıtınızı tıklatın. Merhaba aygıttır içinde bir **yukarı tooset hazır** durumu. Merhaba **cihazı Yapılandır** dikey penceresi açılır.

     ![StorSimple en düşük cihaz kurulumu ağ arabirimleri](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. Merhaba, **cihazı Yapılandır** dikey penceresinde:
   
   1. Cihazınızın **kolay adını** sağlayın. Merhaba varsayılan cihaz adı hello cihaz modeli ve seri numarası gibi bilgileri yansıtır. Cihazınızı too64 karakter toomanage oluşturan bir kolay ad atayabilirsiniz.
   2. Set hello **saat dilimi** hangi hello aygıt dağıtıldığından hello coğrafi konum temelinde. Cihazınız zamanlanan tüm işlemler için bu saat dilimini kullanır.
   3. Merhaba altında **veri 0 ayarları**:

       1. Ağ hello Kurulum Sihirbazı ile yapılandırılmış ayarlarını (IP alt ağ, ağ geçidi), veri 0 ağ arabirimi ile Merhaba etkin olarak gösterir. iSCSI ile birlikte DATA 0 da bulut için otomatik olarak etkinleştirilir.

       2. Merhaba denetleyici 0 için IP adresleri ve denetleyici 1 sabit sağlar. **Merhaba denetleyici sabit IP adresleri toobe IP'leri hello alt ağ içinde erişilebilir hello aygıt IP adresi ile serbest.** Merhaba DATA 0 arabirimi IPv4 için hello yapılandırılmış IP adresleri gerek toobe IPv4 biçiminde hello sağlanan sabit ise. IPv6 Yapılandırması için bir önek sağladıysanız, sabit IP adresleri hello doldurulur otomatik olarak bu alanlara.

            ![StorSimple en düşük cihaz kurulumu ağ arabirimleri](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            Sabit hello denetleyicisi için IP adresleri hello hello güncelleştirmeleri toohello aygıt bakım için kullanılır. Bu nedenle, hello sabit IP'ler yönlendirilebilir ve mümkün tooconnect toohello Internet olması gerekir. Sabit denetleyici ıp'lerinizin yönlendirilebilir olduğunu hello kullanarak denetleyebilirsiniz [Test HcsmConnection] [ Test] cmdlet'i. Denetleyici sabit gösterir yönlendirilmiş toohello Internet olan ve erişebilirsiniz örneği aşağıdaki hello Microsoft Update sunucularına hello.

            ![Yönlendirilebilir IP’leri gösteren Test HcsmConnection](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. **Tamam** düğmesine tıklayın. Merhaba aygıt yapılandırması başlatır. Merhaba aygıt yapılandırması tamamlandığında, size bildirilir. Aygıt durum değişikliklerini çok hello**çevrimiçi** hello içinde **aygıtları** dikey.

    ![StorSimple en düşük cihaz kurulumu ağ arabirimleri](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx

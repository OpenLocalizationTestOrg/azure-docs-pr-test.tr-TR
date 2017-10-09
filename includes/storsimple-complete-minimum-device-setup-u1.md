<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello en düşük StorSimple cihaz Kurulumu
1. Merhaba cihazı seçin ve'ı tıklatın **Hızlı Başlangıç**. Tıklatın **cihaz kurulumunu Tamamla** toostart hello cihaz Yapılandırma Sihirbazı.
2. Merhaba yapılandırma aygıtı Sihirbazı'ndaki **temel ayarları** iletişim kutusunda, aşağıdaki hello:
   
   1. Cihazınızın **kolay adını** sağlayın. Merhaba varsayılan cihaz adı hello cihaz modeli ve seri numarası gibi bilgileri yansıtır. Cihazınızı too64 karakter toomanage oluşturan bir kolay ad atayabilirsiniz.
   2. Set hello **saat dilimi** hangi hello aygıt dağıtıldığından hello coğrafi konum temelinde. Cihazınız zamanlanan tüm işlemler için bu saat dilimini kullanır.
   3. **DNS Ayarları** altında **ikincil DNS Sunucusu** için bir adres girin. IPv6 kullanıyorsanız, hello alan hello Windows PowerShell arabiriminde sağlanan IPv6 önekini hello dayanarak doldurulur. 
      Merhaba ikincil DNS sunucusu yapılandırılmamışsa, tutulacak toosave aygıt yapılandırmanıza izin verilir.
   4. iSCSI etkin arabirimlerin altında iSCSI için en az bir ağ etkinleştirin. En az bir ağ arabiriminin bulut etkin toobe gerekir ve iSCSI etkin toobe bir arabirim gerekiyor. DATA 0 otomatik olarak bulut etkindir.
      
      ![StorSimple en düşük cihaz kurulumu temel ayarları](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupBasicSettings1-include.png)
3. Merhaba ok simgesine tıklayın. ![StorSimple ok simgesi](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
4. Merhaba, **ağ arabirimleri** iletişim kutusunda, hello sabit IP adresleri için denetleyici 0 ve denetleyici 1 sağlayın. **Merhaba denetleyici sabit IP adresleri toobe IP'leri hello alt ağ içinde erişilebilir hello aygıt IP adresi ile serbest.** Merhaba DATA 0 arabirimi IPv4 için hello yapılandırılmış IP adresleri gerek toobe IPv4 biçiminde hello sağlanan sabit ise. IPv6 Yapılandırması için bir önek sağladıysanız bu alanlar sabit IP adresleri hello otomatik olarak doldurulur.

    ![StorSimple en düşük cihaz kurulumu ağ arabirimleri](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

    Sabit hello denetleyicisi için IP adresleri hello hello güncelleştirmeleri toohello aygıt bakım için kullanılır ve bu nedenle sabit IP'leri hello yönlendirilebilir ve mümkün tooconnect toohello Internet olması gerekir. Sabit denetleyici ıp'lerinizin yönlendirilebilir olduğunu hello kullanarak denetleyebilirsiniz [Test HcsmConnection] [ Test] cmdlet'i. Denetleyici sabit gösterir yönlendirilmiş toohello Internet olan ve erişebilirsiniz örneği aşağıdaki hello Microsoft Update sunucularına hello. 

     ![Yönlendirilebilir IP’leri gösteren Test HcsmConnection](./media/storsimple-complete-minimum-device-setup-u1/Test-HcsmConnectionOutputRegisteredDevice.png)

1. Merhaba onay simgesine ![StorSimple onay simgesi](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Toohello aygıt döndürülecek **Hızlı Başlangıç** sayfası.
   
   > [!NOTE]
   > Merhaba erişerek dilediğiniz zaman başka cihaz ayarını tüm hello değiştirebilirsiniz **yapılandırma** sayfası.
   > 
   > 

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a>Merhaba seri Konsolu aracılığıyla tooconnect
1. Seri kabloyu toohello aygıtınızı (doğrudan veya bir USB seri bağdaştırıcısı aracılığıyla) bağlayın.
2. Açık hello **Denetim Masası**ve ardından hello açın **Aygıt Yöneticisi'ni**.
3. Merhaba COM bağlantı noktası hello aşağıdaki çizimde gösterildiği gibi belirleyin.
   
     ![Seri konsol üzerinden bağlanma](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. PuTTY’yi başlatın. 
5. Merhaba sağ bölmede, hello değiştirme **bağlantı türü** çok**seri**.
6. Merhaba sağ bölmede, hello uygun COM bağlantı noktasını yazın. Merhaba seri yapılandırma parametrelerinin gibi ayarlandığından emin olun:
   
   * Hız: 115.200
   * Veri bitleri: 8
   * Dur bitleri: 1
   * Eşlik: Yok
   * Akış denetimi: Yok
     
     Bu ayarlar, aşağıdaki çizimde hello gösterilir.
     
     ![PuTTY ayarları](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > Merhaba varsayılan akış denetimi ayarı çalışmazsa hello akış denetimi tooXON/XOFF ayarlamayı deneyin.
     > 
     > 
7. Tıklatın **açık** toostart seri oturumu.


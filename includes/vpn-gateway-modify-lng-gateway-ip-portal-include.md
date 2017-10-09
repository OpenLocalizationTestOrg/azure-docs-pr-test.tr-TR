### <a name="gwipnoconnection"></a>toomodify hello yerel ağ geçidi IP adresi - hiçbir ağ geçidi bağlantısı

Merhaba örnek toomodify bir ağ geçidi bağlantısı olmayan yerel ağ geçidi kullanın. Bu değer değiştirirken hello adres öneklerini hello adresindeki de değiştirebilirsiniz aynı anda.

1. Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **yapılandırma**.
2. Merhaba, **IP adresi** kutusunda, hello IP adresini değiştirin.
3. Tıklatın **kaydetmek** toosave hello ayarları.

### <a name="gwipwithconnection"></a>ağ geçidi bağlantısı varolan toomodify hello yerel ağ geçidi ağ geçidi IP adresi-

toomodify bağlantısı olan bir yerel ağ geçidi, toofirst Kaldır hello bağlantı gerekir. Merhaba bağlantı kaldırıldıktan sonra hello ağ geçidi IP adresi değiştirebilir ve yeni bir bağlantı oluşturun. Merhaba adres öneklerini hello adresindeki değiştirebilirsiniz aynı anda. Bunun sonucunda, VPN bağlantınızda kesinti oluşur. Merhaba ağ geçidi IP adresi değiştirirken toodelete hello VPN ağ geçidi gerekmez. Yalnızca tooremove hello bağlantı gerekir.
 
#### <a name="1-remove-hello-connection"></a>1. Merhaba bağlantısını kaldırın.

1. Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **bağlantıları**.
2. Merhaba tıklatın **...**  hello bağlantı hello satırında, ardından **silmek**.
3. Tıklatın **kaydetmek** toosave ayarlarınızı.

#### <a name="2-modify-hello-ip-address"></a>2. Başlangıç IP adresini değiştirin.

Merhaba adres öneklerini hello adresindeki değiştirebilirsiniz aynı anda.

1. Merhaba, **IP adresi** kutusunda, hello IP adresini değiştirin.
2. Tıklatın **kaydetmek** toosave hello ayarları.

#### <a name="3-recreate-hello-connection"></a>3. Merhaba bağlantısını yeniden oluşturun.

1. Sanal ağ geçidi toohello ağınız için gidin. (Değil hello yerel ağ geçidi.)
2. Merhaba hello sanal ağ geçidi üzerinde **ayarları** 'yi tıklatın **bağlantıları**.
3. Merhaba tıklatın **+ Ekle** tooopen hello **Bağlantı Ekle** dikey.
4. Bağlantınızı yeniden oluşturun.
5. Tıklatın **Tamam** toocreate hello bağlantı.

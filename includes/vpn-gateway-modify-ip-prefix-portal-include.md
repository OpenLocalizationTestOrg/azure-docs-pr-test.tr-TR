### <a name="noconnection"></a>toomodify yerel ağ geçidi IP adresi öneklerini - ağ geçidi bağlantısı yok

#### <a name="tooadd-additional-address-prefixes"></a>tooadd ek adres öneklerini:

1. Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **yapılandırma**.
2. Hello Hello IP adres alanı Ekle *ek adres aralığı Ekle* kutusu.
3. Tıklatın **kaydetmek** toosave ayarlarınızı.

#### <a name="tooremove-address-prefixes"></a>tooremove adres öneklerini:

1. Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **yapılandırma**.
2. Merhaba tıklatın **'...'** hello önek içeren hello satırda tooremove istiyor.
3. Tıklatın **kaldırmak**.
4. Tıklatın **kaydetmek** toosave ayarlarınızı.

### <a name="withconnection"></a>ağ geçidi bağlantısı varolan toomodify yerel ağ geçidi IP adresi öneklerini-

Bir ağ geçidi bağlantısına sahip ve tooadd istediğiniz veya yerel ağ geçidinizinde başlangıç IP adresi öneklerini kaldırırsanız, aşağıdaki adımları sırayla toodo hello gerekir. Bunun sonucunda, VPN bağlantınızda kesinti oluşur. IP adres öneklerini değiştirirken toodelete hello VPN ağ geçidi gerekmez. Yalnızca tooremove hello bağlantı gerekir.

#### <a name="1-remove-hello-connection"></a>1. Merhaba bağlantısını kaldırın.

1. Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **bağlantıları**.
2. Merhaba tıklatın **...**  her bağlantı hello satırında, ardından **silmek**.
3. Tıklatın **kaydetmek** toosave ayarlarınızı.

#### <a name="2-modify-hello-address-prefixes"></a>2. Merhaba adres öneklerini değiştirme.

tooadd ek adres öneklerini:

1. Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **yapılandırma**.
2. Başlangıç IP adresi alanı ekleyin.
3. Tıklatın **kaydetmek** toosave ayarlarınızı.

tooremove adres öneklerini:

1. Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **yapılandırma**.
2. Merhaba tıklatın **...**  hello önek içeren hello satırda tooremove istiyor.
3. Tıklatın **kaldırmak**.
4. Tıklatın **kaydetmek** toosave ayarlarınızı.

#### <a name="3-recreate-hello-connection"></a>3. Merhaba bağlantısını yeniden oluşturun.

1. Sanal ağ geçidi toohello ağınız için gidin. (Değil hello yerel ağ geçidi.)
2. Merhaba hello sanal ağ geçidi üzerinde **ayarları** 'yi tıklatın **bağlantıları**.
3. Merhaba tıklatın **+ Ekle** tooopen hello **Bağlantı Ekle** dikey.
4. Bağlantınızı yeniden oluşturun.
5. Tıklatın **Tamam** toocreate hello bağlantı.

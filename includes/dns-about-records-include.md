### <a name="record-names"></a>Kayıt adları

Azure DNS’de, kayıtlar göreli adlar kullanılarak belirtilir. A *tam* etki alanı adı (FQDN) içeren hello bölge adını, ancak bir *göreli* adı yok. Örneğin, hello göreli kayıt adı 'contoso.com"Merhaba bölgesinde ' www' hello tam kayıt adını 'www.contoso.com' verir.

Bir *tepesindeki* kaydıdır bir DNS kaydı hello kökündeki (veya *tepesindeki*) bir DNS bölgesinin. Örneğin, hello DNS bölgesine "contoso.com" tepesindeki kayıt ayrıca hello tam adı "contoso.com" vardır (buna bazen denir bir *naked* etki alanı).  Kurala göre göreli adı hello ' @' kullanılan toorepresent tepesindeki kayıttır.

### <a name="record-types"></a>Kayıt türleri

Her DNS kaydında bir ad ve bir tür vardır. Kayıtlar, içerdikleri toohello veri göre çeşitli türleri düzenlenir. Merhaba en yaygın türü adı tooan IPv4 adresi eşleştiren bir 'Bir' kayıttır. Başka bir ortak bir ad tooa posta sunucusu eşler 'MX' kaydı türüdür.

Azure DNS; A, AAAA, CNAME, MX, NS, PTR, SOA, SRV ve TXT gibi tüm yaygın DNS kayıt türlerini destekler. [SPF kayıtlarının TXT kaydı kullanılarak gösterildiğini](../articles/dns/dns-zones-records.md#spf-records) unutmayın.

### <a name="record-sets"></a>Kayıt kümeleri

Bazen bir verilen ad ve türe sahip birden fazla DNS kaydı toocreate gerekir. Örneğin, hello 'www.contoso.com' web sitesinin iki farklı IP adresinde barındırıldığını var sayalım. Merhaba Web sitesi iki farklı A kayıtları, her IP adresi için bir tane gerektirir. Bu bir kayıt kümesi örneğidir:

    www.contoso.com.        3600    IN    A    134.170.185.46
    www.contoso.com.        3600    IN    A    134.170.188.221

Azure DNS tüm DNS kayıtlarını *kayıt kümeleri* kullanarak yönetir. Kayıt kümesi (olarak da bilinen bir *kaynak* kayıt kümesine) hello koleksiyonu aynı ad ve hello olan hello olan DNS kayıtlarının bir bölgede aynı türde. Çoğu kayıt kümesinde tek bir kayıt bulunur. Ancak, örnekleri yukarıda hello gibi bir kayıt kümesinde birden fazla kayıt içeriyor, seyrek değildir.

Örneğin, "contoso.com" Merhaba bölgesinde bir A kaydı 'www' önceden oluşturulmuş varsayalım toohello IP işaret eden adres '134.170.185.46' (Merhaba ilk kaydı yukarıdaki).  toohello mevcut kaydıyla, eklediğiniz toocreate hello ikinci kaydı ayarlamak yerine ek bir kayıt kümesini oluşturun.

Merhaba SOA ve CNAME kayıt türü durumlardır. Merhaba DNS standartlarında hello bu türleri için aynı ad ile birden çok kayıt izin vermez, bu nedenle bu kaydı kümeleri tek bir kayıt yalnızca içerebilir.

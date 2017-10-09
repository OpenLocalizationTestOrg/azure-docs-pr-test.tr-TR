Bir DNS bölgesi belirli bir etki alanı için kullanılan toohost hello DNS kayıtlarını ' dir. Azure DNS, etki alanınızda barındırma toostart toocreate bir DNS bölgesi için o etki alanı adı gerekiyor. Ardından bu DNS bölgesinde etki alanınız için tüm DNS kayıtları oluşturulur.

Örneğin, contoso.com' hello etki alanı' 'mail.contoso.com"(bir posta sunucusu) ve 'www.contoso.com' (bir web sitesi) gibi birçok DNS kayıtlarını içerebilir.

Azure DNS'de bir DNS bölgesi oluştururken:

* Merhaba bölgenin Hello adı hello kaynak grubun içinde benzersiz olmalıdır ve hello bölgesi zaten mevcut olmamalıdır. Aksi takdirde hello işlemi başarısız olur.
* Merhaba aynı bölge adı farklı bir kaynak grubunda veya farklı bir Azure aboneliğinde yeniden kullanılabilir.
* Burada birden çok bölgenin paylaşmak hello aynı adı her örnek farklı ad sunucusu adreslerini atanır. Yalnızca bir adresleri kümesini hello etki alanı adı kayıt ile yapılandırılabilir.

> [!NOTE]
> Bir etki alanı adı toocreate bu etki alanı adı ile bir DNS bölgesi durum Azure DNS'de tooown gerekmez. Ancak, tooown hello etki alanı tooconfigure hello Azure DNS ad sunucuları hello etki alanı adı kayıt hello etki alanı adı için doğru ad sunucularını hello gibi gerekir.
> 
> Daha fazla bilgi için bkz: [bir etki alanı tooAzure DNS temsilci](../articles/dns/dns-domain-delegation.md).

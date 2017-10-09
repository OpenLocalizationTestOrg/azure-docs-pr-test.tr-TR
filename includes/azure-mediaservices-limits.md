>[!NOTE]
>Sabitlenmemiş kaynaklar için yükseltilmiş bir destek bileti açılarak hello kotaları toobe isteyebilir. Yapmak **değil** ek Azure Media Services hesap tooobtain daha yüksek sınırları içinde girişiminde oluşturun.

| Kaynak | Varsayılan Sınır | 
| --- | --- | 
| Tek bir abonelikte Azure Media Services (AMS) hesabı sayısı | 25 (sabit) |
| AMS hesabı başına Medya Ayrılmış Birimleri (RU’lar) |25 (S1, S2)<br/>10 (S3) <sup>(1)</sup> | 
| AMS hesabı başına iş sayısı | 50,000<sup>(2)</sup> |
| İş başına zincirleme görev sayısı | 30 (sabit) |
| AMS hesabı başına varlık sayısı | 1.000.000|
| Görev başına varlık sayısı | 50 |
| İş başına varlık sayısı | 100 |
| Tek seferde bir varlıkla ilişkilendirilen benzersiz bulucu sayısı | 5<sup>(4)</sup> |
| AMS hesabı başına canlı kanal sayısı |5|
| Kanal başına durdurulmuş durumdaki program sayısı |50|
| Kanal başına çalışır durumdaki program sayısı |3|
| AMS hesabı başına çalışır durumdaki akış uç noktaları|2|
| Akış uç noktası başına akış birimleri |10 |
| Depolama hesapları | 1,000<sup>(5)</sup> (sabit) |
| İlkeler | 1,000,000<sup>(6)</sup> |
| Dosya boyutu| Bazı senaryolarda hello en büyük dosya boyutu Media Services işlemek için desteklenen bir sınırı yoktur. <sup>7</sup> |
  
<sup>1</sup> S3 RU’ları Hindistan Batı bölgesinde kullanılamaz. Merhaba müşteri hello türünden (örneğin, S2 tooS1) değişirse hello max RU sınırları sıfırlama. 

<sup>2</sup> Bu sayı kuyruğa alınan, tamamlanan, etkin ve iptal edilmiş işleri içerir. Silinmiş işleri içermez. Merhaba eski işleri kullanarak silebilirsiniz **IJob.Delete** veya hello **silmek** HTTP isteği.

Merhaba toplam kayıt sayısı hello en yüksek kota altında olsa bile 1 Nisan 2017 başlangıç 90 günden daha eski hesabınızda herhangi bir işi kaydının otomatik olarak, ilişkili görev kayıtlarını yanı sıra, silinir. Tooarchive hello iş/görevi bilgiye ihtiyacınız varsa, açıklanan hello kodu kullanabilirsiniz [burada](../articles/media-services/media-services-dotnet-manage-entities.md).

<sup>3</sup> bir isteği toolist iş varlıkları yapılırken, istek başına en çok 1.000 döndürülür. Tookeep izini gerekiyorsa tüm işleri gönderildi, üst/Atla açıklandığı gibi kullanabilirsiniz [OData sorgu seçeneklerinin](http://msdn.microsoft.com/library/gg309461.aspx).

<sup>4</sup> Bulucular kullanıcı başına erişim denetimini yönetmek için tasarlanmamıştır. toogive farklı erişim hakları tooindividual kullanıcılar, dijital hak yönetimi (DRM) çözümleri kullanın. Daha fazla bilgi için [bu](../articles/media-services/media-services-content-protection-overview.md) bölüme bakın.

<sup>5</sup> hello depolama hesapları, hello olmalıdır aynı Azure aboneliği.

<sup>6</sup> Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu politikası veya ContentKeyAuthorizationPolicy için). 

>[!NOTE]
> Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini / vb.. Bilgi ve bir örnek için [bu](../articles/media-services/media-services-dotnet-manage-entities.md#limit-access-policies) bölüme bakın.

<sup>7</sup>, yüklüyorsanız içerik tooan Azure Media varlığı ile Merhaba hedefi tooprocess hizmetimizi hello medya işlemciler biri ile hizmet (yani kodlayıcılar ister Medya Kodlayıcısı standart ve Medya Kodlayıcısı Premium iş akışı veya Analiz altyapıları gibi yüz algılayıcısı), ardından hello en büyük boyutu hello kısıtlaması bilmeniz. 

15 Mayıs 2017'dan sonra için tek bir blob desteklenen hello en büyük boyutu 195 TB - bu sınırından dosya largers ile görev başarısız olur. Bu sınırı bir düzeltme tooaddress çalışıyoruz. Ayrıca, en büyük boyutu hello hello hello kısıtlaması varlık gibidir.

| Medya Ayrılmış Birimi türü | En büyük giriş boyutu (GB)| 
| --- | --- | 
|S1 | 325|
|S2 | 640|
|S3 | 260|

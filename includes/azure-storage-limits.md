| Kaynak | Varsayılan Sınır |
| --- | --- |
| Abonelik başına depolama hesabı sayısı |200<sup>1</sup> |
| En fazla depolama hesabı kapasitesi |500 TB<sup>2</sup> |
| En fazla blob kapsayıcıları, BLOB'lar, dosya paylaşımları, tablolar, kuyruklar, varlık veya depolama hesabı başına ileti sayısı |Sınırsız |
| Tek blob kapsayıcısı, tablo veya kuyruğu en büyük boyutu |En fazla depolama hesabı kapasitesi aynı |
| Bir blok blobu blok sayısını maks. veya blob Ekle |50,000 |
| Bir blok blobu bloğunda en büyük boyutu |100 MB |
| Bir blok blobu en büyük boyutu |50.000 x 100 MB (yaklaşık 4.75 TB) |
| Bir ek blobu bloğunda en büyük boyutu |4 MB |
| Bir ek blobunun en büyük boyutu |50.000 x 4 MB (yaklaşık 195 GB) |
| Bir sayfa blob'u en büyük boyutu |8 TB |
| Tablo varlığı en büyük boyutu |1 MB |
| Tablo varlığı özelliklerinde sayısı üst sınırı |252 |
| Bir kuyruk iletinin en büyük boyutu |64 KB |
| Bir dosya paylaşımı en büyük boyutu |5 TB |
| Bir dosya paylaşımı bir dosyada en büyük boyutu |1 TB |
| Bir dosya paylaşımında dosyalar sayısı üst sınırı |Merhaba 5 TB toplam kapasiteye hello dosya paylaşımının yalnızca sınır: |
| Paylaşım başına maksimum IOPS |1000 |
| Bir dosya paylaşımında dosyalar sayısı üst sınırı |Merhaba 5 TB toplam kapasiteye hello dosya paylaşımının yalnızca sınır: |
| Kapsayıcı, dosya paylaşımı, tablo veya kuyruğu başına depolanmış erişim ilkeleri sayısı üst sınırı |5 |
| Depolama hesabı başına en fazla istek oranı |BLOB'lar: saniye başına 20.000 istek<sup>2</sup> (yalnızca hello hesabın giriş/çıkış sınırları tarafından tutulabilir) herhangi bir geçerli boyuttaki BLOB'lar için <br />Dosyalar: dosya paylaşımı başına IOPS (8 KB boyutunda) 1000 <br />Kuyruklar: 20.000 ileti / saniye (1 KB ileti boyutu olduğunu varsayarak)<br />Tablolar: 20.000 işlemleri / saniye (1 KB varlık boyutu olduğunu varsayarak) |
| Tek blob için hedef işleme |Too60 saniyede MB saniye başına veya too500 yukarı istekleri |
| Tek bir sıraya (1 KB iletileri) için hedef işleme |Saniye başına too2000 iletileri |
| Tek bir tablo bölüm (1 KB varlıklar) için hedef işleme |Saniye başına too2000 varlıklar |
| Tek bir dosya paylaşımı için hedef işleme |Saniye başına too60 MB |
| En fazla giriş<sup>3</sup> her depolama hesabı (BİZE bölgelerde) |10 Gbps GRS/ZRS,<sup>4</sup> etkinse, LRS 20 GB/sn<sup>2</sup> |
| En büyük çıkış<sup>3</sup> her depolama hesabı (BİZE bölgelerde) |RA-GRS/GRS/ZRS ise 20 GB/sn<sup>4</sup> etkinse, LRS için 30 GB/sn<sup>2</sup> |
| En fazla giriş<sup>3</sup> her depolama hesabı (ABD olmayan bölgeleri için) |GRS/ZRS, 5 GB/sn<sup>4</sup> etkinse, LRS için 10 GB/sn<sup>2</sup> |
| En büyük çıkış<sup>3</sup> her depolama hesabı (ABD olmayan bölgeleri için) |10 Gbps RA-GRS/GRS/ZRS,<sup>4</sup> etkinse, LRS 15 GB/sn<sup>2</sup> |

<sup>1</sup>bu standart ve Premium depolama hesaplarını içerir. 200'den fazla depolama hesabı gerekiyorsa, [Azure Destek](https://azure.microsoft.com/support/faq/) üzerinden bir istek oluşturun. Hello Azure depolama ekibi iş durumunuz incelenecek ve too250 depolama hesapları onaylama. 

<sup>2</sup> tooget standart depolama hesapları toogrow geçmiş Merhaba kapasite, giriş/çıkış ve istek oranı tanıtılan sınırları, lütfen aracılığıyla bir istekte [Azure Destek](https://azure.microsoft.com/support/faq/). Hello Azure depolama ekibi hello isteği incelenecek ve olay temelinde daha yüksek sınırları onaylama.

<sup>3</sup>*giriş* tooa depolama hesabı gönderilen tooall veriler (istek) başvuruyor. *Çıkış* tooall veri depolama hesabından alınan (yanıtları) başvuruyor.  

<sup>4</sup>azure depolama çoğaltma seçenekleri:
* **RA-GRS**: coğrafi olarak yedekli depolamaya okuma erişimi. RA-GRS etkinleştirilirse, çıkış hedefleri hello ikincil konum aynı toothose hello birincil konum için ' dir.
* **GRS**: coğrafi olarak yedekli depolama. 
* **ZRS**: bölge olarak yedekli depolama. Yalnızca blok bloblar için kullanılabilir. 
* **LRS**: yerel olarak yedekli depolama. 



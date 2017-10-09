<!--author=alkohli last changed: 12/15/15-->

| Sınır tanımlayıcı | Sınır | Yorumlar |
| --- | --- | --- |
| Depolama hesabının kimlik bilgilerini maksimum sayısı |64 | |
| Birim kapsayıcıları maksimum sayısı |64 | |
| En fazla sayıda birime |255 | |
| Zamanlamalar bant genişliği şablonu başına maksimum sayısı |168 |Her gün (24 * 7) hello haftanın her saat için bir zamanlama. |
| Katmanlı birim fiziksel aygıtlarda en büyük boyutu |8100 ve 8600 64 TB |8100 ve 8600 fiziksel aygıtlardır. |
| Azure'da sanal cihazlarda katmanlı birim en büyük boyutu |8010 30 TB <br></br> 8020 için 64 TB |8010 hem de 8020 sırasıyla standart depolama ve Premium depolama kullanan sanal Azure aygıtlardır. |
| Fiziksel cihazları yerel olarak sabitlenmiş bir birimde en büyük boyutu |8100 9 TB <br></br> 8600 24 TB |8100 ve 8600 fiziksel aygıtlardır. |
| İSCSI bağlantısı sayısı |512 | |
| İSCSI başlatıcıları bağlantılarından maksimum sayısı |512 | |
| Erişim denetimi kayıtları aygıt başına maksimum sayısı |64 | |
| En fazla sayıda birime yedekleme İlkesi başına |24 | |
| Yedekleme İlkesi korunur yedeklemeleri sayısı |64 | |
| Zamanlamalar yedekleme İlkesi başına maksimum sayısı |10 | |
| Maksimum sayıda anlık görüntü birim başına korunabilir herhangi bir türde |256 |Bu yerel anlık görüntülerini içerir ve bulut anlık görüntüleri. |
| Maksimum sayıda içinde herhangi bir cihazda mevcut olabilecek anlık görüntü |10,000 | |
| En fazla sayıda paralel yedekleme, geri yükleme için işlenen ya da kopyalama birime |16 |<ul><li>16'dan fazla birim varsa, bunlar işleme yuvaları kullanılabilir duruma geldiğinde sıralı olarak işlenir.</li><li>Merhaba işlemi tamamlanana kadar bir kopyalanan yeni yedeklerini veya geri yüklenen bir katmanlı birim oluşamaz. Ancak, yerel bir birim için Hello birim çevrimiçi olduktan sonra yedeklemeler izin verilir.</li></ul> |
| Geri yükleme ve kurtarma zamanı katmanlı birimler için kopyalama |< 2 dakika |<ul><li>Merhaba birim boyutu bağımsız olarak, geri yükleme veya kopyalama işleminin 2 dakika içinde Hello birim kullanılabilir hale getirilir.</li><li>Merhaba birim performans başlangıçta hello veri ve meta veri çoğunu hala yer aldığı hello bulutta normalden daha yavaş olabilir. Merhaba bulut toohello StorSimple aygıttan veri akışları olarak performansı artırabilir.</li><li>Merhaba toplam süre toodownload meta veriler üzerinde birim boyutu ayrılmış hello bağlıdır. Meta verileri otomatik olarak ayrılmış birim verilerini TB başına 5 dakika hello hızında hello arka planda hello aygıt halinde duruma getirilir. Bu oran Internet bant genişliği toohello bulut tarafından etkilenebilir.</li><li>geri yükleme hello veya tüm hello meta veriler hello aygıtta olduğunda kopyalama işlemi tamamlanmış demektir.</li><li>Kopya işlemi tam olarak tamamlandıktan veya yedekleme işlemleri kadar hello geri yükleme gerçekleştirilemez. |
| Yerel olarak sabitlenmiş birimler için kurtarma süresi geri yükleme |< 2 dakika |<ul><li>Merhaba birim boyutu bakılmaksızın hello geri yükleme işleminin 2 dakika içinde Hello birim kullanılabilir hale getirilir.</li><li>Merhaba birim performans başlangıçta hello veri ve meta veri çoğunu hala yer aldığı hello bulutta normalden daha yavaş olabilir. Merhaba bulut toohello StorSimple aygıttan veri akışları olarak performansı artırabilir.</li><li>Merhaba toplam süre toodownload meta veriler üzerinde birim boyutu ayrılmış hello bağlıdır. Meta verileri otomatik olarak ayrılmış birim verilerini TB başına 5 dakika hello hızında hello arka planda hello aygıt halinde duruma getirilir. Bu oran Internet bant genişliği toohello bulut tarafından etkilenebilir.</li><li>Yerel olarak sabitlenmiş birimlerin hello durumda katmanlı birimlerin farklı hello birim verilerini de yerel olarak hello aygıtta indirilir. Tüm hello birim verilerini duruma zaman toohello aygıt hello geri yükleme işlemi tamamlanır.</li><li>Merhaba geri yükleme işlemleri uzun olabilir ve sağlanan hello yerel birim, Internet bant genişliği ve veri hello cihazda mevcut hello hello boyutu hello toplam süre toocomplete hello geri yükleme bağlıdır. Merhaba geri yükleme işlemi devam ederken hello yerel olarak sabitlenmiş birim üzerindeki yedekleme işlemlerine izin verilir. |
| Kullanılabilirlik ince-geri yükle |Son yük devretme | |
| (Merhaba SSD katmanından sunulduğunda) en fazla istemci okuma/yazma verimlilik * |920/720 MB/s ile tek bir 10GbE ağ arabirimi |MPIO ve iki ağ arabirimi ile too2x. |
| (Merhaba HDD Katmanı'ndan sunulduğunda) en fazla istemci okuma/yazma verimlilik * |120/250 MB/s | |
| (Merhaba bulut Katmanı'ndan sunulduğunda) en fazla istemci okuma/yazma verimlilik * |11/41 MB/s |Okuma üretilen işi oluşturmak ve yeterli g/ç sıra derinliğini koruyarak istemcilerde bağlıdır. |

&#42; G/ç türü başına en fazla üretilen iş yüzde 100 okuma ve yüzde 100 yazma senaryoları ile ölçülen. Gerçek verimlilik daha düşük olabilir ve g/ç üzerinde bağlı karışımı ve ağ koşulları.


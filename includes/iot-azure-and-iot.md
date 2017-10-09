
# <a name="azure-and-internet-of-things"></a>Azure ve Nesnelerin İnterneti

Nesnelerin interneti (IOT) hello ve tooMicrosoft Azure Hoş Geldiniz. Bu makalede hello Azure hizmetlerini kullanarak dağıtabileceğiniz IOT çözümünün genel özelliklerini açıklayan bir IOT çözüm mimarisi tanıtılmaktadır. IOT çözümleri güvenli, büyük olasılıkla hello milyonlarca ve çözüm arka ucu olabilen cihazlar arasında iki yönlü iletişim gerektirir. Örneğin, bir çözüm arka ucu, cihaz-bulut olay akışının otomatik, Tahmine dayalı analizleri toouncover Öngörüler kullanabilirsiniz.

Azure IoT Hub’ı, Azure hizmetlerini kullanarak bu IoT çözüm mimarisini uyguladığınızda önemli bir yapı taşıdır. IoT Paketi, belirli IoT senaryoları için bu mimarinin eksiksiz, uçtan uca uygulamalarını sağlar. Örneğin:

* Merhaba *Uzaktan izleme* çözüm toomonitor hello satış makineleri gibi cihazların durumunu sağlar.
* Merhaba *Tahmine dayalı Bakım* çözüm yardımcı olan uzak pompa istasyonlarındaki ve tooavoid zamanlanmamış kapalı kalma süresi Pompalar gibi cihazların bakım gereksinimlerini tooanticipate.
* Merhaba *bağlı Fabrika* çözüm endüstriyel aygıtlarınızı izlemek ve tooconnect yardımcı olur.

## <a name="iot-solution-architecture"></a>IOT çözüm mimarisi

Tipik bir IOT çözüm mimarisi diyagramı aşağıdaki hello gösterir. Merhaba diyagramı belirli Azure hizmetlerinin hello adlarını dahil değildir, ancak bir genel IOT çözüm mimarisinde hello anahtar öğeleri açıklar. Bu mimaride, IOT cihazları bulut ağ geçidi tooa gönderdikleri veri toplar. Hello bulut ağ geçidi, veri tooother satır iş kolu uygulamaları veya bir Pano veya başka bir sunu cihazıyla toohuman işleçleri burada teslim diğer arka uç hizmetlerin işleme hello verileri için kullanılabilir yapar.

![IOT çözüm mimarisi][img-solution-architecture]

> [!NOTE]
> IOT mimarisinin ayrıntılı incelemesi için bkz: Merhaba [Microsoft Azure IOT başvuru mimarisi][lnk-refarch].

### <a name="device-connectivity"></a>Cihaz bağlantısı

Bu IOT çözüm mimarisinde cihazlar pompa istasyonuna, depolama tooa bulut uç noktasına ait sensör okumaları ve işleme gibi telemetri gönderin. Belirli bir pompanın bakım gerektirdiğinde bir Tahmine dayalı bakım senaryosunda, algılayıcı verileri toodetermine hello akışı hello çözüm arka ucu kullanabilir. Cihazları da alabilir ve bulut uç noktasına ait iletileri okuyarak toocloud aygıt iletilerine yanıt. Örneğin, hello Tahmine dayalı bakım senaryo hello çözümde arka uç iletileri tooother Pompalar yalnızca bakım önce akışları yeniden yönlendirilmesine istasyon toobegin Pompalama hello gönderebilir toostart. Bu yordamı aynen ulaşır ulaşmaz hello bakım mühendisinin başladığından emin olunmasını sağlar.

IOT projelerinin karşılaştığı hello en büyük zorluklardan biri nasıl tooreliably ve güvenli bir şekilde aygıtları toohello çözüm arka ucu bağlanın. IOT cihazları karşılaştırılan tooother istemcileri tarayıcılar ve mobil uygulamalar gibi farklı özelliklere sahip. IoT cihazları:

* İnsan olan bir operatörü bulunmayan ve genellikle katıştırılmış sistemlerdir.
* Fiziksel erişimin pahalı olduğu uzak konumlarda dağıtılabilir.
* Yalnızca hello çözüm arka ucu aracılığıyla erişilebilir. Herhangi bir şekilde toointeract hello aygıtla yoktur.
* Sınırlı güç ve işleme kaynaklarına sahip olabilir.
* Aralıklı, yavaş veya pahalı bir ağ bağlantısına sahip olabilir.
* Toouse mülkiyete ait, özel veya sektöre özgü uygulama protokolleri gerekebilir.
* Büyük bir popüler donanım ve yazılım platformu kümesi kullanılarak oluşturulabilir.

Ayrıca yukarıdaki toohello gereksinimler, tüm IOT çözümlerinin de ölçek, güvenlik ve güvenilirlik de sunması gerekir. Merhaba elde edilen bağlantı gereksinimleri web kapsayıcıları gibi geleneksel teknolojiler kullanarak ve mesajlaşma aracıları zor ve zaman alıcı tooimplement kümesidir. Azure IOT Hub ve hello Azure IOT cihaz SDK'ları bu gereksinimleri karşılayan daha kolay tooimplement çözümleri olun.

Bir cihaz doğrudan bir bulut ağ geçidi uç noktasıyla iletişim kurabilir veya hello cihaz bulut ağ geçidi destekler hello hello iletişim protokollerinin hiçbirini kullanamıyorsanız, bir ara ağ geçidiyle bağlanabilir. Örneğin, hello [Azure IOT protokolü ağ geçidini] [ lnk-protocol-gateway] cihazlar IOT hub'ı destekleyen hello protokolleri hiçbirini kullanamıyorsanız protokol çevirisi gerçekleştirebilirsiniz.

### <a name="data-processing-and-analytics"></a>Veri işleme ve analizi

Merhaba bulutta bir IOT çözüm arka ucu burada hello veri işleme çoğunu, filtreleme ve telemetri toplama ve yönlendirme tooother Hizmetleri gibi gerçekleşir. Merhaba IOT çözüm arka ucu:

* Cihazlarınızdan ölçekli telemetri alır ve belirler nasıl tooprocess ve bu verileri depolar. 
* Toosend komutları hello bulut toospecific aygıttan sağlayabilir.
* Tooprovision cihazları ve hangi cihazların tooconnect tooyour altyapı izin verilen toocontrol sağlayan cihaz kaydı özellikler sağlar.
* Tootrack cihazlarınızın durumunu hello ve bunların etkinliklerini izlemenize olanak tanır.

Merhaba Tahmine dayalı bakım senaryosunda hello çözüm arka ucu geçmiş telemetri verilerini depolar. Merhaba çözüm arka ucu belirli bir pompada Bakım olan belirtmek bu verileri toouse tooidentify kalıplar kullanabilirsiniz.

IOT çözümlerinde otomatik geri bildirim döngüleri bulunabilir. Örneğin, belirli bir cihazdaki hello sıcaklık normal çalışma seviyesinin üzerinde olduğunu telemetri gelen hello çözüm arka uçtaki analitik bir modül tanımlayabilirsiniz. Merhaba çözüm sonra tootake düzeltme eylemi söyleyen bir komut toohello aygıt gönderebilir.

### <a name="presentation-and-business-connectivity"></a>Sunu ve iş bağlantısı

Merhaba sunu ve iş bağlantı katmanı son kullanıcıların hello IOT çözüm ile toointeract ve hello aygıtları sağlar. Kullanıcıların tooview sağlar ve cihazlarından toplanan hello verileri analiz edin. Bu görünümler panolar veya hem geçmiş verileri görüntüleyebilen BI raporları veya yakın gerçek zamanlı verileri hello form alabilir. Örneğin, bir işleç belirli pompa istasyonunun hello durumunu denetleyin ve hello sistem tarafından gerçekleştirilen tüm uyarıları görebilir. Bu katman de hello IOT çözümü arka ucu mevcut iş kolu satır uygulamaları tootie ile tümleştirme kurumsal iş süreçlerine veya iş akışları sağlar. Merhaba çözüm bir pompaya bakım gerekli belirlediğinde, örneğin, hello Tahmine dayalı bakım çözümü bir zamanlama sistemiyle o books mühendislik toovisit pompa istasyonuna tümleştirebilirsiniz.

![IoT çözüm panosu][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf

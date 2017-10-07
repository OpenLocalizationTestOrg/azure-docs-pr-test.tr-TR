---
title: "aaaAzure depolama performans ve ölçeklenebilirlik Yapılacaklar listesi | Microsoft Docs"
description: "Azure Storage ile kullanıcı uygulamaları geliştirme kullanılmak kanıtlanmış yöntemleri listesi."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 959d831b-a4fd-4634-a646-0d2c0c462ef8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c0cd77da4a1abda42c018255ed93215b71f4fad8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-performance-and-scalability-checklist"></a>Microsoft Azure Depolama Performansı ve Ölçeklenebilirlik Onay Listesi
## <a name="overview"></a>Genel Bakış
Merhaba sürümü hello Microsoft Azure depolama hizmetleri, bu yana Microsoft bu hizmetleri bir kullanıcı şekilde kullanmak için kanıtlanmış uygulamalar sayısı geliştirmiştir ve bu makalede tooconsolidate hello bunlardan en önemli bir denetim listesi stili listesine sunar. Bu makalede Hello amacı, Azure Storage ve benimsemeyi düşünmelisiniz kanıtlanmış diğer yöntemler tanımak toohelp kanıtlanmış yöntemleri kullandıkları toohelp uygulama geliştiricileri doğrulayın ' dir. Bu makalede, her olası performans ve ölçeklenebilirlik iyileştirme toocover denemez — etkilerini küçük veya geniş çapta geçerli olanlar hariç tutar. uygulamanın davranışını hello toohello ölçüde tahmin tasarım sırasında bu sorun önceden yararlı tookeep olmasından performans sorunlarla çalışacak tooavoid tasarımları.  

Azure Storage kullanarak her uygulama geliştiricisi hello zaman tooread bu makalede ele ve kendi uygulama her biri aşağıda listelenen uygulamalar kanıtlanmış hello izlediğini denetleyin gerekir.  

## <a name="checklist"></a>Denetim listesi
Bu makalede kanıtlanmış hello yöntemler grupları aşağıdaki hello düzenler. Kanıtlanmış yöntemleri için geçerlidir:  

* Tüm Azure Storage Hizmetleri (BLOB'lar, tablolar, kuyruklar ve dosyaları)
* Bloblar
* Tablolar
* Kuyruklar  

| Bitti | Alan | Kategori | Soru |
| --- | --- | --- | --- |
| &nbsp; | Tüm Hizmetler |Ölçeklenebilirlik hedefleri |[Tasarlanmış uygulama tooavoid hello ölçeklenebilirlik hedefleri yaklaşıyor?](#subheading1) |
| &nbsp; | Tüm Hizmetler |Ölçeklenebilirlik hedefleri |[Adlandırma kuralı tasarlanmış tooenable daha iyi Yük Dengeleme mi?](#subheading47) |
| &nbsp; | Tüm Hizmetler |Ağ |[İstemci tarafı aygıtları yeterince yüksek bant genişliği ve düşük gecikme süresi tooachieve hello performans gerekli var mı?](#subheading2) |
| &nbsp; | Tüm Hizmetler |Ağ |[İstemci tarafı aygıtları yeterince yüksek kaliteli bağlantı var mı?](#subheading3) |
| &nbsp; | Tüm Hizmetler |Ağ |[Merhaba istemci uygulaması "yakın" Merhaba depolama hesabı bulunuyor?](#subheading4) |
| &nbsp; | Tüm Hizmetler |İçerik Dağıtımı |[İçerik dağıtımı için bir CDN kullanıyor musunuz?](#subheading5) |
| &nbsp; | Tüm Hizmetler |Doğrudan istemci erişimi |[Proxy yerine SAS ve CORS tooallow doğrudan erişim toostorage kullanıyor musunuz?](#subheading6) |
| &nbsp; | Tüm Hizmetler |Önbelleğe alma |[Sürekli olarak kullanılan uygulama verileri önbelleğe alma ve değişiklikleri nadiren mi?](#subheading7) |
| &nbsp; | Tüm Hizmetler |Önbelleğe alma |[Uygulamanız (istemci tarafında önbelleğe alma ve daha büyük kümeleri karşıya) güncelleştirmeleri yığınlama?](#subheading8) |
| &nbsp; | Tüm Hizmetler |.NET yapılandırması |[İstemci toouse yeterli sayıda eşzamanlı bağlantı yapılandırdınız mı?](#subheading9) |
| &nbsp; | Tüm Hizmetler |.NET yapılandırması |[.NET toouse iş parçacığı yeterli sayıda yapılandırdınız mı?](#subheading10) |
| &nbsp; | Tüm Hizmetler |.NET yapılandırması |[.NET 4.5 kullanıyor veya daha sonra hangi çöp toplama geliştirilmiştir?](#subheading11) |
| &nbsp; | Tüm Hizmetler |Paralellik |[Böylece, istemci özelliklerini veya hello ölçeklenebilirlik hedefleri aşırı yükleme yok paralellik uygun şekilde sınırlıdır sağlamış olursunuz?](#subheading12) |
| &nbsp; | Tüm Hizmetler |Araçlar |[Microsoft en son sürümünü hello kullanarak istemci kitaplıkları ve araçlar sağlanır?](#subheading13) |
| &nbsp; | Tüm Hizmetler |Yeniden deneme sayısı |[Üstel geri alma kullanarak yeniden deneme ilkesi hataları ve zaman aşımlarına azaltma için misiniz?](#subheading14) |
| &nbsp; | Tüm Hizmetler |Yeniden deneme sayısı |[Uygulama kaçınarak yeniden deneme denenemeyen hataları mı?](#subheading15) |
| &nbsp; | Bloblar |Ölçeklenebilirlik hedefleri |[Çok sayıda istemci aynı anda tek bir nesne erişimi var mı?](#subheading46) |
| &nbsp; | Bloblar |Ölçeklenebilirlik hedefleri |[Uygulamanızın tek bir blob hello bant genişliği veya işlemleri ölçeklenebilirlik hedef içinde kaldığını?](#subheading16) |
| &nbsp; | Bloblar |BLOB kopyalama |[Kopyalama BLOB'lar verimli bir şekilde misiniz?](#subheading17) |
| &nbsp; | Bloblar |BLOB kopyalama |[BLOB'lar için toplu kopyalarını AzCopy kullanıyor musunuz?](#subheading18) |
| &nbsp; | Bloblar |BLOB kopyalama |[Azure içeri/dışarı aktarma tootransfer çok büyük miktarda veriyi kullanıyor musunuz?](#subheading19) |
| &nbsp; | Bloblar |Meta veri kullanın |[BLOB'ları hakkında sık kullanılan meta verileri, meta verilerde depoluyorsanız?](#subheading20) |
| &nbsp; | Bloblar |Hızlı yükleme |[Tooupload bir blob hızla çalışırken blokları paralel karşıya yükleniyor?](#subheading21) |
| &nbsp; | Bloblar |Hızlı yükleme |[Tooupload çok sayıda BLOB'ları kolayca çalışırken, BLOB'ları paralel karşıya yükleniyor?](#subheading22) |
| &nbsp; | Bloblar |Doğru Blob türü |[Sayfa bloblarını veya blok blobları uygun olduğunda kullanıyor?](#subheading23) |
| &nbsp; | Tablolar |Ölçeklenebilirlik hedefleri |[Saniye başına varlıklar için yaklaşan hello ölçeklenebilirlik hedefleri misiniz?](#subheading24) |
| &nbsp; | Tablolar |Yapılandırma |[JSON tablosu isteklerinizi kullanıyor musunuz?](#subheading25) |
| &nbsp; | Tablolar |Yapılandırma |[Nagle tooimprove hello performansını küçük istekleri devre dışı bırakmış?](#subheading26) |
| &nbsp; | Tablolar |Tabloları ve bölümleri |[Verilerinizi düzgün bir şekilde bölümlenmiş mi?](#subheading27) |
| &nbsp; | Tablolar |Sık kullanılan bölümleri |[Yalnızca ekleme ve yalnızca başına desenleri önleme?](#subheading28) |
| &nbsp; | Tablolar |Sık kullanılan bölümleri |[Ekleme/güncelleştirme birçok bölüm arasında yayılır mı?](#subheading29) |
| &nbsp; | Tablolar |Sorgu kapsamı |[Çoğu durumda ve olabildiğince az kullanılan tablo sorguları toobe kullanılan noktası sorguları toobe için şema tooallow tasarladığınız?](#subheading30) |
| &nbsp; | Tablolar |Sorgu yoğunluğu |[Uygulamanız kullanacak satırları döndürür ve sorguları genellikle yalnızca taramanız musunuz?](#subheading31) |
| &nbsp; | Tablolar |Sınırlama döndürülen veri |[Gerekli olmayan filtreleme tooavoid döndürmeyi varlıklar kullanıyor musunuz?](#subheading32) |
| &nbsp; | Tablolar |Sınırlama döndürülen veri |[Gerekli olmayan özellikler döndüren projeksiyon tooavoid kullanıyor musunuz?](#subheading33) |
| &nbsp; | Tablolar |Denormalization |[Tooget veri çalışırken Verimsiz sorgulara veya birden çok okuma isteklerinin kaçının, verilerinizi normal dışı mi?](#subheading34) |
| &nbsp; | Tablolar |Ekleme/güncelleştirme/silme |[Toobe işlem gerekir veya aynı hello yapılabilir istekleri toplu işleme süresi tooreduce gidiş dönüş?](#subheading35) |
| &nbsp; | Tablolar |Ekleme/güncelleştirme/silme |[Bir varlık yalnızca toodetermine alma önleme toocall ekleme veya güncelleştirme?](#subheading36) |
| &nbsp; | Tablolar |Ekleme/güncelleştirme/silme |[Sık alınır veri serisi birden çok varlık yerine özellikleri olarak tek bir varlık birlikte depolama göz önünde bulundurduğunuzdan?](#subheading37) |
| &nbsp; | Tablolar |Ekleme/güncelleştirme/silme |[Her zaman birlikte alınır ve toplu (örn. zaman serisi veri) yazılabilir varlıklar için BLOB tabloları yerine kullanarak göz önünde bulundurduğunuzdan?](#subheading38) |
| &nbsp; | Kuyruklar |Ölçeklenebilirlik hedefleri |[Saniye başına ileti için yaklaşan hello ölçeklenebilirlik hedefleri misiniz?](#subheading39) |
| &nbsp; | Kuyruklar |Yapılandırma |[Nagle tooimprove hello performansını küçük istekleri devre dışı bırakmış?](#subheading40) |
| &nbsp; | Kuyruklar |İleti Boyutu |[İletilerinizi compact tooimprove hello performans hello sırasının misiniz?](#subheading41) |
| &nbsp; | Kuyruklar |Toplu alma |[Tek bir işlemde "Get" birden çok ileti alma?](#subheading42) |
| &nbsp; | Kuyruklar |Yoklama sıklığı |[Sık gecikme, uygulamanızın algılanan yeterli tooreduce hello yoklama?](#subheading43) |
| &nbsp; | Kuyruklar |Güncelleştirme iletisi |[Bir hata oluşursa tooreprocess hello tüm ileti sahip önleme UpdateMessage toostore ilerleme iletilerini işleme kullanıyor musunuz?](#subheading44) |
| &nbsp; | Kuyruklar |Mimari |[Uzun süre çalışan iş yükleri hello kritik yol ve ölçek dışında sonra bağımsız olarak tutarak daha ölçeklenebilir, tüm uygulama sıraları toomake kullanıyor musunuz?](#subheading45) |

## <a name="allservices"></a>Tüm hizmetler
Bu bölümde geçerli toohello kullanımını hello Azure depolama hizmetleri (BLOB, tablo, kuyruk veya dosyaları) olan kanıtlanmış yöntemler listelenmiştir.  

### <a name="subheading1"></a>Ölçeklenebilirlik hedefleri
Hello Azure Depolama hizmetlerinin her biri, Kapasite (GB), işlem hızını ve bant genişliği için ölçeklenebilirlik hedefleri vardır. Uygulamanızı yaklaşıyor veya hello ölçeklenebilirlik hedefleri hiçbirini aşıyor, artan hareket gecikmeleri veya azaltma karşılaşabilirsiniz. Uygulamanızı bir depolama birimi hizmeti kısıtlar, hello hizmet tooreturn "503 Sunucu meşgul" veya "500 işlem zaman aşımı" hata kodları bazı depolama işlemleri için başlar. Bu bölümde her iki hello genel yaklaşım toodealing ölçeklenebilirlik hedefleri ve bant genişliği ölçeklenebilirlik hedefleri ile özellikle anlatılmaktadır. Tek depolama hizmetleri ile ilgili sonraki bölümlerde ölçeklenebilirlik hedefleri belirli hizmetin hello bağlamda açıklanmaktadır:  

* [BLOB bant genişliği ve saniye başına istek sayısı](#subheading16)
* [Saniye başına tablo varlıkları](#subheading24)
* [İletileri / saniye](#subheading39)  

#### <a name="sub1bandwidth"></a>Tüm hizmetler için bant genişliği ölçeklenebilirlik hedefi
Yazma Hello tarihinde hello bant hedefleri hello ABD coğrafi olarak yedekli depolama (GRS) hesabı 10 Gigabit / saniye (Gbps) giriş için olan (veri gönderilen toohello depolama hesabı) ve çıkış (Merhaba depolama hesabından gönderilen veri) için 20 GB/sn. Merhaba sınırları için bir yerel olarak yedekli depolama (LRS) hesabı, daha yüksek – 20 GB/sn giriş ve çıkışı için 30 GB/sn.  Uluslararası bant genişliği sınırlarını daha düşük olabilir ve bulunabilir bizim [ölçeklenebilirlik hedefleri sayfa](http://msdn.microsoft.com/library/azure/dn249410.aspx).  Merhaba bağlantıları hello Depolama artıklık seçenekleri hakkında daha fazla bilgi için bkz: [kullanışlı kaynaklar](#sub1useful) aşağıda.  

#### <a name="what-toodo-when-approaching-a-scalability-target"></a>Ölçeklenebilirlik hedefe yaklaştığını olduğunda hangi toodo
Uygulamanız için tek bir depolama hesabına hello ölçeklenebilirlik hedefleri yaklaşıyorsa hello aşağıdaki yaklaşımlardan birini benimsenmesi göz önünde bulundurun:  

* Uygulama tooapproach neden hello iş yükü alan veya hello ölçeklenebilirlik hedef aşıyor. Farklı toouse daha az bant genişliği veya kapasite ya da daha az işlemleri tasarlayabilirsiniz?
* Bir uygulama hello ölçeklenebilirlik hedefleri birini aşmalıdır, uygulama verilerinizi birden çok depolama hesapları ve bölüm arasında birden çok bu depolama hesabı oluşturmanız gerekir. Bu deseni kullanır, böylece hello Yük Dengeleme için gelecekte daha fazla depolama hesapları ekleyebilirsiniz emin toodesign uygulamanızın olması. Yazıldığı sırada her Azure aboneliği too100 depolama hesapları olabilir.  Depolama hesapları kullanımınızı depolanan veriler, yapılan işlemleri ya da aktarılan verilerin bakımından dışındaki herhangi bir ücret de.
* Uygulamanızı hello bant hedefleri değerse hello istemcisi tooreduce hello gerekli bant genişliği toosend hello veri toohello depolama hizmetinin verileri sıkıştırma göz önünde bulundurun.  Bu bant genişliğinden tasarruf ve ağ performansını iyileştirmeye olsa da, bu da bazı olumsuz etkiler olabileceğini unutmayın.  Merhaba performans etkisini bu sıkıştırma ve veri hello istemcisinde boyutunda toohello ek işleme gereksinimleri nedeniyle değerlendirmelisiniz. Standart araçlar kullanarak daha zor tooview depolanan verileri olabileceği gerçeğidir ek olarak, sıkıştırılmış veri depolama, daha zor tootroubleshoot sorunları yapabilirsiniz.
* Uygulamanızı hello ölçeklenebilirlik hedefleri değerse, ardından yeniden deneme için üstel geri alma kullandığınızdan emin olun (bkz [yeniden deneme](#subheading14)).  Hiçbir zaman (Merhaba yöntemleri yukarıda birini kullanarak) hello ölçeklenebilirlik hedefleri yaklaşımını, ancak bu, uygulamanızın sağlayacak emin, daha iyi toomake olmaz yalnızca tutmak hızlı bir şekilde yeniden deneniyor, daha da kötüsü azaltma hello yapma.  

#### <a name="useful-resources"></a>Yararlı Kaynaklar
bağlantılar aşağıdaki hello ölçeklenebilirlik hedefleri hakkında ek ayrıntılı bilgi sağlar:

* Bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md) ölçeklenebilirlik hedefleri hakkında bilgi için.
* Bkz: [Azure Storage çoğaltma](storage-redundancy.md) ve hello blog gönderisi [Azure Depolama artıklık seçenekleri ve okuma erişimli coğrafi olarak yedekli depolama](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx) Depolama artıklık seçenekleri hakkında bilgi.
* Azure Hizmetleri için fiyatlandırma hakkında güncel bilgiler için bkz: [Azure fiyatlandırma](https://azure.microsoft.com/pricing/overview/).  

### <a name="subheading47"></a>Bölüm adlandırma kuralı
Azure depolama bir aralık tabanlı bölümleme şeması tooscale ve Yük Dengelemesi hello sistemi kullanır. Merhaba bölüm anahtarı aralıkları kullanılan toopartition verisine ve bu aralıklar hello sistem üzerindeki yük dengelemesi. Bu sözcük sıralama (örneğin msftpayroll, msftperformance, msftemployees, vb.) veya zaman damgalarını (log20160101, log20160102, log20160102, vb.) kullanarak gibi adlandırma kuralları kendisini olası hello üzerinde birlikte bulunuyor toohello bölümleri ödünç anlamına gelir. bir yük dengeleme işlemi bunları küçük aralıklarını ayırır kadar aynı bölüm sunucusu. Örneğin, Hello bu BLOB'lar üzerindeki yükü daha fazla hello bölüm aralığı dengelenmesi gerektirir kadar bir kapsayıcıdaki tüm blob'lara tek bir sunucu tarafından sunulabilen. Benzer şekilde, bir grup adlarını sözcük sırayla düzenlenmiş hafifçe yüklü hesaplarıyla tek bir sunucu tarafından hello kadar hizmet edilebilir birinde yüklemek veya bu hesapların tümü toobe bölünmüş birden fazla bölüm sunucusunda şart. Her yük dengeleme işlemi depolama çağrıları hello gecikme hello işlemi sırasında etkileyebilir. trafik tooa bölümünün ani bir veri bloğu işlemi hello dengelemesini kadar sınırlı tarafından tek bölüm sunucusunun hello ölçeklenebilirlik hello sistemin özelliği toohandle kicks bileşenini ve hello bölüm anahtarı aralığının yeniden dengeler.  

Bazı en iyi yöntemler tooreduce hello sıklığını gibi işlemleri izleyebilirsiniz.  

* Merhaba adlandırma kuralı hesapları, kapsayıcıları, BLOB'lar, tablolar ve Kuyruklar, yakından kullanmak inceleyin. Gereksinimlerinize en uygun karma bir işlevi kullanarak 3 basamaklı karma ile hesap adlarını önek göz önünde bulundurun.  
* Zaman damgaları veya sayısal tanımlayıcıları kullanarak verilerinizi düzenlemek, yalnızca ekleme (veya yalnızca başına) trafiği desenlerini kullanmıyorsanız tooensure sahip. Bu düzenleri için bir aralığı uygun olmayan-sistem bölümleme temel ve sağlama tooall hello trafiği giderek tooa tek bölüm ve sınırlama hello sistemden etkili bir şekilde yük dengeleme. Örneğin, günlük varsa yyyyaagg, ardından tüm hello trafiği gibi bir zaman damgası olan günlük işlemi bir blob nesnesi kullanan işlemler tek bölüm sunucusu tarafından sunulan tooa tek nesne yönlendirilmiş. Blob başına hello olup sınırlar adresindeki bakın ve bölüm başına sınırları ihtiyaçlarınızı karşılamak ve gerekirse bu işlemin birden çok BLOB bölmeyi düşünün. Benzer şekilde, zaman serisi veri tabloları saklarsanız tüm hello trafiği olabilir yönlendirilmiş toohello son hello anahtar ad alanının parçası. Zaman damgaları veya sayısal kimlikleri kullanmanız gerekiyorsa hello kimliği 3 basamaklı karma ile ya da zaman damgaları önek hello saniye bölümü ssyyyymmdd gibi hello süreyi hello durumda önek. Listeleme ve işlemleri sorgulama düzenli olarak yapılan sorguları sayısı sınırlar bir karma işlevi belirleyin. Diğer durumlarda, rastgele bir önek yeterli olabilir.  
* Merhaba SOSP belgesi hello Azure Storage'da kullanılan bölümleme hakkında ek bilgi için okuma [burada](http://sigops.org/sosp/sosp11/current/2011-Cascais/printable/11-calder.pdf).

### <a name="networking"></a>Ağ
Konuya Hello API çağrıları olsa da, genellikle hello fiziksel ağ kısıtlamalarını hello uygulamasının bir önemli performansı etkiler. Merhaba aşağıdaki sınırlamalar kullanıcılar karşılaşabilirsiniz bazıları açıklanmaktadır.  

#### <a name="client-network-capability"></a>İstemci ağ özelliği
##### <a name="subheading2"></a>Üretilen iş
Bant genişliği için hello genellikle hello istemci hello yeteneklerini sorunudur. Örneğin, tek bir depolama hesabına 10 GB/sn veya daha fazla giriş işleyebileceği sırasında (bkz [bant genişliği ölçeklenebilirlik hedefleri](#sub1bandwidth)), "Küçük" Azure çalışan rolü örneğinde hello ağ hızı yaklaşık 100 MB/sn özellikli yalnızca. Daha büyük Azure örnekleri NIC'lerin daha büyük kapasitede vardır, yani tek bir makineden daha yüksek ağ sınırları ihtiyacınız varsa daha büyük bir örneği veya daha fazla VM'nin kullanmayı düşünmeniz gerekir. Bir depolama birimi hizmeti üzerinde bir şirket içi uygulamasından erişme sonra hello aynı kural geçerlidir: hello ağ yeteneklerini hello istemci cihazı ve hello ağ bağlantısı toohello Azure depolama konumu anlama ve ya da bunları gerektiği şekilde artırmak veya Uygulama toowork yeteneklerini içinde tasarlayın.  

##### <a name="subheading3"></a>Bağlantı kalitesi
Tüm ağ kullanımı olduğu gibi hataları ve paket kaybı ağ koşulları etkili verimlilik yavaşlatır unutmayın.  WireShark veya NetMon kullanarak bu sorunu tanılamalarına yardımcı olabilir.  

##### <a name="useful-resources"></a>Yararlı Kaynaklar
Sanal makine boyutları ve ayrılan bant hakkında daha fazla bilgi için bkz: [Windows VM boyutları](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [Linux VM boyutları](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

#### <a name="subheading4"></a>Konum
Dağıtılmış bir ortamda hello istemcinin toohello sunucu yakınında yerleştirme hello en iyi performans sunar. Azure Storage hello en düşük gecikme süresi ile erişmek için hello en iyi istemciniz hello konumudur aynı Azure bölgesi. Azure depolama kullanan bir Azure Web sitesi varsa, örneğin, her ikisinin de tek bir bölge içinde (örneğin, ABD Batı'ya da Güneydoğu Asya) bulmanıza. Bu hello gecikme süresi ve maliyet hello azaltır — hello yazıldığı sırada, tek bir bölge içinde bant genişliği kullanımı ücretsizdir.  

Uygulamaları Azure içinde (mobil cihaz uygulamalarını gibi veya şirket içi Kurumsal Hizmetler), daha sonra tekrar barındırılan değil, istemci, erişecek toohello aygıtları yakın bir bölgede hello depolama hesabı yerleştirme genellikle gecikme azaltır İstemcilerinizi (örneğin, bazı Kuzey Amerika ve Avrupa'da bazı için) kapsamlı dağıtılır sonra birden çok depolama hesabı kullanmayı düşünmelisiniz: Kuzey Amerika bölge, diğeri Avrupa bir bölgede bulunan. Bu, her iki bölgelerdeki kullanıcılar için tooreduce gecikme yardımcı olur. Merhaba veri hello uygulama depoları belirli tooindividual kullanıcılar depolama hesapları arasında veri çoğaltmak gerektirmez varsa ve bu genellikle daha kolay tooimplement yaklaşımdır.  Geniş içerik dağıtımı için bir CDN önerilen – daha fazla ayrıntı için hello sonraki bölüme bakın.  

### <a name="subheading5"></a>İçerik dağıtımı
Bazı durumlarda (örneğin bir Web sitesinin hello giriş sayfası kullanılan video gösteri bir ürün) aynı içerik toomany kullanıcılar ya da bulunan bir uygulama gereksinimlerini tooserve hello aynı ya da birden çok bölgeye hello. Bu senaryoda, Azure CDN gibi bir içerik teslim ağı (CDN) kullanmanız gerekir ve hello CDN Azure depolama hello veri hello kaynak kullanır. Tek bir bölgede bulunduğunu ve düşük gecikme süresine sahip içerik tooother bölgeler sunan olamaz bir Azure Storage hesabı farklı olarak, birden çok veri merkezlerinde Merhaba Dünya sunucuları Azure CDN kullanır. Ayrıca, bir CDN genellikle tek bir depolama hesabına çok daha yüksek çıkış sınırlardan destekleyebilir.  

Azure CDN hakkında daha fazla bilgi için bkz: [Azure CDN](https://azure.microsoft.com/services/cdn/).  

### <a name="subheading6"></a>SAS ve CORS kullanma
Bir kullanıcının web tarayıcısı ya da bir cep telefonu uygulama tooaccess verileri Azure depolama alanında tooauthorize kodu JavaScript gibi gerektiğinde toouse web rolü bir proxy olarak uygulamada bir yaklaşım ise: hello kullanıcının cihaz hangi kapatma hello web rolüyle doğrular Merhaba depolama hizmeti ile kimlik doğrulaması. Bu şekilde, depolama hesabı anahtarlarınızı güvenli olmayan cihazlarda gösterme önleyebilirsiniz. Ancak, bu büyük yükünü hello web rolü'nde hello kullanıcının aygıtı arasında aktarılan tüm hello verileri ve hello depolama hizmeti ile Merhaba web rolü geçmesi gerekir çünkü yerleştirir. Web rolü bir proxy olarak hello depolama hizmeti için paylaşılan erişim imzaları (SAS) bazen üstbilgileri çıkış noktaları arası kaynak paylaşımı (CORS) ile birlikte kullanarak önleyebilirsiniz. SAS kullanarak, tooa depolama hizmeti doğrudan yoluyla sınırlı erişim belirteci, kullanıcının cihaz toomake istekleri izin verebilirsiniz. Örneğin, bir kullanıcı bir fotoğraf tooyour uygulaması tooupload isterse, web rolü oluşturmak ve toohello kullanıcının cihaz izni toowrite tooa belirli blob veya hello için kapsayıcı (daha sonra hello SAS belirteci süresi dolar) sonraki 30 dakika veren bir SAS belirteci gönderin.

Normalde, bir tarayıcı JavaScript "PUT" tooanother etki alanı gibi bir etki alanı tooperform belirli işlemler üzerinde bir Web sitesi tarafından barındırılan bir sayfasında izin vermez. Örneğin, bir web rolü "contosomarketing.cloudapp.net" ve istediğiniz toouse istemci tarafı JavaScript tooupload bir blob tooyour depolama hesabı "contosoproducts.blob.core.windows.net" barındırıyorsanız, tarayıcının hello "aynı kaynak İlkesi" Bu yasaklamaz işlem. CORS isteklerini (Bu roldeki servis talebi hello web) hello kaynak etki alanındaki kaynaklanan güvendiği hello hedef etki alanında (Bu örnek hello depolama hesabı) toocommunicate toohello tarayıcı izin veren bir tarayıcı özelliğidir.  

Bu iki teknolojinin, gereksiz yük (ve performans sorunlarını), web uygulamanızda önlemenize yardımcı olabilir.  

#### <a name="useful-resources"></a>Yararlı Kaynaklar
SAS hakkında daha fazla bilgi için bkz: [paylaşılan erişim imzaları, 1. parça: SAS modelini anlama hello](storage-dotnet-shared-access-signature-part-1.md).  

CORS hakkında daha fazla bilgi için bkz: [hello Azure Storage Hizmetleri için çıkış noktaları arası kaynak paylaşımı (CORS) Destek](http://msdn.microsoft.com/library/azure/dn535601.aspx).  

### <a name="caching"></a>Önbelleğe alma
#### <a name="subheading7"></a>Veri alma
Genel olarak, verileri bir hizmetinden kez alınıyor, iki kez alma daha iyidir. Zaten bir 50 MB blob hello depolama hizmeti tooserve içerik tooa kullanıcı olarak alınır bir web rolü çalıştıran bir MVC web uygulaması Hello örneği göz önünde bulundurun. Merhaba uygulaması sonra o aynı blob bir kullanıcı istekte ya da onu önbelleğe her zaman yerel olarak sonraki kullanıcı istekleri için hello önbelleğe alınan sürüm toodisk ve yeniden alınamadı. Ayrıca, bir kullanıcı hello veri istediğinde, uygulama sorunu değiştirilip değiştirilmediğini varsa hello tüm blob alma kaçının değiştirme saati için koşullu bir üstbilgiyle ALABİLİR hello. Bu aynı düzeni tooworking tablo varlıklarla uygulayabilirsiniz.  

Bazı durumlarda, uygulamanız bu hello blob, onu ve hello blob değiştirilirse bu dönem hello sırasında uygulama toocheck gerekmediğini alınıyor sonra kısa bir süre için geçerli kalır varsayabilirsiniz karar verebilirsiniz.

Yapılandırma, arama ve her zaman hello uygulama tarafından kullanılan diğer verileri önbelleğe almak için harika bir aday değildir.  

.NET kullanarak nasıl tooget bir blob'un özellikleri toodiscover hello son değiştirilme tarihi örneği için bkz: [ayarlama ve alma özelliklerini ve meta veri](storage-properties-metadata.md). Koşullu yüklemeler hakkında daha fazla bilgi için bkz: [koşullu bir Blob yerel bir kopyasını yenileme](http://msdn.microsoft.com/library/azure/dd179371.aspx).  

#### <a name="subheading8"></a>Toplu veri yüklemek
Bazı uygulama senaryolarında verilerini yerel olarak toplamak ve düzenli aralıklarla, her veri parçası hemen karşıya yerine bir toplu işte karşıya yükleyin. Örneğin, bir web uygulaması bir günlük dosyası etkinliklerin tutabilirsiniz: Merhaba uygulama ya da karşıya her etkinlik ayrıntılarını (çok sayıda depolama işlemleri gerektirir) bir tablo varlığı olur veya Etkinlik ayrıntıları tooa yerel günlük dosyası, kaydedebilir ve ardından düzenli aralıklarla tüm Etkinlik ayrıntıları ayrılmış dosya tooa blob olarak karşıya yükleyin. Her günlük girişinin 1 KB boyutunda ise, binlerce (tek bir işlemde boyutunda too64MB kurma, bir blob karşıya yükleyebilirsiniz) tek bir "Put Blob" işlemde karşıya yükleyebilirsiniz. Elbette, Hello yerel makine önceki toohello karşıya yükleme çökerse bazı günlük verilerini potansiyel olarak kaybedersiniz: hello uygulama geliştiricisi tasarlamak için istemci cihazı hello olasılığı veya hataları karşıya yükleme.  Merhaba etkinlik verileri timespans (yalnızca tek etkinliği) indirilen toobe gerekirse, BLOB'ları tablolar üzerindeki önerilir.

### <a name="net-configuration"></a>.NET yapılandırması
.NET Framework kullanarak Merhaba, bu bölümde toomake önemli performans geliştirmeleri kullanabileceğiniz birkaç Hızlı yapılandırma ayarları listelenmiştir.  Seçilen dilinizde benzer kavramları uygularsanız, diğer diller kullanırken toosee kontrol edin.  

#### <a name="subheading9"></a>Varsayılan bağlantı sınırını artırmak
.NET içinde (genellikle olan bir istemci ortamında 2 ya da bir sunucu ortamında 10) hello varsayılan bağlantı sınırı koddan hello artırır too100. Genellikle, hello değeri tooapproximately hello uygulamanız tarafından kullanılan iş parçacığı sayısını ayarlamanız gerekir.  

```csharp
ServicePointManager.DefaultConnectionLimit = 100; //(Or More)  
```

Tüm bağlantılar açmadan önce hello bağlantı sınırı ayarlamanız gerekir.  

Diğer programlama dilleri için nasıl tooset hello bağlantı sınırlamak dil belgelerine toodetermine bakın.  

Ek bilgi için bkz: hello blog gönderisi [Web Hizmetleri: eşzamanlı bağlantı](http://blogs.msdn.com/b/darrenj/archive/2005/03/07/386655.aspx).  

#### <a name="subheading10"></a>İş parçacığı havuzu en az iş parçacığı zaman uyumlu bir kod ile zaman uyumsuz görevleri kullanıyorsanız artırın
Bu kod hello iş parçacığı havuzu min iş parçacıkları artmasına neden olur:  

```csharp
ThreadPool.SetMinThreads(100,100); //(Determine hello right number for your application)  
```

Daha fazla bilgi için bkz: [ThreadPool.SetMinThreads yöntemi](http://msdn.microsoft.com/library/system.threading.threadpool.setminthreads%28v=vs.110%29.aspx).  

#### <a name="subheading11"></a>.NET 4.5 çöp toplama yararlanın
.NET 4.5 veya üzeri hello istemci uygulaması tootake sunucu çöp toplama performans geliştirmeleri avantajlarından için kullanın.

Daha fazla bilgi için hello makalesine bakın [bir genel bakış, performans iyileştirmeleri .NET 4.5 içinde](http://msdn.microsoft.com/magazine/hh882452.aspx).  

### <a name="subheading12"></a>Sınırsız paralellik
Paralellik performans için harika olabilirler, ancak birden çok çalışanları tooaccess kullanarak sınırsız paralellik (iş parçacıkları ve/veya paralel istekler hello sayısının sınır) tooupload ya da indirme verileri birden çok bölüm kullanma konusunda dikkatli olmanız (kapsayıcıları, kuyruklar, veya Tablo bölümlerini) içinde hello birden çok öğe aynı depolama hesabı veya tooaccess hello aynı bölüm. Merhaba paralellik sınırsız ise, uygulamanızın hello istemci cihazın özelliklerini aşan veya uzun gecikme süreleri kaynaklanan ve azaltma depolama hesabının ölçeklenebilirlik hedefleri hello.  

### <a name="subheading13"></a>Depolama istemcisi kitaplıklarını ve araçları
Her zaman hello en son Microsoft sağlanan istemci kitaplıkları ve araçları kullanın. Merhaba yazıldığı sırada, istemci kitaplıkları .NET, Windows Phone, Windows çalışma zamanı, Java ve C++ için kullanılabilir gibi diğer diller için Önizleme kitaplıkları vardır. Ayrıca, Microsoft, PowerShell cmdlet'leri ve Azure Storage ile çalışmak için Azure CLI komutları yayımladı. Microsoft etkin olarak bu araçlar performans aklınızda geliştirir, bunları toodate hello en son hizmet sürümleriyle yukarı tutar ve birçok performans uygulamaları dahili olarak kanıtlanmış hello işlemek sağlanır.  

### <a name="retries"></a>Yeniden deneme sayısı
#### <a name="subheading14"></a>Azaltma ServerBusy
Bazı durumlarda, hello depolama hizmeti, uygulamanızın kısıtlama veya yalnızca toosome geçici koşul nedeniyle yüklenemiyor tooserve hello isteği ve "503 Sunucu meşgul" iletisi ya da "500 zaman aşımı" döndürür.  Bu, uygulamanızın hello ölçeklenebilirlik hedefleri hiçbirini yaklaşıyorsa veya daha yüksek verimlilik, bölümlenmiş veri tooallow hello sistem yeniden dengelenmesi yoksa oluşabilir.  Merhaba istemci uygulaması genellikle işlemi yeniden deneyin, bu tür bir hataya neden olan hello: aynı isteği daha sonra hello çalışırken başarılı olabilir. Ancak, ölçeklenebilirlik hedefleri aşan çünkü hello depolama hizmeti uygulamanız azaltma ya da hello hizmeti oluşturamıyor tooserve hello isteği başka bir nedenle olsa bile, agresif yeniden deneme genellikle hello sorunu daha da kötüsü oluşturur. Bu nedenle, bir üstel geri alma (Merhaba istemci kitaplıkları varsayılan toothis davranışını) kullanmanız gerekir. Örneğin, uygulamanız 2 saniye sonra 4 saniye sonra 10 saniye sonra 30 saniye sonra yeniden deneyin ve tamamen işlemden vazgeçerlerdi. Bu davranış önemli ölçüde hello hizmet kendi yükünü azaltma yerine herhangi bir sorun exacerbating uygulamanızda sonuçlanır.  

Bunlar azaltma hello sonucunu değildir ve beklenen toobe geçici olduğundan bağlantı hataları hemen yeniden denenebilir olduğunu unutmayın.  

#### <a name="subheading15"></a>Denenemeyen hata
Merhaba istemci kitaplıkları hangi hataları yeniden deneme yapabilir ve hangi olmadığı kullanan. Kendi kodunuzu hello depolama REST API karşı yazıyorsanız, Bununla birlikte, yeniden bazı hatalar var. unutmayın: Örneğin, 400 (Hatalı istek yanıt bu Merhaba istemci uygulaması gösterir) nedeniyle işlenemedi bir istek gönderdi, beklenen biçimde değildi. Bu isteği göndermeden neden olur; böylece, yeniden deneniyor içinde hiçbir noktası her zaman hello aynı yanıt. Kendi kodunuzu hello depolama REST API karşı yazıyorsanız, hangi hello hata ortalamasının ve hello uygun şekilde tooretry (veya değil) kodları unutmayın her biri için.  

#### <a name="useful-resources"></a>Yararlı Kaynaklar
Depolama hata kodları hakkında daha fazla bilgi için bkz: [durum ve hata kodları](http://msdn.microsoft.com/library/azure/dd179382.aspx) hello Microsoft Azure web sitesinde.  

## <a name="blobs"></a>Bloblar
Uygulamalar için kanıtlanmış toplama toohello içinde [tüm hizmetleri](#allservices) daha önce açıklandığı gibi hello aşağıdaki yöntemler kanıtlanmış özellikle toohello blob hizmeti uygulayın.  

### <a name="blob-specific-scalability-targets"></a>BLOB özgü ölçeklenebilirlik hedefleri
#### <a name="subheading46"></a>Birden çok istemci aynı anda tek bir nesne erişme
Çok sayıda eş zamanlı olarak tek bir nesne erişen istemcilerin varsa nesnesi ve depolama hesabımın ölçeklenebilirlik hedefleri başına tooconsider gerekir. tek bir nesneye erişmek için istemcilerin tam sayısı Hello hello nesnesi aynı anda isteyen istemcilerin hello nesnenin hello boyutu hello sayısı gibi etkenlere bağlı olarak farklılık gösterir, koşullar vb. ağ.

Merhaba nesnesi üzerinden dağıtılabilir CDN görüntü veya video gibi bir Web sitesinden sunulan sonra bir CDN kullanmanız gerekir. Bkz: [burada](#subheading5).

Bilimsel benzetimleri hello veri gizli olduğu gibi diğer senaryolarda, iki seçeneğiniz vardır. Merhaba, ilk nesne hello İş yükünüzün erişim gibi aynı anda erişilen zaman vs döneminde erişilen toostagger olur. Alternatif olarak, geçici olarak hello nesne toomultiple depolama hesapları böylece artırma hello toplam IOPS nesne başına ve depolama hesapları arasında kopyalayabilirsiniz. Sınırlı testinde yaklaşık 25 VM'ler 100 GB blob paralel (her VM 32 iş parçacığı kullanma hello indirme parallelizing) aynı anda yüklenemedi bulduk. Tooaccess hello nesne gerek 100 istemciye olsaydı, ilk tooa ikinci depolama hesabı kopyalama olan ilk 50 VM'ler erişim hello ilk blob hello ve ikinci 50 VM'ler erişim hello ikinci blob hello. Bu tasarım sırasında test etmeniz gerekir böylece sonuçları uygulamaları davranışına bağlı olarak değişir. 

#### <a name="subheading16"></a>Bant genişliği ve Blob başına işlem
Okuma veya tooa tooa en fazla 60 MB/saniye yukarı adresindeki tek blobu yazma (Bu, pek çok istemci tarafı ağları hello özelliklerini aşan yaklaşık 480 MB / sn'dir (Merhaba istemci cihazda fiziksel NIC hello dahil olmak üzere). Ayrıca, saniye başına too500 isteği oluşturan tek bir blob destekler. Tooread gereken birden fazla istemciniz varsa hello aynı blob ve bu sınırları aşabilir, hello blob dağıtmak amacıyla bir CDN kullanmayı düşünmeniz gerekir.  

BLOB'lar için hedef işleme hakkında daha fazla bilgi için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md).  

### <a name="copying-and-moving-blobs"></a>Kopyalama ve BLOB'lar taşıma
#### <a name="subheading17"></a>BLOB kopyalama
Merhaba depolama REST API sürümü 2012-02-12 sunulan hello kullanışlı özelliği toocopy BLOB'lar hesaplarında: bir istemci uygulaması hello depolama hizmeti toocopy (büyük olasılıkla, farklı bir depolama hesabı) başka bir kaynaktan bir blob isteyin ve hello olanak tanır Hizmet hello kopyalama zaman uyumsuz olarak gerçekleştirin. Bu etmez toodownload gerekir ve hello verileri yüklemek için diğer depolama hesaplarından veri geçişi olduğunda hello uygulama için gereken hello bant genişliğini önemli ölçüde azaltabilir.  

Bir göz önünde bulundurarak, ancak, depolama hesapları arasında kopyalarken, hello kopyalama tamamlandığında üzerinde hiçbir zaman garantisi olmasıdır. Uygulamanızı bir blob kopyalama hızla denetiminiz altında toocomplete gerekiyorsa, tooa VM indiriliyor ve toohello hedef karşıya yüklemeyi daha iyi toocopy hello blob olması olabilir.  Bu durumda tam öngörülebilirlik için hello kopyalama gerçekleştirildiğinden emin hello çalıştıran bir VM tarafından aynı Azure bölgesinde, aksi takdirde ağ koşulları, kopyalama performansını etkileyen olabilir ve muhtemelen.  Ayrıca, program aracılığıyla zaman uyumsuz bir kopyasının hello ilerlemesini izleyebilirsiniz.  

Aynı depolama hesabındaki kendisini genellikle tamamlanır hızlı bir şekilde hello içinde kopyalar unutmayın.  

Daha fazla bilgi için bkz: [kopyalama Blob](http://msdn.microsoft.com/library/azure/dd894037.aspx).  

#### <a name="subheading18"></a>AzCopy kullanma
Hello Azure depolama ekibi, bir komut satırı aracı "AzCopy" yayımladı yani yüksetlmesi toohelp birçok BLOB'lar için gelen ve depolama hesapları arasında aktarma toplu ile.  Bu araç, bu senaryo için en iyi duruma getirilmiş ve yüksek aktarım hızlarıyla elde edebilirsiniz.  Kullanımı toplu karşıya yükleme, indirme ve kopyalama senaryoları için teşvik edilir. Bunun hakkında daha fazla toolearn ve onu indirmek için bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md).  

#### <a name="subheading19"></a>Azure içeri/dışarı aktarma hizmeti
(Birden fazla 1 TB) veri çok büyük birimlerde hello Azure Storage hello karşıya yükleme ve blob depolama alanından sevkiyat sabit sürücüler tarafından indirme sağlar içeri/dışarı aktarma hizmeti sunar.  Verilerinizi bir sabit sürücüye yerleştirin ve karşıya yükleme tooMicrosoft göndermek veya boş sabit disk tooMicrosoft toodownload veri gönder.  Daha fazla bilgi için bkz: [hello Microsoft Azure içeri/dışarı aktarma hizmeti tooTransfer veri tooBlob depolama kullanmak](storage-import-export-service.md).  Karşıya yükleme/bu verilerin hacmi hello ağ üzerinden indirme daha çok daha etkili olabilir.  

### <a name="subheading20"></a>Meta veri kullanın
Merhaba blob hizmeti hello blob hakkındaki meta verileri içerebilir head isteklerini destekler. Örneğin, uygulamanızın hello EXIF veri fotoğraf dışında gerekli olursa, onu hello fotoğraf almak ve ayıklayın toosave bant genişliği ve performansı, Merhaba uygulaması hello fotoğrafı karşıya olduğunda, uygulamanızın hello blob'un meta verilerde hello EXIF veri saklayabilirsiniz: önemli bant genişliği korunarak sonra HEAD isteği yalnızca kullanarak meta verilerde hello EXIF veri alabilirsiniz ve tooextract hello EXIF verileri her zaman hello blobu okuma hello işleme süresi gerekir. Bu, burada yalnızca hello meta verileri ve değil tam içeriğini blob hello gerekir senaryolarda yararlı olacaktır.  Yalnızca 8 KB meta verileri blob depolanabilir unutmayın (Merhaba hizmet değil kabul edeceği bir istek toostore daha yüksek) hello verileri bu boyut sığmadığında şunları yapamazsınız: şekilde mümkün toouse bu yaklaşım olabilir.  

Bir örnek için nasıl tooget .NET kullanarak bir blob'un meta veri bkz [ayarlama ve alma özelliklerini ve meta veri](storage-properties-metadata.md).  

### <a name="uploading-fast"></a>Hızlı yükleme
Merhaba ilk soru tooanswer tooupload BLOB hızlı, sayısıdır: misiniz bir blob ya da birden çok karşıya yükleniyor?  Merhaba Kılavuzu toodetermine hello doğru yöntemi toouse senaryonuza bağlı olarak aşağıdaki kullanın.  

#### <a name="subheading21"></a>Bir büyük blob hızlı bir şekilde karşıya yükleme
büyük tek bir blob hızlı bir şekilde tooupload, istemci uygulamanız blok veya sayfaları (tek tek bloblar ve bir bütün olarak hello depolama hesabı için hello ölçeklenebilirlik hedefleri dikkatli olmak) paralel yüklemeniz gerekir.  Merhaba resmi Microsoft tarafından sağlanan RTM depolama istemcisi kitaplıklarını (.NET, Java) hello özelliği toodo bu gerektiğini unutmayın.  Her hello kitaplıkları için belirtilen nesne/özelliği tooset hello düzeyini eşzamanlılık hello kullanın:  

* .NET: Kümesi ParallelOperationThreadCount kullanılan BlobRequestOptions nesne toobe üzerinde.
* Java/Android: BlobRequestOptions.setConcurrentRequestCount() kullanın
* Node.js: parallelOperationThreadCount ya da hello isteği seçeneklerini veya hello blob hizmeti kullanın.
* C++: Merhaba blob_request_options::set_parallelism_factor yöntemini kullanın.

#### <a name="subheading22"></a>Çok sayıda BLOB'ları hızlı bir şekilde karşıya yükleme
birçok BLOB'ların hızla tooupload BLOB'ları paralel karşıya yükleyin. Bu, hello karşıya yükleme hello depolama hizmeti birden çok bölüm yayılan olduğundan tek BLOB'ları aynı anda paralel blok karşıya yüklemeyi daha hızlıdır. Tek bir blob yalnızca 60 MB/saniye (yaklaşık 480 Mbps) üretimini destekler. Yazma Hello anda ABD tabanlı LRS hesabı hello verimlilik tek tek bir blob tarafından desteklenen daha çok daha fazla olan Gbps giriş too20 destekler.  [AzCopy](#subheading18) yüklemeleri varsayılan olarak paralel olarak gerçekleştirir ve bu senaryo için önerilir.  

### <a name="subheading23"></a>Merhaba doğru blob türünü seçme
Azure Storage blobu iki türlerini destekler: *sayfa* blobları ve *blok* BLOB'lar. Belirli kullanım senaryosu için tercih ettiğiniz blob türü hello performans ve ölçeklenebilirlik çözümünüzün etkiler. Blok blobları, tooupload büyük miktarlarda verinin verimli bir şekilde istediğinizde uygundur: Örneğin, bir istemci uygulaması tooupload fotoğraf veya video tooblob depolama gerekebilir. Sayfa bloblarını Merhaba uygulaması tooperform rastgele yazmaları hello verileri gerekirse uygun: Örneğin, Azure VHD'ler sayfa BLOB olarak depolanır.  

Daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](http://msdn.microsoft.com/library/azure/ee691964.aspx).  

## <a name="tables"></a>Tablolar
Uygulamalar için kanıtlanmış toplama toohello içinde [tüm hizmetleri](#allservices) daha önce açıklandığı gibi hello aşağıdaki yöntemler kanıtlanmış özellikle toohello tablo hizmeti uygulayın.  

### <a name="subheading24"></a>Tablo özgü ölçeklenebilirlik hedefleri
Toplama toohello bant genişliği sınırlamaları tüm depolama hesabının içinde tablolar belirli ölçeklenebilirlik sınırına aşağıdaki hello vardır.  Merhaba sistem trafiği arttıkça Bakiye yükler, ancak trafiğinizi ani WINS'e varsa şunları yapamazsınız: Not mümkün tooget bu birimin sn'ye hemen olması.  WINS'e desen sahiptir, toosee azaltma beklemelisiniz ve/veya hello depolama hizmeti olarak aşırı zaman aşımları sırasında otomatik olarak hello varsa yük tablonuz dengeler.  Yukarı yavaş genellikle ramping uygun şekilde hello sistem saati tooload bakiye verir gibi daha iyi sonuçlar vardır.  

#### <a name="entities-per-second-account"></a>Varlıkları / saniye (hesap)
tabloları erişmek için hello ölçeklenebilirlik sınırına too20, bir hesap için saniye başına 000 varlıkları (1 KB her) çalışıyor.  Genel olarak, eklenir, her bir varlık güncelleştirildi, silinmiş veya bu hedef doğru sayar taranan.  Bu nedenle 100 varlıklarını içeren bir toplu yerleştirme 100 varlık olarak sayar.  1000 varlıklar tarar ve 5 döndüren bir sorgu 1000 varlıklar sayılır.  

#### <a name="entities-per-second-partition"></a>Varlıkları / saniye (bölüm)
Tek bir bölüm içinde ölçeklenebilirlik hedef hello tabloları erişme 2.000 varlıkları (1 KB her) saniye başına için kullanarak hello aynı sayım hello önceki bölümde açıklandığı gibi.  

### <a name="configuration"></a>Yapılandırma
Bu bölümde hello tablo hizmetinde toomake önemli performans geliştirmeleri kullanabileceğiniz çeşitli hızlı yapılandırma ayarları listelenmiştir:  

#### <a name="subheading25"></a>JSON kullanın
Depolama hizmeti sürüm 2013-08-15'den başlayarak, hello tablo hizmeti tablo verileri aktarmak için yerine hello XML tabanlı AtomPub biçimi kullanarak destekler. Bu yükü boyutları % 75 azaltabilir ve uygulamanızın hello performansını önemli ölçüde artırabilir.

Post hello daha fazla bilgi için bkz [Microsoft Azure tabloları: Giriş JSON](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/05/windows-azure-tables-introducing-json.aspx) ve [tablo hizmeti işlemleri için yük biçimi](http://msdn.microsoft.com/library/azure/dn535600.aspx).

#### <a name="subheading26"></a>Nagle devre dışı
Nagle'nın algoritması, yaygın olarak TCP/IP'yi ağlarda anlamına gelir tooimprove ağ performansını uygulanır. Ancak, tüm durumlarda (örneğin, yüksek oranda etkileşimli ortamlarda) uygun değil. Azure Storage Nagle'nın algoritması istekleri toohello tablo ve kuyruk Hizmetleri hello performansını olumsuz etkileyebilir sahiptir ve mümkünse bu seçeneği devre dışı.  

Bizim blog gönderisi daha fazla bilgi için bkz [Nagle'nın algoritmasıdır küçük isteklerini doğru değil kolay](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx), neden Nagle'nın algoritması kötü tablo ve kuyruk istekleri ile etkileşim kurar ve gösterir açıklar nasıl toodisable istemciniz içinde uygulama.  

### <a name="schema"></a>Şema
Nasıl temsil eder ve verilerinizi sorgu hello tablo hizmeti hello performansını etkileyen hello büyük tek faktördür. Her uygulama farklı olsa da, bu bölümde ile ilgili bazı genel kanıtlanmış uygulamalar özetlenmektedir:  

* Tablo Tasarımı
* Verimli sorguları
* Verimli veri güncelleştirmeleri  

#### <a name="subheading27"></a>Tabloları ve bölümleri
Tabloları bölümlere ayrılır. Depolanan her varlık bir bölüm paylaşımları hello aynı bölüm anahtarına ve benzersiz bir satır anahtarı tooidentify sahiptir, bu bölümü. Bölümler fayda sağlar, ancak aynı zamanda ölçeklenebilirlik sınırları tanıtır.  

* Yararları: Aynı too100 ayrı bir depolama operasyonları (4 MB Toplam boyut sınırı) içeren bir tek, atomik, toplu işlemde bölüm hello varlıklarda güncelleştirebilirsiniz. Hello aynı numarası varsayılarak alınan varlıklar toobe de tek bir bölüm içindeki verileri (ancak daha fazla tablo verileri Sorgulama öneriler için okumaya devam edin) bölümleri yayılan verileri daha verimli sorgulayabilirsiniz.
* Ölçeklenebilirlik sınırına: tek bir bölüm içinde depolanan erişim tooentities olamaz yük dengeli bölümleri atomik toplu işlemleri desteklemek için. Bu nedenle, hello ölçeklenebilirlik tek tek tablo bölüm bir bütün olarak hello tablo hizmeti için daha düşük hedefidir.  

Bu özellikleri tablolar ve bölümler nedeniyle, tasarım ilkeleri aşağıdaki hello benimsemeye:  

* İstemci uygulamanızı sık güncelleştirilen veya aynı mantıksal birim çalışma alanında bulunmalıdır hello sorgulanan veriler aynı bölüme hello.  Bu, uygulamanızın yazma toplama veya atomik toplu işlemleri tootake avantajlarından istediğiniz nedeniyle, olabilir.  Ayrıca, tek bir bölüm verileri daha verimli bir şekilde tek bir sorguda veri bölümler sorgulanabilir.
* İstemci uygulamanızı ekleme/güncelleştirme veya aynı mantıksal birim (tek bir sorgu veya toplu güncelleştirme) çalışma alanında bulunmalıdır hello sorgu veri bölümleri ayırın.  Önemli bir not hiçbir sınır toohello sayıda bölüm anahtarı tek bir tablodaki böylece bir sorun değildir ve performansını etkilemez bölüm anahtarlarını milyonlarca sahip olmasıdır.  Örneğin, uygulamanızın kullanıcı oturum açma ile popüler bir Web sitesi ise, hello bölüm anahtarı olarak hello kullanıcı kimliğini kullanarak iyi bir seçimdir olması olabilir.  

#### <a name="hot-partitions"></a>Sık kullanılan bölümleri
Etkin bir bölüm hello trafiği tooan hesabı orantısız yüzdesi alan biridir ve tek bir bölüm olduğundan, yük dengeli olamaz.  Genel olarak, dinamik bölümleri iki yoldan biriyle oluşturulur:  

##### <a name="subheading28"></a>Yalnızca ekleme ve yalnızca desenleri önüne ekleyin
Merhaba "Yalnızca Ekle" deseni burada tüm (veya neredeyse tüm) hello trafiği tooa PK verilen artırır ve geçerli saati according toohello azaltır biridir.  Uygulamanız hello geçerli tarih günlük verileri için bir bölüm anahtarı olarak kullanılan varsa bir örnektir.  Bu toohello son bölümü, tablodaki giderek hello eklemeleri tümünde sonuçlanır ve devam eden toohello son tablonuzun hello yazma işlemlerinin tümü hello sistem Bakiye yükleyemiyor.  Merhaba birim trafiği toothat bölümünün hello bölüm düzeyi ölçeklenebilirlik hedef aşarsa, azaltma içinde sonuçlanır.  Bu, trafiği toomultiple bölümleri gönderilir daha iyi tooensure tooenable Yük Dengelemesi hello tablonuz arasında istekleri olur.  

##### <a name="subheading29"></a>Yüksek trafik verileri
Bölümleme şeması sonuçlarınızda tek bir bölüm, yalnızca daha diğer bölümler kullanılan veri varsa, bu bölüm hello ölçeklenebilirlik hedef tek bir bölümün yaklaştığında da azaltma görebilirsiniz.  Daha iyi toomake bölüm düzeni sonuçlarınızı hiçbir tek yaklaşan hello ölçeklenebilirlik hedefleri bölüm emin olur.  

#### <a name="querying"></a>Sorgulama
Bu bölümde hello tablo hizmeti sorgulamak için kanıtlanmış yöntemleri açıklar.  

##### <a name="subheading30"></a>Sorgu kapsamı
Varlıkları tooquery birkaç yolu toospecify hello aralığı vardır.  Merhaba, her hello kullanımlarını tartışması aşağıdadır.  

Genel olarak, tarama (sorguları tek bir varlık büyük) kaçının ancak tarama gerekir, böylece taramalarınızda tarama veya önemli miktarda gerekmeyen varlıklar döndürüyor gereksinim hello verileri almak tooorganize verilerinizi deneyin.  

###### <a name="point-queries"></a>Noktası sorguları
Noktası sorgu tam olarak bir varlığı alır. Bunu hello bölüm anahtarı ve hello varlık tooretrieve satır anahtarı belirterek yapar. Bu sorgular çok verimli ve onları mümkün olduğunda kullanmalısınız.  

###### <a name="partition-queries"></a>Bölüm sorguları
Ortak bir bölüm anahtarı paylaşan veri kümesini alır. bir sorgu bir bölüm sorgudur. Genellikle, hello sorgu toplama tooa bölüm anahtarı satır anahtar değerleri aralığı veya bazı varlık özelliği için değer aralığını belirtir. Bunlar noktası sorguları az verimlidir ve kullanılmamalıdır.  

###### <a name="table-queries"></a>Tablo sorguları
Tablo sorgusu ortak bir bölüm anahtarı paylaşmaz varlık kümesini alır bir sorgudur. Bu sorguları etkili değildir ve mümkünse kaçınmalısınız.  

##### <a name="subheading31"></a>Sorgu yoğunluğu
Başka bir anahtar etken sorgu verimliliği de hello taranan toofind hello Ayarla döndürülen varlıkları karşılaştırılan toohello sayıda döndürülen varlıkların sayısıdır. Uygulamanızı bir tablo sorgusu yalnızca %1 hello veri paylaşımlarının döndürdüğü her bir varlık için 100 varlık hello sorgu tarama bir özellik değeri için bir filtre ile uyguluyorsa. Merhaba tablo ölçeklenebilirlik hedefleri ele alınan daha önce tüm toohello taranan varlıkların sayısı ilgili ve döndürülen varlıkların sayısı hello değil: çok fazla tarama gerekir çünkü düşük sorgu yoğunluğu kolayca hello tablo hizmeti toothrottle uygulamanızı neden olabilir Aradığınız varlıklar tooretrieve hello varlık.  Merhaba bölümüne bakın üzerinde [denormalization](#subheading34) hakkında daha fazla bilgi için tooavoid bu.  

##### <a name="limiting-hello-amount-of-data-returned"></a>Sınırlama hello tutar, veri döndürdü.
###### <a name="subheading32"></a>Filtreleme
Bir sorgu hello istemci uygulamasında gerekmeyen varlıkları döndürme bildiğiniz durumlarda kümesi döndürdü hello filtre tooreduce hello boyutunu kullanmayı düşünün. Hello varlıklar toohello istemci döndürülen değil hata hala hello ölçeklenebilirlik sınırları doğru sayısı, uygulama performansı azaltılmış hello ağ yükü boyutu nedeniyle geliştirmek ve istemci uygulamanız işlemelidir varlıkların sayısı sınırlı hello .  Not bakın [sorgu yoğunluğu](#subheading31), birkaç varlıklar döndürülen olsa bile birçok varlık filtreler bir sorgu hala azaltma içinde sonuçlanabilir şekilde hello ölçeklenebilirlik hedefleri toohello taranan varlıkların sayısı ancak – ilişkilidir.  

###### <a name="subheading33"></a>Yansıtma
İstemci uygulamanızı yalnızca sınırlı sayıda tablonuz hello varlıklarda özelliklerinden gerekirse, veri kümesi döndürdü hello projeksiyon toolimit hello boyutu kullanabilirsiniz. Gibi filtreleme ile bu tooreduce Ağ Yükü ve işleme istemci yardımcı olur.  

##### <a name="subheading34"></a>Denormalization
İlişkisel veritabanları ile çalışma aksine hello verimli bir şekilde tablo verileri sorgulamak için kanıtlanmış yöntemleri toodenormalizing verilerinizi yol açar. Diğer bir deyişle, çoğaltma izin ver hello birden çok varlık aynı verileri (biri her anahtar için toofind hello veri kullanabilir) toominimize hello bir sorgu varlıklar toofind çok sayıda tooscan sahip olmak yerine toofind hello veri hello istemci ihtiyaçları taramalısınız varlıkların sayısı Merhaba veri uygulamanız gerekir.  Örneğin, bir e-ticaret Web sitesi toofind göre bir sıralamayı hem hello Müşteri Kimliği istediğiniz (bu müşterinin sipariş ver) ve hello tarihe göre (bir tarihte sipariş ver).  Table Storage ' en iyi toostore hello varlık (veya bir başvuru tooit) olmasından iki kez – bir kez Müşteri Kimliği, bir kez hello tarihe göre bulma toofacilitate tarafından tablo adı, PK ve işareti toofacilitate bulma ile.  

#### <a name="insertupdatedelete"></a>Ekleme/güncelleştirme/silme
Bu bölümde hello tablo hizmetinde depolanan varlıklar değiştirme kanıtlanmış yöntemleri açıklar.  

##### <a name="subheading35"></a>Toplu işleme
Toplu işlem, Azure storage'da varlık Grup işlemleri (ETG) olarak adlandırılır; bir ETG tüm hello işlemlerini tek bir tablodaki tek bir bölüm olması gerekir. Mümkünse, ETGs tooperform ekler, güncelleştirmeleri ve silme toplu olarak kullanın. Bu istemci uygulaması toohello sunucunuzdan hello gidiş dönüş sayısını azaltan (bir ETG faturalandırma için tek bir işlem olarak sayar ve too100 depolama operasyonları içerebilir) Faturalanabilir işlemleri hello sayısını azaltır ve atomik sağlar Güncelleştirmeler (tüm işlemlerin başarılı ya da bir ETG içinde başarısız). Mobil cihazlar gibi yüksek gecikme süreleriyle ortamları ETGs kullanarak büyük ölçüde yararlanabilir.  

##### <a name="subheading36"></a>Upsert
Kullanımı tablo **Upsert** işlemlerini mümkün olduğunda. İki tür vardır **Upsert**, her ikisi de Geleneksel daha etkili olabilir **Ekle** ve **güncelleştirme** işlemleri:  

* **InsertOrMerge**: tooupload hello varlığın özelliklerinin bir alt istediğinizde bunu kullanın, ancak emin değilseniz olup hello varlık zaten mevcut. Merhaba varlık varsa, bu çağrıyı hello dahil hello özellikleri güncelleştirmeleri **Upsert** işlemi ve tüm mevcut özellikleri oldukları gibi bırakır, hello varlık yok, hello yeni bir varlık ekler. Yalnızca değiştiriyorsunuz tooupload hello özellikleri gerektiren bir sorgu benzer toousing projeksiyon budur.
* **Yerleştir veya Değiştir**: tooupload tamamen yeni bir varlık istiyor, ancak olup zaten var. emin değilseniz bunu kullanın. Bu yalnızca kullanmalısınız tamamen hello eski varlık yazdığından bu hello yeni varlık karşıya bildiğinizde tamamen doğru olduğundan. Örneğin, kullanıcının geçerli konumuna hello uygulama daha önce depolanan hello kullanıcı için konum verilerini olup olmadığına bakılmaksızın depolar tooupdate hello varlık istediğiniz; Hello yeni konum varlık tamamlandıktan ve tüm önceki varlıktan herhangi bir bilgi gerekmez.

##### <a name="subheading37"></a>Tek bir varlık veri serisi depolama
Bazı durumlarda, bir uygulama, sık tooretrieve tümünü bir defada ihtiyaç duyduğu veri serisi depolar: Örneğin, bir uygulama CPU kullanımı zaman sipariş tooplot hello veri çalışırken bir grafik içinde hello son 24 saat izlemek. Belirli bir saati temsil eden ve hello CPU kullanımı, saat için depolama her varlık, saatte toohave bir tablo varlıkla bir yaklaşımdır. tooplot en son 24 saat hello hello verilerini tutan tooretrieve hello varlıklar bu veriler, Merhaba uygulaması gerekir.  

Uygulamanızın ayrı özelliği tek bir varlık olarak her bir saat hello CPU kullanımı alternatif olarak, saklayabilirsiniz: tooupdate her saat, uygulamanızın tek bir kullanabilir **InsertOrMerge Upsert** tooupdate hello değeri Merhaba çağırın en son saat. tooplot hello veri hello uygulamanın yalnızca tooretrieve 24, çok verimli bir sorgu için yapmak yerine tek bir varlık gerekir (tartışma bakın [sorgu kapsam](#subheading30)).

##### <a name="subheading38"></a>BLOB'ları yapılandırılmış veri depolama
Bazen yapılandırılmış verileri tablolarda, gitmesi gereken ancak aralıkları varlıkların her zaman birlikte alınır ve toplu eklenebilir gibi hissettirir.  Bu iyi bir örneği günlük dosyasıdır.  Bu durumda, birkaç dakikadan günlükler toplu, bunları eklemek ve sonra her zaman aynı anda de günlüklerinin birkaç dakika alıyor.  Bu durumda, nesneleri yazılmış/döndürülen hello sayısını önemli ölçüde azaltmak yanı sıra bu yana genellikle gereksinim yapılan isteklerin sayısı hello performans için bu tablolar, yerine daha iyi toouse BLOB sayısıdır.  

## <a name="queues"></a>Kuyruklar
Uygulamalar için kanıtlanmış toplama toohello içinde [tüm hizmetleri](#allservices) daha önce açıklandığı gibi hello aşağıdaki yöntemler kanıtlanmış özellikle toohello sıra hizmeti uygulayın.  

### <a name="subheading39"></a>Ölçeklenebilirlik sınırları
Tek bir sırada (Buraya bir ileti olarak her AddMessage, GetMessage ve DeleteMessage sayısı) saniyede yaklaşık 2.000 iletileri (1 KB her) işleyebilir. Bu, uygulamanız için yetersiz ise, birden çok sıraya kullanın ve hello iletileri bunların arasında yayılır.  

Konumundaki geçerli ölçeklenebilirlik hedefleri görüntülemek [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md).  

### <a name="subheading40"></a>Nagle devre dışı
Merhaba Nagle algoritma açıklanır tablo yapılandırmasına Hello bölümüne bakın: Merhaba Nagle algoritmasıdır sıra isteklerini hello performans için genellikle bozuk ve devre dışı bırakmalısınız.  

### <a name="subheading41"></a>İleti boyutu
Sıra performans ve ölçeklenebilirlik azalıyor ileti boyutu artar. Bir ileti yalnızca hello bilgi hello alıcı gereksinimlerini yerleştirmeniz gerekir.  

### <a name="subheading42"></a>Toplu alma
Tek bir işlemde bir kuyruktan too32 iletilerini geri alabilirsiniz. Bu gidiş-dönüş hello sayısını mobil cihazlar gibi ortamlar için özellikle yararlıdır hello istemci uygulamasından gelen yüksek gecikme süresiyle azaltabilir.  

### <a name="subheading43"></a>Sıra yoklama aralığı
Bu uygulama için hareketlerinin hello en büyük kaynaklarından biri olabilir bir kuyruktan iletileri için uygulamaların çoğu yoklar. Yoklama aralığı akıllıca seçin: çok sık yoklama neden olabilir, uygulama tooapproach hello ölçeklenebilirlik hedefleri hello sıra için. Ancak, (yazma hello zamanında) $0,01 için 200.000 işlemleri sırasında bir ay boyunca her saniye kadar Maliyet değerinden 15 Sent maliyeti sonra yoklama tek bir işlemcinin genellikle seçiminizi yoklama aralığı etkileyen bir faktör değil.  

Güncel maliyet bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/).  

### <a name="subheading44"></a>UpdateMessage
Kullanabileceğiniz **UpdateMessage** tooincrease hello görünmezlik zaman aşımı veya tooupdate durumu bilgilerini bir ileti. Bu güçlü olmakla birlikte, her unutmayın **UpdateMessage** işlemi hello ölçeklenebilirlik hedef sayar. Ancak, bu her adım hello işin tamamlandı olarak bir iş bir kuyruk toohello ardından, geçirmeden bir iş akışı sahip daha çok daha verimli bir yaklaşım olabilir. Hello kullanarak **UpdateMessage** işlemi uygulama toosave hello iş durumu toohello iletinizi sağlar ve sonra yeniden kuyruğa alma selamlama iletisine bir adım tamamlandıktan her zaman hello işin sonraki adımınız hello yerine çalışmaya devam edin.  

Daha fazla bilgi için hello makalesine bakın [nasıl yapılır: hello kuyruğa alınan iletinin içeriğini değiştirme](storage-dotnet-how-to-use-queues.md#change-the-contents-of-a-queued-message).  

### <a name="subheading45"></a>Uygulama mimarisi
Uygulama Mimarinizi ölçeklenebilir sıraları toomake kullanmanız gerekir. Merhaba aşağıdaki sıralar toomake uygulamanız daha ölçeklenebilir kullanabilir bazı yollarını listeler:  

* Uygulamanızda iş yükleri kesintisiz ve işleme için iş sıraları toocreate biriktirme listelerini kullanın. Örneğin, karşıya yüklenen görüntüleri yeniden boyutlandırma gibi kullanıcıların tooperform işlemci yoğun iş gelen istekleri yukarı sıraya.
* Böylece, bağımsız olarak ölçeklendirebilirsiniz sıraları toodecouple uygulamanızın parçalarını kullanabilirsiniz. Örneğin, bir web ön uç anket sonuçlarını kullanıcılardan sonraki çözümleme ve depolama için bir sıra yerleştirin. Daha fazla çalışan rolü örnekleri tooprocess sıra verileri gereken şekilde hello ekleyebilirsiniz.  

## <a name="conclusion"></a>Sonuç
Bu makalede hello en yaygın bazıları Azure Storage kullanırken performansını iyileştirmek için yöntemler kanıtlanmış açıklanmıştır. Biz her uygulama Geliştirici tooassess her hello yöntemler yukarıda karşı kendi uygulama teşvik edin ve hello önerileri tooget Azure depolama kullanan uygulamaları için harika performans üzerinde hareket göz önünde bulundurun.

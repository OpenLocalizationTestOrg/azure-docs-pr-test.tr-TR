---
title: "aaaAzure Media parçalanmış MP4 live Services alma belirtimi | Microsoft Docs"
description: "Bu belirtimi hello protokolü ve parçalanmış MP4 tabanlı canlı akış alımı için Azure Media Services biçimini açıklar. Merhaba bulut platformu olarak Azure kullanarak gerçek zamanlı içeriği yayını ve Azure Media Services toostream Canlı olayları kullanın. Bu belge, ayrıca en iyi anlatılmaktadır Canlı yüksek oranda yedekli ve sağlam oluşturmaya yönelik yöntemler mekanizmaları alma."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 43fac263-a5ea-44af-8dd5-cc88e423b4de
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 0c191f8d6c5a595621feaba0e571fb984b666f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-fragmented-mp4-live-ingest-specification"></a>Azure Media Services parçalanmış MP4 Canlı belirtimi alma
Bu belirtimi hello protokolü ve parçalanmış MP4 tabanlı canlı akış alımı için Azure Media Services biçimini açıklar. Media Services müşteriler toostream Canlı olayları kullanmak ve içeriği gerçek zamanlı olarak hello bulut platform Azure kullanarak yayını bir canlı akış hizmeti sağlar. Bu belge, ayrıca en iyi anlatılmaktadır Canlı yüksek oranda yedekli ve sağlam oluşturmaya yönelik yöntemler mekanizmaları alma.

## <a name="1-conformance-notation"></a>1. Uygunluk gösterimi
Merhaba anahtar sözcükleri "gerekir," "BULUNMAMALIDIR değil," "Gerekli", "SHALL," "OLACAKTIR," "SHOULD," "Olmamalıdır," "Önerilen", "Olabilir," ve bu belgedeki "isteğe bağlı" RFC 2119 anlatıldığı gibi yorumlanan toobe markalarıdır.

## <a name="2-service-diagram"></a>2. Hizmet diyagramı
Merhaba Aşağıdaki diyagramda hello üst düzey mimarisini hello canlı akış Media Services hizmetinde gösterir:

1. Gerçek zamanlı Kodlayıcı hello Azure Media Services SDK'sı ile oluşturulan ve sağlanan Canlı akışlar toochannels iter.
2. Kanallar, programları ve tüm hello canlı akış işlevlerini; alma biçimlendirme, dahil olmak üzere, Media Services tanıtıcı akış uç noktalarını DVR, güvenlik, ölçeklenebilirlik ve artıklık bulut.
3. İsteğe bağlı olarak, müşteriler hello akış uç noktası ve hello istemci uç noktaları arasındaki bir Azure içerik teslim ağı katmanı toodeploy seçebilirsiniz.
4. HTTP Uyarlamalı akış protokolleri kullanarak akış uç noktası hello istemci uç noktaları akıştan. Microsoft kesintisiz akış, dinamik Uyarlamalı akış HTTP (tire veya MPEG-DASH) ve Apple HTTP canlı akışı (HLS) üzerinden örnekler.

![Akış alma][image1]

## <a name="3-bitstream-format--iso-14496-12-fragmented-mp4"></a>3. Bitstream biçimi – ISO 14496-12 parçalanmış MP4
Canlı akış alma için hello kablo biçiminde ele bu belgeyi [ISO-14496-12] dayanır. Ayrıntılı açıklaması parçalanmış MP4 biçimindeki ve hem uzantıları için isteğe bağlı video dosyaları ve canlı akış alımı için bkz: [[MS-SSTR]](http://msdn.microsoft.com/library/ff469518.aspx).

### <a name="live-ingest-format-definitions"></a>Canlı biçim tanımlarını alma
Merhaba aşağıdaki listede Azure Media Services'e toolive uygulamak tanımları alma özel biçim açıklanmaktadır:

1. Hello **ftyp**, **Canlı sunucusu bildirim kutusu**, ve **moov** her istek (HTTP POST) ile kutuları gönderilir. Bu kutuları hello hello akış başlangıcında gönderilmelidir ve alma dilediğiniz zaman hello Kodlayıcı tooresume akışı yeniden bağlanmanız gerekir. Daha fazla bilgi için bkz: Bölüm 6 [1].
2. [1] 3.3.2 bölümünde tanımlar adlı isteğe bağlı bir kutu **StreamManifestBox** için Canlı alma. Toohello yönlendirme mantığını hello Azure yük dengeleyici, bu kutusunu kullanarak kullanım dışıdır. Merhaba kutusunu Media Services'e alındıktan olduğunda mevcut olmamalıdır. Bu kutu mevcut değilse, Media Services sessizce onu yok sayar.
3. Merhaba **TrackFragmentExtendedHeaderBox** 3.2.3.2 [1] içinde tanımlı kutusunu her parçası için mevcut olmalıdır.
4. Sürüm 2 hello **TrackFragmentExtendedHeaderBox** kutusunu birden çok veri merkezlerinde aynı URL'lere sahip kullanılan toogenerate ortam kesimleri olması gerekir. Merhaba parça dizini dizin tabanlı akış biçimlerine Apple HLS gibi çapraz veri merkezi yük devretme için gerekli ve dizin tabanlı MPEG-DASH alanıdır. tooenable arası veri merkezi yük devretme, hello parça dizin arasında birden çok kodlayıcılar eşitlenen gerekir ve her art arda medya parçası için 1 tarafından bile Kodlayıcı yeniden başlatmalar veya hatalar arasında artırılması.
5. [1] 3.3.6 bölümünde tanımlar adlı bir kutusu **MovieFragmentRandomAccessBox** (**mfra**) hello Canlı alım tooindicate akış uç (EOS) toohello kanal sonunda gönderilebilir. Son toohello alma Media Services mantığını EOS kullanarak kullanım dışıdır ve hello **mfra** Canlı alım gönderilmez için kutusu. Gönderilen, Media Services sessizce onu yok sayar. Merhaba tooreset hello durumunu alma noktası, kullanmanızı öneririz [kanal sıfırlama](https://docs.microsoft.com/rest/api/media/operations/channel#reset_channels). Ayrıca, kullanmanızı öneririz [programı durdurun](https://msdn.microsoft.com/library/azure/dn783463.aspx#stop_programs) tooend sunu ve akış.
6. Merhaba MP4 parça süresi sabit hello istemci bildiriminin tooreduce hello boyutu. Bir sabit MP4 parça süre yineleme etiketlerin hello kullanılarak istemci indirme buluşsal yöntemler de geliştirir. Merhaba süresi tamsayı olmayan kare hızları toocompensate dalgalanma.
7. Merhaba MP4 parça süresi yaklaşık 2-6 saniye arasında olmalıdır.
8. MP4 parçalara zaman damgaları ve dizinleri (**TrackFragmentExtendedHeaderBox** `fragment_ absolute_ time` ve `fragment_index`) artan düzende ulaşması. Media Services dayanıklı tooduplicate parçaları olsa da, toohello medya zaman çizelgesi göre özelliği tooreorder parçaları sınırlıdır.

## <a name="4-protocol-format--http"></a>4. Protokol biçimi – HTTP
ISO parçalanmış MP4 tabanlı Canlı Media Services parçalanmış MP4 biçimi toohello hizmetinde paketlenmiş bir standart uzun süre çalışan HTTP POST isteği kodlanmış tootransmit medya verilerini kullanan için alma. Her HTTP POST tamamı parçalanmış MP4 bitstream ("akış"), üstbilgi kutuları ile Merhaba başından başlayarak gönderir (**ftyp**, **Canlı sunucusu bildirim kutusu**, ve **moov** kutuları) ve parçaları bir dizi devam (**moof** ve **mdat** kutuları). Merhaba HTTP POST isteği için URL sözdizimi için 9.2 in [1] bölümüne bakın. Merhaba gönderme URL'sini örneğidir: 

    http://customer.channel.mediaservices.windows.net/ingest.isml/streams(720p)

### <a name="requirements"></a>Gereksinimler
Ayrıntılı gereksinimler hello şunlardır:

1. Merhaba Kodlayıcı ile boş bir HTTP POST isteği göndererek yayın hello başlamanız gerekir "body kullanarak" (içerik uzunluğu sıfır) hello aynı alım URL. Bu, hızlı bir şekilde tespit hello Canlı alım uç noktanın geçerli olup olmadığını ve herhangi bir kimlik doğrulaması ya da gereken diğer koşulları varsa hello Kodlayıcı yardımcı olabilir. HTTP protokolü hello sunucu Hello hello POST gövde dahil olmak üzere tüm istek alınana kadar bir HTTP yanıtının geri gönderemez. Bu adım, hello Kodlayıcı olmadan canlı bir olay hello uzun süre çalışan yapısını verilen tüm hello veri gönderme sonlanana kadar mümkün toodetect herhangi bir hata olmayabilir.
2. Merhaba Kodlayıcı herhangi bir hata veya kimlik doğrulama sınaması (1) nedeniyle işlemesi gerekir. Varsa (1) başarılı bir 200 yanıt ile devam edin.
3. Merhaba Kodlayıcı yeni bir HTTP POST isteği hello parçalanmış MP4 akışı ile başlamalıdır. Merhaba yükü parçaları tarafından izlenen hello üstbilgi kutuları ile başlamalıdır. Bu hello Not **ftyp**, **Canlı sunucusu bildirim kutusu**, ve **moov** (bu sırayla) kutuları gönderileceği her bir istekle hello Kodlayıcı, çünkü yeniden bağlanmanız gerekir olsa bile hello Önceki istek önceki toohello hello akışın sonuna sonlandırıldı. 
4. Hello Kodlayıcı öbekli aktarım kodlamasını yüklemek için kullanmak için mümkün olmayan toopredict hello tüm içerik uzunluğu hello olduğundan canlı olay gerekir.
5. Merhaba olay üzerinden, hello son parçası, gönderdikten sonra olduğunda hello Kodlayıcı düzgün biçimde hello öbekli aktarım kodlamasını (çoğu HTTP istemci yığınları, otomatik olarak işlemek) ileti sırası bitmelidir. Merhaba Kodlayıcı hello servis tooreturn hello son yanıt kodu için bekleyin ve hello bağlantı sonlandırılacak. 
6. Hello Kodlayıcı gerekir kullanmak hello `Events()` 9.2 in [1] Media Services içine Canlı alımı için açıklanan isim.
7. Merhaba HTTP POST isteği sonlandırır veya saatler dışarı hello Akış TCP hata önceki toohello sonu ile Merhaba Kodlayıcı gerekir yeni bir bağlantı kullanarak yeni bir POST isteği gönderin ve hello gereksinimleri önceki izleyin varsa. Ayrıca, hello Kodlayıcı gerekir hello hello akıştaki her izlemek için önceki iki MP4 parçasının yeniden gönderin ve hello medya zaman çizelgesinde süreksizlik oluşturmaksızın sürdürün. Son iki MP4 parçaları her parçasının Hello göndermeden, veri kaybı olmasını sağlar. Diğer bir deyişle, ses ve video izleme bir akış içeriyor ve hello geçerli POST isteği başarısız olursa, hello Kodlayıcı yeniden bağlanmanız gerekir ve yeniden gönder hello daha önce başarıyla gönderildi, son iki parça hello ses izlemek için ve için hello son iki parça daha önce başarıyla olan hello video izi gönderilen, veri kaybı olduğundan tooensure. Merhaba Kodlayıcı bağlandığında, onu yeniden gönderir medya parçasının "İleri" bir arabellek bulundurmanız gerekir.

## <a name="5-timescale"></a>5. Zaman Çizelgesi
[[MS-SSTR] ](https://msdn.microsoft.com/library/ff469518.aspx) ilişkin zaman ölçeğini hello kullanımını açıklar **SmoothStreamingMedia** (Bölüm 2.2.2.1) **StreamElement** (Bölüm 2.2.2.3) **StreamFragmentElement**(2.2.2.6 bölüm) ve **LiveSMIL** (Bölüm 2.2.7.3.1). Merhaba ölçeği değer yoksa, kullanılan hello varsayılan değeri 10,000,000 (10 MHz) kullanılır. Hello kesintisiz akış biçim belirtimi diğer ölçeği değerleri kullanımını engellemez rağmen çoğu Kodlayıcı uygulamaları bu varsayılan kullanmak değeri (10 MHz) toogenerate kesintisiz akış veri alın. Son toohello [Azure medya dinamik paketleme](media-services-dynamic-packaging-overview.md) özelliği, öneririz, 90 KHz ölçeği video akışları ve 44,1 KHz veya 48.1 KHz ses akışları için kullanmanızı. Farklı bir zaman ölçeğine göre değerleri için farklı akışları kullandıysanız, hello akış düzeyi ölçeği gönderilmelidir. Daha fazla bilgi için bkz: [[MS-SSTR]](https://msdn.microsoft.com/library/ff469518.aspx).     

## <a name="6-definition-of-stream"></a>6. "Akış" tanımı
Akış işleme akış yük devretme ve artıklık senaryoları hello temel Canlı sunuları oluşturma için Canlı alım işlemde birimidir. Akış, tek bir parça içerebilecek bir benzersiz, parçalanmış MP4 bitstream veya birden çok parçaları tanımlanır. Tam canlı sunu hello gerçek zamanlı kodlayıcılar hello yapılandırmasına bağlı olarak bir veya daha fazla akışlar içerebilir. Örnek hello tam canlı sunu akışları toocompose kullanmanın çeşitli seçenekler gösterilmektedir.

**Örnek:** 

Bir müşteri toocreate ses/video bit aşağıdaki hello içeren canlı akış sunu istiyor:

Video – 3000 KB/sn, 1500 KB/sn, 750 KB/sn

Ses – 128 Kb/sn

### <a name="option-1-all-tracks-in-one-stream"></a>Seçenek 1: Tüm parçaları bir akış
Bu seçenek, tek bir kodlayıcı tüm ses/video parçalar oluşturur ve bunları bir parçalanmış MP4 bitstream sunmaktadır. Merhaba parçalanmış MP4 bitstream tek bir HTTP POST bağlantısı üzerinden gönderilir. Bu örnekte, bu canlı sunu için yalnızca bir akış yoktur.

![Akışlar bir izleme][image2]

### <a name="option-2-each-track-in-a-separate-stream"></a>Seçenek 2: Ayrı akıştaki her izleme
Bu seçenek hello Kodlayıcı bir izleme her parça MP4 bitstream yerleştirir ve tüm hello akışları ayrı HTTP bağlantıları üzerinden gönderir. Bu, birden çok kodlayıcılar veya bir kodlayıcı ile yapılabilir. Merhaba Canlı alım bu canlı sunu dört akışları olarak görür.

![Akışlar ayrı izler][image3]

### <a name="option-3-bundle-audio-track-with-hello-lowest-bitrate-video-track-into-one-stream"></a>Seçenek 3: Paket ses izleme hello düşük bit hızlı video izleme bir akışa
Bu seçenekte, hello müşteri toobundle hello ses izleme hello düşük bit hızlı video İzle bir parça MP4 bitstream'ile ve bırakın hello diğer iki video parçaları ayrı akış olarak seçer. 

![Akışlar ses ve video izler][image4]

### <a name="summary"></a>Özet
Bu örneğin tüm olası alım seçenekleri kapsamlı bir listesi değil. Gibi bir matter, hatta herhangi bir gruplama akışları içine parçalarının Canlı alım tarafından desteklenir. Müşteriler ve Kodlayıcı satıcılar mühendislik karmaşıklık, kodlayıcı kapasite ve artıklık ve yük devretme konuları göre kendi uygulamaları seçebilirsiniz. Ancak, çoğu durumda, hello tüm canlı sunu için yalnızca bir ses izleme yoktur. Bu nedenle, önemli tooensure hello healthiness Merhaba, hello ses izleme içeren akışı alma. Bu faktör genellikle kendi akış (seçenek 2) olduğu gibi hello ses izleme almadan veya hello düşük bit hızlı video İzle (olduğu gibi seçeneği 3) ile paketleme sonuçlanır. Ayrıca, daha iyi yedeklik ve hataya dayanıklılık için gönderme hello aynı ses İzle iki farklı akışlar (yedekli ses izleri seçeneği 2)'ya da en az iki hello düşük bit hızlı video izler (seçenek 3, paketlenmiş sesle paket hello ses İzle en az iki video akışları) için Canlı önerilir medya Hizmetleri içine alın.

## <a name="7-service-failover"></a>7. Hizmet yük devretmesi
Canlı akış hello yapısı iyi yük devretme desteği hello hello hizmetinin kullanılabilirliğini sağlamak için önemlidir. Media Services çeşitli hatalar, ağ hataları, sunucu hataları ve depolama sorunları da dahil olmak üzere tasarlanmış toohandle olduğu. Müşteriler, hello gerçek zamanlı Kodlayıcı taraftaki uygun yük devretme mantığı ile birlikte kullanıldığında, yüksek oranda güvenilir bir canlı akış hizmeti hello buluttan elde edebilirsiniz.

Bu bölümde, hizmet bir yük devretme senaryosu açıklanmaktadır. Bu durumda, hello hatası hello hizmet içinde herhangi bir yerde olur ve bir ağ hatası çıkmaktadır. Hizmet yük devretmesi işlemek için hello Kodlayıcı uygulaması için bazı öneriler şunlardır:

1. 10 saniyelik zaman aşımı hello TCP bağlantısı kurmak için kullanın. Bir deneme tooestablish hello bağlantı 10 saniyeden uzun sürerse, hello işlemi durdurmak ve yeniden deneyin. 
2. Kısa bir zaman aşımı hello HTTP istek iletisi öbekleri göndermek için kullanın. Merhaba hedef MP4 parça süresi N saniye ise, N ve 2 N saniye arasında gönderilen zaman aşımı kullanın; Merhaba MP4 parça süresi 6 saniye ise, örneğin, bir zaman aşımı süresi 6 too12 saniye kullanın. Zaman aşımı meydana gelirse, sıfırlama hello bağlantısı, açık yeni bir bağlantı ve sürdürme akış hello yeni bağlantıda alma. 
3. Başarılı bir şekilde ve tamamen toohello hizmet gönderilen hello son iki parça her parçasının sahip çalışırken bir arabellek korur.  Hello HTTP POST isteği bir akış için sonlandırılır veya önceki toohello hello akışın sonuna zaman, yeni bir bağlantı açmak ve başka bir HTTP POST isteği başlatmak, hello akış üstbilgileri yeniden, her izleme için son iki parça hello yeniden ve hello akış olmadan devam Merhaba medya zaman çizelgesinde süreksizlik tanışın. Bu, veri kaybı hello olasılığını azaltır.
4. Bu hello Kodlayıcı hello yeniden deneme tooestablish bağlantı sayısını sınırlamaz veya TCP hata oluştuktan sonra akış sürdürme öneririz.
5. TCP hatasından sonra:
  
    a. Merhaba geçerli bağlantının kapatılması gerekir ve yeni bir bağlantı için yeni bir HTTP POST isteği oluşturulması gerekir.

    b. Yeni HTTP POST URL olmalıdır hello hello ilk gönderme URL'sini hello aynı.
  
    c. Merhaba yeni HTTP POST içermelidir akış üstbilgileri (**ftyp**, **Canlı sunucusu bildirim kutusu**, ve **moov** kutuları) aynı toohello akış hello üstbilgilerinde olan ilk POST.
  
    d. her parça için gönderilen hello son iki parça gönderilmesi gerekir ve akış hello medya zaman çizelgesinde süreksizlik oluşturmaksızın çıkmalıdır. Merhaba MP4 parça zaman damgaları sürekli olarak bile HTTP POST istekleri artırmanız gerekir.
6. Merhaba MP4 parça süresiyle orantılı bir hızda veri gönderilmiyor varsa hello Kodlayıcı hello HTTP POST isteği sonlanmalıdır.  Veri göndermediğini bir HTTP POST isteği Media Services hızlı bir şekilde hello Kodlayıcısı hello olayı bir hizmeti güncelleştirme ile bağlantıyı kesme gelen engelleyebilir. Bu nedenle, HTTP POST için hello seyrek (ad sinyali) parçaları olmalıdır kısa süreli hello seyrek parça gönderilen hemen sonlandırılıyor.

## <a name="8-encoder-failover"></a>8. Kodlayıcı yük devretme
Kodlayıcı yük devretme hello ikinci ele toobe uçtan uca canlı akış halinde teslim için gereken yük devretme senaryosu türüdür. Bu senaryoda, hello hata koşulu hello Kodlayıcı tarafında gerçekleşir. 

![Kodlayıcı yük devretme][image5]

Kodlayıcı yük devretme gerçekleştiğinde beklentilerini aşağıdaki hello hello Canlı alım uç noktasından Uygula:

1. Yeni bir kodlayıcı örnek toocontinue akış ' hello diyagramında (3000 k kesikli çizgi ile video için akış) gösterildiği şekilde oluşturulmalıdır.
2. Kullanım aynı hello gerekir hello URL'si için HTTP POST istekleri hello yeni Kodlayıcı örneği başarısız oldu.
3. Merhaba yeni Kodlayıcı'nın POST isteği hello içermelidir aynı başarısız örneği hello gibi MP4 üstbilgi kutuları parçalanmış.
4. Merhaba yeni Kodlayıcı, düzgün şekilde Hello aynı canlı sunu toogenerate eşitlenen hizalanmış parça sınırlarla ses/video örnekleri için diğer tüm çalışır kodlayıcılarda eşitlenen gerekir.
5. Merhaba yeni akış hello önceki akışıyla anlam olarak eşdeğer olmalıdır ve hello başlığı ve parça düzeylerinde değiştirilebilir.
6. Merhaba yeni Kodlayıcı toominimize veri kaybı denemelisiniz. Merhaba `fragment_absolute_time` ve `fragment_index` ortam parçaları hello Kodlayıcı son durduğu hello noktasından artırmanız gerekir. Merhaba `fragment_absolute_time` ve `fragment_index` sürekli bir biçimde artırmanız gerekir, ancak izin verilen toointroduce süreksizlik, gerekirse değil. Merhaba medya zaman çizelgesinde toointroduce discontinuities daha parçaları göndermeden, hello tarafında daha iyi tooerr olacak şekilde Media Services, daha önce alındı ve işlenen, parça yok sayar. 

## <a name="9-encoder-redundancy"></a>9. Kodlayıcı artıklık
Bazı önemli olayları isteğe bağlı daha yüksek kullanılabilirlik ve kaliteli bir deneyim, veri kaybı ile aktif-aktif yedekli kodlayıcılar tooachieve sorunsuz yük devretme kullanın öneririz, dinamik.

![Kodlayıcı artıklık][image6]

Bu diyagramda gösterildiği gibi kodlayıcılar iki grupları her akış iki kopyasını hello Canlı hizmetinde aynı anda iletin. Media Services akışı kimliği ve parçası zaman damgasını göre yinelenen parçaları filtrelemenize çünkü bu kurulumu desteklenir. Sonuçta elde edilen canlı akış hello ve Arşiv hello en iyi olası toplama hello iki kaynaklardan olan tek bir kopyasını tüm hello akışları olur. Bir kodlayıcı (toobe hello aynı yok) var olduğu sürece Örneğin, kuramsal bir olağanüstü durumda, belirli bir anda her akış için zaman hello canlı akış hello hizmetinden kaynaklanan veri kaybı olmadan sürekli çalışıyor. 

Bu senaryo için Hello gereksinimleri neredeyse aynı hello gereksinimleri hello "Kodlayıcı yük devretme" durumda olarak Merhaba, hello ikinci kodlayıcılar kümesi hello çalıştıran hello özel durum ile aynı birincil kodlayıcılar hello gibi saat.

## <a name="10-service-redundancy"></a>10. Hizmet artıklık
Yüksek oranda yedekli genel dağıtım için bazen çapraz bölge yedekleme toohandle bölgesel afetler olması gerekir. Merhaba "Kodlayıcı artıklık" topolojisine genişleterek, müşterilerin toohave yedekli hizmet dağıtımı hello ikinci kodlayıcılar kümesiyle bağlı farklı bir bölgede seçebilirsiniz. Müşterileri de çalışabilir bir içerik teslim ağı sağlayıcısı toodeploy hello iki hizmet dağıtımları tooseamlessly rota istemci trafiğini önünde genel bir Traffic Manager ile. Merhaba kodlayıcılar Hello gereksinimleri "Kodlayıcı artıklık" durum hello aynı hello değildir. Merhaba yalnızca hello ikinci kodlayıcılar gereksinimlerini toobe kümesi tooa farklı Canlı işaret istisnadır uç noktasını alın. Merhaba Aşağıdaki diyagramda bu kurulum gösterilmektedir:

![Hizmet artıklık][image7]

## <a name="11-special-types-of-ingestion-formats"></a>11. Özel türde alım biçimleri
Bu bölümde tasarlanmış toohandle belirli senaryolar Canlı alım biçimlerinin özel türleri açıklanmaktadır.

### <a name="sparse-track"></a>Seyrek İzle
Bir zengin istemci deneyimi ile canlı akış sunu genellikle, gerekli tootransmit zaman eşitlenmiş olayı veya bant dışı hello ana medya verilerle işaret eder. Bu dinamik Canlı reklam ekleme örneğidir. Bu tür olay sinyal seyrek doğası nedeniyle akış normal ses/video farklıdır. Diğer bir deyişle, verileri genellikle sürekli olarak gerçekleşmez ve başlangıç aralığı sabit toopredict olabilir sinyal hello. seyrek izleme Hello kavramı tasarlanmış tooingest ve yayını bant sinyal verileri oluştu.

Merhaba aşağıdaki adımları seyrek izleme alma için önerilen uygulama şunlardır:

1. Ses/video parçaları olmadan yalnızca seyrek parçaları içeren ayrı bir parçalanmış MP4 bitstream oluşturun.
2. Merhaba, **Canlı sunucusu bildirim kutusu** [1] Bölüm 6'tanımlandığı gibi hello kullanmak *parentTrackName* hello üst parçanın parametre toospecify hello adı. [1] 4.2.1.2.1.2 bölümünde daha fazla bilgi için bkz.
3. Merhaba, **Canlı sunucusu bildirim kutusu**, **manifestOutput** çok ayarlanmalıdır**true**.
4. Olayı sinyali hello seyrek yapısını Hello verildiğinde, hello şunları öneririz:
   
    a. Merhaba canlı olay Hello başında hello Kodlayıcı hello ilk üstbilgi kutuları hello istemci bildiriminde hello hizmet tooregister hello seyrek izleme sağlayan toohello hizmeti, gönderir.
   
    b. Veri gönderilmiyor zaman hello Kodlayıcı hello HTTP POST isteği sonlanmalıdır. Veri göndermediğini uzun süre çalışan HTTP POST Media Services hızlı bir şekilde hello Kodlayıcısı hello olayı bir hizmeti güncelleştirme veya sunucu yeniden başlatma ile bağlantıyı kesme gelen engelleyebilir. Bu durumlarda, hello medya sunucusu hello yuvada alma işleminde geçici olarak engellendi.
   
    c. Veri sinyal kullanılabilir olmadığında hello süre boyunca hello Kodlayıcı hello HTTP POST isteği kapatmanız gerekir. Merhaba POST isteği etkinken hello Kodlayıcı veri göndermesi gerekir.

    d. Kullanılabilir durumdaysa hello Kodlayıcı seyrek parçaları gönderirken, açık bir content-length üstbilgisi ayarlayabilirsiniz.

    e. Yeni bir bağlantıyla seyrek parçaları gönderirken hello Kodlayıcı hello yeni parçaları tarafından izlenen hello üstbilgi kutularından gönderme başlamanız gerekir. Bu durumlar için hangi yük devretme kümesinde ortası olur ve hello yeni seyrek bağlantı hello seyrek izleme önce görmediği kurulan tooa yeni sunucu yapılıyor.

    f. eşit veya daha büyük bir zaman damgası değeri olan hello karşılık gelen üst parça parça kullanılabilir toohello istemci yapıldığında hello seyrek parça parça kullanılabilir toohello istemci haline gelir. Bir zaman damgası t Hello seyrek parça varsa, 1000, örneğin, =, "video" ("video" Merhaba üst parça adı olduğunu varsayarak) parçalara zaman damgası 1000 veya sonrasını, indirebilirsiniz hello istemci görür sonra hello seyrek parça t bekleniyor = 1000. Gerçek sinyal hello Not hello sunu zaman çizelgesi farklı bir konuma için belirlenen amacı için kullanılabilir. Bu örnekte, t seyrek parçasını hello olası kullanıcının = 1000 olan birkaç saniye olan bir konuma bir ad eklemek için bir XML yükü daha sonra.

    g. seyrek parça parça Hello yükünü hello senaryo bağlı olarak (örneğin, XML, metin veya ikili), farklı biçimlerde olabilir.

### <a name="redundant-audio-track"></a>Yedek ses İzle
Tipik bir HTTP Uyarlamalı akış senaryoda (örneğin, kesintisiz akış veya tire), genellikle var. hello sunu içinde yalnızca bir ses İzle Merhaba hello ses parçası içeren hello akış alımı bozulsa bile hata koşullarında hello istemci toochoose için birden çok kalitesi düzeylerini olan video parçaları tek hata noktası hello ses parçası olabilir. 

Bu sorun, Media Services destekleyen toosolve dinamik yedek ses izleri alım. Merhaba, aynı ses izleme birden çok kez farklı akış gönderilebilir bu hello olur. Hello hizmeti yalnızca hello ses izleme kez hello istemci bildirimini kaydeder rağmen hello birincil ses izleme sorunlar varsa, ses parçaları almak için bu yedek ses izleri yedek olarak kullanabilirsiniz. tooingest yedek ses izleri, hello Kodlayıcı gerekir:

1. Aynı ses izlemek hello birden çok parçadaki MP4 bitstreams oluşturun. Merhaba yedekli ses izleri anlam olarak eşdeğer olmalıdır, hello aynı zaman damgaları parçalara ile Merhaba başlığı ve parça düzeylerinde değiştirilebilir.
2. Bu hello "ses" girişi sağlamak hello Canlı sunucu bildirimi (Bölüm 6 [1].) olan hello aynı için tüm gereksiz ses izleri.

uygulaması aşağıdaki hello için yedek ses izleri önerilir:

1. Her benzersiz ses izleme tek başına bir akışa gönderin. Ayrıca, her burada hello ikinci akış farklı hello ilk hello HTTP POST URL hello tanımlayıcısı tarafından yalnızca bu ses izleme akışlar için yedek bir akış gönder: {protokol} :// {sunucu adresi} / {noktası path}/Streams({identifier}) yayımlama.
2. Ayrı akışları toosend hello iki düşük video bit kullanın. Her bu akışlar benzersiz her ses izleme bir kopyasını da içermelidir. Örneğin, birden fazla dili desteklendiğinde, bu akışları her dil için ses izleri içermelidir.
3. Ayrı bir sunucu (kodlayıcı) örnekleri tooencode kullanın ve belirtilen hello yedekli akışlar (1) ve (2) gönderin. 

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[image1]: ./media/media-services-fmp4-live-ingest-overview/media-services-image1.png
[image2]: ./media/media-services-fmp4-live-ingest-overview/media-services-image2.png
[image3]: ./media/media-services-fmp4-live-ingest-overview/media-services-image3.png
[image4]: ./media/media-services-fmp4-live-ingest-overview/media-services-image4.png
[image5]: ./media/media-services-fmp4-live-ingest-overview/media-services-image5.png
[image6]: ./media/media-services-fmp4-live-ingest-overview/media-services-image6.png
[image7]: ./media/media-services-fmp4-live-ingest-overview/media-services-image7.png

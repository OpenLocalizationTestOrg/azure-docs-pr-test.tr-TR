---
title: "Machine Learning Studio'da aaaUse hello örnek veri kümesi | Microsoft Docs"
description: "Machine Learning Studio'da bulunan örnek modelleri kullanılan hello veri kümeleri açıklamaları. Bu örnek veri kümeleri denemelerinizi için kullanabilirsiniz."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 03a0b844-e8a7-4896-996f-d3c7a0db7a50
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: c7786478db82d40aaf27c37b3947ded5f042dd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-sample-datasets-in-azure-machine-learning-studio"></a>Azure Machine Learning Studio'da Hello örnek veri kümesi kullanın
[top]: #machine-learning-sample-datasets

Örnek veri kümelerini ve denemeleri sayısı, Azure Machine Learning ile yeni bir çalışma alanı oluşturduğunuzda, varsayılan olarak dahil edilir. Bu örnek veri kümelerini çoğunu hello örnek hello modellerinde tarafından kullanılan [Azure Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com/). Diğer çeşitli genellikle machine learning'de kullanılan veri türlerine örnek olarak dahil edilir.

Bu veri kümeleri bazıları, Azure Blob Depolama alanında kullanılabilir. Bu veri kümeleri için aşağıdaki tablonun hello doğrudan bir bağlantı sağlar. Hello kullanarak bu veri kümeleri, denemeler kullanabileceğiniz [veri içeri aktarma] [ import-data] modülü.

Bu örnek veri kümelerini Hello kalan kullanılabilir altında çalışma alanınızdaki **kaydedilen veri kümeleri** hello modül paleti toohello açtığınızda veya Machine Learning Studio'da yeni bir deneme oluşturma hello deneme tuvalinin sol.
Bu veri kümeleri birini tooyour deneme tuvalinin sürükleyerek kendi deney kullanabilirsiniz.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<table>

<tr>
  <th align=left>Veri kümesi adı</th>
  <th align=left>Veri kümesi tanımı</th>
</tr>

<tr>
  <td valign=top>Yetişkin Census gelir ikili sınıflandırma veri kümesi</td>
  <td valign=top>
Bir alt kümesini 16 hello yaş > 100 ayarlandı geliri dizini ile üzerinden çalışma yetişkinler kullanarak hello 1994 Census veritabanı.<p> </p><b>Kullanım:</b> üzerinde 50 K yılda bir kişinin kazandığı olup olmadığını demografisine toopredict'ı kullananların sınıflandırmak.<p> </p><b>İlgili araştırma:</b> Kohavi, r, Becker, b, (1996). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi </td>
</tr>

<tr ID=airport-codes-dataset>
  <td valign=top>Havaalanı kodları veri kümesi</td>
  <td valign=top>
ABD havaalanı kodları.<p> </p>Bu veri kümesi hello havaalanı kimlik numarasını ve hello konumu Şehir ve bölge ile birlikte ad sağlayan her ABD havaalanı için bir satır içerir.
  </td>
</tr>

<tr>
  <td valign=top>Otomobil fiyat verileri (ham)</td>
  <td valign=top>
Tarafından otomobiller hakkında bilgi marka ve model, hello fiyat de dahil olmak üzere, silindir ve MPG yanı sıra, bir sigorta risk puanı hello sayısı gibi özellikler.<p> </p>Merhaba risk puanı otomatik fiyatıyla başlangıçta ilişkilendirilir ve tooactuaries symboling olarak bilinen bir işlemle gerçek risk için ayarlanmış. + 3 arası değerini hello otomatik risklidir ve -3 değeri olan büyük olasılıkla güvenlidir gösterir.<p> </p><b>Kullanım:</b> tahmin hello risk puanı regresyon veya multivariate sınıflandırma kullanarak özellik tarafından. <p> </p><b>İlgili araştırma:</b> Schlimmer, J.C. (1987). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi </td>
</tr>

<tr ID=bike-rental-uci-dataset>
  <td valign=top>Bisiklet kiralama UCI veri kümesi</td>
  <td valign=top>
Gerçek veri Washington DC bir bisiklet kiralama ağda tutar sermaye Bikeshare şirketten dayalı UCI bisiklet kiralama veri kümesi.<p> </p>Hello dataset 17,379 satırların toplam 2011 ve 2012, her gün için her saat için bir satır vardır. 1 too977 Hello saatlik bisiklet kiralamaları aralığıdır.

  </td>
</tr>

<tr ID=bill-gates-rgb-image>
  <td valign=top>Fatura geçitleri RGB görüntüsü</td>
  <td valign=top>
Genel kullanıma açık görüntü dosyası tooCSV veri dönüştürülür.<p> </p>Merhaba hello görüntüyü dönüştürme için kod hello sağlanır <strong>renk K-ortalamaları kümeleme kullanarak boyutlandırma</strong> modeli ayrıntı sayfası.
  </td>
</tr>

<tr>
  <td valign=top>Kan Bağış veri</td>
  <td valign=top>
Bir veri alt kümesini veritabanından hello kan Bağış hello kan Transfusion hizmeti, merkezi Hsin Chu Şehir, Tayvan.<p> </p>Bağış verileri gibi hello aydan son Bağış beri) ve sıklığı veya Bağışlar, son Bağış bu yana geçen süre toplam sayısı hello ve bağışlanır kan miktarı.<p> </p><b>Kullanım:</b> hello hedef olup toopredict sınıflandırma aracılığıyla hello Bağış bağışlanır Bağış olmayan kan Mart 2007, burada 1 gösteren bir Bağış hello hedef dönemi ve 0 sırasında. <p> </p><b>İlgili araştırma:</b> Yeh, I.C., (2008). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi <p> </p>Yeh, t-Cheng, Yang, Jang Kol-gönderdi ve toplantı, Tao-msiexec, "bilgi bulma Bernoulli dizisi kullanılarak RFM model üzerinde" uygulamaları, 2008, Uzman sistemleriyle <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  </td>
</tr>

<tr ID=book-reviews-from-amazon>
  <td valign=top>Amazon gelen Kitap incelemeleri</td>
  <td valign=top>
İncelemeler hello amazon.com Web sitesinden University Pennsylvania Araştırmacıları tarafından gerçekleştirilen Amazon defterleri (<a href="http://www.cs.jhu.edu/~mdredze/datasets/sentiment/">düşünceleri</a>). Merhaba araştırma belgesi, "Biyografileri, Bollywood, müzik kutuları ve Blenders: düşünceleri sınıflandırması için etki alanı uyarlama" John Blitzer, işareti Dredze ve Fernando Pereira; Hesaplama Linguistics (ACL), ilişkisi 2007.<p> </p>Merhaba özgün dataset 975 K İnceleme derecelendirmeleri 1, 2, 3, 4 veya 5 ile sahiptir. Merhaba incelemeler İngilizce dilinde yazılmıştır ve hello süre 1997-2007 değildir. Bu veri kümesi aşağı örneklenen too10K incelemeler olmuştur.
  </td>
</tr>

<tr>
  <td valign=top>Breast kanseri verileri</td>
  <td valign=top>
Merhaba sık machine learning belgelerinde görünür Oncology Institute tarafından sağlanan üç kanseri ilişkili veri kümeleri biri. Laboratuar analiz özelliklerinden tanılama bilgilerini yaklaşık 300 dokulu örnekleri birleştirir.<p> </p><b>Kullanım:</b> kanseri hello türünü sınıflandırmak, 9 özniteliklerini temel alarak, bazıları doğrusal ve kategorik bazılarıdır. <p> </p><b>İlgili araştırma:</b> Wohlberg, W.H., Sokak, W.N. ve Mangasarian, O.L. (1995). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi </td>
</tr>

<tr ID=breast-cancer-features>
  <td valign=top>Breast Kanseri özellikleri <td valign=top>
Merhaba dataset her 117 özellikleri tarafından açıklanan röntgen görüntüleri 102 K şüpheli bölgeler (adayları) için bilgiler içerir. Merhaba özellikleri özeldir ve anlamları hello dataset oluşturucuları (Siemens sağlık) tarafından gösterilmez. 
  </td>
</tr>

<tr ID=breast-cancer-info>
  <td valign=top>Breast Kanseri bilgisi</td>
  <td valign=top>
Merhaba dataset röntgen görüntüsünün şüpheli her bölge için ek bilgiler içerir. Her örneğin bilgileri sağlar (örn., etiket, hasta kimliği, düzeltme eki göreli toohello görüntünün tamamını koordinatlarını) hello karşılık gelen satır numarası hello Breast Kanseri özellikleri kümesindeki hakkında. Her hasta örnek sayısına sahip. Bir kanseri sahip hastalar için bazı örnekler pozitif ve negatif bazılarıdır. Bir kanseri yok hastalar tüm örnekler negatiftir. Merhaba dataset 102 K örnekler vardır. Merhaba dataset %0,6 hello noktalarının pozitif ağırlıklı, hello rest negatif. Merhaba dataset Siemens sağlık tarafından kullanılabilir hale getirildi.
  </td>
</tr>

<tr ID=crm-appetency-labels-shared>
  <td valign=top>Paylaşılan CRM Appetency etiketleri</td>
  <td valign=top>
Merhaba KDD fincanı 2009 müşteri ilişkileri tahmin sınama etiketlerden (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>).
  </td>
</tr>

<tr ID=crm-churn-labels-shared>
  <td valign=top>Paylaşılan CRM karmaşası etiketleri</td>
  <td valign=top>
Merhaba KDD fincanı 2009 müşteri ilişkileri tahmin sınama etiketlerden (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>).
  </td>
</tr>

<tr ID=crm-dataset-shared>
  <td valign=top>Paylaşılan CRM veri kümesi</td>
  <td valign=top>
Bu veriler hello KDD fincanı 2009 müşteri ilişkileri tahmin sınama gelir (<a href="http://www.sigkdd.org/kdd-cup-2009-customer-relationship-prediction - orange_small_train.data.zip">orange_small_train.data.zip</a>).<p> </p>Merhaba dataset hello Fransızca telekomünikasyon şirket turuncu 50 K müşterilerden içerir. Her bir müşteri 190 de sayısal 230 anonim özelliklere sahiptir ve 40 kategorik. Merhaba özellikleri çok seyrek.
  </td>
</tr>

<tr ID=crm-upselling-labels-shared>
  <td valign=top>Paylaşılan CRM Upselling etiketleri</td>
  <td valign=top>
Merhaba KDD fincanı 2009 müşteri ilişkileri tahmin sınama etiketlerden (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>).
  </td>
</tr>

<tr>
  <td valign=top>Enerji verimliliği regresyon veri</td>
  <td valign=top>
Benzetimli enerji profilleri, 12 farklı yapı şekillerine göre koleksiyonu. Merhaba binalar alanı, alan dağıtım ve yönlendirmesini glazing hello glazing gibi 8 özellikleri tarafından ayrılır.<p> </p><b>Kullanım:</b> regresyon veya sınıflandırma toopredict hello enerji iki gerçek değerli yanıtları biri olarak tabanlı derecelendirme verimliliği kullanın. Birden çok sınıf sınıflandırma için hello yanıt değişken toohello tamsayı en yakın round ' dir. <p> </p><b>İlgili araştırma:</b> Xifara, a & Tsanas, A. (2012). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi </td>
</tr>

<tr ID=flight-delays-data>
  <td valign=top>Uçuş veri geciktirir</td>
  <td valign=top>
Yolcu uçuş zamanında hello ABD TranStats veri koleksiyonu hello alınan performans verileri Departman, taşıma (<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">zamanında</a>).<p> </p>Merhaba dataset hello süre Nisan-Ekim 2013 kapsar. Machine Learning Studio tooAzure karşıya yüklemeden önce hello dataset gibi işlenmiş:<ul><li>filtrelenmiş toocover yalnızca hello 70 yoğun saatinde havaalanları hello continental ABD içinde Hello dataset edildi</li><li>İptal edilen uçuşlar 15 dakikadan tarafından Gecikmeli olarak etiketlenmiş</li><li>Yolu saptırabilir uçuşlar filtre</li><li>Merhaba aşağıdaki sütun seçildi: yıl, ay, DayofMonth, DayOfWeek, taşıyıcı, OriginAirportID, DestAirportID, CRSDepTime, DepDelay, DepDel15, CRSArrTime, ArrDelay, ArrDel15, iptal edildi</li></ul>
</td>
</tr>

<tr>
  <td valign=top>Uçuş zamanında performans (ham)</td>
  <td valign=top>
Uçak uçuş gelişleri ve departures Ekim 2011 Birleşik Devletler içinde kaydı.<p> </p><b>Kullanım:</b> uçuş gecikmeler tahmin etmek. <p> </p><b>İlgili araştırma:</b> , ABD bölüm taşıma gelen <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time</a>.
  </td>
</tr>

<tr>
  <td valign=top>Orman yangını verileri</td>
  <td valign=top>
Sıcaklık ve nem dizinlerini ve Rüzgar hızı, orman ateşlenir kayıtlarıyla birleştirilmiş Kuzey Doğu Portekiz alanı gibi hava durumu verileri içerir.<p> </p><b>Kullanım:</b> hello AIM toopredict hello Yakılan orman ateşlenir alanının olduğu bir zor regresyon görev budur. <p> </p><b>İlgili araştırma:</b> Cortez, P. & Morais, A. (2008). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi <p> </p>[Cortez ve Morais, 2007] P. Cortez ve A. Morais. Veri araştırma yaklaşım tooPredict orman Meteorological verileri kullanarak etkinleşir. J. Neves, M. f Santos ve J. Machado Eds., yapay zeka, bildirileri, yeni eğilimler yapay zeka, aralık, Guimarães, Portekiz pp. 512-523, EPIA 2007 - Portekizce konferans 13 2007 hello. APPIA, ISBN-13 978-989-95618-0-9'İ TIKLATIN. Bulunabilir: <a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>.
  </td>
</tr>

<tr ID=german-credit-card-uci-dataset>
  <td valign=top>Almanca kredi kartı UCI veri kümesi</td>
  <td valign=top>
UCI Statlog (Almanca kredi kartı) dataset hello (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog + Almanca + kredi + verilerini</a>), hello german.data dosyasını kullanarak.<p> </p>Merhaba dataset kişiler, düşük veya yüksek kredi riskleri olarak öznitelikleri kümesi tarafından açıklanan sınıflandırır. Her örneğin bir kişi temsil eder. Sayısal ve kategorik, 20 özellikleri ve ikili etiket (Merhaba kredi riski değer) vardır. Yüksek kredi riski girişleriniz etiket = 2, düşük kredi riski girişleriniz etiket = 1. yüksek riskli örneğin düşük misclassifying hello maliyetini 5 iken yüksek olarak düşük riskli örnek misclassifying hello maliyeti 1 ' dir.
  </td>
</tr>

<tr ID=imdb-movie-titles>
  <td valign=top>IMDB başlık</td>
  <td valign=top>
Merhaba veri kümesi hakkında bilgi Twitter tweet'leri derecelendirilmiş filmler içerir: IMDB film kimliği, film adı, tarzını ve üretim yıl. Merhaba kümesinde 17K filmler vardır. Merhaba dataset hello kağıt "S. sunulmuştur Dooms, t De Pessemier ve L. Martens. MovieTweetings: Veri kümesi derecelendirme film Twitter'dan toplanır. Atölye kitle kaynak ve İnsan hesaplama öneren sistemleri, RecSys 2013'te CrowdRec."
  </td>
</tr>

<tr>
  <td valign=top>Iris iki sınıf verileri</td>
  <td valign=top>
Merhaba hello desen tanıma belgelerinde bulunan en iyi bilinen veritabanı toobe belki de budur. Merhaba dataset 50 örnekleri her üç iris çeşit yaprağı ölçümler içeren görece küçük.<p> </p><b>Kullanım:</b> hello iris hello ölçümleri türünden tahmin etmek.  <p> </p><b>İlgili araştırma:</b> Fisher, R.A. (1988). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi </td>
</tr>

<tr ID=movie-tweets>
  <td valign=top>Film Tweet'leri</td>
  <td valign=top>
Merhaba dataset hello film Tweetings dataset genişletilmiş bir sürümüdür. Merhaba dataset Twitter'da iyi yapılandırılmış tweet'leri ayıklanan filmler 170 K derecelendirmesi sahiptir. Her örneğinin tweet temsil eder ve bir tanımlama grubu olduğundan: kullanıcı kimliği, IMDB film kimliği, derecelendirme, zaman damgası, bu tweet ve bu tweet retweets sayısı için Sık Kullanılanlara numarası. Hello dataset A. Denirse, S. Dooms, B. Loni ve D. Tikk tarafından öneren sistemleri sınama 2014 için kullanılabilir hale getirildi.
  </td>
</tr>

<tr>
  <td valign=top>Çeşitli otomobiller için MPG verileri</td>
  <td valign=top>
Bu veri kümesi hello StatLib kitaplığının Carnegie Mellon University tarafından sağlanan hello dataset biraz değiştirilmiş bir sürümüdür. Merhaba dataset hello 1983 kullanıldı Amerikan istatistiksel ilişkilendirme Exposition.<p> </p>Merhaba veri galon başına mil, içinde çeşitli otomobiller için yakıt tüketimini bilgilerle bunların Silindir, altyapısı öteleme, beygir gücü, toplam ağırlığı ve Hızlandırma'gibi hello sayısını listeler.<p> </p><b>Kullanım:</b> 3 birden çok değerli ayrık öznitelikleri ve 5 sürekli öznitelikleri temel alınarak yakıt ekonomi tahmin etmek. <p> </p><b>İlgili araştırma:</b> StatLib, Carnegie Mellon University (1993). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi </td>
</tr>

<tr>
  <td valign=top>Pima ana dilidir Diabetes ikili sınıflandırma veri kümesi</td>
  <td valign=top>
Bir veri alt kümesini hello National Institute Diabetes ve Digestive ve serbest Diseases veritabanından. Merhaba dataset Pima Hindistan miras, kadın hastalar üzerinde filtrelenmiş toofocus oluştu. Merhaba verileri lifestyle Etkenler yanı sıra glucose ve insulin düzeyleri gibi sağlık verilerini içerir.<p> </p><b>Kullanım:</b> hello konu diabetes (ikili sınıflandırma) sahip olup olmadığını tahmin etmek. <p> </p><b>İlgili araştırma:</b> Sigillito, V. (1990). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml "</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi </td>
</tr>

<tr>
  <td valign=top>Restoran müşteri verileri</td>
  <td valign=top>
Müşteriler, demografisine ve tercihleri de dahil olmak üzere ilgili meta verileri kümesi.<p> </p><b>Kullanım:</b> , birlikte diğer iki Restoran veri kümeleri, tootrain hello ve öneren sistem test bu veri kümesi kullanın. <p> </p><b>İlgili araştırma:</b> Bache, k ve Lichman, M. (2013). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi.
  </td>
</tr>

<tr>
  <td valign=top>Restoran özelliği verileri</td>
  <td valign=top>
Restoran ve yemek türü, yerinizi stil ve konum gibi özelliklerine hakkındaki meta verileri kümesi.<p> </p><b>Kullanım:</b> , birlikte diğer iki Restoran veri kümeleri, tootrain hello ve öneren sistem test bu veri kümesi kullanın. <p> </p><b>İlgili araştırma:</b> Bache, k ve Lichman, M. (2013). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi.
  </td>
</tr>

<tr>
  <td valign=top>Restoran derecelendirme</td>
  <td valign=top>
Kullanıcıların toorestaurants tarafından bir ölçekte 0 too2 verilen derecelendirmeleri içeriyor.<p> </p><b>Kullanım:</b> , birlikte diğer iki Restoran veri kümeleri, tootrain hello ve öneren sistem test bu veri kümesi kullanın. <p> </p><b>İlgili araştırma:</b> Bache, k ve Lichman, M. (2013). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi.
  </td>
</tr>

<tr>
  <td valign=top>Çelik Annealing çok sınıf veri kümesi</td>
  <td valign=top>
Bu veri kümesi hello fiziksel öznitelikleri (genişlik, kalınlığı, hello kaynaklanan türü (bobini, sayfası, vb.) çelik türleri. ile denemeler annealing çelik kayıtlarından bir dizi içeriyor<p> </p><b>Kullanım:</b> iki sayısal sınıf öznitelikleri; sertliği veya gücü tahmin etmek. Ayrıca öznitelikler arasında bağıntıları analiz.<p> </p>Çelik dereceleri izleyin kümesi standart SAE ve diğer kuruluşlar tarafından tanımlanan. Özel bir 'düzeyde' (Merhaba sınıfı değişken) aradığınız ve gerekli toounderstand hello değerleri istiyor. <p> </p><b>İlgili araştırma:</b> sterlin, d & Buntine, W. (NA). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: California Üniversitesi, okul daha fazla bilgi ve bilgisayar bilimi <p> </p>Yararlı Kılavuzu toosteel dereceleri şurada bulunabilir: <a href="http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf">http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf</a>
  </td>
</tr>

<tr>
  <td valign=top>Teleskop veri</td>
  <td valign=top>
Arka plan gürültü birlikte yüksek enerji gama parçacık WINS'e kayıtları, her ikisi de Monte Carlo bir işlemi kullanarak simulated.<p> </p>İstatistiksel yöntemler toodifferentiate hello istenen sinyal (Cherenkov Radyasyonu duşlar) ve arka plan gürültü (hadronic arasında kullanarak başından başlayarak tabanlı hava Cherenkov gama telescopes, tooimprove hello doğruluğunu hello benzetimi Hello amacı edildi duşlar) cosmic Işınları hello üst Atmosfer içinde tarafından başlatıldı.<p> </p>Merhaba veri önceden işlenen toocreate elongated bir kümeyle oldu hello uzun eksen hello kamera merkezi yönlendirilmiş. Bu üç nokta (Hillas parametreleri olarak da adlandırılır) Hello özelliklerini Ayrımcılığı için kullanılabilir hello görüntü parametreleri arasındadır.<p> </p><b>Kullanım:</b> hediye görüntüsü sinyal ya da arka plan gürültü temsil edip etmediğini tahmin etmek.<p> </p><b>Notlar:</b> basit sınıflandırma doğruluğu değil Bu verileri için anlamlı sinyal sinyal olayı arka olarak sınıflandırma değerinden daha zayıf olduğu gibi bir arka plan olay sınıflandırma itibaren. Merhaba ROC grafik farklı sınıflandırıcı bir karşılaştırması için kullanılmalıdır. Merhaba sinyal eşikleri aşağıdaki hello biri olmalıdır gibi bir arka plan olayı kabul etme olasılığı: 0,01 0,02, 0,05, 0,1 veya 0.2.<p> </p>Ayrıca, gerçek ölçüleri olayları hello çoğunluğu hello h veya gürültü sınıfı temsil eder ancak arka plan olayları (hadronic duşlar için y) hello sayısı önemsemedi unutmayın. <p> </p><b>İlgili araştırma:</b> Bock, R.K. (1995). Depo öğrenme UCI makine <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California Okul daha fazla bilgi </td>
</tr>

<tr ID=weather-dataset>
  <td valign=top>Hava durumu veri kümesi</td>
  <td valign=top>
Saatlik kara bulunduğunuz gözlemleri NOAA gelen (<a href="http://cdo.ncdc.noaa.gov/qclcd_ascii/, merged data from 201304 too201310">birleştirilmiş 201304 too201310 verilerden</a>).<p> </p>Merhaba hava veri havaalanı hava durumu istasyonlarını hello süre Nisan-Ekim 2013 kapsayan yapılan gözlemleri kapsar. Machine Learning Studio tooAzure karşıya yüklemeden önce hello dataset gibi işlenmiş:<ul><li>Eşlenen toocorresponding havaalanı kimlikleri hava durumu istasyon kimliği olan</li><li>Hava durumu hello 70 yoğun saatinde havaalanları ile ilişkili olmayan istasyonlar filtre</li><li>Merhaba tarih sütunu ayrı yıl, ay ve gün sütunlara bölme</li><li>Merhaba aşağıdaki sütun seçildi: AirportID yıl, ay, gün, saat, saat dilimi, SkyCondition, görünürlük, WeatherType, DryBulbFarenheit, DryBulbCelsius, WetBulbFarenheit, WetBulbCelsius, DewPointFarenheit, DewPointCelsius, RelativeHumidity, WindSpeed, WindDirection, ValueForWindCharacter, StationPressure, PressureTendency, PressureChange, SeaLevelPressure, RecordType, HourlyPrecip, Altimeter</li></ul>
  </td>
</tr>

<tr ID=wikipedia-sp-500-dataset>
  <td valign=top>Wikipedia SP 500 veri kümesi</td>
  <td valign=top>
Veri Wikipedia türetilen (<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>) XML verileri olarak depolanan her S & P 500 şirket makalelerinin temel.<p> </p>Machine Learning Studio tooAzure karşıya yüklemeden önce hello dataset gibi işlenmiş:<ul><li>Belirli her şirket için metin içeriği Ayıkla</li><li>Wiki biçimlendirme Kaldır</li><li>Alfasayısal olmayan karakter Kaldır</li><li>Tüm metin toolowercase Dönüştür</li><li>Bilinen şirket kategorileri eklendi</li></ul><p> </p>Kayıt Hello sayısını 500'den az olacak şekilde bazı şirketler için bir makale bulunamadı, unutmayın.
  </td>
</tr>





<tr ID=direct-marketing>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></td>
  <td valign=top>
Müşteri verileri ve bunların yanıt tooa doğrudan posta kampanyayla ilgili göstergeleri Hello veri kümesi içerir. Her satır bir müşteri temsil eder. Merhaba veri kümesi içerdiğinden kullanıcı demografisine hakkında ve geçmiş davranışı ve 3 etiket sütun 9 özellikleri (, dönüştürme, ziyaret edin ve harcamanızı).  Ziyaret hello pazarlama kampanyası, dönüştürme bir müşteri bir şey satın gösterir ve harcamanız sonra ziyaret müşteri harcandığını hello tutar olduğunu belirten ikili bir sütundur.  Merhaba dataset MineThatData e-posta analizi ve veri madenciliği sınaması için Kevin Hillstrom göre sunulmuştur.
  </td>
</tr>

<tr ID=lyrl2004-tokens-test>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></td>
  <td valign=top>
Test örnekleri hello RCV1 V2 Reuters haber kümesindeki özellikleri. Merhaba dataset sahip 781K haber makalelerini kimlikleri birlikte (Merhaba kümesinin ilk sütun). Her makalede, stopworded, simgeleştirilmiş ve stemmed. Merhaba dataset David tarafından kullanılabilir hale getirildi. D. Gamze.
  </td>
</tr>

<tr ID=lyrl2004-tokens-train>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></td>
  <td valign=top>
Eğitim örneklerde hello RCV1 V2 Reuters haber veri kümesi özellikleri. Merhaba dataset sahip 23K haber makalelerini kimlikleri birlikte (Merhaba kümesinin ilk sütun). Her makalede, stopworded, simgeleştirilmiş ve stemmed. Merhaba dataset David tarafından kullanılabilir hale getirildi. D. Gamze.
  </td>
</tr>

<tr ID=intrusion-detection>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a><br></td>
  <td valign=top>
Merhaba KDD fincanı 1999 bilgi bulma kümesinden ve veri madenciliği araçları rekabet (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>).<p> </p>Merhaba dataset indirilir ve Azure Blob depolama alanına depolanır (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) ve hem eğitim ve sınama veri kümesi içerir. Merhaba eğitim veri kümesi yaklaşık 126 K satırları ve hello etiketleri içeren 43 sütunları vardır. Üç sütun hello etiket bilgilerini bir parçasıdır ve 40 sütunlar, sayısal ve dize/kategorik özelliklerini oluşan hello modeli eğitmek için kullanılabilir. Merhaba test verileri hello eğitim verilerini olduğu gibi hello aynı 43 sütunlarla örnekleri test yaklaşık 22,5 K vardır.

  </td>
</tr>

<tr ID=rcv1-v2-topics-qrels>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1 v2.topics.qrels.csv</a></td>
  <td valign=top>
Merhaba RCV1 V2 Reuters haber kümesindeki haber makalelerini atamaları konu. Bir haber makalesi tooseveral konuları atanabilir. her satırın Hello biçimi "&lt;konu adı&gt; &lt;belge kimliği&gt; 1". Merhaba dataset 2.6 M konu atamaları içeriyor. Merhaba dataset David tarafından kullanılabilir hale getirildi. D. Gamze.
  </td>
</tr>

<tr ID=student-performance>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></td>
  <td valign=top>
Bu veriler KDD fincanı 2010 öğrenci performans değerlendirme sınama hello gelir (<a href="http://www.kdd.org/kdd-cup-2010-student-performance-evaluation">Öğrenci Performans değerlendirmesinin</a>). Merhaba kullanılan verileri hello Algebra_2008_2009 eğitim kümesidir (Stamper, J., Niculescu-Mizil, A., Ritter, S. Gordon, G.J. & Koedinger, K.R. (2010). Cebiri ı 2008-2009. KDD fincanı 2010 eğitim veri madenciliği sınama kümesinden sınaması. Şimdi Bul <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a> veya <a href="http://www.kdd.org/sites/default/files/kddcup/site/2010/files/algebra_2008_2009.zip">algebra_2008_2009.zip</a>.<p> </p>Merhaba dataset indirilir ve Azure Blob depolama alanına depolanır (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) ve sistem özel Ders öğrencinin günlük dosyalarını içerir. sağlanan hello özellikleri kullanarak, sorun kimliği ve Öğrenci Kimliği, zaman damgası, kendi kısa bir açıklama ve kaç tane hello hello sorun giderme önce yapılan hello Öğrenci girişimleri sağ yolu. Merhaba özgün dataset 8,9 M kaydeder; yine de sahip istiyor musunuz? Bu veri kümesi aşağı örneklenen toohello ilk 100 K satırları olmuştur. Merhaba dataset çeşitli türlerdeki 23 sekmeyle ayrılmış sütunu var.: kategorik, sayısal ve zaman damgası.

  </td>
</tr>




</table>


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

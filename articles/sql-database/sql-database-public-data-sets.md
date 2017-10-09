---
title: "aaaPublic veri kümeleri için Azure analizi | Microsoft Docs"
description: "Genel veri kümeleri hakkında bilgi edinin tooprototype ve test Azure Analiz Hizmetleri ve çözümleri kullanabilirsiniz."
services: sql-database
documentationcenter: 
author: douglaslMS
manager: craigg
editor: 
tags: 
ms.custom: reference
ms.assetid: 
ms.service: sql-database
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 03/20/2017
ms.author: douglasl
ms.openlocfilehash: 23b645ab7d6730012bba48058f389695d27a02a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="public-data-sets-for-testing-and-prototyping"></a>Test ve prototipi oluşturulurken ortak veri kümeleri

Bu tooprototype kullanın ve depolama ve Analiz Hizmetleri ve çözümleri test verileri için ortak veri kümeleri listesini bulun.

## <a name="us-government-and-agency-data"></a>ABD Kamu ve Teşkilatı verileri

| Veri kaynağı | Merhaba veri hakkında | Merhaba dosyaları hakkında |
|---|---|---|
| [ABD devlet kurumları veri](https://www.census.gov/data.html) | Tarım, iklim, tüketici, ekosistemlerini, eğitim, enerji, Finans, sistem durumu, yerel kamu, üretim, maritime, Okyanusu, genel güvenlik ve Bilim ve hello ABD Araştır kapsayan üzerinde 190,000 veri kümeleri | HTML, XML, CSV, JSON, Excel ve diğer birçok dahil olmak üzere çeşitli biçimlerde çeşitli boyutlarda dosyaları. Dosya biçimi tarafından kullanılabilir veri kümelerini filtreleyebilirsiniz. |
| [ABD Census veri](https://www.census.gov/data.html) | Merhaba ABD hello popülasyonunu hakkında istatistiksel veriler | Veri, çeşitli biçimlerde kümeleridir. |
| [NASA Earth Bilim verileri](https://earthdata.nasa.gov/) | Tarım, Atmosfer, biosphere, iklim, cryosphere, İnsan boyutları, hydrosphere, kara yüzeyini, oceans, sun earth etkileşimleri ve daha fazlasını kapsayan üzerinde 32.000 veri koleksiyonları. | Veri, çeşitli biçimlerde kümeleridir. |
| [Uçak uçuş gecikmeleri ve diğer taşıma verileri](https://www.transtats.bts.gov/OT_Delay/OT_DelayCause1.asp) | "hello ABD Departman, taşıma (nokta) kuruluşu taşıma istatistikleri (BTS) parçaları hello zamanında büyük hava hizmet sağlayıcılar tarafından işletilen yurtiçi uçuşlar performansını, kullanıcının. Özet bilgileri zamanında, Gecikmeli, iptal edilmiş ve yolu saptırabilir uçuşlar hello sayısına... Bu Web sitesinde yayınlanan Özet tabloları görüntülenir." | CSV biçiminde dosyalardır. |
| [Trafik fatalities - BİZE Fatality analiz raporlama sistemi (FARS)](http://www.nhtsa.gov/FARS) | "FARS NHTSA, Kongre ve hello Amerikan ortak yıllık ilgili verileri motor araç trafiği kilitlenmelere başlayamıyorsa önemli injuries sağlama ülke çapında bir census değil." | "Hello FARS sorgu sistemi kullanarak çevrimiçi çalıştırmak için kendi fatality verilerinizi oluşturun. Veya 1975'ten toopresent hello FTP sitesinin gelen tüm FARS veri indirin." |
| [Toxic kimyasal verileri - EPA Toxicity ForeCaster (ToxCast™)](https://www.epa.gov/chemical-research/toxicity-forecaster-toxcasttm-data) | "En güncel, genel kullanıma açık yüksek verimlilik toxicity verileri chemicals binlerce EPA'ın. Bu veriler hello EPA'ın ToxCast araştırma çaba oluşturulur." | Veri kümeleri, elektronik tablolar, R paketleri ve MySQL veritabanı dosyaları dahil olmak üzere çeşitli biçimlerde kullanılabilir. |
| [Toxic kimyasal data - NIH Tox21 veri sınama 2014](https://tripod.nih.gov/tox21/challenge/) | "hello veri güçlük 2014 Tox21 hello chemicals bileşimlerini hello 21 girişimi toodisrupt Biyolojik yollarıyla toxic içinde sonuçlanabilir şekilde hello Toxicology aracılığıyla test edilen ve olası hello bilimcilerine anlamak toohelp tasarlanmış etkiler." | Veri kümeleri GÜLÜMSEMELER ve SDF kullanılabilir biçimleri. Merhaba verileri sağlayan "assay etkinlik verileri ve ~ 10.000 bileşimlerini hello Tox21 koleksiyonu kimyasal yapıları (Tox21 10K)." |
| [Merhaba NCBI biotechnology ve genome verileri](https://www.ncbi.nlm.nih.gov/guide/data-software/) | Birden çok veri kümesi genes, genomes ve proteins kapsayan. | Veri kümeleri, metin, XML, topluca ve diğer biçimlere ' dir. TOPLUCA uygulama kullanılamaz. |

## <a name="other-statistical-and-scientific-data"></a>Diğer istatistiksel ve bilimsel veri

| Veri kaynağı | Merhaba veri hakkında | Merhaba dosyaları hakkında |
|---|---|---|
| [New York şehrinde ücreti verileri](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml) | "Toplama yakalama alanları ücreti seyahat kayıtları içerir ve teslim tarih/zaman, toplama ve teslim konumları, seyahat uzaklıkları, dökümü fares, oranı türleri, ödeme türleri ve sürücü bildirilen yolcu sayar." | Veri kümeleri CSV aya göre dosyalarıdır. |
| [Microsoft Research veri kümelerini - "Research için veri bilimi"](https://www.microsoft.com/research/academic-program/data-science-microsoft-research/) | Birden çok veri bilgisayar insan etkileşimi, ses/video, veri araştırma/bilgi alma, Jeo-uzamsal/konum, doğal dil işleme ve robotics/bilgisayar görme kapsayan ayarlar. | Veri indirme için daraltılmış çeşitli biçimlerde kümeleridir. |
| [Ortak genome veri](http://www.completegenomics.com/public-data/) | "Tüm İnsan genomes farklı bir veri kümesi için ortak kullanım tooenhance ücretsiz herhangi genomic incelemesi..." hello, tam Genomics sağlayıcısıdır özel for-profit corporation. | Veri kümeleri, ayıklama işleminden sonra UNIX metin biçimindedir. Çözümleme Araçları de kullanılabilir. |
| [Açık Bilim veri bulut veri](https://www.opensciencedatacloud.org/) | "hello açık Bilim veri bulut depolama, paylaşımı ve terabayt ve Petabayt ölçekli bilimsel veri kümeleri çözümleme kaynaklarla hello bilimsel topluluk sağlar."| Veri, çeşitli biçimlerde kümeleridir. |
| [Genel iklim data - WorldcLIM](http://worldclim.org/) | "WorldClim genel iklim Katmanlar (gridded iklim veri) yaklaşık 1 km2 uzamsal çözünürlüğü ile kümesidir. Bu verileri eşleştirmesi ve uzamsal modelleme için kullanılabilir." | Bu dosyalar Jeo-uzamsal verileri içerir. Daha fazla bilgi için bkz: [veri biçimi](http://worldclim.org/formats1). |
| [İnsan topluluğu - hello GDELT proje ilgili veriler](http://www.gdeltproject.org/data.html) | "hello GDELT proje hello büyük ve en kapsamlı ve yüksek çözünürlüğe İnsan topluluğu şimdiye kadar oluşturulan veritabanı açın." | CSV biçiminde Hello ham verileri dosyalarıdır. |
| [Reklam tahmin veri Criteo gelen machine learning için tıklatın](http://labs.criteo.com/2013/12/download-terabyte-click-logs/) | "hello en büyük herhangi bir zamanda genel olarak yayımlanan ML dataset." Daha fazla bilgi için bkz: [Criteo'nın 1 TB'ı tıklatın tahmin Dataset](https://blogs.technet.microsoft.com/machinelearning/2015/04/01/now-available-on-azure-ml-criteos-1tb-click-prediction-dataset/). | |
| [ClueWeb09 metin araştırma veri hello Lemur proje kümesinden](http://www.lemurproject.org/clueweb09.php/) | "hello ClueWeb09 dataset toosupport araştırma bilgileri alma ve ilgili İnsan dil teknolojileri oluşturuldu. Yaklaşık 1 milyar web sayfaları Ocak ve Şubat 2009 toplanan 10 dillerde oluşur." | Bkz: [veri kümesi bilgilerini](http://www.lemurproject.org/clueweb09/datasetInformation.php).|

## <a name="online-service-data"></a>Çevrimiçi hizmet verileri

| Veri kaynağı | Merhaba veri hakkında | Merhaba dosyaları hakkında |
|---|---|---|
| [GitHub arşiv](https://www.githubarchive.org/) | "GitHub Arşiv bir proje toorecord hello ortak GitHub zaman çizelgesi [olayların], arşivlemek ve daha fazla çözümleme için kolayca erişilebilir hale olduğu." | JSON encloded olay arşivler .gz (Gzip) biçiminde bir web istemcisinden indirin. |
| [Merhaba GHTorrent projeden GitHub etkinlik verileri](http://ghtorrent.org/) | "hello GHTorrent [veri ölçeklenebilir, sorgulanabilir, çevrimdışı bir yansıtma hello GitHub REST API sunulan bir çaba toocreate projedir]. GHTorrent hello GitHub genel olay zaman çizelgesi izler. Her olay için içeriği ve onların bağımlılıkları ayrıntısına alır." | MySQL veritabanı dökümleri CSV biçimindedir. |
| [Yığın Taşması Veri dökümü](https://archive.org/details/stackexchange) | "[Yığın taşması dahil olmak üzere] hello yığını Exchange ağ kullanıcı katkıda bulunan tüm içeriğine anonim bir dökümünü budur." | "[Yığın taşması] gibi-her site XML dosyalarını oluşan ayrı bir arşiv aracılığıyla daraltılmış olarak biçimlendirilmiş 7-zip bzıp2 sıkıştırma kullanılarak. Her site arşiv gönderileri, kullanıcılar, oyları, yorumlar, PostHistory ve PostLinks içerir." |

---
title: "aaaArchived sürüm notları - Azure hdınsight'ta Hadoop bileşenleri | Microsoft Docs"
description: "Azure Hdınsight için Hadoop bileşenleri eski sürümleri için arşivlenen sürüm notları."
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 7a99c77f4557ca8c1dabe924cc67b2e0a134f8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a>Azure hdınsight'ta Hadoop bileşenleri için sürüm notları (arşiv)

Bu makalede hello hakkında bilgiler sağlanmaktadır **eski** Azure Hdınsight sürüm güncelleştirmeleri. Daha yeni sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight sürüm notları](hdinsight-release-notes.md).

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz: [Hdınsight sürüm makale](hdinsight-component-versioning.md).



## <a name="notes-for-08302016-release-of-hdinsight"></a>Hdınsight 30/08/2016 sürüm notları
Linux tabanlı Hdınsight kümeleri Hello tam sürüm numaralarını bu sürüm ile birlikte dağıtılabilir:

| HDI | HDI kümesi sürüm | HDP | HDP derleme | Ambari derleme |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8268980 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8268980 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8269383 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

Windows tabanlı Hdınsight kümeleri Hello tam sürüm numaralarını bu sürüm ile birlikte dağıtılabilir:

| HDI | HDI kümesi sürüm | HDP | HDP derleme |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1033.2559206 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1033.2559206 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1033.2559206 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1033.2559206 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1033.2559206 |2.3 |2.3.3.1-25 |


## <a name="08172016---release-of-r-server-on-hdinsight"></a>17/08/2016 - hdınsight'ta R Server sürümü
* R Server 8.0.5 - çoğunlukla bir hata düzeltmesi serbest bırakma. Merhaba bkz [R Server sürüm notları](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) daha fazla bilgi için.
* Merhaba kenar düğümüne - AzureML paketi [bu R paketi](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) etkinleştirir R modelleri toobe yayımlanan ve bir Azure ML web hizmeti olarak tüketilen.  Merhaba bkz ["Bir Model faaliyete"](hdinsight-hadoop-r-server-overview.md#operationalize-a-model) bölümünü bizim ["Genel bakış, R Server üzerinde Hdınsight"](hdinsight-hadoop-r-server-overview.md) daha fazla bilgi için makalenin.
* Merhaba Linux bağımlılıkları [100 en popüler R paketleri top](https://github.com/metacran/cranlogs) -bu Linux Paket bağımlılıklarını şimdi önceden yüklenir.
* R eklerken seçeneği toouse hello CRAN depodaki toohello veri düğümlerini paketler. Daha fazla bilgi için bkz: ["Hdınsight'ta R Server kullanmaya başlamanıza"](hdinsight-hadoop-r-server-get-started.md).
* Geliştirilmiş hello güvenilirlik'kümeleri oluşturduğunuzda, R Server sağlama.

## <a name="notes-for-08012016-release-of-hdinsight"></a>Hdınsight 08/01/2016 sürüm notları
Linux tabanlı Hdınsight kümeleri Hello tam sürüm numaralarını bu sürüm ile birlikte dağıtılabilir:

| HDI | HDI kümesi sürüm | HDP | HDP derleme | Ambari derleme |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8028416 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8028416 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8053402 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

Windows tabanlı Hdınsight kümeleri Hello tam sürüm numaralarını bu sürüm ile birlikte dağıtılabilir:

| HDI | HDI kümesi sürüm | HDP | HDP derleme |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1005.2488842 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1005.2488842 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1005.2488842 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1005.2488842 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1005.2488842 |2.3 |2.3.3.1-25 |

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin Spark, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Değişiklikleri tooHDInsight 3.4 kümeleri |Merhaba varsayılan değerleri aşağıdaki hive yapılandırmaları için daha iyi performans için değiştirilir <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |Hizmet |Tümü |Yok |
| Bu sürümde aşağıdaki düzeltmeler bulunmaktadır |HIVE 13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933 |Hizmet |Tümü |Yok |

## <a name="notes-for-07142016-release-of-hdinsight"></a>Hdınsight 07/14/2016 sürüm notları
Linux tabanlı Hdınsight kümeleri Hello tam sürüm numaralarını bu sürüm ile birlikte dağıtılabilir:

| HDI | HDI kümesi sürüm | HDP | HDP derleme | Ambari derleme |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7932505 |2.2 |2.2.9.1-11 |2.2.1.12-2 |
| 3.3 |3.3.1000.0.7932505 |2.3 |2.3.3.1-18 |2.2.1.12-2 |
| 3.4 |3.4.1000.0.7933003 |2.4 |2.4.2.0 |2.2.1.12-2 |

Windows tabanlı Hdınsight kümeleri Hello tam sürüm numaralarını bu sürüm ile birlikte dağıtılabilir:

| HDI | HDI kümesi sürüm | HDP | HDP derleme |
| --- | --- | --- | --- |
| 2.1 |2.1.10.989.2441725 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.989.2441725 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.989.2441725 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.989.2441725 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.989.2441725 |2.3 |2.3.3.1-21 |

## <a name="notes-for-07072016-release-of-hdinsight"></a>Hdınsight 07/07/2016 sürüm notları
Linux tabanlı Hdınsight kümeleri Hello tam sürüm numaralarını bu sürüm ile birlikte dağıtılabilir:

| HDI | HDI kümesi sürüm | HDP | HDP derleme |
| --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7864996 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.1000.0.7864996 |2.3 |2.3.3.1-18 |
| 3.4 |3.4.1000.0.7861906 |2.4 |2.4.2.0 |

Windows tabanlı Hdınsight kümeleri Hello tam sürüm numaralarını bu sürüm ile birlikte dağıtılabilir:

| HDI | HDI kümesi sürüm | HDP | HDP derleme |
| --- | --- | --- | --- |
| 2.1 |2.1.10.977.2413853 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.977.2413853 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.977.2413853 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.977.2413853 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.977.2413853 |2.3 |2.3.3.1-21 |

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin Spark, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| [Intellij için Hdınsight araçları](hdinsight-apache-spark-intellij-tool-plugin.md) |Hdınsight Spark kümeleri için Intellij Idea eklentisi Intellij için artık Azure araç seti ile tümleşiktir. Azure SDK'sı v2.9.1, en son Java SDK'ları, destekler ve hello tek başına Intellij için Hdınsight eklentisi tüm hello özellikleri içerir. |Araçlar |Spark |Yok |
| [Eclipse için Hdınsight araçları](hdinsight-apache-spark-eclipse-tool-plugin.md) |Eclipse için Azure Araç Seti artık Hdınsight Spark kümeleri destekler. Hello aşağıdaki özellikleri sağlar: <ul><li>Oluşturma ve Spark uygulama kolayca Scala ve Java birinci sınıf destek IntelliSense, otomatik biçimlendirme, hata denetimi, vb. için yazma ile yazma.</li><li>Merhaba Spark uygulamayı yerel olarak test edin.</li><li>Merhaba sonuçları almak ve işleri tooHDInsight Spark kümesi göndermek.</li><li>İçinde tooAzure oturum ve Azure aboneliği ile ilişkili tüm hello Spark kümeleri erişebilirsiniz.</li><li>Tüm ilişkili hello depolama kaynaklarını Hdınsight Spark kümenizin gidin.</li></ul> |Araçlar |Spark |Yok |

Bu sürüm ile başlayarak, hello konuk işletim sistemi düzeltme eki uygulama ilkesi Linux tabanlı Hdınsight kümeleri için değiştirilmiştir. Merhaba hello yeni ilke hedefidir toosignificantly yeniden başlatmalar hello sayısını azaltın son toopatching. her Pazartesi ya da verilmiş bir küme düğümleri arasında 00: 00 UTC aşamalı bir şekilde başlayarak Perşembe Hello yeni ilke düzeltme ekleri sanal makinelerde (VM'ler) Linux kümeleri. Ancak, belirli bir VM yalnızca en fazla 30 tooguest OS düzeltme eki uygulama son günde bir kez yeniden başlatır. Ayrıca, yeni oluşturulan bir küme için hello ilk yeniden başlatma hello küme oluşturma tarihten itibaren 30 gün daha erken gerçekleşmez.

> [!NOTE]
> Bu değişiklikler yalnızca kümeleri veya daha büyük bu sürümü oluşturulan toonewly uygulanır.
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a>Hdınsight 06/06/2016 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

| HDP | HDI sürümü | Spark sürüm | Ambari yapı numarası | HDP yapı numarası |
| --- | --- | --- | --- | --- |
| 2.3 |3.3.1000.0.7702215 |1.5.2 |2.2.1.8-2 |2.3.3.1-18 |
| 2.4 |3.4.1000.0.7702224 |1.6.1 |2.2.1.8-2 |2.4.2.0 |

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin Spark, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Hdınsight'ta Spark, genel olarak kullanılabilir |Bu sürüm, kullanılabilirlik, ölçeklenebilirlik ve üretkenlik tooopen kaynak hdınsight'ta Apache Spark geliştirmeleri getirir. <ul><li>Endüstri lideri kullanılabilirlik % 99,9 SLA yoğun kurumsal iş yükleri için uygun olmasını sağlayan.</li><li>Azure Data Lake Store kullanarak ölçeklenebilir depolama katmanı.</li><li>Veri keşfi ve geliştirme her aşaması için üretkenlik araçları. Etkileşimli veri incelemeyi özelleştirilmiş Spark çekirdeği ile Jupyter Not etkinleştirmek, Power BI ve Tableau Qlik gibi BI panoları ile tümleştirme hızlı veri paylaşımı ve sürekli raporlama için yararlı olan, Intellij eklentisi uzun vadeli kodu için güvenilir bir seçenektir Yapı geliştirme ve hata ayıklama.</li></ul> |Hizmet |Spark |Yok |
| Intellij için Hdınsight araçları |Bu, Hdınsight Spark kümeleri için Intellij Idea bir eklentidir. Hello aşağıdaki özellikleri sağlar:<ul><li>Oluşturma ve Spark uygulama kolayca Scala ve Java birinci sınıf destek IntelliSense, otomatik biçimlendirme, hata denetimi, vb. için yazma ile yazma.</li><li>Merhaba Spark uygulamayı yerel olarak test edin.</li><li>Merhaba sonuçları almak ve işleri tooHDInsight Spark kümesi göndermek.</li><li>İçinde tooAzure oturum ve Azure aboneliği ile ilişkili tüm hello Spark kümeleri erişebilirsiniz.</li><li>Tüm ilişkili hello depolama kaynaklarını Hdınsight Spark kümenizin gidin.</li><li>Tüm hello işleri geçmişi ve iş bilgilerini Hdınsight Spark kümenizin gidin.</li><li>Spark işlerinin masaüstü bilgisayarınızdan uzaktan hata ayıklama.</li></ul> |Araçlar |Spark |Yok |

## <a name="notes-for-05132016-release-of-hdinsight"></a>Hdınsight 13/05/2016 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight (Windows) 2.1.10.875.2159884 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight (Windows) 3.0.6.875.2159884 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight (Windows) 3.1.4.922.2266903 (HDP 2.1.15.0-2374 değişmeden -)
* Hdınsight (Windows) 3.2.7.922.2266903 (HDP 2.2.9.1-11)
* Hdınsight (Windows) 3.3.0.922.2266903 (HDP 2.3.3.1-18)
* Hdınsight (Linux) 3.2.1000.0.7565644 (HDP 2.2.9.1-11)
* Hdınsight (Linux) 3.3.1000.0.7565644 (HDP 2.3.3.1-18)
* Hdınsight (Linux) 3.4.1000.0.7548380 (HDP 2.4.2.0)

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin Spark, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Spark sürüm güncelleştirmesi ve diğer hata düzeltmeleri |Bu sürüm hello Spark Hdınsight küme too1.6.1 sürümünde güncelleştirir ve diğer hataları düzeltir |Hizmet |Spark |Yok |

## <a name="notes-for-04112016-release-of-hdinsight"></a>Hdınsight 11/04/2016 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight (Windows) 2.1.10.889.2191206 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight (Windows) 3.0.6.889.2191206 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight (Windows) 3.1.4.889.2191206 (HDP 2.1.15.0-2374 değişmeden -)
* Hdınsight (Windows) 3.2.7.889.2191206 (HDP 2.2.9.1-10)
* Hdınsight (Windows) 3.3.0.889.2191206 (HDP 2.3.3.1-16-değişmeden)
* Hdınsight (Linux) 3.2.1000.0.7339916 (HDP 2.2.9.1-10)
* Hdınsight (Linux) 3.3.1000.0.7339916 (HDP 2.3.3.1-16)
* Hdınsight (Linux) 3.4.1000.0.7338911 (HDP 2.4.1.1-3)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| HDI 3.4 için özel meta depo yükseltme sorunları |Başka bir Hdınsight kümesi daha düşük bir sürümünü daha önce kullanılan bir özel meta depo, kullandıysanız, küme oluşturma işlemi başarısız olur. Şimdi sabit tooan yükseltme komut dosyası hatası, bu |Küme oluşturma |Tümü |Yok |
| Livy kilitlenme kurtarma |Livy gönderilen herhangi bir iş için iş durumu dayanıklılık sağlar |Güvenilirlik |Linux üzerinde Spark |Yok |
| Jupyter içerik HA |Merhaba özelliği toosave ve yük Jupyter not defteri içeriği tooand hello kümesi ile ilişkili hello depolama hesabından sağlar. Daha fazla bilgi için bkz: [defterlerinde Jupyter not defterleri için kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Dizüstü bilgisayarlar |Linux üzerinde Spark |Yok |
| Jupyter not defterleri hiveContext kaldırılması |Kullanım `%%sql` yerine Sihirli `%%hive` Sihirli. SqlContext eşdeğer toohiveContext ' dir. Daha fazla bilgi için bkz: [tekrar Jupyter not defterleri için kullanılabilir](hdinsight-apache-spark-jupyter-notebook-kernels.md) |Dizüstü bilgisayarlar |Linux üzerinde Spark kümeleri |Yok |
| Eski Spark sürümlerinin kullanımdan kaldırma |Eski sürümü Spark 1.3.1 5/31 üzerinde hello hizmetinden kaldırıldı |Hizmet |Windows üzerinde Spark kümeleri |Yok |

## <a name="notes-for-03292016-release-of-hdinsight"></a>Hdınsight 03/29/2016 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight (Windows) 2.1.10.875.2159884 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight (Windows) 3.0.6.875.2159884 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight (Windows) 3.1.4.875.2159884 (HDP 2.1.15.0-2374 değişmeden -)
* Hdınsight (Windows) 3.2.7.875.2159884 (HDP 2.2.9.1-7 değişmeden -)
* Hdınsight (Windows) 3.3.0.875.2159884 (HDP 2.3.3.1-16)
* Hdınsight (Linux) 3.2.1000.0.7193255 (HDP 2.2.9.1-8 değişmeden -)
* Hdınsight (Linux) 3.3.1000.0.7193255 (HDP 2.3.3.1-7 değişmeden -)
* Hdınsight (Linux) 3.4.1000.0.7195842 (HDP 2.4.1.0-327)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Eklenen Hdınsight 3.4 sürüm ve tüm Hdınsight kümeleri için güncelleştirilmiş HDP sürümleri |Bu sürüm ile (HDP 2.4 üzerinde bağlı olarak) Hdınsight v3.4 eklediyseniz ve diğer HDP sürümleri de güncelleştirdiniz. HDP 2.4 sürüm notları kullanılabilir [burada](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html) ve Hdınsight sürümleri hakkında daha fazla bilgi bulunabilir [burada](hdinsight-component-versioning.md). |Hizmet |Tüm Linux kümeleri |Yok |
| Hdınsight Premium |Hdınsight iki kategoride - standart ve Premium kullanıma sunulmuştur. Hdınsight Premium şu anda önizlemede ve Hadoop için kullanılabilir ve Linux üzerinde Spark kümeleri. Daha fazla bilgi için bkz: [burada](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium). |Hizmet |Hadoop ve Linux üzerinde Spark |Yok |
| Microsoft R Server |Hdınsight Premium Linux'ta Hadoop ve Spark kümeleri ile birlikte Microsoft R Server sağlar. Daha fazla bilgi için bkz: [hdınsight'ta R Server genel bakış](hdinsight-hadoop-r-server-overview.md). |Hizmet |Hadoop ve Linux üzerinde Spark |Yok |
| Spark 1.6.0 |Hdınsight 3.4 kümeleri artık Spark 1.6.0 içerir |Hizmet |Linux üzerinde Spark kümeleri |Yok |
| Jupyter not defteri geliştirmeleri |Jupyter not defterleri ile Spark kümeleri kullanılabilir ek Spark çekirdek şimdi sağlar. Bunlar ayrıca kullanımı gibi geliştirmeler %% Sihirli, otomatik Görselleştirme ve Python görselleştirme kitaplıkları (örneğin, matplotlib) ile tümleştirme. Daha fazla bilgi için bkz: [defterlerinde Jupyter not defterleri için kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Hizmet |Linux üzerinde Spark kümeleri |Yok |

## <a name="notes-for-03222016-release-of-hdinsight"></a>Hdınsight 22/03/2016 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight (Windows) 2.1.10.875.2159884 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight (Windows) 3.0.6.875.2159884 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight (Windows) 3.1.4.875.2159884 (HDP 2.1.15.0-2374 değişmeden -)
* Hdınsight (Windows) 3.2.7.875.2159884 (HDP 2.2.9.1-7 değişmeden -)
* Hdınsight (Windows) 3.3.0.875.2159884 (HDP 2.3.3.1-16)
* Hdınsight (Linux) 3.2.1000.0.7193255 (HDP 2.2.9.1-8 değişmeden -)
* Hdınsight (Linux) 3.3.1000.0.7193255 (HDP 2.3.3.1-7 değişmeden -)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Tüm Hdınsight kümeleri için güncelleştirilmiş Hdınsight sürümleri |Bu sürümle birlikte, biz tüm Hdınsight kümeleri için Hdınsight sürümleri güncelleştirdiniz |Hizmet |Tümü |Yok |

## <a name="notes-for-03102016-release-of-hdinsight"></a>Hdınsight 03/10/2016 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight (Windows) 2.1.10.859.2123216 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight (Windows) 3.0.6.859.2123216 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight (Windows) 3.1.4.859.2123216 (HDP 2.1.15.0-2374 değişmeden -)
* Hdınsight (Windows) 3.2.7.859.2123216 (HDP 2.2.9.1-7)
* Hdınsight (Windows) 3.3.0.859.2123216 (HDP 2.3.3.1-5 değişmeden -)
* Hdınsight (Linux) 3.2.1000.7076817 (HDP 2.2.9.1-8)
* Hdınsight (Linux) 3.3.1000.7076817 (HDP 2.3.3.1-7)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Tüm Hdınsight kümeleri için güncelleştirilmiş Hdınsight sürümleri |Bu sürümle birlikte, biz tüm Hdınsight kümeleri için Hdınsight sürümleri güncelleştirdiniz |Hizmet |Tümü |Yok |

## <a name="notes-for-01272016-release-of-hdinsight"></a>Hdınsight 27/01/2016 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight (Windows) 2.1.10.817.2028315 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight (Windows) 3.0.6.817.2028315 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight (Windows) 3.1.4.817.2028315 (HDP 2.1.15.0-2374 değişmeden -)
* Hdınsight (Windows) 3.2.7.817.2028315 (HDP 2.2.9.1-1)
* Hdınsight (Windows) 3.3.0.817.2028315 (HDP 2.3.3.1-5 değişmeden -)
* Hdınsight (Linux) 3.2.1000.4072335 (HDP 2.2.9.1-1)
* Hdınsight (Linux) 3.3.1000.4072335 (HDP 2.3.3.1-1)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Tüm Hdınsight kümeleri için güncelleştirilmiş Hdınsight sürümleri |Bu sürümle birlikte, biz tüm Hdınsight kümeleri için Hdınsight sürümleri güncelleştirdiniz |Hizmet |Tümü |Yok |

## <a name="notes-for-12022015-release-of-hdinsight"></a>Hdınsight 02/12/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight (Windows) 2.1.10.763.1931434 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight (Windows) 3.0.6.763.1931434 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight (Windows) 3.1.4.763.1931434 (HDP 2.1.15.0-2374 değişmeden -)
* Hdınsight (Windows) 3.2.7.763.1931434 (HDP 2.2.7.1-34 değişmeden -)
* Hdınsight (Windows) 3.3.1000.0 (HDP 2.3.3.1-5)
* Hdınsight (Linux) 3.2.1000.0.6392801 (HDP 2.2.7.1-34 değişmeden -)
* Hdınsight (Linux) 3.3.1000.0 (HDP 2.3.3.0-3039)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Eklenen Hdınsight 3.3 Sürüm ve tüm Hdınsight kümeleri için güncelleştirilmiş HDP sürümleri |Bu sürüm ile (HDP 2.3 üzerinde bağlı olarak) Hdınsight v3.3 eklediyseniz ve diğer HDP sürümleri de güncelleştirdiniz. HDP 2.3 sürüm notları kullanılabilir [burada](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html) ve Hdınsight sürümleri hakkında daha fazla bilgi bulunabilir [burada](hdinsight-component-versioning.md). |Hizmet |Tümü |Yok |

## <a name="notes-for-11302015-release-of-hdinsight"></a>Hdınsight 11/30/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight (Windows) 2.1.10.757.1923908 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight (Windows) 3.0.6.757.1923908 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight (Windows) 3.1.4.757.1923908 (HDP 2.1.15.0-2374 değişmeden -)
* Hdınsight (Windows) 3.2.7.757.1923908 (HDP 2.2.7.1-34)
* Hdınsight (Linux) 3.2.1000.0.6392801 (HDP 2.2.7.1-34)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Tüm Hdınsight kümeleri ve Hdınsight 3.2 kümeleri (Windows ve Linux) için HDP sürümleri için güncelleştirilmiş Hdınsight sürümleri |Bu sürümle birlikte, Hdınsight ve HDP sürümleri güncelleştirildi |Hizmet |Tümü |Yok |

## <a name="notes-for-10272015-release-of-hdinsight"></a>Hdınsight 27/10/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight (Windows) 2.1.10.726.1866228 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight (Windows) 3.0.6.726.1866228 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight (Windows) 3.1.4.726.1866228 (HDP 2.1.15.0-2374 değişmeden -)
* Hdınsight (Windows) 3.2.7.726.1866228 (HDP 2.2.7.1-33)
* Hdınsight (Linux) 3.2.1000.0.6035701 (HDP 2.2.7.1-33)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Güncelleştirilmiş Hdınsight sürümleri tüm Hdınsight kümeleri (Windows ve Linux) |Bu sürümle birlikte, Hdınsight ve HDP sürümleri güncelleştirildi |Hizmet |Tümü |Yok |
| Büyük harf kümeleriyle sabit Jupyter için Windows Spark kümeleri |Büyük harflerle belirtilen DNS adları olan kümeleri Jupyter not defterleri tooan kaynak isteği onay son ile ilgili sorunları var. Merhaba düzeltme toochange hello DNS adı Jupyter'ın yapılandırma toolower çalışması için oluştu. |Hizmet |Hdınsight Spark (Windows) |Yok |

## <a name="notes-for-10202015-release-of-hdinsight"></a>Hdınsight 20/10/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.716.1846990 (Windows) (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.716.1846990 (Windows) (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.4.716.1846990 (Windows) (HDP 2.1.16.0-2374)
* Hdınsight 3.2.7.716.1846990 (Windows) (HDP 2.2.7.1-0004)
* Hdınsight 3.2.1000.0.5930166 (Linux) (HDP 2.2.7.1-0004)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Varsayılan HDP değiştirilmiş sürümünü tooHDP 2.2 |Merhaba varsayılan Hdınsight Windows kümeleri için değiştirilmiş tooHDP 2.2 sürümüdür. Hdınsight sürüm 3.2 (HDP 2.2) Şubat 2015 tarihinden itibaren içinde genellikle kullanılmaktadır. Açık bir seçim hello Azure portal, PowerShell cmdlet'lerini veya hello SDK kullanarak hello küme hazırlama sırasında değil yapıldığında bu değişikliği hello varsayılan küme sürümü, yalnızca çevirir. |Hizmet |Tümü |Yok |
| Birden çok Hdınsight Linux kümeleri tek bir sanal ağ üzerinde dağıtmak için VM adı biçiminde değişiklikler |Tek bir sanal ağda birden çok Hdınsight Linux kümeleri dağıtmak için destek bu sürümde eklenir. Güncelleştirmesinin bir parçası olarak, headnode hello kümedeki sanal makine adlarının hello biçimi değişmiştir\*, workernode\* ve zookeepernode\* toohn\*, aşağı\*ve zk\* sırasıyla. Bu konu toochange olduğundan önerilen uygulama tootake sanal makine adları hello biçimi doğrudan bağımlı değildir. "Hostname -f" Merhaba yerel makine veya Ambari API toodetermine hello listesi ana bilgisayarları ve bileşenleri toohosts hello eşlenmesini kullanın. Daha fazla bilgi konumunda bulabilirsiniz [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) ve [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md). |Hizmet |Linux'ta Hdınsight kümeleri |Yok |
| Yapılandırma değişiklikleri |Hdınsight 3.1 kümeler için aşağıdaki yapılandırmaları hello şimdi etkinleştirilir: <ul><li>Tez.yarn.ATS.Enabled ve yarn.log.server.url. Bu uygulama zaman çizelgesi sunucusu hello ve hello günlük sunucu toobe mümkün tooserve günlükleri çıkışı sağlar.</li></ul>Hdınsight 3.2 kümeler için aşağıdaki yapılandırmaları hello değiştirilmiş: <ul><li>mapreduce.fileoutputcommitter.algorithm.Version too2 ayarlandı. Bu sayede hello FileOutputCommitter hello V2 sürümünün kullanılabilir.</li></ul> |Hizmet |Tümü |Yok |

## <a name="notes-for-09092015-release-of-hdinsight"></a>Hdınsight 09/09/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.675.1768697 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.675.1768697 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.4.675.1768697 (HDP 2.1.15.0-2334 değişmeden -)
* Hdınsight 3.2.6.675.1768697 (HDP 2.2.6.1-0012 değişmeden -)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Tüm Hdınsight kümeleri için güncelleştirilmiş Hdınsight sürümleri |Bu sürümle birlikte, Hdınsight sürümleri güncelleştirildi |Hizmet |Tümü |Yok |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Hdınsight 31/07/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.640.1695824 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.640.1695824 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.4.640.1695824 (HDP 2.1.15.0-2334 değişmeden -)
* Hdınsight 3.2.6.640.1695824 (HDP 2.2.6.1-0012 değişmeden -)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Spark küme düğümü yeniden görüntüsünü oluşturuyor iş akışı Düzelt |Spark küme düğümleri toonot yeniden görüntü oluşturma sonra kurtarmak neden olan bir hata sabit |Hizmet |Spark |Yok |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Hdınsight 31/07/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.635.1684502 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.635.1684502 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.4.635.1684502 (HDP 2.1.15.0-2334 değişmeden -)
* Hdınsight 3.2.6.635.1684502 (HDP 2.2.6.1-0012 değişmeden -)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Tüm Hdınsight kümeleri için güncelleştirilmiş Hdınsight sürümleri |Bu sürümle birlikte, Hdınsight sürümleri güncelleştirildi |Hizmet |Tümü |Yok |

## <a name="notes-for-07072015-release-of-hdinsight"></a>Hdınsight 07/07/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.610.1630216 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.610.1630216 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.4.610.1630216 (HDP 2.1.15.0-2334 değişmeden -)
* Hdınsight 3.2.4.610.1630216 (HDP 2.2.6.1-0012)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

| Başlık | Açıklama | Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı) | Küme türü (örneğin, Hadoop, HBase veya Storm) | JIRA (varsa) |
| --- | --- | --- | --- | --- |
| Hdınsight 3.2 kümeleri için güncelleştirilmiş HDP sürümleri |Bu sürümle birlikte, Hdınsight 3.2 HDP 2.2.6.1-0012 dağıtır. |Hizmet |Tümü |Yok |

## <a name="notes-for-06262015-release-of-hdinsight"></a>Hdınsight 06/26/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.601.1610731 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.601.1610731 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.4.601.1610731 (HDP 2.1.15.0-2334 değişmeden -)
* Hdınsight 3.2.4.601.1610731 (HDP 2.2.6.1-0011)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Hdınsight 3.2 kümeleri için güncelleştirilmiş HDP sürümleri</td>
<td>Bu sürümle birlikte, Hdınsight 3.2 HDP 2.2.6.1 dağıtır.</td>
<td>Hizmet</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-06182015-release-of-hdinsight"></a>Hdınsight 18/06/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.596.1601657 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.596.1601657 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.4.596.1601657 (HDP 2.1.15.0-2334)
* Hdınsight 3.2.4.596.1601657 (HDP 2.2.6.1-0002)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Açılan ek HTTPS bağlantı noktaları</td>
<td>Merhaba bulut hizmeti artık 5 bağlantı noktaları 8001 too8005 örn hello kümede açar https:// adresindeki<clustername>.azurehdinsight.net:8001/. Toothese URL'leri kullanarak doğrulaması istekleri hello aynı temel kimlik doğrulaması parola mekanizması olarak bağlantı noktası 443'tür. Bu bağlantı noktalarının aynı bağlantı noktası üzerinde hello etkin headnode toohello bağlayın. Betik eylemleri kullanılan toomake Müşteri Hizmetleri kümede hello headnode ve rota toooutside hello Bu bağlantı noktalarını dinler olabilir.</td>
<td>Bulut hizmeti</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>Hdınsight 3.2 aralıklı MapReduce karışık sorunun</td>
<td>Harita azaltmak karışık büyük kümelerinde bazen görev hatalarına kaynaklanan bir nadir, aralıklı yarış durumu düzeltin. Bkz: <a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE 6361</a> daha fazla bilgi için.</td>
<td>Hadoop çekirdek</td>
<td>Tümü</td>
<td><a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE 6361</a></td>
</tr>
<tr>
<td>Azure Java SDK 2.2 tooLatest Hdınsight 3.2 için taşıma</td>
<td>Merhaba hello WASB sürücü tarafından kullanılan Java için Azure SDK sürümünü toolatest taşındı. Merhaba son SDK var birkaç düzeltmeler ve hello hello sürüm notları aynı https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt kullanılabilir.</td>
<td>Hadoop çekirdek</td>
<td>Tümü</td>
<td><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP 11959</a></td>
</tr>
<tr>
<td>TooHDP 2.1.15 Hdınsight 3.1 kümeleri için taşıma</td>
<td>Merhaba yayın için Hortonworks sürüm notları kullanılabilir <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">burada</a>.</td>
<td>HDP</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a>Hdınsight 06/04/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.583.1575584 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.583.1575584 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.3.583.1575584 (HDP 2.1.12.1-0003 değişmeden -)
* Hdınsight 3.2.4.583.1575584 (HDP 2.2.6.1-1)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Storm kümeleri için 502 hatalı ağ geçidi hata düzeltme</td>
<td>Bu sürüm, yeniden başlatmanın ardından aşağı hello Web sitesi toobe neden hello iş gönderme API etkileyen bir hata düzeltmeleri.</td>
<td>Hizmet</td>
<td>Storm</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a>Hdınsight 06/01/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.577.1563827 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.577.1563827 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.3.577.1563827 (HDP 2.1.12.1-0003 değişmeden -))
* Hdınsight 3.2.4.577.1563827 (HDP 2.2.6.0-2800 değişmeden -)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Çeşitli hata düzeltmeleri</td>
<td>Bu sürüm hataları düzeltir toocluster sağlama ilgili.</td>
<td>Hizmet</td>
<td>Tüm küme türleri</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a>Hdınsight 27/05/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 3.2.4.570.1554102 (HDP 2.2.6.0-2800)
* Diğer küme sürümleri ve SDK bu sürümünün bir parçası dağıtılmaz.

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>HDP 2.2 güncelleştirme</td>
<td>Bu Hdınsight 3.2 sürümünde HDP 2.2.6 içerir ve birkaç önemli hata düzeltmeleri tooHDInsight getirir. Merhaba tam sürüm notları kullanılabilir <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 sürüm notları</a>.</td>
<td>HDP</td>
<td>Tüm küme türleri</td>
<td>Yok</td>
</tr>
<tr>
<td>TooDefault Yarn kapsayıcı bellek yapılandırmasını değiştirme</td>
<td>Bu güncelleştirmede hello varsayılan kullanılabilir bellek tooYARN kapsayıcıları (yarn.nodemanager.resource.memory mb ve yarn.scheduler.maximum ayırma mb), düğüm Yöneticisi tarafından başlatılan, artan too5632MB. Azaltılmış too4608MB, daha önce bu, ancak bağlı olarak çeşitli iş çalışır, hello yeni değeri daha iyi güvenilirlik ve performans toomost işleri sağlaması gerekir, bu nedenle daha iyi bir varsayılandır. Bu bellek yapılandırmasına kritik bağımlılığı varsa, her zamanki gibi açıkça hello küme oluşturulurken ayarlayın.</td>
<td>HDP</td>
<td>Tüm küme türleri</td>
<td>Yok</td>
</tr>
<tr>
<td>HBase ve Storm kümeleri için varsayılan yapılandırma eşlik</td>
<td>Bu güncelleştirme Hbase geri yükler ve Storm kümeleri toouse hello YARN yapılandırmalar aynı değerleri Hadoop kümeleri olarak. Bu, tüm küme türlerine eşlik için gerçekleştirilir.</td>
<td>HDP</td>
<td>HBase, Storm</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a>Hdınsight 20/05/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.564.1542093 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.564.1542093 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.3.564.1542093 (HDP 2.1.12.1-0003)
* Hdınsight 3.2.4.564.1542093 (HDP 2.2.4.6-2)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>SCP.NET EventHub desteği</td>
<td>güncelleştirilmiş hello küme paketler Hdınsight Storm için yeni özellikler tooSCP.NET getirin. Artık daha kolay toouse EventHubSpout veya Java Spout'lar olun topoloji Oluşturucu erişim toonew API'leri var. Merhaba sözleşmeleri güncelleştirilmiş gibi yeni kümeleriyle SCP.NET İstemci SDK toowork güncelleştirmeniz gerekir. Merhaba hakkında ayrıntılı bilgi için toohello hello SCP.NET NuGet paketi dahil Benioku yeni API, kullanım ve sürüm notları (hata düzeltmeleri de dahil olmak üzere) bakın.</td>
<td>VS Tooling</td>
<td>Storm Hdınsight 3.2 kümeleri</td>
<td>Yok</td>
</tr>
<tr>
<td>JDBC sürücüsü güncelleştirme</td>
<td>Güncelleştirilmiş hello sürücü toohello SQL Server sürümü sqljdbc_4.1.5605.100 içinde desteklenir.</td>
<td>Meta depo</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a>Hdınsight 27/04/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.537.1486660 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.537.1486660 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.3.537.1486660 (HDP 2.1.12.0-2329 değişmeden -)
* Hdınsight 3.2.3.537.1486660 (HDP 2.2.2.2-4)
* SDK'SI 1.5.8

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>DLL bağımlılık Düzelt</td>
<td>Birim testi çerçevesi Hdınsight bağlılığı kaldırır.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>Yok</td>
</tr>
<tr>
<td>Yarış durumu için hata düzeltmesi</td>
<td>PUT üzerinde bekler hello durumunu yoklama önce kabul toobe isteği şimdi bir küme oluşturma isteği</td>
<td>SDK</td>
<td>Hadoop</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a>Hdınsight 14/04/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.521.1453250 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.521.1453250 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.3.521.1453250 (HDP 2.1.12.0-2329 değişmeden -)
* Hdınsight 3.2.3.525.1459730 (HDP 2.2.2.2-2)
* SDK'SI 1.5.6

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Tez hata düzeltmeleri</td>
<td>Apache TEZ 2214 ve TEZ 1923 için düzeltmeler bu HDI 3.2 sürümünde bulunmaktadır. Bunlar tooshuffle önemli miktarda veri gerektiren belirli Hive sorguları için Tez üzerinde gerekli.
</td>
<td>HDP</td>
<td>Hadoop</td>
<td><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></br><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a>Hdınsight 06/04/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.521.1453250 (HDP 1.3.12.0-01795 değişmeden -)
* Hdınsight 3.0.6.521.1453250 (HDP 2.0.13.0-2117 değişmeden -)
* Hdınsight 3.1.3.521.1453250 (HDP 2.1.12.0-2329 değişmeden -)
* Hdınsight 3.2.3.521.1453250 (HDP 2.2.2.2-1)
* SDK'SI 1.5.6

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Hdınsight .NET SDK'sı 1.5.6</td>
<td>Linux'ta Hdınsight için bazı iç sınıflar tooremove güncelleştirir.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>Yok</td>
</tr>
<tr>
<td>Avro kitaplığı 1.5.6</td>
<td>Eklenen <b>KnownTypeAttribute</b> yöntemi için <b>GetAllKnownTypes</b>. Bir tür için GetAllKnownTypes yöntemi null olduğunda sabit NullReferenceException.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>Yok</td>
</tr>
<tr>
<td>Hata düzeltmeleri</td>
<td>Çeşitli hata düzeltmeleri toohello hizmeti</td>
<td>Hizmet</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a>Hdınsight 01/04/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.513.1431705 (HDP 1.3.12.0-01795)
* Hdınsight 3.0.6.513.1431705 (HDP 2.0.13.0-2117)
* Hdınsight 3.1.3.513.1431705 (HDP 2.1.12.0-2329)
* Hdınsight 3.2.3.513.1431705 (HDP 2.2.2.1-2600)
* SDK'SI 1.5.5

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Özelliği tooenable/devre dışı bırak Uzak Masaüstü kimlik bilgilerinin .NET SDK'sı üzerinden Windows kümeleri hakkında</td>
<td>RDP kimlik bilgileri Windows kümelerde devre dışı bırakma veya etkinleştirme programlama desteği.</td>
<td>SDK</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>Özelliği tooenable Uzak Masaüstü kimlik bilgileri sağlanır sırada kümeleri hakkında</td>
<td>Merhaba küme oluşturulmakta olduğu gibi Uzak Masaüstü kimlik bilgilerini etkinleştirmek için programlama desteği. Bu ilk sağlama hello kümesi ve Uzak Masaüstü'nü etkinleştirme hello iki adımlı işlem kaldırır.</td>
<td>SDK</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>Yükseltilen Python too2.7.8</td>
<td>Hdınsight sürüm 2.1, 3.0, 3.1 ve 3.2 için bazı önemli güvenlik içeren yükseltilmiş Python Hdınsight kümeleri tooPython 2.7.8, üzerinde düzeltmeler</td>
<td>Hizmet</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>YARN yapılandırma değişikliği</td>
<td>Değiştirilen YARN yapılandırma yarn.resourcemanager.max tamamlandı uygulamaları too1000 Hdınsight sürüm 3.1 ve 3.2 tüm küme türleri. Bu değer yalnızca hello hello YARN kullanıcı Arabiriminde tamamlanmış uygulamaların listesini denetler. olan uygulamalar hakkında bilgi tooget önceki toohello toohello geçmişi sunucu doğrudan gidebilirsiniz hello UI, üzerinde gösterilen uygulamalar listesini gönderildi.</td>
<td>YARN</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>Bir HBase kümesi düğüm yeniden boyutlandırma</td>
<td>HBase kümeleri artık düğümlerinin (yukarı ve aşağı) Hdınsight sürüm 3.1 ve 3.2 için yeniden boyutlandır</td>
<td>Hizmet</td>
<td>HBase</td>
<td>Yok</td>
</tr>
<tr>
<td>JDBC yükseltme</td>
<td>SQL JDBC sürücüsü, Hdınsight sürüm 3.2 için yükseltilen tooversion sqljdbc_4.0.2206.100 değil. Bu sürüm önemli güvenlik geliştirmeleri içerir.</td>
<td>HDP</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>JVM yapılandırmasını güncelleştirme</td>
<td>Güncelleştirilmiş JVM yapılandırma networkaddress.cache.ttl too300 saniyeden hello varsayılan değer-1 Hdınsight sürüm 3.1 ve 3.2. Bu yapılandırma değeri hello İlkesi hello adı hizmetinden başarılı adı aramaları için önbelleğe alma denetler. Bu bir hata düzeltmeleri ilgili toogrowing ve HBase kümeleri küçültme.</td>
<td>Hizmet</td>
<td>HBase</td>
<td>Yok</td>
</tr>
<tr>
<td>Yükseltme tooAzure 2.0 Java için depolama SDK'sı</td>
<td>Hdınsight sürüm 3.2 yükseltilmiş toouse hello son hello Java için Azure depolama SDK sürümüdür. Bu, hello geçerli 0.6.0 sürümünün üzerine bazı önemli hata düzeltmeleri içerir.</td>
<td>HDP</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>Yükseltilen tooApache WASB kaynak kodu</td>
<td>Hdınsight sürüm 3.2 kullanır hello WASB dosya sistemi sürücüsünden Apache Hadoop için en son kod hello artık. Bu değişiklikle hello WASB sürücü ayrı bir jar şimdi paketlenmiştir. Bu yalnızca bir paketleme değişiklik ve tüm değişiklikleri toobehavior hello WASB sürücüsünün içermiyor. Merhaba bu JAR dosyasını hadoop azure 2.6.0.jar adıdır.</td>
<td>HDP</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>Hdınsight 3.2 dosya adı güncelleştirmelerinde jar</td>
<td>Bu güncelleştirme tooHDInsight sürüm 3.2 çeşitli hata düzeltmeleri içerir ve HDP bir parçası olarak paketlenmiş birkaç iç Kavanoz yükseltildi. Bu JAR filesare iç toohello HDP paketi ve müşteri uygulamalar tarafından doğrudan kullanmak için değil. Müşteri uygulamalar HDP iç Jar'lar bir yükseltme toohello değil bölün böylece uygulamaları kendi hello Kavanoz sürümü paketi.</td>
<td>HDP</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a>Hdınsight 03/03/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.488.1375841 (HDP 1.3.9.0-01351 değişmeden -)
* Hdınsight 3.0.6.488.1375841 (HDP 2.0.9.0-2097 değişmeden -)
* Hdınsight 3.1.3.488.1375841 (HDP 2.1.10.0-2290 değişmeden -)
* Hdınsight 3.2.3.488.1375841 (HDP-2.2.10.0-değişmeden 2340 -)
* SDK 1.5.0 (değiştirmeden)

Bu sürüm, güncelleştirmenin ardından hello içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA</th>
</tr>
<tr>
<td>Güvenilirlik geliştirmeleri</td>
<td>Biz hello hizmet tooscale hello artan yük ile saygı toocluster oluşturma ile daha iyi izin düzeltmeleri yapılan.</td>
<td>Hizmet</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a>Hdınsight 18/02/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.471.1342507 (HDP 1.3.9.0-01351 değişmeden -)
* Hdınsight 3.0.6.471.1342507 (HDP 2.0.9.0-2097 değişmeden -)
* Hdınsight 3.1.3.471.1342507 (HDP 2.1.10.0-2290 değişmeden -)
* Hdınsight 3.2.3.471.1342507 (HDP 2.2.10.0 2340)
* SDK'SI 1.5.0

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Hdınsight 3.2 kümeleri</td>
<td>Hadoop 2.6/HDP2.2 Hdınsight 3.2 kümeleriyle kullanılabilir. Önemli güncelleştirmeleri tooall hello açık kaynak bileşenleri içerir. Daha fazla bilgi için bkz: Hdınsight'ta yenilikler ve <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">HDP 2.2.0.0 sürüm notları</a>.</td>
<td>Açık kaynaklı yazılım</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>Hdınsight Linux (Önizleme)</td>
<td>Ubuntu Linux üzerinde çalışan kümeleri dağıtılabilir. Daha fazla bilgi için Linux'ta Hdınsight ile çalışmaya başlama bakın.</td>
<td>Hizmet</td>
<td>Hadoop</td>
<td>Yok</td>
</tr>
<tr>
<td>Storm genel kullanılabilirlik</td>
<td>Apache Storm kümeleri genel olarak kullanılabilir. Daha fazla bilgi için bkz: Get started Hdınsight'ta Storm kullanarak.</td>
<td>Hizmet</td>
<td>Storm</td>
<td>Yok</td>
</tr>
<tr>
<td>Sanal makine boyutları</td>
<td>Azure Hdınsight, daha fazla sanal makine türler ve boyutlarında kullanılabilir. Hdınsight genel amaçlar için A2 tooA7 boyutları kullanabilir; Katı hal sürücüleri (SSD) ve yüzde 60 daha hızlı işlemci özellik D-serisi düğümleri; ve hızlı ağ için InfiniBand sahip A8 ve A9 boyutlarını destekler.</td>
<td>Hizmet</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>Küme ölçeklendirme</td>
<td>Toodelete gerek kalmadan çalışan bir Hdınsight kümesine veri düğümlerini hello sayısını değiştirmek veya yeniden oluşturun. Şu anda yalnızca Hadoop sorgu ve Apache Storm küme türleri bu imkana sahip olmasının Apache HBase küme türü yakında toofollow desteği. Daha fazla bilgi için bkz: yönetmek Hdınsight kümeleri.</td>
<td>Hizmet</td>
<td>Hadoop, Storm</td>
<td>Yok</td>
</tr>
<tr>
<td>Visual Studio Araçları</td>
<td>Ayrıca Apache Storm, Apache Hive Visual Studio için tooling hello için tooling toocomplete güncelleştirilmiş tooinclude deyim tamamlama, yerel doğrulama ve hata ayıklama için geliştirilmiş destek olmuştur. Daha fazla bilgi için Visual Studio için Hdınsight Hadoop araçları ile çalışmaya başlama bakın.</td>
<td>Araçları</td>
<td>Hadoop</td>
<td>Yok</td>
</tr>
<td>Azure Cosmos DB için Hadoop Bağlayıcısı</td>
<td>Azure Cosmos DB Hadoop bağlayıcısıyla Azure Cosmos DB koleksiyonları arasında veya veritabanı hesapları arasında saklanan şema daha az JSON belgeleri üzerinden karmaşık toplamalar, analiz ve işlemeleri gerçekleştirebilirsiniz. Daha fazla bilgi ve bir öğretici için Azure Cosmos DB ve Hdınsight kullanarak çalıştırmak Hadoop işlerini bakın.</td>
<td>Hizmet</td>
<td>Hadoop</td>
<td>Yok</td>
</tr>
<tr>
<td>Hata düzeltmeleri</td>
<td>Biz Hdınsight Hizmetleri için çeşitli küçük hata düzeltmeleri yapıldı. Hiçbir müşteri dönük davranış değişiklikleri beklenir.</td>
<td>Hizmet</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-02062015-release-of-hdinsight"></a>Hdınsight 06/02/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.463.1325367 (HDP 1.3.9.0-01351 değişmeden -)
* Hdınsight 3.0.6.463.1325367 (HDP 2.0.9.0-2097 değişmeden -)
* Hdınsight 3.1.2.463.1325367 (HDP 2.1.10.0-2290)
* SDK'SI YOK

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Hata düzeltmeleri</td>
<td>Biz Hdınsight Hizmetleri için çeşitli küçük hata düzeltmeleri yapıldı. Hiçbir müşteri dönük davranış değişiklikleri beklenir.</td>
<td>Hizmet</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>HDP 2.1 bakım güncelleştirmesi</td>
<td>Hdınsight 3.1 güncelleştirilmiş toodeploy HDP 2.1.10.0 ' dir. Daha fazla bilgi için bkz: <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">sürüm notları HDP-2.1.10</a>. </td>
<td>Açık kaynaklı yazılım</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>HDP ikili güncelleştirmeleri</td>
<td>HBase için hangi dosya adları güncelleştirilmiş birkaç JAR dosyalarını vardır. Müşteriler bu JAR dosyalarını hello adlarına göre bir bağımlılık olması beklenmez şekilde bu JAR dosyaları HBase tarafından dahili olarak kullanılır. Bunlar:
<ul>
<li>./lib/jetty-6.1.26.hwx.jar</li>
<li>./lib/jetty-sslengine-6.1.26.hwx.jar</li>
<li>./lib/jetty-Util-6.1.26.hwx.jar</li>
</ul>
</td>
<td>Açık kaynaklı yazılım</td>
<td>HBase</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-1292015-release-of-hdinsight"></a>Hdınsight 29/1/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.455.1309616 (HDP 1.3.9.0-01351 değişmeden -)
* Hdınsight 3.0.6.455.1309616 (HDP 2.0.9.0-2097 değişmeden -)
* Hdınsight 3.1.2.455.1309616 (HDP 2.1.9.0-2196 değişmeden -)
* SDK'SI YOK

Bu sürüm, güncelleştirmenin ardından hello içerir:

<table border="1">

<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Etkilenen alan (örneğin, hizmet, bileşen veya SDK'sı)</p></th>
<th>Küme türü (örneğin, Hadoop, HBase veya Storm)</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Hata düzeltmeleri</td>
<td>Biz Azure yükseltmeler sırasında hello Hdınsight kümeleri hello güvenilirliğini geliştirmeye birkaç önemli hata düzeltmeleri yapıldı.</td>
<td>Hizmet</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a>Hdınsight 5/1/2015 sürüm notları
Bu sürüm ile dağıtılan Hdınsight kümeleri için Hello tam sürüm numaraları:

* Hdınsight 2.1.10.420.1246118 (HDP 1.3.9.0-01351 değişmeden -)
* Hdınsight 3.0.6.420.1246118 (HDP 2.0.9.0-2097 değişmeden -)
* Hdınsight 3.1.2.420.1246118 (HDP 2.1.9.0-2196 değişmeden -)

Bu sürüm hello şu güncelleştirmeleri içerir:

<table border="1">

<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Bileşen</th>
<th>Küme Türü</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Twitter eğilim analizi ve Mahout tabanlı film önerileri için örnek</td>
<td><p>Bu sürümde, iki ek örnekleri hello Hdınsight sorgu konsol vardır:</p>

<p><b>Twitter eğilim analizi</b><br>
Twitter gibi siteler tarafından sağlanan ortak API'ler verileri çözümlemek ve popüler eğilimleri anlamak için yararlı bir kaynaktır. Bu öğreticide, nasıl toouse Hive tooget belirli bir sözcük içeren çoğu tweet'leri hello gönderilen Twitter kullanıcıların listesini öğrenin. </p>

<p><b>Mahout film önerisi</b><br>
Apache Mahout learning kitaplığı, Apache Hadoop bir makinedir. Mahout (örneğin, filtreleme, Sınıflandırma ve kümeleme) veri işlemeye algoritmalarını içerir. Bu öğreticide, arkadaşlarınızın gördünüz filmler üzerinde temel bir öneri altyapısı toogenerate film önerileri kullanın.</p></td>
<td>Sorgu konsol</td>
<td>Hadoop</td>
<td>Yok</td>
</tr>
<tr>
<td>Hive yapılandırması için toodefault değerini değiştirin: hive.auto.convert.join.noconditionaltask.size</td>
<td><p>Bu boyut yapılandırmasından dönüştürülen tooautomatically harita birleştirmeler geçerlidir. Merhaba değeri belleğe sığmayacak dönüştürülmüş toohash eşlemeleri olabilir tabloları hello boyutlarını hello toplamını temsil eder. Önceki bir sürümde, bu değer 10 MB too128 MB'lık varsayılan değeri hello çıkarılmıştır. Ancak, hello yeni 128 MB değerini işleri toofail neden olan son toolack bellek. Bu sürüm hello varsayılan değer döner too10 MB yedekleyin. Müşteriler hala toooverride bu değer, sorgular ve tablo boyutları verilen küme oluşturma sırasında seçebilirsiniz. Bu ayar hakkında daha fazla bilgi ve nasıl toooverride, bkz: <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">otomatik katılma dönüştürme en iyi duruma</a> Hortonworks belgelerinde. </p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a>Hdınsight 23/12/2014 sürümünün notları
Bu sürüm ile dağıtılan Hdınsight kümeleri Hello tam sürüm numaraları şunlardır:

* Hdınsight 2.1.10.420.1246783 (HDP sürüm değişmeden)
* Hdınsight 3.0.6.420.1246783 (HDP sürüm değişmeden)
* Hdınsight 3.1.1.420.1246783 (HDP sürüm değişmeden)

Bu sürüm, güncelleştirmenin ardından hello içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Bileşen</th>
<th>Küme Türü</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Tooexcessive yük nedeniyle aralıklı küme oluşturma hataları</td>
<td><p>Küme oluşturma sırasında HDP Paketleri indirmeye için geliştirilmiş algoritması hataları tooexcessive yük nedeniyle daha sağlam işlenmesini sağlar.</p></td>
<td>Hizmet</td>
<td>Hadoop, Hbase, Storm</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a>Hdınsight 18/12/2014 sürümünün notları
Bu sürüm bileşeni güncelleştirmenin ardından hello içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Bileşen</th>
<th>Küme Türü</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td><a href = "hdinsight-hadoop-customize-cluster.md" target="_blank">Genel kullanılabilirlik kümesi özelleştirme</a></td>
<td><p>Özelleştirme hello özelliği sizin için hello Apache Hadoop ekosistemi kullanılabilir projeleri, Azure Hdınsight kümeleri toocustomize sağlar. Bu yeni özellik ile denemeler ve Hadoop projeleri tooAzure Hdınsight dağıtın. Bu hello etkinleştirilir **betik eylemi** özelliği Hadoop kümeleri özel komut dosyaları kullanarak rastgele şekilde değiştirebilirsiniz. Bu özelleştirme Hdınsight kümeleri Hadoop, HBase ve Storm dahil olmak üzere tüm türleri kullanılabilir. Bu özellik toodemonstrate hello gücünü, biz belgelenen hello işlem tooinstall hello popüler <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>, <a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>, <a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a>, ve <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a> modüller. Bu sürüm ayrıca hello Azure portal aracılığıyla kendi özel betik eylemi müşteriler toospecify için hello özelliğini ekler, kılavuzları ve en iyi uygulamaları nasıl toobuild özel komut yardımcı yöntemler kullanarak eylemleri hakkında ve nasıl hakkında yönergeler sağlar tootest Merhaba betik eylemi. </p></td>
<td>Özellik genel kullanılabilirlik</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a>Hdınsight 12/05/2014 sürümünün notları
Bu sürüm ile dağıtılan Hdınsight kümeleri Hello tam sürüm numaraları şunlardır:

* Hdınsight 2.1.9.406.1221105 (HDP 1.3.9.0-01351)
* Hdınsight 3.0.5.406.1221105 (HDP 2.0.9.0-2097)
* Hdınsight 3.1.1.406.1221105 (HDP 2.1.9.0-2196)
* Hdınsight SDK'sı yok

Bu sürüm hello şu bileşen güncelleştirmeleri içerir:

<table border="1">
<tr>
<th>Başlık</th>
<th>Açıklama</th>
<th>Bileşen</th>
<th>Küme Türü</th>
<th>JIRA (varsa)</th>
</tr>
<tr>
<td>Hata düzeltmesi: çok sayıda bölüm tooa tablo Hive DDL'de eklenirken aralıklı hata oluştu </td>
<td><p>Çok sayıda bölüm tooa Hive tablosu eklerken aralıklı bağlantısı hatayla hello Hive meta depo veritabanı ise hello Hive DDL başarısız olabilir. Bu sorun oluşursa deyimi isseen hello Hive hata günlüğünde aşağıdaki hello: </p><p>"Hata [ana]: ql. Sürücü (SessionState.java:printError(547)) - başarısız oldu: yürütme hatası, org.apache.hadoop.hive.ql.exec.DDLTask dönüş koddan 1. MetaException (message:java.lang.RuntimeException: commitTransaction openTransactionCalls çağrıldı = 0. Bu büyük olasılıkla dengesiz çağrıları tooopenTransaction/commitTransaction olduğunu gösterir)"</p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>HIVE 482 (dışarıdan quoted edilemez şekilde bir iç JIRA budur. Burada başvurusunu not almıştınız.)</td>
</tr>
<tr>
<td>Hata düzeltmesi: Merhaba Hdınsight sorgu konsol içinde zaman askıda kalabilir</td>
<td>Bu gerçekleştiğinde, hello aşağıdaki ifadeyi hello WebHCat Başlatıcısı işi için hello WebHCat günlüğünde görülebilir: <p>"org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException): geçmiş dosyası {wasb url toohello geçmiş dosyası} yüklenemedi "</p></td>
<td>WebHCat</td>
<td>Hadoop</td>
<td>HIVE 482 (dışarıdan quoted edilemez şekilde bir iç JIRA budur. Burada başvurusunu not almıştınız.)</td>
</tr>
<tr>
<td>Hata düzeltmesi: zaman ani artış Hbase sorguları gecikme süresi</td>
<td>Bu durumda, kullanıcılar, Hbase sorgularının hello gecikme 3 saniyelik zaman zaman bir depo fark edeceksiniz. </td>
<td>Hdınsight kümesi ağ geçidi</td>
<td>HBase</td>
<td>Yok</td>
</tr>
<tr>
<td>Dosya adı değişiklikleri HDP JAR</td>
<td>HDI için sürüm 3.0, burada birkaç HDP tarafından yüklenen değişiklikleri toohello iç JAR dosyalarını küme. jetty 6.1.26.jar jetty 6.1.26.hwx.jar ile değiştirilmiştir. jetty kul 6.1.26.jar kul jetty 6.1.26.hwx.jar ile değiştirilmiştir. Bu değişiklikleri tooHadoop, Mahout, WebHCat ve Oozie projeleri geçerlidir.</td>
<td>Hadoop, Mahout, WebHCat, Oozie</td>
<td>Hadoop, HBase</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a>Hdınsight 21/11/2014 sürümünün notları
Bu sürüm ile dağıtılan Hdınsight kümeleri Hello tam sürüm numaraları şunlardır:

* Hdınsight 2.1.9.382.1169709 (11/14/2014 hiçbir değişiklik)
* Hdınsight 3.0.5.382.1169709 (11/14/2014 hiçbir değişiklik)
* Hdınsight 3.1.1.382.1169709 (11/14/2014 hiçbir değişiklik)
* Hdınsight SDK 1.4.0

Bu sürüm hello şu bileşen güncelleştirmeleri içerir:

<table border="1">
<tr><th>Başlık</th><th>Açıklama</th><th>Bileşen</th><th>Küme Türü</th><th>JIRA (varsa)</th></tr>
<tr>
<td>Erişen uygulama günlükleri</td>
<td>Özelliği tooprogrammatically kümelerinizi üzerinde çalışan uygulamalar ve toodownload ilgili uygulamaya özgü veya kapsayıcı özgü günlükleri toohelp hata ayıklama sorunlu uygulamalar sıralar.</td>
<td>SDK</td>
<td>Hadoop</td>
<td>Yok</td>
</tr>
<tr>
<td>IHdInsightClient.DeleteCluster özelliği toospecify bölge adı </td>
<td>Hello Azure Hdınsight SDK kullanırken bu hello özelliği toospecify bölge adı sağlar **DeleteCluster**. Bu iki kaynak aynı ada sahip farklı bölgelerde karşılaştı ve yüklenemiyor toodelete olsaydı müşteriler engellemesini yardımcı olur. ikisinden biri.</td>
<td>SDK</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>ClusterDetails.DeploymentId</td>
<td>Merhaba **ClusterDetails** nesnesi döndürür bir **Deploymentıd** hello küme için benzersiz bir tanımlayıcı temsil eden alan. Küme oluşturma işlemi benzersiz toobe çalışır hello ile aynı garanti adları.</td>
<td>SDK</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a>Hdınsight 11/14/2014 sürümünün notları

Bu sürüm ile dağıtılan Hdınsight kümeleri Hello tam sürüm numaraları şunlardır:

* Hdınsight 2.1.9.382.1169709
* Hdınsight 3.0.5.382.1169709
* Hdınsight 3.1.1.382.1169709

Bu sürüm hello aşağıdaki yeni özellikleri, bileşen güncelleştirmeleri ve hata düzeltmelerini içerir.

<table border="1">
<tr><th>Başlık</th><th>Açıklama</th><th>Bileşen</th><th>Küme Türü</th><th>JIRA (varsa)</th></tr>
<tr>
<td>Betik eylemi (Önizleme)</td>
<td>Önizleme hello küme özelleştirme özelliğinin Hadoop değiştirilmesini sağlayan özel komut dosyalarını kullanarak rastgele yollarla kümeleri. Bu özellik ile kullanıcılar deneme ve hello Apache Hadoop ekosistemi tooAzure Hdınsight kümeleri kullanılabilir projeler dağıtma. Bu özelleştirme özellik Hdınsight kümeleri, Hadoop, HBase ve Storm dahil olmak üzere tüm türleri kullanılabilir.</td>
<td>Yeni özellik</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>Azure Web siteleri ve depolama günlük analizi için önceden oluşturulmuş işleri</td>
<td>Merhaba Hdınsight sorgu konsol verilerinizi veya örnek veriler üzerinde çalışmak çözümlerini destekler başlarken bir galeri sahiptir.
<p>**Verileriniz üzerinde çalışan çözümler**:<br>
Bazı hello en yaygın veri analizi senaryoları tooprovide kendi çözümleri oluşturmak için bir başlangıç noktası için işleri oluşturduk. Merhaba iş toosee nasıl çalıştığını, verilerinizi kullanabilirsiniz. Hazır olduğunuzda toocreate hello önceden oluşturulmuş işinden sonra modellenir bir çözüm öğrendiniz kullanın.</p>
<p>**Örnek veriler üzerinde çalışan çözümler**:<br>
Bilgi nasıl (web günlükleri ve algılayıcı verilerini analiz etme gibi) bazı temel senaryolar üzerinden taramasını tarafından toowork Hdınsight ile. Hakkında bilgi edineceksiniz nasıl toouse Hdınsight tooanalyze bu tür veri ve diğer uygulamalar ve hizmetler toothis verileri nasıl bağlanabilir. TooMicrosoft Excel bağlanarak veri görselleştirme bu yaklaşım hello gücünü gösteren bir örnek sağlar.</p></td>
<td>Sorgu konsol</td>
<td>Hadoop</td>
<td>Yok</td>
</tr>
<tr>
<td>Templeton bellek sızıntısı düzeltme</td>
<td>İkinci bir ele kümeleri uzun süre çalışan vardı veya işin 100s gönderme müşteriler etkilenen Templeton bir bellek sızıntısı ister. Merhaba Templeton 5xx hataları ve hello geçici çözüm bildirilen sorunu toorestart hello hizmet oluştu. Merhaba geçici çözüm artık gerekli değildir.</td>
<td>Templeton</td>
<td>Tümü</td>
<td>https://issues.apache.org/jira/Browse/HADOOP-11248</td>
</tr>
</table>

> [!NOTE]
> Betik eylemi tooinstall Spark ve R modülleri bir kümede kullanılarak hello yordamları küme özelleştirme tarafından kullanılabilir hale toodemonstrate hello yeni özellikler belgelenmiştir. Daha fazla bilgi için bkz.

* [Yükleme ve Hdınsight kümelerinde Spark 1.0 kullanma](hdinsight-hadoop-spark-install.md)
* [Yükleme ve Hdınsight Hadoop kümeleri üzerinde R kullanma](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a>Hdınsight 07/11/2014 sürümünün notları

Bu sürüm ile dağıtılan Hdınsight kümeleri Hello tam sürüm numaraları şunlardır:

* Hdınsight 2.1 2.1.9.374.1153876
* Hdınsight 3.0 3.0.5.374.1153876
* Hdınsight 3.1 3.1.1.374.1153876

Bu sürüm hello şu bileşen güncelleştirmeleri içerir:

<table border="1">
<tr><th>Başlık</th><th>Açıklama</th><th>Bileşen</th><th>Küme Türü</th><th>JIRA (varsa)</th></tr>
<tr>
<td>HDP 2.1.7</td>
<td>Bu sürüm Hortonworks veri Platformu (HDP) 2.1.7 temel alır. Daha fazla bilgi için bkz: <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html" target="_blank">HDP 2.1.7 için sürüm notları</a>.</td>
<td>HDP</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
<tr>
<td>YARN zaman çizelgesi sunucu</td>
<td>Varsayılan olarak etkin Hello YARN zaman çizelgesi sunucu (olarak da bilinen genel uygulama geçmişi sunucusu hello). Merhaba zaman çizelgesi sunucu tamamlanan uygulamalar (örneğin, uygulama kimliği, uygulama adı, uygulama durumu, uygulama gönderme zamanı ve uygulama tamamlama süresi) hakkında genel bilgi sağlar.

Bu uygulama bilgilerini hello baş düğümünden hello URI http://headnodehost:8188 erişme veya çalışan hello YARN komutu tarafından alınabilir: yarn uygulama-- appStates listesinde tüm.

Bu bilgiler ayrıca uzaktan bir REST API olsa https://{ClusterDnsName adresindeki alınabilir}. azurehdinsight.NET/ws/v1/applicationhistory/.

Daha ayrıntılı bilgi için bkz: <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN zaman çizelgesi sunucu</a>.</td>
<td>Hizmet, YARN</td>
<td>Hadoop, HBase</td>
<td>Yok</td>
</tr>
<tr>
<td>Küme dağıtım kimliği</td>
<td>SDK sürüm 1.3.3.1.5426.29232 ile başlayarak, Hdınsight verilen her küme için benzersiz bir kimliği kullanıcılar erişebilir. Bu etkinleştirir müşteriler toofigure çıkışı bir DNS adı arasında yeniden kullanılıyor olduğunda kümeleri benzersiz örneklerini oluşturmak veya senaryoları bırakılamıyor.</td>
<td>SDK</td>
<td>Tümü</td>
<td>Yok</td>
</tr>
</table>

> [!NOTE]
> Bu sürümde hello tam sürüm numarası hello portalında yukarı gösteren ya da Windows PowerShell veya hello SDK tarafından döndürülen engelledi hello hatanın düzeltildiğini.

## <a name="notes-for-10152014-release"></a>15/10/2014 sürüm notları

Bu düzeltme sürüm hello ağır Templeton kullanıcılarının etkilenen Templeton içinde bellek sızıntısı sabit. Bazı durumlarda, hello istekleri, yeterli bellek toorun sahip değil çünkü 500 hata kodları bildirilen hataları Templeton yoğun kullandı kullanıcılar görür. Bu sorun için geçici çözüm Hello toorestart hello Templeton hizmet oluştu. Bu sorun düzeltilmiştir.

## <a name="notes-for-1072014-release"></a>10/7/2014 sürüm notları

* Ambari kullanırken uç noktası, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}" Merhaba *host_name* alan döndürür Merhaba tam etki alanı adı (FQDN) yalnızca hello ana bilgisayar adı yerine hello düğümünün. Örneğin, döndürme yerine "**headnode0**", hello FQDN Al"**headnode0. { ClusterDNS} .azurehdinsight .net**". Bu değişikliği bir sanal ağda birden çok küme türleri (örneğin, HBase ve Hadoop) dağıtıldığı gerekli toofacilitate senaryoları oluştu. Bu, örneğin, Hadoop için bir arka uç platform olarak HBase kullanarak olur.

* Merhaba Hdınsight küme hello varsayılan dağıtımı için yeni bellek ayarları sağladık. Önceki varsayılan bellek ayarlarını yeterli CPU çekirdeği dağıtılan hello sayısı için hello kılavuzu için dikkate almamıştır. Bu yeni bellek ayarları (Hortonworks öneriler) uygun şekilde daha iyi Varsayılanları sağlamalıdır. toochange bunlar, küme yapılandırmasını değiştirme hakkında toohello SDK başvuru belgelerine bakın. Aşağıdaki tablonun hello hello varsayılan 4 CPU Çekirdeği (8 kapsayıcısı) Hdınsight küme tarafından kullanılan hello yeni bellek ayarları listelenmektedir. (Merhaba kullanılan değerler önceki toothis sürüm ayrıca sağlanan parenthetically.)

<table border="1">
<tr><th>Bileşen</th><th>Bellek ayırma</th></tr>
<tr><td> yarn.Scheduler.minimum ayırma</td><td>768 MB (daha önce 512 MB)</td></tr>
<tr><td> yarn.Scheduler.Maximum ayırma</td><td>6144 (değiştirmeden) MB</td></tr>
<tr><td>yarn.nodemanager.Resource.Memory</td><td>6144 (değiştirmeden) MB</td></tr>
<tr><td>Mapreduce.Map.Memory</td><td>768 MB (daha önce 512 MB)</td></tr>
<tr><td>mapreduce.Map.Java.opts</td><td>= Xmx512m (daha önce - Xmx410m) kabul eder</td></tr>
<tr><td>Mapreduce.reduce.Memory</td><td>1536 MB (daha önce 1024 MB)</td></tr>
<tr><td>mapreduce.reduce.Java.opts</td><td>= Xmx1024m (daha önce - Xmx819m) kabul eder</td></tr>
<tr><td>yarn.app.mapreduce.AM.Resource</td><td>768 MB (daha önce 1024 MB)</td></tr>
<tr><td>yarn.app.mapreduce.AM.Command</td><td>= Xmx512m (daha önce - Xmx819m) kabul eder</td></tr>
<tr><td>mapreduce.Task.io.sort</td><td>256 MB (daha önce 200 MB)</td></tr>
<tr><td>Tez.AM.Resource.Memory</td><td>1536 MB (değiştirmeden)</td></tr>
</table>

Merhaba Hdınsight tarafından kullanılan Hortonworks veri platformu üzerinde MapReduce ve YARN ile kullanılan hello bellek yapılandırma ayarları hakkında daha fazla bilgi için bkz: [HDP bellek yapılandırma ayarlarını belirlemek](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html). Hortonworks bir aracı toocalculate uygun bellek ayarlarını de sağlanır.

Hello Azure PowerShell ve hello Hdınsight SDK hata iletisi ile ilgili: "*küme HTTP Hizmetleri erişim için yapılandırılmamış*":

* Bu bilinen bir hatadır [uyumluluk sorunu](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight) hello hello Hdınsight SDK'sı, Azure PowerShell ve hello sürümünü veya hello küme tooa fark nedeniyle oluşabilir. 8/15 veya daha sonra oluşturulan kümeleri sanal ağlara yeni sağlama özelliği için destek vardır. Ancak bu özellik hello Hdınsight SDK veya Azure PowerShell eski sürümleri tarafından doğru Yorumlanmamış. Merhaba, bazı iş gönderme işlemleri içinde bir hata oluşur. Hdınsight SDK API'leri veya Azure PowerShell cmdlet'leri kullanıyorsanız (**kullanım AzureRmHDInsightCluster** veya **Invoke-AzureRmHDInsightHiveJob**) toosubmit işleri, o işlemler başarısız olabilir hello hata iletisiyle " *Küme <clustername> HTTP Hizmetleri erişim için yapılandırılmamış*. " Veya (Merhaba işlemine bağlı olarak), diğer hata iletileri gibi alabilirsiniz "*toocluster bağlanamıyor*".
* Bu uyumluluk sorunları hello ve en son sürümlerini hello Hdınsight SDK'sı Azure PowerShell içinde çözümlenir. Güncelleştirme öneririz Hdınsight SDK tooversion 1.3.1.6 veya üstü ve Azure PowerShell araçları tooversion 0.8.8 hello veya sonraki bir sürümü. Erişim toohello alabilirsiniz son Hdınsight SDK [NugGet](http://nuget.codeplex.com/wikipage?title=Getting%20Started) ve Azure PowerShell araçları hello [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

## <a name="notes-for-9122014-release-of-hdinsight-31"></a>Hdınsight 3.1 12/9/2014 sürümünün notları
* Bu sürüm Hortonworks veri Platformu (HDP) 2.1.5 temel alır. Merhaba bu sürümde hello düzeltilen listesi için bkz: [bu sürümde sabit](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) hello Hortonworks site sayfasında.
* Merhaba Pig kitaplıkları klasöründe hello "avro mapred 1.7.4.jar" dosyası değiştirildi çok "avro-mapred-1.7.4-hadoop2.jar." Bu dosyanın içeriğini Hello bölünemez küçük bir hata düzeltme içerir. Müşteriler hello hello adını doğrudan bağımlı dosyaları yeniden adlandırıldığında dosya tooavoid sonları JAR yapmayın önerilir.

## <a name="notes-for-8212014-release"></a>21/8/2014 sürüm notları
* İş too1 GB hello varsayılan bellek sınırının Templeton denetleyicisi için ayarlar WebHCat yapılandırması (HIVE-7155) aşağıdaki hello ekliyoruz. (Merhaba önceki varsayılan değer 512 MB idi.)

     templeton.mapper.memory.mb (1024 =)

  * Bu değişiklik aşağıdaki hata toolower bellek sınırlamaları nedeniyle bazı Hive sorguları hello giderir: "Kapsayıcı fiziksel bellek sınırlarının dışına çalışıyor."
  * toorevert toohello eski Varsayılanları, komutu aşağıdaki hello kullanarak küme oluşturma sırasında bu yapılandırma değeri too512 Azure PowerShell aracılığıyla ayarlayabilirsiniz:

      Ekleme AzureRmHDInsightConfigValues-çekirdek @{"templeton.mapper.memory.mb"="512";}
* Merhaba zookeeper rolünün Hello ana bilgisayar adı çok değiştirildi*zookeeper*. Bu ad çözümlemesi hello kümedeki etkiler, ancak dış REST API'leri etkilemez. Bu kullanım hello bileşenleri varsa *zookeepernode* ana bilgisayar adı, tooupdate ihtiyacınız bunları toouse yeni adı. Merhaba üç zookeeper düğümleri için Hello yeni adları şunlardır:

  * zookeeper0
  * zookeeper1
  * zookeeper2
* HBase sürüm destek matrisi güncelleştirilir. Yalnızca Hdınsight sürüm 3.1 (HBase sürüm 0,98) üretim HBase iş yükleri için desteklenir. (Önizleme için kullanılabilir) sürüm 3.0 taşıma İleri desteklenmiyor.

## <a name="notes-about-clusters-created-prior-too8152014"></a>Önceki too8/15/2014 kümeleri ile ilgili notlar oluşturuldu
Bir Azure PowerShell veya Hdınsight SDK hata iletisi "Küme <clustername> HTTP Hizmetleri erişim için yapılandırılmamış" (veya hello işlemine bağlı olarak diğer hata iletileri gibi: "toocluster bağlanılamıyor") tooa sürüm fark karşılaştı Azure PowerShell veya Hdınsight SDK hello ve bir küme arasında. 8/15 veya daha sonra oluşturulan kümeleri sanal ağlara yeni sağlama özelliği için destek vardır. Bu özellik, hello Azure PowerShell veya hello iş gönderme işlemlerinin hatalarına Hdınsight SDK eski sürümleri tarafından doğru yorumlanması değil. Hdınsight SDK API'leri veya Azure PowerShell cmdlet'leri (örneğin, kullanım AzureRmHDInsightCluster veya Invoke-AzureRmHDInsightHiveJob) toosubmit işleri kullanıyorsanız, bu işlemler açıklanan hello hata iletilerinden birini ile başarısız olabilir.

Bu uyumluluk sorunları hello ve en son sürümlerini hello Hdınsight SDK'sı Azure PowerShell içinde çözümlenir. Güncelleştirme öneririz Hdınsight SDK tooversion 1.3.1.6 veya üstü ve Azure PowerShell araçları tooversion 0.8.8 hello veya sonraki bir sürümü. Erişim toohello alabilirsiniz son Hdınsight SDK [NuGet][nuget-link]. Hello Azure PowerShell araçları kullanarak erişebilirsiniz [Microsoft Web Platformu yükleyicisi][webpi-link].

## <a name="notes-for-7282014-release"></a>28/7/2014 sürüm notları
* **Yeni bölgelerdeki Hdınsight**: biz Hdınsight coğrafi varlığı toothree bölgeler genişletilmiştir. Hdınsight müşteriler, bu bölgelerde kümeleri oluşturabilirsiniz:
  * Doğu Asya
  * Orta Kuzey ABD
  * Orta Güney ABD
* Hdınsight sürüm 1.6 (HDP 1.1 ve Hadoop 1.0.3) ve Hdınsight sürüm 2.1 (HDP1.3 ve Hadoop 1.2) hello Azure portal ' kaldırılıyor. Azure PowerShell cmdlet'ini kullanarak bu sürümleri hello için toocreate Hadoop kümeleri devam edebilirsiniz [yeni AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx) veya hello kullanarak [Hdınsight SDK](http://msdn.microsoft.com/library/azure/dn469975.aspx). Daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md).
* Bu sürümde Hortonworks veri Platformu (HDP) değişiklikleri:

<table border="1">
<tr><th>HDP</th><th>Değişiklikleri</th></tr>
<tr><td>1.3 HDP / HDI 2.1</td><td>Değişiklik yok</td></tr>
<tr><td>2.0 HDP / HDI 3.0</td><td>Değişiklik yok</td></tr>
<tr><td>2.1 HDP / HDI 3.1</td><td>zookeeper: ['3.4.5.2.1.3.0-1948'] ['3.4.5.2.1.3.2-0002'] -></td></tr>
</table>

## <a name="notes-for-6242014-release"></a>24/6/2014 sürüm notları
Bu sürümdeki yenilikleri toohello Hdınsight hizmeti içerir:

* **HDP 2.1 kullanılabilirlik**: (HDP 2.1 içeren) Hdınsight 3.1 genel olarak kullanılabilir ve yeni küme için hello varsayılan sürümdür.
* **HBase - Azure portal geliştirmeleri**: HBase kümeleri önizlemede kullanılabilen yapıyoruz. Yalnızca birkaç tıklama ile Merhaba portalından HBase kümeleri oluşturabilirsiniz.

HBase ile milyonlarca uç noktadan gelen algılayıcı ve telemetri verilerini depolayan büyük veri kümeleri tooservices çalışmak etkileşimli Web sitelerinde Hdınsight üzerinde gerçek zamanlı iş yüklerinin oluşturabilirsiniz. Merhaba sonraki adıma tooanalyze hello verileri Hadoop işleriyle bu iş yükleri olabilir ve bu Azure PowerShell ve hello Hive küme Panosu aracılığıyla hdınsight'ta mümkündür.

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a>Apache Mahout Hdınsight 3.1 önceden yüklenmiş
 [Mahout](http://hortonworks.com/hadoop/mahout/) Mahout işleri ek kümesi yapılandırması için hello gerek kalmadan çalıştırabilmeniz için Hdınsight 3.1 Hadoop kümeleri üzerinde önceden yüklenir. Örneğin, uzak bir Hadoop kümesine Uzak Masaüstü Protokolü (RDP) kullanarak yapabilecekleriniz ve ek adımlar olmadan, Hello World Mahout komutu aşağıdaki hello çalıştırabilirsiniz:

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

Bu yordamı daha eksiksiz bir açıklaması için hello hello belgelerine bakın [Breiman örnek](https://mahout.apache.org/users/classification/breiman-example.html) hello Apache Mahout Web sitesinde.

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a>Hdınsight 3.1 Tez Hive sorgularını kullanabilirsiniz
Hive 0,13 Hdınsight 3.1 kullanılabilir ve önemli performans geliştirmeleri yararlanılabilir Tez kullanarak sorguları çalıştırabilen olur.
Tez Hive sorguları için varsayılan olarak etkin değildir. toouse içinde etmeniz gerekir. Tez kod parçacığını aşağıdaki hello çalıştırarak etkinleştirebilirsiniz:

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

Hortonworks ile Tez Hive sorgusu performans geliştirmeleri ayrıntılı bir dökümünü içinde standart kıyaslamaları teslim olarak yayımlanır. Ayrıntılar için bkz [Apache Hive 13 değerlendirmesi'Kurumsal Hadoop için](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/).

Daha fazla bilgi için bkz: [üzerinde Tez Hive](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez).

### <a name="global-availability"></a>Genel kullanılabilirlik
Hdınsight'ta Hadoop 2.2 Hello sürümüyle Microsoft Hdınsight kullanılabilir Azure kullanılabilir olduğu tüm ana coğrafi bölgelerde yapmıştır. Özellikle, hello Batı Avrupa ve Güneydoğu Asya veri merkezleri çevrimiçi bir araya getirilmiştir. Bu, müşterilerin toolocate kümeleri yakın olan bir veri merkezinde ve büyük olasılıkla bir bölgede benzer uyumluluk gereksinimlerini sağlar.

### <a name="dos--donts-between-cluster-versions"></a>DOS & Küme sürümleri arasında yapılmaması gerekenler
**Oozie meta deponuz Hdınsight 3.1 kümesi ile kullanılan Hdınsight 2.1 kümeleri ile geriye dönük olarak uyumlu değildir ve bu önceki sürümüyle kullanılamaz**.

Bir Hdınsight 3.1 kümesi ile dağıtılmış bir özel Oozie meta depo veritabanı bir Hdınsight 2.1 kümeyle yeniden kullanılamaz. Bir Hdınsight 2.1 kümeyle Hello meta depo kaynaklanan olsa bile bu hello durumdur. Merhaba meta depo şeması artık hello Hdınsight 2.1 kümeleri tarafından gerekli hello meta depo ile uyumlu olacak şekilde bir Hdınsight 3.1 kümesi ile kullanıldığında yükseltilmiş çünkü bu senaryo desteklenmiyor. Herhangi bir Hdınsight 3.1 kümesi ile kullanılan bir Oozie meta depo girişimi tooreuse işlemek hello Hdınsight 2.1 küme yaramaz.

**Oozie meta deponuz kümeler arasında paylaşılamaz.**

Oozie meta deponuz ekli toospecific kümesi olan ve kümeler arasında paylaşılamaz.

### <a name="breaking-changes"></a>Yeni değişiklikler
**Sözdizimi önek**: yalnızca hello "wasb: / /" söz dizimi Hdınsight 3.1 ve 3.0 kümeleri desteklenir. eski Hello "asv: / /" söz dizimi Hdınsight 2.1 ve 1.6 kümeleri desteklenir, ancak Hdınsight 3.1 veya 3.0 kümeleri desteklenmez. Herhangi bir işi tooan Hdınsight 3.1 ya da, açıkça küme 3.0 kullanan hello gönderilen yani "asv: / /" sözdizimi başarısız olur. Merhaba "wasb: / /" söz dizimi yerine kullanılmalıdır. Ayrıca, işleri gönderilen tooany Hdınsight 3.1 veya içeren mevcut bir meta depo ile açık oluşturulan 3.0 kümeleri başvuran hello kullanarak tooresources "asv: / /" sözdizimi başarısız olur. Bu meta deponuz toobe hello kullanarak yeniden oluşturulması gerekir "wasb: / /" sözdizimi tooaddress kaynakları.

**Bağlantı noktaları**: Merhaba Hdınsight hizmeti tarafından kullanılan hello bağlantı değişti. kullanılmakta bağlantı noktası numaralarını hello hello kısa ömürlü bağlantı noktası aralığı hello Windows işletim sistemi içinde yoktu. Bağlantı noktaları kısa süreli Internet Protokol tabanlı iletişimleri için önceden tanımlanmış kısa ömürlü bir aralıktan otomatik olarak ayrılır. Merhaba yeni izin verilen Hortonworks veri Platformu (HDP) hizmet bağlantı noktası numaralarını kümesidir hello baş düğüm üzerinde çalışan hizmetleri tarafından kullanılan hello bağlantı noktaları ile meydana gelebilecek çakışmaları karşılaşmadan bu aralık tooavoid dışında. Merhaba yeni bağlantı noktası numaralarını en son değişiklikleri neden olmamalıdır. kullanılan hello numaraları aşağıdaki gibidir:

 **Hdınsight 1.6 (HDP 1.1)**

<table border="1">
<tr><th>Ad</th><th>Değer</th></tr>
<tr><td>DFS.http.address</td><td>namenodehost:30070</td></tr>
<tr><td>DFS.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>DFS.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>DFS.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>DFS.Secondary.http.address</td><td>0.0.0.0:30090</td></tr>
<tr><td>mapred.job.Tracker.http.address</td><td>jobtrackerhost:30030</td></tr>
<tr><td>mapred.Task.Tracker.http.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>mapreduce.History.Server.http.address</td><td>0.0.0.0:31111</td></tr>
<tr><td>templeton.Port</td><td>30111</td></tr>
</table>

 **Hdınsight 3.1 ve 3.0 (HDP 2.1 ve 2. 0)**

<table border="1">
<tr><th>Ad</th><th>Değer</th></tr>
<tr><td>DFS.namenode.HTTP adresi</td><td>namenodehost:30070</td></tr>
<tr><td>DFS.namenode.HTTPS adresi</td><td>headnodehost:30470</td></tr>
<tr><td>DFS.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>DFS.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>DFS.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>DFS.namenode.Secondary.HTTP adresi</td><td>0.0.0.0:30090</td></tr>
<tr><td>yarn.nodemanager.WebApp.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>templeton.Port</td><td>30111</td></tr>
</table>

### <a name="dependencies"></a>Bağımlılıklar
Merhaba aşağıdaki bağımlılıkları Hdınsight'ta eklenen 3.x (HDP2.x):

* guice servlet
* optiq çekirdek
* javax.inject
* Etkinleştirme
* jsr305
* geronimo-jaspic_1.0_spec
* Tem slf4j
* Java xmlbuilder
* ant
* Commons derleyici
* jdo API
* Commons math3
* paranamer
* jaxb impl
* stringtemplate
* eigenbase xom
* bölgesi servlet
* Commons Yönet
* jaxb API
* jetty tüm sunucu
* janino
* xercesImpl
* optiq avatica
* jta
* eigenbase özellikleri
* Tüm Modaya uygun
* hamcrest çekirdek
* Posta
* linq4j
* jpam
* İstemci bölgesi
* aopalliance
* geronimo-annotation_1.0_spec
* ant Başlatıcısı
* bölgesi guice
* XML API'leri
* stax API
* asm commons
* asm-ağacı
* wadl
* geronimo-jta_1.1_spec
* guice
* leveldbjni tüm
* hız
* jettison
* java snappy
* jetty tüm
* Commons dbcp

Merhaba aşağıdaki bağımlılıkları artık Hdınsight'ta mevcut 3.x (HDP2.x):

* jdeb
* kfs
* sqlline
* Sarmaşık
* aspectjrt
* JSON
* çekirdek
* jdo2 API
* avro mapred
* datanucleus Geliştirici
* jsp
* Commons günlük kaydı API
* Commons matematik
* JavaEWAH
* aspectjtools
* javolution
* hdfsproxy
* hbase
* snappy

### <a name="version-changes"></a>Sürüm değişiklikleri
Aşağıdaki sürüm değişiklikler hello arasında Hdınsight yapıldı 2.x (HDP1.x) ve Hdınsight 3.x (HDP2.x):

* Ölçümleri çekirdekli: ['2.1.2'] ['3.0.0'] ->
* derbynet: ['10.4.2.0'] ['10.10.1.1'] ->
* datanucleus: ['rdbms-3.0.8'] -> ['rdbms-3.2.9']
* jasper derleyici: ['5.5.12'] ['5.5.23'] ->
* log4j: ['1.2.15', '1.2.16'] -> ['1.2.16', '1.2.17']
* derbyclient: ['10.4.2.0'] ['10.10.1.1'] ->
* httpcore: ['4.2.4'] ['4.2.5'] ->
* hsqldb: ['1.8.0.10'] ['2.0.0'] ->
* jets3t: ['0.6.1'] ['0.9.0'dan'] ->
* protobuf java: ['2.4.1'] ['2.5.0'] ->
* Derby: ['10.4.2.0'] ['10.10.1.1'] ->
* jasper: [' çalışma zamanı-5.5.12'] -> [' çalışma zamanı-5.5.23']
* Commons arka plan programı: ['1.0.1'] ['1.0.13'] ->
* datanucleus çekirdekli: ['3.0.9'] ['3.2.10'] ->
* datanucleus API jdo: ['3.0.7'] ['3.2.6'] ->
* zookeeper: ['3.4.5.1.3.9.0-01320'] ['3.4.5.2.1.3.0-1948'] ->
* bonecp: ['0.7.1.RELEASE'] -> ['
* 0.8.0.RELEASE']

### <a name="drivers"></a>Sürücüler
SQL Server için Hello Java veritabanı bağlantısı (JDBC) sürücüsü Hdınsight tarafından dahili olarak kullanılır ve dış işlemleri için kullanılmaz. Açık veritabanı bağlantısı (ODBC) kullanarak tooconnect tooHDInsight istiyorsanız, lütfen hello Microsoft Hive ODBC sürücüsü kullanın. Daha fazla bilgi için bkz: [hello Microsoft Hive ODBC sürücüsü ile bağlanma Excel tooHDInsight](hdinsight-connect-excel-hive-odbc-driver.md).

### <a name="bug-fixes"></a>Hata düzeltmeleri
Bu sürümle birlikte, biz çeşitli hata düzeltmeleri ile Hdınsight sürümleri aşağıdaki hello yenileyene:

* Hdınsight 2.1 (HDP 1.3)
* Hdınsight 3.0 (HDP 2.0)
* Hdınsight 3.1 (HDP 2.1)

## <a name="hortonworks-release-notes"></a>Hortonworks sürüm notları
Merhaba Hdınsight sürüm kümeleri tarafından kullanılan Hortonworks veri platformları (HDPs) için sürüm notları aşağıdaki konumlardan hello kullanılabilir:

* Hdınsight sürüm 3.1 kullanan üzerinde hello dayalı bir Hadoop dağıtım [Hortonworks veri platformu 2.1.7][hdp-2-1-7]. 7/11/2014 sonra hello Azure portal kullanarak oluşturulan hello varsayılan Hadoop kümesi budur. 11/7/2014 temel önce hello üzerinde oluşturulan Hdınsight 3.1 kümeleri [Hortonworks veri platformu 2.1.1][hdp-2-1-1]
* Hdınsight sürüm 3.0 üzerinde hello dayalı bir Hadoop dağıtımı kullanır [Hortonworks veri platformu 2.0][hdp-2-0-8].
* Hdınsight sürüm 2.1 üzerinde hello dayalı bir Hadoop dağıtımı kullanır [Hortonworks veri platformu 1.3][hdp-1-3-0].
* Hdınsight sürüm 1.6 üzerinde hello dayalı bir Hadoop dağıtımı kullanır [Hortonworks veri platformu 1.1][hdp-1-1-0].

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/

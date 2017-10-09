---
title: "Web sitesi günlüğü analizi - Azure Hdınsight için Hadoop ile Hive aaaUse | Microsoft Docs"
description: "Toouse Hive Hdınsight tooanalyze Web sitesiyle nasıl günlüğe yazacağını öğrenin. Bir Hdınsight tabloya giriş olarak bir günlük dosyasını kullanın ve HiveQL tooquery hello verileri kullanmak."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a>Web siteleri tooanalyze günlüklerinden Windows tabanlı Hdınsight ile Hive kullanma
Bir Web sitesinden toouse HiveQL Hdınsight tooanalyze ile nasıl oturum öğrenin. Web sitesi günlüğü analizi kullanılan toosegment kitlenizi benzer etkinliklere dayalı olması, site ziyaretçilerini demografisine ve toofind görüntüledikleri hello içerik, geliyor hello Web siteleri ve benzeri tarafından kategorilere ayırma.

> [!IMPORTANT]
> Merhaba Windows tabanlı Hdınsight kümeleri ile bu belgeyi yalnızca çalışma adımları. Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Bu örnekte, bir günde bir Hdınsight kümesi tooanalyze Web sitesi günlük dosyaları tooget fikirler dış Web sitelerini ziyaret toohello sitesinden hello sıklığını kullanır. Ayrıca hello kullanıcı deneyimi Web sitesi hatalarının özetini oluşturacaksınız. Şunları öğreneceksiniz nasıl yapılır:

* Tooa Web sitesinin günlük dosyalarını içeren Azure Blob depolama alanına bağlayın.
* Oluşturma HIVE tabloları tooquery Bu günlükleri.
* HIVE sorguları tooanalyze hello veri oluşturun.
* Microsoft Excel tooconnect tooHDInsight kullanın (açık veritabanı bağlantısı (ODBC) tooretrieve analiz hello verileri kullanarak.

![HDI. Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a>Ön koşullar
* Azure Hdınsight Hadoop kümesinde sağlanması gerekir. Yönergeler için bkz: [sağlama Hdınsight kümeleri][hdinsight-provision].
* Excel 2010 yüklü veya Microsoft Excel 2013 yüklü olmalıdır.
* Bilmeniz gereken [Microsoft Hive ODBC sürücüsü](http://www.microsoft.com/download/details.aspx?id=40886) Hive Excel'e tooimport verileri.

## <a name="toorun-hello-sample"></a>toorun hello örnek
1. Merhaba gelen [Azure Portal](https://portal.azure.com/), Hello ifadesini (Merhaba küme sabitlenmiş varsa) sabitlemek istediğiniz toorun hello örnek hello küme kutucuğa tıklayın.
2. Hello dikey penceresinde altında küme **hızlı bağlantılar**, tıklatın **küme Panosu**ve sonra hello **küme Panosu** dikey penceresinde'ı tıklatın **Hdınsight kümesi Pano**. Alternatif olarak, URL aşağıdaki hello kullanarak hello Pano doğrudan açabilirsiniz:

         https://<clustername>.azurehdinsight.net

    İstendiğinde, hello yönetici kullanıcı adını ve hello küme hazırlama sırasında kullanılan parola kullanarak kimlik doğrulaması.
3. Hello web açan sayfasından hello tıklatın **alma başlatıldı galeri** sekmesinde hello altında ve **örnek verilerle çözümleri** kategorisi, hello tıklatın **Web sitesi günlüğü analizi** örnek.
4. Merhaba web sayfası toofinish hello örnek üzerinde sağlanan hello yönergeleri izleyin.

## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki örnek hello deneyin: [Hdınsight ile Hive kullanma algılayıcı verilerini çözümleme](hdinsight-hive-analyze-sensor-data.md).

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png

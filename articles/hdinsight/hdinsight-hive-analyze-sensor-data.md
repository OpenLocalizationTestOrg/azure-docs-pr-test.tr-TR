---
title: "Hive ve Hadoop - Azure Hdınsight kullanarak aaaAnalyze algılayıcı verilerini | Microsoft Docs"
description: "Hive sorgusu Konsolu Hdınsight (Hadoop) ile kullanarak tooanalyze algılayıcı verilerini nasıl hello öğrenin ve ardından PowerView ile Microsoft Excel'i hello verileri görselleştirmek."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a>Hdınsight'ta Hadoop Hive sorgusu konsol Hello kullanarak algılayıcı verilerini çözümleme

Tooanalyze algılayıcı verilerini kullanarak Hive sorgusu Konsolu Hdınsight (Hadoop) ile nasıl hello öğrenin ve ardından hello Microsoft Excel'de Power View kullanarak görselleştirmek.

> [!IMPORTANT]
> Merhaba Windows tabanlı Hdınsight kümeleri ile bu belgeyi yalnızca çalışma adımları. Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).


Bu örnekte, Hive tooprocess geçmiş verileri kullanın ve sorunları ısıtma sistemleriyle tanımlayın. Özellikle, sistemleri belirlemek olan erişilemiyor tooreliably korumak ayarlı sıcaklığı hello aşağıdaki görevleri gerçekleştirerek:

* Oluşturma HIVE tabloları tooquery verileri virgülle ayrılmış değer (CSV) dosyalarında depolanır.
* HIVE sorguları tooanalyze hello veri oluşturun.
* tooretrieve analiz hello veriler, Microsoft Excel tooconnect tooHDInsight kullanın.
* toovisualize hello verileri, Power View kullanın.

![Merhaba çözüm mimarisi diyagramı](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a>Ön koşullar

* Hdınsight (Hadoop) kümesi: bkz [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md) bir küme oluşturma hakkında daha fazla bilgi için.
* Microsoft Excel 2013

  > [!NOTE]
  > Microsoft Excel ile verileri görselleştirme için kullanıldığından [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).

* [Microsoft Hive ODBC sürücüsü](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a>toorun hello örnek

1. Web tarayıcınızdan URL aşağıdaki toohello gidin: 

         https://<clustername>.azurehdinsight.net

    Değiştir `<clustername>` Hdınsight kümenize hello adı.

    İstendiğinde, hello yönetici kullanıcı adını ve bu küme hazırlama sırasında kullanılan parola kullanarak kimlik doğrulaması.

2. Hello web açan sayfasından hello tıklatın **alma başlatıldı galeri** sekmesinde hello altında ve **çözümleri örnek verilerle** kategorisi, hello tıklatın **algılayıcı verilerini çözümleme** örnek.

    ![Başlatılan galeri görüntüsü alma](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. Merhaba web sayfası toofinish hello örnek üzerinde sağlanan hello yönergeleri izleyin.

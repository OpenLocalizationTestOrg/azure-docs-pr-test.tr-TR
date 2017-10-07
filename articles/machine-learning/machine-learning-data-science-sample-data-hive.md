---
title: "Azure Hdınsight Hive tablolardaki aaaSample verileri | Microsoft Docs"
description: "Azure Hdınsight (Hadopop) Hive tablolarındaki verileri örnekleme aşağı"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a>Azure HDInsight Hive tablolarındaki örnek veriler
Bu makalede, Azure Hdınsight Hive tabloları Hive sorgularını kullanarak depolanan nasıl toodown örnek veriler açıklanmaktadır. Şu üç özellik kullanılan örnekleme yöntemleri kapsar:

* Tekdüzen rastgele örnekleme
* Gruplara göre rastgele örnekleme
* Stratified örnekleme

Merhaba aşağıdaki **menü** açıklayan tootopics bağlantıları nasıl çeşitli depolama ortamları toosample verileri.

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Neden verilerinizi örnek?**
Tooanalyze planladığınız hello veri kümesi, bu genellikle iyi bir fikir toodown örnek hello veri tooreduce büyükse, tooa daha küçük, ancak temsili ve daha kolay yönetilebilir boyutu. Bu, veri anlama, keşfi ve özellik Mühendisliği kolaylaştırır. Kendi hello takım veri bilimi işlemi içinde tooenable hızlı prototipi oluşturulurken hello veri işleme işlevleri ve makine öğrenimi modellerinin oluşturulmasına rolüdür.

Merhaba adımda bu örnekleme görevdir [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="how-toosubmit-hive-queries"></a>Nasıl toosubmit Hive sorguları
Hive sorguları hello Hadoop kümesi baş düğümünde hello hello Hadoop komut satırı konsolundan gönderilebilir. Bu, hello Hadoop küme baş düğümüne hello günlüğüne toodo açmak hello Hadoop komut satırı konsolunu ve buradan hello Hive sorguları göndermek. Merhaba Hadoop komut satırı konsolunda Hive sorguları gönderme ile ilgili yönergeler için bkz: [nasıl tooSubmit Hive sorguları](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="uniform"></a>Tekdüzen rastgele örnekleme
Tekdüzen rastgele örnekleme hello veri kümesindeki her satır örneklenen şansı eşittir sahip olduğu anlamına gelir. Bu hello iç "Seç" sorguda bir ek alan rand() toohello veri kümesi ekleyerek uygulanabilir ve dış "Seç" sorgu içinde rastgele alan bu koşula hello.

Örnek bir sorgu şöyledir:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

Burada, `<sample rate, 0-1>` hello kullanıcıların toosample istediğiniz kayıtları hello oranını belirtir.

## <a name="group"></a>Gruplara göre rastgele örnekleme
Örnekleme kategorik veri istediğinizde, tooeither içerebilir veya tüm belirli bazı Kategorik bir değişkenin değerini hello örneklerinin dışlayabilirsiniz. "Grubu tarafından örnekleme" tarafından amacı budur.
Örneğin, "Durum" Kategorik bir değişken varsa, NY, MA, CA, NJ, PA vb. değerleri olan, kayıtların istediğiniz Merhaba aynı duruma olması her zaman birlikte veya örneklenen.

Grup tarafından bu örnekleri örnek bir sorgu şöyledir:

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <a name="stratified"></a>Stratified örnekleme
Rastgele örnekleme stratified değişkeniyle hello olan hello örnekleri elde edilen değerleri bu kategorik olduğunda saygı tooa kategorik örnekleri hangi hello alınan hello üst popülasyon olduğu gibi aynı oranı. Kullanarak hello yukarıdaki gibi aynı örnek verilerinizi alt yerleştirme tarafından durumda, deyin NJ 100 gözlemleri, NY sahip 60 gözlemleri ve WA varsa 300 gözlemleri varsayalım. Merhaba oranını belirtirseniz örnekleme toobe 0,5 stratified sonra hello elde örnek yaklaşık 50, 30 ve 150 gözlemleri NJ, NY ve WA sırasıyla olması gerekir.

Örnek bir sorgu şöyledir:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


Kovanında kullanılabilir daha gelişmiş örnekleme yöntemleri hakkında daha fazla bilgi için bkz: [LanguageManual örnekleme](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).


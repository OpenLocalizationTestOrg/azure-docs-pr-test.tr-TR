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
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="57271-103">Azure HDInsight Hive tablolarındaki örnek veriler</span><span class="sxs-lookup"><span data-stu-id="57271-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="57271-104">Bu makalede, Azure Hdınsight Hive tabloları Hive sorgularını kullanarak depolanan nasıl toodown örnek veriler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57271-104">In this article, we describe how toodown-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="57271-105">Şu üç özellik kullanılan örnekleme yöntemleri kapsar:</span><span class="sxs-lookup"><span data-stu-id="57271-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="57271-106">Tekdüzen rastgele örnekleme</span><span class="sxs-lookup"><span data-stu-id="57271-106">Uniform random sampling</span></span>
* <span data-ttu-id="57271-107">Gruplara göre rastgele örnekleme</span><span class="sxs-lookup"><span data-stu-id="57271-107">Random sampling by groups</span></span>
* <span data-ttu-id="57271-108">Stratified örnekleme</span><span class="sxs-lookup"><span data-stu-id="57271-108">Stratified sampling</span></span>

<span data-ttu-id="57271-109">Merhaba aşağıdaki **menü** açıklayan tootopics bağlantıları nasıl çeşitli depolama ortamları toosample verileri.</span><span class="sxs-lookup"><span data-stu-id="57271-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="57271-110">**Neden verilerinizi örnek?**</span><span class="sxs-lookup"><span data-stu-id="57271-110">**Why sample your data?**</span></span>
<span data-ttu-id="57271-111">Tooanalyze planladığınız hello veri kümesi, bu genellikle iyi bir fikir toodown örnek hello veri tooreduce büyükse, tooa daha küçük, ancak temsili ve daha kolay yönetilebilir boyutu.</span><span class="sxs-lookup"><span data-stu-id="57271-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="57271-112">Bu, veri anlama, keşfi ve özellik Mühendisliği kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="57271-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="57271-113">Kendi hello takım veri bilimi işlemi içinde tooenable hızlı prototipi oluşturulurken hello veri işleme işlevleri ve makine öğrenimi modellerinin oluşturulmasına rolüdür.</span><span class="sxs-lookup"><span data-stu-id="57271-113">Its role in hello Team Data Science Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="57271-114">Merhaba adımda bu örnekleme görevdir [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="57271-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-toosubmit-hive-queries"></a><span data-ttu-id="57271-115">Nasıl toosubmit Hive sorguları</span><span class="sxs-lookup"><span data-stu-id="57271-115">How toosubmit Hive queries</span></span>
<span data-ttu-id="57271-116">Hive sorguları hello Hadoop kümesi baş düğümünde hello hello Hadoop komut satırı konsolundan gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="57271-116">Hive queries can be submitted from hello Hadoop Command Line console on hello head node of hello Hadoop cluster.</span></span> <span data-ttu-id="57271-117">Bu, hello Hadoop küme baş düğümüne hello günlüğüne toodo açmak hello Hadoop komut satırı konsolunu ve buradan hello Hive sorguları göndermek.</span><span class="sxs-lookup"><span data-stu-id="57271-117">toodo this, log into hello head node of hello Hadoop cluster, open hello Hadoop Command Line console, and submit hello Hive queries from there.</span></span> <span data-ttu-id="57271-118">Merhaba Hadoop komut satırı konsolunda Hive sorguları gönderme ile ilgili yönergeler için bkz: [nasıl tooSubmit Hive sorguları](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="57271-118">For instructions on submitting Hive queries in hello Hadoop Command Line console, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="57271-119"><a name="uniform"></a>Tekdüzen rastgele örnekleme</span><span class="sxs-lookup"><span data-stu-id="57271-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="57271-120">Tekdüzen rastgele örnekleme hello veri kümesindeki her satır örneklenen şansı eşittir sahip olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="57271-120">Uniform random sampling means that each row in hello data set has an equal chance of being sampled.</span></span> <span data-ttu-id="57271-121">Bu hello iç "Seç" sorguda bir ek alan rand() toohello veri kümesi ekleyerek uygulanabilir ve dış "Seç" sorgu içinde rastgele alan bu koşula hello.</span><span class="sxs-lookup"><span data-stu-id="57271-121">This can be implemented by adding an extra field rand() toohello data set in hello inner "select" query, and in hello outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="57271-122">Örnek bir sorgu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="57271-122">Here is an example query:</span></span>

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

<span data-ttu-id="57271-123">Burada, `<sample rate, 0-1>` hello kullanıcıların toosample istediğiniz kayıtları hello oranını belirtir.</span><span class="sxs-lookup"><span data-stu-id="57271-123">Here, `<sample rate, 0-1>` specifies hello proportion of records that hello users want toosample.</span></span>

## <span data-ttu-id="57271-124"><a name="group"></a>Gruplara göre rastgele örnekleme</span><span class="sxs-lookup"><span data-stu-id="57271-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="57271-125">Örnekleme kategorik veri istediğinizde, tooeither içerebilir veya tüm belirli bazı Kategorik bir değişkenin değerini hello örneklerinin dışlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57271-125">When sampling categorical data, you may want tooeither include or exclude all of hello instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="57271-126">"Grubu tarafından örnekleme" tarafından amacı budur.</span><span class="sxs-lookup"><span data-stu-id="57271-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="57271-127">Örneğin, "Durum" Kategorik bir değişken varsa, NY, MA, CA, NJ, PA vb. değerleri olan, kayıtların istediğiniz Merhaba aynı duruma olması her zaman birlikte veya örneklenen.</span><span class="sxs-lookup"><span data-stu-id="57271-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of hello same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="57271-128">Grup tarafından bu örnekleri örnek bir sorgu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="57271-128">Here is an example query that samples by group:</span></span>

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

## <span data-ttu-id="57271-129"><a name="stratified"></a>Stratified örnekleme</span><span class="sxs-lookup"><span data-stu-id="57271-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="57271-130">Rastgele örnekleme stratified değişkeniyle hello olan hello örnekleri elde edilen değerleri bu kategorik olduğunda saygı tooa kategorik örnekleri hangi hello alınan hello üst popülasyon olduğu gibi aynı oranı.</span><span class="sxs-lookup"><span data-stu-id="57271-130">Random sampling is stratified with respect tooa categorical variable when hello samples obtained have values of that categorical that are in hello same ratio as in hello parent population from which hello samples were obtained.</span></span> <span data-ttu-id="57271-131">Kullanarak hello yukarıdaki gibi aynı örnek verilerinizi alt yerleştirme tarafından durumda, deyin NJ 100 gözlemleri, NY sahip 60 gözlemleri ve WA varsa 300 gözlemleri varsayalım.</span><span class="sxs-lookup"><span data-stu-id="57271-131">Using hello same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="57271-132">Merhaba oranını belirtirseniz örnekleme toobe 0,5 stratified sonra hello elde örnek yaklaşık 50, 30 ve 150 gözlemleri NJ, NY ve WA sırasıyla olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="57271-132">If you specify hello rate of stratified sampling toobe 0.5, then hello sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="57271-133">Örnek bir sorgu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="57271-133">Here is an example query:</span></span>

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


<span data-ttu-id="57271-134">Kovanında kullanılabilir daha gelişmiş örnekleme yöntemleri hakkında daha fazla bilgi için bkz: [LanguageManual örnekleme](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="57271-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>


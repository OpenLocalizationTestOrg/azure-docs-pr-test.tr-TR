---
title: "Örnek Azure Hdınsight Hive tablolarındaki verileri | Microsoft Docs"
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
ms.openlocfilehash: d46297dfaf85976114fbf610803e5f1a997041e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="246f4-103">Azure HDInsight Hive tablolarındaki örnek veriler</span><span class="sxs-lookup"><span data-stu-id="246f4-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="246f4-104">Bu makalede, Azure Hdınsight Hive tabloları Hive sorgularını kullanarak depolanan veriler aşağı-sample değiştireceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="246f4-104">In this article, we describe how to down-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="246f4-105">Şu üç özellik kullanılan örnekleme yöntemleri kapsar:</span><span class="sxs-lookup"><span data-stu-id="246f4-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="246f4-106">Tekdüzen rastgele örnekleme</span><span class="sxs-lookup"><span data-stu-id="246f4-106">Uniform random sampling</span></span>
* <span data-ttu-id="246f4-107">Gruplara göre rastgele örnekleme</span><span class="sxs-lookup"><span data-stu-id="246f4-107">Random sampling by groups</span></span>
* <span data-ttu-id="246f4-108">Stratified örnekleme</span><span class="sxs-lookup"><span data-stu-id="246f4-108">Stratified sampling</span></span>

<span data-ttu-id="246f4-109">Aşağıdaki **menü** çeşitli depolama ortamlarından veri örneği nasıl açıklayan konulara bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="246f4-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="246f4-110">**Neden verilerinizi örnek?**</span><span class="sxs-lookup"><span data-stu-id="246f4-110">**Why sample your data?**</span></span>
<span data-ttu-id="246f4-111">Analiz etmek için planlama dataset büyükse, genellikle aşağı örnek için daha küçük, ancak temsili ve daha kolay yönetilebilir bir boyutunu azaltmak için veri için iyi bir fikir değil.</span><span class="sxs-lookup"><span data-stu-id="246f4-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="246f4-112">Bu, veri anlama, keşfi ve özellik Mühendisliği kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="246f4-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="246f4-113">Takım veri bilimi işleminde rolü hızlı prototipi oluşturulurken veri işleme işlevleri ve makine öğrenimi modellerinin oluşturulmasına etkinleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="246f4-113">Its role in the Team Data Science Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="246f4-114">Bir adımda bu örnekleme görevdir [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="246f4-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-to-submit-hive-queries"></a><span data-ttu-id="246f4-115">Hive sorguları gönderme</span><span class="sxs-lookup"><span data-stu-id="246f4-115">How to submit Hive queries</span></span>
<span data-ttu-id="246f4-116">Hive sorguları, Hadoop küme baş düğümü üzerinde Hadoop komut satırı konsolundan gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="246f4-116">Hive queries can be submitted from the Hadoop Command Line console on the head node of the Hadoop cluster.</span></span> <span data-ttu-id="246f4-117">Bunu yapmak için Hadoop küme baş düğümüne oturum, Hadoop komut satırı konsolunu açın ve buradan Hive sorguları göndermek.</span><span class="sxs-lookup"><span data-stu-id="246f4-117">To do this, log into the head node of the Hadoop cluster, open the Hadoop Command Line console, and submit the Hive queries from there.</span></span> <span data-ttu-id="246f4-118">Hadoop komut satırı konsolunda Hive sorguları gönderme ile ilgili yönergeler için bkz: [Hive sorguları göndermek için nasıl](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="246f4-118">For instructions on submitting Hive queries in the Hadoop Command Line console, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="246f4-119"><a name="uniform"></a>Tekdüzen rastgele örnekleme</span><span class="sxs-lookup"><span data-stu-id="246f4-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="246f4-120">Tekdüzen rastgele örnekleme veri kümesindeki her satır örneklenen şansı eşittir sahip olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="246f4-120">Uniform random sampling means that each row in the data set has an equal chance of being sampled.</span></span> <span data-ttu-id="246f4-121">Bu, ek alan rand() veri kümesine iç sorgu "Seç" ve "Seç" dış sorgu bu koşul, rastgele alan üzerinde ekleyerek uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="246f4-121">This can be implemented by adding an extra field rand() to the data set in the inner "select" query, and in the outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="246f4-122">Örnek bir sorgu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="246f4-122">Here is an example query:</span></span>

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

<span data-ttu-id="246f4-123">Burada, `<sample rate, 0-1>` kullanıcıları örneklemek istediğiniz kayıtları oranını belirtir.</span><span class="sxs-lookup"><span data-stu-id="246f4-123">Here, `<sample rate, 0-1>` specifies the proportion of records that the users want to sample.</span></span>

## <span data-ttu-id="246f4-124"><a name="group"></a>Gruplara göre rastgele örnekleme</span><span class="sxs-lookup"><span data-stu-id="246f4-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="246f4-125">Örnekleme kategorik verileri dahil etmek veya hariç tüm belirli bazı Kategorik bir değişkenin değerini örneklerinin istediğinizde.</span><span class="sxs-lookup"><span data-stu-id="246f4-125">When sampling categorical data, you may want to either include or exclude all of the instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="246f4-126">"Grubu tarafından örnekleme" tarafından amacı budur.</span><span class="sxs-lookup"><span data-stu-id="246f4-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="246f4-127">Örneğin, "Durum" Kategorik bir değişken varsa, NY, MA, CA, NJ, PA vb. değerleri olan, her zaman birlikte veya örneklenen olması aynı durumu kayıtları istersiniz.</span><span class="sxs-lookup"><span data-stu-id="246f4-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of the same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="246f4-128">Grup tarafından bu örnekleri örnek bir sorgu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="246f4-128">Here is an example query that samples by group:</span></span>

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

## <span data-ttu-id="246f4-129"><a name="stratified"></a>Stratified örnekleme</span><span class="sxs-lookup"><span data-stu-id="246f4-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="246f4-130">Elde örnekleri değerleri olduğunda rastgele örnekleme kategorik, örnekler elde üst popülasyon olduğu gibi aynı oranı olduğundan göre Kategorik bir değişken stratified.</span><span class="sxs-lookup"><span data-stu-id="246f4-130">Random sampling is stratified with respect to a categorical variable when the samples obtained have values of that categorical that are in the same ratio as in the parent population from which the samples were obtained.</span></span> <span data-ttu-id="246f4-131">Aynı örnek olarak kullanarak yukarıdaki verilerinizi alt yerleştirme tarafından durumda varsayalım, 100 gözlemleri NJ sahiptir, NY 60 gözlemleri ve WA 300 gözlemleri varsa söyleyin.</span><span class="sxs-lookup"><span data-stu-id="246f4-131">Using the same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="246f4-132">0,5 olarak stratified örnekleme oranını belirtirseniz, ardından elde örnek yaklaşık 50, 30 ve 150 gözlemleri NJ, NY ve WA sırasıyla olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="246f4-132">If you specify the rate of stratified sampling to be 0.5, then the sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="246f4-133">Örnek bir sorgu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="246f4-133">Here is an example query:</span></span>

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


<span data-ttu-id="246f4-134">Kovanında kullanılabilir daha gelişmiş örnekleme yöntemleri hakkında daha fazla bilgi için bkz: [LanguageManual örnekleme](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="246f4-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>


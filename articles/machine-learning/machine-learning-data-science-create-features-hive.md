---
title: "bir Hadoop kümesindeki Hive sorgularını kullanarak veri aaaCreate özellikleri | Microsoft Docs"
description: "Bir Azure Hdınsight Hadoop kümesinde depolanan verilerin özelliklerini Oluştur Hive sorguları örnekleri."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="330cb-103">Hive sorgularını kullanarak bir Hadoop kümesindeki verilerin özelliklerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="330cb-103">Create features for data in an Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="330cb-104">Bu belge nasıl veri toocreate özellikleri Hive sorgularını kullanarak, Azure Hdınsight Hadoop kümesi depolanan gösterir.</span><span class="sxs-lookup"><span data-stu-id="330cb-104">This document shows how toocreate features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="330cb-105">Bu Hive sorguları katıştırılmış Hive kullanıcı tanımlı işlevler (UDF'ler) kullanmak, hello betikler kendisi için sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="330cb-105">These Hive queries use embedded Hive User Defined Functions (UDFs), hello scripts for which are provided.</span></span>

<span data-ttu-id="330cb-106">Merhaba gereken işlem toocreate özellikleri yoğun olabilir.</span><span class="sxs-lookup"><span data-stu-id="330cb-106">hello operations needed toocreate features can be memory intensive.</span></span> <span data-ttu-id="330cb-107">Hive sorguları Hello performansını bu gibi durumlarda daha önemli hale gelir ve belirli parametreleri ayarlama tarafından geliştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="330cb-107">hello performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="330cb-108">Bu parametreleri Hello ayarlama hello son bölümünde ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="330cb-108">hello tuning of these parameters is discussed in hello final section.</span></span>

<span data-ttu-id="330cb-109">Sunulan hello sorguları örnekleri olan belirli toohello [NYC ücreti seyahat veri](http://chriswhong.com/open-data/foil_nyc_taxi/) senaryoları burada da sunulmaktadır [GitHub deposunu](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="330cb-109">Examples of hello queries that are presented are specific toohello [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="330cb-110">Bu sorgular zaten belirtilen veri şeması varsa ve gönderilen hazır toobe toorun.</span><span class="sxs-lookup"><span data-stu-id="330cb-110">These queries already have data schema specified and are ready toobe submitted toorun.</span></span> <span data-ttu-id="330cb-111">Merhaba son bölümünde, kullanıcıların ayarlayabilirsiniz ve böylece Hive sorguları hello performansı artırılabilir parametreleri de ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="330cb-111">In hello final section, parameters that users can tune so that hello performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="330cb-112">Bu **menü** nasıl toocreate çeşitli ortamlarda veri özellikleri açıklamak tootopics bağlar.</span><span class="sxs-lookup"><span data-stu-id="330cb-112">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="330cb-113">Bu görev bir hello adımdır [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="330cb-113">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="330cb-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="330cb-114">Prerequisites</span></span>
<span data-ttu-id="330cb-115">Bu makalede, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="330cb-115">This article assumes that you have:</span></span>

* <span data-ttu-id="330cb-116">Bir Azure depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="330cb-116">Created an Azure storage account.</span></span> <span data-ttu-id="330cb-117">Yönergeler gerekiyorsa bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="330cb-117">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="330cb-118">Özelleştirilmiş bir Hadoop kümesine hello Hdınsight hizmeti ile sağlandı.</span><span class="sxs-lookup"><span data-stu-id="330cb-118">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="330cb-119">Yönergeler gerekiyorsa bkz [Advanced Analytics için Azure Hdınsight Hadoop kümeleri özelleştirme](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="330cb-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="330cb-120">Merhaba veri Azure Hdınsight Hadoop kümeleri karşıya yüklenen tooHive tablolarda olmuştur.</span><span class="sxs-lookup"><span data-stu-id="330cb-120">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="330cb-121">Bunu henüz yoksa, lütfen izleyin [oluşturma ve yük veri tooHive tabloları](machine-learning-data-science-move-hive-tables.md) tooupload veri tooHive tabloları ilk.</span><span class="sxs-lookup"><span data-stu-id="330cb-121">If it has not, please follow [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="330cb-122">Uzaktan erişim toohello küme etkin.</span><span class="sxs-lookup"><span data-stu-id="330cb-122">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="330cb-123">Yönergeler gerekiyorsa bkz [erişim hello Hadoop kümesi, baş düğüm](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="330cb-123">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <span data-ttu-id="330cb-124"><a name="hive-featureengineering"></a>Özellik oluşturma</span><span class="sxs-lookup"><span data-stu-id="330cb-124"><a name="hive-featureengineering"></a>Feature Generation</span></span>
<span data-ttu-id="330cb-125">Bu bölümde, hangi özellikler Hive sorguları oluşturarak hello yolları bazı örnekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="330cb-125">In this section, several examples of hello ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="330cb-126">Ek özellikler oluşturduktan sonra sütunları toohello var olan tablo olarak ekleyin veya hello ek özellikler ve ardından hello özgün tabloyla katılabilir birincil anahtarı ile yeni bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="330cb-126">Once you have generated additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, which can then be joined with hello original table.</span></span> <span data-ttu-id="330cb-127">Sunulan hello örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="330cb-127">Here are hello examples presented:</span></span>

1. [<span data-ttu-id="330cb-128">Özellik oluşturma sıklığı alarak</span><span class="sxs-lookup"><span data-stu-id="330cb-128">Frequency based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="330cb-129">İkili sınıflandırma kategorik değişkenlerin riskleri</span><span class="sxs-lookup"><span data-stu-id="330cb-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="330cb-130">Datetime alanından özellikleri Ayıkla</span><span class="sxs-lookup"><span data-stu-id="330cb-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="330cb-131">Metin alanından özellikleri Ayıkla</span><span class="sxs-lookup"><span data-stu-id="330cb-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="330cb-132">GPS koordinatları arasındaki uzaklığı Hesapla</span><span class="sxs-lookup"><span data-stu-id="330cb-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <span data-ttu-id="330cb-133"><a name="hive-frequencyfeature"></a>Özellik oluşturma sıklığı alarak</span><span class="sxs-lookup"><span data-stu-id="330cb-133"><a name="hive-frequencyfeature"></a>Frequency based Feature Generation</span></span>
<span data-ttu-id="330cb-134">Genellikle, yararlı toocalculate hello sıklıkları hello düzeyleri Kategorik bir değişkenin veya birden çok kategorik değişkenleri düzeylerinden belirli birleşimlerini hello sıklıkları olur.</span><span class="sxs-lookup"><span data-stu-id="330cb-134">It is often useful toocalculate hello frequencies of hello levels of a categorical variable, or hello frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="330cb-135">Kullanıcılar bu sıklıklarını betik toocalculate aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="330cb-135">Users can use hello following script toocalculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <span data-ttu-id="330cb-136"><a name="hive-riskfeature"></a>İkili sınıflandırma kategorik değişkenlerin riskleri</span><span class="sxs-lookup"><span data-stu-id="330cb-136"><a name="hive-riskfeature"></a>Risks of Categorical Variables in Binary Classification</span></span>
<span data-ttu-id="330cb-137">Yalnızca kullanılan hello modelleri sayısal özellikleri zaman ikili sınıflandırmasında tooconvert sayısal olmayan kategorik değişkenleri sayısal özelliklerini ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="330cb-137">In binary classification, we need tooconvert non-numeric categorical variables into numeric features when hello models being used only take numeric features.</span></span> <span data-ttu-id="330cb-138">Bu, her bir sayısal olmayan düzeyi ile sayısal bir risk değiştirerek gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="330cb-138">This is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="330cb-139">Bu bölümde, bir kategorik değişkenin hello risk değerleri (günlük büyük olasılıkla) hesaplama bazı genel Hive sorguları gösterir.</span><span class="sxs-lookup"><span data-stu-id="330cb-139">In this section, we show some generic Hive queries that calculate hello risk values (log odds) of a categorical variable.</span></span>

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

<span data-ttu-id="330cb-140">Bu örnekte, değişkenleri `smooth_param1` ve `smooth_param2` ayarlanmış toosmooth hello risk değerlerinin hello verilerden hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="330cb-140">In this example, variables `smooth_param1` and `smooth_param2` are set toosmooth hello risk values calculated from hello data.</span></span> <span data-ttu-id="330cb-141">Risk -INF INF arasındaki aralığı yok.</span><span class="sxs-lookup"><span data-stu-id="330cb-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="330cb-142">Riskleri > 0 hello hedefleyen eşit too1 olma hello olasılığı 0,5 büyük olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="330cb-142">A risks > 0 indicates that hello probability that hello target is equal too1 is greater than 0.5.</span></span>

<span data-ttu-id="330cb-143">Hesaplanan Hello risk tablo sonra kullanıcılar hello risk tabloyla birleştirerek risk değerler tooa tablosu atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="330cb-143">After hello risk table is calculated, users can assign risk values tooa table by joining it with hello risk table.</span></span> <span data-ttu-id="330cb-144">Merhaba Hive katılma sorgusu, önceki bölümde sağlandı.</span><span class="sxs-lookup"><span data-stu-id="330cb-144">hello Hive joining query was provided in previous section.</span></span>

### <span data-ttu-id="330cb-145"><a name="hive-datefeatures"></a>Datetime alanlardan özellikleri Ayıkla</span><span class="sxs-lookup"><span data-stu-id="330cb-145"><a name="hive-datefeatures"></a>Extract features from Datetime Fields</span></span>
<span data-ttu-id="330cb-146">Hive, datetime alanları işlemek için UDF'ler kümesiyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="330cb-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="330cb-147">Kovanında, hello varsayılan tarih/saat biçimi olan ' yyyy-aa-gg 00:00:00 ' (' 1970'ten-01-01 12:21:32 ' gibi).</span><span class="sxs-lookup"><span data-stu-id="330cb-147">In Hive, hello default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="330cb-148">Bu bölümde, hello gün, ay, bir datetime alanı hello month ayıklamak örnekler ve varsayılan biçim hello varsayılan biçimi tooa datetime dizesi dışında tarih saat biçiminde bir dize olarak bir dönüştürme diğer örnekleri göster.</span><span class="sxs-lookup"><span data-stu-id="330cb-148">In this section, we show examples that extract hello day of a month, hello month from a datetime field, and other examples that convert a datetime string in a format other than hello default format tooa datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="330cb-149">Bu Hive sorgusu o hello varsayar *&#60; datetime alan >* hello varsayılan tarih/saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="330cb-149">This Hive query assumes that hello *&#60;datetime field>* is in hello default datetime format.</span></span>

<span data-ttu-id="330cb-150">Bir datetime alanı hello varsayılan biçiminde değil, tooconvert hello datetime alanı UNIX zaman damgası önce gerekir ve ardından damga tooa datetime dize dönüştürme hello UNIX süresi hello varsayılan olarak ise biçimi.</span><span class="sxs-lookup"><span data-stu-id="330cb-150">If a datetime field is not in hello default format, you need tooconvert hello datetime field into Unix time stamp first, and then convert hello Unix time stamp tooa datetime string that is in hello default format.</span></span> <span data-ttu-id="330cb-151">Merhaba datetime biçim varsayılan olduğunda, kullanıcılar katıştırılmış hello datetime UDF'ler tooextract özellikleri uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="330cb-151">When hello datetime is in default format, users can apply hello embedded datetime UDFs tooextract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="330cb-152">Merhaba, bu sorgu *&#60; datetime alanı >* gibi hello düzeni sahip *03/26/2015 12:04:39*, hello *' &#60; hello datetime alanı desenini >'* olmalıdır `'MM/dd/yyyy HH:mm:ss'`.</span><span class="sxs-lookup"><span data-stu-id="330cb-152">In this query, if hello *&#60;datetime field>* has hello pattern like *03/26/2015 12:04:39*, hello *'&#60;pattern of hello datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="330cb-153">tootest, kullanıcıların çalıştırabileceği</span><span class="sxs-lookup"><span data-stu-id="330cb-153">tootest it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="330cb-154">Merhaba *hivesampletable* hello kümeleri sağlandığında bu sorguda tüm Azure Hdınsight Hadoop kümeleri üzerinde varsayılan olarak önceden yüklenmiş olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="330cb-154">hello *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when hello clusters are provisioned.</span></span>

### <span data-ttu-id="330cb-155"><a name="hive-textfeatures"></a>Metin alanları özellikleri Ayıkla</span><span class="sxs-lookup"><span data-stu-id="330cb-155"><a name="hive-textfeatures"></a>Extract features from Text Fields</span></span>
<span data-ttu-id="330cb-156">Merhaba Hive tablosu boşluklarla ayrılmış sözcükler dizesi içeren bir metin alanı olduğunda, hello aşağıdaki sorguyu hello dize ve sözcük hello dizesinde hello sayısını hello uzunluğu ayıklar.</span><span class="sxs-lookup"><span data-stu-id="330cb-156">When hello Hive table has a text field that contains a string of words that are delimited by spaces, hello following query extracts hello length of hello string, and hello number of words in hello string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <span data-ttu-id="330cb-157"><a name="hive-gpsdistance"></a>GPS koordinat kümeleri arasındaki uzaklıkları Hesapla</span><span class="sxs-lookup"><span data-stu-id="330cb-157"><a name="hive-gpsdistance"></a>Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="330cb-158">Bu bölümde verilen hello sorgu doğrudan uygulanan toohello NYC ücreti seyahat veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="330cb-158">hello query given in this section can be directly applied toohello NYC Taxi Trip Data.</span></span> <span data-ttu-id="330cb-159">Bu sorgu Hello amacı tooshow nasıl tooapply katıştırılmış matematik işlevleri Hive toogenerate özellikleri.</span><span class="sxs-lookup"><span data-stu-id="330cb-159">hello purpose of this query is tooshow how tooapply an embedded mathematical functions in Hive toogenerate features.</span></span>

<span data-ttu-id="330cb-160">Merhaba bu sorguda kullanılan adlı, toplama ve dropoff konumları hello GPS koordinatları alanları *toplama\_boylam*, *toplama\_enlem*,  *dropoff\_boylam*, ve *dropoff\_enlem*.</span><span class="sxs-lookup"><span data-stu-id="330cb-160">hello fields that are used in this query are hello GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="330cb-161">Merhaba alımı ve dropoff koordinatları arasındaki hello doğrudan uzaklığı hesaplamak hello sorgular şunlardır:</span><span class="sxs-lookup"><span data-stu-id="330cb-161">hello queries that calculate hello direct distance between hello pickup and dropoff coordinates are:</span></span>

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

<span data-ttu-id="330cb-162">iki GPS koordinatları arasındaki hello uzaklığı hesaplamak hello matematiksel denklemini hello üzerinde bulunabilir <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">taşınabilir tür betikleri</a> Peter Lapisu tarafından yazılan site.</span><span class="sxs-lookup"><span data-stu-id="330cb-162">hello mathematical equations that calculate hello distance between two GPS coordinates can be found on hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="330cb-163">Kendi JavaScript'te işlevi hello `toRad()` tıpkı *lat_or_lon*pi/180 *, derece tooradians dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="330cb-163">In his Javascript, hello function `toRad()` is just *lat_or_lon*pi/180*, which converts degrees tooradians.</span></span> <span data-ttu-id="330cb-164">Burada, *lat_or_lon* hello enlem veya boylam.</span><span class="sxs-lookup"><span data-stu-id="330cb-164">Here, *lat_or_lon* is hello latitude or longitude.</span></span> <span data-ttu-id="330cb-165">Hive hello işlevi sağlamadığından `atan2`, ancak hello işlevi sağlar `atan`, hello `atan2` işlevi tarafından gerçekleştirilir `atan` sağlanan hello tanımı kullanılarak Hive sorgusu yukarıda hello işlevinde <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>.</span><span class="sxs-lookup"><span data-stu-id="330cb-165">Since Hive does not provide hello function `atan2`, but provides hello function `atan`, hello `atan2` function is implemented by `atan` function in hello above Hive query using hello definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![Çalışma alanı oluşturma](./media/machine-learning-data-science-create-features-hive/atan2new.png)

<span data-ttu-id="330cb-167">Katıştırılmış UDF'ler hello bulunabilir Hive tam listesi **yerleşik işlevler** hello bölüm <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span><span class="sxs-lookup"><span data-stu-id="330cb-167">A full list of Hive embedded UDFs can be found in hello **Built-in Functions** section on hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <span data-ttu-id="330cb-168"><a name="tuning"></a>Gelişmiş konular: ayarlama Hive parametreleri tooImprove sorgu hızı</span><span class="sxs-lookup"><span data-stu-id="330cb-168"><a name="tuning"></a> Advanced topics: Tune Hive Parameters tooImprove Query Speed</span></span>
<span data-ttu-id="330cb-169">Merhaba varsayılan parametre ayarları Hive kümesinin hello Hive sorguları ve hello sorguları işlerken hello veri için uygun olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="330cb-169">hello default parameter settings of Hive cluster might not be suitable for hello Hive queries and hello data that hello queries are processing.</span></span> <span data-ttu-id="330cb-170">Bu bölümde, Hive sorguları hello performansını kullanıcılar ayarlayabilirsiniz bazı parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="330cb-170">In this section, we discuss some parameters that users can tune that improve hello performance of Hive queries.</span></span> <span data-ttu-id="330cb-171">Kullanıcıların veri işleme hello sorguları önce sorguları ayarlama tooadd hello parametresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="330cb-171">Users need tooadd hello parameter tuning queries before hello queries of processing data.</span></span>

1. <span data-ttu-id="330cb-172">**Java yığın alanı**: büyük veri kümeleri katılma veya uzun kayıtlarının işlenmesinden içeren sorgular için **yığın alana sahip** hello sık karşılaşılan hatalardan biri.</span><span class="sxs-lookup"><span data-stu-id="330cb-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of hello common error.</span></span> <span data-ttu-id="330cb-173">Bu parametreleri ayarlayarak ayarlanabilecek *mapreduce.map.java.opts* ve *mapreduce.task.io.sort.mb* toodesired değerleri.</span><span class="sxs-lookup"><span data-stu-id="330cb-173">This can be tuned by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* toodesired values.</span></span> <span data-ttu-id="330cb-174">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="330cb-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="330cb-175">Bu parametre, 4 GB bellek tooJava yığın alan ayırır ve ayrıca sıralama daha verimli daha fazla bellek ayırarak hale getirir.</span><span class="sxs-lookup"><span data-stu-id="330cb-175">This parameter allocates 4GB memory tooJava heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="330cb-176">Herhangi bir işi hatası hataları ilgili tooheap alanı olduğunda iyi bir fikir tooplay Bu ayırmaları sahip olur.</span><span class="sxs-lookup"><span data-stu-id="330cb-176">It is a good idea tooplay with these allocations if there are any job failure errors related tooheap space.</span></span>

1. <span data-ttu-id="330cb-177">**DFS bloğu boyutunu** : Bu parametre hello en küçük birim dosya sistemi depoları hello veri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="330cb-177">**DFS block size** : This parameter sets hello smallest unit of data that hello file system stores.</span></span> <span data-ttu-id="330cb-178">Hello DFS blok boyutu 128 MB ise örnek olarak, daha sonra herhangi bir veri boyutu küçüktür ve too128MB yedekleme 128 MB ek blokları ayrılan büyük veriler tek bir blok depolanır.</span><span class="sxs-lookup"><span data-stu-id="330cb-178">As an example, if hello DFS block size is 128MB, then any data of size less than and up too128MB is stored in a single block, while data that is larger than 128MB is allotted extra blocks.</span></span> <span data-ttu-id="330cb-179">Tooprocess toohello dosya ilgili pek çok daha fazla istekleri toofind hello ilgili blok Hello adı düğümü olduğu için çok küçük blok boyutu seçme büyük ek yüklerini Hadoop neden olur.</span><span class="sxs-lookup"><span data-stu-id="330cb-179">Choosing a very small block size causes large overheads in Hadoop since hello name node has tooprocess many more requests toofind hello relevant block pertaining toohello file.</span></span> <span data-ttu-id="330cb-180">Bir önerilen ilgilenme gigabayt ile (veya daha büyük olduğunda) ayarı veriler:</span><span class="sxs-lookup"><span data-stu-id="330cb-180">A recommended setting when dealing with gigabytes (or larger) data is :</span></span>
   
        set dfs.block.size=128m;
2. <span data-ttu-id="330cb-181">**Hive katılma işleminde en iyi duruma getirme** : hello eşleme ve azaltma Framework'te birleştirme işlemleri genellikle hello yerinde alırken aşamasında, bazen azaltmak, muazzam kazanç elde edilebilir ("mapjoins" olarak da bilinir) hello harita aşamasında birleştirmeler zamanlayarak.</span><span class="sxs-lookup"><span data-stu-id="330cb-181">**Optimizing join operation in Hive** : While join operations in hello map/reduce framework typically take place in hello reduce phase, sometimes, enormous gains can be achieved by scheduling joins in hello map phase (also called "mapjoins").</span></span> <span data-ttu-id="330cb-182">toodirect Hive toodo bu mümkün olduğunda, biz ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="330cb-182">toodirect Hive toodo this whenever possible, we can set :</span></span>
   
        set hive.auto.convert.join=true;
3. <span data-ttu-id="330cb-183">**Mappers tooHive Hello sayısını belirterek** : mappers hello sayısı sırada Hadoop hello kullanıcı tooset hello reducers sayısını sağlar, genellikle hello kullanıcı tarafından değil ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="330cb-183">**Specifying hello number of mappers tooHive** : While Hadoop allows hello user tooset hello number of reducers, hello number of mappers is typically not be set by hello user.</span></span> <span data-ttu-id="330cb-184">Bu sayı denetiminde bazı derecesini veren el toochoose hello Hadoop değişkenleri olan *mapred.min.split.size* ve *mapred.max.split.size* her eşleme hello boyutu olarak görev tarafından belirlenir:</span><span class="sxs-lookup"><span data-stu-id="330cb-184">A trick that allows some degree of control on this number is toochoose hello Hadoop variables, *mapred.min.split.size* and *mapred.max.split.size* as hello size of each map task is determined by :</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="330cb-185">Genellikle, varsayılan değeri hello *mapred.min.split.size* 0 ' dır, *mapred.max.split.size* olan **Long.MAX** ve *dfs.block.size* 64 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="330cb-185">Typically, hello default value of *mapred.min.split.size* is 0, that of *mapred.max.split.size* is **Long.MAX** and that of *dfs.block.size* is 64MB.</span></span> <span data-ttu-id="330cb-186">Verilen hello veri boyutu görebiliriz gibi "ayarlayarak" Bu parametreleri ayarlama sağlar bize tootune hello kullanılan mappers sayısı.</span><span class="sxs-lookup"><span data-stu-id="330cb-186">As we can see, given hello data size, tuning these parameters by "setting" them allows us tootune hello number of mappers used.</span></span>
4. <span data-ttu-id="330cb-187">Diğer birkaç daha **Gelişmiş Seçenekler** Hive en iyi duruma getirme için performans belirtilen aşağıda.</span><span class="sxs-lookup"><span data-stu-id="330cb-187">A few other more **advanced options** for optimizing Hive performance are mentioned below.</span></span> <span data-ttu-id="330cb-188">Bunlar tooset hello ayrılmış bellek toomap izin ver ve görevleri azaltır ve performans uyguladıkça yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="330cb-188">These allow you tooset hello memory allocated toomap and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="330cb-189">Lütfen bu hello göz önünde bulundurmanız *mapreduce.reduce.memory.mb* hello Hadoop kümedeki her alt düğümün hello fiziksel bellek boyutundan büyük olamaz.</span><span class="sxs-lookup"><span data-stu-id="330cb-189">Please keep in mind that hello *mapreduce.reduce.memory.mb* cannot be greater than hello physical memory size of each worker node in hello Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;


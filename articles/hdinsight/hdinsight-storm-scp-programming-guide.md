---
title: "SCP.NET Programlama Kılavuzu | Microsoft Docs"
description: "SCP.NET oluşturmak için nasıl kullanılacağını öğrenin. Hdınsight üzerinde Storm ile NET tabanlı Storm Topolojileri için kullanın."
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: 3d76aebd2a1fd729c8e0639e6afcbde4c3fb752b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="88271-103">SCP Programlama Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="88271-103">SCP programming guide</span></span>
<span data-ttu-id="88271-104">SCP, gerçek zamanlı, güvenilir, tutarlı ve yüksek performans veri işleme uygulama oluşturmak için kullanılan bir platformdur.</span><span class="sxs-lookup"><span data-stu-id="88271-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="88271-105">Üstünde oluşturulmuş [Apache Storm](http://storm.incubator.apache.org/) --bir akış tarafından OSS toplulukları tasarlanmış sistemi işleme.</span><span class="sxs-lookup"><span data-stu-id="88271-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span></span> <span data-ttu-id="88271-106">Storm Nathan Marz ve açık kaynaklıdır Twitter tarafından tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="88271-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="88271-107">Bunu yararlanır [Apache ZooKeeper](http://zookeeper.apache.org/), yüksek oranda güvenilir etkinleştirmek için başka bir Apache proje dağıtılmış eşgüdümü ve durum yönetimi.</span><span class="sxs-lookup"><span data-stu-id="88271-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="88271-108">Yalnızca Windows üzerinde Storm SCP proje bağlantı noktası kurulmuş ancak proje uzantıları ve özelleştirme Windows ekosistemi için de eklenir.</span><span class="sxs-lookup"><span data-stu-id="88271-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span></span> <span data-ttu-id="88271-109">Uzantıları .NET geliştirme deneyimi ve kitaplıklarını içerir, Windows tabanlı bir dağıtım özelleştirme içerir.</span><span class="sxs-lookup"><span data-stu-id="88271-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="88271-110">Genişletme ve özelleştirme biz OSS projeleri çatallaştırma gerekmez ve Storm üstünde oluşturulmuş türetilmiş ekosistemlerini yararlanan bir şekilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="88271-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="88271-111">İşlem modeli</span><span class="sxs-lookup"><span data-stu-id="88271-111">Processing model</span></span>
<span data-ttu-id="88271-112">SCP verilerde diziler sürekli akışları olarak modellenir.</span><span class="sxs-lookup"><span data-stu-id="88271-112">The data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="88271-113">Genellikle başlıklar bazı sıraya ilk akış sonra toplanmış ve içindeki bir Storm topolojisinin barındırılan iş mantığı tarafından dönüştürülen, son çıktı başka bir SCP sistemine diziler olarak yöneltilen veya dağıtılmış dosya sistemi veya veritabanları gibi depoları için önem SQL Server gibi.</span><span class="sxs-lookup"><span data-stu-id="88271-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span></span>

![Bir veri deposu akışları işleme veri besleme bir sıra diyagramı](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="88271-115">Storm bir uygulama topolojisi hesaplama grafiği tanımlar.</span><span class="sxs-lookup"><span data-stu-id="88271-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="88271-116">Veri akışı düğümler arasındaki bağlantıları gösterir ve her düğüm topolojisinde işleme mantığı içerir.</span><span class="sxs-lookup"><span data-stu-id="88271-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="88271-117">Topoloji giriş verileri eklemesine düğümleri verileri sıralamak için kullanılan Spout'lar denir.</span><span class="sxs-lookup"><span data-stu-id="88271-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span></span> <span data-ttu-id="88271-118">Giriş verisi dosya günlükleri, işlemsel veritabanı, sistem performans sayacı vb. bulunması. Her iki girdi ve çıktı veri akışları düğümleriyle gerçek verileri filtreleme yapmak Cıvatalar ve seçimleri ve toplama denir.</span><span class="sxs-lookup"><span data-stu-id="88271-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="88271-119">SCP en iyi çaba, en az bir kere destekler ve tam olarak-kez veri işleme.</span><span class="sxs-lookup"><span data-stu-id="88271-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="88271-120">Bir dağıtılmış akış işleme uygulamasında, Ağ kaybı, makine hatasını ya da kullanıcı kodu hatası vb. gibi veri işleme sırasında çeşitli hatalar oluşabilir. En az bir kere işleme tüm veriler hata olduğunda otomatik olarak aynı verileri yeniden oynatmak tarafından en az bir kez işlenir sağlar.</span><span class="sxs-lookup"><span data-stu-id="88271-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span></span> <span data-ttu-id="88271-121">En az bir kere işleme basit ve güvenilir olduğunu ve iyi birçok uygulamada uygun.</span><span class="sxs-lookup"><span data-stu-id="88271-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="88271-122">Uygulamanın tam sayım gerektirdiğinde, aynı veri olası uygulama topolojisinde oynanan beri ancak, örneğin, en az bir kere işleme yeterli değil.</span><span class="sxs-lookup"><span data-stu-id="88271-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span></span> <span data-ttu-id="88271-123">Bu durumda, tam olarak-bile ne zaman veri yeniden ve birden çok kez işlenen işlem sonucu emin olmak için tasarlanmış bir kez doğru olduğundan.</span><span class="sxs-lookup"><span data-stu-id="88271-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="88271-124">SCP Dengeleme Java sanal makine (JVM) altında kapak Storm tabanlı gerçek zamanlı veri işlem uygulamaları geliştirmek .NET geliştiricilerinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="88271-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span></span> <span data-ttu-id="88271-125">.NET ve JVM TCP yerel yuva iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="88271-125">The .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="88271-126">Neredeyse her Spout/Cıvata bir .net/Java işlemi, kullanıcı mantığını .net işlem bir eklenti olarak çalıştığı çiftidir.</span><span class="sxs-lookup"><span data-stu-id="88271-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="88271-127">SCP en üstünde bir veri işleme uygulaması oluşturmak için birkaç adım gerekir:</span><span class="sxs-lookup"><span data-stu-id="88271-127">To build a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="88271-128">Veri sırasından çekmesini Spout'lar tasarlayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="88271-128">Design and implement the Spouts to pull in data from queue.</span></span>
* <span data-ttu-id="88271-129">Tasarım ve girdi verilerini işlemek için Cıvatalar uygulamak ve veritabanı gibi dış depolarına veri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="88271-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span></span>
* <span data-ttu-id="88271-130">Topoloji tasarım, gönderme ve topoloji çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="88271-130">Design the topology, then submit and run the topology.</span></span> <span data-ttu-id="88271-131">Topoloji köşeleri ve verileri tanımlayan köşeleri arasında akışları.</span><span class="sxs-lookup"><span data-stu-id="88271-131">The topology defines vertexes and the data flows between the vertexes.</span></span> <span data-ttu-id="88271-132">SCP topoloji belirtimi alın ve her köşe mantıksal bir düğüm üzerinde çalıştığı bir Storm kümede dağıtın.</span><span class="sxs-lookup"><span data-stu-id="88271-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="88271-133">Yük devretme ve Storm Görev Zamanlayıcı'yı dikkate ölçeklendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="88271-133">The failover and scaling will be taken care of by the Storm task scheduler.</span></span>

<span data-ttu-id="88271-134">Bu belge, SCP ile veri işleme uygulamasının nasıl oluşturulacağını size rehberlik için bazı basit örnekler kullanır.</span><span class="sxs-lookup"><span data-stu-id="88271-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="88271-135">SCP eklentisi arabirimi</span><span class="sxs-lookup"><span data-stu-id="88271-135">SCP Plugin Interface</span></span>
<span data-ttu-id="88271-136">SCP eklentileri (veya uygulamalar) hem de Visual Studio içinde geliştirme aşamasında çalışabilen ve Storm ardışık düzenine üretim dağıtım sonrasında takılı tek başına exe markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="88271-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span></span> <span data-ttu-id="88271-137">SCP eklentisi yazma tıpkı diğer standart Windows konsol uygulamaları yazma olarak olur.</span><span class="sxs-lookup"><span data-stu-id="88271-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="88271-138">Spout/Cıvata için bazı arabirimi SCP.NET platform bildirir ve kullanıcı eklenti kodu bu arabirimi uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="88271-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span></span> <span data-ttu-id="88271-139">Bu tasarım ana amacı, kullanıcının kendi iş logics ve SCP.NET platformu tarafından işlenecek başka şeyler bırakarak odaklanabilirsiniz..</span><span class="sxs-lookup"><span data-stu-id="88271-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span></span>

<span data-ttu-id="88271-140">Kullanıcı eklentisi kodu aşağıdakilere arabirimlerinden biri, uygulamalıdır, topoloji işlem ya da işlem dışı olmasına ve bileşen spout veya Cıvata olmasına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="88271-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span></span>

* <span data-ttu-id="88271-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="88271-141">ISCPSpout</span></span>
* <span data-ttu-id="88271-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="88271-142">ISCPBolt</span></span>
* <span data-ttu-id="88271-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="88271-143">ISCPTxSpout</span></span>
* <span data-ttu-id="88271-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="88271-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="88271-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="88271-145">ISCPPlugin</span></span>
<span data-ttu-id="88271-146">ISCPPlugin eklentileri her türlü ortak arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="88271-146">ISCPPlugin is the common interface for all kinds of plugins.</span></span> <span data-ttu-id="88271-147">Şu anda, onu bir kukla arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="88271-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="88271-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="88271-148">ISCPSpout</span></span>
<span data-ttu-id="88271-149">ISCPSpout işlemsel olmayan spout arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="88271-149">ISCPSpout is the interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="88271-150">Zaman `NextTuple()` çağrılır, C\# kullanıcı kodu bir veya daha fazla tanımlama grubu yayma.</span><span class="sxs-lookup"><span data-stu-id="88271-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="88271-151">Varsa yayma bir şey yok, bu yöntem herhangi bir şey yayma olmadan döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="88271-151">If there is nothing to emit, this method should return without emitting anything.</span></span> <span data-ttu-id="88271-152">Dikkat edilmesi gereken, `NextTuple()`, `Ack()`, ve `Fail()` tümü tek bir iş parçacığı c sıkı döngü denir\# işlemi.</span><span class="sxs-lookup"><span data-stu-id="88271-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="88271-153">Hiçbir tanımlama grubu yayma olduğunda, bu nedenle çok fazla CPU boşa harcanmasına değil olarak için kısa bir süre (örneğin, 10 milisaniye) için NextTuple uyku olması courteous.</span><span class="sxs-lookup"><span data-stu-id="88271-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="88271-154">`Ack()`ve `Fail()` ack mekanizması belirtim dosyasında yalnızca etkin olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="88271-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="88271-155">`seqId` Acked veya başarısız tanımlama grubu tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="88271-155">The `seqId` is used to identify the tuple which is acked or failed.</span></span> <span data-ttu-id="88271-156">Bu nedenle ACK işlemsel olmayan topolojisinde etkinleştirilirse, aşağıdaki emit işlevi içinde Spout kullanılmalıdır:</span><span class="sxs-lookup"><span data-stu-id="88271-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="88271-157">ACK işlemsel olmayan topolojisinde desteklenmiyorsa `Ack()` ve `Fail()` boş işlev olarak bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="88271-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="88271-158">`parms` Bu işlevler giriş parametrelerinde yalnızca boş sözlük, gelecekte kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="88271-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="88271-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="88271-159">ISCPBolt</span></span>
<span data-ttu-id="88271-160">ISCPBolt işlemsel olmayan Cıvata arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="88271-160">ISCPBolt is the interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="88271-161">Yeni tanımlama grubu mevcut olduğunda `Execute()` işlevi, onu işlemek üzere çağrılır.</span><span class="sxs-lookup"><span data-stu-id="88271-161">When new tuple is available, the `Execute()` function will be called to process it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="88271-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="88271-162">ISCPTxSpout</span></span>
<span data-ttu-id="88271-163">ISCPTxSpout işlem spout arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="88271-163">ISCPTxSpout is the interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="88271-164">İşlem olmayan karşı erişmelerini'olduğu gibi `NextTx()`, `Ack()`, ve `Fail()` tümü tek bir iş parçacığı c sıkı döngü denir\# işlemi.</span><span class="sxs-lookup"><span data-stu-id="88271-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="88271-165">Hiçbir veri yayma olduğunda sahip courteous `NextTx` uyku için kısa bir nedenle çok fazla CPU boşa harcanmasına değil olarak süresi (10 milisaniye).</span><span class="sxs-lookup"><span data-stu-id="88271-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="88271-166">`NextTx()`out parametresi yeni bir işlem başlatmaya adlı `seqId` ayrıca kullanılır işlem tanımlamak için kullanılan `Ack()` ve `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="88271-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="88271-167">İçinde `NextTx()`, kullanıcı veri Java dışarıdan yayma.</span><span class="sxs-lookup"><span data-stu-id="88271-167">In `NextTx()`, user can emit data to Java side.</span></span> <span data-ttu-id="88271-168">Verileri yeniden yürütme desteklemek için ZooKeeper içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="88271-168">The data will be stored in ZooKeeper to support replay.</span></span> <span data-ttu-id="88271-169">ZooKeeper kapasitesi sınırlı olduğundan, bir kullanıcı yalnızca meta veri yayma, işlem spout verileri toplu değil.</span><span class="sxs-lookup"><span data-stu-id="88271-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="88271-170">Storm yeniden yürütme bir işlem otomatik olarak başarısız olursa, bunu `Fail()` normal durumda çağrılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="88271-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="88271-171">Ancak SCP işlem spout'un yayılan meta verileri işaretlerseniz çağırabilirsiniz `Fail()` zaman meta veriler geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="88271-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span></span>

<span data-ttu-id="88271-172">`parms` Bu işlevler giriş parametrelerinde yalnızca boş sözlük, gelecekte kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="88271-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="88271-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="88271-173">ISCPBatchBolt</span></span>
<span data-ttu-id="88271-174">ISCPBatchBolt işlem Cıvata arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="88271-174">ISCPBatchBolt is the interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="88271-175">`Execute()`Yeni kayıt sırasında Cıvata ulaşan olduğunda çağrılır.</span><span class="sxs-lookup"><span data-stu-id="88271-175">`Execute()` is called when there is new tuple arriving at the bolt.</span></span> <span data-ttu-id="88271-176">`FinishBatch()`Bu işlem sona erdikten sonra çağrılır.</span><span class="sxs-lookup"><span data-stu-id="88271-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="88271-177">`parms` Giriş parametresi, gelecekte kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="88271-177">The `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="88271-178">İşlem topolojisi için önemli bir kavram – olduğundan `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="88271-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="88271-179">İki alanı olan `TxId` ve `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="88271-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="88271-180">`TxId`belirli bir işlemi tanımlamak için kullanılır ve belirli bir işlem için birden çok deneme işlemi başarısız olur ve durumunda olabilir yeniden.</span><span class="sxs-lookup"><span data-stu-id="88271-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span></span> <span data-ttu-id="88271-181">SCP.NET olacak yeni her işlemek için farklı bir ISCPBatchBolt nesne `StormTxAttempt`, yalnızca Java yan hangi Storm yapmak gibi.</span><span class="sxs-lookup"><span data-stu-id="88271-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="88271-182">Bu tasarım amacı, paralel işlemleri işleme desteklemektir.</span><span class="sxs-lookup"><span data-stu-id="88271-182">The purpose of this design is to support parallel transactions processing.</span></span> <span data-ttu-id="88271-183">Kullanıcı işlem girişimi tamamlandıysa, karşılık gelen ISCPBatchBolt nesne yok olduğunu unutmayın ve toplanacak tutmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="88271-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="88271-184">Nesne modeli</span><span class="sxs-lookup"><span data-stu-id="88271-184">Object Model</span></span>
<span data-ttu-id="88271-185">SCP.NET anahtar nesneleri ile program geliştiriciler için basit bir dizi de sağlar.</span><span class="sxs-lookup"><span data-stu-id="88271-185">SCP.NET also provides a simple set of key objects for developers to program with.</span></span> <span data-ttu-id="88271-186">Bunlar **bağlamı**, **StateStore**, ve **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="88271-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="88271-187">Bu bölümde rest parçası incelenecektir.</span><span class="sxs-lookup"><span data-stu-id="88271-187">They will be discussed in the rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="88271-188">Bağlam</span><span class="sxs-lookup"><span data-stu-id="88271-188">Context</span></span>
<span data-ttu-id="88271-189">Bağlamı uygulamaya çalışan bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="88271-189">Context provides a running environment to the application.</span></span> <span data-ttu-id="88271-190">Her ISCPPlugin örneğinin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) karşılık gelen bir bağlam örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="88271-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="88271-191">Bağlam tarafından sağlanan işlevleri iki bölüme ayrılabilir: tüm C kullanılabilir olan (1 statik bölümü\# işlem, yalnızca belirli bağlam örneği için kullanılabilir olan dinamik (2 bölümü.</span><span class="sxs-lookup"><span data-stu-id="88271-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="88271-192">Statik bölümü</span><span class="sxs-lookup"><span data-stu-id="88271-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="88271-193">`Logger`Günlük amaçla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="88271-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="88271-194">`pluginType`C eklentisi türünü belirtmek için kullanılan\# işlemi.</span><span class="sxs-lookup"><span data-stu-id="88271-194">`pluginType` is used to indicate the plugin type of the C\# process.</span></span> <span data-ttu-id="88271-195">Varsa C\# işlemi (olmadan Java) yerel test modda çalıştırılır, eklenti tür `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="88271-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="88271-196">`Config`Java taraftan yapılandırma parametreleri almak için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="88271-196">`Config` is provided to get configuration parameters from Java side.</span></span> <span data-ttu-id="88271-197">Java taraftan geçilen parametreler zaman C\# eklentisi başlatılır.</span><span class="sxs-lookup"><span data-stu-id="88271-197">The parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="88271-198">`Config` Parametreleri iki parçalara bölünür: `stormConf` ve `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="88271-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="88271-199">`stormConf`Storm tarafından tanımlanan parametre ve `pluginConf` SCP tarafından tanımlanan parametre.</span><span class="sxs-lookup"><span data-stu-id="88271-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span></span> <span data-ttu-id="88271-200">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="88271-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="88271-201">`TopologyContext`sağlanan topoloji içerik almak için birden çok paralellik ile bileşenleri için en yararlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="88271-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="88271-202">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="88271-202">Here is an example:</span></span>

    //demo how to get TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a><span data-ttu-id="88271-203">Dinamik bölümü</span><span class="sxs-lookup"><span data-stu-id="88271-203">Dynamic Part</span></span>
<span data-ttu-id="88271-204">Aşağıdaki arabirimleri belirli bir bağlam örneğine ilgili.</span><span class="sxs-lookup"><span data-stu-id="88271-204">The following interfaces are pertinent to a certain Context instance.</span></span> <span data-ttu-id="88271-205">Bağlam örneği SCP.NET platformu tarafından oluşturulur ve kullanıcı koduna geçirilen:</span><span class="sxs-lookup"><span data-stu-id="88271-205">The Context instance is created by SCP.NET platform and passed to the user code:</span></span>

    // Declare the Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple to default stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple to the specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="88271-206">ACK destekleme işlemsel olmayan spout için aşağıdaki yöntemi sağlanır:</span><span class="sxs-lookup"><span data-stu-id="88271-206">For non-transactional spout supporting ack, the following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="88271-207">ACK destekleme işlemsel olmayan Cıvata için açıkça gerektiği `Ack()` veya `Fail()` aldığı tanımlama grubu.</span><span class="sxs-lookup"><span data-stu-id="88271-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span></span> <span data-ttu-id="88271-208">Ve yeni bir tanımlama grubu yayma, ayrıca yeni tuple bağlayıcılarını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="88271-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span></span> <span data-ttu-id="88271-209">Aşağıdaki yöntemlerden sağlanır.</span><span class="sxs-lookup"><span data-stu-id="88271-209">The following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="88271-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="88271-210">StateStore</span></span>
<span data-ttu-id="88271-211">`StateStore`Meta Veri Hizmetleri, monoton sıra oluşturma ve bekleme serbest eşgüdüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="88271-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="88271-212">Üst düzey dağıtılmış eşzamanlılık soyutlamalar oluşturulabilen `StateStore`dağıtılmış kilitleri, dağıtılmış kuyruklar, engelleri ve işlem Hizmetleri dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="88271-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="88271-213">SCP uygulamalar kullanabilir `State` ZooKeeper, özellikle işlem topolojisi için bazı bilgileri kalıcı hale getirmek için nesne.</span><span class="sxs-lookup"><span data-stu-id="88271-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="88271-214">Böylece işlem spout çöker ve yeniden başlatırsanız, ZooKeeper gerekli bilgileri almak ve ardışık düzeni yeniden yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="88271-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span></span>

<span data-ttu-id="88271-215">`StateStore` Nesnenin çoğunlukla bu yöntemleri vardır:</span><span class="sxs-lookup"><span data-stu-id="88271-215">The `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method to retrieve a state store of the given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all the States in the StateStore
    /// </summary>
    /// <returns>All the States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all the committed states
    /// </summary>
    /// <returns>Registries contain the Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all the Aborted State in the StateStore
    /// </summary>
    /// <returns>Registries contain the Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of the State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="88271-216">`State` Nesnenin çoğunlukla bu yöntemleri vardır:</span><span class="sxs-lookup"><span data-stu-id="88271-216">The `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set the status of the state object to commit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set the status of the state object to abort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under the give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get the attribute value associated with the given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="88271-217">İçin `Commit()` simpleMode ayarlandığında yöntemi true, yalnızca ZooKeeper içinde karşılık gelen ZNode silecektir.</span><span class="sxs-lookup"><span data-stu-id="88271-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="88271-218">Aksi takdirde geçerli ZNode ve kabul edilen içinde yeni bir düğüm ekleme silecektir\_yolu.</span><span class="sxs-lookup"><span data-stu-id="88271-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="88271-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="88271-219">SCPRuntime</span></span>
<span data-ttu-id="88271-220">SCPRuntime aşağıdaki iki yöntem sunar.</span><span class="sxs-lookup"><span data-stu-id="88271-220">SCPRuntime provides the following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="88271-221">`Initialize()`SCP çalışma zamanı ortamı başlatmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="88271-221">`Initialize()` is used to initialize the SCP runtime environment.</span></span> <span data-ttu-id="88271-222">Bu yöntemde, C\# işlem bağlanan Java yan ve yapılandırma parametreleri alır ve topoloji bağlamı.</span><span class="sxs-lookup"><span data-stu-id="88271-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="88271-223">`LaunchPlugin()`ileti işleme döngüsü kazandırın için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="88271-223">`LaunchPlugin()` is used to kick off the message processing loop.</span></span> <span data-ttu-id="88271-224">Bu döngü, C\# eklentisi iletileri form Java yan (başlık ve denetim sinyalleri dahil) alır ve ardından işlem belki de arabirim yöntemini çağırarak iletileri, kullanıcı kodu tarafından sağlayın.</span><span class="sxs-lookup"><span data-stu-id="88271-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span></span> <span data-ttu-id="88271-225">Giriş parametresi yöntemi için `LaunchPlugin()` ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt arabirimini uygulayan nesne döndüren bir temsilci.</span><span class="sxs-lookup"><span data-stu-id="88271-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="88271-226">ISCPBatchBolt için biz alabilirsiniz `StormTxAttempt` gelen `parms`ve bunu denemedir yeniden yürütülmüş olup olmadığını değerlendirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88271-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span></span> <span data-ttu-id="88271-227">Bu genellikle yürütme Cıvata yapılır ve örneklerde gösterildiği `HelloWorldTx` örnek.</span><span class="sxs-lookup"><span data-stu-id="88271-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span></span>

<span data-ttu-id="88271-228">Genel olarak bakıldığında, SCP eklentileri burada iki modda çalışabilir:</span><span class="sxs-lookup"><span data-stu-id="88271-228">Generally speaking, the SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="88271-229">Yerel Test modu: Bu modda SCP eklentileri (C\# kullanıcı kodu) Visual Studio içinde geliştirme aşamasında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="88271-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span></span> <span data-ttu-id="88271-230">`LocalContext`Bu modda, yerel dosyalara verilmiş başlıklar seri hale getirmek ve bunları geri belleğe okumak için yöntem sağlar kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="88271-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="88271-231">Normal modu: Bu modda SCP eklentileri storm java işlemi tarafından başlatılır.</span><span class="sxs-lookup"><span data-stu-id="88271-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="88271-232">SCP eklentisi başlatmanın örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="88271-232">Here is an example of launching SCP plugin:</span></span>
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting the environment variable here can change the log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="88271-233">Topoloji belirtimi dili</span><span class="sxs-lookup"><span data-stu-id="88271-233">Topology Specification Language</span></span>
<span data-ttu-id="88271-234">SCP topoloji açıklayan ve SCP topolojileri yapılandırmak için etki alanı belirli bir dil belirtimidir.</span><span class="sxs-lookup"><span data-stu-id="88271-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="88271-235">Storm'ın Clojure DSL üzerinde temel alır (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) ve SCP tarafından genişletilir.</span><span class="sxs-lookup"><span data-stu-id="88271-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="88271-236">Topoloji belirtimleri yürütmenin storm kümesine doğrudan gönderilebilir ***runspec*** komutu.</span><span class="sxs-lookup"><span data-stu-id="88271-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span></span>

<span data-ttu-id="88271-237">SCP.NET sahip işlem topoloji tanımlamak için izleme işlevleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="88271-237">SCP.NET has add follow functions to define the Transactional Topology:</span></span>

| <span data-ttu-id="88271-238">**Yeni işlevleri**</span><span class="sxs-lookup"><span data-stu-id="88271-238">**New Functions**</span></span> | <span data-ttu-id="88271-239">**Parametreler**</span><span class="sxs-lookup"><span data-stu-id="88271-239">**Parameters**</span></span> | <span data-ttu-id="88271-240">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="88271-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88271-241">**Tx topolopy**</span><span class="sxs-lookup"><span data-stu-id="88271-241">**tx-topolopy**</span></span> |<span data-ttu-id="88271-242">Topoloji adı</span><span class="sxs-lookup"><span data-stu-id="88271-242">topology-name</span></span><br /><span data-ttu-id="88271-243">spout eşleme</span><span class="sxs-lookup"><span data-stu-id="88271-243">spout-map</span></span><br /><span data-ttu-id="88271-244">Cıvata eşleme</span><span class="sxs-lookup"><span data-stu-id="88271-244">bolt-map</span></span> |<span data-ttu-id="88271-245">Topoloji ada sahip bir işlem topolojisi tanımlayın &nbsp;tanımı harita ve Cıvatalar tanımı Haritası spout'lar</span><span class="sxs-lookup"><span data-stu-id="88271-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="88271-246">**SCP tx spout**</span><span class="sxs-lookup"><span data-stu-id="88271-246">**scp-tx-spout**</span></span> |<span data-ttu-id="88271-247">Exec adı</span><span class="sxs-lookup"><span data-stu-id="88271-247">exec-name</span></span><br /><span data-ttu-id="88271-248">bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="88271-248">args</span></span><br /><span data-ttu-id="88271-249">Alanları</span><span class="sxs-lookup"><span data-stu-id="88271-249">fields</span></span> |<span data-ttu-id="88271-250">İşlem spout tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="88271-250">Define a transactional spout.</span></span> <span data-ttu-id="88271-251">İle uygulamanın çalıştırılacağı ***exec adı*** kullanarak ***args***.</span><span class="sxs-lookup"><span data-stu-id="88271-251">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="88271-252">***Alanları*** spout çıktı alanları</span><span class="sxs-lookup"><span data-stu-id="88271-252">The ***fields*** is the Output Fields for spout</span></span> |
| <span data-ttu-id="88271-253">**tx toplu Cıvata SCP**</span><span class="sxs-lookup"><span data-stu-id="88271-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="88271-254">Exec adı</span><span class="sxs-lookup"><span data-stu-id="88271-254">exec-name</span></span><br /><span data-ttu-id="88271-255">bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="88271-255">args</span></span><br /><span data-ttu-id="88271-256">Alanları</span><span class="sxs-lookup"><span data-stu-id="88271-256">fields</span></span> |<span data-ttu-id="88271-257">Bir işlem toplu Cıvata tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="88271-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="88271-258">İle uygulamanın çalıştırılacağı ***exec adı*** kullanarak ***bağımsız değişken.***</span><span class="sxs-lookup"><span data-stu-id="88271-258">It will run the application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="88271-259">Alanlar Cıvata çıktı alanları modudur.</span><span class="sxs-lookup"><span data-stu-id="88271-259">The Fields is the Output Fields for bolt.</span></span> |
| <span data-ttu-id="88271-260">**SCP-tx-yürütme-Cıvata**</span><span class="sxs-lookup"><span data-stu-id="88271-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="88271-261">Exec adı</span><span class="sxs-lookup"><span data-stu-id="88271-261">exec-name</span></span><br /><span data-ttu-id="88271-262">bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="88271-262">args</span></span><br /><span data-ttu-id="88271-263">Alanları</span><span class="sxs-lookup"><span data-stu-id="88271-263">fields</span></span> |<span data-ttu-id="88271-264">Bir işlem Committer Cıvata tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="88271-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="88271-265">İle uygulamanın çalıştırılacağı ***exec adı*** kullanarak ***args***.</span><span class="sxs-lookup"><span data-stu-id="88271-265">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="88271-266">***Alanları*** Cıvata çıktı alanları</span><span class="sxs-lookup"><span data-stu-id="88271-266">The ***fields*** is the Output Fields for bolt</span></span> |
| <span data-ttu-id="88271-267">**nontx topolopy**</span><span class="sxs-lookup"><span data-stu-id="88271-267">**nontx-topolopy**</span></span> |<span data-ttu-id="88271-268">Topoloji adı</span><span class="sxs-lookup"><span data-stu-id="88271-268">topology-name</span></span><br /><span data-ttu-id="88271-269">spout eşleme</span><span class="sxs-lookup"><span data-stu-id="88271-269">spout-map</span></span><br /><span data-ttu-id="88271-270">Cıvata eşleme</span><span class="sxs-lookup"><span data-stu-id="88271-270">bolt-map</span></span> |<span data-ttu-id="88271-271">Topoloji ada sahip bir işlem topolojisi tanımlayın&nbsp; tanımı harita ve Cıvatalar tanımı Haritası spout'lar</span><span class="sxs-lookup"><span data-stu-id="88271-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="88271-272">**SCP spout**</span><span class="sxs-lookup"><span data-stu-id="88271-272">**scp-spout**</span></span> |<span data-ttu-id="88271-273">Exec adı</span><span class="sxs-lookup"><span data-stu-id="88271-273">exec-name</span></span><br /><span data-ttu-id="88271-274">bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="88271-274">args</span></span><br /><span data-ttu-id="88271-275">Alanları</span><span class="sxs-lookup"><span data-stu-id="88271-275">fields</span></span><br /><span data-ttu-id="88271-276">Parametreleri</span><span class="sxs-lookup"><span data-stu-id="88271-276">parameters</span></span> |<span data-ttu-id="88271-277">Bir işlem spout tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="88271-277">Define a nontransactional spout.</span></span> <span data-ttu-id="88271-278">İle uygulamanın çalıştırılacağı ***exec adı*** kullanarak ***args***.</span><span class="sxs-lookup"><span data-stu-id="88271-278">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="88271-279">***Alanları*** spout çıktı alanları</span><span class="sxs-lookup"><span data-stu-id="88271-279">The ***fields*** is the Output Fields for spout</span></span><br /><br /><span data-ttu-id="88271-280">***Parametreleri*** "nontransactional.ack.enabled" gibi bazı parametreler belirtmek için kullanmak isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="88271-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="88271-281">**SCP Cıvata**</span><span class="sxs-lookup"><span data-stu-id="88271-281">**scp-bolt**</span></span> |<span data-ttu-id="88271-282">Exec adı</span><span class="sxs-lookup"><span data-stu-id="88271-282">exec-name</span></span><br /><span data-ttu-id="88271-283">bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="88271-283">args</span></span><br /><span data-ttu-id="88271-284">Alanları</span><span class="sxs-lookup"><span data-stu-id="88271-284">fields</span></span><br /><span data-ttu-id="88271-285">Parametreleri</span><span class="sxs-lookup"><span data-stu-id="88271-285">parameters</span></span> |<span data-ttu-id="88271-286">İşlem dışı Cıvata tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="88271-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="88271-287">İle uygulamanın çalıştırılacağı ***exec adı*** kullanarak ***args***.</span><span class="sxs-lookup"><span data-stu-id="88271-287">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="88271-288">***Alanları*** Cıvata çıktı alanları</span><span class="sxs-lookup"><span data-stu-id="88271-288">The ***fields*** is the Output Fields for bolt</span></span><br /><br /><span data-ttu-id="88271-289">***Parametreleri*** "nontransactional.ack.enabled" gibi bazı parametreler belirtmek için kullanmak isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="88271-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="88271-290">SCP.NET sahip izleyin anahtarlar tanımlı sözcükleri:</span><span class="sxs-lookup"><span data-stu-id="88271-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="88271-291">**Anahtar sözcükler**</span><span class="sxs-lookup"><span data-stu-id="88271-291">**Key Words**</span></span> | <span data-ttu-id="88271-292">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="88271-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="88271-293">**: adı**</span><span class="sxs-lookup"><span data-stu-id="88271-293">**:name**</span></span> |<span data-ttu-id="88271-294">Topoloji adı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="88271-294">Define the Topology Name</span></span> |
| <span data-ttu-id="88271-295">**: topolojisi**</span><span class="sxs-lookup"><span data-stu-id="88271-295">**:topology**</span></span> |<span data-ttu-id="88271-296">Yukarıdaki işlevleri kullanarak topolojisi tanımlayın ve olanları içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88271-296">Define the Topology using the above functions and build in ones.</span></span> |
| <span data-ttu-id="88271-297">**: p**</span><span class="sxs-lookup"><span data-stu-id="88271-297">**:p**</span></span> |<span data-ttu-id="88271-298">Her spout veya Cıvata için paralellik ipucu tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="88271-298">Define the parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="88271-299">**: yapılandırma**</span><span class="sxs-lookup"><span data-stu-id="88271-299">**:config**</span></span> |<span data-ttu-id="88271-300">Tanımlamak parametresini yapılandırabilir veya var olanları güncelleştir</span><span class="sxs-lookup"><span data-stu-id="88271-300">Define configure parameter or update the existing ones</span></span> |
| <span data-ttu-id="88271-301">**: şeması**</span><span class="sxs-lookup"><span data-stu-id="88271-301">**:schema**</span></span> |<span data-ttu-id="88271-302">Akış şeması tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="88271-302">Define the Schema of Stream.</span></span> |

<span data-ttu-id="88271-303">Ve sık kullanılan parametreler:</span><span class="sxs-lookup"><span data-stu-id="88271-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="88271-304">**Parametre**</span><span class="sxs-lookup"><span data-stu-id="88271-304">**Parameter**</span></span> | <span data-ttu-id="88271-305">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="88271-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="88271-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="88271-306">**"plugin.name"**</span></span> |<span data-ttu-id="88271-307">C# eklentisi exe dosyası adı</span><span class="sxs-lookup"><span data-stu-id="88271-307">exe file name of the C# plugin</span></span> |
| <span data-ttu-id="88271-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="88271-308">**"plugin.args"**</span></span> |<span data-ttu-id="88271-309">Eklenti bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="88271-309">plugin args</span></span> |
| <span data-ttu-id="88271-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="88271-310">**"output.schema"**</span></span> |<span data-ttu-id="88271-311">Çıkış şeması</span><span class="sxs-lookup"><span data-stu-id="88271-311">Output schema</span></span> |
| <span data-ttu-id="88271-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="88271-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="88271-313">Ack işlem topolojisi için etkinleştirilip etkinleştirilmediği</span><span class="sxs-lookup"><span data-stu-id="88271-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="88271-314">Runspec komutu BITS ile birlikte dağıtılır, kullanım gibidir:</span><span class="sxs-lookup"><span data-stu-id="88271-314">The runspec command will be deployed together with the bits, the usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="88271-315">***Kaynak dir*** parametre isteğe bağlı, bir C takın istediğinizde belirtmek zorunda\# uygulama ve bu dizinde uygulama, bağımlılıklar ve yapılandırmaları içerecek.</span><span class="sxs-lookup"><span data-stu-id="88271-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span></span>

<span data-ttu-id="88271-316">***Sınıf*** parametredir Ayrıca isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="88271-316">The ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="88271-317">Java Spout veya Cıvata belirtim dosya içeriyorsa, Java sınıf belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="88271-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="88271-318">Çeşitli özellikler</span><span class="sxs-lookup"><span data-stu-id="88271-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="88271-319">Girdi ve çıktı şema bildirimi</span><span class="sxs-lookup"><span data-stu-id="88271-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="88271-320">Kullanıcı c tanımlama grubu yayma\# işlemi, platform gerekir Tanımlama grubu seri byte [], Java yan aktarım ve Storm bu tanımlama grubu hedeflerini transfer.</span><span class="sxs-lookup"><span data-stu-id="88271-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span></span> <span data-ttu-id="88271-321">Aşağı Akış bileşeni, C, bu sırada\# işlemi geri java taraftan tanımlama grubu alır ve platforma göre özgün türlerine dönüştürmek, bu işlemlerin Platform tarafından gizlenir.</span><span class="sxs-lookup"><span data-stu-id="88271-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span></span>

<span data-ttu-id="88271-322">Seri hale getirme ve seri durumdan çıkarma desteklemesi, kullanıcı kodu girişleri ve çıkışları şeması bildirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="88271-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span></span>

<span data-ttu-id="88271-323">Giriş/Çıkış akış şeması bir sözlük olarak tanımlanır, anahtar StreamId ve sütunların türlerini değerdir.</span><span class="sxs-lookup"><span data-stu-id="88271-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span></span> <span data-ttu-id="88271-324">Bileşen bildirilen çok akışları sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="88271-324">The component can have multi-streams declared.</span></span>

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


<span data-ttu-id="88271-325">Bağlam nesnesinde eklenen aşağıdaki API vardır:</span><span class="sxs-lookup"><span data-stu-id="88271-325">In Context object, we have the following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="88271-326">Kullanıcı kodu yayılan diziler için bu akış tanımlanan şemaya uyacak ya da sistem çalışma zamanı özel durum atar emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="88271-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="88271-327">Birden çok akış desteği</span><span class="sxs-lookup"><span data-stu-id="88271-327">Multi-Stream Support</span></span>
<span data-ttu-id="88271-328">SCP yayma veya aynı anda birden çok ayrı akışlardan almak için kullanıcı kodu destekler.</span><span class="sxs-lookup"><span data-stu-id="88271-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span></span> <span data-ttu-id="88271-329">Emit yöntemi bir isteğe bağlı Akış ID parametresi yararlanırken destek bağlamı nesnesinde yansıtır.</span><span class="sxs-lookup"><span data-stu-id="88271-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="88271-330">SCP.NET bağlamı nesnesindeki iki yöntemler eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="88271-330">Two methods in the SCP.NET Context object have been added.</span></span> <span data-ttu-id="88271-331">Tanımlama grubu ya da diziler StreamId belirtmek için yaymak üzere kullanılır.</span><span class="sxs-lookup"><span data-stu-id="88271-331">They are used to emit Tuple or Tuples to specify StreamId.</span></span> <span data-ttu-id="88271-332">StreamId bir dize ve her iki C'de tutarlı olması gerekiyor\# ve topoloji tanımı belirtimi.</span><span class="sxs-lookup"><span data-stu-id="88271-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span></span>

        /* Emit tuple to the specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="88271-333">Var olmayan bir akış yayma çalışma zamanı özel durumları neden olur.</span><span class="sxs-lookup"><span data-stu-id="88271-333">The emitting to a non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="88271-334">Alanları gruplandırma</span><span class="sxs-lookup"><span data-stu-id="88271-334">Fields Grouping</span></span>
<span data-ttu-id="88271-335">Yapı içinde alanları gruplandırma Strom SCP.NET içinde düzgün çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="88271-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="88271-336">Java Proxy tarafında tüm alanlar veri türleri: gerçekte byte [] ve gruplandırma alanları gruplandırma gerçekleştirmek için byte [] nesnesi karma kodu kullanır.</span><span class="sxs-lookup"><span data-stu-id="88271-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span></span> <span data-ttu-id="88271-337">Byte [] nesnesi karma kodu, bu nesnenin bellekte adresidir.</span><span class="sxs-lookup"><span data-stu-id="88271-337">The byte[] object hash code is the address of this object in memory.</span></span> <span data-ttu-id="88271-338">Bu nedenle gruplandırma aynı içerik ancak aynı adresini paylaşan iki byte [] nesneler için yanlış olur.</span><span class="sxs-lookup"><span data-stu-id="88271-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span></span>

<span data-ttu-id="88271-339">Özelleştirilmiş gruplandırma yöntemi SCP.NET ekler ve gruplandırma yapmak için byte [] içeriğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="88271-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span></span> <span data-ttu-id="88271-340">İçinde **SPEC** gibi dosya, söz dizimi:</span><span class="sxs-lookup"><span data-stu-id="88271-340">In **SPEC** file, the syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="88271-341">Burada,</span><span class="sxs-lookup"><span data-stu-id="88271-341">Here,</span></span>

1. <span data-ttu-id="88271-342">"scp alan grup", "SCP tarafından uygulanan özelleştirilmiş alan gruplandırma" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="88271-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="88271-343">": tx"veya": tx olmayan" işlem topoloji olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="88271-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="88271-344">Başlangıç dizini tx olmayan topolojileri tx farklı olduğundan bu bilgileri ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="88271-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="88271-345">[0,1] anlamına alan kimlikleri, 0'dan başlayarak izleri hashset'i.</span><span class="sxs-lookup"><span data-stu-id="88271-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="88271-346">Karma topolojisi</span><span class="sxs-lookup"><span data-stu-id="88271-346">Hybrid topology</span></span>
<span data-ttu-id="88271-347">Yerel Storm Java yazılır.</span><span class="sxs-lookup"><span data-stu-id="88271-347">The native Storm is written in Java.</span></span> <span data-ttu-id="88271-348">SCP.Net C yazmak bizim Gümrük etkinleştirmek için Gelişmiş ve\# kendi iş mantığı işlemek için kod.</span><span class="sxs-lookup"><span data-stu-id="88271-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span></span> <span data-ttu-id="88271-349">Ancak aynı zamanda karma topolojiler yalnızca C içeren destekliyoruz\# spout'lar/Cıvatalar, aynı zamanda Java Spout/Cıvatalar.</span><span class="sxs-lookup"><span data-stu-id="88271-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="88271-350">Java Spout/Cıvata belirtim dosyasında belirtin</span><span class="sxs-lookup"><span data-stu-id="88271-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="88271-351">Belirtim dosyasındaki "scp-spout" ve "scp-Cıvata" de Java Spout'lar ve Cıvatalar belirtmek için kullanılabilir, örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="88271-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="88271-352">Burada `microsoft.scp.example.HybridTopology.Generator` Java Spout sınıfı adı.</span><span class="sxs-lookup"><span data-stu-id="88271-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="88271-353">Java sınıf runSpec komutunu belirtin</span><span class="sxs-lookup"><span data-stu-id="88271-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="88271-354">Java Spout'lar veya Cıvatalar içeren topoloji göndermek istiyorsanız, önce Java Spout'lar veya Cıvatalar derlemek ve Jar dosyalarını almak gerekir.</span><span class="sxs-lookup"><span data-stu-id="88271-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span></span> <span data-ttu-id="88271-355">Ardından topoloji gönderirken Jar dosyalarını içeren java sınıf belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="88271-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span></span> <span data-ttu-id="88271-356">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="88271-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="88271-357">Burada **örnekler\\HybridTopology\\java\\hedef\\**  Spout/Cıvata Java Jar dosyasını içeren klasör.</span><span class="sxs-lookup"><span data-stu-id="88271-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="88271-358">Seri hale getirme ve seri durumdan çıkarma Java ve C\ arasında</span><span class="sxs-lookup"><span data-stu-id="88271-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="88271-359">Java yan ve C bizim SCP bileşeni içerir\# yan.</span><span class="sxs-lookup"><span data-stu-id="88271-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="88271-360">Yerel Java Spout'lar/Cıvatalar ile etkileşim kurmak için serileştirme/seri durumdan çıkarma Java yan ve C uygulanması gereken\# , aşağıdaki grafikte gösterildiği gibi tarafı.</span><span class="sxs-lookup"><span data-stu-id="88271-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span></span>

![Java bileşenine gönderme SCP bileşen gönderme java bileşeni diyagramı](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="88271-362">**Seri hale getirme Java yan ve seri durumdan çıkarma c\# yan**</span><span class="sxs-lookup"><span data-stu-id="88271-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="88271-363">Java taraf serileştirme ve seri durumundan çıkarma c için varsayılan uygulaması ilk sağladığımız\# yan.</span><span class="sxs-lookup"><span data-stu-id="88271-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="88271-364">Java yan serileştirme yönteminde belirtim dosyasında belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="88271-364">The serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="88271-365">Seri durumdan çıkarma yöntemini c\# yan C'de belirtilmelidir\# kullanıcı kodu:</span><span class="sxs-lookup"><span data-stu-id="88271-365">The deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="88271-366">Veri türü çok karmaşık değilse, çoğu durumda bu varsayılan uygulama işlemelidir.</span><span class="sxs-lookup"><span data-stu-id="88271-366">This default implementation should handle most cases if the data type is not too complex.</span></span> <span data-ttu-id="88271-367">Belirli durumlarda, kullanıcı veri türü çok karmaşık olduğu için veya bizim varsayılan uygulama performansını kendi uygulama kullanıcının gereksinim, kullanıcı can eklenti karşılamadığından.</span><span class="sxs-lookup"><span data-stu-id="88271-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="88271-368">Java yan serileştirme arabiriminde olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="88271-368">The serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="88271-369">C deserialize arabiriminde\# yan olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="88271-369">The deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="88271-370">Ortak arabirimi ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="88271-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="88271-371">**Seri hale getirme c\# yan ve Java yan yana çıkarma**</span><span class="sxs-lookup"><span data-stu-id="88271-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="88271-372">C serileştirme yönteminde\# yan C'de belirtilmelidir\# kullanıcı kodu:</span><span class="sxs-lookup"><span data-stu-id="88271-372">The serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="88271-373">Java taraf seri durumdan çıkarma yöntemini belirtim dosyasında belirtilen:</span><span class="sxs-lookup"><span data-stu-id="88271-373">The Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="88271-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="88271-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="88271-375">Burada "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" seri durumdan Çıkarıcının adını, ve "microsoft.scp.example.HybridTopology.Person" için hedef sınıf veri serisi.</span><span class="sxs-lookup"><span data-stu-id="88271-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span></span>
   
   <span data-ttu-id="88271-376">Kullanıcı ayrıca eklenti yapabilir, kendi uygulama c\# seri hale getirici ve Java seri durumdan Çıkarıcının.</span><span class="sxs-lookup"><span data-stu-id="88271-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="88271-377">Bu C arabirimidir\# seri hale getirici:</span><span class="sxs-lookup"><span data-stu-id="88271-377">This is the interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="88271-378">Bu Java kaldırıcı arabirimidir:</span><span class="sxs-lookup"><span data-stu-id="88271-378">This is the interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="88271-379">SCP ana mod</span><span class="sxs-lookup"><span data-stu-id="88271-379">SCP Host Mode</span></span>
<span data-ttu-id="88271-380">Bu modda, kullanıcı kodlarına dll derleyin ve SCP tarafından sağlanan SCPHost.exe topoloji göndermek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="88271-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span></span> <span data-ttu-id="88271-381">Belirtim dosyası şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="88271-381">The spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="88271-382">Burada, `plugin.name` olarak belirtilen `SCPHost.exe` SCP SDK'sı tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="88271-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="88271-383">Tam olarak üç parametre kabul eden SCPHost.exe:</span><span class="sxs-lookup"><span data-stu-id="88271-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="88271-384">İlk olan DLL adıdır `"HelloWorld.dll"` Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="88271-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="88271-385">İkincisi olan sınıf adı olduğu `"Scp.App.HelloWorld.Generator"` Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="88271-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="88271-386">Üçüncü bir ISCPPlugin örneğini almak üzere çağrılabilen genel bir statik yöntem adıdır.</span><span class="sxs-lookup"><span data-stu-id="88271-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span></span>

<span data-ttu-id="88271-387">Ana mod, kullanıcı kodu DLL olarak derlenmiş ve SCP platformu tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="88271-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="88271-388">Bu nedenle SCP platform tüm işlem mantığının tam denetim elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88271-388">So SCP platform can get full control of the whole processing logic.</span></span> <span data-ttu-id="88271-389">Bu nedenle geliştirme deneyimi kolaylaştırmak ve bize de sonraki sürüm için daha fazla esneklik ve daha iyi geriye dönük uyumluluk Getir SCP ana mod topolojisinde göndermek için müşterilerimizin öneririz.</span><span class="sxs-lookup"><span data-stu-id="88271-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="88271-390">SCP programlama örnekleri</span><span class="sxs-lookup"><span data-stu-id="88271-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="88271-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="88271-391">HelloWorld</span></span>
<span data-ttu-id="88271-392">**HelloWorld** SCP.Net bakış göstermek için çok basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="88271-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span></span> <span data-ttu-id="88271-393">Adlı bir spout ile bir işlemsel olmayan topolojisi kullanır **Oluşturucu**ve adlı iki Cıvatalar **Bölümlendirici** ve **sayaç**.</span><span class="sxs-lookup"><span data-stu-id="88271-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="88271-394">Spout **Oluşturucu** rastgele bazı cümleleri oluşturur ve bu cümleleri yayma **Bölümlendirici**.</span><span class="sxs-lookup"><span data-stu-id="88271-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span></span> <span data-ttu-id="88271-395">Cıvata **Bölümlendirici** cümlelere sözcük bölme ve bu sözcükleri yayma **sayaç** Cıvata.</span><span class="sxs-lookup"><span data-stu-id="88271-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span></span> <span data-ttu-id="88271-396">Her sözcüğün oluşum sayısı kaydetmek için bir sözlük "sayacı" Cıvata kullanır.</span><span class="sxs-lookup"><span data-stu-id="88271-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span></span>

<span data-ttu-id="88271-397">İki belirtim dosya **HelloWorld.spec** ve **HelloWorld\_EnableAck.spec** Bu örnek için.</span><span class="sxs-lookup"><span data-stu-id="88271-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="88271-398">C\# kodu, onu bulabilir ack Java taraftan pluginConf alarak etkinleştirilip etkinleştirilmediği çıkışı.</span><span class="sxs-lookup"><span data-stu-id="88271-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span></span>

    /* demo how to get pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="88271-399">ACK etkinleştirilirse, spout içinde bir sözlük acked edilmemiş başlıklar önbelleğe almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="88271-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span></span> <span data-ttu-id="88271-400">Fail() çağrılırsa, başarısız tanımlama grubu yeniden:</span><span class="sxs-lookup"><span data-stu-id="88271-400">If Fail() is called, the failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get the cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay the failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="88271-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="88271-401">HelloWorldTx</span></span>
<span data-ttu-id="88271-402">**HelloWorldTx** örnek nasıl işlem topoloji uygulanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="88271-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span></span> <span data-ttu-id="88271-403">Adlı bir spout sahip **Oluşturucu**, bir toplu Cıvatalar adlı **kısmi-count**, ve bir yürütme Cıvata adlı **sayısı toplam**.</span><span class="sxs-lookup"><span data-stu-id="88271-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="88271-404">Ayrıca üç önceden oluşturulmuş txt dosyaları vardır: **DataSource0.txt**, **DataSource1.txt** ve **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="88271-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="88271-405">Spout her işlemde **Oluşturucu** rastgele iki dosya önceden oluşturulmuş üç dosyaları seçin ve iki dosya adlarına yayma **kısmi-count** Cıvata.</span><span class="sxs-lookup"><span data-stu-id="88271-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span></span> <span data-ttu-id="88271-406">Cıvata **kısmi-count** ilk alınan tanımlama grubundan dosya adı alınmaya sonra dosyasını açın ve bu dosyayı sözcükleri sayar ve son olarak word numarasına yayma **sayısı toplam** Cıvata.</span><span class="sxs-lookup"><span data-stu-id="88271-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span></span> <span data-ttu-id="88271-407">**Sayısı toplam** Cıvata toplam sayı bu sayıyı özetlemek.</span><span class="sxs-lookup"><span data-stu-id="88271-407">The **count-sum** bolt will summarize the total count.</span></span>

<span data-ttu-id="88271-408">Elde etmek için **tam olarak bir kez** semantiği, yürütme Cıvata **sayısı toplam** yeniden yürütülmüş bir işlem olup olmadığını değerlendirmek için gerekir.</span><span class="sxs-lookup"><span data-stu-id="88271-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span></span> <span data-ttu-id="88271-409">Bu örnekte, bir statik üye değişkeni vardır:</span><span class="sxs-lookup"><span data-stu-id="88271-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="88271-410">ISCPBatchBolt örneği oluşturulduğunda, get `txAttempt` Giriş parametrelerinden:</span><span class="sxs-lookup"><span data-stu-id="88271-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from the input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

<span data-ttu-id="88271-411">Zaman `FinishBatch()` olarak adlandırılır, `lastCommittedTxId` yeniden yürütülmüş bir işlem değilse güncelleştirme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="88271-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update the toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="88271-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="88271-412">HybridTopology</span></span>
<span data-ttu-id="88271-413">Bu topoloji Spout Java ve C içeren\# Cıvata.</span><span class="sxs-lookup"><span data-stu-id="88271-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="88271-414">SCP platform tarafından sağlanan varsayılan seri hale getirme ve seri durumdan çıkarma uygulaması kullanır.</span><span class="sxs-lookup"><span data-stu-id="88271-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="88271-415">Ref lütfen **HybridTopology.spec** içinde **örnekler\\HybridTopology** belirtim dosya ayrıntıları için klasör ve **SubmitTopology.bat** için belirtme Java sınıf.</span><span class="sxs-lookup"><span data-stu-id="88271-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="88271-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="88271-416">SCPHostDemo</span></span>
<span data-ttu-id="88271-417">Bu örnek HelloWorld temelde aynıdır.</span><span class="sxs-lookup"><span data-stu-id="88271-417">This example is the same as HelloWorld in essence.</span></span> <span data-ttu-id="88271-418">Tek fark, kullanıcı kodu DLL olarak derlenir ve topoloji SCPHost.exe kullanılarak gönderilen olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="88271-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="88271-419">Ref bölüm "SCP ana modu" daha ayrıntılı açıklaması için lütfen.</span><span class="sxs-lookup"><span data-stu-id="88271-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88271-420">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="88271-420">Next Steps</span></span>
<span data-ttu-id="88271-421">Storm topolojilerini SCP kullanılarak oluşturulan bir örnekleri için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="88271-421">For examples of Storm topologies created using SCP, see the following:</span></span>

* [<span data-ttu-id="88271-422">Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="88271-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="88271-423">Hdınsight üzerinde Storm ile Azure Event hubs'tan işlem olayları</span><span class="sxs-lookup"><span data-stu-id="88271-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="88271-424">Bir C# Storm topolojisinde birden çok veri akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="88271-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="88271-425">Bir Storm topolojisinin verilerini görselleştirmek için Power BI kullanın</span><span class="sxs-lookup"><span data-stu-id="88271-425">Use Power Bi to visualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="88271-426">Event Hubs Hdınsight üzerinde Storm kullanmaya aracın algılayıcı verilerini işlemek</span><span class="sxs-lookup"><span data-stu-id="88271-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="88271-427">Ayıklama, dönüştürme ve HBase için Azure olay hub'larından (ETL) yükleme</span><span class="sxs-lookup"><span data-stu-id="88271-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="88271-428">Hdınsight üzerinde Storm ve HBase kullanarak olayları ilişkilendirmenize</span><span class="sxs-lookup"><span data-stu-id="88271-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)


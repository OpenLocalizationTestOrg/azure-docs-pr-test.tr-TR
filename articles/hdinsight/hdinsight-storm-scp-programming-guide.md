---
title: "aaaSCP.NET Programlama Kılavuzu | Microsoft Docs"
description: "Bilgi nasıl toouse SCP.NET toocreate. Hdınsight üzerinde Storm ile NET tabanlı Storm Topolojileri için kullanın."
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
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="b21d4-103">SCP Programlama Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="b21d4-103">SCP programming guide</span></span>
<span data-ttu-id="b21d4-104">SCP platform toobuild gerçek zamanlı, güvenilir, tutarlı ve yüksek performans veri işleme uygulama olur.</span><span class="sxs-lookup"><span data-stu-id="b21d4-104">SCP is a platform toobuild real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="b21d4-105">Üstünde oluşturulmuş [Apache Storm](http://storm.incubator.apache.org/) --bir akış hello OSS topluluğu tarafından tasarlanmış sistemi işleme.</span><span class="sxs-lookup"><span data-stu-id="b21d4-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by hello OSS communities.</span></span> <span data-ttu-id="b21d4-106">Storm Nathan Marz ve açık kaynaklıdır Twitter tarafından tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="b21d4-107">Bunu yararlanır [Apache ZooKeeper](http://zookeeper.apache.org/), başka bir Apache proje tooenable yüksek oranda güvenilir dağıtılmış koordinasyonu ve durum yönetimi.</span><span class="sxs-lookup"><span data-stu-id="b21d4-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project tooenable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="b21d4-108">Yalnızca Windows üzerinde Storm hello SCP proje bağlantı noktası kurulmuş ancak hello proje uzantıları ve özelleştirme hello Windows ekosistemi için de eklenir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-108">Not only hello SCP project ported Storm on Windows but also hello project added extensions and customization for hello Windows ecosystem.</span></span> <span data-ttu-id="b21d4-109">Merhaba uzantıları .NET geliştirme deneyimi ve kitaplıklarını içerir, Windows tabanlı bir dağıtım hello özelleştirme içerir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-109">hello extensions include .NET developer experience, and libraries, hello customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="b21d4-110">Merhaba genişletme ve özelleştirme toofork hello OSS projeleri gerekmez ve Storm üstünde oluşturulmuş türetilmiş ekosistemlerini yararlanan bir şekilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-110">hello extension and customization is done in such a way that we do not need toofork hello OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="b21d4-111">İşlem modeli</span><span class="sxs-lookup"><span data-stu-id="b21d4-111">Processing model</span></span>
<span data-ttu-id="b21d4-112">SCP Hello verilerde diziler sürekli akışları olarak modellenir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-112">hello data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="b21d4-113">Genellikle hello diziler bazı sıraya ilk akış sonra toplanmış ve içindeki bir Storm topolojisinin barındırılan iş mantığı tarafından dönüştürülen, son olarak hello çıktı diziler tooanother SCP sistem olarak yöneltilen veya kaydedilmiş toostores olması ister dağıtılmış dosya sistemi veya SQL Server veritabanları gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-113">Typically hello tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally hello output could be piped as tuples tooanother SCP system, or be committed toostores like distributed file system or databases like SQL Server.</span></span>

![Bir veri deposu akışları veri tooprocessing besleme bir sıra diyagramı](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="b21d4-115">Storm bir uygulama topolojisi hesaplama grafiği tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b21d4-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="b21d4-116">Veri akışı düğümler arasındaki bağlantıları gösterir ve her düğüm topolojisinde işleme mantığı içerir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="b21d4-117">Merhaba düğümleri tooinject giriş verilerini hello topoloji kullanılan toosequence hello veriler olabilir Spout'lar denir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-117">hello nodes tooinject input data into hello topology are called Spouts, which can be used toosequence hello data.</span></span> <span data-ttu-id="b21d4-118">Merhaba giriş verilerinin bulunduğu dosya günlükleri, işlemsel veritabanı, sistem performans sayacı gerçek verileri filtreleme hello Cıvatalar ve seçimleri ve toplama hem girdi ve çıktı veri akışları ile vb. hello düğüm olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-118">hello input data could reside in file logs, transactional database, system performance counter etc. hello nodes with both input and output data flows are called Bolts, which do hello actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="b21d4-119">SCP en iyi çaba, en az bir kere destekler ve tam olarak-kez veri işleme.</span><span class="sxs-lookup"><span data-stu-id="b21d4-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="b21d4-120">Bir dağıtılmış akış işleme uygulamasında, Ağ kaybı, makine hatasını ya da kullanıcı kodu hatası vb. gibi veri işleme sırasında çeşitli hatalar oluşabilir. En az bir kere işleme sağlar tüm veriler işlenir hata oluştuğunda en az bir kez otomatik olarak yeniden oynatmak tarafından aynı veri hello.</span><span class="sxs-lookup"><span data-stu-id="b21d4-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically hello same data when error happens.</span></span> <span data-ttu-id="b21d4-121">En az bir kere işleme basit ve güvenilir olduğunu ve iyi birçok uygulamada uygun.</span><span class="sxs-lookup"><span data-stu-id="b21d4-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="b21d4-122">Merhaba uygulaması tam sayım gerektirdiğinde hello aynı veri olası hello uygulama topolojisinde yürütülebilir beri ancak, örneğin, en az bir kere işleme yeterli değil.</span><span class="sxs-lookup"><span data-stu-id="b21d4-122">However, when hello application requires exact counting, for example, at-least-once processing is insufficient since hello same data could potentially be played in hello application topology.</span></span> <span data-ttu-id="b21d4-123">Bu durumda, tam olarak-işleme tasarlanmış sonra bile hello veri yeniden ve birden çok kez işlenen toomake emin hello sonuç doğru olur.</span><span class="sxs-lookup"><span data-stu-id="b21d4-123">In that case, exactly-once processing is designed toomake sure hello result is correct even when hello data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="b21d4-124">Dengeleme hello Java sanal makine (JVM) Storm hello kapak altında tabanlı SCP .NET geliştiricilerinin toodevelop gerçek zamanlı veri işlem uygulamalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="b21d4-124">SCP enables .NET developers toodevelop real time data process applications while leverage hello Java Virtual Machine (JVM) based Storm under hello cover.</span></span> <span data-ttu-id="b21d4-125">Merhaba .NET ve JVM TCP yerel yuva iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="b21d4-125">hello .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="b21d4-126">Neredeyse her Spout/Cıvata bir .net/Java işlemi, hello kullanıcı mantığını .net işlem bir eklenti olarak çalıştığı çiftidir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-126">Basically each Spout/Bolt is a .Net/Java process pair, where hello user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="b21d4-127">toobuild işleme uygulaması SCP en üstünde bir veri birkaç adım gereklidir:</span><span class="sxs-lookup"><span data-stu-id="b21d4-127">toobuild a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="b21d4-128">Tasarlayıp hello Spout'lar toopull veri sırasından.</span><span class="sxs-lookup"><span data-stu-id="b21d4-128">Design and implement hello Spouts toopull in data from queue.</span></span>
* <span data-ttu-id="b21d4-129">Tasarım ve Cıvatalar tooprocess hello giriş verisi uygulamak ve veri tooexternal depoları veritabanı gibi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b21d4-129">Design and implement Bolts tooprocess hello input data, and save data tooexternal stores such as Database.</span></span>
* <span data-ttu-id="b21d4-130">Merhaba topolojisi tasarım, gönderme ve hello topoloji çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-130">Design hello topology, then submit and run hello topology.</span></span> <span data-ttu-id="b21d4-131">Merhaba topoloji köşeleri ve hello verileri tanımlayan akışları hello köşeleri arasında.</span><span class="sxs-lookup"><span data-stu-id="b21d4-131">hello topology defines vertexes and hello data flows between hello vertexes.</span></span> <span data-ttu-id="b21d4-132">SCP hello topoloji belirtimi alın ve her köşe mantıksal bir düğüm üzerinde çalıştığı bir Storm kümede dağıtın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-132">SCP will take hello topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="b21d4-133">Merhaba yük devretme ve ölçeklendirme hello Storm Görev Zamanlayıcı'yı dikkate.</span><span class="sxs-lookup"><span data-stu-id="b21d4-133">hello failover and scaling will be taken care of by hello Storm task scheduler.</span></span>

<span data-ttu-id="b21d4-134">Bu belgede bazı basit örnekler toowalk nasıl kullanacağınız toobuild veri işleme uygulama SCP ile.</span><span class="sxs-lookup"><span data-stu-id="b21d4-134">This document will use some simple examples toowalk through how toobuild data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="b21d4-135">SCP eklentisi arabirimi</span><span class="sxs-lookup"><span data-stu-id="b21d4-135">SCP Plugin Interface</span></span>
<span data-ttu-id="b21d4-136">SCP eklentileri (veya uygulamalar) hem de Visual Studio içinde hello geliştirme aşamasında çalışabilen ve üretim dağıtım sonrasında hello Storm ardışık düzenine takılı tek başına exe markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during hello development phase, and be plugged into hello Storm pipeline after deployment in production.</span></span> <span data-ttu-id="b21d4-137">Merhaba SCP eklenti yazma olduğundan yalnızca hello diğer standart Windows konsol uygulamaları yazma aynıdır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-137">Writing hello SCP plugin is just hello same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="b21d4-138">Spout/Cıvata için bazı arabirimi SCP.NET platform bildirir ve hello kullanıcı eklentisi kodu bu arabirimi uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-138">SCP.NET platform declares some interface for spout/bolt, and hello user plugin code should implement these interfaces.</span></span> <span data-ttu-id="b21d4-139">Bu tasarım ana amacı Hello hello kullanıcı kendi iş logics ve SCP.NET platformu tarafından işlenen diğer şeyleri toobe bırakarak odaklanabilirsiniz..</span><span class="sxs-lookup"><span data-stu-id="b21d4-139">hello main purpose of this design is that hello user can focus on their own business logics, and leaving other things toobe handled by SCP.NET platform.</span></span>

<span data-ttu-id="b21d4-140">Merhaba kullanıcı eklentisi kodu hello aşağıdakilere arabirimlerinden biri, uygulamalıdır, hello topoloji işlem ya da işlem dışı olmasına ve hello bileşen spout veya Cıvata olmasına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-140">hello user plugin code should implement one of hello followings interfaces, depends on whether hello topology is transactional or non-transactional, and whether hello component is spout or bolt.</span></span>

* <span data-ttu-id="b21d4-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="b21d4-141">ISCPSpout</span></span>
* <span data-ttu-id="b21d4-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="b21d4-142">ISCPBolt</span></span>
* <span data-ttu-id="b21d4-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="b21d4-143">ISCPTxSpout</span></span>
* <span data-ttu-id="b21d4-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="b21d4-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="b21d4-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="b21d4-145">ISCPPlugin</span></span>
<span data-ttu-id="b21d4-146">ISCPPlugin hello ortak eklenti her türlü arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-146">ISCPPlugin is hello common interface for all kinds of plugins.</span></span> <span data-ttu-id="b21d4-147">Şu anda, onu bir kukla arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="b21d4-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="b21d4-148">ISCPSpout</span></span>
<span data-ttu-id="b21d4-149">ISCPSpout, işlemsel olmayan spout hello arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-149">ISCPSpout is hello interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="b21d4-150">Zaman `NextTuple()` çağrıldığında hello C\# kullanıcı kodu bir veya daha fazla tanımlama grubu yayma.</span><span class="sxs-lookup"><span data-stu-id="b21d4-150">When `NextTuple()` is called, hello C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="b21d4-151">Yoksa hiçbir şey tooemit, bu yöntem döndürmelidir herhangi bir şey yayma olmadan.</span><span class="sxs-lookup"><span data-stu-id="b21d4-151">If there is nothing tooemit, this method should return without emitting anything.</span></span> <span data-ttu-id="b21d4-152">Dikkat edilmesi gereken, `NextTuple()`, `Ack()`, ve `Fail()` tümü tek bir iş parçacığı c sıkı döngü denir\# işlemi.</span><span class="sxs-lookup"><span data-stu-id="b21d4-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="b21d4-153">Diziler tooemit olduğunda, kısa bir süre için (10 milisaniye gibi) değil toowaste olarak nedenle çok fazla CPU courteous toohave NextTuple uyku olduğu.</span><span class="sxs-lookup"><span data-stu-id="b21d4-153">When there are no tuples tooemit, it is courteous toohave NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="b21d4-154">`Ack()`ve `Fail()` ack mekanizması belirtim dosyasında yalnızca etkin olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="b21d4-155">Merhaba `seqId` acked veya başarısız kullanılan tooidentify hello tanımlama grubu değil.</span><span class="sxs-lookup"><span data-stu-id="b21d4-155">hello `seqId` is used tooidentify hello tuple which is acked or failed.</span></span> <span data-ttu-id="b21d4-156">Bu nedenle ACK işlemsel olmayan topolojisinde etkinleştirilirse, emit işlevi aşağıdaki hello içinde Spout kullanılmalıdır:</span><span class="sxs-lookup"><span data-stu-id="b21d4-156">So if ack is enabled in non-transactional topology, hello following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="b21d4-157">ACK işlemsel olmayan topolojisinde desteklenmiyorsa hello `Ack()` ve `Fail()` boş işlev olarak bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-157">If ack is not supported in non-transactional topology, hello `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="b21d4-158">Merhaba `parms` bu işlevler giriş parametrelerinde yalnızca boş sözlük, gelecekte kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-158">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="b21d4-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="b21d4-159">ISCPBolt</span></span>
<span data-ttu-id="b21d4-160">ISCPBolt, işlemsel olmayan Cıvata hello arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-160">ISCPBolt is hello interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="b21d4-161">Yeni tanımlama grubu kullanılabilir olduğunda, hello `Execute()` işlevi tooprocess çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-161">When new tuple is available, hello `Execute()` function will be called tooprocess it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="b21d4-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="b21d4-162">ISCPTxSpout</span></span>
<span data-ttu-id="b21d4-163">ISCPTxSpout, işlem spout hello arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-163">ISCPTxSpout is hello interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="b21d4-164">İşlem olmayan karşı erişmelerini'olduğu gibi `NextTx()`, `Ack()`, ve `Fail()` tümü tek bir iş parçacığı c sıkı döngü denir\# işlemi.</span><span class="sxs-lookup"><span data-stu-id="b21d4-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="b21d4-165">Hiçbir veri tooemit olduğunda courteous toohave olan `NextTx` kısa bir süre (10 milisaniye) için çok fazla CPU değil toowaste olarak nedenle uyku.</span><span class="sxs-lookup"><span data-stu-id="b21d4-165">When there are no data tooemit, it is courteous toohave `NextTx` sleep for a short amount of time (10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="b21d4-166">`NextTx()`Yeni bir işlem toostart hello out parametresi olarak adlandırılır `seqId` ayrıca kullanılır kullanılan tooidentify hello işlem `Ack()` ve `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="b21d4-166">`NextTx()` is called toostart a new transaction, hello out parameter `seqId` is used tooidentify hello transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="b21d4-167">İçinde `NextTx()`, kullanıcı veri tooJava yan yayma.</span><span class="sxs-lookup"><span data-stu-id="b21d4-167">In `NextTx()`, user can emit data tooJava side.</span></span> <span data-ttu-id="b21d4-168">Merhaba veri ZooKeeper toosupport yeniden yürütme içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-168">hello data will be stored in ZooKeeper toosupport replay.</span></span> <span data-ttu-id="b21d4-169">ZooKeeper Hello kapasitesi sınırlı olduğundan, kullanıcı yalnızca meta veri, toplu veri işlem spout içinde değil yayması.</span><span class="sxs-lookup"><span data-stu-id="b21d4-169">Because hello capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="b21d4-170">Storm yeniden yürütme bir işlem otomatik olarak başarısız olursa, bunu `Fail()` normal durumda çağrılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="b21d4-171">Ancak SCP işlem spout'un yayılan hello meta verileri işaretlerseniz çağırabilirsiniz `Fail()` hello meta veri olduğunda geçersiz.</span><span class="sxs-lookup"><span data-stu-id="b21d4-171">But if SCP can check hello metadata emitted by transactional spout, it can call `Fail()` when hello metadata is invalid.</span></span>

<span data-ttu-id="b21d4-172">Merhaba `parms` bu işlevler giriş parametrelerinde yalnızca boş sözlük, gelecekte kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-172">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="b21d4-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="b21d4-173">ISCPBatchBolt</span></span>
<span data-ttu-id="b21d4-174">ISCPBatchBolt, işlem Cıvata hello arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-174">ISCPBatchBolt is hello interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="b21d4-175">`Execute()`Yeni tanımlama grubu hello Cıvata ulaşan olduğunda çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-175">`Execute()` is called when there is new tuple arriving at hello bolt.</span></span> <span data-ttu-id="b21d4-176">`FinishBatch()`Bu işlem sona erdikten sonra çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="b21d4-177">Merhaba `parms` giriş parametresi, gelecekte kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-177">hello `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="b21d4-178">İşlem topolojisi için önemli bir kavram – olduğundan `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="b21d4-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="b21d4-179">İki alanı olan `TxId` ve `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="b21d4-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="b21d4-180">`TxId`kullanılan tooidentify belirli bir işlemdir ve belirli bir işlem için birden çok deneme hello işlem başarısız olur ve durumunda olabilir yeniden.</span><span class="sxs-lookup"><span data-stu-id="b21d4-180">`TxId` is used tooidentify a specific transaction, and for a given transaction, there may be multiple attempt if hello transaction fails and is replayed.</span></span> <span data-ttu-id="b21d4-181">SCP.NET olacak yeni bir farklı ISCPBatchBolt nesne tooprocess her `StormTxAttempt`, yalnızca Java yan hangi Storm yapmak gibi.</span><span class="sxs-lookup"><span data-stu-id="b21d4-181">SCP.NET will new a different ISCPBatchBolt object tooprocess each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="b21d4-182">Bu tasarım Hello amacı toosupport paralel işlemleri işleme budur.</span><span class="sxs-lookup"><span data-stu-id="b21d4-182">hello purpose of this design is toosupport parallel transactions processing.</span></span> <span data-ttu-id="b21d4-183">Kullanıcı bunu göz önünde, işlem girişimi tamamlandı, hello karşılık gelen ISCPBatchBolt nesne yok ve atık toplanan tutmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-183">User should keep it in mind that if transaction attempt is finished, hello corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="b21d4-184">Nesne modeli</span><span class="sxs-lookup"><span data-stu-id="b21d4-184">Object Model</span></span>
<span data-ttu-id="b21d4-185">SCP.NET basit bir anahtar nesneleri kümesi ile geliştiriciler tooprogram için de sağlar.</span><span class="sxs-lookup"><span data-stu-id="b21d4-185">SCP.NET also provides a simple set of key objects for developers tooprogram with.</span></span> <span data-ttu-id="b21d4-186">Bunlar **bağlamı**, **StateStore**, ve **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="b21d4-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="b21d4-187">Merhaba geri kalan bölümünde, bu bölümün incelenecektir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-187">They will be discussed in hello rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="b21d4-188">Bağlam</span><span class="sxs-lookup"><span data-stu-id="b21d4-188">Context</span></span>
<span data-ttu-id="b21d4-189">Bağlam çalışan bir ortam toohello uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="b21d4-189">Context provides a running environment toohello application.</span></span> <span data-ttu-id="b21d4-190">Her ISCPPlugin örneğinin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) karşılık gelen bir bağlam örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="b21d4-191">Bağlam tarafından sağlanan hello işlevselliği iki bölüme bölünmüş: bulunan (1) hello statik bölümü hello tüm C\# işlem, yalnızca hello belirli bağlam örneği için kullanılabilir olan (2) hello dinamik bölümü.</span><span class="sxs-lookup"><span data-stu-id="b21d4-191">hello functionality provided by Context can be divided into two parts: (1) hello static part which is available in hello whole C\# process, (2) hello dynamic part which is only available for hello specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="b21d4-192">Statik bölümü</span><span class="sxs-lookup"><span data-stu-id="b21d4-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="b21d4-193">`Logger`Günlük amaçla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="b21d4-194">`pluginType`olan tooindicate hello eklentisi türü hello C kullanılan\# işlemi.</span><span class="sxs-lookup"><span data-stu-id="b21d4-194">`pluginType` is used tooindicate hello plugin type of hello C\# process.</span></span> <span data-ttu-id="b21d4-195">Varsa hello C\# işlemi (olmadan Java) yerel test modda çalıştırılır, hello eklentisi tür `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="b21d4-195">If hello C\# process is run in local test mode (without Java), hello plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="b21d4-196">`Config`Java taraftaki tooget yapılandırma parametrelerini sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-196">`Config` is provided tooget configuration parameters from Java side.</span></span> <span data-ttu-id="b21d4-197">Merhaba parametreleri Java taraftan geçirilen zaman C\# eklentisi başlatılır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-197">hello parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="b21d4-198">Merhaba `Config` parametreleri iki parçalara bölünür: `stormConf` ve `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="b21d4-198">hello `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="b21d4-199">`stormConf`Storm tarafından tanımlanan parametre ve `pluginConf` SCP tarafından tanımlanan hello parametre.</span><span class="sxs-lookup"><span data-stu-id="b21d4-199">`stormConf` is parameters defined by Storm and `pluginConf` is hello parameters defined by SCP.</span></span> <span data-ttu-id="b21d4-200">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b21d4-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="b21d4-201">`TopologyContext`tooget hello topoloji bağlamı ile birden çok paralellik bileşenleri için en kullanışlı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-201">`TopologyContext` is provided tooget hello topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="b21d4-202">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b21d4-202">Here is an example:</span></span>

    //demo how tooget TopologyContext info
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

### <a name="dynamic-part"></a><span data-ttu-id="b21d4-203">Dinamik bölümü</span><span class="sxs-lookup"><span data-stu-id="b21d4-203">Dynamic Part</span></span>
<span data-ttu-id="b21d4-204">Merhaba arabirimleri ilgili tooa belirli bağlam örneği olan.</span><span class="sxs-lookup"><span data-stu-id="b21d4-204">hello following interfaces are pertinent tooa certain Context instance.</span></span> <span data-ttu-id="b21d4-205">Merhaba bağlam örneği SCP.NET platformu tarafından oluşturulan ve toohello kullanıcı kodu geçirildi:</span><span class="sxs-lookup"><span data-stu-id="b21d4-205">hello Context instance is created by SCP.NET platform and passed toohello user code:</span></span>

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="b21d4-206">ACK destekleme işlemsel olmayan spout için yöntemi aşağıdaki hello sağlanır:</span><span class="sxs-lookup"><span data-stu-id="b21d4-206">For non-transactional spout supporting ack, hello following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="b21d4-207">ACK destekleme işlemsel olmayan Cıvata için açıkça gerektiği `Ack()` veya `Fail()` aldığı tanımlama grubu hello.</span><span class="sxs-lookup"><span data-stu-id="b21d4-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` hello tuple it received.</span></span> <span data-ttu-id="b21d4-208">Ve yeni tanımlama grubu yayma, ayrıca hello bağlayıcılarını hello yeni tanımlama grubu olarak belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-208">And when emitting new tuple, it must also specify hello anchors of hello new tuple.</span></span> <span data-ttu-id="b21d4-209">yöntemler aşağıdaki hello sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-209">hello following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="b21d4-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="b21d4-210">StateStore</span></span>
<span data-ttu-id="b21d4-211">`StateStore`Meta Veri Hizmetleri, monoton sıra oluşturma ve bekleme serbest eşgüdüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="b21d4-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="b21d4-212">Üst düzey dağıtılmış eşzamanlılık soyutlamalar oluşturulabilen `StateStore`dağıtılmış kilitleri, dağıtılmış kuyruklar, engelleri ve işlem Hizmetleri dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="b21d4-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="b21d4-213">SCP uygulamaları hello kullanabilir `State` toopersist ZooKeeper, özellikle işlem topolojisi için bazı bilgileri nesne.</span><span class="sxs-lookup"><span data-stu-id="b21d4-213">SCP applications may use hello `State` object toopersist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="b21d4-214">Böylece işlem spout çöker ve yeniden başlatırsanız, ZooKeeper hello gerekli bilgileri almak ve hello ardışık düzeni yeniden yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="b21d4-214">Doing so, if transactional spout crashes and restart, it can retrieve hello necessary information from ZooKeeper and restart hello pipeline.</span></span>

<span data-ttu-id="b21d4-215">Merhaba `StateStore` nesnenin çoğunlukla bu yöntemleri vardır:</span><span class="sxs-lookup"><span data-stu-id="b21d4-215">hello `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
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
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="b21d4-216">Merhaba `State` nesnenin çoğunlukla bu yöntemleri vardır:</span><span class="sxs-lookup"><span data-stu-id="b21d4-216">hello `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="b21d4-217">Hello için `Commit()` yöntemi, simpleMode tootrue ayarladığınızda, onu yalnızca silecek ZooKeeper ZNode karşılık gelen hello.</span><span class="sxs-lookup"><span data-stu-id="b21d4-217">For hello `Commit()` method, when simpleMode is set tootrue, it will simply delete hello corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="b21d4-218">Aksi takdirde silecek geçerli ZNode hello ve hello kabul edilen yeni bir düğüm ekleme\_yolu.</span><span class="sxs-lookup"><span data-stu-id="b21d4-218">Otherwise, it will delete hello current ZNode, and adding a new node in hello COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="b21d4-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="b21d4-219">SCPRuntime</span></span>
<span data-ttu-id="b21d4-220">SCPRuntime hello aşağıdaki iki yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="b21d4-220">SCPRuntime provides hello following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="b21d4-221">`Initialize()`kullanılan tooinitialize hello SCP çalışma zamanı ortamı alır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-221">`Initialize()` is used tooinitialize hello SCP runtime environment.</span></span> <span data-ttu-id="b21d4-222">Bu yöntemde, C hello\# işlem bağlanan toohello Java yan ve yapılandırma parametreleri alır ve topoloji bağlamı.</span><span class="sxs-lookup"><span data-stu-id="b21d4-222">In this method, hello C\# process will connect toohello Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="b21d4-223">`LaunchPlugin()`kullanılan tookick selamlama iletisine kapalı döngü işliyor.</span><span class="sxs-lookup"><span data-stu-id="b21d4-223">`LaunchPlugin()` is used tookick off hello message processing loop.</span></span> <span data-ttu-id="b21d4-224">Bu bir döngüde C hello\# eklentisi iletileri form Java yan (başlık ve denetim sinyalleri dahil) alır ve ardından belki de hello arabirim yöntemi çağırma işlemi Merhaba iletileri hello kullanıcı kodu tarafından sağlayın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-224">In this loop, hello C\# plugin will receive messages form Java side (including tuples and control signals), and then process hello messages, perhaps calling hello interface method provide by hello user code.</span></span> <span data-ttu-id="b21d4-225">Merhaba giriş parametresi yöntemi için `LaunchPlugin()` ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt arabirimini uygulayan nesne döndüren bir temsilci.</span><span class="sxs-lookup"><span data-stu-id="b21d4-225">hello input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="b21d4-226">ISCPBatchBolt için biz alabilirsiniz `StormTxAttempt` gelen `parms`ve yeniden yürütülmüş bir girişim olduğunu toojudge kullanın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it toojudge whether it is a replayed attempt.</span></span> <span data-ttu-id="b21d4-227">Bu genellikle hello yürütme Cıvata yapılır ve hello gösterilen `HelloWorldTx` örnek.</span><span class="sxs-lookup"><span data-stu-id="b21d4-227">This is usually done at hello commit bolt, and it is demonstrated in hello `HelloWorldTx` example.</span></span>

<span data-ttu-id="b21d4-228">Genel olarak bakıldığında, hello SCP eklentileri burada iki modda çalışabilir:</span><span class="sxs-lookup"><span data-stu-id="b21d4-228">Generally speaking, hello SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="b21d4-229">Yerel Test modu: Bu modda SCP eklentileri hello (Merhaba C\# kullanıcı kodu) Visual Studio içinde hello geliştirme aşamasında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-229">Local Test Mode: In this mode, hello SCP plugins (hello C\# user code) run inside Visual Studio during hello development phase.</span></span> <span data-ttu-id="b21d4-230">`LocalContext`Bu modda, yöntem tooserialize yayılan hello diziler toolocal dosyaları ve toomemory geri okuma sağlayan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-230">`LocalContext` can be used in this mode, which provides method tooserialize hello emitted tuples toolocal files, and read them back toomemory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="b21d4-231">Normal modu: Bu modda, hello SCP eklentileri storm java işlemi tarafından başlatılır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-231">Regular Mode: In this mode, hello SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="b21d4-232">SCP eklentisi başlatmanın örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b21d4-232">Here is an example of launching SCP plugin:</span></span>
   
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
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="b21d4-233">Topoloji belirtimi dili</span><span class="sxs-lookup"><span data-stu-id="b21d4-233">Topology Specification Language</span></span>
<span data-ttu-id="b21d4-234">SCP topoloji açıklayan ve SCP topolojileri yapılandırmak için etki alanı belirli bir dil belirtimidir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="b21d4-235">Storm'ın Clojure DSL üzerinde temel alır (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) ve SCP tarafından genişletilir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="b21d4-236">Merhaba yürütme için doğrudan toostorm küme topolojisi belirtimleri'nin gönderilebilir ***runspec*** komutu.</span><span class="sxs-lookup"><span data-stu-id="b21d4-236">Topology specifications can be submitted directly toostorm cluster for execution via hello ***runspec*** command.</span></span>

<span data-ttu-id="b21d4-237">SCP.NET sahip izleme işlevleri toodefine hello işlem topoloji ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b21d4-237">SCP.NET has add follow functions toodefine hello Transactional Topology:</span></span>

| <span data-ttu-id="b21d4-238">**Yeni işlevleri**</span><span class="sxs-lookup"><span data-stu-id="b21d4-238">**New Functions**</span></span> | <span data-ttu-id="b21d4-239">**Parametreler**</span><span class="sxs-lookup"><span data-stu-id="b21d4-239">**Parameters**</span></span> | <span data-ttu-id="b21d4-240">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b21d4-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b21d4-241">**Tx topolopy**</span><span class="sxs-lookup"><span data-stu-id="b21d4-241">**tx-topolopy**</span></span> |<span data-ttu-id="b21d4-242">Topoloji adı</span><span class="sxs-lookup"><span data-stu-id="b21d4-242">topology-name</span></span><br /><span data-ttu-id="b21d4-243">spout eşleme</span><span class="sxs-lookup"><span data-stu-id="b21d4-243">spout-map</span></span><br /><span data-ttu-id="b21d4-244">Cıvata eşleme</span><span class="sxs-lookup"><span data-stu-id="b21d4-244">bolt-map</span></span> |<span data-ttu-id="b21d4-245">Merhaba topoloji ada sahip bir işlem topolojisi tanımlayın &nbsp;tanımı harita ve hello Cıvatalar tanımı Haritası spout'lar</span><span class="sxs-lookup"><span data-stu-id="b21d4-245">Define a transactional topology with hello topology name, &nbsp;spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="b21d4-246">**SCP tx spout**</span><span class="sxs-lookup"><span data-stu-id="b21d4-246">**scp-tx-spout**</span></span> |<span data-ttu-id="b21d4-247">Exec adı</span><span class="sxs-lookup"><span data-stu-id="b21d4-247">exec-name</span></span><br /><span data-ttu-id="b21d4-248">bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="b21d4-248">args</span></span><br /><span data-ttu-id="b21d4-249">Alanları</span><span class="sxs-lookup"><span data-stu-id="b21d4-249">fields</span></span> |<span data-ttu-id="b21d4-250">İşlem spout tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-250">Define a transactional spout.</span></span> <span data-ttu-id="b21d4-251">Merhaba uygulaması ile çalışacak ***exec adı*** kullanarak ***args***.</span><span class="sxs-lookup"><span data-stu-id="b21d4-251">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b21d4-252">Merhaba ***alanları*** hello çıktı alanları spout için</span><span class="sxs-lookup"><span data-stu-id="b21d4-252">hello ***fields*** is hello Output Fields for spout</span></span> |
| <span data-ttu-id="b21d4-253">**tx toplu Cıvata SCP**</span><span class="sxs-lookup"><span data-stu-id="b21d4-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="b21d4-254">Exec adı</span><span class="sxs-lookup"><span data-stu-id="b21d4-254">exec-name</span></span><br /><span data-ttu-id="b21d4-255">bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="b21d4-255">args</span></span><br /><span data-ttu-id="b21d4-256">Alanları</span><span class="sxs-lookup"><span data-stu-id="b21d4-256">fields</span></span> |<span data-ttu-id="b21d4-257">Bir işlem toplu Cıvata tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="b21d4-258">Merhaba uygulaması ile çalışacak ***exec adı*** kullanarak ***bağımsız değişken.***</span><span class="sxs-lookup"><span data-stu-id="b21d4-258">It will run hello application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="b21d4-259">Merhaba alanlar Cıvata Merhaba çıktı alanları modudur.</span><span class="sxs-lookup"><span data-stu-id="b21d4-259">hello Fields is hello Output Fields for bolt.</span></span> |
| <span data-ttu-id="b21d4-260">**SCP-tx-yürütme-Cıvata**</span><span class="sxs-lookup"><span data-stu-id="b21d4-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="b21d4-261">Exec adı</span><span class="sxs-lookup"><span data-stu-id="b21d4-261">exec-name</span></span><br /><span data-ttu-id="b21d4-262">bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="b21d4-262">args</span></span><br /><span data-ttu-id="b21d4-263">Alanları</span><span class="sxs-lookup"><span data-stu-id="b21d4-263">fields</span></span> |<span data-ttu-id="b21d4-264">Bir işlem Committer Cıvata tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="b21d4-265">Merhaba uygulaması ile çalışacak ***exec adı*** kullanarak ***args***.</span><span class="sxs-lookup"><span data-stu-id="b21d4-265">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b21d4-266">Merhaba ***alanları*** hello çıktı alanları Cıvata için</span><span class="sxs-lookup"><span data-stu-id="b21d4-266">hello ***fields*** is hello Output Fields for bolt</span></span> |
| <span data-ttu-id="b21d4-267">**nontx topolopy**</span><span class="sxs-lookup"><span data-stu-id="b21d4-267">**nontx-topolopy**</span></span> |<span data-ttu-id="b21d4-268">Topoloji adı</span><span class="sxs-lookup"><span data-stu-id="b21d4-268">topology-name</span></span><br /><span data-ttu-id="b21d4-269">spout eşleme</span><span class="sxs-lookup"><span data-stu-id="b21d4-269">spout-map</span></span><br /><span data-ttu-id="b21d4-270">Cıvata eşleme</span><span class="sxs-lookup"><span data-stu-id="b21d4-270">bolt-map</span></span> |<span data-ttu-id="b21d4-271">Merhaba topoloji adı, bir işlem topolojisi tanımlayın&nbsp; tanımı harita ve hello Cıvatalar tanımı Haritası spout'lar</span><span class="sxs-lookup"><span data-stu-id="b21d4-271">Define a nontransactional topology with hello topology name,&nbsp; spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="b21d4-272">**SCP spout**</span><span class="sxs-lookup"><span data-stu-id="b21d4-272">**scp-spout**</span></span> |<span data-ttu-id="b21d4-273">Exec adı</span><span class="sxs-lookup"><span data-stu-id="b21d4-273">exec-name</span></span><br /><span data-ttu-id="b21d4-274">bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="b21d4-274">args</span></span><br /><span data-ttu-id="b21d4-275">Alanları</span><span class="sxs-lookup"><span data-stu-id="b21d4-275">fields</span></span><br /><span data-ttu-id="b21d4-276">parametreler</span><span class="sxs-lookup"><span data-stu-id="b21d4-276">parameters</span></span> |<span data-ttu-id="b21d4-277">Bir işlem spout tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-277">Define a nontransactional spout.</span></span> <span data-ttu-id="b21d4-278">Merhaba uygulaması ile çalışacak ***exec adı*** kullanarak ***args***.</span><span class="sxs-lookup"><span data-stu-id="b21d4-278">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b21d4-279">Merhaba ***alanları*** hello çıktı alanları spout için</span><span class="sxs-lookup"><span data-stu-id="b21d4-279">hello ***fields*** is hello Output Fields for spout</span></span><br /><br /><span data-ttu-id="b21d4-280">Merhaba ***parametreleri*** toospecify kullanarak isteğe bağlıdır, "nontransactional.ack.enabled" gibi bazı parametreler.</span><span class="sxs-lookup"><span data-stu-id="b21d4-280">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="b21d4-281">**SCP Cıvata**</span><span class="sxs-lookup"><span data-stu-id="b21d4-281">**scp-bolt**</span></span> |<span data-ttu-id="b21d4-282">Exec adı</span><span class="sxs-lookup"><span data-stu-id="b21d4-282">exec-name</span></span><br /><span data-ttu-id="b21d4-283">bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="b21d4-283">args</span></span><br /><span data-ttu-id="b21d4-284">Alanları</span><span class="sxs-lookup"><span data-stu-id="b21d4-284">fields</span></span><br /><span data-ttu-id="b21d4-285">parametreler</span><span class="sxs-lookup"><span data-stu-id="b21d4-285">parameters</span></span> |<span data-ttu-id="b21d4-286">İşlem dışı Cıvata tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="b21d4-287">Merhaba uygulaması ile çalışacak ***exec adı*** kullanarak ***args***.</span><span class="sxs-lookup"><span data-stu-id="b21d4-287">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b21d4-288">Merhaba ***alanları*** hello çıktı alanları Cıvata için</span><span class="sxs-lookup"><span data-stu-id="b21d4-288">hello ***fields*** is hello Output Fields for bolt</span></span><br /><br /><span data-ttu-id="b21d4-289">Merhaba ***parametreleri*** toospecify kullanarak isteğe bağlıdır, "nontransactional.ack.enabled" gibi bazı parametreler.</span><span class="sxs-lookup"><span data-stu-id="b21d4-289">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="b21d4-290">SCP.NET sahip izleyin anahtarlar tanımlı sözcükleri:</span><span class="sxs-lookup"><span data-stu-id="b21d4-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="b21d4-291">**Anahtar sözcükler**</span><span class="sxs-lookup"><span data-stu-id="b21d4-291">**Key Words**</span></span> | <span data-ttu-id="b21d4-292">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b21d4-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b21d4-293">**: adı**</span><span class="sxs-lookup"><span data-stu-id="b21d4-293">**:name**</span></span> |<span data-ttu-id="b21d4-294">Merhaba topoloji adı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="b21d4-294">Define hello Topology Name</span></span> |
| <span data-ttu-id="b21d4-295">**: topolojisi**</span><span class="sxs-lookup"><span data-stu-id="b21d4-295">**:topology**</span></span> |<span data-ttu-id="b21d4-296">Tanımlama işlevleri yukarıda hello kullanarak topolojisi hello ve olanları içinde derleme.</span><span class="sxs-lookup"><span data-stu-id="b21d4-296">Define hello Topology using hello above functions and build in ones.</span></span> |
| <span data-ttu-id="b21d4-297">**: p**</span><span class="sxs-lookup"><span data-stu-id="b21d4-297">**:p**</span></span> |<span data-ttu-id="b21d4-298">Her spout veya Cıvata için Hello paralellik ipucu tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-298">Define hello parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="b21d4-299">**: yapılandırma**</span><span class="sxs-lookup"><span data-stu-id="b21d4-299">**:config**</span></span> |<span data-ttu-id="b21d4-300">Tanımlama güncelleştirme var olanları hello veya parametre yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b21d4-300">Define configure parameter or update hello existing ones</span></span> |
| <span data-ttu-id="b21d4-301">**: şeması**</span><span class="sxs-lookup"><span data-stu-id="b21d4-301">**:schema**</span></span> |<span data-ttu-id="b21d4-302">Merhaba, şema akış tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-302">Define hello Schema of Stream.</span></span> |

<span data-ttu-id="b21d4-303">Ve sık kullanılan parametreler:</span><span class="sxs-lookup"><span data-stu-id="b21d4-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="b21d4-304">**Parametre**</span><span class="sxs-lookup"><span data-stu-id="b21d4-304">**Parameter**</span></span> | <span data-ttu-id="b21d4-305">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b21d4-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b21d4-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="b21d4-306">**"plugin.name"**</span></span> |<span data-ttu-id="b21d4-307">Merhaba C# eklentisi exe dosyası adı</span><span class="sxs-lookup"><span data-stu-id="b21d4-307">exe file name of hello C# plugin</span></span> |
| <span data-ttu-id="b21d4-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="b21d4-308">**"plugin.args"**</span></span> |<span data-ttu-id="b21d4-309">Eklenti bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="b21d4-309">plugin args</span></span> |
| <span data-ttu-id="b21d4-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="b21d4-310">**"output.schema"**</span></span> |<span data-ttu-id="b21d4-311">Çıkış şeması</span><span class="sxs-lookup"><span data-stu-id="b21d4-311">Output schema</span></span> |
| <span data-ttu-id="b21d4-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="b21d4-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="b21d4-313">Ack işlem topolojisi için etkinleştirilip etkinleştirilmediği</span><span class="sxs-lookup"><span data-stu-id="b21d4-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="b21d4-314">Merhaba runspec komutu hello BITS ile birlikte dağıtılır, hello kullanım gibidir:</span><span class="sxs-lookup"><span data-stu-id="b21d4-314">hello runspec command will be deployed together with hello bits, hello usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="b21d4-315">Merhaba ***kaynak dir*** parametre isteğe bağlıdır ve toospecify gerekir, tooplug C istediğinizde\# uygulama ve bu dizin hello uygulama, başlangıç bağımlılıkları ve yapılandırmaları içerecek.</span><span class="sxs-lookup"><span data-stu-id="b21d4-315">hello ***resource-dir*** parameter is optional, you need toospecify it when you want tooplug a C\# application, and this directory will contain hello application, hello dependencies and configurations.</span></span>

<span data-ttu-id="b21d4-316">Merhaba ***sınıf*** parametredir Ayrıca isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b21d4-316">hello ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="b21d4-317">Merhaba belirtim dosya Java Spout veya Cıvata içeriyorsa kullanılan toospecify hello Java sınıf olur.</span><span class="sxs-lookup"><span data-stu-id="b21d4-317">It is used toospecify hello Java classpath if hello spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="b21d4-318">Çeşitli özellikler</span><span class="sxs-lookup"><span data-stu-id="b21d4-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="b21d4-319">Girdi ve çıktı şema bildirimi</span><span class="sxs-lookup"><span data-stu-id="b21d4-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="b21d4-320">Merhaba kullanıcı c tanımlama grubu yayma\# işlemek, hello platform tooserialize hello tuple gereken byte [], aktarım tooJava yan ve Storm bu tanımlama grubu toohello hedefleri aktarım.</span><span class="sxs-lookup"><span data-stu-id="b21d4-320">hello user can emit tuple in C\# process, hello platform needs tooserialize hello tuple into byte[], transfer tooJava side, and Storm will transfer this tuple toohello targets.</span></span> <span data-ttu-id="b21d4-321">Bu sırada aşağı akış bileşeni C hello\# işlemi geri java taraftan tanımlama grubu alır ve platforma göre toohello özgün türleri dönüştürme, bu işlemlerin hello Platform tarafından gizlenir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-321">Meanwhile in downstream component, hello C\# process will receive tuple back from java side, and convert it toohello original types by platform, all these operations are hidden by hello Platform.</span></span>

<span data-ttu-id="b21d4-322">toosupport hello serileştirme ve seri durumundan çıkarma, kullanıcı kodu hello girişleri ve çıkışları toodeclare hello şeması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-322">toosupport hello serialization and deserialization, user code needs toodeclare hello schema of hello inputs and outputs.</span></span>

<span data-ttu-id="b21d4-323">hello giriş/çıkış akışı şema bir sözlük olarak tanımlanmış, hello hello StreamId anahtarıdır ve hello sütun hello türlerini hello değerdir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-323">hello input/output stream schema is defined as a dictionary, hello key is hello StreamId and hello value is hello Types of hello columns.</span></span> <span data-ttu-id="b21d4-324">Merhaba bileşen bildirilen çok akışları sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-324">hello component can have multi-streams declared.</span></span>

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


<span data-ttu-id="b21d4-325">Bağlam nesnesinde aşağıdaki API eklenen hello vardır:</span><span class="sxs-lookup"><span data-stu-id="b21d4-325">In Context object, we have hello following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="b21d4-326">Kullanıcı kodu yayılan hello diziler için bu akış tanımlanan hello şema uyma veya hello sistem çalışma zamanı özel durum atar emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-326">User code must make sure hello tuples emitted obey hello schema defined for that stream, or hello system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="b21d4-327">Birden çok akış desteği</span><span class="sxs-lookup"><span data-stu-id="b21d4-327">Multi-Stream Support</span></span>
<span data-ttu-id="b21d4-328">SCP destekler kullanıcı tooemit kod veya birden çok farklı akış hello adresindeki aynı almak zaman.</span><span class="sxs-lookup"><span data-stu-id="b21d4-328">SCP supports user code tooemit or receive from multiple distinct streams at hello same time.</span></span> <span data-ttu-id="b21d4-329">Merhaba Emit yöntemi bir isteğe bağlı Akış ID parametresi yararlanırken hello destek hello bağlamı nesnesinde yansıtır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-329">hello support reflects in hello Context object as hello Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="b21d4-330">Merhaba SCP.NET bağlam nesnesi öğesinde iki yöntem eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-330">Two methods in hello SCP.NET Context object have been added.</span></span> <span data-ttu-id="b21d4-331">Kullanılan tooemit tanımlama grubu ya da diziler toospecify StreamId oldukları.</span><span class="sxs-lookup"><span data-stu-id="b21d4-331">They are used tooemit Tuple or Tuples toospecify StreamId.</span></span> <span data-ttu-id="b21d4-332">Merhaba StreamId bir dize ve toobe hem c tutarlı gerekiyor\# ve topoloji tanımı Spec hello.</span><span class="sxs-lookup"><span data-stu-id="b21d4-332">hello StreamId is a string and it needs toobe consistent in both C\# and hello Topology Definition Spec.</span></span>

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="b21d4-333">Merhaba verme tooa var olmayan akışı çalışma zamanı özel durumları neden olur.</span><span class="sxs-lookup"><span data-stu-id="b21d4-333">hello emitting tooa non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="b21d4-334">Alanları gruplandırma</span><span class="sxs-lookup"><span data-stu-id="b21d4-334">Fields Grouping</span></span>
<span data-ttu-id="b21d4-335">Merhaba yapı içinde alanları gruplandırmasındaki Strom SCP.NET içinde düzgün çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="b21d4-335">hello build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="b21d4-336">Hello Java Proxy tarafı, tüm hello alanları veri türleridir gerçekte byte [] ve gruplandırma hello alanlarını hello byte [] nesnesi karma kodu tooperform hello gruplandırma kullanır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-336">On hello Java Proxy side, all hello fields data types are actually byte[], and hello fields grouping uses hello byte[] object hash code tooperform hello grouping.</span></span> <span data-ttu-id="b21d4-337">Merhaba byte [] nesnesi karma kodu, bu nesnenin bellekte hello adresidir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-337">hello byte[] object hash code is hello address of this object in memory.</span></span> <span data-ttu-id="b21d4-338">[] Hello gruplandırma için iki bayt yanlış olması için aynı içerik ancak aynı adres hello değil o paylaşımı hello nesneleri.</span><span class="sxs-lookup"><span data-stu-id="b21d4-338">So hello grouping will be wrong for two byte[] objects that share hello same content but not hello same address.</span></span>

<span data-ttu-id="b21d4-339">Özelleştirilmiş gruplandırma yöntemi SCP.NET ekler ve hello byte [] toodo hello gruplandırma Merhaba içeriğine kullanır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-339">SCP.NET adds a customized grouping method, and it will use hello content of hello byte[] toodo hello grouping.</span></span> <span data-ttu-id="b21d4-340">İçinde **SPEC** hello sözdizimi dosya, benzer:</span><span class="sxs-lookup"><span data-stu-id="b21d4-340">In **SPEC** file, hello syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="b21d4-341">Burada,</span><span class="sxs-lookup"><span data-stu-id="b21d4-341">Here,</span></span>

1. <span data-ttu-id="b21d4-342">"scp alan grup", "SCP tarafından uygulanan özelleştirilmiş alan gruplandırma" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="b21d4-343">": tx"veya": tx olmayan" işlem topoloji olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="b21d4-344">Dizininden başlayarak hello tx olmayan topolojileri tx farklı olduğundan bu bilgileri ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="b21d4-344">We need this information since hello starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="b21d4-345">[0,1] anlamına alan kimlikleri, 0'dan başlayarak izleri hashset'i.</span><span class="sxs-lookup"><span data-stu-id="b21d4-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="b21d4-346">Karma topolojisi</span><span class="sxs-lookup"><span data-stu-id="b21d4-346">Hybrid topology</span></span>
<span data-ttu-id="b21d4-347">Merhaba yerel Storm Java yazılır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-347">hello native Storm is written in Java.</span></span> <span data-ttu-id="b21d4-348">SCP.Net Gelişmiş ve onu tooenable bizim Gümrük toowrite C\# toohandle kendi iş mantığı kod.</span><span class="sxs-lookup"><span data-stu-id="b21d4-348">And SCP.Net has enhanced it tooenable our customs toowrite C\# code toohandle their business logic.</span></span> <span data-ttu-id="b21d4-349">Ancak aynı zamanda karma topolojiler yalnızca C içeren destekliyoruz\# spout'lar/Cıvatalar, aynı zamanda Java Spout/Cıvatalar.</span><span class="sxs-lookup"><span data-stu-id="b21d4-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="b21d4-350">Java Spout/Cıvata belirtim dosyasında belirtin</span><span class="sxs-lookup"><span data-stu-id="b21d4-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="b21d4-351">Belirtim dosyasındaki "scp-spout" ve "scp-Cıvata" Ayrıca Java kullanılan toospecify Spout'lar ve Cıvatalar olabilir, örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b21d4-351">In spec file, "scp-spout" and "scp-bolt" can also be used toospecify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="b21d4-352">Burada `microsoft.scp.example.HybridTopology.Generator` hello Java Spout sınıfı hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-352">Here `microsoft.scp.example.HybridTopology.Generator` is hello name of hello Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="b21d4-353">Java sınıf runSpec komutunu belirtin</span><span class="sxs-lookup"><span data-stu-id="b21d4-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="b21d4-354">Java Spout'lar veya Cıvatalar içeren toosubmit topoloji istiyorsanız toofirst derleme hello Java Spout'lar veya Cıvatalar gerekir ve hello Jar dosyalarını alın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-354">If you want toosubmit topology containing Java Spouts or Bolts, you need toofirst compile hello Java Spouts or Bolts and get hello Jar files.</span></span> <span data-ttu-id="b21d4-355">Ardından hello java topolojisi gönderirken hello Jar dosyalarını içeren bir sınıf belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-355">Then you should specify hello java classpath that contains hello Jar files when submitting topology.</span></span> <span data-ttu-id="b21d4-356">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b21d4-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="b21d4-357">Burada **örnekler\\HybridTopology\\java\\hedef\\**  olan hello içeren klasör hello Java Spout/Cıvata Jar dosyasını.</span><span class="sxs-lookup"><span data-stu-id="b21d4-357">Here **examples\\HybridTopology\\java\\target\\** is hello folder containing hello Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="b21d4-358">Seri hale getirme ve seri durumdan çıkarma Java ve C\ arasında</span><span class="sxs-lookup"><span data-stu-id="b21d4-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="b21d4-359">Java yan ve C bizim SCP bileşeni içerir\# yan.</span><span class="sxs-lookup"><span data-stu-id="b21d4-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="b21d4-360">Sipariş toointeract ile yerel Java Spout'lar/Cıvatalar, serileştirme/seri durumdan çıkarma Java yan ve C uygulanması gereken\# hello grafiği aşağıdaki gösterildiği gibi tarafı.</span><span class="sxs-lookup"><span data-stu-id="b21d4-360">In order toointeract with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in hello following graph.</span></span>

![java bileşeni tooJava bileşen gönderme tooSCP bileşen gönderme diyagramı](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="b21d4-362">**Seri hale getirme Java yan ve seri durumdan çıkarma c\# yan**</span><span class="sxs-lookup"><span data-stu-id="b21d4-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="b21d4-363">Java taraf serileştirme ve seri durumundan çıkarma c için varsayılan uygulaması ilk sağladığımız\# yan.</span><span class="sxs-lookup"><span data-stu-id="b21d4-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="b21d4-364">Java taraf Hello seri duruma getirme yöntemi belirtim dosyasında belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="b21d4-364">hello serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="b21d4-365">Merhaba C seri durumdan çıkarma yöntemini\# yan C'de belirtilmelidir\# kullanıcı kodu:</span><span class="sxs-lookup"><span data-stu-id="b21d4-365">hello deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="b21d4-366">Merhaba veri türü çok karmaşık değilse, çoğu durumda bu varsayılan uygulama işlemelidir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-366">This default implementation should handle most cases if hello data type is not too complex.</span></span> <span data-ttu-id="b21d4-367">Bazı durumlarda, ya da hello kullanıcı veri türü çok karmaşık olduğu için veya hello bizim varsayılan uygulama performansını karşılamadığı için kullanıcının gereksinim, kullanıcı can eklenti kendi uygulama hello.</span><span class="sxs-lookup"><span data-stu-id="b21d4-367">For certain cases, either because hello user data type is too complex, or because hello performance of our default implementation does not meet hello user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="b21d4-368">Merhaba seri arabirimi Java'da yan olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="b21d4-368">hello serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="b21d4-369">Merhaba seri durumdan C arabiriminde\# yan olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="b21d4-369">hello deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="b21d4-370">Ortak arabirimi ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="b21d4-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="b21d4-371">**Seri hale getirme c\# yan ve Java yan yana çıkarma**</span><span class="sxs-lookup"><span data-stu-id="b21d4-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="b21d4-372">Merhaba seri duruma getirme yöntemi c\# yan C'de belirtilmelidir\# kullanıcı kodu:</span><span class="sxs-lookup"><span data-stu-id="b21d4-372">hello serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="b21d4-373">Merhaba seri durumdan çıkarma yöntemini Java taraf belirtim dosyasında belirtilen:</span><span class="sxs-lookup"><span data-stu-id="b21d4-373">hello Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="b21d4-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="b21d4-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="b21d4-375">Burada "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" Merhaba seri durumdan Çıkarıcının adıdır ve "microsoft.scp.example.HybridTopology.Person" Merhaba hedef sınıf hello verileri seri durumdan olduğu.</span><span class="sxs-lookup"><span data-stu-id="b21d4-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is hello name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is hello target class hello data is deserialized to.</span></span>
   
   <span data-ttu-id="b21d4-376">Kullanıcı ayrıca eklenti yapabilir, kendi uygulama c\# seri hale getirici ve Java seri durumdan Çıkarıcının.</span><span class="sxs-lookup"><span data-stu-id="b21d4-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="b21d4-377">Bu hello C arabirimidir\# seri hale getirici:</span><span class="sxs-lookup"><span data-stu-id="b21d4-377">This is hello interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="b21d4-378">Bu Java kaldırıcı hello arabirimi.</span><span class="sxs-lookup"><span data-stu-id="b21d4-378">This is hello interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="b21d4-379">SCP ana mod</span><span class="sxs-lookup"><span data-stu-id="b21d4-379">SCP Host Mode</span></span>
<span data-ttu-id="b21d4-380">Bu modda, kullanıcı kendi kodlarını tooDLL derleyin ve SCP toosubmit topolojisi tarafından sağlanan SCPHost.exe kullanın.</span><span class="sxs-lookup"><span data-stu-id="b21d4-380">In this mode, user can compile their codes tooDLL, and use SCPHost.exe provided by SCP toosubmit topology.</span></span> <span data-ttu-id="b21d4-381">Merhaba belirtim dosyası şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="b21d4-381">hello spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="b21d4-382">Burada, `plugin.name` olarak belirtilen `SCPHost.exe` SCP SDK'sı tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="b21d4-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="b21d4-383">Tam olarak üç parametre kabul eden SCPHost.exe:</span><span class="sxs-lookup"><span data-stu-id="b21d4-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="b21d4-384">Merhaba ilk olduğu hello DLL adı biridir `"HelloWorld.dll"` Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="b21d4-384">hello first one is hello DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="b21d4-385">Merhaba ikincisi olan hello sınıfı adıdır `"Scp.App.HelloWorld.Generator"` Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="b21d4-385">hello second one is hello Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="b21d4-386">Merhaba üçüncü bir hello çağrılan tooget ISCPPlugin örneği olabilir genel bir statik yöntem adıdır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-386">hello third one is hello name of a public static method, which can be invoked tooget an instance of ISCPPlugin.</span></span>

<span data-ttu-id="b21d4-387">Ana mod, kullanıcı kodu DLL olarak derlenmiş ve SCP platformu tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="b21d4-388">Bu nedenle SCP platform hello tüm işleme mantığı üzerinde tam denetimi elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b21d4-388">So SCP platform can get full control of hello whole processing logic.</span></span> <span data-ttu-id="b21d4-389">Merhaba geliştirme deneyimi kolaylaştırmak ve bize de sonraki sürüm için daha fazla esneklik ve daha iyi geriye dönük uyumluluk Getir müşterilerimizin SCP ana mod toosubmit topolojisinde nedenle öneririz.</span><span class="sxs-lookup"><span data-stu-id="b21d4-389">So we recommend our customers toosubmit topology in SCP host mode since it can simplify hello development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="b21d4-390">SCP programlama örnekleri</span><span class="sxs-lookup"><span data-stu-id="b21d4-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="b21d4-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="b21d4-391">HelloWorld</span></span>
<span data-ttu-id="b21d4-392">**HelloWorld** çok basit bir örnek tooshow SCP.Net bakış değil.</span><span class="sxs-lookup"><span data-stu-id="b21d4-392">**HelloWorld** is a very simple example tooshow a taste of SCP.Net.</span></span> <span data-ttu-id="b21d4-393">Adlı bir spout ile bir işlemsel olmayan topolojisi kullanır **Oluşturucu**ve adlı iki Cıvatalar **Bölümlendirici** ve **sayaç**.</span><span class="sxs-lookup"><span data-stu-id="b21d4-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="b21d4-394">Merhaba spout **Oluşturucu** rastgele bazı cümleleri oluşturur ve bu cümleleri çok yayma**Bölümlendirici**.</span><span class="sxs-lookup"><span data-stu-id="b21d4-394">hello spout **generator** will randomly generate some sentences, and emit these sentences too**splitter**.</span></span> <span data-ttu-id="b21d4-395">Merhaba Cıvata **Bölümlendirici** hello cümleleri toowords bölme ve bu sözcükleri çok yayma**sayaç** Cıvata.</span><span class="sxs-lookup"><span data-stu-id="b21d4-395">hello bolt **splitter** will split hello sentences toowords and emit these words too**counter** bolt.</span></span> <span data-ttu-id="b21d4-396">Merhaba Cıvata "sayacı" bir sözlük toorecord hello oluşum sayısı her sözcüğün kullanır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-396">hello bolt "counter" uses a dictionary toorecord hello occurrence number of each word.</span></span>

<span data-ttu-id="b21d4-397">İki belirtim dosya **HelloWorld.spec** ve **HelloWorld\_EnableAck.spec** Bu örnek için.</span><span class="sxs-lookup"><span data-stu-id="b21d4-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="b21d4-398">Merhaba C içinde\# kodu, onu bulabilir ack Java taraftan hello pluginConf alarak etkinleştirilip etkinleştirilmediği çıkışı.</span><span class="sxs-lookup"><span data-stu-id="b21d4-398">In hello C\# code, it can find out whether ack is enabled by getting hello pluginConf from Java side.</span></span>

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="b21d4-399">ACK etkinleştirilirse hello spout içinde bir sözlük acked edilmemiş kullanılan toocache hello diziler olur.</span><span class="sxs-lookup"><span data-stu-id="b21d4-399">In hello spout, if ack is enabled, a dictionary is used toocache hello tuples that have not been acked.</span></span> <span data-ttu-id="b21d4-400">Fail() çağrılırsa, hello başarısız tanımlama grubu yeniden yürütülmesi:</span><span class="sxs-lookup"><span data-stu-id="b21d4-400">If Fail() is called, hello failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="b21d4-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="b21d4-401">HelloWorldTx</span></span>
<span data-ttu-id="b21d4-402">Merhaba **HelloWorldTx** örnek gösterir nasıl tooimplement işlem topolojisi.</span><span class="sxs-lookup"><span data-stu-id="b21d4-402">hello **HelloWorldTx** example demonstrates how tooimplement transactional topology.</span></span> <span data-ttu-id="b21d4-403">Adlı bir spout sahip **Oluşturucu**, bir toplu Cıvatalar adlı **kısmi-count**, ve bir yürütme Cıvata adlı **sayısı toplam**.</span><span class="sxs-lookup"><span data-stu-id="b21d4-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="b21d4-404">Ayrıca üç önceden oluşturulmuş txt dosyaları vardır: **DataSource0.txt**, **DataSource1.txt** ve **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="b21d4-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="b21d4-405">Spout her işlemde hello **Oluşturucu** rastgele iki dosyaları üç dosya önceden oluşturulmuş hello seçin ve hello iki dosya adları toohello yayma **kısmi-count** Cıvata.</span><span class="sxs-lookup"><span data-stu-id="b21d4-405">In each transaction, hello spout **generator** will randomly choose two files from hello pre-created three files, and emit hello two file names toohello **partial-count** bolt.</span></span> <span data-ttu-id="b21d4-406">Merhaba Cıvata **kısmi-count** ilk hello dosya adı bu dosyada alınan hello tuple sonra açık hello dosya ve sayısı hello sözcük sayısını alın ve son olarak hello word numara toohello yayma **sayısı toplam**Cıvata.</span><span class="sxs-lookup"><span data-stu-id="b21d4-406">hello bolt **partial-count** will first get hello file name from hello received tuple, then open hello file and count hello number of words in this file, and finally emit hello word number toohello **count-sum** bolt.</span></span> <span data-ttu-id="b21d4-407">Merhaba **sayısı toplam** Cıvata hello toplam sayısı özetlemek.</span><span class="sxs-lookup"><span data-stu-id="b21d4-407">hello **count-sum** bolt will summarize hello total count.</span></span>

<span data-ttu-id="b21d4-408">tooachieve **tam olarak bir kez** semantiği, hello yürütme Cıvata **sayısı toplam** yeniden yürütülmüş bir işlem olup olmadığını toojudge gerekir.</span><span class="sxs-lookup"><span data-stu-id="b21d4-408">tooachieve **exactly once** semantics, hello commit bolt **count-sum** need toojudge whether it is a replayed transaction.</span></span> <span data-ttu-id="b21d4-409">Bu örnekte, bir statik üye değişkeni vardır:</span><span class="sxs-lookup"><span data-stu-id="b21d4-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="b21d4-410">ISCPBatchBolt örneği oluşturulduğunda, hello alırsınız `txAttempt` Giriş parametrelerinden:</span><span class="sxs-lookup"><span data-stu-id="b21d4-410">When an ISCPBatchBolt instance is created, it will get hello `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
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

<span data-ttu-id="b21d4-411">Zaman `FinishBatch()` , hello adlandırılır `lastCommittedTxId` yeniden yürütülmüş bir işlem değilse güncelleştirme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-411">When `FinishBatch()` is called, hello `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="b21d4-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="b21d4-412">HybridTopology</span></span>
<span data-ttu-id="b21d4-413">Bu topoloji Spout Java ve C içeren\# Cıvata.</span><span class="sxs-lookup"><span data-stu-id="b21d4-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="b21d4-414">SCP platform tarafından sağlanan hello varsayılan seri hale getirme ve seri durumdan çıkarma uygulaması kullanır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-414">It uses hello default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="b21d4-415">Ref hello lütfen **HybridTopology.spec** içinde **örnekler\\HybridTopology** hello belirtim dosya ayrıntıları için klasör ve **SubmitTopology.bat** nasıl toospecify Java sınıf.</span><span class="sxs-lookup"><span data-stu-id="b21d4-415">Please ref hello **HybridTopology.spec** in **examples\\HybridTopology** folder for hello spec file details, and **SubmitTopology.bat** for how toospecify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="b21d4-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="b21d4-416">SCPHostDemo</span></span>
<span data-ttu-id="b21d4-417">Bu örnekte olduğu hello HelloWorld aynı temelde.</span><span class="sxs-lookup"><span data-stu-id="b21d4-417">This example is hello same as HelloWorld in essence.</span></span> <span data-ttu-id="b21d4-418">Merhaba yalnızca hello kullanıcı kodu DLL olarak derlenir ve hello topoloji SCPHost.exe kullanılarak gönderilen farktır.</span><span class="sxs-lookup"><span data-stu-id="b21d4-418">hello only difference is that hello user code is compiled as DLL and hello topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="b21d4-419">Ref hello bölüm "SCP ana modu" daha ayrıntılı açıklaması için lütfen.</span><span class="sxs-lookup"><span data-stu-id="b21d4-419">Please ref hello section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b21d4-420">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b21d4-420">Next Steps</span></span>
<span data-ttu-id="b21d4-421">Storm topolojilerini SCP kullanılarak oluşturulan bir örnekleri için hello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="b21d4-421">For examples of Storm topologies created using SCP, see hello following:</span></span>

* [<span data-ttu-id="b21d4-422">Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="b21d4-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="b21d4-423">Hdınsight üzerinde Storm ile Azure Event hubs'tan işlem olayları</span><span class="sxs-lookup"><span data-stu-id="b21d4-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="b21d4-424">Bir C# Storm topolojisinde birden çok veri akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b21d4-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="b21d4-425">Power BI toovisualize veri bir Storm topolojisinin kullanın</span><span class="sxs-lookup"><span data-stu-id="b21d4-425">Use Power Bi toovisualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="b21d4-426">Event Hubs Hdınsight üzerinde Storm kullanmaya aracın algılayıcı verilerini işlemek</span><span class="sxs-lookup"><span data-stu-id="b21d4-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="b21d4-427">Ayıklama, dönüştürme ve yükleme (ETL) Azure Event Hubs tooHBase gelen</span><span class="sxs-lookup"><span data-stu-id="b21d4-427">Extract, Transform, and Load (ETL) from Azure Event Hubs tooHBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="b21d4-428">Hdınsight üzerinde Storm ve HBase kullanarak olayları ilişkilendirmenize</span><span class="sxs-lookup"><span data-stu-id="b21d4-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)


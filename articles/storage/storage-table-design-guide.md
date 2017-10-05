---
title: "Azure depolama tablo Tasarım Kılavuzu | Microsoft Docs"
description: "Tasarım ölçeklenebilir ve kullanıcı tablolarında Azure tablo depolaması"
services: storage
documentationcenter: na
author: jasonnewyork
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: jahogg
ms.openlocfilehash: 5ddb234cc97b3113ec865f97195c871b9f2f40d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a><span data-ttu-id="90b75-103">Azure depolama tablo Tasarım Kılavuzu: Ölçeklenebilir tasarlama ve kullanıcı tabloları</span><span class="sxs-lookup"><span data-stu-id="90b75-103">Azure Storage Table Design Guide: Designing Scalable and Performant Tables</span></span>
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="90b75-104">Tasarım ölçeklenebilir ve kullanıcı tabloları bir dizi etkene performans, ölçeklenebilirlik ve maliyet gibi dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-104">To design scalable and performant tables you must consider a number of factors such as performance, scalability, and cost.</span></span> <span data-ttu-id="90b75-105">Daha önce şemaları ilişkisel veritabanları için tasarlanmış, bu noktalar size tanıdık olacaktır, ancak Azure Table hizmet depolama modeli ve ilişkisel modelleri arasında bazı benzerlikler olsa da, aynı zamanda birçok önemli farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="90b75-105">If you have previously designed schemas for relational databases, these considerations will be familiar to you, but while there are some similarities between the Azure Table service storage model and relational models, there are also many important differences.</span></span> <span data-ttu-id="90b75-106">Bu farklılıklar, genellikle, counter-intuitive veya ilişkisel veritabanları ile tanıdık birine yanlış görünebilir, ancak Azure tablo hizmeti gibi bir NoSQL anahtar/değer deposu için tanımlıyorsanız, iyi bir fikir hale getirmeyin çok farklı tasarımları için yol açar.</span><span class="sxs-lookup"><span data-stu-id="90b75-106">These differences typically lead to very different designs that may look counter-intuitive or wrong to someone familiar with relational databases, but which do make good sense if you are designing for a NoSQL key/value store such as the Azure Table service.</span></span> <span data-ttu-id="90b75-107">Tasarım farklar çoğunu tablo hizmeti varlıkları (ilişkisel veritabanı terminolojisi bulunan satırlar) veri veya çok yüksek işlem hacmi desteklemelidir veri kümeleri için milyarlarca içerebilir bulut ölçekli uygulamalar destekleyecek şekilde tasarlanmıştır olgu yansıtır: Bu nedenle, farklı verilerinizi depolamak nasıl hakkında düşünün ve tablo hizmeti nasıl çalıştığını anlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-107">Many of your design differences will reflect the fact that the Table service is designed to support cloud-scale applications that can contain billions of entities (rows in relational database terminology) of data or for datasets that must support very high transaction volumes: therefore, you need to think differently about how you store your data and understand how the Table service works.</span></span> <span data-ttu-id="90b75-108">İyi tasarlanmış bir NoSQL veri deposu çok daha (ve daha düşük maliyetle) ölçeklendirmek, çözümünüzün etkinleştirebilirsiniz bir çözümden bir ilişkisel veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-108">A well designed NoSQL data store can enable your solution to scale much further (and at a lower cost) than a solution that uses a relational database.</span></span> <span data-ttu-id="90b75-109">Bu kılavuz, bu konularda yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="90b75-109">This guide helps you with these topics.</span></span>  

## <a name="about-the-azure-table-service"></a><span data-ttu-id="90b75-110">Azure tablo hizmeti hakkında</span><span class="sxs-lookup"><span data-stu-id="90b75-110">About the Azure Table service</span></span>
<span data-ttu-id="90b75-111">Bu bölümde bazı performans ve ölçeklenebilirlik için tasarlama yakından ilgili olan anahtar özellikleri Tablo hizmetinin vurgular.</span><span class="sxs-lookup"><span data-stu-id="90b75-111">This section highlights some of the key features of the Table service that are especially relevant to designing for performance and scalability.</span></span> <span data-ttu-id="90b75-112">Azure Storage ve tablo hizmeti yeniyseniz, ilk okuma [Microsoft Azure Storage'a giriş](storage-introduction.md) ve [.NET kullanarak Azure Table Storage ile çalışmaya başlama](storage-dotnet-how-to-use-tables.md) bu makalenin sonraki bölümlerinde okuma önce.</span><span class="sxs-lookup"><span data-stu-id="90b75-112">If you are new to Azure Storage and the Table service, first read [Introduction to Microsoft Azure Storage](storage-introduction.md) and [Get started with Azure Table Storage using .NET](storage-dotnet-how-to-use-tables.md) before reading the remainder of this article.</span></span> <span data-ttu-id="90b75-113">Bu kılavuzun odağı tablo hizmetinde olsa da, bazı tartışma Azure kuyruk ve Blob Hizmetleri ve bir çözüm tablo hizmetinde yanı sıra bunları nasıl kullanacağınızı içerecektir.</span><span class="sxs-lookup"><span data-stu-id="90b75-113">Although the focus of this guide is on the Table service, it will include some discussion of the Azure Queue and Blob services, and how you might use them along with the Table service in a solution.</span></span>  

<span data-ttu-id="90b75-114">Tablo hizmeti nedir?</span><span class="sxs-lookup"><span data-stu-id="90b75-114">What is the Table service?</span></span> <span data-ttu-id="90b75-115">Tablo hizmeti tablosal biçimde adından beklediğiniz gibi verileri depolamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-115">As you might expect from the name, the Table service uses a tabular format to store data.</span></span> <span data-ttu-id="90b75-116">Standart terminoloji, tablodaki her satır bir varlığı temsil eden ve sütunları varlık çeşitli özelliklerini depolamak.</span><span class="sxs-lookup"><span data-stu-id="90b75-116">In the standard terminology, each row of the table represents an entity, and the columns store the various properties of that entity.</span></span> <span data-ttu-id="90b75-117">Her varlığın benzersiz şekilde tanımlamak için anahtar çiftini vardır ve tablo hizmeti varlık en son değiştirildiği izlemek için kullandığı bir zaman damgası sütunu güncelleştirilen (Bu otomatik olarak gerçekleşir ve zaman damgası rasgele bir değerle el ile üzerine yazılamıyor).</span><span class="sxs-lookup"><span data-stu-id="90b75-117">Every entity has a pair of keys to uniquely identify it, and a timestamp column that the Table service uses to track when the entity was last updated (this happens automatically and you cannot manually overwrite the timestamp with an arbitrary value).</span></span> <span data-ttu-id="90b75-118">Tablo hizmeti iyimser eşzamanlılık yönetmek için bu son değiştirilen zaman damgası (LMT) kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-118">The Table service uses this last-modified timestamp (LMT) to manage optimistic concurrency.</span></span>  

> [!NOTE]
> <span data-ttu-id="90b75-119">Tablo hizmeti REST API işlemleri aynı zamanda sonuç bir **ETag** son değiştirilen zaman damgası (LMT) türetilen değeri.</span><span class="sxs-lookup"><span data-stu-id="90b75-119">The Table service REST API operations also return an **ETag** value that it derives from the last-modified timestamp (LMT).</span></span> <span data-ttu-id="90b75-120">Aynı temel alınan veri başvurduğundan bu belgede ETag ve LMT terimleri birbirlerinin yerine kullanırız.</span><span class="sxs-lookup"><span data-stu-id="90b75-120">In this document we will use the terms ETag and LMT interchangeably because they refer to the same underlying data.</span></span>  
> 
> 

<span data-ttu-id="90b75-121">Aşağıdaki örnek, çalışan ve departman varlıkları depolamak için bir basit Tablo Tasarımı gösterir.</span><span class="sxs-lookup"><span data-stu-id="90b75-121">The following example shows a simple table design to store employee and department entities.</span></span> <span data-ttu-id="90b75-122">Bu kılavuzda gösterilen örneklerin çoğu bu basit tasarım temel alır.</span><span class="sxs-lookup"><span data-stu-id="90b75-122">Many of the examples shown later in this guide are based on this simple design.</span></span>  

<table>
<tr>
<th><span data-ttu-id="90b75-123">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="90b75-123">PartitionKey</span></span></th>
<th><span data-ttu-id="90b75-124">RowKey</span><span class="sxs-lookup"><span data-stu-id="90b75-124">RowKey</span></span></th>
<th><span data-ttu-id="90b75-125">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="90b75-125">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td><span data-ttu-id="90b75-126">Pazarlama</span><span class="sxs-lookup"><span data-stu-id="90b75-126">Marketing</span></span></td>
<td><span data-ttu-id="90b75-127">00001</span><span class="sxs-lookup"><span data-stu-id="90b75-127">00001</span></span></td>
<td><span data-ttu-id="90b75-128">2014-08-22T00:50:32Z</span><span class="sxs-lookup"><span data-stu-id="90b75-128">2014-08-22T00:50:32Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-129">FirstName</span><span class="sxs-lookup"><span data-stu-id="90b75-129">FirstName</span></span></th>
<th><span data-ttu-id="90b75-130">Soyadı</span><span class="sxs-lookup"><span data-stu-id="90b75-130">LastName</span></span></th>
<th><span data-ttu-id="90b75-131">Yaş</span><span class="sxs-lookup"><span data-stu-id="90b75-131">Age</span></span></th>
<th><span data-ttu-id="90b75-132">E-posta</span><span class="sxs-lookup"><span data-stu-id="90b75-132">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="90b75-133">Tan</span><span class="sxs-lookup"><span data-stu-id="90b75-133">Don</span></span></td>
<td><span data-ttu-id="90b75-134">Hall</span><span class="sxs-lookup"><span data-stu-id="90b75-134">Hall</span></span></td>
<td><span data-ttu-id="90b75-135">34</span><span class="sxs-lookup"><span data-stu-id="90b75-135">34</span></span></td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="90b75-136">Pazarlama</span><span class="sxs-lookup"><span data-stu-id="90b75-136">Marketing</span></span></td>
<td><span data-ttu-id="90b75-137">00002</span><span class="sxs-lookup"><span data-stu-id="90b75-137">00002</span></span></td>
<td><span data-ttu-id="90b75-138">2014-08-22T00:50:34Z</span><span class="sxs-lookup"><span data-stu-id="90b75-138">2014-08-22T00:50:34Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-139">FirstName</span><span class="sxs-lookup"><span data-stu-id="90b75-139">FirstName</span></span></th>
<th><span data-ttu-id="90b75-140">Soyadı</span><span class="sxs-lookup"><span data-stu-id="90b75-140">LastName</span></span></th>
<th><span data-ttu-id="90b75-141">Yaş</span><span class="sxs-lookup"><span data-stu-id="90b75-141">Age</span></span></th>
<th><span data-ttu-id="90b75-142">E-posta</span><span class="sxs-lookup"><span data-stu-id="90b75-142">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="90b75-143">Haz</span><span class="sxs-lookup"><span data-stu-id="90b75-143">Jun</span></span></td>
<td><span data-ttu-id="90b75-144">CAO</span><span class="sxs-lookup"><span data-stu-id="90b75-144">Cao</span></span></td>
<td><span data-ttu-id="90b75-145">47</span><span class="sxs-lookup"><span data-stu-id="90b75-145">47</span></span></td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="90b75-146">Pazarlama</span><span class="sxs-lookup"><span data-stu-id="90b75-146">Marketing</span></span></td>
<td><span data-ttu-id="90b75-147">Bölüm</span><span class="sxs-lookup"><span data-stu-id="90b75-147">Department</span></span></td>
<td><span data-ttu-id="90b75-148">2014-08-22T00:50:30Z</span><span class="sxs-lookup"><span data-stu-id="90b75-148">2014-08-22T00:50:30Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-149">departmentName</span><span class="sxs-lookup"><span data-stu-id="90b75-149">DepartmentName</span></span></th>
<th><span data-ttu-id="90b75-150">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="90b75-150">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="90b75-151">Pazarlama</span><span class="sxs-lookup"><span data-stu-id="90b75-151">Marketing</span></span></td>
<td><span data-ttu-id="90b75-152">153</span><span class="sxs-lookup"><span data-stu-id="90b75-152">153</span></span></td>
</tr>
</table>
</td>
</tr>
<tr>
<td><span data-ttu-id="90b75-153">Satış</span><span class="sxs-lookup"><span data-stu-id="90b75-153">Sales</span></span></td>
<td><span data-ttu-id="90b75-154">00010</span><span class="sxs-lookup"><span data-stu-id="90b75-154">00010</span></span></td>
<td><span data-ttu-id="90b75-155">2014-08-22T00:50:44Z</span><span class="sxs-lookup"><span data-stu-id="90b75-155">2014-08-22T00:50:44Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-156">FirstName</span><span class="sxs-lookup"><span data-stu-id="90b75-156">FirstName</span></span></th>
<th><span data-ttu-id="90b75-157">Soyadı</span><span class="sxs-lookup"><span data-stu-id="90b75-157">LastName</span></span></th>
<th><span data-ttu-id="90b75-158">Yaş</span><span class="sxs-lookup"><span data-stu-id="90b75-158">Age</span></span></th>
<th><span data-ttu-id="90b75-159">E-posta</span><span class="sxs-lookup"><span data-stu-id="90b75-159">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="90b75-160">Ken</span><span class="sxs-lookup"><span data-stu-id="90b75-160">Ken</span></span></td>
<td><span data-ttu-id="90b75-161">Kwok</span><span class="sxs-lookup"><span data-stu-id="90b75-161">Kwok</span></span></td>
<td><span data-ttu-id="90b75-162">23</span><span class="sxs-lookup"><span data-stu-id="90b75-162">23</span></span></td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


<span data-ttu-id="90b75-163">Şu ana kadar bu zorunlu sütunları ve öğeleri aynı tabloda birden çok varlık türleri Depolama olanağı temel farklılıklar ile ilişkisel bir veritabanındaki bir tablo için çok benzer görünür.</span><span class="sxs-lookup"><span data-stu-id="90b75-163">So far, this looks very similar to a table in a relational database with the key differences being the mandatory columns, and the ability to store multiple entity types in the same table.</span></span> <span data-ttu-id="90b75-164">Ayrıca, her kullanıcı tarafından tanımlanan özellikler gibi **FirstName** veya **yaş** tamsayı veya dize, yalnızca gibi ilişkisel bir veritabanındaki sütun gibi bir veri türüne sahip.</span><span class="sxs-lookup"><span data-stu-id="90b75-164">In addition, each of the user-defined properties such as **FirstName** or **Age** has a data type, such as integer or string, just like a column in a relational database.</span></span> <span data-ttu-id="90b75-165">Farklı bir ilişkisel veritabanı içinde tablo hizmeti şema daha az yapısını bir özellik aynı veri her varlığın türü olması gerekmez, ancak.</span><span class="sxs-lookup"><span data-stu-id="90b75-165">Although unlike in a relational database, the schema-less nature of the Table service means that a property need not have the same data type on each entity.</span></span> <span data-ttu-id="90b75-166">Karmaşık veri türleri tek bir özellikte depolamak için JSON veya XML gibi serileştirilmiş bir format kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-166">To store complex data types in a single property, you must use a serialized format such as JSON or XML.</span></span> <span data-ttu-id="90b75-167">Tablo hizmeti gibi desteklenen veri türleri, desteklenen bir tarih aralıkları, adlandırma kuralları ve boyutu kısıtlamaları hakkında daha fazla bilgi için bkz: [tablo hizmeti veri modelini anlama](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="90b75-167">For more information about the table service such as supported data types, supported date ranges, naming rules, and size constraints, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="90b75-168">Göreceğiniz gibi tercih ettiğiniz **PartitionKey** ve **RowKey** iyi tablo tasarımı için temel önemdedir.</span><span class="sxs-lookup"><span data-stu-id="90b75-168">As you will see, your choice of **PartitionKey** and **RowKey** is fundamental to good table design.</span></span> <span data-ttu-id="90b75-169">Bir tablodaki her varlığın benzersiz bir birleşimi olmalıdır **PartitionKey** ve **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="90b75-169">Every entity stored in a table must have a unique combination of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="90b75-170">Bir ilişkisel veritabanı tablosundaki gibi anahtarlarla **PartitionKey** ve **RowKey** değerleri hızlı göz atmayı sağlayan bir kümelenmiş dizin oluşturmak için dizine; bunlar yalnızca iki dizin oluşturulmuş özellikleri (daha sonra açıklanan desenleri bazıları Göster görünen bu sınırlamaya geçici nasıl çalışır); bu nedenle ancak, tablo hizmeti tüm ikincil dizinlerin oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="90b75-170">As with keys in a relational database table, the **PartitionKey** and **RowKey** values are indexed to create a clustered index that enables fast look-ups; however, the Table service does not create any secondary indexes so these are the only two indexed properties (some of the patterns described later show how you can work around this apparent limitation).</span></span>  

<span data-ttu-id="90b75-171">Bir tablo bir veya daha fazla bölümlerini yapılır ve göreceğiniz gibi birçok tasarım kararları uygun bir seçme geçici bir çözüm olacaktır **PartitionKey** ve **RowKey** çözümünüzü en iyi duruma getirme.</span><span class="sxs-lookup"><span data-stu-id="90b75-171">A table is made up of one or more partitions, and as you will see, many of the design decisions you make will be around choosing a suitable **PartitionKey** and **RowKey** to optimize your solution.</span></span> <span data-ttu-id="90b75-172">Tablonun tüm varlıklar bölümlere düzenlenmiş içeren yalnızca tek bir çözüm oluşabilir, ancak bir çözüm, birden çok tablo genellikle sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="90b75-172">A solution could consist of just a single table that contains all your entities organized into partitions, but typically a solution will have multiple tables.</span></span> <span data-ttu-id="90b75-173">Tablolar, mantıksal olarak varlıklarınızı düzenlemek, erişim denetim listeleri kullanarak veri erişimi yönetmenize yardımcı olmak için Yardım ve tek bir depolama işlemi kullanarak tüm bir tabloyu düşürebilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-173">Tables help you to logically organize your entities, help you manage access to the data using access control lists, and you can drop an entire table using a single storage operation.</span></span>  

### <a name="table-partitions"></a><span data-ttu-id="90b75-174">Tablo bölümleri</span><span class="sxs-lookup"><span data-stu-id="90b75-174">Table partitions</span></span>
<span data-ttu-id="90b75-175">Tablo adı, hesap adı ve **PartitionKey** birlikte tablo hizmeti, varlığı depoladığı depolama hizmeti içinde bölümü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="90b75-175">The account name, table name and **PartitionKey** together identify the partition within the storage service where the table service stores the entity.</span></span> <span data-ttu-id="90b75-176">Adres düzeni varlıklar için parçası olmasının yanı sıra, bölüm işlemleri için kapsam tanımlayın (bkz [varlık Grup hareketleri](#entity-group-transactions) aşağıda), ve tablo hizmeti nasıl ölçeklendirir temeli oluştururlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-176">As well as being part of the addressing scheme for entities, partitions define a scope for transactions (see [Entity Group Transactions](#entity-group-transactions) below), and form the basis of how the table service scales.</span></span> <span data-ttu-id="90b75-177">Bölümleri hakkında daha fazla bilgi için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="90b75-177">For more information on partitions see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span>  

<span data-ttu-id="90b75-178">Tablo hizmetinde hizmetlerini tek tek bir düğüm tek tek ya da daha fazla tamamlamak bölümler ve hizmet ölçekler dinamik Yük Dengeleme tarafından düğümleri arasında bölümler.</span><span class="sxs-lookup"><span data-stu-id="90b75-178">In the Table service, an individual node services one or more complete partitions and the service scales by dynamically load-balancing partitions across nodes.</span></span> <span data-ttu-id="90b75-179">Bir düğümü yük altında ise, tablo hizmeti için *bölme* bölümleri aralığını hizmet farklı düğümleri üzerine bu düğüm tarafından; trafiği subsides hizmet yapabilirsiniz *birleştirme* sessiz düğümleri bölüm aralığından tek bir düğüme geri.</span><span class="sxs-lookup"><span data-stu-id="90b75-179">If a node is under load, the table service can *split* the range of partitions serviced by that node onto different nodes; when traffic subsides, the service can *merge* the partition ranges from quiet nodes back onto a single node.</span></span>  

<span data-ttu-id="90b75-180">Daha fazla bilgi için iç Ayrıntılar tablo hizmetinin ve özellikle bölümleri hizmet yöneten nasıl incelemesine bakın [Microsoft Azure Storage: yüksek oranda kullanılabilir bulut depolama hizmet güçlü tutarlılık](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span><span class="sxs-lookup"><span data-stu-id="90b75-180">For more information about the internal details of the Table service, and in particular how the service manages partitions, see the paper [Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span></span>  

### <a name="entity-group-transactions"></a><span data-ttu-id="90b75-181">Varlık Grup işlemleri</span><span class="sxs-lookup"><span data-stu-id="90b75-181">Entity Group Transactions</span></span>
<span data-ttu-id="90b75-182">Tablo hizmetinde varlık Grup hareketleri (EGTs) birden çok varlık arasında atomik güncelleştirmeleri gerçekleştirmek için yalnızca yerleşik sistemdir.</span><span class="sxs-lookup"><span data-stu-id="90b75-182">In the Table service, Entity Group Transactions (EGTs) are the only built-in mechanism for performing atomic updates across multiple entities.</span></span> <span data-ttu-id="90b75-183">EGTs de denir *toplu işlemler* bazı belgelerde.</span><span class="sxs-lookup"><span data-stu-id="90b75-183">EGTs are also referred to as *batch transactions* in some documentation.</span></span> <span data-ttu-id="90b75-184">Bu varlıkların aynı bölümde olduğundan emin olmak için gereken birden çok varlık arasında atomik işlem davranışı gereken herhangi bir zamanda EGTs yalnızca aynı bölümünde (paylaşım verilen bir tablodaki aynı bölüm anahtarı) depolanan varlıklar üzerinde bunu çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-184">EGTs can only operate on entities stored in the same partition (share the same partition key in a given table), so anytime you need atomic transactional behavior across multiple entities you need to ensure that those entities are in the same partition.</span></span> <span data-ttu-id="90b75-185">Genellikle birden fazla tablo farklı varlık türlerine yönelik kullanmayan ve birden çok varlık türleri aynı tablonun (ve bölüm) tutulması için bir neden de budur.</span><span class="sxs-lookup"><span data-stu-id="90b75-185">This is often a reason for keeping multiple entity types in the same table (and partition) and not using multiple tables for different entity types.</span></span> <span data-ttu-id="90b75-186">Tek bir EGT en fazla 100 varlık üzerinde çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-186">A single EGT can operate on at most 100 entities.</span></span>  <span data-ttu-id="90b75-187">İşleme için birden çok eşzamanlı EGTs gönderirseniz bu EGTs, aksi takdirde işleme Gecikmeli olarak EGTs arasında ortak olan varlıklar üzerinde çalıştırmayın emin olmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="90b75-187">If you submit multiple concurrent EGTs for processing it is important to ensure  those EGTs do not operate on entities that are common across EGTs as otherwise processing can be delayed.</span></span>

<span data-ttu-id="90b75-188">EGTs de tasarımınızda değerlendirebilmeniz için olası dengelemeyi tanıtmak: daha fazla bölüm kullanarak artıracaktır ölçeklenebilirlik, uygulamanızın Azure düğümleri arasında dengelemesini istekleri için daha fazla fırsatlarını sahiptir, ancak bu atomik işlemleri gerçekleştirmek ve verileriniz için güçlü tutarlılık sağlamak için uygulamanızın özelliğini sınırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-188">EGTs also introduce a potential trade-off for you to evaluate in your design: using more partitions will increase the scalability of your application because Azure has more opportunities for load balancing requests across nodes, but this might limit the ability of your application to perform atomic transactions and maintain strong consistency for your data.</span></span> <span data-ttu-id="90b75-189">Ayrıca, vardır belirli ölçeklenebilirlik hedefleri için tek bir düğüm beklediğiniz işlemleri verimini sınırlayabilir bir bölümün düzeyinde: Azure depolama hesapları ve tablo hizmeti ölçeklenebilirlik hedefleri hakkında daha fazla bilgi için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="90b75-189">Furthermore, there are specific scalability targets at the level of a partition that might limit the throughput of transactions you can expect for a single node: for more information about the scalability targets for Azure storage accounts and the table service, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="90b75-190">Bu kılavuzun sonraki bölümlerde ele çeşitli yardımcı stratejileri dengelemeler bunun gibi yönetmek ve istemci uygulamanızı belirli gereksinimlerine bağlı olarak, bölüm anahtarı seçmek için en iyi şekilde nasıl ele tasarım.</span><span class="sxs-lookup"><span data-stu-id="90b75-190">Later sections of this guide discuss various design strategies that help you manage trade-offs such as this one, and discuss how best to choose your partition key based on the specific requirements of your client application.</span></span>  

### <a name="capacity-considerations"></a><span data-ttu-id="90b75-191">Kapasite dikkat edilecek noktalar</span><span class="sxs-lookup"><span data-stu-id="90b75-191">Capacity considerations</span></span>
<span data-ttu-id="90b75-192">Aşağıdaki tabloda bazı ne zaman, bir tablo hizmeti çözümü tasarlarken bulundurmanız anahtar değerleri içerir:</span><span class="sxs-lookup"><span data-stu-id="90b75-192">The following table includes some of the key values to be aware of when you are designing a Table service solution:</span></span>  

| <span data-ttu-id="90b75-193">Bir Azure depolama hesabının toplam kapasite</span><span class="sxs-lookup"><span data-stu-id="90b75-193">Total capacity of an Azure storage account</span></span> | <span data-ttu-id="90b75-194">500 TB</span><span class="sxs-lookup"><span data-stu-id="90b75-194">500 TB</span></span> |
| --- | --- |
| <span data-ttu-id="90b75-195">Bir Azure depolama hesabı tablo sayısı</span><span class="sxs-lookup"><span data-stu-id="90b75-195">Number of tables in an Azure storage account</span></span> |<span data-ttu-id="90b75-196">Depolama hesabı kapasitesini yalnızca sınırlıdır</span><span class="sxs-lookup"><span data-stu-id="90b75-196">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="90b75-197">Bir tabloda bölüm sayısı</span><span class="sxs-lookup"><span data-stu-id="90b75-197">Number of partitions in a table</span></span> |<span data-ttu-id="90b75-198">Depolama hesabı kapasitesini yalnızca sınırlıdır</span><span class="sxs-lookup"><span data-stu-id="90b75-198">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="90b75-199">Bir bölümdeki varlıkların sayısı</span><span class="sxs-lookup"><span data-stu-id="90b75-199">Number of entities in a partition</span></span> |<span data-ttu-id="90b75-200">Depolama hesabı kapasitesini yalnızca sınırlıdır</span><span class="sxs-lookup"><span data-stu-id="90b75-200">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="90b75-201">Tek bir varlık boyutu</span><span class="sxs-lookup"><span data-stu-id="90b75-201">Size of an individual entity</span></span> |<span data-ttu-id="90b75-202">En çok 1 MB ile en fazla 255 özellikleri (de dahil olmak üzere **PartitionKey**, **RowKey**, ve **zaman damgası**)</span><span class="sxs-lookup"><span data-stu-id="90b75-202">Up to 1 MB with a maximum of 255 properties (including the **PartitionKey**, **RowKey**, and **Timestamp**)</span></span> |
| <span data-ttu-id="90b75-203">Boyutunu **PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="90b75-203">Size of the **PartitionKey**</span></span> |<span data-ttu-id="90b75-204">Dizenin en çok 1 KB boyutunda</span><span class="sxs-lookup"><span data-stu-id="90b75-204">A string up to 1 KB in size</span></span> |
| <span data-ttu-id="90b75-205">Boyutunu **RowKey**</span><span class="sxs-lookup"><span data-stu-id="90b75-205">Size of the **RowKey**</span></span> |<span data-ttu-id="90b75-206">Dizenin en çok 1 KB boyutunda</span><span class="sxs-lookup"><span data-stu-id="90b75-206">A string up to 1 KB in size</span></span> |
| <span data-ttu-id="90b75-207">Bir varlık grubu işlem boyutu</span><span class="sxs-lookup"><span data-stu-id="90b75-207">Size of an Entity Group Transaction</span></span> |<span data-ttu-id="90b75-208">Bir işlem en fazla 100 varlık içerebilir ve yükü boyutu 4 MB'den az olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-208">A transaction can include at most 100 entities and the payload must be less than 4 MB in size.</span></span> <span data-ttu-id="90b75-209">Bir EGT yalnızca bir kez bir varlık güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-209">An EGT can only update an entity once.</span></span> |

<span data-ttu-id="90b75-210">Daha fazla bilgi için bkz: [tablo hizmeti veri modelini anlama](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="90b75-210">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>  

### <a name="cost-considerations"></a><span data-ttu-id="90b75-211">Maliyet dikkat edilecek noktalar</span><span class="sxs-lookup"><span data-stu-id="90b75-211">Cost considerations</span></span>
<span data-ttu-id="90b75-212">Tablo depolama oldukça masrafsız, ancak kapasite kullanımı ve hareketlerinin miktarı için maliyet tahminleri değerlendirmenize tablo hizmeti kullanan herhangi bir çözümünün bir parçası olarak içermelidir.</span><span class="sxs-lookup"><span data-stu-id="90b75-212">Table storage is relatively inexpensive, but you should include cost estimates for both capacity usage and the quantity of transactions as part of your evaluation of any solution that uses the Table service.</span></span> <span data-ttu-id="90b75-213">Ancak, geliştirmek için Normalleştirilmemiş veya yinelenen veri depolama birçok senaryolarda performansı veya ölçeklenebilirliği çözümünüzün yapılacak bir geçerli yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-213">However, in many scenarios storing denormalized or duplicate data in order to improve the performance or scalability of your solution is a valid approach to take.</span></span> <span data-ttu-id="90b75-214">Fiyatlandırma hakkında daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="90b75-214">For more information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>  

## <a name="guidelines-for-table-design"></a><span data-ttu-id="90b75-215">Tablo Tasarımı için yönergeler</span><span class="sxs-lookup"><span data-stu-id="90b75-215">Guidelines for table design</span></span>
<span data-ttu-id="90b75-216">Bu listeler tablolarınızı tasarlarken göz önünde bulundurmanız gereken anahtar yönergeleri bazıları özetlemek ve bu kılavuzda bunları daha ayrıntılı daha sonra da değerlendirecektir.</span><span class="sxs-lookup"><span data-stu-id="90b75-216">These lists summarize some of the key guidelines you should keep in mind when you are designing your tables, and this guide will address them all in more detail later in.</span></span> <span data-ttu-id="90b75-217">Bu yönergeler, ilişkisel veritabanı tasarımı için genellikle izlersiniz yönergeleri çok farklıdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-217">These guidelines are very different from the guidelines you would typically follow for relational database design.</span></span>  

<span data-ttu-id="90b75-218">Olması için tablo hizmeti çözümünüzü tasarlama *okuma* verimli:</span><span class="sxs-lookup"><span data-stu-id="90b75-218">Designing your Table service solution to be *read* efficient:</span></span>

* <span data-ttu-id="90b75-219">***Okuma ağır uygulamalarda sorgulamaya tasarlayın.***</span><span class="sxs-lookup"><span data-stu-id="90b75-219">***Design for querying in read-heavy applications.***</span></span> <span data-ttu-id="90b75-220">Tabloları tasarlarken, yürütecek sorguları hakkında (özellikle önemli olanları gecikme) düşündüğünüz varlıklarınızı nasıl güncelleştirecektir hakkında düşünmek önce.</span><span class="sxs-lookup"><span data-stu-id="90b75-220">When you are designing your tables, think about the queries (especially the latency sensitive ones) that you will execute before you think about how you will update your entities.</span></span> <span data-ttu-id="90b75-221">Bu genellikle bir verimli ve kullanıcı çözümde sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-221">This typically results in an efficient and performant solution.</span></span>  
* <span data-ttu-id="90b75-222">***PartitionKey ve RowKey sorgularınızda belirtin.***</span><span class="sxs-lookup"><span data-stu-id="90b75-222">***Specify both PartitionKey and RowKey in your queries.***</span></span> <span data-ttu-id="90b75-223">*Noktası sorguları* en verimli tablo hizmeti sorguları bunlar gibi.</span><span class="sxs-lookup"><span data-stu-id="90b75-223">*Point queries* such as these are the most efficient table service queries.</span></span>  
* <span data-ttu-id="90b75-224">***Varlıkları yinelenen kopyalarını depolamayı düşünün.***</span><span class="sxs-lookup"><span data-stu-id="90b75-224">***Consider storing duplicate copies of entities.***</span></span> <span data-ttu-id="90b75-225">Tablo depolama ucuz böylece daha verimli sorguları etkinleştirmek için birden çok kez (anahtarları farklı) aynı varlığa depolama göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="90b75-225">Table storage is cheap so consider storing the same entity multiple times (with different keys) to enable more efficient queries.</span></span>  
* <span data-ttu-id="90b75-226">***Verilerinizi denormalizing göz önünde bulundurun.***</span><span class="sxs-lookup"><span data-stu-id="90b75-226">***Consider denormalizing your data.***</span></span> <span data-ttu-id="90b75-227">Tablo depolama ucuz böylece verilerinizi denormalizing göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="90b75-227">Table storage is cheap so consider denormalizing your data.</span></span> <span data-ttu-id="90b75-228">Örneğin, veri toplama için sorgular yalnızca tek bir varlık erişmesi gereken şekilde Özet varlıklar depolayın.</span><span class="sxs-lookup"><span data-stu-id="90b75-228">For example, store summary entities so that queries for aggregate data only need to access a single entity.</span></span>  
* <span data-ttu-id="90b75-229">***Bileşik anahtar değerlerini kullanın.***</span><span class="sxs-lookup"><span data-stu-id="90b75-229">***Use compound key values.***</span></span> <span data-ttu-id="90b75-230">Sahip olduğunuz yalnızca anahtarlar **PartitionKey** ve **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="90b75-230">The only keys you have are **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="90b75-231">Örneğin, bileşik anahtar değerlerinden varlıklar için alternatif anahtarlı erişim yolları etkinleştirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="90b75-231">For example, use compound key values to enable alternate keyed access paths to entities.</span></span>  
* <span data-ttu-id="90b75-232">***Sorgu projeksiyon kullanın.***</span><span class="sxs-lookup"><span data-stu-id="90b75-232">***Use query projection.***</span></span> <span data-ttu-id="90b75-233">Gereksinim alanları seçin sorgularını kullanarak ağ üzerinden aktarım veri miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="90b75-233">You can reduce the amount of data that you transfer over the network by using queries that select just the fields you need.</span></span>  

<span data-ttu-id="90b75-234">Olması için tablo hizmeti çözümünüzü tasarlama *yazma* verimli:</span><span class="sxs-lookup"><span data-stu-id="90b75-234">Designing your Table service solution to be *write* efficient:</span></span>  

* <span data-ttu-id="90b75-235">***Sık kullanılan bölümleri oluşturmayın.***</span><span class="sxs-lookup"><span data-stu-id="90b75-235">***Do not create hot partitions.***</span></span> <span data-ttu-id="90b75-236">İsteklerinizi birden çok bölüm zaman herhangi bir noktada üzerinden yayılan sağlayan anahtarları'i seçin.</span><span class="sxs-lookup"><span data-stu-id="90b75-236">Choose keys that enable you to spread your requests across multiple partitions at any point of time.</span></span>  
* <span data-ttu-id="90b75-237">***Ani trafiğinin kaçının.***</span><span class="sxs-lookup"><span data-stu-id="90b75-237">***Avoid spikes in traffic.***</span></span> <span data-ttu-id="90b75-238">Trafiği makul bir süre boyunca kesintisiz ve ani trafiğinin kaçının.</span><span class="sxs-lookup"><span data-stu-id="90b75-238">Smooth the traffic over a reasonable period of time and avoid spikes in traffic.</span></span>
* <span data-ttu-id="90b75-239">***Her varlık türü için ayrı bir tablo mutlaka oluşturmayın.***</span><span class="sxs-lookup"><span data-stu-id="90b75-239">***Don't necessarily create a separate table for each type of entity.***</span></span> <span data-ttu-id="90b75-240">Varlık türlerine atomik işlemleri gerektirdiğinde bu birden çok varlık türleri aynı tabloda aynı bölüm depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-240">When you require atomic transactions across entity types, you can store these multiple entity types in the same partition in the same table.</span></span>
* <span data-ttu-id="90b75-241">***En yüksek verimlilik elde gerekir göz önünde bulundurun.***</span><span class="sxs-lookup"><span data-stu-id="90b75-241">***Consider the maximum throughput you must achieve.***</span></span> <span data-ttu-id="90b75-242">Tablo hizmeti ölçeklenebilirlik hedefleri farkında olmanız ve tasarımınızı, bunları aşmasına neden olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-242">You must be aware of the scalability targets for the Table service and ensure that your design will not cause you to exceed them.</span></span>  

<span data-ttu-id="90b75-243">Bu kılavuzu okumadan gibi tüm bu ilkeler uygulamaya koymanın örnekler görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="90b75-243">As you read this guide, you will see examples that put all of these principles into practice.</span></span>  

## <a name="design-for-querying"></a><span data-ttu-id="90b75-244">Sorgulama için Tasarım</span><span class="sxs-lookup"><span data-stu-id="90b75-244">Design for querying</span></span>
<span data-ttu-id="90b75-245">Tablo hizmeti çözümleri yoğun, yazma yoğun veya ikisinin bir karışımı okuyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-245">Table service solutions may be read intensive, write intensive, or a mix of the two.</span></span> <span data-ttu-id="90b75-246">Bu bölümde, okuma işlemleri verimli bir şekilde desteklemek için tablo hizmeti tasarlarken de hesaba katılmalıdır gerekenler odaklanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-246">This section focuses on the things to bear in mind when you are designing your Table service to support read operations efficiently.</span></span> <span data-ttu-id="90b75-247">Genellikle, desteklediği işlemleri verimli bir şekilde okuma tasarım de yazma işlemleri için verimli olur.</span><span class="sxs-lookup"><span data-stu-id="90b75-247">Typically, a design that supports read operations efficiently is also efficient for write operations.</span></span> <span data-ttu-id="90b75-248">Ancak, sonraki bölümde açıklanan yazma işlemlerini desteklemek için tasarlarken göz önünde ayı gereken ek noktalar vardır [veri değişikliği için tasarım](#design-for-data-modification).</span><span class="sxs-lookup"><span data-stu-id="90b75-248">However, there are additional considerations to bear in mind when designing to support write operations, discussed in the next section, [Design for data modification](#design-for-data-modification).</span></span>

<span data-ttu-id="90b75-249">"Sorguları Uygulamam tablo hizmetinden ihtiyacı olan verileri almak için yürütme gerekecek mi?" sormak için veri etkin şekilde okumanızı sağlamak için tablo hizmeti çözümünüzü tasarlamak için iyi bir başlangıç noktası değil</span><span class="sxs-lookup"><span data-stu-id="90b75-249">A good starting point for designing your Table service solution to enable you to read data efficiently is to ask "What queries will my application need to execute to retrieve the data it needs from the Table service?"</span></span>  

> [!NOTE]
> <span data-ttu-id="90b75-250">Tablo hizmeti ile zor ve pahalı daha sonra değiştirmeye olduğundan tasarım doğru Önden almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="90b75-250">With the Table service, it's important to get the design correct up front because it's difficult and expensive to change it later.</span></span> <span data-ttu-id="90b75-251">Örneğin, bir ilişkisel veritabanı genellikle dizinler yalnızca mevcut bir veritabanına ekleyerek performans sorunlarına yönelik mümkündür: Bu tablo hizmeti ile bir seçenek değil.</span><span class="sxs-lookup"><span data-stu-id="90b75-251">For example, in a relational database it's often possible to address performance issues simply by adding indexes to an existing database: this is not an option with the Table service.</span></span>  
> 
> 

<span data-ttu-id="90b75-252">Bu bölümde sorgulamak için tabloları tasarlarken çözülmesi gereken anahtar durumlara odaklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="90b75-252">This section focuses on the key issues you must address when you design your tables for querying.</span></span> <span data-ttu-id="90b75-253">Bu bölümde yer alan konuları içerir:</span><span class="sxs-lookup"><span data-stu-id="90b75-253">The topics covered in this section include:</span></span>

* [<span data-ttu-id="90b75-254">PartitionKey ve RowKey seçiminizi sorgu performansını nasıl etkilediğini</span><span class="sxs-lookup"><span data-stu-id="90b75-254">How your choice of PartitionKey and RowKey impacts query performance</span></span>](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [<span data-ttu-id="90b75-255">Uygun bir PartitionKey seçme</span><span class="sxs-lookup"><span data-stu-id="90b75-255">Choosing an appropriate PartitionKey</span></span>](#choosing-an-appropriate-partitionkey)
* [<span data-ttu-id="90b75-256">Tablo hizmeti için en iyi duruma getirme sorguları</span><span class="sxs-lookup"><span data-stu-id="90b75-256">Optimizing queries for the Table service</span></span>](#optimizing-queries-for-the-table-service)
* [<span data-ttu-id="90b75-257">Tablo hizmetinde verileri sıralama</span><span class="sxs-lookup"><span data-stu-id="90b75-257">Sorting data in the Table service</span></span>](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a><span data-ttu-id="90b75-258">PartitionKey ve RowKey seçiminizi sorgu performansını nasıl etkilediğini</span><span class="sxs-lookup"><span data-stu-id="90b75-258">How your choice of PartitionKey and RowKey impacts query performance</span></span>
<span data-ttu-id="90b75-259">Aşağıdaki örneklerde, tablo hizmetinde şu yapıda çalışan varlıkları depolamak varsayılmaktadır (örnekler çoğunu atlayın **zaman damgası** özelliği daha anlaşılır olması için):</span><span class="sxs-lookup"><span data-stu-id="90b75-259">The following examples assume the table service is storing employee entities with the following structure (most of the examples omit the **Timestamp** property for clarity):</span></span>  

| <span data-ttu-id="90b75-260">*Sütun adı*</span><span class="sxs-lookup"><span data-stu-id="90b75-260">*Column name*</span></span> | <span data-ttu-id="90b75-261">*Veri türü*</span><span class="sxs-lookup"><span data-stu-id="90b75-261">*Data type*</span></span> |
| --- | --- |
| <span data-ttu-id="90b75-262">**PartitionKey** (bölüm adı)</span><span class="sxs-lookup"><span data-stu-id="90b75-262">**PartitionKey** (Department Name)</span></span> |<span data-ttu-id="90b75-263">Dize</span><span class="sxs-lookup"><span data-stu-id="90b75-263">String</span></span> |
| <span data-ttu-id="90b75-264">**RowKey** (çalışan kimliği)</span><span class="sxs-lookup"><span data-stu-id="90b75-264">**RowKey** (Employee Id)</span></span> |<span data-ttu-id="90b75-265">Dize</span><span class="sxs-lookup"><span data-stu-id="90b75-265">String</span></span> |
| <span data-ttu-id="90b75-266">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="90b75-266">**FirstName**</span></span> |<span data-ttu-id="90b75-267">Dize</span><span class="sxs-lookup"><span data-stu-id="90b75-267">String</span></span> |
| <span data-ttu-id="90b75-268">**Soyadı**</span><span class="sxs-lookup"><span data-stu-id="90b75-268">**LastName**</span></span> |<span data-ttu-id="90b75-269">Dize</span><span class="sxs-lookup"><span data-stu-id="90b75-269">String</span></span> |
| <span data-ttu-id="90b75-270">**Geçerlilik süresi**</span><span class="sxs-lookup"><span data-stu-id="90b75-270">**Age**</span></span> |<span data-ttu-id="90b75-271">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="90b75-271">Integer</span></span> |
| <span data-ttu-id="90b75-272">**EmailAddress**</span><span class="sxs-lookup"><span data-stu-id="90b75-272">**EmailAddress**</span></span> |<span data-ttu-id="90b75-273">Dize</span><span class="sxs-lookup"><span data-stu-id="90b75-273">String</span></span> |

<span data-ttu-id="90b75-274">Önceki bölümde [Azure Table hizmetine genel bakış](#overview) bazı Azure tablo Hizmeti sorgu tasarlama üzerinde doğrudan etkisi olan temel özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="90b75-274">The earlier section [Azure Table service overview](#overview) describes some of the key features of the Azure Table service that have a direct influence on designing for query.</span></span> <span data-ttu-id="90b75-275">Bunlar, tablo hizmeti sorguları tasarlamak için aşağıdaki genel yönergeleri sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-275">These result in the following general guidelines for designing Table service queries.</span></span> <span data-ttu-id="90b75-276">Daha fazla bilgi için tablo hizmetinden REST API'si, aşağıdaki örneklerde kullanılan filtresi sözdizimi olduğuna dikkat edin [sorgu varlıklar](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span><span class="sxs-lookup"><span data-stu-id="90b75-276">Note that the filter syntax used in the examples below is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

* <span data-ttu-id="90b75-277">A ***noktası sorgusu*** kullanmak için en verimli arama ve yüksek hacimli aramaları veya en düşük gecikme gerektiren aramalar için kullanılacak önerilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-277">A ***Point Query*** is the most efficient lookup to use and is recommended to be used for high-volume lookups or lookups requiring lowest latency.</span></span> <span data-ttu-id="90b75-278">Böyle bir sorguyu her ikisi de belirterek tek bir varlık çok verimli bir şekilde bulmak için dizinler kullanabilir **PartitionKey** ve **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-278">Such a query can use the indexes to locate an individual entity very efficiently by specifying both the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="90b75-279">Örneğin: $filter (PartitionKey eq 'Satış') = ve (RowKey eq '2')</span><span class="sxs-lookup"><span data-stu-id="90b75-279">For example: $filter=(PartitionKey eq 'Sales') and (RowKey eq '2')</span></span>  
* <span data-ttu-id="90b75-280">İkinci en iyi olan bir ***aralık sorgusu*** kullanan **PartitionKey** ve bir dizi filtreleri **RowKey** birden fazla varlık döndürülecek değer.</span><span class="sxs-lookup"><span data-stu-id="90b75-280">Second best is a ***Range Query*** that uses the **PartitionKey** and filters on a range of **RowKey** values to return more than one entity.</span></span> <span data-ttu-id="90b75-281">**PartitionKey** değer belirli bir bölüm tanımlar ve **RowKey** değerleri o bölümün varlıklarda kümesini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="90b75-281">The **PartitionKey** value identifies a specific partition, and the **RowKey** values identify a subset of the entities in that partition.</span></span> <span data-ttu-id="90b75-282">Örneğin: $filter PartitionKey eq 'Satış ve RowKey ge'nın ' ve RowKey lt 'T ='</span><span class="sxs-lookup"><span data-stu-id="90b75-282">For example: $filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'</span></span>  
* <span data-ttu-id="90b75-283">Üçüncü iyi bir ***bölüm tarama*** kullanan **PartitionKey** ve başka bir anahtar dışı özelliği ve, filtreleri, birden fazla varlık döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-283">Third best is a ***Partition Scan*** that uses the **PartitionKey** and filters on another non-key property and that may return more than one entity.</span></span> <span data-ttu-id="90b75-284">**PartitionKey** değer belirli bir bölüm tanımlar ve değerlerini özellik o bölümün varlıklarda alt kümeleri için seçin.</span><span class="sxs-lookup"><span data-stu-id="90b75-284">The **PartitionKey** value identifies a specific partition, and the property values select for a subset of the entities in that partition.</span></span> <span data-ttu-id="90b75-285">Örneğin: $filter PartitionKey eq 'Satış' ve LastName eq 'Smith' =</span><span class="sxs-lookup"><span data-stu-id="90b75-285">For example: $filter=PartitionKey eq 'Sales' and LastName eq 'Smith'</span></span>  
* <span data-ttu-id="90b75-286">A ***tablo tarama*** içermemesi **PartitionKey** ve tüm tablonuzu sırayla eşleşen tüm varlıkların oluşturan bölümlerin arar çok verimli değildir.</span><span class="sxs-lookup"><span data-stu-id="90b75-286">A ***Table Scan*** does not include the **PartitionKey** and is very inefficient because it searches all of the partitions that make up your table in turn for any matching entities.</span></span> <span data-ttu-id="90b75-287">Olsun veya olmasın, filtre kullanır, bağımsız olarak bir tablo taraması gerçekleştirecek **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="90b75-287">It will perform a table scan regardless of whether or not your filter uses the **RowKey**.</span></span> <span data-ttu-id="90b75-288">Örneğin: $filter LastName eq 'Can' =</span><span class="sxs-lookup"><span data-stu-id="90b75-288">For example: $filter=LastName eq 'Jones'</span></span>  
* <span data-ttu-id="90b75-289">Birden çok varlık döndüren sorgular bunları içinde sıralanmış dönmek **PartitionKey** ve **RowKey** sırası.</span><span class="sxs-lookup"><span data-stu-id="90b75-289">Queries that return multiple entities return them sorted in **PartitionKey** and **RowKey** order.</span></span> <span data-ttu-id="90b75-290">Varlıklar istemci yeniden ayırma önlemek için seçin bir **RowKey** en yaygın sıralama düzenini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-290">To avoid resorting the entities in the client, choose a **RowKey** that defines the most common sort order.</span></span>  

<span data-ttu-id="90b75-291">Bu kullanarak not bir "**veya**" dayalı bir filtre belirtmek için **RowKey** değerleri bir bölüm tarama sonuçları ve aralığı sorgu olarak işlenmez.</span><span class="sxs-lookup"><span data-stu-id="90b75-291">Note that using an "**or**" to specify a filter based on **RowKey** values results in a partition scan and is not treated as a range query.</span></span> <span data-ttu-id="90b75-292">Bu nedenle, filtreleri gibi kullanan sorguları kaçınmanız gerekir: $filter PartitionKey eq 'Satış' ve RowKey eq '121' = (veya RowKey eq '322')</span><span class="sxs-lookup"><span data-stu-id="90b75-292">Therefore, you should avoid queries that use filters such as: $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')</span></span>  

<span data-ttu-id="90b75-293">Verimli sorgularını yürütmek için depolama istemci kitaplığı kullanan istemci-tarafı kod örnekleri için bkz:</span><span class="sxs-lookup"><span data-stu-id="90b75-293">For examples of client-side code that use the Storage Client Library to execute efficient queries, see:</span></span>  

* [<span data-ttu-id="90b75-294">Depolama istemci kitaplığı kullanılarak noktası sorgusu yürütme</span><span class="sxs-lookup"><span data-stu-id="90b75-294">Executing a point query using the Storage Client Library</span></span>](#executing-a-point-query-using-the-storage-client-library)
* [<span data-ttu-id="90b75-295">LINQ kullanarak birden çok varlık alma</span><span class="sxs-lookup"><span data-stu-id="90b75-295">Retrieving multiple entities using LINQ</span></span>](#retrieving-multiple-entities-using-linq)
* [<span data-ttu-id="90b75-296">Sunucu tarafı projeksiyonu</span><span class="sxs-lookup"><span data-stu-id="90b75-296">Server-side projection</span></span>](#server-side-projection)  

<span data-ttu-id="90b75-297">Birden çok varlık türleri aynı tabloda depolanan işleyebilir istemci-tarafı kod örnekleri için bkz:</span><span class="sxs-lookup"><span data-stu-id="90b75-297">For examples of client-side code that can handle multiple entity types stored in the same table, see:</span></span>  

* [<span data-ttu-id="90b75-298">Heterojen varlık türleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="90b75-298">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a><span data-ttu-id="90b75-299">Uygun bir PartitionKey seçme</span><span class="sxs-lookup"><span data-stu-id="90b75-299">Choosing an appropriate PartitionKey</span></span>
<span data-ttu-id="90b75-300">Tercih ettiğiniz **PartitionKey** dengelemeniz (ölçeklenebilir bir çözüm sağlamak için) birden çok bölüm arasında varlıklarınızı dağıtmak için gereksinim karşı gerek EGTs (tutarlılığını sağlamak için) kullanılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="90b75-300">Your choice of **PartitionKey** should balance the need to enables the use of EGTs (to ensure consistency) against the requirement to distribute your entities across multiple partitions (to ensure a scalable solution).</span></span>  

<span data-ttu-id="90b75-301">Bir extreme adresindeki tüm varlıkları tek bir bölüm saklayabilirsiniz, ancak bu çözümünüzü ölçeklenebilirliğini sınırlayabilir ve tablo hizmeti Yük Dengeleme isteklerini engellemek.</span><span class="sxs-lookup"><span data-stu-id="90b75-301">At one extreme, you could store all your entities in a single partition, but this may limit the scalability of your solution and would prevent the table service from being able to load-balance requests.</span></span> <span data-ttu-id="90b75-302">Diğer uçta bu yüksek oranda ölçeklenebilir olur ve Yük Dengeleme isteklerini tablo hizmetine sağlar, ancak hangi, varlık Grup hareketleri kullanmasını önler bölüm başına tek bir varlık saklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-302">At the other extreme, you could store one entity per partition, which would be highly scalable and which enables the table service to load-balance requests, but which would prevent you from using entity group transactions.</span></span>  

<span data-ttu-id="90b75-303">İdeal **PartitionKey** verimli sorguları kullanmanıza olanak sağlayan ve çözümünüzü ölçeklenebilir olduğundan emin olmak için yeterli bölümleri olan biridir.</span><span class="sxs-lookup"><span data-stu-id="90b75-303">An ideal **PartitionKey** is one that enables you to use efficient queries and that has sufficient partitions to ensure your solution is scalable.</span></span> <span data-ttu-id="90b75-304">Genellikle, varlıklarınızı varlıklarınızı yeterli bölümler dağıtır uygun bir özellik olduğunu bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-304">Typically, you will find that your entities will have a suitable property that distributes your entities across sufficient partitions.</span></span>

> [!NOTE]
> <span data-ttu-id="90b75-305">Örneğin, kullanıcılar veya çalışanlar ilgili bilgileri depoladığı bir sistemde, iyi PartitionKey UserID olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-305">For example, in a system that stores information about users or employees, UserID may be a good PartitionKey.</span></span> <span data-ttu-id="90b75-306">Bölüm anahtarı olarak belirli bir kullanıcı kimliği kullanan birden fazla varlık sahip.</span><span class="sxs-lookup"><span data-stu-id="90b75-306">You may have several entities that use a given UserID as the partition key.</span></span> <span data-ttu-id="90b75-307">Bir kullanıcı hakkında verilerini depolayan her varlığın tek bir bölümde gruplandırılır ve bu nedenle bu varlıkları hala yüksek oranda ölçeklenebilir devam ederken varlık Grup hareketleri erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-307">Each entity that stores data about a user is grouped into a single partition, and so these entities are accessible via entity group transactions, while still being highly scalable.</span></span>
> 
> 

<span data-ttu-id="90b75-308">Tercih ettiğiniz hususlar vardır **PartitionKey** ilişkili nasıl, ekleme, güncelleştirme ve varlıkları silmek için: bölümüne bakın [veri değişikliği için tasarım](#design-for-data-modification) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="90b75-308">There are additional considerations in your choice of **PartitionKey** that relate to how you will insert, update, and delete entities: see the section [Design for data modification](#design-for-data-modification) below.</span></span>  

### <a name="optimizing-queries-for-the-table-service"></a><span data-ttu-id="90b75-309">Tablo hizmeti için en iyi duruma getirme sorguları</span><span class="sxs-lookup"><span data-stu-id="90b75-309">Optimizing queries for the Table service</span></span>
<span data-ttu-id="90b75-310">Tablo hizmeti otomatik olarak kullanarak, varlıklarınızı dizinler **PartitionKey** ve **RowKey** tek bir kümelenmiş dizin, bu nedenle sorguları noktası neden değerler kullanmak için en etkili.</span><span class="sxs-lookup"><span data-stu-id="90b75-310">The Table service automatically indexes your entities using the **PartitionKey** and **RowKey** values in a single clustered index, hence the reason that point queries are the most efficient to use.</span></span> <span data-ttu-id="90b75-311">Ancak, vardır kümelenmiş dizini dışında hiçbir dizinler **PartitionKey** ve **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="90b75-311">However, there are no indexes other than that on the clustered index on the **PartitionKey** and **RowKey**.</span></span>

<span data-ttu-id="90b75-312">Çoğu tasarımları birden çok ölçüte dayalı varlıkların aramasını etkinleştirmek için gereksinimleri karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-312">Many designs must meet requirements to enable lookup of entities based on multiple criteria.</span></span> <span data-ttu-id="90b75-313">Örneğin, e-postalar, temel çalışan varlıkları bulma çalışan kimliği ya da son adı.</span><span class="sxs-lookup"><span data-stu-id="90b75-313">For example, locating employee entities based on email, employee id, or last name.</span></span> <span data-ttu-id="90b75-314">Bölümünde aşağıdaki desenleri [tablo Tasarım desenleri](#table-design-patterns) gereksinim bu tür adres ve tablo hizmetinde ikincil dizinler sağlamaz olgu çözümüne yolları açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="90b75-314">The following patterns in the section [Table Design Patterns](#table-design-patterns) address these types of requirement and describe ways of working around the fact that the Table service does not provide secondary indexes:</span></span>  

* <span data-ttu-id="90b75-315">[İçi bölüm ikincil dizin düzeni](#intra-partition-secondary-index-pattern) -her varlık kullanan birden çok kopyalarını farklı depolama **RowKey** değerleri (aynı bölüm) etkinleştir hızlı ve verimli aramalarını kullanarak diğer sıralamalar farklı **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-315">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="90b75-316">[İkincil dizin arası bölüm düzeni](#inter-partition-secondary-index-pattern) - hızlı etkinleştirmek için ayrı bölümlere veya ayrı tablolarda farklı RowKey değerleri kullanarak her bir varlık birden çok kopyasını depolamak ve verimli aramaları ve diğer sıralama siparişleri farklı kullanarak **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-316">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="90b75-317">[Dizin varlıkları düzeni](#index-entities-pattern) -varlıklar listesi Döndür verimli aramalar etkinleştirmek için dizin varlıkları korumak.</span><span class="sxs-lookup"><span data-stu-id="90b75-317">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities to enable efficient searches that return lists of entities.</span></span>  

### <a name="sorting-data-in-the-table-service"></a><span data-ttu-id="90b75-318">Tablo hizmetinde verileri sıralama</span><span class="sxs-lookup"><span data-stu-id="90b75-318">Sorting data in the Table service</span></span>
<span data-ttu-id="90b75-319">Tablo hizmeti göre artan düzende sıralandı varlıklar döndürüyor **PartitionKey** ve sonra **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="90b75-319">The Table service returns entities sorted in ascending order based on **PartitionKey** and then by **RowKey**.</span></span> <span data-ttu-id="90b75-320">Bu anahtarları dize değerlerini ve sayısal değerleri doğru sıralamak emin olmak için sabit bir uzunluğa Dönüştür sıfırlarla doldurur.</span><span class="sxs-lookup"><span data-stu-id="90b75-320">These keys are string values and to ensure that numeric values sort correctly, you should convert them to a fixed length and pad them with zeroes.</span></span> <span data-ttu-id="90b75-321">Örneğin, çalışan kimlik değeri olarak kullanırsanız, **RowKey** bir tamsayı değeri çalışan kimliği dönüştürmeniz gerekir **123** için **00000123**.</span><span class="sxs-lookup"><span data-stu-id="90b75-321">For example, if the employee id value you use as the **RowKey** is an integer value, you should convert employee id **123** to **00000123**.</span></span>  

<span data-ttu-id="90b75-322">Birçok uygulama farklı siparişler sıralanmış veri kullanımı için gereksinimler vardır: Örneğin, çalışanlar ada göre ya da tarih katılarak sıralama.</span><span class="sxs-lookup"><span data-stu-id="90b75-322">Many applications have requirements to use data sorted in different orders: for example, sorting employees by name, or by joining date.</span></span> <span data-ttu-id="90b75-323">Bölümünde aşağıdaki desenleri [tablo Tasarım desenleri](#table-design-patterns) sıralamalar varlıklarınızı için alternatif nasıl adresi:</span><span class="sxs-lookup"><span data-stu-id="90b75-323">The following patterns in the section [Table Design Patterns](#table-design-patterns) address how to alternate sort orders for your entities:</span></span>  

* <span data-ttu-id="90b75-324">[İçi bölüm ikincil dizin düzeni](#intra-partition-secondary-index-pattern) - hızlı etkinleştirmek için (aynı bölümde) farklı RowKey değerleri kullanarak her bir varlık birden çok kopyasını depolamak ve verimli aramaları ve diğer sıralama siparişleri farklı RowKey değerleri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="90b75-324">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>  
* <span data-ttu-id="90b75-325">[İkincil dizin arası bölüm düzeni](#inter-partition-secondary-index-pattern) - hızlı etkinleştirmek için ayrı tablolarda ayrı bölümlerdeki farklı RowKey değerleri kullanarak her bir varlık birden çok kopyasını depolamak ve verimli aramaları ve diğer sıralama siparişleri farklı RowKey değerleri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="90b75-325">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions in separate tables to enable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>
* <span data-ttu-id="90b75-326">[Günlük tail düzeni](#log-tail-pattern) -almak  *n*  kullanılarak bir bölüm için en son eklenen varlıklar bir **RowKey** ters tarihi ve saati sipariş sıralar değeri.</span><span class="sxs-lookup"><span data-stu-id="90b75-326">[Log tail pattern](#log-tail-pattern) - Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="design-for-data-modification"></a><span data-ttu-id="90b75-327">Veri değişikliği için Tasarım</span><span class="sxs-lookup"><span data-stu-id="90b75-327">Design for data modification</span></span>
<span data-ttu-id="90b75-328">Bu bölümde ekler, güncelleştirmeleri, en iyi duruma getirme için tasarım konuları odaklanır ve siler.</span><span class="sxs-lookup"><span data-stu-id="90b75-328">This section focuses on the design considerations for optimizing inserts, updates, and deletes.</span></span> <span data-ttu-id="90b75-329">Bazı durumlarda (Tasarım dengelemeler yönetmek için kullanılan teknikleri ilişkisel bir veritabanında farklı olmasına rağmen) tasarımlarına ilişkisel veritabanları için yaptığınız gibi veri değişikliği için en iyi duruma getirme tasarımlarını karşı sorgulamak için en iyi duruma getirme tasarımları arasındaki dengelemeyi değerlendirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-329">In some cases, you will need to evaluate the trade-off between designs that optimize for querying against designs that optimize for data modification just as you do in designs for relational databases (although the techniques for managing the design trade-offs are different in a relational database).</span></span> <span data-ttu-id="90b75-330">Bölüm [tablo Tasarım desenleri](#table-design-patterns) tablo hizmeti için bazı ayrıntılı tasarım desenleri açıklar ve bazı bu dengelemeler vurgular.</span><span class="sxs-lookup"><span data-stu-id="90b75-330">The section [Table Design Patterns](#table-design-patterns) describes some detailed design patterns for the Table service and highlights some these trade-offs.</span></span> <span data-ttu-id="90b75-331">Uygulamada, varlıkları iyi değiştirmek için varlıkları sorgulamak için en iyi duruma getirilmiş çoğu tasarımları da iş bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="90b75-331">In practice, you will find that many designs optimized for querying entities also work well for modifying entities.</span></span>  

### <a name="optimizing-the-performance-of-insert-update-and-delete-operations"></a><span data-ttu-id="90b75-332">Performansı en iyi duruma getirme, ekleme, güncelleştirme ve silme işlemleri</span><span class="sxs-lookup"><span data-stu-id="90b75-332">Optimizing the performance of insert, update, and delete operations</span></span>
<span data-ttu-id="90b75-333">Güncelleştirmek veya bir varlığı silmek için kullanarak tanımlayabilir olmalıdır **PartitionKey** ve **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-333">To update or delete an entity, you must be able to identify it by using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="90b75-334">Bu açısından, tercih ettiğiniz **PartitionKey** ve **RowKey** varlıklar değiştirme benzer ölçütleri varlıkları mümkün olduğunca verimli bir şekilde tanımlamak istediğiniz için noktası sorguları desteklemek için tercih ettiğiniz için izlemeniz gereken için.</span><span class="sxs-lookup"><span data-stu-id="90b75-334">In this respect, your choice of **PartitionKey** and **RowKey** for modifying entities should follow similar criteria to your choice to support point queries because you want to identify entities as efficiently as possible.</span></span> <span data-ttu-id="90b75-335">Verimsiz bir bölüm veya tablo taraması bulmak üzere bir varlık bulmak için kullanmak istediğiniz değil **PartitionKey** ve **RowKey** değerleri güncelleştirmek veya silmek için gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-335">You do not want to use an inefficient partition or table scan to locate an entity in order to discover the **PartitionKey** and **RowKey** values you need to update or delete it.</span></span>  

<span data-ttu-id="90b75-336">Bölümünde aşağıdaki desenleri [tablo Tasarım desenleri](#table-design-patterns) adres iyileştirme performans veya ekleme, güncelleştirme ve silme işlemleri:</span><span class="sxs-lookup"><span data-stu-id="90b75-336">The following patterns in the section [Table Design Patterns](#table-design-patterns) address optimizing the performance or your insert, update, and delete operations:</span></span>  

* <span data-ttu-id="90b75-337">[Yüksek hacimli silme düzeni](#high-volume-delete-pattern) -kendi ayrı tabloda eşzamanlı silme işlemi için tüm varlıkları depolayarak varlıklar yüksek hacimli silinmesini sağlar; tablo silerek varlıklarını silme.</span><span class="sxs-lookup"><span data-stu-id="90b75-337">[High volume delete pattern](#high-volume-delete-pattern) - Enable the deletion of a high volume of entities by storing all the entities for simultaneous deletion in their own separate table; you delete the entities by deleting the table.</span></span>  
* <span data-ttu-id="90b75-338">[Veri serisi deseni](#data-series-pattern) -deposu tam veri serisi içindeki yaptığınız istek sayısını en aza indirmek için tek bir varlık.</span><span class="sxs-lookup"><span data-stu-id="90b75-338">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity to minimize the number of requests you make.</span></span>  
* <span data-ttu-id="90b75-339">[Geniş varlıklar düzeni](#wide-entities-pattern) -birden çok 252 özellik sahip mantıksal varlık depolamak için birden çok fiziksel varlık kullanın.</span><span class="sxs-lookup"><span data-stu-id="90b75-339">[Wide entities pattern](#wide-entities-pattern) - Use multiple physical entities to store logical entities with more than 252 properties.</span></span>  
* <span data-ttu-id="90b75-340">[Büyük varlıklar düzeni](#large-entities-pattern) -büyük özellik değerlerini depolamak için blob depolama kullanın.</span><span class="sxs-lookup"><span data-stu-id="90b75-340">[Large entities pattern](#large-entities-pattern) - Use blob storage to store large property values.</span></span>  

### <a name="ensuring-consistency-in-your-stored-entities"></a><span data-ttu-id="90b75-341">Saklı varlıklarınızı tutarlılık sağlama</span><span class="sxs-lookup"><span data-stu-id="90b75-341">Ensuring consistency in your stored entities</span></span>
<span data-ttu-id="90b75-342">Veri değişiklikleri iyileştirmek için anahtarların tercih ettiğiniz etkileyen diğer anahtar atomik işlemleri kullanarak tutarlılığını sağlamak nasıl faktördür.</span><span class="sxs-lookup"><span data-stu-id="90b75-342">The other key factor that influences your choice of keys for optimizing data modifications is how to ensure consistency by using atomic transactions.</span></span> <span data-ttu-id="90b75-343">Yalnızca bir EGT aynı bölümünde depolanan varlıklar üzerinde çalışması için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-343">You can only use an EGT to operate on entities stored in the same partition.</span></span>  

<span data-ttu-id="90b75-344">Bölümünde aşağıdaki desenleri [tablo Tasarım desenleri](#table-design-patterns) tutarlılık yönetme adresi:</span><span class="sxs-lookup"><span data-stu-id="90b75-344">The following patterns in the section [Table Design Patterns](#table-design-patterns) address managing consistency:</span></span>  

* <span data-ttu-id="90b75-345">[İçi bölüm ikincil dizin düzeni](#intra-partition-secondary-index-pattern) -her varlık kullanan birden çok kopyalarını farklı depolama **RowKey** değerleri (aynı bölüm) etkinleştir hızlı ve verimli aramalarını kullanarak diğer sıralamalar farklı **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-345">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="90b75-346">[İkincil dizin arası bölüm düzeni](#inter-partition-secondary-index-pattern) - hızlı etkinleştirmek için ayrı bölümlere veya ayrı tablolarda farklı RowKey değerleri kullanarak her bir varlık birden çok kopyasını depolamak ve verimli aramaları ve diğer sıralama siparişleri farklı kullanarak **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-346">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="90b75-347">[Sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern) -etkinleştirmek sonuçta tutarlı davranış bölüm sınırları veya depolama sistemi sınırları boyunca Azure sıraları kullanarak.</span><span class="sxs-lookup"><span data-stu-id="90b75-347">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) - Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>
* <span data-ttu-id="90b75-348">[Dizin varlıkları düzeni](#index-entities-pattern) -varlıklar listesi Döndür verimli aramalar etkinleştirmek için dizin varlıkları korumak.</span><span class="sxs-lookup"><span data-stu-id="90b75-348">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities to enable efficient searches that return lists of entities.</span></span>  
* <span data-ttu-id="90b75-349">[Denormalization deseni](#denormalization-pattern) -birleştirme ilgili verileri birlikte tek nokta sorguyla gereken tüm verileri almak üzere etkinleştirmek için tek bir varlık olarak.</span><span class="sxs-lookup"><span data-stu-id="90b75-349">[Denormalization pattern](#denormalization-pattern) - Combine related data together in a single entity to enable you to retrieve all the data you need with a single point query.</span></span>  
* <span data-ttu-id="90b75-350">[Veri serisi deseni](#data-series-pattern) -deposu tam veri serisi içindeki yaptığınız istek sayısını en aza indirmek için tek bir varlık.</span><span class="sxs-lookup"><span data-stu-id="90b75-350">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity to minimize the number of requests you make.</span></span>  

<span data-ttu-id="90b75-351">Varlık Grup işlemler hakkında daha fazla bilgi için bkz [varlık Grup hareketleri](#entity-group-transactions).</span><span class="sxs-lookup"><span data-stu-id="90b75-351">For information about entity group transactions, see the section [Entity Group Transactions](#entity-group-transactions).</span></span>  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a><span data-ttu-id="90b75-352">Tasarımınız etkili değişiklikler için sağlama verimli sorguları kolaylaştırır</span><span class="sxs-lookup"><span data-stu-id="90b75-352">Ensuring your design for efficient modifications facilitates efficient queries</span></span>
<span data-ttu-id="90b75-353">Çoğu durumda, bunun belirli senaryonuz için geçerli olup olmadığını tasarım etkili değişiklikler, ancak sorgulama verimli sonuçlar için her zaman değerlendirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-353">In many cases, a design for efficient querying results in efficient modifications, but you should always evaluate whether this is the case for your specific scenario.</span></span> <span data-ttu-id="90b75-354">Bazı bölümünde desenleri [tablo Tasarım desenleri](#table-design-patterns) açıkça sorgulama ve varlıkları değiştirme arasındaki dengelemeler değerlendirin ve her zaman her türden işlem sayısını dikkate almanız.</span><span class="sxs-lookup"><span data-stu-id="90b75-354">Some of the patterns in the section [Table Design Patterns](#table-design-patterns) explicitly evaluate trade-offs between querying and modifying entities, and you should always take into account the number of each type of operation.</span></span>  

<span data-ttu-id="90b75-355">Bölümünde aşağıdaki desenleri [tablo Tasarım desenleri](#table-design-patterns) adres için verimli sorguları tasarlama ve verimli veri değişikliği için tasarlama arasındaki dengelemeler:</span><span class="sxs-lookup"><span data-stu-id="90b75-355">The following patterns in the section [Table Design Patterns](#table-design-patterns) address trade-offs between designing for efficient queries and designing for efficient data modification:</span></span>  

* <span data-ttu-id="90b75-356">[Bileşik anahtar düzeni](#compound-key-pattern) -kullanım bileşik **RowKey** tek nokta sorgu ile ilgili veri aramak bir istemci etkinleştirmek için değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-356">[Compound key pattern](#compound-key-pattern) - Use compound **RowKey** values to enable a client to lookup related data with a single point query.</span></span>  
* <span data-ttu-id="90b75-357">[Günlük tail düzeni](#log-tail-pattern) -almak  *n*  kullanılarak bir bölüm için en son eklenen varlıklar bir **RowKey** ters tarihi ve saati sipariş sıralar değeri.</span><span class="sxs-lookup"><span data-stu-id="90b75-357">[Log tail pattern](#log-tail-pattern) - Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="encrypting-table-data"></a><span data-ttu-id="90b75-358">Tablo verileri şifreleme</span><span class="sxs-lookup"><span data-stu-id="90b75-358">Encrypting Table Data</span></span>
<span data-ttu-id="90b75-359">.NET Azure Storage istemci kitaplığı dizesi varlık özellikleri şifrelenmesi için INSERT destekler ve değiştirme işlemlerini.</span><span class="sxs-lookup"><span data-stu-id="90b75-359">The .NET Azure Storage Client Library supports encryption of string entity properties for insert and replace operations.</span></span> <span data-ttu-id="90b75-360">Şifrelenmiş dizelerin hizmette ikili özellikleri olarak depolanır ve şifre çözme sonra dizelere geri dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="90b75-360">The encrypted strings are stored on the service as binary properties, and they are converted back to strings after decryption.</span></span>    

<span data-ttu-id="90b75-361">Şifreleme İlkesi yanı sıra, tablolar için kullanıcıların şifrelenecek özelliklerini belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-361">For tables, in addition to the encryption policy, users must specify the properties to be encrypted.</span></span> <span data-ttu-id="90b75-362">Bu, ya da bir [EncryptProperty] özniteliği (için TableEntity türetilen POCO varlıklar) veya bir şifreleme çözümleyici isteği seçenekleri belirterek yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-362">This can be done by either specifying an [EncryptProperty] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span></span> <span data-ttu-id="90b75-363">Bir şifreleme çözümleyici bölüm anahtarı, satır anahtarını ve özellik adını alır ve bu özellik şifrelenmesi gerekip gerekmediğini belirten bir Boole değeri döndüren bir temsilci ' dir.</span><span class="sxs-lookup"><span data-stu-id="90b75-363">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a Boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="90b75-364">Şifreleme sırasında istemci kitaplığı, bir özellik için kablo yazılırken şifrelenmesi gerekip gerekmediğine karar vermek için bu bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-364">During encryption, the client library will use this information to decide whether a property should be encrypted while writing to the wire.</span></span> <span data-ttu-id="90b75-365">Temsilci özellikler nasıl şifrelenir geçici mantığı olasılığı için de sağlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-365">The delegate also provides for the possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="90b75-366">(Örneğin, X ise ardından özelliği A şifrelemek; Aksi takdirde özellikleri A ve b şifreleme) Bu bilgileri okurken veya varlıkları sorgulamak için gerekli olmadığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="90b75-366">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary to provide this information while reading or querying entities.</span></span>

<span data-ttu-id="90b75-367">Bu birleştirme şu anda desteklenmeyen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="90b75-367">Note that merge is not currently supported.</span></span> <span data-ttu-id="90b75-368">Bir alt özellikler kümesini daha önce farklı bir anahtar kullanılarak şifrelenmiş olabilecek olduğundan, sadece yeni özellikleri birleştirme ve meta verilerini güncelleştirme veri kaybına neden olur.</span><span class="sxs-lookup"><span data-stu-id="90b75-368">Since a subset of properties may have been encrypted previously using a different key, simply merging the new properties and updating the metadata will result in data loss.</span></span> <span data-ttu-id="90b75-369">Ya da birleştirme önceden var olan varlık hizmetinden okumak için fazladan hizmeti çağrıları yapma gerektirir veya yeni bir anahtar özellik başına kullanarak, her ikisi de performansı artırmak için uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="90b75-369">Merging either requires making extra service calls to read the pre-existing entity from the service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>     

<span data-ttu-id="90b75-370">Tablo verisi şifreleme hakkında daha fazla bilgi için bkz: [istemci tarafı şifreleme ve Microsoft Azure depolama için Azure anahtar kasası](storage-client-side-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="90b75-370">For information about encrypting table data, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>  

## <a name="modelling-relationships"></a><span data-ttu-id="90b75-371">İlişkileri modelleme</span><span class="sxs-lookup"><span data-stu-id="90b75-371">Modelling relationships</span></span>
<span data-ttu-id="90b75-372">Etki alanı model oluşturmaya, karmaşık sistemler tasarımında önemli bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-372">Building domain models is a key step in the design of complex systems.</span></span> <span data-ttu-id="90b75-373">Genellikle, varlıkları ve ilişkileri aralarında iş etki alanını anlamak ve sisteminizin tasarımını bildirmek için bir yol olarak tanımlamak için modelling işlemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="90b75-373">Typically, you use the modelling process to identify entities and the relationships between them as a way to understand the business domain and inform the design of your system.</span></span> <span data-ttu-id="90b75-374">Bu bölüm, nasıl sizin tasarımlar tablo hizmeti için etki alanı modellerine bulunan ortak ilişki türlerinden bazıları çevirebilir üzerinde odaklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="90b75-374">This section focuses on how you can translate some of the common relationship types found in domain models to designs for the Table service.</span></span> <span data-ttu-id="90b75-375">İlişkisel veritabanı tasarlarken kullanılan oldukça farklı bir fiziksel dayalı NoSQL veri modeli için bir mantıksal veri modelinden eşlemesinin işlemidir.</span><span class="sxs-lookup"><span data-stu-id="90b75-375">The process of mapping from a logical data-model to a physical NoSQL based data-model is very different from that used when designing a relational database.</span></span> <span data-ttu-id="90b75-376">İlişkisel veritabanları tasarımı, genellikle artıklık – ve nasıl uyarlamasını veritabanı işleyişi soyutlar bildirim temelli bir sorgulama yeteneği en aza indirmek için en iyi duruma getirilmiş veri normalleştirme işlemi varsayar.</span><span class="sxs-lookup"><span data-stu-id="90b75-376">Relational databases design typically assumes a data normalization process optimized for minimizing redundancy – and a declarative querying capability that abstracts how the implementation of how the database works.</span></span>  

### <a name="one-to-many-relationships"></a><span data-ttu-id="90b75-377">Bir-çok ilişkileri</span><span class="sxs-lookup"><span data-stu-id="90b75-377">One-to-many relationships</span></span>
<span data-ttu-id="90b75-378">İş etki alanı nesneler arasındaki bir-çok ilişkileri ortaya çok sık: Örneğin, bir bölümü çok sayıda çalışan vardır.</span><span class="sxs-lookup"><span data-stu-id="90b75-378">One-to-many relationships between business domain objects occur very frequently: for example, one department has many employees.</span></span> <span data-ttu-id="90b75-379">Tablo hizmetinde her Artıları ve eksileri belirli senaryoya ilgili olabilecek ile bir-çok ilişkileri uygulamak için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="90b75-379">There are several ways to implement one-to-many relationships in the Table service each with pros and cons that may be relevant to the particular scenario.</span></span>  

<span data-ttu-id="90b75-380">Büyük çok Ulusal corporation örneği on binlerce Departmanlar ve her departman çok sayıda çalışan ve her çalışan belirli bir bölüm ile ilişkili olarak sahip olduğu çalışan varlıkları ile göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="90b75-380">Consider the example of a large multi-national corporation with tens of thousands of departments and employee entities where every department has many employees and each employee as associated with one specific department.</span></span> <span data-ttu-id="90b75-381">Ayrı departmanı ve bunlar gibi çalışan varlıkları depolamak için bir yaklaşım ise:</span><span class="sxs-lookup"><span data-stu-id="90b75-381">One approach is to store separate department and employee entities such as these:</span></span>  

![][1]

<span data-ttu-id="90b75-382">Bu örnek, temel türleri arasında örtük bir-çok ilişkisi gösterir **PartitionKey** değeri.</span><span class="sxs-lookup"><span data-stu-id="90b75-382">This example shows an implicit one-to-many relationship between the types based on the **PartitionKey** value.</span></span> <span data-ttu-id="90b75-383">Her bölüm çok sayıda çalışan olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-383">Each department can have many employees.</span></span>  

<span data-ttu-id="90b75-384">Bu örnek ayrıca aynı bölümde departmanı varlık ve ilgili çalışan varlıklarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="90b75-384">This example also shows a department entity and its related employee entities in the same partition.</span></span> <span data-ttu-id="90b75-385">Farklı bölümleri, tablolar veya hatta depolama hesapları farklı varlık türleri için kullanılacak tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-385">You could choose to use different partitions, tables, or even storage accounts for the different entity types.</span></span>  

<span data-ttu-id="90b75-386">Verilerinizi denormalize ve yalnızca çalışan varlıklarıyla aşağıdaki örnekte gösterildiği gibi Normalleştirilmemiş Departman verileri depolamak için alternatif bir yaklaşım var.</span><span class="sxs-lookup"><span data-stu-id="90b75-386">An alternative approach is to denormalize your data and store only employee entities with denormalized department data as shown in the following example.</span></span> <span data-ttu-id="90b75-387">Bunu yapmak için her çalışan departmanındaki güncelleştirmeniz gerekir çünkü bir bölüm Yöneticisi'ni ayrıntılarını değiştirebilmesi gereksinimi varsa bu belirli bir senaryoda, en iyi Normalleştirilmemiş bu yaklaşım olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-387">In this particular scenario, this denormalized approach may not be the best if you have a requirement to be able to change the details of a department manager because to do this you need to update every employee in the department.</span></span>  

![][2]

<span data-ttu-id="90b75-388">Daha fazla bilgi için bkz: [Denormalization düzeni](#denormalization-pattern) bu kılavuzda daha sonra.</span><span class="sxs-lookup"><span data-stu-id="90b75-388">For more information, see the [Denormalization pattern](#denormalization-pattern) later in this guide.</span></span>  

<span data-ttu-id="90b75-389">Aşağıdaki tabloda Artıları ve eksileri her çalışan ve bir-çok ilişkisi departmanı varlıkları depolamak için yukarıda özetlenen yaklaşımlardan biri özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="90b75-389">The following table summarizes the pros and cons of each of the approaches outlined above for storing employee and department entities that have a one-to-many relationship.</span></span> <span data-ttu-id="90b75-390">Çeşitli işlemleri ne sıklıkta yapılacağı düşünmelisiniz: pahalı bir işlem bu işlemi yalnızca seyrek durumda içeren bir tasarıma sahip kabul edilebilir olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-390">You should also consider how often you expect to perform various operations: it may be acceptable to have a design that includes an expensive operation if that operation only happens infrequently.</span></span>  

<table>
<tr>
<th><span data-ttu-id="90b75-391">Yaklaşım</span><span class="sxs-lookup"><span data-stu-id="90b75-391">Approach</span></span></th>
<th><span data-ttu-id="90b75-392">Uzmanları</span><span class="sxs-lookup"><span data-stu-id="90b75-392">Pros</span></span></th>
<th><span data-ttu-id="90b75-393">Simgeler</span><span class="sxs-lookup"><span data-stu-id="90b75-393">Cons</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="90b75-394">Ayrı bir varlık türleri, aynı bölüm, aynı tablosu</span><span class="sxs-lookup"><span data-stu-id="90b75-394">Separate entity types, same partition, same table</span></span></td>
<td>
<ul>
<li><span data-ttu-id="90b75-395">Tek bir işlemle bir departman varlık güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-395">You can update a department entity with a single operation.</span></span></li>
<li><span data-ttu-id="90b75-396">Bir EGT departman varlığı değiştirmek için bir gereksinim duyarsanız tutarlılığın korunmasını için kullanabileceğiniz olduğunda, güncelleştirme/ekleme/silme çalışan varlık.</span><span class="sxs-lookup"><span data-stu-id="90b75-396">You can use an EGT to maintain consistency if you have a requirement to modify a department entity whenever you update/insert/delete an employee entity.</span></span> <span data-ttu-id="90b75-397">Örneğin, bir departman çalışan sayısı her bölüm için sahipseniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-397">For example if you maintain a departmental employee count for each department.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="90b75-398">Bir çalışan ve bazı istemci etkinlikler için bir bölüm varlık almak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-398">You may need to retrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="90b75-399">Depolama işlemleri aynı bölümde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="90b75-399">Storage operations happen in the same partition.</span></span> <span data-ttu-id="90b75-400">Yüksek işlem birimlerinin, bu bir etkin nokta neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-400">At high transaction volumes, this may result in a hotspot.</span></span></li>
<li><span data-ttu-id="90b75-401">Bir çalışan bir EGT kullanarak yeni bir bölüm taşınamıyor.</span><span class="sxs-lookup"><span data-stu-id="90b75-401">You cannot move an employee to a new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="90b75-402">Ayrı bir varlık türleri, farklı bölümleri veya tablolar veya depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="90b75-402">Separate entity types, different partitions or tables or storage accounts</span></span></td>
<td>
<ul>
<li><span data-ttu-id="90b75-403">Tek bir işlemle bir departman varlık veya çalışan varlık güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-403">You can update a department entity or employee entity with a single operation.</span></span></li>
<li><span data-ttu-id="90b75-404">Yüksek işlem birimlerinin, bu yük daha fazla bölüm yayılan yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-404">At high transaction volumes, this may help spread the load across more partitions.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="90b75-405">Bir çalışan ve bazı istemci etkinlikler için bir bölüm varlık almak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-405">You may need to retrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="90b75-406">Tutarlılık sağlamak için EGTs kullanamazsınız olduğunda, güncelleştirme/ekleme/silme bir çalışan ve güncelleştirme bir bölüm.</span><span class="sxs-lookup"><span data-stu-id="90b75-406">You cannot use EGTs to maintain consistency when you update/insert/delete an employee and update a department.</span></span> <span data-ttu-id="90b75-407">Örneğin, bir çalışan sayısı departmanı varlıktaki güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="90b75-407">For example, updating an employee count in a department entity.</span></span></li>
<li><span data-ttu-id="90b75-408">Bir çalışan bir EGT kullanarak yeni bir bölüm taşınamıyor.</span><span class="sxs-lookup"><span data-stu-id="90b75-408">You cannot move an employee to a new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="90b75-409">Tek varlık türüne denormalize</span><span class="sxs-lookup"><span data-stu-id="90b75-409">Denormalize into single entity type</span></span></td>
<td>
<ul>
<li><span data-ttu-id="90b75-410">Tek bir istekle gereken tüm bilgileri alabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-410">You can retrieve all the information you need with a single request.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="90b75-411">(Bu, bir departmandaki tüm çalışanlar güncelleştirmek gerekir) departmanı bilgileri güncelleştirmek gereksinim duyarsanız tutarlılığın korunmasını pahalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-411">It may be expensive to maintain consistency if you need to update department information (this would require you to update all the employees in a department).</span></span></li>
</ul>
</td>
</tr>
</table>

<span data-ttu-id="90b75-412">Nasıl Bu seçenekler ve Artıları ve eksileri hangisinin en önemli, belirli bir uygulama senaryolarınızı bağlıdır arasında seçin.</span><span class="sxs-lookup"><span data-stu-id="90b75-412">How you choose between these options, and which of the pros and cons are most significant, depends on your specific application scenarios.</span></span> <span data-ttu-id="90b75-413">Örneğin, ne sıklıkta, departman varlıklar değiştirmeyin; Tüm çalışan sorguları ek departman bilgi gerekiyor; ölçeklenebilirlik sınırları, bölüm veya depolama hesabınız için ne kadar yakın misiniz?</span><span class="sxs-lookup"><span data-stu-id="90b75-413">For example, how often do you modify department entities; do all your employee queries need the additional departmental information; how close are you to the scalability limits on your partitions or your storage account?</span></span>  

### <a name="one-to-one-relationships"></a><span data-ttu-id="90b75-414">Bire bir ilişkiler</span><span class="sxs-lookup"><span data-stu-id="90b75-414">One-to-one relationships</span></span>
<span data-ttu-id="90b75-415">Etki alanı modelleri varlıklar arasındaki birebir ilişkileri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-415">Domain models may include one-to-one relationships between entities.</span></span> <span data-ttu-id="90b75-416">Tablo hizmetinde bire bir ilişki uygulamanız gerekiyorsa, her ikisinin de almanız gerektiğinde, iki ilgili varlık bağlanma seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-416">If you need to implement a one-to-one relationship in the Table service, you must also choose how to link the two related entities when you need to retrieve them both.</span></span> <span data-ttu-id="90b75-417">Bu bağlantıyı biçiminde bir bağlantı depolayarak örtük, bir kural anahtar değerlerine göre veya açık olabilir **PartitionKey** ve **RowKey** ilgili varlık için her bir varlıkta değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-417">This link can be either implicit, based on a convention in the key values, or explicit by storing a link in the form of **PartitionKey** and **RowKey** values in each entity to its related entity.</span></span> <span data-ttu-id="90b75-418">Bölüm olup aynı bölümde ilgili varlıkları saklamalısınız bir tartışma için bkz [-çok ilişkileri](#one-to-many-relationships).</span><span class="sxs-lookup"><span data-stu-id="90b75-418">For a discussion of whether you should store the related entities in the same partition, see the section [One-to-many relationships](#one-to-many-relationships).</span></span>  

<span data-ttu-id="90b75-419">Olduğunu da tablo hizmetinde bire bir ilişkiler uygulamak için yol açabilecek uygulama konuları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-419">Note that there are also implementation considerations that might lead you to implement one-to-one relationships in the Table service:</span></span>  

* <span data-ttu-id="90b75-420">Büyük varlıklar işleme (daha fazla bilgi için bkz: [büyük varlıklar düzeni](#large-entities-pattern)).</span><span class="sxs-lookup"><span data-stu-id="90b75-420">Handling large entities (for more information, see [Large Entities Pattern](#large-entities-pattern)).</span></span>  
* <span data-ttu-id="90b75-421">Erişim denetimleri uygulama (daha fazla bilgi için bkz: [paylaşılan erişim imzaları ile erişimi denetleme](#controlling-access-with-shared-access-signatures)).</span><span class="sxs-lookup"><span data-stu-id="90b75-421">Implementing access controls (for more information, see [Controlling access with Shared Access Signatures](#controlling-access-with-shared-access-signatures)).</span></span>  

### <a name="join-in-the-client"></a><span data-ttu-id="90b75-422">İstemci katılma</span><span class="sxs-lookup"><span data-stu-id="90b75-422">Join in the client</span></span>
<span data-ttu-id="90b75-423">Tablo hizmetinde ilişkileri modellemek için yollar olsa da, tablo hizmeti kullanmak için iki prime nedenler ölçeklenebilirlik ve performans olduğunu unuttunuz değil.</span><span class="sxs-lookup"><span data-stu-id="90b75-423">Although there are ways to model relationships in the Table service, you should not forget that the two prime reasons for using the Table service are scalability and performance.</span></span> <span data-ttu-id="90b75-424">Performans ve ölçeklenebilirlik çözümünüzün tehlikeye birçok ilişki modelleme bulursanız, tablo tasarımınıza tüm veri ilişkileri oluşturmak gerekli olup olmadığını kendiniz istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-424">If you find you are modelling many relationships that compromise the performance and scalability of your solution, you should ask yourself if it is necessary to build all the data relationships into your table design.</span></span> <span data-ttu-id="90b75-425">Tasarım basitleştirmek ve istemci uygulamanızı gerekli tüm birleştirmeler gerçekleştirme izin verirseniz çözümünüzün performansını ve ölçeklenebilirliğini artırmak mümkün olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-425">You may be able to simplify the design and improve the scalability and performance of your solution if you let your client application perform any necessary joins.</span></span>  

<span data-ttu-id="90b75-426">Örneğin, çok sık değişmeyen veriler içeren küçük tablolar sahip yaparsanız, ardından bu verileri bir kez ve istemcide önbelleğe.</span><span class="sxs-lookup"><span data-stu-id="90b75-426">For example, if you have small tables that contain data that does not change very often, then you can retrieve this data once and cache it on the client.</span></span> <span data-ttu-id="90b75-427">Bu, aynı veri almak için yinelenen gidiş-dönüş önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-427">This can avoid repeated roundtrips to retrieve the same data.</span></span> <span data-ttu-id="90b75-428">Bu kılavuzda inceledik örneklerde, küçük ve seyrek veri ara olarak istemci uygulamasını bir kez indirebilirsiniz verileri ve önbellek için iyi bir aday yapmadan değiştirmek küçük bir kuruluşta Departmanlar kümesi olasıdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-428">In the examples we have looked at in this guide, the set of departments in a small organization is likely to be small and change infrequently making it a good candidate for data that client application can download once and cache as look up data.</span></span>  

### <a name="inheritance-relationships"></a><span data-ttu-id="90b75-429">Devralma ilişkisi</span><span class="sxs-lookup"><span data-stu-id="90b75-429">Inheritance relationships</span></span>
<span data-ttu-id="90b75-430">İstemci uygulamanızın iş varlıkları temsil etmek için bir devralma ilişkisi parçasını sınıflar kümesini kullanıyorsa, bu varlıkların tablo hizmetinde kolayca devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-430">If your client application uses a set of classes that form part of an inheritance relationship to represent business entities, you can easily persist those entities in the Table service.</span></span> <span data-ttu-id="90b75-431">Örneğin, aşağıdaki istemci uygulamanızda tanımlanan sınıflar kümesini olabilir nerede **kişi** bir Özet sınıf.</span><span class="sxs-lookup"><span data-stu-id="90b75-431">For example, you might have the following set of classes defined in your client application where **Person** is an abstract class.</span></span>

![][3]

<span data-ttu-id="90b75-432">İki somut sınıfların görünüm bu gibi varlıkları kullanarak tek bir kişi tablosunu kullanarak tablo hizmetinde örneklerini devam edebilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-432">You can persist instances of the two concrete classes in the Table service using a single Person table using entities in that look like this:</span></span>  

![][4]

<span data-ttu-id="90b75-433">İstemci kodu aynı tablodaki birden çok varlık türleri ile çalışma hakkında daha fazla bilgi için bkz [heterojen varlık türleriyle çalışma](#working-with-heterogeneous-entity-types) bu kılavuzda daha sonra.</span><span class="sxs-lookup"><span data-stu-id="90b75-433">For more information about working with multiple entity types in the same table in client code, see the section [Working with heterogeneous entity types](#working-with-heterogeneous-entity-types) later in this guide.</span></span> <span data-ttu-id="90b75-434">Bu, istemci kodu varlık türünde tanımak nasıl örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-434">This provides examples of how to recognize the entity type in client code.</span></span>  

## <a name="table-design-patterns"></a><span data-ttu-id="90b75-435">Tablo Tasarım desenleri</span><span class="sxs-lookup"><span data-stu-id="90b75-435">Table Design Patterns</span></span>
<span data-ttu-id="90b75-436">Önceki bölümlerde bazı tartışmalar tablo tasarımınızı ekleme, güncelleştirme ve varlık verileri siliniyor ve sorguları kullanarak her iki varlık verileri için en iyi duruma getirme hakkında ayrıntılı gördünüz.</span><span class="sxs-lookup"><span data-stu-id="90b75-436">In previous sections, you have seen some detailed discussions about how to optimize your table design for both retrieving entity data using queries and for inserting, updating, and deleting entity data.</span></span> <span data-ttu-id="90b75-437">Bu bölümde tablo hizmeti çözümleri ile kullanım için uygun bazı desenleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="90b75-437">This section describes some patterns appropriate for use with Table service solutions.</span></span> <span data-ttu-id="90b75-438">Ayrıca, nasıl, pratikte bazı sorunlar ve bu kılavuzda daha önce oluşturulan dengelemeler karşılayabilirsiniz görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="90b75-438">In addition, you will see how you can practically address some of the issues and trade-offs raised previously in this guide.</span></span> <span data-ttu-id="90b75-439">Aşağıdaki diyagramda farklı desenleri arasındaki ilişkileri özetlenmektedir:</span><span class="sxs-lookup"><span data-stu-id="90b75-439">The following diagram summarizes the relationships between the different patterns:</span></span>  

![][5]

<span data-ttu-id="90b75-440">Yukarıdaki desenini eşleme desenleri (mavi) ve bu kılavuzda belgelenen koruma desenleri (turuncu) arasında bazı ilişkiler vurgular.</span><span class="sxs-lookup"><span data-stu-id="90b75-440">The pattern map above highlights some relationships between patterns (blue) and anti-patterns (orange) that are documented in this guide.</span></span> <span data-ttu-id="90b75-441">Elbette dikkate değer olan diğer birçok desenleri de vardır.</span><span class="sxs-lookup"><span data-stu-id="90b75-441">There are of course many other patterns that are worth considering.</span></span> <span data-ttu-id="90b75-442">Örneğin, tablo hizmeti için ana senaryoları kullanmak için biri [gerçekleştirilip görünüm düzeni](https://msdn.microsoft.com/library/azure/dn589782.aspx) gelen [komutu sorgu sorumluluk ayrımı (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) düzeni.</span><span class="sxs-lookup"><span data-stu-id="90b75-442">For example, one of the key scenarios for Table Service is to use the [Materialized View Pattern](https://msdn.microsoft.com/library/azure/dn589782.aspx) from the [Command Query Responsibility Segregation (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) pattern.</span></span>  

### <a name="intra-partition-secondary-index-pattern"></a><span data-ttu-id="90b75-443">Bölüm içi ikincil dizin düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-443">Intra-partition secondary index pattern</span></span>
<span data-ttu-id="90b75-444">Her varlık kullanan birden çok kopyalarını farklı depolama **RowKey** değerleri (aynı bölüm) etkinleştir hızlı ve verimli aramalarını kullanarak diğer sıralamalar farklı **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-444">Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span> <span data-ttu-id="90b75-445">Güncelleştirmeleri kopyaları arasında saklanması tutarlı EGT'ın kullanma.</span><span class="sxs-lookup"><span data-stu-id="90b75-445">Updates between copies can be kept consistent using EGT's.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-446">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-446">Context and problem</span></span>
<span data-ttu-id="90b75-447">Tablo hizmeti otomatik olarak kullanarak varlıkları dizinler **PartitionKey** ve **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-447">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="90b75-448">Bu, verimli bir şekilde bu değerleri kullanarak bir varlık almak bir istemci uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-448">This enables a client application to retrieve an entity efficiently using these values.</span></span> <span data-ttu-id="90b75-449">Örneğin, aşağıda gösterilen tablo yapısı kullanarak bir istemci uygulaması noktası sorgu bölüm adını ve çalışan kimliği kullanarak bir tek çalışan varlık almak için kullanabilirsiniz ( **PartitionKey** ve **RowKey** değerleri).</span><span class="sxs-lookup"><span data-stu-id="90b75-449">For example, using the table structure shown below, a client application can use a point query to retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="90b75-450">Bir istemci, her bölüm içinde çalışan kimliğine göre sıralanmış varlıklar de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-450">A client can also retrieve entities sorted by employee id within each department.</span></span>

![][6]

<span data-ttu-id="90b75-451">Ayrıca e-posta adresi gibi başka bir özelliğin değerini dayalı bir çalışan varlık bulamaz istiyorsanız bir eşleşme bulmak için daha az verimli bir bölüm tarama kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-451">If you also want to be able to find an employee entity based on the value of another property, such as email address, you must use a less efficient partition scan to find a match.</span></span> <span data-ttu-id="90b75-452">Tablo hizmetinde ikincil dizinler sağlamadığından budur.</span><span class="sxs-lookup"><span data-stu-id="90b75-452">This is because the table service does not provide secondary indexes.</span></span> <span data-ttu-id="90b75-453">Ayrıca, çalışanların farklı bir düzende sıralanmış bir listesini istemek için bir seçenek yoktur **RowKey** sırası.</span><span class="sxs-lookup"><span data-stu-id="90b75-453">In addition, there is no option to request a list of employees sorted in a different order than **RowKey** order.</span></span>  

#### <a name="solution"></a><span data-ttu-id="90b75-454">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-454">Solution</span></span>
<span data-ttu-id="90b75-455">İkincil dizinler eksikliği olarak çözmek için farklı bir kullanarak her kopyayla her varlığın birden çok kopya depolayabilir **RowKey** değeri.</span><span class="sxs-lookup"><span data-stu-id="90b75-455">To work around the lack of secondary indexes, you can store multiple copies of each entity with each copy using a different **RowKey** value.</span></span> <span data-ttu-id="90b75-456">Aşağıda gösterilen yapıları içeren bir varlık depolarsanız, e-posta adresi veya çalışan kimliği temel alarak çalışan varlıkları verimli bir şekilde alabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-456">If you store an entity with the structures shown below, you can efficiently retrieve employee entities based on email address or employee id.</span></span> <span data-ttu-id="90b75-457">Önek değerleri **RowKey**, "empid_" ve "email_" tek bir çalışan veya bir dizi çalışanlar için bir aralığı e-posta adresleri ya da çalışan kimlikleri kullanarak sorgulama olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-457">The prefix values for the **RowKey**, "empid_" and "email_" enable you to query for a single employee or a range of employees by using a range of email addresses or employee ids.</span></span>  

![][7]

<span data-ttu-id="90b75-458">(Bir çalışan kimliği ve bir e-posta adresine göre arayarak bakan) aşağıdaki iki filtre ölçütü her ikisi de noktası sorguları belirtin:</span><span class="sxs-lookup"><span data-stu-id="90b75-458">The following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="90b75-459">$filter (PartitionKey eq 'Satış') = ve (RowKey eq 'empid_000223')</span><span class="sxs-lookup"><span data-stu-id="90b75-459">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')</span></span>  
* <span data-ttu-id="90b75-460">$filter (PartitionKey eq 'Satış') = ve (RowKey eq 'email_jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="90b75-460">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')</span></span>  

<span data-ttu-id="90b75-461">Çalışan varlıklar için bir aralığı sorgu, çalışan kimliği düzende sıralanmış bir aralık veya uygun önekle varlıklar için sorgulayarak e-posta adresi düzende sıralanmış bir aralığı belirtebilirsiniz **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="90b75-461">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with the appropriate prefix in the **RowKey**.</span></span>  

* <span data-ttu-id="90b75-462">Satış departmanında çalışan kimliği aralığı 000100 için 000199 kullanımda olan tüm çalışanlar bulmak için: $filter (PartitionKey eq 'Satış') = ve (RowKey ge 'empid_000100') ve (RowKey le 'empid_000199')</span><span class="sxs-lookup"><span data-stu-id="90b75-462">To find all the employees in the Sales department with an employee id in the range 000100 to 000199 use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000100') and (RowKey le 'empid_000199')</span></span>  
* <span data-ttu-id="90b75-463">Tüm çalışanlar satış departmanında 'bir' kullanımı harfle başlayan bir e-posta adresiyle bulmak için: $filter (PartitionKey eq 'Satış') = ve (RowKey ge 'email_a') ve (RowKey lt 'email_b')</span><span class="sxs-lookup"><span data-stu-id="90b75-463">To find all the employees in the Sales department with an email address starting with the letter 'a' use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'email_a') and (RowKey lt 'email_b')</span></span>  
  
  <span data-ttu-id="90b75-464">Daha fazla bilgi için tablo hizmetinden REST API, Yukarıdaki örneklerde kullanılan filtresi sözdizimi olduğuna dikkat edin [sorgu varlıklar](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span><span class="sxs-lookup"><span data-stu-id="90b75-464">Note that the filter syntax used in the examples above is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-465">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-465">Issues and considerations</span></span>
<span data-ttu-id="90b75-466">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-466">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-467">Tablo depolama yinelenen veri depolamanın maliyeti yükünü başlıca sorunlardan olmamalıdır şekilde kullanmak görece ucuz ' dir.</span><span class="sxs-lookup"><span data-stu-id="90b75-467">Table storage is relatively cheap to use so the cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="90b75-468">Ancak, her zaman öngörülen depolama gereksinimlerinize göre tasarımınızı maliyetini değerlendirmek ve yalnızca istemci uygulamanızı yürütecek sorguları desteklemek için yinelenen varlıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90b75-468">However, you should always evaluate the cost of your design based on your anticipated storage requirements and only add duplicate entities to support the queries your client application will execute.</span></span>  
* <span data-ttu-id="90b75-469">İkincil dizin varlıkları özgün varlıkları aynı bölümünde depolandığından tek tek bir bölüm için ölçeklenebilirlik hedefleri aşmamasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="90b75-469">Because the secondary index entities are stored in the same partition as the original entities, you should ensure that you do not exceed the scalability targets for an individual partition.</span></span>  
* <span data-ttu-id="90b75-470">Varlık iki kopyasını otomatik olarak güncelleştirmek için EGTs kullanarak, yinelenen varlıklarınızı birbiriyle tutarlı tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-470">You can keep your duplicate entities consistent with each other by using EGTs to update the two copies of the entity atomically.</span></span> <span data-ttu-id="90b75-471">Bu, bir varlığın tüm kopyaları aynı bölümde saklamalısınız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="90b75-471">This implies that you should store all copies of an entity in the same partition.</span></span> <span data-ttu-id="90b75-472">Daha fazla bilgi için bkz [kullanarak varlık Grup hareketleri](#entity-group-transactions).</span><span class="sxs-lookup"><span data-stu-id="90b75-472">For more information, see the section [Using Entity Group Transactions](#entity-group-transactions).</span></span>  
* <span data-ttu-id="90b75-473">İçin kullanılan değer **RowKey** her bir varlık için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-473">The value used for the **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="90b75-474">Bileşik anahtar değerlerinden kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="90b75-474">Consider using compound key values.</span></span>  
* <span data-ttu-id="90b75-475">Sayısal değerler doldurma **RowKey** (örneğin, çalışan kimliği 000223), sıralama ve filtreleme göre üst ve alt sınırlarını etkinleştirir düzeltin.</span><span class="sxs-lookup"><span data-stu-id="90b75-475">Padding numeric values in the **RowKey** (for example, the employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="90b75-476">Mutlaka, varlığın tüm özellikleri yinelenen gerekmez.</span><span class="sxs-lookup"><span data-stu-id="90b75-476">You do not necessarily need to duplicate all the properties of your entity.</span></span> <span data-ttu-id="90b75-477">Örneğin, sorguları, e-posta kullanarak varlıkları aramanın adres **RowKey** hiçbir zaman, çalışanın yaşı gerekir, bu varlıkları aşağıdaki yapısına sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-477">For example, if the queries that lookup the entities using the email address in the **RowKey** never need the employee's age, these entities could have the following structure:</span></span>

![][8]

* <span data-ttu-id="90b75-478">Yinelenen verileri depolamak ve tek bir sorgu ile gereken tüm verileri alabilir sağlamak genellikle daha iyi bir varlık ve gerekli verileri aramak için başka bulmak için bir sorgu kullanımı çok.</span><span class="sxs-lookup"><span data-stu-id="90b75-478">It is typically better to store duplicate data and ensure that you can retrieve all the data you need with a single query, than to use one query to locate an entity and another to lookup the required data.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-479">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-479">When to use this pattern</span></span>
<span data-ttu-id="90b75-480">İstemci uygulamanızın istemci farklı sıralamalar varlıklarda almak gerektiğinde farklı anahtarlar, çeşitli kullanarak varlık almaya gerektiğinde ve benzersiz değerler çeşitli kullanarak her bir varlık tanımlayabilirsiniz bu deseni kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-480">Use this pattern when your client application needs to retrieve entities using a variety of different keys, when your client needs to retrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="90b75-481">Ancak, farklı kullanarak varlık arama yaparken bölüm ölçeklenebilirlik sınırları aşmadığından emin olmalıdır **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-481">However, you should be sure that you do not exceed the partition scalability limits when you are performing entity lookups using the different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-482">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-482">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-483">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-483">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-484">İkincil dizin arası bölüm düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-484">Inter-partition secondary index pattern</span></span>](#inter-partition-secondary-index-pattern)
* [<span data-ttu-id="90b75-485">Bileşik anahtar düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-485">Compound key pattern</span></span>](#compound-key-pattern)
* [<span data-ttu-id="90b75-486">Varlık Grup işlemleri</span><span class="sxs-lookup"><span data-stu-id="90b75-486">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="90b75-487">Heterojen varlık türleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="90b75-487">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a><span data-ttu-id="90b75-488">İkincil dizin arası bölüm düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-488">Inter-partition secondary index pattern</span></span>
<span data-ttu-id="90b75-489">Her varlık kullanan birden çok kopyalarını farklı depolama **RowKey** değerleri de, bölümler ayrı veya tablolara etkinleştir hızlı ve verimli aramaları ve kullanarak diğer sıralamalar farklı'de ayrı **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-489">Store multiple copies of each entity using different **RowKey** values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-490">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-490">Context and problem</span></span>
<span data-ttu-id="90b75-491">Tablo hizmeti otomatik olarak kullanarak varlıkları dizinler **PartitionKey** ve **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-491">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="90b75-492">Bu, verimli bir şekilde bu değerleri kullanarak bir varlık almak bir istemci uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-492">This enables a client application to retrieve an entity efficiently using these values.</span></span> <span data-ttu-id="90b75-493">Örneğin, aşağıda gösterilen tablo yapısı kullanarak bir istemci uygulaması noktası sorgu bölüm adını ve çalışan kimliği kullanarak bir tek çalışan varlık almak için kullanabilirsiniz ( **PartitionKey** ve **RowKey** değerleri).</span><span class="sxs-lookup"><span data-stu-id="90b75-493">For example, using the table structure shown below, a client application can use a point query to retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="90b75-494">Bir istemci, her bölüm içinde çalışan kimliğine göre sıralanmış varlıklar de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-494">A client can also retrieve entities sorted by employee id within each department.</span></span>  

![][9]

<span data-ttu-id="90b75-495">Ayrıca e-posta adresi gibi başka bir özelliğin değerini dayalı bir çalışan varlık bulamaz istiyorsanız bir eşleşme bulmak için daha az verimli bir bölüm tarama kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-495">If you also want to be able to find an employee entity based on the value of another property, such as email address, you must use a less efficient partition scan to find a match.</span></span> <span data-ttu-id="90b75-496">Tablo hizmetinde ikincil dizinler sağlamadığından budur.</span><span class="sxs-lookup"><span data-stu-id="90b75-496">This is because the table service does not provide secondary indexes.</span></span> <span data-ttu-id="90b75-497">Ayrıca, çalışanların farklı bir düzende sıralanmış bir listesini istemek için bir seçenek yoktur **RowKey** sırası.</span><span class="sxs-lookup"><span data-stu-id="90b75-497">In addition, there is no option to request a list of employees sorted in a different order than **RowKey** order.</span></span>  

<span data-ttu-id="90b75-498">Bu varlıklar karşı işlemleri çok yüksek hacimli bekleme ve tablo hizmeti istemci azaltma riskini en aza indirmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-498">You are anticipating a very high volume of transactions against these entities and want to minimize the risk of the Table service throttling your client.</span></span>  

#### <a name="solution"></a><span data-ttu-id="90b75-499">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-499">Solution</span></span>
<span data-ttu-id="90b75-500">İkincil dizinler eksikliği olarak çözmek için birden çok kopyası her kopyalama kullanarak her bir varlık farklı depolayabilir **PartitionKey** ve **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-500">To work around the lack of secondary indexes, you can store multiple copies of each entity with each copy using different **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="90b75-501">Aşağıda gösterilen yapıları içeren bir varlık depolarsanız, e-posta adresi veya çalışan kimliği temel alarak çalışan varlıkları verimli bir şekilde alabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-501">If you store an entity with the structures shown below, you can efficiently retrieve employee entities based on email address or employee id.</span></span> <span data-ttu-id="90b75-502">Önek değerleri **PartitionKey**, "empid_" ve "email_" bir sorgu için kullanmak istediğiniz hangi dizin tanımlamak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="90b75-502">The prefix values for the **PartitionKey**, "empid_" and "email_" enable you to identify which index you want to use for a query.</span></span>  

![][10]

<span data-ttu-id="90b75-503">(Bir çalışan kimliği ve bir e-posta adresine göre arayarak bakan) aşağıdaki iki filtre ölçütü her ikisi de noktası sorguları belirtin:</span><span class="sxs-lookup"><span data-stu-id="90b75-503">The following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="90b75-504">$filter (PartitionKey eq ' empid_Sales') = ve (RowKey eq '000223')</span><span class="sxs-lookup"><span data-stu-id="90b75-504">$filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')</span></span>
* <span data-ttu-id="90b75-505">$filter (PartitionKey eq ' email_Sales') = ve (RowKey eq 'jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="90b75-505">$filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')</span></span>  

<span data-ttu-id="90b75-506">Çalışan varlıklar için bir aralığı sorgu, çalışan kimliği düzende sıralanmış bir aralık veya uygun önekle varlıklar için sorgulayarak e-posta adresi düzende sıralanmış bir aralığı belirtebilirsiniz **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="90b75-506">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with the appropriate prefix in the **RowKey**.</span></span>  

* <span data-ttu-id="90b75-507">Çalışan kimliği aralığında Satış departmanındaki tüm çalışanlar bulmak için **000100** için **000199** çalışan kimliği sipariş kullanımda sıralanır: $filter (PartitionKey eq ' empid_Sales') = ve (RowKey ge '000100') ve (RowKey le '000199')</span><span class="sxs-lookup"><span data-stu-id="90b75-507">To find all the employees in the Sales department with an employee id in the range **000100** to **000199** sorted in employee id order use: $filter=(PartitionKey eq 'empid_Sales') and (RowKey ge '000100') and (RowKey le '000199')</span></span>  
* <span data-ttu-id="90b75-508">E-posta adresi sipariş kullanımda sıralanmış 'a' ile başlayan e-posta adresi olan Satış departmanındaki tüm çalışanlar bulmak için: $filter (PartitionKey eq ' email_Sales') = ve (RowKey ge 'bir') ve (RowKey lt 'b')</span><span class="sxs-lookup"><span data-stu-id="90b75-508">To find all the employees in the Sales department with an email address that starts with 'a' sorted in email address order use: $filter=(PartitionKey eq 'email_Sales') and (RowKey ge 'a') and (RowKey lt 'b')</span></span>  

<span data-ttu-id="90b75-509">Daha fazla bilgi için tablo hizmetinden REST API, Yukarıdaki örneklerde kullanılan filtresi sözdizimi olduğuna dikkat edin [sorgu varlıklar](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span><span class="sxs-lookup"><span data-stu-id="90b75-509">Note that the filter syntax used in the examples above is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-510">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-510">Issues and considerations</span></span>
<span data-ttu-id="90b75-511">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-511">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-512">Kullanarak, yinelenen varlıklarınızı birbiriyle sonunda tutarlı tutabilirsiniz [sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern) birincil ve ikincil dizin varlıkları korumak için.</span><span class="sxs-lookup"><span data-stu-id="90b75-512">You can keep your duplicate entities eventually consistent with each other by using the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) to maintain the primary and secondary index entities.</span></span>  
* <span data-ttu-id="90b75-513">Tablo depolama yinelenen veri depolamanın maliyeti yükünü başlıca sorunlardan olmamalıdır şekilde kullanmak görece ucuz ' dir.</span><span class="sxs-lookup"><span data-stu-id="90b75-513">Table storage is relatively cheap to use so the cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="90b75-514">Ancak, her zaman öngörülen depolama gereksinimlerinize göre tasarımınızı maliyetini değerlendirmek ve yalnızca istemci uygulamanızı yürütecek sorguları desteklemek için yinelenen varlıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90b75-514">However, you should always evaluate the cost of your design based on your anticipated storage requirements and only add duplicate entities to support the queries your client application will execute.</span></span>  
* <span data-ttu-id="90b75-515">İçin kullanılan değer **RowKey** her bir varlık için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-515">The value used for the **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="90b75-516">Bileşik anahtar değerlerinden kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="90b75-516">Consider using compound key values.</span></span>  
* <span data-ttu-id="90b75-517">Sayısal değerler doldurma **RowKey** (örneğin, çalışan kimliği 000223), sıralama ve filtreleme göre üst ve alt sınırlarını etkinleştirir düzeltin.</span><span class="sxs-lookup"><span data-stu-id="90b75-517">Padding numeric values in the **RowKey** (for example, the employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="90b75-518">Mutlaka, varlığın tüm özellikleri yinelenen gerekmez.</span><span class="sxs-lookup"><span data-stu-id="90b75-518">You do not necessarily need to duplicate all the properties of your entity.</span></span> <span data-ttu-id="90b75-519">Örneğin, sorguları, e-posta kullanarak varlıkları aramanın adres **RowKey** hiçbir zaman, çalışanın yaşı gerekir, bu varlıkları aşağıdaki yapısına sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-519">For example, if the queries that lookup the entities using the email address in the **RowKey** never need the employee's age, these entities could have the following structure:</span></span>
  
  ![][11]
* <span data-ttu-id="90b75-520">Yinelenen verileri depolamak ve ikincil dizin ve arama gerekli verileri için başka birincil dizinde kullanarak bir varlık bulmak için bir sorgu kullanımı çok tek bir sorgu ile gereken tüm verileri alabilir sağlamak genellikle daha iyi olur.</span><span class="sxs-lookup"><span data-stu-id="90b75-520">It is typically better to store duplicate data and ensure that you can retrieve all the data you need with a single query than to use one query to locate an entity using the secondary index and another to lookup the required data in the primary index.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-521">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-521">When to use this pattern</span></span>
<span data-ttu-id="90b75-522">İstemci uygulamanızın istemci farklı sıralamalar varlıklarda almak gerektiğinde farklı anahtarlar, çeşitli kullanarak varlık almaya gerektiğinde ve benzersiz değerler çeşitli kullanarak her bir varlık tanımlayabilirsiniz bu deseni kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-522">Use this pattern when your client application needs to retrieve entities using a variety of different keys, when your client needs to retrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="90b75-523">Varlık aramalarını farklı kullanarak gerçekleştirirken bölüm ölçeklenebilirlik sınırları aşmamak istediğinizde bu deseni kullanın **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-523">Use this pattern when you want to avoid exceeding the partition scalability limits when you are performing entity lookups using the different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-524">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-524">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-525">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-525">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-526">Sonuçta tutarlı işlemleri düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-526">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="90b75-527">Bölüm içi ikincil dizin düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-527">Intra-partition secondary index pattern</span></span>](#intra-partition-secondary-index-pattern)  
* [<span data-ttu-id="90b75-528">Bileşik anahtar düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-528">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="90b75-529">Varlık Grup işlemleri</span><span class="sxs-lookup"><span data-stu-id="90b75-529">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="90b75-530">Heterojen varlık türleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="90b75-530">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a><span data-ttu-id="90b75-531">Sonuçta tutarlı işlemleri düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-531">Eventually consistent transactions pattern</span></span>
<span data-ttu-id="90b75-532">Sonuçta tutarlı davranışı, Azure sıraları kullanarak bölüm sınırları veya depolama sistemi sınırları boyunca etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="90b75-532">Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-533">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-533">Context and problem</span></span>
<span data-ttu-id="90b75-534">EGTs atomik işlemleri aynı bölüm anahtarına paylaşan birden çok varlık arasında etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="90b75-534">EGTs enable atomic transactions across multiple entities that share the same partition key.</span></span> <span data-ttu-id="90b75-535">Performans ve ölçeklenebilirlik için ayrı bölümlere veya ayrı bir depolama sistemi tutarlılık gereksinimlerin varlıkları depolamak karar verebilirsiniz: Böyle bir senaryoda EGTs tutarlılığını korumak için kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="90b75-535">For performance and scalability reasons, you might decide to store entities that have consistency requirements in separate partitions or in a separate storage system: in such a scenario, you cannot use EGTs to maintain consistency.</span></span> <span data-ttu-id="90b75-536">Örneğin, arasında nihai tutarlılık sağlamak için bir zorunluluk olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-536">For example, you might have a requirement to maintain eventual consistency between:</span></span>  

* <span data-ttu-id="90b75-537">Varlık aynı tablodaki farklı tablolar, iki farklı bölümlere farklı depolama hesaplarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-537">Entities stored in two different partitions in the same table, in different tables, in in different storage accounts.</span></span>  
* <span data-ttu-id="90b75-538">Tablo hizmetinde depolanan bir varlık ve Blob hizmetinde depolanan bir blob.</span><span class="sxs-lookup"><span data-stu-id="90b75-538">An entity stored in the Table service and a blob stored in the Blob service.</span></span>  
* <span data-ttu-id="90b75-539">Tablo hizmeti ve bir dosya bir dosya sisteminde depolanan bir varlık.</span><span class="sxs-lookup"><span data-stu-id="90b75-539">An entity stored in the Table service and a file in a file system.</span></span>  
* <span data-ttu-id="90b75-540">Tablo hizmeti varlık deposunda henüz Azure Search hizmeti kullanarak dizin.</span><span class="sxs-lookup"><span data-stu-id="90b75-540">An entity store in the Table service yet indexed using the Azure Search service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="90b75-541">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-541">Solution</span></span>
<span data-ttu-id="90b75-542">Azure sıralar kullanarak, iki veya daha fazla bölüm ya da depolama sistemleri arasında nihai tutarlılık teslim bir çözüm uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-542">By using Azure queues, you can implement a solution that delivers eventual consistency across two or more partitions or storage systems.</span></span>
<span data-ttu-id="90b75-543">Bu yaklaşım göstermek için eski çalışan varlıkları arşivlemek için gereksinim varsayalım.</span><span class="sxs-lookup"><span data-stu-id="90b75-543">To illustrate this approach, assume you have a requirement to be able to archive old employee entities.</span></span> <span data-ttu-id="90b75-544">Eski çalışan varlıkları nadiren seçmeleri istenir ve geçerli çalışanlar ile ilgili tüm etkinlikleri dışında tutulması.</span><span class="sxs-lookup"><span data-stu-id="90b75-544">Old employee entities are rarely queried and should be excluded from any activities that deal with current employees.</span></span> <span data-ttu-id="90b75-545">Bu gereksinim uygulamak için etkin çalışanlara depolamak **geçerli** tablo ve eski çalışanların **arşiv** tablo.</span><span class="sxs-lookup"><span data-stu-id="90b75-545">To implement this requirement you store active employees in the **Current** table and old employees in the **Archive** table.</span></span> <span data-ttu-id="90b75-546">Bir çalışan arşivleme gerektirir varlıktan silmek **geçerli** tablo ve varlığa ekleyin **arşiv** tablosu, ancak bir EGT iki bu işlemleri gerçekleştirmek için kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="90b75-546">Archiving an employee requires you to delete the entity from the **Current** table and add the entity to the **Archive** table, but you cannot use an EGT to perform these two operations.</span></span> <span data-ttu-id="90b75-547">Bir hata görünmesi bir varlık hem veya hiçbiri tablolarda neden riskini önlemek için arşiv işlemi sonunda tutarlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-547">To avoid the risk that a failure causes an entity to appear in both or neither tables, the archive operation must be eventually consistent.</span></span> <span data-ttu-id="90b75-548">Aşağıdaki sıralı diyagramı adımlar bu işlemde açıklanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-548">The following sequence diagram outlines the steps in this operation.</span></span> <span data-ttu-id="90b75-549">Daha fazla ayrıntı metin aşağıdaki özel durum yollarında sağlanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-549">More detail is provided for exception paths in the text following.</span></span>  

![][12]

<span data-ttu-id="90b75-550">Bir istemci üzerinde çalışan #456 arşivlemek için bu örnek bir Azure sırada bir ileti koyarak Arşiv işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="90b75-550">A client initiates the archive operation by placing a message on an Azure queue, in this example to archive employee #456.</span></span> <span data-ttu-id="90b75-551">Çalışan rolü yeni iletiler için sıra yoklar; bir bulduğunda, iletiyi okur ve gizli bir kopyasını sıra üzerinde bırakır.</span><span class="sxs-lookup"><span data-stu-id="90b75-551">A worker role polls the queue for new messages; when it finds one, it reads the message and leaves a hidden copy on the queue.</span></span> <span data-ttu-id="90b75-552">Çalışan rolü sonraki varlıktan kopyasını getirir **geçerli** tablo, bir kopya ekler **arşiv** tablo ve özgün siler **geçerli** tablo.</span><span class="sxs-lookup"><span data-stu-id="90b75-552">The worker role next fetches a copy of the entity from the **Current** table, inserts a copy in the **Archive** table, and then deletes the original from the **Current** table.</span></span> <span data-ttu-id="90b75-553">Son olarak, önceki adımlarda hata olsaydı, çalışan rolü gizli ileti kuyruktan siler.</span><span class="sxs-lookup"><span data-stu-id="90b75-553">Finally, if there were no errors from the previous steps, the worker role deletes the hidden message from the queue.</span></span>  

<span data-ttu-id="90b75-554">Bu örnekte, 4. adım çalışanı ekler **arşiv** tablo.</span><span class="sxs-lookup"><span data-stu-id="90b75-554">In this example, step 4 inserts the employee into the **Archive** table.</span></span> <span data-ttu-id="90b75-555">Blob hizmetinde bir blob veya bir dosya sistemindeki bir dosyaya çalışan ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-555">It could add the employee to a blob in the Blob service or a file in a file system.</span></span>  

#### <a name="recovering-from-failures"></a><span data-ttu-id="90b75-556">Hatalardan kurtarma</span><span class="sxs-lookup"><span data-stu-id="90b75-556">Recovering from failures</span></span>
<span data-ttu-id="90b75-557">Önemlidir, adımları işlemlerinde **4** ve **5** olmalıdır *ıdempotent* durumda çalışan rolü Arşiv işleminin yeniden başlatılması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="90b75-557">It is important that the operations in steps **4** and **5** must be *idempotent* in case the worker role needs to restart the archive operation.</span></span> <span data-ttu-id="90b75-558">Adım için tablo hizmeti kullanıyorsanız, **4** "Ekle veya Değiştir" işlemi kullanmanız gerekir; adım için **5** kullanması gereken bir "silin var" işlemi kullanmakta olduğunuz istemci Kitaplığı'nda.</span><span class="sxs-lookup"><span data-stu-id="90b75-558">If you are using the Table service, for step **4** you should use an "insert or replace" operation; for step **5** you should use a "delete if exists" operation in the client library you are using.</span></span> <span data-ttu-id="90b75-559">Başka bir depolama sistemi kullanıyorsanız, uygun ıdempotent işlemi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-559">If you are using another storage system, you must use an appropriate idempotent operation.</span></span>  

<span data-ttu-id="90b75-560">Çalışan rolü asla adım tamamlarsa **6**, sonra da bir zaman aşımından sonra ileti yeniden görünür, sıranın onu yeniden işlemek denemek çalışan rolü için hazır.</span><span class="sxs-lookup"><span data-stu-id="90b75-560">If the worker role never completes step **6**, then after a timeout the message reappears on the queue ready for the worker role to try to reprocess it.</span></span> <span data-ttu-id="90b75-561">Çalışan rolü sıraya bir ileti okumak ve gerekirse, bayrak açıldı kaç kez denetleyebilirsiniz ayrı bir sıraya göndermek tarafından araştırma için "zarar" iletisi olduğu.</span><span class="sxs-lookup"><span data-stu-id="90b75-561">The worker role can check how many times a message on the queue has been read and, if necessary, flag it is a "poison" message for investigation by sending it to a separate queue.</span></span> <span data-ttu-id="90b75-562">Kuyruk iletileri okumak ve dequeue sayısı denetimi hakkında daha fazla bilgi için bkz: [iletileri almak](https://msdn.microsoft.com/library/azure/dd179474.aspx).</span><span class="sxs-lookup"><span data-stu-id="90b75-562">For more information about reading queue messages and checking the dequeue count, see [Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx).</span></span>  

<span data-ttu-id="90b75-563">Bazı hatalar tablo ve kuyruk Hizmetleri geçici hataları ve bunları işlemek için uygun yeniden deneme mantığı istemci uygulamanızı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="90b75-563">Some errors from the Table and Queue services are transient errors, and your client application should include suitable retry logic to handle them.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-564">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-564">Issues and considerations</span></span>
<span data-ttu-id="90b75-565">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-565">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-566">Bu çözüm için işlem yalıtım sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="90b75-566">This solution does not provide for transaction isolation.</span></span> <span data-ttu-id="90b75-567">Örneğin, bir istemci okuyabilir **geçerli** ve **arşiv** tabloları arasında adımları çalışan rolü olduğu zaman **4** ve **5**ve verileri tutarlı bir görünümünü bakın.</span><span class="sxs-lookup"><span data-stu-id="90b75-567">For example, a client could read the **Current** and **Archive** tables when the worker role was between steps **4** and **5**, and see an inconsistent view of the data.</span></span> <span data-ttu-id="90b75-568">Veri sonunda tutarlı olacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="90b75-568">Note that the data will be consistent eventually.</span></span>  
* <span data-ttu-id="90b75-569">Adım 4 ve 5 nihai tutarlılık sağlamak için ıdempotent olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-569">You must be sure that steps 4 and 5 are idempotent in order to ensure eventual consistency.</span></span>  
* <span data-ttu-id="90b75-570">Birden çok kuyruklar ve çalışan rolü örnekleri kullanarak çözüm ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-570">You can scale the solution by using multiple queues and worker role instances.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-571">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-571">When to use this pattern</span></span>
<span data-ttu-id="90b75-572">Farklı bölümleri veya tablo mevcut varlıklar arasında nihai tutarlılığı garanti istediğinizde bu deseni kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-572">Use this pattern when you want to guarantee eventual consistency between entities that exist in different partitions or tables.</span></span> <span data-ttu-id="90b75-573">Nihai tutarlılık işlemleri için tablo ve Blob hizmeti ve diğer olmayan - Azure Storage veritabanı veya dosya sistemi gibi veri kaynakları sağlamak için bu deseni genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-573">You can extend this pattern to ensure eventual consistency for operations across the Table service and the Blob service and other non-Azure Storage data sources such as database or the file system.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-574">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-574">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-575">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-575">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-576">Varlık Grup işlemleri</span><span class="sxs-lookup"><span data-stu-id="90b75-576">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="90b75-577">Birleştirme ya da değiştirme</span><span class="sxs-lookup"><span data-stu-id="90b75-577">Merge or replace</span></span>](#merge-or-replace)  

> [!NOTE]
> <span data-ttu-id="90b75-578">İşlem yalıtım çözümünüz için önemliyse, EGTs kullanmanızı sağlamak için tablolarınız yeniden düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-578">If transaction isolation is important to your solution, you should consider redesigning your tables to enable you to use EGTs.</span></span>  
> 
> 

### <a name="index-entities-pattern"></a><span data-ttu-id="90b75-579">Dizin varlıkları düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-579">Index Entities Pattern</span></span>
<span data-ttu-id="90b75-580">Varlıklar listesi Döndür verimli aramalar etkinleştirmek için dizin varlıkları korur.</span><span class="sxs-lookup"><span data-stu-id="90b75-580">Maintain index entities to enable efficient searches that return lists of entities.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-581">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-581">Context and problem</span></span>
<span data-ttu-id="90b75-582">Tablo hizmeti otomatik olarak kullanarak varlıkları dizinler **PartitionKey** ve **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-582">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="90b75-583">Bu, verimli bir şekilde noktası sorgusu kullanarak bir varlık almak bir istemci uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-583">This enables a client application to retrieve an entity efficiently using a point query.</span></span> <span data-ttu-id="90b75-584">Örneğin, aşağıda gösterilen tablo yapısı kullanarak, bir istemci uygulaması verimli bir şekilde bir tek çalışan varlık bölüm adını ve çalışan kimliği kullanarak alabilirsiniz ( **PartitionKey** ve **RowKey**).</span><span class="sxs-lookup"><span data-stu-id="90b75-584">For example, using the table structure shown below, a client application can efficiently retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey**).</span></span>  

![][13]

<span data-ttu-id="90b75-585">Ayrıca son kullanıcıların adı gibi başka bir benzersiz olmayan özelliğinin değeri göre çalışan varlıklar listesini almak istiyorsanız doğrudan aramak için bir dizin kullanmak yerine eşleşmeleri bulmak için daha az verimli bir bölüm tarama kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-585">If you also want to be able to retrieve a list of employee entities based on the value of another non-unique property, such as their last name, you must use a less efficient partition scan to find matches rather than using an index to look them up directly.</span></span> <span data-ttu-id="90b75-586">Tablo hizmetinde ikincil dizinler sağlamadığından budur.</span><span class="sxs-lookup"><span data-stu-id="90b75-586">This is because the table service does not provide secondary indexes.</span></span>  

#### <a name="solution"></a><span data-ttu-id="90b75-587">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-587">Solution</span></span>
<span data-ttu-id="90b75-588">Yukarıda gösterilen varlık yapısına sahip son ada göre arama etkinleştirmek için çalışan kimlikleri listesini bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-588">To enable lookup by last name with the entity structure shown above, you must maintain lists of employee ids.</span></span> <span data-ttu-id="90b75-589">Can gibi belirli bir son adı çalışan varlıklarıyla almak istiyorsanız, önce kendi son adıyla Etikan olan çalışanlar için çalışan kimliklerinin listesi bulun ve bu çalışan varlıkların almak gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-589">If you want to retrieve the employee entities with a particular last name, such as Jones, you must first locate the list of employee ids for employees with Jones as their last name, and then retrieve those employee entities.</span></span> <span data-ttu-id="90b75-590">Çalışan kimlikleri listesini depolamak için üç ana seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="90b75-590">There are three main options for storing the lists of employee ids:</span></span>  

* <span data-ttu-id="90b75-591">BLOB storage'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="90b75-591">Use blob storage.</span></span>  
* <span data-ttu-id="90b75-592">Çalışan varlıkları aynı bölüme dizin varlıklar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90b75-592">Create index entities in the same partition as the employee entities.</span></span>  
* <span data-ttu-id="90b75-593">Dizin varlıkları ayrı bölüm ya da tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90b75-593">Create index entities in a separate partition or table.</span></span>  

<span data-ttu-id="90b75-594"><u>#1. seçenek: Blob storage'ı kullanma</u></span><span class="sxs-lookup"><span data-stu-id="90b75-594"><u>Option #1: Use blob storage</u></span></span>  

<span data-ttu-id="90b75-595">İlk seçenek için bir listesini her benzersiz soyadı ve her blob Mağazası'nda bir blob oluşturun **PartitionKey** (bölüm) ve **RowKey** son bu ada sahip çalışanlar için (çalışan kimliği) değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-595">For the first option, you create a blob for every unique last name, and in each blob store a list of the **PartitionKey** (department) and **RowKey** (employee id) values for employees that have that last name.</span></span> <span data-ttu-id="90b75-596">Eklemek veya bir çalışan sildiğinizde ilgili blob içeriği çalışan varlıklarıyla sonuçta tutarlı olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-596">When you add or delete an employee you should ensure that the content of the relevant blob is eventually consistent with the employee entities.</span></span>  

<span data-ttu-id="90b75-597"><u>#2. seçenek:</u> aynı bölümde dizin varlıkları oluşturma</span><span class="sxs-lookup"><span data-stu-id="90b75-597"><u>Option #2:</u> Create index entities in the same partition</span></span>  

<span data-ttu-id="90b75-598">İkinci seçenek için aşağıdaki veri depolayan dizin varlıklar kullanın:</span><span class="sxs-lookup"><span data-stu-id="90b75-598">For the second option, use index entities that store the following data:</span></span>  

![][14]

<span data-ttu-id="90b75-599">**EmployeeIDs** özelliği depolanan Soyadı ile çalışanlar için çalışan kimlikleri listesini içeren **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="90b75-599">The **EmployeeIDs** property contains a list of employee ids for employees with the last name stored in the **RowKey**.</span></span>  

<span data-ttu-id="90b75-600">Aşağıdaki adımları ikinci seçeneği kullanıyorsanız, yeni bir çalışan ekleme yapıyorsanız izlemeniz gereken sürecini özetlemektedir.</span><span class="sxs-lookup"><span data-stu-id="90b75-600">The following steps outline the process you should follow when you are adding a new employee if you are using the second option.</span></span> <span data-ttu-id="90b75-601">Bu örnekte, bir çalışan kimliği 000152 ve satış departmanında son adıyla Etikan ekliyoruz:</span><span class="sxs-lookup"><span data-stu-id="90b75-601">In this example, we are adding an employee with Id 000152 and a last name Jones in the Sales department:</span></span>  

1. <span data-ttu-id="90b75-602">Dizin varlıkla almak bir **PartitionKey** "Satış" değeri ve **RowKey** "Can" değeri</span><span class="sxs-lookup"><span data-stu-id="90b75-602">Retrieve the index entity with a **PartitionKey** value "Sales" and the **RowKey** value "Jones."</span></span> <span data-ttu-id="90b75-603">2. adımda kullanmak üzere bu varlığın ETag kaydedin.</span><span class="sxs-lookup"><span data-stu-id="90b75-603">Save the ETag of this entity to use in step 2.</span></span>  
2. <span data-ttu-id="90b75-604">Yeni bir çalışan varlık ekleyen bir varlık Grup hareketi (diğer bir deyişle, toplu işlem) oluşturun (**PartitionKey** "Satış" değeri ve **RowKey** değer "000152") ve dizin varlığı güncelleştirir (**PartitionKey** "Satış" değeri ve **RowKey** "Can" değer) EmployeeIDs alan listesinde yeni çalışan kimliği ekleyerek.</span><span class="sxs-lookup"><span data-stu-id="90b75-604">Create an entity group transaction (that is, a batch operation) that inserts the new employee entity (**PartitionKey** value "Sales" and **RowKey** value "000152"), and updates the index entity (**PartitionKey** value "Sales" and **RowKey** value "Jones") by adding the new employee id to the list in the EmployeeIDs field.</span></span> <span data-ttu-id="90b75-605">Varlık Grup işlemler hakkında daha fazla bilgi için bkz: [varlık Grup hareketleri](#entity-group-transactions).</span><span class="sxs-lookup"><span data-stu-id="90b75-605">For more information about entity group transactions, see [Entity Group Transactions](#entity-group-transactions).</span></span>  
3. <span data-ttu-id="90b75-606">Varlık Grup hareketi (birisi yalnızca dizin varlık değiştirdi) iyimser eşzamanlılık hata nedeniyle başarısız olursa, 1. adımda yeniden başlatabilirsiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-606">If the entity group transaction fails because of an optimistic concurrency error (someone else has just modified the index entity), then you need to start over at step 1 again.</span></span>  

<span data-ttu-id="90b75-607">İkinci seçeneği kullanıyorsanız, bir çalışan silmek için benzer bir yaklaşım kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-607">You can use a similar approach to deleting an employee if you are using the second option.</span></span> <span data-ttu-id="90b75-608">Bir çalışanın soyadını değiştirmek, biraz daha karmaşık çünkü üç varlık güncelleştirmeleri bir varlık Grup işlemi yürütmek gerekecektir: çalışan varlık, dizin varlık eski soyadı ve yeni Soyadı dizin varlık.</span><span class="sxs-lookup"><span data-stu-id="90b75-608">Changing an employee's last name is slightly more complex because you will need to execute an entity group transaction that updates three entities: the employee entity, the index entity for the old last name, and the index entity for the new last name.</span></span> <span data-ttu-id="90b75-609">Ardından iyimser eşzamanlılık kullanarak güncelleştirmeleri gerçekleştirmek için kullanabileceğiniz ETag değerleri almak için herhangi bir değişiklik yapmadan önce her bir varlık almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-609">You must retrieve each entity before making any changes in order to retrieve the ETag values that you can then use to perform the updates using optimistic concurrency.</span></span>  

<span data-ttu-id="90b75-610">Aşağıdaki adımları verilen Soyadı bir departmandaki tüm çalışanlarla ikinci seçeneği kullanılıyorsa bakmak gerektiğinde izlemeniz gereken sürecini özetlemektedir.</span><span class="sxs-lookup"><span data-stu-id="90b75-610">The following steps outline the process you should follow when you need to look up all the employees with a given last name in a department if you are using the second option.</span></span> <span data-ttu-id="90b75-611">Bu örnekte, satış departmanında son adıyla Etikan tüm çalışanlar yukarı arıyoruz:</span><span class="sxs-lookup"><span data-stu-id="90b75-611">In this example, we are looking up all the employees with last name Jones in the Sales department:</span></span>  

1. <span data-ttu-id="90b75-612">Dizin varlıkla almak bir **PartitionKey** "Satış" değeri ve **RowKey** "Can" değeri</span><span class="sxs-lookup"><span data-stu-id="90b75-612">Retrieve the index entity with a **PartitionKey** value "Sales" and the **RowKey** value "Jones."</span></span>  
2. <span data-ttu-id="90b75-613">Çalışan EmployeeIDs alanında kimlikleri listesini ayrıştırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="90b75-613">Parse the list of employee Ids in the EmployeeIDs field.</span></span>  
3. <span data-ttu-id="90b75-614">(Örneğin, e-postaları) bu çalışanların her hakkında ek bilgi gerekirse, her kullanarak çalışan varlıkları almak **PartitionKey** "Satış" değeri ve **RowKey** 2. adımda elde ettiğiniz çalışanların listesini değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-614">If you need additional information about each of these employees (such as their email addresses), retrieve each of the employee entities using **PartitionKey** value "Sales" and **RowKey** values from the list of employees you obtained in step 2.</span></span>  

<span data-ttu-id="90b75-615"><u>#3. seçenek:</u> ayrı bölüm veya tablo içinde dizin varlıkları oluşturma</span><span class="sxs-lookup"><span data-stu-id="90b75-615"><u>Option #3:</u> Create index entities in a separate partition or table</span></span>  

<span data-ttu-id="90b75-616">Üçüncü seçenek için aşağıdaki veri depolayan dizin varlıklar kullanın:</span><span class="sxs-lookup"><span data-stu-id="90b75-616">For the third option, use index entities that store the following data:</span></span>  

![][15]

<span data-ttu-id="90b75-617">**EmployeeIDs** özelliği depolanan Soyadı ile çalışanlar için çalışan kimlikleri listesini içeren **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="90b75-617">The **EmployeeIDs** property contains a list of employee ids for employees with the last name stored in the **RowKey**.</span></span>  

<span data-ttu-id="90b75-618">Üçüncü seçenek dizin varlıkları çalışan varlıklardaki ayrı bir bölüme olduğundan tutarlılık sağlamak için EGTs kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="90b75-618">With the third option, you cannot use EGTs to maintain consistency because the index entities are in a separate partition from the employee entities.</span></span> <span data-ttu-id="90b75-619">Dizin varlıkları çalışan varlıklarıyla sonuçta tutarlı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="90b75-619">You should ensure that the index entities are eventually consistent with the employee entities.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-620">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-620">Issues and considerations</span></span>
<span data-ttu-id="90b75-621">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-621">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-622">Bu çözüm eşleşen varlıkları almak için en az iki sorgular gerektirir: bir listesini almak için dizin varlıkları sorgulamak için **RowKey** değerler ve listedeki her varlık almak için sorgular.</span><span class="sxs-lookup"><span data-stu-id="90b75-622">This solution requires at least two queries to retrieve matching entities: one to query the index entities to obtain the list of **RowKey** values, and then queries to retrieve each entity in the list.</span></span>  
* <span data-ttu-id="90b75-623">Tek bir varlık 1 MB maksimum boyuta sahip koşuluyla, seçeneği #2 ve seçeneği #3 çözümdeki verilen Soyadı çalışanı kimliklerinin listesi hiçbir zaman 1 MB'den daha büyük olduğu varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="90b75-623">Given that an individual entity has a maximum size of 1 MB, option #2 and option #3 in the solution assume that the list of employee ids for any given last name is never greater than 1 MB.</span></span> <span data-ttu-id="90b75-624">Çalışan kimliklerinin listesi boyutu 1 MB'den büyük olasılıkla ise #1 seçeneğini kullanın ve blob depolama alanına dizin verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="90b75-624">If the list of employee ids is likely to be greater than 1 MB in size, use option #1 and store the index data in blob storage.</span></span>  
* <span data-ttu-id="90b75-625">Seçenek #2 kullanırsanız, işlem hacmi belli bir bölüm ölçeklenebilirlik sınırları yaklaşımını, (ekleme ve çalışanlar silme ve bir çalışanın soyadını değiştirme işlemek için EGTs kullanarak), değerlendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-625">If you use option #2 (using EGTs to handle adding and deleting employees, and changing an employee's last name) you must evaluate if the volume of transactions will approach the scalability limits in a given partition.</span></span> <span data-ttu-id="90b75-626">Bu durumda, güncelleştirme isteklerini işlemek için kuyrukları kullanan ve ayrı bir bölüme çalışan varlıklardaki dizin varlıklarınızı depolamanıza olanak sağlar sonuçta tutarlı çözümünü (#1 veya seçeneği #3) düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-626">If this is the case, you should consider an eventually consistent solution (option #1 or option #3) that uses queues to handle the update requests and enables you to store your index entities in a separate partition from the employee entities.</span></span>  
* <span data-ttu-id="90b75-627">Bu çözüm #2 seçeneğinde varsayar bir bölüm içinde son ada göre arama yapmak istediğiniz: Örneğin, son adıyla Etikan satış departmanında çalışan listesini almak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="90b75-627">Option #2 in this solution assumes that you want to look up by last name within a department: for example, you want to retrieve a list of employees with a last name Jones in the Sales department.</span></span> <span data-ttu-id="90b75-628">Son adıyla Etikan tüm kuruluş genelinde tüm çalışanlar aramak istiyorsanız, seçeneğini #1 veya #3 seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="90b75-628">If you want to be able to look up all the employees with a last name Jones across the whole organization, use either option #1 or option #3.</span></span>
* <span data-ttu-id="90b75-629">Nihai tutarlılık sunar sıra tabanlı bir çözüm uygulayabilirsiniz (bkz [sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern) daha fazla ayrıntı için).</span><span class="sxs-lookup"><span data-stu-id="90b75-629">You can implement a queue-based solution that delivers eventual consistency (see the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) for more details).</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-630">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-630">When to use this pattern</span></span>
<span data-ttu-id="90b75-631">Tüm son adıyla Etikan tüm çalışanlar gibi ortak bir özellik değeri paylaşır varlık kümesi için arama yapmak istediğinizde bu deseni kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-631">Use this pattern when you want to lookup a set of entities that all share a common property value, such as all employees with the last name Jones.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-632">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-632">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-633">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-633">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-634">Bileşik anahtar düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-634">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="90b75-635">Sonuçta tutarlı işlemleri düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-635">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="90b75-636">Varlık Grup işlemleri</span><span class="sxs-lookup"><span data-stu-id="90b75-636">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="90b75-637">Heterojen varlık türleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="90b75-637">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a><span data-ttu-id="90b75-638">Denormalization deseni</span><span class="sxs-lookup"><span data-stu-id="90b75-638">Denormalization pattern</span></span>
<span data-ttu-id="90b75-639">İlgili verileri içeren bir tek nokta sorgu gereken tüm verileri almak üzere etkinleştirmek için tek bir varlık birleştirmek.</span><span class="sxs-lookup"><span data-stu-id="90b75-639">Combine related data together in a single entity to enable you to retrieve all the data you need with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-640">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-640">Context and problem</span></span>
<span data-ttu-id="90b75-641">İlişkisel bir veritabanında genellikle birden çok tablodan veri sorgularda kaynaklanan çoğaltma kaldırmak için veri normalleştirin.</span><span class="sxs-lookup"><span data-stu-id="90b75-641">In a relational database, you typically normalize data to remove duplication resulting in queries that retrieve data from multiple tables.</span></span> <span data-ttu-id="90b75-642">Verilerinizi Azure tablolardaki normalleştirin gerekirse, birden çok gidiş dönüş ilgili verileri almak için sunucuya istemciden yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-642">If you normalize your data in Azure tables, you must make multiple round trips from the client to the server to retrieve your related data.</span></span> <span data-ttu-id="90b75-643">Örneğin, aşağıda gösterilen tablosu yapısına sahip bir bölüm ayrıntılarını almak için iki gidiş dönüş gerekir: bir yöneticisinin kimliği ve bir çalışan varlık Yöneticisi'nin ayrıntılar getirmek için başka bir istek içerir departmanı varlık getirilemedi.</span><span class="sxs-lookup"><span data-stu-id="90b75-643">For example, with the table structure shown below you need two round trips to retrieve the details for a department: one to fetch the department entity that includes the manager's id, and then another request to fetch the manager's details in an employee entity.</span></span>  

![][16]

#### <a name="solution"></a><span data-ttu-id="90b75-644">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-644">Solution</span></span>
<span data-ttu-id="90b75-645">Verileri iki ayrı varlıklarda depolayarak, yerine verileri denormalize ve departman varlıkta Yöneticisi'nin ayrıntılar kopyasını tutun.</span><span class="sxs-lookup"><span data-stu-id="90b75-645">Instead of storing the data in two separate entities, denormalize the data and keep a copy of the manager's details in the department entity.</span></span> <span data-ttu-id="90b75-646">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="90b75-646">For example:</span></span>  

![][17]

<span data-ttu-id="90b75-647">Bu özellikleri depolanan departmanı varlıklarıyla noktası sorgusu kullanarak bir bölüm hakkında gereken tüm ayrıntıları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-647">With department entities stored with these properties, you can now retrieve all the details you need about a department using a point query.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-648">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-648">Issues and considerations</span></span>
<span data-ttu-id="90b75-649">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-649">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-650">Ek yükü bazı verileri iki kez saklamanın bazı maliyet yoktur.</span><span class="sxs-lookup"><span data-stu-id="90b75-650">There is some cost overhead associated with storing some data twice.</span></span> <span data-ttu-id="90b75-651">Depolama maliyetleri Marjinal artırma (daha az isteklerden kaynaklanan depolama birimi hizmeti) performans avantajı genellikle ağır (ve bu maliyet kısmen bir bölüm ayrıntılarını getirmek için gereken işlem sayısı azalmasına tarafından uzaklığı).</span><span class="sxs-lookup"><span data-stu-id="90b75-651">The performance benefit (resulting from fewer requests to the storage service) typically outweighs the marginal increase in storage costs (and this cost is partially offset by a reduction in the number of transactions you require to fetch the details of a department).</span></span>  
* <span data-ttu-id="90b75-652">Yöneticileri hakkında bilgi depolamak iki varlık tutarlılığını bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-652">You must maintain the consistency of the two entities that store information about managers.</span></span> <span data-ttu-id="90b75-653">Tek bir atomik işlemle birden çok varlık güncelleştirileceğini EGTs kullanarak tutarlılık sorunu işleyebilir: Bu durumda, departman varlık ve bölüm Yöneticisi'ni çalışan varlık aynı bölümünde depolanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-653">You can handle the consistency issue by using EGTs to update multiple entities in a single atomic transaction: in this case, the department entity, and the employee entity for the department manager are stored in the same partition.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-654">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-654">When to use this pattern</span></span>
<span data-ttu-id="90b75-655">Sık ilgili bilgi aramak ihtiyacınız olduğunda bu deseni kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-655">Use this pattern when you frequently need to look up related information.</span></span> <span data-ttu-id="90b75-656">Bu deseni istemciniz gerektirdiği verileri almak üzere yapmalısınız olan sorgu sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="90b75-656">This pattern reduces the number of queries your client must make to retrieve the data it requires.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-657">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-657">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-658">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-658">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-659">Bileşik anahtar düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-659">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="90b75-660">Varlık Grup işlemleri</span><span class="sxs-lookup"><span data-stu-id="90b75-660">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="90b75-661">Heterojen varlık türleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="90b75-661">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a><span data-ttu-id="90b75-662">Bileşik anahtar düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-662">Compound key pattern</span></span>
<span data-ttu-id="90b75-663">Kullanım bileşik **RowKey** tek nokta sorgu ile ilgili veri aramak bir istemci etkinleştirmek için değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-663">Use compound **RowKey** values to enable a client to lookup related data with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-664">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-664">Context and problem</span></span>
<span data-ttu-id="90b75-665">İlişkisel bir veritabanında tek bir sorgu istemcisinde veri ilgili parçalarını dönmek için sorguları birleşimlerde kullanmak için oldukça doğal.</span><span class="sxs-lookup"><span data-stu-id="90b75-665">In a relational database, it is quite natural to use joins in queries to return related pieces of data to the client in a single query.</span></span> <span data-ttu-id="90b75-666">Örneğin, bu çalışan için verileri gözden geçirin ve performans içeren ilgili varlıklar listesi bakmak için çalışan kimliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-666">For example, you might use the employee id to look up a list of related entities that contain performance and review data for that employee.</span></span>  

<span data-ttu-id="90b75-667">Aşağıdaki yapısını kullanarak tablo hizmetinde çalışan varlıkları depolayan varsayın:</span><span class="sxs-lookup"><span data-stu-id="90b75-667">Assume you are storing employee entities in the Table service using the following structure:</span></span>  

![][18]

<span data-ttu-id="90b75-668">Ayrıca incelemeler ve performans çalışanın çalıştığı her yıl, kuruluşunuz için ilgili geçmiş verileri depolamak gerekir ve bu bilgileri yıla göre erişebilmeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-668">You also need to store historical data relating to reviews and performance for each year the employee has worked for your organization and you need to be able to access this information by year.</span></span> <span data-ttu-id="90b75-669">Bir seçenek varlıkların şu yapıda depolayan başka bir tablo oluşturmaktır:</span><span class="sxs-lookup"><span data-stu-id="90b75-669">One option is to create another table that stores entities with the following structure:</span></span>  

![][19]

<span data-ttu-id="90b75-670">Bu yaklaşımda, bazı bilgiler (örneğin, ad ve Soyadı) yinelenen karar verebilir, tek bir istek verilerinizle almanıza olanak sağlamak için yeni bir varlık olarak dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="90b75-670">Notice that with this approach you may decide to duplicate some information (such as first name and last name) in the new entity to enable you to retrieve your data with a single request.</span></span> <span data-ttu-id="90b75-671">Ancak, iki varlık otomatik olarak güncelleştirmek için bir EGT kullanamadığından güçlü tutarlılık korunamaz.</span><span class="sxs-lookup"><span data-stu-id="90b75-671">However, you cannot maintain strong consistency because you cannot use an EGT to update the two entities atomically.</span></span>  

#### <a name="solution"></a><span data-ttu-id="90b75-672">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-672">Solution</span></span>
<span data-ttu-id="90b75-673">Yeni bir varlık türü aşağıdaki yapısıyla varlıkları kullanarak özgün tablonuzu saklayın:</span><span class="sxs-lookup"><span data-stu-id="90b75-673">Store a new entity type in your original table using entities with the following structure:</span></span>  

![][20]

<span data-ttu-id="90b75-674">Bildirim nasıl **RowKey** olan şimdi çalışan kimliği ve çalışanın performans almak ve verileri tek bir varlık için tek bir istekle gözden sağlar gözden geçirme verilerini yılın oluşan bir bileşik anahtarı.</span><span class="sxs-lookup"><span data-stu-id="90b75-674">Notice how the **RowKey** is now a compound key made up of the employee id and the year of the review data that enables you to retrieve the employee's performance and review data with a single request for a single entity.</span></span>  

<span data-ttu-id="90b75-675">Aşağıdaki örnek, belirli bir çalışan (örneğin, satış departmanında çalışan 000123) için tüm gözden geçirme verilerini nasıl alabilirsiniz özetlenmektedir:</span><span class="sxs-lookup"><span data-stu-id="90b75-675">The following example outlines how you can retrieve all the review data for a particular employee (such as employee 000123 in the Sales department):</span></span>  

<span data-ttu-id="90b75-676">$filter (PartitionKey eq 'Satış') = ve (RowKey ge 'empid_000123') ve (RowKey lt 'empid_000124') & $select = RowKey, Yöneticisi derecelendirme, eş derecelendirme, Yorumlar</span><span class="sxs-lookup"><span data-stu-id="90b75-676">$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-677">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-677">Issues and considerations</span></span>
<span data-ttu-id="90b75-678">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-678">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-679">Ayrıştırılacak kolaylaştıran bir uygun ayırıcı karakter kullanması gereken **RowKey** değeri: Örneğin, **000123_2012**.</span><span class="sxs-lookup"><span data-stu-id="90b75-679">You should use a suitable separator character that makes it easy to parse the **RowKey** value: for example, **000123_2012**.</span></span>  
* <span data-ttu-id="90b75-680">Bu varlık, aynı bölüme EGTs güçlü tutarlılık sağlamak için kullanabileceğiniz anlamına gelir aynı çalışan için ilgili verileri içeren diğer varlıklar olarak da depoluyorsanız.</span><span class="sxs-lookup"><span data-stu-id="90b75-680">You are also storing this entity in the same partition as other entities that contain related data for the same employee, which means you can use EGTs to maintain strong consistency.</span></span>
* <span data-ttu-id="90b75-681">Bu desen uygun olup olmadığını belirlemek için verileri ne sıklıkla sorgulayacak göz önünde bulundurmalısınız.</span><span class="sxs-lookup"><span data-stu-id="90b75-681">You should consider how frequently you will query the data to determine whether this pattern is appropriate.</span></span>  <span data-ttu-id="90b75-682">Örneğin, gözden geçirme seyrek ve ana çalışan verilere genellikle erişecekse bunları olarak ayrı varlıklar tutmalısınız.</span><span class="sxs-lookup"><span data-stu-id="90b75-682">For example, if you will access the review data infrequently and the main employee data often you should keep them as separate entities.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-683">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-683">When to use this pattern</span></span>
<span data-ttu-id="90b75-684">Bu deseni, bir saklamanız gerekir veya ilgili daha fazla varlıklar, sorgu sık kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-684">Use this pattern when you need to store one or more related entities that you query frequently.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-685">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-685">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-686">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-686">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-687">Varlık Grup işlemleri</span><span class="sxs-lookup"><span data-stu-id="90b75-687">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="90b75-688">Heterojen varlık türleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="90b75-688">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  
* [<span data-ttu-id="90b75-689">Sonuçta tutarlı işlemleri düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-689">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a><span data-ttu-id="90b75-690">Günlük tail düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-690">Log tail pattern</span></span>
<span data-ttu-id="90b75-691">Alma  *n*  kullanılarak bir bölüm için en son eklenen varlıklar bir **RowKey** ters tarihi ve saati sipariş sıralar değeri.</span><span class="sxs-lookup"><span data-stu-id="90b75-691">Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-692">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-692">Context and problem</span></span>
<span data-ttu-id="90b75-693">Ortak bir gereksinim en son oluşturulan varlıkları alabilir, örneğin on en son çalışan tarafından gönderilen talepleri gider.</span><span class="sxs-lookup"><span data-stu-id="90b75-693">A common requirement is be able to retrieve the most recently created entities, for example the ten most recent expense claims submitted by an employee.</span></span> <span data-ttu-id="90b75-694">Tablo sorguları destek bir **$top** sorgu işleminin ilk döndürmesi için  *n*  bir kümesindeki varlıkların: kümesindeki son n varlıkları döndürme eşdeğer sorgu işlem yok.</span><span class="sxs-lookup"><span data-stu-id="90b75-694">Table queries support a **$top** query operation to return the first *n* entities from a set: there is no equivalent query operation to return the last n entities in a set.</span></span>  

#### <a name="solution"></a><span data-ttu-id="90b75-695">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-695">Solution</span></span>
<span data-ttu-id="90b75-696">Kullanarak varlıkları depolayan bir **RowKey** doğal sıralar böylece en son giriş kullanarak geri tarih olduğunu her zaman Birinci tablodaki.</span><span class="sxs-lookup"><span data-stu-id="90b75-696">Store the entities using a **RowKey** that naturally sorts in reverse date/time order by using so the most recent entry is always the first one in the table.</span></span>  

<span data-ttu-id="90b75-697">Örneğin, bir çalışan tarafından gönderilen en son on gider talep almak için geçerli tarih/saat türetilmiş bir ters onay değer kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-697">For example, to be able to retrieve the ten most recent expense claims submitted by an employee, you can use a reverse tick value derived from the current date/time.</span></span> <span data-ttu-id="90b75-698">Aşağıdaki C# kod örneği için uygun bir "çizgilerine ters" değer oluşturmanın yollarından gösterir bir **RowKey** , en son sıralar eski için:</span><span class="sxs-lookup"><span data-stu-id="90b75-698">The following C# code sample shows one way to create a suitable "inverted ticks" value for a **RowKey** that sorts from the most recent to the oldest:</span></span>  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

<span data-ttu-id="90b75-699">Aşağıdaki kodu kullanarak tarih saat değerine geri alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90b75-699">You can get back to the date time value using the following code:</span></span>  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

<span data-ttu-id="90b75-700">Tablo sorgusu şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="90b75-700">The table query looks like this:</span></span>  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-701">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-701">Issues and considerations</span></span>
<span data-ttu-id="90b75-702">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-702">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-703">Dize değeri beklendiği gibi sıralar emin olmak için sıfır eklenerek ters onay değeri paneli gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-703">You must pad the reverse tick value with leading zeroes to ensure the string value sorts as expected.</span></span>  
* <span data-ttu-id="90b75-704">Bir bölümün düzeyinde ölçeklenebilirlik hedefleri farkında olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-704">You must be aware of the scalability targets at the level of a partition.</span></span> <span data-ttu-id="90b75-705">Dikkatli olun etkin nokta bölümleri oluşturma değil.</span><span class="sxs-lookup"><span data-stu-id="90b75-705">Be careful not create hot spot partitions.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-706">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-706">When to use this pattern</span></span>
<span data-ttu-id="90b75-707">Ters tarih sırası veya en son eklenen varlıklar erişim gerektiğinde varlıklarda erişmeye ihtiyacınız olduğunda bu deseni kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-707">Use this pattern when you need to access entities in reverse date/time order or when you need to access the most recently added entities.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-708">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-708">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-709">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-709">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-710">Başına / koruma düzeni ekleme</span><span class="sxs-lookup"><span data-stu-id="90b75-710">Prepend / append anti-pattern</span></span>](#prepend-append-anti-pattern)  
* [<span data-ttu-id="90b75-711">Varlıkları alma</span><span class="sxs-lookup"><span data-stu-id="90b75-711">Retrieving entities</span></span>](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a><span data-ttu-id="90b75-712">Yüksek hacimli delete düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-712">High volume delete pattern</span></span>
<span data-ttu-id="90b75-713">Yüksek hacimli varlıkların silinmesini kendi ayrı tabloda eşzamanlı silme işlemi için tüm varlıkları depolayarak etkinleştirme; Tablo silerek varlıkları silin.</span><span class="sxs-lookup"><span data-stu-id="90b75-713">Enable the deletion of a high volume of entities by storing all the entities for simultaneous deletion in their own separate table; you delete the entities by deleting the table.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-714">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-714">Context and problem</span></span>
<span data-ttu-id="90b75-715">Birçok uygulama, artık bir istemci uygulaması kullanılabilir olması gerekir veya uygulamayı başka bir depolama ortamına arşivlenmiş eski verileri silin.</span><span class="sxs-lookup"><span data-stu-id="90b75-715">Many applications delete old data which no longer needs to be available to a client application, or that the application has archived to another storage medium.</span></span> <span data-ttu-id="90b75-716">Genellikle bu tür veriler tarihe göre belirleyin: Örneğin, 60 günden eski olan tüm oturum açma isteklerinin kayıtları silmek için gereksinim.</span><span class="sxs-lookup"><span data-stu-id="90b75-716">You typically identify such data by a date: for example, you have a requirement to delete records of all login requests that are more than 60 days old.</span></span>  

<span data-ttu-id="90b75-717">Bir olası tasarım kullanmaktır tarih ve saat oturum açma isteğinin **RowKey**:</span><span class="sxs-lookup"><span data-stu-id="90b75-717">One possible design is to use the date and time of the login request in the **RowKey**:</span></span>  

![][21]

<span data-ttu-id="90b75-718">Uygulama eklemek ve ayrı bir bölüme her kullanıcı için oturum açma varlıkları silmek için bu yaklaşım bölüm etkin önler.</span><span class="sxs-lookup"><span data-stu-id="90b75-718">This approach avoids partition hotspots because the application can insert and delete login entities for each user in a separate partition.</span></span> <span data-ttu-id="90b75-719">Ancak, bu yaklaşım pahalı ve zaman alıcı ilk silmek için tüm varlıkları tanımlamak üzere bir tablo taraması gerçekleştirmeniz gerekir ve ardından eski her varlık silmeniz gerekir çünkü çok sayıda varlık varsa olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-719">However, this approach may be costly and time consuming if you have a large number of entities because first you need to perform a table scan in order to identify all the entities to delete, and then you must delete each old entity.</span></span> <span data-ttu-id="90b75-720">Not EGTs birden çok silme isteklerinin'toplu işleme eski varlıkları silmek için gerekli sunucuya gidiş dönüş sayısını azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-720">Note that you can reduce the number of round trips to the server required to delete the old entities by batching multiple delete requests into EGTs.</span></span>  

#### <a name="solution"></a><span data-ttu-id="90b75-721">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-721">Solution</span></span>
<span data-ttu-id="90b75-722">Oturum açma denemesi her gün için ayrı bir tablo kullanın.</span><span class="sxs-lookup"><span data-stu-id="90b75-722">Use a separate table for each day of login attempts.</span></span> <span data-ttu-id="90b75-723">Etkin noktalarına varlıklar ekleme ve eski varlıkları silmek şimdi her gün bir tablo silme yalnızca bir soru olduğunda kaçınmak için yukarıdaki varlık tasarım kullanabilirsiniz (tek bir depolama işlemi) bulma ve her gün yüzlerce ve tek tek oturum açma varlıklar binlerce silme yerine.</span><span class="sxs-lookup"><span data-stu-id="90b75-723">You can use the entity design above to avoid hotspots when you are inserting entities, and deleting old entities is now simply a question of deleting one table every day (a single storage operation) instead of finding and deleting hundreds and thousands of individual login entities every day.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-724">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-724">Issues and considerations</span></span>
<span data-ttu-id="90b75-725">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-725">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-726">Tasarımınızın, uygulamanızın belirli varlıklar, diğer veri ya da oluşturma toplama bilgisi ile bağlama bakarak gibi verileri kullanacak diğer yolları destekliyor mu?</span><span class="sxs-lookup"><span data-stu-id="90b75-726">Does your design support other ways your application will use the data such as looking up specific entities, linking with other data, or generating aggregate information?</span></span>  
* <span data-ttu-id="90b75-727">Yeni varlıklar eklerken tasarımınızı etkin noktalar önlenir?</span><span class="sxs-lookup"><span data-stu-id="90b75-727">Does your design avoid hot spots when you are inserting new entities?</span></span>  
* <span data-ttu-id="90b75-728">Aynı tablo adı sildikten sonra yeniden kullanmak istiyorsanız bir gecikme bekler.</span><span class="sxs-lookup"><span data-stu-id="90b75-728">Expect a delay if you want to reuse the same table name after deleting it.</span></span> <span data-ttu-id="90b75-729">Her zaman benzersiz tablo adları kullanmak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="90b75-729">It's better to always use unique table names.</span></span>  
* <span data-ttu-id="90b75-730">Tablo hizmeti erişim desenlerini öğrenir ve bölümleri düğümleri arasında dağıtır sırasında yeni bir tablo ilk kullandığınızda, bazı azaltma bekler.</span><span class="sxs-lookup"><span data-stu-id="90b75-730">Expect some throttling when you first use a new table while the Table service learns the access patterns and distributes the partitions across nodes.</span></span> <span data-ttu-id="90b75-731">Yeni tablo oluşturmak gereken ne sıklıkta göz önünde bulundurmalısınız.</span><span class="sxs-lookup"><span data-stu-id="90b75-731">You should consider how frequently you need to create new tables.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-732">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-732">When to use this pattern</span></span>
<span data-ttu-id="90b75-733">Aynı anda silmelisiniz varlıklar hacmi yüksek olduğunda bu deseni kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-733">Use this pattern when you have a high volume of entities that you must delete at the same time.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-734">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-734">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-735">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-735">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-736">Varlık Grup işlemleri</span><span class="sxs-lookup"><span data-stu-id="90b75-736">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="90b75-737">Varlıkları değiştirme</span><span class="sxs-lookup"><span data-stu-id="90b75-737">Modifying entities</span></span>](#modifying-entities)  

### <a name="data-series-pattern"></a><span data-ttu-id="90b75-738">Veri serisi deseni</span><span class="sxs-lookup"><span data-stu-id="90b75-738">Data series pattern</span></span>
<span data-ttu-id="90b75-739">Tam veri serisinde yaptığınız istek sayısını en aza indirmek için tek bir varlık deposu.</span><span class="sxs-lookup"><span data-stu-id="90b75-739">Store complete data series in a single entity to minimize the number of requests you make.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-740">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-740">Context and problem</span></span>
<span data-ttu-id="90b75-741">Yaygın bir senaryo, genellikle aynı anda almak için gereken verileri bir dizi depolamak bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="90b75-741">A common scenario is for an application to store a series of data that it typically needs to retrieve all at once.</span></span> <span data-ttu-id="90b75-742">Örneğin, uygulamanız her çalışan her saat gönderir kaç anlık ileti iletileri kaydetmek ve ardından bu bilgileri kaç iletileri çizmek için önceki 24 saat içinde gönderilen her bir kullanıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="90b75-742">For example, your application might record how many IM messages each employee sends every hour, and then use this information to plot how many messages each user sent over the preceding 24 hours.</span></span> <span data-ttu-id="90b75-743">Her çalışan için 24 varlıkları depolamak için bir tasarım olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-743">One design might be to store 24 entities for each employee:</span></span>  

![][22]

<span data-ttu-id="90b75-744">Bu tasarım ile kolayca bulmanıza ve uygulama ileti sayısı değerini güncelleştirmeniz gerektiğinde her bir çalışana güncelleştirilecek varlık güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="90b75-744">With this design, you can easily locate and update the entity to update for each employee whenever the application needs to update the message count value.</span></span> <span data-ttu-id="90b75-745">Ancak, önceki 24 saat için etkinliğin bir grafiği çizmek için bilgi almak için 24 varlıklar almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-745">However, to retrieve the information to plot a chart of the activity for the preceding 24 hours, you must retrieve 24 entities.</span></span>  

#### <a name="solution"></a><span data-ttu-id="90b75-746">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-746">Solution</span></span>
<span data-ttu-id="90b75-747">Aşağıdaki tasarım sahip ayrı bir özellik ileti sayısı için her bir saat depolamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="90b75-747">Use the following design with a separate property to store the message count for each hour:</span></span>  

![][23]

<span data-ttu-id="90b75-748">Bu tasarımla, bir çalışanın ileti sayısı için belirli bir saat güncelleştirmek için bir birleştirme işlemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-748">With this design, you can use a merge operation to update the message count for an employee for a specific hour.</span></span> <span data-ttu-id="90b75-749">Şimdi, tek bir varlık için bir istek kullanarak grafiği çizmek gereken tüm bilgileri alabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-749">Now, you can retrieve all the information you need to plot the chart using a request for a single entity.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-750">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-750">Issues and considerations</span></span>
<span data-ttu-id="90b75-751">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-751">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-752">Tam veri dizileriniz (bir varlık en çok 252 özellik olabilir) tek bir varlık uygun değilse, alternatif veri deposu blob gibi kullanın.</span><span class="sxs-lookup"><span data-stu-id="90b75-752">If your complete data series does not fit into a single entity (an entity can have up to 252 properties), use an alternative data store such as a blob.</span></span>  
* <span data-ttu-id="90b75-753">Bir varlık aynı anda güncelleştirme birden fazla istemciniz varsa kullanmanız gerekecektir **ETag** iyimser eşzamanlılık uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="90b75-753">If you have multiple clients updating an entity simultaneously, you will need to use the **ETag** to implement optimistic concurrency.</span></span> <span data-ttu-id="90b75-754">Birçok istemciniz varsa, yüksek çakışma karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-754">If you have many clients, you may experience high contention.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-755">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-755">When to use this pattern</span></span>
<span data-ttu-id="90b75-756">Güncelleştirme ve tek bir varlık ile ilişkili bir veri serisi almak ihtiyacınız olduğunda bu deseni kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-756">Use this pattern when you need to update and retrieve a data series associated with an individual entity.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-757">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-757">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-758">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-758">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-759">Büyük varlıklar düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-759">Large entities pattern</span></span>](#large-entities-pattern)  
* [<span data-ttu-id="90b75-760">Birleştirme ya da değiştirme</span><span class="sxs-lookup"><span data-stu-id="90b75-760">Merge or replace</span></span>](#merge-or-replace)  
* <span data-ttu-id="90b75-761">[Sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern) (, veri serisi bir blob'a depoladığınız varsa)</span><span class="sxs-lookup"><span data-stu-id="90b75-761">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) (if you are storing the data series in a blob)</span></span>  

### <a name="wide-entities-pattern"></a><span data-ttu-id="90b75-762">Geniş varlıklar düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-762">Wide entities pattern</span></span>
<span data-ttu-id="90b75-763">Birden çok 252 özellik sahip mantıksal varlık depolamak için birden çok fiziksel varlık kullanın.</span><span class="sxs-lookup"><span data-stu-id="90b75-763">Use multiple physical entities to store logical entities with more than 252 properties.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-764">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-764">Context and problem</span></span>
<span data-ttu-id="90b75-765">Tek bir varlık (zorunlu sistem özellikleri dışında) en çok 252 özellik olabilir ve birden fazla 1 MB veri toplama depolanamıyor.</span><span class="sxs-lookup"><span data-stu-id="90b75-765">An individual entity can have no more than 252 properties (excluding the mandatory system properties) and cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="90b75-766">İlişkisel bir veritabanında, genellikle bir satır boyutu üzerinde herhangi bir sınır round yeni bir tablo ekleyerek ve aralarında 1-1 ilişkisi zorlamayı elde edebileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-766">In a relational database, you would typically get round any limits on the size of a row by adding a new table and enforcing a 1-to-1 relationship between them.</span></span>  

#### <a name="solution"></a><span data-ttu-id="90b75-767">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-767">Solution</span></span>
<span data-ttu-id="90b75-768">Tablo hizmeti kullanarak, birden çok 252 özellik tek büyük iş nesnesiyle temsil etmek için birden çok varlık depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-768">Using the Table service, you can store multiple entities to represent a single large business object with more than 252 properties.</span></span> <span data-ttu-id="90b75-769">Örneğin, son 365 gün için her çalışan tarafından gönderilen IM iletilerin sayısını saklamak isterseniz, iki varlık farklı şemalarda kullanan aşağıdaki tasarım kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90b75-769">For example, if you want to store a count of the number of IM messages sent by each employee for the last 365 days, you could use the following design that uses two entities with different schemas:</span></span>  

![][24]

<span data-ttu-id="90b75-770">Onları korumak için her iki varlıkları güncelleştirme birbirleri ile eşitlenen gerektiren bir değişiklik yapmanız gerekirse bir EGT kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-770">If you need to make a change that requires updating both entities to keep them synchronized with each other you can use an EGT.</span></span> <span data-ttu-id="90b75-771">Aksi takdirde, ileti sayısı için belirli bir gün güncelleştirmek için bir tek birleştirme işlemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-771">Otherwise, you can use a single merge operation to update the message count for a specific day.</span></span> <span data-ttu-id="90b75-772">Tek bir çalışan için tüm verileri almak için her ikisini de kullanmanız iki verimli isteği ile yapabileceğiniz her iki varlığa alma bir **PartitionKey** ve **RowKey** değeri.</span><span class="sxs-lookup"><span data-stu-id="90b75-772">To retrieve all the data for an individual employee you must retrieve both entities, which you can do with two efficient requests that use both a **PartitionKey** and a **RowKey** value.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-773">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-773">Issues and considerations</span></span>
<span data-ttu-id="90b75-774">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-774">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-775">Eksiksiz bir mantıksal varlık alma, en az iki depolama işlemleri içerir: biri her fiziksel varlık almak için.</span><span class="sxs-lookup"><span data-stu-id="90b75-775">Retrieving a complete logical entity involves at least two storage transactions: one to retrieve each physical entity.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-776">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-776">When to use this pattern</span></span>
<span data-ttu-id="90b75-777">Bu desen ne zaman kullanın, boyutunu veya sayısını özelliklerinin tablo hizmetinde tek bir varlık için sınırlarını aşıyor varlıkları depolamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-777">Use this pattern when  need to store entities whose size or number of properties exceeds the limits for an individual entity in the Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-778">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-778">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-779">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-779">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-780">Varlık Grup işlemleri</span><span class="sxs-lookup"><span data-stu-id="90b75-780">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="90b75-781">Birleştirme ya da değiştirme</span><span class="sxs-lookup"><span data-stu-id="90b75-781">Merge or replace</span></span>](#merge-or-replace)

### <a name="large-entities-pattern"></a><span data-ttu-id="90b75-782">Büyük varlıklar düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-782">Large entities pattern</span></span>
<span data-ttu-id="90b75-783">Büyük özellik değerlerini depolamak için BLOB Depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-783">Use blob storage to store large property values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-784">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-784">Context and problem</span></span>
<span data-ttu-id="90b75-785">Tek bir varlık 1 MB'tan fazla veri toplama depolanamıyor.</span><span class="sxs-lookup"><span data-stu-id="90b75-785">An individual entity cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="90b75-786">Bir veya birkaç özelliklerinizin bu değeri aşacak varlığınız toplam boyutu neden değerleri depolarsanız, tablo hizmetinde tüm varlık depolanamıyor.</span><span class="sxs-lookup"><span data-stu-id="90b75-786">If one or several of your properties store values that cause the total size of your entity to exceed this value, you cannot store the entire entity in the Table service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="90b75-787">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-787">Solution</span></span>
<span data-ttu-id="90b75-788">Bir veya daha fazla özellikleri büyük miktarda veri içerdiğinden varlığınız 1 MB boyutunda aşarsa, Blob hizmetinde verileri depolamak ve ardından bir özellikte varlık blob adresi depolamak.</span><span class="sxs-lookup"><span data-stu-id="90b75-788">If your entity exceeds 1 MB in size because one or more properties contain a large amount of data, you can store data in the Blob service and then store the address of the blob in a property in the entity.</span></span> <span data-ttu-id="90b75-789">Örneğin, bir çalışanın fotoğrafı blob storage'da depolamak ve fotoğraf bağlantı depolamak **fotoğraf** çalışan varlığınız özelliği:</span><span class="sxs-lookup"><span data-stu-id="90b75-789">For example, you can store the photo of an employee in blob storage and store a link to the photo in the **Photo** property of your employee entity:</span></span>  

![][25]

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-790">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-790">Issues and considerations</span></span>
<span data-ttu-id="90b75-791">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-791">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-792">Tablo hizmeti varlıkta ve verileri Blob hizmeti arasında nihai tutarlılık sağlamak için kullanmak [sonuçta tutarlı işlemleri düzeni](#eventually-consistent-transactions-pattern) varlıklarınızı korumak için.</span><span class="sxs-lookup"><span data-stu-id="90b75-792">To maintain eventual consistency between the entity in the Table service and the data in the Blob service, use the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) to maintain your entities.</span></span>
* <span data-ttu-id="90b75-793">Eksiksiz bir varlık alma, en az iki depolama işlemleri içerir: bir varlık ve bir blob verileri almak üzere alınamadı.</span><span class="sxs-lookup"><span data-stu-id="90b75-793">Retrieving a complete entity involves at least two storage transactions: one to retrieve the entity and one to retrieve the blob data.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-794">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-794">When to use this pattern</span></span>
<span data-ttu-id="90b75-795">Büyüklüğü tablo hizmetinde tek bir varlık için sınırlarını aşıyor varlıkları depolamak ihtiyacınız olduğunda bu deseni kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-795">Use this pattern when you need to store entities whose size exceeds the limits for an individual entity in the Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-796">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-796">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-797">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-797">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-798">Sonuçta tutarlı işlemleri düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-798">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="90b75-799">Geniş varlıklar düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-799">Wide entities pattern</span></span>](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a><span data-ttu-id="90b75-800">Koruma deseni başına ve ekleme</span><span class="sxs-lookup"><span data-stu-id="90b75-800">Prepend/append anti-pattern</span></span>
<span data-ttu-id="90b75-801">Birden çok bölüm arasında eklemeleri yayarak eklemeleri hacmi yüksek olduğunda ölçeklenebilirliği artırır.</span><span class="sxs-lookup"><span data-stu-id="90b75-801">Increase scalability when you have a high volume of inserts by spreading the inserts across multiple partitions.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-802">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-802">Context and problem</span></span>
<span data-ttu-id="90b75-803">Eklenmesini veya varlıklar saklı varlıklarınızı genellikle sonuna ekleme sırası bölümlerinin ilk veya son bölümü için yeni varlıklar ekleme uygulama sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-803">Prepending or appending entities to your stored entities typically results in the application adding new entities to the first or last partition of a sequence of partitions.</span></span> <span data-ttu-id="90b75-804">Bu durumda, tüm eklemeleri verilen herhangi bir zamanda birden çok düğümüne ekler Dengeleme ve büyük olasılıkla bölüm ölçeklenebilirlik hedefleri isabet uygulamanıza neden yük tablo hizmetinden engelleyen bir etkin nokta oluşturma aynı bölüme yerinde sürüyor.</span><span class="sxs-lookup"><span data-stu-id="90b75-804">In this case, all of the inserts at any given time are taking place in the same partition, creating a hotspot that prevents the table service from load balancing inserts across multiple nodes, and possibly causing your application to hit the scalability targets for partition.</span></span> <span data-ttu-id="90b75-805">Örneğin, bir uygulamanız varsa ağ kaydeder ve kaynak erişimini çalışanlar, aşağıda gösterildiği gibi daha sonra bir varlık yapısı tarafından birimin işlemlerinin tek bir bölüm için ölçeklenebilirlik hedef ulaşırsa bir etkin nokta olmadan geçerli saatlik bölüm neden olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-805">For example, if you have an application that logs network and resource access by employees, then an entity structure as shown below could result in the current hour's partition becoming a hotspot if the volume of transactions reaches the scalability target for an individual partition:</span></span>  

![][26]

#### <a name="solution"></a><span data-ttu-id="90b75-806">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-806">Solution</span></span>
<span data-ttu-id="90b75-807">Aşağıdaki alternatif varlık yapısını belirli bölümlerinin etkin nokta uygulama günlükleri olayları ortadan kaldırır:</span><span class="sxs-lookup"><span data-stu-id="90b75-807">The following alternative entity structure avoids a hotspot on any particular partition as the application logs events:</span></span>  

![][27]

<span data-ttu-id="90b75-808">Bu örnekle nasıl hem bildirimi **PartitionKey** ve **RowKey** bileşik anahtarlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-808">Notice with this example how both the **PartitionKey** and **RowKey** are compound keys.</span></span> <span data-ttu-id="90b75-809">**PartitionKey** günlüğe birden çok bölüm arasında dağıtmak için hem Bölüm hem de çalışana kimliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-809">The **PartitionKey** uses both the department and employee id to distribute the logging across multiple partitions.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-810">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-810">Issues and considerations</span></span>
<span data-ttu-id="90b75-811">Bu desen uygulamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-811">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="90b75-812">Dinamik bölümleri ekler üzerinde verimli bir şekilde oluşturulmasını engeller alternatif anahtar yapısı istemci uygulamanızı yapar sorgularını destekliyor mu?</span><span class="sxs-lookup"><span data-stu-id="90b75-812">Does the alternative key structure that avoids creating hot partitions on inserts efficiently support the queries your client application makes?</span></span>  
* <span data-ttu-id="90b75-813">Beklenen biriminiz işlemlerinin tek bir bölüm için ölçeklenebilirlik hedefleri erişmek ve depolama hizmeti tarafından kısıtlanan büyük olasılıkla anlama geliyor?</span><span class="sxs-lookup"><span data-stu-id="90b75-813">Does your anticipated volume of transactions mean that you are likely to reach the scalability targets for an individual partition and be throttled by the storage service?</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="90b75-814">Bu desen kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="90b75-814">When to use this pattern</span></span>
<span data-ttu-id="90b75-815">Biriminiz işlemlerinin büyük bir olasılıkla dinamik bir bölüm eriştiğinizde depolama hizmeti tarafından azaltma neden olduğunda prepend ve append koruma düzeni kaçının.</span><span class="sxs-lookup"><span data-stu-id="90b75-815">Avoid the prepend/append anti-pattern when your volume of transactions is likely to result in throttling by the storage service when you access a hot partition.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="90b75-816">İlgili desenleri ve Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="90b75-816">Related patterns and guidance</span></span>
<span data-ttu-id="90b75-817">Aşağıdaki desenleri ve rehberlik de bu deseni uygularken ilgili olabilir:</span><span class="sxs-lookup"><span data-stu-id="90b75-817">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="90b75-818">Bileşik anahtar düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-818">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="90b75-819">Günlük tail düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-819">Log tail pattern</span></span>](#log-tail-pattern)  
* [<span data-ttu-id="90b75-820">Varlıkları değiştirme</span><span class="sxs-lookup"><span data-stu-id="90b75-820">Modifying entities</span></span>](#modifying-entities)  

### <a name="log-data-anti-pattern"></a><span data-ttu-id="90b75-821">Günlük veri koruma düzeni</span><span class="sxs-lookup"><span data-stu-id="90b75-821">Log data anti-pattern</span></span>
<span data-ttu-id="90b75-822">Genellikle, Blob hizmeti yerine tablo hizmeti günlük verilerini depolamak için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-822">Typically, you should use the Blob service instead of the Table service to store log data.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="90b75-823">İçerik ve sorunu</span><span class="sxs-lookup"><span data-stu-id="90b75-823">Context and problem</span></span>
<span data-ttu-id="90b75-824">Özel tarih aralığı için günlük girişlerini seçimi almak için günlük verileri için ortak bir kullanım örneği: Örneğin, tüm hata ve kritik iletileri 15:04 15:06 belirli bir tarihte arasındaki uygulamanızı günlüğe bulmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-824">A common use case for log data is to retrieve a selection of log entries for a specific date/time range: for example, you want to find all the error and critical messages that your application logged between 15:04 and 15:06 on a specific date.</span></span> <span data-ttu-id="90b75-825">Günlük varlıklara kaydettiğiniz bölüm belirlemek için tarih ve saat günlük iletisi kullanmak istiyor musunuz: belirli bir zamanda, tüm günlük varlıkları aynı paylaşacak çünkü etkin bir bölümünde sonuçlarının **PartitionKey** değeri (bölümüne bakın [Prepend ve append koruma düzeni](#prepend-append-anti-pattern)).</span><span class="sxs-lookup"><span data-stu-id="90b75-825">You do not want to use the date and time of the log message to determine the partition you save log entities to: that results in a hot partition because at any given time, all the log entities will share the same **PartitionKey** value (see the section [Prepend/append anti-pattern](#prepend-append-anti-pattern)).</span></span> <span data-ttu-id="90b75-826">Örneğin, uygulamanın tüm günlük iletilerini bölüm için geçerli tarih ve saat için yazdığından aşağıdaki varlık şemanın bir günlük iletisi için etkin bir bölümünde sonuçları:</span><span class="sxs-lookup"><span data-stu-id="90b75-826">For example, the following entity schema for a log message results in a hot partition because the application writes all log messages to the partition for the current date and hour:</span></span>  

![][28]

<span data-ttu-id="90b75-827">Bu örnekte, **RowKey** tarih ve saat günlük iletilerini tarih sırasına koyulmuş depolanan emin olmak için günlük iletisinin içerir ve birden çok günlük iletilerini aynı tarih ve saat paylaşmak durumunda bir ileti kimliği içerir.</span><span class="sxs-lookup"><span data-stu-id="90b75-827">In this example, the **RowKey** includes the date and time of the log message to ensure that log messages are stored sorted in date/time order, and includes a message id in case multiple log messages share the same date and time.</span></span>  

<span data-ttu-id="90b75-828">Başka bir yaklaşım kullanmaktır bir **PartitionKey** sağlar uygulama bölümleri aralığı iletileri yazar.</span><span class="sxs-lookup"><span data-stu-id="90b75-828">Another approach is to use a **PartitionKey** that ensures that the application writes messages across a range of partitions.</span></span> <span data-ttu-id="90b75-829">Örneğin, günlüğü kaynağı iletisi iletilerini birçok bölüm arasında dağıtmak için bir yol sağlar, aşağıdaki varlık şema kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90b75-829">For example, if the source of the log message provides a way to distribute messages across many partitions, you could use the following entity schema:</span></span>  

![][29]

<span data-ttu-id="90b75-830">Belirli bir süre için tüm günlük iletileri almak için her bölüm tablosunda arama gerekir, ancak bu şemayı sorun olur.</span><span class="sxs-lookup"><span data-stu-id="90b75-830">However, the problem with this schema is that to retrieve all the log messages for a specific time span you must search every partition in the table.</span></span>

#### <a name="solution"></a><span data-ttu-id="90b75-831">Çözüm</span><span class="sxs-lookup"><span data-stu-id="90b75-831">Solution</span></span>
<span data-ttu-id="90b75-832">Önceki bölümde günlük girişlerini ve önerilen iki, yetersiz, tasarımları depolamak için tablo hizmeti kullanmayı denemek sorunu vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-832">The previous section highlighted the problem of trying to use the Table service to store log entries and suggested two, unsatisfactory, designs.</span></span> <span data-ttu-id="90b75-833">Günlük iletileri yazma performansının düşük riskini etkin bir bölüm için bir çözüm öncülük; başka bir çözümü her bölüm tablosundaki belirli bir süre için günlüğü iletileri almak için tarama gereksinimi nedeniyle zayıf sorgu performansı sonuçlandı.</span><span class="sxs-lookup"><span data-stu-id="90b75-833">One solution led to a hot partition with the risk of poor performance writing log messages; the other solution resulted in poor query performance because of the requirement to scan every partition in the table to retrieve log messages for a specific time span.</span></span> <span data-ttu-id="90b75-834">BLOB storage bu tür senaryosu için daha iyi bir çözüm sunar ve bu, nasıl Azure depolama çözümlemeleri depoları günlük verilerini toplar.</span><span class="sxs-lookup"><span data-stu-id="90b75-834">Blob storage offers a better solution for this type of scenario and this is how Azure Storage Analytics stores the log data it collects.</span></span>  

<span data-ttu-id="90b75-835">Bu bölümde, nasıl Storage Analytics bir aralık tarafından genellikle sorgu verileri depolamak için bu yaklaşım çizimi olarak blob depolama alanına günlük verilerini depolar özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="90b75-835">This section outlines how Storage Analytics stores log data in blob storage as an illustration of this approach to storing data that you typically query by range.</span></span>  

<span data-ttu-id="90b75-836">Storage Analytics günlük iletilerini birden çok BLOB'ları sınırlandırılmış biçimde depolar.</span><span class="sxs-lookup"><span data-stu-id="90b75-836">Storage Analytics stores log messages in a delimited format in multiple blobs.</span></span> <span data-ttu-id="90b75-837">Sınırlandırılmış biçimde günlük iletisi verileri ayrıştırmak bir istemci uygulaması kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="90b75-837">The delimited format makes it easy for a client application to parse the data in the log message.</span></span>  

<span data-ttu-id="90b75-838">Depolama çözümlemeleri için aradığınız günlük iletilerini içeren blob bulmanızı sağlar BLOB'ları (veya BLOB'ları) için adlandırma kuralı kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-838">Storage Analytics uses a naming convention for blobs that enables you to locate the blob (or blobs) that contain the log messages for which you are searching.</span></span> <span data-ttu-id="90b75-839">Örneğin, "queue/2014/07/31/1800/000001.log" adlı bir blob, kuyruk hizmeti 18:00 31 Temmuz 2014 üzerinde başlayan bir saat ile ilgili günlük iletilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="90b75-839">For example, a blob named "queue/2014/07/31/1800/000001.log" contains log messages that relate to the queue service for the hour starting at 18:00 on 31 July 2014.</span></span> <span data-ttu-id="90b75-840">"000001" Bu ilk günlük dosyası bu dönem için gösterir.</span><span class="sxs-lookup"><span data-stu-id="90b75-840">The "000001" indicates that this is the first log file for this period.</span></span> <span data-ttu-id="90b75-841">Storage Analytics ayrıca blob'un meta verilerinin bir parçası dosyasında depolanan ilk ve son günlük iletilerini damgalarının kaydeder.</span><span class="sxs-lookup"><span data-stu-id="90b75-841">Storage Analytics also records the timestamps of the first and last log messages stored in the file as part of the blob's metadata.</span></span> <span data-ttu-id="90b75-842">Blob depolama etkinleştirir adı ön ekini temel alarak bir kapsayıcıdaki blobları bulmanıza API'si: 18: 00'dan başlayarak saat için sıraya günlük verilerini içeren tüm BLOB'lar bulmak için "sıra/2014/07/31/1800." öneki kullanabilir</span><span class="sxs-lookup"><span data-stu-id="90b75-842">The API for blob storage enables you locate blobs in a container based on a name prefix: to locate all the blobs that contain queue log data for the hour starting at 18:00, you can use the prefix "queue/2014/07/31/1800."</span></span>  

<span data-ttu-id="90b75-843">Depolama Analytics arabellekleri iletileri dahili olarak oturum açın ve düzenli aralıklarla uygun blob güncelleştirir veya en son toplu günlük girişlerinin ile yeni bir tane oluşturur.</span><span class="sxs-lookup"><span data-stu-id="90b75-843">Storage Analytics buffers log messages internally and then periodically updates the appropriate blob or creates a new one with the latest batch of log entries.</span></span> <span data-ttu-id="90b75-844">Blob hizmeti gerçekleştirmelisiniz yazma sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="90b75-844">This reduces the number of writes it must perform to the blob service.</span></span>  

<span data-ttu-id="90b75-845">Benzer bir çözüm, kendi uygulamanızda uyguluyorsanız, yönetme ve güvenilirlik (olduğu sürece her günlük girişinin blob depolama alanına yazılmasını) ve Maliyet (güncelleştirmeler, uygulamanızda arabelleğe alma ve blob depolama yığınlardaki yazma) ölçeklenebilirlik arasındaki dengelemeyi dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-845">If you are implementing a similar solution in your own application, you must consider how to manage the trade-off between reliability (writing every log entry to blob storage as it happens) and cost and scalability (buffering updates in your application and writing them to blob storage in batches).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="90b75-846">Sorunları ve dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="90b75-846">Issues and considerations</span></span>
<span data-ttu-id="90b75-847">Günlük verilerini depolamak nasıl karar verirken aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="90b75-847">Consider the following points when deciding how to store log data:</span></span>  

* <span data-ttu-id="90b75-848">Olası dinamik bölümleri önler bir tablo tasarımı oluşturursanız, günlük verilerinizi verimli bir şekilde erişemiyor bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-848">If you create a table design that avoids potential hot partitions, you may find that you cannot access your log data efficiently.</span></span>  
* <span data-ttu-id="90b75-849">Günlük verileri işlemek için bir istemci genellikle çok sayıda kayıt yüklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-849">To process log data, a client often needs to load many records.</span></span>  
* <span data-ttu-id="90b75-850">Günlük verileri genellikle yapılandırılmış olsa da, blob depolama daha iyi bir çözüm olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-850">Although log data is often structured, blob storage may be a better solution.</span></span>  

### <a name="implementation-considerations"></a><span data-ttu-id="90b75-851">Uygulama konuları</span><span class="sxs-lookup"><span data-stu-id="90b75-851">Implementation considerations</span></span>
<span data-ttu-id="90b75-852">Bu bölümde önceki bölümlerde açıklanan desenleri uyguladığınızda de hesaba katılmalıdır üzere konuları bazıları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="90b75-852">This section discusses some of the considerations to bear in mind when you implement the patterns described in the previous sections.</span></span> <span data-ttu-id="90b75-853">Bu bölümde çoğunu depolama istemci kitaplığı (sürüm 4.3.0 zaman yazma) kullanarak C# ile yazılmış örnekler kullanır.</span><span class="sxs-lookup"><span data-stu-id="90b75-853">Most of this section uses examples written in C# that use the Storage Client Library (version 4.3.0 at the time of writing).</span></span>  

### <a name="retrieving-entities"></a><span data-ttu-id="90b75-854">Varlıkları alma</span><span class="sxs-lookup"><span data-stu-id="90b75-854">Retrieving entities</span></span>
<span data-ttu-id="90b75-855">Bölümünde açıklandığı gibi [sorgulamak için tasarım](#design-for-querying), en verimli sorgudur noktası sorgusu.</span><span class="sxs-lookup"><span data-stu-id="90b75-855">As discussed in the section [Design for querying](#design-for-querying), the most efficient query is a point query.</span></span> <span data-ttu-id="90b75-856">Ancak, bazı senaryolarda birden çok varlık almak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-856">However, in some scenarios you may need to retrieve multiple entities.</span></span> <span data-ttu-id="90b75-857">Bu bölüm için depolama istemci kitaplığı kullanılarak varlıkları almak için bazı ortak yaklaşımlar açıklar.</span><span class="sxs-lookup"><span data-stu-id="90b75-857">This section describes some common approaches to retrieving entities using the Storage Client Library.</span></span>  

#### <a name="executing-a-point-query-using-the-storage-client-library"></a><span data-ttu-id="90b75-858">Depolama istemci kitaplığı kullanılarak noktası sorgusu yürütme</span><span class="sxs-lookup"><span data-stu-id="90b75-858">Executing a point query using the Storage Client Library</span></span>
<span data-ttu-id="90b75-859">Noktası sorguyu yürütmek için en kolay yolu kullanmaktır **almak** sahip bir varlık alan aşağıdaki C# kod parçacığında gösterildiği gibi işlemi tablo bir **PartitionKey** "Satış" değerinin ve **RowKey** "212" değerinin:</span><span class="sxs-lookup"><span data-stu-id="90b75-859">The easiest way to execute a point query is to use the **Retrieve** table operation as shown in the following C# code snippet that retrieves an entity with a **PartitionKey** of value "Sales" and a **RowKey** of value "212":</span></span>  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

<span data-ttu-id="90b75-860">Bu örnek varlık nasıl bekliyor fark türünde olmasını alır. **EmployeeEntity**.</span><span class="sxs-lookup"><span data-stu-id="90b75-860">Notice how this example expects the entity it retrieves to be of type **EmployeeEntity**.</span></span>  

#### <a name="retrieving-multiple-entities-using-linq"></a><span data-ttu-id="90b75-861">LINQ kullanarak birden çok varlık alma</span><span class="sxs-lookup"><span data-stu-id="90b75-861">Retrieving multiple entities using LINQ</span></span>
<span data-ttu-id="90b75-862">LINQ ile depolama istemci kitaplığı kullanılarak ve bir sorgu belirterek birden çok varlık almak bir **burada** yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="90b75-862">You can retrieve multiple entities by using LINQ with Storage Client Library and specifying a query with a **where** clause.</span></span> <span data-ttu-id="90b75-863">Bir tablo taraması önlemek için her zaman içermelidir **PartitionKey** değeri WHERE yan tümcesi ve mümkünse **RowKey** tablo ve bölüm taramalar önlemek için değer.</span><span class="sxs-lookup"><span data-stu-id="90b75-863">To avoid a table scan, you should always include the **PartitionKey** value in the where clause, and if possible the **RowKey** value to avoid table and partition scans.</span></span> <span data-ttu-id="90b75-864">Tablo hizmeti nerede kullanılacak Karşılaştırma işleçleri (büyük, daha büyük veya eşit, daha az daha küçüktür veya eşit, eşit ve eşit değildir), sınırlı bir kümesini destekler yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="90b75-864">The table service supports a limited set of comparison operators (greater than, greater than or equal, less than, less than or equal, equal, and not equal) to use in the where clause.</span></span> <span data-ttu-id="90b75-865">Aşağıdaki C# kod parçacığını tüm çalışanlar, son adı ile başlayan, "B" bulur (varsayılarak **RowKey** Soyadı depolar) satış departmanında (varsayılarak **PartitionKey** bölüm adını depolar):</span><span class="sxs-lookup"><span data-stu-id="90b75-865">The following C# code snippet finds all the employees whose last name starts with "B" (assuming that the **RowKey** stores the last name) in the sales department (assuming the **PartitionKey** stores the department name):</span></span>  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

<span data-ttu-id="90b75-866">Sorgu her ikisi de nasıl belirtiyor fark bir **RowKey** ve **PartitionKey** daha iyi bir performans sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="90b75-866">Notice how the query specifies both a **RowKey** and a **PartitionKey** to ensure better performance.</span></span>  

<span data-ttu-id="90b75-867">Aşağıdaki kod örneği fluent API kullanılarak eşdeğer işlevselliğini göstermektedir (genel olarak, akıcı API'ler hakkında daha fazla bilgi için bkz [Fluent API tasarlamak için en iyi yöntemler](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):</span><span class="sxs-lookup"><span data-stu-id="90b75-867">The following code sample shows equivalent functionality using the fluent API (for more information about fluent APIs in general, see [Best Practices for Designing a Fluent API](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):</span></span>  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> <span data-ttu-id="90b75-868">Birden çok örnek katmandan **CombineFilters** üç filtre koşulları dahil etmek için yöntemler.</span><span class="sxs-lookup"><span data-stu-id="90b75-868">The sample nests multiple **CombineFilters** methods to include the three filter conditions.</span></span>  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a><span data-ttu-id="90b75-869">Sorgudan çok sayıda varlık alma</span><span class="sxs-lookup"><span data-stu-id="90b75-869">Retrieving large numbers of entities from a query</span></span>
<span data-ttu-id="90b75-870">En iyi sorgu göre tek bir varlık döndüren bir **PartitionKey** değeri ve **RowKey** değeri.</span><span class="sxs-lookup"><span data-stu-id="90b75-870">An optimal query returns an individual entity based on a **PartitionKey** value and a **RowKey** value.</span></span> <span data-ttu-id="90b75-871">Bununla birlikte, bazı senaryolarda aynı bölüme ya da birçok bölüm birçok varlıkları döndürme zorunluluğu olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-871">However, in some scenarios you may have a requirement to return many entities from the same partition or even from many partitions.</span></span>  

<span data-ttu-id="90b75-872">Her zaman tam gibi senaryolarda, uygulamanızın performansını test etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-872">You should always fully test the performance of your application in such scenarios.</span></span>  

<span data-ttu-id="90b75-873">Tablo hizmetinde bir sorgu en çok 1.000 varlıkları aynı anda döndürebilir ve en fazla beş saniyede için yürütür.</span><span class="sxs-lookup"><span data-stu-id="90b75-873">A query against the table service may return a maximum of 1,000 entities at one time and may execute for a maximum of five seconds.</span></span> <span data-ttu-id="90b75-874">Sonuç kümesi sorgu beş saniye içinde tamamlanmadı 1000'den fazla varlıklar varsa veya sorgu bölüm sınır kestiği, tablo hizmeti sonraki varlıkları kümesinin istemek istemci uygulaması etkinleştirmek için devamlılık belirteci döndürür.</span><span class="sxs-lookup"><span data-stu-id="90b75-874">If the result set contains more than 1,000 entities, if the query did not complete within five seconds, or if the query crosses the partition boundary, the Table service returns a continuation token to enable the client application to request the next set of entities.</span></span> <span data-ttu-id="90b75-875">İş devamlılığı nasıl belirteçleri hakkında daha fazla bilgi için bkz: [sorgu zaman aşımı ve sayfa numaralandırma](http://msdn.microsoft.com/library/azure/dd135718.aspx).</span><span class="sxs-lookup"><span data-stu-id="90b75-875">For more information about how continuation tokens work, see [Query Timeout and Pagination](http://msdn.microsoft.com/library/azure/dd135718.aspx).</span></span>  

<span data-ttu-id="90b75-876">Depolama istemcisi kitaplığı kullanıyorsanız, tablo hizmetinden varlıklar döndürüyor gibi otomatik olarak devamlılık belirteçleri sizin için işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-876">If you are using the Storage Client Library, it can automatically handle continuation tokens for you as it returns entities from the Table service.</span></span> <span data-ttu-id="90b75-877">Tablo hizmeti bunları bir yanıt döndürürse depolama istemci kitaplığı kullanılarak otomatik olarak aşağıdaki C# kod örneği devamlılık belirteçleri işler:</span><span class="sxs-lookup"><span data-stu-id="90b75-877">The following C# code sample using the Storage Client Library automatically handles continuation tokens if the table service returns them in a response:</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

<span data-ttu-id="90b75-878">Aşağıdaki C# kodu devamlılık belirteçleri açıkça işler:</span><span class="sxs-lookup"><span data-stu-id="90b75-878">The following C# code handles continuation tokens explicitly:</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

<span data-ttu-id="90b75-879">Devamlılık belirteçleri açıkça kullanarak, uygulamanızın veri sonraki kesimin zaman alır kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-879">By using continuation tokens explicitly, you can control when your application retrieves the next segment of data.</span></span> <span data-ttu-id="90b75-880">Örneğin, istemci uygulamanız kullanıcıların tablo içinde saklanan varlıkları aracılığıyla sayfasında olanak sağlayan, bir kullanıcı, uygulamanızın, kullanıcının geçerli kesime alanındaki tüm varlıkları sayfalama bittiğinde sonraki segment almak için devamlılık belirteci yalnızca kullanırsınız şekilde sorgu tarafından alınan tüm varlıklar aracılığıyla sayfası değil karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-880">For example, if your client application enables users to page through the entities stored in a table, a user may decide not to page through all the entities retrieved by the query so your application would only use a continuation token to retrieve the next segment when the user had finished paging through all the entities in the current segment.</span></span> <span data-ttu-id="90b75-881">Bu yaklaşımın birkaç avantaj vardır:</span><span class="sxs-lookup"><span data-stu-id="90b75-881">This approach has several benefits:</span></span>  

* <span data-ttu-id="90b75-882">Tablo hizmetinden almak için veri miktarını sınırlamak sağlar ve ağ üzerinden taşıması.</span><span class="sxs-lookup"><span data-stu-id="90b75-882">It enables you to limit the amount of data to retrieve from the Table service and that you move over the network.</span></span>  
* <span data-ttu-id="90b75-883">. NET'te zaman uyumsuz g/ç gerçekleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-883">It enables you to perform asynchronous IO in .NET.</span></span>  
* <span data-ttu-id="90b75-884">Bir uygulama çökmesi durumunda devam edebilmek için kalıcı depolama birimine devamlılık belirteci seri hale getirmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-884">It enables you to serialize the continuation token to persistent storage so you can continue in the event of an application crash.</span></span>  

> [!NOTE]
> <span data-ttu-id="90b75-885">Daha az olabilir ancak bir devamlılık belirteci 1.000 varlık içeren bir kesimi genellikle döndürür.</span><span class="sxs-lookup"><span data-stu-id="90b75-885">A continuation token typically returns a segment containing 1,000 entities, although it may be fewer.</span></span> <span data-ttu-id="90b75-886">Bir sorgunun döndürdüğü kullanarak girdi sayısı sınırlarsa da böyledir **ele** arama ölçütlerinizle eşleşen ilk n varlıklar döndürülecek: Tablo hizmeti kalan varlık almaya sağlamak için devamlılık belirteci ile birlikte n varlıklar taneden içeren bir segment döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-886">This is also the case if you limit the number of entries a query returns by using **Take** to return the first n entities that match your lookup criteria: the table service may return a segment containing fewer than n entities along with a continuation token to enable you to retrieve the remaining entities.</span></span>  
> 
> 

<span data-ttu-id="90b75-887">Aşağıdaki C# kod içinde bir kesim döndürülen varlıkların sayısını değiştirmek nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="90b75-887">The following C# code shows how to modify the number of entities returned inside a segment:</span></span>  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a><span data-ttu-id="90b75-888">Sunucu tarafı projeksiyonu</span><span class="sxs-lookup"><span data-stu-id="90b75-888">Server-side projection</span></span>
<span data-ttu-id="90b75-889">Tek bir varlık, en fazla 255 özelliklere sahip ve en çok 1 MB boyutunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-889">A single entity can have up to 255 properties and be up to 1 MB in size.</span></span> <span data-ttu-id="90b75-890">Tabloyu sorgulamak ve varlıkları almak, tüm özellikler gerekli değildir ve gereksiz yere (gecikme süresi ve maliyetini azaltmaya yardımcı olmak üzere) veri aktarımı önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-890">When you query the table and retrieve entities, you may not need all the properties and can avoid transferring data unnecessarily (to help reduce latency and cost).</span></span> <span data-ttu-id="90b75-891">Sunucu tarafı projeksiyon gereksinim özellikleri aktarmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-891">You can use server-side projection to transfer just the properties you need.</span></span> <span data-ttu-id="90b75-892">Aşağıdaki örnek alır olduğundan yalnızca **e-posta** özelliği (ile birlikte **PartitionKey**, **RowKey**, **zaman damgası**, ve **ETag**) sorgu tarafından seçilen gelen.</span><span class="sxs-lookup"><span data-stu-id="90b75-892">The following example is retrieves just the **Email** property (along with **PartitionKey**, **RowKey**, **Timestamp**, and **ETag**) from the entities selected by the query.</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

<span data-ttu-id="90b75-893">Bildirim nasıl **RowKey** değeri, almak için özellikler listesinde eklenmemiş olsa da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-893">Notice how the **RowKey** value is available even though it was not included in the list of properties to retrieve.</span></span>  

### <a name="modifying-entities"></a><span data-ttu-id="90b75-894">Varlıkları değiştirme</span><span class="sxs-lookup"><span data-stu-id="90b75-894">Modifying entities</span></span>
<span data-ttu-id="90b75-895">Depolama istemcisi kitaplığı, ekleme, silme ve varlıkları güncelleştirme tablo hizmetinde depolanan varlıklarınızı değiştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-895">The Storage Client Library enables you to modify your entities stored in the table service by inserting, deleting, and updating entities.</span></span> <span data-ttu-id="90b75-896">Birden çok ekleme, güncelleştirme ve silme işlemleri birlikte gerekli gidiş dönüş sayısını azaltmak için batch ve çözümünüzün performansını artırmak için EGTs kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-896">You can use EGTs to batch multiple insert, update, and delete operations together to reduce the number of round trips required and improve the performance of your solution.</span></span>  

<span data-ttu-id="90b75-897">Depolama istemcisi kitaplığı bir EGT genellikle yürüttüğünde oluşturulan özel durumları batch başarısız olmasına neden varlık dizinini içerdiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="90b75-897">Note that exceptions thrown when the Storage Client Library executes an EGT typically include the index of the entity that caused the batch to fail.</span></span> <span data-ttu-id="90b75-898">EGTs kullanan kodu ayıklarken bu yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-898">This is helpful when you are debugging code that uses EGTs.</span></span>  

<span data-ttu-id="90b75-899">İstemci uygulamanızı eşzamanlılık ve güncelleştirme işlemlerinin nasıl işlediğini tasarımınızı nasıl etkileyeceğini de dikkate almalısınız.</span><span class="sxs-lookup"><span data-stu-id="90b75-899">You should also consider how your design affects how your client application handles concurrency and update operations.</span></span>  

#### <a name="managing-concurrency"></a><span data-ttu-id="90b75-900">Eşzamanlılık yönetme</span><span class="sxs-lookup"><span data-stu-id="90b75-900">Managing concurrency</span></span>
<span data-ttu-id="90b75-901">Varsayılan olarak tablo hizmeti iyimser eşzamanlılık denetler ayrı varlıklar için düzeyinde uygulayan **Ekle**, **birleştirme**, ve **silmek** işlemleri, bir istemci bu denetimleri atlamak için tablo hizmeti zorlamak mümkün olsa.</span><span class="sxs-lookup"><span data-stu-id="90b75-901">By default, the table service implements optimistic concurrency checks at the level of individual entities for **Insert**, **Merge**, and **Delete** operations, although it is possible for a client to force the table service to bypass these checks.</span></span> <span data-ttu-id="90b75-902">Tablo hizmeti eşzamanlılık nasıl yönettiği hakkında daha fazla bilgi için bkz: [yönetme eşzamanlılık Microsoft Azure depolama alanında](storage-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="90b75-902">For more information about how the table service manages concurrency, see  [Managing Concurrency in Microsoft Azure Storage](storage-concurrency.md).</span></span>  

#### <a name="merge-or-replace"></a><span data-ttu-id="90b75-903">Birleştirme ya da değiştirme</span><span class="sxs-lookup"><span data-stu-id="90b75-903">Merge or replace</span></span>
<span data-ttu-id="90b75-904">**Değiştir** yöntemi **TableOperation** sınıfı her zaman tam varlık tablo hizmetinde yerini alır.</span><span class="sxs-lookup"><span data-stu-id="90b75-904">The **Replace** method of the **TableOperation** class always replaces the complete entity in the Table service.</span></span> <span data-ttu-id="90b75-905">Bu özellik saklı varlıkta mevcut olduğunda, bir özellik istekte içermiyorsa, istek bu özellik saklı varlıktan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="90b75-905">If you do not include a property in the request when that property exists in the stored entity, the request removes that property from the stored entity.</span></span> <span data-ttu-id="90b75-906">Bir özellik açıkça depolanan bir varlıktan kaldırmak istemediğiniz sürece, istekte her özellik eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b75-906">Unless you want to remove a property explicitly from a stored entity, you must include every property in the request.</span></span>  

<span data-ttu-id="90b75-907">Kullanabileceğiniz **birleştirme** yöntemi **TableOperation** bir varlığı güncelleştirmek istediğiniz zaman tablo hizmetine gönderdiğiniz veri miktarını azaltmak için sınıf.</span><span class="sxs-lookup"><span data-stu-id="90b75-907">You can use the **Merge** method of the **TableOperation** class to reduce the amount of data that you send to the Table service when you want to update an entity.</span></span> <span data-ttu-id="90b75-908">**Birleştirme** yöntemi istekte bulunan varlık özellik değerleriyle saklı varlıktaki tüm özelliklerini değiştirir, ancak istekte dahil edilmeyen saklı varlık özelliklerinde dokunmaz.</span><span class="sxs-lookup"><span data-stu-id="90b75-908">The **Merge** method replaces any properties in the stored entity with property values from the entity included in the request, but leaves intact any properties in the stored entity that are not included in the request.</span></span> <span data-ttu-id="90b75-909">Büyük varlıklar varsa ve yalnızca küçük bir istek özelliklerinde çeşitli güncelleştirmeniz gerektiğinde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-909">This is useful if you have large entities and only need to update a small number of properties in a request.</span></span>  

> [!NOTE]
> <span data-ttu-id="90b75-910">**Değiştir** ve **birleştirme** yöntemler başarısız varlık mevcut değilse.</span><span class="sxs-lookup"><span data-stu-id="90b75-910">The **Replace** and **Merge** methods fail if the entity does not exist.</span></span> <span data-ttu-id="90b75-911">Alternatif olarak, kullandığınız **Yerleştir veya Değiştir** ve **InsertOrMerge** yoksa, yeni varlık oluşturma yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-911">As an alternative, you can use the **InsertOrReplace** and **InsertOrMerge** methods that create a new entity if it doesn't exist.</span></span>  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a><span data-ttu-id="90b75-912">Heterojen varlık türleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="90b75-912">Working with heterogeneous entity types</span></span>
<span data-ttu-id="90b75-913">Tablo hizmeti bir *şema daha az* tasarımınızda büyük esneklik sağlayan birden çok tür varlıklarının tek bir tabloyu depolayabilir anlamına gelir tablo deposu.</span><span class="sxs-lookup"><span data-stu-id="90b75-913">The Table service is a *schema-less* table store that means that a single table can store entities of multiple types providing great flexibility in your design.</span></span> <span data-ttu-id="90b75-914">Aşağıdaki örnek, çalışan ve departman varlıkları depolayan bir tablo gösterir:</span><span class="sxs-lookup"><span data-stu-id="90b75-914">The following example illustrates a table storing both employee and department entities:</span></span>  

<table>
<tr>
<th><span data-ttu-id="90b75-915">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="90b75-915">PartitionKey</span></span></th>
<th><span data-ttu-id="90b75-916">RowKey</span><span class="sxs-lookup"><span data-stu-id="90b75-916">RowKey</span></span></th>
<th><span data-ttu-id="90b75-917">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="90b75-917">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-918">FirstName</span><span class="sxs-lookup"><span data-stu-id="90b75-918">FirstName</span></span></th>
<th><span data-ttu-id="90b75-919">Soyadı</span><span class="sxs-lookup"><span data-stu-id="90b75-919">LastName</span></span></th>
<th><span data-ttu-id="90b75-920">Yaş</span><span class="sxs-lookup"><span data-stu-id="90b75-920">Age</span></span></th>
<th><span data-ttu-id="90b75-921">E-posta</span><span class="sxs-lookup"><span data-stu-id="90b75-921">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-922">FirstName</span><span class="sxs-lookup"><span data-stu-id="90b75-922">FirstName</span></span></th>
<th><span data-ttu-id="90b75-923">Soyadı</span><span class="sxs-lookup"><span data-stu-id="90b75-923">LastName</span></span></th>
<th><span data-ttu-id="90b75-924">Yaş</span><span class="sxs-lookup"><span data-stu-id="90b75-924">Age</span></span></th>
<th><span data-ttu-id="90b75-925">E-posta</span><span class="sxs-lookup"><span data-stu-id="90b75-925">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-926">departmentName</span><span class="sxs-lookup"><span data-stu-id="90b75-926">DepartmentName</span></span></th>
<th><span data-ttu-id="90b75-927">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="90b75-927">EmployeeCount</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-928">FirstName</span><span class="sxs-lookup"><span data-stu-id="90b75-928">FirstName</span></span></th>
<th><span data-ttu-id="90b75-929">Soyadı</span><span class="sxs-lookup"><span data-stu-id="90b75-929">LastName</span></span></th>
<th><span data-ttu-id="90b75-930">Yaş</span><span class="sxs-lookup"><span data-stu-id="90b75-930">Age</span></span></th>
<th><span data-ttu-id="90b75-931">E-posta</span><span class="sxs-lookup"><span data-stu-id="90b75-931">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

<span data-ttu-id="90b75-932">Her varlığın hala olmalıdır Not **PartitionKey**, **RowKey**, ve **zaman damgası** değerleri, ancak herhangi bir özellikler kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-932">Note that each entity must still have **PartitionKey**, **RowKey**, and **Timestamp** values, but may have any set of properties.</span></span> <span data-ttu-id="90b75-933">Ayrıca, bir şey yok Bu bilgileri bir yerde saklamak seçmediğiniz sürece bir varlık türünü belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="90b75-933">Furthermore, there is nothing to indicate the type of an entity unless you choose to store that information somewhere.</span></span> <span data-ttu-id="90b75-934">Varlık türü tanımlamak için iki seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="90b75-934">There are two options for identifying the entity type:</span></span>  

* <span data-ttu-id="90b75-935">Varlık türü başına **RowKey** (veya büyük olasılıkla **PartitionKey**).</span><span class="sxs-lookup"><span data-stu-id="90b75-935">Prepend the entity type to the **RowKey** (or possibly the **PartitionKey**).</span></span> <span data-ttu-id="90b75-936">Örneğin, **EMPLOYEE_000123** veya **DEPARTMENT_SALES** olarak **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-936">For example, **EMPLOYEE_000123** or **DEPARTMENT_SALES** as **RowKey** values.</span></span>  
* <span data-ttu-id="90b75-937">Aşağıdaki tabloda gösterildiği gibi kayıt varlık türü için ayrı özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="90b75-937">Use a separate property to record the entity type as shown in the table below.</span></span>  

<table>
<tr>
<th><span data-ttu-id="90b75-938">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="90b75-938">PartitionKey</span></span></th>
<th><span data-ttu-id="90b75-939">RowKey</span><span class="sxs-lookup"><span data-stu-id="90b75-939">RowKey</span></span></th>
<th><span data-ttu-id="90b75-940">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="90b75-940">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-941">EntityType</span><span class="sxs-lookup"><span data-stu-id="90b75-941">EntityType</span></span></th>
<th><span data-ttu-id="90b75-942">FirstName</span><span class="sxs-lookup"><span data-stu-id="90b75-942">FirstName</span></span></th>
<th><span data-ttu-id="90b75-943">Soyadı</span><span class="sxs-lookup"><span data-stu-id="90b75-943">LastName</span></span></th>
<th><span data-ttu-id="90b75-944">Yaş</span><span class="sxs-lookup"><span data-stu-id="90b75-944">Age</span></span></th>
<th><span data-ttu-id="90b75-945">E-posta</span><span class="sxs-lookup"><span data-stu-id="90b75-945">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="90b75-946">Çalışan</span><span class="sxs-lookup"><span data-stu-id="90b75-946">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-947">EntityType</span><span class="sxs-lookup"><span data-stu-id="90b75-947">EntityType</span></span></th>
<th><span data-ttu-id="90b75-948">FirstName</span><span class="sxs-lookup"><span data-stu-id="90b75-948">FirstName</span></span></th>
<th><span data-ttu-id="90b75-949">Soyadı</span><span class="sxs-lookup"><span data-stu-id="90b75-949">LastName</span></span></th>
<th><span data-ttu-id="90b75-950">Yaş</span><span class="sxs-lookup"><span data-stu-id="90b75-950">Age</span></span></th>
<th><span data-ttu-id="90b75-951">E-posta</span><span class="sxs-lookup"><span data-stu-id="90b75-951">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="90b75-952">Çalışan</span><span class="sxs-lookup"><span data-stu-id="90b75-952">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-953">EntityType</span><span class="sxs-lookup"><span data-stu-id="90b75-953">EntityType</span></span></th>
<th><span data-ttu-id="90b75-954">departmentName</span><span class="sxs-lookup"><span data-stu-id="90b75-954">DepartmentName</span></span></th>
<th><span data-ttu-id="90b75-955">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="90b75-955">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="90b75-956">Bölüm</span><span class="sxs-lookup"><span data-stu-id="90b75-956">Department</span></span></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="90b75-957">EntityType</span><span class="sxs-lookup"><span data-stu-id="90b75-957">EntityType</span></span></th>
<th><span data-ttu-id="90b75-958">FirstName</span><span class="sxs-lookup"><span data-stu-id="90b75-958">FirstName</span></span></th>
<th><span data-ttu-id="90b75-959">Soyadı</span><span class="sxs-lookup"><span data-stu-id="90b75-959">LastName</span></span></th>
<th><span data-ttu-id="90b75-960">Yaş</span><span class="sxs-lookup"><span data-stu-id="90b75-960">Age</span></span></th>
<th><span data-ttu-id="90b75-961">E-posta</span><span class="sxs-lookup"><span data-stu-id="90b75-961">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="90b75-962">Çalışan</span><span class="sxs-lookup"><span data-stu-id="90b75-962">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

<span data-ttu-id="90b75-963">Varlık eklenmesini ilk seçenek türü için **RowKey**, farklı türlerde iki varlık aynı anahtar değerine sahip olabileceğiniz olasılığı varsa faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-963">The first option, prepending the entity type to the **RowKey**, is useful if there is a possibility that two entities of different types might have the same key value.</span></span> <span data-ttu-id="90b75-964">Ayrıca, aynı türde birlikte bölümündeki varlıklar gruplandırır.</span><span class="sxs-lookup"><span data-stu-id="90b75-964">It also groups entities of the same type together in the partition.</span></span>  

<span data-ttu-id="90b75-965">Bu bölümde açıklanan teknikleri tartışmaya yakından ilgili olan [devralma ilişkileri](#inheritance-relationships) bölümünde bu kılavuzun önceki bölümlerinde [ilişkileri modelleme](#modelling-relationships).</span><span class="sxs-lookup"><span data-stu-id="90b75-965">The techniques discussed in this section are especially relevant to the discussion [Inheritance relationships](#inheritance-relationships) earlier in this guide in the section [Modelling relationships](#modelling-relationships).</span></span>  

> [!NOTE]
> <span data-ttu-id="90b75-966">İstemci uygulamaların POCO nesneleri gelişmesi ve farklı sürümleri ile çalışmasını sağlamak için varlık türü değeri bir sürüm numarası dahil olmak üzere göz önünde bulundurmalısınız.</span><span class="sxs-lookup"><span data-stu-id="90b75-966">You should consider including a version number in the entity type value to enable client applications to evolve POCO objects and work with different versions.</span></span>  
> 
> 

<span data-ttu-id="90b75-967">Bu bölüm geri kalanı aynı tablodaki birden çok varlık türü ile çalışmayı kolaylaştırmak için depolama istemci kitaplığı özelliklerinde bazıları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="90b75-967">The remainder of this section describes some of the features in the Storage Client Library that facilitate working with multiple entity types in the same table.</span></span>  

#### <a name="retrieving-heterogeneous-entity-types"></a><span data-ttu-id="90b75-968">Heterojen varlık türleri alınıyor</span><span class="sxs-lookup"><span data-stu-id="90b75-968">Retrieving heterogeneous entity types</span></span>
<span data-ttu-id="90b75-969">Depolama istemcisi kitaplığı kullanıyorsanız, birden çok varlık türleri ile çalışmak için üç seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="90b75-969">If you are using the Storage Client Library, you have three options for working with multiple entity types.</span></span>  

<span data-ttu-id="90b75-970">Belirli bir ile depolanan varlık türünü biliyorsanız **RowKey** ve **PartitionKey** değerleri varlık türünde varlıklar almak önceki iki örneklerde gösterildiği gibi aldığınızda varlık türünü belirtebilirsiniz ardından **EmployeeEntity**: [için depolama istemci kitaplığı kullanılarak noktası sorgu yürütülürken](#executing-a-point-query-using-the-storage-client-library) ve [LINQ kullanarak birden çok varlık alma](#retrieving-multiple-entities-using-linq).</span><span class="sxs-lookup"><span data-stu-id="90b75-970">If you know the type of the entity stored with a specific **RowKey** and **PartitionKey** values, then you can specify the entity type when you retrieve the entity as shown in the previous two examples that retrieve entities of type **EmployeeEntity**: [Executing a point query using the Storage Client Library](#executing-a-point-query-using-the-storage-client-library) and [Retrieving multiple entities using LINQ](#retrieving-multiple-entities-using-linq).</span></span>  

<span data-ttu-id="90b75-971">İkinci seçenek kullanmaktır **DynamicTableEntity** türü (bir özellik paketi) yerine (Bu seçenek ayrıca performansı iyileştirebilir seri hale getirmek ve seri durumdan .NET türleri varlığa gerek yoktur çünkü) somut bir POCO varlık türü.</span><span class="sxs-lookup"><span data-stu-id="90b75-971">The second option is to use the **DynamicTableEntity** type (a property bag) instead of a concrete POCO entity type (this option may also improve performance because there is no need to serialize and deserialize the entity to .NET types).</span></span> <span data-ttu-id="90b75-972">Aşağıdaki C# kodu potansiyel olarak farklı türlerde birden çok varlık tablosundan alır, ancak tüm varlıklar olarak döndürür **DynamicTableEntity** örnekleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-972">The following C# code potentially retrieves multiple entities of different types from the table, but returns all entities as **DynamicTableEntity** instances.</span></span> <span data-ttu-id="90b75-973">Daha sonra kullanır **EntityType** özelliği her bir varlık türünü belirlemek için:</span><span class="sxs-lookup"><span data-stu-id="90b75-973">It then uses the **EntityType** property to determine the type of each entity:</span></span>  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

<span data-ttu-id="90b75-974">Kullanmalısınız diğer özelliklerini almak için unutmayın **TryGetValue** yöntemi **özellikleri** özelliği **DynamicTableEntity** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="90b75-974">Note that to retrieve other properties you must use the **TryGetValue** method on the **Properties** property of the **DynamicTableEntity** class.</span></span>  

<span data-ttu-id="90b75-975">Kullanarak birleştirmek için üçüncü seçenek olan **DynamicTableEntity** türü ve bir **Varlıkçözümleyicisi** örneği.</span><span class="sxs-lookup"><span data-stu-id="90b75-975">A third option is to combine using the **DynamicTableEntity** type and an **EntityResolver** instance.</span></span> <span data-ttu-id="90b75-976">Bu, birden çok POCO tür aynı sorguda çözümlemek sağlar.</span><span class="sxs-lookup"><span data-stu-id="90b75-976">This enables you to resolve to multiple POCO types in the same query.</span></span> <span data-ttu-id="90b75-977">Bu örnekte, **Varlıkçözümleyicisi** temsilci kullanarak **EntityType** sorgunun döndürdüğü varlık iki tür arasında ayrım yapmak için özellik.</span><span class="sxs-lookup"><span data-stu-id="90b75-977">In this example, the **EntityResolver** delegate is using the **EntityType** property to distinguish between the two types of entity that the query returns.</span></span> <span data-ttu-id="90b75-978">**Gidermek** yöntemi kullanan **çözümleyici** çözümlemek için temsilci **DynamicTableEntity** için örnekler **TableEntity** örnekleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-978">The **Resolve** method uses the **resolver** delegate to resolve **DynamicTableEntity** instances to **TableEntity** instances.</span></span>  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a><span data-ttu-id="90b75-979">Heterojen varlık türlerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="90b75-979">Modifying heterogeneous entity types</span></span>
<span data-ttu-id="90b75-980">Silmek için bir varlık türünü bilmeniz gerek yoktur ve bu eklediğinizde her zaman bir varlık türünü bilmeniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-980">You do not need to know the type of an entity to delete it, and you always know the type of an entity when you insert it.</span></span> <span data-ttu-id="90b75-981">Ancak, kullanabileceğiniz **DynamicTableEntity** türünü bilerek ve bir POCO varlık sınıfı kullanarak olmadan bir varlığı güncelleştirmek için türü.</span><span class="sxs-lookup"><span data-stu-id="90b75-981">However, you can use **DynamicTableEntity** type to update an entity without knowing its type and without using a POCO entity class.</span></span> <span data-ttu-id="90b75-982">Aşağıdaki kod örneği, tek bir varlık alır ve denetler **EmployeeCount** özellik var güncelleştirmeden önce.</span><span class="sxs-lookup"><span data-stu-id="90b75-982">The following code sample retrieves a single entity, and checks the **EmployeeCount** property exists before updating it.</span></span>  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a><span data-ttu-id="90b75-983">Paylaşılan erişim imzaları ile erişimi denetleme</span><span class="sxs-lookup"><span data-stu-id="90b75-983">Controlling access with Shared Access Signatures</span></span>
<span data-ttu-id="90b75-984">İstemci uygulamaları doğrudan tablo hizmeti ile kimlik doğrulaması gerek kalmadan doğrudan tablo varlıkları değiştirmek (ve sorgulamak) etkinleştirmek için paylaşılan erişim imzası (SAS) belirteçleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-984">You can use Shared Access Signature (SAS) tokens to enable client applications to modify (and query) table entities directly without the need to authenticate directly with the table service.</span></span> <span data-ttu-id="90b75-985">Genellikle, uygulamanızda SAS kullanarak için üç ana faydası vardır:</span><span class="sxs-lookup"><span data-stu-id="90b75-985">Typically, there are three main benefits to using SAS in your application:</span></span>  

* <span data-ttu-id="90b75-986">Erişim ve tablo hizmeti varlıklarda değiştirmek o aygıtı izin vermek üzere depolama hesabı anahtarınızı güvenli olmayan bir platforma (örneğin, bir mobil cihaz) dağıtmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="90b75-986">You do not need to distribute your storage account key to an insecure platform (such as a mobile device) in order to allow that device to access and modify entities in the Table service.</span></span>  
* <span data-ttu-id="90b75-987">Web ve çalışan rolleri varlıklarınızı son kullanıcı bilgisayarlar gibi istemci cihazları ve mobil aygıtlara yönetilmesindeki gerçekleştirmek işinin bir kısmını boşaltabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-987">You can offload some of the work that web and worker roles perform in managing your entities to client devices such as end-user computers and mobile devices.</span></span>  
* <span data-ttu-id="90b75-988">Bir kısıtlanmış atayabilir ve izinleri (örneğin, belirli kaynaklara salt okunur erişime izin verme) istemciye zaman sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="90b75-988">You can assign a constrained and time limited set of permissions to a client (such as allowing read-only access to specific resources).</span></span>  

<span data-ttu-id="90b75-989">SAS belirteci tablo hizmeti ile kullanma hakkında daha fazla bilgi için bkz: [kullanarak paylaşılan erişim imzaları (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="90b75-989">For more information about using SAS tokens with the Table service, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>  

<span data-ttu-id="90b75-990">Ancak, yine bir istemci uygulaması tablo hizmeti varlıklarla vermek SAS belirteci oluşturmanız gerekir: depolama hesabı anahtarlarını güvenli erişimi olan bir ortamda yapmalısınız.</span><span class="sxs-lookup"><span data-stu-id="90b75-990">However, you must still generate the SAS tokens that grant a client application to the entities in the table service: you should do this in an environment that has secure access to your storage account keys.</span></span> <span data-ttu-id="90b75-991">Genellikle, web veya çalışan rolü SAS belirteçleri oluşturmak ve bunları varlıklarınızı erişmesi gereken istemci uygulamaları için teslim etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="90b75-991">Typically, you use a web or worker role to generate the SAS tokens and deliver them to the client applications that need access to your entities.</span></span> <span data-ttu-id="90b75-992">Olduğundan hala bir ek yük oluşturma ve SAS belirteci istemciler için en iyi şekilde nasıl düşünmelisiniz yüksek hacimli senaryolarda özellikle bu yükünü azaltmak için teslim etmek dahil edilen.</span><span class="sxs-lookup"><span data-stu-id="90b75-992">Because there is still an overhead involved in generating and delivering SAS tokens to clients, you should consider how best to reduce this overhead, especially in high-volume scenarios.</span></span>  

<span data-ttu-id="90b75-993">Bir alt tabloda bulunan varlıklara erişim veren bir SAS belirteci oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="90b75-993">It is possible to generate a SAS token that grants access to a subset of the entities in a table.</span></span> <span data-ttu-id="90b75-994">Varsayılan olarak, tüm tablo için bir SAS belirteci oluşturur, ancak SAS belirteci bir dizi ya da erişim izni belirtmek mümkündür **PartitionKey** değerleri veya bir dizi **PartitionKey** ve **RowKey** değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b75-994">By default, you create a SAS token for an entire table, but it is also possible to specify that the SAS token grant access to either a range of **PartitionKey** values, or a range of **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="90b75-995">Her kullanıcının SAS belirteci yalnızca kendi varlıklarına erişmek için tablo hizmetinde veren şekilde sisteminizin bireysel kullanıcılar için SAS belirteci oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b75-995">You might choose to generate SAS tokens for individual users of your system such that each user's SAS token only allows them access to their own entities in the table service.</span></span>  

### <a name="asynchronous-and-parallel-operations"></a><span data-ttu-id="90b75-996">Zaman uyumsuz ve paralel işlemleri</span><span class="sxs-lookup"><span data-stu-id="90b75-996">Asynchronous and parallel operations</span></span>
<span data-ttu-id="90b75-997">İsteklerinizi birden çok bölüm arasında yayılmak sağlanan zaman uyumsuz veya paralel sorguları kullanarak verimlilik ve istemci yanıt hızını artırabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-997">Provided you are spreading your requests across multiple partitions, you can improve throughput and client responsiveness by using asynchronous or parallel queries.</span></span>
<span data-ttu-id="90b75-998">Örneğin, tablolarınızı paralel erişme iki veya daha fazla çalışan rolü örneklerine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-998">For example, you might have two or more worker role instances accessing your tables in parallel.</span></span> <span data-ttu-id="90b75-999">Ayrı ayrı çalışan rolleri bölümler belirli kümeleri için sorumlu olan veya yalnızca birden çok çalışan rolü örnekleri, her bir tablodaki tüm bölümleri erişim olanağına sahip.</span><span class="sxs-lookup"><span data-stu-id="90b75-999">You could have individual worker roles responsible for particular sets of partitions, or simply have multiple worker role instances, each able to access all the partitions in a table.</span></span>  

<span data-ttu-id="90b75-1000">Bir istemci örneği içinde depolama işlemlerini zaman uyumsuz olarak yürüterek üretilen işi artırabilir.</span><span class="sxs-lookup"><span data-stu-id="90b75-1000">Within a client instance, you can improve throughput by executing storage operations asynchronously.</span></span> <span data-ttu-id="90b75-1001">Depolama istemcisi kitaplığı zaman uyumsuz sorgular ve değişiklikleri yazma kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="90b75-1001">The Storage Client Library makes it easy to write asynchronous queries and modifications.</span></span> <span data-ttu-id="90b75-1002">Örneğin, aşağıdaki C# kodu gösterildiği gibi bir bölümdeki tüm varlıklar alır zaman uyumlu yöntemi ile başlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90b75-1002">For example, you might start with the synchronous method that retrieves all the entities in a partition as shown in the following C# code:</span></span>  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

<span data-ttu-id="90b75-1003">Sorgu zaman uyumsuz şekilde olarak çalışır, böylece bu kodu kolayca değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90b75-1003">You can easily modify this code so that the query runs asynchronously as follows:</span></span>  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

<span data-ttu-id="90b75-1004">Zaman uyumsuz Bu örnekte, zaman uyumlu sürümünden aşağıdaki değişiklikleri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90b75-1004">In this asynchronous example, you can see the following changes from the synchronous version:</span></span>  

* <span data-ttu-id="90b75-1005">Yöntem imzası artık içerir **zaman uyumsuz** değiştiricisini ve döndürür bir **görev** örneği.</span><span class="sxs-lookup"><span data-stu-id="90b75-1005">The method signature now includes the **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="90b75-1006">Çağırmak yerine **ExecuteSegmented** sonuçları, yöntemi şimdi almak için yöntemini çağırır **ExecuteSegmentedAsync** yöntemi ve kullandığı **await** sonuçlarını zaman uyumsuz olarak almak için değiştiricisi.</span><span class="sxs-lookup"><span data-stu-id="90b75-1006">Instead of calling the **ExecuteSegmented** method to retrieve results, the method now calls the **ExecuteSegmentedAsync** method and uses the **await** modifier to retrieve results asynchronously.</span></span>  

<span data-ttu-id="90b75-1007">İstemci uygulaması birden çok kez bu yöntemi çağırabilmeniz (farklı değerlere sahip **departmanı** parametresi), ve her sorgu ayrı bir iş parçacığı üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="90b75-1007">The client application can call this method multiple times (with different values for the **department** parameter), and each query will run on a separate thread.</span></span>  

<span data-ttu-id="90b75-1008">Hiçbir zaman uyumsuz sürümü olduğuna dikkat edin **yürütme** yönteminde **TableQuery** çünkü sınıf **IEnumerable** arabirimi zaman uyumsuz numaralandırması desteklemez.</span><span class="sxs-lookup"><span data-stu-id="90b75-1008">Note that there is no asynchronous version of the **Execute** method in the **TableQuery** class because the **IEnumerable** interface does not support asynchronous enumeration.</span></span>  

<span data-ttu-id="90b75-1009">Ekle, Güncelleştir ve varlıkları zaman uyumsuz olarak silin.</span><span class="sxs-lookup"><span data-stu-id="90b75-1009">You can also insert, update, and delete entities asynchronously.</span></span> <span data-ttu-id="90b75-1010">Aşağıdaki C# örnek eklemek veya çalışan varlığı değiştirmek için basit, zaman uyumlu bir yöntemi gösterir:</span><span class="sxs-lookup"><span data-stu-id="90b75-1010">The following C# example shows a simple, synchronous method to insert or replace an employee entity:</span></span>  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="90b75-1011">Güncelleştirmeyi zaman uyumsuz şekilde olarak çalışır kolayca bu kodu değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90b75-1011">You can easily modify this code so that the update runs asynchronously as follows:</span></span>  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="90b75-1012">Zaman uyumsuz Bu örnekte, zaman uyumlu sürümünden aşağıdaki değişiklikleri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90b75-1012">In this asynchronous example, you can see the following changes from the synchronous version:</span></span>  

* <span data-ttu-id="90b75-1013">Yöntem imzası artık içerir **zaman uyumsuz** değiştiricisini ve döndürür bir **görev** örneği.</span><span class="sxs-lookup"><span data-stu-id="90b75-1013">The method signature now includes the **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="90b75-1014">Çağırmak yerine **yürütme** yöntemi şimdi varlık güncelleştirileceğini yöntemini çağırır **ExecuteAsync** yöntemi ve kullandığı **await** sonuçlarını zaman uyumsuz olarak almak için değiştiricisi.</span><span class="sxs-lookup"><span data-stu-id="90b75-1014">Instead of calling the **Execute** method to update the entity, the method now calls the **ExecuteAsync** method and uses the **await** modifier to retrieve results asynchronously.</span></span>  

<span data-ttu-id="90b75-1015">İstemci uygulaması bunun gibi birden çok zaman uyumsuz yöntemleri çağırabilir ve her yöntem çağırma ayrı bir iş parçacığı üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="90b75-1015">The client application can call multiple asynchronous methods like this one, and each method invocation will run on a separate thread.</span></span>  

### <a name="credits"></a><span data-ttu-id="90b75-1016">KREDİLERİ</span><span class="sxs-lookup"><span data-stu-id="90b75-1016">Credits</span></span>
<span data-ttu-id="90b75-1017">Aşağıdaki üyeleri Azure ekibi Katkıları için teşekkür ederiz isteriz: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah ve Serdar Ozler yanı sıra Microsoft DX gelen zel Hollander.</span><span class="sxs-lookup"><span data-stu-id="90b75-1017">We would like to thank the following members of the Azure team for their contributions: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah and Serdar Ozler as well as  Tom Hollander from Microsoft DX.</span></span> 

<span data-ttu-id="90b75-1018">Biz de gözden geçirme döngüsü sırasında aşağıdaki Microsoft MVP ait değerli görüşlerini için teşekkür ederiz ister misiniz: Igor Papirov ve Edward Bakker.</span><span class="sxs-lookup"><span data-stu-id="90b75-1018">We would also like to thank the following Microsoft MVP's for their valuable feedback during review cycles: Igor Papirov and Edward Bakker.</span></span>

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png


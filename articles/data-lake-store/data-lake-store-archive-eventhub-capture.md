---
title: Azure Data Lake Store Event Hubs verilerini yakalama | Microsoft Docs
description: "Event Hubs verilerini yakalamak için kullanım Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: a9e69576958ae96d22a4eb03d0df429f0b307298
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-store-to-capture-data-from-event-hubs"></a><span data-ttu-id="71b5c-103">Event Hubs verilerini yakalamak için kullanım Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="71b5c-103">Use Azure Data Lake Store to capture data from Event Hubs</span></span>

<span data-ttu-id="71b5c-104">Azure Event Hubs tarafından alınan verileri yakalamak için Azure Data Lake Store kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="71b5c-104">Learn how to use Azure Data Lake Store to capture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71b5c-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="71b5c-105">Prerequisites</span></span>

* <span data-ttu-id="71b5c-106">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-106">**An Azure subscription**.</span></span> <span data-ttu-id="71b5c-107">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71b5c-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="71b5c-108">**Bir Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="71b5c-109">Bir oluşturma hakkında yönergeler için bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="71b5c-109">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="71b5c-110">**Bir olay hub'ları ad alanı**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="71b5c-111">Yönergeler için bkz: [bir olay hub'ları ad alanı oluşturma](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="71b5c-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="71b5c-112">Data Lake Store hesabı ve Event Hubs ad alanı aynı Azure abonelikte olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="71b5c-112">Make sure the Data Lake Store account and the Event Hubs namespace are in the same Azure subscription.</span></span>


## <a name="assign-permissions-to-event-hubs"></a><span data-ttu-id="71b5c-113">Olay hub'ları için izinleri atayın</span><span class="sxs-lookup"><span data-stu-id="71b5c-113">Assign permissions to Event Hubs</span></span>

<span data-ttu-id="71b5c-114">Bu bölümde, Event Hubs verilerini yakalamak istediğiniz bir klasörde hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71b5c-114">In this section, you create a folder within the account where you want to capture the data from Event Hubs.</span></span> <span data-ttu-id="71b5c-115">Bir Data Lake Store hesabına veri yazabilirsiniz böylece Event Hubs'a de izinleri atayın.</span><span class="sxs-lookup"><span data-stu-id="71b5c-115">You also assign permissions to Event Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="71b5c-116">Event Hubs verilerini yakalamak ve tıklayın istediğiniz Data Lake Store hesabını açın **Veri Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-116">Open the Data Lake Store account where you want to capture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="71b5c-117">![Data Lake Store Veri Gezgini](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store Veri Gezgini")</span><span class="sxs-lookup"><span data-stu-id="71b5c-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="71b5c-118">Tıklatın **yeni klasör** ve verileri yakalamak istediğiniz klasörü için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="71b5c-118">Click **New Folder** and then enter a name for folder where you want to capture the data.</span></span>

    <span data-ttu-id="71b5c-119">![Data Lake Store içinde yeni bir klasör oluşturun](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Data Lake Store içinde yeni bir klasör oluşturun")</span><span class="sxs-lookup"><span data-stu-id="71b5c-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="71b5c-120">Data Lake Store'un kökünde izinleri atayın.</span><span class="sxs-lookup"><span data-stu-id="71b5c-120">Assign permissions at the root of the Data Lake Store.</span></span> 

    <span data-ttu-id="71b5c-121">a.</span><span class="sxs-lookup"><span data-stu-id="71b5c-121">a.</span></span> <span data-ttu-id="71b5c-122">Tıklatın **Veri Gezgini**, Data Lake Store hesabı kök seçin ve ardından **erişim**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-122">Click **Data Explorer**, select the root of the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="71b5c-123">![Data Lake Store kök izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Data Lake Store kök izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="71b5c-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="71b5c-124">b.</span><span class="sxs-lookup"><span data-stu-id="71b5c-124">b.</span></span> <span data-ttu-id="71b5c-125">Altında **erişim**, tıklatın **Ekle**, tıklatın **kullanıcı veya Grup Seç**, arayın ve sonra `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="71b5c-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="71b5c-126">![Data Lake Store kök izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Data Lake Store kök izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="71b5c-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="71b5c-127">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71b5c-127">Click **Select**.</span></span>

    <span data-ttu-id="71b5c-128">c.</span><span class="sxs-lookup"><span data-stu-id="71b5c-128">c.</span></span> <span data-ttu-id="71b5c-129">Altında **izinleri atamak**, tıklatın **Select izinleri**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="71b5c-130">Ayarlama **izinleri** için **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-130">Set **Permissions** to **Execute**.</span></span> <span data-ttu-id="71b5c-131">Ayarlama **eklemek** için **bu klasör ve tüm alt öğeleri**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-131">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="71b5c-132">Ayarlama **olarak eklemek** için **erişim izni girdisi ve varsayılan izin girdisi**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-132">Set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="71b5c-133">![Data Lake Store kök izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Data Lake Store kök izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="71b5c-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="71b5c-134">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71b5c-134">Click **OK**.</span></span>

4. <span data-ttu-id="71b5c-135">Data Lake Store hesabı altında veri yakalamak istediğiniz klasör izinlerini atayın.</span><span class="sxs-lookup"><span data-stu-id="71b5c-135">Assign permissions for the folder under Data Lake Store account where you want to capture data.</span></span>

    <span data-ttu-id="71b5c-136">a.</span><span class="sxs-lookup"><span data-stu-id="71b5c-136">a.</span></span> <span data-ttu-id="71b5c-137">Tıklatın **Veri Gezgini**, Data Lake Store hesabında klasör seçin ve ardından **erişim**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-137">Click **Data Explorer**, select the folder in the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="71b5c-138">![Data Lake Store klasör izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Data Lake Store klasörün izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="71b5c-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="71b5c-139">b.</span><span class="sxs-lookup"><span data-stu-id="71b5c-139">b.</span></span> <span data-ttu-id="71b5c-140">Altında **erişim**, tıklatın **Ekle**, tıklatın **kullanıcı veya Grup Seç**, arayın ve sonra `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="71b5c-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="71b5c-141">![Data Lake Store klasör izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Data Lake Store klasörün izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="71b5c-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="71b5c-142">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71b5c-142">Click **Select**.</span></span>

    <span data-ttu-id="71b5c-143">c.</span><span class="sxs-lookup"><span data-stu-id="71b5c-143">c.</span></span> <span data-ttu-id="71b5c-144">Altında **izinleri atamak**, tıklatın **Select izinleri**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="71b5c-145">Ayarlama **izinleri** için **okuma, yazma,** ve **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-145">Set **Permissions** to **Read, Write,** and **Execute**.</span></span> <span data-ttu-id="71b5c-146">Ayarlama **eklemek** için **bu klasör ve tüm alt öğeleri**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-146">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="71b5c-147">Son olarak, ayarlamak **olarak eklemek** için **erişim izni girdisi ve varsayılan izin girdisi**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-147">Finally, set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="71b5c-148">![Data Lake Store klasör izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Data Lake Store klasörün izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="71b5c-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="71b5c-149">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71b5c-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-to-capture-data-to-data-lake-store"></a><span data-ttu-id="71b5c-150">Olay hub'ı Data Lake Store'a veri yakalamak için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="71b5c-150">Configure Event Hubs to capture data to Data Lake Store</span></span>

<span data-ttu-id="71b5c-151">Bu bölümde, bir olay hub'ları ad alanı içindeki bir Event Hub oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71b5c-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="71b5c-152">Bir Azure Data Lake Store hesabına veri yakalamak için olay hub'ı yapılandırmanız da.</span><span class="sxs-lookup"><span data-stu-id="71b5c-152">You also configure the Event Hub to capture data to an Azure Data Lake Store account.</span></span> <span data-ttu-id="71b5c-153">Bu bölümde, bir olay hub'ları ad alanı zaten oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="71b5c-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="71b5c-154">Gelen **genel bakış** bölmesi olay hub'ları ad **+ olay hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-154">From the **Overview** pane of the Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="71b5c-155">![Olay hub'ı oluşturma](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "olay hub'ı Oluştur")</span><span class="sxs-lookup"><span data-stu-id="71b5c-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="71b5c-156">Olay hub'ı Data Lake Store'a veri yakalamak için yapılandırmak için aşağıdaki değerleri girin.</span><span class="sxs-lookup"><span data-stu-id="71b5c-156">Provide the following values to configure Event Hubs to capture data to Data Lake Store.</span></span>

    <span data-ttu-id="71b5c-157">![Olay hub'ı oluşturma](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "olay hub'ı Oluştur")</span><span class="sxs-lookup"><span data-stu-id="71b5c-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="71b5c-158">a.</span><span class="sxs-lookup"><span data-stu-id="71b5c-158">a.</span></span> <span data-ttu-id="71b5c-159">Olay hub'ı için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="71b5c-159">Provide a name for the Event Hub.</span></span>
    
    <span data-ttu-id="71b5c-160">b.</span><span class="sxs-lookup"><span data-stu-id="71b5c-160">b.</span></span> <span data-ttu-id="71b5c-161">Bu öğretici için ayarlanmış **bölüm sayısı** ve **ileti bekletme** varsayılan değerlere.</span><span class="sxs-lookup"><span data-stu-id="71b5c-161">For this tutorial, set **Partition Count** and **Message Retention** to the default values.</span></span>
    
    <span data-ttu-id="71b5c-162">c.</span><span class="sxs-lookup"><span data-stu-id="71b5c-162">c.</span></span> <span data-ttu-id="71b5c-163">Ayarlama **yakalama** için **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="71b5c-163">Set **Capture** to **On**.</span></span> <span data-ttu-id="71b5c-164">Ayarlama **zaman penceresi** (sık yakalamak nasıl) ve **boyutu penceresi** (yakalamak için veri boyutu).</span><span class="sxs-lookup"><span data-stu-id="71b5c-164">Set the **Time Window** (how frequently to capture) and **Size Window** (data size to capture).</span></span> 
    
    <span data-ttu-id="71b5c-165">d.</span><span class="sxs-lookup"><span data-stu-id="71b5c-165">d.</span></span> <span data-ttu-id="71b5c-166">İçin **yakalama sağlayıcısı**seçin **Azure Data Lake Store** ve daha önce oluşturduğunuz Data Lake Store seçin.</span><span class="sxs-lookup"><span data-stu-id="71b5c-166">For **Capture Provider**, select **Azure Data Lake Store** and the select the Data Lake Store you created earlier.</span></span> <span data-ttu-id="71b5c-167">İçin **Data Lake yolu**, Data Lake Store hesabında oluşturduğunuz klasör adını girin.</span><span class="sxs-lookup"><span data-stu-id="71b5c-167">For **Data Lake Path**, enter the name of the folder you created in the Data Lake Store account.</span></span> <span data-ttu-id="71b5c-168">Yalnızca klasöre göreli yol sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="71b5c-168">You only need to provide the relative path to the folder.</span></span>

    <span data-ttu-id="71b5c-169">e.</span><span class="sxs-lookup"><span data-stu-id="71b5c-169">e.</span></span> <span data-ttu-id="71b5c-170">Bırakın **örnek yakalama dosyası adı biçimlerini** varsayılan değere.</span><span class="sxs-lookup"><span data-stu-id="71b5c-170">Leave the **Sample capture file name formats** to the default value.</span></span> <span data-ttu-id="71b5c-171">Bu seçenek yakalama klasörü altında oluşturulan klasör yapısını yönetir.</span><span class="sxs-lookup"><span data-stu-id="71b5c-171">This option governs the folder structure that is created under the capture folder.</span></span>

    <span data-ttu-id="71b5c-172">f.</span><span class="sxs-lookup"><span data-stu-id="71b5c-172">f.</span></span> <span data-ttu-id="71b5c-173">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71b5c-173">Click **Create**.</span></span>

## <a name="test-the-setup"></a><span data-ttu-id="71b5c-174">Test Kurulumu</span><span class="sxs-lookup"><span data-stu-id="71b5c-174">Test the setup</span></span>

<span data-ttu-id="71b5c-175">Artık Azure Event Hub'ına veri göndererek çözümü test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71b5c-175">You can now test the solution by sending data to the Azure Event Hub.</span></span> <span data-ttu-id="71b5c-176">Bölümündeki yönergeleri izleyin [olayları Azure Event Hubs'a gönderme](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="71b5c-176">Follow the instructions at [Send events to Azure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="71b5c-177">Veri göndermeye başla sonra belirttiğiniz klasör yapısını kullanarak Data Lake Store'da yansıtılan veri bakın.</span><span class="sxs-lookup"><span data-stu-id="71b5c-177">Once you start sending the data, you see the data reflected in Data Lake Store using the folder structure you specified.</span></span> <span data-ttu-id="71b5c-178">Örneğin, bir klasör yapısı, Data Lake Store'da aşağıdaki ekran görüntüsünde gösterildiği gibi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="71b5c-178">For example, you see a folder structure, as shown in the following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="71b5c-179">![Data Lake Store'da EventHub veri örneği](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Data Lake Store'da örnek EventHub veri")</span><span class="sxs-lookup"><span data-stu-id="71b5c-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="71b5c-180">Event Hubs'a gelen iletileri yoksa bile, olay hub'ları başlıklarını boş dosyalarıyla Data Lake Store hesabına veri yazar.</span><span class="sxs-lookup"><span data-stu-id="71b5c-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just the headers into the Data Lake Store account.</span></span> <span data-ttu-id="71b5c-181">Dosyalar, olay hub'ları oluştururken sağladığınız aynı zaman aralığında yazılır.</span><span class="sxs-lookup"><span data-stu-id="71b5c-181">The files are written at the same time interval that you provided while creating the Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="71b5c-182">Data Lake Store'da verileri analiz etme</span><span class="sxs-lookup"><span data-stu-id="71b5c-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="71b5c-183">Data Lake Store'da verileri olduktan sonra analitik işleri işlemi ve crunch veri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71b5c-183">Once the data is in Data Lake Store, you can run analytical jobs to process and crunch the data.</span></span> <span data-ttu-id="71b5c-184">Bkz: [USQL Avro örnek](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) kullanarak Azure Data Lake Analytics bunu konusunda.</span><span class="sxs-lookup"><span data-stu-id="71b5c-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how to do this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="71b5c-185">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="71b5c-185">See also</span></span>
* [<span data-ttu-id="71b5c-186">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="71b5c-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="71b5c-187">Azure Storage Bloblarından Data Lake Store'a veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="71b5c-187">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)

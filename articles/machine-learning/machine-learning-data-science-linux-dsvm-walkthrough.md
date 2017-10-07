---
title: "Merhaba Linux veri bilimi sanal makine üzerinde aaaData Bilim | Microsoft Docs"
description: "Nasıl tooperform birçok ortak veri bilimi hello Linux veri bilimi VM ile görevler."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a><span data-ttu-id="0e89f-103">Veri bilimi hello Linux veri bilimi sanal makine üzerinde</span><span class="sxs-lookup"><span data-stu-id="0e89f-103">Data science on hello Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="0e89f-104">Bu anlatımda tooperform birçok ortak veri bilimi hello Linux veri bilimi VM ile nasıl görevler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-104">This walkthrough shows you how tooperform several common data science tasks with hello Linux Data Science VM.</span></span> <span data-ttu-id="0e89f-105">Merhaba Linux veri bilimi sanal makine (DSVM) veri analizi ve makine öğrenme için yaygın olarak kullanılan bir araç koleksiyonu ile önceden yüklenmiş olan Azure üzerinde kullanılabilir bir sanal makine görüntüdür.</span><span class="sxs-lookup"><span data-stu-id="0e89f-105">hello Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="0e89f-106">Merhaba anahtar yazılım bileşenleri hello dökümü [sağlama hello Linux veri bilimi sanal makine](machine-learning-data-science-linux-dsvm-intro.md) konu.</span><span class="sxs-lookup"><span data-stu-id="0e89f-106">hello key software components are itemized in hello [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="0e89f-107">Merhaba VM görüntüsü kolay tooget kolaylaştırır tooinstall gerek kalmadan dakika cinsinden veri bilimi yapılması başlatıldı ve hello araçların her biri ayrı ayrı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0e89f-107">hello VM image makes it easy tooget started doing data science in minutes, without having tooinstall and configure each of hello tools individually.</span></span> <span data-ttu-id="0e89f-108">Kolayca VM hello gerekirse ölçekleme ve uygulamayı kullanılmadığında durdurun.</span><span class="sxs-lookup"><span data-stu-id="0e89f-108">You can easily scale up hello VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="0e89f-109">Bu nedenle bu kaynak, esnek ve ekonomik içindir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="0e89f-110">Merhaba bu kılavuzda gösterilen veri bilimi görevleri hello özetlenen hello adımları [takım veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="0e89f-110">hello data science tasks demonstrated in this walkthrough follow hello steps outlined in hello [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="0e89f-111">Bu işlem, veri bilimcilerine tooeffectively işbirliği akıllı uygulamaları oluşturma hello ömrü ekiplerin sağlayan sistematik bir yaklaşım toodata bilimsel sunar.</span><span class="sxs-lookup"><span data-stu-id="0e89f-111">This process provides a systematic approach toodata science that enables teams of data scientists tooeffectively collaborate over hello lifecycle of building intelligent applications.</span></span> <span data-ttu-id="0e89f-112">Merhaba veri bilimi işlemi da bir kişi tarafından izlenebilir veri bilimi için yinelemeli bir çerçeve sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e89f-112">hello data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="0e89f-113">Biz hello analiz [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) bu kılavuzda veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="0e89f-113">We analyze hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="0e89f-114">Bu e-postaların istenmeyen posta ya da (olmadıkları istenmeyen posta anlamına gelir) ham, olarak işaretlenmiş kümesidir ve ayrıca bazı istatistiklerle hello e-postaları Merhaba içeriğine içerir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on hello content of hello emails.</span></span> <span data-ttu-id="0e89f-115">Merhaba istatistikleri dahil hello sonraki bir bölümü ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-115">hello statistics included are discussed in hello next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e89f-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0e89f-116">Prerequisites</span></span>
<span data-ttu-id="0e89f-117">Linux veri bilimi sanal makine kullanmadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0e89f-117">Before you can use a Linux Data Science Virtual Machine, you must have hello following:</span></span>

* <span data-ttu-id="0e89f-118">Bir **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-118">An **Azure subscription**.</span></span> <span data-ttu-id="0e89f-119">Zaten bir yoksa, bkz: [ücretsiz Azure hesabınızı bugün oluşturmak](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="0e89f-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="0e89f-120">A [ **Linux veri bilimi VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="0e89f-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="0e89f-121">Bu VM sağlama hakkında daha fazla bilgi için bkz: [sağlama hello Linux veri bilimi sanal makine](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="0e89f-121">For information on provisioning this VM, see [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="0e89f-122">[X2Go](http://wiki.x2go.org/doku.php) bilgisayarınızda yüklü ve bir XFCE oturumu açılır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="0e89f-123">Yükleme ve yapılandırma hakkında bilgi için bir **X2Go istemci**, bkz: [yükleme ve yapılandırma X2Go istemci](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="0e89f-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="0e89f-124">Bir **AzureML hesap**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-124">An **AzureML account**.</span></span> <span data-ttu-id="0e89f-125">Bir hello en yeni bir kayıt zaten yoksa, [AzureML giriş sayfası](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="0e89f-125">If you don't already have one, sign up for new one at hello [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="0e89f-126">Kullanmaya başlama ücretsiz kullanım katmanı toohelp yoktur.</span><span class="sxs-lookup"><span data-stu-id="0e89f-126">There is a free usage tier toohelp you get started.</span></span>

## <a name="download-hello-spambase-dataset"></a><span data-ttu-id="0e89f-127">Merhaba spambase dataset indirin</span><span class="sxs-lookup"><span data-stu-id="0e89f-127">Download hello spambase dataset</span></span>
<span data-ttu-id="0e89f-128">Merhaba [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) veri kümesi yalnızca 4601 örnekleri içeren veri görece küçük kümesidir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="0e89f-129">Bu kullanışlı boyutu toouse hello veri bilimi VM şekilde hello önemli özelliklerinden bazıları tutmasını hello kaynak gereksinimlerini uygun gösteren durumdur.</span><span class="sxs-lookup"><span data-stu-id="0e89f-129">This is a convenient size toouse when demonstrating that some of hello key features of hello Data Science VM as it keeps hello resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="0e89f-130">Bu kılavuz bir D2 v2 ölçekli Linux veri bilimi sanal makinede oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="0e89f-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="0e89f-131">Bu boyut DSVM hello yordamları bu kılavuzda işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-131">This size DSVM is capable of handling hello procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="0e89f-132">Daha fazla depolama alanı gerekiyorsa, ek diskleri oluşturma ve bunları tooyour VM ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e89f-132">If you need more storage space, you can create additional disks and attach them tooyour VM.</span></span> <span data-ttu-id="0e89f-133">Hello sunucu bile sağlama verilerini son korunur şekilde bu diskleri kalıcı Azure depolama kullanan tooresizing veya kapatılır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-133">These disks use persistent Azure storage, so their data is preserved even when hello server is reprovisioned due tooresizing or is shut down.</span></span> <span data-ttu-id="0e89f-134">tooadd bir disk ve tooyour VM ekleme, hello yönergeleri izleyin [disk tooa Linux VM eklemek](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e89f-134">tooadd a disk and attach it tooyour VM, follow hello instructions in [Add a disk tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0e89f-135">Bu adımları hello DSVM hello üzerinde önceden yüklenmiş Azure komut satırı arabirimi (Azure CLI) kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e89f-135">These steps use hello Azure Command-Line Interface (Azure CLI), which is already installed on hello DSVM.</span></span> <span data-ttu-id="0e89f-136">Bu nedenle bu yordamları tamamen hello VM kendisini ' yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-136">So these procedures can be done entirely from hello VM itself.</span></span> <span data-ttu-id="0e89f-137">Başka bir seçenek tooincrease depolama toouse olan [Azure dosyaları](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0e89f-137">Another option tooincrease storage is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="0e89f-138">toodownload hello verileri, bir terminal penceresi açın ve şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-138">toodownload hello data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="0e89f-139">Merhaba indirilen dosya bir başlık satırı yok, sağlandığından üstbilgi sahip başka bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e89f-139">hello downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="0e89f-140">Bu komut toocreate hello uygun üst bilgilerle bir dosya çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-140">Run this command toocreate a file with hello appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="0e89f-141">Ardından hello komutu ile birlikte hello iki dosyaları birleştirme:</span><span class="sxs-lookup"><span data-stu-id="0e89f-141">Then concatenate hello two files together with hello command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="0e89f-142">Hello dataset istatistikleri çeşitli türlerde her e-postaya sahiptir:</span><span class="sxs-lookup"><span data-stu-id="0e89f-142">hello dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="0e89f-143">Sütunları ister ***word\_freq\_WORD*** eşleşen hello e-posta sözcükleri hello yüzdesini belirtmek *WORD*.</span><span class="sxs-lookup"><span data-stu-id="0e89f-143">Columns like ***word\_freq\_WORD*** indicate hello percentage of words in hello email that match *WORD*.</span></span> <span data-ttu-id="0e89f-144">Örneğin, varsa *word\_freq\_olun* %1 hello e-posta içindeki tüm sözcükleri bundan sonra 1 ' dir *olun*.</span><span class="sxs-lookup"><span data-stu-id="0e89f-144">For example, if *word\_freq\_make* is 1, then 1% of all words in hello email were *make*.</span></span>
* <span data-ttu-id="0e89f-145">Sütunları ister ***char\_freq\_CHAR*** olan tüm hello e-posta karakter hello yüzdesini belirtmek *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="0e89f-145">Columns like ***char\_freq\_CHAR*** indicate hello percentage of all characters in hello email that were *CHAR*.</span></span>
* <span data-ttu-id="0e89f-146">***büyük\_çalıştırmak\_uzunluğu\_uzun*** hello uzun büyük harf bir dizi uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="0e89f-146">***capital\_run\_length\_longest*** is hello longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="0e89f-147">***büyük\_çalıştırmak\_uzunluğu\_ortalama*** büyük harfle tüm sıralarının hello ortalama uzunluğudur.</span><span class="sxs-lookup"><span data-stu-id="0e89f-147">***capital\_run\_length\_average*** is hello average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="0e89f-148">***büyük\_çalıştırmak\_uzunluğu\_toplam*** büyük harfle tüm sıralarının hello toplam uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="0e89f-148">***capital\_run\_length\_total*** is hello total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="0e89f-149">***istenmeyen posta*** hello e-posta istenmeyen posta kabul olup olmadığını gösterir (1 istenmeyen posta, 0 = değil istenmeyen posta =).</span><span class="sxs-lookup"><span data-stu-id="0e89f-149">***spam*** indicates whether hello email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-hello-dataset-with-microsoft-r-open"></a><span data-ttu-id="0e89f-150">Microsoft R açık Hello kümesiyle keşfedin</span><span class="sxs-lookup"><span data-stu-id="0e89f-150">Explore hello dataset with Microsoft R Open</span></span>
<span data-ttu-id="0e89f-151">Şimdi hello verileri incelemek ve bazı temel machine learning ile veri bilimi VM ile birlikte gelen r hello yapın [Microsoft R açık](https://mran.revolutionanalytics.com/open/) önceden yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="0e89f-151">Let's examine hello data and do some basic machine learning with R. hello Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="0e89f-152">Merhaba birden çok iş parçacıklı matematik kitaplıkları R bu sürümündeki çeşitli tek iş parçacıklı sürümleri daha iyi performans sunar.</span><span class="sxs-lookup"><span data-stu-id="0e89f-152">hello multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="0e89f-153">Microsoft R açık de yeniden Üretilebilirlik hello CRAN Paket Deposu görüntüsünü kullanarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e89f-153">Microsoft R Open also provides reproducibility by using a snapshot of hello CRAN package repository.</span></span>

<span data-ttu-id="0e89f-154">Merhaba tooget kopyalarını kod örnekleri bu kılavuzda, kopya hello kullanılan **Azure-Machine-Learning-Data-Bilim** hello VM üzerinde önceden yüklenmiş olduğu git, kullanarak deposu.</span><span class="sxs-lookup"><span data-stu-id="0e89f-154">tooget copies of hello code samples used in this walkthrough, clone hello **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on hello VM.</span></span> <span data-ttu-id="0e89f-155">Merhaba git komut satırından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-155">From hello git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="0e89f-156">Bir terminal penceresi açın ve hello R etkileşimli konsolu ile yeni bir R oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="0e89f-156">Open a terminal window and start a new R session with hello R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="0e89f-157">Rstudio'dan yordamları izleyerek hello için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e89f-157">You can also use RStudio for hello following procedures.</span></span> <span data-ttu-id="0e89f-158">tooinstall Rstudio'dan, bir terminal, bu komutu yürütün:`./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="0e89f-158">tooinstall RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="0e89f-159">tooimport hello veri ve hello ortamı kurma çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-159">tooimport hello data and set up hello environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="0e89f-160">Her sütunun hakkında özet istatistikleri toosee:</span><span class="sxs-lookup"><span data-stu-id="0e89f-160">toosee summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="0e89f-161">Merhaba verileri farklı bir görünüm için:</span><span class="sxs-lookup"><span data-stu-id="0e89f-161">For a different view of hello data:</span></span>

    str(data)

<span data-ttu-id="0e89f-162">Bu, her bir değişken türü hello ve ilk birkaç değerleri hello kümesindeki hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-162">This shows you hello type of each variable and hello first few values in hello dataset.</span></span>

<span data-ttu-id="0e89f-163">Merhaba *istenmeyen posta* sütun bir tamsayı olarak okundu, ancak gerçekte kategorik olan değişkeni (veya faktörü).</span><span class="sxs-lookup"><span data-stu-id="0e89f-163">hello *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="0e89f-164">tooset türü:</span><span class="sxs-lookup"><span data-stu-id="0e89f-164">tooset its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="0e89f-165">toodo bazı keşif analiz, kullanım hello [ggplot2](http://ggplot2.org/) paketini, hello VM üzerinde zaten yüklü R için popüler bir grafik kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="0e89f-165">toodo some exploratory analysis, use hello [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on hello VM.</span></span> <span data-ttu-id="0e89f-166">, Daha önce görüntülenen hello Özet verilerden biz Özet istatistikleri hello ünlem işareti karakteri hello sıklığını sahip olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0e89f-166">Note, from hello summary data displayed earlier, that we have summary statistics on hello frequency of hello exclamation mark character.</span></span> <span data-ttu-id="0e89f-167">Şimdi bu sıklıklarını burada komutları aşağıdaki hello çizimi:</span><span class="sxs-lookup"><span data-stu-id="0e89f-167">Let's plot those frequencies here with hello following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="0e89f-168">Şimdi Hello sıfır çubuğu hello çizim eğriltme olduğundan, bunu kurtulun:</span><span class="sxs-lookup"><span data-stu-id="0e89f-168">Since hello zero bar is skewing hello plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="0e89f-169">Önemsiz olmayan yoğunluğu ilginç görünüyor 1 yukarıda yoktur.</span><span class="sxs-lookup"><span data-stu-id="0e89f-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="0e89f-170">Bu verileri yalnızca bakalım:</span><span class="sxs-lookup"><span data-stu-id="0e89f-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="0e89f-171">Ardından istenmeyen posta vs ham tarafından böl:</span><span class="sxs-lookup"><span data-stu-id="0e89f-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="0e89f-172">Bu örnekler, toomake benzer çizimleri Merhaba, diğer sütunları tooexplore etkinleştirmelisiniz hello içerdikleri veriler.</span><span class="sxs-lookup"><span data-stu-id="0e89f-172">These examples should enable you toomake similar plots of hello other columns tooexplore hello data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="0e89f-173">Eğitme ve test ML modeli</span><span class="sxs-lookup"><span data-stu-id="0e89f-173">Train and test an ML model</span></span>
<span data-ttu-id="0e89f-174">Şimdi tren birkaç machine learning tooclassify hello hello dataset postalarda modeller artık ya da içerecek şekilde span veya ham.</span><span class="sxs-lookup"><span data-stu-id="0e89f-174">Now let's train a couple of machine learning models tooclassify hello emails in hello dataset as containing either span or ham.</span></span> <span data-ttu-id="0e89f-175">Biz karar ağacı modeli ve bu bölümdeki rastgele orman modeli eğitmek ve kendi tahminleri kendi doğruluğunu test edin.</span><span class="sxs-lookup"><span data-stu-id="0e89f-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="0e89f-176">koddan hello kullanılan hello rpart (özyinelemeli bölümlendirme ve regresyon ağaçlarında) paket hello veri bilimi VM üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="0e89f-176">hello rpart (Recursive Partitioning and Regression Trees) package used in hello following code is already installed on hello Data Science VM.</span></span>
>
>

<span data-ttu-id="0e89f-177">İlk olarak, şimdi hello dataset eğitim ve test ayarlar böl:</span><span class="sxs-lookup"><span data-stu-id="0e89f-177">First, let's split hello dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="0e89f-178">Ve ardından e-postaları karar ağacı tooclassify hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e89f-178">And then create a decision tree tooclassify hello emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="0e89f-179">Merhaba sonuç şöyledir:</span><span class="sxs-lookup"><span data-stu-id="0e89f-179">Here is hello result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="0e89f-181">ne kadar iyi üzerinde hello eğitim gerçekleştirir toodetermine ayarlamak, koddan hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-181">toodetermine how well it performs on hello training set, use hello following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="0e89f-182">toodetermine ne kadar iyi hello test kümesinde gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="0e89f-182">toodetermine how well it performs on hello test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="0e89f-183">Ayrıca bir rastgele orman modeli deneyelim.</span><span class="sxs-lookup"><span data-stu-id="0e89f-183">Let's also try a random forest model.</span></span> <span data-ttu-id="0e89f-184">Rastgele ormanları karar ağaçları çok sayıda eğitmek ve tüm hello ayrı ayrı karar ağaçları hello sınıflandırmaları hello modunun bir sınıf çıkış.</span><span class="sxs-lookup"><span data-stu-id="0e89f-184">Random forests train a multitude of decision trees and output a class that is hello mode of hello classifications from all of hello individual decision trees.</span></span> <span data-ttu-id="0e89f-185">Karar ağacı modeli toooverfit bir eğitim veri kümesi hello eğilimi için düzeltirken yaklaşım öğrenme daha güçlü bir makine sağlarlar.</span><span class="sxs-lookup"><span data-stu-id="0e89f-185">They provide a more powerful machine learning approach as they correct for hello tendency of a decision tree model toooverfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a><span data-ttu-id="0e89f-186">Model tooAzure ML dağıtma</span><span class="sxs-lookup"><span data-stu-id="0e89f-186">Deploy a model tooAzure ML</span></span>
<span data-ttu-id="0e89f-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML), kolay toobuild kolaylaştırır ve Tahmine dayalı analiz modelleriniz dağıtan bir bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy toobuild and deploy predictive analytics models.</span></span> <span data-ttu-id="0e89f-188">AzureML iyi özelliklerini hello herhangi R işlev bir web hizmeti olarak kendi yeteneği toopublish biridir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-188">One of hello nice features of AzureML is its ability toopublish any R function as a web service.</span></span> <span data-ttu-id="0e89f-189">Merhaba AzureML R paketi dağıtımı kolay toodo DSVM hello üzerinde bizim R oturumundan sağ hale getirir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-189">hello AzureML R package makes deployment easy toodo right from our R session on hello DSVM.</span></span>

<span data-ttu-id="0e89f-190">toodeploy hello karar ağacı kod hello önceki bölümdeki tooAzure Machine Learning Studio toosign gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-190">toodeploy hello decision tree code from hello previous section, you need toosign in tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="0e89f-191">Çalışma alanı Kimliğinizi ve bir yetkilendirme belirteci toosign gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-191">You need your workspace ID and an authorization token toosign in.</span></span> <span data-ttu-id="0e89f-192">toofind bu değerleri ve onlarla Initialize hello AzureML değişkenleri:</span><span class="sxs-lookup"><span data-stu-id="0e89f-192">toofind these values and initialize hello AzureML variables with them:</span></span>

<span data-ttu-id="0e89f-193">Seçin **ayarları** hello sol menüdeki.</span><span class="sxs-lookup"><span data-stu-id="0e89f-193">Select **Settings** on hello left-hand menu.</span></span> <span data-ttu-id="0e89f-194">Not, **çalışma alanı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="0e89f-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="0e89f-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="0e89f-196">Seçin **yetkilendirme belirteçleri** hello genel gider menüsünden ve Not, **birincil yetkilendirme belirteci**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="0e89f-196">Select **Authorization Tokens** from hello overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="0e89f-197">Yük hello **AzureML** paketini ve belirteç ve çalışma alanı Kimliğiniz ile Merhaba değişkenlerin değerleri R oturumunuzda DSVM hello üzerinde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-197">Load hello **AzureML** package and then set values of hello variables with your token and workspace ID in your R session on hello DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="0e89f-198">Şimdi bu tanıtımı daha kolay tooimplement hello modeli toomake basitleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e89f-198">Let's simplify hello model toomake this demonstration easier tooimplement.</span></span> <span data-ttu-id="0e89f-199">Merhaba üç değişkenleri hello karar ağacı en yakın toohello kök dizininde seçin ve yalnızca bu üç değişkenin kullanarak yeni bir ağaç yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-199">Pick hello three variables in hello decision tree closest toohello root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="0e89f-200">Merhaba özellikleri bir girdi olarak alır tahmin işlevinde ihtiyacımız ve tahmin edilen değerler döndürür hello:</span><span class="sxs-lookup"><span data-stu-id="0e89f-200">We need a prediction function that takes hello features as an input and returns hello predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="0e89f-201">Yayımlama Hello kullanarak hello predictSpam işlevi tooAzureML **publishWebService** işlevi:</span><span class="sxs-lookup"><span data-stu-id="0e89f-201">Publish hello predictSpam function tooAzureML using hello **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="0e89f-202">Bu işlev hello alır **predictSpam** işlev, adlı bir web hizmeti oluşturur **spamWebService** girişleri ve çıkışları ile tanımlanan ve hello yeni uç noktası hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-202">This function takes hello **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about hello new endpoint.</span></span>

<span data-ttu-id="0e89f-203">Merhaba ayrıntılarını görüntüleme web hizmeti, kendi API uç noktası ve erişim anahtarları hello komutuyla dahil yayımlanan:</span><span class="sxs-lookup"><span data-stu-id="0e89f-203">View details of hello published web service, including its API endpoint and access keys with hello command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="0e89f-204">tootry, çıkışı hello hello test kümesinin ilk 10 satır:</span><span class="sxs-lookup"><span data-stu-id="0e89f-204">tootry it out on hello first 10 rows of hello test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="0e89f-205">Kullanılabilir diğer araçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="0e89f-205">Use other tools available</span></span>
<span data-ttu-id="0e89f-206">Merhaba kalan bölümleri nasıl hello araçlardan bazıları yüklü toouse hello Linux veri bilimi VM gösterir. Açıklanan araçları hello listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="0e89f-206">hello remaining sections show how toouse some of hello tools installed on hello Linux Data Science VM.Here is hello list of tools discussed:</span></span>

* <span data-ttu-id="0e89f-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="0e89f-207">XGBoost</span></span>
* <span data-ttu-id="0e89f-208">Python</span><span class="sxs-lookup"><span data-stu-id="0e89f-208">Python</span></span>
* <span data-ttu-id="0e89f-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="0e89f-209">Jupyterhub</span></span>
* <span data-ttu-id="0e89f-210">Çıngırağı</span><span class="sxs-lookup"><span data-stu-id="0e89f-210">Rattle</span></span>
* <span data-ttu-id="0e89f-211">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="0e89f-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="0e89f-212">SQL Server veri ambarı</span><span class="sxs-lookup"><span data-stu-id="0e89f-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="0e89f-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="0e89f-213">XGBoost</span></span>
<span data-ttu-id="0e89f-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) hızlı ve doğru boosted ağaç uygulaması sağlayan bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

<span data-ttu-id="0e89f-215">XGBoost, python veya bir komut satırından da çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e89f-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="0e89f-216">Python</span><span class="sxs-lookup"><span data-stu-id="0e89f-216">Python</span></span>
<span data-ttu-id="0e89f-217">Python kullanarak geliştirme için hello Anaconda Python dağıtımları 2.7 ve 3.5 hello DSVM yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="0e89f-217">For development using Python, hello Anaconda Python distributions 2.7 and 3.5 have been installed in hello DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="0e89f-218">Merhaba Anaconda dağıtım içeren [Condas](http://conda.pydata.org/docs/index.html), hangi kullanılan toocreate farklı sürümlerini ve/veya bunları yüklü olan paketleri sahip Python için özel ortamları olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-218">hello Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used toocreate custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="0e89f-219">Şimdi hello spambase dataset bazıları okuyun ve Destek vektör scikit makinelerinizde ile Merhaba e-postaları sınıflandırmak-öğrenin:</span><span class="sxs-lookup"><span data-stu-id="0e89f-219">Let's read in some of hello spambase dataset and classify hello emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="0e89f-220">toomake tahminleri:</span><span class="sxs-lookup"><span data-stu-id="0e89f-220">toomake predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="0e89f-221">tooshow nasıl toopublish bir AzureML uç nokta, şimdi yapma daha basit bir model hello üç değişkenleri olarak biz hello R modeli önceden yayımlandığında yaptığımız.</span><span class="sxs-lookup"><span data-stu-id="0e89f-221">tooshow how toopublish an AzureML endpoint, let's make a simpler model hello three variables as we did when we published hello R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="0e89f-222">toopublish hello modeli tooAzureML:</span><span class="sxs-lookup"><span data-stu-id="0e89f-222">toopublish hello model tooAzureML:</span></span>

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="0e89f-223">Bu, yalnızca python 2.7 için kullanılabilir ve 3.5 henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="0e89f-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="0e89f-224">Çalıştırma **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="0e89f-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="0e89f-225">Jupyterhub</span></span>
<span data-ttu-id="0e89f-226">Merhaba Anaconda hello dağıtımlarında DSVM Jupyter Not Defteri, platformlar arası ortamda tooshare Python, R veya Jale kodunu ve analiz ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-226">hello Anaconda distribution in hello DSVM comes with a Jupyter notebook, a cross-platform environment tooshare Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="0e89f-227">Merhaba Jupyter not defteri JupyterHub erişilir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-227">hello Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="0e89f-228">Yerel Linux kullanıcı adı ve parola kullanarak oturum ***https://\<VM DNS adı veya IP adresi\>: 8000 /***.</span><span class="sxs-lookup"><span data-stu-id="0e89f-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="0e89f-229">Tüm yapılandırma dosyalarını JupyterHub için dizinde bulunan **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="0e89f-230">Birkaç örnek not defterlerini hello VM üzerinde zaten yüklenir:</span><span class="sxs-lookup"><span data-stu-id="0e89f-230">Several sample notebooks are already installed on hello VM:</span></span>

* <span data-ttu-id="0e89f-231">Merhaba bkz [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) bir örnek Python not defteri için.</span><span class="sxs-lookup"><span data-stu-id="0e89f-231">See hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="0e89f-232">Bkz: [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) bir örnek için **R** dizüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="0e89f-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="0e89f-233">Merhaba bkz [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) başka bir örnek için **Python** dizüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="0e89f-233">See hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="0e89f-234">Merhaba Jale dil hello Linux veri bilimi VM üzerinde hello komut satırından da mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="0e89f-234">hello Julia language is also available from hello command line on hello Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="0e89f-235">Çıngırağı</span><span class="sxs-lookup"><span data-stu-id="0e89f-235">Rattle</span></span>
<span data-ttu-id="0e89f-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (R analitik aracı tooLearn kolayca hello) veri araştırma için grafiksel bir R aracıdır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (hello R Analytical Tool tooLearn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="0e89f-237">Kolay tooload kolaylaştırır sezgisel bir arabirim sahip, keşfetmek, veri dönüştürme ve yapı ve modelleri değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="0e89f-237">It has an intuitive interface that makes it easy tooload, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="0e89f-238">Merhaba makale [Rattle: bir veri madenciliği GUI r](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) özelliklerini gösteren bir kılavuz sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e89f-238">hello article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="0e89f-239">Yükleyin ve aşağıdaki komutları hello ile Çıngırağı başlatın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-239">Install and start Rattle with hello following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="0e89f-240">Yükleme DSVM hello üzerinde gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-240">Installation is not required on hello DSVM.</span></span> <span data-ttu-id="0e89f-241">Ancak Çıngırağı onu yüklediğinde tooinstall ek paketler isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-241">But Rattle may prompt you tooinstall additional packages when it loads.</span></span>
>
>

<span data-ttu-id="0e89f-242">Çıngırağı sekmesini tabanlı bir arabirim kullanır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="0e89f-243">Merhaba sekmeleri çoğunu karşılık hello toosteps [veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)veri yükleme veya araştırma gibi.</span><span class="sxs-lookup"><span data-stu-id="0e89f-243">Most of hello tabs correspond toosteps in hello [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="0e89f-244">Sol tooright hello sekmeleri üzerinden gelen Hello veri bilimi işlemi akar.</span><span class="sxs-lookup"><span data-stu-id="0e89f-244">hello data science process flows from left tooright through hello tabs.</span></span> <span data-ttu-id="0e89f-245">Ancak hello R komutlarını tarafından Çıngırağı Çalıştır günlüğünü hello son sekme içerir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-245">But hello last tab contains a log of hello R commands run by Rattle.</span></span>

<span data-ttu-id="0e89f-246">tooload ve hello dataset yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-246">tooload and configure hello dataset:</span></span>

* <span data-ttu-id="0e89f-247">tooload hello dosya, select hello **veri** sekmesinde, ardından</span><span class="sxs-lookup"><span data-stu-id="0e89f-247">tooload hello file, select hello **Data** tab, then</span></span>
* <span data-ttu-id="0e89f-248">Merhaba Seçici sonraki çok seçin**Filename** ve **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-248">Choose hello selector next too**Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="0e89f-249">tooload hello dosyası.</span><span class="sxs-lookup"><span data-stu-id="0e89f-249">tooload hello file.</span></span> <span data-ttu-id="0e89f-250">seçin **yürütme** düğmelerinin üst satırda hello.</span><span class="sxs-lookup"><span data-stu-id="0e89f-250">select **Execute** in hello top row of buttons.</span></span> <span data-ttu-id="0e89f-251">Bir giriş, bir hedef veya başka bir değişken türü ve benzersiz değerlerin sayısını hello olup olmadığını, belirtilen veri türü de dahil olmak üzere her bir sütunun özetini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and hello number of unique values.</span></span>
* <span data-ttu-id="0e89f-252">Çıngırağı hello doğru tanımlanan **istenmeyen posta** hello hedefi olarak sütun.</span><span class="sxs-lookup"><span data-stu-id="0e89f-252">Rattle has correctly identified hello **spam** column as hello target.</span></span> <span data-ttu-id="0e89f-253">Select hello istenmeyen posta sütun sonra kümesi hello **hedef veri türü** çok**Categoric**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-253">Select hello spam column, then set hello **Target Data Type** too**Categoric**.</span></span>

<span data-ttu-id="0e89f-254">tooexplore hello verileri:</span><span class="sxs-lookup"><span data-stu-id="0e89f-254">tooexplore hello data:</span></span>

* <span data-ttu-id="0e89f-255">Select hello **Araştır** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0e89f-255">Select hello **Explore** tab.</span></span>
* <span data-ttu-id="0e89f-256">Tıklatın **Özet**, ardından **yürütme**, toosee hello değişken türleri ve bazı Özet istatistikleri hakkında bazı bilgiler.</span><span class="sxs-lookup"><span data-stu-id="0e89f-256">Click **Summary**, then **Execute**, toosee some information about hello variable types and some summary statistics.</span></span>
* <span data-ttu-id="0e89f-257">tooview her bir değişken hakkındaki istatistiklerdir diğer türleri gibi diğer seçenekleri seçin **açıklayın** veya **Temelleri**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-257">tooview other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="0e89f-258">Merhaba **Araştır** sekme ayrıca ayrıntılı birçok çizer toogenerate, sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e89f-258">hello **Explore** tab also allows you toogenerate many insightful plots.</span></span> <span data-ttu-id="0e89f-259">tooplot hello verilerin bir histogram oluşturur:</span><span class="sxs-lookup"><span data-stu-id="0e89f-259">tooplot a histogram of hello data:</span></span>

* <span data-ttu-id="0e89f-260">Seçin **dağıtımları**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-260">Select **Distributions**.</span></span>
* <span data-ttu-id="0e89f-261">Denetleme **Histogram** için **word_freq_remove** ve **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="0e89f-262">Seçin **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-262">Select **Execute**.</span></span> <span data-ttu-id="0e89f-263">Her iki yoğunluğu Temizle olduğu bir tek grafik penceresinde "siz" Kaldır"den" e-postalarda çok daha sık görünür bu hello word çizer görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-263">You should see both density plots in a single graph window, where it is clear that hello word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="0e89f-264">Merhaba bağıntı çizimler, ayrıca ilginç.</span><span class="sxs-lookup"><span data-stu-id="0e89f-264">hello Correlation plots are also interesting.</span></span> <span data-ttu-id="0e89f-265">toocreate biri:</span><span class="sxs-lookup"><span data-stu-id="0e89f-265">toocreate one:</span></span>

* <span data-ttu-id="0e89f-266">Seçin **bağıntı** hello olarak **türü**, ardından</span><span class="sxs-lookup"><span data-stu-id="0e89f-266">Choose **Correlation** as hello **Type**, then</span></span>
* <span data-ttu-id="0e89f-267">Seçin **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-267">Select **Execute**.</span></span>
* <span data-ttu-id="0e89f-268">Çıngırağı, en çok 40 değişkenleri önerir sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="0e89f-269">Seçin **Evet** tooview hello çizim.</span><span class="sxs-lookup"><span data-stu-id="0e89f-269">Select **Yes** tooview hello plot.</span></span>

<span data-ttu-id="0e89f-270">Gündeme bazı ilginç bağıntıları vardır: "teknolojisinin" kesinlikle bağıntılı çok "HP" ve "labs" Örneğin.</span><span class="sxs-lookup"><span data-stu-id="0e89f-270">There are some interesting correlations that come up: "technology" is strongly correlated too"HP" and "labs", for example.</span></span> <span data-ttu-id="0e89f-271">Ayrıca kesinlikle bağıntılı çok "650", hello alan kodu hello dataset bağışta 650 olduğundan.</span><span class="sxs-lookup"><span data-stu-id="0e89f-271">It is also strongly correlated too"650", because hello area code of hello dataset donors is 650.</span></span>

<span data-ttu-id="0e89f-272">sözcükler arasındaki hello bağıntıları Hello sayısal değerleri hello Araştır penceresi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-272">hello numeric values for hello correlations between words are available in hello Explore window.</span></span> <span data-ttu-id="0e89f-273">Bu ilginç "teknolojisinin" olumsuz "sizin" bağıntılı, örneğin toonote ve "para" olur.</span><span class="sxs-lookup"><span data-stu-id="0e89f-273">It is interesting toonote, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="0e89f-274">Çıngırağı hello dataset toohandle bazı yaygın sorunlar dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e89f-274">Rattle can transform hello dataset toohandle some common issues.</span></span> <span data-ttu-id="0e89f-275">Örneğin, toorescale özelliklerini tanır, eksik değerleri impute, aykırı değerlerini işlemek ve değişkenleri veya eksik verilerle gözlemleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="0e89f-275">For example, it allows you toorescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="0e89f-276">Çıngırağı gözlemleri ve/veya değişkenleri arasındaki ilişkilendirme kuralları da tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e89f-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="0e89f-277">Bu sekme, bu tanıtıcı kılavuz için kapsam dışına:.</span><span class="sxs-lookup"><span data-stu-id="0e89f-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="0e89f-278">Çıngırağı küme analiz de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e89f-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="0e89f-279">Şimdi bazı özellikleri toomake hello çıktı daha kolay tooread dışlayın.</span><span class="sxs-lookup"><span data-stu-id="0e89f-279">Let's exclude some features toomake hello output easier tooread.</span></span> <span data-ttu-id="0e89f-280">Merhaba üzerinde **veri** sekmesinde, seçin **Yoksay** on bu öğeler dışında hello değişkenlerin sonraki tooeach:</span><span class="sxs-lookup"><span data-stu-id="0e89f-280">On hello **Data** tab, choose **Ignore** next tooeach of hello variables except these ten items:</span></span>

* <span data-ttu-id="0e89f-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="0e89f-281">word_freq_hp</span></span>
* <span data-ttu-id="0e89f-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="0e89f-282">word_freq_technology</span></span>
* <span data-ttu-id="0e89f-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="0e89f-283">word_freq_george</span></span>
* <span data-ttu-id="0e89f-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="0e89f-284">word_freq_remove</span></span>
* <span data-ttu-id="0e89f-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="0e89f-285">word_freq_your</span></span>
* <span data-ttu-id="0e89f-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="0e89f-286">word_freq_dollar</span></span>
* <span data-ttu-id="0e89f-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="0e89f-287">word_freq_money</span></span>
* <span data-ttu-id="0e89f-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="0e89f-288">capital_run_length_longest</span></span>
* <span data-ttu-id="0e89f-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="0e89f-289">word_freq_business</span></span>
* <span data-ttu-id="0e89f-290">istenmeyen posta</span><span class="sxs-lookup"><span data-stu-id="0e89f-290">spam</span></span>

<span data-ttu-id="0e89f-291">Toohello geri dönün **küme** sekmesinde, seçin **KMeans**ve kümesi hello *küme sayısı* too4.</span><span class="sxs-lookup"><span data-stu-id="0e89f-291">Then go back toohello **Cluster** tab, choose **KMeans**, and set hello *Number of clusters* too4.</span></span> <span data-ttu-id="0e89f-292">Ardından **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-292">Then **Execute**.</span></span> <span data-ttu-id="0e89f-293">Merhaba sonuçlar hello çıktı penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-293">hello results are displayed in hello output window.</span></span> <span data-ttu-id="0e89f-294">Bir küme yüksek sıklığı "Hasan" ve "hp" vardır ve büyük olasılıkla yasal iş e-posta olur.</span><span class="sxs-lookup"><span data-stu-id="0e89f-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="0e89f-295">toobuild basit karar ağacı machine learning modelini:</span><span class="sxs-lookup"><span data-stu-id="0e89f-295">toobuild a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="0e89f-296">Select hello **modeli** sekmesi</span><span class="sxs-lookup"><span data-stu-id="0e89f-296">Select hello **Model** tab,</span></span>
* <span data-ttu-id="0e89f-297">Seçin **ağaç** hello olarak **türü**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-297">Choose **Tree** as hello **Type**.</span></span>
* <span data-ttu-id="0e89f-298">Seçin **yürütme** toodisplay hello metin biçiminde hello ağacında çıktı penceresi.</span><span class="sxs-lookup"><span data-stu-id="0e89f-298">Select **Execute** toodisplay hello tree in text form in hello output window.</span></span>
* <span data-ttu-id="0e89f-299">Select hello **çizin** düğmesini tooview grafik bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="0e89f-299">Select hello **Draw** button tooview a graphical version.</span></span> <span data-ttu-id="0e89f-300">Bu oldukça benzer toohello ağaç elde daha önce kullanarak arar *rpart*.</span><span class="sxs-lookup"><span data-stu-id="0e89f-300">This looks quite similar toohello tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="0e89f-301">Biri hello iyi Çıngırağı özelliklerini kendi yeteneği toorun birkaç machine learning yöntemleri ve bunları hızlı bir şekilde değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="0e89f-301">One of hello nice features of Rattle is its ability toorun several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="0e89f-302">Merhaba yordamı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="0e89f-302">Here is hello procedure:</span></span>

* <span data-ttu-id="0e89f-303">Seçin **tüm** hello için **türü**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-303">Choose **All** for hello **Type**.</span></span>
* <span data-ttu-id="0e89f-304">Seçin **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-304">Select **Execute**.</span></span>
* <span data-ttu-id="0e89f-305">Sona erdikten sonra tüm tek tıklatabilirsiniz **türü**gibi **SVM**ve hello sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="0e89f-305">After it finishes you can click any single **Type**, like **SVM**, and view hello results.</span></span>
* <span data-ttu-id="0e89f-306">Merhaba kullanılarak ayarlanan hello doğrulama hello modellerinde hello performansını de karşılaştırabilirsiniz **değerlendir** sekmesi. Örneğin, hello **hata matris** seçimi gösterir, hello karışıklığı matrisi, genel hata ve her model için ortalama sınıfı hata hello doğrulama kümesinde.</span><span class="sxs-lookup"><span data-stu-id="0e89f-306">You can also compare hello performance of hello models on hello validation set using hello **Evaluate** tab. For example, hello **Error Matrix** selection shows you hello confusion matrix, overall error, and averaged class error for each model on hello validation set.</span></span>
* <span data-ttu-id="0e89f-307">Ayrıca ROC eğriler çizme, duyarlılık çözümlemesi ve diğer türleri modeli değerlendirmeleri yapın.</span><span class="sxs-lookup"><span data-stu-id="0e89f-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="0e89f-308">Model oluşturmaya yaptıktan sonra hello seçeneğini **günlük** sekmesinde tooview hello R kodu tarafından Çıngırağı oturumunuz sırasında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e89f-308">Once you're finished building models, select hello **Log** tab tooview hello R code run by Rattle during your session.</span></span> <span data-ttu-id="0e89f-309">Merhaba seçebilirsiniz **verme** düğmesini toosave onu.</span><span class="sxs-lookup"><span data-stu-id="0e89f-309">You can select hello **Export** button toosave it.</span></span>

> [!NOTE]
> <span data-ttu-id="0e89f-310">Çıngırağı geçerli sürümde bir hata var.</span><span class="sxs-lookup"><span data-stu-id="0e89f-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="0e89f-311">toomodify hello komut dosyası veya toorepeat kullanın adımlarınızı daha sonra # karakterini önüne eklemeniz gerekir *... Bu günlüğünü Dışarı Aktar * hello günlüğünün hello metin.</span><span class="sxs-lookup"><span data-stu-id="0e89f-311">toomodify hello script or use it toorepeat your steps later, you must insert a # character in front of *Export this log ... * in hello text of hello log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="0e89f-312">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="0e89f-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="0e89f-313">Merhaba DSVM yüklü PostgreSQL ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-313">hello DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="0e89f-314">PostgreSQL Gelişmiş, açık kaynak ilişkisel veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="0e89f-315">Bu bölümde gösterilmiştir nasıl tooload bizim PostgreSQL dataset istenmeyen posta göndermek ve ardından sorgu.</span><span class="sxs-lookup"><span data-stu-id="0e89f-315">This section shows how tooload our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="0e89f-316">Merhaba veri yükleyebilir önce hello localhost tooallow parola kimlik doğrulamasını gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-316">Before you can load hello data, you need tooallow password authentication from hello localhost.</span></span> <span data-ttu-id="0e89f-317">Bir komut isteminde:</span><span class="sxs-lookup"><span data-stu-id="0e89f-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="0e89f-318">Merhaba yapılandırma dosyası Hello altına bağlantılara izin hello ayrıntı birden çok satıra şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0e89f-318">Near hello bottom of hello config file are several lines that detail hello allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="0e89f-319">Biz bir kullanıcı adı ve parola kullanarak oturum şekilde hello "IPv4 yerel bağlantılar" satırı toouse md5 plainname, yerine değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0e89f-319">Change hello "IPv4 local connections" line toouse md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="0e89f-320">Ve hello postgres hizmetini yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-320">And restart hello postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="0e89f-321">toolaunch psql, etkileşimli terminal hello yerleşik postgres kullanıcı olarak, PostgreSQL için komutu bir isteminden aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-321">toolaunch psql, an interactive terminal for PostgreSQL, as hello built-in postgres user, run hello following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="0e89f-322">Yeni bir kullanıcı hesabı oluşturma, kullanarak aynı kullanıcı adı şu anda olarak oturum açtınız Linux hesabı hello gibi hello ve parola verin:</span><span class="sxs-lookup"><span data-stu-id="0e89f-322">Create a new user account, using hello same username as hello Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="0e89f-323">Ardından toopsql, kullanıcı olarak oturum açın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-323">Then log in toopsql as your user:</span></span>

    psql

<span data-ttu-id="0e89f-324">Ve yeni bir veritabanına hello veri içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-324">And import hello data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="0e89f-325">Şimdi, şimdi hello verileri araştırırken kullanarak bazı sorgular çalıştırmak **Squirrel SQL**, JDBC sürücüsü aracılığıyla veritabanlarıyla etkileşim olanak sağlayan bir grafik aracıdır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-325">Now, let's explore hello data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="0e89f-326">tooget başlatıldı, Squirrel SQL hello uygulamaları menüsünden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0e89f-326">tooget started, launch Squirrel SQL from hello Applications menu.</span></span> <span data-ttu-id="0e89f-327">Merhaba sürücü yukarı tooset:</span><span class="sxs-lookup"><span data-stu-id="0e89f-327">tooset up hello driver:</span></span>

* <span data-ttu-id="0e89f-328">Seçin **Windows**, ardından **görüntülemek sürücüleri**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="0e89f-329">Sağ **PostgreSQL** seçip **değiştirmek sürücü**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="0e89f-330">Seçin **yolu'fazladan sınıf**, ardından **eklemek**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="0e89f-331">Girin ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** hello için **dosya adı** ve</span><span class="sxs-lookup"><span data-stu-id="0e89f-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for hello **File Name** and</span></span>
* <span data-ttu-id="0e89f-332">Seçin **açık**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-332">Select **Open**.</span></span>
* <span data-ttu-id="0e89f-333">Liste sürücüleri seçin ve ardından **org.postgresql.Driver** içinde **sınıf adı**seçip **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0e89f-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="0e89f-334">tooset hello bağlantı toohello yerel sunucusu:</span><span class="sxs-lookup"><span data-stu-id="0e89f-334">tooset up hello connection toohello local server:</span></span>

* <span data-ttu-id="0e89f-335">Seçin **Windows**, ardından **diğer adlar görüntüleyin.**</span><span class="sxs-lookup"><span data-stu-id="0e89f-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="0e89f-336">Merhaba seçin  **+**  düğmesini toomake yeni bir diğer ad.</span><span class="sxs-lookup"><span data-stu-id="0e89f-336">Choose hello **+** button toomake a new alias.</span></span>
* <span data-ttu-id="0e89f-337">Adlandırın *istenmeyen posta veritabanı*, seçin **PostgreSQL** hello içinde **sürücü** açılır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-337">Name it *Spam database*, choose **PostgreSQL** in hello **Driver** drop-down.</span></span>
* <span data-ttu-id="0e89f-338">Merhaba URL çok ayarlanmış*jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="0e89f-338">Set hello URL too*jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="0e89f-339">Girin, *kullanıcıadı* ve *parola*.</span><span class="sxs-lookup"><span data-stu-id="0e89f-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="0e89f-340">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e89f-340">Click **OK**.</span></span>
* <span data-ttu-id="0e89f-341">tooopen hello **bağlantı** penceresinde hello çift ***istenmeyen posta veritabanı*** diğer adı.</span><span class="sxs-lookup"><span data-stu-id="0e89f-341">tooopen hello **Connection** window, double-click hello ***Spam database*** alias.</span></span>
* <span data-ttu-id="0e89f-342">**Bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="0e89f-342">Select **Connect**.</span></span>

<span data-ttu-id="0e89f-343">toorun bazı sorgular:</span><span class="sxs-lookup"><span data-stu-id="0e89f-343">toorun some queries:</span></span>

* <span data-ttu-id="0e89f-344">Select hello **SQL** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0e89f-344">Select hello **SQL** tab.</span></span>
* <span data-ttu-id="0e89f-345">Basit bir sorgu girin `SELECT * from data;` hello sorgu metin kutusuna hello SQL sekmesi hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="0e89f-345">Enter a simple query such as `SELECT * from data;` in hello query textbox at hello top of hello SQL tab.</span></span>
* <span data-ttu-id="0e89f-346">Tuşuna **Ctrl-Enter** toorun onu.</span><span class="sxs-lookup"><span data-stu-id="0e89f-346">Press **Ctrl-Enter** toorun it.</span></span> <span data-ttu-id="0e89f-347">Varsayılan olarak Squirrel SQL hello sorgunuzdan ilk 100 satırı döndürür.</span><span class="sxs-lookup"><span data-stu-id="0e89f-347">By default Squirrel SQL returns hello first 100 rows from your query.</span></span>

<span data-ttu-id="0e89f-348">Bu veriler tooexplore çalıştırabilir pek çok daha fazla sorguları vardır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-348">There are many more queries you could run tooexplore this data.</span></span> <span data-ttu-id="0e89f-349">Örneğin, nasıl mu hello hello word sıklığını *olun* istenmeyen ve ham arasında farklı?</span><span class="sxs-lookup"><span data-stu-id="0e89f-349">For example, how does hello frequency of hello word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="0e89f-350">Veya sık içeren e-posta hello özellikleri nelerdir *3B*?</span><span class="sxs-lookup"><span data-stu-id="0e89f-350">Or what are hello characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="0e89f-351">Yüksek bir oluşumunu sahip çoğu e-postaları *3B* olan görünüşe göre istenmeyen posta göndermek, e-postaları Tahmine dayalı bir model tooclassify hello oluşturmak için yararlı bir özellik olması.</span><span class="sxs-lookup"><span data-stu-id="0e89f-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model tooclassify hello emails.</span></span>

<span data-ttu-id="0e89f-352">Bir PostgreSQL veritabanında depolanan verilerle tooperform machine learning istediyseniz, kullanmayı [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="0e89f-352">If you wanted tooperform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="0e89f-353">SQL Server veri ambarı</span><span class="sxs-lookup"><span data-stu-id="0e89f-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="0e89f-354">Azure SQL Veri Ambarı, hem ilişkisel hem de ilişkisel olmayan çok geniş hacimlerdeki verileri işleyebilen, bulut tabanlı bir genişletme veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="0e89f-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="0e89f-355">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse nedir?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="0e89f-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="0e89f-356">tooconnect toohello veri ambarı ve hello tablo, bir komut isteminden çalıştırma hello şu komutu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0e89f-356">tooconnect toohello data warehouse and create hello table, run hello following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="0e89f-357">Ardından hello sqlcmd isteminde:</span><span class="sxs-lookup"><span data-stu-id="0e89f-357">Then at hello sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="0e89f-358">Bcp ile veri kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="0e89f-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="0e89f-359">Merhaba satır sonları hello indirilen dosyadaki Windows stili olsa da, - r bayrağı hello ile tootell bcp ihtiyacımız şekilde bcp UNIX stilinde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="0e89f-359">hello line endings in hello downloaded file are Windows-style, but bcp expects UNIX-style, so we need tootell bcp that with hello -r flag.</span></span>
>
>

<span data-ttu-id="0e89f-360">Ve sorgu sqlcmd ile:</span><span class="sxs-lookup"><span data-stu-id="0e89f-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="0e89f-361">Ayrıca Squirrel SQL ile sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="0e89f-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="0e89f-362">Merhaba Microsoft MSSQL Server JDBC sürücüsü içinde bulunan kullanarak PostgreSQL için benzer adımları ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="0e89f-362">Follow similar steps for PostgreSQL, using hello Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e89f-363">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e89f-363">Next steps</span></span>
<span data-ttu-id="0e89f-364">Azure'da hello veri bilimi işlemi oluşturan hello görevleri rehberlik konuları genel bakış için bkz: [takım veri bilimi işlemi](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="0e89f-364">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="0e89f-365">Merhaba takım veri bilimi işlemi belirli senaryoları için hello adımlarda gösteren diğer uçtan uca talimatlara açıklaması için bkz: [takım veri bilimi süreci gözden geçirmeleri](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="0e89f-365">For a description of other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="0e89f-366">Hello izlenecek yollar da nasıl toocombine bulut göstermek ve şirket içi araçları ve akıllı bir uygulama bir iş akışı veya ardışık düzen toocreate Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="0e89f-366">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>

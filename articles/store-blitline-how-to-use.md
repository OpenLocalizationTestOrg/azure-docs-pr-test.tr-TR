---
title: "Görüntü işleme - aaaHow toouse Blitline Azure özellik Kılavuzu"
description: "Nasıl toouse hello Blitline hizmet tooprocess görüntüleri Azure uygulamadaki öğrenin."
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="48d35-103">Nasıl toouse Blitline Azure ve Azure Storage ile</span><span class="sxs-lookup"><span data-stu-id="48d35-103">How toouse Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="48d35-104">Bu kılavuz anlatılmıştır nasıl tooaccess Blitline Hizmetleri ve nasıl toosubmit tooBlitline işler.</span><span class="sxs-lookup"><span data-stu-id="48d35-104">This guide will explain how tooaccess Blitline services and how toosubmit jobs tooBlitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="48d35-105">Blitline nedir?</span><span class="sxs-lookup"><span data-stu-id="48d35-105">What is Blitline?</span></span>
<span data-ttu-id="48d35-106">Blitline kurumsal düzey görüntü işleme bir kısmı toobuild mal olacağını hello fiyat sağlayan hizmet işleme bulut tabanlı bir görüntü olduğundan bunu kendiniz.</span><span class="sxs-lookup"><span data-stu-id="48d35-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of hello price that it would cost toobuild it yourself.</span></span>

<span data-ttu-id="48d35-107">Merhaba olgu görüntü işleme tekrar tekrar, genellikle hello başından başlayarak her Web sitesi için gelen yeniden gerçekleştirildi emin olur.</span><span class="sxs-lookup"><span data-stu-id="48d35-107">hello fact is that image processing has been done over and over again, usually rebuilt from hello ground up for each and every website.</span></span> <span data-ttu-id="48d35-108">Biz bunları milyon kez çok oluşturuncaya çünkü Biz bu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="48d35-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="48d35-109">Bir belki de, zaman olduğunu karar gün biz yalnızca herkes için bunu.</span><span class="sxs-lookup"><span data-stu-id="48d35-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="48d35-110">Biliyoruz nasıl toodo, hızlı ve verimli bir şekilde ve kaydetme herkesin çalışır hello sırada toodo.</span><span class="sxs-lookup"><span data-stu-id="48d35-110">We know how toodo it, toodo it fast and efficiently, and save everyone work in hello meantime.</span></span>

<span data-ttu-id="48d35-111">Daha fazla bilgi için bkz: [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="48d35-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="48d35-112">Ne Blitline değil...</span><span class="sxs-lookup"><span data-stu-id="48d35-112">What Blitline is NOT...</span></span>
<span data-ttu-id="48d35-113">tooclarify ne Blitline ileriye doğru taşımadan önce yapmaz genellikle daha kolay tooidentify olduğu için ne Blitline yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="48d35-113">tooclarify what Blitline is useful for, it is often easier tooidentify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="48d35-114">Blitline HTML pencere öğeleri tooupload görüntüleri yok.</span><span class="sxs-lookup"><span data-stu-id="48d35-114">Blitline does NOT have HTML widgets tooupload images.</span></span> <span data-ttu-id="48d35-115">Genel olarak veya kısıtlı izinleri Blitline tooreach için kullanılabilir olan kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="48d35-115">You must have images available publicly or with restricted permissions available for Blitline tooreach.</span></span>
* <span data-ttu-id="48d35-116">Blitline yapmaz dinamik görüntü işleme, Aviary.com gibi</span><span class="sxs-lookup"><span data-stu-id="48d35-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="48d35-117">Blitline görüntüyü karşıya kabul etmez, görüntüleri tooBlitline doğrudan gönderemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="48d35-117">Blitline does NOT accept image uploads, you cannot push your images tooBlitline directly.</span></span> <span data-ttu-id="48d35-118">Bunları tooAzure depolama veya Blitline destekleyen diğer yerler gönderme ve toogo nereden bunları Blitline söyleyin.</span><span class="sxs-lookup"><span data-stu-id="48d35-118">You must push them tooAzure Storage or other places Blitline supports and then tell Blitline where toogo get them.</span></span>
* <span data-ttu-id="48d35-119">Blitline yüksek düzeyde paralel ve herhangi bir zaman uyumlu işlem yapmaz.</span><span class="sxs-lookup"><span data-stu-id="48d35-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="48d35-120">Başka bir deyişle vermelidir bize bir postback_url ve biz, biz tamamladığınızda söyleyebilir işleniyor.</span><span class="sxs-lookup"><span data-stu-id="48d35-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="48d35-121">Blitline hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="48d35-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a><span data-ttu-id="48d35-122">Nasıl toocreate Blitline işi</span><span class="sxs-lookup"><span data-stu-id="48d35-122">How toocreate a Blitline job</span></span>
<span data-ttu-id="48d35-123">Blitline tootake görüntüdeki istediğiniz JSON toodefine hello eylemleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="48d35-123">Blitline uses JSON toodefine hello actions you want tootake on an image.</span></span> <span data-ttu-id="48d35-124">Bu JSON birkaç basit alanlarının oluşur.</span><span class="sxs-lookup"><span data-stu-id="48d35-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="48d35-125">Merhaba basit örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="48d35-125">hello simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="48d35-126">Burada "src" görüntü sürer JSON sahibiz "... boys.jpeg" ve bu görüntüyü too240x140 yeniden boyutlandırın.</span><span class="sxs-lookup"><span data-stu-id="48d35-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image too240x140.</span></span>

<span data-ttu-id="48d35-127">Merhaba uygulama kimliği olan şey içinde bulabilirsiniz, **bağlantı bilgisi** veya **Yönet** Azure sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="48d35-127">hello Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="48d35-128">Üzerinde Blitline toorun işleri sağlar, gizli tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="48d35-128">It is your secret identifier that allows you toorun jobs on Blitline.</span></span>

<span data-ttu-id="48d35-129">Merhaba "Kaydet" parametresi biz işledikten sonra tooput hello görüntü istediğiniz hakkında bilgi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="48d35-129">hello "save" parameter identifies information about where you want tooput hello image once we have processed it.</span></span> <span data-ttu-id="48d35-130">Önemsiz bu durumda, biz tanımlanan henüz.</span><span class="sxs-lookup"><span data-stu-id="48d35-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="48d35-131">Konum tanımlanmışsa Blitline, yerel olarak (ve geçici olarak) depolar benzersiz bulut konumda.</span><span class="sxs-lookup"><span data-stu-id="48d35-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="48d35-132">Merhaba Blitline yaptığınızda, hello JSON konumdan Blitline tarafından döndürülen mümkün tooget olacaktır.</span><span class="sxs-lookup"><span data-stu-id="48d35-132">You will be able tooget that location from hello JSON returned by Blitline when you make hello Blitline.</span></span> <span data-ttu-id="48d35-133">Merhaba "Görüntü" tanımlayıcısı gereklidir ve tooidentify görüntü bu belirli kaydedildiğinde tooyou döndürülür.</span><span class="sxs-lookup"><span data-stu-id="48d35-133">hello "image" identifier is required and is returned tooyou when tooidentify this particular saved image.</span></span>

<span data-ttu-id="48d35-134">Merhaba hakkında daha fazla bilgi bulabilirsiniz *işlevleri* burada destekliyoruz: <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="48d35-134">You can find more information about hello *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="48d35-135">Merhaba hakkındaki belgeler işi seçenekleri burada bulabilirsiniz: <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="48d35-135">You can also find documentation about hello job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="48d35-136">JSON olduktan sonra tek toodo ihtiyacınız olan **POST** , çok`http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="48d35-136">Once you have your JSON all you need toodo is **POST** it too`http://api.blitline.com/job`</span></span>

<span data-ttu-id="48d35-137">Şunun gibi JSON geri alırsınız:</span><span class="sxs-lookup"><span data-stu-id="48d35-137">You will get JSON back that looks something like this:</span></span>

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


<span data-ttu-id="48d35-138">Bu, Blitline isteği aldı, onu bir işleme sırasına getirdi ve onu tamamlandığında hello görüntü adresinde bildirir: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_uygulama\_kimliği /CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="48d35-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed hello image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a><span data-ttu-id="48d35-139">Nasıl toosave bir görüntü tooyour Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="48d35-139">How toosave an image tooyour Azure Storage account</span></span>
<span data-ttu-id="48d35-140">Bir Azure depolama hesabınız varsa, kolayca Blitline itme işlenen hello görüntüleri Azure kapsayıcıya sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="48d35-140">If you have an Azure Storage account, you can easily have Blitline push hello processed images into your Azure container.</span></span> <span data-ttu-id="48d35-141">Bir "azure_destination" ekleyerek hello konumu ve Blitline toopush izinlerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="48d35-141">By adding an "azure_destination" you define hello location and permissions for Blitline toopush to.</span></span>

<span data-ttu-id="48d35-142">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="48d35-142">Here is an example:</span></span>

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


<span data-ttu-id="48d35-143">Merhaba CAPITALIZED değerleri kendi değerlerinizle doldurarak, bu JSON toohttp://api.blitline.com/job gönderebilir ve hello "src" görüntü Bulanıklaştırma filtresi ile işlenir ve tooyou Azure hedef gönderilir.</span><span class="sxs-lookup"><span data-stu-id="48d35-143">By filling in hello CAPITALIZED values with your own, you can submit this JSON toohttp://api.blitline.com/job and hello "src" image will be processed with a blur filter and then pushed tooyou Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="48d35-144">Lütfen unutmayın:</span><span class="sxs-lookup"><span data-stu-id="48d35-144">Please note:</span></span>
<span data-ttu-id="48d35-145">Merhaba SAS hello dosya hello hedef dosya adını dahil olmak üzere hello tüm SAS URL'si, içermelidir.</span><span class="sxs-lookup"><span data-stu-id="48d35-145">hello SAS must contain hello entire SAS url, including hello filename of hello destination file.</span></span>

<span data-ttu-id="48d35-146">Örnek:</span><span class="sxs-lookup"><span data-stu-id="48d35-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="48d35-147">Ayrıca, Blitline'nın Azure Storage belgeleri en son sürümünü hello okuyabilirsiniz [burada](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="48d35-147">You can also read hello latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48d35-148">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="48d35-148">Next Steps</span></span>
<span data-ttu-id="48d35-149">Bizim diğer özellikler hakkında blitline.com tooread ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="48d35-149">Visit blitline.com tooread about all our other features:</span></span>

* <span data-ttu-id="48d35-150">Blitline API uç noktası belgeleri <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="48d35-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="48d35-151">Blitline API işlevleri <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="48d35-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="48d35-152">Blitline API örnekleri <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="48d35-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="48d35-153">Üçüncü Nuget kitaplığı Kısım <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="48d35-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>


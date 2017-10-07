---
title: "Merhaba Java için Azure kitaplıkları paketi için Eclipse Javadoc içeriği aaaDisplaying"
description: "Nasıl toodisplay hello Javadoc içerik eclipse'te hello Azure kitaplıkları."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a><span data-ttu-id="4360f-103">Merhaba Java için Azure kitaplıkları paketi için Eclipse'te Javadoc içerik görüntüleme</span><span class="sxs-lookup"><span data-stu-id="4360f-103">Displaying Javadoc Content in Eclipse for hello Azure Libraries Package for Java</span></span>
<span data-ttu-id="4360f-104">Merhaba Javadoc içerik hello Java için Azure kitaplıkları için Eclipse ortamınızda hello Javadoc içerik toohello Java için Azure kitaplıkları ilişkilendirerek görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="4360f-104">hello Javadoc content for hello Azure Libraries for Java can be viewed within your Eclipse environment by associating hello Javadoc content toohello Azure Libraries for Java.</span></span> <span data-ttu-id="4360f-105">Merhaba aşağıdaki adımlarda size yol gösterecektir toouse Eclipse içinde bu işlev.</span><span class="sxs-lookup"><span data-stu-id="4360f-105">hello following steps show you how toouse this functionality within Eclipse.</span></span>

<span data-ttu-id="4360f-106">Bu yordam, Java tooyour derleme yolu için hello Azure kitaplığı eklemiş varsayar.</span><span class="sxs-lookup"><span data-stu-id="4360f-106">This procedure assumes you have already added hello Azure Library for Java tooyour build path.</span></span>

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a><span data-ttu-id="4360f-107">toodisplay eclipse'te Javadoc içerik hello Java için Azure kitaplıkları için</span><span class="sxs-lookup"><span data-stu-id="4360f-107">toodisplay Javadoc content in Eclipse for hello Azure Libraries for Java</span></span>
* <span data-ttu-id="4360f-108">Merhaba de Eclipse'nın Proje Gezgini'nde içinde **başvurulan kitaplıkları** projenizin bölümü, açık hello bağlam menüsü hello JAR Java için Azure kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="4360f-108">Within Eclipse's Project Explorer, in hello **Referenced Libraries** section of your project, open hello context menu for hello Azure Library for Java JAR.</span></span> <span data-ttu-id="4360f-109">Örneğin, **microsoft-windowsazure-API-0.1.0.jar** (Merhaba sürüm numarası farklı, yüklediğiniz hangi sürümünün bağımlı olabilir).</span><span class="sxs-lookup"><span data-stu-id="4360f-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (hello version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="4360f-110">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4360f-110">Click **Properties**.</span></span>

* <span data-ttu-id="4360f-111">Merhaba içinde **özellikleri** hello sol bölmesinde, iletişim tıklatın **Javadoc konumu**.</span><span class="sxs-lookup"><span data-stu-id="4360f-111">Within hello **Properties** dialog, in hello left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="4360f-112">Merhaba **Javadoc konumu** iletişim kutusu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="4360f-112">hello **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="4360f-113">Belirleyebileceğiniz bir **Javadoc URL**, veya bir **Javadoc arşivde**.</span><span class="sxs-lookup"><span data-stu-id="4360f-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="4360f-114">Toospecify seçerseniz bir **Javadoc URL**, hello URL'ler gibi kullandığınız **http://dl.windowsazure.com/javadoc** veya **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="4360f-114">If you choose toospecify a **Javadoc URL**, use hello URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="4360f-115">Toouse seçerseniz **Javadoc arşivde**, dış bir dosya veya bir çalışma dosyası belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4360f-115">If you choose toouse **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="4360f-116">Seçiminizi yapın ve Gözat/gerektiğinde doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4360f-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="4360f-117">Merhaba aşağıdaki örnek hello Java için Azure kitaplıkları karşılık gelen Javadoc boyunca JAR indirilen yerel olarak adlı tooa klasör hello ile ilişkilendirir **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="4360f-117">hello following example associates hello Azure Libraries for Java with hello corresponding Javadoc JAR that has been downloaded locally tooa folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="4360f-118">*İsteğe bağlı adım*: tıklatın **doğrulamak**.</span><span class="sxs-lookup"><span data-stu-id="4360f-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="4360f-119">Olası sorunlar hello Javadoc JAR burada gösterilemedi.</span><span class="sxs-lookup"><span data-stu-id="4360f-119">Potential issues with hello Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="4360f-120">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4360f-120">Click **OK**.</span></span>

<span data-ttu-id="4360f-121">Merhaba Kitaplıkla ilişkilendirilmiş sonra hello Javadoc içerik Eclipse IDE içinde görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="4360f-121">Once associated with hello library, hello Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="4360f-122">Örneğin, varsa `blob` türü tanımlı `CloudBlockBlob` yazarken görüntülenen Javadoc içeriğine bir örnek kodunuzu içinde hello aşağıdadır `blob.acquireLease` kod:</span><span class="sxs-lookup"><span data-stu-id="4360f-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, hello following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="4360f-123">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="4360f-123">See Also</span></span>
<span data-ttu-id="4360f-124">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4360f-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="4360f-125">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4360f-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="4360f-126">[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4360f-126">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="4360f-127">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="4360f-127">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->

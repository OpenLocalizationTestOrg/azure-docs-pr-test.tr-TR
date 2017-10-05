---
title: "Java için Azure kitaplıkları paketine Eclipse'te Javadoc içerik görüntüleme"
description: "Eclipse'te Azure kitaplıkları Javadoc içeriği görüntülemek nasıl."
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
ms.openlocfilehash: b44deb773b2159cba1d5d957455409f10fc49334
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="a9bcd-103">Java için Azure kitaplıkları paketine Eclipse'te Javadoc içerik görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a9bcd-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>
<span data-ttu-id="a9bcd-104">Javadoc içerik Java için Azure kitaplıkları için Java için Azure kitaplıkları Javadoc içeriği ilişkilendirerek Eclipse ortamınızda görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="a9bcd-105">Aşağıdaki adımlar bu işlevselliğinin Eclipse içinde nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="a9bcd-106">Bu yordam, Java için Azure kitaplığı yapı yolunuzu eklemiş varsayar.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="a9bcd-107">Java için Azure kitaplıkları için Eclipse'te Javadoc içeriği görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="a9bcd-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>
* <span data-ttu-id="a9bcd-108">Eclipse'nın Proje Gezgini içinde içinde **başvurulan kitaplıkları** bölüm projenizi bağlam menüsü için Azure kitaplığı Java JAR için açın.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="a9bcd-109">Örneğin, **microsoft-windowsazure-API-0.1.0.jar** (sürüm numarası olabilir farklı, yüklediğiniz hangi sürümünün bağımlı).</span><span class="sxs-lookup"><span data-stu-id="a9bcd-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="a9bcd-110">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-110">Click **Properties**.</span></span>

* <span data-ttu-id="a9bcd-111">İçinde **özellikleri** iletişim kutusunda, sol bölmedeki tıklatın **Javadoc konumu**.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="a9bcd-112">**Javadoc konumu** iletişim kutusu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-112">The **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="a9bcd-113">Belirleyebileceğiniz bir **Javadoc URL**, veya bir **Javadoc arşivde**.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="a9bcd-114">Belirtmeyi seçerseniz bir **Javadoc URL**, URL'ler gibi kullandığınız **http://dl.windowsazure.com/javadoc** veya **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="a9bcd-115">Kullanmayı seçerseniz **Javadoc arşivde**, dış bir dosya veya bir çalışma dosyası belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="a9bcd-116">Seçiminizi yapın ve Gözat/gerektiğinde doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="a9bcd-117">Aşağıdaki örnek Java için Azure kitaplıkları karşılık gelen Javadoc adlı bir klasöre yerel olarak indirdiği JAR ilişkilendirir **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="a9bcd-118">*İsteğe bağlı adım*: tıklatın **doğrulamak**.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="a9bcd-119">Javadoc JAR olası sorunlar burada gösterilemedi.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-119">Potential issues with the Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="a9bcd-120">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-120">Click **OK**.</span></span>

<span data-ttu-id="a9bcd-121">Kitaplıkla ilişkilendirilmiş sonra Eclipse IDE içinde Javadoc içeriği görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-121">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="a9bcd-122">Örneğin, varsa `blob` türü tanımlı `CloudBlockBlob` kodunuzu içinde yazarken görüntülenen Javadoc içeriğine bir örnek verilmiştir `blob.acquireLease` kod:</span><span class="sxs-lookup"><span data-stu-id="a9bcd-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="a9bcd-123">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a9bcd-123">See Also</span></span>
<span data-ttu-id="a9bcd-124">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a9bcd-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="a9bcd-125">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a9bcd-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="a9bcd-126">[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a9bcd-126">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="a9bcd-127">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="a9bcd-127">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->

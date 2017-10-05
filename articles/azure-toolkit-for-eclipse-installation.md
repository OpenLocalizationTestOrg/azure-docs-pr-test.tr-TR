---
title: "Eclipse için Azure araç setini yükleme | Microsoft Docs"
description: "Eclipse için Azure Araç Seti yüklemeyi öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35cddba38c364dfb2f6a8646b0014d48ca4cb795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="29407-103">Eclipse için Azure araç setini yükleme</span><span class="sxs-lookup"><span data-stu-id="29407-103">Installing the Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="29407-104">Eclipse için Azure araç seti, şablonları ve kolayca oluşturun, geliştirme, test olanak sağlar ve Eclipse geliştirme ortamı'nı kullanarak Azure uygulamalarını dağıtma işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="29407-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="29407-105">Eclipse için Azure Araç Seti açık kaynaklı proje ' dir.</span><span class="sxs-lookup"><span data-stu-id="29407-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="29407-106">Kaynak kodu MIT lisansı altında kullanılabilir <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="29407-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="29407-107">Aşağıdaki adımlar, Azure araç setini Eclipse için yükleme gösterir.</span><span class="sxs-lookup"><span data-stu-id="29407-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="29407-108">Eclipse için Azure Araç Seti yüklemek için</span><span class="sxs-lookup"><span data-stu-id="29407-108">To install the Azure Toolkit for Eclipse</span></span>
1. <span data-ttu-id="29407-109">Eclipse'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="29407-109">Start Eclipse.</span></span>
2. <span data-ttu-id="29407-110">Tıklatın **yardımcı** menüsüne ve ardından **yeni yazılımı yükle**, aşağıdaki çizimde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="29407-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
    ![Eclipse için Azure araç setini yükleme][01]
3. <span data-ttu-id="29407-112">İçinde **kullanılabilir yazılım** iletişim, içinde **çalışmak** metin kutusunda, `http://dl.microsoft.com/eclipse` arkasından **Enter** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="29407-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse` followed by the **Enter** key.</span></span>
4. <span data-ttu-id="29407-113">İçinde **adı** bölmesinde, onay **Eclipse için Azure Araç Seti**ve işaretini **gerekli yazılımı bulmak için yükleme sırasında tüm güncelleştirme siteleri başvurun**.</span><span class="sxs-lookup"><span data-stu-id="29407-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="29407-114">Ekranınızın aşağıdakine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="29407-114">Your screen should appear similar to the following:</span></span>
   
    ![Eclipse için Azure araç setini yükleme][02]
5. <span data-ttu-id="29407-116">Genişletirseniz **Eclipse için Azure Araç Seti**, aşağıdaki öğeleri görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="29407-116">If you expand the **Azure Toolkit for Eclipse**, you will see the following items:</span></span>
   
   * <span data-ttu-id="29407-117">**Java için uygulama Insights eklentisiyle**: Bu bileşen, uygulamaları ve sunucu örnekleri için Azure'nın telemetri günlüğe kaydetme ve Analiz Hizmetleri kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="29407-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="29407-118">**Azure erişim denetimi Hizmetleri filtre**: Bu bileşen Azure ACS ile uygulama kullanıcıların kimlik doğrulaması, tek oturum açma senaryoları etkinleştirmek ve uygulamadan kimlik mantığını harici hale getirerek için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="29407-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="29407-119">**Azure ortak eklenti**: Bu bileşen, diğer araç seti bileşenleri tarafından gereken ortak işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="29407-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="29407-120">**Eclipse için Azure Explorer**: Bu bileşen, diğer araç seti bileşenleri tarafından gereken ortak işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="29407-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="29407-121">**Java ile Eclipse için Azure eklentisi**: Bu bileşen, derleme, test ve Eclipse ve komut satırı aracılığıyla Microsoft Azure bulut için Java uygulamaları dağıtmanıza yardımcı projeleri geliştirmek için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="29407-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="29407-122">**Java ile Azure Web Apps eklentisi**: Bu bileşen, Microsoft Azure Web uygulaması kapsayıcıları için Java web uygulamalarını dağıtmak için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="29407-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="29407-123">**SQL Server için Microsoft JDBC sürücüsü 4.2**: Bu bileşen JDBC API SQL Server ve Microsoft Azure SQL veritabanı için Java Platform Enterprise Edition 8 sağlar.</span><span class="sxs-lookup"><span data-stu-id="29407-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="29407-124">**Apache Qpid istemci kitaplıkları JMS için paket**: Bu bileşen, Microsoft Azure'da AMQP Mesajlaşma kullanmak için uygulamanızı etkinleştirmek için Apache Qpid projeden JMS istemci bileşeni sağlar.</span><span class="sxs-lookup"><span data-stu-id="29407-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="29407-125">**Java için Microsoft Azure kitaplıkları için paketi**: Bu bileşen, Microsoft Azure Hizmetleri, depolama, hizmet veri yolu, hizmet çalışma zamanı vb. gibi erişmek için API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="29407-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>
6. <span data-ttu-id="29407-126">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="29407-126">Click **Next**.</span></span> <span data-ttu-id="29407-127">(Araç Seti yüklerken olağan dışı gecikmeler yaşıyorsanız emin **gerekli yazılımı bulmak için yükleme sırasında tüm güncelleştirme siteleri başvurun** işaretli değildir.)</span><span class="sxs-lookup"><span data-stu-id="29407-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>
7. <span data-ttu-id="29407-128">İçinde **Yükleme ayrıntıları** iletişim kutusunda, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="29407-128">In the **Install Details** dialog, click **Next**.</span></span>
   
    ![Kurulum ayrıntılarını gözden geçirin][03]
8. <span data-ttu-id="29407-130">İçinde **gözden lisansları** iletişim kutusunda, Lisans Sözleşmesi koşullarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="29407-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="29407-131">Lisans Sözleşmesi koşullarını kabul ediyorsanız **Lisans Sözleşmesi koşullarını kabul ediyorum** ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="29407-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="29407-132">(Kalan adımları Lisans Sözleşmesi koşullarını kabul ediyor musunuz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="29407-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="29407-133">Lisans Sözleşmesi koşullarını kabul etmezseniz, yükleme işlemden.)</span><span class="sxs-lookup"><span data-stu-id="29407-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
    ![Lisansları gözden geçirin][04]
   
    <span data-ttu-id="29407-135">Eclipse indirin ve gerekli paketleri yüklemek.</span><span class="sxs-lookup"><span data-stu-id="29407-135">Eclipse will download and install the requisite packages.</span></span>
   
    ![Yükleme ilerleme durumu][05]
9. <span data-ttu-id="29407-137">Yüklemeyi tamamlamak için Eclipse'i yeniden başlatmanız istenirse, tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="29407-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
    ![İstemi yeniden başlatın][06]

## <a name="see-also"></a><span data-ttu-id="29407-139">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="29407-139">See Also</span></span>
<span data-ttu-id="29407-140">Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:</span><span class="sxs-lookup"><span data-stu-id="29407-140">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="29407-141">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="29407-141">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="29407-142">[Eclipse için Azure Araç Seti Yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="29407-142">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="29407-143">*Azure araç setini Eclipse (Bu makalede) için yükleme*</span><span class="sxs-lookup"><span data-stu-id="29407-143">*Installing the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="29407-144">[Eclipse için Azure Araç Setinde Oturum Açma Yönergeleri]</span><span class="sxs-lookup"><span data-stu-id="29407-144">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="29407-145">[Eclipse Azure'da Hello World Web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="29407-145">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="29407-146">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="29407-146">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="29407-147">[IntelliJ için Azure Araç Seti Yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="29407-147">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="29407-148">[IntelliJ için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="29407-148">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="29407-149">[IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]</span><span class="sxs-lookup"><span data-stu-id="29407-149">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="29407-150">[Intellij Azure'da Hello World Web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="29407-150">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="29407-151">Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi].</span><span class="sxs-lookup"><span data-stu-id="29407-151">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="29407-152">[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="29407-152">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="29407-153">[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="29407-153">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="29407-154">[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="29407-154">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="29407-155">[Intellij Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="29407-155">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
<span data-ttu-id="29407-156">[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="29407-156">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="29407-157">[Eclipse için Azure Araç Setinde Oturum Açma Yönergeleri]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="29407-157">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="29407-158">[IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="29407-158">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="29407-159">[Eclipse için Azure Araç Seti Yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="29407-159">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="29407-160">[IntelliJ için Azure Araç Seti Yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="29407-160">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="29407-161">[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="29407-161">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

---
title: bir sertifika toohello Java CA deposu aaaAdd | Microsoft Docs
description: "Nasıl tooadd bir sertifika yetkilisi (CA) sertifika toohello Java CA sertifikasını (cacerts) depolamak Twilio hizmet veya Azure Service Bus için öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a><span data-ttu-id="a24e9-103">Sertifika toohello Java CA sertifikaları deposu ekleme</span><span class="sxs-lookup"><span data-stu-id="a24e9-103">Adding a Certificate toohello Java CA Certificates Store</span></span>
<span data-ttu-id="a24e9-104">Aşağıdaki adımları hello nasıl tooadd bir sertifika yetkilisi (CA) sertifika toohello Java CA sertifikasını (cacerts) depolamak gösterir.</span><span class="sxs-lookup"><span data-stu-id="a24e9-104">hello following steps show you how tooadd a certificate authority (CA) certificate toohello Java CA certificate (cacerts) store.</span></span> <span data-ttu-id="a24e9-105">kullanılan hello örnek hello Twilio hizmeti tarafından hello CA sertifikası gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a24e9-105">hello example used is for hello CA certificate required by hello Twilio service.</span></span> <span data-ttu-id="a24e9-106">Daha sonra hello konuda sağlanan bilgiler nasıl tooinstall hello CA sertifika hello Azure Service Bus açıklar.</span><span class="sxs-lookup"><span data-stu-id="a24e9-106">Information provided later in hello topic describes how tooinstall hello CA certificate for hello Azure Service Bus.</span></span> 

<span data-ttu-id="a24e9-107">JDK ve tooyour Azure projesi 's ekleyerek keytool tooadd hello CA sertifikası önceki toozipping kullanabileceğiniz **approot** klasör veya keytool tooadd hello sertifika kullanan bir Azure başlangıç görevi çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="a24e9-107">You can use keytool tooadd hello CA certificate prior toozipping your JDK and adding it tooyour Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool tooadd hello certificate.</span></span> <span data-ttu-id="a24e9-108">Bu örnek, bir CA sertifikası önceki toohello daraltılmış JDK ekleyeceksiniz varsayar.</span><span class="sxs-lookup"><span data-stu-id="a24e9-108">This example assumes you will add a CA certificate prior toohello JDK being zipped.</span></span> <span data-ttu-id="a24e9-109">Ayrıca, belirli bir CA sertifikası hello örnek, ancak farklı bir CA sertifikasını alma adımları hello kullanılacak ve hello cacerts alma deposu benzer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a24e9-109">Also, a specific CA certificate will be used in hello example, but hello steps of obtaining a different CA certificate and importing it into hello cacerts store would be similar.</span></span>

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a><span data-ttu-id="a24e9-110">bir sertifika toohello cacerts tooadd depolama</span><span class="sxs-lookup"><span data-stu-id="a24e9-110">tooadd a certificate toohello cacerts store</span></span>
1. <span data-ttu-id="a24e9-111">Bir komut isteminde tooyour JDK'ın ayarlamak **jdk\jre\lib\security** klasörü, hangi sertifikaların yüklü toosee aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a24e9-111">At a command prompt that is set tooyour JDK's **jdk\jre\lib\security** folder, run hello following toosee what certificates are installed:</span></span>
   
    `keytool -list -keystore cacerts`
   
    <span data-ttu-id="a24e9-112">Merhaba deposu parolasını istenir.</span><span class="sxs-lookup"><span data-stu-id="a24e9-112">You'll be prompted for hello store password.</span></span> <span data-ttu-id="a24e9-113">Merhaba varsayılan parola **değiştirme**.</span><span class="sxs-lookup"><span data-stu-id="a24e9-113">hello default password is **changeit**.</span></span> <span data-ttu-id="a24e9-114">(Toochange hello parola istiyorsanız hello keytool belgelerine bakın <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) Bu örnek, MD5 parmak izi 67:CB:9 D hello sertifikayla varsayar: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 listede ve tooimport istediğiniz BT (Merhaba Twilio API hizmeti tarafından bu belirli sertifika gereklidir).</span><span class="sxs-lookup"><span data-stu-id="a24e9-114">(If you want toochange hello password, see hello keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) This example assumes that hello certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 is not listed, and that you want tooimport it (this particular certificate is needed by hello Twilio API service).</span></span>
2. <span data-ttu-id="a24e9-115">Konumunda listelenen sertifikaları hello listesinden Hello sertifika elde [GeoTrust kök sertifikalarını](http://www.geotrust.com/resources/root-certificates/).</span><span class="sxs-lookup"><span data-stu-id="a24e9-115">Obtain hello certificate from hello list of certificates listed at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span> <span data-ttu-id="a24e9-116">Merhaba sertifikanın seri numarası 35:DE:F4:CF ile Merhaba bağlantıyı sağ tıklatın ve toohello kaydetmek **jdk\jre\lib\security** klasör.</span><span class="sxs-lookup"><span data-stu-id="a24e9-116">Right-click hello link for hello certificate with serial number 35:DE:F4:CF and save it toohello **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="a24e9-117">Bu örneğin amaçları doğrultusunda adlı tooa dosya kaydedildi **Equifax\_güvenli\_sertifika\_Authority.cer**.</span><span class="sxs-lookup"><span data-stu-id="a24e9-117">For purposes of this example, it was saved tooa file named **Equifax\_Secure\_Certificate\_Authority.cer**.</span></span>
3. <span data-ttu-id="a24e9-118">Komutu aşağıdaki hello aracılığıyla Hello sertifikasını içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="a24e9-118">Import hello certificate via hello following command:</span></span>
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    <span data-ttu-id="a24e9-119">Zaman MD5 parmak izi 67:CB:9 D hello sertifika varsa, bu sertifika tootrust istenir: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, yazarak yanıtlayın **y**.</span><span class="sxs-lookup"><span data-stu-id="a24e9-119">When prompted tootrust this certificate, if hello certificate has MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, respond by typing **y**.</span></span>
4. <span data-ttu-id="a24e9-120">Komut tooensure hello CA sertifika aşağıdaki çalışma hello başarıyla alındı:</span><span class="sxs-lookup"><span data-stu-id="a24e9-120">Run hello following command tooensure hello CA certificate has been successfully imported:</span></span>
   
    `keytool -list -keystore cacerts`
5. <span data-ttu-id="a24e9-121">Merhaba JDK zip ve tooyour Azure projesi 's ekleyin **approot** klasör.</span><span class="sxs-lookup"><span data-stu-id="a24e9-121">Zip hello JDK and add it tooyour Azure project's **approot** folder.</span></span>

<span data-ttu-id="a24e9-122">Keytool hakkında daha fazla bilgi için bkz: <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="a24e9-122">For information about keytool, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

## <a name="azure-root-certificates"></a><span data-ttu-id="a24e9-123">Azure kök sertifikaları</span><span class="sxs-lookup"><span data-stu-id="a24e9-123">Azure Root Certificates</span></span>
<span data-ttu-id="a24e9-124">Azure Hizmetleri (örneğin, Azure Service Bus) kullanan, uygulamaları tootrust hello Baltimore CyberTrust kök sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="a24e9-124">Your applications that use Azure services (such as Azure Service Bus) need tootrust hello Baltimore CyberTrust Root certificate.</span></span> <span data-ttu-id="a24e9-125">(15 Nisan 2013 başlayan Azure hello GTE CyberTrust genel kök toohello Baltimore CyberTrust Root ' geçiş başlamıştır.</span><span class="sxs-lookup"><span data-stu-id="a24e9-125">(Beginning April 15, 2013, Azure began migrating from hello GTE CyberTrust Global Root toohello Baltimore CyberTrust Root.</span></span> <span data-ttu-id="a24e9-126">Bu geçiş birkaç ay toocomplete sürdü.)</span><span class="sxs-lookup"><span data-stu-id="a24e9-126">This migration took several months toocomplete.)</span></span>

<span data-ttu-id="a24e9-127">Merhaba sertifika önceden yüklenmiş olmalıdır cacerts deponuzda Baltimore şekilde unutmayın toorun hello **keytool-liste** zaten varsa, ilk toosee komutu.</span><span class="sxs-lookup"><span data-stu-id="a24e9-127">hello Baltimore certificate might already be installed in your cacerts store, so remember toorun hello **keytool -list** command first toosee if it already exists.</span></span>

<span data-ttu-id="a24e9-128">Tooadd gerekiyorsa Baltimore CyberTrust Root Merhaba, seri numarası 02:00:00:b9 ve SHA1 parmak izi d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 c vardır: 78:db:28:52:ca:e4:74.</span><span class="sxs-lookup"><span data-stu-id="a24e9-128">If you need tooadd hello Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span></span> <span data-ttu-id="a24e9-129">Adresten yüklenebilir <https://cacert.omniroot.com/bc2025.crt>, tooa yerel dosya uzantısı ile kaydedilen **.cer**ve kullanılarak içe **keytool** yukarıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="a24e9-129">It can be downloaded from <https://cacert.omniroot.com/bc2025.crt>, saved tooa local file with extension **.cer**, and then imported using **keytool** as shown above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a24e9-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a24e9-130">Next steps</span></span>
<span data-ttu-id="a24e9-131">Azure tarafından kullanılan hello kök sertifikaları hakkında daha fazla bilgi için bkz: [Azure kök sertifika geçiş](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span><span class="sxs-lookup"><span data-stu-id="a24e9-131">For more information about hello root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span></span>

<span data-ttu-id="a24e9-132">Java hakkında daha fazla bilgi için bkz: [Java geliştiriciler için Azure](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="a24e9-132">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>


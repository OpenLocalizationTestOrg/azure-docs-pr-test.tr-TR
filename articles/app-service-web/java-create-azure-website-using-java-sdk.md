---
title: "aaaCreate hello Azure SDK'sı için Java kullanarak Azure App Service Web uygulamasında"
description: "Nasıl toocreate program aracılığıyla kullanarak Azure App Service'te bir Web uygulaması hello Java için Azure SDK'sı hakkında bilgi edinin."
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a><span data-ttu-id="5fe2d-103">Java için hello Azure SDK kullanarak Azure App Service Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-103">Create a Web App in Azure App Service using hello Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a><span data-ttu-id="5fe2d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5fe2d-104">Overview</span></span>
<span data-ttu-id="5fe2d-105">Bu kılavuz size nasıl gösterir toocreate bir Web uygulamasını oluşturan bir Java uygulamanız için bir Azure SDK [Azure App Service][Azure App Service], bir uygulama tooit dağıtın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-105">This walkthrough shows you how toocreate an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application tooit.</span></span> <span data-ttu-id="5fe2d-106">İki bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-106">It consists of two parts:</span></span>

* <span data-ttu-id="5fe2d-107">Bölüm 1 nasıl bir web uygulamasını oluşturur toobuild bir Java uygulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-107">Part 1 demonstrates how toobuild a Java application that creates a web app.</span></span>
* <span data-ttu-id="5fe2d-108">2. Bölüm gösterir nasıl toocreate basit bir JSP "Hello World" uygulaması, sonra kullanım bir FTP istemcisi toodeploy kod tooApp hizmet.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-108">Part 2 demonstrates how toocreate a simple JSP "Hello World" application, then use an FTP client toodeploy code tooApp Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fe2d-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5fe2d-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="5fe2d-110">Yazılım yüklemeleri</span><span class="sxs-lookup"><span data-stu-id="5fe2d-110">Software Installations</span></span>
<span data-ttu-id="5fe2d-111">Merhaba AzureWebDemo uygulama kodu bu makalede, Azure Java kullanarak yükleyebileceğiniz SDK 0.7.0, kullanarak yazıldı hello [Web Platformu yükleyicisi] [ Web Platform Installer] (Webpı).</span><span class="sxs-lookup"><span data-stu-id="5fe2d-111">hello AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using hello [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="5fe2d-112">Ayrıca, emin toouse hello en son sürümünü hello olun [Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="5fe2d-112">In addition, make sure toouse hello latest version of hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="5fe2d-113">Çalıştırarak Eclipse projenizin hello bağımlılıkları hello SDK yükledikten sonra güncelleştirme **güncelleştirme dizin** içinde **Maven depoları**, hello hello her paketi en son sürümünü yeniden ekleyin  **Bağımlılıklar** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-113">After you install hello SDK, update hello dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add hello latest version of each package in hello **Dependencies** window.</span></span> <span data-ttu-id="5fe2d-114">Eclipse'te yüklü yazılım hello sürümü tıklatarak doğrulayabilirsiniz **Yardım > Yükleme ayrıntıları**; size sahip en az hello sürümler:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-114">You can verify hello version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least hello following versions:</span></span>

* <span data-ttu-id="5fe2d-115">Microsoft Azure kitaplıkları için Java 0.7.0.20150309 paketi</span><span class="sxs-lookup"><span data-stu-id="5fe2d-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="5fe2d-116">Java EE geliştiricileri 4.4.2.20150219 için Eclipse IDE</span><span class="sxs-lookup"><span data-stu-id="5fe2d-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="5fe2d-117">Oluşturma ve Azure içinde bulut kaynaklarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="5fe2d-118">Bu yordama başlamadan önce toohave etkin bir Azure aboneliği gerekir ve varsayılan Active Directory (AD) Azure üzerinde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-118">Before you begin this procedure, you need toohave an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="5fe2d-119">Bir Active Directory (AD) oluşturma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="5fe2d-120">Bir Active Directory (AD), Azure aboneliğinizde zaten yoksa, hello oturum [Klasik Azure portalı] [ Azure classic portal] Microsoft hesabınızla.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into hello [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="5fe2d-121">Birden çok aboneliğiniz varsa, tıklatın **abonelikleri** ve select hello varsayılan dizin hello abonelik için bu proje için toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-121">If you have multiple subscriptions, click **Subscriptions** and select hello default directory for hello subscription you want toouse for this project.</span></span> <span data-ttu-id="5fe2d-122">Ardından **Uygula** tooswitch toothat abonelik görünümü.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-122">Then click **Apply** tooswitch toothat subscription view.</span></span>

1. <span data-ttu-id="5fe2d-123">Seçin **Active Directory** sol hello menüden.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-123">Select **Active Directory** from hello menu at left.</span></span> <span data-ttu-id="5fe2d-124">**Yeni tıklayın > Dizin > özel Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="5fe2d-125">İçinde **Dizin Ekle**seçin **yeni dizin oluştur**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="5fe2d-126">İçinde **adı**, bir dizin adı girin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="5fe2d-127">İçinde **etki alanı**, bir etki alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="5fe2d-128">Bu dizin ile varsayılan olarak bulunan bir temel etki alanı adıdır; Merhaba form sahip `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-128">This is a basic domain name that is included by default with your directory; it has hello form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="5fe2d-129">Örneğin hello dizin adı veya sahip olduğunuz başka bir etki alanı adını temel alarak adı verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-129">You can name it based on hello directory name or another domain name that you own.</span></span> <span data-ttu-id="5fe2d-130">Daha sonra kuruluşunuzun zaten kullanan başka bir etki alanı adı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="5fe2d-131">İçinde **ülke veya bölge**, bölgeniz seçin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="5fe2d-132">AD hakkında daha fazla bilgi için bkz: [Azure AD dizini nedir][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="5fe2d-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="5fe2d-133">Azure için bir yönetim sertifikası oluşturun</span><span class="sxs-lookup"><span data-stu-id="5fe2d-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="5fe2d-134">Merhaba Java için Azure SDK'sı Azure abonelikleri ile yönetim sertifikaları tooauthenticate kullanır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-134">hello Azure SDK for Java uses management certificates tooauthenticate with Azure subscriptions.</span></span> <span data-ttu-id="5fe2d-135">X.509 v3 sertifikaları tooauthenticate hello abonelik sahibi toomanage abonelik kaynakları adına hello Hizmet Yönetimi API'si tooact kullanan bir istemci uygulaması kullandığınız bunlar.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-135">These are X.509 v3 certificates you use tooauthenticate a client application that uses hello Service Management API tooact on behalf of hello subscription owner toomanage subscription resources.</span></span>

<span data-ttu-id="5fe2d-136">Bu yordamdaki Hello kod Azure ile otomatik olarak imzalanan sertifika tooauthenticate kullanır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-136">hello code in this procedure uses a self-signed certificate tooauthenticate with Azure.</span></span> <span data-ttu-id="5fe2d-137">Bu yordam için toocreate bir sertifika gerekir ve toohello karşıya [Klasik Azure portalı] [ Azure classic portal] önceden.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-137">For this procedure, you need toocreate a certificate and upload it toohello [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="5fe2d-138">Merhaba aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-138">This involves hello following steps:</span></span>

* <span data-ttu-id="5fe2d-139">İstemci sertifikanızın temsil eden bir PFX dosyası oluşturma ve yerel olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="5fe2d-140">Merhaba PFX dosyasından bir yönetim sertifikası (CER dosyası) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-140">Generate a management certificate (CER file) from hello PFX file.</span></span>
* <span data-ttu-id="5fe2d-141">Merhaba CER dosyasını tooyour Azure aboneliği karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-141">Upload hello CER file tooyour Azure subscription.</span></span>
* <span data-ttu-id="5fe2d-142">Java sertifikaları kullanarak bu biçimi tooauthenticate kullandığından hello PFX dosyasını JKS dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-142">Convert hello PFX file into JKS, because Java uses that format tooauthenticate using certificates.</span></span>
* <span data-ttu-id="5fe2d-143">Toohello yerel JKS dosyası başvuruyor hello uygulamanın kimlik doğrulama kodu yazın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-143">Write hello application's authentication code, which refers toohello local JKS file.</span></span>

<span data-ttu-id="5fe2d-144">Bu yordamı tamamladıktan sonra hello CER sertifika Azure aboneliğinizde yer alacağını ve hello JKS sertifika yerel diskinize yer alacağı.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-144">When you complete this procedure, hello CER certificate will reside in your Azure subscription and hello JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="5fe2d-145">Yönetim sertifikaları hakkında daha fazla bilgi için bkz: [oluşturun ve Azure için yönetim sertifikası karşıya][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="5fe2d-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="5fe2d-146">Sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-146">Create a certificate</span></span>
<span data-ttu-id="5fe2d-147">toocreate kendi otomatik olarak imzalanan sertifika, işletim sisteminde bir komut konsolunu açın ve hello aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-147">toocreate your own self-signed certificate, open a command console on your operating system and run hello following commands.</span></span>

> <span data-ttu-id="5fe2d-148">**Not:** bu komutu çalıştırdığınız hello bilgisayarın hello JDK yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-148">**Note:**  hello computer on which you run this command must have hello JDK installed.</span></span> <span data-ttu-id="5fe2d-149">Ayrıca, hello yolu toohello keytool hello JDK yüklemek hello konumuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-149">Also, hello path toohello keytool depends on hello location in which you install hello JDK.</span></span> <span data-ttu-id="5fe2d-150">Daha fazla bilgi için bkz: [anahtar ve Sertifika Yönetim Aracı (keytool)] [ Key and Certificate Management Tool (keytool)] hello Java çevrimiçi belgeleri içinde.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in hello Java online docs.</span></span>
> 
> 

<span data-ttu-id="5fe2d-151">toocreate hello .pfx dosyası:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-151">toocreate hello .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="5fe2d-152">toocreate hello .cer dosyası:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-152">toocreate hello .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="5fe2d-153">Burada:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-153">where:</span></span>

* <span data-ttu-id="5fe2d-154">`<java-install-dir>`Java yüklü hello yolu toohello dizinidir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-154">`<java-install-dir>` is hello path toohello directory in which you installed Java.</span></span>
* <span data-ttu-id="5fe2d-155">`<keystore-id>`Merhaba bir anahtar girişi tanımlayıcıdır (örneğin, `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="5fe2d-155">`<keystore-id>` is hello keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="5fe2d-156">`<cert-store-dir>`toostore sertifikaları istediğiniz hello yolu toohello dizin (örneğin `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="5fe2d-156">`<cert-store-dir>` is hello path toohello directory in which you want toostore certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="5fe2d-157">`<cert-file-name>`Merhaba hello sertifika dosyasının adıdır (örneğin `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="5fe2d-157">`<cert-file-name>` is hello name of hello certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="5fe2d-158">`<password>`Merhaba'a kadar olan tooprotect hello sertifika seçtiğiniz paroladır; en az 6 karakter uzunluğunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-158">`<password>` is hello password you choose tooprotect hello certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="5fe2d-159">Önerilmemesine rağmen bir parola girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="5fe2d-160">`<dname>`Merhaba X.500 ayırt edici ad toobe diğer ad ile ilişkili olan ve hello veren ve hello otomatik olarak imzalanan sertifika konu alanları olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-160">`<dname>` is hello X.500 Distinguished Name toobe associated with alias, and is used as hello issuer and subject fields in hello self-signed certificate.</span></span>

<span data-ttu-id="5fe2d-161">Daha fazla bilgi için bkz: [oluşturun ve Azure için yönetim sertifikası karşıya][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="5fe2d-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-hello-certificate"></a><span data-ttu-id="5fe2d-162">Merhaba sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="5fe2d-162">Upload hello certificate</span></span>
<span data-ttu-id="5fe2d-163">tooupload otomatik olarak imzalanan sertifika tooAzure gidin toohello **ayarları** sayfasında hello Klasik Portalı'nda ve ardından hello **yönetim sertifikaları** sekmesi. Tıklatın **karşıya** hello hello sonundaki sayfasında ve oluşturduğunuz hello CER dosyasını toohello konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-163">tooupload a self-signed certificate tooAzure, go toohello **Settings** page in hello classic portal, then click hello **Management Certificates** tab. Click **Upload** at hello bottom of hello page and navigate toohello location of hello CER file you created.</span></span>

#### <a name="convert-hello-pfx-file-into-jks"></a><span data-ttu-id="5fe2d-164">Merhaba PFX dosyasının JKS Dönüştür</span><span class="sxs-lookup"><span data-stu-id="5fe2d-164">Convert hello PFX file into JKS</span></span>
<span data-ttu-id="5fe2d-165">Hello Windows komut istemi (yönetici olarak çalışır), cd toohello dizinini içeren hello sertifikaları ve komut, aşağıdaki hello çalıştırmak nerede `<java-install-dir>` yüklediğiniz Java bilgisayarınızda hello dizindir:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-165">In hello Windows Command Prompt (running as admin), cd toohello directory containing hello certificates and run hello following command, where `<java-install-dir>` is hello directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="5fe2d-166">İstendiğinde, hello hedef anahtar deposu parolasını girin; Bu hello JKS dosyası hello parolası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-166">When prompted, enter hello destination keystore password; this will be hello password for hello JKS file.</span></span>
2. <span data-ttu-id="5fe2d-167">İstendiğinde, hello kaynağı anahtar deposu parolasını girin; Bu hello PFX dosyası için belirtilen hello paroladır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-167">When prompted, enter hello source keystore password; this is hello password you specified for hello PFX file.</span></span>

<span data-ttu-id="5fe2d-168">Merhaba iki parola aynı hello toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-168">hello two passwords do not have toobe hello same.</span></span> <span data-ttu-id="5fe2d-169">Önerilmemesine rağmen bir parola girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="5fe2d-170">Bir Web uygulaması oluşturma uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-170">Build a Web App creation application</span></span>
### <a name="create-hello-eclipse-workspace-and-maven-project"></a><span data-ttu-id="5fe2d-171">Oluşturma Eclipse çalışma alanında ve bir Maven projesi hello</span><span class="sxs-lookup"><span data-stu-id="5fe2d-171">Create hello Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="5fe2d-172">Bu bölümde bir çalışma alanı ve AzureWebDemo adlı hello web uygulaması oluşturma uygulaması için bir Maven projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-172">In this section you create a workspace and a Maven project for hello web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="5fe2d-173">Yeni bir Maven projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-173">Create a new Maven project.</span></span> <span data-ttu-id="5fe2d-174">Tıklatın **Dosya > Yeni > Maven projesine**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="5fe2d-175">İçinde **yeni bir Maven projesi**seçin **basit bir proje oluşturun** ve **varsayılan çalışma alanı konumu kullanacak**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="5fe2d-176">Merhaba ikinci sayfasında **yeni bir Maven projesi**, hello aşağıdakileri belirtin:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-176">On hello second page of **New Maven Project**, specify hello following:</span></span>
   
   * <span data-ttu-id="5fe2d-177">Grup Kimliği:`com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="5fe2d-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="5fe2d-178">Artifact ID: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="5fe2d-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="5fe2d-179">Sürüm: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="5fe2d-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="5fe2d-180">Paketleme: jar</span><span class="sxs-lookup"><span data-stu-id="5fe2d-180">Packaging: jar</span></span>
   * <span data-ttu-id="5fe2d-181">Ad: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="5fe2d-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="5fe2d-182">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-182">Click **Finish**.</span></span>
3. <span data-ttu-id="5fe2d-183">Proje Gezgini'nde Hello yeni projenin pom.xml dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-183">Open hello new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="5fe2d-184">Select hello **bağımlılıkları** sekmesi. Yeni bir proje olarak hiç paket henüz listelenir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-184">Select hello **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="5fe2d-185">Açık hello Maven depoları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-185">Open hello Maven Repositories view.</span></span> <span data-ttu-id="5fe2d-186">**Pencere tıklayın > Görünümü Göster > Diğer > Maven > Maven depoları** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="5fe2d-187">Merhaba **Maven depoları** görünüm hello IDE hello alt kısmında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-187">hello **Maven Repositories** view will appear at hello bottom of hello IDE.</span></span>
5. <span data-ttu-id="5fe2d-188">Açık **genel depoları**, sağ hello **Merkezi** depo ve select **yeniden dizin**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-188">Open **Global Repositories**, right-click hello **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="5fe2d-189">Bu adım hello bağlantınızın hızına bağlı olarak birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-189">This step can take several minutes depending on hello speed of your connection.</span></span> <span data-ttu-id="5fe2d-190">Merhaba dizini yeniden oluşturur, hello hello Microsoft Azure paketlerinde görmelisiniz **Merkezi** Maven deposu.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-190">When hello index rebuilds, you should see hello Microsoft Azure packages in hello **central** Maven repository.</span></span>
6. <span data-ttu-id="5fe2d-191">İçinde **bağımlılıkları**, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="5fe2d-192">İçinde **grubu kimliği girin...**  girin `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="5fe2d-193">Temel ve App Service Web Apps Yönetimi Hello paketlerini seçin:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-193">Select hello packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="5fe2d-194">**Not:** sonra yeni bir sürüm yayın hello bağımlılıkları güncelleştiriyorsanız toore gereksinim-her hello bağımlılıkları bu listeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-194">**Note:** If you are updating hello dependencies after a new version release, you need toore-add each of hello dependencies in this list.</span></span>
   > <span data-ttu-id="5fe2d-195">Tıklattıktan sonra **Ekle** ve hello yeni sürüm numarasıyla hello olarak göründüğü her bir bağımlılığın seçin **bağımlılıkları** listesi.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-195">After you click **Add** and select each dependency, it appears with hello new version number in hello **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="5fe2d-196">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-196">Click **OK**.</span></span> <span data-ttu-id="5fe2d-197">Azure paketleri hello sonra hello görünür **bağımlılıkları** listesi.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-197">hello Azure packages then appear in hello **Dependencies** list.</span></span>

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a><span data-ttu-id="5fe2d-198">Java kod tooCreate arama hello Azure SDK'sı tarafından bir Web uygulaması yazma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-198">Writing Java Code tooCreate a Web App by Calling hello Azure SDK</span></span>
<span data-ttu-id="5fe2d-199">Ardından, Java toocreate hello App Service web uygulaması hello Azure SDK'sı API'lerini çağırır hello kodu yazın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-199">Next, write hello code that calls APIs in hello Azure SDK for Java toocreate hello App Service web app.</span></span>

1. <span data-ttu-id="5fe2d-200">Bir Java sınıfı toocontain hello ana giriş noktası kodu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-200">Create a Java class toocontain hello main entry point code.</span></span> <span data-ttu-id="5fe2d-201">Proje Gezgini'nde hello proje düğümüne sağ tıklayın ve seçin **yeni > sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-201">In Project Explorer, right-click on hello project node and select **New > Class**.</span></span>
2. <span data-ttu-id="5fe2d-202">İçinde **yeni Java sınıfı**, ad hello sınıfı `WebCreator` ve hello denetleyin **ortak statik void ana** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-202">In **New Java Class**, name hello class `WebCreator` and check hello **public static void main** checkbox.</span></span> <span data-ttu-id="5fe2d-203">Merhaba seçimleri aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-203">hello selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="5fe2d-204">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-204">Click **Finish**.</span></span> <span data-ttu-id="5fe2d-205">Merhaba WebCreator.java dosyası proje Gezgini'nde görünür.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-205">hello WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a><span data-ttu-id="5fe2d-206">Bir App Service Web uygulaması Hello Azure API tooCreate çağırma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-206">Calling hello Azure API tooCreate an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="5fe2d-207">Gerekli içeri aktarmaları ekleyin</span><span class="sxs-lookup"><span data-stu-id="5fe2d-207">Add necessary imports</span></span>
<span data-ttu-id="5fe2d-208">WebCreator.java içinde hello aşağıdaki içeri aktarmaları ekleyin; Bu içeri aktarmalar erişim tooclasses hello içinde Azure API'lerini kullanan yönetim kitaplıkları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-208">In WebCreator.java, add hello following imports; these imports provide access tooclasses in hello management libraries for consuming Azure APIs:</span></span>

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-hello-main-entry-point-class"></a><span data-ttu-id="5fe2d-209">Merhaba ana giriş noktası sınıf tanımlama</span><span class="sxs-lookup"><span data-stu-id="5fe2d-209">Define hello main entry point class</span></span>
<span data-ttu-id="5fe2d-210">Merhaba AzureWebDemo uygulama Hello amacı toocreate bir App Service Web uygulaması olduğundan, bu uygulama için hello ana sınıf adını `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-210">Because hello purpose of hello AzureWebDemo application is toocreate an App Service Web App, name hello main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="5fe2d-211">Bu sınıf hello Azure Hizmet Yönetimi API toocreate hello web uygulamasını çağıran hello ana giriş noktası kodu sağlar.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-211">This class provides hello main entry point code that calls hello Azure Service Management API toocreate hello web app.</span></span>

<span data-ttu-id="5fe2d-212">Parametre tanımları hello web uygulaması ve Web alanı için aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-212">Add hello following parameter definitions for hello web app and webspace.</span></span> <span data-ttu-id="5fe2d-213">Kendi Azure abonelik kimliği ve sertifika bilgilerini tooprovide gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-213">You will need tooprovide your own Azure subscription ID and certificate information.</span></span>

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

<span data-ttu-id="5fe2d-214">Burada:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-214">where:</span></span>

* <span data-ttu-id="5fe2d-215">`<subscription-id>`toocreate hello kaynak istediğiniz hello Azure abonelik kimliği değil.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-215">`<subscription-id>` is hello Azure subscription ID in which you want toocreate hello resource.</span></span>
* <span data-ttu-id="5fe2d-216">`<certificate-store-path>`Merhaba yol ve dosya adı toohello JKS yerel sertifika deposu dizininizde dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-216">`<certificate-store-path>` is hello path and filename toohello JKS file in your local certificate store directory.</span></span> <span data-ttu-id="5fe2d-217">Örneğin, `C:/Certificates/CertificateName.jks` Linux için ve `C:\Certificates\CertificateName.jks` Windows için.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="5fe2d-218">`<certificate-password>`Merhaba'a kadar olan JKS sertifikanızı oluştururken belirttiğiniz paroladır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-218">`<certificate-password>` is hello password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="5fe2d-219">`webAppName`Seçtiğiniz herhangi bir ad olabilir; Bu yordam hello adı kullanır `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-219">`webAppName` can be any name you choose; this procedure uses hello name `WebDemoWebApp`.</span></span> <span data-ttu-id="5fe2d-220">Merhaba tam etki alanı adıdır hello `webAppName` hello ile `domainName` eklenir, bu durumda hello tam etki alanı içinde `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-220">hello full domain name is hello `webAppName` with hello `domainName` appended, so in this case hello full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="5fe2d-221">`domainName`yukarıda gösterildiği gibi belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="5fe2d-222">`webSpaceName`hello tanımlanan hello değerlerinden biri olmalıdır [WebSpaceNames] [ WebSpaceNames] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-222">`webSpaceName` should be one of hello values defined in hello [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="5fe2d-223">`appServicePlanName`yukarıda gösterildiği gibi belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="5fe2d-224">**Not:** her zaman bu uygulamayı çalıştırmak, toochange hello değerini gerek `webAppName` ve `appServicePlanName` (veya hello Azure Portal hello web uygulamasını silmek) hello uygulamayı yeniden çalıştırmadan önce.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-224">**Note:** Each time you run this application, you need toochange hello value of `webAppName` and `appServicePlanName` (or delete hello web app on hello Azure Portal) before running hello application again.</span></span> <span data-ttu-id="5fe2d-225">Aksi takdirde Hello aynı kaynak Azure üzerinde zaten olduğundan yürütme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-225">Otherwise, execution will fail because hello same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-hello-web-creation-method"></a><span data-ttu-id="5fe2d-226">Merhaba web oluşturma yöntemini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="5fe2d-226">Define hello web creation method</span></span>
<span data-ttu-id="5fe2d-227">Ardından, bir yöntem toocreate hello web uygulaması tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-227">Next, define a method toocreate hello web app.</span></span> <span data-ttu-id="5fe2d-228">Bu yöntem `createWebApp`, hello web app ve hello Web alanı hello parametreleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-228">This method, `createWebApp`, specifies hello parameters of hello web app and hello webspace.</span></span> <span data-ttu-id="5fe2d-229">Ayrıca oluşturur ve hello tarafından tanımlanan hello App Service Web Apps yönetim istemcisini yapılandırır [WebSiteManagementClient] [ WebSiteManagementClient] nesnesi.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-229">It also creates and configures hello App Service Web Apps management client, which is defined by hello [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="5fe2d-230">anahtar toocreating Web Apps Hello yönetim istemcidir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-230">hello management client is key toocreating Web Apps.</span></span> <span data-ttu-id="5fe2d-231">Merhaba Hizmet Yönetimi API'sini çağırarak web uygulamaları (oluşturmak gibi güncelleştirme ve silme işlemlerini gerçekleştirme) uygulamaları toomanage izin RESTful web hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-231">It provides RESTful web services that allow applications toomanage web apps (performing operations such as create, update, and delete) by calling hello service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="5fe2d-232">Merhaba kod hello HTTP durum başarı veya başarısızlık belirten hello yanıtının çıkarır ve başarılı olursa, web uygulaması oluşturuldu hello hello adını çıkarır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-232">hello code will output hello HTTP status of hello response indicating success or failure, and if successful, will output hello name of hello created web app.</span></span>

#### <a name="define-hello-main-method"></a><span data-ttu-id="5fe2d-233">Merhaba main() yöntemi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="5fe2d-233">Define hello main() method</span></span>
<span data-ttu-id="5fe2d-234">Merhaba main() yönteminin kodu bu çağrıları createWebApp() toocreate hello web uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-234">Provide hello main() method code that calls createWebApp() toocreate hello web app.</span></span>

<span data-ttu-id="5fe2d-235">Son olarak, arama `createWebApp` gelen `main`:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a><span data-ttu-id="5fe2d-236">Merhaba uygulamayı çalıştırın ve web uygulaması oluşturma doğrulayın</span><span class="sxs-lookup"><span data-stu-id="5fe2d-236">Run hello application and verify web app creation</span></span>
<span data-ttu-id="5fe2d-237">Uygulamanızı çalıştıran, tooverify tıklatın **Çalıştır > Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-237">tooverify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="5fe2d-238">Merhaba uygulaması çalışıyor tamamlandığında, çıkış hello Eclipse konsolunda aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-238">When hello application completes running, you should see hello following output in hello Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="5fe2d-239">Klasik Azure portalı hello oturum ve'ı tıklatın **Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-239">Log into hello Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="5fe2d-240">Hello yeni web uygulaması, birkaç dakika içinde hello Web uygulamaları listesinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-240">hello new web app should appear in hello Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-toohello-web-app"></a><span data-ttu-id="5fe2d-241">Bir uygulama toohello Web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-241">Deploying an Application toohello Web App</span></span>
<span data-ttu-id="5fe2d-242">AzureWebDemo çalıştırıp hello yeni web uygulaması, hello Klasik portal günlüğüne oluşturulan tıklatın sonra **Web Apps**seçip **WebDemoWebApp** hello içinde **Web Apps** listesi.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-242">After you have run AzureWebDemo and created hello new web app, log into hello classic portal, click **Web Apps**, and select **WebDemoWebApp** in hello **Web Apps** list.</span></span> <span data-ttu-id="5fe2d-243">Merhaba web uygulamanızın panosu sayfasında tıklatın **Gözat** (veya hello URL'yi tıklatın `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-243">In hello web app's dashboard page, click **Browse** (or click hello URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span></span> <span data-ttu-id="5fe2d-244">İçerik yayımlanan toohello web uygulaması henüz bırakıldığından boş yer tutucu sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-244">You will see a blank placeholder page, because no content has been published toohello web app yet.</span></span>

<span data-ttu-id="5fe2d-245">Sonraki bir "Hello World" uygulaması oluşturacak ve toohello web uygulaması dağıtma.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-245">Next you will create a "Hello World" application and deploy it toohello web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="5fe2d-246">JSP Merhaba Dünya uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-246">Create a JSP Hello World application</span></span>
#### <a name="create-hello-application"></a><span data-ttu-id="5fe2d-247">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-247">Create hello application</span></span>
<span data-ttu-id="5fe2d-248">Nasıl toodeploy bir uygulama toohello web hello sipariş toodemonstrate içinde aşağıdaki yordamı, nasıl gösterir toocreate basit bir "Hello World" Java uygulaması ve Web uygulamanızı oluşturduğunuz uygulama hizmeti toohello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-248">In order toodemonstrate how toodeploy an application toohello web, hello following procedure shows you how toocreate a simple "Hello World" Java application and upload it toohello App Service Web App that your application created.</span></span>

1. <span data-ttu-id="5fe2d-249">Tıklatın **Dosya > Yeni > Dinamik Web projesi**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="5fe2d-250">Bunu, `JSPHello` olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-250">Name it `JSPHello`.</span></span> <span data-ttu-id="5fe2d-251">Bu iletişim kutusunda herhangi bir ayarı toochange gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-251">You do not need toochange any other settings in this dialog.</span></span> <span data-ttu-id="5fe2d-252">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="5fe2d-253">Proje Gezgini'nde hello genişletin **JSPHello** projesinde **WebContent**, ardından **yeni > JSP dosyası**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-253">In Project Explorer, expand hello **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="5fe2d-254">Merhaba yeni JSP dosyası iletişim kutusunda, hello yeni dosya adı `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-254">In hello New JSP File dialog, name hello new file `index.jsp`.</span></span> <span data-ttu-id="5fe2d-255">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-255">Click **Next**.</span></span>
3. <span data-ttu-id="5fe2d-256">Merhaba, **JSP şablon seç** iletişim kutusunda **yeni JSP dosyası (html)** tıklatıp **son**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-256">In hello **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="5fe2d-257">İndex.jsp içinde hello kodda aşağıdaki hello eklemek `<head>` ve `<body>` etiketi bölümler:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-257">In index.jsp, add hello following code in hello `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a><span data-ttu-id="5fe2d-258">İçinde localhost Hello Hello World uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="5fe2d-258">Run hello Hello World application in localhost</span></span>
<span data-ttu-id="5fe2d-259">Bu uygulamayı çalıştırmadan önce birkaç özelliği tooconfigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-259">Before you run this application, you need tooconfigure a few properties.</span></span>

1. <span data-ttu-id="5fe2d-260">Sağ hello **JSPHello** proje ve seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-260">Right-click hello **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="5fe2d-261">Merhaba, **özellikleri** iletişim: seçin **Java oluşturma yolu**seçin hello **sipariş ve dışarı aktarma** sekmesi, onay **JRE sistem kitaplığı**,'ye tıklayın **Yukarı** toomove onu hello listenin toohello.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-261">In hello **Properties** dialog: select **Java Build Path**, select hello **Order and Export** tab, check **JRE System Library**, then click **Up** toomove it toohello top of hello list.</span></span>
   
    ![][4]
3. <span data-ttu-id="5fe2d-262">Merhaba, ayrıca **özellikleri** iletişim: seçin **hedeflenen çalışma zamanları** tıklatıp **yeni**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-262">Also in hello **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="5fe2d-263">Merhaba, **yeni sunucu çalışma zamanı ortamı** iletişim, sunucusu gibi bir seçin **Apache Tomcat v7.0** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-263">In hello **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="5fe2d-264">Merhaba, **Tomcat sunucusunu** iletişim, kümesi **adı** çok`Apache Tomcat v7.0`ve ayarlayın **Tomcat yükleme dizinini** toohello directory hello sürümü yüklü Tomcat sunucusunu toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-264">In hello **Tomcat Server** dialog, set **Name** too`Apache Tomcat v7.0`, and set **Tomcat Installation Directory** toohello directory in which you installed hello version of Tomcat server you want toouse.</span></span>
   
    ![][5]
   
    <span data-ttu-id="5fe2d-265">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-265">Click **Finish**.</span></span>
5. <span data-ttu-id="5fe2d-266">Toohello sonra geri dönüp **hedeflenen çalışma zamanları** hello sayfasının **özellikleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-266">You then return toohello **Targeted Runtimes** page of hello **Properties** dialog.</span></span> <span data-ttu-id="5fe2d-267">Seçin **Apache Tomcat v7.0**, ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="5fe2d-268">Merhaba Eclipse içinde **çalıştırmak** menüsünde tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-268">In hello Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="5fe2d-269">Merhaba, **Çalıştır** iletişim kutusunda **sunucu üzerinde çalışan**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-269">In hello **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="5fe2d-270">Merhaba, **sunucu üzerinde çalışan** iletişim kutusunda **Tomcat v7.0 sunucusu**:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-270">In hello **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="5fe2d-271">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-271">Click **Finish**.</span></span>
7. <span data-ttu-id="5fe2d-272">Olduğunda, uygulama çalıştığında Merhaba, hello görmelisiniz **JSPHello** sayfa görünür Eclipse localhost penceresinde (`http://localhost:8080/JSPHello/`), görüntüleme hello ileti:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-272">When hello application runs, you should see hello **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying hello following message:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a><span data-ttu-id="5fe2d-273">Merhaba uygulaması bir WAR olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-273">Export hello application as a WAR</span></span>
<span data-ttu-id="5fe2d-274">Böylece toohello web uygulaması dağıtma hello web projesi dosyaları web arşivi (WAR) dosyası dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-274">Export hello web project files as a web archive (WAR) file so that you can deploy it toohello web app.</span></span> <span data-ttu-id="5fe2d-275">Merhaba aşağıdaki web projesi dosyaları hello WebContent klasöründe bulunur:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-275">hello following web project files reside in hello WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="5fe2d-276">Merhaba WebContent klasörünü sağ tıklatın ve seçin **verme**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-276">Right-click hello WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="5fe2d-277">Merhaba, **ver'i seçin** iletişim kutusunda, tıklatın **Web > WAR** dosya ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-277">In hello **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="5fe2d-278">Merhaba, **WAR dışarı** iletişim kutusunda, hello geçerli projede hello src dizin seçin ve hello WAR dosyasını hello sonunda hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-278">In hello **WAR Export** dialog, select hello src directory in hello current project, and include hello name of hello WAR file at hello end.</span></span> <span data-ttu-id="5fe2d-279">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="5fe2d-280">WAR dosyaları dağıtma hakkında daha fazla bilgi için bkz: [bir Java uygulaması tooAzure App Service Web Apps eklemek](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="5fe2d-280">For more information on deploying WAR files, see [Add a Java application tooAzure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-hello-hello-world-application-using-ftp"></a><span data-ttu-id="5fe2d-281">Merhaba Hello World uygulama kullanarak FTP dağıtma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-281">Deploying hello Hello World Application Using FTP</span></span>
<span data-ttu-id="5fe2d-282">Bir üçüncü taraf FTP istemcisi toopublish hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-282">Select a third-party FTP client toopublish hello application.</span></span> <span data-ttu-id="5fe2d-283">Bu yordam, iki seçenek açıklar: Azure'da; yerleşik hello Kudu konsol ve FileZilla, kolay ve grafik kullanıcı Arabirimi ile popüler bir araç.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-283">This procedure describes two options: hello Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="5fe2d-284">**Not:** Azure Araç Seti hello Eclipse destekleyen dağıtım toostorage hesapları ve bulut Hizmetleri, ancak şu anda dağıtım tooweb uygulamaları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-284">**Note:** hello Azure Toolkit for Eclipse supports deployment toostorage accounts and cloud services, but does not currently support deployment tooweb apps.</span></span> <span data-ttu-id="5fe2d-285">Toostorage hesapları dağıtmayı ve bulut hizmetlerini açıklandığı gibi Azure dağıtım projesi kullanarak [bir Hello World uygulamasının Azure için Eclipse'te oluşturma](http://msdn.microsoft.com/library/azure/hh690944.aspx), ancak değil tooweb uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-285">You can deploy toostorage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not tooweb apps.</span></span> <span data-ttu-id="5fe2d-286">FTP veya GitHub tootransfer dosyaları tooyour web uygulaması gibi diğer yöntemleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-286">Use other methods such as FTP or GitHub tootransfer files tooyour web app.</span></span>
> 
> <span data-ttu-id="5fe2d-287">**Not:** hello Windows komut isteminde (Windows ile birlikte gelen hello komut satırı FTP.EXE yardımcı programı) FTP kullanmanızı önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-287">**Note:** We do not recommend using FTP from hello Windows command prompt (hello command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="5fe2d-288">FTP.EXE gibi etkin FTP Kullan FTP istemcileri, güvenlik duvarları toowork sık sık başarısız.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-288">FTP clients that use active FTP, such as FTP.EXE, often fail toowork over firewalls.</span></span> <span data-ttu-id="5fe2d-289">Bir iç LAN tabanlı adresi etkin FTP belirtir, toowhich bir FTP sunucusu tooconnect büyük olasılıkla başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-289">Active FTP specifies an internal LAN-based address, toowhich an FTP server will likely fail tooconnect.</span></span>
> 
> 

<span data-ttu-id="5fe2d-290">FTP kullanarak dağıtım tooan App Service web uygulaması hakkında daha fazla bilgi için aşağıdaki konularda hello bakın:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-290">For more information on deployment tooan App Service web app using FTP, see hello following topics:</span></span>

* [<span data-ttu-id="5fe2d-291">Bir FTP yardımcı programını kullanarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="5fe2d-292">Dağıtım kimlik bilgilerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="5fe2d-292">Set up deployment credentials</span></span>
<span data-ttu-id="5fe2d-293">Merhaba çalıştırmak olduğundan emin olun **AzureWebDemo** uygulama toocreate bir web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-293">Make sure you have run hello **AzureWebDemo** application toocreate a web app.</span></span> <span data-ttu-id="5fe2d-294">Dosyaları toothis konumu aktarır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-294">You will transfer files toothis location.</span></span>

1. <span data-ttu-id="5fe2d-295">Oturum hello Klasik Portalı'na ve tıklatın **Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-295">Log into hello classic portal and click **Web Apps**.</span></span> <span data-ttu-id="5fe2d-296">Emin olun **WebDemoWebApp** hello web uygulamaları listesinde görüntülenir ve çalışır durumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-296">Make sure **WebDemoWebApp** appears in hello list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="5fe2d-297">Tıklatın **WebDemoWebApp** tooopen kendi **Pano** sayfası.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-297">Click **WebDemoWebApp** tooopen its **Dashboard** page.</span></span>
2. <span data-ttu-id="5fe2d-298">Merhaba üzerinde **Pano** sayfasında **Hızlı Bakış**, tıklatın **, dağıtım kimlik bilgilerini ayarlayın** (dağıtım kimlik bilgileri zaten varsa bu okur  **Dağıtım kimlik bilgilerinizi sıfırlayın**).</span><span class="sxs-lookup"><span data-stu-id="5fe2d-298">On hello **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="5fe2d-299">Dağıtım kimlik bilgileri bir Microsoft hesabıyla ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="5fe2d-300">Toospecify bir kullanıcı adı ve parola, Git ve FTP kullanarak toodeploy kullanabileceğiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-300">You need toospecify a username and password that you can use toodeploy using Git and FTP.</span></span> <span data-ttu-id="5fe2d-301">Bu kimlik bilgileri toodeploy tooany web uygulaması, Microsoft hesabınızla ilişkili tüm Azure abonelikleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-301">You can use these credentials toodeploy tooany web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="5fe2d-302">Git ve FTP dağıtımı kimlik bilgilerini hello iletişim kutusunda, kayıt hello kullanıcı adı ve parola gelecekte kullanılmak üzere sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-302">Provide Git and FTP deployment credentials in hello dialog, and record hello username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="5fe2d-303">FTP bağlantı bilgileri alma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-303">Get FTP connection information</span></span>
<span data-ttu-id="5fe2d-304">toouse FTP toodeploy uygulama dosyaları toohello yeni oluşturulan web uygulaması, tooobtain bağlantı bilgilerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-304">toouse FTP toodeploy application files toohello newly created web app, you need tooobtain connection information.</span></span> <span data-ttu-id="5fe2d-305">Tooobtain bağlantı bilgilerini iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-305">There are two ways tooobtain connection information.</span></span> <span data-ttu-id="5fe2d-306">Toovisit hello web uygulamanızın tek yönlü **Pano** sayfasında; hello diğer toodownload hello web uygulamanızın yayımlama profili yoludur.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-306">One way is toovisit hello web app's **Dashboard** page; hello other way is toodownload hello web app's publish profile.</span></span> <span data-ttu-id="5fe2d-307">Merhaba yayımlama profili web uygulamalarınızda Azure App Service için FTP ana bilgisayar adı ve oturum açma kimlik bilgileri gibi bilgileri sağlayan bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-307">hello publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="5fe2d-308">Bu kullanıcı adı ve parola toodeploy tooany web uygulaması hello ile Azure hesabı değil yalnızca bu bir ilişkili tüm Aboneliklerde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-308">You can use this username and password toodeploy tooany web app in all subscriptions associated with hello Azure account, not only this one.</span></span>

<span data-ttu-id="5fe2d-309">Merhaba web uygulamanızın dikey penceresinde hello tooobtain FTP bağlantı bilgileri [Azure Portal][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-309">tooobtain FTP connection information from hello web app's blade in hello [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="5fe2d-310">Altında **Essentials**, bulma ve kopyalama hello **FTP ana bilgisayar adı**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-310">Under **Essentials**, find and copy hello **FTP hostname**.</span></span> <span data-ttu-id="5fe2d-311">Bu çok benzer bir URI değil`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-311">This is a URI similar too`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="5fe2d-312">Altında **Essentials**, bulma ve kopyalama **FTP/dağıtım kullanıcı adı**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="5fe2d-313">Bu hello biçimde olacaktır *webappname\deployment-username*; örneğin `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-313">This will have hello form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="5fe2d-314">tooobtain FTP bağlantı bilgileri hello profili yayımlayın:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-314">tooobtain FTP connection information from hello publish profile:</span></span>

1. <span data-ttu-id="5fe2d-315">Merhaba web uygulamanızın dikey penceresinde tıklayın **Get yayımlama profili**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-315">In hello web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="5fe2d-316">Bu .publishsettings dosyasını tooyour yerel bir sürücünün indirir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-316">This will download a .publishsettings file tooyour local drive.</span></span>
2. <span data-ttu-id="5fe2d-317">Bir XML Düzenleyicisi'ni veya metin düzenleyicide hello .publishsettings dosyasını açın ve hello bulur `<publishProfile>` öğeyi içeren `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-317">Open hello .publishsettings file in an XML editor or text editor and find hello `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="5fe2d-318">Merhaba aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-318">It should look like hello following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="5fe2d-319">Bu hello web uygulamanızın Not `publishProfile` ayarları aşağıdaki gibi toohello FileZilla Site Yöneticisi ayarları eşleyin:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-319">Note that hello web app's `publishProfile` settings map toohello FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="5fe2d-320">`publishUrl`olduğundan, hello aynı **FTP konak adı**, hello içinde ayarladığınız değer **konak**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-320">`publishUrl` is hello same as **FTP host name**, hello value you set in **Host**.</span></span>
* <span data-ttu-id="5fe2d-321">`publishMethod="FTP"`ayarladığınız anlamına gelir **Protokolü** çok**FTP - Dosya Aktarım Protokolü**, ve **şifreleme** çok**düz FTP Kullan**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-321">`publishMethod="FTP"` means that you set **Protocol** too**FTP - File Transfer Protocol**, and **Encryption** too**Use plain FTP**.</span></span>
* <span data-ttu-id="5fe2d-322">`userName`ve `userPWD` hello tuşları belirtilen hello dağıtım kimlik bilgileri sıfırlandığında gerçek kullanıcı adı ve parola değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-322">`userName` and `userPWD` are keys for hello actual username and password values you specified when you reset hello deployment credentials.</span></span> <span data-ttu-id="5fe2d-323">`userName`olduğundan, hello aynı **dağıtım / FTP kullanıcısı**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-323">`userName` is hello same as **Deployment / FTP user**.</span></span> <span data-ttu-id="5fe2d-324">Bunlar çok eşleme**kullanıcı** ve **parola** FileZilla içinde.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-324">They map too**User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="5fe2d-325">`ftpPassiveMode="True"`Bu hello FTP sitesi edilgen FTP aktarımı kullanır anlamına gelir; seçin **pasif** hello üzerinde **aktarım ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-325">`ftpPassiveMode="True"` means that hello FTP site uses passive FTP transfer; select **Passive** on hello **Transfer Settings** tab.</span></span>

#### <a name="configure-hello-web-app-toohost-a-java-application"></a><span data-ttu-id="5fe2d-326">Merhaba Web uygulaması toohost bir Java uygulaması yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5fe2d-326">Configure hello Web App toohost a Java application</span></span>
<span data-ttu-id="5fe2d-327">Merhaba uygulaması yayımlamadan önce böylece hello web uygulaması bir Java uygulamasını barındırmak birkaç yapılandırma ayarlarını toochange gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-327">Before you publish hello application, you need toochange a few configuration settings so that hello web app can host a Java application.</span></span>

1. <span data-ttu-id="5fe2d-328">Merhaba Klasik Portalı'nda, toohello web uygulamanızın Git **Pano** sayfasında ve tıklayın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-328">In hello classic portal, go toohello web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="5fe2d-329">Merhaba üzerinde **yapılandırma** sayfasında, ayarları aşağıdaki hello belirtin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-329">On hello **Configure** page, specify hello following settings.</span></span>
2. <span data-ttu-id="5fe2d-330">İçinde **Java sürümü** hello varsayılandır **devre dışı**; select hello Java sürümü, uygulama hedeflerine; örneğin 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-330">In **Java version** hello default is **Off**; select hello Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="5fe2d-331">Bunu yaptıktan sonra da emin olmanız **Web kapsayıcısına** Tomcat sunucusunu tooa sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-331">After you do this, also make sure that **Web container** is set tooa version of Tomcat Server.</span></span>
3. <span data-ttu-id="5fe2d-332">İçinde **varsayılan belgeler**, index.jsp ekleyin ve toohello listenin hello taşır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-332">In **Default Documents**, add index.jsp and move it up toohello top of hello list.</span></span> <span data-ttu-id="5fe2d-333">(Merhaba varsayılan web uygulamaları için hostingstart.html dosyasıdır.)</span><span class="sxs-lookup"><span data-stu-id="5fe2d-333">(hello default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="5fe2d-334">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="5fe2d-335">Kudu kullanarak uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="5fe2d-335">Publish your application using Kudu</span></span>
<span data-ttu-id="5fe2d-336">Tek yönlü toopublish hello toouse hello Kudu hata ayıklama Azure'da yerleşik konsol uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-336">One way toopublish hello application is toouse hello Kudu debug console built into Azure.</span></span> <span data-ttu-id="5fe2d-337">Kudu toobe kararlı ve App Service Web Apps ve Tomcat Server ile tutarlı denir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-337">Kudu is known toobe stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="5fe2d-338">Form aşağıdaki hello tooa URL'sini göz atarak hello konsol hello web uygulaması için erişim:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-338">You access hello console for hello web app by browsing tooa URL of hello following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="5fe2d-339">Bu yordam, hello Kudu konsol URL aşağıdaki hello bulunur; toothis konuma göz atın:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-339">For this procedure, hello Kudu console is located at hello following URL; browse toothis location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="5fe2d-340">Merhaba üst menüsünden seçin **Hata Ayıkla Konsolu > CMD**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-340">From hello top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="5fe2d-341">Hello konsol komut satırında çok gidin`/site/wwwroot` (veya `site`, ardından `wwwroot` hello sayfanın üst kısmındaki hello hello dizin görünümünde):</span><span class="sxs-lookup"><span data-stu-id="5fe2d-341">In hello console command line, navigate too`/site/wwwroot` (or click `site`, then `wwwroot` in hello directory view at hello top of hello page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="5fe2d-342">Belirttikten sonra **Java Sürüm**, Tomcat sunucusunun webapps dizinine oluşturmanız.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="5fe2d-343">Merhaba konsol komut satırında toohello webapps dizinine gidin:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-343">In hello console command line, navigate toohello webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="5fe2d-344">Gelen JSPHello.war sürükleyin `<project-path>/JSPHello/src/` ve gelsin hello Kudu dizini altında bırakma `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into hello Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="5fe2d-345">Tomcat sıkıştırmasını çünkü bunu toohello "tooupload ve ZIP buraya sürükleyin" alanı, sürükleyin değil.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-345">Do not drag it toohello "Drag here tooupload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="5fe2d-346">İlk JSPHello.war hello dizin alanında kendisi tarafından görünür:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-346">At first JSPHello.war appears in hello directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="5fe2d-347">Kısa bir süre (büyük olasılıkla 5 dakikadan daha az) paketten JSPHello dizine hello WAR dosyasını Tomcat sunucusunu ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip hello WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="5fe2d-348">İndex.jsp olduğundan sıkıştırması açılmış ve orada kopyalanan olup olmadığını hello kök dizin toosee'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-348">Click hello ROOT directory toosee whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="5fe2d-349">Dizini oluşturulan JSPHello Hello açılmış olup olmadığını varsa, arka toohello webapps dizinine toosee gidin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-349">If so, navigate back toohello webapps directory toosee whether hello unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="5fe2d-350">Bu öğeleri görmüyorsanız bekleyin ve yineleyin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="5fe2d-351">FileZilla (isteğe bağlı) kullanarak uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="5fe2d-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="5fe2d-352">Toopublish Merhaba uygulaması kullanabileceğiniz başka bir FileZilla, kolay ve grafik kullanıcı Arabirimi ile popüler bir üçüncü taraf FTP istemcisi aracıdır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-352">Another tool you can use toopublish hello application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="5fe2d-353">Gelen FileZilla yükleyip [http://filezilla-project.org/](http://filezilla-project.org/) zaten olmayan.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="5fe2d-354">Hello hello istemci kullanma hakkında daha fazla bilgi için bkz: [FileZilla belgelerine](https://wiki.filezilla-project.org/Documentation) ve bu blog girişi [FTP istemcileri - bölümü 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="5fe2d-354">For more information on using hello client, see hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="5fe2d-355">FileZilla içinde tıklatın **Dosya > Site Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="5fe2d-356">Merhaba, **Site Yöneticisi** iletişim kutusunda, tıklatın **Yeni Site**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-356">In hello **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="5fe2d-357">Yeni ve boş bir FTP sitesi görünür **seçin girişi** tooprovide bir ad isteyen.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-357">A new blank FTP site will appear in **Select Entry** prompting you tooprovide a name.</span></span> <span data-ttu-id="5fe2d-358">Bu yordam, adlandırın `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="5fe2d-359">Merhaba üzerinde **genel** sekmesinde, ayarlar aşağıdaki hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-359">On hello **General** tab, specify hello following settings:</span></span>
   
   * <span data-ttu-id="5fe2d-360">**Ana bilgisayarı:** Enter hello **FTP konak adı** hello panodan kopyaladığınız.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-360">**Host:** Enter hello **FTP Host Name** that you copied from hello dashboard.</span></span>
   * <span data-ttu-id="5fe2d-361">**Bağlantı noktası:** (Bu bu pasif aktarımı ve hello sunucu başlangıç bağlantı noktası toouse belirleyecektir olarak boş bırakın.)</span><span class="sxs-lookup"><span data-stu-id="5fe2d-361">**Port:** (Leave this blank, as this is a passive transfer and hello server will determine hello port toouse.)</span></span>
   * <span data-ttu-id="5fe2d-362">**Protokol:** FTP Dosya Aktarım Protokolü</span><span class="sxs-lookup"><span data-stu-id="5fe2d-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="5fe2d-363">**Şifreleme:** düz FTP Kullan</span><span class="sxs-lookup"><span data-stu-id="5fe2d-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="5fe2d-364">**Oturum açma türü:** Normal</span><span class="sxs-lookup"><span data-stu-id="5fe2d-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="5fe2d-365">**Kullanıcı:** Enter hello dağıtım / FTP kullanıcısı hello panodan kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-365">**User:** Enter hello Deployment / FTP user that you copied from hello dashboard.</span></span> <span data-ttu-id="5fe2d-366">Merhaba form olan hello tam FTP kullanıcı adı, budur *webappname\username*.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-366">This is hello full FTP username, which has hello form *webappname\username*.</span></span>
   * <span data-ttu-id="5fe2d-367">**Parola:** hello dağıtım kimlik bilgileri ayarlandığında belirtilen hello parola gir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-367">**Password:** Enter hello password that you specified when you set hello deployment credentials.</span></span>
     
     <span data-ttu-id="5fe2d-368">Merhaba üzerinde **aktarım ayarları** sekmesine **pasif**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-368">On hello **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="5fe2d-369">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-369">Click **Connect**.</span></span> <span data-ttu-id="5fe2d-370">Başarılı, FileZilla'nin Konsolu görüntüler varsa bir `Status: Connected` iletisi ve sorunu bir `LIST` toolist hello dizin içeriği komutu.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command toolist hello directory contents.</span></span>
4. <span data-ttu-id="5fe2d-371">Merhaba, **yerel** site paneli seçin hello kaynak hangi hello JSPHello.war dosya dizindeki; hello yolu benzer toohello şu olacaktır:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-371">In hello **Local** site panel, select hello source directory in which hello JSPHello.war file resides; hello path will be similar toohello following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="5fe2d-372">Merhaba, **uzak** site paneli, select hello hedef klasör.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-372">In hello **Remote** site panel, select hello destination folder.</span></span> <span data-ttu-id="5fe2d-373">Merhaba WAR dosyası toohello dağıtacağınız `webapps` hello web uygulamanızın kök altında dizin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-373">You will deploy hello WAR file toohello `webapps` directory under hello web app's root.</span></span> <span data-ttu-id="5fe2d-374">Çok gidin`/site/wwwroot`, sağ tıklayın `wwwroot`seçip **dizin oluştur**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-374">Navigate too`/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="5fe2d-375">Adı hello dizini `webapps` ve o dizini girin.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-375">Name hello directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="5fe2d-376">JSPHello.war çok aktarım`/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-376">Transfer JSPHello.war too`/site/wwwroot/webapps`.</span></span> <span data-ttu-id="5fe2d-377">Hello JSPHello.war seçin **yerel** dosya listesi, üzerinde sağ tıklatın ve seçin **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-377">Select JSPHello.war in hello **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="5fe2d-378">Bunun görüntülendiğini görmeniz gerekir `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="5fe2d-379">JSPHello.war toohello webapps dizinine kopyaladıktan sonra Tomcat sunucusunun otomatik olarak açın (sıkıştırmasını açın) hello hello WAR dosyasını dosyalarında.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-379">After you copy JSPHello.war toohello webapps directory, Tomcat Server will automatically unpack (unzip) hello files in hello WAR file.</span></span> <span data-ttu-id="5fe2d-380">Tomcat sunucusunu hemen paketi açılırken başlasa uzun sürebilir hello FTP İstemcisi'nde hello dosyaları tooappear için süresi (büyük olasılıkla saat).</span><span class="sxs-lookup"><span data-stu-id="5fe2d-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for hello files tooappear in hello FTP client.</span></span>

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a><span data-ttu-id="5fe2d-381">Web uygulaması hello üzerinde Hello Hello World uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="5fe2d-381">Run hello Hello World application on hello Web App</span></span>
1. <span data-ttu-id="5fe2d-382">Merhaba WAR dosyasını karşıya ve Tomcat sunucusunun bir paketten oluşturdu doğruladıktan sonra `JSPHello` dizini çok Gözat`http://webdemowebapp.azurewebsites.net/JSPHello` toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-382">After you have uploaded hello WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse too`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello application.</span></span>
   
   > <span data-ttu-id="5fe2d-383">**Not:** tıklatırsanız **Gözat** hello Klasik portalından hello varsayılan Web sayfası, "Bu temel Java web uygulaması başarıyla oluşturuldu." belirten alabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5fe2d-383">**Note:** If you click **Browse** from hello classic portal, you might get hello default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="5fe2d-384">Sipariş tooview hello uygulama çıktıda hello varsayılan Web sayfası yerine toorefresh hello Web sayfası olabilir.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-384">You might have toorefresh hello webpage in order tooview hello application output instead of hello default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="5fe2d-385">Merhaba uygulamayı çalıştırdığında, çıktı aşağıdaki hello ile bir web sayfasını görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="5fe2d-385">When hello application runs, you should see a web page with hello following output:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="5fe2d-386">Azure kaynakları temizlemek</span><span class="sxs-lookup"><span data-stu-id="5fe2d-386">Clean up Azure resources</span></span>
<span data-ttu-id="5fe2d-387">Bu yordam, App Service web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="5fe2d-388">Mevcut olduğu sürece hello kaynak için Fatura edilecek.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-388">You will be billed for hello resource as long as it exists.</span></span> <span data-ttu-id="5fe2d-389">Toocontinue hello web uygulaması sınama veya geliştirme için kullanmayı planlamıyorsanız, durdurma veya silme düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-389">Unless you plan toocontinue using hello web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="5fe2d-390">Durduruldu bir web uygulaması küçük bir ücret doğurur, ancak herhangi bir zamanda yeniden başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="5fe2d-391">Bir web uygulaması silme tooit karşıya yüklediğiniz tüm verileri siler.</span><span class="sxs-lookup"><span data-stu-id="5fe2d-391">Deleting a web app erases all data you have uploaded tooit.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com

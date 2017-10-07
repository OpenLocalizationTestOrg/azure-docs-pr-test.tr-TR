---
title: "aaaDeploy bölünmüş birleştirme hizmetine | Microsoft Docs"
description: "Bölme ve esnek veritabanı araçları ile birleştirme"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="2f578-103">Ayırma-birleştirme hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="2f578-103">Deploy a split-merge service</span></span>
<span data-ttu-id="2f578-104">Merhaba bölünmüş Birleştirme aracı parçalı veritabanları arasında veri taşımanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2f578-104">hello split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="2f578-105">Bkz: [ölçeklendirilmiş bulut veritabanları arasında veri taşıma](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="2f578-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-hello-split-merge-packages"></a><span data-ttu-id="2f578-106">Merhaba bölünmüş birleştirme paketlerini yükleyin</span><span class="sxs-lookup"><span data-stu-id="2f578-106">Download hello Split-Merge packages</span></span>
1. <span data-ttu-id="2f578-107">Merhaba en son NuGet sürümü [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="2f578-107">Download hello latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="2f578-108">Bir komut istemi açın ve nuget.exe indirdiğiniz toohello dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="2f578-108">Open a command prompt and navigate toohello directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="2f578-109">Merhaba indirme PowerShell commmands içerir.</span><span class="sxs-lookup"><span data-stu-id="2f578-109">hello download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="2f578-110">Merhaba komutu aşağıda ile Merhaba geçerli dizine Hello son bölünmüş birleştirme paketini indirin:</span><span class="sxs-lookup"><span data-stu-id="2f578-110">Download hello latest Split-Merge package into hello current directory with hello below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="2f578-111">Merhaba dosyaları adlı bir dizinde yerleştirilir **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** nerede *x.x.xxx.x* hello sürüm numarası yansıtır.</span><span class="sxs-lookup"><span data-stu-id="2f578-111">hello files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects hello version number.</span></span> <span data-ttu-id="2f578-112">Merhaba hello bölünmüş birleştirme hizmet dosyalarını bulmak **content\splitmerge\service** alt dizini ve hello bölünmüş birleştirme PowerShell komut dosyaları (ve gerekli istemci .dll) hello **content\splitmerge\powershell** alt dizini.</span><span class="sxs-lookup"><span data-stu-id="2f578-112">Find hello split-merge Service files in hello **content\splitmerge\service** sub-directory, and hello Split-Merge PowerShell scripts (and required client .dlls) in hello **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f578-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2f578-113">Prerequisites</span></span>
1. <span data-ttu-id="2f578-114">Merhaba bölünmüş birleştirme durumu veritabanı olarak kullanılacak bir Azure SQL DB veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f578-114">Create an Azure SQL DB database that will be used as hello split-merge status database.</span></span> <span data-ttu-id="2f578-115">Toohello Git [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f578-115">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2f578-116">Yeni bir **SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="2f578-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="2f578-117">Merhaba veritabanı bir ad verin ve yeni yönetici ve parola oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f578-117">Give hello database a name and create a new administrator and password.</span></span> <span data-ttu-id="2f578-118">Daha sonra kullanmak için emin toorecord hello adı ve parola olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f578-118">Be sure toorecord hello name and password for later use.</span></span>
2. <span data-ttu-id="2f578-119">Azure SQL DB sunucunuz Azure Hizmetleri tooconnect tooit verdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2f578-119">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="2f578-120">Merhaba portalında, hello **güvenlik duvarı ayarlarını**, o hello olun **tooAzure Hizmetleri erişimine izin** ayar çok**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="2f578-120">In hello portal, in hello **Firewall Settings**, ensure that hello **Allow access tooAzure Services** setting is set too**On**.</span></span> <span data-ttu-id="2f578-121">Merhaba "Kaydet" simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f578-121">Click hello "save" icon.</span></span>
   
   ![İzin verilen hizmetler][1]
3. <span data-ttu-id="2f578-123">Tanılama çıktı için kullanılacak bir Azure depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f578-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="2f578-124">Toohello Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="2f578-124">Go toohello Azure Portal.</span></span> <span data-ttu-id="2f578-125">Merhaba sol çubuğunda, **yeni**, tıklatın **veri + depolama**, ardından **depolama**.</span><span class="sxs-lookup"><span data-stu-id="2f578-125">In hello left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="2f578-126">Bölünmüş birleştirme hizmetinizi içerecek bir Azure bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f578-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="2f578-127">Toohello Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="2f578-127">Go toohello Azure Portal.</span></span> <span data-ttu-id="2f578-128">Merhaba sol çubuğunda, **yeni**, ardından **işlem**, **bulut hizmeti**, ve **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="2f578-128">In hello left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="2f578-129">Bölünmüş birleştirme hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2f578-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="2f578-130">Bölünmüş birleştirme hizmet yapılandırması</span><span class="sxs-lookup"><span data-stu-id="2f578-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="2f578-131">Merhaba bölünmüş birleştirme derlemeleri indirdiğiniz hello klasöründe hello bir kopyasını oluşturmak **ServiceConfiguration.Template.cscfg** yanında sevk dosya **SplitMergeService.cspkg** ve yeniden adlandırın **ServiceConfiguration.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="2f578-131">In hello folder where you downloaded hello Split-Merge assemblies, create a copy of hello **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="2f578-132">Açık **ServiceConfiguration.cscfg** girişleri hello biçimi sertifika parmak izleri gibi doğrulama Visual Studio gibi bir metin düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="2f578-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as hello format of certificate thumbprints.</span></span>
3. <span data-ttu-id="2f578-133">Yeni bir veritabanı oluşturmak veya hello durum veritabanı bölünmüş birleştirme işlemleri için varolan bir veritabanı tooserve seçin ve bu veritabanının hello bağlantı dizesini almak.</span><span class="sxs-lookup"><span data-stu-id="2f578-133">Create a new database or choose an existing database tooserve as hello status database for Split-Merge operations and retrieve hello connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="2f578-134">Şu anda hello durum veritabanı hello Latin harmanlamayı kullanması gerekir (SQL\_Latin1\_genel\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="2f578-134">At this time, hello status database must use hello Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="2f578-135">Daha fazla bilgi için bkz: [Windows harmanlama adı (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f578-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="2f578-136">Azure SQL DB ile Merhaba bağlantı dizesi genellikle hello şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="2f578-136">With Azure SQL DB, hello connection string typically is of hello form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="2f578-137">Her iki hello hello cscfg dosyasında bu bağlantı dizesi girin **SplitMergeWeb** ve **SplitMergeWorker** hello ElasticScaleMetadata ayarı rol bölümlerde.</span><span class="sxs-lookup"><span data-stu-id="2f578-137">Enter this connection string in hello cscfg file in both hello **SplitMergeWeb** and **SplitMergeWorker** role sections in hello ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="2f578-138">Hello için **SplitMergeWorker** rol, geçerli bir bağlantı dizesi tooAzure depolama Merhaba girin **WorkerRoleSynchronizationStorageAccountConnectionString** ayarı.</span><span class="sxs-lookup"><span data-stu-id="2f578-138">For hello **SplitMergeWorker** role, enter a valid connection string tooAzure storage for hello **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="2f578-139">Güvenliği yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2f578-139">Configure security</span></span>
<span data-ttu-id="2f578-140">Ayrıntılı yönergeler tooconfigure hello güvenlik hello hizmetinin için toohello başvuran [bölünmüş birleştirme Güvenlik Yapılandırması](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="2f578-140">For detailed instructions tooconfigure hello security of hello service, refer toohello [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="2f578-141">Bu öğretici için basit bir sınama dağıtımı Hello amaçları doğrultusunda, yapılandırma adımları olacaktır en az sayıda tooget hello hizmeti çalışır gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2f578-141">For hello purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed tooget hello service up and running.</span></span> <span data-ttu-id="2f578-142">Bu adımları yalnızca hello bir makine/toocommunicate hello hizmetiyle yürütme hesabını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2f578-142">These steps enable only hello one machine/account executing them toocommunicate with hello service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="2f578-143">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f578-143">Create a self-signed certificate</span></span>
<span data-ttu-id="2f578-144">Yeni bir dizin oluşturun ve aşağıdaki komutu kullanarak bu dizine yürütme hello bir [Visual Studio için geliştirici komut istemi](http://msdn.microsoft.com/library/ms229859.aspx) penceresi:</span><span class="sxs-lookup"><span data-stu-id="2f578-144">Create a new directory and from this directory execute hello following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="2f578-145">Parola tooprotect hello için özel bir anahtar istenir.</span><span class="sxs-lookup"><span data-stu-id="2f578-145">You are asked for a password tooprotect hello private key.</span></span> <span data-ttu-id="2f578-146">Güçlü bir parola girin ve onaylayın.</span><span class="sxs-lookup"><span data-stu-id="2f578-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="2f578-147">Bir kez daha sonra kullanılan hello parola toobe için istenir.</span><span class="sxs-lookup"><span data-stu-id="2f578-147">You are then prompted for hello password toobe used once more after that.</span></span> <span data-ttu-id="2f578-148">Tıklatın **Evet** hello son tooimport adresindeki onu toohello güvenilen sertifika yetkilileri kök deponuza.</span><span class="sxs-lookup"><span data-stu-id="2f578-148">Click **Yes** at hello end tooimport it toohello Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="2f578-149">Bir PFX dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f578-149">Create a PFX file</span></span>
<span data-ttu-id="2f578-150">Hello komutu aşağıdaki hello yürütme nerede makecert yürütüldü; aynı penceresi Kullanım, kullanılan toocreate hello sertifikanın aynı parolayı hello:</span><span class="sxs-lookup"><span data-stu-id="2f578-150">Execute hello following command from hello same window where makecert was executed; use hello same password that you used toocreate hello certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a><span data-ttu-id="2f578-151">Merhaba kişisel deposuna Hello istemci sertifikasını içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="2f578-151">Import hello client certificate into hello personal store</span></span>
1. <span data-ttu-id="2f578-152">Windows Gezgini'nde çift tıklayarak **mycert.pfx'i**.</span><span class="sxs-lookup"><span data-stu-id="2f578-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="2f578-153">Merhaba, **Sertifika Alma Sihirbazı'nı** seçin **geçerli kullanıcı** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2f578-153">In hello **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="2f578-154">Merhaba dosya yolunu doğrulayın ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2f578-154">Confirm hello file path and click **Next**.</span></span>
4. <span data-ttu-id="2f578-155">Türü hello parola bırakın **dahil tüm genişletilmiş özellikleri** denetlenir ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2f578-155">Type hello password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="2f578-156">Bırakın **Otomatik Seç hello sertifika deposu [...]**  denetlenir ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2f578-156">Leave **Automatically select hello certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="2f578-157">Tıklatın **son** ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2f578-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a><span data-ttu-id="2f578-158">Merhaba PFX dosyası toohello bulut hizmeti karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="2f578-158">Upload hello PFX file toohello cloud service</span></span>
1. <span data-ttu-id="2f578-159">Toohello Git [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f578-159">Go toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2f578-160">Seçin **bulut hizmetlerini**.</span><span class="sxs-lookup"><span data-stu-id="2f578-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="2f578-161">Merhaba bölünmüş/Merge hizmeti için yukarıda oluşturduğunuz hello bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="2f578-161">Select hello cloud service you created above for hello Split/Merge service.</span></span>
4. <span data-ttu-id="2f578-162">Tıklatın **sertifikaları** hello üst menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2f578-162">Click **Certificates** on hello top menu.</span></span>
5. <span data-ttu-id="2f578-163">Tıklatın **karşıya** hello alt çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="2f578-163">Click **Upload** in hello bottom bar.</span></span>
6. <span data-ttu-id="2f578-164">Merhaba PFX dosyasını seçin ve hello girin yukarıdaki aynı parola.</span><span class="sxs-lookup"><span data-stu-id="2f578-164">Select hello PFX file and enter hello same password as above.</span></span>
7. <span data-ttu-id="2f578-165">Tamamlandığında, hello sertifika parmak izi hello yeni giriş hello listesinde kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2f578-165">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

### <a name="update-hello-service-configuration-file"></a><span data-ttu-id="2f578-166">Merhaba hizmeti yapılandırma dosyasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="2f578-166">Update hello service configuration file</span></span>
<span data-ttu-id="2f578-167">Yukarıdaki hello parmak izi/value özniteliği bu ayarların kopyalanan hello sertifika parmak izi yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="2f578-167">Paste hello certificate thumbprint copied above into hello thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="2f578-168">Merhaba çalışan rolü için:</span><span class="sxs-lookup"><span data-stu-id="2f578-168">For hello worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="2f578-169">Merhaba web rolü için:</span><span class="sxs-lookup"><span data-stu-id="2f578-169">For hello web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="2f578-170">Lütfen sunucu sertifikası ve istemci sertifikaları Merhaba, üretim dağıtımları ayrı sertifika şifreleme için CA ' nın hello için kullanılması gereken dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2f578-170">Please note that for production deployments separate certificates should be used for hello CA, for encryption, hello Server certificate and client certificates.</span></span> <span data-ttu-id="2f578-171">Bu ayrıntılı yönergeler için bkz: [Güvenlik Yapılandırması](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="2f578-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="2f578-172">Hizmet dağıtma</span><span class="sxs-lookup"><span data-stu-id="2f578-172">Deploy your service</span></span>
1. <span data-ttu-id="2f578-173">Toohello Git [Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="2f578-173">Go toohello [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2f578-174">Merhaba tıklatın **bulut Hizmetleri** sekmesinde hello solda ve daha önce oluşturduğunuz hello bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="2f578-174">Click hello **Cloud Services** tab on hello left, and select hello cloud service that you created earlier.</span></span>
3. <span data-ttu-id="2f578-175">Tıklatın **Pano**.</span><span class="sxs-lookup"><span data-stu-id="2f578-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="2f578-176">Ortamı hazırlama hello seçin ve ardından **yeni bir hazırlama dağıtımı karşıya**.</span><span class="sxs-lookup"><span data-stu-id="2f578-176">Choose hello staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Hazırlama][3]
5. <span data-ttu-id="2f578-178">Merhaba iletişim kutusunda, bir dağıtım etiketini girin.</span><span class="sxs-lookup"><span data-stu-id="2f578-178">In hello dialog box, enter a deployment label.</span></span> <span data-ttu-id="2f578-179">'Paketi' ve 'Configuration' için 'Den yerel' tıklatın ve hello seçin **SplitMergeService.cspkg** dosyası ve daha önce yapılandırılmış .cscfg dosyanız.</span><span class="sxs-lookup"><span data-stu-id="2f578-179">For both 'Package' and 'Configuration', click 'From Local' and choose hello **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="2f578-180">Etiketli o hello onay kutusunu olun **bir veya daha fazla rol tek bir örnek içeriyorsa bile Dağıt** denetlenir.</span><span class="sxs-lookup"><span data-stu-id="2f578-180">Ensure that hello checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="2f578-181">Merhaba alt sağ toobegin hello dağıtımda Hello onay düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="2f578-181">Hit hello tick button in hello bottom right toobegin hello deployment.</span></span> <span data-ttu-id="2f578-182">Tootake beklediğiniz birkaç dakika toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2f578-182">Expect it tootake a few minutes toocomplete.</span></span>

   ![Karşıya Yükle][4]

## <a name="troubleshoot-hello-deployment"></a><span data-ttu-id="2f578-184">Merhaba dağıtım sorunlarını gider</span><span class="sxs-lookup"><span data-stu-id="2f578-184">Troubleshoot hello deployment</span></span>
<span data-ttu-id="2f578-185">Web rolünüz çevrimiçi toocome başarısız olursa, büyük olasılıkla hello güvenlik yapılandırması ile ilgili bir sorun olur.</span><span class="sxs-lookup"><span data-stu-id="2f578-185">If your web role fails toocome online, it is likely a problem with hello security configuration.</span></span> <span data-ttu-id="2f578-186">SSL yukarıda açıklandığı şekilde yapılandırıldığından bu hello denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2f578-186">Check that hello SSL is configured as described above.</span></span>

<span data-ttu-id="2f578-187">Çalışan rolü çevrimiçi toocome başarısız olur, ancak web rolünüz başarılı, büyük olasılıkla daha önce oluşturduğunuz toohello durum veritabanına bağlanırken bir sorun olur.</span><span class="sxs-lookup"><span data-stu-id="2f578-187">If your worker role fails toocome online, but your web role succeeds, it is most likely a problem connecting toohello status database that you created earlier.</span></span>

* <span data-ttu-id="2f578-188">Merhaba bağlantı dizesinde, .cscfg doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2f578-188">Make sure that hello connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="2f578-189">Merhaba sunucu ve veritabanı var olduğundan ve hello kullanıcı kimliği ve parola doğru olduğunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2f578-189">Check that hello server and database exist, and that hello user id and password are correct.</span></span>
* <span data-ttu-id="2f578-190">Azure SQL DB için hello bağlantı dizesi hello biçiminde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="2f578-190">For Azure SQL DB, hello connection string should be of hello form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="2f578-191">Bu hello sunucu adı ile başlayan değil olun **https://**.</span><span class="sxs-lookup"><span data-stu-id="2f578-191">Ensure that hello server name does not begin with **https://**.</span></span>
* <span data-ttu-id="2f578-192">Azure SQL DB sunucunuz Azure Hizmetleri tooconnect tooit verdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2f578-192">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="2f578-193">toodo Bu, https://manage.windowsazure.com açın, "SQL veritabanlarını" Merhaba üzerinde sol tıklayın, "" Merhaba üstünde sunucular ve sunucunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="2f578-193">toodo this, open https://manage.windowsazure.com, click “SQL Databases” on hello left, click “Servers” at hello top, and select your server.</span></span> <span data-ttu-id="2f578-194">Tıklatın **Yapılandır** hello en üst ve o hello olun **Azure Hizmetleri** ayar çok "Evet".</span><span class="sxs-lookup"><span data-stu-id="2f578-194">Click **Configure** at hello top and ensure that hello **Azure Services** setting is set too“Yes”.</span></span> <span data-ttu-id="2f578-195">(Merhaba önkoşullara bakın, bu makalenin hello üst kısmına).</span><span class="sxs-lookup"><span data-stu-id="2f578-195">(See hello Prerequisites section at hello top of this article).</span></span>

## <a name="test-hello-service-deployment"></a><span data-ttu-id="2f578-196">Merhaba hizmet dağıtımı test etme</span><span class="sxs-lookup"><span data-stu-id="2f578-196">Test hello service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="2f578-197">Bir web tarayıcısı ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="2f578-197">Connect with a web browser</span></span>
<span data-ttu-id="2f578-198">Bölünmüş birleştirme hizmetinizin Hello web uç noktası belirleyin.</span><span class="sxs-lookup"><span data-stu-id="2f578-198">Determine hello web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="2f578-199">Bu hello Klasik Azure portalı giderek toohello tarafından bulabilirsiniz **Pano** , bulut hizmeti ve altında arayan **Site URL'si** hello sağ tarafında.</span><span class="sxs-lookup"><span data-stu-id="2f578-199">You can find this in hello Azure Classic Portal by going toohello **Dashboard** of your cloud service and looking under **Site URL** on hello right side.</span></span> <span data-ttu-id="2f578-200">Değiştir **http://** ile **https://** hello varsayılan güvenlik ayarlarını hello HTTP uç noktası devre dışı olduğundan.</span><span class="sxs-lookup"><span data-stu-id="2f578-200">Replace **http://** with **https://** since hello default security settings disable hello HTTP endpoint.</span></span> <span data-ttu-id="2f578-201">Başlangıç sayfası, bu URL için tarayıcınıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f578-201">Load hello page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="2f578-202">PowerShell komut dosyalarıyla test</span><span class="sxs-lookup"><span data-stu-id="2f578-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="2f578-203">Merhaba dağıtım ve ortamınıza dahil hello örnek PowerShell komut dosyaları çalıştırarak test edilebilir.</span><span class="sxs-lookup"><span data-stu-id="2f578-203">hello deployment and your environment can be tested by running hello included sample PowerShell scripts.</span></span>

<span data-ttu-id="2f578-204">Merhaba komut dosyaları dahil şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2f578-204">hello script files included are:</span></span>

1. <span data-ttu-id="2f578-205">**SetupSampleSplitMergeEnvironment.ps1** -bölünmüş/birleştirme için bir test veri katmanını ayarlar (ayrıntılı bir açıklaması için aşağıdaki tabloya bakın)</span><span class="sxs-lookup"><span data-stu-id="2f578-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="2f578-206">**ExecuteSampleSplitMerge.ps1** -hello testi test işlemlerini yürüten veri katmanı (ayrıntılı bir açıklaması için aşağıdaki tabloya bakın)</span><span class="sxs-lookup"><span data-stu-id="2f578-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on hello test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="2f578-207">**GetMappings.ps1** - üst düzey örnek hello geçerli durumunu hello parça eşlemeleri yazdırır komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="2f578-207">**GetMappings.ps1** - top-level sample script that prints out hello current state of hello shard mappings.</span></span>
4. <span data-ttu-id="2f578-208">**ShardManagement.psm1** -sarmalar Yardımcısı betik hello ShardManagement API</span><span class="sxs-lookup"><span data-stu-id="2f578-208">**ShardManagement.psm1**  - helper script that wraps hello ShardManagement API</span></span>
5. <span data-ttu-id="2f578-209">**SqlDatabaseHelpers.psm1** -Yardımcısı betik oluşturma ve SQL veritabanlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="2f578-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="2f578-210">PowerShell dosyası</span><span class="sxs-lookup"><span data-stu-id="2f578-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="2f578-211">Adımlar</span><span class="sxs-lookup"><span data-stu-id="2f578-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="2f578-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="2f578-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="2f578-213">Bir parça eşleme Yöneticisi veritabanı oluşturur</span><span class="sxs-lookup"><span data-stu-id="2f578-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="2f578-214">2 parça veritabanları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2f578-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="2f578-215">Bu veritabanı (varolan bir parça bu veritabanlarını eşlemeleri siler) için bir parça eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2f578-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="2f578-216">Her iki hello parça küçük örnek bir tablo oluşturur ve hello parça hello tabloda doldurur.</span><span class="sxs-lookup"><span data-stu-id="2f578-216">Creates a small sample table in both hello shards, and populates hello table in one of hello shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="2f578-217">Merhaba SchemaInfo hello parçalı tablo için bildirir.</span><span class="sxs-lookup"><span data-stu-id="2f578-217">Declares hello SchemaInfo for hello sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="2f578-218">PowerShell dosyası</span><span class="sxs-lookup"><span data-stu-id="2f578-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="2f578-219">Adımlar</span><span class="sxs-lookup"><span data-stu-id="2f578-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="2f578-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="2f578-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="2f578-221">Hangi hello ilk parça toohello ikinci parça yarım hello verilerinden ayırır bir bölme isteği toohello bölünmüş birleştirme hizmetine web ön uç, gönderir.</span><span class="sxs-lookup"><span data-stu-id="2f578-221">Sends a split request toohello Split-Merge Service web frontend, which splits half hello data from hello first shard toohello second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="2f578-222">Yoklamalar web ön uç hello istek tamamlanana kadar bölme istek durumunu ve bekler hello için hello.</span><span class="sxs-lookup"><span data-stu-id="2f578-222">Polls hello web frontend for hello split request status and waits until hello request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="2f578-223">Hangi hello ikinci parça geri toohello ilk parça hello verileri taşır bir birleştirme isteği toohello bölünmüş birleştirme hizmetine web ön uç, gönderir.</span><span class="sxs-lookup"><span data-stu-id="2f578-223">Sends a merge request toohello Split-Merge Service web frontend, which moves hello data from hello second shard back toohello first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="2f578-224">Anketler hello web ön hello birleştirme isteği durumu ve hello istek tamamlanana kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="2f578-224">Polls hello web frontend for hello merge request status and waits until hello request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a><span data-ttu-id="2f578-225">Dağıtımınızı PowerShell tooverify kullanın</span><span class="sxs-lookup"><span data-stu-id="2f578-225">Use PowerShell tooverify your deployment</span></span>
1. <span data-ttu-id="2f578-226">Yeni bir PowerShell penceresi açın ve hello bölünmüş birleştirme paketi indirdiğiniz toohello dizinine gidin ve ardından hello "powershell" dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="2f578-226">Open a new PowerShell window and navigate toohello directory where you downloaded hello Split-Merge package, and then navigate into hello “powershell” directory.</span></span>
2. <span data-ttu-id="2f578-227">Bir Azure SQL database sunucusu oluşturun (veya var olan bir sunucu seçin) burada hello parça eşleme Yöneticisi ve parça oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2f578-227">Create an Azure SQL database server (or choose an existing server) where hello shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2f578-228">Merhaba SetupSampleSplitMergeEnvironment.ps1 komut dosyası oluşturur bu veritabanları üzerinde hello aynı sunucu varsayılan tookeep hello betik basit tarafından.</span><span class="sxs-lookup"><span data-stu-id="2f578-228">hello SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on hello same server by default tookeep hello script simple.</span></span> <span data-ttu-id="2f578-229">Bu bir kısıtlaması hello bölünmüş birleştirme hizmetine kendisini değil.</span><span class="sxs-lookup"><span data-stu-id="2f578-229">This is not a restriction of hello Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="2f578-230">SQL kimlik doğrulaması oturum açma ile okuma/yazma erişimi toohello DBs hello bölünmüş birleştirme hizmet toomove verileri ve güncelleştirme hello parça eşleme için gerekli.</span><span class="sxs-lookup"><span data-stu-id="2f578-230">A SQL authentication login with read/write access toohello DBs will be needed for hello Split-Merge service toomove data and update hello shard map.</span></span> <span data-ttu-id="2f578-231">Merhaba bölünmüş birleştirme hizmetine hello bulutta çalışan olduğundan, tümleşik kimlik doğrulaması şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="2f578-231">Since hello Split-Merge Service runs in hello cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="2f578-232">Hello Azure SQL server yapılandırıldığından emin olun, bu komut dosyası çalıştırarak hello makinenin hello IP adresinden tooallow erişim.</span><span class="sxs-lookup"><span data-stu-id="2f578-232">Make sure hello Azure SQL server is configured tooallow access from hello IP address of hello machine running these scripts.</span></span> <span data-ttu-id="2f578-233">Bu ayar hello Azure SQL sunucusu altında bulabilirsiniz / configuration / izin verilen IP adreslerini.</span><span class="sxs-lookup"><span data-stu-id="2f578-233">You can find this setting under hello Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="2f578-234">Merhaba SetupSampleSplitMergeEnvironment.ps1 komut dosyası toocreate hello örnek ortamı yürütün.</span><span class="sxs-lookup"><span data-stu-id="2f578-234">Execute hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello sample environment.</span></span>
   
   <span data-ttu-id="2f578-235">Bu komut dosyasını çalıştıran var olan tüm parça eşleme yönetim verilerini hello parça eşleme manager veritabanı ve hello parça yapıları temizleyin.</span><span class="sxs-lookup"><span data-stu-id="2f578-235">Running this script will wipe out any existing shard map management data structures on hello shard map manager database and hello shards.</span></span> <span data-ttu-id="2f578-236">Toore başlatma hello parça harita veya parça istiyorsanız yararlı toorerun hello komut dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f578-236">It may be useful toorerun hello script if you wish toore-initialize hello shard map or shards.</span></span>
   
   <span data-ttu-id="2f578-237">Örnek komut satırı:</span><span class="sxs-lookup"><span data-stu-id="2f578-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="2f578-238">Şu anda mevcut hello Getmappings.ps1 komut dosyası tooview hello eşlemelerini hello örnek ortamında yürütün.</span><span class="sxs-lookup"><span data-stu-id="2f578-238">Execute hello Getmappings.ps1 script tooview hello mappings that currently exist in hello sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="2f578-239">Merhaba ExecuteSampleSplitMerge.ps1 betik tooexecute (Merhaba ilk parça toohello ikinci parça üzerinde yarı hello veri taşıma) bir bölme işlemi'i ve ardından (Merhaba verileri hello ilk parça geri taşıma) bir birleştirme işlemi yürütün.</span><span class="sxs-lookup"><span data-stu-id="2f578-239">Execute hello ExecuteSampleSplitMerge.ps1 script tooexecute a split operation (moving half hello data on hello first shard toohello second shard) and then a merge operation (moving hello data back onto hello first shard).</span></span> <span data-ttu-id="2f578-240">SSL ve sol hello http uç noktası devre dışı yapılandırdıysanız, hello https:// uç noktası yerine kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2f578-240">If you configured SSL and left hello http endpoint disabled, ensure that you use hello https:// endpoint instead.</span></span>
   
   <span data-ttu-id="2f578-241">Örnek komut satırı:</span><span class="sxs-lookup"><span data-stu-id="2f578-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="2f578-242">Hello aşağıda hata alırsanız, büyük olasılıkla Web uç noktanın sertifikayla ilgili bir sorun olduğunu.</span><span class="sxs-lookup"><span data-stu-id="2f578-242">If you receive hello below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="2f578-243">Sık kullanılan Web tarayıcınızda toohello Web uç noktası bağlanmayı deneyin ve bir sertifika hatası olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2f578-243">Try connecting toohello Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="2f578-244">Bu başarılı olursa hello çıktı hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="2f578-244">If it succeeded, hello output should look like hello below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="2f578-245">Diğer veri türleri ile deneyin!</span><span class="sxs-lookup"><span data-stu-id="2f578-245">Experiment with other data types!</span></span> <span data-ttu-id="2f578-246">Bu komut dosyalarının tümü toospecify hello anahtar türü sağlayan isteğe bağlı - ShardKeyType parametresi alın.</span><span class="sxs-lookup"><span data-stu-id="2f578-246">All of these scripts take an optional -ShardKeyType parameter that allows you toospecify hello key type.</span></span> <span data-ttu-id="2f578-247">Int32 Hello varsayılandır ancak Int64, GUID ya da ikili de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f578-247">hello default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="2f578-248">Oluşturma istekleri</span><span class="sxs-lookup"><span data-stu-id="2f578-248">Create requests</span></span>
<span data-ttu-id="2f578-249">Merhaba hizmet hello web kullanıcı arabirimini kullanarak veya içeri aktarma ve isteklerinizi hello web rolü aracılığıyla göndereceğini hello SplitMerge.psm1 PowerShell modülünü kullanarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2f578-249">hello service can be used either by using hello web UI or by importing and using hello SplitMerge.psm1 PowerShell module which will submit your requests through hello web role.</span></span>

<span data-ttu-id="2f578-250">Merhaba hizmet parçalı tablolar ve başvuru tabloları veri taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f578-250">hello service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="2f578-251">Parçalı tablo parçalama anahtar sütunu ve her parça üzerinde farklı satır veri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2f578-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="2f578-252">Bir başvuru tablosu parçalı değil hello içerecek şekilde aynı veri üzerinde her parça satır.</span><span class="sxs-lookup"><span data-stu-id="2f578-252">A reference table is not sharded so it contains hello same row data on every shard.</span></span> <span data-ttu-id="2f578-253">Başvuru tabloları genellikle değiştirmez ve sorgularda parçalı tablolar ile kullanılan tooJOIN olan veriler için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="2f578-253">Reference tables are useful for data that does not change often and is used tooJOIN with sharded tables in queries.</span></span>

<span data-ttu-id="2f578-254">Sipariş tooperform bölünmüş birleştirme işlemi, hello parçalı tablolar ve taşınmış toohave istediğiniz başvuru tabloları bildirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f578-254">In order tooperform a split-merge operation, you must declare hello sharded tables and reference tables that you want toohave moved.</span></span> <span data-ttu-id="2f578-255">Bu hello ile gerçekleştirilir **SchemaInfo** API.</span><span class="sxs-lookup"><span data-stu-id="2f578-255">This is accomplished with hello **SchemaInfo** API.</span></span> <span data-ttu-id="2f578-256">Bu API hello olan **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** ad alanı.</span><span class="sxs-lookup"><span data-stu-id="2f578-256">This API is in hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="2f578-257">Her parçalı tablo için oluşturun bir **ShardedTableInfo** Merhaba tablonun üst şema adını tanımlayan nesne (isteğe bağlı, çok varsayılan olarak "dbo"), hello tablo adı ve hello hello parçalama anahtarı içeren bu tablodaki sütun adı.</span><span class="sxs-lookup"><span data-stu-id="2f578-257">For each sharded table, create a **ShardedTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”), hello table name, and hello column name in that table that contains hello sharding key.</span></span>
2. <span data-ttu-id="2f578-258">Her başvuru tablosu için bir **ReferenceTableInfo** Merhaba tablonun üst şema adını tanımlayan nesne (isteğe bağlı, çok varsayılan olarak "dbo") ve hello tablo adı.</span><span class="sxs-lookup"><span data-stu-id="2f578-258">For each reference table, create a **ReferenceTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”) and hello table name.</span></span>
3. <span data-ttu-id="2f578-259">Merhaba TableInfo nesneleri tooa yeni yukarıda eklemek **SchemaInfo** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="2f578-259">Add hello above TableInfo objects tooa new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="2f578-260">Bir başvuru tooa almak **ShardMapManager** nesne ve çağrı **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="2f578-260">Get a reference tooa **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="2f578-261">Merhaba eklemek **SchemaInfo** toohello **SchemaInfoCollection**, hello parça eşleme adı sağlama.</span><span class="sxs-lookup"><span data-stu-id="2f578-261">Add hello **SchemaInfo** toohello **SchemaInfoCollection**, providing hello shard map name.</span></span>

<span data-ttu-id="2f578-262">Bunun bir örneğini hello SetupSampleSplitMergeEnvironment.ps1 betik görülebilir.</span><span class="sxs-lookup"><span data-stu-id="2f578-262">An example of this can be seen in hello SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="2f578-263">Merhaba bölünmüş birleştirme hizmetine hello hedef veritabanı (veya hello veritabanındaki herhangi bir tablo için şema), oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="2f578-263">hello Split-Merge service does not create hello target database (or schema for any tables in hello database) for you.</span></span> <span data-ttu-id="2f578-264">Bir istek toohello hizmet göndermeden önce önceden oluşturulmuş olmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f578-264">They must be pre-created before sending a request toohello service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2f578-265">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="2f578-265">Troubleshooting</span></span>
<span data-ttu-id="2f578-266">Merhaba örnek powershell komut dosyaları çalıştırırken hello ileti aşağıda görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2f578-266">You may see hello below message when running hello sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

<span data-ttu-id="2f578-267">Bu hata, SSL sertifikası doğru yapılandırılmamış anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2f578-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="2f578-268">Lütfen 'Bağlanıyor bir web tarayıcısı' bölümündeki hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="2f578-268">Please follow hello instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="2f578-269">İstek gönderemez varsa bu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2f578-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="2f578-270">Bu durumda, belirli hello ayarı için yapılandırma dosyanızı denetleyin **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="2f578-270">In this case, check your configuration file, in particular hello setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="2f578-271">Bu hata genellikle o hello çalışan rolü hello meta veri veritabanı ilk kullanımda başarıyla başlatılamadı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2f578-271">This error typically indicates that hello worker role could not successfully initialize hello metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png


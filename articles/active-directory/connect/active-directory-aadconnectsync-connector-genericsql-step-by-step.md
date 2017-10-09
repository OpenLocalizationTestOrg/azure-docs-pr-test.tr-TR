---
title: "aaaGeneric SQL bağlayıcı adım adım | Microsoft Docs"
description: "Bu makalede, taramasını basit bir ik sistemi genel SQL bağlayıcı hello adım adım kullanma."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="d6cf7-103">Adım adım Genel SQL Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="d6cf7-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="d6cf7-104">Bu konu hakkında adım adım bir kılavuzdur.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="d6cf7-105">Bir Basit örnek HR veritabanı oluşturur ve bazı kullanıcı ve grup üyeliklerini içeri aktarmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-hello-sample-database"></a><span data-ttu-id="d6cf7-106">Merhaba örnek veritabanını hazırlama</span><span class="sxs-lookup"><span data-stu-id="d6cf7-106">Prepare hello sample database</span></span>
<span data-ttu-id="d6cf7-107">SQL Server çalıştıran bir sunucuda bulunan hello SQL betiği çalıştırma [ek A](#appendix-a). Bu komut dosyası GSQLDEMO hello adla örnek bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-107">On a server running SQL Server, run hello SQL script found in [Appendix A](#appendix-a). This script creates a sample database with hello name GSQLDEMO.</span></span> <span data-ttu-id="d6cf7-108">Merhaba hello için nesne modeli bu resimdeki veritabanı görülüyor oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="d6cf7-108">hello object model for hello created database looks like this picture:</span></span>  
<span data-ttu-id="d6cf7-109">![Nesne modeli](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="d6cf7-110">Ayrıca toouse tooconnect toohello veritabanı istediğiniz bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-110">Also create a user you want toouse tooconnect toohello database.</span></span> <span data-ttu-id="d6cf7-111">Bu kılavuzda, hello kullanıcı FABRIKAM\SQLUser çağrılır ve hello etki alanında bulunan.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-111">In this walkthrough, hello user is called FABRIKAM\SQLUser and located in hello domain.</span></span>

## <a name="create-hello-odbc-connection-file"></a><span data-ttu-id="d6cf7-112">Merhaba ODBC bağlantı dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6cf7-112">Create hello ODBC connection file</span></span>
<span data-ttu-id="d6cf7-113">Merhaba Genel SQL bağlayıcı ODBC tooconnect toohello uzak sunucu kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-113">hello Generic SQL Connector is using ODBC tooconnect toohello remote server.</span></span> <span data-ttu-id="d6cf7-114">İlk toocreate hello ODBC bağlantı bilgilerini dosyasıyla gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-114">First we need toocreate a file with hello ODBC connection information.</span></span>

1. <span data-ttu-id="d6cf7-115">Merhaba ODBC Yönetimi yardımcı programı, sunucunuzda başlatın:</span><span class="sxs-lookup"><span data-stu-id="d6cf7-115">Start hello ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="d6cf7-117">Select hello sekmesini **dosya DSN**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-117">Select hello tab **File DSN**.</span></span> <span data-ttu-id="d6cf7-118">Tıklatın **Ekle...** .</span><span class="sxs-lookup"><span data-stu-id="d6cf7-118">Click **Add...**.</span></span>  
   <span data-ttu-id="d6cf7-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="d6cf7-120">Merhaba out-of-box sürücü works ince, bu nedenle seçin ve **sonraki >**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-120">hello out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="d6cf7-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="d6cf7-122">Merhaba dosyası gibi bir ad verin **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-122">Give hello file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="d6cf7-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="d6cf7-124">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-124">Click **Finish**.</span></span>  
   <span data-ttu-id="d6cf7-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="d6cf7-126">Zamanı tooconfigure hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-126">Time tooconfigure hello connection.</span></span> <span data-ttu-id="d6cf7-127">Merhaba veri kaynağı iyi bir açıklama girin ve SQL Server çalıştıran hello sunucu hello adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-127">Give hello data source a good description and provide hello name of hello server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="d6cf7-129">Select nasıl tooauthenticate SQL ile.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-129">Select how tooauthenticate with SQL.</span></span> <span data-ttu-id="d6cf7-130">Bu durumda, Windows kimlik doğrulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="d6cf7-132">Merhaba hello örnek veritabanı adını sağlayın **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-132">Provide hello name of hello sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="d6cf7-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="d6cf7-134">Bu ekranda her şeyi varsayılan devam eder.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-134">Keep everything default on this screen.</span></span> <span data-ttu-id="d6cf7-135">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-135">Click **Finish**.</span></span>  
   <span data-ttu-id="d6cf7-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="d6cf7-137">her şeyi çalıştığını beklendiği gibi tooverify tıklatın **Test veri kaynağı**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-137">tooverify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="d6cf7-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="d6cf7-139">Merhaba test başarılı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-139">Make sure hello test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="d6cf7-141">Merhaba ODBC yapılandırma dosyası artık dosya DSN görünür olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-141">hello ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="d6cf7-143">Şimdi gerekir ve hello bağlayıcı oluşturmaya başlamadan hello dosya sahibiz.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-143">We now have hello file we need and can start creating hello Connector.</span></span>

## <a name="create-hello-generic-sql-connector"></a><span data-ttu-id="d6cf7-144">Merhaba Genel SQL bağlayıcısı oluşturun</span><span class="sxs-lookup"><span data-stu-id="d6cf7-144">Create hello Generic SQL Connector</span></span>
1. <span data-ttu-id="d6cf7-145">Hello Eşitleme Hizmeti Yöneticisi kullanıcı Arabirimi, seçin **Bağlayıcılar** ve **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-145">In hello Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="d6cf7-146">Seçin **Genel SQL (Microsoft)** ve açıklayıcı bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="d6cf7-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="d6cf7-148">Merhaba önceki bölümde oluşturduğunuz hello DSN dosyası bulunamıyor ve toohello server yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-148">Find hello DSN file you created in hello previous section and upload it toohello server.</span></span> <span data-ttu-id="d6cf7-149">Merhaba kimlik bilgileri tooconnect toohello veritabanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-149">Provide hello credentials tooconnect toohello database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="d6cf7-151">Bu kılavuzda, biz bize kolaylaşır ve iki nesne türlerini olduğunu söylemek **kullanıcı** ve **grup**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="d6cf7-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="d6cf7-153">toofind hello öznitelikleri hello tablosuna kendisini bakarak özniteliklerle bağlayıcı toodetect hello istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-153">toofind hello attributes, we want hello Connector toodetect those attributes by looking at hello table itself.</span></span> <span data-ttu-id="d6cf7-154">Bu yana **kullanıcılar** ayrılmış bir sözcük içinde köşeli ayraçlar [] tooprovide ihtiyacımız SQL'de.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-154">Since **Users** is a reserved word in SQL, we need tooprovide it in square brackets [ ].</span></span>  
   <span data-ttu-id="d6cf7-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="d6cf7-156">Zaman toodefine hello bağlantı özniteliği ve hello DN özniteliği.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-156">Time toodefine hello anchor attribute and hello DN attribute.</span></span> <span data-ttu-id="d6cf7-157">İçin **kullanıcılar**, hello birleşimi hello iki öznitelikleri kullanıcı adı ve EmployeeID kullanırız.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-157">For **Users**, we use hello combination of hello two attributes username and EmployeeID.</span></span> <span data-ttu-id="d6cf7-158">İçin **grup**, GroupName kullanıyoruz (değil gerçekçi gerçekçi, ancak bu kılavuz çalışır).</span><span class="sxs-lookup"><span data-stu-id="d6cf7-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="d6cf7-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="d6cf7-160">Tüm öznitelik türlerini, bir SQL veritabanında algılanabilir.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="d6cf7-161">Merhaba başvuru öznitelik türü özellikle yapılamıyor.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-161">hello reference attribute type in particular cannot.</span></span> <span data-ttu-id="d6cf7-162">Merhaba grup nesne türü için toochange hello OwnerId ve Memberıd tooreference gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-162">For hello group object type, we need toochange hello OwnerID and MemberID tooreference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="d6cf7-164">başvuru özniteliği hello önceki adımda hello nesne türü bir başvuru bu değerleri gerektiği hello öznitelikleri seçtik.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-164">hello attributes we selected as reference attributes in hello previous step require hello object type these values are a reference to.</span></span> <span data-ttu-id="d6cf7-165">Örneğimizde, kullanıcı nesnesi türü hello.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-165">In our case, hello User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="d6cf7-167">Merhaba genel parametreleri sayfasında seçin **Filigran** hello delta stratejisi olarak.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-167">On hello Global Parameters page, select **Watermark** as hello delta strategy.</span></span> <span data-ttu-id="d6cf7-168">Ayrıca hello tarih/saat biçiminde yazın **yyyy-aa-gg ss: dd:**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-168">Also type in hello date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="d6cf7-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="d6cf7-170">Merhaba üzerinde **yapılandırma bölümleri ve hiyerarşileri** sayfasında, her iki nesne türlerini seçin.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-170">On hello **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="d6cf7-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="d6cf7-172">Merhaba üzerinde **nesne türlerini Seç** ve **öznitelikleri Seç**, nesne türleri ve tüm öznitelikleri seçin.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-172">On hello **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="d6cf7-173">Merhaba üzerinde **yapılandırma bağlayıcılarını** sayfasında, **son**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-173">On hello **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="d6cf7-174">Çalıştırma profillerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6cf7-174">Create Run Profiles</span></span>
1. <span data-ttu-id="d6cf7-175">Hello Eşitleme Hizmeti Yöneticisi kullanıcı Arabirimi, seçin **Bağlayıcılar**, ve **çalıştırma profillerini Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-175">In hello Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="d6cf7-176">Tıklatın **yeni bir profil**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-176">Click **New Profile**.</span></span> <span data-ttu-id="d6cf7-177">Biz başlayın **tam içeri aktarma**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="d6cf7-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="d6cf7-179">Merhaba türünü seçin **tam içeri aktarma (yalnızca aşama)**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-179">Select hello type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="d6cf7-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="d6cf7-181">Merhaba bölümü seçin **nesne = kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-181">Select hello partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="d6cf7-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="d6cf7-183">Seçin **tablo** ve türü **[kullanıcılar]**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="d6cf7-184">Toohello birden çok değerli nesne türü bölümüne kaydırın ve resim aşağıdaki hello olduğu gibi hello veri girin.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-184">Scroll down toohello multi-valued object type section and enter hello data as in hello following picture.</span></span> <span data-ttu-id="d6cf7-185">Seçin **son** toosave hello adım.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-185">Select **Finish** toosave hello step.</span></span>  
   <span data-ttu-id="d6cf7-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="d6cf7-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="d6cf7-188">Seçin **yeni adım**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-188">Select **New Step**.</span></span> <span data-ttu-id="d6cf7-189">Bu süre, select **nesne grubu =**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="d6cf7-190">Merhaba son sayfasında, resim aşağıdaki hello olduğu gibi hello yapılandırmasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-190">On hello last page, use hello configuration as in hello following picture.</span></span> <span data-ttu-id="d6cf7-191">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-191">Click **Finish**.</span></span>  
   <span data-ttu-id="d6cf7-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="d6cf7-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="d6cf7-194">İsteğe bağlı: istiyorsanız, ek çalıştırma profillerini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="d6cf7-195">Bu kılavuzda, yalnızca tam içeri aktarma hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-195">For this walkthrough, only hello Full Import is used.</span></span>
7. <span data-ttu-id="d6cf7-196">Tıklatın **Tamam** değiştirme toofinish farklı çalıştır profili.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-196">Click **OK** toofinish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-hello-import"></a><span data-ttu-id="d6cf7-197">Bazı test verilerini ve test hello alma ekleme</span><span class="sxs-lookup"><span data-stu-id="d6cf7-197">Add some test data and test hello import</span></span>
<span data-ttu-id="d6cf7-198">Örnek veritabanınızdaki bazı test verilerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="d6cf7-199">Hazır olduğunuzda seçin **çalıştırmak** ve **tam alma**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="d6cf7-200">İşte, iki telefon numarası olan bir kullanıcı ve Grup bazı üyeleri ile.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![CS2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="d6cf7-203">Ek A</span><span class="sxs-lookup"><span data-stu-id="d6cf7-203">Appendix A</span></span>
<span data-ttu-id="d6cf7-204">**SQL komut dosyası toocreate hello örnek veritabanı**</span><span class="sxs-lookup"><span data-stu-id="d6cf7-204">**SQL script toocreate hello sample database**</span></span>

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```

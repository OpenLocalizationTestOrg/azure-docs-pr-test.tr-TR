---
title: "Genel SQL bağlayıcı adım adım | Microsoft Docs"
description: "Bu makalede bir basit ik sistemi genel SQL Bağlayıcısı'nı kullanarak adım adım taramasını değil."
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
ms.openlocfilehash: 3fdc1b405b95180d031aa4ad45b406f7fc149d8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="cc1a6-103">Adım adım Genel SQL Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="cc1a6-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="cc1a6-104">Bu konu hakkında adım adım bir kılavuzdur.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="cc1a6-105">Bir Basit örnek HR veritabanı oluşturur ve bazı kullanıcı ve grup üyeliklerini içeri aktarmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-the-sample-database"></a><span data-ttu-id="cc1a6-106">Örnek veritabanını hazırlama</span><span class="sxs-lookup"><span data-stu-id="cc1a6-106">Prepare the sample database</span></span>
<span data-ttu-id="cc1a6-107">İçinde SQL komut dosyasını çalıştırın, SQL Server çalıştıran bir sunucuda bulunan [ek A](#appendix-a). Bu komut dosyası GSQLDEMO adı ile örnek bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span></span> <span data-ttu-id="cc1a6-108">Oluşturulan veritabanı için nesne modeli Bu resim gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="cc1a6-108">The object model for the created database looks like this picture:</span></span>  
<span data-ttu-id="cc1a6-109">![Nesne modeli](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="cc1a6-110">Ayrıca veritabanına bağlanmak için kullanmak istediğiniz bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-110">Also create a user you want to use to connect to the database.</span></span> <span data-ttu-id="cc1a6-111">Bu kılavuzda, kullanıcı FABRIKAM\SQLUser çağrılır ve etki alanında bulunan.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span></span>

## <a name="create-the-odbc-connection-file"></a><span data-ttu-id="cc1a6-112">ODBC bağlantı dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc1a6-112">Create the ODBC connection file</span></span>
<span data-ttu-id="cc1a6-113">Genel SQL bağlayıcı uzak sunucuya bağlanmak için ODBC kullanma.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span></span> <span data-ttu-id="cc1a6-114">İlk olarak kimliğinizi ODBC bağlantı bilgilerini bir dosya oluşturmak gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-114">First we need to create a file with the ODBC connection information.</span></span>

1. <span data-ttu-id="cc1a6-115">ODBC Yönetimi yardımcı programı, sunucunuzda başlatın:</span><span class="sxs-lookup"><span data-stu-id="cc1a6-115">Start the ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="cc1a6-117">Sekmeyi seçin **dosya DSN**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-117">Select the tab **File DSN**.</span></span> <span data-ttu-id="cc1a6-118">Tıklatın **Ekle...** .</span><span class="sxs-lookup"><span data-stu-id="cc1a6-118">Click **Add...**.</span></span>  
   <span data-ttu-id="cc1a6-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="cc1a6-120">Out-of-box sürücü works ince, bu nedenle seçin ve **sonraki >**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-120">The out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="cc1a6-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="cc1a6-122">Dosyaya gibi bir ad verin **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-122">Give the file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="cc1a6-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="cc1a6-124">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-124">Click **Finish**.</span></span>  
   <span data-ttu-id="cc1a6-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="cc1a6-126">Bağlantıyı yapılandırmak için süre.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-126">Time to configure the connection.</span></span> <span data-ttu-id="cc1a6-127">Veri kaynağı iyi bir açıklama girin ve SQL Server çalıştıran sunucunun adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-127">Give the data source a good description and provide the name of the server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="cc1a6-129">SQL ile kimlik doğrulaması yapmayı seçin.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-129">Select how to authenticate with SQL.</span></span> <span data-ttu-id="cc1a6-130">Bu durumda, Windows kimlik doğrulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="cc1a6-132">Örnek veritabanı adını sağlayın **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-132">Provide the name of the sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="cc1a6-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="cc1a6-134">Bu ekranda her şeyi varsayılan devam eder.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-134">Keep everything default on this screen.</span></span> <span data-ttu-id="cc1a6-135">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-135">Click **Finish**.</span></span>  
   <span data-ttu-id="cc1a6-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="cc1a6-137">Her şeyi çalıştığını beklendiği gibi doğrulamak için tıklatın **Test veri kaynağı**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-137">To verify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="cc1a6-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="cc1a6-139">Test başarılı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-139">Make sure the test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="cc1a6-141">ODBC yapılandırma dosyası artık dosya DSN görünür olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-141">The ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="cc1a6-143">Dosyanın gerekir ve bağlayıcı oluşturmaya başlamak şimdi sahibiz.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-143">We now have the file we need and can start creating the Connector.</span></span>

## <a name="create-the-generic-sql-connector"></a><span data-ttu-id="cc1a6-144">Genel SQL bağlayıcısı oluşturun</span><span class="sxs-lookup"><span data-stu-id="cc1a6-144">Create the Generic SQL Connector</span></span>
1. <span data-ttu-id="cc1a6-145">Eşitleme Hizmeti Yöneticisi Arabiriminde seçin **Bağlayıcılar** ve **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="cc1a6-146">Seçin **Genel SQL (Microsoft)** ve açıklayıcı bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="cc1a6-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="cc1a6-148">Önceki bölümde oluşturduğunuz DSN dosyasını bulun ve sunucuya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-148">Find the DSN file you created in the previous section and upload it to the server.</span></span> <span data-ttu-id="cc1a6-149">Veritabanına bağlanmak için kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-149">Provide the credentials to connect to the database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="cc1a6-151">Bu kılavuzda, biz bize kolaylaşır ve iki nesne türlerini olduğunu söylemek **kullanıcı** ve **grup**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="cc1a6-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="cc1a6-153">Öznitelikleri bulmak amacıyla tablosuna kendisini bakarak özniteliklerle algılamak için bağlayıcı istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span></span> <span data-ttu-id="cc1a6-154">Bu yana **kullanıcılar** ayrılmış bir sözcük içinde köşeli ayraçlar [] bunu sağlamak ihtiyacımız SQL'de.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span></span>  
   <span data-ttu-id="cc1a6-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="cc1a6-156">Bağlayıcı öznitelik ve DN özniteliği tanımlamak için süre.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-156">Time to define the anchor attribute and the DN attribute.</span></span> <span data-ttu-id="cc1a6-157">İçin **kullanıcılar**, iki öznitelik kullanıcı adı ve EmployeeID birleşimi kullanırız.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span></span> <span data-ttu-id="cc1a6-158">İçin **grup**, GroupName kullanıyoruz (değil gerçekçi gerçekçi, ancak bu kılavuz çalışır).</span><span class="sxs-lookup"><span data-stu-id="cc1a6-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="cc1a6-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="cc1a6-160">Tüm öznitelik türlerini, bir SQL veritabanında algılanabilir.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="cc1a6-161">Başvuru özniteliği türü özellikle yapılamıyor.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-161">The reference attribute type in particular cannot.</span></span> <span data-ttu-id="cc1a6-162">Grup nesnesi türü için biz OwnerId ve Memberıd başvurmak için değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="cc1a6-164">Başvuru özniteliği önceki adımda nesne türü gerektiği seçtik bu değerleri başvuru öznitelikleridir.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span></span> <span data-ttu-id="cc1a6-165">Örneğimizde, kullanıcı nesnesi yazın.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-165">In our case, the User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="cc1a6-167">Genel Parametreler sayfasında seçin **Filigran** delta stratejisi olarak.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span></span> <span data-ttu-id="cc1a6-168">Ayrıca tarih/saat biçiminde yazın **yyyy-aa-gg ss: dd:**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="cc1a6-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="cc1a6-170">Üzerinde **yapılandırma bölümleri ve hiyerarşileri** sayfasında, her iki nesne türlerini seçin.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="cc1a6-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="cc1a6-172">Üzerinde **nesne türlerini Seç** ve **öznitelikleri Seç**, nesne türleri ve tüm öznitelikleri seçin.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="cc1a6-173">Üzerinde **yapılandırma bağlayıcılarını** sayfasında, **son**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-173">On the **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="cc1a6-174">Çalıştırma profillerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc1a6-174">Create Run Profiles</span></span>
1. <span data-ttu-id="cc1a6-175">Eşitleme Hizmeti Yöneticisi Arabiriminde seçin **Bağlayıcılar**, ve **çalıştırma profillerini Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="cc1a6-176">Tıklatın **yeni bir profil**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-176">Click **New Profile**.</span></span> <span data-ttu-id="cc1a6-177">Biz başlayın **tam içeri aktarma**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="cc1a6-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="cc1a6-179">Seçin **tam içeri aktarma (yalnızca aşama)**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-179">Select the type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="cc1a6-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="cc1a6-181">Bölümü seçin **nesne = kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-181">Select the partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="cc1a6-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="cc1a6-183">Seçin **tablo** ve türü **[kullanıcılar]**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="cc1a6-184">Birden çok değerli nesne türü bölümüne gidin ve aşağıdaki resimde olduğu gibi veri girin.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span></span> <span data-ttu-id="cc1a6-185">Seçin **son** adım kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-185">Select **Finish** to save the step.</span></span>  
   <span data-ttu-id="cc1a6-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="cc1a6-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="cc1a6-188">Seçin **yeni adım**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-188">Select **New Step**.</span></span> <span data-ttu-id="cc1a6-189">Bu süre, select **nesne grubu =**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="cc1a6-190">Son sayfasında, aşağıdaki resimde olduğu gibi yapılandırmasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-190">On the last page, use the configuration as in the following picture.</span></span> <span data-ttu-id="cc1a6-191">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-191">Click **Finish**.</span></span>  
   <span data-ttu-id="cc1a6-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="cc1a6-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="cc1a6-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="cc1a6-194">İsteğe bağlı: istiyorsanız, ek çalıştırma profillerini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="cc1a6-195">Bu kılavuzda, yalnızca tam içeri aktarma kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-195">For this walkthrough, only the Full Import is used.</span></span>
7. <span data-ttu-id="cc1a6-196">Tıklatın **Tamam** çalıştırma profillerini değiştirme işlemini tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-196">Click **OK** to finish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-the-import"></a><span data-ttu-id="cc1a6-197">Bazı test verilerini ve içeri aktarma test ekleyin</span><span class="sxs-lookup"><span data-stu-id="cc1a6-197">Add some test data and test the import</span></span>
<span data-ttu-id="cc1a6-198">Örnek veritabanınızdaki bazı test verilerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="cc1a6-199">Hazır olduğunuzda seçin **çalıştırmak** ve **tam alma**.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="cc1a6-200">İşte, iki telefon numarası olan bir kullanıcı ve Grup bazı üyeleri ile.</span><span class="sxs-lookup"><span data-stu-id="cc1a6-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![CS2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="cc1a6-203">Ek A</span><span class="sxs-lookup"><span data-stu-id="cc1a6-203">Appendix A</span></span>
<span data-ttu-id="cc1a6-204">**Örnek veritabanı oluşturmak için SQL komut dosyası**</span><span class="sxs-lookup"><span data-stu-id="cc1a6-204">**SQL script to create the sample database**</span></span>

```SQL
---Creating the Database---------
Create Database GSQLDEMO
Go
-------Using the Database-----------
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

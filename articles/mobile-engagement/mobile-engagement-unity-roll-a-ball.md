---
title: "aaaUnity bir küre öğretici alma"
description: "Adımları toocreate hello Klasik Unity Roll tüm Mobile Engagement Unity öğreticileri için önkoşul olan Top oyun"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="3f6bc-103"><a id="unity-roll-a-ball"></a>Unity Roll Top oyuna oluşturma</span><span class="sxs-lookup"><span data-stu-id="3f6bc-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="3f6bc-104">Bu öğretici için biraz değiştirilmiş hello ana adım adım anlatılmaktadır [Unity Roll bir küre öğretici](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="3f6bc-104">This tutorial walks through hello main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="3f6bc-105">Bu örnek oyun hello uygulama kullanıcı tarafından denetlenen bir küresel 'player' nesnesi oluşur ve hello oyun hello amacı olan too'collect' collectible nesneleri yazılımlarla çakışma hello player nesnesiyle collectible bu nesneler tarafından.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-105">This sample game consists of a spherical 'player' object which is controlled by hello app user and hello objective of hello game is too'collect' collectible objects by colliding hello player object with these collectible objects.</span></span> <span data-ttu-id="3f6bc-106">Bu Unity Düzenleyicisi ortamıyla temel benzer olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="3f6bc-107">Ardından herhangi bir sorunla çalıştırırsanız toohello tam öğretici başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-107">If you run into any issues then you should refer toohello full tutorial.</span></span> 

### <a name="setting-up-hello-game"></a><span data-ttu-id="3f6bc-108">Merhaba oyun ayarlama</span><span class="sxs-lookup"><span data-stu-id="3f6bc-108">Setting up hello game</span></span>
<span data-ttu-id="3f6bc-109">Merhaba adımları olan hello [Unity Öğreticisi](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="3f6bc-109">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="3f6bc-110">Açık **Unity Düzenleyicisi** tıklatıp **yeni**.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="3f6bc-111">Sağlayan bir **proje adı** & **konumu**seçin **3B** tıklatıp **proje oluştur**.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="3f6bc-112">Yalnızca hello adla gibi hello yeni projenin bir parçası oluşturulan hello varsayılan Sahne Kaydet **MiniGame** içinde yeni bir  **\_planda** klasörü altında **varlıklar** klasörü:</span><span class="sxs-lookup"><span data-stu-id="3f6bc-112">Save hello default scene just created as part of hello new project as with hello name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="3f6bc-113">Oluşturma bir **3B nesne düzlemi ->** hello çalma olarak alan ve bu düzlemi nesnesi olarak yeniden adlandırın **başından başlayarak**</span><span class="sxs-lookup"><span data-stu-id="3f6bc-113">Create a **3D Object -> Plane** as hello playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="3f6bc-114">Bu sıfırlama hello dönüştürme bileşeni **başından başlayarak** kaynak hello olmasını nesne.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-114">Reset hello transform component for this **Ground** object so that it is at hello Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="3f6bc-115">İşaretini **Göster kılavuz** gelen **en menü** hello için **başından başlayarak** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-115">Uncheck **Show Grid** from **Gizmos menu** for hello **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="3f6bc-116">Güncelleştirme hello **ölçek** hello için bileşen **başından başlayarak** toobe nesnesi [X = 2, Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="3f6bc-116">Update hello **Scale** component for hello **Ground** object toobe [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="3f6bc-117">Yeni bir ekleme **3B nesne küre ->** toohello proje ve yeniden adlandırma bu küre nesnesi olarak **Player**.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-117">Add a new **3D Object -> Sphere** toohello project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="3f6bc-118">Select hello **Player** nesnesi ve'ı tıklatın **dönüştürmeyi Sıfırla** benzer toohello düzlemi nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-118">Select hello **Player** object and click **Reset Transform** similar toohello Plane object.</span></span> 
10. <span data-ttu-id="3f6bc-119">Güncelleştirme **dönüştürme -> konumu Y koordinatını ->** hello Player Y 0,5 olarak için bileşen.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-119">Update **Transform -> Position -> Y Coordinate** component for hello Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="3f6bc-120">Adlı yeni bir klasör oluşturun **malzemeleri** burada biz oluşturacak hello malzeme toocolor hello player hello projesinde.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-120">Create a new folder called **Materials** in hello project where we will create hello material toocolor hello player.</span></span> 
12. <span data-ttu-id="3f6bc-121">Yeni bir **malzeme** adlı **arka plan** bu klasörde.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="3f6bc-122">Merhaba güncelleştirerek hello malzeme Hello rengini Güncelleştir **Albedo** bunu özelliği.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-122">Update hello color of hello material by updating hello **Albedo** property of it.</span></span> <span data-ttu-id="3f6bc-123">[0,32,64] hello RGB değerleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-123">You can select hello RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="3f6bc-124">Bu yazıda hello Sahne görünüm tooapply renk toohello sürükleyin **başından başlayarak** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-124">Drag this material into hello scene view tooapply color toohello **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="3f6bc-125">Son olarak hello güncelleştirme **dönüştürme -> döndürme Y ->** too60 daha anlaşılır olması için hello tek yönlü ışığı nesne üzerinde.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-125">Finally update hello **Transform -> Rotation -> Y** too60 on hello Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-hello-player"></a><span data-ttu-id="3f6bc-126">Taşıma hello player</span><span class="sxs-lookup"><span data-stu-id="3f6bc-126">Moving hello player</span></span>
<span data-ttu-id="3f6bc-127">Merhaba adımları olan hello [Unity Öğreticisi](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="3f6bc-127">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="3f6bc-128">Ekleme bir **RigidBody** bileşen toohello **Player** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-128">Add a **RigidBody** component toohello **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="3f6bc-129">Adlı yeni bir klasör oluşturun **betikleri** başlangıç projesi olarak.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-129">Create a new folder called **Scripts** in hello Project.</span></span> 
3. <span data-ttu-id="3f6bc-130">Tıklatın **Bileşen Ekle yeni betik -> C# betik ->**.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="3f6bc-131">Bu ad **PlayerController**, tıklatıp **oluştur ve Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="3f6bc-132">Bu, oluşturabilir ve bir komut dosyası toohello Player nesnesine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-132">This will create and attach a script toohello Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="3f6bc-133">Bu komut dosyasını hello altında taşımak **betikleri** hello proje klasöründe.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-133">Move this script under hello **Scripts** folder in hello project.</span></span> 
5. <span data-ttu-id="3f6bc-134">Sık kullanılan komut dosyası Düzenleyicisi'nde düzenlemek için hello komut dosyasını açın, hello kod koddan hello ile güncelleştirin ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-134">Open hello script for editing in your favorite script editor, update hello script code with hello following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="3f6bc-135">Kullanımlar yukarıda hello komut dosyasını Not bir **hızı** özelliği.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-135">Note that hello script above uses a **Speed** property.</span></span> <span data-ttu-id="3f6bc-136">Merhaba Unity Düzenleyicisi'nde hello hızı özelliği too10 güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-136">In hello Unity editor, update hello speed property too10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="3f6bc-137">İsabet **Yürüt** hello Unity Düzenleyicisi içinde.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-137">Hit **Play** in hello Unity Editor.</span></span> <span data-ttu-id="3f6bc-138">Artık mümkün toocontrol hello Top hello klavyeyi kullanarak olması gerekir ve döndürme ve hareket ettirin.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-138">Now you should be able toocontrol hello ball using hello keyboard and it should rotate and move around.</span></span> 

### <a name="moving-hello-camera"></a><span data-ttu-id="3f6bc-139">Taşıma hello kamera</span><span class="sxs-lookup"><span data-stu-id="3f6bc-139">Moving hello camera</span></span>
<span data-ttu-id="3f6bc-140">Merhaba adımları olan hello [Unity öğretici](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) ve hello tie **ana kamera** toohello **Player** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-140">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie hello **Main Camera** toohello **Player** object.</span></span> 

1. <span data-ttu-id="3f6bc-141">Güncelleştirme hello **Transform.Position** toobe X = 0, Y 10.5, Z =-10 =.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-141">Update hello **Transform.Position** toobe X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="3f6bc-142">Güncelleştirme hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-142">Update hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="3f6bc-143">Adlı yeni bir komut dosyası eklemek **CameraController** toohello **MainCamera** ve altında hello betikler klasörüne taşıyın.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-143">Add a new script called **CameraController** toohello **MainCamera** and move it under hello Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="3f6bc-144">Merhaba betiğini düzenlemek için açın ve aşağıdaki kodu hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3f6bc-144">Open up hello script for editing and add hello following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="3f6bc-145">Böylece Hello iki başka bir işlemle ilişkili Unity ortamında - hello Player değişkeni hello ana kamera nesnesinin hello Player yuvasına sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-145">In Unity environment - drag hello Player variable into hello Player slot for hello Main Camera object so that hello two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="3f6bc-146">Şimdi hello Unity Düzenleyicisi'ni ve döndürme hello Player Top nesne Play isabet durumunda hello hello hareketini izleyen kamera görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-146">Now if you hit Play in hello Unity editor and rotate hello Player Ball object then you will see hello Camera following it in hello movement.</span></span>  

### <a name="setting-up-hello-play-area"></a><span data-ttu-id="3f6bc-147">Hello Kullan alanını ayarlama</span><span class="sxs-lookup"><span data-stu-id="3f6bc-147">Setting up hello Play area</span></span>
<span data-ttu-id="3f6bc-148">Merhaba adımları olan hello [Unity Öğreticisi](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="3f6bc-148">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="3f6bc-149">Böylece hello Player Top nesne hello oynatma hareketini alanında devre dışı bırakma değil hello başından başlayarak çevreleyen hello duvarları oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-149">We will create hello Walls surrounding hello Ground so that hello Player Ball object doesn't drop off hello play area in its movement.</span></span> 

1. <span data-ttu-id="3f6bc-150">Tıklatın **Oluştur -> boş oluştur oyun nesnesi ->** ve adlandırın **duvarları**</span><span class="sxs-lookup"><span data-stu-id="3f6bc-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="3f6bc-151">Bu duvarları nesne altında - yeni bir oluşturma **3B nesne küp ->** ve "Batı duvar" olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="3f6bc-152">Güncelleştirme hello **dönüştürme konumu ->** ve **dönüştürme -> Ölçek** bu Batı duvar nesne.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-152">Update hello **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="3f6bc-153">Merhaba Batı duvar toocreate yinelenen bir **Doğu duvar** konumlandırma ve ölçeklendirme ile güncelleştirilmiş hello Dönüştür.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-153">Duplicate hello West wall toocreate an **East wall** with hello updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="3f6bc-154">Merhaba Doğu duvar toocreate yinelenen bir **Kuzey duvar** güncelleştirilmiş hello ile konum & ölçek Dönüştür.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-154">Duplicate hello East wall toocreate a **North wall** with hello updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="3f6bc-155">Merhaba Kuzey duvar yinelenen ve oluşturma bir **Güney duvar** güncelleştirilmiş hello ile konum & ölçek Dönüştür.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-155">Duplicate hello North wall and create a **South wall** with hello updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="3f6bc-156">Collectible nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="3f6bc-156">Creating Collectible objects</span></span>
<span data-ttu-id="3f6bc-157">Merhaba adımları olan hello [Unity Öğreticisi](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="3f6bc-157">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="3f6bc-158">Hangi hello Player Top nesnenin gerekiyor too'collect collectible nesneleri hello kümesi biçimlendiren nesneleri arayan bazı çekici oluşturuyoruz ' bunlarla yazılımlarla çakışma tarafından.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-158">We will create some attractive looking objects which will form hello set of collectible objects which hello Player Ball object needs too'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="3f6bc-159">Yeni bir **3B küp nesnesi** ve toplama adlandırın.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="3f6bc-160">Merhaba ayarlamak **dönüştürme -> döndürme** & **dönüştürme -> Ölçek** hello toplama nesnesinin.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-160">Adjust hello **Transform -> Rotation** & **Transform -> Scale** of hello Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="3f6bc-161">Oluşturulacağı ve bir **yeni C# betik** adlı **değiştirici** toohello toplama nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-161">Create and attach a **new C# Script** called **Rotator** toohello Pickup object.</span></span> <span data-ttu-id="3f6bc-162">Emin tooput hello betik hello betikleri klasörü altında yapın.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-162">Make sure tooput hello script under hello Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="3f6bc-163">Düzenlemek için bu komut dosyasını açın ve aşağıdaki toobe hello güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="3f6bc-163">Open this script for editing and update it toobe hello following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="3f6bc-164">Şimdi isabet hello oynatma modunda hello Unity Düzenleyicisi'ni ve toplama nesne Göster kendi ekseninde döndürme.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-164">Now hit hello Play mode in hello Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="3f6bc-165">Adlı yeni bir klasör oluşturun **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="3f6bc-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="3f6bc-166">Sürükleme hello **toplama** nesne ve hello Prefabs klasörüne yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-166">Drag hello **Pickup** object and put it in hello Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="3f6bc-167">Yeni bir **boş oyun nesne** adlı **Pickups**.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="3f6bc-168">Konum tooorigin sıfırlamak ve oyun bu nesne altındaki hello toplama nesne sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-168">Reset its position tooorigin and then drag hello Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="3f6bc-169">Yinelenen hello **toplama** nesne ve üzerinde hello yayılan **başından başlayarak** nesneyi hello çevresinde **Player** hello güncelleştirerek nesne **Transform.Position'in X & Z**  uygun şekilde değerleri.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-169">Duplicate hello **Pickup** object and spread it on hello **Ground** object around hello **Player** object by updating hello **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="3f6bc-170">Oluşturma bir **yeni Materyaller** adlı **toplama** ve hello güncelleştirerek toobe kırmızı renk güncelleştirme **Albedo özelliği** benzer toowhat biz hello başından başlayarak güncelleştirmek için nesne.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-170">Create a **new material** called **Pickup** and update it toobe Red in color by updating hello **Albedo property** similar toowhat we did for updating hello Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="3f6bc-171">Merhaba malzeme tooall hello 4 toplama nesneleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-171">Apply hello material tooall hello 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a><span data-ttu-id="3f6bc-172">Merhaba toplama nesneleri toplama</span><span class="sxs-lookup"><span data-stu-id="3f6bc-172">Collecting hello Pickup objects</span></span>
<span data-ttu-id="3f6bc-173">Merhaba adımları olan hello [Unity Öğreticisi](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="3f6bc-173">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="3f6bc-174">Mümkün too'collect olmasını hello Player güncelleştireceğiz ' bunlarla yazılımlarla çakışma toplama nesneleri hello.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-174">We will update hello Player so that it is able too'collect' hello pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="3f6bc-175">Merhaba açın **PlayerController** düzenlemek için Player nesnesine ekli toohello komut dosyası ve aşağıdaki toohello güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="3f6bc-175">Open up hello **PlayerController** script attached toohello Player object for editing and update it toohello following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="3f6bc-176">Yeni bir **etiketi** adlı **çekme yukarı** (Bu hello komut dosyasında nedir eşleşmelidir)</span><span class="sxs-lookup"><span data-stu-id="3f6bc-176">Create a new **Tag** called **Pick Up** (it must match what is in hello script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="3f6bc-177">Bu, geçerli **etiketi** toohello Prefab toplama nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-177">Apply this **Tag** toohello Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="3f6bc-178">Etkinleştirme **IsTrigger** hello Prefab nesne için onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-178">Enable **IsTrigger** checkbox for hello Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="3f6bc-179">Katı gövde tooPickup Prefab nesnesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-179">Add a Rigid body tooPickup Prefab object.</span></span> <span data-ttu-id="3f6bc-180">Performansı iyileştirmek için hello statik collider tooa dinamik collider kullandık güncelleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-180">For performance optimization we will update hello static collider that we used tooa Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="3f6bc-181">Son olarak hello denetleyin **IsKinematic** hello prefab nesnesi için özelliği.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-181">Finally check hello **IsKinematic** property for hello prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="3f6bc-182">İsabet **Yürüt** hello Unity Düzenleyicisi ve, mümkün tooplay bu olacaktır **Top alma** taşıyarak oyun hello yönü giriş için klavye tuşlarını kullanarak Player nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-182">Hit **Play** in hello Unity editor and you will be able tooplay this **Roll a Ball** game by moving hello Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-hello-game-for-mobile-play"></a><span data-ttu-id="3f6bc-183">Merhaba mobil oynatmak için oyun güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="3f6bc-183">Updating hello game for mobile play</span></span>
<span data-ttu-id="3f6bc-184">Unity gelen sonuçları hello temel öğretici yukarıda Hello bölümler.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-184">hello sections above concluded hello basic tutorial from Unity.</span></span> <span data-ttu-id="3f6bc-185">Biz değiştirecek artık oyun toomake Merhaba, mobil cihaz kolay.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-185">Now we will modify hello game toomake it mobile device friendly.</span></span> <span data-ttu-id="3f6bc-186">Biz hello test etmek için o ana kadarki oyun için klavye girişi kullanılan unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-186">Note that we used keyboard input for hello game so far for testing.</span></span> <span data-ttu-id="3f6bc-187">Biz denetleyebilmeniz için değişiklik artık hello hello hareket kullanarak hello player telefon yani Accelerometer hello giriş olarak kullanma.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-187">Now we will modify it so that we can control hello player by using hello motion of hello phone i.e. using Accelerometer as hello input.</span></span> 

<span data-ttu-id="3f6bc-188">Merhaba açın **PlayerController** düzenleme ve güncelleştirme hello için komut dosyası **FixedUpdate** yöntemi toouse hello hareket hello accelerometer toomove hello Player nesnesinden.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-188">Open up hello **PlayerController** script for editing and update hello **FixedUpdate** method toouse hello motion from hello accelerometer toomove hello Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="3f6bc-189">Unity ile temel bir oyun oluşturma Bu öğreticiyi sonlandırır ve bu seçenek tooplay hello oyununuzu aygıtta dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f6bc-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice tooplay hello game.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png














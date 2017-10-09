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
# <a id="unity-roll-a-ball"></a>Unity Roll Top oyuna oluşturma
Bu öğretici için biraz değiştirilmiş hello ana adım adım anlatılmaktadır [Unity Roll bir küre öğretici](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial). Bu örnek oyun hello uygulama kullanıcı tarafından denetlenen bir küresel 'player' nesnesi oluşur ve hello oyun hello amacı olan too'collect' collectible nesneleri yazılımlarla çakışma hello player nesnesiyle collectible bu nesneler tarafından. Bu Unity Düzenleyicisi ortamıyla temel benzer olduğu varsayılır. Ardından herhangi bir sorunla çalıştırırsanız toohello tam öğretici başvurmalıdır. 

### <a name="setting-up-hello-game"></a>Merhaba oyun ayarlama
Merhaba adımları olan hello [Unity Öğreticisi](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)

1. Açık **Unity Düzenleyicisi** tıklatıp **yeni**. 
   
    ![][51] 
2. Sağlayan bir **proje adı** & **konumu**seçin **3B** tıklatıp **proje oluştur**.
   
    ![][52]
3. Yalnızca hello adla gibi hello yeni projenin bir parçası oluşturulan hello varsayılan Sahne Kaydet **MiniGame** içinde yeni bir  **\_planda** klasörü altında **varlıklar** klasörü:
   
    ![][53]
4. Oluşturma bir **3B nesne düzlemi ->** hello çalma olarak alan ve bu düzlemi nesnesi olarak yeniden adlandırın **başından başlayarak**
   
    ![][1]
5. Bu sıfırlama hello dönüştürme bileşeni **başından başlayarak** kaynak hello olmasını nesne. 
   
    ![][3]
6. İşaretini **Göster kılavuz** gelen **en menü** hello için **başından başlayarak** nesnesi.
   
    ![][4]
7. Güncelleştirme hello **ölçek** hello için bileşen **başından başlayarak** toobe nesnesi [X = 2, Y = 1, Z = 2]. 
   
    ![][5]
8. Yeni bir ekleme **3B nesne küre ->** toohello proje ve yeniden adlandırma bu küre nesnesi olarak **Player**. 
   
    ![][6]
9. Select hello **Player** nesnesi ve'ı tıklatın **dönüştürmeyi Sıfırla** benzer toohello düzlemi nesnesi. 
10. Güncelleştirme **dönüştürme -> konumu Y koordinatını ->** hello Player Y 0,5 olarak için bileşen.  
    
    ![][7]
11. Adlı yeni bir klasör oluşturun **malzemeleri** burada biz oluşturacak hello malzeme toocolor hello player hello projesinde. 
12. Yeni bir **malzeme** adlı **arka plan** bu klasörde. 
    
    ![][8]
13. Merhaba güncelleştirerek hello malzeme Hello rengini Güncelleştir **Albedo** bunu özelliği. [0,32,64] hello RGB değerleri seçebilirsiniz. 
    
    ![][9]
14. Bu yazıda hello Sahne görünüm tooapply renk toohello sürükleyin **başından başlayarak** nesnesi. 
    
    ![][10]
15. Son olarak hello güncelleştirme **dönüştürme -> döndürme Y ->** too60 daha anlaşılır olması için hello tek yönlü ışığı nesne üzerinde. 
    
    ![][12]

### <a name="moving-hello-player"></a>Taşıma hello player
Merhaba adımları olan hello [Unity Öğreticisi](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)

1. Ekleme bir **RigidBody** bileşen toohello **Player** nesnesi. 
   
    ![][13]
2. Adlı yeni bir klasör oluşturun **betikleri** başlangıç projesi olarak. 
3. Tıklatın **Bileşen Ekle yeni betik -> C# betik ->**. Bu ad **PlayerController**, tıklatıp **oluştur ve Ekle**. Bu, oluşturabilir ve bir komut dosyası toohello Player nesnesine ekleyebilirsiniz.  
   
    ![][14]
4. Bu komut dosyasını hello altında taşımak **betikleri** hello proje klasöründe. 
5. Sık kullanılan komut dosyası Düzenleyicisi'nde düzenlemek için hello komut dosyasını açın, hello kod koddan hello ile güncelleştirin ve kaydedin. 
   
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
6. Kullanımlar yukarıda hello komut dosyasını Not bir **hızı** özelliği. Merhaba Unity Düzenleyicisi'nde hello hızı özelliği too10 güncelleştirin.  
   
    ![][15]
7. İsabet **Yürüt** hello Unity Düzenleyicisi içinde. Artık mümkün toocontrol hello Top hello klavyeyi kullanarak olması gerekir ve döndürme ve hareket ettirin. 

### <a name="moving-hello-camera"></a>Taşıma hello kamera
Merhaba adımları olan hello [Unity öğretici](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) ve hello tie **ana kamera** toohello **Player** nesnesi. 

1. Güncelleştirme hello **Transform.Position** toobe X = 0, Y 10.5, Z =-10 =.  
2. Güncelleştirme hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.  
   
    ![][16]
3. Adlı yeni bir komut dosyası eklemek **CameraController** toohello **MainCamera** ve altında hello betikler klasörüne taşıyın. 
   
    ![][17]
4. Merhaba betiğini düzenlemek için açın ve aşağıdaki kodu hello ekleyin:
   
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
5. Böylece Hello iki başka bir işlemle ilişkili Unity ortamında - hello Player değişkeni hello ana kamera nesnesinin hello Player yuvasına sürükleyin. 
   
    ![][18]
6. Şimdi hello Unity Düzenleyicisi'ni ve döndürme hello Player Top nesne Play isabet durumunda hello hello hareketini izleyen kamera görürsünüz.  

### <a name="setting-up-hello-play-area"></a>Hello Kullan alanını ayarlama
Merhaba adımları olan hello [Unity Öğreticisi](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141). Böylece hello Player Top nesne hello oynatma hareketini alanında devre dışı bırakma değil hello başından başlayarak çevreleyen hello duvarları oluşturacağız. 

1. Tıklatın **Oluştur -> boş oluştur oyun nesnesi ->** ve adlandırın **duvarları**
   
    ![][19]
2. Bu duvarları nesne altında - yeni bir oluşturma **3B nesne küp ->** ve "Batı duvar" olarak adlandırın. 
   
    ![][20]
3. Güncelleştirme hello **dönüştürme konumu ->** ve **dönüştürme -> Ölçek** bu Batı duvar nesne. 
   
    ![][21]
4. Merhaba Batı duvar toocreate yinelenen bir **Doğu duvar** konumlandırma ve ölçeklendirme ile güncelleştirilmiş hello Dönüştür. 
   
    ![][22]
5. Merhaba Doğu duvar toocreate yinelenen bir **Kuzey duvar** güncelleştirilmiş hello ile konum & ölçek Dönüştür. 
   
    ![][23]
6. Merhaba Kuzey duvar yinelenen ve oluşturma bir **Güney duvar** güncelleştirilmiş hello ile konum & ölçek Dönüştür. 
   
    ![][24]

### <a name="creating-collectible-objects"></a>Collectible nesneleri oluşturma
Merhaba adımları olan hello [Unity Öğreticisi](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141). Hangi hello Player Top nesnenin gerekiyor too'collect collectible nesneleri hello kümesi biçimlendiren nesneleri arayan bazı çekici oluşturuyoruz ' bunlarla yazılımlarla çakışma tarafından. 

1. Yeni bir **3B küp nesnesi** ve toplama adlandırın. 
2. Merhaba ayarlamak **dönüştürme -> döndürme** & **dönüştürme -> Ölçek** hello toplama nesnesinin. 
   
    ![][25]
3. Oluşturulacağı ve bir **yeni C# betik** adlı **değiştirici** toohello toplama nesnesi. Emin tooput hello betik hello betikleri klasörü altında yapın. 
   
    ![][26]
4. Düzenlemek için bu komut dosyasını açın ve aşağıdaki toobe hello güncelleştirin: 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. Şimdi isabet hello oynatma modunda hello Unity Düzenleyicisi'ni ve toplama nesne Göster kendi ekseninde döndürme.
6. Adlı yeni bir klasör oluşturun **Prefabs** 
   
    ![][27]
7. Sürükleme hello **toplama** nesne ve hello Prefabs klasörüne yerleştirin.
   
    ![][28]
8. Yeni bir **boş oyun nesne** adlı **Pickups**. Konum tooorigin sıfırlamak ve oyun bu nesne altındaki hello toplama nesne sürükleyin.  
   
    ![][29]
9. Yinelenen hello **toplama** nesne ve üzerinde hello yayılan **başından başlayarak** nesneyi hello çevresinde **Player** hello güncelleştirerek nesne **Transform.Position'in X & Z**  uygun şekilde değerleri. 
   
    ![][30]
10. Oluşturma bir **yeni Materyaller** adlı **toplama** ve hello güncelleştirerek toobe kırmızı renk güncelleştirme **Albedo özelliği** benzer toowhat biz hello başından başlayarak güncelleştirmek için nesne. 
    
    ![][31]
11. Merhaba malzeme tooall hello 4 toplama nesneleri uygulayın.
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a>Merhaba toplama nesneleri toplama
Merhaba adımları olan hello [Unity Öğreticisi](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141). Mümkün too'collect olmasını hello Player güncelleştireceğiz ' bunlarla yazılımlarla çakışma toplama nesneleri hello. 

1. Merhaba açın **PlayerController** düzenlemek için Player nesnesine ekli toohello komut dosyası ve aşağıdaki toohello güncelleştirin:  
   
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
2. Yeni bir **etiketi** adlı **çekme yukarı** (Bu hello komut dosyasında nedir eşleşmelidir)  
   
    ![][33]
   
    ![][34]
3. Bu, geçerli **etiketi** toohello Prefab toplama nesnesi. 
   
    ![][35]
4. Etkinleştirme **IsTrigger** hello Prefab nesne için onay kutusu.
   
    ![][36]
5. Katı gövde tooPickup Prefab nesnesi ekleyin. Performansı iyileştirmek için hello statik collider tooa dinamik collider kullandık güncelleştireceğiz. 
   
    ![][37]
6. Son olarak hello denetleyin **IsKinematic** hello prefab nesnesi için özelliği. 
   
    ![][38]
7. İsabet **Yürüt** hello Unity Düzenleyicisi ve, mümkün tooplay bu olacaktır **Top alma** taşıyarak oyun hello yönü giriş için klavye tuşlarını kullanarak Player nesnesi. 

### <a name="updating-hello-game-for-mobile-play"></a>Merhaba mobil oynatmak için oyun güncelleştiriliyor
Unity gelen sonuçları hello temel öğretici yukarıda Hello bölümler. Biz değiştirecek artık oyun toomake Merhaba, mobil cihaz kolay. Biz hello test etmek için o ana kadarki oyun için klavye girişi kullanılan unutmayın. Biz denetleyebilmeniz için değişiklik artık hello hello hareket kullanarak hello player telefon yani Accelerometer hello giriş olarak kullanma. 

Merhaba açın **PlayerController** düzenleme ve güncelleştirme hello için komut dosyası **FixedUpdate** yöntemi toouse hello hareket hello accelerometer toomove hello Player nesnesinden. 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

Unity ile temel bir oyun oluşturma Bu öğreticiyi sonlandırır ve bu seçenek tooplay hello oyununuzu aygıtta dağıtabilirsiniz. 

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














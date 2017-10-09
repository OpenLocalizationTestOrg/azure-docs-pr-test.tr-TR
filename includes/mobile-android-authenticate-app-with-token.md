
<span data-ttu-id="0b1d1-101">Merhaba uygulama her başlatıldığında hello önceki örnek bir standart oturum hello istemci toocontact gerektiren açma, her iki hello kimlik sağlayıcısı ve hello arka uç Azure hizmeti gösterdi.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-101">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello back-end Azure service every time hello app starts.</span></span> <span data-ttu-id="0b1d1-102">Bu yöntem yetersiz olduğunu ve birçok müşteri toostart uygulamanız aynı anda çalışırsanız kullanımı ile ilgili sorunlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-102">This method is inefficient, and you can have usage-related issues if many customers try toostart your app simultaneously.</span></span> <span data-ttu-id="0b1d1-103">Daha iyi bir toocache hello yetkilendirme belirtecini hello Azure hizmeti ve try toouse bu ilk önce bir sağlayıcı tabanlı oturum açma kullanarak döndürülen yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-103">A better approach is toocache hello authorization token returned by hello Azure service, and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="0b1d1-104">Merhaba arka uç istemcisi tarafından yönetilen veya hizmet tarafından yönetilen kimlik doğrulaması kullanıp bağımsız olarak Azure hizmeti tarafından verilen hello belirteç önbelleğe alabilir.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-104">You can cache hello token issued by hello back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="0b1d1-105">Bu öğretici, kimlik doğrulama hizmeti tarafından yönetilen kullanır.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="0b1d1-106">Merhaba ToDoActivity.java dosyasını açın ve içeri aktarma deyimlerini aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0b1d1-106">Open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="0b1d1-107">Üyeleri toohello aşağıdaki hello eklemek `ToDoActivity` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-107">Add hello following members toohello `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="0b1d1-108">Merhaba ToDoActivity.java dosyasında hello tanımı aşağıdaki hello eklemek `cacheUserToken` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-108">In hello ToDoActivity.java file, add hello following definition for hello `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="0b1d1-109">Bu yöntem hello kullanıcı kimliği ve belirteç özel olarak işaretlenmiş bir tercih dosyasında depolar.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-109">This method stores hello user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="0b1d1-110">Merhaba cihazdaki diğer uygulamalar erişim toohello belirteci yok, bu erişim toohello önbellek korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-110">This should protect access toohello cache so that other apps on hello device do not have access toohello token.</span></span> <span data-ttu-id="0b1d1-111">Merhaba tercih hello uygulaması için korumalı.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-111">hello preference is sandboxed for hello app.</span></span> <span data-ttu-id="0b1d1-112">Birisi erişim toohello aygıtı sağlarsa, ancak bunlar arasında başka yollarla toohello belirteç önbelleği erişim kazanabilir mümkündür.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-112">However, if someone gains access toohello device, it is possible that they may gain access toohello token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0b1d1-113">Ayrıca, belirteç erişimi tooyour veri yüksek oranda gizli olarak kabul edilir ve birisi erişim toohello aygıtı kazanabilir hello belirteç şifreleme ile koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-113">You can further protect hello token with encryption, if token access tooyour data is considered highly sensitive and someone may gain access toohello device.</span></span> <span data-ttu-id="0b1d1-114">Tamamen güvenli bir çözümdür hello Bu öğretici kapsamında değildir ancak ve güvenlik gereksinimlerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-114">A completely secure solution is beyond hello scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="0b1d1-115">Merhaba ToDoActivity.java dosyasında hello tanımı aşağıdaki hello eklemek `loadUserTokenCache` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-115">In hello ToDoActivity.java file, add hello following definition for hello `loadUserTokenCache` method.</span></span>

        private boolean loadUserTokenCache(MobileServiceClient client)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            String userId = prefs.getString(USERIDPREF, null);
            if (userId == null)
                return false;
            String token = prefs.getString(TOKENPREF, null);
            if (token == null)
                return false;

            MobileServiceUser user = new MobileServiceUser(userId);
            user.setAuthenticationToken(token);
            client.setCurrentUser(user);

            return true;
        }
5. <span data-ttu-id="0b1d1-116">Merhaba, *ToDoActivity.java* dosya, hello yerine `authenticate` belirteç önbelleği kullanan yöntemi aşağıdaki hello yöntemiyle.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-116">In hello *ToDoActivity.java* file, replace hello `authenticate` method with hello following method, which uses a token cache.</span></span> <span data-ttu-id="0b1d1-117">Toouse Google dışında bir hesap istiyorsanız hello oturum açma sağlayıcısı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-117">Change hello login provider if you want toouse an account other than Google.</span></span>

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. <span data-ttu-id="0b1d1-118">Geçerli bir hesap kullanarak hello uygulama ve test kimlik doğrulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-118">Build hello app and test authentication using a valid account.</span></span> <span data-ttu-id="0b1d1-119">Çalıştırın en az iki kez.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-119">Run it at least twice.</span></span> <span data-ttu-id="0b1d1-120">İlk çalıştırma hello sırasında bir komut istemi toosign içinde almak ve hello belirteç önbelleği oluşturmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-120">During hello first run, you should receive a prompt toosign in and create hello token cache.</span></span> <span data-ttu-id="0b1d1-121">Bundan sonra her çalıştırmayı tooload hello belirteç önbelleği kimlik doğrulaması için çalışır.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-121">After that, each run attempts tooload hello token cache for authentication.</span></span> <span data-ttu-id="0b1d1-122">İçinde gerekli toosign olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="0b1d1-122">You should not be required toosign in.</span></span>

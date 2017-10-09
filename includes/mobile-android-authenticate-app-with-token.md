
Merhaba uygulama her başlatıldığında hello önceki örnek bir standart oturum hello istemci toocontact gerektiren açma, her iki hello kimlik sağlayıcısı ve hello arka uç Azure hizmeti gösterdi. Bu yöntem yetersiz olduğunu ve birçok müşteri toostart uygulamanız aynı anda çalışırsanız kullanımı ile ilgili sorunlar olabilir. Daha iyi bir toocache hello yetkilendirme belirtecini hello Azure hizmeti ve try toouse bu ilk önce bir sağlayıcı tabanlı oturum açma kullanarak döndürülen yaklaşımdır.

> [!NOTE]
> Merhaba arka uç istemcisi tarafından yönetilen veya hizmet tarafından yönetilen kimlik doğrulaması kullanıp bağımsız olarak Azure hizmeti tarafından verilen hello belirteç önbelleğe alabilir. Bu öğretici, kimlik doğrulama hizmeti tarafından yönetilen kullanır.
>
>

1. Merhaba ToDoActivity.java dosyasını açın ve içeri aktarma deyimlerini aşağıdaki hello ekleyin:

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. Üyeleri toohello aşağıdaki hello eklemek `ToDoActivity` sınıfı.

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. Merhaba ToDoActivity.java dosyasında hello tanımı aşağıdaki hello eklemek `cacheUserToken` yöntemi.

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    Bu yöntem hello kullanıcı kimliği ve belirteç özel olarak işaretlenmiş bir tercih dosyasında depolar. Merhaba cihazdaki diğer uygulamalar erişim toohello belirteci yok, bu erişim toohello önbellek korumanız gerekir. Merhaba tercih hello uygulaması için korumalı. Birisi erişim toohello aygıtı sağlarsa, ancak bunlar arasında başka yollarla toohello belirteç önbelleği erişim kazanabilir mümkündür.

   > [!NOTE]
   > Ayrıca, belirteç erişimi tooyour veri yüksek oranda gizli olarak kabul edilir ve birisi erişim toohello aygıtı kazanabilir hello belirteç şifreleme ile koruyabilirsiniz. Tamamen güvenli bir çözümdür hello Bu öğretici kapsamında değildir ancak ve güvenlik gereksinimlerine bağlıdır.
   >
   >
4. Merhaba ToDoActivity.java dosyasında hello tanımı aşağıdaki hello eklemek `loadUserTokenCache` yöntemi.

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
5. Merhaba, *ToDoActivity.java* dosya, hello yerine `authenticate` belirteç önbelleği kullanan yöntemi aşağıdaki hello yöntemiyle. Toouse Google dışında bir hesap istiyorsanız hello oturum açma sağlayıcısı değiştirin.

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
6. Geçerli bir hesap kullanarak hello uygulama ve test kimlik doğrulaması oluşturun. Çalıştırın en az iki kez. İlk çalıştırma hello sırasında bir komut istemi toosign içinde almak ve hello belirteç önbelleği oluşturmak gerekir. Bundan sonra her çalıştırmayı tooload hello belirteç önbelleği kimlik doğrulaması için çalışır. İçinde gerekli toosign olmamalıdır.

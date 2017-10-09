
1. Merhaba MainPage.xaml.cs proje dosyasında hello aşağıdakileri ekleyin **kullanarak** deyimleri:
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. Hello yerine **AuthenticateAsync** koddan hello yöntemiyle:
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses hello Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use hello PasswordVault toosecurely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try tooget an existing credential from hello vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from hello stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set hello user from hello stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check toodetermine if hello token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with hello identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store hello user credentials.
                    credential = new PasswordCredential(provider.ToString(),
                        user.UserId, user.MobileServiceAuthenticationToken);
                    vault.Add(credential);
   
                    success = true;
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (MobileServiceInvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
   
            return success;
        }
   
    Bu sürümünde **AuthenticateAsync**, hello uygulama çalıştığında hello depolanan toouse kimlik **PasswordVault** tooaccess hello hizmet. Hiçbir depolanmış kimlik bilgisi olduğunda bir normal oturum açma da gerçekleştirilir.
   
   > [!NOTE]
   > Önbelleğe alınan bir belirteç süresi dolmuş olabilir ve hello uygulama kullanımda olduğunda belirteci süre sonu kimlik doğrulamasından sonra da oluşabilir. bir belirteç süresi dolmuşsa, toodetermine nasıl görürüm toolearn [denetlemek için süresi dolmuş kimlik doğrulama belirteçleri](http://aka.ms/jww5vp). Bir çözüm toohandling yetkilendirme hataları için ilgili tooexpiring belirteçleri bakın sonrası hello [önbelleğe alma ve Azure Mobile Services belirteçlerin süresinin işleme yönetilen SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx). 
   > 
   > 
3. Merhaba uygulamayı iki kez yeniden başlatın.
   
    Merhaba ilk başlatma üzerinde hello sağlayıcısı ile oturum açma yeniden gerekli olduğuna dikkat edin. Ancak, hello ikinci başlatmada hello önbelleğe alınmış kimlik bilgileri kullanılır ve oturum açma atlanır. 


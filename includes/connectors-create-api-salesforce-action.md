Bir koşul hello tetik tarafından oluşturulan hello verilerle ilginç bir şey kendi zaman toodo eklediğiniz göre. Bu adımları tooadd hello izleyin **Salesforce - Get nesne** eylem. Bu eylemin hello veri yeni bir sağlama her oluşturulduğunda alırsınız. Bu gibi durumlarda, hello Salesforce - Get bir nesne eylem toosend hello verileri kullanır ikinci bir eylem de hello Office 365 Bağlayıcısı'nı kullanarak bir e-posta ekleyeceksiniz.  

tooconfigure Merhaba Bu eylem, aşağıdaki bilgilerle tooprovide hello gerekir. Merhaba yeni dosyasının hello özelliklerinden bazıları için giriş olarak hello tetik tarafından oluşturulan kolay toouse veri olduğunu fark edersiniz:

| Dosya özelliği oluşturma | Açıklama |
| --- | --- |
| Nesne türü |İlgilendiğiniz Salesforce nesnesinin hello türü budur. Örnekler sağlama, hesap, vs. |
| Nesne Kimliği |Bu hello nesne için bir tanımlayıcıyı temsil eder. |

1. Seçin **Eylem Ekle** bağlantı. Bu açılır hello arama kutusu için herhangi bir işlem, arayabileceğiniz tootake ister. Bu örnekte, Salesforce ilgi eylemlerdir.      
   ![Salesforce eylem görüntü 1](./media/connectors-create-api-salesforce/action-1.png)  
2. Girin *salesforce* Eylemler ilgili toosalesforce toosearch.
3. Seçin **Salesforce - Get nesne** eylem tootake hello gibi.   **Not**:, istendiğinde tooauthorize Salesforce hesabını, daha önce yapmadıysanız, logic app tooaccess olacaktır.    
   ![Salesforce eylem görüntü 2](./media/connectors-create-api-salesforce/action-2.png)    
4. Merhaba **Get nesne** kontrol açar.  
5. Seçin *neden* hello nesne türü olarak.
6. Select hello **nesne kimliği** denetim.
7. Seçin **...**  tooexpand hello giriş olarak Eylemler için kullanılabilir belirteç listesi.       
   ![Salesforce eylem görüntüsü 3](./media/connectors-create-api-salesforce/action-3.png)    
8. Seçin **neden kimliği** kontrol açar.   
   ![Salesforce eylem görüntüsü 4](./media/connectors-create-api-salesforce/action-4.png)     
9. Merhaba sağlama kimliği belirtecini şimdi hello bu hello nesne eylem, bu mantıksal uygulama tetiklenen sağlama eşit toohello sağlama Kimliğini bir Kimliğe sahip bir sağlama arar Get gösteren nesne kimliği denetim olduğuna dikkat edin.  
   ![Salesforce eylem görüntüsü 5](./media/connectors-create-api-salesforce/action-5.png)  
10. Çalışmanızı kaydedin. İşte bu kadar hello Get nesne eylem tooyour mantıksal uygulama eklendi. Get nesne denetimi aşağıdaki gibi görünmelidir:    
    ![Salesforce eylem görüntüsü 6](./media/connectors-create-api-salesforce/action-6.png)  

Bir eylem tooget bir sağlama eklediğiniz, toodo yeni oluşturulan hello sağlama ile ilgi çekici bir şey isteyebilirsiniz. Bir kuruluşta toosend bir e-posta toonotify yeni bir sağlama oluşturulduğunu belirten bir dağıtım listesi isteyebilirsiniz. Şimdi hello Office 365 Bağlayıcısı toosend bazı nesnesinden hello yeni sağlama Salesforce hello ilgili bilgiler içeren bir e-posta kullanın.  

1. Seçin **Eylem Ekle** enter *e-posta* hello arama denetiminde. İlgili toosending ve e-posta alma hello Eylemler toothose filtreler.  
2. Select hello **Office 365 Outlook - bir e-posta Gönder** liste öğesi. Zaten oluşturmadıysanız bir *bağlantı* tooyour Office 365 hesabı, şunları yapacaksınız istendiğinde tooenter Office 365 kimlik bilgilerini toocreate olması artık BT. Tamamlandıktan sonra hello **bir e-posta Gönder** kontrol açar.        
   ![Salesforce eylem görüntüsü 7](./media/connectors-create-api-salesforce/action-7.png)  
3. Toosend e-posta tooin hello istediğiniz hello e-posta adresi girin **için** denetim.
4. Merhaba, **konu** denetlemek, girin *yeni oluşturulan neden* - seçip hello *şirket* belirteci. Bu hello görüntüler *şirket* hello yeni sağlama Salesforce'ta oluşturulan alanının.  
5. Merhaba, **gövde** denetim, şunları yapabilirsiniz hello belirteçlerinden hello yeni sağlama nesne ve birini de girebilirsiniz gövdesinde hello toodisplay istediğiniz herhangi bir metni seçin, e-posta hello. Örnek aşağıda verilmiştir:  
   ![Salesforce eylem görüntüsü 8](./media/connectors-create-api-salesforce/action-8.png)   
6. İş akışınızı kaydedin.  

Bu kadar. Mantıksal uygulamanızı tamamlanmıştır.  

Artık, mantıksal uygulamanızı test edebilirsiniz: Salesforce içinde oluşturduğunuz hello koşulunu sağlayan yeni bir sağlama oluşturun.  Bu kılavuz tam olarak izlediyseniz, müşteri adayı içeren bir e-posta adresiyle yalnızca oluşturma *amazon.com* da. Birkaç saniye sonra mantıksal uygulamanızı tetiklenmesi ve hello sonuçları benzer toothis görünebilir:  
![Salesforce eylem görüntü 9](./media/connectors-create-api-salesforce/action-9.png)  


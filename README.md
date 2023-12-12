# **Modelin Oluşturulmaya Başlanması**

## **Etiketleme**

Clean Reddit Postlarının bulunduğu "data_cleaned.csv" dosyası dataframeye aktarılmıştır. 
Reddit Postlarının kategorileri kelime şeklinde kayıtlı olduğu için bu kategoriler 0, 1, 2, 3 gibi bilgisayarın anlayabileceği bir formata dönüştürülmelidir. 
Labels adında yeni bir kolon açılarak kategorisi ekonomi olan Reddit Postları için 0 rakamı, kategorisi sanat olan Reddit Postları için 1 rakamı, kategorisi teknoloji olan Reddit Postları için 2 rakamı ve kategorisi politika olan Reddit Postları için 3 rakamı labels olarak eklenmiştir.

![etiketlemeresim](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/994b0bce-ffdd-41b0-802e-bb949923a22d)

## **Verisetinin Parçalanması**

Modelin başarısını doğru şekilde ölçebilmek için modeli eğittiğimiz veriler ile test ettiğimiz veriler farklı olmalıdır. Modelin eğitilmiş olduğu verileri tekrar modele gönderirsek model bu veriler ile eğitildiği için başarısı yüksek ve yanıltıcı olacaktır. Bu yüzden verisetini parçalamamız gerekir. Bu projede verisetinin %80 'i modeli eğitmek için, %20 'si de modeli test etmek için kullanılacaktır.
Aşağıda verisetinin nasıl parçalanacağının bir örneği gösterilmiştir.

![verisetininparçalanmasıresim](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/b54bd9cb-e47a-42c7-87dd-99e168d5eb71)

## **Reddit Postlarının Vektörel Matrisinin Çıkarılması**

Reddit Postlarını metinden oluştuğu için bunun bilgisayar ortamında işlenmesi mümkün değildir bu yüzden veriler sayısal değerlere dönüştürülmelidir. 
Bir sözlük oluşturularak dökümandaki her kelime için bir indexleme yapılır. 
Daha sonra hangi index numarasına sahip kelimenin hangi Reddit Postunda kaç kere geçtiği hesaplanarak sayma matrisi oluşturulur. 
Bu işlemi yaparken tf-idf vectorizer kullanılarak bir kelimenin döküman içindeki önemi istatistiksel olarak hesaplanmıştır. 
Bu sayede her Reddit Postunda geçen model için anlamsız kelimelerin önemi düşürülmüştür yani stopwordsler tekrardan ayıklanmıştır.

 ## **Modellerin Eğitilmesi**

Daha önceden parçalanmış olan X_train ve y_train verileri Naive Bayes ve Support Vector Machine modeline gönderilerek modeller eğitilmiştir. Eğitim sonucunda modellerin accuracy ve f1 score değerleri hesaplanmıştır. Modelleri eğitmek için sklearn kütüphanesi kullanılmıştır.

 
 ## **Modellerin Başarısının Hesaplanması**

Modelin başarısı hem train hem test verileri üzerinden Accuracy ve F1 score ile ölçülmüştür. 
Alınan sonuçlar aşağıda bulunmaktadır.

![resim1](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/35953f64-c1d3-4a4c-a791-861858b90226)     ![resim2](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/a6fda108-2dd6-4600-98b0-245c3c6c64bc)


 ## **Kategorilere Göre Başarı Dağılımları**
 ## **Modellerin Reddit Postlarına Göre Yaptığı Tahminler**
 ## **Modellerin Hata Oranları**
 ## **Manuel Reddit Postu Testi**






# **Manuel Reddit Postu Testi**

Modeli manuel olarak test etmek için elle bazı Reddit Postları girilecek ve modelin bu Reddit Postlarının hangi kategoriye ait olduğunu tahmin etmesi istenecektir. Test sonuçları aşağıda gösterilmiştir.

**Test1:**

![test1](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/b40707dd-45a0-470d-bf99-de270a80da5d)


**Test2:**

![test2](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/ca4775b9-51db-494b-b74c-ed37721d973c)


**Test3:**

![test3](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/35e02842-e112-48af-b77a-a730aebd14ef)


**Test4:**

![test4](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/7e2434d0-9398-4b4b-bfb0-b8d8bc4c0f50)


**Test5:**

![test5](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/1f201db4-9e4e-4385-aa25-54a572921546)

# **SONUÇ**


Sonuca bakıldığında yapılan projede seçilen modelin ne kadar önemli olduğu görülmektedir.
Yapılan farklı projelerde farklı modeller daha iyi sonuç verebilmektedir.
Her proje için seçilen modelin kendine göre bazı avantajları ve dezavantajları vardır.
Model seçiminde bu avantajları ve dezavantajları göz önüne alarak model seçimi yapılmalıdır.
Modelin bize en düşük hata oranı ile sonuçları göstermesini isteriz ve bu isteğimizi yerine getiren modeli seçmek bizim sorumluluğumuzdur.
Model seçiminin önemi kadar verisetinin güzel bir şekilde hazırlanmış olması, verisetindeki noktalama işaretleri ve modele olumsuz etki edecek stopwordslerden arındırılmış olması, verisetindeki verilerin miktari, eğitim-test verilerinin parçalanma oranı vs. modelin başarısına etki eden çok önemli faktörlerdir. 

Bu projede ulaşılan başarı oranı(%61 NB ve %77 SVM) yüksek bir başarı oranına sahip değildir bunun en temel sebebi verisetini oluştururken farklı kategorilerden aldığımız Reddit postlarıdır ve bunları sayılarıdır çünkü her kategoriden 125 tane veri çektik bu verilerin az olması sebebiyle bu başarı oranlarına sahibiz.
Eğer ki verisetinde ki verilerin sayısını her kategori için 125 tane değilde 10 bin tane yapsaydık bu testler daha fazla veriye maruz kalacağı için kategori işlemlerini daha düzgün yapacaktı çünkü elimizde ne kadar çok veri varsa testler o denli doğru çalışacaktır.

Yukarıda da belirtitğimiz gibi, 4 farklı kategoriden 125'er tane veri alarak bir veriseti oluşturduk. Toplamda bu 500 tane veriyle bir dil eğitmeye çalıştık. Sonuç olarak verilerin az olması sebebiyle dilimizi düzgün bir şekilde eğitemedik.Dilin düzgün bir şekilde eğitilebilmesi için daha çok veriye ihtiyacımız var. Ancak Redditten aldığımız veriler sınırlı olduğu için ve daha fazlasını ekleyemediğimiz için dilimiz yeteri kadar beslenemedi. Bundan dolayı incelenen text'in hangi kategoriye ait olduğunu yeteri kadar düzgün belirleyemiyoruz. Bunun çözümü basit ama elimizde ki imkanlar el vermediği için çözemiyoruz.Çözümü şudur ki yukarıda da belirttiğimiz gibi verisetinin çok fazla veriden oluşması bu sorunun çözümüdür. Ancak Reddit platformunda ki verilerin azlığı sebebiyle bunu gerçekleştiremiyoruz. 
Ancak geçici bir çözüm olarak analiz edeceğimiz text'in kelime sayısını olabildiğince fazla tutarak dilimizin bu text'in kategorisini analiz etmesine yardımcı olabiliriz. 


Yukarıda ki test3, test4, test5 bu çözüme uygun olarak analiz edilmiştir ve bir nebzede olsa dilimiz doğru tahminde bulunmuştur.
test1 ve test2 sadece 1 cümleden oluşan ve yeterince kelime olmayan testlerdir ve bu testlerin kategorilerinin yanlış tahmin edildiğini görüyoruz.
test1'de kategori olarak kesinlikle teknoloji ve test2'de de kategori olarak kesinlikle ekonomi çıkması gerekirken sanat ve politika çıkıyor bunu sebebi verisetinin az sayıda veriden oluşmasıdır.
test3,test4,test5'de bu çözüme dayalı bir süreç yürütebilmek için her test için 10 cümlelik bir text yazdık.
test3'de kategori olarak kesinlikle sanat çıkması gerekiyor ve gerçekten sanat çıkıyor çünkü analiz ettiğimiz text'in kelime sayısını olabildiğince fazla tuttuk ve yukarıda belirttiğimiz çözüm ile bu durumu ispatladık. 
Benzer şekilde test4'de kategori olarak kesinlikle politika  ve test5'de ise kesinlik teknoloji çıkması gerekiyor ve gerçekten dilimiz tahminlerini doğru yapıyor.







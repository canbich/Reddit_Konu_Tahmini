





Etiketleme

Clean Reddit Postlarının bulunduğu "data_cleaned.csv" dosyası dataframeye aktarılmıştır. 
Reddit Postlarının kategorileri kelime şeklinde kayıtlı olduğu için bu kategoriler 0, 1, 2, 3 gibi bilgisayarın anlayabileceği bir formata dönüştürülmelidir. 
Labels adında yeni bir kolon açılarak kategorisi ekonomi olan Reddit Postları için 0 rakamı, kategorisi sanat olan Reddit Postları için 1 rakamı, kategorisi teknoloji olan Reddit Postları için 2 rakamı ve kategorisi politika olan Reddit Postları için 3 rakamı labels olarak eklenmiştir.
![etiketlemeresim](https://github.com/canbich/Reddit_Konu_Tahmini/assets/99393604/562b6fef-b3b8-4556-ba09-5ed815e25d00)
Verisetinin Parçalanması
Modelin başarısını doğru şekilde ölçebilmek için modeli eğittiğimiz veriler ile test ettiğimiz veriler farklı olmalıdır. Modelin eğitilmiş olduğu verileri tekrar modele gönderirsek model bu veriler ile eğitildiği için başarısı yüksek ve yanıltıcı olacaktır. Bu yüzden verisetini parçalamamız gerekir. Bu projede verisetinin %80 'i modeli eğitmek için, %20 'si de modeli test etmek için kullanılacaktır.
Aşağıda verisetinin nasıl parçalanacağının bir örneği gösterilmiştir.
![verisetininparçalanmasıresim](https://github.com/canbich/Reddit_Konu_Tahmini/assets/99393604/1742378b-e916-4364-bdd6-d8a0c51ba0b6)
Reddit Postlarını metinden oluştuğu için bunun bilgisayar ortamında işlenmesi mümkün değildir bu yüzden veriler sayısal değerlere dönüştürülmelidir. 
Bir sözlük oluşturularak dökümandaki her kelime için bir indexleme yapılır. 
Daha sonra hangi index numarasına sahip kelimenin hangi Reddit Postunda kaç kere geçtiği hesaplanarak sayma matrisi oluşturulur. 
Bu işlemi yaparken tf-idf vectorizer kullanılarak bir kelimenin döküman içindeki önemi istatistiksel olarak hesaplanmıştır. 
Bu sayede her Reddit Postunda geçen model için anlamsız kelimelerin önemi düşürülmüştür yani stopwordsler tekrardan ayıklanmıştır.
<img width="1595" alt="image" src="https://github.com/canbich/Reddit_Konu_Tahmini/assets/99393604/e0ef62f7-0b05-4928-8dab-40dd0a4ccd6c">

Modelin başarısı hem train hem test verileri üzerinden Accuracy ve F1 score ile ölçülmüştür. 
Alınan sonuçlar aşağıda bulunmaktadır.

<img width="962" alt="image" src="https://github.com/canbich/Reddit_Konu_Tahmini/assets/99393604/6fcd5d25-e76a-4398-acdd-3031be3bc3c5">

<img width="1580" alt="image" src="https://github.com/canbich/Reddit_Konu_Tahmini/assets/99393604/d07c3dd8-1332-4c55-a402-1c7597a7fce7">

Kategorilere göre modellerin test verisetindeki başarı dağılımları classification_report() fonksiyonu kullanılarak hesaplanmıştır. 
Alınan sonuçlar aşağıda bulunmaktadır.

![3 1](https://github.com/canbich/Reddit_Konu_Tahmini/assets/99393604/77ca65d3-ff85-46a7-b5e9-ff9fb35bbcb6)

Sonuçlar incelendiğinde Her iki modelin de en başarılı tahmin yaptığı kategorinin ekonomi kategorisi olduğunu görülmektedir. 
![3 2](https://github.com/canbich/Reddit_Konu_Tahmini/assets/99393604/86c0ca10-0ff3-4eb0-beb0-7cb234eb546e)


Aşağıdaki görseldeki kolonlarda, Reddit Postu, Reddit Postunun bulunduğu kategori, Naive Bayes modelinin Reddit postu için tahmini ve Support Vector Machine modelinin Reddit Postu için tahmini gösterilmektedir.

0=ekonomi , 1=sanat , 2=teknoloji , 3=politika

![4](https://github.com/canbich/Reddit_Konu_Tahmini/assets/99393604/fdcbf29e-1f1a-434e-ae73-62972ecde23b)

Reddit Postlarının kategorilerine ve modellerin yaptığı tahminlere bakıldığında modeller oldukça iyi çalışıyor gibi gözüküyor. 94. Reddit Postuna bakıldığında naive bayes modelinin bu Reddit Postu için yanlış tahmin yaptığını görüyoruz.
Modellerin hata oranlarını tespit etmek için 2 farklı metrik kullanılmıştır. Bunlar Ortalama Kare Hatası(MSE) ve Ortalama Mutlak Hata(MAE) dir.

Ortalama Kare Hatası(MSE)
Ortalama Kare Hatası tahmin edilen sonuçlarınızın gerçek sayıdan ne kadar farklı olduğuna dair size mutlak bir sayı verir.

Ortalama Mutlak Hata(MAE)
Ortalama mutlak hata, mutlak hata değerinin toplamını alır, hata terimlerinin toplamının daha doğrudan bir temsilidir.
![5](https://github.com/canbich/Reddit_Konu_Tahmini/assets/99393604/5e3c4397-fec0-4b42-b36d-f44742ccef55)
Sonuçlar incelendiğinde Naive Bayes modelinin Support Vector Machine modeline göre biraz daha fazla hata yaptığını görüyoruz.

Modeli manuel olarak test etmek için elle bazı Reddit Postları girilecek ve modelin bu Reddit Postlarının hangi kategoriye ait olduğunu tahmin etmesi istenecektir. Test sonuçları aşağıda gösterilmiştir.

Test1:
![6](https://github.com/canbich/Reddit_Konu_Tahmini/assets/99393604/5ad1d71d-e31c-4ad6-8214-9c65d8a417d3)
Test2:




# Node Silme

Bu C# sınıfı, binary ağaç veri yapısını oluşturmak için kullanılır. `tree` adlı bir sınıf içerir ve `nodeSil` metodunu kullanarak ağaçtan bir düğüm silmeyi sağlar.

## `tree` Sınıfı

```csharp
class tree
{
    public int value;
    public tree right;
    public tree left;
}
```

### Özellikler

- `value`: Düğümün değerini temsil eder.
- `right`: Düğüme bağlı olan sağ alt düğümü belirtir.
- `left`: Düğüme bağlı olan sol alt düğümü belirtir.


## `nodeSil` Metodu
Bu C# metodunun amacı, verilen bir değeri ağaçtan silmektir. Ağaç içinde gezinerek belirli bir değeri bulur ve bu değeri ağaçtan kaldırır. Metot, ağacın kök düğümü ve silinecek değeri parametre olarak alır.
```csharp
static tree nodeSil(tree root, int value)
{
    if (root == null) return null;

    else if (root.value < value) // aranan value daha büyük
    {
        root.right = nodeSil(root.right, value);
    }
    else if (root.value > value) // aranan value daha küçük
    {
        root.left = nodeSil(root.left, value);
    }
    else // aranan value eşit, node u bulduk yani
    {
        if (root.left == null)
        {
            return root.right;
        }
        else if (root.right == null)
        {
            return root.left;
        }
        else
        {
            tree tmp = root.right;
            while (tmp.left != null)
            {
                tmp = tmp.left;
            }

            root.value = tmp.value;
            root.right = nodeSil(root.right, tmp.value);
        }
    }

    return root;
}
```

## Parametreler

- `node`: Ağaçtaki mevcut düğüm.
- `value`: Silenecek düğümün değeri.

## Dönüş Değeri

Metot, güncellenmiş ağaç yapısını temsil eden kök düğümü döndürür.

### İşleyiş:

1. Eğer ağacın kökü null ise, ağaç zaten boş demektir, dolayısıyla herhangi bir işlem yapmadan null döner.

2. Eğer aranan değer, kök düğümün değerinden küçükse, sağ ağaç üzerinde devam eder ve `nodeSil` metodu rekürsif olarak çağrılır.

3. Eğer aranan değer, kök düğümün değerinden büyükse, sol ağaç üzerinde devam eder ve yine `nodeSil` metodu rekürsif olarak çağrılır.

4. Eğer aranan değer, kök düğümün değerine eşitse, bu durumda silme işlemi gerçekleştirilir, bu işlemde 3 tane durum olacak:
   1. Eğer sol alt ağaç boşsa, sağ alt ağacı geri döner.
   2. Eğer sağ alt ağaç boşsa, sol alt ağacı geri döner.
   3. Eğer her iki alt ağaç da doluysa, sağ alt ağacın en küçük düğümü bulunur ve kök düğümün değeri bu düğümle değiştirilir. Ardından, sağ alt ağaç üzerinde tekrar `nodeSil` metodu çağrılır ki taşıdığımız düğüm kaldırılsın.

5. Her adımda güncellenmiş ağaç yapısı, son olarak kök düğümü geri döndürülür.

## Örnekler

<div align="center">
    <h3>Binary Ağaç</h3>
    <img src="https://github.com/yasir723/node-ekle/assets/111686779/11d4aac8-b0d4-4762-b028-17d29fada8d1" width="600">
</div>

Yukarıdaki binary ağaçtan düğümler silme işlemi yapacağız
##### Soru 1: 4 değeri olan düğümü silme işlemi gerçekleştirin
bu durum yukarıdaki işleyişin 4. maddesinde ilk durum olarak tanımlanır (sol alt ağaç boşsa, sağ alt ağacı geri döner) ve silme işlemi yaptıktan sonra sağ alt ağacın düğümü sileceğimiz düğümün yerine gelecektir 


### Soru 1: 4 Değeri Olan Düğümü Silme İşlemi

Bu durum, ağacın 4. maddesinde belirtildiği gibi ele alınacaktır: "Eğer aranan değer, kök düğümün değerine eşitse, bu durumda silme işlemi gerçekleştirilir."

- İlk olarak, ağaçtaki düğümler şu şekildedir:

        9
       / \
      7   12
     / \  / \
    6   8 11 14
   / \    / / \
  3   4  10 13 15
       \
        5

- Silme işlemi için 4 değerine sahip düğümü bulmalıyız. 4, 7 düğümünün sağ alt ağacında yer alır.
- Sağ alt ağacın sol altında herhangi bir düğüm bulunmadığı için (sol alt ağaç boşsa), 4 değeri olan düğümü sileceğiz.
- Silme işlemi sonrasında sağ alt ağaç şu hale gelecektir:

        9
       / \
      7   12
     / \  / \
    6   8 11 14
   / \    / / \
  3   5  10 13 15

Bu şekilde, 4 değerine sahip düğüm başarıyla silinmiş olacaktır.



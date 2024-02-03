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

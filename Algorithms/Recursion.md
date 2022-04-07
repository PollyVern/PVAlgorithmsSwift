# Рекурсия

<p align="center">
<img src="https://github.com/PollyVern/ContentForRepositories/blob/main/Algorithms/%20RecursionPicture.png">
</p>

## Упражнения из книги "Грокаем алгоритмы"
### Упражнение 4.1 (стр. 85)

__Вопрос:__ Код для функции sum.

__Ответ:__

```SWIFT
func sum(array: [Int]) -> Int {
    if array == [] {
        return 0
    }
    
    var tempArray = array
    tempArray.remove(at: 0)
    return array[0] + sum(array: tempArray)
}

print(sum(array: [1, 2, 3, 4])) // 10
```

### Упражнение 4.2 (стр. 85)
__Вопрос:__ Напишите рекурсивную функцию для подсчета элементов в списке.

__Ответ:__

```SWIFT
func count(array: [Int]) -> Int {
    if array == [] {
        return 0
    }
    
    var tempArray = array
    tempArray.remove(at: 0)
    return 1 + count(array: tempArray)
}

print(count(array: [1, 2, 3, 4])) // 4

```

### Упражнение 4.3 (стр. 85)
__Вопрос:__ Найдите наибольшее число в списке.

__Ответ:__

```SWIFT
func max(list : [Int]) -> Int {
    if list.count == 2 {
        return (list[0] > list[1]) ? list[0] : list[1]
    } else if list.count < 2 {
        return list.first ?? 0
    }
    
    var tempArray = list
    tempArray.remove(at: 0)
    let subMax = max(list: tempArray)
    return (list[0] > subMax) ? list[0] : subMax
}

print(max(list: [1, 5, 25, 16])) // 25
```

#  Сортировка выбором
## Пример алгоритма из книги "Грокаем алгоритмы"
```SWIFT
func selectionSort(array: [Int]) -> [Int] {
    guard array.count > 1 else { return array }
    
    var newArray = [Int]()
    var mutableArray = array
    
    for _ in 0..<mutableArray.count {
        let smallestIndex = findSmallest(array: mutableArray)
        newArray.append(mutableArray.remove(at: smallestIndex))
    }
    return newArray
}

private func findSmallest(array: [Int]) -> Int {
    var smallest = array[0]
    var smallestIndex = 0
    for i in 0..<array.count-1 {
        if array[i] < smallest {
            print("\(array[i]) - \(smallest)")
            smallest = array[i]
            smallestIndex = i
        }
    }
    return smallestIndex
}

selectionSort(array: [5,3,6,2,10]) // [2,3,5,6,10]
```

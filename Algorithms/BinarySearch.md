#  Бинарный поиск

<p align="center">
<img src="https://github.com/PollyVern/ContentForRepositories/blob/18473c5c205a39c06d0d8f6af9cab21ffa8f3747/Algorithms/BinarySearchPicture.png">
</p>

## Применение
Бинарный поиск рассматривается, когда нужно:
* искать индекс
* искать элемент коллекции

## Этапы
1. __Предварительная обработка__ - коллекция обязательно должна быть отсортирована.
2. __Бинарный поиск__ - использование цикла или рекурсии для разделения пространства поиска пополам после каждого сравнения.
3. __Постобработка__ - определение жизнеспособных кандидатов в оставшемся пространстве.

## Шаблон 1
Используется для поиска элемента или условия, которое можно определить, получив доступ к одному индексу в массиве.

```SWIFT
func binarySearch(sortArray: [Int], searchNumber: Int) -> Any {
    var low = 0
    var high = sortArray.count-1
    while low <= high {
        let mid = (low + high)/2
        let guess = sortArray[mid]
        if guess == searchNumber {
            return "Число \(mid) найдено"
        } else if guess > searchNumber {
            high = mid - 1
        } else {
            low = mid + 1
        }
    }
    return "Число \(searchNumber) не найдено"
}

binarySearch(sortArray: [0,1,2,3,4,5,6,7,8], searchNumber: 8) //Число 8 найдено
binarySearch(sortArray: [0,1,2,3,4,5,6,7,8], searchNumber: 9) //Число 9 не найдено
```

## Шаблон 2
Используется для поиска элемента или условия, которое требует доступа к текущему индексу и индексу его ближайшего правого соседа в массиве.
```SWIFT
func binarySearch(nums: [Int], target: Int) -> Int {
    if nums.isEmpty || nums.count == 0 {
        return -1
    }
    
    var left = 0
    var right = nums.count-1
    while left < right {
        let mid = left + (right - left) / 2
        if nums[mid] == target {
            return mid
        } else if nums[mid] < target {
            left = mid + 1
        } else {
            right = mid
        }
    }

    if left != nums.count && nums[left] == target {return left}
    return -1
}

binarySearch(nums: [0,2,4,6,7], target: 2) //1
```

## Шаблон 3
Используется для поиска элемента или условия, которое требует доступа к текущему индексу и его непосредственному индексу левого и правого соседа в массиве.
```SWIFT
class Solution {
    
    func searchRange(_ nums: [Int], _ target: Int) -> [Int] {
        
        var low = 0
        var high = nums.count-1
        
        if nums.isEmpty {
            return [-1,-1]
        }
        
        if nums[0] == target {
            return identicalIndexTarget(nums, target, 0)
        } else {
            while low <= high {
                let mid = low + (high - low)/2
                let guess = nums[mid]
                
                if guess == target && nums[mid-1] < target{
                    return identicalIndexTarget(nums, target, mid)
                } else if guess < target {
                    low = mid + 1
                } else {
                    high = mid - 1
                }
            }
        }

        return [-1,-1]
    }
    
    private func identicalIndexTarget(_ nums: [Int], _ target: Int, _ mid: Int) -> [Int] {
        var indexArray = [Int]()
        
        for i in mid...nums.count-1 {
            if nums[i] == target {
                indexArray.append(i)
            } else {
                break
            }
        }
        
        if indexArray.count == 1 {
            indexArray.append(indexArray[0])
        } else if indexArray.count > 2 {
            var newIndexArray = [Int]()
            newIndexArray.append(indexArray[0])
            newIndexArray.append(indexArray.last!)
            return newIndexArray
        }
        
        return indexArray
    }
}
```

## Упражнения из книги "Грокаем алгоритмы"
### Упражнение 1.1 (стр.27)
__Вопрос:__ Имеется отсортированный список из 128 имен, и вы ищите в нем значение методом бинарного поиска. Какое максимальное количество проверок для этого может потребоваться?

__Ответ:__ 7 проверок, так как log128 = 7

### Упражнение 1.2 (стр.28)
__Вопрос:__ Предположим, размер списка увеличился вдвое (256 имен). Как изменится максимальное количество проверок?

__Ответ:__ 8 проверок, так как log256 = 8



## Несколько задач с [Leetcode](https://leetcode.com/PollyVern/)

### 35. Search Insert Position 
```SWIFT
class Solution {
    func searchInsert(_ nums: [Int], _ target: Int) -> Int {
        var lowIndex = 0
        var highIndex = nums.count-1

        while lowIndex <= highIndex {
            let midIndex = (lowIndex + highIndex)/2
            let guess = nums[midIndex]
            if guess == target {
                return midIndex
            } else if guess > target {
                highIndex = midIndex - 1
            } else {
                lowIndex = midIndex + 1
            }
        }

        return lowIndex
    }
}

Solution().searchInsert([1,3,5,6], 7) //4
Solution().searchInsert([1,3,5,6], 2) //1
Solution().searchInsert([1,3,5,6], 5) //2
```
### 69. Sqrt(x)
```SWIFT
class Solution {
    func mySqrt(_ x: Int) -> Int {
        var lowIndex = 0
        var highIndex = x

        while lowIndex < highIndex {
            let midIndex = (lowIndex + highIndex + 1)/2
            if midIndex * midIndex <= x {
                lowIndex = midIndex
            } else {
                highIndex = midIndex - 1
            }
        }
        return lowIndex
    }
}

Solution().mySqrt(2) //1
Solution().mySqrt(3) //1
Solution().mySqrt(5) //2
Solution().mySqrt(10) //3
```
### 33. "Search in Rotated Sorted Array"
```SWIFT
class Solution {
    func search(_ nums: [Int], _ target: Int) -> Int {
        
        if nums.count == 1 {
            return nums[0] == target ? 0 : -1
        }
        
        var lowIndex = searchPivotIndex(nums, target).lowIndex
        var highIndex = searchPivotIndex(nums, target).highIndex
                
        while lowIndex <= highIndex {
            let middleIndex = lowIndex + (highIndex - lowIndex)/2

            if nums[middleIndex] == target {
                return middleIndex
            } else if nums[middleIndex] > target {
                highIndex = middleIndex - 1
            } else {
                lowIndex = middleIndex + 1
            }
        }
        return -1
    }
    
    private func searchPivotIndex(_ nums: [Int], _ target: Int) -> (lowIndex: Int, highIndex: Int) {
        
        var lowIndex = 0
        var highIndex = nums.count-1
        
        while lowIndex < highIndex {
            let midIndex = lowIndex + (highIndex - lowIndex)/2
            
            if nums[midIndex] > nums[highIndex] {
                lowIndex = midIndex + 1
            } else {
                highIndex = midIndex
            }
        }

        let pivotIndex = lowIndex

        lowIndex = 0
        highIndex = nums.count - 1
        
        if nums[pivotIndex] <= target && target <= nums[highIndex] {
            lowIndex = pivotIndex
        } else {
            highIndex = pivotIndex
        }
        
        return (lowIndex, highIndex)
    }
}

```

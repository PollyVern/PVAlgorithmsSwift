#  Бинарный поиск

## Пример алгоритма из книги "Грокаем алгоритмы"
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


## Упражнения из книги "Грокаем алгоритмы"
### Упражнение 1.1 (стр.27)
__Вопрос:__ Имеется отсортированный список из 128 имен, и вы ищите в нем значение методом бинарного поиска. Какое максимальное количество проверок для этого может потребоваться?

__Ответ:__ 7 проверок, так как log128 = 7

### Упражнение 1.2 (стр.28)
__Вопрос:__ Предположим, размер списка увеличился вдвое (256 имен). Как изменится максимальное количество проверок?

__Ответ:__ 8 проверок, так как log256 = 8



## Мои решенные задачи с [Leetcode](https://leetcode.com/PollyVern/)
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

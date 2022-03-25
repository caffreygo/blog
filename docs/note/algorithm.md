# JavaScript数据结构和算法

## 数据结构

### 双端队列

```javascript
class Deque {
    constructor() {
        this.count = 0;
        this.lowestCount = 0;
        this.items = {};
    }
    addBack(element) {
        this.items[this.count] = element;
        this.count++;
    }
    addFront(element) {
        if (this.isEmpty()) {
            this.addBack(element);
        } else if (this.lowestCount > 0) {
            this.lowestCount--;
            this.items[this.lowestCount] = element;
        } else {
            // lowestCount = 0,全部后移一步
            for (let i = this.count; i > 0; i--) {
                this.items[i] = this.items[i -1];
            }
            this.count++;
            this.lowestCount = 0;
            this.items[0] = element;
        }
    }
    removeFront() {
        if (this.isEmpty()) {
            return undefined;
        }
        const result = this.items[this.lowestCount];
        delete this.items[this.lowestCount];
        this.lowestCount++;
        return result;
    }
    peekFront() {
        if (this.isEmpty()) {
            return undefined;
        }
        return this.items[this.lowestCount];
    }
    isEmpty() {
        return this.count - this.lowestCount === 0;
    }
    size() {
        return this.count - this.lowestCount;
    }
}
```

### 字典和散列表

::: tip 概念

在字典Dictionary（或映射Map）中，我们用[键，值]对的形式来存储数据。

在散列表中也是一样（也是以[键，值]对的形式来存储数据）。

但是两种数据结构的实现方式略有不同，例如字典中的每个键只能有一个值

:::

#### 散列表HashTable

散列表的创建需要一个hash函数生成键，即散列函数

```javascript
loseloseHashCode(key) {
  if (typeof key === 'number') {
    return key;
  }
  const tableKey = this.toStrFn(key);
  let hash = 0;
  for (let i = 0; i < tableKey.length; i++) {
    hash += tableKey.charCodeAt(i);
  }
  return hash % 37;
}

hashCode(key) {
  return this.loseloseHashCode(key);
}

// 更好的散列函数可以降低冲突
djb2HashCode(key) {
  const tableKey = this.toStrFn(key);
  let hash = 5381;
  for (let i = 0; i < tableKey.length; i++) {
    hash = (hash * 33) + tableKey.charCodeAt(i);
  }
  return hash % 1013;
}
```

有时候，一些键会有相同的散列值。不同的值在散列表中对应相同位置的时候，我们称其为冲突。

::: tip 处理冲突有几种方法：

- 分离链接：包括为散列表的每一个位置创建一个**链表**并将元素存储在里面。它是解决冲突的最简单的方法，但是在HashTable实例之外还需要额外的存储空间

- 线性探查：将元素直接存储到表中，而不是在单独的数据结构中

  线性探查技术分为两种。第一种是软删除方法。我们使用一个特殊的值（标记）来表示键值对被删除了（惰性删除或软删除），而不是真的删除它。经过一段时间，散列表被操作过后，我们会得到一个标记了若干删除位置的散列表。这会逐渐降低散列表的效率，因为搜索键值会随时间变得更慢。能快速访问并找到一个键是我们使用散列表的一个重要原因。

  第二种方法需要检验是否有必要将一个或多个元素移动到之前的位置。当搜索一个键的时候，这种方法可以避免找到一个空位置。如果移动元素是必要的，我们就需要在散列表中挪动键值对。

- 双散列

:::

## 排序和搜索算法

### 冒泡排序

::: tip 冒泡排序
* 冒泡排序是比较相邻的两个项，如果第一个比第二个大，则交换它们。
* 元素项向上移动至正确的顺序，就好像气泡升至表面一样，冒泡排序因此而得名。
* 冒泡排序可能是所有排序算法中最简单的，但从运行时间的角度而言，冒泡排序是最差的一个。

::: 

```js
function toggleItem(array, index1, index2) {
    [array[index1], array[index2]] = [array[index2], array[index1]];
}
function bubbleSort(arr) {
    const { length } = arr
    for (let i = 0; i < length; i++) {
        // 每一次外循环之后，都能确定一个最大值
        for (let j = 0; j < length - 1 - i; j++) {
            // 每次内循环，间隔对比找到最大的值，放到后面
            // 如果前者比后者大，调换位置达到从小到大的效果
            if (arr[j] > arr[j + 1]) toggleItem(arr, j, j + 1)
        }
    }
    return arr
}
```

### 选择排序

::: tip 选择排序

  * 选择排序算法是一种原址比较排序算法。
  * 选择排序大致的思路是找到数据结构中的最小值并将其放置在第一位，接着找到第二小的值将其放在第二位，以此类推。

::: 

```js
function selectSort(arr) {
    const { length } = arr
    let minIndex;
    for (let i = 0; i < length; i++) {
        minIndex = i;
        // 每次内循环，遍历对比找到最小值的索引，所以每次都能确定一个最小值
        for (let j = i + 1; j < length; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j
            }
        }
        // 如果找到比当前开始数值更小的索引，交换位置
        if (minIndex !== i) {
            toggleItem(arr, i, minIndex)
        }
    }
    return arr
}
```

### 插入排序

如果要将`[1,2,3,0]`数组当中的0移动到第一个位置，我们需要设置一个变量`temp`保存`arr[3]`；

然后从右向左遍历将所有数组项的索引右移一位，最后把`0temp赋值给`arr[0]`即可。

```js
const arr = [1,2,3,0];
let i = arr.length - 1;
let temp = arr[i];  // 0
while(i>0) {
    arr[i] = arr[i-1];
    i--;
}
arr[0] = temp;
console.log(arr);  // [0, 1, 2, 3]
```

插入排序每次排一个数组项，以此方式构建最后的排序数组。

```js
function insertSort(array) {
    const {
        length
    } = array
    let temp;

    for (let i = 1; i < length; i++) {
        let j = i;
        temp = array[j];
        while (j > 0 && array[j - 1] > temp) {
            array[j] = array[j - 1]
            j--;
        }
        array[j] = temp;
    }
    return array;
}
```

**注意**：在排序小型数组时，此算法比选择排序和冒泡排序性能要好

### 归并排序

📗 归并排序是第一个可以实际使用的排序算法，我们之前的三种算法性能不是特别的好，但归并排序性能不错，在`JavaScript`中，`Array.prototype.sort()`方法，`ECMAScript`并没有定义使用哪种排序算法，而是交给浏览器厂商自己去实现，而对于谷歌`V8引擎`，其使用了快速排序的变体；在`Firefox`浏览器中，则是使用了归并排序。

#### 实现

![](./img/mergeSort.png)

首先，假设我们有两个已经是排序过的数组，实现一个将这两个数组合并成一个的`merge`方法:

```js
function merge(left, right) {
    let i = 0;
    let j = 0;
    // 需要一个额外的数组空间保存结果
    const result = [];
    // 当left和right都还有未遍历项时
    while (i < left.length && j < right.length) {
        // 找到left和right当中的最小一项push到result,然后索引自增1
        result.push(left[i] > right[j] ? right[j++] : left[i++]);
    }
    // left如果已经遍历完, 将right连接到result,反之将left的剩余项连接到result
    // result.concat(i < left.length ? left.slice(i) : right.slice(j))
    return result.concat(i == left.length ? right.slice(j) : left.slice(i))
    
}

console.log(merge([1, 2], [0, 4]));  // [0, 1, 2, 4]
console.log(merge([2, 3, 5], [0, 4]));  // [0, 2, 3, 4, 5]
console.log(merge([1], [0]));  // [0, 1] 
```

归并排序是一种分而治之的算法，其思想是将原始数组切分为较小的数组，直到每个小数组只有一个位置，接着将小数组归并成较大的数组，直到最后只有一个排序完毕的大数组。

```js
function mergeSort(array) {
    if (array.length > 1) {
        const { length } = array
        const middle = Math.floor(length / 2)
        const left = mergeSort(array.slice(0, middle))
        const right = mergeSort(array.slice(middle, length))
        array = merge(left, right)
    }
    return array
}

const result = mergeSort([8, 7, 6, 5, 4, 3, 2, 1])
console.log(result) // [1, 2, 3, 4, 5, 6, 7, 8]
```

#### 总结

- 归并排序是**稳定**排序，它也是一种十分高效的排序，能利用完全二叉树特性的排序一般性能都不会太差。从上文的图中可看出，每次合并操作的平均时间复杂度为O(n)，而完全二叉树的深度为|log2n|。总的平均时间复杂度为O(nlogn)。而且，归并排序的最好，最坏，平均时间复杂度均为O(nlogn)。
-  归并的空间复杂度就是那个临时的数组和递归时压入栈的数据占用的空间：n + logn；所以空间复杂度为: O(n)

### 快速排序

📗 快速排序也许是最常用的排序算法了。它的复杂度为O(nlog(n))，且性能通常比其他复杂度为O(nlog(n))的排序算法要好。和归并排序一样，快速排序也使用**分而治之**的方法，将原始数组分为较小的数组（但它没有像归并排序那样将它们分割开）。

::: tip 快速排序的思想很简单，整个排序过程只需要三步：

- 在数据集之中，选择一个元素作为"基准"（pivot）。
- 所有小于"基准"的元素，都移到"基准"的左边；所有大于"基准"的元素，都移到"基准"的右边。
- 对"基准"左边和右边的两个子集，不断重复第一步和第二步，直到所有子集只剩下一个元素为止。

::: 

#### 基本实现

```js
function quickSort(arr) {
    if (arr.length <= 1) { return arr; }
    var pivotIndex = Math.floor(arr.length / 2);
    var pivot = arr.splice(pivotIndex, 1)[0];
    var left = [];
    var right = [];
    for (var i = 0; i < arr.length; i++){
        if (arr[i] < pivot) {
            left.push(arr[i]);
        } else {
            right.push(arr[i]);
        }
    }
    return quickSort(left).concat([pivot], quickSort(right));
};
```

#### 双指针

```js
function quickSort(array, left, right) {
    let index;
    if (array.length > 1) {
        index = partition(array, left, right);
        if (left < index - 1) {
            quickSort(array, left, index - 1);
        }
        if (index < right) {
            quickSort(array, index, right);
        }
    }
    return array;
};

function partition(array, left, right) {
    const pivot = array[Math.floor((right + left) / 2)];
    let i = left;
    let j = right;

    while (i <= j) {
        while (array[i] < pivot) {
            i++;
        }
        while (array[j] > pivot) {
            j--;
        }
        if (i <= j) {
            toggleItem(array, i, j)
            i++;
            j--;
        }
    }
    return i;
}

const array = [9, 6, 7, 8, 2, 3, 5, 1]
console.table(quickSort(array, 0, array.length - 1))
```

### 计数排序

📗 计数排序是我们学到的第一个**分布式**排序，分布式排序使用已组织好的辅助数据结构，然后进行合并，得到排好序的数组。计数排序使用一个用来存储每个元素在原始数组中出现次数的临时数组，在所有元素都计数完完成后，临时数组已排好序并可迭代已构建排序后的结果数组。

计数排序是一种用来**排序整数**优秀的算法，它的时间复杂度非常简单，但其额外引入了辅助数据结构从而需要**更多的内存空间**。

```js
function countingSort(array) {
    if (array.length < 2) {
        return array
    }
    const maxValue = findMaxValue(array)
    const counts = new Array(maxValue + 1)
    array.forEach(item => {
        if (!counts[item]) {
            counts[item] = 0
        }
        counts[item]++
    })
    let sortIndex = 0
    counts.forEach((item, index) => {
        while (item > 0) {
            array[sortIndex++] = index
            item--
        }
    })
    return array
}
function findMaxValue(array) {
    let max = array[0]
    for (let index = 1; index < array.length; index++) {
        if (array[index] > max) {
            max = array[index]
        }
    }
    return max
}

const result = countingSort([5, 4, 3, 2, 1])
console.log(result) // [1, 2, 3, 4, 5]
```

### 顺序搜索

📗 顺序搜索(线性搜索)是最基本的搜索算法，它的机制是，将每一个数据结构中的元素和我们要找的元素做比较，一直到找到位置。顺序搜索是最低效的一种搜索算法。

```js
function sequentSearch (array, value) {
    let result = -1
    for(let index = 0; index < array.length; index++) {
        if (array[index] === value) {
            result = index
            return
        }
    }
}
```

![](./img/sequentSearch.png)

### 二分搜索

📗 二分搜索算法的原理和猜数字游戏类似，假设有1-100的数，一个人猜，另一个人只需要回答高了还是低了，一直到找到这个数位置。

二分搜索算法对数据结构有一定的要求，它首先要求数据结构已经是**排好序**的，其次它还要遵守如下的规则：

::: 二分搜索

1. 首先选择数组的中间值。

2. 如果选中的值是待搜索的值，那么停止搜索。

3. 如果待搜索的值比选中的值要小，则返回步骤1并在选中值左边的子数组中查找。

4. 如果待搜索的值比选中的值要大，则返回步骤1并在选中值的右边的子数组中查找。


::: 

```js
function binarySearch (array, value) {
    array.sort()
    let low = 0
    let high = array.length - 1
    while (low <= high) {
        const mid = Math.floor((low + high) / 2)
        const element = array[mid]
        if (value === element) {
            return true
        } else if (value < element) {
            high = mid - 1
        } else {
            low = mid + 1
        }
    }
    return false
}
console.log(binarySearch([8, 7, 6, 5, 4, 3, 2, 1], 2))  // true
```

代码分析：为了进一步简单化，我们使用了内置的`Array.prototype.sort()`方法来进行排序，也可以使用我们之前学到的任何排序算法来替换。

以下是二分搜索算法的搜索示意图：

![](./img/binarySearch.png)

## 二叉树

::: tip 二叉树的遍历

- 前序遍历：若二叉树为空，则空操作返回，否则**先访问根结点**，然后前序遍历左子树，再前序遍历右子树。
- 中序遍历：若树为空，则空操作返回，否则从根结点开始（注意并不是先访问根结点)，中序遍历根结点的左子树，**然后访问根结点**，最后中序遍历右子树。
- 后序遍历：若树为空，则空操作返回，否则从左到右先叶子后结点的方式遍历访问左右子树，**最后访问根结点**。

:::

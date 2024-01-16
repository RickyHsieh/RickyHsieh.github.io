---
title: Daily Leetcode - 380. Insert Delete GetRandom O(1)
description: Medium 
date: 2024-01-16 12:00:00+0000
categories:
    - Math
---

##  2024 Jan LC challenge

### 題目  380. Insert Delete GetRandom O(1)

### 方法

Implement the RandomizedSet class:

* RandomizedSet() Initializes the RandomizedSet object.

* bool insert(int val) Inserts an item val into the set if not present. Returns true if the item was not present, false otherwise.

* bool remove(int val) Removes an item val from the set if present. Returns true if 
the item was present, false otherwise.

* int getRandom() Returns a random element from the current set of elements (it's guaranteed that at least one element exists when this method is called). Each element must have the same probability of being returned.


### My Code

#### 方法一

```java
import java.util.*;

public class RandomizedSet {
    private Map<Integer, Integer> map; // 將值映射到其在數組中的索引
    private List<Integer> list; // 存儲元素
    private Random rand; // 用於生成隨機數

    public RandomizedSet() {
        map = new HashMap<>();
        list = new ArrayList<>();
        rand = new Random();
    }

    public boolean insert(int val) {
        if (map.containsKey(val)) {
            return false; // 元素已存在
        }
        map.put(val, list.size());
        list.add(val);
        return true;
    }

    public boolean remove(int val) {
        if (!map.containsKey(val)) {
            return false; // 元素不存在
        }
        int index = map.get(val);
        int lastElement = list.get(list.size() - 1);
        list.set(index, lastElement); // 與最後一個元素交換
        map.put(lastElement, index); // 更新交換元素的索引
        list.remove(list.size() - 1); // 移除最後一個元素
        map.remove(val); // 從映射中移除
        return true;
    }

    public int getRandom() {
        return list.get(rand.nextInt(list.size()));
    }
}

```

#### 問題

##### Q1 map.put(val, list.size());為何 ?

目的在於將新加入List的元素，將它的index，記錄在HashMap中，HashMap儲存該值以及其所引。
當我們添加一個新元素時會加在List尾巴，所以list.size()的由來就是這樣。
如此一來我們添加新元素進list時保持O(1)。

##### Q2 remove 方法在O(1) ?

關鍵在於，要刪除點與最後一個元素交換，可以把時間保持O(1)；

```java
list.set(index, lastElement); // 與最後一個元素交換
map.put(lastElement, index); // 更新交換元素的索引
```
因為我們在List、Array刪除元素時，假設是在中間刪除，那它後面的元素都要往前挪動，造成時間複雜度為O(n)。

而直接跟最後一個數交換，頂多O(1)。

再來更新map元素索引，因為最後一個元素被移動到了一個新的位置（即原來要刪除的元素的位置）。 因此，需要在 map 中更新這個元素的索引。

map 中儲存了每個元素及其在 list 中的索引。 由於 lastElement 的位置已經改變，其索引也必須相應更新。

### 方法二

Dynamic array，動態Array擴容策略
```java
class RandomizedSet {
    private final Random random = new Random();
    private final Map<Integer, Integer> map = new HashMap<>();
    private int[] vals = new int[32];
    private int i = 0;

    public RandomizedSet() {
        
    }
    
    public boolean insert(int val) {
        Integer added = map.putIfAbsent(val, i);
        if (added != null) return false;

        if (i >= vals.length) {
            vals = Arrays.copyOf(vals, vals.length * 2);
        }
        vals[i++] = val;
        return true;
    }
    
    public boolean remove(int val) {
        //從 map 中移除元素 val，如果該元素存在，則傳回其在數組 vals 中的索引。
        Integer removed = map.remove(val);
        if (removed == null) return false; //不存在

        if (removed < i - 1) {
            vals[removed] = vals[i-1];
            map.put(vals[i-1], removed);
        }
        i--;
        return true;
    }
    
    public int getRandom() {
        int index = random.nextInt(i);
        return vals[index];
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```

* `map.putIfAbsent(key, value)` :

    如果它不存在則放置，如果存在返回該已存在key的value。
    在這裡的解釋為 : 如果 val 已經存在，putIfAbsent 方法將傳回已存在元素的索引，否則傳回 null。

    if (added != null) return false;: 如果 val 已經存在於雜湊表中，方法傳回 false。
    if (i >= vals.length) { vals = Arrays.copyOf(vals, vals.length * 2); }:

    如果陣列 vals 沒有足夠空間儲存新元素，則將其容量擴大兩倍。
    vals[i++] = val;: 將新元素儲存在陣列 vals 中，並增加索引 i。
    傳回 true 表示插入成功。

* remove
    如果被移除的元素不是陣列中的最後一個元素，則將最後一個元素移至被移除元素的位置，並更新雜湊表中該元素的索引。
    i--;: 減少數組 vals 中的元素計數。
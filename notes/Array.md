# Array
---
## 1. 基本概念 (Array Basics)

- **陣列 (array)：** 連續記憶體位置中的元素集合。
- **特性：**
  - 固定大小 (Fixed size)  
  - 隨機存取 (Random access)，透過索引 (index) 可直接存取，時間複雜度 O(1)  
  - 元素型別一致 (Same data type)，利於效率與儲存  

---

## 2. 靜態與動態陣列 (Static array & Dynamic array)

- **靜態陣列 (Static array)**：
  - 固定長度陣列 (Fixed-length array)
  - 元素數量在編譯時確定，無法改變

- **動態陣列 (Dynamic array)**：
  - 可變長度陣列 (Variable-length array)
  - 元素數量可於執行期 (runtime) 變動，需使用 `malloc` / `realloc`
  - 使用完畢後需釋放記憶體 (`free`)

---

### 🔹 動態陣列範例 (C語言)

#### 宣告
```c
int *array;                                       // 宣告指標作為陣列開頭
int n = 10;                                       // 陣列大小
array = (int*) malloc(n * sizeof(int));           // 配置連續記憶體空間
```

#### 初始化
```c
for (int i = 0; i < n; i++) {
    array[i] = 0;                                 // 將每個元素設為 0
}
```

#### 輸出
```c
for (int i = 0; i < n; i++) {
    printf("%d ", array[i]);                      // 輸出每個元素
}
```

#### 調整大小
```c
n = n * 2;                                        // 擴大陣列容量
array = (int*) realloc(array, n * sizeof(int));   // 重新配置記憶體

for (int i = n/2; i < n; i++) {
    array[i] = 0;                                 // 初始化新增部分
}
```

#### 釋放空間
```c
free(array);
```

---

## 3. 排序 (Sorting)

- 目標：將陣列由小到大排序。
- 常見方法：

### 氣泡排序 (Bubble Sort)
- 原理：相鄰兩元素互相比較，若順序錯誤則交換，重複直到排序完成。  
- **時間複雜度：** O(n²)  
- **最佳情況 (已排序)：** Ω(n)  
- **平均：** Θ(n²)

```c
void bubbleSort(int A[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (A[j] > A[j + 1]) {
                int temp = A[j];
                A[j] = A[j + 1];
                A[j + 1] = temp;
            }
        }
    }
}
```

---

### 選擇排序 (Selection Sort)
- 原理：每次找到最小值，與目前未排序區的最前面交換。  
- **時間複雜度：** O(n²)  
- **最佳 / 平均 / 最差：** Θ(n²)

```c
void selectionSort(int A[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (A[j] < A[minIndex])
                minIndex = j;
        }
        int temp = A[i];
        A[i] = A[minIndex];
        A[minIndex] = temp;
    }
}
```

---

### 插入排序 (Insertion Sort)
- 原理：從第二個元素開始，逐一將右側未排序區的元素插入到左側已排序區的正確位置。  
- **時間複雜度：** O(n²)  
- **最佳情況 (幾乎已排序)：** Ω(n)  
- **平均：** Θ(n²)

```c
void insertionSort(int A[], int n) {
    for (int i = 1; i < n; i++) {
        int key = A[i];
        int j = i - 1;
        while (j >= 0 && A[j] > key) {
            A[j + 1] = A[j];
            j--;
        }
        A[j + 1] = key;
    }
}
```

---

## 4. 優缺點 (Pros & Cons)

| 項目 | 優點 | 缺點 |
|------|------|------|
| 記憶體配置 | 連續配置，存取快 | 無法動態擴展（靜態） |
| 存取效率 | 隨機存取 O(1) | 插入刪除 O(n) |
| 空間效率 | 結構簡單，無額外指標 | 無法釋放部分空間 |
| 可預測性 | 固定索引、快取命中率高 | 大量搬移資料成本高 |
| 動態版本 | 可彈性擴充 | 使用 malloc / realloc 較耗時 |

---

## 5. 抽象資料型態 (ADT: Array)

```
ADT Array is
  objects:
    一組 <index, value> 的配對，index 屬於有限整數集合。
  functions:
    Create(size)          建立固定長度陣列
    Retrieve(A, i)        取得第 i 個元素
    Store(A, i, x)        將第 i 個元素設為 x
    Insert(A, i, x)       在第 i 個位置插入新值 (需搬移)
    Delete(A, i)          刪除第 i 個元素 (需搬移)
    Traverse(A)           依序訪問每個元素
    Resize(A, new_size)   調整大小 (僅動態陣列)
end
```

---

## 6. 時間複雜度與實作摘要 (Time Complexity & Summary)

| 操作 | 時間複雜度 | 備註 |
|------|-------------|------|
| Access | O(1) | 直接以索引取值 |
| Search | O(n) / O(log n) | 未排序為線性、排序可用二分搜尋 |
| Insert | O(n) | 搬移元素 |
| Delete | O(n) | 搬移元素 |
| Traverse | O(n) | 訪問所有元素 |
| Resize (Dynamic) | O(n) | 重新配置記憶體 |

---


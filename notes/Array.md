# Array
---
## 1.基本概念 (Array Basics)

- **陣列 (array) :** 連續記憶體位置中的元素集合。
- **特性 :**
  - 固定大小 (Fixed size)  
  - 隨機存取 (Random access)，透過索引 (index) 可直接存取，時間複雜度 O(1)  
  - 元素型別一致 (Same data type)，利於效率與儲存  
---

## 2. 靜態與動態陣列(Static array & Dynamic array)

- **靜態陣列 (Static array)**：
  - 固定長度陣列(Fix-length array)
  - 元素數量在編譯時確定，無法改變

- **動態陣列 (Dynamic array)**：
  - 可變長度陣列(Variable-length array)
  - 元素數量可於執行期 (runtime) 變動，需使用 `malloc` / `realloc`。
  - 使用完畢後需釋放記憶體，使用 `free`。
    
- **動態陣列執行範例**
  - 宣告 
  ```c
  int *array;                                         //宣告陣列記憶體起始位置
  int n = 10;                                         //設定陣列大小
  array = (int*) malloc(n * sizeof(int));             //配置array向後 n*sizeof(int)的記憶體空間，並以每(int*)為單位
  ```
  - 初始化
  ```c
  for(int i = 0; i < n; i++) {
    array[i] = 0;                                     //設定所有element為0
  }
  ```
  - 輸出
  ```c
  for (int i = 0; i < n; i++) {
    printf("%d ", array[i]);                         //從i為0開始，輸出array中的element
  }
  ```
   - 調整大小
  ```c
  n = n * 2;                                        //將原先設定的element數量n變為兩倍大小
  array = (int *) realloc(array, n * sizeof(int));  //重新配置array向後 n*sizeof(int)的記憶體空間，並以每(int*)為單位  !!若空間不足將重新分配記憶體位置，若空間足夠則會從原先記憶體位置延長
  for (int i = n/2; i < n; i++) {
    array[i] = 0;                                   //新初始化array[n]以後，新增出來的陣列element為0
  }
  ```
     - 釋放空間
  ```c
  free(array);
  ```
---
## 3. 排序 (Sorting)

- 目標：將陣列由小到大排序。
- 方法：
  - 氣泡排序 (Bubble Sort)
    - 由前往後依序將兩兩相鄰的值互相比較，直到所有的值都被排到正確的位置為止。
    - 時間複雜度(Time Complexity)：O(n²) 、 Ω(n) 、 Θ(n²)
      
  - 選擇排序 (Selection Sort)
    - 每次都從陣列中尋找最小值，放到未被排序區的最前面。
    - 時間複雜度(Time Complexity)：O(n²) 、 Ω(n²) 、 Θ(n²)
      
  - 插入排序 (Insertion Sort)
    - 依照順序，從第二個元素開始，將右側未排序區域的元素向左插入到已排序區域。
    - 時間複雜度(Time Complexity)：O(n²) 、 Ω(n) 、 Θ(n²)
---

## 4. 優缺點 (Pros & Cons) 建設中．．．
- 優點：
  - 快速隨機存取 (O(1))。
  - 適合靜態資料。
- 缺點：
  - 插入 / 刪除成本高 (需位移大量元素)。
  - 動態擴充需重新配置記憶體。



















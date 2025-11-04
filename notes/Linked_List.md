# Linked List — Study Notes

## 1. Definition
- Linked List 是一種**線性資料結構 (linear data structure)**。
- 節點之間以**指標 (pointer)** 連結，而不是像陣列一樣連續儲存。
- 每個節點 (node) 包含兩個部分：
  - **Data**：實際的資料內容
  - **Next**：指向下一個節點的指標
- 最後一個節點的 Next 會指向 `NULL`，表示串列結束。
- Linked List 可以**動態調整大小**，支援在執行期間新增與刪除節點。
- 常見應用：Stack、Queue、Hash Table chaining、音樂播放清單、Undo 功能等。

---

## 2. Visualization

```
Head → [ 10 | * ] → [ 20 | * ] → [ 30 | NULL ]
```

- Head：指向串列的第一個節點。
- 每個節點都儲存一筆資料與下一個節點的位址。
- 若 head = NULL，代表串列為空。

### 類型 (Types)
1. **Singly Linked List**：
   - 單向鏈結，每個節點只有 `next` 指標。
2. **Doubly Linked List**：
   - 雙向鏈結，每個節點有 `prev` 和 `next` 指標。
3. **Circular Linked List**：
   - 環狀結構，最後一個節點的 next 會指回 head。

---

## 3. Characteristic
- 節點儲存在**非連續記憶體**位置。
- 串列長度可**動態變化**（不像陣列有固定大小）。
- 存取資料需**從頭遍歷 (O(n))**，無法直接跳到指定索引。
- 每個節點至少需要一個指標空間，因此會多一點記憶體開銷。
- 支援快速的插入與刪除操作。

**Time Complexity (一般操作)：**
| 操作 | 時間複雜度 |
|------|-------------|
| Access | O(n) |
| Search | O(n) |
| Insert at head | O(1) |
| Insert at tail | O(n) |
| Delete node | O(1) ~ O(n) |
| Traverse | O(n) |

---

## 4. Limitation
- 無法 O(1) 隨機存取資料，只能從頭節點開始走訪。
- 額外的指標空間會導致較高的記憶體使用量。
- 操作指標時容易出錯（例如遺失節點或產生記憶體洩漏）。
- Cache 效率不佳，因節點分散於不同記憶體區段。
- 相較於陣列，搜尋速度較慢。

---

## 5. Pros & Cons

| 比較項目 | Linked List | Array |
|-----------|--------------|--------|
| 記憶體配置 | 動態配置、非連續 | 固定大小、連續 |
| 插入 / 刪除 | 快速 (O(1) 若位置已知) | 慢 (O(n))，需搬移資料 |
| 存取 | 需遍歷 (O(n)) | 直接存取 (O(1)) |
| 記憶體開銷 | 需額外指標空間 | 較省 |
| 大小調整 | 可動態增減 | 固定 |
| Cache 效率 | 較差 | 較佳 |
| 實作難度 | 較高 (需管理指標) | 較低 |

---

## 6. Abstract Data Type (ADT)

```
ADT LinkedList is
  objects:
    節點序列，每個節點包含 (data, next)。
  functions:
    Create()         建立空的 linked list
    IsEmpty(L)       檢查是否為空
    Length(L)        回傳節點數
    Retrieve(L, p)   回傳第 p 個節點的資料
    Insert(L, p, x)  在位置 p 插入資料 x
    Delete(L, p)     刪除位置 p 的節點
    Update(L, p, x)  修改第 p 個節點內容
    Search(L, x)     找出資料為 x 的節點
end
```

> ADT 描述「能做什麼」而非「怎麼實作」。

---

## 7. Implementation

### (a) C語言結構定義
```c
struct Node {
    int data;
    struct Node* next;
};
```

### (b) 建立新節點
```c
Node* createNode(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    if (newNode == NULL) {
      printf("Memory allocation failed.\n");
      exit(1);
    }

    newNode->data = value;
    newNode->next = NULL;
    return newNode;
}
```

### (c) 插入節點 (Insert)
```c
void insert(Node** head, int value, int index) {
    Node* newNode = createNode(value);

    if (index == 0) {
        newNode->next = *head;
        *head = newNode;
        return;
    }

    Node* current = *head;

    for (int i = 0; current != NULL && i < index - 1; i++) {
        current = current->next;
    }

    if (current == NULL) {
        printf("Index out of range.\n");
        free(newNode);
        return;
    }

    // 插入節點
    newNode->next = current->next;
    current->next = newNode;
}

```

### (d) 刪除節點 (Delete by Value)
```c
void deleteNode(Node** head, int key) {
    Node* temp = *head;
    Node* prev = NULL;

    if (temp != NULL && temp->data == key) {
        *head = temp->next;
        free(temp);
        return;
    }

    while (temp != NULL && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == NULL) return;
    prev->next = temp->next;
    free(temp);
}
```

### (e) 遍歷 (Traversal)
```c
void traverseList(Node* head) {
    Node* current = head;
    int index = 0;
    while (current != NULL) {
        printf("Node %d: Value = %d, Address = %p, Next = %p\n",
            index, current->data, (void*)current, (void*)current->next);
        current = current->next;
    index++;
    }
}

```

---

### Linked List類型
| 類型 | 特性 | 優點 | 缺點 |
|------|------|------|------|
| Singly Linked List | 單向鏈結 | 節省記憶體 | 無法回溯 |
| Doubly Linked List | 雙向鏈結 | 可雙向遍歷 | 多一個指標空間 |
| Circular Linked List | 環狀 | 可循環使用 | 難以判斷結尾 |

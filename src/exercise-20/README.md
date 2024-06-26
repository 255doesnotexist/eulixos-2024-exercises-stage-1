# 20 - 合并两个任务队列

将两个任务队列（例如运行队列）合并在一起，这在多核处理器中尤为常见，当某个处理器的任务队列需要与另一个处理器的任务队列合并时，可以使用这一操作。

你需要实现一个函数 `merge_task_queues`，该函数用于合并两个已经排序的任务队列。每个任务队列由 `TaskNode` 结构体表示，任务队列按任务 ID (`task_id`) 从小到大排序。合并后的任务队列也需要保持有序。

任务队列的节点由以下结构体表示：

```c
typedef struct TaskNode {
    int task_id;
    struct TaskNode *next;
} TaskNode;
```

## 例子

假设我们有两个任务队列：

- 队列 A：`1 -> 3 -> 5`
- 队列 B：`2 -> 4 -> 6`

调用 `merge_task_queues(A, B)` 后，返回的新队列应该是：

合并后的队列：`1 -> 2 -> 3 -> 4 -> 5 -> 6`

## 输入

1. 一组任务 id 组成的的队列，由 `,` 分割，比如 `1,3,5`。
2. 另一组任务 id 组成的的队列，由 `,` 分割，比如 `2,4,6`。

## 输出

打印合并后的任务队列：

`Merged Queue: 1 2 3 4 5 6`

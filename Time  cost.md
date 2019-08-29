#	Time  cost
| model                |  hdfs -put (none)  |  hdfs -put (XOR-2-1-1024k)  |  hdfs -read (none)  |  hdfs -read (XOR-2-1-1024k)  | load time consumption （cpu) | predict time consumption (cpu) | load time consumption （gpu) | predict time consumption (gpu) |
| -------------------- | ---------------- | ------------------------- | ----------------- | -------------------------- | ---------------------------- | ------------------------------ | ---------------------------- | ------------------------------ |
| resnet152 (231 MB)   | 3.455 s          | 3.102 s                   | 2.947 s           | 2.820 s                    | 367.28 ms             | 348.22 ms               | 5166.73 ms              | 2218.87 ms                   |
| vgg16 (528 MB)       | 4.379 s          | 4.224 s                   | 3.907 s           | 3.380 s                    | 350.06 ms               | 636.20 ms                 | 4580.60 ms              | 229.67 ms               |
| Inception-v3 (44 MB) | 2.505 s          | 2.317 s                   | 2.432 s           | 2.383 s                    | 135.07 ms               | 93.67 ms                   | 4692.55 ms              | 23.12 ms                     |

注：gpu加载时间目前仅供参考，有些地方还有些奇怪，比如vgg16为什么比resnet152 加载时间快。

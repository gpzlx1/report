#	Time  cost
| model                |  hdfs -put (none)  |  hdfs -put (XOR-2-1-1024k)  |  hdfs -read (none)  |  hdfs -read (XOR-2-1-1024k)  | load time consumption （cpu) | predict time consumption (cpu) | load time consumption （gpu) | predict time consumption (gpu) |
| -------------------- | ---------------- | ------------------------- | ----------------- | -------------------------- | ---------------------------- | ------------------------------ | ---------------------------- | ------------------------------ |
| resnet152 (231 MB)   | 3.455 s          | 3.102 s                   | 2.947 s           | 2.820 s                    | 404.74 ms                    | 304.69 ms                      | 944.86 ms                    | 2270.42 ms                     |
| vgg16 (549 MB)       | 4.379 s          | 4.224 s                   | 3.907 s           | 3.380 s                    | 444.63 ms                    | 751.36 ms                      | 507.00 ms                    | 205.62 ms                      |
| Inception-v3 (44 MB) | 2.505 s          | 2.317 s                   | 2.432 s           | 2.383 s                    | 167.82 ms                    | 94.72 ms                       | 424.89 ms                    | 23.72 ms                       |

注：gpu加载时间目前仅供参考，有些地方还有些奇怪，比如vgg16为什么比resnet152 加载时间快。

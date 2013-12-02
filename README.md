这是一个redis zset的新功能patch。

redis中的sorted set（即zset）， 可以用于处理TOP N，有序队列等场景，还可以用于reverted index，实现搜索功能。 但是，zset只有一个score可作为weight权重指标， 在用于reverted index时，我们常常需要多个weight，或者filter参数。 比如，当score相同时，redis默认是按lexicographical排序，但我们可能需要的是其他order方式，还需要一些额外的filter。 所以这个patch给redis加了一个zset patch，实现可存储附加的score参数， 同时，相关的读取操作（zrange, zscore等）可增加更多过滤条件。

新增命令：
ZZADD key score score2 member [...]
ZZSCORE key member
ZZRANGE key start end
ZZREVRANGE key start end

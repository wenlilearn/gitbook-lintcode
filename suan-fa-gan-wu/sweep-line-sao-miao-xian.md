# Sweep Line\(扫描线\)

### 扫描线:

#### 定义: 扫描线是一种解决在某个时段内事件计数的一个算法, 具体原理很简单, 就是把某个时段拆成两个部分, 起点和终点, 然后分别标记这两个事件, 最后循环然后对这两个事件进行计数, 大概的代码如下:

```text
sweepline(intervals):
    events = []
    for interval in intervals:
        events.add([interval.start, 0])
        events.add([interval.end, 1])
    
    # sort by time then event
    events.sort()
    
    //processing events
    for event : events:
        if(event[1] == 0):
            //...do something...
        else if(event[1] == 1):
            //...do something else...
    
    return 
```


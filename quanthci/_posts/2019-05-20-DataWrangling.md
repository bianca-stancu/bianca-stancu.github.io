---
layout: post
title: "Data Wrangling"
date: 2019-05-20
---
The following blog post covers data wrangling, following the concepts presenting in [this link](https://www.youtube.com/watch?v=85tud7I8MAE&list=PLXugMGL39JWO_n-WNdppkyMuYfQBU_h_U&index=7&t=1135s). The **tidyverse** package is used.

## Steps
1. **Loading data into a tribble**: a small subsample from the previously used ereader dataset was used.

2. **Sorting**
```
arrange(time)
```

```
arrange(desc(time))
```

3. **Selecting**
* Only columns:
```
select(device,time)
```
 * Everything but a column:
```
 select(device)
```
 * Columns with conditions of name
```
select(matches('time'))
```

```
select(starts_with('l'))
```

```
select(ends_with('e'))
```

4. **Reordering**
```
select(lighting,everything())
```

 5. **Renaming**
```
select(DeviceType = device,LightingConditions = lighting, ReadingTime = time)
```

 6. **Filtering**
```
filter(device == 2)
```

```
filter(device == 1 & time>1200)
```

7. **Combining columns**
```
unite(conditions, device, lighting)
```

8. **Separating columns**
```
separate(conditions,c('device','lighting'))
```

9. **Binding columns**
```
bind_cols(data,data2)
```

10. **Binding rows**
```
bind_rows(data,data2)
```

11. **Joins**
* Inner join:
```
inner_join(data1,data2,by = c('device','lighting','participant'))
```

* Full join:
```
full_join(data1,data2,by = c('device','lighting','participant'))
```

* Left join:
```
left_join(data1,data2,by = c('device','lighting','participant'))
```
* Right join:
```
right_join(data1,data2,by = c('device','lighting','participant'))
```

12. **Set operations**
* Union:
```
union(data1,data2)
```

* Intersection:
```
intersect(data1,data2)
```

* Difference:
```
setdiff(data2,data1)
```

13. **Changing the shape**

* Spread:
```
spread(device,time)
```

* Gather:
```
gather(device,time,`1`,`2`)
```

14. **Summarizing**
```
group_by(participant)
```

```
summarize(mean_time = mean(time))
```

```
summarize(time = sum_time(time))
```

```
summarize(count=n())
```

15. **Mutating**
```
mutate(time = time/60)
```

```
mutate(order = row_number())
```

16. **Working with strings**
```
mutate(user = str_sub(participant,start = 2))
```

17. **Durations**



## Useful links
Some useful links:
* [Tidy Explain](https://github.com/gadenbuie/tidyexplain)

The full code can be viewed at [this link](https://github.com/bianca-stancu/QuantHCI2019/blob/master/data_wrangling.R).


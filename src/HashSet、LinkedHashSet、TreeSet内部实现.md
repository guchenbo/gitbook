## HashSet、LinkedHashSet、TreeSet内部实现

HashSet、LinkedHashSet、TreeSet内部分别是用HashMap、LinkedHashMap、TreeMap实现的，它们保存的元素分别是内部Map的Key。理解了这点有利于理解Set。

Set是不能重复的集合，其中HashSet和LinkedHashSet通过hashCode和equals判断是否重复

1、通过hashCode得到hash，进一步得到数组下标；

2、比较key是否相等，(key1 == key2 || key1.equals(key2))
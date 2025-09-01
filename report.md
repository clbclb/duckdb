虽然 DeepSeek 没有办法直接提供一种方法，但是也给出了实现的一些提示：根据原有的array_sort函数进行修改。

![](/pitcture//1.png)

我们按照这种方法搜索关键字 "array_sort"

![](/pitcture/2.png)

这里只用考虑上面三个文件，因为下面 test 开头的都是用来测试的，不用管。

具体修改

1.在 extension/core_functions/include/core_functions/scalar/list_functions.hpp 中添加：

```cpp
struct MyArraySortFun {
	using ALIAS = ListSortFun;

	static constexpr const char *Name = "my_array_sort";
};
```

2.在 extension/core_functions/function_list.cpp 中添加：

```
DUCKDB_SCALAR_FUNCTION_SET_ALIAS(MyArraySortFun),
```

3.在 src/include/duckdb/main/extension_entries.hpp 中添加：

```
{"my_array_sort", "core_functions", CatalogType::SCALAR_FUNCTION_ENTRY},
```

测试：

![alt text](3.png)
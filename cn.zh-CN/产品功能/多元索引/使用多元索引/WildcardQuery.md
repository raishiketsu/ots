# WildcardQuery {#concept_227248 .concept}

通配符查询中，要匹配的值可以是一个带有通配符的字符串。要匹配的值中可以用星号\("\*"\)代表任意字符序列，或者用问号\("?"\)代表任意单个字符。比如查询“table\*e”, 可以匹配到“tablestore”。

## 参数 {#section_82a_s75_kjx .section}

-   fieldName：字段名。
-   value：含有通配符的值。目前支持两种通配符：“\*”和“？”。不能以“\*”开头，且字符长度不能超过10字节。

## 示例 {#section_kr4_qaz_6od .section}

``` {#codeblock_t0i_gmf_pn2}
/**
 * 使用通配符查询，查询表中Col_Keyword这一列的值匹配"hang*u"的数据
 * @param client
 */
private static void wildcardQuery(SyncClient client) {
    SearchQuery searchQuery = new SearchQuery();
    WildcardQuery wildcardQuery = new WildcardQuery(); // 设置查询类型为WildcardQuery
    wildcardQuery.setFieldName("Col_Keyword");
    wildcardQuery.setValue("hang*u"); //wildcardQuery支持通配符
    searchQuery.setQuery(wildcardQuery);
    SearchRequest searchRequest = new SearchRequest(TABLE_NAME, INDEX_NAME, searchQuery);

    SearchRequest.ColumnsToGet columnsToGet = new SearchRequest.ColumnsToGet();
    columnsToGet.setReturnAll(true); // 设置返回所有列
    searchRequest.setColumnsToGet(columnsToGet);

    SearchResponse resp = client.search(searchRequest);

    System.out.println("TotalCount: " + resp.getTotalCount()); // 匹配到的总行数，非返回行数
    System.out.println("Row: " + resp.getRows());
}
```


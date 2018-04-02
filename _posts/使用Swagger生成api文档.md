
方法注释

```
@SWG\Post( //Post方法
	tags={"Tags"}, // 标签
	path="/filder/swagger", //路径
	
	//参数
	@SWG\Parameter(
		name="limit",
		in="query",
		description="maximum number of results to return",
		required=false,
		type="integer",
		format="int32"
	),
	@SWG\Parameter(
		name="petId",
		in="path",
		type="string"
	),
	
	//响应
	@SWG\Response(response="200", description="An test resource"),
	@SWG\Response(
		response="default",
		description="unexpected error",
	)
)
```


参数：

```
@SWG\Parameter(
	name="petId", //参数名
	in="path",    //位置
	type="string" //类型
),
```

响应：

```
@SWG\Response(
	response="200", //响应码
	description="response content", //内容
)
```
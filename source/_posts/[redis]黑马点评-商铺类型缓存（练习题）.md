---
title: '[redis]黑马点评-商铺类型缓存（练习题）'
date: 2022-10-26 21:34:57
tags: redis
cover: https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/img/redis_%E7%99%BE%E5%BA%A6%E5%9B%BE%E7%89%87%E6%90%9C%E7%B4%A2.gif
---
黑马点评P37集，给商铺类型业务添加缓存。
和上一条商户缓存不同的是，商户类型的数据是list集合类型，需要做一些改动。

ShopTypeController

~~~ java
@RestController
@RequestMapping("/shop-type")
public class ShopTypeController {
    @Resource
    private IShopTypeService typeService;

    @GetMapping("list")
    public Result queryTypeList() {
        return typeService.queryList();
    }
}

~~~

IShopTypeService

```java
public interface IShopTypeService extends IService<ShopType> {

    Result queryList();
}

```

ShopTypeServiceImpl

```java
@Service
public class ShopTypeServiceImpl extends ServiceImpl<ShopTypeMapper, ShopType> implements IShopTypeService {
    @Resource
    private StringRedisTemplate stringRedisTemplate;

    @Override
    public Result queryList() {
        String key = CACHE_TYPE_LIST;
        //从redis中查询类型缓存
        String typeJson = stringRedisTemplate.opsForValue().get(key);
        //如果缓存不为空，直接返回
        if (StrUtil.isNotBlank(typeJson)) {
            List<ShopType> shopTypeList = JSONUtil.toList(typeJson, ShopType.class);
            return Result.ok(shopTypeList);
        }
        //为空，查询
        List<ShopType> shopTypeList = query().orderByAsc("sort").list();
        //将数据库信息保存到缓存
        stringRedisTemplate.opsForValue().set(key,JSONUtil.toJsonStr(shopTypeList));
        return Result.ok(shopTypeList);
    }
}

```





![image-20221026214041517](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/img/image-20221026214041517.png)

![image-20221026214130195](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/img/image-20221026214130195.png)

可以看出缓存之后，刷新的时间变少了

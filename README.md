# MySQL数据库建表规约
- 【强制】表达是与否概念的字段，必须使用is_xxx的方式命名，数据类型是unsignedtinyint，默认值为0（1表示是，0表示否）

        * 说明：任何字段如果为非负数，必须是unsigned。
        * 正例：表达逻辑删除的字段名is_deleted，1 表示删除，0 表示未删除。
- 【强制】表名、字段名必须使用小写字母或数字，禁止出现数字开头，禁止两个下划线中间只出现数字。数据库字段名的修改代价很大，因为无法进行预发布，所以字段名称需要慎重考虑。

        * 正例：getter_admin，task_config，level3_name
        * 反例：GetterAdmin，taskConfig，level_3_name
-  【强制】表名不使用复数名词。

        *  说明：表名应该仅仅表示表里面的实体内容，不应该表示实体数量，对应于DO类名也是单数形式，符合表达习惯。
- 【强制】禁用保留字，如desc、range、match、delayed等，请参考MySQL官方保留字。
 
- 【强制】 数据库必要字段

        * 创建时间
        * 创建人
        * 修改时间
        * 修改人
        * 是否删除    
- 【强制】主键索引名为pk_字段名；唯一索引名为uk_字段名；普通索引名则为idx_字段名。

        *  说明：pk_ 即primary key；uk_ 即uniquekey；idx_ 即index的简称。
- 【强制】小数类型为decimal，禁止使用float和double。

        * 说明：float和double在存储的时候，存在精度损失的问题，很可能在值的比较时，得到不正确的结果。如果存储的数据范围超过decimal的范围，建议将数据拆成整数和小数分开存储。
- 【强制】如果存储的字符串长度几乎相等，使用char定长字符串类型。

- 【强制】varchar是可变长字符串，不预先分配存储空间，长度不要超过5000，如果存储长度大于此值，定义字段类型为text，独立出来一张表，用主键来对应，避免影响其它字段索引效率。

- 【推荐】表的命名最好是加上“业务名称_表的作用”

         * 正例：tiger_task/ tiger_reader/ mpp_config
- 【推荐】库名与应用名称尽量一致。

- 【推荐】设计表的时候需要添加注释，修改字段含义或对字段表示的状态追加时，需要及时更新字段注释。

- 【推荐】字段允许适当冗余，以提高查询性能，但必须考虑数据一致。冗余字段应遵循：

        * 不是频繁修改的字段。
        * 不是varchar超长字段，更不能是text字段。
        * 正例：商品类目名称使用频率高，字段长度短，名称基本一成不变，可在相关联的表中冗余存储类目名称，避免关联查询


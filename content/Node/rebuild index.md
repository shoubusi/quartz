rebuild index

```sql
alter index all on ‘UserProjectRights’ rebuild
EXEC sp_updatestats
```

- `alter index`：这是用于修改索引的关键字组合，表明接下来要对索引执行某种修改操作。
- `all`：指定要对表上的所有索引进行操作。如果不使用 `all`，而是指定具体的索引名称，那么就只会对那个特定的索引进行相应操作。这里因为用了 `all`，所以会针对 `UserProjectRights` 表上的每一个索引执行后续的重建动作。
- `on 'UserProjectRights'`：明确指出这些操作是针对名为 `UserProjectRights` 的表进行的。这里表名需要根据实际数据库中的表名准确填写，如果表名写错，语句将无法正确执行并会报错。
- `rebuild`：这是具体要执行的索引操作类型，即重建索引。当执行重建操作时，数据库引擎会重新创建索引结构，丢弃原有的索引页，并根据表中的数据重新生成索引数据页，从而使索引更加紧凑、高效，减少碎片等情况，以提升索引相关操作的性能。
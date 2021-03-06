solr4新特性
===========
近实时搜索:  
near-real-time(NRT)近实时搜索特性能够使应用有一个高速的在文档添加到索引中去之后在几秒内可以被搜索得到。13  

原子更新，乐观锁并发：  
原子更新允许客户端添加、更新、删除或者自增字段（field），而不需要发送整个文档，如果两个不同的用户尝试同时改变相同的文档，那么Solr通过使用乐观锁并发控制防止不兼容的更新。简言之，在提交数据更新之前，每个事务会先检查在该事务读取数据后，有没有其他事务又修改了该数据，如果其他事务有更新的话，那么正在提交的事务就会进行回滚。乐观并发控制多用于数据争用不大，冲突较少的环境中。12  

实时get：  
Solr是一个NoSQL技术，Solr的实时get特性肯定满足以NoSQL的方式允许你使用id来获取最新的文档，而不管文档是否已经提交到了索引中，它类似于key-value存储。solr4之前的版本中，在文档没有提交到Lucene索引之前是没法获取的，solr4有了这个特性之后，这样使得你可以提交过程中解耦出来去，通过id来获取文档，这种特性在你需要更新一个已经存在的文档时是非常有用的，因为在更新前你再需要commit了，因为commit是一个非常昂贵的操作，影响查询的性能。 5

事务日志，持久性写：  
当文档正发送给Solr索引时，它会写一个事务日志用于防止数据丢失，万一服务器失败了。Solr的事务日志位于client应用和额Lucene索引之间。事务日志在实时get也扮演着角色，因为他是根据id来获取的。 5  

基于zookeeper的易于分片和复制：  

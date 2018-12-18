# 常用扩展

## apcu

介绍apcu扩展之前，首先介绍下apc扩展，apc(alternative php cache)，apc的功能分为两部分 1. opcode缓存 2. 数据缓存，可以存储k/v对，类似memcache，但是apc扩展存在两个问题，1，在php5.3.* 之后的版本自带php_opcache，不再需要apc的opcode缓存功能，2，apc的3.1.14版本在php5.5版本上有严重的内存问题，被官方废弃。最新可用的apc版本为3.1.13，仅支持php 5.3.* 。所以，如果你的php版本是5.3.*之后的版本，那意味着你不再能使用apc扩展。

apcu，一个完全类似apc的php扩展，保留了数据缓存功能，去掉了opcode缓存。php api接口完全和apc相同，如果你的代码使用了apc数据缓存，在改到apcu扩展时，代码无需进行任何修改。
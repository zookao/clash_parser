基于 https://github.com/Loyalsoldier/clash-rules 项目

```
function main(config) {
  // 定义自动测速组
  const autoGroup = {
    name: "自动",
    type: "url-test",
    url: "http://www.gstatic.com/generate_204",
    interval: 300,
    tolerance: 50,
    proxies: config.proxies.map(p => p.name).filter(name => 
      name.includes('香港') || name.includes('美国') || name.includes('日本') || name.includes('台湾') || name.includes('新加坡') || name.includes('HK') || name.includes('US') || name.includes('JP') || name.includes('TW') || name.includes('SG') || name.includes('Hong Kong') || name.includes('United States') || name.includes('Japan') || name.includes('Taiwan') || name.includes('Singapore')
    )
  };

  // 将自动组插入到策略组数组开头
  config['proxy-groups'].unshift(autoGroup);
  
  return config;
}
```

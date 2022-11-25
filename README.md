```
parsers: # array
  - reg: ^.*$
    code: |
      module.exports.parse = (raw, { yaml }) => {
        const rawObj = yaml.parse(raw)
        const groups = []
        const rules = []
        return yaml.stringify({ ...rawObj, 'proxy-groups': groups, rules })
      }

    yaml:
      prepend-proxy-groups:
        - name: 全部
          type: url-test
          url: http://www.gstatic.com/generate_204
          interval: 600

        - name: 香港
          type: url-test
          url: http://www.gstatic.com/generate_204
          interval: 600

        - name: 台湾
          type: url-test
          url: http://www.gstatic.com/generate_204
          interval: 600

        - name: 日本
          type: url-test
          url: http://www.gstatic.com/generate_204
          interval: 600

        - name: 新加坡
          type: url-test
          url: http://www.gstatic.com/generate_204
          interval: 600

        - name: 美国
          type: url-test
          url: http://www.gstatic.com/generate_204
          interval: 600

        - name: 选择
          type: select
          proxies:
            - 全部
            - 香港
            - 台湾
            - 日本
            - 新加坡
            - 美国

      commands:
        - proxy-groups.全部.proxies=[]proxyNames
        #- proxy-groups.全部.proxies.0+DIRECT
        - proxy-groups.香港.proxies=[]proxyNames|香港
        - proxy-groups.台湾.proxies=[]proxyNames|台湾
        - proxy-groups.日本.proxies=[]proxyNames|日本
        - proxy-groups.新加坡.proxies=[]proxyNames|新加坡
        - proxy-groups.美国.proxies=[]proxyNames|美国
        
      prepend-rules:
        - RULE-SET,applications,DIRECT
        - DOMAIN,clash.razord.top,DIRECT
        - DOMAIN,yacd.haishan.me,DIRECT
        - RULE-SET,private,DIRECT
        - RULE-SET,reject,REJECT
        - RULE-SET,icloud,DIRECT
        - RULE-SET,apple,DIRECT
        - RULE-SET,google,DIRECT
        - RULE-SET,proxy,选择
        - RULE-SET,direct,DIRECT
        - RULE-SET,lancidr,DIRECT
        - RULE-SET,cncidr,DIRECT
        - RULE-SET,telegramcidr,选择
        - GEOIP,LAN,DIRECT
        - GEOIP,CN,DIRECT
        - MATCH,选择

      mix-rule-providers: 
        reject:
          type: http
          behavior: domain
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/reject.txt"
          path: ./ruleset/reject.yaml
          interval: 86400

        icloud:
          type: http
          behavior: domain
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/icloud.txt"
          path: ./ruleset/icloud.yaml
          interval: 86400

        apple:
          type: http
          behavior: domain
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/apple.txt"
          path: ./ruleset/apple.yaml
          interval: 86400

        google:
          type: http
          behavior: domain
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/google.txt"
          path: ./ruleset/google.yaml
          interval: 86400

        proxy:
          type: http
          behavior: domain
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/proxy.txt"
          path: ./ruleset/proxy.yaml
          interval: 86400

        direct:
          type: http
          behavior: domain
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/direct.txt"
          path: ./ruleset/direct.yaml
          interval: 86400

        private:
          type: http
          behavior: domain
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/private.txt"
          path: ./ruleset/private.yaml
          interval: 86400

        gfw:
          type: http
          behavior: domain
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/gfw.txt"
          path: ./ruleset/gfw.yaml
          interval: 86400

        greatfire:
          type: http
          behavior: domain
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/greatfire.txt"
          path: ./ruleset/greatfire.yaml
          interval: 86400

        tld-not-cn:
          type: http
          behavior: domain
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/tld-not-cn.txt"
          path: ./ruleset/tld-not-cn.yaml
          interval: 86400

        telegramcidr:
          type: http
          behavior: ipcidr
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/telegramcidr.txt"
          path: ./ruleset/telegramcidr.yaml
          interval: 86400

        cncidr:
          type: http
          behavior: ipcidr
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/cncidr.txt"
          path: ./ruleset/cncidr.yaml
          interval: 86400

        lancidr:
          type: http
          behavior: ipcidr
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/lancidr.txt"
          path: ./ruleset/lancidr.yaml
          interval: 86400

        applications:
          type: http
          behavior: classical
          url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/applications.txt"
          path: ./ruleset/applications.yaml
          interval: 86400
```

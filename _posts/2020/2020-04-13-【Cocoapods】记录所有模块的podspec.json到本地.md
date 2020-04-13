---
layout: base
permalink: /note/2020-04-13-00
title: 【Cocoapods】记录所有模块的podspec.json到本地
---

```ruby
pre_install do |installer|
    Dir.mkdir('specs') unless Dir.exist?('specs')
    installer.send('root_specs').each { |spec|
        File.open(File.join('specs', spec.name + '.podspec.json'), 'w') {
            |file|
            file.puts spec.to_pretty_json 
        }
    }
end
```
This repo shows how we can use Stated templates to pull in and merge plugins. It uses a "fake" query for plugins, but this would be replaced by a real REST query 

```json
> .open
1: FruitBasket.json
2: FruitPlugin1.json
3: FruitPlugin2.json
4: FruitPluginCollector.yaml
5: QueryForPlugins.json
Enter the number of the file to open (or type "abort" to cancel): 1
{
  "fruits": "${$import('https://raw.githubusercontent.com/geoffhendrey/plugindemo/main/example/FruitPluginCollector.yaml')}",
  "fruitBasket": "${ {'contents': fruits.collected}  }"
}
...try '.out' or 'template.output' to see evaluated template
> .out
{
  "fruits": {
    "name": "FruitCollector",
    "plugins": [
      {
        "name": "apples-n-pears",
        "collector": "extensibility:pluginDef/safeway:FruitCollector",
        "content": {
          "fruits": {
            "apples": 4,
            "pears": 3
          }
        }
      },
      {
        "name": "apples-n-oranges",
        "collector": "extensibility:pluginDef/safeway:FruitCollector",
        "content": {
          "fruits": {
            "apples": 4,
            "oranges": 9
          }
        }
      }
    ],
    "collected": {
      "apples": 8,
      "pears": 3,
      "oranges": 9
    }
  },
  "fruitBasket": {
    "contents": {
      "apples": 8,
      "pears": 3,
      "oranges": 9
    }
  }
}
```

# 目录结构

```
├───applications/
├───storage/
│   ├───cache/
│   ├───config/
│   ├───logs/
│   └───recycle/
├───system/
│   ├───assets/
│   │   ├───dist/
│   │   ├───images/
│   │   │   └───favicon.ico
│   │   └───impl.js
│   ├───controllers/
│   │   ├───ModelController.php
│   │   └───SchemaController.php
│   ├───exceptions/
│   │   └───SystemException.php
│   ├───helpers/
│   │   ├───helpers.php
│   │   ├───main.php
│   │   └───validator.php
│   ├───services/
│   │   ├───ApiService.php
│   │   ├───CacheService.php
│   │   ├───CommandService.php
│   │   ├───LogService.php
│   │   ├───ModelService.php
│   │   ├───RequestService.php
│   │   ├───ResponseService.php
│   │   ├───SessionService.php
│   │   └───WebService.php
│   ├───template/
│   │   ├───node/
│   │   │   ├───ComponentNode.php
│   │   │   ├───ComponentTokenParser.php
│   │   │   ├───PageNode.php
│   │   │   ├───PageTokenParser.php
│   │   │   ├───ScriptsNode.php
│   │   │   ├───ScriptsTokenParser.php
│   │   │   ├───StylesNode.php
│   │   │   └───StylesTokenParser.php
│   │   └───ImplTwigExtension.php
│   └───Cms.php
├───composer.json
├───implcms
├───index.php
├───readme.md
└───service.php
```